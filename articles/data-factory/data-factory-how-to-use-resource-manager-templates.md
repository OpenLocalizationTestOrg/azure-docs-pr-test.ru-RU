---
title: "шаблоны диспетчера ресурсов aaaUse в фабрике данных | Документы Microsoft"
description: "Узнайте, как toocreate и использование сущностей фабрики данных Azure Resource Manager шаблоны toocreate."
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
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="22713-103">Использовать шаблоны toocreate фабрики данных Azure сущности</span><span class="sxs-lookup"><span data-stu-id="22713-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="22713-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="22713-104">Overview</span></span>
<span data-ttu-id="22713-105">При использовании фабрики данных Azure по интеграции данных, возможно, вам придется повторно используя Здравствуйте, подход и в разных средах или реализации hello же задачи несколько раз в пределах hello же решения.</span><span class="sxs-lookup"><span data-stu-id="22713-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="22713-106">Шаблоны помогают реализовать эти сценарии и с легкостью управлять ими.</span><span class="sxs-lookup"><span data-stu-id="22713-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="22713-107">Шаблоны в фабрике данных Azure идеально подходят для сценариев, включающих возможность многократного использования и повторения.</span><span class="sxs-lookup"><span data-stu-id="22713-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="22713-108">Рассмотрим ситуацию hello, которой предоставлен 10 производственных фабриках Здравствуй, мир! организации.</span><span class="sxs-lookup"><span data-stu-id="22713-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="22713-109">журналы Hello из каждого растения хранятся в отдельной локальной базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="22713-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="22713-110">Hello фирма toobuild в одну базу данных в облаке hello ad-hoc аналитики.</span><span class="sxs-lookup"><span data-stu-id="22713-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="22713-111">Кроме того, он хочет toohave hello же логику, но различные конфигурации для разработки, тестирования и рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="22713-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="22713-112">В этом случае задача должна повторяться toobe внутри hello той же среде, но с разными значениями между hello 10 фабрики данных для каждого завода-изготовителя.</span><span class="sxs-lookup"><span data-stu-id="22713-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="22713-113">По факту **повторение** реализовано.</span><span class="sxs-lookup"><span data-stu-id="22713-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="22713-114">Шаблоны позволяют абстракции hello этот универсальный потока (то есть конвейеров Здравствуйте, имеющих те же действия в каждой фабрики данных), но использует файл отдельный параметр для каждого завод.</span><span class="sxs-lookup"><span data-stu-id="22713-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="22713-115">Кроме того, как hello организация хочет toodeploy этих фабрик 10 данных несколько раз в различных средах, шаблоны можно использовать это **возможность повторного использования** за счет использования файлы отдельный параметр для разработки, тестирования, и рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="22713-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="22713-116">Использование шаблонов с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22713-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="22713-117">[Шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) являются шаблонов tooachieve хорошим способом в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="22713-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="22713-118">Шаблоны диспетчера ресурсов определяют hello инфраструктурой и настройкой решение Azure с использованием файла JSON.</span><span class="sxs-lookup"><span data-stu-id="22713-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="22713-119">Поскольку шаблоны диспетчера ресурсов Azure работают с все или большинство служб Azure, широко используется tooeasily управления ресурсами Azure средств.</span><span class="sxs-lookup"><span data-stu-id="22713-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="22713-120">В разделе [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Подробнее о hello шаблоны диспетчера ресурсов в целом.</span><span class="sxs-lookup"><span data-stu-id="22713-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="22713-121">Учебники</span><span class="sxs-lookup"><span data-stu-id="22713-121">Tutorials</span></span>
<span data-ttu-id="22713-122">См. следующие учебники для сущностей фабрики данных toocreate пошаговые инструкции с помощью шаблонов диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="22713-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="22713-123">Учебник: Создание конвейера toocopy данных с помощью шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="22713-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="22713-124">Учебник: Создание конвейера tooprocess данных с помощью шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="22713-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="22713-125">Шаблоны фабрики данных на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="22713-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="22713-126">Ознакомьтесь с hello следующие шаблоны быстрый запуск Azure на GitHub:</span><span class="sxs-lookup"><span data-stu-id="22713-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="22713-127">Создание данных toocopy фабрики данных из хранилища больших двоичных объектов tooAzure базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="22713-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* <span data-ttu-id="22713-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Создание фабрики данных с действием Hive в кластере Azure HDInsight)</span><span class="sxs-lookup"><span data-stu-id="22713-128">[Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)</span></span>
* [<span data-ttu-id="22713-129">Создание данных toocopy фабрики данных из больших двоичных объектов tooAzure Salesforce</span><span class="sxs-lookup"><span data-stu-id="22713-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="22713-130">Создать фабрику данных, который связан действий: копирование данных из FTP-сервера tooAzure больших двоичных объектов, вызывает скрипт hive на hello объекта по запросу кластера HDInsight tootransform данных и копирует результат в базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="22713-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="22713-131">Чувствовать себя свободного tooshare шаблонами фабрики данных Azure в [Azure краткого](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="22713-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="22713-132">См. toohello [руководство по участию в](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) при разработке шаблоны, которые могут использоваться совместно через этот репозиторий.</span><span class="sxs-lookup"><span data-stu-id="22713-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="22713-133">Hello в следующих разделах содержатся сведения об определение ресурсов фабрики данных шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="22713-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="22713-134">Определение ресурсов фабрики данных в шаблонах</span><span class="sxs-lookup"><span data-stu-id="22713-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="22713-135">— Hello верхнего уровня шаблона для определения фабрики данных:</span><span class="sxs-lookup"><span data-stu-id="22713-135">hello top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="22713-136">Определение фабрики данных</span><span class="sxs-lookup"><span data-stu-id="22713-136">Define data factory</span></span>
<span data-ttu-id="22713-137">Фабрика данных определить в шаблоне hello диспетчера ресурсов, как показано в следующих образец hello:</span><span class="sxs-lookup"><span data-stu-id="22713-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="22713-138">с именем dataFactoryName Hello определены в «переменные» следующим образом:</span><span class="sxs-lookup"><span data-stu-id="22713-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="22713-139">Определение связанных служб</span><span class="sxs-lookup"><span data-stu-id="22713-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="22713-140">В разделе [связанной службы хранилища](data-factory-azure-blob-connector.md#azure-storage-linked-service) или [связанные службы вычислений](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) подробные сведения о свойствах hello JSON для hello конкретную связанную службу нужно toodeploy.</span><span class="sxs-lookup"><span data-stu-id="22713-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="22713-141">параметр «dependsOn» Hello указывает имя фабрики данных соответствующего hello.</span><span class="sxs-lookup"><span data-stu-id="22713-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="22713-142">Пример определения связанной службы хранилища Azure отображается в hello после определения JSON:</span><span class="sxs-lookup"><span data-stu-id="22713-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="22713-143">Определение наборов данных</span><span class="sxs-lookup"><span data-stu-id="22713-143">Define datasets</span></span>

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
<span data-ttu-id="22713-144">См. слишком[поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) подробные сведения о свойствах hello JSON для заданного набора данных типа hello нужно toodeploy.</span><span class="sxs-lookup"><span data-stu-id="22713-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="22713-145">Параметр «dependsOn» hello Примечание задает имя для соответствующих данных hello фабрики и хранения связанной службы.</span><span class="sxs-lookup"><span data-stu-id="22713-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="22713-146">Пример определения типа набора данных из хранилища BLOB-объектов Azure отображается в hello после определения JSON:</span><span class="sxs-lookup"><span data-stu-id="22713-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="22713-147">Определение конвейеров</span><span class="sxs-lookup"><span data-stu-id="22713-147">Define pipelines</span></span>

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

<span data-ttu-id="22713-148">См. слишком[определения конвейеров](data-factory-create-pipelines.md#pipeline-json) для hello сведения о свойствах hello JSON для определения конкретных конвейера и действия нужно toodeploy.</span><span class="sxs-lookup"><span data-stu-id="22713-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="22713-149">Параметр «dependsOn» hello Примечание указывает имя фабрики данных hello и все соответствующие связанные службы или наборов данных.</span><span class="sxs-lookup"><span data-stu-id="22713-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="22713-150">Пример конвейера, который копирует данные из хранилища больших двоичных объектов tooAzure базы данных SQL является показан hello, следующий фрагмент JSON:</span><span class="sxs-lookup"><span data-stu-id="22713-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="22713-151">Параметризация шаблона фабрики данных</span><span class="sxs-lookup"><span data-stu-id="22713-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="22713-152">Рекомендации по параметризации см. в статье [Рекомендации по созданию шаблонов Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="22713-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="22713-153">Как правило, следует использовать как можно меньше параметров, особенно если вместо них можно использовать переменные.</span><span class="sxs-lookup"><span data-stu-id="22713-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="22713-154">Предоставляет только параметры в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="22713-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="22713-155">параметры различаются в зависимости от среды (например, среда разработки, тестирования и рабочая среда);</span><span class="sxs-lookup"><span data-stu-id="22713-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="22713-156">секретов (например, паролей);</span><span class="sxs-lookup"><span data-stu-id="22713-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="22713-157">Если вам требуется toopull секретные данные из [хранилище ключей Azure](../key-vault/key-vault-get-started.md) при развертывании с помощью шаблонов сущностей фабрики данных Azure, укажите hello **хранилища ключей** и **секретное имя** как показано в Следующий пример Hello:</span><span class="sxs-lookup"><span data-stu-id="22713-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

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
> <span data-ttu-id="22713-158">Хотя Экспорт шаблонов для существующих фабрик данных в настоящее время еще не поддерживается, она используется в hello работает.</span><span class="sxs-lookup"><span data-stu-id="22713-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
