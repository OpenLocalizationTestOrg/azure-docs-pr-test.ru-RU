---
title: "aaaMove данных из SAP Business Warehouse, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данных из SAP Business Warehouse, с помощью фабрики данных Azure."
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
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a>Перемещение данных из SAP Business Warehouse с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в данных toomove фабрики данных Azure из локального SAP Business хранилища (BW). Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из локальной SAP Business Warehouse хранилища поддерживается tooany приемник данных хранилища данных. Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Фабрика данных в настоящее время поддерживает только для перемещения данных из объекта данных SAP Business Warehouse tooother хранятся, но не для перемещения данных из других данных хранит tooan SAP Business Warehouse. 

## <a name="supported-versions-and-installation"></a>Поддерживаемые версии и установка
Этот соединитель поддерживает SAP Business Warehouse версии 7.x. Он поддерживает копирование данных из InfoCube и QueryCubes (включая запросы BEx) с помощью запросов многомерных выражений.

tooenable hello подключения toohello экземпляра SAP BW, установите hello следующие компоненты:
- **Шлюз управления данными**: подключение локальной tooon данных поддерживает службы фабрики данных хранилища (включая SAP Business Warehouse) с помощью компонента вызывается шлюз управления данными. toolearn о шлюз управления данными и пошаговые инструкции по настройке шлюза hello. в разделе [перемещение данных между локальными данными хранения хранилища данных toocloud](data-factory-move-data-between-onprem-and-cloud.md) статьи. Требуется использовать шлюз, даже если hello SAP Business Warehouse размещается в Azure IaaS виртуальной машины (VM). Hello шлюз можно установить на hello одной виртуальной Машины как данные hello хранения или же в другой виртуальной Машине, при условии, что шлюз hello могут подключаться toohello базы данных.
- **Библиотека SAP NetWeaver** на компьютере шлюза hello. Библиотека SAP Netweaver hello можно получить у администратора SAP или непосредственно из hello [центра загрузки программного обеспечения SAP](https://support.sap.com/swdc). Поиск hello **&#1025361; Примечание SAP** расположения загрузки hello tooget hello самой последней версии. Убедитесь, что что hello архитектура для библиотеки SAP NetWeaver hello (32-разрядной или 64-разрядной) соответствует установку шлюза. Установите все файлы, включенные в hello SAP NetWeaver RFC SDK соответствующим toohello Примечание SAP. Библиотека SAP NetWeaver Hello также включается в hello установки клиентских средств SAP.

> [!TIP]
> Поместите hello библиотек DLL, извлеченных из hello NetWeaver RFC SDK в папку system32.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API. 

- toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера. 
- Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локальной SAP Business Warehouse см. в разделе [JSON пример: копирование данных из SAP Business Warehouse tooAzure большого двоичного объекта](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) этой статьи. 

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooan SAP BW хранилища данных:

## <a name="linked-service-properties"></a>Свойства связанной службы
Привет, в следующей таблице приводится описание tooSAP службы хранилища предприятия (BW) связаны определенные элементы JSON.

Свойство | Описание | Допустимые значения | Обязательно
-------- | ----------- | -------------- | --------
server | Имя сервера hello, на какие hello SAP BW расположен экземпляр. | string | Да
systemNumber | Номер системы hello системы SAP BW. | Двузначное десятичное число, представленное в виде строки. | Да
clientid | Идентификатор клиента для клиента hello в hello системы SAP-W. | Трехзначное десятичное число, представленное в виде строки. | Да
Имя пользователя | Имя пользователя hello с сервера SAP toohello доступа | string | Да
пароль | Пароль для пользователя hello. | string | Да
gatewayName | Имя шлюза hello, hello служба фабрики данных должна использовать tooconnect toohello локальной SAP BW экземпляр. | string | Да
encryptedCredential | Строка Hello шифрования учетных данных. | string | Нет

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Свойства определенного типа, не поддерживается для набора данных SAP BW hello типа **RelationalTable**. 


## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.

В то время как свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

Если источник в действии копирования имеет тип **RelationalSource** (включает SAP BW), hello следующие свойства доступны в разделе "typeProperties":

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query | Указывает tooread hello многомерных Выражений запроса данных из экземпляра SAP BW hello. | Запрос многомерных выражений. | Да |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a>Пример JSON: копирование данных из SAP Business Warehouse tooAzure больших двоичных объектов
Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). В этом примере показано, как данные toocopy из tooan SAP Business Warehouse локального хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.  

> [!IMPORTANT]
> Этот пример содержит фрагменты кода JSON. Он не включает пошаговые инструкции по созданию фабрики данных hello. Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .

Образец Hello имеет hello, следуя сущностей фабрики данных.

1. Связанная служба типа [SapBw](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из tooan экземпляра SAP Business Warehouse BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

В качестве первого шага настройки шлюза управления данными hello. Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.

### <a name="sap-business-warehouse-linked-service"></a>Связанная служба SAP Business Warehouse
Ссылки на службы связаны toohello данных SAP BW экземпляр фабрики. Hello свойство type установлено слишком**SapBw**. Hello typeProperties раздел содержит сведения о соединении для экземпляра SAP BW hello. 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
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

### <a name="sap-bw-input-dataset"></a>Входной набор данных SAP Business Warehouse
Этот набор данных определяет набор данных SAP Business Warehouse hello. Задание типа hello фабрики данных набора данных hello слишком**RelationalTable**. В настоящее время какие-либо свойства типа для набора данных SAP Business Warehouse не указываются пользователем. запрос Hello в hello определение действия копирования указывает, какие tooread данных из экземпляра SAP BW hello. 

Установка значения внешнего свойства tootrue сообщает hello служба фабрики данных, этой таблицы hello является фабрикой toohello внешних данных и не был создан из действия в фабрике данных hello.

Свойства частоту и интервал определяет расписание hello. В этом случае hello считывании данных из экземпляра SAP BW hello каждый час. 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
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
Этот набор данных определяет hello выходной BLOB-объектов Azure, набор данных. свойство типа Hello задается tooAzureBlob. раздел typeProperties Hello содержит, где хранятся данные hello, скопированные из экземпляра SAP BW hello. Hello записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** (для источника SAP BW) и **приемник** тип установлен слишком**BlobSink**. Hello запрос, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a>Сопоставление типов для SAP Business Warehouse
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных из SAP BW из SAP BW типы too.NET типы используются следующие сопоставления hello.

Тип данных в словаре ABAP hello | Тип данных .NET
-------------------------------- | --------------
ACCP |  int
CHAR | Строка
CLNT | Строка
CURR | Decimal
CUKY | Строка
DEC | Decimal
FLTP | Double
INT1 | Byte
INT2 | Int16
INT4 | int
LANG | Строка
LCHR | string
LRAW | Byte[]
PREC | Int16
QUAN | Decimal
RAW | Byte[]
RAWSTRING | Byte[]
STRING | string
ЕДИНИЦА ИЗМЕРЕНИЯ | Строка
DATS | Строка
NUMC | Строка
TIMS | Строка

> [!NOTE]
> toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).


## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
