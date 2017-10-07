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
# <a name="migrate-your-sql-code-toosql-data-warehouse"></a>Перенос вашей tooSQL кода SQL хранилища данных
В этой статье описываются изменения кода, возможно, потребуется toomake при переносе кода из другого tooSQL базы данных хранилища данных. Некоторые функции хранилища данных SQL может значительно повысить производительность, как и разработанные toowork образом распределенных. Тем не менее toomaintain производительность и масштабируемость, некоторые функции недоступны также.

## <a name="common-t-sql-limitations"></a>Общие ограничения T-SQL
После списка Hello перечислены наиболее распространенные возможности hello, которые хранилище данных SQL не поддерживает. Hello ссылкам можно найти tooworkarounds для hello неподдерживаемые компоненты:

* [соединение ANSI при обновлении][ANSI joins on updates];
* [соединение ANSI при удалении][ANSI joins on deletes];
* [инструкция merge][merge statement];
* соединение join между базами данных
* [курсоры][cursors];
* <seg>
  [INSERT..EXEC][INSERT..EXEC];</seg>
* предложение output
* встроенные функции, определяемые пользователем
* функции с несколькими инструкциями
* [обобщенные табличные выражения](#Common-table-expressions)
* [рекурсивные обобщенные табличные выражения (CTE)](#Recursive-common-table-expressions-(CTE)
* функции и процедуры среды CLR
* функция $partition
* переменные таблицы
* параметры табличных значений
* распределенные транзакции
* фиксация или откат
* транзакция save
* контекст выполнения EXECUTE AS
* [предложение group by с параметрами rollup, cube или grouping sets][group by clause with rollup / cube / grouping sets options];
* [уровни вложенности больше 8][nesting levels beyond 8];
* [обновление через представления][updating through views];
* [использование инструкции select для назначения переменных][use of select for variable assignment];
* [отсутствие типа данных MAX для динамических строк SQL][no MAX data type for dynamic SQL strings].

К счастью, большинство из этих ограничений можно обойти. Объяснения приведены в указанной выше статьи соответствующие разработки hello.

## <a name="supported-cte-features"></a>Поддерживаемые функции CTE
Хранилище данных SQL частично поддерживает обобщенные табличные выражения (CTE).  в настоящее время поддерживаются следующие атрибуты ОТВ Hello:

* Выражение CTE можно указать в инструкции SELECT.
* Выражение CTE можно указать в инструкции CREATE VIEW.
* Выражение CTE можно указать в инструкции CREATE TABLE AS SELECT (CTAS).
* Выражение CTE можно указать в инструкции CREATE REMOTE TABLE AS SELECT (CRTAS).
* Выражение CTE можно указать в инструкции CREATE EXTERNAL TABLE AS SELECT (CETAS).
* Из выражения CTE можно сослаться на удаленную таблицу.
* Из выражения CTE можно сослаться на внешнюю таблицу.
* В CTE можно определить несколько запросов CTE.

## <a name="cte-limitations"></a>Ограничения СTE
В хранилище данных SQL обобщенные табличные выражения имеют следующие ограничения:

* За CTE должна следовать одиночная инструкция SELECT. Инструкции INSERT, UPDATE, DELETE и MERGE не поддерживаются.
* Обобщенное табличное выражение, включающее tooitself ссылки (Рекурсивное обобщенное табличное выражение) не поддерживается (см. ниже раздел).
* Указание более одного предложения WITH в выражении CTE не допускается. Например, если определение запроса CTE содержит вложенный запрос, этот вложенный запрос не может содержать предложение WITH, определяющее другое выражение CTE.
* Предложение ORDER BY не может использоваться в hello определений запроса, за исключением того, если указано предложение TOP.
* Если обобщенное табличное Выражение используется в инструкции, которая является частью пакета, инструкции hello перед ним должен следовать точкой с запятой.
* При использовании в инструкции, созданные sp_prepare, обобщенных табличных выражений будет вести себя hello так же, как другие инструкции SELECT в PDW. Однако если обобщенных табличных выражений используются как часть CETAS подготовил sp_prepare, поведение hello могут быть отложены из SQL Server и других инструкций PDW из-за hello способ реализации привязки для sp_prepare. Если ссылки на обобщенное табличное Выражение используется в неверный столбец, который не существует в обобщенного табличного Выражения, не обнаруживает ошибки hello передаст hello sp_prepare, что hello, возникает ошибка во время sp_execute вместо SELECT.

## <a name="recursive-ctes"></a>Рекурсивные CTE
Рекурсивные CTE в хранилище данных SQL не поддерживаются.  Hello миграции Рекурсивное ОТВ может быть довольно сложной, и процесс наиболее hello toobreak его на несколько этапов. Обычно можно использовать цикл и заполнить временной таблицы, как перебора hello рекурсивные промежуточные запросы. После заполнения временной таблицы hello hello данные затем можно вернуть как один результирующий набор. Аналогичный подход был используется toosolve `GROUP BY WITH CUBE` в hello [группировать по предложение with rollup, куб, объединение наборов параметров] [ group by clause with rollup / cube / grouping sets options] статьи.

## <a name="unsupported-system-functions"></a>Неподдерживаемые системные функции
Ряд системных функций также не поддерживаются. Ниже приведены некоторые hello основные ресурсы обычно может оказаться полезен в хранилища данных.

* NEWSEQUENTIALID()
* @@NESTLEVEL()
* @@IDENTITY()
* @@ROWCOUNT()
* ROWCOUNT_BIG
* ERROR_LINE()

Некоторые из этих проблем можно обойти.

## <a name="rowcount-workaround"></a>Возможное решение для замены @@ROWCOUNT
toowork вокруг отсутствия поддержки @@ROWCOUNT, создайте хранимую процедуру, которая будет извлекать hello последний счетчик строк из sys.dm_pdw_request_steps и затем выполнять `EXEC LastRowCount` после инструкции DML.

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

## <a name="next-steps"></a>Дальнейшие действия
Полный список всех поддерживаемых инструкций T-SQL приведен в [разделах о Transact-SQL][Transact-SQL topics].

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
