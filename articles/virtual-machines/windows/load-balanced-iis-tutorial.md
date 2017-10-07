---
title: "aaaTutorial - построения приложение с высокой доступностью на виртуальных машинах Azure | Документы Microsoft"
description: "Узнайте, как toocreate приложении высокой доступности и безопасности через три виртуальные машины Windows с подсистемой балансировки нагрузки в Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Создание в Azure высокодоступного приложения с балансировкой нагрузки, выполняемого на виртуальных машинах Windows

В этом учебнике создается приложение с высокой доступностью, устойчивыми toomaintenance события. приложение Hello использует подсистему балансировки нагрузки, доступности и три виртуальных машинах (ВМ). Этот учебник Установка служб IIS, на то, что можно использовать этот учебник toodeploy framework другого приложения с помощью hello же компонентов высокого уровня доступности и рекомендации. 

## <a name="step-1---azure-prerequisites"></a>Шаг 1. Предварительные требования Azure

toocomplete этого учебника, убедитесь, что hello установлена последняя версия [Azure PowerShell](/powershell/azure/overview) модуля.

Во-первых войдите в tooyour подписки Azure с hello команда AzureRmAccount входа в систему и выполните hello на экране инструкциям.

```powershell
Login-AzureRmAccount
```

Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. Перед созданием другие ресурсы Azure, необходимо toocreate группу ресурсов с [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` области: 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>Шаг 2. Создание группы доступности

Виртуальные машины можно создать в логических доменах сбоя и обновления. Каждый логический домен представляет часть оборудования в hello основной центр обработки данных Azure. При создании двух и более виртуальных машин вычислительные ресурсы и ресурсы хранения распределяются по этим доменам. Это распределение позволяет сохранить доступность hello приложения, если это аппаратный компонент должен обслуживания. Группы доступности позволяют определить эти логические домены сбоя и обновления.

Создайте группу доступности с помощью командлета [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Hello следующий пример создает именованный набор доступности `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>Шаг 3. Создание балансировщика нагрузки

Приложение Azure Load Balancer распределяет трафик между набором определенных виртуальных машин с помощью правил балансировщика нагрузки. Зонда работоспособности наблюдает за данный порт на каждой виртуальной Машине и только распределяет трафик tooan оперативной виртуальной Машины.

### <a name="create-public-ip-address"></a>Создание общедоступного IP-адреса

tooaccess приложения в Интернет, hello назначить балансировщик нагрузки toohello открытый IP адрес. Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Hello следующий пример создает общедоступный IP-адрес с именем `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Создание подсистемы балансировки нагрузки

Создайте интерфейсный IP-адрес с помощью командлета [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Hello следующий пример создает интерфейсный IP-адрес с именем `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Создайте внутренний пул адресов с помощью командлета [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Hello следующий пример создает пул адресов серверной части с именем `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Теперь создадим hello подсистемы балансировки нагрузки с [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Hello следующий пример создает подсистемы балансировки нагрузки с именем `myLoadBalancer` с помощью hello `myPublicIP` адрес:

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Создание пробы работоспособности

tooallow hello балансировки toomonitor hello состояние загрузки приложения, используйте проверки работоспособности. Проверка работоспособности Hello динамически добавляет или удаляет виртуальные машины из ротации подсистемы балансировки нагрузки hello, в зависимости от их проверки toohealth ответа. По умолчанию виртуальная машина удаляется из распределения подсистемы балансировки нагрузки hello после двух последовательных сбоев каждые 15 секунд.

Создайте пробу работоспособности с помощью командлета [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Hello следующий пример создает зонда работоспособности с именем `myHealthProbe` , отслеживает каждой виртуальной Машины:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Создание правила подсистемы балансировки нагрузки

Правило подсистемы балансировки нагрузки — toodefine используется как трафика является распределенной toohello виртуальных машин.

Создайте правило балансировщика нагрузки с помощью командлета [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Hello следующий пример создает правила подсистемы балансировки нагрузки с именем `myLoadBalancerRule` и распределяет трафик через порт `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Обновление подсистемы балансировки нагрузки hello с [AzureRmLoadBalancer набор](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>Шаг 4. Настройка сети

Каждая Виртуальная машина имеет один или несколько виртуальных сетевых плат (NIC), подключить виртуальную сеть tooa. Эта виртуальная сеть обеспечивается toofilter трафика в зависимости от определенных правил доступа.

### <a name="create-virtual-network"></a>Создание виртуальной сети

Сначала настройте подсеть с помощью командлета [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Hello следующий пример создает подсеть с именем `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooyour подключения tooprovide сети виртуальных машин, создайте виртуальную сеть с [New AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello следующий пример создает виртуальную сеть с именем `myVnet` с `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>Настройка безопасности сети

[Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md) Azure управляет входящим и исходящим трафиком одной или нескольких виртуальных машин. Правила группы безопасности сети разрешают или запрещают передачу сетевого трафика на определенный порт или диапазон портов. Эти правила также могут включать префикс адреса источника, чтобы на виртуальную машину передавался только трафик от определенного источника.

tooallow веб-трафика tooreach приложения, создайте правило группы безопасности сети с [New AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Hello следующий пример создает правило группы сетевой безопасности с именем `myNetworkSecurityGroupRule`:

```powershell
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
```

Создайте группу безопасности сети с помощью командлета [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Hello следующий пример создает NSG с именем `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Добавить подсеть toohello группы безопасности сети hello с [AzureRmVirtualNetworkSubnetConfig набор](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Обновление hello виртуальную сеть с [AzureRmVirtualNetwork набор](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Создание виртуальных сетевых адаптеров

Загрузить функцию балансировки нагрузки с hello виртуальных Сетевых ресурсов, а не hello фактических виртуальных Машин. Hello виртуальный сетевой Адаптер подключенных toohello Подсистема балансировки нагрузки и затем прикрепляется tooa виртуальной Машины.

Создайте виртуальную сетевую карту с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hello следующий пример создает три виртуальных сетевых адаптеров. (Один виртуальный сетевой Адаптер для каждой виртуальной Машины, создать приложение hello следующих шагов):


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>Шаг 5. Создание виртуальных машин

С базовым компоненты на месте всех hello теперь можно создать высокодоступные виртуальные машины toorun приложения. 

Получить hello имя пользователя и пароль для учетной записи администратора hello на виртуальной машине hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Создание виртуальных машин hello с [New AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [набор AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [AzureRmVMSourceImage набор](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Добавить AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), и [новый AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Следующий пример Hello создает три виртуальные машины:

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

Он занимает несколько минут toocreate и настроить все три виртуальные машины. Hello зонда работоспособности подсистемы балансировки нагрузки автоматически определяет, когда приложение hello выполняется на каждой виртуальной Машине. После запуска приложение hello правило подсистемы балансировки нагрузки hello запускает toodistribute трафика.

### <a name="install-hello-app"></a>Установите приложение hello 

Расширения виртуальных машин Azure, используемых tooautomate задачи настройки виртуальной машины, такие как установка приложений и настройка hello операционной системы. Hello [расширение пользовательского скрипта для Windows](./../virtual-machines-windows-extensions-customscript.md) является используется toorun любой сценарий PowerShell на виртуальной машине hello. сценарий Hello могут хранится в хранилище Azure, любой доступный конечной точкой HTTP, или внедрены в конфигурации расширения пользовательского скрипта hello. При использовании hello расширение пользовательского скрипта, агент ВМ Azure hello управляет выполнением скрипта hello.

Используйте [AzureRmVMExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello настраиваемое расширение сценария. Здравствуйте, выполняется расширение `powershell Add-WindowsFeature Web-Server` веб-сервер IIS hello tooinstall:

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>Тестирование приложения

Получить hello общедоступный IP-адрес балансировки нагрузки, с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello следующий пример извлекает hello IP-адрес для `myPublicIP` созданную ранее:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Введите hello общедоступный IP-адрес в tooa веб-браузера. С помощью правила NSG hello в месте отображается веб-сайт IIS по умолчанию hello. 

![Сайт IIS по умолчанию](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>Шаг 6. Задачи управления

Может потребоваться tooperform обслуживания на hello приложения, таких как установка обновления ОС работающих виртуальных машин. toodeal с приложением tooyour большего объема трафика, может потребоваться tooadd дополнительных ВМ. В этом разделе показано, как tooremove или добавить виртуальную Машину из балансировки нагрузки hello. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Удалите виртуальную Машину из балансировки нагрузки hello

Удалите виртуальную Машину из пула адресов серверной части hello, сбросив свойство пулы Loadbalancerbackendaddresspool hello hello сетевой интерфейсной платы.

Получить hello сетевой адаптер с [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Задайте для свойства пулы Loadbalancerbackendaddresspool hello hello сетевой интерфейсной платы слишком $null:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Обновление hello сетевой адаптер:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>Добавляет подсистему балансировки нагрузки виртуальной Машины toohello

После обслуживания виртуальной Машины, или если требуется емкость tooexpand добавления hello сетевой Адаптер подсистемы балансировки нагрузки hello пула адресов серверной части toohello виртуальной Машины.

Получите hello балансировки нагрузки:

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Добавление пула адресов серверной части hello hello подсистемы балансировки нагрузки toohello сетевой интерфейсной платы:

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Обновление hello сетевой адаптер:

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Дальнейшие действия

[Примеры PowerShell для виртуальной машины Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
