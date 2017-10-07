---
title: "aaaMove данные из FTP-сервера с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о данных toomove с FTP-сервера, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Перемещение данных с FTP-сервера с использованием фабрики данных Azure
В этой статье объясняется, как toouse hello в действии копирования данных toomove фабрики данных Azure из FTP-сервера. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из хранилища данных приемник tooany поддерживается сервера FTP. Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Фабрика данных в настоящее время поддерживает только хранит перемещение данных из объекта данных tooother сервера FTP, но не перемещения данных из других данных хранит tooan FTP-сервера. Она поддерживает локальные и облачные FTP-серверы.

> [!NOTE]
> Действие копирования Hello не удаляет исходный файл hello после назначения успешно скопированного toohello. Если вам требуется toodelete hello исходного файла после успешным копированием, создайте файл hello toodelete пользовательского действия и использовать действие hello в конвейере hello. 

## <a name="enable-connectivity"></a>Включение соединения
При перемещении данных из **локальной** FTP сервера tooa Облачное хранилище данных (например, tooAzure хранилища больших двоичных объектов), установить и использовать шлюз управления данными. Hello шлюз управления данными — это агент клиента, который установлен на локальном компьютере и позволяет облачных служб tooconnect tooan локального ресурса. Подробные сведения см. в разделе [Шлюз управления данными](data-factory-data-management-gateway.md). Пошаговые инструкции по настройке шлюза hello и его использования см. в разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md). Hello tooconnect tooan FTP шлюза, использовать, даже если hello server в Azure инфраструктуры как услуги (IaaS) виртуальной машины (VM).

Он служит шлюзом hello возможных tooinstall hello же на локальный компьютер или ВМ IaaS как hello FTP-сервера. Тем не менее рекомендуется установить шлюз hello на отдельный компьютер или ВМ IaaS конкуренцию за ресурсы tooavoid и для повышения производительности. При установке шлюза hello на отдельном компьютере hello машина должна была может tooaccess hello FTP-сервера.

## <a name="get-started"></a>Начало работы
Вы можете создать конвейер с действием копирования, который перемещает данные с исходного FTP-сервера, с помощью разных средств или интерфейсов API.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования фабрики данных**. Краткое пошаговое руководство представлено в статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md).

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **PowerShell**, **шаблона Azure Resource Manager**, **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.

Используется ли hello инструменты или интерфейсы API, выполните следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств или API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных. Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных FTP см. в разделе hello [JSON. Пример: копирование данных из большого двоичного объекта tooAzure сервера FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) этой статьи.

> [!NOTE]
> Дополнительные сведения о поддерживаемых сжатие файлов и форматы toouse см [сжатие файлов и форматы в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md).

Hello в следующих разделах приведены сведения о JSON свойства, которые являются определенной tooFTP используется toodefine фабрики данных сущности.

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello в следующей таблице описываются JSON элементов определенного tooan связанные службы FTP.

| Свойство | Описание | Обязательно | значение по умолчанию |
| --- | --- | --- | --- |
| type |Задайте этот tooFtpServer. |Да |&nbsp; |
| host |Укажите hello имя или IP-адрес сервера FTP hello. |Да |&nbsp; |
| authenticationType |Укажите тип проверки подлинности hello. |Да |Обычная, анонимная |
| Имя пользователя |Укажите hello пользователя, имеющего доступ toohello FTP-сервера. |Нет |&nbsp; |
| пароль |Укажите пароль hello hello пользователя (имя пользователя). |Нет |&nbsp; |
| encryptedCredential |Укажите tooaccess hello FTP hello зашифрованные учетные данные сервера. |Нет |&nbsp; |
| gatewayName |Укажите имя шлюза hello hello в шлюз управления данными tooconnect tooan локальной для FTP-сервера. |Нет |&nbsp; |
| порт |Укажите порт hello какие hello FTP прослушивает сервер. |Нет |21 |
| enableSsl |Укажите, является ли toouse FTP через канал SSL/TLS. |Нет |Да |
| enableServerCertificateValidation |Укажите, является ли сервер tooenable SSL проверку сертификата при использовании FTP по каналу SSL/TLS. |Нет |Да |

### <a name="use-anonymous-authentication"></a>Использование анонимной проверки подлинности

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Использование имени пользователя и пароля в виде обычного текста для обычной проверки подлинности

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Использование свойств port, enableSsl, enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>Использование свойства encryptedCredential для проверки подлинности и шлюза

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойств, доступных для определения наборов данных, см. в разделе [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md). Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.

Hello **typeProperties** раздела отличается для каждого типа набора данных. Он предоставляет сведения о, тип toohello конкретного набора данных. Hello **typeProperties** раздел для набора данных типа **FileShare** имеет hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Папка toohello вложенным. Использовать escape-символ "\" для специальных символов в строке приветствия. Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).<br/><br/>Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза начальных и конечных дат. |Да |
| fileName |Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello. Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.<br/><br/>Когда **fileName** для не указан выходной набор данных hello hello созданный файл имеет имя в hello следующий формат: <br/><br/>Data.<Guid>.txt (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Нет |
| fileFilter |Укажите фильтр toobe используется tooselect подмножества файлов в hello **folderPath**, а не все файлы.<br/><br/>Допустимые значения: `*` (несколько знаков) и `?` (один знак).<br/><br/>Пример 1: `"fileFilter": "*.log"`<br/>Пример 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> Свойство **fileFilter** применяется ко входному набору данных FileShare. Распределенная файловая система Hadoop (HDFS) не поддерживает это свойство. |Нет |
| partitionedBy |Использовать динамический toospecify **folderPath** и **fileName** для временного ряда данных. Например, можно указать **путь к папке**, который будет параметризироваться для данных за каждый час. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделе hello [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формат Json](data-factory-supported-file-and-compression-formats.md#json-format), [формат Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формат Orc](data-factory-supported-file-and-compression-formats.md#orc-format), и [Parquet формат ](data-factory-supported-file-and-compression-formats.md#parquet-format) разделы. <br><br> Если нужно toocopy файлы, как они находятся в диапазоне от файловых хранилищ (двоичный копия), пропустите hello формат раздела оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |
| useBinaryTransfer |Укажите toouse hello двоичный режим передачи. Hello значениями являются true для двоичном режиме (это значение по умолчанию hello) и значение false для ASCII. Это свойство может использоваться, только если hello типа связанного связанной службы типа: FTP-сервер. |Нет |

> [!NOTE]
> Свойства **fileName** и **fileFilter** нельзя использовать одновременно.

### <a name="use-hello-partionedby-property"></a>Используйте свойство partionedBy hello
Как упоминалось в предыдущем разделе hello, можно указать динамический **folderPath** и **fileName** для временного ряда данных с hello **partitionedBy** свойство.

toolearn о наборы данных для ряда времени, планирования и срезов, в разделе [Создание наборов данных](data-factory-create-datasets.md), [планирования и выполнения](data-factory-scheduling-and-execution.md), и [Создание конвейеры](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Пример 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
В этом примере {Slice} заменяется hello значение системной переменной фабрики данных SliceStart, в hello форматирования заданного (ГГГГММДДЧЧ). Hello SliceStart ссылается toostart время hello среза. путь к папке Hello отличается для каждого среза. (Пример: wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.)

#### <a name="sample-2"></a>Пример 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
В этом примере hello год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые hello **folderPath** и **fileName** свойства.

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойств, доступных для определения действий, см. в разделе [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.

Свойства, доступные в hello **typeProperties** раздел Здравствуйте действия на hello другой стороны, могут различаться для каждого типа действия. Для действия копирования hello hello тип свойства зависят от типов hello источники и приемники.

В действии копирования, когда источник hello типа **FileSystemSource**, hello следующие свойства доступны в **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данные из вложенных папок hello, или только из указанной папки hello. |True, False (по умолчанию) |Нет |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>Пример JSON: копирование данных из сервера FTP tooAzure больших двоичных объектов
В этом примере показано, как данные toocopy из tooAzure сервера FTP хранилища больших двоичных объектов. Тем не менее, данные можно скопировать непосредственно tooany из hello приемники уже говорилось в hello [поддерживаемых хранилищ данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats), с помощью действия копирования hello в фабрике данных.  

Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Связанная служба типа [FtpServer](#linked-service-properties)
* Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties)
* Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

Образец Hello копирует данные из tooan сервера FTP BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

### <a name="ftp-linked-service"></a>Связанная служба FTP

Этот пример использует обычную проверку подлинности с hello имя пользователя и пароль в виде обычного текста. Также можно использовать один из следующих способов hello:

* анонимная аутентификация;
* обычная аутентификация и шифрование учетных данных;
* FTP через SSL или TLS (FTPS).

В разделе hello [FTP связанная служба](#linked-service-properties) раздел для различных типов проверки подлинности, можно использовать.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Связанная служба хранения Azure

```JSON
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
### <a name="ftp-input-dataset"></a>Входной набор данных FTP

Этот набор данных указывает папку toohello FTP `mysharedfolder` и файл `test.csv`. конвейер Hello копирует hello файл toohello назначения.

Установка **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Выходной набор данных BLOB-объекта Azure

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется, на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует hello года, месяца, дня и часа части времени начала hello.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Действие копирования в конвейере с файловой системой в качестве источника и BLOB-объектом в качестве приемника

Hello конвейера содержит операции копирования, настроенные toouse hello наборы входных и выходных данных, а — запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource**и hello **приемник** тип установлен слишком**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="next-steps"></a>Дальнейшие действия
См. следующие статьи hello.

* toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных и различных способов toooptimize, разделе hello [копирование действия производительности и руководство по настройке](data-factory-copy-activity-performance.md).

* Пошаговые инструкции для создания конвейера с помощью операции копирования см. в разделе hello [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
