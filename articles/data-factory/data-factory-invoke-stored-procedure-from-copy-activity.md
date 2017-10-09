---
title: "aaaInvoke хранимой процедуры из действия копирования фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как действие копирования tooinvoke хранимую процедуру в базе данных SQL Azure и SQL Server с фабрикой данных Azure."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="4484f-103">Вызов хранимой процедуры из действия копирования в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="4484f-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="4484f-104">При копировании данных в [SQL Server](data-factory-sqlserver-connector.md) или [базы данных SQL Azure](data-factory-azure-sql-connector.md), можно настроить hello **SqlSink** в tooinvoke действия копирования хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="4484f-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="4484f-105">Вы можете toouse hello хранимой процедуры tooperform перед вставкой данных в целевую таблицу toohello требуется дополнительная обработка (Объединение столбцов, поиск значений, вставлять в нескольких таблицах, т. д.).</span><span class="sxs-lookup"><span data-stu-id="4484f-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="4484f-106">В этой функции используются [параметры с табличным значением](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="4484f-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="4484f-107">Следующий образец Hello показано, как tooinvoke хранимую процедуру в SQL Server базы данных из конвейера фабрики данных (действие копирования):</span><span class="sxs-lookup"><span data-stu-id="4484f-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="4484f-108">Определение JSON выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="4484f-108">Output dataset JSON</span></span>
<span data-ttu-id="4484f-109">В hello набор выходных данных JSON, задайте hello **тип** для: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="4484f-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="4484f-110">Задайте для него слишком**AzureSqlTable** toouse с базой данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="4484f-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="4484f-111">Здравствуйте, значение для **tableName** свойство должно соответствовать имени hello первый параметр hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="4484f-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="4484f-112">Раздел SqlSink в определении JSON действия копирования</span><span class="sxs-lookup"><span data-stu-id="4484f-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="4484f-113">Определение hello **SqlSink** раздела действие копирования hello JSON.</span><span class="sxs-lookup"><span data-stu-id="4484f-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="4484f-114">tooinvoke хранимой процедуры во время вставки данных в базу данных или объект назначения приемник hello, указать значения для **SqlWriterStoredProcedureName** и **SqlWriterTableType** свойства.</span><span class="sxs-lookup"><span data-stu-id="4484f-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="4484f-115">Описание этих свойств см. в разделе [SqlSink раздел статьи соединителя SQL Server hello](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="4484f-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="4484f-116">Определение хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="4484f-116">Stored procedure definition</span></span> 
<span data-ttu-id="4484f-117">В базе данных, определить hello хранимой процедуры с hello одинаковые имена, как **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="4484f-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="4484f-118">Hello хранимой процедуры обрабатывает входные данные из хранилища данных источника hello и вставляет данные в таблицу в базе данных назначения hello.</span><span class="sxs-lookup"><span data-stu-id="4484f-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="4484f-119">Имя Hello hello первый параметр хранимой процедуры должно соответствовать tableName hello, определенные в наборе данных hello JSON (маркетинг).</span><span class="sxs-lookup"><span data-stu-id="4484f-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="4484f-120">Определение типа таблицы</span><span class="sxs-lookup"><span data-stu-id="4484f-120">Table type definition</span></span>
<span data-ttu-id="4484f-121">В базе данных, определение типа таблицы hello с hello одинаковые имена, как **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="4484f-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="4484f-122">Схема Hello hello табличного типа должна соответствовать схеме hello hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="4484f-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="4484f-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4484f-123">Next steps</span></span>
<span data-ttu-id="4484f-124">Просмотрите следующие соединителя статьи, в которых для полные примеры JSON hello.</span><span class="sxs-lookup"><span data-stu-id="4484f-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="4484f-125">База данных SQL Azure;</span><span class="sxs-lookup"><span data-stu-id="4484f-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="4484f-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4484f-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
