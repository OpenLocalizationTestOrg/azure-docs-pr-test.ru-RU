---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "aaaLoad данных из Azure хранилище больших двоичных объектов в хранилище данных SQL Azure (фабрики данных Azure) | Документы Microsoft"
description: "Дополнительные сведения tooload данных с помощью фабрики данных Azure"
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: 29a220679a11cedefb0dfd06c0a6838f81a90447
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a>Загрузка данных из хранилища больших двоичных объектов Azure в хранилище данных SQL Azure (фабрика данных Azure).
> [!div class="op_single_selector"]
> * [Фабрика данных](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase;](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 В этом учебнике показано как toocreate конвейера в фабрике данных Azure toomove данных из BLOB-объекта хранилища Azure tooSQL хранилища данных. Следующие шаги hello вы сделаете следующее:

* настроить образец данных в большом двоичном объекте службы хранилища Azure;
* Подключите tooAzure ресурсы фабрики данных.
* Создание данных конвейера toomove из tooSQL хранилища больших двоичных объектов хранилища данных.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Перед началом работы
toofamiliarize самостоятельно с фабрикой данных Azure, в разделе [tooAzure введение фабрики данных][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Создание или определение ресурсов
Перед запуском этого учебника, необходимо toohave hello следующие ресурсы.

* **Хранилище BLOB-объектов Azure**: в этом учебнике используется BLOB-объекта хранилища Azure как hello источник данных для конвейера фабрики данных Azure hello, и поэтому необходимо toohave один доступных toostore hello образец данных. Если у еще его нет, узнайте, как слишком[создать учетную запись хранилища][Create a storage account].
* **Хранилище данных SQL**: этого учебника перемещает hello данные из BLOB-объекта хранилища Azure слишком хранилище данных SQL, поэтому требуется toohave к хранилищу данных через Интернет, заполняемые hello образец данных AdventureWorksDW. Если вы еще нет в хранилище данных, узнайте, как слишком[подготовить один][Create a SQL Data Warehouse]. Если есть хранилище данных, но не удалось инициализировать его с образцами данных hello, вы можете [вручную загрузить][Load sample data into SQL Data Warehouse].
* **Фабрика данных Azure**: фабрики данных Azure завершится реальную нагрузку hello и поэтому необходимо toohave один, которые можно использовать конвейер перемещения данных toobuild hello. Если у еще его нет, узнайте, как toocreate один на шаге 1 из [приступить к работе с фабрикой данных Azure (редактор фабрики данных)][Get started with Azure Data Factory (Data Factory Editor)].
* **AZCopy**: требуется AZCopy toocopy hello образцы данных из вашего локального клиента tooyour BLOB-объекта хранилища Azure. Инструкции по установке, в разделе hello [документации AZCopy][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>Шаг 1: Скопируйте образец данных tooAzure хранилища больших двоичных объектов
После получения всех фрагментов hello готова, вы являетесь готов toocopy образец данных tooyour BLOB-объекта хранилища Azure.

1. [Скачайте демонстрационные данные][Download sample data]. Эти данные добавляется другой трех лет tooyour данные о продажах образец данных AdventureWorksDW.
2. Используйте этот hello toocopy команды AZCopy три года tooyour данных больших двоичных объектов хранилища Azure.

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-tooazure-data-factory"></a>Шаг 2: Подключение tooAzure ресурсы фабрики данных
Теперь, hello данных можно создать hello фабрики данных Azure конвейера toomove hello данных из хранилища BLOB-объектов Azure в хранилище данных SQL.

tooget к работе, откройте hello [портал Azure] [ Azure portal] и выберите из меню слева hello фабрики данных.

### <a name="step-21-create-linked-service"></a>Шаг 2.1. Создание связанной службы
Свяжите учетную запись хранилища Azure и фабрики данных tooyour хранилище данных SQL.  

1. Во-первых начать процесс регистрации hello, щелкнув раздел «Связанной службы» Привет фабрики данных и нажмите кнопку «Новое хранилище данных». Выберите tooregister имя вашего хранилища azure в списке select хранилища Azure в качестве типа, а затем введите имя учетной записи и ключ учетной записи.
2. tooregister хранилище данных SQL перейдите toohello раздел «Автор и развертывание», выберите «Создать хранилище данных» и «Хранилище данных SQL Azure». Скопируйте этот шаблон и добавьте в него свои данные.

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

### <a name="step-22-define-hello-dataset"></a>Шаг 2.2: Определение набора данных hello
После создания hello связанные службы, мы получите наборы данных toodefine hello.  Здесь это означает определения структуры hello hello данных, которая перемещается из хранилища данных tooyour хранилища.  Вы можете прочитать об этом подробнее.

1. Запустите этот процесс, перейдите в раздел «Автор и развернуть» toohello фабрики данных.
2. Нажмите кнопку «Новый набор данных», а затем «Azure Blob storage» toolink фабрики данных tooyour хранилища.  Hello ниже toodefine скрипт можно использовать данные в хранилище больших двоичных объектов Azure:

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


1. Теперь мы настроим также набор данных, предназначенный для хранилища данных SQL.  Мы начнем в hello одинаково, нажав кнопку «Новый набор данных», а затем «Хранилище данных SQL Azure».

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

## <a name="step-3-create-and-run-your-pipeline"></a>Шаг 3. Создание и запуск конвейера
Наконец мы и сделаем настройки и выполнения hello конвейера в фабрике данных Azure.  Это операция hello, которая будет выполнена hello перемещения фактических данных.  Можно найти полный просмотр hello операций, которые можно выполнить с хранилищем данных SQL и фабрики данных Azure [здесь][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

В разделе «Автор и развернуть» hello Теперь нажмите кнопку «Более команды» и выберите «Новый конвейер».  После создания конвейера hello, можно использовать hello ниже tooyour кода tootransfer hello данных хранилища данных:

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

## <a name="next-steps"></a>Дальнейшие действия
toolearn больше, начните с просмотра:

* [Схема обучения по фабрике данных Azure][Azure Data Factory learning path].
* [Перемещение данных в хранилище данных Azure SQL и из него с помощью фабрики данных Azure][Azure SQL Data Warehouse Connector]. Это hello core справочном разделе для использования фабрики данных Azure с хранилищем данных SQL Azure.

В приведенных ниже статьях содержатся подробные сведения о фабрике данных Azure. Они обсуждают базы данных SQL Azure или HDinsight, но hello сведения также относятся tooAzure хранилище данных SQL.

* [Учебник: Приступая к работе с фабрикой данных Azure] [ Tutorial: Get started with Azure Data Factory] это учебник hello основных компонентов для обработки данных с помощью фабрики данных Azure. В этом учебнике будут построены вашего первого конвейера, который использует HDInsight tootransform и анализировать веб-журналы на ежемесячной основе. Обратите внимание, что в этом руководстве копирование не используется.
* [Учебник: Копирование данных из больших двоичных объектов хранилища Azure tooAzure базы данных SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. В этом учебнике будет создана конвейера в фабрике данных Azure toocopy данных из больших двоичных объектов хранилища Azure tooAzure базы данных SQL.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
