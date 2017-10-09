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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Руководство. Создание фабрики данных Azure с помощью шаблона диспетчера ресурсов Azure
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-build-your-first-pipeline.md)
> * [Портал Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Шаблон Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

В этой статье используется toocreate шаблона диспетчера ресурсов Azure первый фабрики данных Azure. toodo hello учебника при помощи других средств и пакетов SDK, выберите один из вариантов hello из раскрывающегося списка hello.

конвейер Hello в этот учебник содержит одно действие: **действие Hive в HDInsight**. Это действие выполняет сценарий hive в кластере Azure HDInsight, что преобразует входящие данные tooproduce выходных данных. Hello конвейера — запланированных toorun после времени начала и окончания месяца между hello. 

> [!NOTE]
> конвейер данных Hello в этом учебнике преобразует входные данные tooproduce выходных данных. Учебник по toocopy данных с помощью фабрики данных Azure, см. [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> конвейер Hello в этот учебник содержит только одно действие типа: HDInsightHive. Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>Предварительные требования
* Прочтите [Обзор учебника](data-factory-build-your-first-pipeline.md) статьи и завершения hello **необходимого компонента** действия.
* Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи tooinstall последнюю версию Azure PowerShell на компьютере.
* В разделе [разработки шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn шаблоны диспетчера ресурсов Azure. 

## <a name="in-this-tutorial"></a>В этом учебнике рассматриваются следующие темы:
| Сущность | Описание |
| --- | --- |
| Связанная служба хранения Azure |Связывает фабрику данных toohello учетной записи хранилища Azure. содержит учетную запись хранилища Azure Hello hello входных и выходных данных для конвейера hello в этом образце. |
| Связанная служба кластера HDInsight по запросу |Связывает фабрику данных кластера toohello для HDInsight по требованию. кластер Hello для tooprocess данных автоматически создается и удаляется после завершения обработки hello. |
| Входной набор данных BLOB-объекта Azure |Ссылается toohello связанной службой хранилища Azure. Hello связанной службы ссылается tooan учетную запись хранилища Azure и набор данных больших двоичных объектов Azure hello указывает контейнер hello, папки и имя файла в хранилище hello, содержащий hello входных данных. |
| Выходной набор данных BLOB-объекта Azure |Ссылается toohello связанной службой хранилища Azure. Hello связанной службы ссылается tooan учетную запись хранилища Azure и набор данных больших двоичных объектов Azure hello указывает контейнер hello, папки и имя файла в хранилище hello, содержащий hello выходных данных. |
| Конвейер данных |конвейер Hello содержит одно действие типа HDInsightHive, которая использует hello входного набора данных и создает выходной набор данных hello. |

Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Есть два типа действий: [действия перемещения данных](data-factory-data-movement-activities.md) и [действия преобразования данных](data-factory-data-transformation-activities.md). В этом руководстве описано создание конвейера с одним действием (действием Hive).

Hello следующий раздел содержит hello завершения шаблона диспетчера ресурсов для определения сущностей фабрики данных, позволяющие быстро выполнять через шаблон hello hello учебник и тестирования. toounderstand определение каждой сущности фабрики данных. в разделе [фабрики данных сущности в шаблоне hello](#data-factory-entities-in-the-template) раздела.

## <a name="data-factory-json-template"></a>Шаблон JSON фабрики данных
— Hello верхнего уровня шаблона диспетчера ресурсов для определения фабрики данных: 

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
Создайте JSON-файл с именем **ADFTutorialARM.json** в **C:\ADFGetStarted** папка с hello после содержимого:

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
> Еще один пример шаблона Resource Manager для создания фабрики данных Azure можно найти в статье [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md) (Руководство. Создание конвейера с действием копирования с помощью шаблона Azure Resource Manager).  
> 
> 

## <a name="parameters-json"></a>JSON-файл параметров
Создайте JSON-файл с именем **ADFTutorialARM Parameters.json** , содержащий параметры для шаблона Azure Resource Manager hello.  

> [!IMPORTANT]
> Укажите имя hello и ключ учетной записи хранилища Azure для hello **storageAccountName** и **storageAccountKey** параметров в этот файл параметров. 
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
> Возможно, файлы JSON отдельный параметр для разработки, тестирования и рабочих средах, которые можно использовать с hello того же шаблона JSON фабрики данных. Скрипт PowerShell позволяет автоматизировать развертывание сущностей фабрики данных в этих средах. 
> 
> 

## <a name="create-data-factory"></a>Создание фабрики данных
1. Запуск **Azure PowerShell** и выполнения hello следующую команду: 
   * Запустите следующую команду hello и введите hello имя пользователя и пароль, использовать toosign в toohello портал Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * Запустите следующие команды tooview hello все hello подписки для этой учетной записи.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * Следующая команда tooselect hello подписки на toowork с выполнения hello. Эта подписка должна hello равна hello, который используется в hello портал Azure.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Запустите hello, следующая команда toodeploy фабрики данных сущностей с помощью шаблона диспетчера ресурсов hello, созданный на шаге 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Отслеживание конвейера
1. После входа в toohello [портал Azure](https://portal.azure.com/), нажмите кнопку **Обзор** и выберите **фабрик данных**.
     ![Обзор -> Фабрики данных](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. В hello **фабрик данных** колонка, щелкните фабрики данных hello (**TutorialFactoryARM**) был создан.    
3. В hello **фабрики данных** колонку для фабрики данных, нажмите кнопку **схема**.

     ![Плитка «Схема»](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. В hello **представление диаграммы**, просмотреть обзор конвейеров hello и использовать наборы данных в этом учебнике.
   
   ![Представление схемы](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. В hello представление диаграммы, дважды щелкните набор данных hello **AzureBlobOutput**. Вы увидите, что hello срез, который обрабатывается в данный момент.
   
    ![Выборка](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. После завершения обработки отображается срез hello в **готовности** состояния. Создание используемого по требованию кластера HDInsight обычно занимает некоторое время (около 20 минут). Таким образом, ожидать hello конвейера tootake **около 30 минут** tooprocess hello среза.
   
    ![Выборка](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Если срез hello находится в **готовности** состоянии, проверьте hello **partitioneddata** папки в hello **adfgetstarted** контейнера в хранилище BLOB-объектов для hello выходных данных.  

В разделе [отслеживать наборы данных и конвейера](data-factory-monitor-manage-pipelines.md) инструкции о том, как toouse hello Azure портала колонках toomonitor hello конвейера и наборы данных вы создали в этом учебнике.

Также можно использовать монитор и управлять приложениями toomonitor конвейеры данных. В разделе [монитора и управлять ими с помощью мониторинга приложения конвейеров фабрики данных Azure](data-factory-monitor-manage-app.md) подробные сведения об использовании приложения hello. 

> [!IMPORTANT]
> входной файл Hello, удаляется при успешно обработал hello среза. Таким образом папка hello входного файла (input.log) toohello inputdata контейнера adfgetstarted hello отправки toorerun hello среза или hello учебника.
> 
> 

## <a name="data-factory-entities-in-hello-template"></a>Фабрика сущностями данных в шаблоне hello
### <a name="define-data-factory"></a>Определение фабрики данных
Фабрика данных определить в шаблоне hello диспетчера ресурсов, как показано в следующих образец hello:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
с именем dataFactoryName Hello определяются следующим образом. 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
Это уникальная строка, на основе идентификатора hello ресурсов группы.  

### <a name="defining-data-factory-entities"></a>Определение сущностей фабрики данных
Hello следующие сущности фабрики данных определены в шаблоне hello JSON: 

* [Связанная служба хранения Azure](#azure-storage-linked-service)
* [Связанная служба кластера HDInsight по запросу](#hdinsight-on-demand-linked-service)
* [Входной набор данных большого двоичного объекта Azure](#azure-blob-input-dataset)
* [Выходной набор данных большого двоичного объекта Azure](#azure-blob-output-dataset)
* [Конвейер данных с действием копирования](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Связанная служба хранения Azure
Укажите имя hello и ключ учетной записи хранилища Azure в этом разделе. В разделе [связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойства, используемые toodefine связанная служба хранилища Azure. 

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
Hello **connectionString** использует hello storageAccountName и storageAccountKey параметров. Hello значения для этих параметров, передаваемых с помощью файла конфигурации. Определение Hello также использует переменные: azureStroageLinkedService и с именем dataFactoryName, определенные в шаблоне hello. 

#### <a name="hdinsight-on-demand-linked-service"></a>Связанная служба кластера HDInsight по запросу
В разделе [связанные службы вычислений](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) статьи для получения сведений об toodefine свойства, используемые JSON связанной службы HDInsight по требованию.  

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
Обратите внимание hello после точки. 

* Hello фабрики данных создает **под управлением Linux** кластера HDInsight можно с помощью hello выше JSON. Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). 
* Вместо кластера HDInsight по запросу можно использовать **собственный кластер HDInsight**. См. сведения о [связанной службе Azure HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).
* Создает кластер HDInsight Hello **контейнер по умолчанию** в хранилище больших двоичных объектов hello, указанный в hello JSON (**linkedServiceName**). При удалении hello кластера HDInsight не удаляет этот контейнер. В этом весь замысел. С помощью по требованию связанной службы HDInsight, кластер HDInsight создается каждый раз фрагмент должен обработать, если нет существующего кластера динамической toobe (**timeToLive**) и удаляется при завершении обработки hello.
  
    По мере обработки новых срезов количество контейнеров в хранилище BLOB-объектов будет увеличиваться. Если они не нужны для устранения неполадок hello заданий, вы можете toodelete их затраты на хранение tooreduce hello. имена этих контейнеров Hello соответствуют шаблону: «adf**yourdatafactoryname**-**linkedservicename**- datetimestamp». Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) toodelete контейнеры в Azure хранилище больших двоичных объектов.

Дополнительные сведения см. в разделе [Связанная служба Azure HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).

#### <a name="azure-blob-input-dataset"></a>Входной набор данных большого двоичного объекта Azure
Указывать имена hello контейнер больших двоичных объектов, папки и файла, содержащего входные данные hello. В разделе [свойства набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure. 

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
Это определение использует следующие параметры, определенные в шаблоне параметр hello: blobContainer inputBlobFolder и inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Выходной набор данных BLOB-объекта Azure
Указывать имена hello контейнер больших двоичных объектов и папке, содержащей hello выходных данных. В разделе [свойства набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure.  

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

Это определение использует следующие параметры, определенные в шаблоне параметр hello hello: blobContainer и outputBlobFolder. 

#### <a name="data-pipeline"></a>Конвейер данных
Здесь вы определите конвейер для преобразования данных. Для этого нужно запустить скрипт Hive в кластере Azure HDInsight по требованию. В разделе [конвейера JSON](data-factory-create-pipelines.md#pipeline-json) описания toodefine элементы, используемые JSON конвейера в этом примере. 

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

## <a name="reuse-hello-template"></a>Повторное использование шаблона hello
В учебнике hello вы создали шаблон для определения сущностей фабрики данных и для передачи значений для параметров шаблона. toouse Здравствуйте средах toodifferent того же шаблона toodeploy фабрики данных сущности, создать файл параметров для каждой среды и использовать его при развертывании среды toothat.     

Пример:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Обратите внимание, что hello первая команда использует параметр файла для среды разработки hello, второй hello тестовой среды и hello третий один hello производственную среду.  

Также можно повторно использовать шаблон tooperform hello повторяющиеся задачи. Например требуется toocreate множество фабрик данных с одним или дополнительные конвейеры, реализующих hello же логику, но каждый фабрики использует другой Azure хранилища данных и учетные записи базы данных SQL Azure. В этом сценарии используется hello того же шаблона в hello в одной среде (разработки, тестирования или рабочей), с другой параметр файлы toocreate фабрик данных. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Шаблон Resource Manager для создания шлюза
Ниже приведен образец шаблона диспетчера ресурсов для создания логических шлюза в hello обратно. Установить шлюз на локальном компьютере или ВМ IaaS Azure и зарегистрируйте шлюз hello со службой фабрики данных, с помощью ключа. Дополнительные сведения см. в статье [Перемещение данных между локальными источниками и облаком при помощи шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).

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
Этот шаблон создает фабрику данных с именем GatewayUsingArmDF и шлюз с именем GatewayUsingARM. 

## <a name="see-also"></a>См. также
| Раздел | Описание |
|:--- |:--- |
| [Конвейеры](data-factory-create-pipelines.md) |Эта статья поможет вам понять, конвейеры и действия в фабрике данных Azure и как toouse их tooconstruct конца в конец управляемые данными рабочие процессы сценария или бизнеса. |
| [Наборы данных](data-factory-create-datasets.md) |Эта статья поможет вам понять, что такое наборы данных в фабрике данных Azure. |
| [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md) |В этой статье описываются hello планированием и выполнением аспекты модели приложения фабрики данных Azure. |
| [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md) |В этой статье описывается управление toomonitor и отладка конвейеров с помощью hello мониторинг & приложение для управления. |

