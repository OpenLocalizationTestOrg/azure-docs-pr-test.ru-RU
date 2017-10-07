---
title: "aaaMove данных из базы данных Azure Cosmos | Документы Microsoft"
description: "Узнайте, как переместить данные в коллекцию Azure Cosmos DB и из нее с помощью фабрики данных Azure"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Tooand перемещения данных из базы данных Azure Cosmos, с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в данных toomove фабрики данных Azure из DB Cosmos Azure (DocumentDB API). Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello. 

Можно скопировать данные из любого поддерживаемого источника данных хранения Cosmos DB tooAzure или из Azure Cosmos DB tooany поддерживается приемник данных хранилища. Список хранилищ данных, поддерживаемые действием копирования hello как источники или приемники см. в разделе hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. 

> [!IMPORTANT]
> Соединитель Azure Cosmos DB поддерживает только API DocumentDB.

toocopy данные в виде-— см. в/из JSON-файлов или другой коллекции Cosmos DB [документов JSON импорта и экспорта](#importexport-json-documents).

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из хранилища Azure Cosmos DB или обратно, с помощью различных инструментов и API-интерфейсов.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello. 

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из БД Cosmos. в разделе [JSON примеры](#json-examples) этой статьи. 

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooCosmos DB: 

## <a name="linked-service-properties"></a>Свойства связанной службы
Привет, в следующей таблице приводится описание tooAzure определенные элементы JSON DB Cosmos связанной службы.

| **Свойство** | **Описание** | **Обязательный** |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **DocumentDb** |Да |
| connectionString |Укажите сведения, необходимые tooconnect tooAzure Cosmos DB, базы данных. |Да |

Пример:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных можно найти toohello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных hello типа **DocumentDbCollection** имеет следующие свойства hello.

| **Свойство** | **Описание** | **Обязательный** |
| --- | --- | --- |
| collectionName |Имя коллекции документов Cosmos DB hello. |Да |

Пример:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Схема фабрики данных
Для хранилищ данных, без схемы, таких как Azure Cosmos DB служба фабрики данных hello выводит схему hello в одном из следующих способов hello:  

1. При указании hello структуру данных с помощью hello **структуры** свойство в определении набора данных hello, hello служба фабрики данных учитывает эту структуру как hello схемы. В этом случае, если строка не содержит значение столбца, ему будет присвоено значение NULL.
2. Если не указать hello структуру данных с помощью hello **структуры** свойство в определении набора данных hello, hello служба фабрики данных выводит схему hello, используя первую строку hello в данных hello. В этом случае если первая строка hello не содержит полную схему hello, некоторые столбцы будет отсутствовать в результате hello операции копирования.

Таким образом, для источников данных без схемы hello рекомендуется toospecify hello структуру данных с помощью hello **структуры** свойство.

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий можно найти toohello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

> [!NOTE]
> Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.

Свойства доступны в разделе typeProperties hello hello действий на hello различные другой стороны, для каждого типа действия и в случае действия копирования, они различаются в зависимости от типа hello источники и приемники.

В случае действия копирования, когда источник типа **DocumentDbCollectionSource** hello следующие свойства доступны в **typeProperties** раздела:

| **Свойство** | **Описание** | **Допустимые значения** | **Обязательный** |
| --- | --- | --- | --- |
| query |Укажите данные tooread hello запроса. |Строка запроса, поддерживаемая Azure Cosmos DB. <br/><br/>Пример: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Нет <br/><br/>Если не указан, hello выполняемой инструкции SQL:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Вложенные tooindicate специальный символ, который hello документа |Любой символ. <br/><br/>Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры. Фабрика данных Azure позволяет пользовательская иерархия toodenote через nestingSeparator, который является «.» в hello выше примерах. Разделитель hello hello действие копирования будет создавать объект «Name» hello с тремя дочерние элементы первой, средней и Last, соответствующим too"Name.First», «Name.Middle» и «Name.Last» в hello определение таблицы. |Нет |

**DocumentDbCollectionSink** поддерживает hello следующие свойства:

| **Свойство** | **Описание** | **Допустимые значения** | **Обязательный** |
| --- | --- | --- | --- |
| nestingSeparator |Требуется специальный символ в tooindicate имя столбца источника hello вложенном документе. <br/><br/>Пример выше: `Name.First` в выходных данных hello таблицы выводятся hello следующая структура JSON в документе Cosmos DB hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Символ, используемые tooseparate уровней вложения.<br/><br/>Значение по умолчанию — `.` (точка). |Символ, используемые tooseparate уровней вложения. <br/><br/>Значение по умолчанию — `.` (точка). |
| writeBatchSize |Число используемых параллельных запросов документов toocreate tooAzure Cosmos DB службы.<br/><br/>Можно оптимизировать производительность hello, при копировании данных из базы данных Cosmos при помощи этого свойства. При увеличении writeBatchSize, так как несколько параллельных запросов tooCosmos DB отправляются можно ожидать более высокую производительность. Тем не менее необходимо tooavoid регулирования, может вызывать ошибки приветственное сообщение: «частота велик» запроса.<br/><br/>Регулирование может произойти по ряду причин, включая размер документов, количество терминов в документах, политику индексации целевой коллекции и т. д. Для операций копирования, можно использовать доступной пропускной способностью большинство лучше hello toohave коллекции (например S3) (2 500 запрос единицы в секунду). |Целое число  |Нет (значение по умолчанию — 5) |
| writeBatchTimeout |Время ожидания для операции toocomplete hello до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |

## <a name="importexport-json-documents"></a>Документы JSON для импорта и экспорта
С помощью этого соединителя Cosmos DB можно выполнять следующие задачи:

* импортировать документы JSON из различных источников в Cosmos DB, включая хранилище BLOB-объектов Azure, Azure Data Lake, локальную файловую систему или другие файловые хранилища, поддерживаемые фабрикой данных Azure;
* экспортировать документы JSON из коллекции Cosmos DB в различные файловые хранилища;
* переносить данные между коллекциями Cosmos DB "как есть".

tooachieve скопировать такие независимо от схемы, 
* При использовании мастера копирования, проверьте hello **«экспортировать как-файлы tooJSON или Cosmos DB коллекции «** параметр.
* Когда редактирования JSON, не указывают раздел «структура» hello в наборах данных Cosmos DB ни свойство «nestingSeparator» на Cosmos DB источника и приемника в действии копирования. tooimport из / tooJSON файлы экспорта в наборе hello файла хранилища данных укажите тип формата как «JsonFormat», конфигурации «filePattern» и пропустить hello настроек формата rest, см. [формат JSON](data-factory-supported-file-and-compression-formats.md#json-format) раздела подробно.

## <a name="json-examples"></a>Примеры определений JSON
Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают как toocopy tooand данных из базы данных Cosmos Azure и хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** из любого tooany источников hello приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Пример: Копирование данных из tooAzure Azure Cosmos DB BLOB-объект
Hello ниже приведен пример:

1. Связанная служба типа [DocumentDb](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [DocumentDbCollection](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [DocumentDbCollectionSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирования данных в Azure Cosmos DB tooAzure больших двоичных объектов. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба Azure Cosmos DB**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Связанная служба хранилища BLOB-объектов Azure**

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
**Входной набор данных Azure Document DB**

Образец Hello предполагается, что имеется коллекция с именем **лицо** в базе данных Azure Cosmos DB.

Параметр «external»: «true», и указание externalData сведения о политике hello фабрики данных Azure службы этой таблицы hello является внешней toohello фабрики данных и не полученные в результате действия в фабрике данных hello.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Выходной набор данных BLOB-объекта Azure**

Данные — новый большой двоичный объект скопированный tooa каждый час с hello путь для большого двоичного объекта hello отражения hello определенной даты и времени с гранулярностью час.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Пример документа JSON в коллекции пользователя в базе данных Cosmos DB hello:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Служба Cosmos DB поддерживает выполнение запросов к документам, используя для обработки иерархических JSON-документов синтаксис наподобие SQL.

Пример: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

следующие Hello конвейера копирует данные из hello коллекции человека в hello tooan базы данных Azure Cosmos DB BLOB-объектов Azure. Как часть hello действия копирования hello указаны входные и выходные наборы данных.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Пример: Копирование данных из больших двоичных объектов Azure tooAzure Cosmos DB 
Hello ниже приведен пример:

1. Связанная служба типа [DocumentDb](#azure-documentdb-linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

Образец Hello копирует данные из BLOB-объектов Azure tooAzure Cosmos DB. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба хранилища BLOB-объектов Azure**

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
**Связанная служба Azure Cosmos DB**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Входной набор данных BLOB-объекта Azure**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Выходной набор данных Azure Cosmos DB**

Образец Hello копирует tooa сбора данных, с именем «Person».

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
следующие Hello конвейера копирует данные из BLOB-объектов Azure toohello коллекции человека в hello Cosmos DB. Как часть hello действия копирования hello указаны входные и выходные наборы данных.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Если входные данные большого двоичного объекта образец hello как

```
1,John,,Doe
```
Затем hello выходных данных JSON в Cosmos DB будет как:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры. Фабрика данных Azure позволяет пользовательская иерархия toodenote через **nestingSeparator**, который является «.» которым в этом примере является точка. Разделитель hello hello действие копирования будет создавать объект «Name» hello с тремя дочерние элементы первой, средней и Last, соответствующим too"Name.First», «Name.Middle» и «Name.Last» в hello определение таблицы.

## <a name="appendix"></a>Приложение
1. **Вопрос:** hello действие копирования поддержки обновления существующих записей?

    **Ответ.** Нет.
2. **Вопрос:** как работает при повторной попытке копирования tooAzure Cosmos DB приходится иметь дело с уже скопированы записей?

    **Ответ:** Если записей имеет поля «Идентификатор», и операция копирования hello пытается tooinsert запись с hello таким же Идентификатором операции копирования hello выдает ошибку.  
3. **Вопрос.** Поддерживает ли фабрика данных [секционирование данных по диапазонам или хэш-секционирование](../documentdb/documentdb-partition-data.md)?

    **Ответ.** Нет.
4. **Вопрос.** Можно ли указать больше одной коллекции Azure Cosmos DB для таблицы?

    **Ответ.** Нет. Сейчас можно указать только одну коллекцию.

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
