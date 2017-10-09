---
title: "aaaAdd устойчивость к сбоям в действии копирования фабрики данных Azure, пропустив несовместимые строк | Документы Microsoft"
description: "Узнайте, как tooadd отказоустойчивость в действии копирования фабрики данных Azure, пропустив несовместимые строк во время копирования"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Обеспечение отказоустойчивости для действия копирования с помощью пропуска несовместимых строк

Фабрика данных Azure [действие копирования](data-factory-data-movement-activities.md) предлагает два способа toohandle несовместимые строк при копировании данных между хранилищами данных источника и приемника:

- Можно прервать и сбой копирования hello действии при несовместимые данные произошла (по умолчанию).
- Вы можете продолжить toocopy все данные hello, добавив отказоустойчивость и пропуск несовместимые данные строк. Кроме того вы можете войти hello несовместимые строк хранилища больших двоичных объектов Azure. Затем можно проверить hello журнала toolearn hello причину hello, исправить hello данные в источнике данных hello и повторите действие копирования hello.

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.
Действие копирования поддерживает три сценария для обработки несовместимых данных: обнаружение, пропуск и запись в журнал.

- **Несовместимость hello исходного типа данных и собственный тип приемника hello**

    Например: копирование данных из CSV-файла в tooa хранилища больших двоичных объектов SQL базы данных с помощью определения схемы, содержащий три **INT** столбцов типа. Здравствуйте строк файла CSV, содержащих числовые данные, такие как `123,456,789` успешно скопированы toohello приемника хранилища. Однако hello строки, которые содержат нечисловые значения, такие как `123,456,abc` определяются как несовместимые и пропускаются.

- **Несоответствие числа hello столбцы между hello источника и приемника hello**

    Например: копирование данных из CSV-файла в tooa хранилища больших двоичных объектов SQL базы данных с помощью определения схемы, который содержит шесть столбцов. Hello CSV-файла, строки, содержащие шесть столбцов будут успешно скопированы toohello приемника хранилища. Hello CSV файла строк, содержащих столбцы более или менее шести определяются как несовместимый и пропускаются.

- **Нарушения первичного ключа при написании tooa реляционной базы данных**

    Например: копирование данных из базы данных SQL tooa SQL server. Определен первичный ключ в базе данных SQL приемник hello, но такой первичный ключ определен в hello исходному серверу SQL server. Hello повторяющиеся строки, которые существуют в источнике hello не может быть скопированный toohello приемника. Действие копирования копирует только hello первая строка hello источника данных в приемник hello. Hello последующие исходные строки, содержащие hello повторяющиеся значения первичного ключа определяются как несовместимый и пропускаются.

## <a name="configuration"></a>Конфигурация
Hello следующий пример возвращает tooconfigure определение JSON, пропуск hello несовместимые строк в действии копирования:

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Включить или отключить пропуск несовместимых строк во время копирования. | Да<br/>False (по умолчанию) | Нет |
| **redirectIncompatibleRowSettings** | Группа свойств, которые могут быть указан при необходимости toolog hello несовместимые строк. | &nbsp; | Нет |
| **linkedServiceName (имя связанной службы)** | Hello связанная служба хранилища Azure toostore hello журнала, содержащей hello пропущенных строк. | Имя Hello [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) или [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) связанной службы, который ссылается toohello экземпляра хранилища, что требуется файл журнала toouse toostore hello. | Нет |
| **path** | путь Hello hello файла журнала, содержащий hello пропущен строк. | Укажите путь к хранилищу больших двоичных объектов hello нужных toouse toolog hello несовместимые данные. Если путь не предоставляется, hello службы создает контейнер. | Нет |

## <a name="monitoring"></a>Мониторинг
После завершения выполнения действия копирования hello видно hello количество пропущенных строк в hello мониторинга раздела:

![Мониторинг пропущенных несовместимых строк](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

При настройке toolog hello несовместимые строк, можно найти файл журнала hello по этому пути: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` в файле журнала hello, вы можете просмотреть hello строк, которые были пропущены и hello основной причиной несовместимости hello.

Исходные данные hello и hello соответствующая ошибка записи в файл hello. Ниже приведен пример содержимого файла журнала hello:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о действии копирования фабрики данных Azure, в разделе [перемещения данных с помощью действия копирования](data-factory-data-movement-activities.md).
