---
title: "aaaLeverage циклы T-SQL, в хранилище данных SQL Azure | Документы Microsoft"
description: "Рекомендации по применению циклов Transact-SQL и замене курсоров в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a>Циклы в хранилище данных SQL
Хранилище данных SQL поддерживает hello [при][при] цикл для повторным выполнением блоков инструкций. Эти возможности будут доступны для при условии, что указан hello условий, или пока не будет кода hello специально завершает цикл hello при помощи hello `BREAK` ключевое слово. Циклы особенно полезны для замены курсоров, определенных в коде SQL. К счастью почти все курсоры, которые записываются в код SQL для быстрого hello вперед, считываются только различные. Поэтому [при] циклы, отличную альтернативу, если вы обнаружите наличие tooreplace один.

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a>Применение циклов и замена курсоров в хранилище данных SQL
Тем не менее, прежде чем углубляться в голове сначала вам следует задать себе hello следующий вопрос: «этот курсор удалось переписать toouse операции на основе наборов?». Во многих случаях hello ответ будет иметь значение yes, часто является лучшим подходом hello. Операция, ориентированная на работу с набором данных, нередко выполняется намного быстрее, чем итеративный метод построчного перебора.

Курсоры быстрой перемотки, доступные только для чтения, легко заменяются циклической конструкцией. Ниже приведен простой пример. Данный пример кода обновляет статистику hello для каждой таблицы в базе данных hello. Путем итерации hello таблиц в цикле hello мы являются может tooexecute каждая команда в последовательности.

Во-первых создайте временную таблицу, содержащая уникальную строку чисел используется tooidentify hello отдельные инструкции:

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

Во-вторых инициализируйте необходимые tooperform hello hello переменных цикла:

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

Теперь запустите цикл последовательного выполнения операторов:

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

Наконец, удалите hello временной таблицы, созданные в первом шаге hello

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[при]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
