---
title: "aaaAzure виртуальной машины шкалы наборов присоединенные диски с данными | Документы Microsoft"
description: "Узнайте, как toouse присоединенных дисков с данными с наборы масштабирования виртуальных машин"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Масштабируемые наборы ВМ Azure и подключенные диски данных
[Масштабируемые наборы виртуальных машин](/azure/virtual-machine-scale-sets/) Azure теперь поддерживают виртуальные машины с подключенными дисками данных. Диски данных можно определить в профиле хранилища hello для набора масштабирования, которые были созданы с управлять дисками Azure. Ранее hello только непосредственно подключенного хранилища варианты с виртуальными машинами в наборы масштабирования были диск ОС hello и временные диски.

> [!NOTE]
>  При создании наборе с подключенными дисками данных определен масштабирования, по-прежнему нужна toomount и формат hello диски из внутри toouse ВМ их (как для автономных виртуальных машинах Azure). Toodo удобный способ это toouse расширение пользовательского скрипта, которая вызывает toopartition стандартного скрипта и форматировать все диски с данными hello на виртуальной Машине.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Создание масштабируемого набора с подключенными дисками данных
Простой способ toocreate, задать шкалу с подключенными дисками — toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss создания_ команды. Следующий пример Hello создает группы ресурсов Azure и набора масштабирования виртуальных Машин 10 Ubuntu виртуальных машин, каждая из которых 2 подключенные диски данных, 50 ГБ и 100 ГБ соответственно.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Обратите внимание, что hello _vmss создания_ команды по умолчанию определенные значения конфигурации, если они не указаны. toosee hello доступные параметры, можно переопределить try:
```bash
az vmss create --help
```
Другой способ toocreate, наборе с подключенными дисками данных масштабирования является toodefine шкалу, задайте в шаблоне диспетчера ресурсов Azure, включают _dataDisks_ раздела hello _storageProfile_и развертывание hello шаблон. Hello 50 ГБ до 100 ГБ дискового приведенном выше примере должны быть определены следующим образом в hello шаблона:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
Пример завершения, готовая toodeploy шаблон набора масштабирования можно увидеть на подключенный диск, определенные здесь: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Добавление существующих шкалу tooan диск данных набора
> [!NOTE]
>  Можно присоединить только набор масштабирования tooa диски данных которого был создан с [управляемых дисков Azure](./virtual-machine-scale-sets-managed-disks.md).

Можно добавить данные диск tooa масштабирования виртуальных Машин с помощью Azure CLI _присоединить диск vmss az_ команды. Обязательно укажите логический номер устройства (LUN), который еще не используется. Следующий пример CLI Hello добавляет toolun диск 50 ГБ 3:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

Следующий пример PowerShell Hello добавляет toolun диск 50 ГБ 3:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Различные размеры виртуальной Машины имеют различные ограничения на hello количество подключенных дисков, которые они поддерживают. Проверьте hello [характеристики размер виртуальной машины](../virtual-machines/windows/sizes.md) перед добавлением нового диска.

Можно также добавить диск, добавив новый toohello входа _dataDisks_ свойство в hello _storageProfile_ шкалы задать определения и применения изменений hello. tootest, найти существующее определение набора масштабирования hello [обозревателя ресурсов Azure](https://resources.azure.com/). Выберите _изменить_ и добавьте новый диск toohello список дисков данных. Например:  Используя пример hello выше:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

Выберите _ПОМЕСТИТЬ_ tooapply hello изменяет набор tooyour масштабирования. Этот пример будет работать, если вы используете размер виртуальной машины, который поддерживает более двух подключенных дисков данных.

> [!NOTE]
> При внесении изменений tooa набора масштабирования определения, такие как добавление или удаление диска с данными, он применяет tooall вновь созданные виртуальные машины, но применяется tooexisting виртуальных машин, только если hello _upgradePolicy_ задано слишком «Automatic». Если задано слишком «Manual», необходимо toomanually применить hello новой модели tooexisting виртуальных машин. Это можно сделать на портале hello помощью hello _обновление AzureRmVmssInstance_ PowerShell команды или hello _обновление vmss az-экземпляры_ команду CLI.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Добавление данных предварительно заполненных дисков tooan существующая масштабного набора 
> При добавлении дисков tooan существующие модели набора масштабирования намеренно, hello диск будет создана пустая. Этот сценарий также включает новые экземпляры, созданные набором масштабирования hello. Это поведение связано определение scaleset hello имеет пустой диск данных. В порядок toocreate предварительно заполненных дисков с данными для модели набор существующих шкалы можно выбрать любой из следующих двух параметров:

* Копирование данных из диски с данными toohello ВМ hello экземпляр 0 hello других виртуальных машин с помощью пользовательского скрипта.
* Создайте управляемый образ с диска hello ОС, а также диск данных (с данными требуется hello) и новый scaleset с изображением hello. Таким образом, в каждой новой созданной виртуальной Машине будет иметь данных на диске, указанным в определении hello hello scaleset. Поскольку это определение ссылается tooan изображения с диска данных, который изменил данные, каждой виртуальной машины на hello scaleset автоматически запустится с этих изменений.

> Здравствуйте, toocreate способом пользовательского изображения можно найти здесь: [создать управляемый образ универсальной ВМ в Azure](/azure/virtual-machines/windows/capture-image-resource/) 

> Hello пользователь должен toocapture hello экземпляр 0 виртуальную Машину, которая имеет hello необходимых данных, а затем использовать виртуального жесткого диска для определения образа hello.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Удаление диска данных из масштабируемого набора
Вы можете удалить диск данных в масштабируемом наборе виртуальных машин, используя команду Azure CLI _az vmss disk detach_. Пример hello следующая команда удаляет диск hello, определенный в lun 2:
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
Аналогичным образом можно также удалить диск из наборе, удаляя запись из hello масштабирования _dataDisks_ свойство в hello _storageProfile_ и применения изменений hello. 

## <a name="additional-notes"></a>Дополнительные замечания
Поддержка для дисков Azure управляемых и масштаб задайте подключенные диски данных доступна в версии API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) или более поздней hello Microsoft.Compute API.

В реализации начальной hello подключенный диск поддержка набора масштабирования нельзя присоединять или отсоединять диски с данными из отдельных виртуальных машин в наборе масштабирования.

Изначально поддержка портала Azure для подключенных дисков данных в масштабируемых наборах ограничена. В зависимости от требований, которые можно использовать шаблоны Azure CLI, пакеты SDK, PowerShell и API-интерфейса REST toomanage подключенные диски.


