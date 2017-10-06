---
title: "aaaCreate виртуальной машины Windows с помощью PowerShell в стек Azure | Документы Microsoft"
description: "Создание виртуальной машины Windows с помощью PowerShell Azure стека."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: de063eae6f0782d8916da991f285a9de6b41def4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a>Создание виртуальной машины Windows с помощью PowerShell в стек Azure

Виртуальные машины в стек Azure обеспечивает hello гибкие возможности виртуализации без необходимости toobuy и поддерживать hello физического оборудования, который запускает задача. При использовании виртуальных машин следует понимать, что существуют некоторые различия между hello функции, доступные в Azure и Azure стека см. в toohello [рекомендации для виртуальных машин в Azure стека](azure-stack-vm-considerations.md) toolearn статьи о Эти различия. 

Сведения, с помощью PowerShell toocreate руководства виртуальной машины Windows Server 2016 в стек Azure. Можно запустить hello действия, описанные в этой статье из пакета средств разработки Azure стека hello или из внешнего клиента на основе Windows, при подключении через виртуальную частную сеть. 

## <a name="prerequisites"></a>Предварительные требования

1. Стек Azure marketplace Hello не содержит hello Windows Server 2016 изображения по умолчанию. Перед созданием виртуальной машины, убедитесь, что оператор hello Azure стека [добавляет hello Windows Server 2016 изображения toohello стека Azure marketplace](azure-stack-add-default-image.md). 
2. Стек Azure требует определенной версии toocreate модуля Azure PowerShell и управлять ресурсами hello. Используйте hello действия, описанные в [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) разделе tooinstall hello требуемой версии.
3. [Настройка среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Группы ресурсов — это логический контейнер, в какой стек Azure ресурсы развертываются и управляются. Используйте hello, следующий блок кода toocreate группу ресурсов. Мы присвоили значения для всех переменных в этом документе, можно использовать их как есть или назначить другое значение.  

```powershell
# Create variables toostore hello location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a>Создание ресурсов хранилища 

Создайте учетную запись хранения и образ Windows Server 2016 hello toostore контейнера хранилища.

```powershell
# Create variables toostore hello storage account name and hello storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container toostore hello virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a>Создание сетевых ресурсов

Создайте виртуальную сеть, подсеть и общедоступный IP-адрес. Эти ресурсы, используемые tooprovide сетевого подключения toohello виртуальной машины.  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Создайте группу безопасности сети и правило группы безопасности сети.

группы безопасности сети Hello защищает hello виртуальной машины с помощью правила входящего и исходящего трафика. Позволяет создать правило для порта 3389 tooallow входящих подключений удаленного рабочего стола и входящее правило для порта 80 tooallow входящего веб-трафика.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleRDP `
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
  -Name myNetworkSecurityGroupRuleWWW `
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
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-hello-virtual-machine"></a>Создать карту сети для виртуальной машины hello

Hello сетевой адаптер подключается подсети tooa hello виртуальных машин, группы безопасности сети и общедоступный IP-адрес.

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a>Создание виртуальной машины

Создайте конфигурацию виртуальной машины. Конфигурация Hello включает hello параметров, используемых при развертывании виртуальной машины hello, такие как образ виртуальной машины, размер, учетные данные.

```powershell
# Define a credential object toostore hello username and password for hello virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create hello virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets hello operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create hello virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-toohello-virtual-machine"></a>Подключение toohello виртуальной машины

После успешного создания виртуальной машины hello откройте виртуальной машины toohello подключения удаленного рабочего стола из пакета средств разработки hello, или из внешнего клиента на основе Windows при подключении через виртуальную частную сеть. tooremote hello виртуальную машину, созданную в предыдущем шаге hello, необходимо его общедоступный IP-адрес. Выполните следующие команды tooget hello общедоступный IP-адрес виртуальной машины hello hello. 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с виртуальной машиной hello. Замените hello IP-адрес publicIPAddress hello виртуальной машины. При появлении запроса введите hello имя пользователя и пароль, который использовался при создании виртуальной машины hello.

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-hello-virtual-machine"></a>Удалить виртуальную машину hello

Когда больше не нужен, hello используйте следующую команду, tooremove hello ресурсов группы, которая содержит hello виртуальной машины и его связанные ресурсы:

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a>Дальнейшие действия

toolearn о хранилище в стек Azure см. toohello [Обзор хранилища](azure-stack-storage-overview.md) раздела.

