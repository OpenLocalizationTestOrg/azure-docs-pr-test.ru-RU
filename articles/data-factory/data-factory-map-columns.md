---
title: "aaaMapping столбцов набора данных в фабрике данных Azure | Документы Microsoft"
description: "Узнайте, как столбцы toodestination столбцов источника toomap."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="17bd2-103">Сопоставление столбцов исходного набора данных столбцы toodestination набора данных</span><span class="sxs-lookup"><span data-stu-id="17bd2-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="17bd2-104">Сопоставление столбцов можно использовать toospecify как столбцов, указанных в «структура» из исходной таблицы карты toocolumns hello, указанный в hello «структура» таблицы приемника.</span><span class="sxs-lookup"><span data-stu-id="17bd2-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="17bd2-105">Hello **columnMapping** это свойство доступно в hello **typeProperties** раздел hello действие копирования.</span><span class="sxs-lookup"><span data-stu-id="17bd2-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="17bd2-106">Сопоставление столбцов поддерживает hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="17bd2-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="17bd2-107">Все столбцы в структуре набора данных источника hello являются сопоставленных tooall в структуре набора данных приемник hello.</span><span class="sxs-lookup"><span data-stu-id="17bd2-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="17bd2-108">Подмножество столбцов hello в структуре набора данных источника hello — tooall сопоставленных столбцов в структуре набора данных приемник hello.</span><span class="sxs-lookup"><span data-stu-id="17bd2-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="17bd2-109">Hello ниже приведены условия ошибок, которые приводят к возникновению исключения.</span><span class="sxs-lookup"><span data-stu-id="17bd2-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="17bd2-110">Меньшее число столбцов или столбцов в hello «структура» таблицы приемника указан в сопоставлении hello.</span><span class="sxs-lookup"><span data-stu-id="17bd2-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="17bd2-111">Повторяющееся сопоставление.</span><span class="sxs-lookup"><span data-stu-id="17bd2-111">Duplicate mapping.</span></span>
* <span data-ttu-id="17bd2-112">Результат запроса SQL не имеет имени столбца, который указан в сопоставлении hello.</span><span class="sxs-lookup"><span data-stu-id="17bd2-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="17bd2-113">Hello следующие образцы для Azure SQL и больших двоичных объектов Azure но применимо tooany хранилища данных, которое поддерживает прямоугольный наборов данных.</span><span class="sxs-lookup"><span data-stu-id="17bd2-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="17bd2-114">Измените набор данных и определения связанной службы в примерах toopoint toodata в hello соответствующий источник данных.</span><span class="sxs-lookup"><span data-stu-id="17bd2-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="17bd2-115">Пример 1 – из большого двоичного объекта Azure SQL tooAzure сопоставления столбцов</span><span class="sxs-lookup"><span data-stu-id="17bd2-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="17bd2-116">В этом образце hello входной таблицы имеет структуру, и он указывает tooa SQL таблицы в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="17bd2-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="17bd2-117">В этом образце hello выходная таблица имеет структуру, и он указывает tooa больших двоичных объектов в службе хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="17bd2-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="17bd2-118">Привет, следуя JSON определяет операции копирования в конвейере.</span><span class="sxs-lookup"><span data-stu-id="17bd2-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="17bd2-119">Сопоставление столбцов Hello из источника toocolumns в приемник (**columnMappings**) с помощью hello **переводчик** свойство.</span><span class="sxs-lookup"><span data-stu-id="17bd2-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
<span data-ttu-id="17bd2-120">**Процесс сопоставления столбцов:**</span><span class="sxs-lookup"><span data-stu-id="17bd2-120">**Column mapping flow:**</span></span>

![Процесс сопоставления столбцов](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="17bd2-122">Пример 2 — с SQL-запрос из большого двоичного объекта Azure SQL tooAzure сопоставления столбцов</span><span class="sxs-lookup"><span data-stu-id="17bd2-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="17bd2-123">В этом примере SQL-запрос — используется tooextract данные из Azure SQL вместо просто указания имени таблицы hello и имена столбцов hello в разделе «Структура».</span><span class="sxs-lookup"><span data-stu-id="17bd2-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
<span data-ttu-id="17bd2-124">В этом случае результаты запроса hello — первый сопоставленный toocolumns, указанный в «Структура» источника.</span><span class="sxs-lookup"><span data-stu-id="17bd2-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="17bd2-125">Далее hello столбцы из источника «структура», сопоставленные toocolumns в приемник «структура» с правилами, определенными в columnMappings.</span><span class="sxs-lookup"><span data-stu-id="17bd2-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="17bd2-126">Предположим, что hello запрос возвращает 5 столбцов, двух дополнительных столбцов, чем указано в hello «Структура» источника.</span><span class="sxs-lookup"><span data-stu-id="17bd2-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="17bd2-127">**Процесс сопоставления столбцов**</span><span class="sxs-lookup"><span data-stu-id="17bd2-127">**Column mapping flow**</span></span>

![Процесс сопоставления столбцов 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="17bd2-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17bd2-129">Next steps</span></span>
<span data-ttu-id="17bd2-130">В статье hello учебник по использованию действии копирования:</span><span class="sxs-lookup"><span data-stu-id="17bd2-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="17bd2-131">Копирование данных из хранилища больших двоичных объектов tooSQL базы данных</span><span class="sxs-lookup"><span data-stu-id="17bd2-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
