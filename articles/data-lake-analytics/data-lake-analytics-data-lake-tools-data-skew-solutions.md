---
title: "проблемы aaaResolve Рассогласование данных с помощью средств Озера данных Azure для Visual Studio | Документы Microsoft"
description: "Сведения об устранении проблем неравномерного распределения данных с помощью средств Azure Data Lake для Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="573fc-103">Решение проблем неравномерного распределения данных с помощью средств Azure Data Lake для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="573fc-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="573fc-104">Что такое неравномерное распределение данных?</span><span class="sxs-lookup"><span data-stu-id="573fc-104">What is data skew?</span></span>

<span data-ttu-id="573fc-105">Коротко говоря, неравномерное распределение данных — это чрезмерно представленное значение.</span><span class="sxs-lookup"><span data-stu-id="573fc-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="573fc-106">Предположим, что вы присвоили 50 налога прошедшие tooaudit налоговых деклараций, один examiner для каждого из штатов США.</span><span class="sxs-lookup"><span data-stu-id="573fc-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="573fc-107">examiner Вайоминг Hello, так как существует заполнение hello мал, имеет немного toodo.</span><span class="sxs-lookup"><span data-stu-id="573fc-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="573fc-108">В Калифорнии Однако hello examiner хранится сильно загружен из-за состояния hello большое.</span><span class="sxs-lookup"><span data-stu-id="573fc-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="573fc-109">![Пример проблемы неравномерного распределения данных](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="573fc-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="573fc-110">В нашем сценарии hello данных неравномерно распределяется по все прошедшие налогов, который означает, что некоторые прошедшие должен работать в более, чем другие.</span><span class="sxs-lookup"><span data-stu-id="573fc-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="573fc-111">В свою работу часто возникают ситуаций, как в данном примере hello examiner налога.</span><span class="sxs-lookup"><span data-stu-id="573fc-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="573fc-112">С более технической точки зрения одной вершины возвращает намного больше данных, чем его коллегами ситуацию, которая делает вершин hello работать более чем hello другим пользователям, которые в конечном итоге замедляет все задание.</span><span class="sxs-lookup"><span data-stu-id="573fc-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="573fc-113">Что еще хуже, hello задания может закончится, так как вершины может иметь, например, ограничение 5 часов выполнения и ограничение 6 ГБ памяти.</span><span class="sxs-lookup"><span data-stu-id="573fc-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="573fc-114">Устранение неравномерного распределения данных</span><span class="sxs-lookup"><span data-stu-id="573fc-114">Resolving data-skew problems</span></span>

<span data-ttu-id="573fc-115">Средства Azure Data Lake для Visual Studio помогают обнаружить проблемы неравномерного распределения данных в задании.</span><span class="sxs-lookup"><span data-stu-id="573fc-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="573fc-116">Если существует проблема, можно разрешить ее, попытавшись hello решения в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="573fc-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="573fc-117">Решение 1. Улучшение секционирования таблиц</span><span class="sxs-lookup"><span data-stu-id="573fc-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="573fc-118">Вариант 1: Hello фильтра неравномерным значение ключа заранее</span><span class="sxs-lookup"><span data-stu-id="573fc-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="573fc-119">Если он не влияет на бизнес-логики, можно фильтровать значения повышение частоты hello заранее.</span><span class="sxs-lookup"><span data-stu-id="573fc-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="573fc-120">Например при наличии большой объем 000-000-000 в столбце GUID, это может быть tooaggregate это значение.</span><span class="sxs-lookup"><span data-stu-id="573fc-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="573fc-121">Прежде чем aggregate, можно написать «ГДЕ GUID! = «000 000 000» «toofilter hello высокочастотные значение.</span><span class="sxs-lookup"><span data-stu-id="573fc-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="573fc-122">Вариант 2. Выберите другой ключ секции или распределения</span><span class="sxs-lookup"><span data-stu-id="573fc-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="573fc-123">В hello предшествующий пример Если требуется, чтобы рабочая нагрузка налога аудита hello только toocheck все через hello страны, может улучшить распределение данных hello выбрав hello идентификатор в качестве ключа.</span><span class="sxs-lookup"><span data-stu-id="573fc-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="573fc-124">Комплектации другой раздел или ключ распределения могут иногда hello данных более равномерно распределять, но необходимо убедиться, что этот вариант не влияет на бизнес-логики toomake.</span><span class="sxs-lookup"><span data-stu-id="573fc-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="573fc-125">Для экземпляра toocalculate сумма налога hello для каждого состояния, может потребоваться toodesignate _состояние_ в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="573fc-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="573fc-126">Если вы продолжите tooexperience эту проблему, попробуйте использовать параметр 3.</span><span class="sxs-lookup"><span data-stu-id="573fc-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="573fc-127">Вариант 3. Добавьте дополнительные ключи секции или распределения</span><span class="sxs-lookup"><span data-stu-id="573fc-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="573fc-128">Помимо использования одного _штата_ можно использовать несколько ключей для секционирования.</span><span class="sxs-lookup"><span data-stu-id="573fc-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="573fc-129">Например, рассмотрите возможность добавления _ПОЧТОВЫЙ индекс_ как дополнительный раздел секцию данных ключа tooreduce размеров и более равномерно распределять данные hello.</span><span class="sxs-lookup"><span data-stu-id="573fc-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="573fc-130">Вариант 4. Используйте распределение путем циклического перебора</span><span class="sxs-lookup"><span data-stu-id="573fc-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="573fc-131">Если не удается найти подходящего ключа для секции и распространения, можно попробовать toouse циклическое распределение.</span><span class="sxs-lookup"><span data-stu-id="573fc-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="573fc-132">При распределении путем циклического перебора все строки обрабатываются одинаково и случайным образом помещаются в соответствующий контейнер.</span><span class="sxs-lookup"><span data-stu-id="573fc-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="573fc-133">Возвращает равномерного распределения данных Hello, но он приводит к потере сведений местоположению, недостаток, который может снизить производительность работы при выполнении некоторых операций.</span><span class="sxs-lookup"><span data-stu-id="573fc-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="573fc-134">Кроме того при выполнении статистической обработки для ключа асимметричные hello все равно hello Рассогласование данных проблема не будет устранена.</span><span class="sxs-lookup"><span data-stu-id="573fc-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="573fc-135">toolearn Дополнительные сведения о циклическое распределение распределения таблицы hello U-SQL см. в разделе [CREATE TABLE (U-SQL): создание таблицы со схемой](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="573fc-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="573fc-136">Решение 2: Улучшить план запроса hello</span><span class="sxs-lookup"><span data-stu-id="573fc-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="573fc-137">Вариант 1: Использование инструкции CREATE STATISTICS hello</span><span class="sxs-lookup"><span data-stu-id="573fc-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="573fc-138">U-SQL предоставляет инструкции CREATE STATISTICS hello в таблицах.</span><span class="sxs-lookup"><span data-stu-id="573fc-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="573fc-139">Эта инструкция предоставляет дополнительные оптимизатор запросов toohello сведения о hello характеристики данных, таких как распределение значений, хранящихся в таблице.</span><span class="sxs-lookup"><span data-stu-id="573fc-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="573fc-140">Для большинства запросов оптимизатор запросов hello уже приводит к возникновению ошибки hello необходимую статистику для плана запроса высокого качества.</span><span class="sxs-lookup"><span data-stu-id="573fc-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="573fc-141">В некоторых случаях может потребоваться tooimprove производительность запросов, создав дополнительную статистику с помощью инструкции CREATE STATISTICS, либо изменив hello конструктор запросов.</span><span class="sxs-lookup"><span data-stu-id="573fc-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="573fc-142">Дополнительные сведения см. в разделе hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="573fc-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="573fc-143">Пример кода:</span><span class="sxs-lookup"><span data-stu-id="573fc-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="573fc-144">Статистика не обновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="573fc-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="573fc-145">При обновлении данных hello в таблице без повторного создания статистики hello hello производительность запросов может ухудшиться.</span><span class="sxs-lookup"><span data-stu-id="573fc-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="573fc-146">Вариант 2. Используйте SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="573fc-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="573fc-147">Если требуется toosum hello налога для каждого состояния, должны использовать GROUP BY поле "состояние" подход, который не избежать Рассогласование данных hello.</span><span class="sxs-lookup"><span data-stu-id="573fc-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="573fc-148">Тем не менее можно задать подсказку данных в вашей tooidentify запрос, который искажению данных ключи, чтобы оптимизатор hello можно подготовить план выполнения.</span><span class="sxs-lookup"><span data-stu-id="573fc-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="573fc-149">Как правило можно установить для параметра hello как 0,5 и 1, то есть не наклон интенсивной наклона и 1 значение 0,5.</span><span class="sxs-lookup"><span data-stu-id="573fc-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="573fc-150">Поскольку указание hello влияет на оптимизацию плана выполнения для текущей инструкции hello и все подчиненные инструкции, быть убедиться, что указание hello tooadd hello потенциальных неравномерным key-wise статистической обработки.</span><span class="sxs-lookup"><span data-stu-id="573fc-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="573fc-151">Пример кода:</span><span class="sxs-lookup"><span data-stu-id="573fc-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="573fc-152">Вариант 3. Использование ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="573fc-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="573fc-153">Кроме tooSKEWFACTOR для определенного неравномерным ключа соединения случаев, если известно, что hello другого набора связанных строк невелико, оптимизатор hello можно определить путем добавления Указание количества СТРОК в инструкции hello U-SQL перед ПРИСОЕДИНЕНИЕМ.</span><span class="sxs-lookup"><span data-stu-id="573fc-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="573fc-154">Таким образом, оптимизатор может выбрать, toohelp широковещательных соединения стратегия повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="573fc-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="573fc-155">Имейте в виду, что количество СТРОК не была устранена hello Рассогласование данных, но он может предложить некоторые дополнительные справочные материалы.</span><span class="sxs-lookup"><span data-stu-id="573fc-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="573fc-156">Пример кода:</span><span class="sxs-lookup"><span data-stu-id="573fc-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="573fc-157">Решение 3: Улучшить редуктора определяемых пользователем hello и функции объединения</span><span class="sxs-lookup"><span data-stu-id="573fc-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="573fc-158">Иногда можно написать определяемый пользователем оператор toodeal с логикой сложным процессом и грамотно сконструированные редуктора и функции объединения может снизить проблема Рассогласование данных в некоторых случаях.</span><span class="sxs-lookup"><span data-stu-id="573fc-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="573fc-159">Вариант 1. По возможности используйте рекурсивный редуктор</span><span class="sxs-lookup"><span data-stu-id="573fc-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="573fc-160">По умолчанию определяемый пользователем редуктор выполняется в нерекурсивном режиме, а это означает, что уменьшенный объем работы для ключа распределяется в одну вершину.</span><span class="sxs-lookup"><span data-stu-id="573fc-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="573fc-161">Но если данные искажены hello огромный наборы данных могут обрабатываться в одной вершины и запуска в течение долгого времени.</span><span class="sxs-lookup"><span data-stu-id="573fc-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="573fc-162">tooimprove производительности, можно добавить атрибут в toorun редуктора toodefine вашего кода, в режиме рекурсивной.</span><span class="sxs-lookup"><span data-stu-id="573fc-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="573fc-163">Затем hello огромный наборов данных можно распределенных toomultiple вершин и запустить параллельно, что ускоряет вашу работу.</span><span class="sxs-lookup"><span data-stu-id="573fc-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="573fc-164">toochange toorecursive редуктора нерекурсивного необходимо toomake убедитесь, что ваш алгоритм ассоциативных.</span><span class="sxs-lookup"><span data-stu-id="573fc-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="573fc-165">Например сумма hello имеет ассоциативность и МЕДИАНА hello не является.</span><span class="sxs-lookup"><span data-stu-id="573fc-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="573fc-166">Необходимо также убедиться, что hello входные и выходные данные для редуктора поддерживать hello toomake одной схеме.</span><span class="sxs-lookup"><span data-stu-id="573fc-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="573fc-167">Атрибут для рекурсивного редуктора:</span><span class="sxs-lookup"><span data-stu-id="573fc-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="573fc-168">Пример кода:</span><span class="sxs-lookup"><span data-stu-id="573fc-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="573fc-169">Вариант 2. По возможности используйте режим средства объединения на уровне строк</span><span class="sxs-lookup"><span data-stu-id="573fc-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="573fc-170">Аналогичные указания ROWCOUNT toohello для определенного соединения неравномерным ключа вариантов, режим функции объединения предпринимает наборы toomultiple toodistribute огромное значение неравномерным ключ вершин, чтобы hello работы могут быть выполнены одновременно.</span><span class="sxs-lookup"><span data-stu-id="573fc-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="573fc-171">Режим средства объединения не устранит проблему неравномерного распределения данных, но может дополнительно помочь с обработкой массивных наборов неравномерно распределенных значений ключей.</span><span class="sxs-lookup"><span data-stu-id="573fc-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="573fc-172">По умолчанию режим hello функции объединения является полной резервной копии, то есть hello слева набора строк и набор вправо строк не могут быть разделены.</span><span class="sxs-lookup"><span data-stu-id="573fc-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="573fc-173">Установка режима hello как влево или вправо/внутренний позволяет уровня строки соединения.</span><span class="sxs-lookup"><span data-stu-id="573fc-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="573fc-174">Hello система разделяет hello соответствующих наборов строк и распространяет их в несколько вершин, параллельное выполнение.</span><span class="sxs-lookup"><span data-stu-id="573fc-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="573fc-175">Тем не менее прежде чем настраивать режим функции объединения hello, будьте внимательны, что tooensure, hello соответствующие наборы строк могут быть разделены.</span><span class="sxs-lookup"><span data-stu-id="573fc-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="573fc-176">в следующем примере Hello показан набор отдельных строк слева.</span><span class="sxs-lookup"><span data-stu-id="573fc-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="573fc-177">Каждой строке вывода зависит от одной входной строки слева hello и потенциально зависит все строки из hello справа с hello же значение ключа.</span><span class="sxs-lookup"><span data-stu-id="573fc-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="573fc-178">Если устанавливается режим hello функции объединения как слева, hello система разделяет hello огромный слева-набора строк в небольших описаний и назначает им toomultiple вершин.</span><span class="sxs-lookup"><span data-stu-id="573fc-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Иллюстрация режима средства объединения](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="573fc-180">Если режим hello неправильный функции объединения hello комбинация является менее эффективным и hello результаты могут оказаться некорректными.</span><span class="sxs-lookup"><span data-stu-id="573fc-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="573fc-181">Атрибуты режима средства объединения:</span><span class="sxs-lookup"><span data-stu-id="573fc-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="573fc-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Каждая строка выходных данных зависит от одной входной строки слева hello (и потенциально все строки из hello справа с hello же значение ключа).</span><span class="sxs-lookup"><span data-stu-id="573fc-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="573fc-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): каждая строка выходных данных зависит от одной входной строки из правой hello (и потенциально все строки из левой hello с hello же значение ключа).</span><span class="sxs-lookup"><span data-stu-id="573fc-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="573fc-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Каждая строка выходных данных зависит от одной входной строки из слева hello и hello справа с hello же значение.</span><span class="sxs-lookup"><span data-stu-id="573fc-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="573fc-185">Пример кода:</span><span class="sxs-lookup"><span data-stu-id="573fc-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
