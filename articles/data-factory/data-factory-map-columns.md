---
title: "aaaMapping столбцов набора данных в фабрике данных Azure | Документы Microsoft"
description: "Узнайте, как столбцы toodestination столбцов источника toomap."
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>Сопоставление столбцов исходного набора данных столбцы toodestination набора данных
Сопоставление столбцов можно использовать toospecify как столбцов, указанных в «структура» из исходной таблицы карты toocolumns hello, указанный в hello «структура» таблицы приемника. Hello **columnMapping** это свойство доступно в hello **typeProperties** раздел hello действие копирования.

Сопоставление столбцов поддерживает hello следующие сценарии:

* Все столбцы в структуре набора данных источника hello являются сопоставленных tooall в структуре набора данных приемник hello.
* Подмножество столбцов hello в структуре набора данных источника hello — tooall сопоставленных столбцов в структуре набора данных приемник hello.

Hello ниже приведены условия ошибок, которые приводят к возникновению исключения.

* Меньшее число столбцов или столбцов в hello «структура» таблицы приемника указан в сопоставлении hello.
* Повторяющееся сопоставление.
* Результат запроса SQL не имеет имени столбца, который указан в сопоставлении hello.

> [!NOTE]
> Hello следующие образцы для Azure SQL и больших двоичных объектов Azure но применимо tooany хранилища данных, которое поддерживает прямоугольный наборов данных. Измените набор данных и определения связанной службы в примерах toopoint toodata в hello соответствующий источник данных.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>Пример 1 – из большого двоичного объекта Azure SQL tooAzure сопоставления столбцов
В этом образце hello входной таблицы имеет структуру, и он указывает tooa SQL таблицы в базе данных Azure SQL.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

В этом образце hello выходная таблица имеет структуру, и он указывает tooa больших двоичных объектов в службе хранилища BLOB-объектов Azure.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Привет, следуя JSON определяет операции копирования в конвейере. Сопоставление столбцов Hello из источника toocolumns в приемник (**columnMappings**) с помощью hello **переводчик** свойство.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**Процесс сопоставления столбцов:**

![Процесс сопоставления столбцов](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>Пример 2 — с SQL-запрос из большого двоичного объекта Azure SQL tooAzure сопоставления столбцов
В этом примере SQL-запрос — используется tooextract данные из Azure SQL вместо просто указания имени таблицы hello и имена столбцов hello в разделе «Структура». 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
В этом случае результаты запроса hello — первый сопоставленный toocolumns, указанный в «Структура» источника. Далее hello столбцы из источника «структура», сопоставленные toocolumns в приемник «структура» с правилами, определенными в columnMappings.  Предположим, что hello запрос возвращает 5 столбцов, двух дополнительных столбцов, чем указано в hello «Структура» источника.

**Процесс сопоставления столбцов**

![Процесс сопоставления столбцов 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>Дальнейшие действия
В статье hello учебник по использованию действии копирования: 

- [Копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
