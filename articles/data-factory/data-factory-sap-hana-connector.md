---
title: "aaaMove данных из SAP HANA, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данных из SAP HANA, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a>Перемещение данных из SAP HANA с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в данных toomove фабрики данных Azure с локальным SAP HANA. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из локальной SAP HANA хранилища поддерживается tooany приемник данных хранилища данных. Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Фабрика данных в настоящее время поддерживает только для перемещения хранятся данные из объекта данных SAP HANA tooother, но не для перемещения данных из других данных хранит tooan SAP HANA.

## <a name="supported-versions-and-installation"></a>Поддерживаемые версии и установка
Этот соединитель поддерживает все версии базы данных SAP HANA. Он поддерживает копирование данных из информационных моделей HANA (например, представлений Analytic и Calculation) и таблиц со строками и столбцами с помощью SQL-запросов.

tooenable hello подключения toohello экземпляра SAP HANA, установите hello следующие компоненты:
- **Шлюз управления данными**: подключение локальной tooon данных поддерживает службы фабрики данных хранилища (включая SAP HANA) с помощью компонента вызывается шлюз управления данными. toolearn о шлюз управления данными и пошаговые инструкции по настройке шлюза hello. в разделе [перемещение данных между локальными данными хранения хранилища данных toocloud](data-factory-move-data-between-onprem-and-cloud.md) статьи. Требуется использовать шлюз, даже если hello SAP HANA размещается в Azure IaaS виртуальной машины (VM). Hello шлюз можно установить на hello одной виртуальной Машины как данные hello хранения или же в другой виртуальной Машине, при условии, что шлюз hello могут подключаться toohello базы данных.
- **Драйвер SAP HANA ODBC** на компьютере шлюза hello. Можно загрузить драйвер SAP HANA ODBC hello hello [центра загрузки программного обеспечения SAP](https://support.sap.com/swdc). Поиска с ключевым словом hello **SAP HANA КЛИЕНТА для Windows**. 

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API. 

- toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера. 
- Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из SAP HANA в локальной среде, см. [пример JSON: копирование данных из SAP HANA tooAzure больших двоичных объектов](#json-example-copy-data-from-sap-hana-to-azure-blob) данной статьи. 

Hello в следующих разделах подробно свойства JSON, хранилище данных SAP HANA tooan определенных сущностей используется toodefine фабрики данных:

## <a name="linked-service-properties"></a>Свойства связанной службы
в следующей таблице Hello предоставляет описание tooSAP HANA определенные элементы JSON связанной службы.

Свойство | Описание | Допустимые значения | Обязательно
-------- | ----------- | -------------- | --------
server | Имя сервера hello, на какие hello SAP HANA расположен экземпляр. Если ваш сервер использует настроенный порт, укажите `server:port`. | строка | Да
authenticationType | Тип проверки подлинности. | string. Basic или Windows. | Да 
Имя пользователя | Имя пользователя hello с сервера SAP toohello доступа | string | Да
пароль | Пароль для пользователя hello. | string | Да
gatewayName | Имя шлюза hello, hello служба фабрики данных должна использовать tooconnect toohello локальной SAP HANA экземпляр. | string | Да
encryptedCredential | Строка Hello шифрования учетных данных. | string | Нет

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Свойства конкретного типа, не поддерживается для набора данных SAP HANA hello типа **RelationalTable**. 


## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.

В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

Если источник в действии копирования имеет тип **RelationalSource** (включает SAP HANA), hello следующие свойства доступны в разделе "typeProperties":

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query | Указывает tooread hello SQL запроса данных из экземпляра SAP HANA hello. | SQL-запрос. | Да |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a>Пример JSON: копирование данных из SAP HANA tooAzure больших двоичных объектов
Hello следующий пример предоставляет образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). В этом примере показано, как данные toocopy из tooan SAP HANA локального хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** tooany приемников hello в списке [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.  

> [!IMPORTANT]
> Этот пример содержит фрагменты кода JSON. Он не включает пошаговые инструкции по созданию фабрики данных hello. Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .

Образец Hello имеет hello, следуя сущностей фабрики данных.

1. Связанная служба типа [SapHana](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из tooan экземпляра SAP HANA BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

В качестве первого шага настройки шлюза управления данными hello. Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.

### <a name="sap-hana-linked-service"></a>Связанная служба SAP HANA
Ссылки на службы связаны toohello данных SAP HANA экземпляр фабрики. Hello свойство type установлено слишком**SapHana**. Hello typeProperties раздел содержит сведения о соединении для экземпляра SAP HANA hello.

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a>Связанная служба хранения Azure
Ссылки на службы связаны фабрики данных toohello учетной записи хранилища Azure. Hello свойство type установлено слишком**AzureStorage**. Hello typeProperties раздел содержит сведения о соединении для hello учетной записи хранилища Azure.

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="sap-hana-input-dataset"></a>Входной набор данных SAP HANA

Этот набор данных определяет набор данных SAP HANA hello. Задание типа hello фабрики данных набора данных hello слишком**RelationalTable**. В настоящее время какие-либо свойства типа для набора данных SAP HANA не указываются пользователем. запрос Hello в hello определение действия копирования указывает, какие tooread данных из экземпляра SAP HANA hello. 

Установка значения внешнего свойства tootrue сообщает hello служба фабрики данных, этой таблицы hello является фабрикой toohello внешних данных и не был создан из действия в фабрике данных hello.

Свойства частоту и интервал определяет расписание hello. В этом случае hello считывании данных из экземпляра SAP HANA hello каждый час. 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a>Выходной набор данных BLOB-объекта Azure
Этот набор данных определяет hello выходной BLOB-объектов Azure, набор данных. свойство типа Hello задается tooAzureBlob. раздел typeProperties Hello содержит, где хранятся данные hello, скопированные из экземпляра SAP HANA hello. Hello записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>Конвейер с действием копирования

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** (для источника SAP HANA) и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a>Сопоставление типов для SAP HANA
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных из SAP HANA из SAP HANA типы too.NET типы используются следующие сопоставления hello.

Тип SAP HANA | Тип данных на основе .NET
------------- | ---------------
TINYINT | Byte
SMALLINT | Int16
INT | Int32
BIGINT | Int64
REAL | Single
DOUBLE | Single
DECIMAL | Decimal
BOOLEAN | Byte
VARCHAR | string
NVARCHAR | Строка
CLOB | Byte[]
ALPHANUM | string
BLOB | Byte[]
DATE | DateTime
TIME | Интервал времени
TIMESTAMP | DateTime
SECONDDATE | DateTime

## <a name="known-limitations"></a>Известные ограничения
Существует несколько известных ограничений, действующих при копировании данных из SAP HANA.

- Строки NVARCHAR, усеченных toomaximum длиной 4000 символов Юникода
- SMALLDECIMAL не поддерживается.
- VARBINARY не поддерживается.
- Допустимый диапазон дат: 30.12.1899–31.12.9999.

## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
