---
title: "aaaMove данные из источника HTTP - Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove из локальной или облачной HTTP источника с помощью фабрики данных Azure."
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Перемещение данных из источника HTTP с помощью фабрики данных Azure
В этой статье рассматриваются как hello toouse действие копирования в данных toomove фабрики данных Azure из tooa конечной точки HTTP на локальная/облачная поддерживается приемника хранилища данных. Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, дан обзор перемещения данных на копии действия и hello список хранилищ данных, поддерживаемые в качестве источников и приемников.

Фабрика данных в настоящее время поддерживает только перемещение данных из HTTP источника tooother хранилищ данных, но не перемещения данных из других данных хранит назначения tooan HTTP.

## <a name="supported-scenarios-and-authentication-types"></a>Поддерживаемые сценарии и типы аутентификации
Можно использовать эти данные tooretrieve HTTP соединителя с **облачной и локальной конечной точки HTTP/s** по протоколу HTTP **получить** или **POST** метод. поддерживаются следующие типы проверки подлинности Hello: **Anonymous**, **основные**, **дайджест**, **Windows**, и  **ClientCertificate**. Обратите внимание, hello отличие от этого соединителя hello [соединитель таблицы веб](data-factory-web-table-connector.md) является: hello последний является таблица используется tooextract содержимого с веб-страницы HTML.

При копировании данных из локальной конечной точки HTTP, необходимо установить шлюз управления данными в hello в локальной среде и ВМ Azure. В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из источника HTTP с помощью разных инструментов и интерфейсов API.

- toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

- Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. JSON выбирает toocopy данные из источника HTTP tooAzure хранилища больших двоичных объектов, см. в разделе [JSON примеры](#json-examples) части этой статьи.

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello в следующей таблице приводится описание службы конкретных tooHTTP связанные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type | свойство типа Hello должно быть присвоено: `Http`. | Да |
| url | Базовый URL-адрес toohello веб-сервера | Да |
| authenticationType | Указывает тип проверки подлинности hello. Допустимые значения: **Anonymous**, **Basic**, **Digest**, **Windows** и **ClientCertificate**. <br><br> Относятся toosections под этой таблицей в дополнительные свойства и примерами JSON для этих типов проверки подлинности, соответственно. | Да |
| enableServerCertificateValidation | Укажите ли tooenable сервера SSL сертификата проверки, если источником является HTTPS веб-сервера | Нет. Значение по умолчанию — true. |
| gatewayName | Имя tooan tooconnect шлюз управления данными hello локального источника HTTP. | Да, если копирование выполняется из локального источника HTTP. |
| encryptedCredential | Конечная точка HTTP hello tooaccess зашифрованных учетных данных. Автоматически сгенерированный при настройке hello сведения для проверки подлинности в копирования мастера или hello ClickOnce всплывающее диалоговое окно. | Нет. Применимо, только когда копирование данных выполняется с локального HTTP-сервера. |

В разделе [перемещения данных между локальным источникам и hello облако с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) подробные сведения о задании учетных данных для источника данных соединителя HTTP в локальной среде.

### <a name="using-basic-digest-or-windows-authentication"></a>Использование типов проверки подлинности Basic, Digest или Windows

Задать `authenticationType` как `Basic`, `Digest`, или `Windows`и укажите следующие свойства, кроме hello HTTP соединителя универсального историй, представленные выше hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| Имя пользователя | Конечная точка HTTP hello tooaccess имя пользователя. | Да |
| пароль | Пароль для пользователя hello (имя пользователя). | Да |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Пример: использование типов проверки подлинности Basic, Digest или Windows

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>Использование типа проверки подлинности ClientCertificate

Задайте обычную проверку подлинности toouse `authenticationType` как `ClientCertificate`и укажите следующие свойства, кроме hello HTTP соединителя универсального историй, представленные выше hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| embeddedCertData | Hello кодировке Base64 содержимое двоичных данных hello файл обмена личной информацией (PFX). | Укажите либо hello `embeddedCertData` или `certThumbprint`. |
| certThumbprint | Здравствуйте, отпечаток сертификата hello, который был установлен в хранилище сертификатов на компьютере шлюза. Применимо, только когда копирование данных выполняется из локального источника HTTP. | Укажите либо hello `embeddedCertData` или `certThumbprint`. |
| пароль | Пароль, связанный с сертификатом hello. | Нет |

При использовании `certThumbprint` необходимо для проверки подлинности и hello сертификат должен быть установлен в личном хранилище локального компьютера hello hello, служба шлюза toohello разрешение на чтение hello toogrant:

1. Запустите консоль управления (MMC). Добавить hello **сертификаты** этой цели hello оснастки **локального компьютера**.
2. Разверните **Сертификаты**, **Личные**, а затем щелкните **Сертификаты**.
3. Щелкните правой кнопкой мыши hello сертификат из личного хранилища hello и выберите **все задачи**->**управление закрытыми ключами...**
3. На hello **безопасности** добавьте учетную запись пользователя hello, под которой выполняется служба узла шлюза управления данными с сертификатом toohello hello доступ для чтения.  

#### <a name="example-using-client-certificate"></a>Пример: использование сертификата клиента
Ссылки на службы связанных данных фабрики tooan локальной HTTP веб-сервере. Она использует сертификат клиента, которая устанавливается на компьютере hello с установлен шлюз управления данными.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Пример: использование сертификата клиента в файле
Ссылки на службы связанных данных фабрики tooan локальной HTTP веб-сервере. Он использует файл сертификата клиента на компьютере hello с установлен шлюз управления данными.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных типа **Http** имеет следующие свойства hello

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| type | Указанный тип hello hello набора данных. необходимо задать слишком`Http`. | Да |
| relativeUrl | Относительный URL-адрес toohello ресурс, содержащий данные hello. Если путь не указан, используется только hello URL-адрес, указанный в определении службы hello связаны. <br><br> tooconstruct динамического URL-адреса можно использовать [функции фабрики данных, а системные переменные](data-factory-functions-variables.md), например «relativeUrl»: «$$Text.Format ("/ my/отчета? месяц = {0: yyyy}-{0:MM} & fmt = csv", SliceStart)». | Нет |
| requestMethod | Метод HTTP. Допустимые значения: **GET** или **POST**. | Нет. Значение по умолчанию — `GET`. |
| additionalHeaders | Дополнительные заголовки HTTP-запроса. | Нет |
| requestBody | Текст HTTP-запроса. | Нет |
| свойства | Если требуется toosimply **получения данных hello из конечной точки HTTP-является** без его синтаксического анализа пропустить этот формат параметров. <br><br> Если требуется ответ hello HTTP tooparse содержимого во время копирования, поддерживаются следующие типы формата hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

### <a name="example-using-hello-get-default-method"></a>Пример использования hello метод GET (по умолчанию)

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>Пример: с помощью метода POST hello

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

Свойства, доступные в hello **typeProperties** раздел hello действий на hello другой стороны, зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

В настоящее время, если источник hello в действии копирования имеет тип **HttpSource**, поддерживаются следующие свойства hello.

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- |
| httpRequestTimeout | Здравствуйте, время ожидания (TimeSpan) для hello HTTP tooget ответа для запроса. Это tooget hello время ожидания ответа, не hello время ожидания tooread данные ответа. | Нет. Значение по умолчанию  — 00:01:40. |

## <a name="supported-file-and-compression-formats"></a>Поддерживаемые форматы файлов и сжатия
Дополнительные сведения см. в статье [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).

## <a name="json-examples"></a>Примеры определений JSON
Следующий пример Hello предоставить определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают, как toocopy из HTTP источника tooAzure хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>Пример: Копирование данных из источника HTTP tooAzure хранилища больших двоичных объектов
решение фабрики данных для данного образца Hello содержит hello, следуя фабрики данных сущности:

1. Связанная служба типа [HTTP](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [Http](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [HttpSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из tooan источника HTTP BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

### <a name="http-linked-service"></a>Связанная служба HTTP
В этом примере, что использует hello HTTP связанная служба с анонимной проверкой подлинности. Сведения о возможных типах аутентификации см. в разделе о [связанной службе HTTP](#linked-service-properties).

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

### <a name="http-input-dataset"></a>Входной набор данных HTTP
Установка **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Выходной набор данных BLOB-объекта Azure

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a>Конвейер с действием копирования

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**HttpSource** и **приемник** тип установлен слишком**BlobSink**.

В разделе [HttpSource](#copy-activity-properties) список свойств, поддерживаемых hello HttpSource hello.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
