---
title: "aaaAttach tooa диска данных виртуальной Машины Windows в Azure с помощью PowerShell | Документы Microsoft"
description: "Как tooattach новых или существующих данных на диске tooa виртуальной Машины Windows с помощью PowerShell с помощью модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a>Присоединение tooa диска данных виртуальной Машины Windows с помощью PowerShell

В этой статье показано, как tooattach новые и существующие диски виртуальной машины tooa Windows с помощью PowerShell. Если виртуальная машина использует управляемые диски, к ней можно подключить дополнительные управляемые диски данных. Можно также присоединить tooa неуправляемые данные дисков виртуальной Машины, использующей неуправляемые дисков в учетной записи хранения.

Перед этим ознакомьтесь со следующими советами:
* размер Hello hello виртуальной машины определяет число дисков, можно присоединить. Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* toouse хранилище Premium, вам потребуется хранилище Premium включена размер виртуальной Машины как hello виртуальную машину серии DS или GS-series. Эти виртуальные машины позволяют использовать диски из учетных записей хранения Premium и Standard. Хранилище Premium доступно в определенных регионах. Дополнительные сведения см. в разделе [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="before-you-begin"></a>Перед началом работы
При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello. Запустите hello следующие tooinstall команды.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a>Добавить пустые данные tooa диска виртуальной машины

В этом примере показано, как tooadd пустые данные на диске tooan существующей виртуальной машины.

### <a name="using-managed-disks"></a>Использование управляемых дисков

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a>Использование неуправляемых дисков в учетной записи хранения

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a>Инициализация диска hello

После добавления пустого диска необходимо tooinitialize его. диск tooinitialize hello, можно войти tooa виртуальной Машине и использовать средства управления дисками. Если вы включили WinRM и сертификат на hello виртуальной Машины при ее создании, можно использовать удаленный диск hello tooinitialize PowerShell. Можно также использовать расширение пользовательского сценария. 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
Hello файл скрипта может содержать нечто похожее на этот код tooinitialize hello дисков:

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-tooa-vm"></a>Подключить существующий диск данных tooa виртуальной Машины

Можно также присоединить существующий виртуальный жесткий ДИСК как виртуальная машина tooa диска управляемых данных. 

### <a name="using-managed-disks"></a>Использование управляемых дисков

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a>Дальнейшие действия

Создайте [моментальный снимок](snapshot-copy-managed-disk.md).
