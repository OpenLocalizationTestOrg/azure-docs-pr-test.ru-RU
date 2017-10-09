---
title: "AAA «создание событий пула пакетной службы Azure | Документы Microsoft»"
description: "Справочник по событию создания пула пакетной службы."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>Событие создания пула

 Это событие возникает при создании пула. содержимое Hello hello журнала будут предоставлены общие сведения о кластере hello. Обратите внимание, что если целевой размер пула hello hello больше 0 вычислительных узлов, событие начала изменения размера пула будет следовать сразу после этого события.

 Hello примере показан текст hello пула создать событие для пула, созданные с помощью свойства CloudServiceConfiguration hello.

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|Элемент|Тип|Примечания|
|-------------|----------|-----------|
|id|Строка|Идентификатор Hello hello пула.|
|displayName|Строка|Hello отображаемое имя пула hello.|
|vmSize|Строка|размер Hello hello виртуальных машин в пуле hello. Все виртуальные машины в пуле находятся hello одинакового размера. <br/><br/> Сведения о доступных размерах виртуальных машин для пулов облачных служб (пулы, созданные с помощью cloudServiceConfiguration), см. в статье [Размеры для облачных служб](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/). Пакетная служба поддерживает все размеры виртуальных машин для облачных служб, кроме `ExtraSmall`.<br/><br/> Сведения о доступных виртуальных Машин содержатся размеры для пулов, использование образов из hello Marketplace виртуальных машин (пулы, созданных с помощью virtualMachineConfiguration) [размеры виртуальных машин](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) или [размеры Виртуальные машины](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (Windows). Пакетная служба поддерживает все размеры виртуальных машин Azure, кроме `STANDARD_A0`. Для хранилища класса Premium также не поддерживаются размеры таких серий: `STANDARD_GS`, `STANDARD_DS` и `STANDARD_DSV2`.|
|[cloudServiceConfiguration](#bk_csconf)|Сложный тип|Hello конфигурацию облачной службы для пула hello.|
|[virtualMachineConfiguration](#bk_vmconf)|Сложный тип|Конфигурация виртуальной машины Hello hello в пуле.|
|[networkConfiguration](#bk_netconf)|Сложный тип|Конфигурация сети Hello hello пула.|
|resizeTimeout|Время|Здравствуйте, время ожидания для выделения вычислительных узлов toohello пула, указанных для hello последней операции изменения размера в пуле hello.  (hello начальной изменения размера, при создании пула hello счетчики как изменение размера).|
|targetDedicated|Int32|количество вычислительных узлов, которые запрашиваются для пула hello Hello.|
|enableAutoScale|Bool|Указывает, изменяется ли размер пула hello со временем.|
|enableInterNodeCommunication|Bool|Указывает, настроен ли пул hello для прямого взаимодействия между узлами.|
|isAutoPool|Bool|Указывает ли пул hello была создана с помощью механизма автоматический пул задания.|
|maxTasksPerNode|Int32|Максимальное число задач, которые могут выполняться параллельно на одном вычислительном узле в пуле hello Hello.|
|vmFillType|Строка|Определяет, каким образом hello пакетная служба распределяет задачи между вычислительными узлами в пуле hello. Допустимые значения: "Spread" (Распределение) или "Pack" (Упаковка).|

###  <a name="bk_csconf"></a> cloudServiceConfiguration

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|osFamily|Строка|Hello гостевой ОС Azure семейства toobe установленных на виртуальных машинах hello в пуле hello.<br /><br /> Возможные значения:<br /><br /> **2** — 2 семейства ОС, эквивалентный tooWindows Server 2008 R2 SP1.<br /><br /> **3** – ОС семейства 3, эквивалентное tooWindows Server 2012.<br /><br /> **4** — 4 семейства ОС, эквивалентный tooWindows Server 2012 R2.<br /><br /> Дополнительные сведения см. в статье [Выпуски гостевой ОС Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|
|targetOSVersion|Строка|версия гостевой ОС Azure Hello toobe установленных на виртуальных машинах hello в пуле hello.<br /><br /> значение по умолчанию Hello —  **\***  определяющий hello последнюю версию операционной системы для hello указанного семейства.<br /><br /> Другие допустимые значения см. в статье [Выпуски гостевой ОС Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|

###  <a name="bk_vmconf"></a> virtualMachineConfiguration

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|[imageReference](#bk_imgref)|Сложный тип|Задает сведения о платформе hello или toouse образа Marketplace.|
|nodeAgentSKUId|Строка|Здравствуйте, SKU агента узла пакетной hello, подготовлена на вычислительном узле hello.|
|[windowsConfiguration](#bk_winconf)|Сложный тип|Задает параметры операционной системы Windows на виртуальной машине hello. Это свойство не должно быть указано, если объект imageReference hello ссылается образа операционной системы Linux.|

###  <a name="bk_imgref"></a> imageReference

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|publisher|Строка|Издатель Hello hello изображения.|
|offer|Строка|предложение Hello hello изображения.|
|sku|Строка|Здравствуйте, SKU образа hello.|
|версия|Строка|Версия образа hello Hello.|

###  <a name="bk_winconf"></a> windowsConfiguration

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|enableAutomaticUpdates|Логический|Указывает, включено ли автоматическое обновление hello виртуальной машины. Если это свойство не указано, значение по умолчанию hello верно.|

###  <a name="bk_netconf"></a> networkConfiguration

|Имя элемента|Тип|Примечания|
|------------------|--------------|----------|
|subnetId|Строка|Указывает идентификатор ресурса hello hello подсети, в какой пул hello вычислительные узлы создаются.|
