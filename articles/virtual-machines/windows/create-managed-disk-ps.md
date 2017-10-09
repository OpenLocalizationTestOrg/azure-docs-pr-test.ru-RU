---
title: "aaaCreate управляемого диска из VHD в Azure | Документы Microsoft"
description: "Создание управляемого диска из VHD, который в данный момент учетной записью хранения Azure с помощью модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Создание управляемых дисков из неуправляемых дисков в учетной записи хранения

Управляемый диск можно создать из существующего диска данных или диска ОС, который в данный момент находится в учетной записи хранения Azure. Вы также можете создавать пустой диск, который можно использовать в качестве нового диска данных для виртуальной машины. 

## <a name="before-you-begin"></a>Перед началом работы
При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello. Запустите hello следующие tooinstall команды.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Создание управляемого диска из виртуального жесткого диска в учетной записи хранения Azure

В примере hello мы создать диск из VHD как управляемого диска и назначьте его параметр toohello **диск 1 $** toouse позже. 

Hello управляемого диска будет создан в hello **Запад США** расположения в группу ресурсов с именем **myResourceGroup**. Hello диск будет называться **myDisk** и он будет создан из VHD-файл с именем **myDisk.vhd** мы ранее отправленные tooa учетной записи хранилища с именем **mystorageaccount**. Hello управляемого диска будут созданы в premium локально избыточное хранилище (LRS). StandardLRS и PremiumLRS являются только hello **- AccountType** параметры, доступные для управляемых дисках. 

1.  Задайте некоторые параметры.

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Создайте диск данных hello. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Создание пустого диска данных в качестве управляемого диска

В примере hello мы создайте пустой диск данных как управляемого диска и назначьте его параметр toohello **$dataDisk2** toouse позже. Пустой диск данных потребуется инициализировать toobe входа в toohello виртуальной Машины, с помощью diskmgmt.msc или [удаленно с помощью WinRM и сценарий](attach-disk-ps.md#initialize-the-disk), после вложенного tooa запуск виртуальной Машины.

Hello пустой диск данных будет создан в hello **Западная центральной части США** расположения в группу ресурсов с именем **myResourceGroup**. Hello диск будет называться **myEmptyDataDisk**. пустой диск Hello будут созданы в premium локально избыточное хранилище (LRS). StandardLRS и PremiumLRS являются только hello **- AccountType** параметры, доступные для управляемых дисках.

размер диска Hello в этом примере — 128 ГБ, но необходимо выбрать размер, который соответствует требованиям hello любые приложения, запущенные на виртуальной Машине.

1.  Задайте некоторые параметры.

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Создайте диск данных hello.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Дальнейшие действия   
- К имеющейся виртуальной машине можно [подключить диск данных](attach-disk-portal.md).
