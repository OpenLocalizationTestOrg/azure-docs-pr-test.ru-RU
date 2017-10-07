---
title: "aaaMove tooand данных из SQL Server | Документы Microsoft"
description: "Дополнительные сведения о как toomove данных из SQL Server базы данных, локально или на виртуальной Машине Azure, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Переместить tooand данных из SQL Server локально или в IaaS (ВМ Azure) с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данные из локальной базы данных SQL Server. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello. 

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.
Можно скопировать данные **из базы данных SQL Server** toohello следующие хранилищ данных:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Можно скопировать данные из hello, следуя хранилищ данных **базы данных SQL Server tooa**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Поддерживаемые версии SQL Server
Эта поддержка соединителя SQL Server, копирование данных из / toohello следующие версии экземпляра, размещенного локально, либо в Azure IaaS с помощью проверки подлинности SQL и проверка подлинности Windows: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>Включение соединения
Основные понятия Hello и шаги, необходимые для соединения с SQL Server, размещенный в локальной или в Azure IaaS (инфраструктура как услуга) виртуальных машин hello же. В обоих случаях необходимо toouse шлюз управления данными для подключения.

В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello. Настройка экземпляра шлюза необходима для подключения к SQL Server.

При установке шлюза на hello же локальной машины или облака экземпляр виртуальной Машины как hello SQL Server для повышения производительности, рекомендуется установить их на отдельных компьютерах. Наличие шлюза hello и SQL Server на отдельных компьютерах уменьшает конкуренцию за ресурсы.

## <a name="getting-started"></a>Приступая к работе
Можно создать конвейер с действием копирования, которое перемещает данные из базы данных SQL Server или в нее с помощью различных инструментов и интерфейсов API.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello. 

1. Создание **фабрики данных**. Фабрика данных может содержать один или несколько конвейеров. 
2. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных. Например при копировании данных из tooan базы данных SQL Server хранилище больших двоичных объектов создается две связанные службы toolink вашей базы данных SQL Server и фабрику данных tooyour учетной записи хранилища Azure. Свойства связанной службы, определенные tooSQL базы данных сервера, в разделе [связанные свойства службы](#linked-service-properties) раздела. 
3. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. В примере hello, упомянутые в последнем шаге hello создайте таблицу dataset hello toospecify SQL в базе данных SQL Server, содержащий hello входных данных. Создайте другой контейнер больших двоичных объектов dataset toospecify hello и hello папке, содержащей данные hello копируются hello базы данных SQL Server. Свойства набора данных, определенных tooSQL базы данных сервера, в разделе [свойства набора данных](#dataset-properties) раздела.
4. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. В примере hello приведенные выше используются SqlSource в BlobSink источника и в приемник для действия копирования hello. Аналогично при копировании из хранилища больших двоичных объектов tooSQL базы данных сервера использовать BlobSource и SqlSink в действии копирования hello. Свойства действия копирования, определенные tooSQL базы данных сервера, в разделе [скопировать свойства действия](#copy-activity-properties) раздела. Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локальной базы данных SQL Server см. в разделе [JSON примеры](#json-examples-for-copying-data-from-and-to-sql-server) этой статьи. 

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooSQL сервера: 

## <a name="linked-service-properties"></a>Свойства связанной службы
Создание связанной службы типа **OnPremisesSqlServer** toolink фабрикой данных базы данных tooa в локальной среде SQL Server. Привет, в следующей таблице приводится описание JSON элементов определенного tooon локальной связанной службы SQL Server.

Привет, в следующей таблице приводится описание tooSQL определенные элементы JSON службы связанного сервера.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **OnPremisesSqlServer**. |Да |
| connectionString |Укажите сведения connectionString, необходимые tooconnect toohello локальной SQL Server базы данных с помощью проверки подлинности Windows или проверка подлинности SQL. |Да |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных SQL Server. |Да |
| Имя пользователя |При использовании проверки подлинности Windows укажите имя пользователя. Например, **domainname\\username**. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |

Вы можете зашифровать учетные данные с помощью hello **New AzureRmDataFactoryEncryptValue** командлета и использовать их в строке подключения hello, как показано в следующий пример hello (**EncryptedCredential** свойство):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>Примеры
**JSON для использования проверки подлинности SQL**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**JSON для использования проверки подлинности Windows**

Шлюз управления данными будет олицетворять указанное hello базы данных SQL Server в локальной toohello в tooconnect учетной записи пользователя. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
В образцах hello использовании набора данных типа **SqlServerTable** toorepresent таблицы в базе данных SQL Server.  

Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы JSON набора данных, такие как структура, доступность и политика, одинаковы для всех типов наборов данных (SQL Server, большой двоичный объект Azure, таблица Azure и т. д.).

раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello **typeProperties** раздел для набора данных hello типа **SqlServerTable** имеет hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя hello таблицы или представления в экземпляр базы данных SQL Server hello, связанная служба ссылается. |Да |

## <a name="copy-activity-properties"></a>Свойства действия копирования
При перемещении данных из базы данных SQL Server, следует установить hello исходного типа в действие копирования hello слишком**SqlSource**. Аналогичным образом, при перемещении базы данных SQL Server tooa данных задаются тип приемника hello в действии копирования hello слишком**SqlSink**. Этот раздел содержит список свойств, поддерживаемых типами SqlSource и SqlSink.

Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.

> [!NOTE]
> Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.

В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

### <a name="sqlsource"></a>SqlSource
Если источник в операции копирования имеет тип **SqlSource**, hello следующие свойства доступны в **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| SqlReaderQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, select * from MyTable. Может ссылаться на несколько таблиц из базы данных hello ссылается hello входного набора данных. Если не указан, hello выполняемой инструкции SQL: select from MyTable. |Нет |
| sqlReaderStoredProcedureName |Имя hello хранимой процедуры, который считывает данные из таблицы источника hello. |Имя hello хранимой процедуры. Hello последней инструкцией SQL должна быть инструкция SELECT в hello хранимой процедуре. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |

Если hello **sqlReaderQuery** указан для hello SqlSource, hello действие копирования выполняет этот запрос данных hello базы данных SQL Server источника tooget hello.

Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).

Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello, используемые toobuild toorun запрос select для hello базы данных SQL Server. Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.

> [!NOTE]
> При использовании **sqlReaderStoredProcedureName**, по-прежнему требуется toospecify значение для hello **tableName** свойство в наборе данных hello JSON. Хотя какие-либо проверки этой таблицы отсутствуют.

### <a name="sqlsink"></a>SqlSink
**SqlSink** поддерживает hello следующие свойства:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| writeBatchTimeout |Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |
| writeBatchSize |Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello. |Целое число (количество строк) |Нет (значение по умолчанию — 10 000). |
| sqlWriterCleanupScript |Укажите запрос для действия копирования tooexecute, таким образом, чтобы очистить данные особый срез. Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy). |Инструкция запроса. |Нет |
| sliceIdentifierColumnName |Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения. Дополнительные сведения см. в разделе [Повторяющаяся операция копирования](#repeatable-copy). |Имя столбца с типом данных binary(32). |Нет |
| sqlWriterStoredProcedureName |Имя hello хранимой процедуры upserts (обновления или вставки) данные в целевой таблице hello. |Имя hello хранимой процедуры. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |
| sqlWriterTableType |Укажите toobe имя типа таблицы, используемых в hello хранимой процедуре. Действие копирования предоставляет hello данных, перемещаемых во временной таблице с этой таблицей. Кода хранимой процедуры можно объединять hello данные копируются с существующими данными. |Имя типа таблицы. |Нет |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>Примеры JSON для копирования данных из и tooSQL сервера
Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Здравствуйте, следующие примеры Показать как toocopy tooand данных из SQL Server и хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Пример: Копирование данных из SQL Server tooAzure больших двоичных объектов
Hello следующем образце показано:

1. Связанная служба типа [OnPremisesSqlServer](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [SqlSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные временных рядов с tooan таблицы SQL Server BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

В качестве первого шага настройки шлюза управления данными hello. Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.

**Связанная служба SQL Server**
```json
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
**Связанная служба хранилища BLOB-объектов Azure**

```json
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
**Входной набор данных SQL Server**

Образец Hello предполагается создания таблицы «MyTable» в SQL Server, и она содержит столбец с именем «timestampcolumn» для временного ряда данных. Вы можете запрашивать через несколько таблиц в одной базе данных с помощью одного набора данных, но одна таблица должна использоваться для набора данных hello tableName typeProperty приветствия.

Параметр «external»: «true» уведомляет службу фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```json
{
  "name": "SqlServerInput",
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
**Выходной набор данных BLOB-объекта Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```json
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
**Конвейер с действием копирования**

конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlSource** и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
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
В этом примере **sqlReaderQuery** указан для hello SqlSource. Действие копирования Hello этот запрос запускает hello tooget hello базы данных SQL Server исходных данных. Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры). Hello sqlReaderQuery ссылаться на несколько таблиц в базе данных hello ссылается hello входного набора данных. Это не таблица hello ограниченный tooonly, задайте как hello typeProperty tableName набора данных.

Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello, используется toobuild toorun запрос select для hello базы данных SQL Server. Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.

В разделе hello [источника Sql](#sqlsource) раздел и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) список свойств, поддерживаемых SqlSource и BlobSink hello.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Пример: Копирование данных из больших двоичных объектов Azure tooSQL сервера
Hello следующем образце показано:

1. Hello связанной службы типа [OnPremisesSqlServer](#linked-service-properties).
2. Hello связанной службы типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
5. Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [SqlSink](#sql-server-copy-activity-type-properties).

Образец Hello копирует временных рядов данных из таблицы SQL Server tooa BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба SQL Server**

```json
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
**Связанная служба хранилища BLOB-объектов Azure**

```json
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
**Входной набор данных BLOB-объекта Azure**

Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1). Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello. «external»: параметр «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```json
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
**Выходной набор данных SQL Server**

Образец Hello копирует tooa таблицу данных, с именем «MyTable» в SQL Server. Создать таблицу hello в SQL Server с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов. Новые строки добавляются в таблицу toohello каждый час.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Конвейер с действием копирования**

конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlSink**.

```json
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
            "name": " SqlServerOutput "
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

## <a name="troubleshooting-connection-issues"></a>Устранение неполадок с подключением
1. Настройка удаленных соединений tooaccept SQL Server. Запустите **SQL Server Management Studio**, щелкните правой кнопкой мыши свой **сервер** и выберите пункт **Свойства**. Выберите **подключений** из списка hello и проверка **toohello сервера разрешить удаленные соединения**.

    ![Включение удаленных подключений](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    В разделе [Настройка параметра конфигурации сервера remote access hello](https://msdn.microsoft.com/library/ms191464.aspx) подробное описание шагов.
2. Запустите **диспетчер конфигурации SQL Server**. Разверните **сетевая конфигурация SQL Server** для hello экземпляра, который хотите, а затем выберите **протоколы для MSSQLSERVER**. Вы увидите протоколов в правой области hello. Включите TCP/TP, щелкнув правой кнопкой мыши имя протокола **TCP/IP** и выбрав пункт **Включить**.

    ![Включение TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Подробные сведения и альтернативные способы включения протокола TCP/IP см. в статье [Включение или отключение сетевого протокола сервера](https://msdn.microsoft.com/library/ms191294.aspx).
3. В том же окне hello, дважды щелкните **TCP/IP** toolaunch **свойства TCP/IP** окна.
4. Переключение toohello **IP-адреса** вкладки. Прокрутите вниз toosee **IPAll** раздела. Запишите hello ** TCP-порт ** (по умолчанию — **1433**).
5. Создание **правило для брандмауэра Windows hello** на hello машины tooallow входящий трафик через этот порт.  
6. **Проверка подключения**: tooconnect toohello SQL Server с помощью полного имени, используйте SQL Server Management Studio с другого компьютера. Например, <machine><domain>.corp<company>.com,1433.

   > [!IMPORTANT]

   > В разделе [перемещения данных между локальным источникам и hello облако с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) подробные сведения.
   >
   > Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Столбцы идентификаторов в целевой базе данных hello
Этот раздел содержит пример, в котором данные копируются из исходной таблицы с без идентификатора столбца tooa целевую таблицу со столбцом идентификаторов.

**Исходная таблица:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Целевая таблица:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

Обратите внимание, что этот hello целевая таблица имеет столбец идентификаторов.

**Определение JSON исходного набора данных**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
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

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
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

## <a name="type-mapping-for-sql-server"></a>Сопоставление типов SQL Server
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статья hello действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

После перемещения данных слишком & из SQL server, hello следующие сопоставления используются из типа too.NET типа SQL и наоборот.

сопоставление Hello выполняется аналогично hello сопоставление типов данных SQL Server для ADO.NET.

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

## <a name="mapping-source-toosink-columns"></a>Сопоставление столбцов toosink источника
toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Повторяющаяся операция копирования
При копировании данных tooSQL базы данных сервера, действие копирования hello добавляет таблицу приемник toohello данных по умолчанию. tooperform UPSERT. Вместо этого в разделе [tooSqlSink Repeatable записи](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) статьи. 

При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
