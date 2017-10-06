---
title: "Индекс tooSearch aaaPush данных с помощью фабрики данных | Документы Microsoft"
description: "Дополнительные сведения о данных toopush tooAzure индекс поиска с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Извещающие индекс поиска Azure tooan данных с помощью фабрики данных Azure
В этой статье описывается, как tooAzure поиска индекса хранилища данных toopush toouse hello действие копирования из поддерживаемых исходных данных. Поддерживаемой исходной хранилищ данных, перечислены в исходный столбец hello hello [поддерживаемые источники и приемники](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования и сочетания поддерживаемых данных хранилища.

## <a name="enabling-connectivity"></a>Включение соединения
Служба фабрики данных tooallow подключения tooan к локальному хранилищу данных, установить шлюз управления данными в локальной среде. Можно установить шлюз на hello того же компьютера, на котором размещен источник данных hello хранения или на отдельном компьютере tooavoid, конкурирующие за ресурсы с данными hello хранилище.

Шлюз управления данными подключается локальными службами toocloud источники данных в виде безопасности и управления. Сведения о шлюзе управления данными см. в статье [Перемещение данных между локальными источниками и облаком](data-factory-move-data-between-onprem-and-cloud.md).

## <a name="getting-started"></a>Приступая к работе
Можно создать конвейер действием копирования, которое передает данные из индекса поиска tooAzure источника данных хранилища с помощью различных средств и API-интерфейсы.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello. 

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, которые являются индекс поиска tooAzure данных используется toocopy см [пример JSON: скопировать данные из индекса поиска tooAzure SQL Server в локальной](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) этой статьи. 

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure индекс поиска:

## <a name="linked-service-properties"></a>Свойства связанной службы

Привет, в следующей таблице приводится описание службы поиска Azure связаны определенные toohello элементы JSON.

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- |
| type | свойство типа Hello должно быть присвоено: **AzureSearch**. | Да |
| url | URL-адрес для службы поиска Azure hello. | Да |
| key | Ключ администратора для hello службы поиска Azure. | Да |

## <a name="dataset-properties"></a>Свойства набора данных

Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных. Hello **typeProperties** раздела отличается для каждого типа набора данных. Hello typeProperties статьи для набора данных типа hello **AzureSearchIndex** имеет hello следующие свойства:

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- |
| type | свойство типа Hello должно быть задано слишком**AzureSearchIndex**.| Да |
| indexName | Имя индекса поиска Azure hello. Фабрика данных hello индекс не создается. Hello индекс должен существовать в поиске Azure. | Да |


## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий. В то время как свойства в разделе "typeProperties" hello, зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

Для действия копирования, если приемник hello имеет тип hello **AzureSearchIndexSink**, hello следующие свойства доступны в разделе "typeProperties":

| Свойство | Описание | Допустимые значения | Обязательно |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Указывает ли toomerge или замены, если документ уже существует в индексе hello. В разделе hello [WriteBehavior свойства](#writebehavior-property).| Merge (по умолчанию)<br/>Отправить| Нет |
| WriteBatchSize | Передает данные в индекс поиска Azure hello достижении writeBatchSize hello размер буфера. В разделе hello [WriteBatchSize свойство](#writebatchsize-property) подробные сведения. | 1 too1 000. Значение по умолчанию — 1000. | Нет |

### <a name="writebehavior-property"></a>Свойство WriteBehavior
При записи данных AzureSearchSink выполняет операцию upsert. Другими словами при создании документа, если ключ документа hello уже существует в индекс поиска Azure hello, поиска Azure обновляет существующий документ hello, а не исключения конфликтов.

Hello AzureSearchSink предоставляет hello, следующие два поведения upsert (с помощью пакета SDK AzureSearch):

- **Слияние**: объединение всех столбцов hello в новый документ hello с существующие один hello. Для столбцов со значением null в новый документ hello hello значение hello существующих один сохраняется.
- **Отправка**: hello новый документ заменяет hello существующий. Для столбцов, не указанных в новый документ hello hello значение toonull есть ли ненулевое значение в существующем документе hello или нет.

по умолчанию Hello **слияния**.

### <a name="writebatchsize-property"></a>Свойство WriteBatchSize
Служба Поиска Azure поддерживает запись документов в виде пакета. Пакет может содержать 1 too1, 000 действия. Действие, которое обрабатывает одной операции отправки или слияния hello tooperform документа.

### <a name="data-type-support"></a>Поддержка типов данных
Hello следующей таблице указывает, поддерживается ли тип данных поиска Azure.

| Тип данных Поиска Azure | Поддерживается в приемнике Поиска Azure |
| ---------------------- | ------------------------------ |
| Строка | Да |
| Int32 | Да |
| Int64 | Да |
| Double | Да |
| Логический | Да |
| DataTimeOffset | Да |
| Массив строк | Нет |
| GeographyPoint | Нет |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>Пример JSON: копирование данных из индекса поиска tooAzure в локальной среде SQL Server

Hello следующем образце показано:

1.  Связанная служба типа [AzureSqlDW](#linked-service-properties).
2.  Связанная служба типа [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Входной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSearchIndex](#dataset-properties).
4.  [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) и [AzureSearchIndexSink](#copy-activity-properties).

Образец Hello копирует данные временного ряда из индекса поиска Azure tooan базы данных SQL Server в локальной каждый час. свойства JSON Hello, используемый в этом примере описаны в разделах, следующие примеры hello.

В качестве первого шага установки hello шлюз управления данными на локальном компьютере. Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.

**Связанная служба Поиска Azure:**

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**Связанная служба SQL Server**

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

**Входной набор данных SQL Server**

Образец Hello предполагается создания таблицы «MyTable» в SQL Server, и она содержит столбец с именем «timestampcolumn» для временного ряда данных. Вы можете запрашивать через несколько таблиц в одной базе данных с помощью одного набора данных, но одна таблица должна использоваться для набора данных hello tableName typeProperty приветствия.

Параметр «external»: «true» уведомляет службу фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

**Выходной набор данных Поиска Azure:**

Hello образец копий данных tooan индекс поиска Azure с именем **продуктов**. Фабрика данных hello индекс не создается. tootest hello образца, создайте индекс с таким именем. Создайте индекс поиска Azure hello с hello столько же столбцов, как и hello входного набора данных. Новые записи добавляются в индекс поиска Azure toohello каждый час.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**Действие копирования в конвейере со средой SQL в качестве источника и индексом Поиска Azure в качестве приемника**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource** и **приемник** тип установлен слишком**AzureSearchIndexSink**. запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

При копировании данных из облачного хранилища данных в Поиск Azure свойство `executionLocation` является обязательным. Hello следующем фрагменте JSON показан hello изменений в соответствии с действием копирования `typeProperties` в качестве примера. Дополнительные сведения и поддерживаемые значения см. в разделе [Копирование данных из одного облачного хранилища данных в другое](data-factory-data-movement-activities.md#global).

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Копирование из облачного источника
При копировании данных из облачного хранилища данных в Поиск Azure свойство `executionLocation` является обязательным. Hello следующем фрагменте JSON показан hello изменений в соответствии с действием копирования `typeProperties` в качестве примера. Дополнительные сведения и поддерживаемые значения см. в разделе [Копирование данных из одного облачного хранилища данных в другое](data-factory-data-movement-activities.md#global).

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

Также можно сопоставить столбцы из источника toocolumns набора данных из набора данных приемник в определении действия копирования hello. Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Производительность и настройка  
. В разделе hello [действие копирования производительности и руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) и различные способы toooptimize его.

## <a name="next-steps"></a>Дальнейшие действия
См. следующие статьи hello.

* [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .
