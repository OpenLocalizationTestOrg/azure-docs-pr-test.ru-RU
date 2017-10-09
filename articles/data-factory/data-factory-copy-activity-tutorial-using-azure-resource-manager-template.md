---
title: "Руководство. Создание конвейера с помощью шаблона Resource Manager | Документация Майкрософт"
description: "Работая с этим руководством, вы создадите конвейер фабрики данных Azure с помощью шаблона Azure Resource Manager. В этом конвейере копирует данные из базы данных Azure SQL tooan хранилища BLOB-объектов Azure."
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
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="98a58-104">Учебник: Использование диспетчера ресурсов Azure шаблона toocreate toocopy данных конвейера фабрики данных</span><span class="sxs-lookup"><span data-stu-id="98a58-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98a58-105">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="98a58-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="98a58-106">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="98a58-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="98a58-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="98a58-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98a58-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="98a58-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="98a58-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="98a58-110">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="98a58-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="98a58-111">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="98a58-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="98a58-112">API .NET</span><span class="sxs-lookup"><span data-stu-id="98a58-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="98a58-113">В этом учебнике показано как toouse toocreate шаблона диспетчера ресурсов Azure фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="98a58-114">конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="98a58-115">Он не выполняет преобразование входных данных tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="98a58-116">Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="98a58-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="98a58-117">В этом руководстве описывается создание конвейера с одним действием — действием копирования.</span><span class="sxs-lookup"><span data-stu-id="98a58-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="98a58-118">Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="98a58-119">Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="98a58-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="98a58-120">Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы.</span><span class="sxs-lookup"><span data-stu-id="98a58-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="98a58-121">Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="98a58-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="98a58-122">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="98a58-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="98a58-123">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="98a58-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="98a58-124">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="98a58-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="98a58-125">конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="98a58-126">Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="98a58-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="98a58-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="98a58-127">Prerequisites</span></span>
* <span data-ttu-id="98a58-128">Выполните [учебника Обзор и необходимые компоненты](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="98a58-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="98a58-129">Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи tooinstall последнюю версию Azure PowerShell на компьютере.</span><span class="sxs-lookup"><span data-stu-id="98a58-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="98a58-130">В этом учебнике используйте PowerShell toodeploy фабрики данных сущности.</span><span class="sxs-lookup"><span data-stu-id="98a58-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="98a58-131">(необязательно) В разделе [разработки шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn шаблоны диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="98a58-132">В этом учебнике рассматриваются следующие темы:</span><span class="sxs-lookup"><span data-stu-id="98a58-132">In this tutorial</span></span>
<span data-ttu-id="98a58-133">В этом учебнике создается фабрики данных с hello, следуя фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="98a58-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="98a58-134">Сущность</span><span class="sxs-lookup"><span data-stu-id="98a58-134">Entity</span></span> | <span data-ttu-id="98a58-135">Описание</span><span class="sxs-lookup"><span data-stu-id="98a58-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98a58-136">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-136">Azure Storage linked service</span></span> |<span data-ttu-id="98a58-137">Связывает фабрику данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="98a58-138">Хранилище Azure — hello хранилище данных источника и базы данных Azure SQL является хранилищем данных приемник hello для действия копирования hello в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="98a58-139">Он указывает hello учетной записи хранилища, содержащий hello входные данные для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="98a58-140">Связанная служба базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="98a58-141">Связывает фабрику данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="98a58-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="98a58-142">Он указывает hello базы данных Azure SQL, содержащий hello выходные данные для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="98a58-143">Входной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-143">Azure Blob input dataset</span></span> |<span data-ttu-id="98a58-144">Ссылается toohello связанной службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="98a58-145">Hello связанной службы ссылается tooan учетную запись хранилища Azure и набор данных больших двоичных объектов Azure hello указывает контейнер hello, папки и имя файла в хранилище hello, содержащий hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="98a58-146">Выходной набор данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-146">Azure SQL output dataset</span></span> |<span data-ttu-id="98a58-147">Ссылается toohello связанной службой Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="98a58-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="98a58-148">Hello связанной службой Azure SQL ссылается tooan Azure SQL server и набора данных Azure SQL hello указывает имя hello hello таблица, содержащая hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="98a58-149">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="98a58-149">Data pipeline</span></span> |<span data-ttu-id="98a58-150">конвейер Hello содержит одно действие введите копию, которая принимает набор данных BLOB-объектов Azure hello в качестве входных данных и hello набор данных Azure SQL в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="98a58-151">Действие копирования Hello копирует данные из таблицы в базе данных Azure SQL hello tooa BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="98a58-152">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="98a58-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="98a58-153">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="98a58-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="98a58-154">Есть два типа действий: [действия перемещения данных](data-factory-data-movement-activities.md) и [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="98a58-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="98a58-155">В этом руководстве описывается создание конвейера с одним действием (действием копирования).</span><span class="sxs-lookup"><span data-stu-id="98a58-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Копирование больших двоичных объектов Azure tooAzure базы данных SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="98a58-157">Hello следующий раздел содержит hello завершения шаблона диспетчера ресурсов для определения сущностей фабрики данных, позволяющие быстро выполнять через шаблон hello hello учебник и тестирования.</span><span class="sxs-lookup"><span data-stu-id="98a58-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="98a58-158">toounderstand определение каждой сущности фабрики данных. в разделе [фабрики данных сущности в шаблоне hello](#data-factory-entities-in-the-template) раздела.</span><span class="sxs-lookup"><span data-stu-id="98a58-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="98a58-159">Шаблон JSON фабрики данных</span><span class="sxs-lookup"><span data-stu-id="98a58-159">Data Factory JSON template</span></span>
<span data-ttu-id="98a58-160">— Hello верхнего уровня шаблона диспетчера ресурсов для определения фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="98a58-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="98a58-161">Создайте JSON-файл с именем **ADFCopyTutorialARM.json** в **C:\ADFGetStarted** папка с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="98a58-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
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
                  "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="parameters-json"></a><span data-ttu-id="98a58-162">JSON-файл параметров</span><span class="sxs-lookup"><span data-stu-id="98a58-162">Parameters JSON</span></span>
<span data-ttu-id="98a58-163">Создайте JSON-файл с именем **ADFCopyTutorialARM Parameters.json** , содержащий параметры для шаблона Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="98a58-164">Укажите значения имени и ключа вашей учетной записи хранения Azure для параметров storageAccountName и storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="98a58-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="98a58-165">Укажите сервер Azure SQL, базу данных, пользователя и пароль для параметров sqlServerName, databaseName, sqlServerUserName и sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="98a58-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="98a58-166">Возможно, файлы JSON отдельный параметр для разработки, тестирования и рабочих средах, которые можно использовать с hello того же шаблона JSON фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="98a58-167">Скрипт PowerShell позволяет автоматизировать развертывание сущностей фабрики данных в этих средах.</span><span class="sxs-lookup"><span data-stu-id="98a58-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="98a58-168">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="98a58-168">Create data factory</span></span>
1. <span data-ttu-id="98a58-169">Запуск **Azure PowerShell** и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="98a58-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="98a58-170">Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="98a58-171">Запустите следующие команды tooview hello все hello подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="98a58-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="98a58-172">Следующая команда tooselect hello подписки на toowork с выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="98a58-173">Запустите hello, следующая команда toodeploy фабрики данных сущностей с помощью шаблона диспетчера ресурсов hello, созданный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="98a58-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="98a58-174">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="98a58-174">Monitor pipeline</span></span>

1. <span data-ttu-id="98a58-175">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="98a58-176">Нажмите кнопку **фабрик данных** hello левого меню (или) щелкните **дополнительные службы** и нажмите кнопку **фабрик данных** под **АНАЛИТИКИ + АНАЛИТИКА** Категория.</span><span class="sxs-lookup"><span data-stu-id="98a58-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Меню "Фабрики данных"](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="98a58-178">В hello **фабрик данных** страницы, искать и находить фабрики данных (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="98a58-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Поиск фабрики данных](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="98a58-180">Щелкните свою фабрику данных Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-180">Click your Azure data factory.</span></span> <span data-ttu-id="98a58-181">Вы увидите страницу домашней hello для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-181">You see hello home page for hello data factory.</span></span>
   
    ![Домашняя страница фабрики данных](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="98a58-183">Следуйте инструкциям из [отслеживать наборы данных и конвейера](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello конвейера и наборы данных создан в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="98a58-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="98a58-184">Сейчас Visual Studio не поддерживает мониторинг конвейеров фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="98a58-185">Когда срез будет hello **готовности** состоянии, убедитесь, что данные hello скопированный toohello **emp** таблицы в базе данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="98a58-186">Дополнительные сведения о как toouse Azure портала колонках toomonitor конвейера и наборы данных вы создали в этом учебнике см. в разделе [отслеживать наборы данных и конвейера](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="98a58-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="98a58-187">Дополнительные сведения о том, как toouse hello отслеживать состо & Управление приложения toomonitor данные конвейеров см. в разделе [монитора и управлять ими с помощью мониторинга приложения конвейеров фабрики данных Azure](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="98a58-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="98a58-188">Фабрика сущностями данных в шаблоне hello</span><span class="sxs-lookup"><span data-stu-id="98a58-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="98a58-189">Определение фабрики данных</span><span class="sxs-lookup"><span data-stu-id="98a58-189">Define data factory</span></span>
<span data-ttu-id="98a58-190">Фабрика данных определить в шаблоне hello диспетчера ресурсов, как показано в следующих образец hello:</span><span class="sxs-lookup"><span data-stu-id="98a58-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="98a58-191">с именем dataFactoryName Hello определяются следующим образом.</span><span class="sxs-lookup"><span data-stu-id="98a58-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="98a58-192">Это уникальная строка, на основе идентификатора hello ресурсов группы.</span><span class="sxs-lookup"><span data-stu-id="98a58-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="98a58-193">Определение сущностей фабрики данных</span><span class="sxs-lookup"><span data-stu-id="98a58-193">Defining Data Factory entities</span></span>
<span data-ttu-id="98a58-194">Hello следующие сущности фабрики данных определены в шаблоне hello JSON:</span><span class="sxs-lookup"><span data-stu-id="98a58-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="98a58-195">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="98a58-196">Связанная служба SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="98a58-197">Набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="98a58-198">Набор данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="98a58-199">Конвейер данных с действием копирования</span><span class="sxs-lookup"><span data-stu-id="98a58-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="98a58-200">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-200">Azure Storage linked service</span></span>
<span data-ttu-id="98a58-201">Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="98a58-202">Создан контейнер и загруженные в рамках учетной записи хранения данных toothis [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="98a58-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="98a58-203">Укажите имя hello и ключ учетной записи хранилища Azure в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="98a58-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="98a58-204">В разделе [связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойства, используемые toodefine связанная служба хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="98a58-205">Hello connectionString используются параметры storageAccountName и storageAccountKey hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="98a58-206">Hello значения для этих параметров, передаваемых с помощью файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="98a58-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="98a58-207">Определение Hello также использует переменные: azureStroageLinkedService и с именем dataFactoryName, определенные в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="98a58-208">Связанная служба базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="98a58-209">AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="98a58-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="98a58-210">Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="98a58-211">Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="98a58-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="98a58-212">Укажите имя сервера Azure SQL hello, имя базы данных, имя пользователя и пароль пользователя в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="98a58-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="98a58-213">В разделе [связанная служба Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) подробные сведения о JSON свойства, используемые toodefine связанная служба SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="98a58-214">Hello connectionString использует sqlServerName, имя базы данных, sqlServerUserName и sqlServerPassword параметров, значения которого передаются с помощью файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="98a58-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="98a58-215">Hello определение также использует следующие переменные из шаблона hello hello: azureSqlLinkedServiceName с именем dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="98a58-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="98a58-216">Набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-216">Azure blob dataset</span></span>
<span data-ttu-id="98a58-217">Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="98a58-218">В определении набора данных BLOB-объектов Azure укажите имена контейнер больших двоичных объектов, папки и файла, содержащего входные данные hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="98a58-219">В разделе [свойства набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="98a58-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="98a58-220">Набор данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98a58-220">Azure SQL dataset</span></span>
<span data-ttu-id="98a58-221">Укажите имя hello hello таблицы в базе данных Azure SQL hello, содержащий hello скопировать данные из хранилища больших двоичных объектов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="98a58-222">В разделе [свойства набора данных Azure SQL](data-factory-azure-sql-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="98a58-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

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

#### <a name="data-pipeline"></a><span data-ttu-id="98a58-223">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="98a58-223">Data pipeline</span></span>
<span data-ttu-id="98a58-224">Определяется конвейера, который копирует данные из набора данных Azure SQL toohello hello Azure BLOB-объекта dataset.</span><span class="sxs-lookup"><span data-stu-id="98a58-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="98a58-225">В разделе [конвейера JSON](data-factory-create-pipelines.md#pipeline-json) описания toodefine элементы, используемые JSON конвейера в этом примере.</span><span class="sxs-lookup"><span data-stu-id="98a58-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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
              "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="reuse-hello-template"></a><span data-ttu-id="98a58-226">Повторное использование шаблона hello</span><span class="sxs-lookup"><span data-stu-id="98a58-226">Reuse hello template</span></span>
<span data-ttu-id="98a58-227">В учебнике hello вы создали шаблон для определения сущностей фабрики данных и для передачи значений для параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="98a58-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="98a58-228">конвейер Hello копирует данные из базы Azure SQL tooan учетной записи хранилища Azure, указанного с помощью параметров.</span><span class="sxs-lookup"><span data-stu-id="98a58-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="98a58-229">toouse Здравствуйте средах toodifferent того же шаблона toodeploy фабрики данных сущности, создать файл параметров для каждой среды и использовать его при развертывании среды toothat.</span><span class="sxs-lookup"><span data-stu-id="98a58-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="98a58-230">Пример:</span><span class="sxs-lookup"><span data-stu-id="98a58-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="98a58-231">Обратите внимание, что hello первая команда использует параметр файла для среды разработки hello, второй hello тестовой среды и hello третий один hello производственную среду.</span><span class="sxs-lookup"><span data-stu-id="98a58-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="98a58-232">Также можно повторно использовать шаблон tooperform hello повторяющиеся задачи.</span><span class="sxs-lookup"><span data-stu-id="98a58-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="98a58-233">Например, необходимо toocreate множество фабрик данных с одним или более конвейеры, реализующих hello таким же логику, но Каждая фабрика данных использует учетные записи хранилища и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="98a58-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="98a58-234">В этом сценарии используется hello того же шаблона в hello в одной среде (разработки, тестирования или рабочей), с другой параметр файлы toocreate фабрик данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="98a58-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98a58-235">Next steps</span></span>
<span data-ttu-id="98a58-236">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="98a58-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="98a58-237">Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения:</span><span class="sxs-lookup"><span data-stu-id="98a58-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="98a58-238">toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="98a58-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
