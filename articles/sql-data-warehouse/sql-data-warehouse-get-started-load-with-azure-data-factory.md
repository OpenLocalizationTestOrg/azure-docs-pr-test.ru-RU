---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "aaaLoad данных с помощью фабрики данных Azure | Документы Microsoft"
description: "Дополнительные сведения tooload данных с помощью фабрики данных Azure"
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="19d5b-103">Загрузка данных с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="19d5b-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19d5b-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="19d5b-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="19d5b-105">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="19d5b-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="19d5b-106">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="19d5b-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="19d5b-107">BCP</span><span class="sxs-lookup"><span data-stu-id="19d5b-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="19d5b-108">В этом учебнике показано как toocreate конвейера в фабрике данных Azure toomove данных из больших двоичных объектов хранилища Azure tooAzure хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="19d5b-108">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="19d5b-109">Следующие шаги hello вы сделаете следующее:</span><span class="sxs-lookup"><span data-stu-id="19d5b-109">With hello following steps you will:</span></span>

* <span data-ttu-id="19d5b-110">настроить демонстрационные данные в хранилище BLOB-объектов Azure;</span><span class="sxs-lookup"><span data-stu-id="19d5b-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="19d5b-111">Подключите tooAzure ресурсы фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="19d5b-111">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="19d5b-112">Создание данных конвейера toomove из tooSQL хранилища больших двоичных объектов хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="19d5b-112">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="19d5b-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="19d5b-113">Before you begin</span></span>
<span data-ttu-id="19d5b-114">toofamiliarize самостоятельно с фабрикой данных Azure, в разделе [tooAzure введение фабрики данных][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="19d5b-114">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="19d5b-115">Создание или определение ресурсов</span><span class="sxs-lookup"><span data-stu-id="19d5b-115">Create or identify resources</span></span>
<span data-ttu-id="19d5b-116">Перед запуском этого учебника, необходимо toohave hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="19d5b-116">Before starting this tutorial, you need toohave hello following resources:</span></span>

* <span data-ttu-id="19d5b-117">**Хранилище BLOB-объектов Azure**: в этом учебнике используется BLOB-объекта хранилища Azure как hello источник данных для конвейера фабрики данных Azure hello, и поэтому необходимо toohave один доступных toostore hello образец данных.</span><span class="sxs-lookup"><span data-stu-id="19d5b-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="19d5b-118">Если у еще его нет, узнайте, как слишком[создать учетную запись хранилища][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="19d5b-118">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="19d5b-119">**Хранилище данных SQL**: этого учебника перемещает hello данные из BLOB-объекта хранилища Azure слишком хранилище данных SQL, поэтому требуется toohave к хранилищу данных через Интернет, заполняемые hello образец данных AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="19d5b-119">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="19d5b-120">Если вы еще нет в хранилище данных, узнайте, как слишком[подготовить один][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="19d5b-120">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="19d5b-121">Если есть хранилище данных, но не удалось инициализировать его с образцами данных hello, вы можете [вручную загрузить][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="19d5b-121">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="19d5b-122">**Фабрика данных Azure**: фабрики данных Azure завершает реальную нагрузку hello и поэтому необходимо toohave один, которые можно использовать конвейер перемещения данных toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="19d5b-122">**Azure Data Factory**: Azure Data Factory completes hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.</span></span> <span data-ttu-id="19d5b-123">Если у еще его нет, узнайте, как toocreate один на шаге 1 из [приступить к работе с фабрикой данных Azure (редактор фабрики данных)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="19d5b-123">If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="19d5b-124">**AZCopy**: требуется AZCopy toocopy hello образцы данных из вашего локального клиента tooyour BLOB-объекта хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5b-124">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="19d5b-125">Инструкции по установке, в разделе hello [документации AZCopy][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="19d5b-125">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="19d5b-126">Шаг 1: Скопируйте образец данных tooAzure хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="19d5b-126">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="19d5b-127">Получив все составляющие hello готова, вы являетесь готов toocopy образец данных tooyour BLOB-объекта хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5b-127">Once you have all hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="19d5b-128">[Скачайте демонстрационные данные][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="19d5b-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="19d5b-129">Эти данные добавляет другой трех лет tooyour данные о продажах образец данных AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="19d5b-129">This data adds another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="19d5b-130">Используйте этот hello toocopy команды AZCopy три года tooyour данных больших двоичных объектов хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5b-130">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="19d5b-131">Шаг 2: Подключение tooAzure ресурсы фабрики данных</span><span class="sxs-lookup"><span data-stu-id="19d5b-131">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="19d5b-132">Теперь, hello данных можно создать hello фабрики данных Azure конвейера toomove hello данных из хранилища BLOB-объектов Azure в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="19d5b-132">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="19d5b-133">tooget к работе, откройте hello [портал Azure] [ Azure portal] и выберите из меню слева hello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="19d5b-133">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="19d5b-134">Шаг 2.1. Создание связанной службы</span><span class="sxs-lookup"><span data-stu-id="19d5b-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="19d5b-135">Свяжите учетную запись хранилища Azure и фабрики данных tooyour хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="19d5b-135">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="19d5b-136">Во-первых начать процесс регистрации hello, щелкнув раздел «Связанной службы» Привет фабрики данных и нажмите кнопку «Новое хранилище данных».</span><span class="sxs-lookup"><span data-stu-id="19d5b-136">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="19d5b-137">Выберите tooregister имя вашего хранилища azure в списке select хранилища Azure в качестве типа, а затем введите имя учетной записи и ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="19d5b-137">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="19d5b-138">tooregister хранилище данных SQL перейдите toohello раздел «Автор и развертывание», выберите «Создать хранилище данных» и «Хранилище данных SQL Azure».</span><span class="sxs-lookup"><span data-stu-id="19d5b-138">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="19d5b-139">Скопируйте этот шаблон и добавьте в него свои данные.</span><span class="sxs-lookup"><span data-stu-id="19d5b-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="19d5b-140">Шаг 2.2: Определение набора данных hello</span><span class="sxs-lookup"><span data-stu-id="19d5b-140">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="19d5b-141">После создания hello связанные службы, мы получите наборы данных toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="19d5b-141">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="19d5b-142">Здесь это означает определения структуры hello hello данных, которая перемещается из хранилища данных tooyour хранилища.</span><span class="sxs-lookup"><span data-stu-id="19d5b-142">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="19d5b-143">Вы можете прочитать об этом подробнее.</span><span class="sxs-lookup"><span data-stu-id="19d5b-143">You can read more about creating</span></span>

1. <span data-ttu-id="19d5b-144">Запустите этот процесс, перейдите в раздел «Автор и развернуть» toohello фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="19d5b-144">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="19d5b-145">Нажмите кнопку «Новый набор данных», а затем «Azure Blob storage» toolink фабрики данных tooyour хранилища.</span><span class="sxs-lookup"><span data-stu-id="19d5b-145">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="19d5b-146">Hello ниже toodefine скрипт можно использовать данные в хранилище больших двоичных объектов Azure:</span><span class="sxs-lookup"><span data-stu-id="19d5b-146">You can use hello below script toodefine your data in Azure Blob storage:</span></span>
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
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
3. <span data-ttu-id="19d5b-147">Теперь мы настроим набор данных для хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="19d5b-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="19d5b-148">Мы начнем в hello одинаково, нажав кнопку «Новый набор данных», а затем «Хранилище данных SQL Azure».</span><span class="sxs-lookup"><span data-stu-id="19d5b-148">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="19d5b-149">Шаг 3. Создание и запуск конвейера</span><span class="sxs-lookup"><span data-stu-id="19d5b-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="19d5b-150">Наконец мы установки и запуска hello конвейера в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5b-150">Finally, we set up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="19d5b-151">Это hello операция, выполняющая hello перемещения фактических данных.</span><span class="sxs-lookup"><span data-stu-id="19d5b-151">This is hello operation that completes hello actual data movement.</span></span>  <span data-ttu-id="19d5b-152">Можно найти полный просмотр hello операций, которые можно выполнить с хранилищем данных SQL и фабрики данных Azure [здесь][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="19d5b-152">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="19d5b-153">В hello в разделе «Автор и развертывание» нажмите кнопку «Более команды» и затем «Новый конвейер».</span><span class="sxs-lookup"><span data-stu-id="19d5b-153">In hello 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="19d5b-154">После создания конвейера hello, можно использовать hello ниже tooyour кода tootransfer hello данных хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="19d5b-154">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
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
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="19d5b-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19d5b-155">Next steps</span></span>
<span data-ttu-id="19d5b-156">toolearn больше, начните с просмотра:</span><span class="sxs-lookup"><span data-stu-id="19d5b-156">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="19d5b-157">[Схема обучения по фабрике данных Azure][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="19d5b-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="19d5b-158">[Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="19d5b-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="19d5b-159">Это hello core справочном разделе для использования фабрики данных Azure с хранилищем данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5b-159">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="19d5b-160">В приведенных ниже статьях содержатся подробные сведения о фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5b-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="19d5b-161">Они обсуждают базы данных SQL Azure или HDInsight, но hello сведения также относятся tooAzure хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="19d5b-161">They discuss Azure SQL Database or HDInsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="19d5b-162">[Учебник: Приступая к работе с фабрикой данных Azure] [ Tutorial: Get started with Azure Data Factory] это учебник hello основных компонентов для обработки данных с помощью фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5b-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="19d5b-163">В этом учебнике будут построены вашего первого конвейера, который использует HDInsight tootransform и анализировать веб-журналы на ежемесячной основе.</span><span class="sxs-lookup"><span data-stu-id="19d5b-163">In this tutorial, you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="19d5b-164">Обратите внимание, что в этом руководстве копирование не используется.</span><span class="sxs-lookup"><span data-stu-id="19d5b-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="19d5b-165">[Учебник: Копирование данных из больших двоичных объектов хранилища Azure tooAzure базы данных SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="19d5b-165">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="19d5b-166">В этом учебнике можно создать конвейер в данных toocopy фабрики данных Azure BLOB-объекта хранилища Azure tooAzure базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="19d5b-166">In this tutorial, you create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
