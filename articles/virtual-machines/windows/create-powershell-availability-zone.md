---
title: "Создание зонированной виртуальной машины Windows с помощью PowerShell | Документация Майкрософт"
description: "Создание виртуальной машины Windows в зоне доступности с помощью Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 09/19/2017
ms.author: danlep
ms.custom: 
ms.openlocfilehash: ada47536dbd736386a4efc76249f4ff3a1cfd527
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="create-a-windows-virtual-machine-in-an-availability-zone-with-powershell"></a>Создание виртуальной машины Windows в зоне доступности с помощью PowerShell

В этой статье описывается использование Azure PowerShell для создания виртуальной машины Azure под управлением Windows Server 2016 в зоне доступности Azure. [Зона доступности](../../availability-zones/az-overview.md) представляет собой физически отдельную зону в регионе Azure. Зоны доступности позволяют защитить приложения и данные от маловероятных сбоев и потери всего центра обработки данных.

[!INCLUDE [availability-zones-preview-statement.md](../../../includes/availability-zones-preview-statement.md)]

Убедитесь, что установлен последний модуль Azure PowerShell. Если вам необходимо выполнить установку или обновление, см. статью [об установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="log-in-to-azure"></a>Вход в Azure

Войдите в подписку Azure с помощью команды `Login-AzureRmAccount` и следуйте инструкциям на экране.

```powershell
Login-AzureRmAccount
```

## <a name="check-vm-sku-availability"></a>Проверка доступности SKU виртуальной машины
Доступность размеров или номеров SKU виртуальных машин зависит от региона и зоны. Чтобы спланировать использование с учетом зон доступности, можно составить список доступных SKU виртуальных машин по регионам и зонам Azure. Так вы сможете выбрать нужный размер виртуальной машины и получить требуемую степень устойчивости в разных зонах. См. дополнительные сведения о разных типах и [размерах виртуальных машин](sizes.md).

Доступные номера SKU виртуальных машин можно просмотреть с помощью командлета [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku). В следующем примере перечислены доступные номера SKU виртуальных машин в регионе *eastus2*:

```powershell
Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("eastus2")};
```

Вывод команды будет примерно таким, как в следующем сокращенном примере с отображением размеров виртуальных машин, используемых в пределах разных зон доступности:

```powershell
ResourceType                Name  Location      Zones
------------                ----  --------      -----
virtualMachines  Standard_DS1_v2   eastus2  {1, 2, 3}
virtualMachines  Standard_DS2_v2   eastus2  {1, 2, 3}
[...]
virtualMachines     Standard_F1s   eastus2  {1, 2, 3}
virtualMachines     Standard_F2s   eastus2  {1, 2, 3}
[...]
virtualMachines  Standard_D2s_v3   eastus2  {1, 2, 3}
virtualMachines  Standard_D4s_v3   eastus2  {1, 2, 3}
[...]
virtualMachines   Standard_E2_v3   eastus2  {1, 2, 3}
virtualMachines   Standard_E4_v3   eastus2  {1, 2, 3}
```


## <a name="create-resource-group"></a>Создать группу ресурсов

Создайте группу ресурсов Azure с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими. В этом примере создается группа ресурсов с именем *myResourceGroup* в регионе *eastus2*. eastus2 (восточная часть США 2) — это один из регионов Azure, который поддерживает зоны доступности в предварительной версии.

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus2
```

## <a name="create-networking-resources"></a>Создание сетевых ресурсов

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Создайте виртуальную сеть, подсеть и общедоступный IP-адрес. 
Эти ресурсы используются для того, чтобы установить сетевое подключение к виртуальной машине и подключить ее к Интернету. Создайте IP-адрес в зоне доступности (*2* в этом примере). Чтобы создать виртуальную машину в зоне доступности (как показано в ниже), укажите ту же зону, которая использовалась для создания IP-адреса.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus2 `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address in an availability zone and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus2 -Zone 2 `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Создайте группу безопасности сети и правило группы безопасности сети. 
Группа безопасности сети обеспечивает защиту виртуальной машины с помощью правил для входящего и исходящего трафика. В нашем случае создается правило для входящего трафика порта 3389, которое разрешает входящие подключения к удаленному рабочему столу. Мы также создадим правило входящего трафика для порта 80, разрешающее входящий веб-трафик.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus2 `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-the-virtual-machine"></a>Создание сетевой карты для виртуальной машины 
Создайте сетевую карту для виртуальной машины с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Сетевая карта подключает виртуальную машину к подсети, группе безопасности сети и общедоступному IP-адресу.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus2 `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Создание виртуальной машины

Создайте конфигурацию виртуальной машины. Эта конфигурация содержит параметры, которые используются при развертывании виртуальной машины, в том числе образ виртуальной машины, ее размер и настройки аутентификации. В этом примере в предварительной версии зон доступности поддерживается размер *Standard_DS1_v2*. Эта конфигурация также указывает зону доступности, заданную при создании IP-адреса. При выполнении этого шага будут запрошены учетные данные. В качестве вводимых значений указываются имя пользователя и пароль для виртуальной машины.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS1_v2 -Zone 2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Создайте виртуальную машину с помощью командлета [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus2 -VM $vmConfig
```

## <a name="zone-for-ip-address-and-managed-disk"></a>Зона для IP-адреса и управляемого диска

Вы создали ресурс IP-адреса виртуальной машины в той же зоне доступности, где находится виртуальная машина. В той же зоне доступности также создается управляемый диск для виртуальной машины. Это можно проверить с помощью командлета [Get-AzureRmDisk](/powershell/module/azurerm.compute/get-azurermdisk):

```powershell
Get-AzureRmDisk -ResourceGroupName myResourceGroup
```

В выходных данных видно, что управляемый диск находится в той же зоне доступности, что и виртуальная машина:

```powershell
ResourceGroupName  : myResourceGroup
AccountType        : PremiumLRS
OwnerId            : /subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.
                     Compute/virtualMachines/myVM
ManagedBy          : /subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.
                     Compute/virtualMachines/myVM
Sku                : Microsoft.Azure.Management.Compute.Models.DiskSku
Zones              : {2}
TimeCreated        : 9/7/2017 6:57:26 PM
OsType             : Windows
CreationData       : Microsoft.Azure.Management.Compute.Models.CreationData
DiskSizeGB         : 127
EncryptionSettings :
ProvisioningState  : Succeeded
Id                 : /subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.
                     Compute/disks/myVM_OsDisk_1_bd921920bb0a4650becfc2d830000000
Name               : myVM_OsDisk_1_bd921920bb0a4650becfc2d830000000
Type               : Microsoft.Compute/disks
Location           : eastus2
Tags               : {}
```




## <a name="next-steps"></a>Дополнительная информация

В этой статье вы узнали, как создать виртуальную машину в зоне доступности. Узнайте о [регионах и доступности](regions-and-availability.md) виртуальных машин Azure.