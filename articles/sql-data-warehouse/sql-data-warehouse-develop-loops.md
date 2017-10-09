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
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="0a7bc-103">Циклы в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="0a7bc-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="0a7bc-104">Хранилище данных SQL поддерживает hello [при][при] цикл для повторным выполнением блоков инструкций.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="0a7bc-105">Эти возможности будут доступны для при условии, что указан hello условий, или пока не будет кода hello специально завершает цикл hello при помощи hello `BREAK` ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="0a7bc-106">Циклы особенно полезны для замены курсоров, определенных в коде SQL.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="0a7bc-107">К счастью почти все курсоры, которые записываются в код SQL для быстрого hello вперед, считываются только различные.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="0a7bc-108">Поэтому [при] циклы, отличную альтернативу, если вы обнаружите наличие tooreplace один.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="0a7bc-109">Применение циклов и замена курсоров в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="0a7bc-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="0a7bc-110">Тем не менее, прежде чем углубляться в голове сначала вам следует задать себе hello следующий вопрос: «этот курсор удалось переписать toouse операции на основе наборов?».</span><span class="sxs-lookup"><span data-stu-id="0a7bc-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="0a7bc-111">Во многих случаях hello ответ будет иметь значение yes, часто является лучшим подходом hello.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="0a7bc-112">Операция, ориентированная на работу с набором данных, нередко выполняется намного быстрее, чем итеративный метод построчного перебора.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="0a7bc-113">Курсоры быстрой перемотки, доступные только для чтения, легко заменяются циклической конструкцией.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="0a7bc-114">Ниже приведен простой пример.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-114">Below is a simple example.</span></span> <span data-ttu-id="0a7bc-115">Данный пример кода обновляет статистику hello для каждой таблицы в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="0a7bc-116">Путем итерации hello таблиц в цикле hello мы являются может tooexecute каждая команда в последовательности.</span><span class="sxs-lookup"><span data-stu-id="0a7bc-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="0a7bc-117">Во-первых создайте временную таблицу, содержащая уникальную строку чисел используется tooidentify hello отдельные инструкции:</span><span class="sxs-lookup"><span data-stu-id="0a7bc-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

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

<span data-ttu-id="0a7bc-118">Во-вторых инициализируйте необходимые tooperform hello hello переменных цикла:</span><span class="sxs-lookup"><span data-stu-id="0a7bc-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="0a7bc-119">Теперь запустите цикл последовательного выполнения операторов:</span><span class="sxs-lookup"><span data-stu-id="0a7bc-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="0a7bc-120">Наконец, удалите hello временной таблицы, созданные в первом шаге hello</span><span class="sxs-lookup"><span data-stu-id="0a7bc-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="0a7bc-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a7bc-121">Next steps</span></span>
<span data-ttu-id="0a7bc-122">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="0a7bc-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[при]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
