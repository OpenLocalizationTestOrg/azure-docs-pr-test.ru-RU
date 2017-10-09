---
title: "aaaStored процедуры в хранилище данных SQL | Документы Microsoft"
description: "Советы по реализации хранимых процедур в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="a8c2a-103">Хранимые процедуры в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="a8c2a-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="a8c2a-104">Хранилище данных SQL поддерживает многие функции hello Transact-SQL, имеющихся в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="a8c2a-105">Что более важно, конкретных компонентов, что мы хотите tooleverage toomaximize hello производительности решения для горизонтального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="a8c2a-106">Однако toomaintain hello масштаб и производительность хранилища данных SQL существует также являются некоторых функций, которые имеют различия в поведении и другим пользователям, которые не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="a8c2a-107">В этой статье объясняется, как tooimplement хранимые процедуры в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="a8c2a-108">Введение в хранимые процедуры</span><span class="sxs-lookup"><span data-stu-id="a8c2a-108">Introducing stored procedures</span></span>
<span data-ttu-id="a8c2a-109">Хранимые процедуры — это отличный способ для инкапсуляции кода SQL; хранение его закрыть tooyour данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="a8c2a-110">Путем инкапсуляции кода hello в управляемые единицы хранимых процедур помочь разработчикам модули различных своих решений; Облегчение многократному использованию больше кода.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="a8c2a-111">Каждая хранимая процедура может также принимать параметры toomake их еще более гибким.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="a8c2a-112">Хранилище данных SQL предоставляет упрощенную и оптимизированную реализацию хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="a8c2a-113">Hello Главное отличие tooSQL которой находится сервер, hello хранимой процедуры не предварительно скомпилированный код.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="a8c2a-114">В хранилищах данных мы интересует обычно менее hello времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="a8c2a-115">Очень важно правильно компактная кода hello хранимой процедуры при обработке больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="a8c2a-116">Задача Hello — toosave часов, минут и секунд не в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="a8c2a-117">Поэтому происходит гораздо больше полезных toothink хранимых процедур как контейнеры для логики SQL.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="a8c2a-118">При выполнении хранилище данных SQL инструкций SQL hello хранимой процедуры синтаксического анализа, переводятся и оптимизирован во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="a8c2a-119">Во время этого процесса каждая инструкция преобразуется в распределенные запросы.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="a8c2a-120">Hello кода SQL, который фактически выполняется для hello данных — другой toohello запроса, отправленного.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="a8c2a-121">Вложенные хранимые процедуры</span><span class="sxs-lookup"><span data-stu-id="a8c2a-121">Nesting stored procedures</span></span>
<span data-ttu-id="a8c2a-122">Если хранимые процедуры вызывать другие хранимые процедуры или выполняется динамический код sql, то внутреннее hello хранимой процедуры или вызова кода, называется вложенным toobe.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="a8c2a-123">Хранилище данных SQL поддерживает до 8 уровней вложенности.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="a8c2a-124">Это немного отличается tooSQL сервера.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="a8c2a-125">уровень вложенности Hello в SQL Server — 32.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="a8c2a-126">Hello верхнего уровня вызова хранимой процедуры соответствует toonest уровня 1</span><span class="sxs-lookup"><span data-stu-id="a8c2a-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="a8c2a-127">Если hello хранимой процедуры также делает другой EXEC вызова, то это приведет к увеличению too2 уровня вложенности hello</span><span class="sxs-lookup"><span data-stu-id="a8c2a-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="a8c2a-128">Если вторая процедура hello затем выполняет некоторые динамического sql затем это приведет к увеличению too3 уровня вложенности hello</span><span class="sxs-lookup"><span data-stu-id="a8c2a-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="a8c2a-129">Примечание. Хранилище данных SQL не поддерживает @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="a8c2a-130">Вам потребуется tookeep за уровень вложенности самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="a8c2a-131">Однако маловероятно, ограничение уровня вложенности hello 8 выполнение будет остановлено, но если это сделать, вы должны toore рабочего кода и «сведение» его, чтобы он не превышает это ограничение.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="a8c2a-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="a8c2a-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="a8c2a-133">Хранилище данных SQL не выполняет tooconsume hello результирующего набора хранимой процедуры с инструкцией INSERT.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="a8c2a-134">Однако существует другой подход, которым можно воспользоваться.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="a8c2a-135">Можно найти toohello следующей статьей [временные таблицы] пример toodo это.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="a8c2a-136">Ограничения</span><span class="sxs-lookup"><span data-stu-id="a8c2a-136">Limitations</span></span>
<span data-ttu-id="a8c2a-137">Существуют некоторые аспекты хранимых процедур Transact-SQL, которые не реализованы в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="a8c2a-138">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="a8c2a-138">They are:</span></span>

* <span data-ttu-id="a8c2a-139">временные хранимые процедуры;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-139">temporary stored procedures</span></span>
* <span data-ttu-id="a8c2a-140">нумерованные хранимые процедуры;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-140">numbered stored procedures</span></span>
* <span data-ttu-id="a8c2a-141">расширенные хранимые процедуры;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-141">extended stored procedures</span></span>
* <span data-ttu-id="a8c2a-142">хранимые процедуры CLR;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-142">CLR stored procedures</span></span>
* <span data-ttu-id="a8c2a-143">возможность шифрования;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-143">encryption option</span></span>
* <span data-ttu-id="a8c2a-144">возможность репликации;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-144">replication option</span></span>
* <span data-ttu-id="a8c2a-145">параметры с табличным значением;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-145">table-valued parameters</span></span>
* <span data-ttu-id="a8c2a-146">параметры только для чтения;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-146">read-only parameters</span></span>
* <span data-ttu-id="a8c2a-147">параметры по умолчанию;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-147">default parameters</span></span>
* <span data-ttu-id="a8c2a-148">контекст выполнения;</span><span class="sxs-lookup"><span data-stu-id="a8c2a-148">execution contexts</span></span>
* <span data-ttu-id="a8c2a-149">инструкция Return.</span><span class="sxs-lookup"><span data-stu-id="a8c2a-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8c2a-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8c2a-150">Next steps</span></span>
<span data-ttu-id="a8c2a-151">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="a8c2a-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[временные таблицы]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
