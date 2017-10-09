---
title: "aaaHow tooload распределения виртуальной машины Windows Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure распределять балансировки toocreate высокой доступности и безопасного приложения в три виртуальные машины Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Как tooload сбалансировать виртуальных машинах в Azure toocreate приложение с высокой доступностью
Балансировка нагрузки обеспечивает более высокий уровень доступности за счет распределения входящих запросов между несколькими виртуальными машинами. В этом учебнике вы узнаете о hello различных компонентов подсистемы балансировки нагрузки Azure hello, распределения трафика и обеспечения высокого уровня доступности. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создание Azure Load Balancer
> * Создание пробы работоспособности балансировщика нагрузки
> * создавать правила трафика подсистемы балансировки нагрузки;
> * Использовать настраиваемое расширение скриптов hello toocreate простого узла IIS
> * Создание виртуальных машин и присоединения tooa балансировки нагрузки
> * Просмотр балансировщика нагрузки в действии
> * добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Обзор Azure Load Balancer
Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами. Отслеживает данный порт на каждой виртуальной Машине зонда работоспособности подсистемы балансировки нагрузки и только распределяет трафик tooan оперативной виртуальной Машины.

Вы определяете интерфейсную конфигурацию IP-адресов, содержащую один или несколько общедоступных IP-адресов. Эту интерфейсный IP-конфигурацию позволяет вашей toobe нагрузки балансировки и приложения доступны через Интернет hello. 

Виртуальные машины подключены tooa подсистемы балансировки нагрузки с помощью их виртуальный сетевой адаптер (NIC). toodistribute toohello трафика виртуальных машин, пул адресов серверной части содержит IP-адреса hello hello виртуальный (NIC) подключенных toohello подсистемы балансировки нагрузки.

toocontrol hello потока трафика, определить правила подсистемы балансировки нагрузки для определенных портов и протоколов, сопоставить виртуальные машины tooyour.


## <a name="create-azure-load-balancer"></a>Создание Azure Load Balancer
В этом разделе описаны создание и настройка каждого компонента балансировки нагрузки hello. Прежде чем создать балансировщик нагрузки, выполните команду [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) для создания группы ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupLoadBalancer* в hello *EastUS* расположение:

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Создание общедоступного IP-адреса
tooaccess приложения на Здравствуйте Интернет, необходимые для балансировки нагрузки hello общедоступный IP-адрес. Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Hello следующий пример создает общедоступный IP-адрес с именем *myPublicIP* в hello *myResourceGroupLoadBalancer* группа ресурсов:

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Создание балансировщика нагрузки
Создайте интерфейсный IP-адрес с помощью командлета [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Hello следующий пример создает интерфейсный IP-адрес с именем *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Создайте внутренний пул адресов с помощью командлета [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Hello следующий пример создает пул адресов серверной части с именем *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Теперь создадим hello подсистемы балансировки нагрузки с [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Hello следующий пример создает подсистемы балансировки нагрузки с именем *myLoadBalancer* с помощью hello *myPublicIP* адрес:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Создание пробы работоспособности
tooallow hello балансировки toomonitor hello состояние загрузки приложения, используйте проверки работоспособности. Проверка работоспособности Hello динамически добавляет или удаляет виртуальные машины из ротации подсистемы балансировки нагрузки hello, в зависимости от их проверки toohealth ответа. По умолчанию виртуальная машина удаляется из распределения подсистемы балансировки нагрузки hello после двух последовательных сбоев каждые 15 секунд. Пробу работоспособности можно создать на основе протокола или конкретной страницы проверки работоспособности приложения. 

Следующий пример Hello создает TCP-зонды. Вы также можете создать настраиваемую пробу HTTP для более детальных проверок. При использовании пользовательских проверку HTTP, необходимо создать страницу проверки работоспособности hello, таких как *healthcheck.aspx*. Hello пробы должен возвращать **HTTP 200 OK** ответа для узла hello tookeep подсистемы балансировки нагрузки hello в поворота.

использовать toocreate TCP-зонды работоспособности [AzureRmLoadBalancerProbeConfig добавить](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Hello следующий пример создает зонда работоспособности с именем *myHealthProbe* , отслеживает каждой виртуальной Машины:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Обновление подсистемы балансировки нагрузки hello с [AzureRmLoadBalancer набор](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Создание правила балансировщика нагрузки
Правило подсистемы балансировки нагрузки — toodefine используется как трафика является распределенной toohello виртуальных машин. Можно определить hello интерфейсный IP-конфигурацию для hello входящий трафик и hello серверной части IP пула tooreceive hello трафика, а также требуемых исходных hello и порт назначения. toomake убедиться, что только работоспособное ВМ получать трафик также определять toouse проверки работоспособности hello.

Создайте правило балансировщика нагрузки с помощью командлета [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Hello следующий пример создает правила подсистемы балансировки нагрузки с именем *myLoadBalancerRule* и распределяет трафик через порт *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

Обновление подсистемы балансировки нагрузки hello с [AzureRmLoadBalancer набор](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Настройка виртуальной сети
Перед развертыванием некоторые виртуальные машины и можно проверить балансировки, создайте hello, поддерживающие ресурсы виртуальной сети. Дополнительные сведения о виртуальных сетях см. в разделе hello [управление виртуальными сетями Azure](tutorial-virtual-network.md) учебника.

### <a name="create-network-resources"></a>Создание сетевых ресурсов
Создайте виртуальную сеть с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello следующий пример создает виртуальную сеть с именем *myVnet* с *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Создайте правило группы безопасности сети с помощью командлета [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), а затем группу безопасности сети с помощью [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Добавить подсеть toohello группы безопасности сети hello с [набор AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) и обновите hello виртуальную сеть с [AzureRmVirtualNetwork набор](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

Hello следующий пример создает правило группы сетевой безопасности с именем *myNetworkSecurityGroup* и применяет его слишком*mySubnet*:

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

Для создания виртуальных сетевых карт используется командлет [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hello следующий пример создает три виртуальных сетевых адаптеров. (Один виртуальный сетевой Адаптер для каждой виртуальной Машины, создать приложение hello следующих шагов). Можно создать в любое время дополнительных виртуальных сетевых адаптеров и виртуальные машины и добавить их toohello балансировки нагрузки:

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>Создание виртуальных машин
tooimprove hello высокий уровень доступности приложения, поместите виртуальные машины в группу доступности.

Создайте группу доступности с помощью командлета [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Hello следующий пример создает именованный набор доступности *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Набор администратору имя пользователя и пароль для виртуальных машин hello с [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Теперь можно создавать виртуальные машины hello с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Следующий пример Hello создает три виртуальные машины:

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

Он занимает несколько минут toocreate и настроить все три виртуальные машины.

### <a name="install-iis-with-custom-script-extension"></a>Установка IIS с помощью расширения пользовательских сценариев
В предыдущем учебнике на [как toocustomize виртуальной машины Windows](tutorial-automate-vm-deployment.md), вы узнали, каким образом tooautomate настройки виртуальной Машины с hello пользовательский скрипт расширения для Windows. Можно использовать hello же подходов tooinstall и настройте службы IIS на виртуальные машины.

Используйте [AzureRmVMExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello настраиваемого расширения скриптов. Здравствуйте, выполняется расширение `powershell Add-WindowsFeature Web-Server` tooinstall hello веб-сервере IIS, а затем обновления hello *Default.htm* страницы tooshow hello имя узла виртуальной Машины hello:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>Проверка балансировщика нагрузки
Получить hello общедоступный IP-адрес балансировки нагрузки, с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello следующий пример извлекает hello IP-адрес для *myPublicIP* созданную ранее:

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

После этого можно вводить hello общедоступный IP-адрес в tooa веб-браузере. отображается Hello веб-сайта, включая имя узла виртуальной Машины hello hello балансировки нагрузки, hello распределенных tooas трафика в следующий пример hello:

![Выполнение веб-сайта IIS](./media/tutorial-load-balancer/running-iis-website.png)

Подсистема балансировки нагрузки hello toosee распределять трафик между все три виртуальные машины, запускающий ваше приложение, вы может принудительно обновить веб-браузере.


## <a name="add-and-remove-vms"></a>Добавление и удаление виртуальных машин
Может потребоваться tooperform обслуживания на hello приложения, таких как установка обновления ОС работающих виртуальных машин. toodeal с приложением tooyour большего объема трафика, может потребоваться tooadd дополнительных ВМ. В этом разделе показано, как tooremove или добавить виртуальную Машину из балансировки нагрузки hello.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Удалите виртуальную Машину из балансировки нагрузки hello
Получить hello сетевой адаптер с [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), затем набор hello *пулы Loadbalancerbackendaddresspool* свойство hello виртуального сетевого Адаптера в слишком*$null*. Наконец обновите hello виртуального сетевого адаптера.:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

подсистемы балансировки нагрузки hello toosee распределять трафик между hello остальные две виртуальные машины под управлением приложения вы можно принудительно обновить веб-браузере. Теперь можно выполнить обслуживание на hello виртуальной Машины, таких как установка обновлений операционной системы или перезагрузки виртуальной Машины.

### <a name="add-a-vm-toohello-load-balancer"></a>Добавляет подсистему балансировки нагрузки виртуальной Машины toohello
После обслуживания виртуальной Машины или tooexpand емкости, задайте hello *пулы Loadbalancerbackendaddresspool* свойство hello виртуального сетевого Адаптера toohello *BackendAddressPool* из [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Получите hello балансировки нагрузки:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы создается подсистемы балансировки нагрузки и прикрепляется tooit виртуальных машин. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание Azure Load Balancer
> * Создание пробы работоспособности балансировщика нагрузки
> * создавать правила трафика подсистемы балансировки нагрузки;
> * Использовать настраиваемое расширение скриптов hello toocreate простого узла IIS
> * Создание виртуальных машин и присоединения tooa балансировки нагрузки
> * Просмотр балансировщика нагрузки в действии
> * добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.

Как переместить следующий учебник toolearn toohello toomanage сети виртуальной Машины.

> [!div class="nextstepaction"]
> [Управление виртуальными сетями Azure и виртуальными машинами Linux с помощью Azure CLI](./tutorial-virtual-network.md)
