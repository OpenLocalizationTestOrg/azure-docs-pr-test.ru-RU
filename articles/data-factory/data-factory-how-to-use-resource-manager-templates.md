---
title: "Использование шаблонов Resource Manager в фабрике данных | Документация Майкрософт"
description: "Узнайте, как создать шаблоны Azure Resource Manager и использовать их для создания сущностей фабрики данных."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="b3436-103">Создание сущностей фабрики данных Azure с помощью шаблонов</span><span class="sxs-lookup"><span data-stu-id="b3436-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="b3436-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b3436-104">Overview</span></span>
<span data-ttu-id="b3436-105">Пользуясь фабрикой данных Azure для интеграции данных, возможно, вы захотите повторно использовать один и тот же шаблон в разных средах или несколько раз реализовать одну задачу в том же самом решении.</span><span class="sxs-lookup"><span data-stu-id="b3436-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="b3436-106">Шаблоны помогают реализовать эти сценарии и с легкостью управлять ими.</span><span class="sxs-lookup"><span data-stu-id="b3436-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="b3436-107">Шаблоны в фабрике данных Azure идеально подходят для сценариев, включающих возможность многократного использования и повторения.</span><span class="sxs-lookup"><span data-stu-id="b3436-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="b3436-108">Рассмотрим ситуацию, когда организация имеет 10 производственных фабрик по всему миру.</span><span class="sxs-lookup"><span data-stu-id="b3436-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="b3436-109">Журналы каждой фабрики хранятся в отдельной локальной базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b3436-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="b3436-110">Компания хочет создать одно хранилище данных в облаке для ad-hoc-анализа.</span><span class="sxs-lookup"><span data-stu-id="b3436-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="b3436-111">Требуется также использовать одну логику и разные конфигурации для сред разработки, тестирования и рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="b3436-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="b3436-112">В этом случае в пределах одной среды задача выполняется несколько раз. Однако при этом для каждой производственной фабрики следует использовать разные значения в 10 фабриках данных.</span><span class="sxs-lookup"><span data-stu-id="b3436-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="b3436-113">По факту **повторение** реализовано.</span><span class="sxs-lookup"><span data-stu-id="b3436-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="b3436-114">Использование шаблонов (то есть одинаковых действий в конвейерах в каждой фабрике данных) позволяет абстрагировать этот общий процесс. Однако при этом для каждой производственной фабрики используется отдельный файл параметров.</span><span class="sxs-lookup"><span data-stu-id="b3436-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="b3436-115">Кроме того, так как организации нужно развернуть эти 10 фабрик данных несколько раз в различных средах, шаблоны могут получить эту **возможность многократного использования** за счет использования отдельных файлов параметров для сред разработки, тестирования и рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="b3436-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="b3436-116">Использование шаблонов с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3436-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="b3436-117">[Шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) — отличный способ реализации возможности использования шаблонов в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="b3436-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="b3436-118">Они определяют инфраструктуру и конфигурацию решения Azure в JSON-файле.</span><span class="sxs-lookup"><span data-stu-id="b3436-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="b3436-119">Так как шаблоны Azure Resource Manager совместимы почти со всеми службами Azure, с их помощью можно упростить управление всеми ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="b3436-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="b3436-120">Общие сведения о шаблонах Azure Resource Manager см. в статье [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b3436-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="b3436-121">Учебники</span><span class="sxs-lookup"><span data-stu-id="b3436-121">Tutorials</span></span>
<span data-ttu-id="b3436-122">Пошаговые инструкции по созданию сущностей фабрики данных с помощью шаблонов Resource Manager см. в следующих руководствах:</span><span class="sxs-lookup"><span data-stu-id="b3436-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* <span data-ttu-id="b3436-123">[Tutorial: Create a pipeline to copy data by using Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Руководство. Создание конвейера для копирования данных с помощью шаблона Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="b3436-123">[Tutorial: Create a pipeline to copy data by using Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)</span></span>
* <span data-ttu-id="b3436-124">[Tutorial: Create a pipeline to process data by using Azure Resource Manager template](data-factory-build-your-first-pipeline.md) (Руководство. Создание конвейера для обработки данных с помощью шаблона Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="b3436-124">[Tutorial: Create a pipeline to process data by using Azure Resource Manager template](data-factory-build-your-first-pipeline.md)</span></span>

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="b3436-125">Шаблоны фабрики данных на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="b3436-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="b3436-126">Ознакомьтесь со следующими шаблонами быстрого запуска Azure на сайте GitHub:</span><span class="sxs-lookup"><span data-stu-id="b3436-126">Check out the following Azure quick start templates on GitHub:</span></span>

* <span data-ttu-id="b3436-127">[Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) (Создание фабрики данных для копирования данных из хранилища BLOB-объектов Azure в Базу данных SQL Azure)</span><span class="sxs-lookup"><span data-stu-id="b3436-127">[Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)</span></span>
* <span data-ttu-id="b3436-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Создание фабрики данных с действием Hive в кластере Azure HDInsight)</span><span class="sxs-lookup"><span data-stu-id="b3436-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)</span></span>
* <span data-ttu-id="b3436-129">[Create a Data factory to copy data from Salesforce to Azure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) (Создание фабрики данных для копирования данных из Salesforce в большие двоичные объекты Azure)</span><span class="sxs-lookup"><span data-stu-id="b3436-129">[Create a Data factory to copy data from Salesforce to Azure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)</span></span>
* [<span data-ttu-id="b3436-130">Создание фабрики данных, которая связывает действия в цепочку: копирует данные из FTP-сервера в большие двоичные объекты Azure, вызывает скрипт Hive в кластере HDInsight по запросу для преобразования данных и копирует результаты в базу данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="b3436-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="b3436-131">Вы можете поделиться своими шаблонами фабрики данных Azure на странице [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="b3436-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="b3436-132">Если вы разрабатываете шаблоны, к которым можно предоставить общий доступ в этом репозитории, см. [руководство по добавлению](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).</span><span class="sxs-lookup"><span data-stu-id="b3436-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="b3436-133">В следующих разделах представлены сведения об определении ресурсов фабрики данных в шаблоне Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3436-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="b3436-134">Определение ресурсов фабрики данных в шаблонах</span><span class="sxs-lookup"><span data-stu-id="b3436-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="b3436-135">Шаблон верхнего уровня для определения фабрики данных выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b3436-135">The top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="b3436-136">Определение фабрики данных</span><span class="sxs-lookup"><span data-stu-id="b3436-136">Define data factory</span></span>
<span data-ttu-id="b3436-137">Фабрику данных следует определить в шаблоне Resource Manager, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b3436-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="b3436-138">Параметр dataFactoryName определяется в разделе переменных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b3436-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="b3436-139">Определение связанных служб</span><span class="sxs-lookup"><span data-stu-id="b3436-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="b3436-140">Дополнительные сведения о свойствах JSON для конкретной связанной службы, которую нужно развернуть, см. в разделе [Связанная служба хранилища](data-factory-azure-blob-connector.md#azure-storage-linked-service) или [Связанные службы вычислений](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b3436-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="b3436-141">Параметр dependsOn указывает имя соответствующей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="b3436-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="b3436-142">Пример определения связанной службы для службы хранилища Azure показан в следующем определении JSON:</span><span class="sxs-lookup"><span data-stu-id="b3436-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="b3436-143">Определение наборов данных</span><span class="sxs-lookup"><span data-stu-id="b3436-143">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="b3436-144">Дополнительные сведения о свойствах JSON для конкретного типа набора данных, который нужно развернуть, см. в разделе [Поддерживаемые хранилища данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b3436-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="b3436-145">Обратите внимание, что параметр dependsOn указывает имя соответствующей фабрики данных и связанной службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="b3436-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="b3436-146">Пример определения типа набора данных хранилища BLOB-объектов Azure показан в следующем определении JSON:</span><span class="sxs-lookup"><span data-stu-id="b3436-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="b3436-147">Определение конвейеров</span><span class="sxs-lookup"><span data-stu-id="b3436-147">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="b3436-148">Дополнительные сведения о свойствах JSON для определения конкретного конвейера и действий, которые нужно развернуть, см. в разделе [Определение конвейеров](data-factory-create-pipelines.md#pipeline-json).</span><span class="sxs-lookup"><span data-stu-id="b3436-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="b3436-149">Обратите внимание, что параметр dependsOn указывает имя фабрики данных, а также все соответствующие связанные службы или наборы данных.</span><span class="sxs-lookup"><span data-stu-id="b3436-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="b3436-150">В следующем фрагменте кода JSON показан пример конвейера, копирующего данные из хранилища BLOB-объектов Azure в Базу данных SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="b3436-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="b3436-151">Параметризация шаблона фабрики данных</span><span class="sxs-lookup"><span data-stu-id="b3436-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="b3436-152">Рекомендации по параметризации см. в статье [Рекомендации по созданию шаблонов Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="b3436-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="b3436-153">Как правило, следует использовать как можно меньше параметров, особенно если вместо них можно использовать переменные.</span><span class="sxs-lookup"><span data-stu-id="b3436-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="b3436-154">Предоставляйте параметры только в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="b3436-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="b3436-155">параметры различаются в зависимости от среды (например, среда разработки, тестирования и рабочая среда);</span><span class="sxs-lookup"><span data-stu-id="b3436-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="b3436-156">секретов (например, паролей);</span><span class="sxs-lookup"><span data-stu-id="b3436-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="b3436-157">Если при развертывании сущностей фабрики данных Azure с помощью шаблонов секреты необходимо извлечь из [хранилища ключей Azure](../key-vault/key-vault-get-started.md), укажите **хранилище ключей** и **секретное имя**, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b3436-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="b3436-158">Сейчас экспорт шаблонов для существующих фабрик данных не поддерживается. Однако планируется реализовать такую возможность.</span><span class="sxs-lookup"><span data-stu-id="b3436-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
