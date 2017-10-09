---
title: "aaaManage Azure диски с hello Azure PowerShell | Документы Microsoft"
description: "Учебник - Управление дисками Azure с hello Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Управление дисками Azure с помощью PowerShell

Виртуальные машины Azure используют диски toostore hello виртуальные машины операционной системы, приложений и данных. При создании виртуальной Машины это важно toochoose размер диска и рабочей нагрузки соответствующие toohello ожидается конфигурации. В этом руководстве рассматривается развертывание дисков виртуальных машин и управление ими. Здесь содержатся сведения о:

> [!div class="checklist"]
> * дисках ОС и временных дисках;
> * Диски данных
> * дисками уровня "Стандартный" и "Премиум";
> * производительностью дисков;
> * присоединением и подготовкой дисков данных;

Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Диски Azure по умолчанию

При создании виртуальной машины Azure двух дисков являются toohello автоматически подключенных виртуальных машин. 

**Диск операционной системы** - дисков операционной системы можно изменять, но копирование too1 терабайт и узлы hello операционной системы виртуальных машин.  диск ОС Hello назначается буква *c:* по умолчанию. кэширование конфигурацию диска ОС hello диска Hello оптимизирован для работы операционной системы. диск ОС Hello **не должны** размещения приложений или данных. Для приложений и данных используйте диск данных, который описан далее в этой статье.

**Временный диск** -временные диски используют твердотельного накопителя, которая находится на hello же Azure узле hello виртуальной Машины. Временные диски обладают высокой производительностью и могут быть использованы для таких операций, как обработка временных данных. Данные, хранящиеся на временный диск удаляется, если hello виртуальной Машины, перемещенные tooa новый узел. размер Hello hello временного диска определяется hello размер виртуальной Машины. Для временных дисков по умолчанию назначается буква *d*.

### <a name="temporary-disk-sizes"></a>Размеры временных дисков

| Тип | Размер виртуальной машины | Максимальный размер временного диска (ГБ) |
|----|----|----|
| [Универсальные](sizes-general.md) | Серии A и D | 800 |
| [Оптимизированные для вычислений](sizes-compute.md) | Серия F | 800 |
| [Оптимизированные для памяти](../virtual-machines-windows-sizes-memory.md) | Серии D и G | 6144 |
| [Оптимизированные для хранилища](../virtual-machines-windows-sizes-storage.md) | Серия L | 5630 |
| [GPU](sizes-gpu.md) | Серия N | 1440 |
| [Высокопроизводительные](sizes-hpc.md) | Серии A и H | 2000 |

## <a name="azure-data-disks"></a>Диски данных Azure

Вы можете добавить дополнительные диски данных, чтобы установить приложения и хранить данные. Диски данных следует использовать в любой ситуации, где требуется надежное хранилище данных, обеспечивающее высокую скорость реагирования. Максимальная емкость каждого диска данных составляет 1 ТБ. Hello размера виртуальной машины hello определяет число дисков может быть tooa подключенных виртуальных Машин. Для каждого ядра виртуальной машины можно подключить два диска данных. 

### <a name="max-data-disks-per-vm"></a>Максимальное число дисков данных на виртуальную машину

| Тип | Размер виртуальной машины | Максимальное число дисков данных на виртуальную машину |
|----|----|----|
| [Универсальные](sizes-general.md) | Серии A и D | 32 |
| [Оптимизированные для вычислений](sizes-compute.md) | Серия F | 32 |
| [Оптимизированные для памяти](../virtual-machines-windows-sizes-memory.md) | Серии D и G | 64 |
| [Оптимизированные для хранилища](../virtual-machines-windows-sizes-storage.md) | Серия L | 64 |
| [GPU](sizes-gpu.md) | Серия N | 48 |
| [Высокопроизводительные](sizes-hpc.md) | Серии A и H | 32 |

## <a name="vm-disk-types"></a>Типы дисков виртуальной машины

В Azure предоставляются диски двух типов.

### <a name="standard-disk"></a>Диск уровня "Стандартный"

Хранилище класса Standard использует жесткие диски и обеспечивает экономичное хранилище с достаточной производительностью. Эти диски идеально подходят для экономных рабочих нагрузок разработки и тестирования.

### <a name="premium-disk"></a>Диск уровня "Премиум"

Диски уровня "Премиум" используют высокопроизводительные твердотельные накопители с низкой задержкой. Они идеально подходят для виртуальных машин, выполняющих производственную рабочую нагрузку. Хранилище уровня "Премиум" поддерживает виртуальные машины серий DS, DSv2, GS и FS. Диски Premium бывают трех типов (P10 P20, P30), размер диска hello hello определяет тип диска hello. При выборе, следующий тип toohello округляется hello значение размера диска. Например если размер hello ниже тип диска hello 128 ГБ будет P10, 129 512 P20 и более 512 P30. 

### <a name="premium-disk-performance"></a>Производительность диска уровня "Премиум"

|Тип диска хранилища уровня "Премиум" | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Размер диска (округленный в большую сторону) | 128 ГБ | 512 ГБ | 1024 ГБ (1 ТБ) |
| Количество операций ввода-вывода в секунду на диск | 500 | 2300 | 5 000 |
Пропускная способность на диск | 100 МБ/с | 150 МБ/с | 200 МБ/с |

Хотя hello над таблицей идентифицирует max IOP для дисков, более высокий уровень производительности достигается путем чередования несколько дисков данных. Для экземпляра 64 данных диски могут быть присоединены tooStandard_GS5 виртуальной Машины. Если каждый из этих дисков относится к размеру P30, можно добиться производительности до 80 000 операций ввода-вывода в секунду. Дополнительные сведения о максимальных количествах операций ввода-вывода в секунду для виртуальных машин см. в разделе [Размеры виртуальных машин Linux](./sizes.md).

## <a name="create-and-attach-disks"></a>Создание и подключение дисков

Пример hello toocomplete в этом учебнике, необходимо иметь существующую виртуальную машину. Этот [пример сценария](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) позволяет создать ее при необходимости. Если заменить прохождение учебника hello группы ресурсов hello и ВМ имен при необходимости.

Создание начальной настройки hello с [New AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig). Следующий пример Hello настраивает диск, находящийся в размер 128 гигабайт.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Создать диск данных hello hello [New AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) команды.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Get hello виртуальной машины, которые должны tooadd hello данных диска toowith hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) команды.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Добавить hello данных диска toohello конфигурация виртуальной машины с hello [AzureRmVMDataDisk добавить](/powershell/module/azurerm.compute/add-azurermvmdatadisk) команды.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Обновить hello виртуальную машину с hello [AzureRmVM обновление](/powershell/module/azurerm.compute/add-azurermvmdatadisk) команды.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Подготовка дисков данных

После диск toohello подключенных виртуальных машин, hello операционной системы должен настроить toobe toouse hello диска. Hello следующем примере показано, как toomanually Настройка hello первый диск добавлен toohello виртуальной Машины. Также можно автоматизировать этот процесс с помощью hello [расширение пользовательского скрипта](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Настройка вручную

Создайте RDP-подключение с hello виртуальной машины. Откройте PowerShell и выполните этот сценарий.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы ознакомились с дисками виртуальных машин, а именно с:

> [!div class="checklist"]
> * дисками ОС и временными дисками;
> * Диски данных
> * дисками уровня "Стандартный" и "Премиум";
> * производительностью дисков;
> * присоединением и подготовкой дисков данных;

Переместить следующий учебник toolearn toohello об автоматической конфигурации виртуальной Машины.

> [!div class="nextstepaction"]
> [Автоматизация настройки виртуальной машины](./tutorial-automate-vm-deployment.md)
