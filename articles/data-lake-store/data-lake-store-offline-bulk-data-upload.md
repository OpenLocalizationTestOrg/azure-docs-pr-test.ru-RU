---
title: "aaaUpload больших объемов данных в хранилище Озера данных с помощью автономного методов | Документы Microsoft"
description: "Используйте hello AdlCopy средство toocopy данных из хранилища Azure BLOB-объектов хранилища Озера tooData"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Использовать службу импорта и экспорта Azure hello для хранилища Озера данных tooData автономную копию
В этой статье вы узнаете, как данные огромный toocopy задает (> 200 ГБ) в хранилище Озера данных Azure с помощью методов автономной копии, например hello [службы импорта и экспорта Azure](../storage/common/storage-import-export-service.md). В частности 339,420,860,416 байтов или 319 ГБ на диске используется файл hello в качестве примера в этой статье. Давайте назовем этот файл 319GB.tsv.

Hello службы импорта и экспорта Azure помогает tootransfer больших объемов данных, более безопасно tooAzure хранилища больших двоичных объектов с жесткого диска доставки дисков tooan центра обработки данных Azure.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать, необходимо иметь следующие hello.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись хранения Azure.**
* **Учетная запись Azure Data Lake Store.** Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Подготовка данных hello
Перед использованием службы импорта и экспорта hello, передаваемых данных файла разрыв hello toobe **в копии, которые являются менее 200 ГБ** в размере. Средство импорта Hello не работает с файлами, больше 200 ГБ. В этом учебнике мы разделить hello файл на блоки по 100 ГБ. Это можно сделать с помощью [Cygwin](https://cygwin.com/install.html). Это средство поддерживает команды Linux. В этом случае используйте hello следующую команду:

    split -b 100m 319GB.tsv

Операция split Hello создает файлы с hello следующие имена.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Подготовка дисков с данными
Следуйте инструкциям в разделе hello [с помощью службы импорта и экспорта Azure hello](../storage/common/storage-import-export-service.md) (в разделе hello **подготовки дисков** раздел) tooprepare жестких дисков. Вот hello общей последовательности:

1. Получите жесткого диска, соответствующий toobe требование hello, используемый для hello службы импорта и экспорта Azure.
2. Определите учетную запись хранения Azure, куда будут скопированы hello данных после поставки toohello центра обработки данных Azure.
3. Используйте hello [средство импорта и экспорта Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), программы командной строки. Ниже приведен пример фрагмент, который показывает, как toouse hello средство.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    В разделе [с помощью службы импорта и экспорта Azure hello](../storage/common/storage-import-export-service.md) несколько фрагментов образца.
4. Hello предыдущая команда создает журнал файла в hello определенное место. Используйте этот toocreate файла журнала задания импорта из hello [классический портал Azure](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>создание задания импорта;
Теперь можно создать задание импорта с помощью инструкций hello в [с помощью службы импорта и экспорта Azure hello](../storage/common/storage-import-export-service.md) (в разделе hello **создать задание импорта hello** раздел). Для этого задания импорта с другими сведениями, предоставлять hello файл журнала, созданный при подготовке дисков hello.

## <a name="physically-ship-hello-disks"></a>Физически переслать диски, hello
Теперь можно физически переслать диски hello tooan центра обработки данных Azure. Нет hello данные копируются над большими двоичными объектами toohello хранилища Azure, предоставленный при создании задания импорта hello. Кроме того при создании задания hello, если вы выбрали более поздней версии, сведения об отслеживании hello tooprovide теперь можно перейти обратно tooyour импорта задания и обновления hello номер отслеживания.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Скопировать данные из хранилища Озера данных tooAzure больших двоичных объектов хранилища Azure
После hello состояние hello задания импорта отображается, его завершения, можно проверить, доступен ли hello данных в больших двоичных объектах hello хранилища Azure, была задана. Затем можно использовать различные методы toomove, что данные из hello большие двоичные объекты tooAzure хранилища Озера данных. Здравствуйте, все доступные параметры для передачи данных, см. в разделе [принимать данные в хранилище Озера данных](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

В этом разделе мы предоставляют определения JSON hello, toocreate конвейера фабрики данных Azure можно использовать для копирования данных. Можно использовать эти определения JSON из hello [портал Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), или [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Связанная служба источника (большой двоичный объект службы хранилища Azure)
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a>Связанная служба назначения (Azure Data Lake Store)
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a>Входной набор данных
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a>Выходной набор данных
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a>Конвейер (действие копирования)
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
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
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
Дополнительные сведения см. в разделе [перемещения данных из хранилища Azure BLOB-объектов с помощью фабрики данных Azure хранилища Озера данных tooAzure](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Восстановить файлы данных hello в хранилище Озера данных Azure
Мы начали с файлом, который был 319 ГБ, а было передано его в файлы меньшего размера, чтобы могут быть переданы с помощью службы импорта и экспорта Azure hello. Теперь, когда hello данные хранятся в хранилище Озера данных Azure, мы воссоздания hello файл tooits исходный размер. Можно использовать hello, поэтому после toodo cmldts Azure PowerShell.

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a>Дальнейшие действия
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
