---
title: "aaaFind данных с помощью поиска журналов в службе анализа журналов Azure | Документы Microsoft"
description: "Поиск по журналам позволяют toocombine и сопоставлять данные компьютеров из нескольких источников в существующей среде."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="1560e-103">Поиск данных по журналам в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1560e-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="1560e-104">В этой статье описывается использование hello текущий язык запроса в службе анализа журналов запросов поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="1560e-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="1560e-105">Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то вы должны обращаться слишком[основные сведения о журнале ищет в службе анализа журналов (новый)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="1560e-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="1560e-106">В основе hello аналитики журналов является функция поиска журналов hello, позволяющий toocombine и сопоставлять данные компьютеров из нескольких источников в существующей среде.</span><span class="sxs-lookup"><span data-stu-id="1560e-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="1560e-107">Решения также берутся из журнала поиска toobring сведенных вы показатели по определенной проблемной области.</span><span class="sxs-lookup"><span data-stu-id="1560e-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="1560e-108">На странице поиска hello можно создать запрос и затем при поиске, можно фильтровать результаты hello с помощью элементов управления аспектами.</span><span class="sxs-lookup"><span data-stu-id="1560e-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="1560e-109">Также можно создать сложные запросы tootransform, фильтрации и отчетов результатов.</span><span class="sxs-lookup"><span data-stu-id="1560e-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="1560e-110">Общие запросы поиска журналов отображаются на большинстве страниц решений.</span><span class="sxs-lookup"><span data-stu-id="1560e-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="1560e-111">В консоли hello OMS можно щелкать плитки или детализировать элементы tooother tooview сведения об элементе hello с помощью функции поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="1560e-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="1560e-112">В этом учебнике мы рассмотрим примеры toocover все основы hello при использовании поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="1560e-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="1560e-113">Мы начинаться с простых практических примеров и затем разовьем их, чтобы получить представление о способе toouse hello синтаксис tooextract hello аналитики из данных hello реальных вариантах.</span><span class="sxs-lookup"><span data-stu-id="1560e-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="1560e-114">После ознакомления с методиками поиска можно просмотреть hello [Справочник поиска журнала анализа журналов](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1560e-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="1560e-115">использование базовых фильтров;</span><span class="sxs-lookup"><span data-stu-id="1560e-115">Use basic filters</span></span>
<span data-ttu-id="1560e-116">Hello первое, что tooknow — что hello первая часть запрос поиска перед любым» | «символ вертикальной черты, всегда *фильтра*.</span><span class="sxs-lookup"><span data-stu-id="1560e-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="1560e-117">Его можно рассматривать как предложение WHERE в TSQL, он определяет *что* подмножество toopull данные из хранилища данных OMS hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="1560e-118">Поиск в хранилище данных hello главным образом заключается указания характеристики hello hello данных необходимо tooextract, поэтому логично, что запрос будет начинаться с предложения WHERE hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="1560e-119">Hello самый простой из доступных фильтров являются *ключевые слова*, такие как «ошибка», «время ожидания» или имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="1560e-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="1560e-120">Эти типы простых запросов обычно возвращают различные формы данных в рамках hello же результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="1560e-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="1560e-121">Так как служба аналитики журналов содержит различные *типы* данных в системе hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="1560e-122">tooconduct простого поиска</span><span class="sxs-lookup"><span data-stu-id="1560e-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="1560e-123">На портале OMS hello щелкните **поиска журналов**.</span><span class="sxs-lookup"><span data-stu-id="1560e-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="1560e-124">![плитка поиска](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="1560e-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="1560e-125">Введите в поле запроса hello `error` и нажмите кнопку **поиска**.</span><span class="sxs-lookup"><span data-stu-id="1560e-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="1560e-126">![ошибка поиска](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="1560e-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="1560e-127">Например, запрос hello для `error` hello следующем рисунке возвратил 100 000 **событий** записей (собранных функцией управления журналами), 18 **ConfigurationAlert** записей (созданных в ходе настройки Оценка) и 12 **ConfigurationChange** записей (полученных функцией отслеживания изменений hello).</span><span class="sxs-lookup"><span data-stu-id="1560e-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="1560e-128">![результаты поиска](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="1560e-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="1560e-129">Эти фильтры на самом деле не являются классами и типами объектов.</span><span class="sxs-lookup"><span data-stu-id="1560e-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="1560e-130">*Тип* просто тег, или свойство или строка/имя/категория, присоединенные tooa части данных.</span><span class="sxs-lookup"><span data-stu-id="1560e-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="1560e-131">Некоторые документы в системе hello помечены как **Type: ConfigurationAlert** и другие помечены как **типа: производительности**, или **Type: Event**, и т. д.</span><span class="sxs-lookup"><span data-stu-id="1560e-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="1560e-132">Каждый результат поиска, документ, записи или запись отображает все общие свойства hello и их значения для каждого из этих фрагментов данных, а также можно использовать эти toospecify имена полей в фильтре hello при необходимости tooretrieve только записи hello где hello поле имеет заданное значение.</span><span class="sxs-lookup"><span data-stu-id="1560e-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="1560e-133">*Type* — это просто поле, которое имеет все записи, оно ничем не отличается от любого другого поля.</span><span class="sxs-lookup"><span data-stu-id="1560e-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="1560e-134">Это было установлено на основе значения hello поля типа hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="1560e-135">Эта запись будет иметь другую форму.</span><span class="sxs-lookup"><span data-stu-id="1560e-135">That record will have a different shape or form.</span></span> <span data-ttu-id="1560e-136">Кстати **тип = Perf**, или **тип события =** также является hello синтаксиса, что toolearn tooquery событий или данных о производительности.</span><span class="sxs-lookup"><span data-stu-id="1560e-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="1560e-137">Двоеточие (:) или знак равенства (=) можно использовать после имени поля hello и перед значением hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="1560e-138">**Type: Event** и **тип события =** являются одинаковое значение, можно выбрать hello стиль, который вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="1560e-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="1560e-139">Поэтому, если hello введите = Perf записи имеют поле с именем «CounterName», а затем можно написать запрос наподобие `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="1560e-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="1560e-140">Это позволит получить только данные о производительности hello где hello счетчик производительности имеет имя «% Processor Time».</span><span class="sxs-lookup"><span data-stu-id="1560e-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="1560e-141">toosearch для данных производительности по загруженности процессора</span><span class="sxs-lookup"><span data-stu-id="1560e-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="1560e-142">Введите в поле запроса поиска hello`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="1560e-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="1560e-143">Можно также указать значение более точно и использовать **InstanceName = _ 'Total'** в запросе hello, который представляет собой счетчик производительности Windows.</span><span class="sxs-lookup"><span data-stu-id="1560e-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="1560e-144">Можно также выбрать другой аспект и другую пару **поле:значение**.</span><span class="sxs-lookup"><span data-stu-id="1560e-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="1560e-145">Hello фильтр автоматически добавляется tooyour фильтра панели запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="1560e-146">Это можно увидеть в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="1560e-146">You can see this in hello following image.</span></span> <span data-ttu-id="1560e-147">Показано, где tooclick tooadd **InstanceName: '_Total'** toohello запроса, не вводя никакого текста.</span><span class="sxs-lookup"><span data-stu-id="1560e-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![аспект поиска](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="1560e-149">Ваш запрос превращается в `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="1560e-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="1560e-150">В этом примере нет toospecify **тип = Perf** tooget toothis результат.</span><span class="sxs-lookup"><span data-stu-id="1560e-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="1560e-151">Так как hello поля CounterName и InstanceName существуют только для записей Type = Perf hello запроса является достаточно точным, tooreturn hello такие же результаты, как hello и предыдущий более длинный:</span><span class="sxs-lookup"><span data-stu-id="1560e-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="1560e-152">Это, поскольку все фильтры hello в запросе hello вычисляются как если бы *AND* друг с другом.</span><span class="sxs-lookup"><span data-stu-id="1560e-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="1560e-153">По сути, hello дополнительные поля, добавить критерии toohello, вы получаете менее точные и детальные результаты.</span><span class="sxs-lookup"><span data-stu-id="1560e-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="1560e-154">Например, запрос hello `Type=Event EventLog="Windows PowerShell"` идентичен слишком`Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="1560e-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="1560e-155">Он возвращает все события, которые были зарегистрированы и собраны из журнала событий Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="1560e-156">Если вы добавляете фильтр несколько раз, выбрав приветствия же аспект, затем hello проблема является совершенно формальной — он может загромождать панель поиска hello, но она по-прежнему возвращает hello же результаты, так как hello неявный оператор и всегда присутствует несколько раз.</span><span class="sxs-lookup"><span data-stu-id="1560e-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="1560e-157">Вы можете легко обратить неявный оператор и hello с помощью явного оператора NOT.</span><span class="sxs-lookup"><span data-stu-id="1560e-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="1560e-158">Например:</span><span class="sxs-lookup"><span data-stu-id="1560e-158">For example:</span></span>

<span data-ttu-id="1560e-159">`Type:Event NOT(EventLog:"Windows PowerShell")`или его эквивалент `Type=Event EventLog!="Windows PowerShell"` возвращают все события из всех журналов, которые не являются журналами Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="1560e-160">Либо можно использовать другой логический оператор, такой как ИЛИ (OR).</span><span class="sxs-lookup"><span data-stu-id="1560e-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="1560e-161">Hello следующий запрос возвращает записи, для которых hello EventLog имеет значение Application или System.</span><span class="sxs-lookup"><span data-stu-id="1560e-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="1560e-162">С помощью hello выше запрос, вы получаете записи для обоих журналов в hello же результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="1560e-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="1560e-163">Однако при удалении hello или, оставив неявный hello и на месте, то hello следующий запрос не даст никаких результатов, так как запись журнала событий, к которому относится tooBOTH журналы, не существует.</span><span class="sxs-lookup"><span data-stu-id="1560e-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="1560e-164">Каждая запись журнала событий была записана tooonly один из двух журналов hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="1560e-165">использование дополнительных фильтров;</span><span class="sxs-lookup"><span data-stu-id="1560e-165">Use additional filters</span></span>
<span data-ttu-id="1560e-166">Hello следующий запрос возвращает записи для 2 журналов событий для всех компьютеров hello, которые отправляли данные.</span><span class="sxs-lookup"><span data-stu-id="1560e-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![результаты поиска](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="1560e-168">При выборе одного из полей hello или фильтры, можно провести hello запроса tooa конкретного компьютера, исключив все остальные.</span><span class="sxs-lookup"><span data-stu-id="1560e-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="1560e-169">Hello результирующий запрос будет выглядеть следующим образом следующие hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="1560e-170">Это следующие эквивалентные toohello из-за hello неявного оператора и.</span><span class="sxs-lookup"><span data-stu-id="1560e-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="1560e-171">Каждый запрос вычисляется в явной последовательностью hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="1560e-172">Примечание hello скобки.</span><span class="sxs-lookup"><span data-stu-id="1560e-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="1560e-173">Так же, как hello полем журнала событий, можно извлечь данные только для набора определенных компьютеров путем добавления или.</span><span class="sxs-lookup"><span data-stu-id="1560e-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="1560e-174">Например:</span><span class="sxs-lookup"><span data-stu-id="1560e-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="1560e-175">Аналогичным образом, этот hello следующих запроса возвращают **% времени ЦП** hello выбранного только двух компьютеров.</span><span class="sxs-lookup"><span data-stu-id="1560e-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="1560e-176">Типы полей</span><span class="sxs-lookup"><span data-stu-id="1560e-176">Field types</span></span>
<span data-ttu-id="1560e-177">При создании фильтров, следует учитывать hello различия в работе с различными типами полей, возвращаемых из запросов поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="1560e-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="1560e-178">**Поля, доступные для поиска,** выделены синим цветом в результатах.</span><span class="sxs-lookup"><span data-stu-id="1560e-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="1560e-179">Можно использовать для поиска полей в поля конкретного toohello условия поиска, например hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1560e-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="1560e-180">**Поля с возможностью поиска произвольного текста** выделены серым цветом в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="1560e-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="1560e-181">Они не может использоваться с поле toohello конкретных условий поиска, как поля поиска.</span><span class="sxs-lookup"><span data-stu-id="1560e-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="1560e-182">Осуществляется только при выполнении запроса для всех полей, например следующих hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="1560e-183">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="1560e-183">Boolean operators</span></span>
<span data-ttu-id="1560e-184">С помощью полей даты и времени и числовых полей можно выполнить поиск значений с помощью операторов *больше*, *меньше* и *меньше или равно*.</span><span class="sxs-lookup"><span data-stu-id="1560e-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="1560e-185">Можно использовать простые операторы, такие как >, <>, =, < =,! = в строке поиска hello запроса.</span><span class="sxs-lookup"><span data-stu-id="1560e-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="1560e-186">Можно запросить журнал событий за конкретный период времени.</span><span class="sxs-lookup"><span data-stu-id="1560e-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="1560e-187">Например hello последние 24 часа выражается с hello следующее мнемоническое выражение.</span><span class="sxs-lookup"><span data-stu-id="1560e-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="1560e-188">с помощью логического оператора toosearch</span><span class="sxs-lookup"><span data-stu-id="1560e-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="1560e-189">Введите в поле запроса поиска hello`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="1560e-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="1560e-190">![поиск с логическими операторами](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="1560e-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="1560e-191">Несмотря на то, что можно управлять графически hello интервал времени, а большая часть времени может потребоваться toodo, что существуют преимущества tooincluding фильтра времени непосредственно в запрос hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="1560e-192">Например, это прекрасно работает с панелями мониторинга, где можно переопределить время hello для каждой плитки независимо от hello *глобальной* селектора времени на странице панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="1560e-193">Дополнительные сведения см. в статье [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/) (Аспекты использования времени на панели мониторинга).</span><span class="sxs-lookup"><span data-stu-id="1560e-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="1560e-194">При фильтрации по времени, имейте в виду, что можно получить результаты для hello *пересечение* из hello двух периодов: hello, указанному в hello портал OMS (S1) и Здравствуйте, указанному в запросе hello (S2).</span><span class="sxs-lookup"><span data-stu-id="1560e-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![пересечению](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="1560e-196">Это означает, что если hello периоды не пересекаются, например на портале OMS hello, где выбрано **на этой неделе** и в запросе hello, где определена **прошлой неделе**, то нет пересечение отсутствует, и вы не Получите никаких результатов.</span><span class="sxs-lookup"><span data-stu-id="1560e-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="1560e-197">Операторы сравнения, используемые для поля TimeGenerated hello можно также в других ситуациях.</span><span class="sxs-lookup"><span data-stu-id="1560e-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="1560e-198">Например, для числовых полей.</span><span class="sxs-lookup"><span data-stu-id="1560e-198">For example, with numeric fields.</span></span>

<span data-ttu-id="1560e-199">К примеру Предположим, что оповещения оценки конфигурации имеют следующие уровни серьезности hello:</span><span class="sxs-lookup"><span data-stu-id="1560e-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="1560e-200">0 = информационный</span><span class="sxs-lookup"><span data-stu-id="1560e-200">0 = Information</span></span>
* <span data-ttu-id="1560e-201">1 = предупреждение</span><span class="sxs-lookup"><span data-stu-id="1560e-201">1 = Warning</span></span>
* <span data-ttu-id="1560e-202">2 = критический</span><span class="sxs-lookup"><span data-stu-id="1560e-202">2 = Critical</span></span>

<span data-ttu-id="1560e-203">Можно запросить предупреждения и критические оповещения, а также исключить информационные оповещения с приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="1560e-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="1560e-204">Можно также использовать запросы в диапазоне.</span><span class="sxs-lookup"><span data-stu-id="1560e-204">You can also use range queries.</span></span> <span data-ttu-id="1560e-205">Это означает, что может предоставить hello начало и конец диапазона значений в последовательности.</span><span class="sxs-lookup"><span data-stu-id="1560e-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="1560e-206">Например, если события из журнала событий Operations Manager hello там, где hello EventID — больше или равно too2100, но не больше 2199, а затем приветствия при следующем запросе позволит получить их.</span><span class="sxs-lookup"><span data-stu-id="1560e-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="1560e-207">необходимо использовать синтаксис диапазона Hello — hello двоеточие (:): значение поля и *не* hello знак равенства (=).</span><span class="sxs-lookup"><span data-stu-id="1560e-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="1560e-208">Заключите hello нижнюю и верхнюю границу диапазона hello в квадратные скобки, разделив их двумя точками (..).</span><span class="sxs-lookup"><span data-stu-id="1560e-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="1560e-209">работа с результатами поиска;</span><span class="sxs-lookup"><span data-stu-id="1560e-209">Manipulate search results</span></span>
<span data-ttu-id="1560e-210">При поиске данных вам требуется toorefine запрос поиска и наличие высокого уровня контроля над hello результаты.</span><span class="sxs-lookup"><span data-stu-id="1560e-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="1560e-211">При извлечении результатов можно применять команды tootransform их.</span><span class="sxs-lookup"><span data-stu-id="1560e-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="1560e-212">Команды в поиске анализа журналов *должен* следовать после символа hello вертикальной черты (|).</span><span class="sxs-lookup"><span data-stu-id="1560e-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="1560e-213">Фильтр должен всегда быть hello первой части строки запроса.</span><span class="sxs-lookup"><span data-stu-id="1560e-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="1560e-214">Он определяет набор данных hello, с которыми работает, а затем» направляет эти результаты в команду.</span><span class="sxs-lookup"><span data-stu-id="1560e-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="1560e-215">Затем можно использовать дополнительные команды hello канала tooadd.</span><span class="sxs-lookup"><span data-stu-id="1560e-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="1560e-216">Это приблизительно конвейера toohello Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1560e-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="1560e-217">В общем случае язык поиска аналитики журналов hello пытается toomake стилю и правилам PowerShell toofollow ИТ аналогичные toohello ИТ-специалисты и tooease hello обучения.</span><span class="sxs-lookup"><span data-stu-id="1560e-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="1560e-218">Команды имеют форму глаголов, чтобы можно было легко понять, что именно они делают.</span><span class="sxs-lookup"><span data-stu-id="1560e-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="1560e-219">Сортировать</span><span class="sxs-lookup"><span data-stu-id="1560e-219">Sort</span></span>
<span data-ttu-id="1560e-220">Команда sort Hello позволяет hello toodefine сортировку по одному или нескольким полям.</span><span class="sxs-lookup"><span data-stu-id="1560e-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="1560e-221">Даже если вы не используете ее, по умолчанию применяется сортировка по времени в порядке убывания.</span><span class="sxs-lookup"><span data-stu-id="1560e-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="1560e-222">Hello самые новые результаты всегда находятся в hello верхней части результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="1560e-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="1560e-223">Это означает, что при выполнении поиска с учетом `Type=Event EventID=1234` реально выполняется следующее:</span><span class="sxs-lookup"><span data-stu-id="1560e-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="1560e-224">Это, так как он является типом hello возможности, знакомые с в журналах.</span><span class="sxs-lookup"><span data-stu-id="1560e-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="1560e-225">Например в hello в окне просмотра событий Windows.</span><span class="sxs-lookup"><span data-stu-id="1560e-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="1560e-226">Можно использовать результаты toochange hello способ сортировки.</span><span class="sxs-lookup"><span data-stu-id="1560e-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="1560e-227">Hello следующих примерах показано, как это работает.</span><span class="sxs-lookup"><span data-stu-id="1560e-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="1560e-228">Hello простые примеры выше показывают работу команды: они изменяют форму hello hello результатов, фильтр вернул hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="1560e-229">Limit и top</span><span class="sxs-lookup"><span data-stu-id="1560e-229">Limit and top</span></span>
<span data-ttu-id="1560e-230">Другой менее известной командой является LIMIT.</span><span class="sxs-lookup"><span data-stu-id="1560e-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="1560e-231">Эта команда похожа на команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1560e-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="1560e-232">Предел — идентичных по функциональности toohello команде TOP.</span><span class="sxs-lookup"><span data-stu-id="1560e-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="1560e-233">Hello следующие запросы возвращают hello одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="1560e-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="1560e-234">toosearch с помощью предложения top</span><span class="sxs-lookup"><span data-stu-id="1560e-234">toosearch using top</span></span>
* <span data-ttu-id="1560e-235">Введите в поле запроса поиска hello`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="1560e-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="1560e-236">![поиск лучших результатов](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="1560e-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="1560e-237">Hello рисунке выше, 358 тысяч записей с EventID = 600.</span><span class="sxs-lookup"><span data-stu-id="1560e-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="1560e-238">Здравствуйте, поля, аспекты и фильтры для hello слева всегда отображаются сведения о hello результаты, возвращаемые *частью фильтра hello* запросе hello, которая входит в состав hello до знака вертикальной черты.</span><span class="sxs-lookup"><span data-stu-id="1560e-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="1560e-239">Hello **результатов** возвращает только самые последние 1 hello результат, так как команда в примере hello форму результатов и преобразовала hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="1560e-240">Выберите пункт</span><span class="sxs-lookup"><span data-stu-id="1560e-240">Select</span></span>
<span data-ttu-id="1560e-241">Hello команда SELECT похожа на команду Select-Object в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1560e-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="1560e-242">Она возвращает отфильтрованные результаты, имеющие не все свои первоначальные свойства.</span><span class="sxs-lookup"><span data-stu-id="1560e-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="1560e-243">Вместо этого она выбирает только hello вами свойства.</span><span class="sxs-lookup"><span data-stu-id="1560e-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="1560e-244">toorun поиска с использованием команды select hello</span><span class="sxs-lookup"><span data-stu-id="1560e-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="1560e-245">В поле поиска введите `Type=Event` и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="1560e-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="1560e-246">Нажмите кнопку **+ Дополнительно** в одном tooview результаты hello, имеют все свойства hello, hello результаты.</span><span class="sxs-lookup"><span data-stu-id="1560e-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="1560e-247">Выберите некоторые из них явным образом и hello изменения запроса слишком`Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="1560e-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="1560e-248">![поиск с помощью select](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="1560e-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="1560e-249">Эта команда особенно полезен, если необходимо toocontrol выходными данными поиска и отбирать только hello фрагменты данных, которые важны для проводимого исследования, а не полный спектр записей hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="1560e-250">Это также полезно, когда записи различных типов имеют *несколько* общих свойств, но не *все* их свойства являются общими.</span><span class="sxs-lookup"><span data-stu-id="1560e-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="1560e-251">, Можно сформировать выходные данные, более естественным образом выглядит как таблицу или удобны для экспорта tooa CSV-файл и последующей обработки в Excel.</span><span class="sxs-lookup"><span data-stu-id="1560e-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="1560e-252">Использование команды measure hello</span><span class="sxs-lookup"><span data-stu-id="1560e-252">Use hello measure command</span></span>
<span data-ttu-id="1560e-253">MEASURE является одной из hello наиболее универсальных команд в поиске анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="1560e-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="1560e-254">Оно позволяет tooapply статистические *функции* tooyour данным и агрегировать результаты, сгруппированные по заданному полю.</span><span class="sxs-lookup"><span data-stu-id="1560e-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="1560e-255">Существует несколько статистических функций, поддерживаемых командой Measure.</span><span class="sxs-lookup"><span data-stu-id="1560e-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="1560e-256">Measure count()</span><span class="sxs-lookup"><span data-stu-id="1560e-256">Measure count()</span></span>
<span data-ttu-id="1560e-257">Hello первой статистической функцией toowork с, и один из простой toounderstand hello hello *count()* функции.</span><span class="sxs-lookup"><span data-stu-id="1560e-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="1560e-258">Результатов любого поискового запроса, например `Type=Event`, отображаются фильтры, которые также называются аспектами на hello левая сторона результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="1560e-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="1560e-259">Hello фильтры показывают распределение значений по заданному полю для hello результатов выполненного поиска hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![поиск с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="1560e-261">Например, в hello изображения выше вы увидите hello **компьютера** поле и он показывает, что в пределах hello почти 739 тысячи событий в результатах hello 68 уникальных значений для hello **компьютер** поле в этих записях.</span><span class="sxs-lookup"><span data-stu-id="1560e-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="1560e-262">Hello плитке отображаются только hello пяти, hello наиболее распространенные значений, которые записаны в hello **компьютера** полей), с сортировкой по hello количество документов, содержащих это конкретное значение в этом поле.</span><span class="sxs-lookup"><span data-stu-id="1560e-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="1560e-263">В образ hello, вы увидите, что среди почти 369 тысячи событий 90 тысяч поступают с компьютера OpsInsights04.contoso.com hello, 83 тысячи — с компьютера DB03.contoso.com hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="1560e-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="1560e-264">Что делать, если требуется toosee всех значений, поскольку hello плитке отображаются только только hello пяти?</span><span class="sxs-lookup"><span data-stu-id="1560e-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="1560e-265">Вот какие меры hello команды можно сделать с помощью функции count() hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="1560e-266">Эта функция не использует никаких параметров.</span><span class="sxs-lookup"><span data-stu-id="1560e-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="1560e-267">Просто укажите поле hello, по которому требуется toogroup, — hello **компьютера** в данном случае:</span><span class="sxs-lookup"><span data-stu-id="1560e-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![поиск с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="1560e-269">Однако **Computer** — это просто поле, используемое *в* каждом фрагменте данных. Нет никаких реляционных баз данных и никакого отдельного объекта **Computer**.</span><span class="sxs-lookup"><span data-stu-id="1560e-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="1560e-270">Просто hello значения *в* hello данных могут описывать, какая сущность создала их, а также ряд других характеристик и аспектов данных hello, поэтому hello термин *аспекта*.</span><span class="sxs-lookup"><span data-stu-id="1560e-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="1560e-271">Однако вы точно так же можете выполнять группировку по другим полям.</span><span class="sxs-lookup"><span data-stu-id="1560e-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="1560e-272">Поскольку исходные результаты почти 739 тысячи событий, которые передаются в команду measure hello hello, также имеют поле с именем **EventID**, можно применить hello же методика toogroup по этому полю и получить количество событий по EventID:</span><span class="sxs-lookup"><span data-stu-id="1560e-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="1560e-273">Если вас не интересует hello реальное число записей, содержащих определенное значение, но вместо этого требуется только список hello значения самостоятельно, можно добавить *выберите* команду в конце hello и просто выберите hello первый столбец:</span><span class="sxs-lookup"><span data-stu-id="1560e-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="1560e-274">Затем можно усложнить и предварительно отсортировать результаты hello в запросе hello, или можно просто щелкнуть столбцы hello в сетке hello слишком.</span><span class="sxs-lookup"><span data-stu-id="1560e-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="1560e-275">toosearch с использованием measure count</span><span class="sxs-lookup"><span data-stu-id="1560e-275">toosearch using measure count</span></span>
* <span data-ttu-id="1560e-276">Введите в поле запроса поиска hello`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="1560e-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="1560e-277">Добавление `| Select EventID` toohello конец запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="1560e-278">Наконец, добавьте `| Sort EventID asc` toohello конец запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="1560e-279">Существует несколько важных моментов toonotice внимание:</span><span class="sxs-lookup"><span data-stu-id="1560e-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="1560e-280">Во-первых, отображаемые результаты hello не являются исходными необработанными результатами hello больше.</span><span class="sxs-lookup"><span data-stu-id="1560e-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="1560e-281">Вместо этого они являются агрегированными результатами, то есть группами результатов.</span><span class="sxs-lookup"><span data-stu-id="1560e-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="1560e-282">Это не проблема, однако следует понимать, что взаимодействие осуществляется с очень иной формой данных, которая отличается от hello исходной необработанной формы, который создается на лету hello в результате статистической обработки или применения статистической функции hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="1560e-283">Во-вторых, **мер числа** в настоящее время возвращает только hello первых 100 различных результатов.</span><span class="sxs-lookup"><span data-stu-id="1560e-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="1560e-284">Это ограничение не применяется toohello другим статистическим функциям.</span><span class="sxs-lookup"><span data-stu-id="1560e-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="1560e-285">Таким образом обычно необходимо toouse точнее toosearch первый фильтр для определенных элементов, перед применением measure count().</span><span class="sxs-lookup"><span data-stu-id="1560e-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="1560e-286">Использование функций hello max и min с командой measure hello</span><span class="sxs-lookup"><span data-stu-id="1560e-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="1560e-287">Существуют различные сценарии, где использование **Measure Max()** и **Measure Min()** имеет смысл.</span><span class="sxs-lookup"><span data-stu-id="1560e-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="1560e-288">Однако поскольку каждая функция является противоположностью другой, мы опишем Max(), а с Min() вы сможете поэкспериментировать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="1560e-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="1560e-289">При запросе событий системы безопасности они имеют свойство **Level**, которое может изменяться.</span><span class="sxs-lookup"><span data-stu-id="1560e-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="1560e-290">Например:</span><span class="sxs-lookup"><span data-stu-id="1560e-290">For example:</span></span>

```
Type=SecurityEvent
```

![начало поиска с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="1560e-292">Если требуется tooview hello наибольшее значение для всех безопасности hello события назначено общее поле Computer, hello группировкой по полю, можно использовать</span><span class="sxs-lookup"><span data-stu-id="1560e-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![поиск с помощью measure max по computer](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="1560e-294">Он покажет, hello компьютеров с **уровень** записи, большинство из них имеют по крайней мере 8, на уровне многих уровень 16.</span><span class="sxs-lookup"><span data-stu-id="1560e-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![поиск с помощью measure max для времени создания по computer](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="1560e-296">Эта функция хорошо работает с числами, однако она также работает с полями типа DateTime.</span><span class="sxs-lookup"><span data-stu-id="1560e-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="1560e-297">Это полезно toocheck для hello последней или наиболее поздним штампом времени для любого фрагмента данных, индексируемых для каждого компьютера.</span><span class="sxs-lookup"><span data-stu-id="1560e-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="1560e-298">Например: Если hello последнего события безопасности сообщалось для каждого компьютера?</span><span class="sxs-lookup"><span data-stu-id="1560e-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="1560e-299">Использование функции avg hello с командой measure hello</span><span class="sxs-lookup"><span data-stu-id="1560e-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="1560e-300">Hello статистическая функция Avg(), используемая с командой measure можно toocalculate hello среднее значение для некоторого поля, а результаты группируются по hello того же или другому полю.</span><span class="sxs-lookup"><span data-stu-id="1560e-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="1560e-301">Это оказывается полезным в самых различных случаях, например в случае с данными о производительности.</span><span class="sxs-lookup"><span data-stu-id="1560e-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="1560e-302">Мы начнем с данных о производительности.</span><span class="sxs-lookup"><span data-stu-id="1560e-302">We'll start with performance data.</span></span> <span data-ttu-id="1560e-303">Обратите внимание, что OMS в настоящее время собирает счетчики производительности для машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="1560e-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="1560e-304">toosearch для *все* — самый простой запрос hello данных о производительности:</span><span class="sxs-lookup"><span data-stu-id="1560e-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![начало поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="1560e-306">Hello первое, что вы заметите, — что анализа журналов показано три перспективы: список, в котором отображается которой показаны фактические записи hello за hello диаграмм; Таблица, которая показывает табличное представление данных счетчиков производительности; и метрик, которые отображаются графики для hello счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="1560e-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="1560e-307">В выше рисунке hello существует два набора поля, помеченные, указывающие hello следующее:</span><span class="sxs-lookup"><span data-stu-id="1560e-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="1560e-308">Hello первый набор определяет имя счетчика производительности Windows, имя объекта и имя экземпляра в фильтре запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="1560e-309">Это hello поля, которые, вероятно, наиболее часто используется в качестве аспектов и фильтров</span><span class="sxs-lookup"><span data-stu-id="1560e-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="1560e-310">**Значения counterValue** — hello фактическое значение счетчика "hello".</span><span class="sxs-lookup"><span data-stu-id="1560e-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="1560e-311">В этом примере значение hello — *75*.</span><span class="sxs-lookup"><span data-stu-id="1560e-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="1560e-312">**TimeGenerated** имеет значение 12:51 в 24-часовом формате.</span><span class="sxs-lookup"><span data-stu-id="1560e-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="1560e-313">Здесь показано представление hello метрик на графике.</span><span class="sxs-lookup"><span data-stu-id="1560e-313">Here's a view of hello metrics in a graph.</span></span>

![начало поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="1560e-315">После чтения сведений о записи фигуры hello производительности и ознакомления другими методиками поиска можно использовать measure Avg() tooaggregate этот тип числовых данных.</span><span class="sxs-lookup"><span data-stu-id="1560e-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="1560e-316">Ниже приведен простой пример.</span><span class="sxs-lookup"><span data-stu-id="1560e-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![поиска с помощью avg по samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="1560e-318">В этом примере выберите счетчик производительности hello общее время ЦП и среднее по компьютерам.</span><span class="sxs-lookup"><span data-stu-id="1560e-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="1560e-319">Если вы хотите toonarrow работу вашей hello tooonly результаты последние 6 часов, можно использовать элемент управления фильтром времени hello или укажите в запросе следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1560e-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="1560e-320">Использование функции avg hello с командой measure hello toosearch</span><span class="sxs-lookup"><span data-stu-id="1560e-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="1560e-321">Введите в поле запроса поиска hello `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="1560e-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="1560e-322">Можно объединять и сопоставлять данные *по* разным компьютерам.</span><span class="sxs-lookup"><span data-stu-id="1560e-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="1560e-323">Например предположим, что имеется набор узлов в некоторой ферме, где каждый узел является равно tooany других и заполним требуется грубая Балансировка одного типа рабочих и загрузка всех приветствия.</span><span class="sxs-lookup"><span data-stu-id="1560e-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="1560e-324">Можно получить собрать счетчики за один проход с hello ниже запрос и получить средние значения для всей фермы hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="1560e-325">Для начала можно выбрать компьютеры hello с hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1560e-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="1560e-326">Теперь, когда у вас есть компьютеры hello, также требуется только tooselect две ключевые показатели эффективности (KPI): % ЦП и % свободного места на диске.</span><span class="sxs-lookup"><span data-stu-id="1560e-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="1560e-327">Таким образом эту часть запроса hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1560e-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="1560e-328">Теперь можно добавить компьютеры и счетчики с hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1560e-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="1560e-329">Здравствуйте, так как у вас есть выбору конкретных элементов, **измерения Avg()** позволяет возвратить среднее значение hello не для компьютера, а для всей фермы hello путем группирования по CounterName.</span><span class="sxs-lookup"><span data-stu-id="1560e-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="1560e-330">Например:</span><span class="sxs-lookup"><span data-stu-id="1560e-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="1560e-331">Это позволяет получить удобное компактное представление с парой ключевых показателей эффективности вашей среды.</span><span class="sxs-lookup"><span data-stu-id="1560e-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![группировка поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="1560e-333">Можно легко использовать запрос поиска hello в панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="1560e-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="1560e-334">Например, можно сохранить запрос поиска hello и создания панели мониторинга из него с именем *ключевые показатели эффективности фермы Web*.</span><span class="sxs-lookup"><span data-stu-id="1560e-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="1560e-335">toolearn Дополнительные сведения об использовании панелей мониторинга, в разделе [создания настраиваемой панели мониторинга в службе анализа журналов](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="1560e-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![панель мониторинга поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="1560e-337">Использование функции hello sum с командой measure hello</span><span class="sxs-lookup"><span data-stu-id="1560e-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="1560e-338">функция sum Hello — функции, подобные tooother hello мер команды.</span><span class="sxs-lookup"><span data-stu-id="1560e-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="1560e-339">Вы увидите пример как toouse hello функции sum с [поиск журналов IIS W3C в Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="1560e-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="1560e-340">Функции Max() и Min() можно использовать с числами, датой и временем, а также с текстовыми строками.</span><span class="sxs-lookup"><span data-stu-id="1560e-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="1560e-341">Текстовые строки сортируются в алфавитном порядке, и вы получаете первую и последнюю сроку.</span><span class="sxs-lookup"><span data-stu-id="1560e-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="1560e-342">Однако функцию Sum() можно использовать только с числовыми полями.</span><span class="sxs-lookup"><span data-stu-id="1560e-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="1560e-343">Это также применимо tooAvg().</span><span class="sxs-lookup"><span data-stu-id="1560e-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="1560e-344">Использование функции процентиля hello с командой measure hello</span><span class="sxs-lookup"><span data-stu-id="1560e-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="1560e-345">функция вычисления процентиля Hello является аналогичные tooAvg() и Sum(), его можно использовать только для числовых полей.</span><span class="sxs-lookup"><span data-stu-id="1560e-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="1560e-346">Можно использовать любой процентиля между 1 too99 на числовое поле.</span><span class="sxs-lookup"><span data-stu-id="1560e-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="1560e-347">Можно использовать оба варианта команды: **percentile** и **pct**.</span><span class="sxs-lookup"><span data-stu-id="1560e-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="1560e-348">Рассмотрим несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="1560e-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="1560e-349">Использовать hello, где команды</span><span class="sxs-lookup"><span data-stu-id="1560e-349">Use hello where command</span></span>
<span data-ttu-id="1560e-350">Hello команда работает как фильтр, когда он может быть применен фильтр toofurther конвейера hello статистическая обработка результатов, полученных с помощью команды Measure как противоположность tooraw результатов, которые фильтруются в начале hello запроса.</span><span class="sxs-lookup"><span data-stu-id="1560e-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="1560e-351">Например:</span><span class="sxs-lookup"><span data-stu-id="1560e-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="1560e-352">Можно добавить другой канал» | «символьных и hello, где tooonly команды получить которых средняя загрузка ЦП превышает 80%, с компьютеров hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1560e-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="1560e-353">Если вы знакомы с Microsoft System Center Operations Manager, контролирующий hello там, где в терминах пакета управления.</span><span class="sxs-lookup"><span data-stu-id="1560e-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="1560e-354">Если пример hello правило, первая часть запроса hello hello будет hello источника данных и hello где команда будет выглядеть определение условия hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="1560e-355">Hello запрос можно использовать в качестве плитки в **Моя панель мониторинга**, как отслеживать, toosee при чрезмерную загрузку ЦП компьютера.</span><span class="sxs-lookup"><span data-stu-id="1560e-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="1560e-356">toolearn Дополнительные сведения о панели мониторинга, в разделе [создания настраиваемой панели мониторинга в службе анализа журналов](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="1560e-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="1560e-357">Можно также создать и использовать панели мониторинга с помощью мобильного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="1560e-358">Дополнительные сведения вы найдете в описании [мобильного приложения OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="1560e-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="1560e-359">В двух нижних плитках hello hello после изображения, вы увидите hello монитор, отображающий список и число.</span><span class="sxs-lookup"><span data-stu-id="1560e-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="1560e-360">По существу всегда требуется номер toobe hello ноль и hello toobe список пустой.</span><span class="sxs-lookup"><span data-stu-id="1560e-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="1560e-361">Иное состояние указывает на наличие условия предупреждения.</span><span class="sxs-lookup"><span data-stu-id="1560e-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="1560e-362">При необходимости, его можно использовать tootake взглянуть на какие компьютеры находятся в условиях нехватки.</span><span class="sxs-lookup"><span data-stu-id="1560e-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![панель мониторинга на мобильном устройстве](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="1560e-364">Используйте оператор in hello</span><span class="sxs-lookup"><span data-stu-id="1560e-364">Use hello in operator</span></span>
<span data-ttu-id="1560e-365">Hello *в* оператор, вместе с *NOT IN* позволяет toouse вложенные поиски, которые являются поисками, включающими другой поиск в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="1560e-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="1560e-366">Такой поисковый запрос заключается в фигурные скобки {} внутри другого поискового запроса, который называется *основным* или *внешним*.</span><span class="sxs-lookup"><span data-stu-id="1560e-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="1560e-367">Результат вложенного поиска, часто это список уникальных результатов Hello затем используется как аргумент в его основном поиске.</span><span class="sxs-lookup"><span data-stu-id="1560e-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="1560e-368">Можно использовать вложенные поиски применяются toomatch подмножества данных, которые нельзя описать непосредственно в выражении поиска, но которые могут быть созданы из поиска.</span><span class="sxs-lookup"><span data-stu-id="1560e-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="1560e-369">Например, если вы хотите использовать один поиск toofind все события из *компьютерах отсутствуют обновления безопасности*, то вы должны toodesign вложенный поиск, который сначала определяет, что *компьютерах отсутствуют обновления безопасности*  поиск события принадлежность toothose узлов.</span><span class="sxs-lookup"><span data-stu-id="1560e-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="1560e-370">Таким образом, вы выражаете *компьютеры на которых сейчас отсутствуют необходимые обновления для системы безопасности* с приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="1560e-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="1560e-372">После получения списка hello hello поиск можно использовать в качестве внутреннего поиска toofeed hello списка компьютеров во внешний (основной) поиск, который будет искать события для этих компьютеров.</span><span class="sxs-lookup"><span data-stu-id="1560e-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="1560e-373">Для этого внутренний поиск hello в фигурные скобки, а его результаты передаются как возможные значения для поля или фильтра во внешний поиск hello, с помощью оператора hello in..</span><span class="sxs-lookup"><span data-stu-id="1560e-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="1560e-374">Hello запрос будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1560e-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="1560e-376">Также Обратите внимание hello оценка системных обновлений hello фильтр, используемый в hello внутреннего поиска, так как время моментальный снимок всех компьютеров каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="1560e-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="1560e-377">Hello внутренний запрос можно сделать более простым и точным счет поиска только за день.</span><span class="sxs-lookup"><span data-stu-id="1560e-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="1560e-378">Hello внешний поиск использует Выбор времени hello в пользовательском интерфейсе hello, получая события за последние 7 дней hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="1560e-379">Подробные сведения об операторах времени см. в разделе [Логические операторы](#boolean-operators).</span><span class="sxs-lookup"><span data-stu-id="1560e-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="1560e-380">Так как вы только использовать hello результаты внутреннего поиска hello как значение фильтра для Здравствуйте внешнего, можно по-прежнему применять команды в hello внешнего поиска.</span><span class="sxs-lookup"><span data-stu-id="1560e-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="1560e-381">Например можно по-прежнему hello группы выше события с помощью другой команды measure:</span><span class="sxs-lookup"><span data-stu-id="1560e-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="1560e-383">Обычно следует вашего внутреннего запроса tooexecute быстро за время ожидания на стороне службы анализа журналов и также tooreturn небольшое количество результатов.</span><span class="sxs-lookup"><span data-stu-id="1560e-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="1560e-384">Если hello внутренний запрос возвращает больше результатов, hello список результатов усекается, что может привести tooreturn внешнего поиска hello неверные результаты.</span><span class="sxs-lookup"><span data-stu-id="1560e-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="1560e-385">Другое правило заключается в этом hello сейчас внутренний поиск должен tooprovide *агрегированных* результаты.</span><span class="sxs-lookup"><span data-stu-id="1560e-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="1560e-386">Другими словами, в нем должна содержаться команда *measure*. Необработанные результаты пока нельзя передавать во внешний поиск.</span><span class="sxs-lookup"><span data-stu-id="1560e-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="1560e-387">Кроме того может существовать только один оператор IN, и он должен быть последним фильтром hello в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="1560e-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="1560e-388">Несколько операторов IN не может быть либо — это предотвращает запуск нескольких вложенных поисков: важно происходит, только один вложенный или внутренний поиск hello возможна для каждого внешнего поиска.</span><span class="sxs-lookup"><span data-stu-id="1560e-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="1560e-389">Даже при наличии этих ограничений IN позволяет множество видов коррелированных поисков и вы toodefine содержать что-нибудь подобное toogroups, таких как компьютеры, пользователей или файлы, независимо от hello полей данных.</span><span class="sxs-lookup"><span data-stu-id="1560e-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="1560e-390">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="1560e-390">Here are more examples:</span></span>

<span data-ttu-id="1560e-391">**Все обновления, отсутствующие на компьютерах, где отключен параметр автоматического обновления.**</span><span class="sxs-lookup"><span data-stu-id="1560e-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="1560e-392">**Все события ошибок для компьютеров, на которых работает SQL Server (то есть тех, где выполнялась оценка SQL).**</span><span class="sxs-lookup"><span data-stu-id="1560e-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="1560e-393">**Все события безопасности для компьютеров, являющихся контроллерами домена (то есть тех, где выполнялась оценка AD).**</span><span class="sxs-lookup"><span data-stu-id="1560e-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="1560e-394">**Какие другие учетные записи входили на toohello же компьютеры, в которых учетная запись BACONLAND\jochan?**</span><span class="sxs-lookup"><span data-stu-id="1560e-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="1560e-395">Использование команды distinct hello</span><span class="sxs-lookup"><span data-stu-id="1560e-395">Use hello distinct command</span></span>
<span data-ttu-id="1560e-396">Как hello названия, эта команда предоставляет список уникальных значений для поля.</span><span class="sxs-lookup"><span data-stu-id="1560e-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="1560e-397">Несмотря на простоту команды, она весьма полезна.</span><span class="sxs-lookup"><span data-stu-id="1560e-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="1560e-398">Здравствуйте, же может осуществляться с помощью команды measure count() также, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1560e-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![пример команды поиска DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="1560e-400">Однако если вас интересует только список уникальных значений, а не hello число документов, что значения, затем DISTINCT может предоставить tooread более понятные и удобочитаемые выходные данные и более короткий синтаксис, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1560e-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![пример команды поиска DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="1560e-402">Функция countdistinct hello с командой measure hello</span><span class="sxs-lookup"><span data-stu-id="1560e-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="1560e-403">функция countdistinct Hello подсчитывает hello число различающихся значений в каждой группе.</span><span class="sxs-lookup"><span data-stu-id="1560e-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="1560e-404">Например, это может быть использован toocount hello количество уникальных компьютеров, создание отчетов для каждого типа:</span><span class="sxs-lookup"><span data-stu-id="1560e-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="1560e-406">Используйте команду интервал измерения hello</span><span class="sxs-lookup"><span data-stu-id="1560e-406">Use hello measure interval command</span></span>
<span data-ttu-id="1560e-407">Log Analytics собирает данные практически в режиме реального времени, что позволяет собирать и наглядно отображать почти любой счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="1560e-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="1560e-408">Просто введите запрос hello **типа: производительности** вернет тысячи метрики диаграмм на основе hello числа счетчиков и серверов в вашей среде анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="1560e-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="1560e-409">С метрики статистической обработки по требованию, можно взглянуть на hello общую метрики в вашей среде на высоком уровне и глубокое погружение в более подробных данных, необходимого для.</span><span class="sxs-lookup"><span data-stu-id="1560e-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="1560e-410">Предположим, что требуется tooknow Какова средняя загрузка ЦП hello на всех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="1560e-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="1560e-411">Просмотрев hello средняя загрузка ЦП для каждого компьютера, может оказаться полезным так как результаты могут получить сглажены. toolook Дополнительные сведения о можно собрать ваши результаты в меньшее время окна фрагментами и найти в временных рядов по разным измерениям.</span><span class="sxs-lookup"><span data-stu-id="1560e-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="1560e-412">Например нужно выполнить hello почасовой среднее использование ЦП на всех компьютерах следующим образом.</span><span class="sxs-lookup"><span data-stu-id="1560e-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![measure average interval](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="1560e-414">По умолчанию эти результаты будут отображаться в виде интерактивного графика с несколькими рядами данных.</span><span class="sxs-lookup"><span data-stu-id="1560e-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="1560e-415">Этот график поддерживает переключение рядов (с масштабированием по оси y), масштабирование и подсказки при наведении указателя мыши.</span><span class="sxs-lookup"><span data-stu-id="1560e-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="1560e-416">параметр отображения таблицы Hello по-прежнему доступен для просмотра hello необработанных данных, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="1560e-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="1560e-417">Также можно сгруппировать результаты по другим полям.</span><span class="sxs-lookup"><span data-stu-id="1560e-417">You can also group by other fields.</span></span> <span data-ttu-id="1560e-418">В этом примере просматриваю все счетчики % hello для одного конкретного компьютера и требуется tooknow возможности hello каждый час 70 процентилем каждого счетчика.</span><span class="sxs-lookup"><span data-stu-id="1560e-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="1560e-419">Один toonote вещь: эти запросы не, ограниченный tooperformance счетчики.</span><span class="sxs-lookup"><span data-stu-id="1560e-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="1560e-420">Можно применить их tooany метрику.</span><span class="sxs-lookup"><span data-stu-id="1560e-420">You can apply them tooany metric.</span></span> <span data-ttu-id="1560e-421">В этом примере выполняется просмотр журналов W3C IIS.</span><span class="sxs-lookup"><span data-stu-id="1560e-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="1560e-422">Я хочу tooknow возможности hello максимальное время, затрачиваемое на 5-минутный интервал для обработки каждого запроса:</span><span class="sxs-lookup"><span data-stu-id="1560e-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="1560e-423">Использование нескольких статистических выражений в одном запросе</span><span class="sxs-lookup"><span data-stu-id="1560e-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="1560e-424">Для команды measure можно указать несколько статистических выражений.</span><span class="sxs-lookup"><span data-stu-id="1560e-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="1560e-425">Каждому из них можно присвоить отдельный псевдоним.</span><span class="sxs-lookup"><span data-stu-id="1560e-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="1560e-426">Если не задан, возникающие hello псевдоним именем поля будет hello агрегатной функции, который был использован (т. е. «avg(CounterValue)» для avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="1560e-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="1560e-428">Вот еще один пример:</span><span class="sxs-lookup"><span data-stu-id="1560e-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="1560e-429">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1560e-429">Next steps</span></span>
<span data-ttu-id="1560e-430">Дополнительные сведения о поиске по журналам можно получить в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="1560e-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="1560e-431">Используйте [настраиваемые поля в службе анализа журналов](log-analytics-custom-fields.md) tooextend запросов поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="1560e-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="1560e-432">Просмотрите hello [Справочник поиска журнала анализа журналов](log-analytics-search-reference.md) tooview все hello поиск поля и аспекты, доступных в службе анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="1560e-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
