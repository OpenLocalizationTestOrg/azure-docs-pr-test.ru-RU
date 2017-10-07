---
title: "aaaMove данные из Amazon Simple Storage Service с помощью фабрики данных | Документы Microsoft"
description: "Дополнительные сведения о том, как данные toomove из Amazon Simple Storage Service (S3) с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Перемещение данных из Amazon Simple Storage Service с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello в действии копирования данных toomove фабрики данных Azure из Amazon Simple Storage Service (S3). Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из хранилища Amazon S3 tooany поддерживается приемник данных. Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Фабрика данных в настоящее время поддерживает только перемещения данных из хранилищ данных tooother Amazon S3, но не перемещения данных из других данных хранит tooAmazon S3.

## <a name="required-permissions"></a>Необходимые разрешения
toocopy данные из Amazon S3, убедитесь, что предоставлены следующие разрешения hello:

* `s3:GetObject` и `s3:GetObjectVersion` для операций с объектами Amazon S3.
* `s3:ListBucket` для операций в контейнере Amazon S3. Если вы используете приветствия мастера копирования фабрики данных, `s3:ListAllMyBuckets` также является обязательным.

Дополнительные сведения о hello полный список разрешений Amazon S3 см [указание разрешений в политике](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из источника Amazon S3 с помощью различных средств или API-интерфейсов.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. Краткое пошаговое руководство представлено в разделе [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md).

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. Пошаговые инструкции toocreate конвейер с операции копирования, в разделе hello [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Используется ли инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello:

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств или API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных. Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных Amazon S3 в разделе hello [пример JSON: копирование данных из tooAzure Amazon S3 большого двоичного объекта](#json-example-copy-data-from-amazon-s3-to-azure-blob) этой статьи.

> [!NOTE]
> Подробные сведения о поддерживаемых форматах файлов и сжатия для действия копирования см. в разделе [Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure](data-factory-supported-file-and-compression-formats.md).

Hello в следующих разделах приведены сведения о JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAmazon S3.

## <a name="linked-service-properties"></a>Свойства связанной службы
Связанная служба связывает фабрику данных tooa хранилища данных. Создание связанной службы типа **AwsAccessKey** toolink данных Amazon S3 хранения tooyour фабрики данных. службу описание для конкретных tooAmazon элементы JSON S3 (AwsAccessKey) связан обеспечивает Hello в следующей таблице.

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| accessKeyID |Идентификатор hello доступа секретного ключа. |string |Да |
| secretAccessKey |Hello секретный доступа самого ключа. |Зашифрованная строка секрета |Да |

Пример:

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Свойства набора данных
toospecify dataset toorepresent входные данные в хранилище больших двоичных объектов Azure, задать свойство типа hello hello набора данных, слишком**AmazonS3**. Набор hello **linkedServiceName** toohello имя набора данных hello hello Amazon S3 свойство связанной службы. Полный список разделов и свойств, доступных для определения наборов данных, см. в разделе [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md). 

Разделы structure, availability и policy одинаковы для всех типов наборов данных (таких как базы данных SQL, большие двоичные объекты Azure и таблицы Azure). Hello **typeProperties** разделе отличается для каждого типа набора данных, а также содержит сведения о месте hello hello данных в хранилище данных hello. Hello **typeProperties** раздел для набора данных типа **AmazonS3** (включает набор данных hello Amazon S3) имеет следующие свойства hello:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| bucketName |Имя сегмента Hello S3. |Строка |Да |
| key |ключ объекта Hello S3. |Строка |Нет |
| prefix |Префикс для ключа объекта S3 hello. Выбираются объекты, ключи которых начинаются с этого префикса. Применяется, только если ключ пустой. |string |Нет |
| версия |версия Hello hello S3 объекта, если включено управление версиями S3. |Строка |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделе hello [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формат JSON](data-factory-supported-file-and-compression-formats.md#json-format), [формат Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формат Orc](data-factory-supported-file-and-compression-formats.md#orc-format), и [Parquet формат ](data-factory-supported-file-and-compression-formats.md#parquet-format) разделы. <br><br> Если требуется, чтобы файлы toocopy как — между файловых хранилищ (двоичного копирования), skip hello формат раздела оба определения набора входных и выходных данных. |Нет | |
| compression | Укажите тип hello и уровень сжатия данных hello. Hello поддерживаемые типы: **GZip**, **Deflate**, **BZip2**, и **ZipDeflate**. уровни Hello поддерживается: **оптимальный** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет | |


> [!NOTE]
> **bucketName + клавиша** указывает расположение hello объекта hello S3, где контейнеров — hello корневой контейнер для объектов S3 и ключ — объект toohello S3 hello полный путь.

### <a name="sample-dataset-with-prefix"></a>Пример набора данных с префиксом

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Пример набора данных (с версией)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Динамические пути для S3
Hello предыдущего примера использует фиксированные значения для hello **ключ** и **bucketName** свойства в наборе данных hello Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

Можно настроить фабрику данных для динамического вычисления значений этих свойств во время выполнения с помощью системных переменных, например SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Можно сделать hello одинаково для hello **префикс** свойства набора данных Amazon S3. Список поддерживаемых функций и переменных см. в статье [Функции и системные переменные фабрики данных](data-factory-functions-variables.md).

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойств, доступных для определения действий, см. в разделе [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий. Свойства, доступные в hello **typeProperties** раздел hello действия зависят от типа каждого действия. Для действия копирования hello свойства зависят от типов источников и приемников hello. Если источник в действии копирования hello имеет тип **FileSystemSource** (включая Amazon S3), hello следующие свойства доступны в **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает объекты ли список toorecursively S3 hello в каталоге. |True или false |Нет |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>Пример JSON: копирование данных из tooAzure Amazon S3 хранилища больших двоичных объектов
В этом примере показано, как данные toocopy из tooan Amazon S3 хранилища больших двоичных объектов Azure. Тем не менее, данные можно скопировать непосредственно слишком[любой hello приемников, которые поддерживаются](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью действия копирования hello в фабрике данных.

Образец Hello предоставляет определения JSON для hello, следуя сущностей фабрики данных. Можно использовать эти определения toocreate toocopy конвейера данных из хранилища tooBlob Amazon S3, с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Связанная служба типа [AwsAccessKey](#linked-service-properties).
* Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Входной [набор данных](data-factory-create-datasets.md) типа [AmazonS3](#dataset-properties).
* Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [FileSystemSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из tooan Amazon S3 BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

### <a name="amazon-s3-linked-service"></a>Связанная служба Amazon S3

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Связанная служба хранения Azure

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

### <a name="amazon-s3-input-dataset"></a>Входной набор данных Amazon S3

Установка **«external»: true** информирует служба фабрики данных hello hello набор данных является фабрикой toohello внешних данных. Задайте это свойство tootrue для входного набора данных, который не был создан из действия в конвейере hello.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Выходной набор данных BLOB-объекта Azure

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует hello года, месяца, дня и часа части времени начала hello.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Действие копирования в конвейере с Amazon S3 в качестве источника и BLOB-объектом в качестве приемника

Hello конвейера содержит операции копирования, настроенные toouse hello наборы входных и выходных данных, а — запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**FileSystemSource**, и **приемник** тип установлен слишком**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> разделе toomap столбцы из источника toocolumns набора данных, из набора приемника [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).


## <a name="next-steps"></a>Дальнейшие действия
См. следующие статьи hello.

* toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных и различных способов toooptimize, разделе hello [копирование действия производительности и руководство по настройке](data-factory-copy-activity-performance.md).

* Пошаговые инструкции для создания конвейера с помощью операции копирования см. в разделе hello [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
