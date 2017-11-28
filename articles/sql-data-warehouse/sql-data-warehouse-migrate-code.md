---
title: "aaaMigrate вашей tooSQL кода SQL хранилища данных | Документы Microsoft"
description: "Советы по миграции SQL кода tooAzure хранилище данных SQL для разработки решений."
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
ms.openlocfilehash: 7a16d579d068e9df9aba3dc61e4a09bcaa551588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a><span data-ttu-id="612f5-103">Перенос вашей tooSQL кода SQL хранилища данных</span><span class="sxs-lookup"><span data-stu-id="612f5-103">Migrate your SQL code tooSQL Data Warehouse</span></span>
<span data-ttu-id="612f5-104">В этой статье описываются изменения кода, возможно, потребуется toomake при переносе кода из другого tooSQL базы данных хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="612f5-104">This article explains code changes you will probably need toomake when migrating your code from another database tooSQL Data Warehouse.</span></span> <span data-ttu-id="612f5-105">Некоторые функции хранилища данных SQL может значительно повысить производительность, как и разработанные toowork образом распределенных.</span><span class="sxs-lookup"><span data-stu-id="612f5-105">Some SQL Data Warehouse features can significantly improve performance as they are designed toowork in a distributed fashion.</span></span> <span data-ttu-id="612f5-106">Тем не менее toomaintain производительность и масштабируемость, некоторые функции недоступны также.</span><span class="sxs-lookup"><span data-stu-id="612f5-106">However, toomaintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="612f5-107">Общие ограничения T-SQL</span><span class="sxs-lookup"><span data-stu-id="612f5-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="612f5-108">После списка Hello перечислены наиболее распространенные возможности hello, которые хранилище данных SQL не поддерживает.</span><span class="sxs-lookup"><span data-stu-id="612f5-108">hello following list summarizes hello most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="612f5-109">Hello ссылкам можно найти tooworkarounds для hello неподдерживаемые компоненты:</span><span class="sxs-lookup"><span data-stu-id="612f5-109">hello links take you tooworkarounds for hello unsupported features:</span></span>

* <span data-ttu-id="612f5-110">[соединение ANSI при обновлении][ANSI joins on updates];</span><span class="sxs-lookup"><span data-stu-id="612f5-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="612f5-111">[соединение ANSI при удалении][ANSI joins on deletes];</span><span class="sxs-lookup"><span data-stu-id="612f5-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="612f5-112">[инструкция merge][merge statement];</span><span class="sxs-lookup"><span data-stu-id="612f5-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="612f5-113">соединение join между базами данных</span><span class="sxs-lookup"><span data-stu-id="612f5-113">cross-database joins</span></span>
* <span data-ttu-id="612f5-114">[курсоры][cursors];</span><span class="sxs-lookup"><span data-stu-id="612f5-114">[cursors][cursors]</span></span>
* <span data-ttu-id="612f5-115"><seg>
  [INSERT..EXEC][INSERT..EXEC];</seg></span><span class="sxs-lookup"><span data-stu-id="612f5-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="612f5-116">предложение output</span><span class="sxs-lookup"><span data-stu-id="612f5-116">output clause</span></span>
* <span data-ttu-id="612f5-117">встроенные функции, определяемые пользователем</span><span class="sxs-lookup"><span data-stu-id="612f5-117">inline user-defined functions</span></span>
* <span data-ttu-id="612f5-118">функции с несколькими инструкциями</span><span class="sxs-lookup"><span data-stu-id="612f5-118">multi-statement functions</span></span>
* [<span data-ttu-id="612f5-119">обобщенные табличные выражения</span><span class="sxs-lookup"><span data-stu-id="612f5-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="612f5-120">[рекурсивные обобщенные табличные выражения (CTE)](#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="612f5-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="612f5-121">функции и процедуры среды CLR</span><span class="sxs-lookup"><span data-stu-id="612f5-121">CLR functions and procedures</span></span>
* <span data-ttu-id="612f5-122">функция $partition</span><span class="sxs-lookup"><span data-stu-id="612f5-122">$partition function</span></span>
* <span data-ttu-id="612f5-123">переменные таблицы</span><span class="sxs-lookup"><span data-stu-id="612f5-123">table variables</span></span>
* <span data-ttu-id="612f5-124">параметры табличных значений</span><span class="sxs-lookup"><span data-stu-id="612f5-124">table value parameters</span></span>
* <span data-ttu-id="612f5-125">распределенные транзакции</span><span class="sxs-lookup"><span data-stu-id="612f5-125">distributed transactions</span></span>
* <span data-ttu-id="612f5-126">фиксация или откат</span><span class="sxs-lookup"><span data-stu-id="612f5-126">commit / rollback work</span></span>
* <span data-ttu-id="612f5-127">транзакция save</span><span class="sxs-lookup"><span data-stu-id="612f5-127">save transaction</span></span>
* <span data-ttu-id="612f5-128">контекст выполнения EXECUTE AS</span><span class="sxs-lookup"><span data-stu-id="612f5-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="612f5-129">[предложение group by с параметрами rollup, cube или grouping sets][group by clause with rollup / cube / grouping sets options];</span><span class="sxs-lookup"><span data-stu-id="612f5-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="612f5-130">[уровни вложенности больше 8][nesting levels beyond 8];</span><span class="sxs-lookup"><span data-stu-id="612f5-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="612f5-131">[обновление через представления][updating through views];</span><span class="sxs-lookup"><span data-stu-id="612f5-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="612f5-132">[использование инструкции select для назначения переменных][use of select for variable assignment];</span><span class="sxs-lookup"><span data-stu-id="612f5-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="612f5-133">[отсутствие типа данных MAX для динамических строк SQL][no MAX data type for dynamic SQL strings].</span><span class="sxs-lookup"><span data-stu-id="612f5-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="612f5-134">К счастью, большинство из этих ограничений можно обойти.</span><span class="sxs-lookup"><span data-stu-id="612f5-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="612f5-135">Объяснения приведены в указанной выше статьи соответствующие разработки hello.</span><span class="sxs-lookup"><span data-stu-id="612f5-135">Explanations are provided in hello relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="612f5-136">Поддерживаемые функции CTE</span><span class="sxs-lookup"><span data-stu-id="612f5-136">Supported CTE features</span></span>
<span data-ttu-id="612f5-137">Хранилище данных SQL частично поддерживает обобщенные табличные выражения (CTE).</span><span class="sxs-lookup"><span data-stu-id="612f5-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="612f5-138">в настоящее время поддерживаются следующие атрибуты ОТВ Hello:</span><span class="sxs-lookup"><span data-stu-id="612f5-138">hello following CTE features are currently supported:</span></span>

* <span data-ttu-id="612f5-139">Выражение CTE можно указать в инструкции SELECT.</span><span class="sxs-lookup"><span data-stu-id="612f5-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="612f5-140">Выражение CTE можно указать в инструкции CREATE VIEW.</span><span class="sxs-lookup"><span data-stu-id="612f5-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="612f5-141">Выражение CTE можно указать в инструкции CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="612f5-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="612f5-142">Выражение CTE можно указать в инструкции CREATE REMOTE TABLE AS SELECT (CRTAS).</span><span class="sxs-lookup"><span data-stu-id="612f5-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="612f5-143">Выражение CTE можно указать в инструкции CREATE EXTERNAL TABLE AS SELECT (CETAS).</span><span class="sxs-lookup"><span data-stu-id="612f5-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="612f5-144">Из выражения CTE можно сослаться на удаленную таблицу.</span><span class="sxs-lookup"><span data-stu-id="612f5-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="612f5-145">Из выражения CTE можно сослаться на внешнюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="612f5-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="612f5-146">В CTE можно определить несколько запросов CTE.</span><span class="sxs-lookup"><span data-stu-id="612f5-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="612f5-147">Ограничения СTE</span><span class="sxs-lookup"><span data-stu-id="612f5-147">CTE Limitations</span></span>
<span data-ttu-id="612f5-148">В хранилище данных SQL обобщенные табличные выражения имеют следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="612f5-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="612f5-149">За CTE должна следовать одиночная инструкция SELECT.</span><span class="sxs-lookup"><span data-stu-id="612f5-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="612f5-150">Инструкции INSERT, UPDATE, DELETE и MERGE не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="612f5-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="612f5-151">Обобщенное табличное выражение, включающее tooitself ссылки (Рекурсивное обобщенное табличное выражение) не поддерживается (см. ниже раздел).</span><span class="sxs-lookup"><span data-stu-id="612f5-151">A common table expression that includes references tooitself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="612f5-152">Указание более одного предложения WITH в выражении CTE не допускается.</span><span class="sxs-lookup"><span data-stu-id="612f5-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="612f5-153">Например, если определение запроса CTE содержит вложенный запрос, этот вложенный запрос не может содержать предложение WITH, определяющее другое выражение CTE.</span><span class="sxs-lookup"><span data-stu-id="612f5-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="612f5-154">Предложение ORDER BY не может использоваться в hello определений запроса, за исключением того, если указано предложение TOP.</span><span class="sxs-lookup"><span data-stu-id="612f5-154">An ORDER BY clause cannot be used in hello CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="612f5-155">Если обобщенное табличное Выражение используется в инструкции, которая является частью пакета, инструкции hello перед ним должен следовать точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="612f5-155">When a CTE is used in a statement that is part of a batch, hello statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="612f5-156">При использовании в инструкции, созданные sp_prepare, обобщенных табличных выражений будет вести себя hello так же, как другие инструкции SELECT в PDW.</span><span class="sxs-lookup"><span data-stu-id="612f5-156">When used in statements prepared by sp_prepare, CTEs will behave hello same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="612f5-157">Однако если обобщенных табличных выражений используются как часть CETAS подготовил sp_prepare, поведение hello могут быть отложены из SQL Server и других инструкций PDW из-за hello способ реализации привязки для sp_prepare.</span><span class="sxs-lookup"><span data-stu-id="612f5-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, hello behavior can defer from SQL Server and other PDW statements because of hello way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="612f5-158">Если ссылки на обобщенное табличное Выражение используется в неверный столбец, который не существует в обобщенного табличного Выражения, не обнаруживает ошибки hello передаст hello sp_prepare, что hello, возникает ошибка во время sp_execute вместо SELECT.</span><span class="sxs-lookup"><span data-stu-id="612f5-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, hello sp_prepare will pass without detecting hello error, but hello error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="612f5-159">Рекурсивные CTE</span><span class="sxs-lookup"><span data-stu-id="612f5-159">Recursive CTEs</span></span>
<span data-ttu-id="612f5-160">Рекурсивные CTE в хранилище данных SQL не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="612f5-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="612f5-161">Hello миграции Рекурсивное ОТВ может быть довольно сложной, и процесс наиболее hello toobreak его на несколько этапов.</span><span class="sxs-lookup"><span data-stu-id="612f5-161">hello migration of recursive CTE can be somewhat complex and hello best process is toobreak it into multiple steps.</span></span> <span data-ttu-id="612f5-162">Обычно можно использовать цикл и заполнить временной таблицы, как перебора hello рекурсивные промежуточные запросы.</span><span class="sxs-lookup"><span data-stu-id="612f5-162">You can typically use a loop and populate a temporary table as you iterate over hello recursive interim queries.</span></span> <span data-ttu-id="612f5-163">После заполнения временной таблицы hello hello данные затем можно вернуть как один результирующий набор.</span><span class="sxs-lookup"><span data-stu-id="612f5-163">Once hello temporary table is populated you can then return hello data as a single result set.</span></span> <span data-ttu-id="612f5-164">Аналогичный подход был используется toosolve `GROUP BY WITH CUBE` в hello [группировать по предложение with rollup, куб, объединение наборов параметров] [ group by clause with rollup / cube / grouping sets options] статьи.</span><span class="sxs-lookup"><span data-stu-id="612f5-164">A similar approach has been used toosolve `GROUP BY WITH CUBE` in hello [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="612f5-165">Неподдерживаемые системные функции</span><span class="sxs-lookup"><span data-stu-id="612f5-165">Unsupported system functions</span></span>
<span data-ttu-id="612f5-166">Ряд системных функций также не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="612f5-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="612f5-167">Ниже приведены некоторые hello основные ресурсы обычно может оказаться полезен в хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="612f5-167">Some of hello main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="612f5-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="612f5-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="612f5-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="612f5-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="612f5-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="612f5-170">@@IDENTITY()</span></span>
* <span data-ttu-id="612f5-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="612f5-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="612f5-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="612f5-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="612f5-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="612f5-173">ERROR_LINE()</span></span>

<span data-ttu-id="612f5-174">Некоторые из этих проблем можно обойти.</span><span class="sxs-lookup"><span data-stu-id="612f5-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="612f5-175">Возможное решение для замены @@ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="612f5-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="612f5-176">toowork вокруг отсутствия поддержки @@ROWCOUNT, создайте хранимую процедуру, которая будет извлекать hello последний счетчик строк из sys.dm_pdw_request_steps и затем выполнять `EXEC LastRowCount` после инструкции DML.</span><span class="sxs-lookup"><span data-stu-id="612f5-176">toowork around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve hello last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="612f5-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="612f5-177">Next steps</span></span>
<span data-ttu-id="612f5-178">Полный список всех поддерживаемых инструкций T-SQL приведен в [разделах о Transact-SQL][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="612f5-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

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
