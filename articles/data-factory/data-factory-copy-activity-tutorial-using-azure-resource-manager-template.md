---
title: "Руководство. Создание конвейера с помощью шаблона Resource Manager | Документация Майкрософт"
description: "Работая с этим руководством, вы создадите конвейер фабрики данных Azure с помощью шаблона Azure Resource Manager. Этот конвейер копирует данные из хранилища BLOB-объектов Azure в базу данных SQL Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8a155213ed17e516a5c46abbe3d8a2bcc52268ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="c54b6-104">Руководство по созданию конвейера фабрики данных для копирования данных с использованием шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c54b6-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c54b6-105">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c54b6-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="c54b6-106">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="c54b6-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="c54b6-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="c54b6-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c54b6-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="c54b6-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c54b6-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="c54b6-110">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c54b6-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="c54b6-111">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="c54b6-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="c54b6-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="c54b6-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="c54b6-113">В этом руководстве показано, как создать фабрику данных Azure с использованием шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c54b6-113">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="c54b6-114">В этом руководстве конвейер данных копирует данные из исходного хранилища данных в целевое.</span><span class="sxs-lookup"><span data-stu-id="c54b6-114">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="c54b6-115">Он не преобразовывает входные данные в выходные.</span><span class="sxs-lookup"><span data-stu-id="c54b6-115">It does not transform input data to produce output data.</span></span> <span data-ttu-id="c54b6-116">Инструкции по преобразованию данных с помощью фабрики данных Azure см. в [руководстве по созданию конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="c54b6-116">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="c54b6-117">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="c54b6-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="c54b6-118">Действие копирования копирует данные из поддерживаемого хранилища данных в поддерживаемое хранилище данных-приемник.</span><span class="sxs-lookup"><span data-stu-id="c54b6-118">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="c54b6-119">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c54b6-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c54b6-120">Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="c54b6-120">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="c54b6-121">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c54b6-121">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="c54b6-122">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="c54b6-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c54b6-123">Два действия можно объединить в цепочку (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="c54b6-123">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="c54b6-124">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c54b6-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="c54b6-125">В этом руководстве конвейер данных копирует данные из исходного хранилища данных в целевое.</span><span class="sxs-lookup"><span data-stu-id="c54b6-125">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="c54b6-126">Инструкции по преобразованию данных с помощью фабрики данных Azure см. в [руководстве по созданию конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="c54b6-126">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c54b6-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c54b6-127">Prerequisites</span></span>
* <span data-ttu-id="c54b6-128">Прочтите [обзор руководства](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) и выполните **предварительные требования**.</span><span class="sxs-lookup"><span data-stu-id="c54b6-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="c54b6-129">Чтобы установить последнюю версию Azure PowerShell на локальном компьютере, следуйте инструкциям в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="c54b6-129">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="c54b6-130">В этом руководстве PowerShell используется для развертывания сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-130">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="c54b6-131">Сведения о шаблонах Azure Resource Manager см. в [этой статье](../azure-resource-manager/resource-group-authoring-templates.md) (необязательно).</span><span class="sxs-lookup"><span data-stu-id="c54b6-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="c54b6-132">В этом учебнике рассматриваются следующие темы:</span><span class="sxs-lookup"><span data-stu-id="c54b6-132">In this tutorial</span></span>
<span data-ttu-id="c54b6-133">В этом руководстве вы создадите фабрику данных со следующими сущностями.</span><span class="sxs-lookup"><span data-stu-id="c54b6-133">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="c54b6-134">Сущность</span><span class="sxs-lookup"><span data-stu-id="c54b6-134">Entity</span></span> | <span data-ttu-id="c54b6-135">Описание</span><span class="sxs-lookup"><span data-stu-id="c54b6-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c54b6-136">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-136">Azure Storage linked service</span></span> |<span data-ttu-id="c54b6-137">Связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-137">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="c54b6-138">Служба хранилища Azure — источник данных, а база данных SQL Azure — приемник данных для действия копирования, рассматриваемого в руководстве.</span><span class="sxs-lookup"><span data-stu-id="c54b6-138">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="c54b6-139">Эта сущность указывает учетную запись хранения, содержащую входные данные для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="c54b6-139">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="c54b6-140">Связанная служба базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="c54b6-141">Связывает базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-141">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="c54b6-142">Эта сущность указывает базу данных SQL Azure, содержащую выходные данные для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="c54b6-142">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="c54b6-143">Входной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-143">Azure Blob input dataset</span></span> |<span data-ttu-id="c54b6-144">Относится к связанной службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-144">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="c54b6-145">Связанная служба указывает на учетную запись хранения Azure, а набор данных большого двоичного объекта Azure указывает имя контейнера, папки и файла в хранилище, содержащем входные данные.</span><span class="sxs-lookup"><span data-stu-id="c54b6-145">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="c54b6-146">Выходной набор данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-146">Azure SQL output dataset</span></span> |<span data-ttu-id="c54b6-147">Относится к связанной службе SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-147">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="c54b6-148">Связанная служба SQL Azure указывает на сервер SQL Azure, а набор данных SQL Azure указывает имя таблицы, содержащей выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c54b6-148">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="c54b6-149">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="c54b6-149">Data pipeline</span></span> |<span data-ttu-id="c54b6-150">Конвейер содержит одно действие копирования, которое принимает в качестве входных данных набор данных большого двоичного объекта Azure, а в качестве выходных данных — набор данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-150">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="c54b6-151">Действие копирования копирует данные из большого двоичного объекта Azure в таблицу в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-151">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="c54b6-152">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="c54b6-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c54b6-153">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="c54b6-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c54b6-154">Есть два типа действий: [действия перемещения данных](data-factory-data-movement-activities.md) и [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c54b6-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="c54b6-155">В этом руководстве описывается создание конвейера с одним действием (действием копирования).</span><span class="sxs-lookup"><span data-stu-id="c54b6-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Копирование большого двоичного объекта Azure в базу данных SQL Azure](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="c54b6-157">В следующем разделе содержится полный шаблон Resource Manager для определения сущностей фабрики данных. Таким образом, вы сможете быстро изучить это руководство и протестировать шаблон.</span><span class="sxs-lookup"><span data-stu-id="c54b6-157">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="c54b6-158">Дополнительные сведения о том, как определяется каждая сущность фабрики данных, см. в разделе [Сущности фабрики данных в шаблоне](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="c54b6-158">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="c54b6-159">Шаблон JSON фабрики данных</span><span class="sxs-lookup"><span data-stu-id="c54b6-159">Data Factory JSON template</span></span>
<span data-ttu-id="c54b6-160">Шаблон Resource Manager верхнего уровня для определения фабрики данных выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c54b6-160">The top-level Resource Manager template for defining a data factory is:</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
<span data-ttu-id="c54b6-161">Создайте в папке **C:\ADFGetStarted** файл JSON с именем **ADFCopyTutorialARM.json** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="c54b6-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureStorage",
              "description": "Azure Storage linked service",
              "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
              }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
              }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureBlob",
              "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureStorageLinkedServiceName')]",
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob to Azure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="c54b6-162">JSON-файл параметров</span><span class="sxs-lookup"><span data-stu-id="c54b6-162">Parameters JSON</span></span>
<span data-ttu-id="c54b6-163">Создайте JSON-файл с именем **ADFCopyTutorialARM-Parameters.json**, содержащий параметры для шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c54b6-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c54b6-164">Укажите значения имени и ключа вашей учетной записи хранения Azure для параметров storageAccountName и storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="c54b6-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="c54b6-165">Укажите сервер Azure SQL, базу данных, пользователя и пароль для параметров sqlServerName, databaseName, sqlServerUserName и sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="c54b6-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="c54b6-166">Можно создать отдельные JSON-файлы параметров для сред разработки, тестирования и рабочей среды, которые можно использовать с одним и тем же шаблоном JSON фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="c54b6-167">Скрипт PowerShell позволяет автоматизировать развертывание сущностей фабрики данных в этих средах.</span><span class="sxs-lookup"><span data-stu-id="c54b6-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="c54b6-168">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="c54b6-168">Create data factory</span></span>
1. <span data-ttu-id="c54b6-169">Запустите **Azure PowerShell** и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c54b6-169">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="c54b6-170">Выполните следующую команду и введите имя пользователя и пароль, которые используются для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-170">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="c54b6-171">Выполните следующую команду, чтобы просмотреть все подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c54b6-171">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="c54b6-172">Выполните следующую команду, чтобы выбрать подписку, с которой вы собираетесь работать.</span><span class="sxs-lookup"><span data-stu-id="c54b6-172">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="c54b6-173">Чтобы развернуть сущности фабрики данных с помощью шаблона Resource Manager, созданного на шаге 1, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c54b6-173">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="c54b6-174">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="c54b6-174">Monitor pipeline</span></span>

1. <span data-ttu-id="c54b6-175">Войдите на [портал Azure](https://portal.azure.com), используя свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-175">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="c54b6-176">Щелкните **Фабрики данных** в меню слева или выберите **Больше служб** и щелкните **Фабрики данных** в категории **АНАЛИТИКА**.</span><span class="sxs-lookup"><span data-stu-id="c54b6-176">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Меню "Фабрики данных"](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="c54b6-178">На странице **Фабрики данных** найдите свою фабрику данных (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="c54b6-178">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Поиск фабрики данных](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="c54b6-180">Щелкните свою фабрику данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-180">Click your Azure data factory.</span></span> <span data-ttu-id="c54b6-181">После этого откроется домашняя страница фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-181">You see the home page for the data factory.</span></span>
   
    ![Домашняя страница фабрики данных](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="c54b6-183">Следуйте инструкциям из раздела [Отслеживание конвейера](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) для мониторинга конвейера и баз данных, созданных при работе с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="c54b6-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="c54b6-184">Сейчас Visual Studio не поддерживает мониторинг конвейеров фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="c54b6-185">Когда срез будет в состоянии **Готово**, проверьте, были ли скопированы данные в таблицу **emp** в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-185">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="c54b6-186">Дополнительные сведения о том, как использовать колонки на портале Azure для мониторинга конвейера и наборов данных, созданных с помощью этого руководства, см.в [этой статье](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c54b6-186">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="c54b6-187">Дополнительные сведения о том, как использовать приложение по мониторингу и управлению для мониторинга конвейеров данных, см. в [этой статье](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="c54b6-187">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="c54b6-188">Сущности фабрики данных в шаблоне</span><span class="sxs-lookup"><span data-stu-id="c54b6-188">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="c54b6-189">Определение фабрики данных</span><span class="sxs-lookup"><span data-stu-id="c54b6-189">Define data factory</span></span>
<span data-ttu-id="c54b6-190">Фабрику данных следует определить в шаблоне Resource Manager, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="c54b6-190">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="c54b6-191">Параметр dataFactoryName определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c54b6-191">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="c54b6-192">Это уникальная строка благодаря идентификатору группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c54b6-192">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="c54b6-193">Определение сущностей фабрики данных</span><span class="sxs-lookup"><span data-stu-id="c54b6-193">Defining Data Factory entities</span></span>
<span data-ttu-id="c54b6-194">В шаблоне JSON определены следующие сущности фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="c54b6-194">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="c54b6-195">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="c54b6-196">Связанная служба SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="c54b6-197">Набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="c54b6-198">Набор данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="c54b6-199">Конвейер данных с действием копирования</span><span class="sxs-lookup"><span data-stu-id="c54b6-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="c54b6-200">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-200">Azure Storage linked service</span></span>
<span data-ttu-id="c54b6-201">Связанная служба хранилища Azure связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-201">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="c54b6-202">Вы создали контейнер и отправили данные в эту учетную запись хранения в ходе выполнения предварительных [требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c54b6-202">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="c54b6-203">В этом разделе вы укажете имя и ключ вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-203">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="c54b6-204">Дополнительные сведения о свойствах JSON для определения связанной службы хранилища Azure см. в разделе [Связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="c54b6-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```

<span data-ttu-id="c54b6-205">Для connectionString используются параметры storageAccountName и storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="c54b6-205">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="c54b6-206">Значения для этих параметров передаются с помощью файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c54b6-206">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="c54b6-207">В этом определении также используются переменные azureStroageLinkedService и dataFactoryName, заданные в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="c54b6-207">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="c54b6-208">Связанная служба базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="c54b6-209">Связанная служба SQL Azure связывает базу данных SQL Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-209">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="c54b6-210">В этой базе данных хранятся данные, скопированные из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="c54b6-210">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="c54b6-211">Вы создали пустую таблицу в этой базе данных в ходе выполнения [предварительных требований](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c54b6-211">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="c54b6-212">В этом разделе вы укажете имя сервера SQL Azure, имя базы данных, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="c54b6-212">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="c54b6-213">Дополнительные сведения о свойствах JSON для определения связанной службы SQL Azure см. в разделе [Связанная служба SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c54b6-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="c54b6-214">Для connectionString используются параметры sqlServerName, databaseName, sqlServerUserName и sqlServerPassword, значения которых передаются с помощью файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c54b6-214">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="c54b6-215">В определении также используются переменные azureSqlLinkedServiceName dataFactoryName из шаблона.</span><span class="sxs-lookup"><span data-stu-id="c54b6-215">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="c54b6-216">Набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-216">Azure blob dataset</span></span>
<span data-ttu-id="c54b6-217">Связанная служба хранилища Azure указывает строку подключения, которую фабрика данных использует во время выполнения, чтобы подключиться к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-217">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="c54b6-218">В определении набора данных большого двоичного объекта Azure укажите имена контейнера больших двоичных объектов, папки и файла, содержащего входные данные.</span><span class="sxs-lookup"><span data-stu-id="c54b6-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="c54b6-219">Подробные сведения о свойствах JSON, которые используются для определения набора данных большого двоичного объекта Azure, см. в разделе [Свойства типа "Набор данных большого двоичного объекта Azure"](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c54b6-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]",
      "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
          "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="c54b6-220">Набор данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c54b6-220">Azure SQL dataset</span></span>
<span data-ttu-id="c54b6-221">В этом разделе нужно указать имя таблицы в базе данных SQL Azure, содержащей скопированные данные из хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-221">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="c54b6-222">Подробные сведения о свойствах JSON, которые используются для определения набора данных SQL Azure, см. в разделе [Свойства типа "Набор данных SQL Azure"](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c54b6-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="c54b6-223">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="c54b6-223">Data pipeline</span></span>
<span data-ttu-id="c54b6-224">Здесь вы определите конвейер, копирующий данные из набора данных большого двоичного объекта Azure в набор данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c54b6-224">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="c54b6-225">В разделе [Конвейер JSON](data-factory-create-pipelines.md#pipeline-json) описаны элементы JSON, используемые для определения конвейера в этом примере.</span><span class="sxs-lookup"><span data-stu-id="c54b6-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob to Azure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="c54b6-226">Повторное использование шаблона</span><span class="sxs-lookup"><span data-stu-id="c54b6-226">Reuse the template</span></span>
<span data-ttu-id="c54b6-227">В этом руководстве описывается создание шаблона для определения сущностей фабрики данных, а также шаблона, передающего значения для параметров.</span><span class="sxs-lookup"><span data-stu-id="c54b6-227">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="c54b6-228">Конвейер копирует данные из учетной записи хранения Azure в базу данных SQL Azure, указанную с помощью параметров.</span><span class="sxs-lookup"><span data-stu-id="c54b6-228">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="c54b6-229">Чтобы использовать один шаблон для развертывания сущностей фабрики данных в разных средах, нужно создать файл параметров для каждой среды и использовать его при развертывании в определенной среде.</span><span class="sxs-lookup"><span data-stu-id="c54b6-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="c54b6-230">Пример:</span><span class="sxs-lookup"><span data-stu-id="c54b6-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="c54b6-231">Обратите внимание, что первая команда использует файл параметров для среды разработки, вторая — для среды тестирования, а третья — для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="c54b6-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="c54b6-232">Шаблон можно снова использовать для выполнения повторяющихся задач.</span><span class="sxs-lookup"><span data-stu-id="c54b6-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="c54b6-233">Например, вам нужно создать несколько фабрик данных с одним или несколькими конвейерами, которые реализуют одинаковую логику, но при этом каждая фабрика данных использует разные учетные записи хранения и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c54b6-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="c54b6-234">В этом сценарии для создания фабрик данных используется один шаблон в той же среде (разработки, тестирования или рабочей) с различными файлами параметров.</span><span class="sxs-lookup"><span data-stu-id="c54b6-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="c54b6-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c54b6-235">Next steps</span></span>
<span data-ttu-id="c54b6-236">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="c54b6-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="c54b6-237">В следующей таблице приведен список хранилищ данных, которые поддерживаются в качестве источников и целевых расположений для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="c54b6-237">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="c54b6-238">Чтобы получить дополнительные сведения о том, как скопировать данные в хранилище данных или из него, щелкните ссылку для хранилища данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="c54b6-238">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
