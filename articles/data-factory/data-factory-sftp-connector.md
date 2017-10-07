---
title: "aaaMove данные из SFTP-сервере, с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из локальной или сервером SFTP облака, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Перемещение данных с SFTP-сервера с использованием фабрики данных Azure
В этой статье рассматриваются как hello toouse действие копирования в данных toomove фабрики данных Azure из tooa сервера на локальные и облачные SFTP поддерживается приемника хранилища данных. Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, дан обзор перемещения данных на копии действия и hello список хранилищ данных, поддерживаемые в качестве источников и приемников.

Фабрика данных в настоящее время поддерживает только для перемещения данных из объекта данных tooother сервера SFTP хранятся, но не для перемещения данных из других данных хранит tooan SFTP-сервере. Она поддерживает локальные и облачные SFTP-серверы.

> [!NOTE]
> Действие копирования не удаляет исходный файл hello после назначения успешно скопированного toohello. Если вам требуется toodelete hello исходного файла после успешным копированием, создайте файл hello toodelete пользовательское действие и действие hello используется в конвейере hello. 

## <a name="supported-scenarios-and-authentication-types"></a>Поддерживаемые сценарии и типы аутентификации
Можно использовать эти данные toocopy SFTP соединителя с **облачные SFTP серверов и локальных серверов SFTP**. **Основные** и **параметры SshPublicKey** , поддерживаются типы проверки подлинности при подключении toohello SFTP-сервере.

При копировании данных из локальной SFTP-сервере, необходимо установить шлюз управления данными в hello в локальной среде и ВМ Azure. В разделе [шлюз управления данными](data-factory-data-management-gateway.md) сведения о шлюзе hello. В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговые инструкции по настройке шлюза hello и его использования.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные с SFTP-сервера с помощью разных инструментов и API-интерфейсов.

- toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

- Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. JSON образцы данных toocopy из tooAzure сервера SFTP хранилища больших двоичных объектов, см. в разделе [пример JSON: копирование данных из большого двоичного объекта tooAzure сервера SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) этой статьи.

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello в следующей таблице приводится описание службы конкретных tooFTP связанные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- | --- |
| type | свойство типа Hello должно быть задано слишком`Sftp`. |Да |
| host | Имя или IP-адрес SFTP-сервере hello. |Да |
| порт |Какие hello SFTP сервера прослушивает порт. значение по умолчанию Hello: 21 |Нет |
| authenticationType |Укажите тип аутентификации. Допустимые значения: **Basic**, **SshPublicKey**. <br><br> См. слишком[использование обычной проверки подлинности](#using-basic-authentication) и [с помощью открытого ключа проверки подлинности SSH](#using-ssh-public-key-authentication) разделы в дополнительные свойства и примерами JSON, соответственно. |Да |
| skipHostKeyValidation | Укажите, размещена ли tooskip ключа проверки. | Нет. Здравствуйте, значение по умолчанию: false |
| hostKeyFingerprint | Укажите отпечаток пальца hello hello узла ключа. | Да, если hello `skipHostKeyValidation` имеет значение toofalse.  |
| gatewayName |Имя tooan tooconnect шлюз управления данными hello локальной SFTP-сервере. | Да, если копирование выполняется с локального SFTP-сервера. |
| encryptedCredential | Сервер SFTP hello tooaccess зашифрованных учетных данных. Формируется автоматически при указании обычной проверки подлинности (имя пользователя + пароль) или параметры SshPublicKey проверки подлинности (имя пользователя + пути закрытого ключа или содержимое) в копирования мастера или hello ClickOnce всплывающее диалоговое окно. | Нет. Применимо, только если копирование выполняется с локального SFTP-сервера. |

### <a name="using-basic-authentication"></a>Использование обычной аутентификации

Задайте обычную проверку подлинности toouse `authenticationType` как `Basic`и укажите следующие свойства, кроме hello SFTP соединителя универсального из них, представленные в последнем разделе hello hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- | --- |
| Имя пользователя | Пользователь, обладающий доступом toohello SFTP-сервере. |Да |
| пароль | Пароль для пользователя hello (имя пользователя). | Да |

#### <a name="example-basic-authentication"></a>Пример обычной аутентификации
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Пример обычной аутентификации с шифрованием учетных данных

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>Использование аутентификации с открытым ключом SSH

задать toouse открытого ключа проверки подлинности SSH, `authenticationType` как `SshPublicKey`и укажите следующие свойства, кроме hello SFTP соединителя универсального из них, представленные в последнем разделе hello hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- | --- |
| Имя пользователя |Пользователь, имеющий доступ toohello SFTP-сервера |Да |
| privateKeyPath | Укажите абсолютный путь toohello можно получить доступ к файлу закрытого ключа этого шлюза. | Укажите либо hello `privateKeyPath` или `privateKeyContent`. <br><br> Применимо, только если копирование выполняется с локального SFTP-сервера. |
| privateKeyContent | Сериализованная строка hello закрытого ключа содержимого. Hello мастер копирования можно считать файл закрытого ключа hello и автоматически извлекать hello закрытого ключа содержимого. При использовании любой другой инструмент и SDK, используйте свойство privateKeyPath hello. | Укажите либо hello `privateKeyPath` или `privateKeyContent`. |
| passPhrase | Укажите фразу пароль toodecrypt hello hello закрытый ключ, если hello файл ключа защищен парольную фразу. | Да, если файл закрытого ключа hello защищен парольную фразу. |

> [!NOTE]
> Соединитель SFTP поддерживает только ключ OpenSSH. Убедитесь, что файл ключа находится в правильном формате hello. Можно использовать средство Putty tooconvert из .ppk tooOpenSSH формата.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>Пример аутентификации с закрытым ключом SSH, для которого указан путь к файлу

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Пример аутентификации с закрытым ключом SSH, для которого указано содержимое

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных.

Hello **typeProperties** раздела отличается для каждого типа набора данных. Он предоставляет сведения о, тип toohello конкретного набора данных. Hello typeProperties статьи для набора данных типа **FileShare** набор данных имеет следующие свойства hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Путь toohello вложенной папкой. Использовать escape-символ "\" для специальных символов в строке приветствия. Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).<br/><br/>Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания. |Да |
| fileName |Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello. Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.<br/><br/>Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате: <br/><br/>Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Нет |
| fileFilter |Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов.<br/><br/>Допустимые значения: `*` (несколько знаков) и `?` (один знак).<br/><br/>Пример 1: `"fileFilter": "*.log"`<br/>Пример 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> Свойство fileFilter применяется к входному набору данных FileShare. HDFS не поддерживает это свойство. |Нет |
| partitionedBy |partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных. Например, путь к папке folderPath каждый час будет другим. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |
| useBinaryTransfer |Укажите, использовать ли режим передачи в двоичном формате. Значение true, если использовать двоичный режим, и false, если ASCII. Значение по умолчанию: True. Это свойство можно использовать, только когда тип связанной службы является FTP-сервер. |Нет |

> [!NOTE]
> Свойства filename и fileFilter нельзя использовать одновременно.

### <a name="using-partionedby-property"></a>Использование свойства partionedBy
Как упоминалось в предыдущем разделе hello, можно указать динамический folderPath, имя файла для временного ряда данных с partitionedBy. Это можно сделать с макросы фабрики данных hello и hello системной переменной SliceStart, SliceEnd, указывающие hello логических период для среза данных.

toolearn о наборы данных для ряда времени, планирования и срезов, в разделе [Создание наборов данных](data-factory-create-datasets.md), [планирования и исполнение](data-factory-scheduling-and-execution.md), и [создания конвейеров](data-factory-create-pipelines.md) статей.

#### <a name="sample-1"></a>Пример 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
В этом примере {Slice} заменяется hello значение системной переменной фабрики данных SliceStart в формате hello (ГГГГММДДЧЧ) указан. Hello SliceStart ссылается toostart время hello среза. Hello folderPath отличается для каждого среза. Например, wikidatagateway/wikisampledataout/2014100103 или wikidatagateway/wikisampledataout/2014100104.

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
В этом примере год, месяц, день и время SliceStart извлекаются в отдельные переменные, используемые в свойствах folderPath и fileName.

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.

В то время как hello свойства раздела typeProperties hello hello действия зависят от типа каждого действия. Для действия копирования hello тип свойства зависят от типов hello источники и приемники.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>Поддерживаемые форматы файлов и сжатия
Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>Пример JSON: Копирование данных из большого двоичного объекта tooAzure сервера SFTP
Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают, как toocopy из SFTP источника tooAzure хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.

> [!IMPORTANT]
> Этот пример содержит фрагменты кода JSON. Он не включает пошаговые инструкции по созданию фабрики данных hello. Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .

Образец Hello имеет hello, следуя сущностей фабрики данных.

* Связанная служба типа [sftp](#linked-service-properties).
* Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Входной [набор данных](data-factory-create-datasets.md) типа [FileShare](#dataset-properties).
* Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из tooan сервера SFTP BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба SFTP**

Этот пример использует обычную проверку подлинности hello с именем пользователя и пароль в виде обычного текста. Также можно использовать один из следующих способов hello:

* обычная аутентификация и шифрование учетных данных;
* Аутентификация с открытым ключом SSH

Сведения о возможных типах аутентификации см. в разделе [Связанная служба FTP](#linked-service-properties).

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Связанная служба хранения Azure**

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
**Входной набор данных SFTP**

Этот набор данных ссылается папки SFTP toohello `mysharedfolder` и файл `test.csv`. конвейер Hello копирует hello файл toohello назначения.

Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Выходной набор данных BLOB-объекта Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource** и **приемник** тип установлен слишком**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.

## <a name="next-steps"></a>Дальнейшие действия
См. следующие статьи hello.

* [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .
