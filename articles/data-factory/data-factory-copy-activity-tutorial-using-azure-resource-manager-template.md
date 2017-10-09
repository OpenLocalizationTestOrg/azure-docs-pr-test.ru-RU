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
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>Учебник: Использование диспетчера ресурсов Azure шаблона toocreate toocopy данных конвейера фабрики данных 
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Мастер копирования](data-factory-copy-data-wizard-tutorial.md)
> * [Портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Шаблон Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [ИНТЕРФЕЙС REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

В этом учебнике показано как toouse toocreate шаблона диспетчера ресурсов Azure фабрикой данных Azure. конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных. Он не выполняет преобразование входных данных tooproduce выходных данных. Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).

В этом руководстве описывается создание конвейера с одним действием — действием копирования. Действие копирования Hello копирует данные из поддерживаемых хранилища tooa поддерживаемых приемник данных хранилищ данных. Список хранилищ данных, которые поддерживаются в качестве источников и приемников, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Действие Hello выключен глобально доступной можно копировать данные между различными хранилищами данных в виде безопасные, надежные и масштабируемые службы. Дополнительные сведения о действии копирования hello см. в разделе [действия перемещения данных](data-factory-data-movement-activities.md).

Конвейер может содержать сразу несколько действий. Кроме того, можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Дополнительные сведения см. в разделе [Несколько действий в конвейере](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных. Учебник о том, как tootransform данных, с помощью фабрики данных Azure, в разделе [учебника: построение конвейера анализа tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a>Предварительные требования
* Выполните [учебника Обзор и необходимые компоненты](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) и завершения hello **необходимого компонента** действия.
* Следуйте инструкциям в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи tooinstall последнюю версию Azure PowerShell на компьютере. В этом учебнике используйте PowerShell toodeploy фабрики данных сущности. 
* (необязательно) В разделе [разработки шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn шаблоны диспетчера ресурсов Azure.

## <a name="in-this-tutorial"></a>В этом учебнике рассматриваются следующие темы:
В этом учебнике создается фабрики данных с hello, следуя фабрики данных сущности:

| Сущность | Описание |
| --- | --- |
| Связанная служба хранения Azure |Связывает фабрику данных toohello учетной записи хранилища Azure. Хранилище Azure — hello хранилище данных источника и базы данных Azure SQL является хранилищем данных приемник hello для действия копирования hello в учебнике hello. Он указывает hello учетной записи хранилища, содержащий hello входные данные для действия копирования hello. |
| Связанная служба базы данных SQL Azure |Связывает фабрику данных toohello базы данных Azure SQL. Он указывает hello базы данных Azure SQL, содержащий hello выходные данные для действия копирования hello. |
| Входной набор данных BLOB-объекта Azure |Ссылается toohello связанной службой хранилища Azure. Hello связанной службы ссылается tooan учетную запись хранилища Azure и набор данных больших двоичных объектов Azure hello указывает контейнер hello, папки и имя файла в хранилище hello, содержащий hello входных данных. |
| Выходной набор данных SQL Azure |Ссылается toohello связанной службой Azure SQL. Hello связанной службой Azure SQL ссылается tooan Azure SQL server и набора данных Azure SQL hello указывает имя hello hello таблица, содержащая hello выходных данных. |
| Конвейер данных |конвейер Hello содержит одно действие введите копию, которая принимает набор данных BLOB-объектов Azure hello в качестве входных данных и hello набор данных Azure SQL в качестве выходных данных. Действие копирования Hello копирует данные из таблицы в базе данных Azure SQL hello tooa BLOB-объектов Azure. |

Фабрика данных может иметь один или несколько конвейеров. Конвейер может содержать одно или несколько действий. Есть два типа действий: [действия перемещения данных](data-factory-data-movement-activities.md) и [действия преобразования данных](data-factory-data-transformation-activities.md). В этом руководстве описывается создание конвейера с одним действием (действием копирования).

![Копирование больших двоичных объектов Azure tooAzure базы данных SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

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
Создайте JSON-файл с именем **ADFCopyTutorialARM.json** в **C:\ADFGetStarted** папка с hello после содержимого:

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

## <a name="parameters-json"></a>JSON-файл параметров
Создайте JSON-файл с именем **ADFCopyTutorialARM Parameters.json** , содержащий параметры для шаблона Azure Resource Manager hello. 

> [!IMPORTANT]
> Укажите значения имени и ключа вашей учетной записи хранения Azure для параметров storageAccountName и storageAccountKey.  
> 
> Укажите сервер Azure SQL, базу данных, пользователя и пароль для параметров sqlServerName, databaseName, sqlServerUserName и sqlServerPassword.  

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
   * Следующая команда tooselect hello подписки на toowork с выполнения hello.
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. Запустите hello, следующая команда toodeploy фабрики данных сущностей с помощью шаблона диспетчера ресурсов hello, созданный на шаге 1.

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Отслеживание конвейера

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи Azure.
2. Нажмите кнопку **фабрик данных** hello левого меню (или) щелкните **дополнительные службы** и нажмите кнопку **фабрик данных** под **АНАЛИТИКИ + АНАЛИТИКА** Категория.
   
    ![Меню "Фабрики данных"](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. В hello **фабрик данных** страницы, искать и находить фабрики данных (AzureBlobToAzureSQLDatabaseDF). 
   
    ![Поиск фабрики данных](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. Щелкните свою фабрику данных Azure. Вы увидите страницу домашней hello для фабрики данных hello.
   
    ![Домашняя страница фабрики данных](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. Следуйте инструкциям из [отслеживать наборы данных и конвейера](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello конвейера и наборы данных создан в этом учебнике. Сейчас Visual Studio не поддерживает мониторинг конвейеров фабрики данных.
7. Когда срез будет hello **готовности** состоянии, убедитесь, что данные hello скопированный toohello **emp** таблицы в базе данных Azure SQL hello.


Дополнительные сведения о как toouse Azure портала колонках toomonitor конвейера и наборы данных вы создали в этом учебнике см. в разделе [отслеживать наборы данных и конвейера](data-factory-monitor-manage-pipelines.md) .

Дополнительные сведения о том, как toouse hello отслеживать состо & Управление приложения toomonitor данные конвейеров см. в разделе [монитора и управлять ими с помощью мониторинга приложения конвейеров фабрики данных Azure](data-factory-monitor-manage-app.md).

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
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

Это уникальная строка, на основе идентификатора hello ресурсов группы.  

### <a name="defining-data-factory-entities"></a>Определение сущностей фабрики данных
Hello следующие сущности фабрики данных определены в шаблоне hello JSON: 

1. [Связанная служба хранения Azure](#azure-storage-linked-service)
2. [Связанная служба SQL Azure](#azure-sql-database-linked-service)
3. [Набор данных большого двоичного объекта Azure](#azure-blob-dataset)
4. [Набор данных SQL Azure](#azure-sql-dataset)
5. [Конвейер данных с действием копирования](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Связанная служба хранения Azure
Hello AzureStorageLinkedService связывает фабрику данных toohello учетной записи хранилища Azure. Создан контейнер и загруженные в рамках учетной записи хранения данных toothis [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Укажите имя hello и ключ учетной записи хранилища Azure в этом разделе. В разделе [связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) подробные сведения о JSON свойства, используемые toodefine связанная служба хранилища Azure. 

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

Hello connectionString используются параметры storageAccountName и storageAccountKey hello. Hello значения для этих параметров, передаваемых с помощью файла конфигурации. Определение Hello также использует переменные: azureStroageLinkedService и с именем dataFactoryName, определенные в шаблоне hello. 

#### <a name="azure-sql-database-linked-service"></a>Связанная служба базы данных SQL Azure
AzureSqlLinkedService связывает фабрику данных toohello базы данных Azure SQL. Hello данные, копируемые из хранилища больших двоичных объектов hello хранится в этой базе данных. Создана таблица emp hello в этой базе данных как часть [необходимых компонентов](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Укажите имя сервера Azure SQL hello, имя базы данных, имя пользователя и пароль пользователя в этом разделе. В разделе [связанная служба Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) подробные сведения о JSON свойства, используемые toodefine связанная служба SQL Azure.  

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

Hello connectionString использует sqlServerName, имя базы данных, sqlServerUserName и sqlServerPassword параметров, значения которого передаются с помощью файла конфигурации. Hello определение также использует следующие переменные из шаблона hello hello: azureSqlLinkedServiceName с именем dataFactoryName.

#### <a name="azure-blob-dataset"></a>Набор данных большого двоичного объекта Azure
Hello связанной службой хранилища Azure задает строку подключения hello, который использует служба фабрики данных во время выполнения tooconnect tooyour учетной записи хранилища Azure. В определении набора данных BLOB-объектов Azure укажите имена контейнер больших двоичных объектов, папки и файла, содержащего входные данные hello. В разделе [свойства набора данных больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных больших двоичных объектов Azure. 

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

#### <a name="azure-sql-dataset"></a>Набор данных SQL Azure
Укажите имя hello hello таблицы в базе данных Azure SQL hello, содержащий hello скопировать данные из хранилища больших двоичных объектов Azure hello. В разделе [свойства набора данных Azure SQL](data-factory-azure-sql-connector.md#dataset-properties) для получения сведений об toodefine JSON свойства, используемые набором данных Azure SQL. 

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

#### <a name="data-pipeline"></a>Конвейер данных
Определяется конвейера, который копирует данные из набора данных Azure SQL toohello hello Azure BLOB-объекта dataset. В разделе [конвейера JSON](data-factory-create-pipelines.md#pipeline-json) описания toodefine элементы, используемые JSON конвейера в этом примере. 

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

## <a name="reuse-hello-template"></a>Повторное использование шаблона hello
В учебнике hello вы создали шаблон для определения сущностей фабрики данных и для передачи значений для параметров шаблона. конвейер Hello копирует данные из базы Azure SQL tooan учетной записи хранилища Azure, указанного с помощью параметров. toouse Здравствуйте средах toodifferent того же шаблона toodeploy фабрики данных сущности, создать файл параметров для каждой среды и использовать его при развертывании среды toothat.     

Пример:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

Обратите внимание, что hello первая команда использует параметр файла для среды разработки hello, второй hello тестовой среды и hello третий один hello производственную среду.  

Также можно повторно использовать шаблон tooperform hello повторяющиеся задачи. Например, необходимо toocreate множество фабрик данных с одним или более конвейеры, реализующих hello таким же логику, но Каждая фабрика данных использует учетные записи хранилища и базы данных SQL. В этом сценарии используется hello того же шаблона в hello в одной среде (разработки, тестирования или рабочей), с другой параметр файлы toocreate фабрик данных.   

## <a name="next-steps"></a>Дальнейшие действия
В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных. Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn о том, как хранилище данных toocopy из данных, щелкните ссылку hello hello хранилища данных в таблице hello.
