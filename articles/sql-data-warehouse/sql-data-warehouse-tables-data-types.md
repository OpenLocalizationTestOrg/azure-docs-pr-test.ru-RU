---
title: "aaaData типы руководство - хранилище данных SQL Azure | Документы Microsoft"
description: "Рекомендации, что типы данных toodefine совместимы с хранилищем данных SQL."
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
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="e5621-103">Руководство по определению типов данных для таблиц в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="e5621-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="e5621-104">Используйте следующие рекомендации toodefine табличные типы данных, совместимые с хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e5621-104">Use these recommendations toodefine table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="e5621-105">Кроме того, toocompatibility, сводя к минимуму размер hello типов данных повышает производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="e5621-105">In addition toocompatibility, minimizing hello size of data types improves query performance.</span></span>

<span data-ttu-id="e5621-106">Хранилище данных SQL поддерживает hello наиболее часто используемых типов данных.</span><span class="sxs-lookup"><span data-stu-id="e5621-106">SQL Data Warehouse supports hello most commonly used data types.</span></span> <span data-ttu-id="e5621-107">Список hello поддерживаемых типов данных см. в разделе [типы данных](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) в инструкции CREATE TABLE hello.</span><span class="sxs-lookup"><span data-stu-id="e5621-107">For a list of hello supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="e5621-108">Уменьшение длины строки</span><span class="sxs-lookup"><span data-stu-id="e5621-108">Minimize row length</span></span>
<span data-ttu-id="e5621-109">Минимизация hello размер типов данных сокращает hello строку длиной, которая ведет toobetter производительность запросов.</span><span class="sxs-lookup"><span data-stu-id="e5621-109">Minimizing hello size of data types shortens hello row length, which leads toobetter query performance.</span></span> <span data-ttu-id="e5621-110">Используйте hello наименьший тип данных, работать для реальных данных.</span><span class="sxs-lookup"><span data-stu-id="e5621-110">Use hello smallest data type that works for your data.</span></span> 

- <span data-ttu-id="e5621-111">Не рекомендуется использовать по умолчанию длинные значения столбцов.</span><span class="sxs-lookup"><span data-stu-id="e5621-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="e5621-112">Например если hello длинного значения — 25 символов, затем определите столбца как VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="e5621-112">For example, if hello longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="e5621-113">Не нужно использовать [NVARCHAR][NVARCHAR], если вам требуется только VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="e5621-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="e5621-114">По возможности используйте NVARCHAR(4000) или VARCHAR(8000) вместо NVARCHAR(MAX) или VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="e5621-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="e5621-115">При использовании Polybase tooload таблиц, определенных hello длина строки в таблице hello не может превышать 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="e5621-115">If you are using Polybase tooload your tables, hello defined length of hello table row cannot exceed 1 MB.</span></span> <span data-ttu-id="e5621-116">Когда строку с данными переменной длины превышает 1 МБ, можно загрузить строку hello BCP, но не с PolyBase.</span><span class="sxs-lookup"><span data-stu-id="e5621-116">When a row with variable-length data exceeds 1 MB, you can load hello row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="e5621-117">Определение неподдерживаемых типов данных</span><span class="sxs-lookup"><span data-stu-id="e5621-117">Identify unsupported data types</span></span>
<span data-ttu-id="e5621-118">Если вы переносите базу данных из другой базы данных SQL, вы можете обнаружить некоторые типы данных, неподдерживаемые в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e5621-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="e5621-119">Используйте типы данных toodiscover неподдерживаемый этого запроса в существующую схему SQL.</span><span class="sxs-lookup"><span data-stu-id="e5621-119">Use this query toodiscover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="e5621-120"><a name="unsupported-data-types"></a>Использование обходных решений для неподдерживаемых типов данных</span><span class="sxs-lookup"><span data-stu-id="e5621-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="e5621-121">Hello ниже перечислены hello типы данных, хранилище данных SQL не поддерживает и предоставляет альтернативные варианты, которые можно использовать вместо hello неподдерживаемые типы данных.</span><span class="sxs-lookup"><span data-stu-id="e5621-121">hello following list shows hello data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of hello unsupported data types.</span></span>

| <span data-ttu-id="e5621-122">Неподдерживаемые типы данных</span><span class="sxs-lookup"><span data-stu-id="e5621-122">Unsupported data type</span></span> | <span data-ttu-id="e5621-123">Возможное решение</span><span class="sxs-lookup"><span data-stu-id="e5621-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="e5621-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="e5621-124">[geometry][geometry]</span></span> |<span data-ttu-id="e5621-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="e5621-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="e5621-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="e5621-126">[geography][geography]</span></span> |<span data-ttu-id="e5621-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="e5621-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="e5621-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="e5621-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="e5621-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="e5621-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="e5621-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="e5621-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="e5621-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="e5621-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="e5621-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="e5621-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="e5621-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="e5621-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="e5621-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="e5621-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="e5621-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="e5621-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="e5621-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="e5621-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="e5621-137">Разделите столбец на несколько строго типизированных столбцов.</span><span class="sxs-lookup"><span data-stu-id="e5621-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="e5621-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="e5621-138">[table][table]</span></span> |<span data-ttu-id="e5621-139">Преобразуйте tootemporary таблицы.</span><span class="sxs-lookup"><span data-stu-id="e5621-139">Convert tootemporary tables.</span></span> |
| <span data-ttu-id="e5621-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="e5621-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="e5621-141">Переработайте код toouse [datetime2] [ datetime2] и `CURRENT_TIMESTAMP` функции.</span><span class="sxs-lookup"><span data-stu-id="e5621-141">Rework code toouse [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="e5621-142">По умолчанию поддерживаются только константы, поэтому нельзя использовать current_timestamp как ограничение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5621-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="e5621-143">Если вам требуется toomigrate значение версии строки с типизированным столбцом отметок времени, используйте [ДВОИЧНЫХ][BINARY](8) или [VARBINARY][BINARY](8) для NOT NULL или Значение NULL, значение версии строки.</span><span class="sxs-lookup"><span data-stu-id="e5621-143">If you need toomigrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="e5621-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="e5621-144">[xml][xml]</span></span> |<span data-ttu-id="e5621-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="e5621-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="e5621-146">[тип, определенный пользователем][user defined types]</span><span class="sxs-lookup"><span data-stu-id="e5621-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="e5621-147">Преобразуйте тип данных в собственном toohello назад по возможности.</span><span class="sxs-lookup"><span data-stu-id="e5621-147">Convert back toohello native data type when possible.</span></span> |
| <span data-ttu-id="e5621-148">Значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e5621-148">default values</span></span> | <span data-ttu-id="e5621-149">Значения по умолчанию поддерживают только литералы и константы.</span><span class="sxs-lookup"><span data-stu-id="e5621-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="e5621-150">Недетерминированные выражения или функции, такие как `GETDATE()` или `CURRENT_TIMESTAMP`, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="e5621-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e5621-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5621-151">Next steps</span></span>
<span data-ttu-id="e5621-152">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="e5621-152">toolearn more, see:</span></span>

- <span data-ttu-id="e5621-153">[Рекомендации по использованию хранилища данных SQL Azure][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="e5621-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="e5621-154">[Общие сведения о таблицах в хранилище данных SQL][Overview]</span><span class="sxs-lookup"><span data-stu-id="e5621-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="e5621-155">[Распределение таблиц в хранилище данных SQL][Distribute]</span><span class="sxs-lookup"><span data-stu-id="e5621-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="e5621-156">[Индексирование таблиц в хранилище данных SQL][Index]</span><span class="sxs-lookup"><span data-stu-id="e5621-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="e5621-157">[Секционирование таблиц в хранилище данных SQL][Partition]</span><span class="sxs-lookup"><span data-stu-id="e5621-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="e5621-158">[Управление статистикой таблиц в хранилище данных SQL][Statistics]</span><span class="sxs-lookup"><span data-stu-id="e5621-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="e5621-159">[Временные таблицы в хранилище данных SQL][Temporary]</span><span class="sxs-lookup"><span data-stu-id="e5621-159">[Temporary Tables][Temporary]</span></span>

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
