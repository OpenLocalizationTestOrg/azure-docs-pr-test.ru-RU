---
title: "aaaCopy данных из базы данных SQL Azure | Документы Microsoft"
description: "Узнайте, как toocopy данных из базы данных SQL Azure, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Tooand копирования данных из базы данных SQL Azure, с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в tooand данных toomove фабрики данных Azure, из базы данных SQL Azure. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.  

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.
Можно скопировать данные **из базы данных SQL Azure** toohello следующие хранилищ данных:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Можно скопировать данные из hello, следуя хранилищ данных **tooAzure базы данных SQL**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>Поддерживаемый тип проверки подлинности
Соединитель базы данных SQL Azure поддерживает обычную проверку подлинности.

## <a name="getting-started"></a>Приступая к работе
Можно создать конвейер с действием копирования, которое перемещает данные из базы данных SQL Azure или в нее с помощью различных инструментов и API-интерфейсов.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello. 

1. Создание **фабрики данных**. Фабрика данных может содержать один или несколько конвейеров. 
2. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных. Например при копировании данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure, создается два связанных служб toolink вашей учетной записи хранилища Azure и фабрики данных tooyour базы данных Azure SQL. Свойства связанной службы, определенные tooAzure базы данных SQL, в разделе [связанные свойства службы](#linked-service-properties) раздела. 
3. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных. И создайте другую таблицу SQL hello toospecify набора данных в базе данных Azure SQL hello, содержащий hello данные, скопированные из хранилища больших двоичных объектов hello. Свойства набора данных, определенных tooAzure хранилища Озера данных, в разделе [свойства набора данных](#dataset-properties) раздела.
4. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. В примере hello приведенные выше используются BlobSource в исходной и SqlSink в приемник для действия копирования hello. Аналогично Если копируются из базы данных SQL Azure tooAzure хранилища больших двоичных объектов, использовать SqlSource и BlobSink в действии копирования hello. Свойства действия копирования, определенные tooAzure базы данных SQL, в разделе [скопировать свойства действия](#copy-activity-properties) раздела. Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из базы данных SQL Azure см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-sql-database) этой статьи. 

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure базы данных SQL: 

## <a name="linked-service-properties"></a>Свойства связанной службы
Azure SQL связанные ссылки на службу фабрики данных tooyour базы данных Azure SQL. в следующей таблице Hello предоставляет описание tooAzure SQL определенные элементы JSON связанной службы.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **AzureSqlDatabase** |Да |
| connectionString |Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных SQL Azure toohello tooconnect. Поддерживается только обычная проверка подлинности. |Да |

> [!IMPORTANT]
> Настройка [брандмауэр базы данных SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello сервера базы данных слишком[сервер служб Azure tooaccess hello](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Кроме того при копировании данных tooAzure базы данных SQL из внешней в Azure, включая из локальных источников данных со шлюзом фабрики данных, настройте соответствующий диапазон IP-адресов для компьютера hello, передающий данные tooAzure базы данных SQL.

## <a name="dataset-properties"></a>Свойства набора данных
toospecify dataset toorepresent входных или выходных данных в базе данных Azure SQL, задайте свойство типа hello hello набора данных для: **AzureSqlTable**. Набор hello **linkedServiceName** свойство toohello имя набора данных hello hello Azure SQL связанной службы.  

Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello **typeProperties** раздел для набора данных hello типа **AzureSqlTable** имеет hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя hello таблицы или представления в экземпляр базы данных SQL Azure hello, связанная служба ссылается. |Да |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

> [!NOTE]
> Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.

В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

При перемещении данных из базы данных Azure SQL, следует установить hello исходного типа в действие копирования hello слишком**SqlSource**. Аналогичным образом, при перемещении базы данных Azure SQL tooan данных задаются тип приемника hello в действии копирования hello слишком**SqlSink**. Этот раздел содержит список свойств, поддерживаемых типами SqlSource и SqlSink.

### <a name="sqlsource"></a>SqlSource
В действии копирования, когда источник hello типа **SqlSource**, hello следующие свойства доступны в **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| SqlReaderQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Пример: `select * from MyTable`. |Нет |
| sqlReaderStoredProcedureName |Имя hello хранимой процедуры, который считывает данные из таблицы источника hello. |Имя hello хранимой процедуры. Hello последней инструкцией SQL должна быть инструкция SELECT в hello хранимой процедуре. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |

Если hello **sqlReaderQuery** указан для hello SqlSource, hello действие копирования выполняет этот запрос данных hello базы данных SQL Azure источника tooget hello. Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).

Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello hello набора данных JSON, используемые toobuild запроса (`select column1, column2 from mytable`) toorun от hello базы данных SQL Azure. Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.

> [!NOTE]
> При использовании **sqlReaderStoredProcedureName**, по-прежнему требуется toospecify значение для hello **tableName** свойство в наборе данных hello JSON. Хотя какие-либо проверки этой таблицы отсутствуют.
>
>

### <a name="sqlsource-example"></a>Пример SqlSource

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**Определение Hello хранимые процедуры:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>SqlSink
**SqlSink** поддерживает hello следующие свойства:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| writeBatchTimeout |Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |
| writeBatchSize |Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello. |Целое число (количество строк) |Нет (значение по умолчанию — 10 000). |
| sqlWriterCleanupScript |Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез. Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy). |Инструкция запроса. |Нет |
| sliceIdentifierColumnName |Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения. Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy). |Имя столбца с типом данных binary(32). |Нет |
| sqlWriterStoredProcedureName |Имя hello хранимой процедуры upserts (обновления или вставки) данные в целевой таблице hello. |Имя hello хранимой процедуры. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |
| sqlWriterTableType |Укажите имя toobe тип таблицы, используемых в hello хранимой процедуре. Действие копирования предоставляет hello данных, перемещаемых во временной таблице с этой таблицей. Кода хранимой процедуры можно объединять hello данные копируются с существующими данными. |Имя типа таблицы. |Нет |

#### <a name="sqlsink-example"></a>Пример SqlSink

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>Примеры JSON для копирования данных tooand из базы данных SQL
Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают как toocopy tooand данных из базы данных SQL Azure и хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>Пример: Копирование данных из базы данных SQL Azure tooAzure больших двоичных объектов
Hello же определяет hello, следуя фабрики данных сущности:

1. Связанная служба типа [AzureSqlDatabase](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [AzureSqlTable](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные временных рядов (каждый час, день, т. д.) из таблицы в большом двоичном объекте tooa базы данных Azure SQL каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.  

**Связанная служба базы данных SQL Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
В разделе hello [связанной службы SQL Azure](#linked-service) раздел hello список свойств, поддерживаемых этой связанной службой.

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
В разделе hello [больших двоичных объектов Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) статье hello список свойств, поддерживаемых этой связанной службой.


**Входной набор данных SQL Azure**

Образец Hello предполагается создания таблицы «MyTable» в Azure SQL и содержит столбец с именем «timestampcolumn» для временного ряда данных.

Параметр «external»: «true» уведомляет службу hello фабрики данных Azure, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

. В разделе hello [свойства тип набора данных Azure SQL](#dataset) раздел hello список свойств, поддерживаемых этим типом набора данных.  

**Выходной набор данных BLOB-объекта Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
. В разделе hello [свойства тип набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) раздел hello список свойств, поддерживаемых этим типом набора данных.  

**Действие копирования в конвейере с базой данных SQL в качестве источника и BLOB-объектом в качестве приемника:**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource** и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
В примере hello **sqlReaderQuery** указан для hello SqlSource. Действие копирования Hello этот запрос запускает hello tooget hello базы данных SQL Azure исходных данных. Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).

Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello hello набора данных JSON, используемые toobuild toorun запроса от hello базы данных SQL Azure. Например, `select column1, column2 from mytable`. Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.

В разделе hello [источника Sql](#sqlsource) раздел и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) список свойств, поддерживаемых SqlSource и BlobSink hello.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>Пример: Копирование данных из больших двоичных объектов Azure tooAzure базы данных SQL
Образец Hello определяет hello, следуя фабрики данных сущности:  

1. Связанная служба типа [AzureSqlDatabase](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSqlTable](#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [SqlSink](#copy-activity-properties).

Образец Hello копирует данные временных рядов (каждый час, день, т. д.) из таблицы tooa BLOB-объектов Azure в базе данных Azure SQL каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба SQL Azure**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
В разделе hello [связанной службы SQL Azure](#linked-service) раздел hello список свойств, поддерживаемых этой связанной службой.

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
В разделе hello [больших двоичных объектов Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) статье hello список свойств, поддерживаемых этой связанной службой.


**Входной набор данных BLOB-объекта Azure**

Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1). Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello. «external»: параметр «true» уведомляет службу hello фабрики данных, что эта таблица является внешней toohello фабрики данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
. В разделе hello [свойства тип набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) раздел hello список свойств, поддерживаемых этим типом набора данных.

**Выходной набор данных базы данных SQL Azure:**

Образец Hello копирует tooa таблицу данных, с именем «MyTable» в Azure SQL. Создать таблицу hello в SQL Azure с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов. Новые строки добавляются в таблицу toohello каждый час.

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
. В разделе hello [свойства тип набора данных Azure SQL](#dataset) раздел hello список свойств, поддерживаемых этим типом набора данных.

**Действие копирования в конвейере с BLOB-объектом в качестве источника и базой данных SQL в качестве приемника:**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
В разделе hello [приемника Sql](#sqlsink) раздел и [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) hello список свойств, поддерживаемых SqlSink и BlobSource.

## <a name="identity-columns-in-hello-target-database"></a>Столбцы идентификаторов в целевой базе данных hello
В этом разделе приведен пример копирования данных из исходной таблицы без tooa назначения идентификаторов столбца таблицы со столбцом идентификаторов.

**Исходная таблица:**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Целевая таблица:**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
Обратите внимание, что этот hello целевая таблица имеет столбец идентификаторов.

**Определение JSON исходного набора данных**

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Определение JSON целевого набора данных**

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

Обратите внимание, что у исходной и целевой таблиц разные схемы (в целевой есть дополнительный столбец с идентификаторами). В этом случае необходимо toospecify **структуры** свойство в определении набора данных целевого hello, который не содержит столбца идентификаторов hello.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Вызов хранимой процедуры из приемника SQL
Пример вызова хранимой процедуры из приемника SQL в действии копирования в конвейере приведен в статье [Invoke stored procedure from copy activity in Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md) (Вызов хранимой процедуры из действия копирования в фабрике данных Azure). 

## <a name="type-mapping-for-azure-sql-database"></a>Сопоставление типов для базы данных SQL Azure
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статье действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных tooand из базы данных SQL Azure, hello следующие сопоставления используются из типа too.NET типа SQL и наоборот. сопоставление Hello выполняется аналогично hello сопоставление типов данных SQL Server для ADO.NET.

| Тип ядра СУБД SQL Server | Тип .NET Framework |
| --- | --- |
| bigint |Int64 |
| binary; |Byte[] |
| bit |Логический |
| char; |String, Char[] |
| дата |DateTime |
| DateTime |DateTime |
| datetime2; |DateTime |
| Datetimeoffset |Datetimeoffset |
| Decimal |Decimal |
| Атрибут FILESTREAM (varbinary(max)) |Byte[] |
| Float |Double |
| изображение |Byte[] |
| int |Int32 |
| money; |Decimal |
| nchar; |String, Char[] |
| ntext |String, Char[] |
| numeric |Decimal |
| nvarchar; |String, Char[] |
| real; |Single |
| rowversion |Byte[] |
| smalldatetime; |DateTime |
| smallint; |Int16 |
| smallmoney; |Decimal |
| sql_variant |Object * |
| text |String, Char[] |
| time |Интервал времени |
| Timestamp |Byte[] |
| tinyint; |Byte |
| uniqueidentifier |Guid |
| varbinary; |Byte[] |
| varchar. |String, Char[] |
| xml |xml |

## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Повторяющаяся операция копирования
При копировании данных tooSQL базы данных сервера, действие копирования hello добавляет таблицу приемник toohello данных по умолчанию. tooperform UPSERT. Вместо этого в разделе [tooSqlSink Repeatable записи](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) статьи. 

При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
