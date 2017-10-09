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
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="d17db-103">Использовать службу импорта и экспорта Azure hello для хранилища Озера данных tooData автономную копию</span><span class="sxs-lookup"><span data-stu-id="d17db-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="d17db-104">В этой статье вы узнаете, как данные огромный toocopy задает (> 200 ГБ) в хранилище Озера данных Azure с помощью методов автономной копии, например hello [службы импорта и экспорта Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="d17db-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="d17db-105">В частности 339,420,860,416 байтов или 319 ГБ на диске используется файл hello в качестве примера в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d17db-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="d17db-106">Давайте назовем этот файл 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="d17db-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="d17db-107">Hello службы импорта и экспорта Azure помогает tootransfer больших объемов данных, более безопасно tooAzure хранилища больших двоичных объектов с жесткого диска доставки дисков tooan центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d17db-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d17db-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d17db-108">Prerequisites</span></span>
<span data-ttu-id="d17db-109">Прежде чем начать, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="d17db-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="d17db-110">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="d17db-110">**An Azure subscription**.</span></span> <span data-ttu-id="d17db-111">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d17db-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d17db-112">**Учетная запись хранения Azure.**</span><span class="sxs-lookup"><span data-stu-id="d17db-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="d17db-113">**Учетная запись Azure Data Lake Store.**</span><span class="sxs-lookup"><span data-stu-id="d17db-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="d17db-114">Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d17db-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="d17db-115">Подготовка данных hello</span><span class="sxs-lookup"><span data-stu-id="d17db-115">Preparing hello data</span></span>
<span data-ttu-id="d17db-116">Перед использованием службы импорта и экспорта hello, передаваемых данных файла разрыв hello toobe **в копии, которые являются менее 200 ГБ** в размере.</span><span class="sxs-lookup"><span data-stu-id="d17db-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="d17db-117">Средство импорта Hello не работает с файлами, больше 200 ГБ.</span><span class="sxs-lookup"><span data-stu-id="d17db-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="d17db-118">В этом учебнике мы разделить hello файл на блоки по 100 ГБ.</span><span class="sxs-lookup"><span data-stu-id="d17db-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="d17db-119">Это можно сделать с помощью [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="d17db-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="d17db-120">Это средство поддерживает команды Linux.</span><span class="sxs-lookup"><span data-stu-id="d17db-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="d17db-121">В этом случае используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d17db-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="d17db-122">Операция split Hello создает файлы с hello следующие имена.</span><span class="sxs-lookup"><span data-stu-id="d17db-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="d17db-123">Подготовка дисков с данными</span><span class="sxs-lookup"><span data-stu-id="d17db-123">Get disks ready with data</span></span>
<span data-ttu-id="d17db-124">Следуйте инструкциям в разделе hello [с помощью службы импорта и экспорта Azure hello](../storage/common/storage-import-export-service.md) (в разделе hello **подготовки дисков** раздел) tooprepare жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="d17db-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="d17db-125">Вот hello общей последовательности:</span><span class="sxs-lookup"><span data-stu-id="d17db-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="d17db-126">Получите жесткого диска, соответствующий toobe требование hello, используемый для hello службы импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="d17db-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="d17db-127">Определите учетную запись хранения Azure, куда будут скопированы hello данных после поставки toohello центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d17db-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="d17db-128">Используйте hello [средство импорта и экспорта Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="d17db-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="d17db-129">Ниже приведен пример фрагмент, который показывает, как toouse hello средство.</span><span class="sxs-lookup"><span data-stu-id="d17db-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="d17db-130">В разделе [с помощью службы импорта и экспорта Azure hello](../storage/common/storage-import-export-service.md) несколько фрагментов образца.</span><span class="sxs-lookup"><span data-stu-id="d17db-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="d17db-131">Hello предыдущая команда создает журнал файла в hello определенное место.</span><span class="sxs-lookup"><span data-stu-id="d17db-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="d17db-132">Используйте этот toocreate файла журнала задания импорта из hello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d17db-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="d17db-133">создание задания импорта;</span><span class="sxs-lookup"><span data-stu-id="d17db-133">Create an import job</span></span>
<span data-ttu-id="d17db-134">Теперь можно создать задание импорта с помощью инструкций hello в [с помощью службы импорта и экспорта Azure hello](../storage/common/storage-import-export-service.md) (в разделе hello **создать задание импорта hello** раздел).</span><span class="sxs-lookup"><span data-stu-id="d17db-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="d17db-135">Для этого задания импорта с другими сведениями, предоставлять hello файл журнала, созданный при подготовке дисков hello.</span><span class="sxs-lookup"><span data-stu-id="d17db-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="d17db-136">Физически переслать диски, hello</span><span class="sxs-lookup"><span data-stu-id="d17db-136">Physically ship hello disks</span></span>
<span data-ttu-id="d17db-137">Теперь можно физически переслать диски hello tooan центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d17db-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="d17db-138">Нет hello данные копируются над большими двоичными объектами toohello хранилища Azure, предоставленный при создании задания импорта hello.</span><span class="sxs-lookup"><span data-stu-id="d17db-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="d17db-139">Кроме того при создании задания hello, если вы выбрали более поздней версии, сведения об отслеживании hello tooprovide теперь можно перейти обратно tooyour импорта задания и обновления hello номер отслеживания.</span><span class="sxs-lookup"><span data-stu-id="d17db-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="d17db-140">Скопировать данные из хранилища Озера данных tooAzure больших двоичных объектов хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="d17db-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="d17db-141">После hello состояние hello задания импорта отображается, его завершения, можно проверить, доступен ли hello данных в больших двоичных объектах hello хранилища Azure, была задана.</span><span class="sxs-lookup"><span data-stu-id="d17db-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="d17db-142">Затем можно использовать различные методы toomove, что данные из hello большие двоичные объекты tooAzure хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="d17db-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="d17db-143">Здравствуйте, все доступные параметры для передачи данных, см. в разделе [принимать данные в хранилище Озера данных](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="d17db-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="d17db-144">В этом разделе мы предоставляют определения JSON hello, toocreate конвейера фабрики данных Azure можно использовать для копирования данных.</span><span class="sxs-lookup"><span data-stu-id="d17db-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="d17db-145">Можно использовать эти определения JSON из hello [портал Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), или [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d17db-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="d17db-146">Связанная служба источника (большой двоичный объект службы хранилища Azure)</span><span class="sxs-lookup"><span data-stu-id="d17db-146">Source linked service (Azure Storage blob)</span></span>
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

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="d17db-147">Связанная служба назначения (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="d17db-147">Target linked service (Azure Data Lake Store)</span></span>
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
### <a name="input-data-set"></a><span data-ttu-id="d17db-148">Входной набор данных</span><span class="sxs-lookup"><span data-stu-id="d17db-148">Input data set</span></span>
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
### <a name="output-data-set"></a><span data-ttu-id="d17db-149">Выходной набор данных</span><span class="sxs-lookup"><span data-stu-id="d17db-149">Output data set</span></span>
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
### <a name="pipeline-copy-activity"></a><span data-ttu-id="d17db-150">Конвейер (действие копирования)</span><span class="sxs-lookup"><span data-stu-id="d17db-150">Pipeline (copy activity)</span></span>
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
<span data-ttu-id="d17db-151">Дополнительные сведения см. в разделе [перемещения данных из хранилища Azure BLOB-объектов с помощью фабрики данных Azure хранилища Озера данных tooAzure](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="d17db-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="d17db-152">Восстановить файлы данных hello в хранилище Озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="d17db-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="d17db-153">Мы начали с файлом, который был 319 ГБ, а было передано его в файлы меньшего размера, чтобы могут быть переданы с помощью службы импорта и экспорта Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d17db-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="d17db-154">Теперь, когда hello данные хранятся в хранилище Озера данных Azure, мы воссоздания hello файл tooits исходный размер.</span><span class="sxs-lookup"><span data-stu-id="d17db-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="d17db-155">Можно использовать hello, поэтому после toodo cmldts Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d17db-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d17db-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d17db-156">Next steps</span></span>
* [<span data-ttu-id="d17db-157">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="d17db-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="d17db-158">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="d17db-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d17db-159">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="d17db-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
