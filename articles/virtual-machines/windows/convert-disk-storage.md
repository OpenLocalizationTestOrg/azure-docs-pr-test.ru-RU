---
title: "aaaConvert Azure управлять дисками из стандартных toopremium и наоборот | Документы Microsoft"
description: "Как tooconvert Azure Управление дисками из стандартных toopremium и наоборот, с помощью Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 11f35cde216e91c0599d3619682686e8eb162fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Преобразовать Azure управлять дисками из стандартных toopremium и наоборот

Для компонента "Управляемые диски" доступны два варианта хранилища: уровень [Премиум](../../storage/storage-premium-storage.md) (на базе SSD) и уровень [Стандартный](../../storage/storage-standard-storage.md) (на базе жестких дисков). Она позволяет tooeasily переключение между hello двух параметров с минимальным временем простоя, зависимости от потребностей производительности. Эта возможность недоступна для неуправляемых дисков. Но вы можете легко [преобразования дисков toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily переключение между hello двух параметров.

В этой статье показано, как управление tooconvert диски из стандартных toopremium и обратно с помощью Azure PowerShell. Если необходима tooinstall или обновить ее, см. раздел [Установка и настройка Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Перед началом работы

* требуется для преобразования Hello hello виртуальной Машины, таким образом график миграции hello дисков хранилища во время периода обслуживания существующих. 
* При использовании неуправляемого диски сначала [преобразования дисков toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch этой статье между hello двух вариантов хранения. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Преобразовать все hello управляемых дисков виртуальной машины из стандартных toopremium и наоборот

В следующем примере hello, показано, как tooswitch все hello дисков виртуальной машины из стандартных toopremium хранилища. toouse premium управляемых дисков, необходимо использовать ВМ [размер виртуальной Машины](sizes.md) с поддержкой хранилище premium. В этом примере также переключает tooa размер, который поддерживает хранилище premium.

```powershell
# Name of hello resource group that contains hello VM
$rgName = 'yourResourceGroup'

# Name of hello your virtual machine
$vmName = 'yourVM'

# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'

# Premium capable size
# Required only if converting storage from standard toopremium
$size = 'Standard_DS2_v2'
$vm = Get-AzureRmVM -Name $vmName -resourceGroupName $rgName

# Stop and deallocate hello VM before changing hello size
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Get all disks in hello resource group of hello VM
$vmDisks = Get-AzureRmDisk -ResourceGroupName $rgName 

# For disks that belong toohello selected VM, convert toopremium storage
foreach ($disk in $vmDisks)
{
    if ($disk.OwnerId -eq $vm.Id)
    {
        $diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
        Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
        -DiskName $disk.Name
    }
}

Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Преобразовать управляемого диска из стандартных toopremium и наоборот

Для рабочей нагрузки для разработки и тестирования вы можете toohave сочетание tooreduce диски standard и premium затрат. Его можно выполнить после обновления хранилища toopremium только диски hello, требующих более высокую производительность. В следующем примере hello, показано, как tooswitch одного диска виртуальной машины из стандартных toopremium хранилища и наоборот. toouse premium управляемых дисков, необходимо использовать ВМ [размер виртуальной Машины](sizes.md) с поддержкой хранилище premium. В этом примере также переключает tooa размер, который поддерживает хранилище premium.

```powershell

$diskName = 'yourDiskName'
# resource group that contains hello managed disk
$rgName = 'yourResourceGroupName'
# Choose between StandardLRS and PremiumLRS based on your scenario
$storageType = 'PremiumLRS'
# Premium capable size 
$size = 'Standard_DS2_v2'

$disk = Get-AzureRmDisk -DiskName $diskName -ResourceGroupName $rgName

# Get hello ARM resource tooget name and resource group of hello VM
$vmResource = Get-AzureRmResource -ResourceId $disk.OwnerId
$vm = Get-AzureRmVM $vmResource.ResourceGroupName -Name $vmResource.ResourceName 

# Stop and deallocate hello VM before changing hello storage type
Stop-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name -Force

# Change hello VM size tooa size that supports premium storage
# Skip this step if converting storage from premium toostandard
$vm.HardwareProfile.VmSize = $size
Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Update hello storage type
$diskUpdateConfig = New-AzureRmDiskUpdateConfig –AccountType $storageType
Update-AzureRmDisk -DiskUpdate $diskUpdateConfig -ResourceGroupName $rgName `
-DiskName $disk.Name

Start-AzureRmVM -ResourceGroupName $vm.ResourceGroupName -Name $vm.Name
```

## <a name="next-steps"></a>Дальнейшие действия

Создайте копию виртуальной машины, доступную только для чтения, с помощью [моментальных снимков](snapshot-copy-managed-disk.md).

