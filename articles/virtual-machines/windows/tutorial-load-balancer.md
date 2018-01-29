---
title: "Балансировка нагрузки виртуальных машин Windows в Azure | Документы Майкрософт"
description: "Сведения о создании высокодоступного безопасного приложения, выполняемого на трех виртуальных машинах Windows с использованием Azure Load Balancer."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 12/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6eee852e703d25ccc4b13401c3e4ab46d09655da
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="how-to-load-balance-windows-virtual-machines-in-azure-to-create-a-highly-available-application"></a>Балансировка нагрузки виртуальных машин Windows в Azure для создания высокодоступного приложения
Балансировка нагрузки обеспечивает более высокий уровень доступности за счет распределения входящих запросов между несколькими виртуальными машинами. В этом руководстве вы узнаете о различных компонентах балансировщика нагрузки Azure Load Balancer, распределяющего трафик и обеспечивающего высокую доступность. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создание Azure Load Balancer
> * Создание пробы работоспособности балансировщика нагрузки
> * Создание правил трафика балансировщика нагрузки
> * Использование расширения пользовательских скриптов для создания базового сайта IIS
> * Создание виртуальных машин и присоединение их к балансировщику нагрузки
> * Просмотр балансировщика нагрузки в действии
> * добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.

Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 3.6. Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`. Если вам необходимо выполнить обновление, ознакомьтесь со статьей, посвященной [установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Обзор Azure Load Balancer
Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами. Проба работоспособности позволяет отслеживать данный порт на каждой виртуальной машине и передавать трафик только в рабочую виртуальную машину.

Вы определяете интерфейсную конфигурацию IP-адресов, содержащую один или несколько общедоступных IP-адресов. Такая интерфейсная конфигурация IP-адресов предоставляет доступ к балансировщику нагрузки и приложениям через Интернет. 

Виртуальные машины подключаются к балансировщику нагрузки с помощью виртуальной сетевой карты. Для распределения трафика между виртуальными машинами внутренний пул адресов содержит IP-адреса виртуальных сетевых карт, подключенных к балансировщику нагрузки.

Чтобы управлять потоком трафика, нужно определить правила балансировщика нагрузки для определенных портов и протоколов, сопоставленных с виртуальными машинами.


## <a name="create-azure-load-balancer"></a>Создание Azure Load Balancer
Этот раздел подробно описывает, как создать и настроить каждый из компонентов балансировщика нагрузки. Прежде чем создать балансировщик нагрузки, выполните команду [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) для создания группы ресурсов. В следующем примере создается группа ресурсов с именем *myResourceGroupLoadBalancer* в расположении *EastUS*.

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Создание общедоступного IP-адреса
Для доступа к приложению через Интернет требуется общедоступный IP-адрес для балансировщика нагрузки. Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). В следующем примере создается общедоступный IP-адрес *myPublicIP* в группе ресурсов *myResourceGroupLoadBalancer*.

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Создание балансировщика нагрузки
Создание пула IP переднего плана с [New AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). В следующем примере создается пул IP переднего плана, с именем *myFrontEndPool* и присоединяет *myPublicIP* адрес: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Создайте внутренний пул адресов с помощью командлета [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Виртуальные машины присоединить этот внутренний пул в выполнении оставшихся шагов. В следующем примере создается внутренний пул адресов *myBackEndPool*.

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Теперь создайте балансировщик нагрузки с помощью командлета [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). В следующем примере создается подсистемы балансировки нагрузки с именем *myLoadBalancer* используйте пулы IP-адресов внешнего и внутреннего, созданный на предыдущем шаге:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Создание пробы работоспособности
Чтобы балансировщик нагрузки мог следить за состоянием приложения, необходимо настроить пробу работоспособности. Проба работоспособности динамически добавляет или удаляет виртуальные машины из балансировщика нагрузки на основе их ответа на проверки работоспособности. По умолчанию виртуальная машина удаляется из числа машин, на которые балансировщик распределяет нагрузку, после двух последовательных сбоев с интервалом в 15 секунд. Пробу работоспособности можно создать на основе протокола или конкретной страницы проверки работоспособности приложения. 

В следующем примере создается проба TCP. Вы также можете создать настраиваемую пробу HTTP для более детальных проверок. При использовании настраиваемой пробы HTTP нужно создать страницу проверки работоспособности, например *healthcheck.aspx*. Чтобы обеспечить работоспособность узла, проба должна возвращать ответ **HTTP 200 OK** для балансировщика нагрузки.

Чтобы создать пробу работоспособности TCP, используйте команду [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). В следующем примере создается с именем зонда работоспособности *myHealthProbe* , наблюдает за каждую виртуальную Машину на *TCP* порт *80*:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Чтобы применить проверки работоспособности, обновление подсистемы балансировки нагрузки с [AzureRmLoadBalancer набор](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Создание правила балансировщика нагрузки
Правило балансировщика нагрузки позволяет определить распределение трафика между виртуальными машинами. Вы определяете интерфейсную конфигурацию IP-адресов для входящего трафика и внутренний пул IP-адресов для приема трафика, а также требуемый порт источника и назначения. Чтобы обеспечить получение трафика только работоспособными виртуальными машинами, можно также определить используемую пробу работоспособности.

Создайте правило балансировщика нагрузки с помощью командлета [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). В следующем примере создается правило балансировки нагрузки с именем *myLoadBalancerRule* и распределяет трафик на *TCP* порт *80*:

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

Обновите подсистему балансировки нагрузки с помощью командлета [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Настройка виртуальной сети
Прежде чем развертывать виртуальные машины и тестировать балансировщик нагрузки, создайте вспомогательные ресурсы виртуальной сети. Дополнительные сведения о виртуальных сетях см. в руководстве [Управление виртуальными сетями Azure](tutorial-virtual-network.md).

### <a name="create-network-resources"></a>Создание сетевых ресурсов
Создайте виртуальную сеть с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). В следующем примере создаются виртуальная сеть *myVnet* и подсеть *mySubnet*.

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Создайте правило группы безопасности сети с помощью командлета [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), а затем группу безопасности сети с помощью [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Добавьте группу безопасности сети в подсеть с помощью командлета [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig), а затем обновите виртуальную сеть с помощью [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

В следующем примере создается правило группы безопасности сети *myNetworkSecurityGroup*, применяемое к *mySubnet*.

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

# Create the network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply the network security group to a subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update the virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

Для создания виртуальных сетевых карт используется командлет [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). В следующем примере создаются три виртуальных сетевых адаптера (по одной виртуальной сетевой карте для каждой виртуальной машины, используемой приложением). Вы можете в любое время создать дополнительные виртуальные сетевые карты и виртуальные машины и добавить их в балансировщик нагрузки:

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
Чтобы улучшить высокую доступность приложения, поместите виртуальные машины в группу доступности.

Создайте группу доступности с помощью командлета [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). В следующем примере создается группа доступности *myAvailabilitySet*.

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Укажите имя и пароль администратора для виртуальной машины с помощью командлета [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Теперь вы можете создать виртуальные машины с помощью командлета [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). В следующем примере создаются три виртуальные машины:

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

Создание и настройка трех виртуальных машин занимает несколько минут.

### <a name="install-iis-with-custom-script-extension"></a>Установка IIS с помощью расширения пользовательских сценариев
В предыдущем руководстве [Настройка виртуальной машины Windows](tutorial-automate-vm-deployment.md) вы узнали, как автоматизировать настройку виртуальной машины с помощью расширения настраиваемых сценариев для Windows. Аналогичный подход можно использовать для установки и настройки служб IIS на виртуальных машинах.

Воспользуйтесь командлетом [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension), чтобы установить расширение настраиваемых сценариев. Это расширение запускает `powershell Add-WindowsFeature Web-Server` для установки веб-сервера IIS, а затем обновляет страницу *Default.htm* для отображения имени узла виртуальной машины.

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
Получите общедоступный IP-адрес своей подсистемы балансировки нагрузки с помощью командлета [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Следующий пример позволяет получить IP-адрес для созданного ранее *myPublicIP*.

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

После этого можно ввести общедоступный IP-адрес в веб-браузер. Отображается веб-сайт, а также имя узла виртуальной машины, на которую балансировщик нагрузки направил трафик, как показано в следующем примере:

![Выполнение веб-сайта IIS](./media/tutorial-load-balancer/running-iis-website.png)

Чтобы увидеть, как балансировщик нагрузки распределяет трафик между тремя виртуальными машинами, на которых выполняется приложение, принудительно обновите веб-браузер.


## <a name="add-and-remove-vms"></a>Добавление и удаление виртуальных машин
На виртуальных машинах, выполняющих приложение, может потребоваться выполнить обслуживание, например установить обновления операционной системы. Для обработки большего объема трафика в приложении необходимо добавить дополнительные виртуальные машины. В этом разделе показано, как удалить или добавить виртуальную машину из балансировщика нагрузки.

### <a name="remove-a-vm-from-the-load-balancer"></a>Удаление виртуальной машины из балансировщика нагрузки
Получите сетевую карту с помощью командлета [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), а затем задайте для свойства *LoadBalancerBackendAddressPools* виртуальной сетевой карты значение *$null*. Наконец, обновите виртуальную сетевую карту.

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Чтобы увидеть, как балансировщик нагрузки распределяет трафик между оставшимися двумя виртуальными машинами, на которых выполняется приложение, принудительно обновите веб-браузер. Теперь можно выполнить обслуживание на виртуальной машине, например установить обновления операционной системы или перезагрузить виртуальную машину.

### <a name="add-a-vm-to-the-load-balancer"></a>Добавление виртуальной машины в балансировщик нагрузки
После выполнения обслуживания виртуальной машины, или если необходимо увеличить емкость, задайте для свойства *LoadBalancerBackendAddressPools* виртуальной сетевой карты значение *BackendAddressPool* из [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer).

Получите подсистему балансировки нагрузки:

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Дальнейшие действия

В рамках этого руководства вы создали балансировщик нагрузки и присоединили к нему виртуальные машины. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание Azure Load Balancer
> * Создание пробы работоспособности балансировщика нагрузки
> * Создание правил трафика балансировщика нагрузки
> * Использование расширения пользовательских скриптов для создания базового сайта IIS
> * Создание виртуальных машин и присоединение их к балансировщику нагрузки
> * Просмотр балансировщика нагрузки в действии
> * Добавление и удаление виртуальных машин из балансировщика нагрузки

Перейдите к следующему руководству, чтобы научиться управлять сетевым взаимодействием виртуальных машин.

> [!div class="nextstepaction"]
> [Управление виртуальными сетями Azure и виртуальными машинами Windows с помощью Azure PowerShell](./tutorial-virtual-network.md)
