---
title: "Назначение переменных в хранилище данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: 045d5148cd3f12dac63c961ccf7c953d355ed725
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="2fb3c-103">Назначение переменных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="2fb3c-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="2fb3c-104">Переменные в хранилище данных SQL задаются с помощью инструкции `DECLARE` или инструкции `SET`.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span></span>

<span data-ttu-id="2fb3c-105">Ниже перечислены допустимые способы задания значения переменной:</span><span class="sxs-lookup"><span data-stu-id="2fb3c-105">All of the following are perfectly valid ways to set a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="2fb3c-106">Задание переменных с помощью DECLARE</span><span class="sxs-lookup"><span data-stu-id="2fb3c-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="2fb3c-107">Инициализация переменных с помощью DECLARE — один из наиболее гибких способов задать значение переменной в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="2fb3c-108">С помощью DECLARE можно задать одновременно несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-108">You can also use DECLARE to set more than one variable at a time.</span></span> <span data-ttu-id="2fb3c-109">Использовать `SELECT` или `UPDATE` для этого нельзя:</span><span class="sxs-lookup"><span data-stu-id="2fb3c-109">You cannot use `SELECT` or `UPDATE` to do this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="2fb3c-110">Нельзя инициализировать и использовать переменную в одной и той же инструкции DECLARE.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-110">You cannot initialise and use a variable in the same DECLARE statement.</span></span> <span data-ttu-id="2fb3c-111">Чтобы проиллюстрировать это, ниже приведен **недопустимый** пример, так как @p1 инициализируется и используется в одной и той же инструкции DECLARE.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span></span> <span data-ttu-id="2fb3c-112">Это приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="2fb3c-113">Задание значений с помощью SET</span><span class="sxs-lookup"><span data-stu-id="2fb3c-113">Setting values with SET</span></span>
<span data-ttu-id="2fb3c-114">SET — это очень распространенный метод задания одной переменной.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="2fb3c-115">Ниже приведены примеры допустимого задания переменной с помощью SET:</span><span class="sxs-lookup"><span data-stu-id="2fb3c-115">All of the examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="2fb3c-116">С помощью SET можно одновременно задать только одну переменную.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="2fb3c-117">Тем не менее, как видно выше, допускаются составные операторы.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="2fb3c-118">Ограничения</span><span class="sxs-lookup"><span data-stu-id="2fb3c-118">Limitations</span></span>
<span data-ttu-id="2fb3c-119">Нельзя использовать SELECT или UPDATE, чтобы присвоить значение переменной.</span><span class="sxs-lookup"><span data-stu-id="2fb3c-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fb3c-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2fb3c-120">Next steps</span></span>
<span data-ttu-id="2fb3c-121">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="2fb3c-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
