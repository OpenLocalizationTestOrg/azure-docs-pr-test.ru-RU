---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "Загрузка данных с помощью фабрики данных Azure | Документация Майкрософт"
description: "Сведения о том, как загружать данные с помощью фабрики данных Azure."
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
ms.openlocfilehash: 0b01c77c916b616974545fc3da442e72e5336399
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="89eb0-103">Загрузка данных с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="89eb0-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89eb0-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="89eb0-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="89eb0-105">Фабрика данных</span><span class="sxs-lookup"><span data-stu-id="89eb0-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="89eb0-106">PolyBase;</span><span class="sxs-lookup"><span data-stu-id="89eb0-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="89eb0-107">BCP</span><span class="sxs-lookup"><span data-stu-id="89eb0-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="89eb0-108">В этом руководстве показано, как создать конвейер в фабрике данных Azure для перемещения данных из хранилища BLOB-объектов Azure в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-108">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="89eb0-109">С помощью описанных ниже шагов вы сможете:</span><span class="sxs-lookup"><span data-stu-id="89eb0-109">With the following steps you will:</span></span>

* <span data-ttu-id="89eb0-110">настроить демонстрационные данные в хранилище BLOB-объектов Azure;</span><span class="sxs-lookup"><span data-stu-id="89eb0-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="89eb0-111">подключить ресурсы к фабрике данных Azure;</span><span class="sxs-lookup"><span data-stu-id="89eb0-111">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="89eb0-112">создать конвейер для перемещения данных из больших двоичных объектов службы хранилища в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="89eb0-112">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="89eb0-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="89eb0-113">Before you begin</span></span>
<span data-ttu-id="89eb0-114">Чтобы получить основные сведения о фабрике данных Azure, изучите статью [Общие сведения о службе фабрики данных Azure, службе интеграции данных в облаке][Introduction to Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="89eb0-114">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="89eb0-115">Создание или определение ресурсов</span><span class="sxs-lookup"><span data-stu-id="89eb0-115">Create or identify resources</span></span>
<span data-ttu-id="89eb0-116">Для работы с этим руководством потребуются следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="89eb0-116">Before starting this tutorial, you need to have the following resources:</span></span>

* <span data-ttu-id="89eb0-117">**Хранилище BLOB-объектов Azure.** Оно используется как источник демонстрационных данных для конвейера фабрики данных Azure, поэтому его нужно создать заранее.</span><span class="sxs-lookup"><span data-stu-id="89eb0-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="89eb0-118">Если у вас еще нет учетной записи хранения, [создайте ее][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="89eb0-118">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="89eb0-119">**Хранилище данных SQL.** В этом руководстве мы будем перемещать данные из хранилища BLOB-объектов Azure в хранилище данных SQL. Для этого в Интернете нам потребуется хранилище данных с демонстрационными данными AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="89eb0-119">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="89eb0-120">Если у вас еще нет хранилища данных, [подготовьте его][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="89eb0-120">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="89eb0-121">Если у вас уже есть хранилище данных, но в нем нет демонстрационных данных, [загрузите их вручную][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="89eb0-121">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="89eb0-122">**Фабрика данных Azure.** В ней выполняется фактическая нагрузка. Ее нужно использовать для создания конвейера перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="89eb0-122">**Azure Data Factory**: Azure Data Factory completes the actual load and so you need to have one that you can use to build the data movement pipeline.</span></span> <span data-ttu-id="89eb0-123">Если она еще не создана, см. статью [Руководство. Создание первой фабрики данных Azure с помощью портала Azure][Get started with Azure Data Factory (Data Factory Editor)] (шаг 1).</span><span class="sxs-lookup"><span data-stu-id="89eb0-123">If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="89eb0-124">**AZCopy.** Служебная программа AZCopy нужна, чтобы скопировать демонстрационные данные из локального клиента в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-124">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="89eb0-125">Инструкции по установке см. в [документации по AZCopy][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="89eb0-125">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="89eb0-126">Шаг 1. Копирование демонстрационных данных в BLOB-объект хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="89eb0-126">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="89eb0-127">Когда все ресурсы будут готовы, скопируйте демонстрационные данные в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-127">Once you have all the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="89eb0-128">[Скачайте демонстрационные данные][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="89eb0-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="89eb0-129">К демонстрационным данным AdventureWorksDW будут добавлены данные продаж еще за три года.</span><span class="sxs-lookup"><span data-stu-id="89eb0-129">This data adds another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="89eb0-130">Чтобы скопировать данные о продажах в BLOB-объект хранилища Azure, выполните такую команду AZCopy:</span><span class="sxs-lookup"><span data-stu-id="89eb0-130">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="89eb0-131">Шаг 2. Подключение ресурсов к фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-131">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="89eb0-132">Теперь, когда BLOB-объект содержит нужные нам данные, мы можем создать конвейер фабрики данных Azure, чтобы переместить их из хранилища BLOB-объектов Azure в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="89eb0-132">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="89eb0-133">Для начала откройте [портал Azure][Azure portal] и в меню слева выберите свою фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="89eb0-133">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="89eb0-134">Шаг 2.1. Создание связанной службы</span><span class="sxs-lookup"><span data-stu-id="89eb0-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="89eb0-135">Свяжите свою учетную запись хранения Azure и хранилище данных SQL с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="89eb0-135">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="89eb0-136">Сначала начните процесс регистрации, щелкнув в колонке фабрики данных раздел "Связанные службы" и выбрав пункт "Новое хранилище данных".</span><span class="sxs-lookup"><span data-stu-id="89eb0-136">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="89eb0-137">Выберите имя, под которым будет зарегистрирована ваша служба хранилища Azure, выберите тип "Служба хранилища Azure", а затем введите имя и ключ своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="89eb0-137">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="89eb0-138">Чтобы зарегистрировать хранилище данных SQL, перейдите в раздел "Создать и развернуть" и последовательно щелкните "Новое хранилище данных" и "Хранилище данных SQL Azure".</span><span class="sxs-lookup"><span data-stu-id="89eb0-138">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="89eb0-139">Скопируйте этот шаблон и добавьте в него свои данные.</span><span class="sxs-lookup"><span data-stu-id="89eb0-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
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

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="89eb0-140">Шаг 2.2. Определение набора данных</span><span class="sxs-lookup"><span data-stu-id="89eb0-140">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="89eb0-141">После создания связанных служб следует определить наборы данных.</span><span class="sxs-lookup"><span data-stu-id="89eb0-141">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="89eb0-142">Это означает, что нужно задать структуру данных, перемещаемых из вашего хранилища в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="89eb0-142">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="89eb0-143">Вы можете прочитать об этом подробнее.</span><span class="sxs-lookup"><span data-stu-id="89eb0-143">You can read more about creating</span></span>

1. <span data-ttu-id="89eb0-144">Сначала перейдите к разделу фабрики данных "Разработка и развертывание".</span><span class="sxs-lookup"><span data-stu-id="89eb0-144">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="89eb0-145">Чтобы привязать хранилище к фабрике данных, щелкните элемент "Создать набор данных", а затем — "Хранилище BLOB-объектов Azure".</span><span class="sxs-lookup"><span data-stu-id="89eb0-145">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="89eb0-146">Для определения данных в хранилище BLOB-объектов Azure вы можете использовать приведенный ниже сценарий.</span><span class="sxs-lookup"><span data-stu-id="89eb0-146">You can use the below script to define your data in Azure Blob storage:</span></span>
   
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
3. <span data-ttu-id="89eb0-147">Теперь мы настроим набор данных для хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="89eb0-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="89eb0-148">Начнем так же, то есть щелкнем элемент "Создать набор данных", а затем — "Хранилище данных SQL Azure".</span><span class="sxs-lookup"><span data-stu-id="89eb0-148">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="89eb0-149">Шаг 3. Создание и запуск конвейера</span><span class="sxs-lookup"><span data-stu-id="89eb0-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="89eb0-150">Теперь мы настроим и запустим конвейер в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-150">Finally, we set up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="89eb0-151">Эта операция будет выполнять фактическое перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="89eb0-151">This is the operation that completes the actual data movement.</span></span>  <span data-ttu-id="89eb0-152">Полный список операций, которые можно выполнять в хранилище данных SQL и фабрике данных Azure, см. [здесь][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="89eb0-152">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="89eb0-153">В разделе "Создать и развернуть" щелкните "Дополнительные команды", а затем — "Создать конвейер".</span><span class="sxs-lookup"><span data-stu-id="89eb0-153">In the 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="89eb0-154">Создав конвейер, вы сможете передавать данные в хранилище данных с помощью приведенного ниже кода.</span><span class="sxs-lookup"><span data-stu-id="89eb0-154">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="89eb0-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89eb0-155">Next steps</span></span>
<span data-ttu-id="89eb0-156">Дополнительные сведения можно найти в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="89eb0-156">To learn more, start by viewing:</span></span>

* <span data-ttu-id="89eb0-157">[Схема обучения по фабрике данных Azure][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="89eb0-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="89eb0-158">[Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="89eb0-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="89eb0-159">Это основная справочная статья, посвященная использованию фабрики данных Azure с хранилищем данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-159">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="89eb0-160">В приведенных ниже статьях содержатся подробные сведения о фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="89eb0-161">В них речь идет о базах данных SQL Azure и HDinsight, но эти сведения также относятся к хранилищу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-161">They discuss Azure SQL Database or HDInsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="89eb0-162">[Руководство по началу работы с фабрикой данных Azure][Tutorial: Get started with Azure Data Factory]. Это основное руководство по обработке данных с помощью фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="89eb0-163">Из этого руководства вы узнаете, как создать конвейер, в котором веб-журналы ежемесячно преобразовываются и анализируются с помощью HDInsight.</span><span class="sxs-lookup"><span data-stu-id="89eb0-163">In this tutorial, you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="89eb0-164">Обратите внимание, что в этом руководстве копирование не используется.</span><span class="sxs-lookup"><span data-stu-id="89eb0-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="89eb0-165">[Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="89eb0-165">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="89eb0-166">В этом руководстве вы создадите конвейер в фабрике данных Azure, чтобы скопировать данные из хранилища BLOB-объектов Azure в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="89eb0-166">In this tutorial, you create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
