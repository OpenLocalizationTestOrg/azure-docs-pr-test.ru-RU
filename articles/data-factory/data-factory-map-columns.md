---
title: "Сопоставление столбцов наборов данных в фабрике данных Azure | Документация Майкрософт"
description: "Узнайте, как сопоставить исходные столбцы с целевыми столбцами."
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
ms.openlocfilehash: a50661b377cfbbff3f1f762342cb275d5da82cea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="map-source-dataset-columns-to-destination-dataset-columns"></a><span data-ttu-id="953ce-103">Сопоставление столбцов исходного набора данных со столбцами целевого набора данных</span><span class="sxs-lookup"><span data-stu-id="953ce-103">Map source dataset columns to destination dataset columns</span></span>
<span data-ttu-id="953ce-104">Сопоставление столбцов можно использовать, чтобы указать, как столбцы, указанные в «structure» исходной схемы таблицы, сопоставляются со столбцами, указанными в «structure» таблицы-приемника.</span><span class="sxs-lookup"><span data-stu-id="953ce-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="953ce-105">Свойство **ColumnMapping** доступно в разделе **typeProperties** действия копирования.</span><span class="sxs-lookup"><span data-stu-id="953ce-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="953ce-106">Сопоставление столбцов применимо в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="953ce-106">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="953ce-107">Все столбцы в разделе structure набора данных, используемого в качестве источника, сопоставляются со всеми столбцами в разделе structure набора данных, используемого в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="953ce-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span></span>
* <span data-ttu-id="953ce-108">Подмножество столбцов в разделе structure набора данных, используемого в качестве источника, сопоставляется со всеми столбцами в разделе structure набора данных, используемого в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="953ce-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span></span>

<span data-ttu-id="953ce-109">Ниже приведены неправильные условия, которые приводят к порождению исключения.</span><span class="sxs-lookup"><span data-stu-id="953ce-109">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="953ce-110">Меньше или больше столбцов в «structure» таблицы-приемника, чем указано в сопоставлении.</span><span class="sxs-lookup"><span data-stu-id="953ce-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="953ce-111">Повторяющееся сопоставление.</span><span class="sxs-lookup"><span data-stu-id="953ce-111">Duplicate mapping.</span></span>
* <span data-ttu-id="953ce-112">В результате запроса SQL нет имени столбца, который указан в сопоставлении.</span><span class="sxs-lookup"><span data-stu-id="953ce-112">SQL query result does not have a column name that is specified in the mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="953ce-113">Приведенные ниже примеры предназначены для SQL Azure и большого двоичного объекта Azure, но подходят для любого хранилища данных, поддерживающего прямоугольные наборы данных.</span><span class="sxs-lookup"><span data-stu-id="953ce-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="953ce-114">В этих примерах можно настроить набор данных и определения связанных служб, чтобы указать данные в соответствующем источнике данных.</span><span class="sxs-lookup"><span data-stu-id="953ce-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="953ce-115">Пример 1. Сопоставление столбцов из SQL Azure с большим двоичным объектом Azure</span><span class="sxs-lookup"><span data-stu-id="953ce-115">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="953ce-116">В этом примере входная таблица имеет структуру, и она указывает на таблицу SQL в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="953ce-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="953ce-117">Выходная таблица имеет структуру, и она указывает на большой двоичный объект в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="953ce-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="953ce-118">Ниже приведен фрагмент JSON, который определяет действие копирования в конвейере.</span><span class="sxs-lookup"><span data-stu-id="953ce-118">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="953ce-119">Столбцы из источника сопоставляются со столбцами в приемнике (**ColumnMappings**) с помощью свойства **Translator**.</span><span class="sxs-lookup"><span data-stu-id="953ce-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span></span>

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
<span data-ttu-id="953ce-120">**Процесс сопоставления столбцов:**</span><span class="sxs-lookup"><span data-stu-id="953ce-120">**Column mapping flow:**</span></span>

![Процесс сопоставления столбцов](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="953ce-122">Пример 2. Сопоставление столбцов из Azure SQL с большим двоичным объектом Azure с помощью SQL-запроса</span><span class="sxs-lookup"><span data-stu-id="953ce-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="953ce-123">В этом примере используется SQL-запрос для извлечения данных из SQL Azure, а не просто указывается имя таблицы и имена столбцов в разделе «structure».</span><span class="sxs-lookup"><span data-stu-id="953ce-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

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
<span data-ttu-id="953ce-124">В этом случае сначала результаты запроса сопоставляются со столбцами, указанными в «structure» источника.</span><span class="sxs-lookup"><span data-stu-id="953ce-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="953ce-125">Затем столбцы из «structure» источника сопоставляются со столбцами в «structure» приемника посредством правил, определенных в columnMappings.</span><span class="sxs-lookup"><span data-stu-id="953ce-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="953ce-126">Предположим, что запрос возвращает 5 столбцов, то есть на два столбца больше, чем указано в разделе structure источника.</span><span class="sxs-lookup"><span data-stu-id="953ce-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span></span>

<span data-ttu-id="953ce-127">**Процесс сопоставления столбцов**</span><span class="sxs-lookup"><span data-stu-id="953ce-127">**Column mapping flow**</span></span>

![Процесс сопоставления столбцов 2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="953ce-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="953ce-129">Next steps</span></span>
<span data-ttu-id="953ce-130">Ознакомьтесь с руководством по использованию действия копирования в следующей статье:</span><span class="sxs-lookup"><span data-stu-id="953ce-130">See the article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="953ce-131">Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL</span><span class="sxs-lookup"><span data-stu-id="953ce-131">Copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
