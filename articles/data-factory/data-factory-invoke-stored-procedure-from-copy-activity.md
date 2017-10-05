---
title: "Вызов хранимой процедуры из действия копирования в фабрике данных Azure | Документация Microsoft"
description: "Узнайте, как вызвать хранимую процедуру в базе данных SQL Azure или SQL Server из действия копирования в фабрике данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="131c1-103">Вызов хранимой процедуры из действия копирования в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="131c1-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="131c1-104">При копировании данных в базу данных [SQL Server](data-factory-sqlserver-connector.md) или [SQL Azure](data-factory-azure-sql-connector.md) можно настроить класс **SqlSink** в действии копирования для вызова хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="131c1-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="131c1-105">Хранимые процедуры можно использовать для дополнительной обработки (объединения столбцов, поиска значений, вставки в несколько таблиц и т. д.), которая может потребоваться перед вставкой данных в целевую таблицу.</span><span class="sxs-lookup"><span data-stu-id="131c1-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="131c1-106">В этой функции используются [параметры с табличным значением](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="131c1-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="131c1-107">В следующем примере показано, как вызвать хранимую процедуру в базе данных SQL Server из конвейера фабрики данных (действие копирования):</span><span class="sxs-lookup"><span data-stu-id="131c1-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="131c1-108">Определение JSON выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="131c1-108">Output dataset JSON</span></span>
<span data-ttu-id="131c1-109">В определении JSON выходного набора данных задайте для свойства **type** значение **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="131c1-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="131c1-110">При использовании с базой данных SQL Azure задайте для него значение **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="131c1-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="131c1-111">Значение свойства **tableName** должно соответствовать имени первого параметра хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="131c1-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="131c1-112">Раздел SqlSink в определении JSON действия копирования</span><span class="sxs-lookup"><span data-stu-id="131c1-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="131c1-113">Определите раздел **SqlSink** в JSON действия копирования следующим образом.</span><span class="sxs-lookup"><span data-stu-id="131c1-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="131c1-114">Чтобы вызвать хранимую процедуру при вставке данных в целевую базу данных (приемник), необходимо указать значения для свойств **SqlWriterStoredProcedureName** и **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="131c1-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="131c1-115">Описания этих свойств см. в разделе [SqlSink](data-factory-sqlserver-connector.md#sqlsink) статьи, посвященной соединителю SQL Server.</span><span class="sxs-lookup"><span data-stu-id="131c1-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="131c1-116">Определение хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="131c1-116">Stored procedure definition</span></span> 
<span data-ttu-id="131c1-117">В своей базе данных определите хранимую процедуру с тем же именем, что и **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="131c1-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="131c1-118">Хранимая процедура обрабатывает входные данные из исходного хранилища данных и вставляет данные в таблицу в целевой базе данных.</span><span class="sxs-lookup"><span data-stu-id="131c1-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="131c1-119">Имя первого параметра хранимой процедуры должно совпадать со значением свойства tableName, заданным в определении JSON (Marketing) набора данных.</span><span class="sxs-lookup"><span data-stu-id="131c1-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="131c1-120">Определение типа таблицы</span><span class="sxs-lookup"><span data-stu-id="131c1-120">Table type definition</span></span>
<span data-ttu-id="131c1-121">В своей базе данных определите тип таблицы с тем же именем, что и **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="131c1-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="131c1-122">Схема типа таблицы должна соответствовать схеме входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="131c1-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="131c1-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="131c1-123">Next steps</span></span>
<span data-ttu-id="131c1-124">См. следующие статьи о соединителях, где есть полные примеры JSON:</span><span class="sxs-lookup"><span data-stu-id="131c1-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="131c1-125">База данных SQL Azure;</span><span class="sxs-lookup"><span data-stu-id="131c1-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="131c1-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="131c1-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
