---
title: "aaaCopy данных из Oracle, с помощью фабрики данных | Документы Microsoft"
description: "Узнайте, как toocopy данных из базы данных Oracle, локально с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Копирование данных в локальную базу данных Oracle и обратно с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данные из локальной базы данных Oracle. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.
Можно скопировать данные **из базы данных Oracle** toohello следующие хранилищ данных:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Можно скопировать данные из hello, следуя хранилищ данных **базы данных Oracle tooan**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>Предварительные требования
Фабрика данных поддерживает подключения Oracle tooon локальные источники, с помощью hello шлюз управления данными. В разделе [шлюз управления данными](data-factory-data-management-gateway.md) toolearn статьи о шлюз управления данными и [перемещения данных из локальной toocloud](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговые инструкции по настройке шлюза hello в конвейере данных toomove данные.

Даже если hello Oracle находится в ВМ IaaS Azure требуется шлюз. Hello шлюз можно установить на hello же ВМ IaaS как данные hello хранения или в другой виртуальной Машине, при условии, что шлюз hello подключения toohello базы данных.

> [!NOTE]
> Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).

## <a name="supported-versions-and-installation"></a>Поддерживаемые версии и установка
Этот соединитель Oracle поддерживает две версии драйверов.

- **Драйвер Microsoft для Oracle (рекомендуется)**: начальной из шлюза управления данными версии 2.7, драйвер Microsoft для Oracle автоматически устанавливается вместе с hello шлюза, поэтому не требуется драйвер hello дескриптор tooadditionally в порядке tooOracle tooestablish подключения, а также могут возникать большую производительность копирования при использовании этого драйвера. Ниже перечислены поддерживаемые версии баз данных Oracle.
    - Oracle 12c R1 (12.1)
    - Oracle 11g R1, R2 (11.1, 11.2)
    - Oracle 10g R1, R2 (10.1, 10.2)
    - Oracle 9i R1, R2 (9.0.1, 9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> В настоящее время драйвер Microsoft для Oracle поддерживает только копирование данных из Oracle, но не запись tooOracle. И обратите внимание, что hello тестированию подключения на вкладке диагностику шлюза управления данными не поддерживает этот драйвер. Кроме того можно использовать hello копирования мастера toovalidate hello подключения.
>

- **Поставщик данных Oracle для .NET:** можно также выбрать данные toocopy toouse поставщик данных Oracle из / tooOracle. Входит в состав [компонентов доступа к данным Oracle для Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/). Установите соответствующую версию hello (32 или 64-разрядная версия) на компьютере hello, где установлен шлюз hello. [Поставщик данных Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) можно получить доступ к tooOracle 10 g, выпуск 2 или более поздней версии базы данных.

    При выборе «XCopy Installation», выполните действия в файле readme.htm hello. Мы рекомендуем выбрать hello установщика с пользовательским Интерфейсом (не XCopy один).

    После установки поставщика hello **перезапустите** hello служба узла шлюза управления данными на компьютере с помощью служб приложения (или) диспетчера конфигурации шлюза управления данными.  

При использовании копирования мастера tooauthor hello копирования конвейера тип драйвера hello будет определяется автоматически. Драйвер Майкрософт будет использоваться по умолчанию, если только вы не используете версию шлюза ниже 2.7 или выбрали Oracle в качестве приемника.

## <a name="getting-started"></a>Приступая к работе
Создать конвейер с действием копирования, который перемещает данные из локальной базы данных Oracle или в нее, можно с помощью различных инструментов и интерфейсов API.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **фабрики данных**. Фабрика данных может содержать один или несколько конвейеров. 
2. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных. Например при копировании данных из tooan базы данных Oralce хранилище больших двоичных объектов создается две связанные службы toolink базы данных Oracle и фабрики данных tooyour учетной записи хранилища Azure. Свойства связанной службы, определенные tooOracle см [связанные свойства службы](#linked-service-properties) раздела.
3. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. В примере hello, упомянутые в последнем шаге hello создайте таблице hello toospecify набора данных в базе данных Oracle, содержащий hello входных данных. Создайте другой контейнер больших двоичных объектов dataset toospecify hello и hello папке, содержащей данные hello копируются hello базы данных Oracle. Свойства набора данных, которые являются определенной tooOracle, в разделе [свойства набора данных](#dataset-properties) раздела.
4. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. В примере hello приведенные выше используются OracleSource в BlobSink источника и в приемник для действия копирования hello. Аналогично при копировании из tooOracle хранилища больших двоичных объектов базы данных использовать BlobSource и OracleSink в действии копирования hello. Свойства действия копирования, определенные tooOracle базы данных, в разделе [скопировать свойства действия](#copy-activity-properties) раздела. Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локальной базы данных Oracle см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-oracle-database) этой статьи.

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущности:

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello в следующей таблице приводится описание службы конкретных tooOracle связанные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **OnPremisesOracle** |Да |
| driverType | Указать, какие данные toocopy драйвер toouse из / tooOracle базы данных. Допустимые значения: **Майкрософт** или **ODP** (по умолчанию). Дополнительные сведения о драйверах см. в разделе [Поддерживаемые версии и установка](#supported-versions-and-installation). | Нет |
| connectionString | Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных Oracle toohello tooconnect. | Да |
| gatewayName | Имя шлюза hello, что является toohello tooconnect используется локальный сервер Oracle |Да |

**Пример: использование драйвера Майкрософт**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Пример: использование драйвера ODP**

См. слишком[этот сайт](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) для hello, разрешенные форматы.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Такие разделы, как структура, доступность и политика набора данных JSON, одинаковы для всех видов наборов данных (Oracle, большие двоичные объекты Azure, таблицы Azure и т. д.).

раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. раздел typeProperties Hello для набора данных hello типа OracleTable имеет hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в hello базы данных Oracle, hello связанной службы относится. |Нет (если указан параметр **oracleReaderQuery** объекта **OracleSource**) |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

> [!NOTE]
> Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.

В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

### <a name="oraclesource"></a>OracleSource
В действии копирования, когда источник hello типа **OracleSource** hello следующие свойства доступны в **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| oracleReaderQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, select * from MyTable <br/><br/>Если не указан, hello в инструкции SQL, выполняемой: выберите * from MyTable |Нет (если для свойства **tableName** задано значение **dataset**). |

### <a name="oraclesink"></a>OracleSink
**OracleSink** поддерживает hello следующие свойства:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| writeBatchTimeout |Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |
| writeBatchSize |Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello. |Целое число (количество строк) |Нет (значение по умолчанию — 100) |
| sqlWriterCleanupScript |Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез. |Инструкция запроса. |Нет |
| sliceIdentifierColumnName |Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения. |Имя столбца с типом данных binary(32). |Нет |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>Примеры JSON для копирования данных tooand из базы данных Oracle
Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают как toocopy данные из / tooan Oracle база данных из хранилища больших двоичных объектов. Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>Пример: Копирование данных из Oracle tooAzure больших двоичных объектов

Образец Hello имеет hello, следуя сущностей фабрики данных.

1. Связанная служба типа [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) в качестве источника и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) в качестве приемника.

Образец Hello копирует данные из таблицы в локальной базы данных Oracle tooa blob каждый час. Дополнительные сведения о различных свойств, используемых в образце hello см. в документации в разделах, следующие примеры hello.

**Связанная служба Oracle**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
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
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Входной набор данных Oracle**

Образец Hello предполагается создания таблицы «MyTable» в Oracle, и она содержит столбец с именем «timestampcolumn» для временного ряда данных.

Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

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

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и выполняется запланированное toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**OracleSource** и **приемник** тип установлен слишком**BlobSink**.  запрос SQL Hello, указанный с **oracleReaderQuery** свойство выбирает данные hello в hello за час toocopy.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>Пример: Копирование данных из tooOracle больших двоичных объектов Azure
В этом примере показано, как toocopy данных из хранилища больших двоичных объектов tooan в локальной базе данных Oracle. Тем не менее, данные можно скопировать **непосредственно** из любого из указанных источников hello [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.  

Образец Hello имеет hello, следуя сущностей фабрики данных.

1. Связанная служба типа [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) в качестве источника и [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) в качестве приемника.

Образец Hello копирует данные из таблицы tooa большого двоичного объекта в базе данных Oracle в локальной каждый час. Дополнительные сведения о различных свойств, используемых в образце hello см. в документации в разделах, следующие примеры hello.

**Связанная служба Oracle**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
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
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Входной набор данных BLOB-объекта Azure**

Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1). Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello. «external»: параметр «true» уведомляет службу hello фабрики данных, что эта таблица является внешней toohello фабрики данных и не был создан из действия в фабрике данных hello.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

**Выходной набор данных Oracle**

Образец Hello предполагается, что вы создали таблицу «MyTable» в Oracle. Создать таблицу hello в Oracle с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов. Новые строки добавляются в таблицу toohello каждый час.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**Конвейер с действием копирования**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и hello **приемник** тип установлен слишком**OracleSink**.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>Советы по устранению неполадок
### <a name="problem-1-net-framework-data-provider"></a>Проблема 1: поставщик данных .NET Framework

Вы видите следующее hello **сообщение об ошибке**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**Возможные причины:**

1. Hello поставщик данных .NET Framework для Oracle не установлен.
2. Hello поставщик данных .NET Framework для Oracle не установленных too.NET Framework 2.0 и не найден в папках hello .NET Framework 4.0.

**Решение:**

1. Если вы не установили hello поставщика .NET для Oracle, [установить его](http://www.oracle.com/technetwork/topics/dotnet/downloads/) и повторите сценарий hello.
2. Если появляется сообщение об ошибке hello даже после установки поставщика hello, hello следующие действия:
   1. Открытие файла конфигурации компьютера .NET 2.0 папки hello: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.
   2. Поиск **поставщик данных Oracle для .NET**, и должен быть доступ toofind запись, как показано в следующий пример в разделе hello **system.data** -> **DbProviderFactories**: «<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Поставщик данных oracle для .NET" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />”
3. Скопируйте этот файл machine.config toohello записи в следующие папки v4.0 hello: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config и too4.xxx.x.x версии изменение hello.
4. Установить «< путь к установленному ODP.NET > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll» в hello глобальный кэш сборок (GAC), запустив `gacutil /i [provider path]`. ## Советы по устранению неполадок

### <a name="problem-2-datetime-formatting"></a>Проблема 2: формат даты и времени

Вы видите следующее hello **сообщение об ошибке**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**Решение:**

Строка запроса hello tooadjust может потребоваться в зависимости настройки даты в базе данных Oracle, как показано в следующих hello действие копирования (используя функцию to_date hello) Пример:

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Сопоставление типов для Oracle
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статье действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных из Oracle, hello следующие сопоставления используются типа too.NET тип данных Oracle и наоборот.

| Тип данных Oracle | Тип данных платформы .NET |
| --- | --- |
| BFILE |Byte[] |
| BLOB |Byte[] |
| CHAR |Строка |
| CLOB |Строка |
| DATE |DateTime |
| FLOAT |десятичное число, строка (если точность больше 28) |
| INTEGER |десятичное число, строка (если точность больше 28) |
| ИНТЕРВАЛ tooMONTH год |Int32 |
| ДЕНЬ tooSECOND ИНТЕРВАЛ |TimeSpan |
| LONG |Строка |
| LONG RAW |Byte[] |
| NCHAR |Строка |
| NCLOB |Строка |
| NUMBER |десятичное число, строка (если точность больше 28) |
| NVARCHAR2 |Строка |
| RAW |Byte[] |
| ROWID |Строка |
| TIMESTAMP |DateTime |
| TIMESTAMP WITH LOCAL TIME ZONE |DateTime |
| TIMESTAMP WITH TIME ZONE |DateTime |
| UNSIGNED INTEGER |NUMBER |
| VARCHAR2 |Строка |
| XML |Строка |

> [!NOTE]
> Тип данных **tooMONTH ИНТЕРВАЛ года** и **tooSECOND ИНТЕРВАЛ день** не поддерживаются при использовании драйвера Microsoft.

## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
