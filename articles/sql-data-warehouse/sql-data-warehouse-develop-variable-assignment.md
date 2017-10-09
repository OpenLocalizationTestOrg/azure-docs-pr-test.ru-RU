---
title: "переменные aaaAssign в хранилище данных SQL | Документы Microsoft"
description: "Советы по присваиванию значений переменных Transact-SQL в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="a77e8-103">Назначение переменных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="a77e8-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="a77e8-104">Переменные в хранилище данных SQL задаются с использованием hello `DECLARE` инструкции или hello `SET` инструкции.</span><span class="sxs-lookup"><span data-stu-id="a77e8-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="a77e8-105">Все следующие hello не вполне допустимые способы tooset значение переменной:</span><span class="sxs-lookup"><span data-stu-id="a77e8-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="a77e8-106">Задание переменных с помощью DECLARE</span><span class="sxs-lookup"><span data-stu-id="a77e8-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="a77e8-107">Инициализация переменных с DECLARE является одним из наиболее гибкий tooset способов hello значение переменной в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a77e8-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="a77e8-108">Также можно использовать более одной переменной DECLARE tooset одновременно.</span><span class="sxs-lookup"><span data-stu-id="a77e8-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="a77e8-109">Нельзя использовать `SELECT` или `UPDATE` toodo это:</span><span class="sxs-lookup"><span data-stu-id="a77e8-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="a77e8-110">Не удается инициализировать и использовать переменную в hello же инструкции DECLARE.</span><span class="sxs-lookup"><span data-stu-id="a77e8-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="a77e8-111">tooillustrate hello точке hello приведенном ниже примере показан **не** допускается в качестве @p1 и инициализируется и используется в hello же инструкции DECLARE.</span><span class="sxs-lookup"><span data-stu-id="a77e8-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="a77e8-112">Это приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="a77e8-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="a77e8-113">Задание значений с помощью SET</span><span class="sxs-lookup"><span data-stu-id="a77e8-113">Setting values with SET</span></span>
<span data-ttu-id="a77e8-114">SET — это очень распространенный метод задания одной переменной.</span><span class="sxs-lookup"><span data-stu-id="a77e8-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="a77e8-115">Все примеры hello ниже показаны допустимые способы задания переменной с НАБОРОМ:</span><span class="sxs-lookup"><span data-stu-id="a77e8-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="a77e8-116">С помощью SET можно одновременно задать только одну переменную.</span><span class="sxs-lookup"><span data-stu-id="a77e8-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="a77e8-117">Тем не менее, как видно выше, допускаются составные операторы.</span><span class="sxs-lookup"><span data-stu-id="a77e8-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="a77e8-118">Ограничения</span><span class="sxs-lookup"><span data-stu-id="a77e8-118">Limitations</span></span>
<span data-ttu-id="a77e8-119">Нельзя использовать SELECT или UPDATE, чтобы присвоить значение переменной.</span><span class="sxs-lookup"><span data-stu-id="a77e8-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a77e8-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a77e8-120">Next steps</span></span>
<span data-ttu-id="a77e8-121">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="a77e8-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
