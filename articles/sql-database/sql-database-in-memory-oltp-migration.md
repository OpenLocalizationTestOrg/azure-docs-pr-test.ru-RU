---
title: "aaaIn-Memory OLTP повышает производительность транзакций SQL | Документы Microsoft"
description: "In-Memory OLTP adopt tooimprove транзакций производительности в существующую базу данных SQL."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="daa5d-103">Использование In-Memory OLTP tooimprove производительность приложений базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="daa5d-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="daa5d-104">[In-Memory OLTP](sql-database-in-memory.md) может быть используется tooimprove hello производительность обработки транзакций, приема данных и сценариев временных данных, в [Premium](sql-database-service-tiers.md) баз данных SQL Azure без увеличения hello ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="daa5d-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="daa5d-105">Узнайте, как [Quorum удваивает ключевую рабочую нагрузку на базу данных при одновременном сокращении DTU на 70 % благодаря использованию базы данных SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="daa5d-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="daa5d-106">Выполните эти шаги по tooadopt In-Memory OLTP в существующей базе данных.</span><span class="sxs-lookup"><span data-stu-id="daa5d-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="daa5d-107">Этап 1. Проверка того, что используется база данных уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="daa5d-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="daa5d-108">Выполняющаяся в памяти OLTP поддерживается только в базах данных уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="daa5d-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="daa5d-109">Поддерживаются в памяти, если hello возвращаемый результат равен 1 (не 0):</span><span class="sxs-lookup"><span data-stu-id="daa5d-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="daa5d-110">Сокращение *XTP* обозначает технологию *экстремальной обработки транзакций (Extreme Transaction Processing)*.</span><span class="sxs-lookup"><span data-stu-id="daa5d-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="daa5d-111">Шаг 2: Определение объектов toomigrate tooIn-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="daa5d-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="daa5d-112">Среда SSMS позволяет создать отчет **Обзор анализа производительности транзакций** , который затем можно запустить для базы данных с активной рабочей нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="daa5d-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="daa5d-113">отчет Hello определяет таблицы и хранимые процедуры, которые являются кандидатами на перенос tooIn-Memory OLTP.</span><span class="sxs-lookup"><span data-stu-id="daa5d-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="daa5d-114">В среде SSMS toogenerate hello отчета:</span><span class="sxs-lookup"><span data-stu-id="daa5d-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="daa5d-115">В hello **обозревателя объектов**, щелкните правой кнопкой мыши узел вашей базы данных.</span><span class="sxs-lookup"><span data-stu-id="daa5d-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="daa5d-116">Щелкните **Отчеты** > **Стандартные отчеты** > **Обзор анализа производительности транзакций**.</span><span class="sxs-lookup"><span data-stu-id="daa5d-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="daa5d-117">Дополнительные сведения см. в разделе [определение ли таблица или хранимая процедура должна быть перенесена tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="daa5d-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="daa5d-118">Шаг 3. Создание сопоставимой тестовой базы данных</span><span class="sxs-lookup"><span data-stu-id="daa5d-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="daa5d-119">Предположим, что отчет hello указывает базу данных таблицу, которая будет полезным, преобразовать tooa оптимизированной для памяти таблицы.</span><span class="sxs-lookup"><span data-stu-id="daa5d-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="daa5d-120">Рекомендуется сначала протестировать tooconfirm hello указывает путем проверки.</span><span class="sxs-lookup"><span data-stu-id="daa5d-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="daa5d-121">Вам понадобится тестовая копия рабочей базы данных.</span><span class="sxs-lookup"><span data-stu-id="daa5d-121">You need a test copy of your production database.</span></span> <span data-ttu-id="daa5d-122">Hello тестирования базы данных должны находиться в hello же службы уровень как ваша рабочая база данных.</span><span class="sxs-lookup"><span data-stu-id="daa5d-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="daa5d-123">тестирование, tooease настроить тестовой базы данных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="daa5d-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="daa5d-124">Подключение toohello тестовую базу данных с помощью среды SSMS.</span><span class="sxs-lookup"><span data-stu-id="daa5d-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="daa5d-125">tooavoid необходимости Здравствуйте параметр WITH (SNAPSHOT) в запросах, задайте параметр hello базы данных, как показано в hello, следующие инструкции T-SQL:</span><span class="sxs-lookup"><span data-stu-id="daa5d-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="daa5d-126">Шаг 4. Миграция таблиц</span><span class="sxs-lookup"><span data-stu-id="daa5d-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="daa5d-127">Необходимо создать и заполнить копии оптимизированных для памяти таблицы hello требуется tootest.</span><span class="sxs-lookup"><span data-stu-id="daa5d-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="daa5d-128">Ее можно создать с помощью:</span><span class="sxs-lookup"><span data-stu-id="daa5d-128">You can create it by using either:</span></span>

* <span data-ttu-id="daa5d-129">Hello удобные мастера оптимизации памяти в среде SSMS.</span><span class="sxs-lookup"><span data-stu-id="daa5d-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="daa5d-130">вручную с помощью инструкций T-SQL.</span><span class="sxs-lookup"><span data-stu-id="daa5d-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="daa5d-131">Создание таблицы с помощью мастера оптимизации памяти в SSMS</span><span class="sxs-lookup"><span data-stu-id="daa5d-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="daa5d-132">toouse этот вариант миграции:</span><span class="sxs-lookup"><span data-stu-id="daa5d-132">toouse this migration option:</span></span>

1. <span data-ttu-id="daa5d-133">Подключение toohello тестовую базу данных с помощью SSMS.</span><span class="sxs-lookup"><span data-stu-id="daa5d-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="daa5d-134">В hello **обозревателя объектов**, щелкните правой кнопкой мыши в таблице hello и нажмите кнопку **помощник по оптимизации памяти**.</span><span class="sxs-lookup"><span data-stu-id="daa5d-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="daa5d-135">Hello **помощника по оптимизатор памяти таблицы** появится мастер.</span><span class="sxs-lookup"><span data-stu-id="daa5d-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="daa5d-136">В мастере приветствия щелкните **проверки миграции** (или hello **Далее** кнопки) toosee, если таблица hello неподдерживаемые функции, которые не поддерживаются в таблицах, оптимизированных для памяти.</span><span class="sxs-lookup"><span data-stu-id="daa5d-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="daa5d-137">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="daa5d-137">For more information, see:</span></span>
   
   * <span data-ttu-id="daa5d-138">Hello *контрольный список оптимизации памяти* в [помощник по оптимизации памяти](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="daa5d-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="daa5d-139">[Конструкции языка Transact-SQL не поддерживаются компонентом In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="daa5d-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="daa5d-140">[Миграция tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="daa5d-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="daa5d-141">Если hello таблицы без неподдерживаемых функций, hello advisor можно выполнять схемой, фактически hello и переноса данных для вас.</span><span class="sxs-lookup"><span data-stu-id="daa5d-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="daa5d-142">Создание таблицы вручную с помощью инструкций T-SQL</span><span class="sxs-lookup"><span data-stu-id="daa5d-142">Manual T-SQL</span></span>
<span data-ttu-id="daa5d-143">toouse этот вариант миграции:</span><span class="sxs-lookup"><span data-stu-id="daa5d-143">toouse this migration option:</span></span>

1. <span data-ttu-id="daa5d-144">Подключение tooyour тестовую базу данных с помощью SSMS (или другой подобной программы).</span><span class="sxs-lookup"><span data-stu-id="daa5d-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="daa5d-145">Получите hello полный сценарий T-SQL для таблицы и ее индексов.</span><span class="sxs-lookup"><span data-stu-id="daa5d-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="daa5d-146">В среде SSMS щелкните правой кнопкой мыши узел таблицы.</span><span class="sxs-lookup"><span data-stu-id="daa5d-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="daa5d-147">Щелкните **Создать сценарий для таблицы** > **Используя CREATE** > **Новое окно запроса**.</span><span class="sxs-lookup"><span data-stu-id="daa5d-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="daa5d-148">В окне приветствия сценария добавьте WITH (MEMORY_OPTIMIZED = ON) toohello инструкции CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="daa5d-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="daa5d-149">Если имеется КЛАСТЕРИЗОВАННЫЙ индекс, измените его tooNONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="daa5d-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="daa5d-150">С помощью SP_RENAME переименуйте существующую таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="daa5d-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="daa5d-151">Создайте hello новые оптимизированные для памяти копии hello таблицы, выполнив измененного скрипта CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="daa5d-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="daa5d-152">Копировать hello данных tooyour оптимизированной для памяти таблицы с помощью инструкции INSERT... ВЫБЕРИТЕ * В:</span><span class="sxs-lookup"><span data-stu-id="daa5d-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="daa5d-153">Шаг 5 (необязательный). Миграция хранимых процедур</span><span class="sxs-lookup"><span data-stu-id="daa5d-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="daa5d-154">функция Hello в памяти можно также изменить хранимую процедуру для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="daa5d-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="daa5d-155">Общие сведения о скомпилированных в собственном коде хранимых процедурах</span><span class="sxs-lookup"><span data-stu-id="daa5d-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="daa5d-156">Скомпилированные в собственном коде хранимой процедуры должен иметь следующие параметры в своем предложении T-SQL с hello:</span><span class="sxs-lookup"><span data-stu-id="daa5d-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="daa5d-157">NATIVE_COMPILATION;</span><span class="sxs-lookup"><span data-stu-id="daa5d-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="daa5d-158">SCHEMABINDING: таблицы значения, которые hello хранимая процедура не может иметь свои определения столбцов, изменен каким-либо образом повлияет на hello хранимые процедуры, только удаления hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="daa5d-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="daa5d-159">Собственный модуль должен использовать один большой [блок ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) для управления транзакциями.</span><span class="sxs-lookup"><span data-stu-id="daa5d-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="daa5d-160">Роли для явной транзакции BEGIN TRANSACTION или ROLLBACK TRANSACTION не существует.</span><span class="sxs-lookup"><span data-stu-id="daa5d-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="daa5d-161">Если код обнаруживает нарушение бизнес-правила, оно может завершаться блока atomic hello с [THROW](http://msdn.microsoft.com/library/ee677615.aspx) инструкции.</span><span class="sxs-lookup"><span data-stu-id="daa5d-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="daa5d-162">Стандартная инструкция CREATE PROCEDURE для создания скомпилированных в собственном коде процедур</span><span class="sxs-lookup"><span data-stu-id="daa5d-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="daa5d-163">Обычно hello T-SQL toocreate скомпилированной хранимой процедуры — примерно toohello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="daa5d-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="daa5d-164">Для hello TRANSACTION_ISOLATION_LEVEL моментального СНИМКА является наиболее распространенные значение hello скомпилированные в собственном коде хранимые процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="daa5d-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="daa5d-165">Однако подмножество hello других поддерживаются значения:</span><span class="sxs-lookup"><span data-stu-id="daa5d-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="daa5d-166">REPEATABLE READ;</span><span class="sxs-lookup"><span data-stu-id="daa5d-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="daa5d-167">SERIALIZABLE.</span><span class="sxs-lookup"><span data-stu-id="daa5d-167">SERIALIZABLE</span></span>
* <span data-ttu-id="daa5d-168">Hello значение языка должен присутствовать в представлении sys.languages hello.</span><span class="sxs-lookup"><span data-stu-id="daa5d-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="daa5d-169">Как toomigrate хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="daa5d-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="daa5d-170">Hello миграции, необходимо:</span><span class="sxs-lookup"><span data-stu-id="daa5d-170">hello migration steps are:</span></span>

1. <span data-ttu-id="daa5d-171">Получите hello CREATE PROCEDURE сценария toohello обычных интерпретируемых хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="daa5d-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="daa5d-172">Перепишите его toomatch заголовок hello предыдущего шаблона.</span><span class="sxs-lookup"><span data-stu-id="daa5d-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="daa5d-173">Проверить, использует ли hello хранимой процедуры код T-SQL любых компонентов, которые не поддерживаются для хранимых процедур, скомпилированных в собственном коде.</span><span class="sxs-lookup"><span data-stu-id="daa5d-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="daa5d-174">При необходимости устраните эту проблему.</span><span class="sxs-lookup"><span data-stu-id="daa5d-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="daa5d-175">Дополнительные сведения см. в статье [Проблемы миграции, связанные с хранимыми процедурами, скомпилированными в собственном коде](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="daa5d-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="daa5d-176">С помощью хранимой процедуры SP_RENAME переименуйте hello старую хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="daa5d-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="daa5d-177">Или просто удалите ее с помощью DROP.</span><span class="sxs-lookup"><span data-stu-id="daa5d-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="daa5d-178">Запустите измененный сценарий T-SQL CREATE PROCEDURE.</span><span class="sxs-lookup"><span data-stu-id="daa5d-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="daa5d-179">Шаг 6. Запуск рабочей нагрузки в тестовой среде</span><span class="sxs-lookup"><span data-stu-id="daa5d-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="daa5d-180">Запустите рабочую нагрузку в тестовой базы данных, аналогичные toohello рабочая нагрузка, которая выполняется в вашей рабочей базы данных.</span><span class="sxs-lookup"><span data-stu-id="daa5d-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="daa5d-181">Должна помочь определить hello выигрыш в производительности достигается путем использования функции hello в памяти для таблиц и хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="daa5d-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="daa5d-182">Основные атрибуты hello рабочей нагрузки являются:</span><span class="sxs-lookup"><span data-stu-id="daa5d-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="daa5d-183">количество одновременных подключений;</span><span class="sxs-lookup"><span data-stu-id="daa5d-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="daa5d-184">отношение количества операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="daa5d-184">Read/write ratio.</span></span>

<span data-ttu-id="daa5d-185">tootailor и выполнения hello тестовую рабочую нагрузку, рассмотрите возможность использования средства под рукой ostress.exe hello, которое показано в [здесь](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="daa5d-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="daa5d-186">toominimize задержку в сети и выполнить тест в hello же Azure географическом регионе, где существует hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="daa5d-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="daa5d-187">Шаг 7. Мониторинг после реализации</span><span class="sxs-lookup"><span data-stu-id="daa5d-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="daa5d-188">Рассмотрим наблюдения за эффекты производительности hello реализации в памяти в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="daa5d-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="daa5d-189">[Мониторинг хранилища In-Memory](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="daa5d-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="daa5d-190">Мониторинг базы данных SQL Azure с помощью динамических представлений управления</span><span class="sxs-lookup"><span data-stu-id="daa5d-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="daa5d-191">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="daa5d-191">Related links</span></span>
* [<span data-ttu-id="daa5d-192">In-Memory OLTP (оптимизация в памяти)</span><span class="sxs-lookup"><span data-stu-id="daa5d-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="daa5d-193">Введение tooNatively хранимых процедур, скомпилированных</span><span class="sxs-lookup"><span data-stu-id="daa5d-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="daa5d-194">Помощник по оптимизации памяти</span><span class="sxs-lookup"><span data-stu-id="daa5d-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

