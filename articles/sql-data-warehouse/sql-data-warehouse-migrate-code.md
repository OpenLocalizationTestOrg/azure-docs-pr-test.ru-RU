---
title: "Перенос кода SQL в хранилище данных SQL | Документация Майкрософт"
description: "Советы по переносу кода SQL в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: c6e6b890f5e2d0e31b10bbb6803adad02bf60248
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-code-to-sql-data-warehouse"></a><span data-ttu-id="b7120-103">Перенос кода SQL в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="b7120-103">Migrate your SQL code to SQL Data Warehouse</span></span>
<span data-ttu-id="b7120-104">В этой статье поясняются изменения кода, которые, вероятно, потребуется внести при переносе кода в хранилище данных SQL из другой базы данных.</span><span class="sxs-lookup"><span data-stu-id="b7120-104">This article explains code changes you will probably need to make when migrating your code from another database to SQL Data Warehouse.</span></span> <span data-ttu-id="b7120-105">Некоторые функции хранилища данных SQL могут значительно повысить производительность, так как они предназначены для работы в распределенной форме.</span><span class="sxs-lookup"><span data-stu-id="b7120-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span></span> <span data-ttu-id="b7120-106">Однако для обеспечения производительности и масштабирования некоторые функции недоступны.</span><span class="sxs-lookup"><span data-stu-id="b7120-106">However, to maintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="b7120-107">Общие ограничения T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7120-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="b7120-108">В следующем списке перечислены наиболее распространенные функции, которые не поддерживаются хранилищем данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b7120-108">The following list summarizes the most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="b7120-109">Предоставленные ссылки позволят вам ознакомиться со способами обхода для соответствующей неподдерживаемой функции:</span><span class="sxs-lookup"><span data-stu-id="b7120-109">The links take you to workarounds for the unsupported features:</span></span>

* <span data-ttu-id="b7120-110">[соединение ANSI при обновлении][ANSI joins on updates];</span><span class="sxs-lookup"><span data-stu-id="b7120-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="b7120-111">[соединение ANSI при удалении][ANSI joins on deletes];</span><span class="sxs-lookup"><span data-stu-id="b7120-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="b7120-112">[инструкция merge][merge statement];</span><span class="sxs-lookup"><span data-stu-id="b7120-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="b7120-113">соединение join между базами данных</span><span class="sxs-lookup"><span data-stu-id="b7120-113">cross-database joins</span></span>
* <span data-ttu-id="b7120-114">[курсоры][cursors];</span><span class="sxs-lookup"><span data-stu-id="b7120-114">[cursors][cursors]</span></span>
* <span data-ttu-id="b7120-115"><seg>
  [INSERT..EXEC][INSERT..EXEC];</seg></span><span class="sxs-lookup"><span data-stu-id="b7120-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="b7120-116">предложение output</span><span class="sxs-lookup"><span data-stu-id="b7120-116">output clause</span></span>
* <span data-ttu-id="b7120-117">встроенные функции, определяемые пользователем</span><span class="sxs-lookup"><span data-stu-id="b7120-117">inline user-defined functions</span></span>
* <span data-ttu-id="b7120-118">функции с несколькими инструкциями</span><span class="sxs-lookup"><span data-stu-id="b7120-118">multi-statement functions</span></span>
* [<span data-ttu-id="b7120-119">обобщенные табличные выражения</span><span class="sxs-lookup"><span data-stu-id="b7120-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="b7120-120">[рекурсивные обобщенные табличные выражения (CTE)](#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="b7120-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="b7120-121">функции и процедуры среды CLR</span><span class="sxs-lookup"><span data-stu-id="b7120-121">CLR functions and procedures</span></span>
* <span data-ttu-id="b7120-122">функция $partition</span><span class="sxs-lookup"><span data-stu-id="b7120-122">$partition function</span></span>
* <span data-ttu-id="b7120-123">переменные таблицы</span><span class="sxs-lookup"><span data-stu-id="b7120-123">table variables</span></span>
* <span data-ttu-id="b7120-124">параметры табличных значений</span><span class="sxs-lookup"><span data-stu-id="b7120-124">table value parameters</span></span>
* <span data-ttu-id="b7120-125">распределенные транзакции</span><span class="sxs-lookup"><span data-stu-id="b7120-125">distributed transactions</span></span>
* <span data-ttu-id="b7120-126">фиксация или откат</span><span class="sxs-lookup"><span data-stu-id="b7120-126">commit / rollback work</span></span>
* <span data-ttu-id="b7120-127">транзакция save</span><span class="sxs-lookup"><span data-stu-id="b7120-127">save transaction</span></span>
* <span data-ttu-id="b7120-128">контекст выполнения EXECUTE AS</span><span class="sxs-lookup"><span data-stu-id="b7120-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="b7120-129">[предложение group by с параметрами rollup, cube или grouping sets][group by clause with rollup / cube / grouping sets options];</span><span class="sxs-lookup"><span data-stu-id="b7120-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="b7120-130">[уровни вложенности больше 8][nesting levels beyond 8];</span><span class="sxs-lookup"><span data-stu-id="b7120-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="b7120-131">[обновление через представления][updating through views];</span><span class="sxs-lookup"><span data-stu-id="b7120-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="b7120-132">[использование инструкции select для назначения переменных][use of select for variable assignment];</span><span class="sxs-lookup"><span data-stu-id="b7120-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="b7120-133">[отсутствие типа данных MAX для динамических строк SQL][no MAX data type for dynamic SQL strings].</span><span class="sxs-lookup"><span data-stu-id="b7120-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="b7120-134">К счастью, большинство из этих ограничений можно обойти.</span><span class="sxs-lookup"><span data-stu-id="b7120-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="b7120-135">Пояснения см. в соответствующих разделах по разработке, указанных выше.</span><span class="sxs-lookup"><span data-stu-id="b7120-135">Explanations are provided in the relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="b7120-136">Поддерживаемые функции CTE</span><span class="sxs-lookup"><span data-stu-id="b7120-136">Supported CTE features</span></span>
<span data-ttu-id="b7120-137">Хранилище данных SQL частично поддерживает обобщенные табличные выражения (CTE).</span><span class="sxs-lookup"><span data-stu-id="b7120-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="b7120-138">В настоящее время поддерживаются следующие функции CTE:</span><span class="sxs-lookup"><span data-stu-id="b7120-138">The following CTE features are currently supported:</span></span>

* <span data-ttu-id="b7120-139">Выражение CTE можно указать в инструкции SELECT.</span><span class="sxs-lookup"><span data-stu-id="b7120-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="b7120-140">Выражение CTE можно указать в инструкции CREATE VIEW.</span><span class="sxs-lookup"><span data-stu-id="b7120-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="b7120-141">Выражение CTE можно указать в инструкции CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="b7120-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="b7120-142">Выражение CTE можно указать в инструкции CREATE REMOTE TABLE AS SELECT (CRTAS).</span><span class="sxs-lookup"><span data-stu-id="b7120-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="b7120-143">Выражение CTE можно указать в инструкции CREATE EXTERNAL TABLE AS SELECT (CETAS).</span><span class="sxs-lookup"><span data-stu-id="b7120-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="b7120-144">Из выражения CTE можно сослаться на удаленную таблицу.</span><span class="sxs-lookup"><span data-stu-id="b7120-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="b7120-145">Из выражения CTE можно сослаться на внешнюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="b7120-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="b7120-146">В CTE можно определить несколько запросов CTE.</span><span class="sxs-lookup"><span data-stu-id="b7120-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="b7120-147">Ограничения СTE</span><span class="sxs-lookup"><span data-stu-id="b7120-147">CTE Limitations</span></span>
<span data-ttu-id="b7120-148">В хранилище данных SQL обобщенные табличные выражения имеют следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="b7120-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="b7120-149">За CTE должна следовать одиночная инструкция SELECT.</span><span class="sxs-lookup"><span data-stu-id="b7120-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="b7120-150">Инструкции INSERT, UPDATE, DELETE и MERGE не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b7120-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="b7120-151">Обобщенные табличные выражения, которые включают ссылки на самих себя (рекурсивные обобщенные табличные выражения), не поддерживаются (см. раздел ниже).</span><span class="sxs-lookup"><span data-stu-id="b7120-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="b7120-152">Указание более одного предложения WITH в выражении CTE не допускается.</span><span class="sxs-lookup"><span data-stu-id="b7120-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="b7120-153">Например, если определение запроса CTE содержит вложенный запрос, этот вложенный запрос не может содержать предложение WITH, определяющее другое выражение CTE.</span><span class="sxs-lookup"><span data-stu-id="b7120-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="b7120-154">Предложение ORDER BY не может использоваться в определении запроса CTE, если не указано предложение TOP.</span><span class="sxs-lookup"><span data-stu-id="b7120-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="b7120-155">Если выражение CTE используется в инструкции, которая является частью пакета, то после выражения необходимо указать точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="b7120-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="b7120-156">При использовании инструкций, подготовленных с помощью sp_prepare, выражения CTE будут вести себя так же, как другие инструкции SELECT в PDW.</span><span class="sxs-lookup"><span data-stu-id="b7120-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="b7120-157">Тем не менее, если CTE используются в инструкции CETAS, подготовленной процедурой sp_prepare, поведение может переопределяться SQL Server и другими инструкциями PDW из-за способа реализации привязки в sp_prepare.</span><span class="sxs-lookup"><span data-stu-id="b7120-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="b7120-158">Если инструкция SELECT, ссылающаяся на CTE, использует несуществующий в CTE столбец, процедура sp_prepare будет выполнена без ошибок. Ошибка возникнет при выполнении sp_execute.</span><span class="sxs-lookup"><span data-stu-id="b7120-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="b7120-159">Рекурсивные CTE</span><span class="sxs-lookup"><span data-stu-id="b7120-159">Recursive CTEs</span></span>
<span data-ttu-id="b7120-160">Рекурсивные CTE в хранилище данных SQL не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b7120-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="b7120-161">Перенос рекурсивных CTE может быть сложен, и оптимальным решением станет разделение этой процедуры на несколько этапов.</span><span class="sxs-lookup"><span data-stu-id="b7120-161">The migration of recursive CTE can be somewhat complex and the best process is to break it into multiple steps.</span></span> <span data-ttu-id="b7120-162">Обычно используется цикл для заполнения временной таблицы по мере выполнения рекурсивных промежуточных запросов.</span><span class="sxs-lookup"><span data-stu-id="b7120-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span></span> <span data-ttu-id="b7120-163">После заполнения временной таблицы можно возвратить данные как единый результирующий набор.</span><span class="sxs-lookup"><span data-stu-id="b7120-163">Once the temporary table is populated you can then return the data as a single result set.</span></span> <span data-ttu-id="b7120-164">Похожий подход использовался для решения `GROUP BY WITH CUBE` в статье [Группировка по параметрам в хранилище данных SQL][group by clause with rollup / cube / grouping sets options].</span><span class="sxs-lookup"><span data-stu-id="b7120-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="b7120-165">Неподдерживаемые системные функции</span><span class="sxs-lookup"><span data-stu-id="b7120-165">Unsupported system functions</span></span>
<span data-ttu-id="b7120-166">Ряд системных функций также не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b7120-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="b7120-167">Ниже приводится список некоторых системных функций, которые могут быть полезны в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="b7120-167">Some of the main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="b7120-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="b7120-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="b7120-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="b7120-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="b7120-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="b7120-170">@@IDENTITY()</span></span>
* <span data-ttu-id="b7120-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="b7120-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="b7120-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="b7120-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="b7120-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="b7120-173">ERROR_LINE()</span></span>

<span data-ttu-id="b7120-174">Некоторые из этих проблем можно обойти.</span><span class="sxs-lookup"><span data-stu-id="b7120-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="b7120-175">Возможное решение для замены @@ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="b7120-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="b7120-176">Чтобы обойти отсутствие поддержки @@ROWCOUNT, создайте хранимую процедуру, которая будет извлекать значение счетчика последней строки из sys.dm_pdw_request_steps и затем выполнять `EXEC LastRowCount` после инструкции DML.</span><span class="sxs-lookup"><span data-stu-id="b7120-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a><span data-ttu-id="b7120-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7120-177">Next steps</span></span>
<span data-ttu-id="b7120-178">Полный список всех поддерживаемых инструкций T-SQL приведен в [разделах о Transact-SQL][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="b7120-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
