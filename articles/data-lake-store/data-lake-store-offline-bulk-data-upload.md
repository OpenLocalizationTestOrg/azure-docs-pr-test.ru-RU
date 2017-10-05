---
title: "Отправка больших объемов данных в Data Lake Store автономными методами | Документация Майкрософт"
description: "Использование средства AdlCopy для копирования данных из больших двоичных объектов хранилища Azure в Data Lake Store"
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
ms.openlocfilehash: b469c0ebe9838a1ea986cff3043e3008941e9aa9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-importexport-service-for-offline-copy-of-data-to-data-lake-store"></a><span data-ttu-id="fc46f-103">Использование службы импорта и экспорта Azure для автономного копирования данных в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fc46f-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span></span>
<span data-ttu-id="fc46f-104">В этой статье вы узнаете о том, как скопировать огромные наборы данных (> 200 ГБ) в Azure Data Lake Store, используя методы автономного копирования, такие как [служба импорта и экспорта Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="fc46f-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="fc46f-105">В частности, в качестве примера в этой статье используется файл размером 339 420 860 416 байт, т. е. 319 ГБ на диске.</span><span class="sxs-lookup"><span data-stu-id="fc46f-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="fc46f-106">Давайте назовем этот файл 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="fc46f-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="fc46f-107">Служба импорта и экспорта Azure позволяет безопасно переносить большие объемы данных в хранилище BLOB-объектов Azure, отправляя жесткие диски в центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fc46f-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc46f-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fc46f-108">Prerequisites</span></span>
<span data-ttu-id="fc46f-109">Перед началом работы убедитесь, что у вас есть такие компоненты.</span><span class="sxs-lookup"><span data-stu-id="fc46f-109">Before you begin, you must have the following:</span></span>

* <span data-ttu-id="fc46f-110">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="fc46f-110">**An Azure subscription**.</span></span> <span data-ttu-id="fc46f-111">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc46f-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fc46f-112">**Учетная запись хранения Azure.**</span><span class="sxs-lookup"><span data-stu-id="fc46f-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="fc46f-113">**Учетная запись Azure Data Lake Store.**</span><span class="sxs-lookup"><span data-stu-id="fc46f-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="fc46f-114">Инструкции по созданию учетной записи см. в статье [Начало работы с Azure Data Lake Store с помощью портала Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fc46f-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-the-data"></a><span data-ttu-id="fc46f-115">Подготовка данных</span><span class="sxs-lookup"><span data-stu-id="fc46f-115">Preparing the data</span></span>
<span data-ttu-id="fc46f-116">Перед использованием службы импорта и экспорта необходимо разделить передаваемый файл данных на **копии, размер которых не превышает 200 ГБ**.</span><span class="sxs-lookup"><span data-stu-id="fc46f-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="fc46f-117">Это нужно сделать, так как инструмент для импорта не работает с файлами, размер которых превышает 200 ГБ.</span><span class="sxs-lookup"><span data-stu-id="fc46f-117">The import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="fc46f-118">В этом руководстве мы разделим файл на блоки по 100 ГБ.</span><span class="sxs-lookup"><span data-stu-id="fc46f-118">In this tutorial, we split the file into chunks of 100 GB each.</span></span> <span data-ttu-id="fc46f-119">Это можно сделать с помощью [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="fc46f-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="fc46f-120">Это средство поддерживает команды Linux.</span><span class="sxs-lookup"><span data-stu-id="fc46f-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="fc46f-121">Воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="fc46f-121">In this case, use the following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="fc46f-122">Операция Split создает файлы с именами, указанными ниже.</span><span class="sxs-lookup"><span data-stu-id="fc46f-122">The split operation creates files with the following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="fc46f-123">Подготовка дисков с данными</span><span class="sxs-lookup"><span data-stu-id="fc46f-123">Get disks ready with data</span></span>
<span data-ttu-id="fc46f-124">Для подготовки жестких дисков следуйте инструкциям в статье [Использование службы импорта и экспорта Azure для передачи данных в хранилище BLOB-объектов](../storage/common/storage-import-export-service.md) в подразделе **Подготовка дисков**.</span><span class="sxs-lookup"><span data-stu-id="fc46f-124">Follow the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span></span> <span data-ttu-id="fc46f-125">Вот общая последовательность действий:</span><span class="sxs-lookup"><span data-stu-id="fc46f-125">Here's the overall sequence:</span></span>

1. <span data-ttu-id="fc46f-126">Приобретите жесткий диск, который отвечает требованиям к использованию в службе импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="fc46f-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span></span>
2. <span data-ttu-id="fc46f-127">Определите учетную запись хранения Azure, в которую будут скопированы данные после доставки диска в центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fc46f-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span></span>
3. <span data-ttu-id="fc46f-128">Используйте [инструмент импорта и экспорта Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) — служебную программу командной строки.</span><span class="sxs-lookup"><span data-stu-id="fc46f-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="fc46f-129">Ниже приведен пример фрагмента кода, демонстрирующий использование инструмента.</span><span class="sxs-lookup"><span data-stu-id="fc46f-129">Here's a sample snippet that shows how to use the tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="fc46f-130">Дополнительные фрагменты кода см. в статье [Использование службы импорта и экспорта Azure для передачи данных в хранилище BLOB-объектов](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="fc46f-130">See [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="fc46f-131">Приведенная выше команда создает файл журнала в указанном расположении.</span><span class="sxs-lookup"><span data-stu-id="fc46f-131">The preceding command creates a journal file at the specified location.</span></span> <span data-ttu-id="fc46f-132">С его помощью вы создадите задание импорта из [классического портала Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fc46f-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="fc46f-133">создание задания импорта;</span><span class="sxs-lookup"><span data-stu-id="fc46f-133">Create an import job</span></span>
<span data-ttu-id="fc46f-134">Теперь можно создать задание импорта, воспользовавшись инструкциями в статье [Использование службы импорта и экспорта Azure для передачи данных в хранилище BLOB-объектов](../storage/common/storage-import-export-service.md) в подразделе **Создание задания импорта**.</span><span class="sxs-lookup"><span data-stu-id="fc46f-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Create the Import job** section).</span></span> <span data-ttu-id="fc46f-135">Помимо других сведений укажите для этого задания импорта файл журнала, созданный при подготовке дисков.</span><span class="sxs-lookup"><span data-stu-id="fc46f-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span></span>

## <a name="physically-ship-the-disks"></a><span data-ttu-id="fc46f-136">Физическая доставка дисков</span><span class="sxs-lookup"><span data-stu-id="fc46f-136">Physically ship the disks</span></span>
<span data-ttu-id="fc46f-137">Теперь можно выполнить физическую доставку дисков в центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fc46f-137">You can now physically ship the disks to an Azure datacenter.</span></span> <span data-ttu-id="fc46f-138">Там данные копируются в большие двоичные объекты службы хранилища Azure, указанные при создании задания импорта.</span><span class="sxs-lookup"><span data-stu-id="fc46f-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span></span> <span data-ttu-id="fc46f-139">Кроме того, если при создании задания было решено указать сведения об отслеживании позже, теперь можно вернуться к заданию импорта и обновить номер отслеживания.</span><span class="sxs-lookup"><span data-stu-id="fc46f-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-to-azure-data-lake-store"></a><span data-ttu-id="fc46f-140">Копирование данных из больших двоичных объектов службы хранилища Azure в Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fc46f-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span></span>
<span data-ttu-id="fc46f-141">После того как задание импорта перейдет в состояние "Завершено", можно проверить, доступны ли данные в указанных больших двоичных объектах службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="fc46f-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span></span> <span data-ttu-id="fc46f-142">Затем можно переместить данные из больших двоичных объектов в Azure Data Lake Store, используя различные методы.</span><span class="sxs-lookup"><span data-stu-id="fc46f-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span></span> <span data-ttu-id="fc46f-143">Сведения о всех доступных вариантах передачи данных см. в разделе [Прием данных в Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="fc46f-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="fc46f-144">В этом разделе указаны определения JSON, с помощью которых можно создать конвейер фабрики данных Azure для копирования данных.</span><span class="sxs-lookup"><span data-stu-id="fc46f-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="fc46f-145">Эти определения JSON доступны на [портале Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), а также в [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fc46f-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="fc46f-146">Связанная служба источника (большой двоичный объект службы хранилища Azure)</span><span class="sxs-lookup"><span data-stu-id="fc46f-146">Source linked service (Azure Storage blob)</span></span>
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

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="fc46f-147">Связанная служба назначения (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="fc46f-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' to allow this data factory and the activities it runs to access this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from the OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="fc46f-148">Входной набор данных</span><span class="sxs-lookup"><span data-stu-id="fc46f-148">Input data set</span></span>
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
### <a name="output-data-set"></a><span data-ttu-id="fc46f-149">Выходной набор данных</span><span class="sxs-lookup"><span data-stu-id="fc46f-149">Output data set</span></span>
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
### <a name="pipeline-copy-activity"></a><span data-ttu-id="fc46f-150">Конвейер (действие копирования)</span><span class="sxs-lookup"><span data-stu-id="fc46f-150">Pipeline (copy activity)</span></span>
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
<span data-ttu-id="fc46f-151">Дополнительные сведения см. в статье [Перемещение данных в Azure Data Lake Store и обратно с помощью фабрики данных Azure](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="fc46f-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-the-data-files-in-azure-data-lake-store"></a><span data-ttu-id="fc46f-152">Воссоздание файлов данных в Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fc46f-152">Reconstruct the data files in Azure Data Lake Store</span></span>
<span data-ttu-id="fc46f-153">Мы начали работу с файлом размером 319 ГБ и разделили его на файлы меньшего размера для передачи с помощью службы импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="fc46f-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span></span> <span data-ttu-id="fc46f-154">Теперь после передачи данных в Azure Data Lake Store мы можем воссоздать исходный файл.</span><span class="sxs-lookup"><span data-stu-id="fc46f-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span></span> <span data-ttu-id="fc46f-155">Для этого вы также можете воспользоваться следующими командлетами Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc46f-155">You can use the following Azure PowerShell cmldts to do so.</span></span>

````
# Login to our account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch to the subscription you want to work with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  the files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="fc46f-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc46f-156">Next steps</span></span>
* [<span data-ttu-id="fc46f-157">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="fc46f-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="fc46f-158">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="fc46f-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="fc46f-159">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="fc46f-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
