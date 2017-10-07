---
title: "aaaCreate суррогатных ключей с использованием идентификатора | Документы Microsoft"
description: "Узнайте, как toouse УДОСТОВЕРЕНИЕ toocreate суррогатные ключи на ваших таблицах."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="3a52a-103">Создание суррогатных ключей с использованием свойства IDENTITY</span><span class="sxs-lookup"><span data-stu-id="3a52a-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3a52a-104">[Обзор][Overview]</span><span class="sxs-lookup"><span data-stu-id="3a52a-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3a52a-105">[Типы данных][Data Types]</span><span class="sxs-lookup"><span data-stu-id="3a52a-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="3a52a-106">[Распределение][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3a52a-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="3a52a-107">[Индекс][Index]</span><span class="sxs-lookup"><span data-stu-id="3a52a-107">[Index][Index]</span></span>
> * <span data-ttu-id="3a52a-108">[Секция][Partition]</span><span class="sxs-lookup"><span data-stu-id="3a52a-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="3a52a-109">[Статистика][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3a52a-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="3a52a-110">[Временные таблицы][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3a52a-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="3a52a-111">[Удостоверение][Identity]</span><span class="sxs-lookup"><span data-stu-id="3a52a-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="3a52a-112">Многие администраторы моделей данных, например toocreate суррогатными ключами на эти таблицы при их разработке моделей хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="3a52a-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="3a52a-113">Можно использовать tooachieve свойство IDENTITY hello этой цели просто и эффективно без влияния на производительность нагрузки.</span><span class="sxs-lookup"><span data-stu-id="3a52a-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="3a52a-114">Приступая к работе со свойством IDENTITY</span><span class="sxs-lookup"><span data-stu-id="3a52a-114">Get started with IDENTITY</span></span>
<span data-ttu-id="3a52a-115">Таблицы можно определить как имеющий свойство IDENTITY hello при первом создании hello таблицы с помощью синтаксиса, аналогичные toohello следующей инструкцией:</span><span class="sxs-lookup"><span data-stu-id="3a52a-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="3a52a-116">Затем можно использовать `INSERT..SELECT` toopopulate hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="3a52a-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="3a52a-117">Поведение</span><span class="sxs-lookup"><span data-stu-id="3a52a-117">Behavior</span></span>
<span data-ttu-id="3a52a-118">Hello свойство IDENTITY может спроектированный tooscale out все hello распределения в хранилище данных hello без влияния на производительность нагрузки.</span><span class="sxs-lookup"><span data-stu-id="3a52a-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="3a52a-119">Таким образом реализация hello удостоверения ориентирован по достижению этой цели.</span><span class="sxs-lookup"><span data-stu-id="3a52a-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="3a52a-120">В этом разделе описываются особенности hello из toohelp реализацию hello понимаете их более подробно.</span><span class="sxs-lookup"><span data-stu-id="3a52a-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="3a52a-121">Распределение значений</span><span class="sxs-lookup"><span data-stu-id="3a52a-121">Allocation of values</span></span>
<span data-ttu-id="3a52a-122">Hello свойство IDENTITY не гарантирует порядок hello в какой hello распределяются значения символов-заместителей, отображающие hello поведение SQL Server и базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3a52a-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="3a52a-123">Тем не менее в хранилище данных SQL Azure, гарантирует отсутствие hello более заметно.</span><span class="sxs-lookup"><span data-stu-id="3a52a-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="3a52a-124">Следующий пример Hello. приведен пример:</span><span class="sxs-lookup"><span data-stu-id="3a52a-124">hello following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="3a52a-125">В предыдущих пример hello две строки, приобретенных в распределении 1.</span><span class="sxs-lookup"><span data-stu-id="3a52a-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="3a52a-126">Первая строка Hello имеет hello символов-заместителей значение 1 в столбце `C1`, и hello вторая строка имеет значение 61 hello символов-заместителей.</span><span class="sxs-lookup"><span data-stu-id="3a52a-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="3a52a-127">Оба эти значения были созданы при hello свойство IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="3a52a-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="3a52a-128">Однако hello распределением значений hello не является непрерывным.</span><span class="sxs-lookup"><span data-stu-id="3a52a-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="3a52a-129">В этом весь замысел.</span><span class="sxs-lookup"><span data-stu-id="3a52a-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="3a52a-130">Неравномерные данные</span><span class="sxs-lookup"><span data-stu-id="3a52a-130">Skewed data</span></span> 
<span data-ttu-id="3a52a-131">диапазон значений для типа данных hello Hello равномерно распределены по hello распределения.</span><span class="sxs-lookup"><span data-stu-id="3a52a-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="3a52a-132">Если таблица распространения страдает от становятся ассиметричные данные, затем hello диапазон значений, которые доступны toohello тип данных может быть исчерпана преждевременно.</span><span class="sxs-lookup"><span data-stu-id="3a52a-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="3a52a-133">Например, все данные hello в одном распространения заканчивается, затем эффективно hello таблица имеет доступ tooonly sixtieth один hello значений типа данных hello.</span><span class="sxs-lookup"><span data-stu-id="3a52a-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="3a52a-134">По этой причине hello свойство IDENTITY ограничено слишком`INT` и `BIGINT` только для типов данных.</span><span class="sxs-lookup"><span data-stu-id="3a52a-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="3a52a-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="3a52a-135">SELECT..INTO</span></span>
<span data-ttu-id="3a52a-136">При выборе существующего столбца ИДЕНТИФИКАТОРОВ в новую таблицу hello новый столбец наследует свойство IDENTITY hello, если верно одно из следующих условий hello:</span><span class="sxs-lookup"><span data-stu-id="3a52a-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="3a52a-137">Hello инструкция SELECT содержит соединение.</span><span class="sxs-lookup"><span data-stu-id="3a52a-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="3a52a-138">несколько инструкций SELECT соединены с помощью инструкции UNION;</span><span class="sxs-lookup"><span data-stu-id="3a52a-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="3a52a-139">столбец ИДЕНТИФИКАТОРОВ Hello встречается более одного раза в списке SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="3a52a-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="3a52a-140">столбец ИДЕНТИФИКАТОРОВ Hello является частью выражения.</span><span class="sxs-lookup"><span data-stu-id="3a52a-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="3a52a-141">Если истинно одно из этих условий, hello столбец создается не NULL и не наследует свойство IDENTITY hello.</span><span class="sxs-lookup"><span data-stu-id="3a52a-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="3a52a-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="3a52a-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="3a52a-143">Создание таблицы AS ВЫБЕРИТЕ (CTAS) следующим hello же SQL Server поведение, описанное для SELECT... В.</span><span class="sxs-lookup"><span data-stu-id="3a52a-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="3a52a-144">Тем не менее, нельзя указать свойство IDENTITY в определении столбца hello hello `CREATE TABLE` инструкцию hello.</span><span class="sxs-lookup"><span data-stu-id="3a52a-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="3a52a-145">Функция IDENTITY hello нельзя использовать в hello `SELECT` частью hello CTAS.</span><span class="sxs-lookup"><span data-stu-id="3a52a-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="3a52a-146">toopopulate таблицы необходимо toouse `CREATE TABLE` toodefine hello таблицы, за которым следует `INSERT..SELECT` toopopulate его.</span><span class="sxs-lookup"><span data-stu-id="3a52a-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="3a52a-147">Явная вставка значений в столбец IDENTITY</span><span class="sxs-lookup"><span data-stu-id="3a52a-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="3a52a-148">Хранилище данных SQL поддерживает синтаксис `SET IDENTITY_INSERT <your table> ON|OFF`.</span><span class="sxs-lookup"><span data-stu-id="3a52a-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="3a52a-149">Можно использовать этот синтаксис tooexplicitly вставки значений в столбец ИДЕНТИФИКАТОРОВ hello.</span><span class="sxs-lookup"><span data-stu-id="3a52a-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="3a52a-150">Многие архитекторы данных как стандартные отрицательное toouse для определенных значений строк в их измерений.</span><span class="sxs-lookup"><span data-stu-id="3a52a-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="3a52a-151">Пример: hello -1 или строка «неизвестный элемент».</span><span class="sxs-lookup"><span data-stu-id="3a52a-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="3a52a-152">следующий скрипт Hello показано, как tooexplicitly добавить эту строку с помощью SET IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="3a52a-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="3a52a-153">Загрузка данных в таблицу со свойством IDENTITY</span><span class="sxs-lookup"><span data-stu-id="3a52a-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="3a52a-154">наличие Hello hello свойство IDENTITY имеет некоторые последствия tooyour загрузка данных код.</span><span class="sxs-lookup"><span data-stu-id="3a52a-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="3a52a-155">В этом разделе описываются некоторые основные схемы загрузки данных в таблицы с использованием свойства IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="3a52a-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="3a52a-156">Загрузка данных с помощью PolyBase</span><span class="sxs-lookup"><span data-stu-id="3a52a-156">Load data with PolyBase</span></span>
<span data-ttu-id="3a52a-157">tooload данные в таблицу и создать суррогатный ключ, используя УДОСТОВЕРЕНИЕ, создать таблицу hello и затем использовать инструкции INSERT... SELECT или INSERT... Загрузка hello tooperform значения.</span><span class="sxs-lookup"><span data-stu-id="3a52a-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="3a52a-158">Hello следующий пример выделяет hello базовый шаблон:</span><span class="sxs-lookup"><span data-stu-id="3a52a-158">hello following example highlights hello basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="3a52a-159">Это не возможные toouse `CREATE TABLE AS SELECT` в настоящее время при загрузке данных в таблицу со столбцом ИДЕНТИФИКАТОРОВ.</span><span class="sxs-lookup"><span data-stu-id="3a52a-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="3a52a-160">Дополнительные сведения о загрузке данных с помощью hello массового копирования программу (BCP) средства см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="3a52a-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="3a52a-161">[Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="3a52a-162">[Руководство по использованию PolyBase в хранилище данных SQL][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="3a52a-163">Загрузка данных с помощью BCP</span><span class="sxs-lookup"><span data-stu-id="3a52a-163">Load data with BCP</span></span>
<span data-ttu-id="3a52a-164">Средство командной строки, которые можно использовать tooload данных в хранилище данных SQL является BCP.</span><span class="sxs-lookup"><span data-stu-id="3a52a-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="3a52a-165">Один из параметров (-E) элементы управления hello BCP поведение при загрузке данных в таблицу со столбцом ИДЕНТИФИКАТОРОВ.</span><span class="sxs-lookup"><span data-stu-id="3a52a-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="3a52a-166">Если указан параметр -E, hello значения, которые содержатся в hello входного файла для столбца hello с УДОСТОВЕРЕНИЕМ, сохраняются.</span><span class="sxs-lookup"><span data-stu-id="3a52a-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="3a52a-167">Если -E *не* указано, то hello значения в этом столбце учитываются.</span><span class="sxs-lookup"><span data-stu-id="3a52a-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="3a52a-168">Если столбец идентификаторов hello не указан, hello данных загружается в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="3a52a-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="3a52a-169">Hello значения создаются политики toohello увеличения и начальное значение свойства hello в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="3a52a-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="3a52a-170">Дополнительные сведения о загрузке данных с помощью команды BCP см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="3a52a-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="3a52a-171">[Загрузка данных с помощью bcp][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-171">[Load with BCP][]</span></span>
- <span data-ttu-id="3a52a-172">[bcp Utility][] (Служебная программа BCP)</span><span class="sxs-lookup"><span data-stu-id="3a52a-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="3a52a-173">Представления каталога</span><span class="sxs-lookup"><span data-stu-id="3a52a-173">Catalog views</span></span>
<span data-ttu-id="3a52a-174">Хранилище данных SQL поддерживает hello `sys.identity_columns` представления каталога.</span><span class="sxs-lookup"><span data-stu-id="3a52a-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="3a52a-175">Данное представление может быть используется tooidentify столбца, имеющего свойство IDENTITY hello.</span><span class="sxs-lookup"><span data-stu-id="3a52a-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="3a52a-176">toohelp лучше понять hello схемы базы данных, в этом примере показано, как toointegrate `sys.identity_columns` с другими представлениями каталога системы:</span><span class="sxs-lookup"><span data-stu-id="3a52a-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="3a52a-177">Ограничения</span><span class="sxs-lookup"><span data-stu-id="3a52a-177">Limitations</span></span>
<span data-ttu-id="3a52a-178">Hello свойство IDENTITY не может использоваться в hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="3a52a-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="3a52a-179">Когда тип данных столбца hello не INT или BIGINT</span><span class="sxs-lookup"><span data-stu-id="3a52a-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="3a52a-180">Где hello столбец присутствует также ключ распределения hello</span><span class="sxs-lookup"><span data-stu-id="3a52a-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="3a52a-181">Где hello таблица является внешней таблицы</span><span class="sxs-lookup"><span data-stu-id="3a52a-181">Where hello table is an external table</span></span> 

<span data-ttu-id="3a52a-182">в хранилище данных SQL не поддерживаются следующие функции, связанные с Hello:</span><span class="sxs-lookup"><span data-stu-id="3a52a-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="3a52a-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="3a52a-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="3a52a-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="3a52a-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="3a52a-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="3a52a-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="3a52a-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="3a52a-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="3a52a-190">Задачи</span><span class="sxs-lookup"><span data-stu-id="3a52a-190">Tasks</span></span>

<span data-ttu-id="3a52a-191">Этот раздел содержит пример кода можно использовать tooperform общих задач при работе со столбцами ИДЕНТИФИКАТОРОВ.</span><span class="sxs-lookup"><span data-stu-id="3a52a-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="3a52a-192">Столбец C1 — hello УДОСТОВЕРЕНИЯ в все hello следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="3a52a-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="3a52a-193">Найти значение hello наибольшим выделенной таблицы</span><span class="sxs-lookup"><span data-stu-id="3a52a-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="3a52a-194">Используйте hello `MAX()` функцию toodetermine hello наибольшее значение выделенной для распределенных таблицы:</span><span class="sxs-lookup"><span data-stu-id="3a52a-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="3a52a-195">Найти hello начального значения и шага приращения для свойства IDENTITY hello</span><span class="sxs-lookup"><span data-stu-id="3a52a-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="3a52a-196">Можно использовать hello каталога представлений toodiscover hello увеличения и начального значения конфигурации значения идентификаторов для таблицы с помощью приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="3a52a-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="3a52a-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a52a-197">Next steps</span></span>

* <span data-ttu-id="3a52a-198">toolearn Дополнительные сведения о разработке таблиц, в разделе [Общие сведения о таблицах][Overview], [типы табличных данных][Data Types], [распространять таблицы] [ Distribute], [Индекса таблицы][Index], [секционировать таблицу][Partition], и [ Временные таблицы][Temporary].</span><span class="sxs-lookup"><span data-stu-id="3a52a-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="3a52a-199">Дополнительные рекомендации см. в статье [Рекомендации по использованию хранилища данных SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="3a52a-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Загрузка данных с помощью bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Руководство по использованию PolyBase в хранилище данных SQL]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[bcp Utility]: https://msdn.microsoft.com/library/ms162802.aspx (Служебная программа BCP)
  

<!--Other Web references-->  
