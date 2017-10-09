---
title: "aaaCustomize виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Узнайте, как toouse hello расширение пользовательского скрипта и хранилище ключей toocustomize виртуальные машины Windows в Azure"
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
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a>Как toocustomize виртуальной машине в Azure
Обычно требуется tooconfigure виртуальных машин (ВМ) в виде краткое и согласованное, средства автоматизации. Общие toocustomize подход ВМ Windows — toouse [пользовательский скрипт расширения для Windows](extensions-customscript.md). Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * Использовать настраиваемое расширение скриптов hello tooinstall IIS
> * Создание виртуальной Машины, которая использует hello настраиваемое расширение скриптов
> * Просмотр выполняющегося сайт IIS после применения расширения hello

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).


## <a name="custom-script-extension-overview"></a>Общие сведения о расширении настраиваемых сценариев
Hello настраиваемое расширение скриптов загружает и запускает сценарии на виртуальных машинах Azure. Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления. Скрипты можно загружается из хранилища Azure или GitHub, или предоставить toohello портал Azure во время выполнения модуля.

Hello расширение пользовательского скрипта интегрируется с шаблоны Azure Resource Manager и также можно выполнить с помощью hello Azure CLI, PowerShell, портал Azure или hello API REST Azure виртуальной машины.

Hello настраиваемое расширение скриптов можно использовать с Windows и виртуальных машин Linux.


## <a name="create-virtual-machine"></a>Создание виртуальной машины
Прежде чем создать виртуальную машину, выполните команду [az group create](/powershell/module/azurerm.resources/new-azurermresourcegroup) для создания группы ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupAutomate* в hello *EastUS* расположение:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

Набор администратору имя пользователя и пароль для виртуальных машин hello с [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Теперь можно создавать hello виртуальной Машины с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hello следующий пример создает компоненты hello необходимые виртуальной сети, конфигурации hello ОС и затем создает Виртуальную машину с именем *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

Он занимает несколько минут для ресурсов hello и toobe виртуальная машина создана.


## <a name="automate-iis-install"></a>Автоматизация установки IIS
Используйте [AzureRmVMExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello настраиваемого расширения скриптов. Здравствуйте, выполняется расширение `powershell Add-WindowsFeature Web-Server` tooinstall hello веб-сервере IIS, а затем обновления hello *Default.htm* страницы tooshow hello имя узла виртуальной Машины hello:

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a>Проверка веб-сайта
Получить hello общедоступный IP-адрес балансировки нагрузки, с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello следующий пример извлекает hello IP-адрес для *myPublicIP* созданную ранее:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

После этого можно вводить hello общедоступный IP-адрес в tooa веб-браузере. отображается Hello веб-сайта, включая имя узла виртуальной Машины hello hello балансировки нагрузки, hello распределенных tooas трафика в следующий пример hello:

![Выполнение веб-сайта IIS](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике автоматической hello, службы IIS устанавливаются на виртуальной Машине. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Использовать настраиваемое расширение скриптов hello tooinstall IIS
> * Создание виртуальной Машины, которая использует hello настраиваемое расширение скриптов
> * Просмотр выполняющегося сайт IIS после применения расширения hello

Как переместить следующий учебник toolearn toohello toocreate пользовательских образов виртуальной Машины.

> [!div class="nextstepaction"]
> [Создание образа настраиваемой виртуальной машины](./tutorial-custom-images.md)
