---
title: "Перемещение данных в Azure Cosmos DB и обратно | Документация Майкрософт"
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
robots: noindex
ms.openlocfilehash: 32b72577002962f049f446d6f3c2353189867e92
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a>Перемещение данных в Azure Cosmos DB и из нее с помощью фабрики данных Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Версия 1 — общедоступная](data-factory-azure-documentdb-connector.md)
> * [Версия 2 — предварительная](../connector-azure-cosmos-db.md)

> [!NOTE]
> Статья относится к версии 1 фабрики данных, которая является общедоступной версией. Если вы используете версию 2 службы фабрики данных, которая находится на этапе предварительной версии, см. статью [Копирование данных из Azure Cosmos DB с помощью фабрики данных Azure](../connector-azure-cosmos-db.md).

В этой статье объясняется, как с помощью действия копирования в фабрике данных Azure перемещать данные в Azure Cosmos DB и обратно (API DocumentDB). Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования. 

Данные можно скопировать из любого поддерживаемого в качестве источника хранилища данных в Azure Cosmos DB или из Azure Cosmos DB в любое поддерживаемое в качестве приемника хранилище данных. Список хранилищ данных, которые поддерживаются в качестве источников и приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 

> [!IMPORTANT]
> Соединитель Azure Cosmos DB поддерживает только API DocumentDB.

Сведения о копировании данных "как есть" в JSON-файлы или другую коллекцию Cosmos DB либо из них см. в разделе [Импорт и экспорт документов JSON](#importexport-json-documents).

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из хранилища Azure Cosmos DB или обратно, с помощью различных инструментов и API-интерфейсов.

Проще всего создать конвейер с помощью **мастера копирования**. В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.

Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**. Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги: 

1. Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.
2. Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера). При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.  Примеры с определениями JSON для сущностей фабрики данных, которые используются для копирования данных в службу Azure Cosmos DB и из нее, приведены в разделе с [примерами JSON](#json-examples) в этой статье. 

Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для службы Cosmos DB. 

## <a name="linked-service-properties"></a>Свойства связанной службы
В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе Azure Cosmos DB.

| **Свойство** | **Описание** | **Обязательный** |
| --- | --- | --- |
| type |Для свойства надо указать тип **DocumentDb** |Да |
| connectionString |Укажите сведения, необходимые для подключения к базе данных Azure Cosmos DB. |Да |

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
Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Создание наборов данных](data-factory-create-datasets.md). Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Раздел typeProperties во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных. Раздел typeProperties для набора данных типа **DocumentDbCollection** содержит приведенные ниже свойства.

| **Свойство** | **Описание** | **Обязательный** |
| --- | --- | --- |
| collectionName |Имя коллекции документов Cosmos DB. |Да |

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
Для хранилищ данных без схемы, таких как Azure Cosmos DB, служба фабрики данных определяет схему одним из следующих способов.  

1. Если указать структуру данных с помощью свойства **structure** в определении набора данных, служба фабрики данных считает эту структуру схемой. В этом случае, если строка не содержит значение столбца, ему будет присвоено значение NULL.
2. Если структура данных не указана с помощью свойства **structure** в определении набора данных, то служба фабрики данных определяет схему, используя первую строку данных. В этом случае, если первая строка не содержит полную схему, после операции копирования некоторые столбцы будут отсутствовать.

Таким образом для источников данных без схемы рекомендуется указывать структуру данных с помощью свойства **structure** .

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md). Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

> [!NOTE]
> Действие копирования принимает только один набор входных данных и возвращает только один набор выходных.

То, какие свойства будут доступны в разделе typeProperties, зависит от типа действия, а в случае с действием копирования — еще и от типов источников и приемников.

В случае действия копирования, когда источник относится к типу **DocumentDbCollectionSource**, в разделе **typeProperties** доступны приведенные ниже свойства.

| **Свойство** | **Описание** | **Допустимые значения** | **Обязательный** |
| --- | --- | --- | --- |
| запрос |Запрос, нужный для чтения данных. |Строка запроса, поддерживаемая Azure Cosmos DB. <br/><br/>Пример: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Нет <br/><br/>Если не указано, то выполняется инструкция SQL `select <columns defined in structure> from mycollection`. |
| nestingSeparator |Специальный символ, обозначающий, что документ является вложенным. |Любой символ. <br/><br/>Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры. Фабрика данных Azure позволяет обозначать иерархию с помощью разделителя nestingSeparator. В приведенных выше примерах это точка. Благодаря этому разделителю действие копирование создаст объект Name с тремя дочерними элементами, First, Middle и Last, в соответствии с элементами Name.First, Name.Middle и Name.Last в определении таблицы. |Нет |

**DocumentDbCollectionSink** поддерживает приведенные ниже свойства.

| **Свойство** | **Описание** | **Допустимые значения** | **Обязательный** |
| --- | --- | --- | --- |
| nestingSeparator |Такой специальный символ в имени исходного столбца, который указывает, что нужен вложенный документ. <br/><br/>См. пример выше: элемент `Name.First` в выходной таблице обуславливает в документе Cosmos DB такую структуру JSON:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Символ, используемый для разделения уровней вложенности.<br/><br/>Значение по умолчанию — `.` (точка). |Символ, используемый для разделения уровней вложенности. <br/><br/>Значение по умолчанию — `.` (точка). |
| writeBatchSize |Число параллельных запросов к службе Azure Cosmos DB для создания документов.<br/><br/>При копировании данных в службу Cosmos DB или из нее с помощью этого свойства можно оптимизировать производительность. Если увеличить значение свойства writeBatchSize, производительность повышается, потому что в Cosmos DB начинает поступать больше параллельных запросов. Однако необходимо избежать регулирования, которое может вызвать сообщение об ошибке: "Высокая частота запросов".<br/><br/>Регулирование может произойти по ряду причин, включая размер документов, количество терминов в документах, политику индексации целевой коллекции и т. д. Для операций копирования вы можете использовать коллекцию получше (например, S3), чтобы обеспечить максимальную пропускную способность (2500 единиц запроса в секунду). |Целое число  |Нет (значение по умолчанию — 5) |
| writeBatchTimeout |Время ожидания до выполнения операции, пока не завершится срок ее действия. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |

## <a name="importexport-json-documents"></a>Документы JSON для импорта и экспорта
С помощью этого соединителя Cosmos DB можно выполнять следующие задачи:

* импортировать документы JSON из различных источников в Cosmos DB, включая хранилище BLOB-объектов Azure, Azure Data Lake, локальную файловую систему или другие файловые хранилища, поддерживаемые фабрикой данных Azure;
* экспортировать документы JSON из коллекции Cosmos DB в различные файловые хранилища;
* переносить данные между коллекциями Cosmos DB "как есть".

Для обеспечения такого копирования без использования схем: 
* При использовании мастера копирования установите флажок **Export as-is to JSON files or DocumentDB collection** (Экспортировать как есть в JSON-файлы или коллекцию Cosmos DB).
* При редактировании JSON не указывайте раздел structure в наборах данных Cosmos DB и свойство nestingSeparator для источника или приемника Cosmos DB в действии копирования. Чтобы импортировать данные в JSON-файлы или экспортировать их оттуда, в наборе хранилища файлов укажите тип формата "JsonFormat", конфигурацию "filePattern" и пропустите остальные параметры формата. Дополнительные сведения см. в разделе [Формат JSON](data-factory-supported-file-and-compression-formats.md#json-format).

## <a name="json-examples"></a>Примеры определений JSON
Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают, как копировать данные в Azure Cosmos DB и хранилище BLOB-объектов Azure и обратно. Тем не менее данные можно копировать **непосредственно** из любых источников в любой указанный [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемник. Для этого используется действие копирования в фабрике данных Azure.

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a>Пример. Копирование данных из Azure Cosmos DB в большой двоичный объект Azure
В примере ниже показано следующее.

1. Связанная служба типа [DocumentDb](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [DocumentDbCollection](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [DocumentDbCollectionSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Этот пример копирует данные из Azure Cosmos DB в большой двоичный объект Azure. Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.

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

В этом примере предполагается, что в базе данных Azure Cosmos DB есть коллекция **Person**.

Если для параметра external задать значение true и указать политику externalData, фабрика данных Azure будет считать эту таблицу внешней по отношению к себе и не созданной в результате какого-либо действия в фабрике данных.

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

Данные копируются в новый BLOB-объект каждый час. Путь к BLOB-объекту отражает дату и время по часам.

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
Образец JSON-документа в коллекции Person в базе данных Azure Cosmos DB:

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

В конвейере ниже данные копируются из коллекции Person, находящейся в базе данных Azure Cosmos DB, в большой двоичный объект Azure. Для действия копирования указаны входные и выходные наборы данных.  

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
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a>Пример. Копирование данных из большого двоичного объекта в Azure Cosmos DB 
В примере ниже показано следующее.

1. Связанная служба типа [DocumentDb](#azure-documentdb-linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

В этом примере данные копируются из большого двоичного объекта Azure в Azure Cosmos DB. Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.

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

В примере данные копируются в коллекцию Person.

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
В приведенном ниже конвейере данные копируются из большого двоичного объекта Azure в коллекцию Person, находящуюся в Cosmos DB. Для действия копирования указаны входные и выходные наборы данных.

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
Если пример входных данных BLOB-объекта выглядит так:

```
1,John,,Doe
```
JSON-файл выходных данных в Cosmos DB будет выглядеть так:

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
Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры. Фабрика данных Azure позволяет обозначать иерархию с помощью разделителя **nestingSeparator**, которым в этом примере является точка. Благодаря этому разделителю действие копирование создаст объект Name с тремя дочерними элементами, First, Middle и Last, в соответствии с элементами Name.First, Name.Middle и Name.Last в определении таблицы.

## <a name="appendix"></a>Приложение
1. **Вопрос.** Поддерживает ли действие копирования обновление существующих записей?

    **Ответ.** Нет.
2. **Вопрос.** Как при повторной попытке копирования в Azure Cosmos DB обрабатываются уже скопированные записи?

    **Ответ.** Если у записи есть поле идентификатора, и операция копирования пытается вставить запись с тем же идентификатором, операция копирования завершается ошибкой.  
3. **Вопрос.** Поддерживает ли фабрика данных [секционирование данных по диапазонам или хэш-секционирование](../../cosmos-db/documentdb-partition-data.md)?

    **Ответ.** Нет.
4. **Вопрос.** Можно ли указать больше одной коллекции Azure Cosmos DB для таблицы?

    **Ответ.** Нет. Сейчас можно указать только одну коллекцию.

## <a name="performance-and-tuning"></a>Производительность и настройка
Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.
