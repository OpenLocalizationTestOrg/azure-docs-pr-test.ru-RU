---
title: "aaaMigrate tooan классических виртуальных Машин ARM управляемого диска ВМ | Документы Microsoft"
description: "Миграция одной виртуальной Машины Azure из классического развертывания hello модели tooManaged дисков в модели развертывания диспетчера ресурсов hello."
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Вручную перенести tooa классической виртуальной Машины новая ARM управляемого диска ВМ из hello виртуального жесткого диска 


Этот раздел поможет вам toomigrate существующих виртуальных машин Azure из hello классической модели развертывания слишком[управляемых дисков](managed-disks-overview.md) в модели развертывания диспетчера ресурсов hello.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>План миграции hello tooManaged дисков

Этот раздел поможет вам toomake hello наилучшее решение в типах виртуальной Машины и диска.


### <a name="location"></a>Расположение

Выберите расположение, в котором доступны Управляемые диски Azure. При переносе дисков управляемых tooPremium Убедитесь также, хранилище Premium доступно в регионе hello, где вы планируете toomigrate для. Актуальные сведения о поддерживаемых расположениях см. на странице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/#services).

### <a name="vm-sizes"></a>Размеры виртуальной машины

При переносе дисков управляемых tooPremium у вас tooupdate hello размер ВМ hello tooPremium хранилища поддерживает размер доступной в hello регион, где находится виртуальная машина. Просмотрите hello размеры виртуальных Машин, поддерживают хранилище класса Premium. Hello спецификаций размера виртуальной Машины Azure, перечислены в [размеры виртуальных машин](sizes.md).
Проверьте характеристики производительности hello виртуальные машины, работающие с хранилищем Premium и выберите размер виртуальной Машины наиболее подходящий hello, который лучше всего подходит для рабочей нагрузки. Убедитесь, что недоступна достаточную пропускную способность трафика диска виртуальной Машины toodrive hello.

### <a name="disk-sizes"></a>Размеры диска

**Управляемые диски уровня "Премиум"**

Существует семь типов управляемых дисков уровня "Премиум", которые можно использовать с виртуальной машиной. Для каждого из них действуют определенные ограничения на пропускную способность и число операций ввода-вывода в секунду. Учитывайте следующие ограничения при выборе hello Premium тип диска для виртуальной Машины на основе hello потребностей вашего приложения с точки зрения производительности, производительность, масштабируемость и пиковых нагрузок.

| Диски уровня "Премиум"  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Размер диска           | 128 ГБ| 512 ГБ| 128 ГБ| 512 ГБ            | 1024 ГБ (1 ТБ)    | 2048 ГБ (2 ТБ)    | 4095 ГБ (4 ТБ)    | 
| Количество операций ввода-вывода в секунду на диск       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Пропускная способность на диск | 25 МБ в секунду  | 50 МБ в секунду  | 100 МБ в секунду | 150 МБ в секунду | 200 МБ в секунду | 250 МБ в секунду | 250 МБ в секунду | 

**Управляемые диски уровня "Стандартный"**

Существует семь типов управляемых дисков уровня "Стандартный", которые можно использовать с виртуальной машиной. У них разная емкость, но одинаковые ограничения пропускной способности и числа операций ввода-вывода в секунду. Выберите тип hello Стандартная управляемых дисков, в зависимости от потребностей в емкости hello приложения.

| Диски уровня "Стандартный"  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Размер диска           | 30 ГБ            | 64 ГБ            | 128 ГБ           | 512 ГБ           | 1024 ГБ (1 ТБ)   | 2048 ГБ (2 ТБ)    | 4095 ГБ (4 ТБ)   | 
| Количество операций ввода-вывода в секунду на диск       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Пропускная способность на диск | 60 МБ в секунду | 60 МБ в секунду | 60 МБ в секунду | 60 МБ в секунду | 60 МБ в секунду | 60 МБ в секунду | 60 МБ в секунду | 


### <a name="disk-caching-policy"></a>Политика кэширования дисков 

**Управляемые диски уровня "Премиум"**

По умолчанию политика кэширования диска — *только для чтения* для всех hello Premium дисков с данными и *чтения и записи* для диска операционной системы Premium hello присоединенного toohello виртуальной Машины. Этот параметр конфигурации рекомендуется tooachieve hello оптимальную производительность операций ввода-вывода приложения. Отключите кэширование дисков данных, которые отличаются высокой интенсивностью записи или используются только для записи (например, файлов журналов SQL Server), чтобы улучшить производительность приложения.

### <a name="pricing"></a>Цены

Просмотрите hello [цены для дисков, управляемых](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Цены управляемых дисков "премиум" совпадает с неуправляемой дисков "премиум" hello. При этом цены на управляемые диски уровня "Стандартный" отличаются от цен на неуправляемые диски уровня "Стандартный".


## <a name="checklist"></a>Контрольный список

1.  При переносе дисков управляемых tooPremium убедитесь, что он доступен в области hello, которую вы переносите.

2.  Решите, Серия виртуальных Машин новый hello, который будет использоваться. При переносе дисков управляемых tooPremium следует возможность хранения уровня Premium.

3.  Определите hello точный размер виртуальной Машины используется которой доступны в области hello, которую вы переносите. Размер виртуальной Машины должен toobe достаточно большой toosupport hello количество дисков данных вами. Например при наличии четырех дисков данных hello виртуальной Машины должен иметь не менее двух ядер. Кроме того, учитывайте требования к вычислительной мощности, памяти и пропускной способности сети.

4.  Иметь hello текущей виртуальной Машины сведений под рукой, включая hello список дисков и соответствующих больших двоичных объектов VHD.

Подготовьте приложение к простою. toodo очистить миграции у вас toostop вся обработка hello в текущей системе hello. Только после этого можно получить его состояние tooconsistent, который можно перенести toohello новой платформы. Длительность времени простоя зависит от hello объем данных в toomigrate диски hello.


## <a name="migrate-hello-vm"></a>Перенос hello виртуальной Машины

Подготовьте приложение к простою. toodo очистить миграции у вас toostop вся обработка hello в текущей системе hello. Только после этого можно получить его состояние tooconsistent, который можно перенести toohello новой платформы. Длительность времени простоя зависит от hello объем данных в toomigrate диски hello.


1.  Во-первых можно задать общие параметры hello:

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Создание управляемого диска операционной системы с помощью hello виртуального жесткого диска из hello классической виртуальной Машины.

    Обеспечьте предоставляемых hello завершения URI hello параметр toohello $osVhdUri виртуального жесткого диска операционной системы. Также для параметра **-AccountType** укажите значение **PremiumLRS** или **StandardLRS**, в зависимости от типа дисков ("Премиум" или "Стандартный"), на которые выполняется миграция.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Присоединить диск toohello hello ОС новой виртуальной Машины.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Создать диск управляемые данные из файла виртуального жесткого диска данных hello и добавьте его toohello новой виртуальной Машины.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Создание hello новую виртуальную Машину, установив открытый IP-адрес, виртуальной сети и сетевой адаптер.

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Может быть toosupport необходимые дополнительные действия приложения, не будут рассмотрены в данном руководстве.
>
>

## <a name="next-steps"></a>Дальнейшие действия

- Подключение toohello виртуальной машины. Инструкции см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

