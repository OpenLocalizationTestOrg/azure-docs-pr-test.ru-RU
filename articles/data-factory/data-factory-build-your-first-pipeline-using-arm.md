---
title: "aaaBuild первый фабрики данных (диспетчер ресурсов шаблона) | Документы Microsoft"
description: "Работая с этим руководством, вы создадите образец конвейера фабрики данных Azure с помощью шаблона Azure Resource Manager."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="270c0-103">Руководство. Создание фабрики данных Azure с помощью шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="270c0-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="270c0-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="270c0-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="270c0-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="270c0-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="270c0-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="270c0-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="270c0-108">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="270c0-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="270c0-109">REST API</span><span class="sxs-lookup"><span data-stu-id="270c0-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="270c0-110">В этой статье используется toocreate шаблона диспетчера ресурсов Azure первый фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="270c0-111">toodo hello учебника при помощи других средств и пакетов SDK, выберите один из вариантов hello из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="270c0-112">конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="270c0-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="270c0-113">Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="270c0-114">Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="270c0-115">конвейер данных Hello в этом учебнике преобразует входные данные tooproduce выходных данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="270c0-116">Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="270c0-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="270c0-117">конвейер Hello в этот учебник содержит только одно действие типа: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="270c0-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="270c0-118">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="270c0-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="270c0-119">Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="270c0-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="270c0-120">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="270c0-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="270c0-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="270c0-121">Prerequisites</span></span>
* <span data-ttu-id="270c0-122">Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.</span><span class="sxs-lookup"><span data-stu-id="270c0-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="270c0-123">Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи tooinstall последнюю версию Azure PowerShell на компьютере.</span><span class="sxs-lookup"><span data-stu-id="270c0-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="270c0-124">В разделе [разработки шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn шаблоны диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="270c0-125">В этом учебнике рассматриваются следующие темы:</span><span class="sxs-lookup"><span data-stu-id="270c0-125">In this tutorial</span></span>
| <span data-ttu-id="270c0-126">Сущность</span><span class="sxs-lookup"><span data-stu-id="270c0-126">Entity</span></span> | <span data-ttu-id="270c0-127">Описание</span><span class="sxs-lookup"><span data-stu-id="270c0-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="270c0-128">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-128">Azure Storage linked service</span></span> |<span data-ttu-id="270c0-129">Связывает фабрику данных toohello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="270c0-130">содержит учетную запись хранилища Azure Hello hello входных и выходных данных для конвейера hello в этом образце.</span><span class="sxs-lookup"><span data-stu-id="270c0-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="270c0-131">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="270c0-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="270c0-132">Связывает фабрику данных кластера toohello для HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="270c0-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="270c0-133">кластер Hello для tooprocess данных автоматически создается и удаляется после завершения обработки hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="270c0-134">Входной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-134">Azure Blob input dataset</span></span> |<span data-ttu-id="270c0-135">Ссылается toohello связанной службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="270c0-136">Hello связанной службы ссылается tooan учетную запись хранилища Azure и набор данных больших двоичных объектов Azure hello указывает контейнер hello, папки и имя файла в хранилище hello, содержащий hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="270c0-137">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-137">Azure Blob output dataset</span></span> |<span data-ttu-id="270c0-138">Ссылается toohello связанной службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="270c0-139">Hello связанной службы ссылается tooan учетную запись хранилища Azure и набор данных больших двоичных объектов Azure hello указывает контейнер hello, папки и имя файла в хранилище hello, содержащий hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="270c0-140">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="270c0-140">Data pipeline</span></span> |<span data-ttu-id="270c0-141">конвейер Hello содержит одно действие типа HDInsightHive, которая использует hello входного набора данных и создает выходной набор данных hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="270c0-142">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="270c0-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="270c0-143">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="270c0-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="270c0-144">Есть два типа действий: [действия перемещения данных](data-factory-data-movement-activities.md) и [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="270c0-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="270c0-145">В этом руководстве описано создание конвейера с одним действием (действием Hive).</span><span class="sxs-lookup"><span data-stu-id="270c0-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="270c0-146">Hello следующий раздел содержит hello завершения шаблона диспетчера ресурсов для определения сущностей фабрики данных, позволяющие быстро выполнять через шаблон hello hello учебник и тестирования.</span><span class="sxs-lookup"><span data-stu-id="270c0-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="270c0-147">toounderstand определение каждой сущности фабрики данных. в разделе [фабрики данных сущности в шаблоне hello](#data-factory-entities-in-the-template) раздела.</span><span class="sxs-lookup"><span data-stu-id="270c0-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="270c0-148">Шаблон JSON фабрики данных</span><span class="sxs-lookup"><span data-stu-id="270c0-148">Data Factory JSON template</span></span>
<span data-ttu-id="270c0-149">— Hello верхнего уровня шаблона диспетчера ресурсов для определения фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="270c0-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="270c0-150">Создайте JSON-файл с именем **ADFTutorialARM.json** в **C:\ADFGetStarted** папка с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="270c0-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
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
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
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
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
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
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="270c0-151">Еще один пример шаблона Resource Manager для создания фабрики данных Azure можно найти в статье [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Руководство. Создание конвейера с действием копирования с помощью шаблона Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="270c0-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="270c0-152">JSON-файл параметров</span><span class="sxs-lookup"><span data-stu-id="270c0-152">Parameters JSON</span></span>
<span data-ttu-id="270c0-153">Создайте JSON-файл с именем **ADFTutorialARM Parameters.json** , содержащий параметры для шаблона Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="270c0-154">Укажите имя hello и ключ учетной записи хранилища Azure для hello **storageAccountName** и **storageAccountKey** параметров в этот файл параметров.</span><span class="sxs-lookup"><span data-stu-id="270c0-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="270c0-155">Возможно, файлы JSON отдельный параметр для разработки, тестирования и рабочих средах, которые можно использовать с hello того же шаблона JSON фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="270c0-156">Скрипт PowerShell позволяет автоматизировать развертывание сущностей фабрики данных в этих средах.</span><span class="sxs-lookup"><span data-stu-id="270c0-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="270c0-157">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="270c0-157">Create data factory</span></span>
1. <span data-ttu-id="270c0-158">Запуск **Azure PowerShell** и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="270c0-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="270c0-159">Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="270c0-160">Запустите следующие команды tooview hello все hello подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="270c0-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="270c0-161">Следующая команда tooselect hello подписки на toowork с выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="270c0-162">Эта подписка должна hello равна hello, который используется в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="270c0-163">Запустите hello, следующая команда toodeploy фабрики данных сущностей с помощью шаблона диспетчера ресурсов hello, созданный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="270c0-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="270c0-164">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="270c0-164">Monitor pipeline</span></span>
1. <span data-ttu-id="270c0-165">После входа в toohello [портал Azure](https://portal.azure.com/), нажмите кнопку **Обзор** и выберите **фабрик данных**.</span><span class="sxs-lookup"><span data-stu-id="270c0-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="270c0-166">![Обзор -> Фабрики данных](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="270c0-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="270c0-167">В hello **фабрик данных** колонка, щелкните фабрики данных hello (**TutorialFactoryARM**) был создан.</span><span class="sxs-lookup"><span data-stu-id="270c0-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="270c0-168">В hello **фабрики данных** колонку для фабрики данных, нажмите кнопку **схема**.</span><span class="sxs-lookup"><span data-stu-id="270c0-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Плитка «Схема»](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="270c0-170">В hello **представление диаграммы**, просмотреть обзор конвейеров hello и использовать наборы данных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="270c0-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Представление схемы](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="270c0-172">В hello представление диаграммы, дважды щелкните набор данных hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="270c0-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="270c0-173">Вы увидите, что hello срез, который обрабатывается в данный момент.</span><span class="sxs-lookup"><span data-stu-id="270c0-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Выборка](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="270c0-175">После завершения обработки отображается срез hello в **готовности** состояния.</span><span class="sxs-lookup"><span data-stu-id="270c0-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="270c0-176">Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут).</span><span class="sxs-lookup"><span data-stu-id="270c0-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="270c0-177">Таким образом, ожидать hello конвейера tootake **около 30 минут** tooprocess hello среза.</span><span class="sxs-lookup"><span data-stu-id="270c0-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Выборка](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="270c0-179">Если срез hello находится в **готовности** состоянии, проверьте hello **partitioneddata** папки в hello **adfgetstarted** контейнера в хранилище BLOB-объектов для hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="270c0-180">В разделе [отслеживать наборы данных и конвейера](data-factory-monitor-manage-pipelines.md) инструкции о том, как toouse hello Azure портала колонках toomonitor hello конвейера и наборы данных вы создали в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="270c0-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="270c0-181">Также можно использовать монитор и управлять приложениями toomonitor конвейеры данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="270c0-182">В разделе [монитора и управлять ими с помощью мониторинга приложения конвейеров фабрики данных Azure](data-factory-monitor-manage-app.md) подробные сведения об использовании приложения hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="270c0-183">входной файл Hello, удаляется при успешно обработал hello среза.</span><span class="sxs-lookup"><span data-stu-id="270c0-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="270c0-184">Таким образом папка hello входного файла (input.log) toohello inputdata контейнера adfgetstarted hello отправки toorerun hello среза или hello учебника.</span><span class="sxs-lookup"><span data-stu-id="270c0-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="270c0-185">Фабрика сущностями данных в шаблоне hello</span><span class="sxs-lookup"><span data-stu-id="270c0-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="270c0-186">Определение фабрики данных</span><span class="sxs-lookup"><span data-stu-id="270c0-186">Define data factory</span></span>
<span data-ttu-id="270c0-187">Фабрика данных определить в шаблоне hello диспетчера ресурсов, как показано в следующих образец hello:</span><span class="sxs-lookup"><span data-stu-id="270c0-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="270c0-188">с именем dataFactoryName Hello определяются следующим образом.</span><span class="sxs-lookup"><span data-stu-id="270c0-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="270c0-189">Это уникальная строка, на основе идентификатора hello ресурсов группы.</span><span class="sxs-lookup"><span data-stu-id="270c0-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="270c0-190">Определение сущностей фабрики данных</span><span class="sxs-lookup"><span data-stu-id="270c0-190">Defining Data Factory entities</span></span>
<span data-ttu-id="270c0-191">Hello следующие сущности фабрики данных определены в шаблоне hello JSON:</span><span class="sxs-lookup"><span data-stu-id="270c0-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="270c0-192">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="270c0-193">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="270c0-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="270c0-194">Входной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="270c0-195">Выходной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="270c0-196">Конвейер данных с действием копирования</span><span class="sxs-lookup"><span data-stu-id="270c0-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="270c0-197">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-197">Azure Storage linked service</span></span>
<span data-ttu-id="270c0-198">Укажите имя hello и ключ учетной записи хранилища Azure в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="270c0-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="270c0-199">В разделе [связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойства, используемые toodefine связанная служба хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="270c0-200">Hello **connectionString** использует hello storageAccountName и storageAccountKey параметров.</span><span class="sxs-lookup"><span data-stu-id="270c0-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="270c0-201">Hello значения для этих параметров, передаваемых с помощью файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="270c0-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="270c0-202">Определение Hello также использует переменные: azureStroageLinkedService и с именем dataFactoryName, определенные в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="270c0-203">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="270c0-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="270c0-204">В разделе [связанные службы вычислений](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) статьи для получения сведений об toodefine свойства, используемые JSON связанной службы HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="270c0-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="270c0-205">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="270c0-205">Note hello following points:</span></span> 

* <span data-ttu-id="270c0-206">Hello фабрики данных создает **под управлением Linux** кластера HDInsight можно с помощью hello выше JSON.</span><span class="sxs-lookup"><span data-stu-id="270c0-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="270c0-207">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="270c0-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="270c0-208">Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="270c0-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="270c0-209">См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="270c0-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="270c0-210">Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="270c0-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="270c0-211">При удалении hello кластера HDInsight не удаляет этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="270c0-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="270c0-212">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="270c0-212">This behavior is by design.</span></span> <span data-ttu-id="270c0-213">С помощью по требованию связанной службы HDInsight, кластер HDInsight создается каждый раз фрагмент должен обработать, если нет существующего кластера динамической toobe (**timeToLive**) и удаляется при завершении обработки hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="270c0-214">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="270c0-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="270c0-215">Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="270c0-216">имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp».</span><span class="sxs-lookup"><span data-stu-id="270c0-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="270c0-217">Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="270c0-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="270c0-218">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="270c0-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="270c0-219">Входной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-219">Azure blob input dataset</span></span>
<span data-ttu-id="270c0-220">Указывать имена hello контейнер больших двоичных объектов, папки и файла, содержащего входные данные hello.</span><span class="sxs-lookup"><span data-stu-id="270c0-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="270c0-221">В разделе [свойства набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="270c0-222">Это определение использует следующие параметры, определенные в шаблоне параметр hello: blobContainer inputBlobFolder и inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="270c0-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="270c0-223">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="270c0-223">Azure Blob output dataset</span></span>
<span data-ttu-id="270c0-224">Указывать имена hello контейнер больших двоичных объектов и папке, содержащей hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="270c0-225">В разделе [свойства набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="270c0-226">Это определение использует следующие параметры, определенные в шаблоне параметр hello hello: blobContainer и outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="270c0-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="270c0-227">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="270c0-227">Data pipeline</span></span>
<span data-ttu-id="270c0-228">Здесь вы определите конвейер для преобразования данных. Для этого нужно запустить скрипт Hive в кластере Azure HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="270c0-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="270c0-229">В разделе [конвейера JSON](data-factory-create-pipelines.md#pipeline-json) описания toodefine элементы, используемые JSON конвейера в этом примере.</span><span class="sxs-lookup"><span data-stu-id="270c0-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a><span data-ttu-id="270c0-230">Повторное использование шаблона hello</span><span class="sxs-lookup"><span data-stu-id="270c0-230">Reuse hello template</span></span>
<span data-ttu-id="270c0-231">В учебнике hello вы создали шаблон для определения сущностей фабрики данных и для передачи значений для параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="270c0-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="270c0-232">toouse Здравствуйте средах toodifferent того же шаблона toodeploy фабрики данных сущности, создать файл параметров для каждой среды и использовать его при развертывании среды toothat.</span><span class="sxs-lookup"><span data-stu-id="270c0-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="270c0-233">Пример:</span><span class="sxs-lookup"><span data-stu-id="270c0-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="270c0-234">Обратите внимание, что hello первая команда использует параметр файла для среды разработки hello, второй hello тестовой среды и hello третий один hello производственную среду.</span><span class="sxs-lookup"><span data-stu-id="270c0-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="270c0-235">Также можно повторно использовать шаблон tooperform hello повторяющиеся задачи.</span><span class="sxs-lookup"><span data-stu-id="270c0-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="270c0-236">Например требуется toocreate множество фабрик данных с одним или дополнительные конвейеры, реализующих hello же логику, но каждый фабрики использует другой Azure хранилища данных и учетные записи базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="270c0-237">В этом сценарии используется hello того же шаблона в hello в одной среде (разработки, тестирования или рабочей), с другой параметр файлы toocreate фабрик данных.</span><span class="sxs-lookup"><span data-stu-id="270c0-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="270c0-238">Шаблон Resource Manager для создания шлюза</span><span class="sxs-lookup"><span data-stu-id="270c0-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="270c0-239">Ниже приведен образец шаблона диспетчера ресурсов для создания логических шлюза в hello обратно.</span><span class="sxs-lookup"><span data-stu-id="270c0-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="270c0-240">Установить шлюз на локальном компьютере или ВМ IaaS Azure и зарегистрируйте шлюз hello со службой фабрики данных, с помощью ключа.</span><span class="sxs-lookup"><span data-stu-id="270c0-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="270c0-241">Дополнительные сведения см. в статье [Перемещение данных между локальными источниками и облаком при помощи шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="270c0-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
<span data-ttu-id="270c0-242">Этот шаблон создает фабрику данных с именем GatewayUsingArmDF и шлюз с именем GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="270c0-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="270c0-243">См. также</span><span class="sxs-lookup"><span data-stu-id="270c0-243">See Also</span></span>
| <span data-ttu-id="270c0-244">Раздел</span><span class="sxs-lookup"><span data-stu-id="270c0-244">Topic</span></span> | <span data-ttu-id="270c0-245">Описание</span><span class="sxs-lookup"><span data-stu-id="270c0-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="270c0-246">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="270c0-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="270c0-247">Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct конца в конец управляемые данными рабочие процессы сценария или бизнеса.</span><span class="sxs-lookup"><span data-stu-id="270c0-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="270c0-248">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="270c0-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="270c0-249">Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="270c0-250">Планирование и исполнение с использованием фабрики данных</span><span class="sxs-lookup"><span data-stu-id="270c0-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="270c0-251">В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="270c0-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="270c0-252">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="270c0-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="270c0-253">В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления.</span><span class="sxs-lookup"><span data-stu-id="270c0-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

