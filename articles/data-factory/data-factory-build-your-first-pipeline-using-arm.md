---
title: "Создание первой фабрики данных (шаблон Resource Manager) | Документация Майкрософт"
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
ms.openlocfilehash: c67169f296f2f13b9ee87180f126fb1dcf10fbea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="31893-103">Руководство. Создание фабрики данных Azure с помощью шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="31893-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31893-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="31893-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="31893-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="31893-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="31893-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31893-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="31893-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31893-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="31893-108">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31893-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="31893-109">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="31893-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="31893-110">Из этой статьи вы узнаете, как создать свою первую фабрику данных с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="31893-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="31893-111">Чтобы выполнить приведенные здесь инструкции с помощью других средств или пакетов SDK, выберите в раскрывающемся списке один из доступных вариантов.</span><span class="sxs-lookup"><span data-stu-id="31893-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="31893-112">В этом руководстве конвейеру доступно одно действие — **действие Hive HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="31893-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="31893-113">Это действие запускает сценарий Hive в кластере HDInsight Azure, который преобразует входные данные в выходные.</span><span class="sxs-lookup"><span data-stu-id="31893-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="31893-114">Конвейер запускается раз в месяц по расписанию. Время начала и окончания запуска также указаны.</span><span class="sxs-lookup"><span data-stu-id="31893-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="31893-115">В этом руководстве конвейер данных преобразовывает входные данные в выходные.</span><span class="sxs-lookup"><span data-stu-id="31893-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="31893-116">Инструкции по копированию данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных Azure см. в [этой статье](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="31893-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="31893-117">В этом руководстве конвейеру доступно только одно действие типа — HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="31893-117">The pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="31893-118">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="31893-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="31893-119">Два действия можно объединить в цепочку (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="31893-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="31893-120">Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="31893-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="31893-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="31893-121">Prerequisites</span></span>
* <span data-ttu-id="31893-122">Прочтите [обзорную статью](data-factory-build-your-first-pipeline.md) и выполните **предварительные требования** .</span><span class="sxs-lookup"><span data-stu-id="31893-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="31893-123">Чтобы установить последнюю версию Azure PowerShell на локальном компьютере, следуйте инструкциям в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="31893-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="31893-124">Сведения о шаблонах Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="31893-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="31893-125">В этом учебнике рассматриваются следующие темы:</span><span class="sxs-lookup"><span data-stu-id="31893-125">In this tutorial</span></span>
| <span data-ttu-id="31893-126">Сущность</span><span class="sxs-lookup"><span data-stu-id="31893-126">Entity</span></span> | <span data-ttu-id="31893-127">Описание</span><span class="sxs-lookup"><span data-stu-id="31893-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="31893-128">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="31893-128">Azure Storage linked service</span></span> |<span data-ttu-id="31893-129">Связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="31893-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="31893-130">В этом примере учетная запись хранения Azure содержит входные и выходные данные для конвейера.</span><span class="sxs-lookup"><span data-stu-id="31893-130">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="31893-131">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="31893-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="31893-132">Связывает кластер HDInsight по запросу с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="31893-132">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="31893-133">Кластер создается автоматически для обработки данных и удаляется после ее завершения.</span><span class="sxs-lookup"><span data-stu-id="31893-133">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="31893-134">Входной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="31893-134">Azure Blob input dataset</span></span> |<span data-ttu-id="31893-135">Относится к связанной службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="31893-135">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="31893-136">Связанная служба указывает на учетную запись хранения Azure, а набор данных большого двоичного объекта Azure указывает имя контейнера, папки и файла в хранилище, содержащем входные данные.</span><span class="sxs-lookup"><span data-stu-id="31893-136">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="31893-137">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="31893-137">Azure Blob output dataset</span></span> |<span data-ttu-id="31893-138">Относится к связанной службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="31893-138">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="31893-139">Связанная служба указывает на учетную запись хранения Azure, а набор данных большого двоичного объекта Azure указывает контейнер, папку и имя файла в хранилище, содержащем выходные данные.</span><span class="sxs-lookup"><span data-stu-id="31893-139">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="31893-140">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="31893-140">Data pipeline</span></span> |<span data-ttu-id="31893-141">Конвейер содержит одно действие типа HDInsightHive, использующее входной набор данных и создающее выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="31893-141">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="31893-142">Фабрика данных может иметь один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="31893-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="31893-143">Конвейер может содержать одно или несколько действий.</span><span class="sxs-lookup"><span data-stu-id="31893-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="31893-144">Есть два типа действий: [действия перемещения данных](data-factory-data-movement-activities.md) и [действия преобразования данных](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="31893-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="31893-145">В этом руководстве описано создание конвейера с одним действием (действием Hive).</span><span class="sxs-lookup"><span data-stu-id="31893-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="31893-146">В следующем разделе содержится полный шаблон Resource Manager для определения сущностей фабрики данных. Таким образом, вы сможете быстро изучить это руководство и протестировать шаблон.</span><span class="sxs-lookup"><span data-stu-id="31893-146">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="31893-147">Дополнительные сведения о том, как определяется каждая сущность фабрики данных, см. в разделе [Сущности фабрики данных в шаблоне](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="31893-147">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="31893-148">Шаблон JSON фабрики данных</span><span class="sxs-lookup"><span data-stu-id="31893-148">Data Factory JSON template</span></span>
<span data-ttu-id="31893-149">Шаблон Resource Manager верхнего уровня для определения фабрики данных выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31893-149">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="31893-150">Создайте в папке **C:\ADFGetStarted** файл JSON с именем **ADFTutorialARM.json** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="31893-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
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
> <span data-ttu-id="31893-151">Еще один пример шаблона Resource Manager для создания фабрики данных Azure можно найти в статье [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Руководство. Создание конвейера с действием копирования с помощью шаблона Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="31893-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="31893-152">JSON-файл параметров</span><span class="sxs-lookup"><span data-stu-id="31893-152">Parameters JSON</span></span>
<span data-ttu-id="31893-153">Создайте JSON-файл с именем **ADFTutorialARM Parameters.json**, содержащий параметры для шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="31893-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="31893-154">Укажите значения имени и ключа вашей учетной записи хранения Azure для параметров **storageAccountName** и **storageAccountKey** в этом файле параметров.</span><span class="sxs-lookup"><span data-stu-id="31893-154">Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="31893-155">Можно создать отдельные JSON-файлы параметров для сред разработки, тестирования и рабочей среды, которые можно использовать с одним и тем же шаблоном JSON фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="31893-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="31893-156">Скрипт PowerShell позволяет автоматизировать развертывание сущностей фабрики данных в этих средах.</span><span class="sxs-lookup"><span data-stu-id="31893-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="31893-157">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="31893-157">Create data factory</span></span>
1. <span data-ttu-id="31893-158">Запустите **Azure PowerShell** и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="31893-158">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="31893-159">Выполните следующую команду и введите имя пользователя и пароль, которые используются для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="31893-159">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="31893-160">Выполните следующую команду, чтобы просмотреть все подписки для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="31893-160">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="31893-161">Выполните следующую команду, чтобы выбрать подписку, с которой вы собираетесь работать.</span><span class="sxs-lookup"><span data-stu-id="31893-161">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="31893-162">Эта подписка должна совпадать с той, которая используется на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="31893-162">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="31893-163">Чтобы развернуть сущности фабрики данных с помощью шаблона Resource Manager, созданного на шаге 1, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="31893-163">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="31893-164">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="31893-164">Monitor pipeline</span></span>
1. <span data-ttu-id="31893-165">Войдя на [портал Azure](https://portal.azure.com/), щелкните **Обзор** и выберите **Фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="31893-165">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="31893-166">![Обзор -> Фабрики данных](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="31893-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="31893-167">В колонке **Фабрики данных** выберите созданную фабрику данных (**TutorialFactoryARM**).</span><span class="sxs-lookup"><span data-stu-id="31893-167">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="31893-168">В колонке **Фабрика данных** для своей фабрики данных щелкните плитку **Схема**.</span><span class="sxs-lookup"><span data-stu-id="31893-168">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Плитка «Схема»](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="31893-170">В **представлении схемы**вы увидите все конвейеры и наборы данных, используемые в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="31893-170">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![представлении схемы](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="31893-172">В представлении схемы дважды щелкните набор данных **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="31893-172">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="31893-173">Вы увидите срез, который сейчас обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="31893-173">You see that the slice that is currently being processed.</span></span>
   
    ![Выборка](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="31893-175">Как только обработка завершится, срез перейдет в состояние **Готово** .</span><span class="sxs-lookup"><span data-stu-id="31893-175">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="31893-176">Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут).</span><span class="sxs-lookup"><span data-stu-id="31893-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="31893-177">Таким образом, конвейер обработает срез **примерно через 30 минут** .</span><span class="sxs-lookup"><span data-stu-id="31893-177">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Выборка](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="31893-179">Когда срез перейдет в состояние **Готово**, проверьте выходные данные в папке **partitioneddata** контейнера **adfgetstarted** в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="31893-179">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="31893-180">Инструкции по использованию колонок на портале Azure для мониторинга конвейера и наборов данных, созданных с помощью этого руководства, см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="31893-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="31893-181">Вы также можете использовать приложение мониторинга и управления для мониторинга данных конвейеров.</span><span class="sxs-lookup"><span data-stu-id="31893-181">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="31893-182">Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="31893-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="31893-183">В случае успешной обработки среза входной файл удаляется.</span><span class="sxs-lookup"><span data-stu-id="31893-183">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="31893-184">Если вы хотите повторно обработать срез или еще раз выполнить инструкции из руководства, передайте входной файл (input.log) в папку inputdata в контейнере adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="31893-184">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="31893-185">Сущности фабрики данных в шаблоне</span><span class="sxs-lookup"><span data-stu-id="31893-185">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="31893-186">Определение фабрики данных</span><span class="sxs-lookup"><span data-stu-id="31893-186">Define data factory</span></span>
<span data-ttu-id="31893-187">Фабрику данных следует определить в шаблоне Resource Manager, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="31893-187">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="31893-188">Параметр dataFactoryName определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="31893-188">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="31893-189">Это уникальная строка благодаря идентификатору группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="31893-189">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="31893-190">Определение сущностей фабрики данных</span><span class="sxs-lookup"><span data-stu-id="31893-190">Defining Data Factory entities</span></span>
<span data-ttu-id="31893-191">В шаблоне JSON определены следующие сущности фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="31893-191">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="31893-192">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="31893-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="31893-193">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="31893-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="31893-194">Входной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="31893-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="31893-195">Выходной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="31893-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="31893-196">Конвейер данных с действием копирования</span><span class="sxs-lookup"><span data-stu-id="31893-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="31893-197">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="31893-197">Azure Storage linked service</span></span>
<span data-ttu-id="31893-198">В этом разделе вы укажете имя и ключ вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="31893-198">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="31893-199">Дополнительные сведения о свойствах JSON для определения связанной службы хранилища Azure см. в разделе [Связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="31893-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="31893-200">Для **connectionString** используются параметры storageAccountName и storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="31893-200">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="31893-201">Значения для этих параметров передаются с помощью файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="31893-201">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="31893-202">В этом определении также используются переменные azureStroageLinkedService и dataFactoryName, заданные в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="31893-202">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="31893-203">Связанная служба кластера HDInsight по запросу</span><span class="sxs-lookup"><span data-stu-id="31893-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="31893-204">Дополнительные сведения о свойствах JSON, используемых для определения связанной службы кластера HDInsight по запросу, см. в статье [Связанные службы вычислений](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="31893-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="31893-205">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="31893-205">Note the following points:</span></span> 

* <span data-ttu-id="31893-206">С помощью приведенного выше JSON-файла фабрика данных создает кластер HDInsight **под управлением Linux**.</span><span class="sxs-lookup"><span data-stu-id="31893-206">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="31893-207">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="31893-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="31893-208">Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="31893-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="31893-209">См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="31893-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="31893-210">Кластер HDInsight создает **контейнер по умолчанию** в хранилище BLOB-объектов, указанном в коде JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="31893-210">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="31893-211">При удалении кластера HDInsight этот контейнер не удаляется.</span><span class="sxs-lookup"><span data-stu-id="31893-211">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="31893-212">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="31893-212">This behavior is by design.</span></span> <span data-ttu-id="31893-213">Если используется связанная служба HDInsight по запросу, кластер HDInsight создается всякий раз, когда нужно обработать срез данных (если не используется динамический кластер**timeToLive**), после чего кластер удаляется.</span><span class="sxs-lookup"><span data-stu-id="31893-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="31893-214">По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="31893-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="31893-215">Если эти контейнеры не используются для устранения неполадок с заданиями, удалите их — это позволит сократить расходы на хранение.</span><span class="sxs-lookup"><span data-stu-id="31893-215">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="31893-216">Имена контейнеров указаны в формате adf**имя_фабрики_данных**-**имя_связанной_службы**-метка_даты_и_времени.</span><span class="sxs-lookup"><span data-stu-id="31893-216">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="31893-217">Для удаления контейнеров в хранилище BLOB-объектов Azure используйте такие инструменты, как [Microsoft Storage Explorer](http://storageexplorer.com/) .</span><span class="sxs-lookup"><span data-stu-id="31893-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="31893-218">Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="31893-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="31893-219">Входной набор данных большого двоичного объекта Azure</span><span class="sxs-lookup"><span data-stu-id="31893-219">Azure blob input dataset</span></span>
<span data-ttu-id="31893-220">Укажите имя контейнера больших двоичных объектов, папку и файл, который содержит входные данные.</span><span class="sxs-lookup"><span data-stu-id="31893-220">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="31893-221">Подробные сведения о свойствах JSON, которые используются для определения набора данных большого двоичного объекта Azure, см. в разделе [Свойства типа "Набор данных большого двоичного объекта Azure"](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="31893-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="31893-222">В этом определении используются следующие параметры, заданные в шаблоне параметров: blobContainer, outputBlobFolder и inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="31893-222">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="31893-223">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="31893-223">Azure Blob output dataset</span></span>
<span data-ttu-id="31893-224">Укажите имя контейнера больших двоичных объектов и папку, которая содержит выходные данные.</span><span class="sxs-lookup"><span data-stu-id="31893-224">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="31893-225">Подробные сведения о свойствах JSON, которые используются для определения набора данных большого двоичного объекта Azure, см. в разделе [Свойства типа "Набор данных большого двоичного объекта Azure"](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="31893-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="31893-226">В этом определении используются следующие параметры, заданные в шаблоне параметров: blobContainer и outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="31893-226">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="31893-227">Конвейер данных</span><span class="sxs-lookup"><span data-stu-id="31893-227">Data pipeline</span></span>
<span data-ttu-id="31893-228">Здесь вы определите конвейер для преобразования данных. Для этого нужно запустить скрипт Hive в кластере Azure HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="31893-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="31893-229">В разделе [Конвейер JSON](data-factory-create-pipelines.md#pipeline-json) описаны элементы JSON, используемые для определения конвейера в этом примере.</span><span class="sxs-lookup"><span data-stu-id="31893-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

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

## <a name="reuse-the-template"></a><span data-ttu-id="31893-230">Повторное использование шаблона</span><span class="sxs-lookup"><span data-stu-id="31893-230">Reuse the template</span></span>
<span data-ttu-id="31893-231">В этом руководстве описывается создание шаблона для определения сущностей фабрики данных, а также шаблона, передающего значения для параметров.</span><span class="sxs-lookup"><span data-stu-id="31893-231">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="31893-232">Чтобы использовать один шаблон для развертывания сущностей фабрики данных в разных средах, нужно создать файл параметров для каждой среды и использовать его при развертывании в определенной среде.</span><span class="sxs-lookup"><span data-stu-id="31893-232">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="31893-233">Пример:</span><span class="sxs-lookup"><span data-stu-id="31893-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="31893-234">Обратите внимание, что первая команда использует файл параметров для среды разработки, вторая — для среды тестирования, а третья — для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="31893-234">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="31893-235">Шаблон можно снова использовать для выполнения повторяющихся задач.</span><span class="sxs-lookup"><span data-stu-id="31893-235">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="31893-236">Например, вам нужно создать несколько фабрик данных с одним или с несколькими конвейерами, которые реализуют одинаковую логику, но при этом каждая фабрика данных использует различные учетные записи хранения Azure и базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="31893-236">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="31893-237">В этом сценарии для создания фабрик данных используется один шаблон в той же среде (разработки, тестирования или рабочей) с различными файлами параметров.</span><span class="sxs-lookup"><span data-stu-id="31893-237">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="31893-238">Шаблон Resource Manager для создания шлюза</span><span class="sxs-lookup"><span data-stu-id="31893-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="31893-239">Ниже приведен пример шаблона Resource Manager для создания логического шлюза в серверной части.</span><span class="sxs-lookup"><span data-stu-id="31893-239">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="31893-240">Установите шлюз на локальном компьютере или виртуальной машине IaaS Azure и зарегистрируйте его в службе фабрики данных с помощью ключа.</span><span class="sxs-lookup"><span data-stu-id="31893-240">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="31893-241">Дополнительные сведения см. в статье [Перемещение данных между локальными источниками и облаком при помощи шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="31893-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="31893-242">Этот шаблон создает фабрику данных с именем GatewayUsingArmDF и шлюз с именем GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="31893-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="31893-243">См. также</span><span class="sxs-lookup"><span data-stu-id="31893-243">See Also</span></span>
| <span data-ttu-id="31893-244">Раздел</span><span class="sxs-lookup"><span data-stu-id="31893-244">Topic</span></span> | <span data-ttu-id="31893-245">Описание</span><span class="sxs-lookup"><span data-stu-id="31893-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="31893-246">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="31893-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="31893-247">Эта статья поможет вам понять сущность конвейеров и действий в фабрике данных Azure, а также научиться с их помощью создавать комплексные рабочие процессы, управляемые данными, для конкретных бизнес-сценариев.</span><span class="sxs-lookup"><span data-stu-id="31893-247">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="31893-248">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="31893-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="31893-249">Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="31893-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="31893-250">Планирование и исполнение с использованием фабрики данных</span><span class="sxs-lookup"><span data-stu-id="31893-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="31893-251">Здесь объясняются аспекты планирования и исполнения в модели приложений фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="31893-251">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="31893-252">Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению</span><span class="sxs-lookup"><span data-stu-id="31893-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="31893-253">В этой статье описывается мониторинг и отладка конвейеров, а также управление ими с помощью приложения мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="31893-253">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

