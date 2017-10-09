---
title: "aaaMove данные из таблиц Azure | Документы Microsoft"
description: "Узнайте, как toomove данных из табличного хранилища Azure, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Tooand перемещения данных из таблицы Azure, с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данных из табличного хранилища Azure. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello. 

Можно скопировать данные из любого поддерживаемого источника данных хранения tooAzure хранилище таблиц или из табличного хранилища Azure поддерживается tooany приемник данных хранилища. Список хранилищ данных, поддерживаемые действием копирования hello как источники или приемники см. в разделе hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. 

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, который перемещает данные в хранилище таблиц Azure или из него, с помощью различных инструментов и интерфейсов API.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello. 

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из таблицы хранилища Azure см. в разделе [JSON примеры](#json-examples) этой статьи. 

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure хранилище таблиц: 

## <a name="linked-service-properties"></a>Свойства связанной службы
Существует два типа связанных служб можно использовать toolink фабрикой данных Azure tooan хранилища BLOB-объектов Azure. **AzureStorage** и **AzureStorageSas**. Hello связанной службой хранилища Azure обеспечивает для фабрики данных hello с toohello глобальный доступ к службе хранилища Azure. В то время как связанные hello SAS хранилища Azure (подпись общего доступа) службы обеспечивает для фабрики данных hello с toohello ограничен или ограниченным временем доступа хранилища Azure. Других различий между этими связанными службами нет. Выберите службу hello связаны, которая соответствует вашим потребностям. Hello следующие подразделы содержат дополнительные сведения в этих двух связанных служб.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello **typeProperties** раздел для набора данных hello типа **AzureTable** имеет следующие свойства hello.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в экземпляре базы данных таблицы Azure hello, что связанная служба ссылается. |Да. При tableName указан без azureTableSourceQuery, все записи из таблицы hello не копируются toohello назначения. Если также указан azureTableSourceQuery записи из таблицы hello, удовлетворяющий hello запроса являются скопированный toohello назначения. |

### <a name="schema-by-data-factory"></a>Схема фабрики данных
Для хранилищ данных, без схемы, таких как таблицы Azure служба фабрики данных hello выводит схему hello в одном из следующих способов hello:

1. При указании hello структуру данных с помощью hello **структуры** свойство в определении набора данных hello, hello служба фабрики данных учитывает эту структуру как hello схемы. В этом случае, если строка не содержит значение столбца, ему присваивается значение NULL.
2. Если не указать hello структуру данных с помощью hello **структуры** свойство в определении набора данных hello, фабрики данных выводит схему hello, используя первую строку hello в данных hello. В этом случае если первая строка hello не содержит полную схему hello, в результате операции копирования hello пропущены некоторые столбцы.

Таким образом, для источников данных без схемы hello рекомендуется toospecify hello структуру данных с помощью hello **структуры** свойство.

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства, например имя, описание, входные и выходные таблицы, политики и т. д., доступны для всех типов действий.

Свойства доступны в разделе typeProperties hello hello действий на hello другой стороны, могут различаться для каждого типа действия. Для действия копирования они зависят от типов источников и приемников hello.

**AzureTableSource** поддерживает следующие свойства в разделе "typeProperties" hello:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса таблицы Azure. Примеры в следующем разделе hello. |Нет. При tableName указан без azureTableSourceQuery, все записи из таблицы hello не копируются toohello назначения. Если также указан azureTableSourceQuery записи из таблицы hello, удовлетворяющий hello запроса являются скопированный toohello назначения. |
| azureTableSourceIgnoreTableNotFound |Указывают ли проглотить исключение hello таблицы не существует. |TRUE<br/>FALSE |Нет |

### <a name="azuretablesourcequery-examples"></a>Примеры azureTableSourceQuery
Если столбец таблицы Azure имеет тип строки:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Если столбец таблицы Azure имеет тип даты и времени:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** поддерживает следующие свойства в разделе "typeProperties" hello:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Значение по умолчанию раздел ключа, может использоваться приемником hello. |Строковое значение. |Нет |
| azureTablePartitionKeyName |Укажите имя столбца hello, значения которых используются в качестве ключей секционирования. Если не указано, в качестве ключа секции hello используется AzureTableDefaultPartitionKeyValue. |Имя столбца. |Нет |
| azureTableRowKeyName |Укажите имя столбца hello, значение которого используются в качестве ключа строки. Если имя не указано, используйте для каждой строки идентификатор GUID. |Имя столбца. |Нет |
| azureTableInsertType |режим Hello tooinsert данные в таблицу Azure.<br/><br/>Это свойство определяет, имеют ли существующие строки в выходной диапазон hello соответствующие ключи секций и строк значениями заменить или слияние. <br/><br/>toolearn о работе этих параметров (слияния и замены) в разделе [Вставка или слияние сущности](https://msdn.microsoft.com/library/azure/hh452241.aspx) и [Вставка или замена сущности](https://msdn.microsoft.com/library/azure/hh452242.aspx) разделы. <br/><br> Этот параметр применяется на уровне строк hello, не уровне hello таблицы и ни один из параметров удаляются строки в таблице вывода hello, которые не существуют во входном файле hello. |merge (по умолчанию)<br/>replace |Нет |
| writeBatchSize |Вставляет данные в таблицу Azure hello при hello writeBatchSize или writeBatchTimeout. |Целое число (количество строк) |Нет (значение по умолчанию — 10 000). |
| writeBatchTimeout |Вставляет данные в таблицу Azure hello при hello writeBatchSize или writeBatchTimeout |Интервал времени<br/><br/>Пример: 00:20:00 (20 минут). |Нет (время ожидания по умолчанию клиент toostorage по умолчанию значение составляет 90 сек) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Сопоставьте исходный столбец tooa целевой столбец с помощью свойства JSON переводчик hello, прежде чем использовать hello целевой столбец как hello azureTablePartitionKeyName.

В следующем примере hello, исходный столбец DivisionID имеет сопоставленных toohello целевого столбца: DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
Hello DivisionID указывается в качестве ключа секции hello.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>Примеры определений JSON
Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают как toocopy tooand данных из табличного хранилища Azure и базы данных больших двоичных объектов Azure. Тем не менее, данные можно скопировать **непосредственно** из любого tooany источников hello приемников hello поддерживается. Дополнительные сведения см. в разделе hello раздел «поддерживаемые хранилищ данных и форматы» в [перемещения данных с помощью действия копирования](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>Пример: Копирование данных из таблиц Azure tooAzure больших двоичных объектов
Hello следующем образце показано:

1. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (используется для таблиц и больших двоичных объектов).
2. Входной [набор данных](data-factory-create-datasets.md) типа [AzureTable](#dataset-properties).
3. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [AzureTableSource](#activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные, принадлежащие секции по умолчанию toohello в большом двоичном объекте tooa таблиц Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба хранилища Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Фабрика данных Azure поддерживает два типа связанных служб хранилища Azure: **AzureStorage** и **AzureStorageSas**. Для hello первый, укажите строку подключения hello, содержащую ключ учетной записи hello и для hello позже у одного укажите hello Uri подписи общего доступа (SAS). Дополнительные сведения см. в разделе [Связанные службы](#linked-service-properties).  

**Входной набор данных таблицы Azure**

Образец Hello предполагается, что вы создали таблицу «MyTable» в таблице Azure.

Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

**Выходной набор данных BLOB-объекта Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Действие копирования в конвейере с источником AzureTableSource и приемником BlobSink**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**AzureTableSource** и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный с **AzureTableSourceQuery** свойство выбирает hello данные из секции по умолчанию hello toocopy каждый час.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },                
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>Пример: Копирование данных из больших двоичных объектов Azure tooAzure таблицы
Hello следующем образце показано:

1. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (используется для таблиц и больших двоичных объектов).
2. Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureTable](#dataset-properties).
4. Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [AzureTableSink](#copy-activity-properties).

Образец Hello копирует временных рядов данных из больших двоичных объектов Azure tooan таблицы Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба хранилища Azure (для таблиц и больших двоичных объектов Azure)**:

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

Фабрика данных Azure поддерживает два типа связанных служб хранилища Azure: **AzureStorage** и **AzureStorageSas**. Для hello первый, укажите строку подключения hello, содержащую ключ учетной записи hello и для hello позже у одного укажите hello Uri подписи общего доступа (SAS). Дополнительные сведения см. в разделе [Связанные службы](#linked-service-properties).

**Входной набор данных BLOB-объекта Azure**

Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1). Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello. «external»: параметр «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

**Выходной набор данных таблицы Azure**

Образец Hello копирует tooa таблицу данных, с именем «MyTable» в таблице Azure. Создание таблицы Azure с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов. Новые строки добавляются в таблицу toohello каждый час.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Действие копирования в конвейере с источником BlobSource и приемником AzureTableSink**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**AzureTableSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
          }
        },
        "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },                        
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a>Сопоставление типов для таблиц Azure
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello.

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных слишком & из таблицы Azure hello следующие [сопоставления, которые определены службой таблицы Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) используются из типа too.NET типы OData Azure таблицы и наоборот.

| Тип данных OData | Тип .NET | Сведения |
| --- | --- | --- |
| Edm.Binary |byte[] |Массив байтов, копирование too64 КБ. |
| Edm.Boolean |bool |Логическое значение. |
| Edm.DateTime |DateTime |64-битное значение времени, выраженное в формате UTC. Hello поддерживается DateTime диапазон начинается от 00:00 1 января 1601 г. нашей эры Англиканское летоисчисление, часовой пояс — UTC. диапазон Hello заканчивается 31 декабря 9999 года. |
| Edm.Double |double |64-битное значение с плавающей запятой. |
| Edm.Guid |Guid |128-битный идентификатор GUID. |
| Edm.Int32 |Int32 |32-битное целое число. |
| Edm.Int64 |Int64 |64-битное целое число. |
| Edm.String |Строка |Значение в кодировке UTF-16. Строковые значения могут иметь копии too64 КБ. |

### <a name="type-conversion-sample"></a>Пример преобразования типов
Следующий образец Hello предназначен для копирования данных из больших двоичных объектов Azure tooAzure таблицы, с помощью преобразования типов.

Предположим, что набор данных BLOB-объектов hello в формате CSV и содержит три столбца. Один из них — это столбец datetime с пользовательского формата datetime использование сокращенного французский имен для дня недели hello.

Определите набор данных BLOB-объект источника hello следующим, а также определения типов для столбцов hello.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
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
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
        },
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
Даны сопоставление типов hello too.NET тип OData таблицы Azure, можно задать hello таблицы в таблице Azure с hello следующие схемы.

**Схема таблицы Azure**

| Имя столбца | Тип |
| --- | --- |
| userid |Edm.Int64 |
| name |Edm.String |
| lastlogindate |Edm.DateTime |

После этого определите набор данных таблиц Azure hello следующим образом. Раздел «структура» toospecify hello сведения о типе не обязательно, поскольку сведения о типе hello уже задан в hello базового хранилища данных.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

В этом случае фабрики данных автоматически тип преобразования, включая hello поля даты и времени с hello пользовательского формата datetime с помощью языка и региональных параметров «fr-fr» hello при перемещении данных из большого двоичного объекта tooAzure таблицы.

> [!NOTE]
> toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Производительность и настройка
toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize, в разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md).
