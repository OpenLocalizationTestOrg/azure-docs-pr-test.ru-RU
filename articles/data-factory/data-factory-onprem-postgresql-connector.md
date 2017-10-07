---
title: "aaaMove данных PostgreSQL с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из базы данных PostgreSQL, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a>Перемещение данных из PostgreSQL с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данные из локальной базы данных PostgreSQL. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из локальной PostgreSQL хранилища поддерживается tooany приемник данных хранилища данных. Список хранилищ данных, поддерживаемые действием копирования hello как приемники см. в разделе [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Фабрика данных в настоящее время поддерживает перемещение данных из PostgreSQL баз данных хранилища данных tooother, но не для перемещения данных из других данных хранит tooan база данных PostgreSQL. 

## <a name="prerequisites"></a>Необходимые компоненты

Служба фабрики данных поддерживает подключения PostgreSQL tooon локальные источники, с помощью hello шлюз управления данными. В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.

Даже если база данных PostgreSQL hello размещается на виртуальной Машине Azure IaaS требуется шлюз. Можно установить шлюз на hello же ВМ IaaS как данные hello хранения или в другой виртуальной Машине, при условии, что шлюз hello подключения toohello базы данных.

> [!NOTE]
> Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).

## <a name="supported-versions-and-installation"></a>Поддерживаемые версии и установка
Шлюз управления данными tooconnect toohello базы данных PostgreSQL, установите hello [Ngpsql поставщик данных для PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 или выше на hello же системы как hello шлюз управления данными. Поддерживается PostgreSQL версии 7.4 и более.

## <a name="getting-started"></a>Приступая к работе
Создать конвейер с действием копирования, который перемещает данные из локального хранилища данных PostgreSQL, можно с помощью различных инструментов и интерфейсов API. 

- toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера. 
- Можно также использовать следующие средства toocreate конвейера hello: 
    - Портал Azure
    - Visual Studio
    - Azure PowerShell
    - Шаблон диспетчера ресурсов Azure
    - .NET API
    - Интерфейс REST API

     В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локального хранилища данных PostgreSQL см [пример JSON: копирования данных из PostgreSQL tooAzure больших двоичных объектов](#json-example-copy-data-from-postgresql-to-azure-blob) этой статьи. 

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooa PostgreSQL хранилища данных:

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello в следующей таблице приводится описание службы конкретных tooPostgreSQL связанные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **OnPremisesPostgreSql** |Да |
| server |Имя сервера PostgreSQL hello. |Да |
| database |Имя базы данных PostgreSQL hello. |Да |
| schema |Имя схемы hello в базе данных hello. Имя схемы Hello учитывается регистр. |Нет |
| authenticationType |Тип проверки подлинности используется база данных PostgreSQL toohello tooconnect. Возможными значениями являются: анонимная, обычная и Windows. |Да |
| Имя пользователя |При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальная база данных PostgreSQL. |Да |

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.

раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных типа **RelationalTable** (включает набор данных PostgreSQL) имеет следующие свойства hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в экземпляр базы данных PostgreSQL, который ссылается связанная служба hello. Hello tableName учитывается регистр. |Нет (если для свойства **RelationalSource** задано значение **query**). |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

Если источник имеет тип **RelationalSource** (включая PostgreSQL), hello следующие свойства доступны в разделе "typeProperties":

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, "query": "select * from \"MySchema\".\"MyTable\"". |Нет (если для свойства **tableName** задано значение **dataset**). |

> [!NOTE]
> В именах схем и таблиц учитывается регистр. Заключайте их в `""` (двойные кавычки) в запросе hello.  

**Пример**

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a>Пример JSON: копирование данных из PostgreSQL tooAzure больших двоичных объектов
В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают, как данные toocopy из PostgreSQL базы данных tooAzure хранилища больших двоичных объектов. Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.   

> [!IMPORTANT]
> Этот пример содержит фрагменты кода JSON. Он не включает пошаговые инструкции по созданию фабрики данных hello. Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .

Образец Hello имеет hello, следуя сущностей фабрики данных.

1. Связанная служба типа [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hello [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из результатов запроса в большом двоичном объекте tooa базы данных PostgreSQL каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

В качестве первого шага настройки шлюза управления данными hello. Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.

**Связанная служба PostgreSQL**

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
**Связанная служба хранилища BLOB-объектов Azure**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
**Входной набор данных PostgreSQL**

Образец Hello предполагается создания таблицы «MyTable» в PostgreSQL, и она содержит столбец с именем «timestamp» для временного ряда данных.

Параметр `"external": true` информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
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

**Выходной набор данных BLOB-объекта Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Конвейер с действием копирования**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и выполняется запланированное toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **запроса** свойство выбирает hello данные из таблицы public.usstates hello в базе данных PostgreSQL hello.

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a>Сопоставление типов для PostgreSQL
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статье действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных tooPostgreSQL, hello следующие сопоставления используются из типа too.NET PostgreSQL типа.

| Тип базы данных PostgreSQL | Псевдонимы PostgresSQL | Тип .NET Framework |
| --- | --- | --- |
| abstime | |Datetime | &nbsp;
| bigint |int8 |Int64 |
| bigserial |serial8 |Int64 |
| bit [ (n) ] | |Byte[], String | &nbsp;
| bit varying [ (n) ] |varbit |Byte[], String |
| Логическое |bool |Логическое |
| box | |Byte[], String |&nbsp;
| bytea | |Byte[], String |&nbsp;
| character [ (n) ] |char [ (n) ] |Строка |
| character varying [ (n) ] |varchar [ (n) ] |Строка |
| cid | |Строка |&nbsp;
| cidr | |Строка |&nbsp;
| circle | |Byte[], String |&nbsp;
| дата | |Datetime |&nbsp;
| daterange | |Строка |&nbsp;
| double precision |float8 |Double |
| inet | |Byte[], String |&nbsp;
| intarry | |Строка |&nbsp;
| int4range | |Строка |&nbsp;
| int8range | |Строка |&nbsp;
| целое число |int, int4 |Int32 |
| interval [ fields ] [ (p) ] | |Timespan |&nbsp;
| json | |Строка |&nbsp;
| jsonb | |Byte[] |&nbsp;
| line | |Byte[], String |&nbsp;
| lseg | |Byte[], String |&nbsp;
| macaddr | |Byte[], String |&nbsp;
| money; | |Decimal |&nbsp;
| numeric [ (p, s) ] |decimal [ (p, s) ] |Decimal |
| numrange | |Строка |&nbsp;
| oid | |Int32 |&nbsp;
| path | |Byte[], String |&nbsp;
| pg_lsn | |Int64 |&nbsp;
| point | |Byte[], String |&nbsp;
| polygon | |Byte[], String |&nbsp;
| real; |float4 |Single |
| smallint; |int2 |Int16 |
| smallserial |serial2 |Int16 |
| serial |serial4 |Int32 |
| text | |Строка |&nbsp;

## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
