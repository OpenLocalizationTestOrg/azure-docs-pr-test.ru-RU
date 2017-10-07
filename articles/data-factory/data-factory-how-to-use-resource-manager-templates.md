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
# <a name="use-templates-toocreate-azure-data-factory-entities"></a>Использовать шаблоны toocreate фабрики данных Azure сущности
## <a name="overview"></a>Обзор
При использовании фабрики данных Azure по интеграции данных, возможно, вам придется повторно используя Здравствуйте, подход и в разных средах или реализации hello же задачи несколько раз в пределах hello же решения. Шаблоны помогают реализовать эти сценарии и с легкостью управлять ими. Шаблоны в фабрике данных Azure идеально подходят для сценариев, включающих возможность многократного использования и повторения.

Рассмотрим ситуацию hello, которой предоставлен 10 производственных фабриках Здравствуй, мир! организации. журналы Hello из каждого растения хранятся в отдельной локальной базы данных SQL Server. Hello фирма toobuild в одну базу данных в облаке hello ad-hoc аналитики. Кроме того, он хочет toohave hello же логику, но различные конфигурации для разработки, тестирования и рабочих средах.

В этом случае задача должна повторяться toobe внутри hello той же среде, но с разными значениями между hello 10 фабрики данных для каждого завода-изготовителя. По факту **повторение** реализовано. Шаблоны позволяют абстракции hello этот универсальный потока (то есть конвейеров Здравствуйте, имеющих те же действия в каждой фабрики данных), но использует файл отдельный параметр для каждого завод.

Кроме того, как hello организация хочет toodeploy этих фабрик 10 данных несколько раз в различных средах, шаблоны можно использовать это **возможность повторного использования** за счет использования файлы отдельный параметр для разработки, тестирования, и рабочих средах.

## <a name="templating-with-azure-resource-manager"></a>Использование шаблонов с помощью Azure Resource Manager
[Шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) являются шаблонов tooachieve хорошим способом в фабрике данных Azure. Шаблоны диспетчера ресурсов определяют hello инфраструктурой и настройкой решение Azure с использованием файла JSON. Поскольку шаблоны диспетчера ресурсов Azure работают с все или большинство служб Azure, широко используется tooeasily управления ресурсами Azure средств. В разделе [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Подробнее о hello шаблоны диспетчера ресурсов в целом.

## <a name="tutorials"></a>Учебники
См. следующие учебники для сущностей фабрики данных toocreate пошаговые инструкции с помощью шаблонов диспетчера ресурсов hello.

* [Учебник: Создание конвейера toocopy данных с помощью шаблона диспетчера ресурсов Azure](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Учебник: Создание конвейера tooprocess данных с помощью шаблона диспетчера ресурсов Azure](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Шаблоны фабрики данных на сайте GitHub
Ознакомьтесь с hello следующие шаблоны быстрый запуск Azure на GitHub:

* [Создание данных toocopy фабрики данных из хранилища больших двоичных объектов tooAzure базы данных SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Create a Data factory with Hive activity on Azure HDInsight cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) (Создание фабрики данных с действием Hive в кластере Azure HDInsight)
* [Создание данных toocopy фабрики данных из больших двоичных объектов tooAzure Salesforce](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Создать фабрику данных, который связан действий: копирование данных из FTP-сервера tooAzure больших двоичных объектов, вызывает скрипт hive на hello объекта по запросу кластера HDInsight tootransform данных и копирует результат в базе данных SQL Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

Чувствовать себя свободного tooshare шаблонами фабрики данных Azure в [Azure краткого](https://azure.microsoft.com/documentation/templates/). См. toohello [руководство по участию в](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) при разработке шаблоны, которые могут использоваться совместно через этот репозиторий.

Hello в следующих разделах содержатся сведения об определение ресурсов фабрики данных шаблона диспетчера ресурсов.

## <a name="defining-data-factory-resources-in-templates"></a>Определение ресурсов фабрики данных в шаблонах
— Hello верхнего уровня шаблона для определения фабрики данных:

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

### <a name="define-data-factory"></a>Определение фабрики данных
Фабрика данных определить в шаблоне hello диспетчера ресурсов, как показано в следующих образец hello:

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
с именем dataFactoryName Hello определены в «переменные» следующим образом:

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a>Определение связанных служб

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

В разделе [связанной службы хранилища](data-factory-azure-blob-connector.md#azure-storage-linked-service) или [связанные службы вычислений](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) подробные сведения о свойствах hello JSON для hello конкретную связанную службу нужно toodeploy. параметр «dependsOn» Hello указывает имя фабрики данных соответствующего hello. Пример определения связанной службы хранилища Azure отображается в hello после определения JSON:

### <a name="define-datasets"></a>Определение наборов данных

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
См. слишком[поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) подробные сведения о свойствах hello JSON для заданного набора данных типа hello нужно toodeploy. Параметр «dependsOn» hello Примечание задает имя для соответствующих данных hello фабрики и хранения связанной службы. Пример определения типа набора данных из хранилища BLOB-объектов Azure отображается в hello после определения JSON:

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

### <a name="define-pipelines"></a>Определение конвейеров

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

См. слишком[определения конвейеров](data-factory-create-pipelines.md#pipeline-json) для hello сведения о свойствах hello JSON для определения конкретных конвейера и действия нужно toodeploy. Параметр «dependsOn» hello Примечание указывает имя фабрики данных hello и все соответствующие связанные службы или наборов данных. Пример конвейера, который копирует данные из хранилища больших двоичных объектов tooAzure базы данных SQL является показан hello, следующий фрагмент JSON:

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
## <a name="parameterizing-data-factory-template"></a>Параметризация шаблона фабрики данных
Рекомендации по параметризации см. в статье [Рекомендации по созданию шаблонов Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters). Как правило, следует использовать как можно меньше параметров, особенно если вместо них можно использовать переменные. Предоставляет только параметры в hello следующие сценарии:

* параметры различаются в зависимости от среды (например, среда разработки, тестирования и рабочая среда);
* секретов (например, паролей);

Если вам требуется toopull секретные данные из [хранилище ключей Azure](../key-vault/key-vault-get-started.md) при развертывании с помощью шаблонов сущностей фабрики данных Azure, укажите hello **хранилища ключей** и **секретное имя** как показано в Следующий пример Hello:

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
> Хотя Экспорт шаблонов для существующих фабрик данных в настоящее время еще не поддерживается, она используется в hello работает.
>
>
