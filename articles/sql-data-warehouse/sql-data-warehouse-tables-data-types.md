---
title: "Руководство по типам данных. Хранилище данных SQL Azure | Документация Майкрософт"
description: "Рекомендации для определения типов данных, совместимых с хранилищем данных SQL."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 5c24c71af16bd9851d9caf15fecfa4bb76f5f77e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="35db8-103">Руководство по определению типов данных для таблиц в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="35db8-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="35db8-104">Используйте эти рекомендации для определения типов данных таблиц, совместимых с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="35db8-104">Use these recommendations to define table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="35db8-105">Кроме обеспечения совместимости, уменьшение размера типов данных повышает производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="35db8-105">In addition to compatibility, minimizing the size of data types improves query performance.</span></span>

<span data-ttu-id="35db8-106">Хранилище данных SQL поддерживает самые распространенные типы данных.</span><span class="sxs-lookup"><span data-stu-id="35db8-106">SQL Data Warehouse supports the most commonly used data types.</span></span> <span data-ttu-id="35db8-107">Список поддерживаемых типов данных см. в [типах данных](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) в инструкции CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="35db8-107">For a list of the supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in the CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="35db8-108">Уменьшение длины строки</span><span class="sxs-lookup"><span data-stu-id="35db8-108">Minimize row length</span></span>
<span data-ttu-id="35db8-109">Уменьшение размера типов данных сокращает длину строки, что улучшает производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="35db8-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span></span> <span data-ttu-id="35db8-110">Используйте наименьший тип данных для данных.</span><span class="sxs-lookup"><span data-stu-id="35db8-110">Use the smallest data type that works for your data.</span></span> 

- <span data-ttu-id="35db8-111">Не рекомендуется использовать по умолчанию длинные значения столбцов.</span><span class="sxs-lookup"><span data-stu-id="35db8-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="35db8-112">Например, если самое длинное значение состоит из 25 знаков, столбец необходимо определить как VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="35db8-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="35db8-113">Не нужно использовать [NVARCHAR][NVARCHAR], если вам требуется только VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="35db8-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="35db8-114">По возможности используйте NVARCHAR(4000) или VARCHAR(8000) вместо NVARCHAR(MAX) или VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="35db8-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="35db8-115">Если для загрузки таблиц используется Polybase, определенная длина таблицы не должна превышать 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="35db8-115">If you are using Polybase to load your tables, the defined length of the table row cannot exceed 1 MB.</span></span> <span data-ttu-id="35db8-116">Если строка с данными переменной длины превышает 1 МБ, можно загрузить строку с помощью BCP, а не PolyBase.</span><span class="sxs-lookup"><span data-stu-id="35db8-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="35db8-117">Определение неподдерживаемых типов данных</span><span class="sxs-lookup"><span data-stu-id="35db8-117">Identify unsupported data types</span></span>
<span data-ttu-id="35db8-118">Если вы переносите базу данных из другой базы данных SQL, вы можете обнаружить некоторые типы данных, неподдерживаемые в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="35db8-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="35db8-119">Используйте этот запрос для определения неподдерживаемых типов данных в существующей схеме SQL.</span><span class="sxs-lookup"><span data-stu-id="35db8-119">Use this query to discover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="35db8-120"><a name="unsupported-data-types"></a>Использование обходных решений для неподдерживаемых типов данных</span><span class="sxs-lookup"><span data-stu-id="35db8-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="35db8-121">Ниже перечислены типы данных, неподдерживаемые хранилищем данных SQL, а также варианты, доступные для использования вместо неподдерживаемых типов данных.</span><span class="sxs-lookup"><span data-stu-id="35db8-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span></span>

| <span data-ttu-id="35db8-122">Неподдерживаемые типы данных</span><span class="sxs-lookup"><span data-stu-id="35db8-122">Unsupported data type</span></span> | <span data-ttu-id="35db8-123">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="35db8-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="35db8-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="35db8-124">[geometry][geometry]</span></span> |<span data-ttu-id="35db8-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="35db8-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="35db8-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="35db8-126">[geography][geography]</span></span> |<span data-ttu-id="35db8-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="35db8-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="35db8-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="35db8-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="35db8-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="35db8-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="35db8-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="35db8-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="35db8-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="35db8-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="35db8-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="35db8-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="35db8-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="35db8-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="35db8-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="35db8-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="35db8-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="35db8-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="35db8-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="35db8-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="35db8-137">Разделите столбец на несколько строго типизированных столбцов.</span><span class="sxs-lookup"><span data-stu-id="35db8-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="35db8-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="35db8-138">[table][table]</span></span> |<span data-ttu-id="35db8-139">Преобразуйте во временные таблицы.</span><span class="sxs-lookup"><span data-stu-id="35db8-139">Convert to temporary tables.</span></span> |
| <span data-ttu-id="35db8-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="35db8-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="35db8-141">Переработайте код, чтобы использовать [datetime2][datetime2] и функцию `CURRENT_TIMESTAMP`.</span><span class="sxs-lookup"><span data-stu-id="35db8-141">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="35db8-142">По умолчанию поддерживаются только константы, поэтому нельзя использовать current_timestamp как ограничение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="35db8-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="35db8-143">Если нужно перенести значения версии строки из типизированного столбца timestamp, используйте [BINARY][BINARY](8) или [VARBINARY][BINARY](8) для значений версии строки NOT NULL или NULL.</span><span class="sxs-lookup"><span data-stu-id="35db8-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="35db8-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="35db8-144">[xml][xml]</span></span> |<span data-ttu-id="35db8-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="35db8-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="35db8-146">[тип, определенный пользователем][user defined types]</span><span class="sxs-lookup"><span data-stu-id="35db8-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="35db8-147">По возможности выполните преобразование в исходный тип данных.</span><span class="sxs-lookup"><span data-stu-id="35db8-147">Convert back to the native data type when possible.</span></span> |
| <span data-ttu-id="35db8-148">Значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="35db8-148">default values</span></span> | <span data-ttu-id="35db8-149">Значения по умолчанию поддерживают только литералы и константы.</span><span class="sxs-lookup"><span data-stu-id="35db8-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="35db8-150">Недетерминированные выражения или функции, такие как `GETDATE()` или `CURRENT_TIMESTAMP`, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="35db8-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="35db8-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35db8-151">Next steps</span></span>
<span data-ttu-id="35db8-152">Дополнительные сведения см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="35db8-152">To learn more, see:</span></span>

- <span data-ttu-id="35db8-153">[Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="35db8-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="35db8-154">[Общие сведения о таблицах в хранилище данных SQL][Overview]</span><span class="sxs-lookup"><span data-stu-id="35db8-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="35db8-155">[Распределение таблиц в хранилище данных SQL][Distribute]</span><span class="sxs-lookup"><span data-stu-id="35db8-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="35db8-156">[Индексирование таблиц в хранилище данных SQL][Index]</span><span class="sxs-lookup"><span data-stu-id="35db8-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="35db8-157">[Секционирование таблиц в хранилище данных SQL][Partition]</span><span class="sxs-lookup"><span data-stu-id="35db8-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="35db8-158">[Управление статистикой таблиц в хранилище данных SQL][Statistics]</span><span class="sxs-lookup"><span data-stu-id="35db8-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="35db8-159">[Временные таблицы в хранилище данных SQL][Temporary]</span><span class="sxs-lookup"><span data-stu-id="35db8-159">[Temporary Tables][Temporary]</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
