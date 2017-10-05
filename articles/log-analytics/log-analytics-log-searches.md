---
title: "Поиск данных по журналам в Azure Log Analytics | Документация Майкрософт"
description: "Поиск по журналам позволяет объединять и сопоставлять любые данные о компьютерах из нескольких источников в вашей среде."
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
ms.openlocfilehash: bf237a837297cb8f1ab3a3340139133adcd2b244
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="8f2f2-103">Поиск данных по журналам в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8f2f2-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="8f2f2-104">В этой статье описывается поиск по журналам с использованием текущего языка запросов в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="8f2f2-105">Если ваша рабочая область переведена на [новый язык запросов Log Analytics](log-analytics-log-search-upgrade.md), ознакомьтесь с описанием [функции поиска по журналам в Log Analytics (новая версия)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="8f2f2-106">Основой Log Analytics является функция поиска по журналам, которая позволяет объединять и сопоставлять данные компьютеров из нескольких источников в существующей среде.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-106">At the core of Log Analytics is the log search feature which allows you to combine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="8f2f2-107">Функция поиска журналов также дополняет решения, позволяя получать сводные показатели по определенной проблемной области.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-107">Solutions are also powered by log search to bring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="8f2f2-108">На странице Поиск можно создать запрос, а затем во время поиска отфильтровать результаты с помощью элементов управления аспектами.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-108">On the Search page, you can create a query, and then when you search, you can filter the results by using facet controls.</span></span> <span data-ttu-id="8f2f2-109">Можно создать сложные запросы для преобразования и фильтрации результатов, а также для формирования соответствующих отчетов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-109">You can also create advanced queries to transform, filter, and report on your results.</span></span>

<span data-ttu-id="8f2f2-110">Общие запросы поиска журналов отображаются на большинстве страниц решений.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="8f2f2-111">В консоли OMS можно щелкнуть плитки или открыть вложенные элементы, чтобы просмотреть сведения о них с помощью функции поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-111">Throughout the OMS console, you can click tiles or drill in to other items to view details about the item by using log search.</span></span>

<span data-ttu-id="8f2f2-112">В этом учебнике мы рассмотрим примеры, охватывающие все основные аспекты использования поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-112">In this tutorial, we'll walk through examples to cover all the basics when you use log search.</span></span>

<span data-ttu-id="8f2f2-113">Мы начнем с простых практических примеров, а затем разовьем их, чтобы получить представление о реальных вариантах использования синтаксиса для извлечения нужных ценных сведений из данных.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how to use the syntax to extract the insights you want from the data.</span></span>

<span data-ttu-id="8f2f2-114">После ознакомления с методиками поиска рекомендуем изучить [справочник по поиску в журналах Log Analytics](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-114">After you've familiar with search techniques, you can review the [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="8f2f2-115">использование базовых фильтров;</span><span class="sxs-lookup"><span data-stu-id="8f2f2-115">Use basic filters</span></span>
<span data-ttu-id="8f2f2-116">Прежде всего, необходимо знать, что первой частью поискового запроса, расположенной перед символом вертикальной черты "|", всегда является *фильтр*.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-116">The first thing to know is that the first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="8f2f2-117">Его можно рассматривать как предложение WHERE в TSQL: он определяет, *какое* подмножество данных следует извлекать из хранилища данных OMS.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data to pull out of the OMS data store.</span></span> <span data-ttu-id="8f2f2-118">Поиск в хранилище данных заключается главным образом в указании характеристик данных, которые нужно извлечь, поэтому логично, что запрос будет начинаться с предложения WHERE.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-118">Searching in the data store is largely about specifying the characteristics of the data that you want to extract, so it is natural that a query would start with the WHERE clause.</span></span>

<span data-ttu-id="8f2f2-119">Самыми простыми из доступных фильтров являются *ключевые слова*, такие как "ошибка", "время ожидания" или имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-119">The most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="8f2f2-120">Эти типы простых запросов обычно возвращают различные формы данных в рамках одного результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-120">These types of simple queries generally return diverse shapes of data within the same result set.</span></span> <span data-ttu-id="8f2f2-121">Это происходит потому, что Log Analytics использует в системе различные *типы* данных.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-121">This is because Log Analytics has different *types* of data in the system.</span></span>

### <a name="to-conduct-a-simple-search"></a><span data-ttu-id="8f2f2-122">Выполнение простого поиска</span><span class="sxs-lookup"><span data-stu-id="8f2f2-122">To conduct a simple search</span></span>
1. <span data-ttu-id="8f2f2-123">На портале OMS щелкните **Поиск по журналам**.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-123">In the OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="8f2f2-124">![плитка поиска](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="8f2f2-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="8f2f2-125">В поле запроса введите `error` и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-125">In the query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="8f2f2-126">![ошибка поиска](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="8f2f2-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="8f2f2-127">Например, запрос для `error` на следующем рисунке вернул 100 000 записей **Event** (собранных функцией управления журналами), 18 записей **ConfigurationAlert** (созданных в ходе оценки конфигурации) и 12 записей **ConfigurationChange** (полученных функцией отслеживания изменений).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-127">For example, the query for `error` in the following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by the Change Tracking).</span></span>   
    <span data-ttu-id="8f2f2-128">![результаты поиска](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="8f2f2-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="8f2f2-129">Эти фильтры на самом деле не являются классами и типами объектов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="8f2f2-130">*Type* — это просто тег, свойство, строка, имя или категория, присоединяемые к фрагменту данных.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-130">*Type* is just a tag, or a property, or a string/name/category, that is attached to a piece of data.</span></span> <span data-ttu-id="8f2f2-131">Некоторые документы в системе помечены как **Type:ConfigurationAlert**, другие — как **Type:Perf** или **Type:Event** и т. д.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-131">Some documents in the system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="8f2f2-132">Каждый результат поиска, документ или запись отображает все общие свойства и их значения для каждого из этих фрагментов данных, и вы можете использовать эти имена полей в фильтре, когда необходимо получить только те записи, где поле имеет заданное значение.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-132">Each search result, document, record, or entry displays all the raw properties and their values for each of those pieces of data, and you can use those field names to specify in the filter when you want to retrieve only the records where the field has that given value.</span></span>

<span data-ttu-id="8f2f2-133">*Type* — это просто поле, которое имеет все записи, оно ничем не отличается от любого другого поля.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="8f2f2-134">Это было установлено на основе значения поля "Тип".</span><span class="sxs-lookup"><span data-stu-id="8f2f2-134">This was established based on the value of the Type field.</span></span> <span data-ttu-id="8f2f2-135">Эта запись будет иметь другую форму.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-135">That record will have a different shape or form.</span></span> <span data-ttu-id="8f2f2-136">Кстати, синтаксис вида **Type=Perf** или **Type=Event** понадобится вам еще и для запроса событий или данных о производительности.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-136">Incidentally, **Type=Perf**, or **Type=Event** is also the syntax that you need to learn to query for performance data or events.</span></span>

<span data-ttu-id="8f2f2-137">Между именем поля и значением можно использовать двоеточие (:) или знак равенства (=).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-137">You can use either a colon (:) or an equal sign (=) after the field name and before the value.</span></span> <span data-ttu-id="8f2f2-138">**Type:Event** и **Type=Event** имеют одинаковое значение, и вы можете выбрать любой из этих стилей.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose the style you prefer.</span></span>

<span data-ttu-id="8f2f2-139">Например, если записи с Type=Perf имеют поле с именем CounterName, вы можете написать запрос такого вида: `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-139">So, if the Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="8f2f2-140">Это позволит получить только те данные о производительности, где счетчик производительности имеет имя "% Processor Time" (% загруженности процессора).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-140">This will give you only the performance data where the performance counter name is "% Processor Time".</span></span>

### <a name="to-search-for-processor-time-performance-data"></a><span data-ttu-id="8f2f2-141">Поиск данных о производительности по загруженности процессора</span><span class="sxs-lookup"><span data-stu-id="8f2f2-141">To search for processor time performance data</span></span>
* <span data-ttu-id="8f2f2-142">В поле поискового запроса введите `Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="8f2f2-142">In the search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="8f2f2-143">Можно указать значение более точно и использовать в запросе элемент **InstanceName=_'Total'**, который представляет собой счетчик производительности Windows.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-143">You can also be more specific and use **InstanceName=_'Total'** in the query, which is a Windows performance counter.</span></span> <span data-ttu-id="8f2f2-144">Можно также выбрать другой аспект и другую пару **поле:значение**.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="8f2f2-145">Фильтр автоматически добавляется в фильтр в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-145">The filter is automatically added to your filter in the query bar.</span></span> <span data-ttu-id="8f2f2-146">Вы увидите это на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-146">You can see this in the following image.</span></span> <span data-ttu-id="8f2f2-147">Там показано, как добавить **InstanceName:’_Total’** в запрос, не вводя никакого текста.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-147">It shows you where to click to add **InstanceName:’_Total’** to the query without typing anything.</span></span>

![аспект поиска](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="8f2f2-149">Ваш запрос превращается в `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="8f2f2-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="8f2f2-150">В этом примере нет необходимости указывать **Type=Perf** для получения этого результата.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-150">In this example, you don't have to specify **Type=Perf** to get to this result.</span></span> <span data-ttu-id="8f2f2-151">Так как поля CounterName и InstanceName существуют только для записей Type=Perf, запрос является достаточно точным и вернет точно такие же результаты, как и предыдущий, более длинный запрос.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-151">Because the fields CounterName and InstanceName only exist for records of Type=Perf, the query is specific enough to return the same results as the longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="8f2f2-152">Это происходит потому, что все фильтры в запросе вычисляются так, как если бы они были связаны оператором *И (AND)* .</span><span class="sxs-lookup"><span data-stu-id="8f2f2-152">This is because all the filters in the query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="8f2f2-153">Фактически, чем больше поле вы добавляете в условия, тем менее точные и детальные результаты вы получаете.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-153">Effectively, the more fields you add to the criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="8f2f2-154">Например, запрос `Type=Event EventLog="Windows PowerShell"` идентичен запросу `Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-154">For example, the query `Type=Event EventLog="Windows PowerShell"` is identical to `Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="8f2f2-155">Он возвращает все события, которые были зарегистрированы и собраны из журнала событий Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-155">It returns all events that were logged in and collected from the Windows PowerShell event log.</span></span> <span data-ttu-id="8f2f2-156">Если вы добавляете фильтр несколько раз, выбирая один и тот же аспект, проблема является совершенно формальной — он может загромождать панель поиска, но по-прежнему возвращает те же результаты, так как неявный оператор И всегда присутствует.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-156">If you add a filter multiple times by repeatedly selecting the same facet, then the issue is purely cosmetic--it might clutter the Search bar, but it still returns the same results because the implicit AND operator is always there.</span></span>

<span data-ttu-id="8f2f2-157">Вы можете легко обратить неявный оператор И с помощью явного оператора НЕ (NOT).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-157">You can easily reverse the implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="8f2f2-158">Например:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-158">For example:</span></span>

<span data-ttu-id="8f2f2-159">Запрос `Type:Event NOT(EventLog:"Windows PowerShell")` или его эквивалент `Type=Event EventLog!="Windows PowerShell"` возвращают все события из всех журналов, которые НЕ являются журналом Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT the Windows PowerShell log.</span></span>

<span data-ttu-id="8f2f2-160">Либо можно использовать другой логический оператор, такой как ИЛИ (OR).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="8f2f2-161">Следующий запрос возвращает записи, для которых EventLog имеет значение Application ИЛИ System.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-161">The following query returns records for which the EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="8f2f2-162">Используя приведенный выше запрос, вы получаете записи для обоих журналов в одном результирующем наборе.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-162">Using the above query, you’ll get entries for both logs in the same result set.</span></span>

<span data-ttu-id="8f2f2-163">Однако если удалить оператор ИЛИ, оставив неявный оператор И на месте, то следующий запрос не даст никаких результатов, так как запись журнала событий, относящаяся к обоим журналам, не существует.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-163">However, if you remove the OR by leaving the implicit AND in place, then the following query will not produce any results because there isn’t an event log entry that belongs to BOTH logs.</span></span> <span data-ttu-id="8f2f2-164">Каждая запись журнала была записана только в один из двух журналов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-164">Each event log entry was written to only one of the two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="8f2f2-165">использование дополнительных фильтров;</span><span class="sxs-lookup"><span data-stu-id="8f2f2-165">Use additional filters</span></span>
<span data-ttu-id="8f2f2-166">Следующий запрос возвращает записи для 2 журналов событий для всех компьютеров, которые отправляли данные.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-166">The following query returns entries for 2 event logs for all the computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![результаты поиска](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="8f2f2-168">Выбрав одно из полей и один из фильтров, можно будут сузить запрос до конкретного компьютера, исключив при этом все остальные.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-168">Selecting one of the fields or filters will narrow the query to a specific computer, excluding all other ones.</span></span> <span data-ttu-id="8f2f2-169">Результирующий запрос будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-169">The resulting query would resemble the following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="8f2f2-170">Это эквивалентно следующему запросу из-за неявного оператора И.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-170">Which is equivalent to the following, because of the implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="8f2f2-171">Каждый запрос вычисляется в следующем явном порядке.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-171">Each query is evaluated in the following explicit order.</span></span> <span data-ttu-id="8f2f2-172">Обратите внимание на скобки.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-172">Note the parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="8f2f2-173">Как и в случае с полем журнала событий, вы можете извлечь данные только для набора определенных компьютеров путем добавления оператора ИЛИ.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-173">Just like the event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="8f2f2-174">Например:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="8f2f2-175">Аналогичным образом, этот следующий запрос возвращает значение **% времени ЦП** только для двух выбранных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-175">Similarly, this the following query return **% CPU Time** for the selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="8f2f2-176">Типы полей</span><span class="sxs-lookup"><span data-stu-id="8f2f2-176">Field types</span></span>
<span data-ttu-id="8f2f2-177">При создании фильтров следует учитывать особенности работы с разными типами полей, возвращаемых в результатах поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-177">When creating filters, you should understand the differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="8f2f2-178">**Поля, доступные для поиска,** выделены синим цветом в результатах.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="8f2f2-179">Эти поля можно включить в условия поиска по конкретному полю, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-179">You can use searchable fields in search conditions specific to the field such as the following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="8f2f2-180">**Поля с возможностью поиска произвольного текста** выделены серым цветом в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="8f2f2-181">В отличие от полей, доступных для поиска, их нельзя включить в условия поиска по определенному полю.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-181">They cannot be used with search conditions specific to the field like searchable fields.</span></span>  <span data-ttu-id="8f2f2-182">Они включаются в поиск только при выполнении запроса по всем полям, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-182">They are only searched when performing a query across all fields such as the following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="8f2f2-183">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="8f2f2-183">Boolean operators</span></span>
<span data-ttu-id="8f2f2-184">С помощью полей даты и времени и числовых полей можно выполнить поиск значений с помощью операторов *больше*, *меньше* и *меньше или равно*.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="8f2f2-185">На панели поисковых запросов можно использовать простые операторы, такие как >, < , >=, <= , !=.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-185">You can use simple operators such as >, < , >=, <= , != in the query search bar.</span></span>

<span data-ttu-id="8f2f2-186">Можно запросить журнал событий за конкретный период времени.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="8f2f2-187">Например, последние 24 часа обозначает следующее мнемоническое выражение.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-187">For example, the last 24 hours is expressed with the following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="to-search-using-a-boolean-operator"></a><span data-ttu-id="8f2f2-188">Поиск с помощью логического оператора</span><span class="sxs-lookup"><span data-stu-id="8f2f2-188">To search using a boolean operator</span></span>
* <span data-ttu-id="8f2f2-189">В поле поискового запроса введите `EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="8f2f2-189">In the search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="8f2f2-190">![поиск с логическими операторами](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="8f2f2-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="8f2f2-191">Хотя интервалом времени можно управлять графически и в большинстве случаев так и следует поступать, включение фильтра времени непосредственно в запрос дает определенные преимущества.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-191">Although you can control the time interval graphically, and most times you might want to do that, there are advantages to including a time filter directly into the query.</span></span> <span data-ttu-id="8f2f2-192">Например, это прекрасно работает с панелями мониторинга, где можно переопределить время для каждой плитки независимо от *глобального* селектора времени на странице панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-192">For example, this works great with dashboards where you can override the time for each tile, regardless of the *global* time selector on the dashboard page.</span></span> <span data-ttu-id="8f2f2-193">Дополнительные сведения см. в статье [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/) (Аспекты использования времени на панели мониторинга).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="8f2f2-194">При фильтрации по времени помните о том, что вы получите результаты, соответствующие *пересечению* двух периодов: заданного на портале OMS (S1) и в запросе (S2).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-194">When filtering by time, keep in mind that you get results for the *intersection* of the two time periods: the one specified in the OMS portal (S1) and the one specified in the query (S2).</span></span>

![пересечению](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="8f2f2-196">Это означает, что, если периоды не пересекаются (например, на портале OMS выбрана **текущая неделя**, а в запросе указана **прошлая неделя**), вы не получите никаких результатов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-196">This means, if the time periods don’t intersect, for example in the OMS portal where you choose **This week** and in the query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="8f2f2-197">Операторы сравнения, используемые для поля TimeGenerated, также могут пригодиться и в других ситуациях.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-197">Comparison operators used for the TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="8f2f2-198">Например, для числовых полей.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-198">For example, with numeric fields.</span></span>

<span data-ttu-id="8f2f2-199">Предположим, что оповещения оценки конфигурации имеют следующие уровни серьезности:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-199">For example, given that Configuration Assessment’s alerts have the following severity values:</span></span>

* <span data-ttu-id="8f2f2-200">0 = информационный</span><span class="sxs-lookup"><span data-stu-id="8f2f2-200">0 = Information</span></span>
* <span data-ttu-id="8f2f2-201">1 = предупреждение</span><span class="sxs-lookup"><span data-stu-id="8f2f2-201">1 = Warning</span></span>
* <span data-ttu-id="8f2f2-202">2 = критический</span><span class="sxs-lookup"><span data-stu-id="8f2f2-202">2 = Critical</span></span>

<span data-ttu-id="8f2f2-203">С помощью следующего запроса можно запросить предупреждения и критические оповещения, а также исключить информационные оповещения:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-203">You can query for both warning and critical alerts and also exclude informational ones with the following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="8f2f2-204">Можно также использовать запросы в диапазоне.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-204">You can also use range queries.</span></span> <span data-ttu-id="8f2f2-205">Это означает, что вы можете задать начало и конец диапазона значений в последовательности.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-205">This means that you can provide the beginning and end range of values in a sequence.</span></span> <span data-ttu-id="8f2f2-206">Например, если требуются события из журнала событий Operations Manager, где EventID больше или равен 2100, но не больше 2199, следующий запрос позволит получить их.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-206">For example, if you want events from the Operations Manager event log where the EventID is greater than or equal to 2100 but not greater than 2199, then the following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="8f2f2-207">Необходимо использовать синтаксис диапазона, подразумевающий использование в качестве разделителя пары поле:значение двоеточия (:), а *не* знака равенства (=).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-207">The range syntax you must use is the colon (:) field:value separator and *not* the equal sign (=).</span></span> <span data-ttu-id="8f2f2-208">Заключите нижнюю и верхнюю границу диапазона в квадратные скобки, разделив их двумя точками (..).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-208">Enclose the lower and upper end of the range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="8f2f2-209">работа с результатами поиска;</span><span class="sxs-lookup"><span data-stu-id="8f2f2-209">Manipulate search results</span></span>
<span data-ttu-id="8f2f2-210">При поиске данных может потребоваться уточнение поискового запроса и наличие высокого уровня контроля над результатами.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-210">When you're searching for data, you'll want to refine your search query and have a good level of control over the results.</span></span> <span data-ttu-id="8f2f2-211">При извлечении результатов можно применять команды для их преобразования.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-211">When results are retrieved, you can apply commands to transform them.</span></span>

<span data-ttu-id="8f2f2-212">Команды в поиске Log Analytics *обязательно* указываются после символа вертикальной черты (|).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-212">Commands in Log Analytics searches *must* follow after the vertical pipe character (|).</span></span> <span data-ttu-id="8f2f2-213">Фильтр должен всегда быть первой частью строки запроса.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-213">A filter must always be the first part of a query string.</span></span> <span data-ttu-id="8f2f2-214">Он определяет набор данных, с которым вы работаете, а затем направляет эти результаты в команду.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-214">It defines the data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="8f2f2-215">После этого можно использовать символ черты, чтобы добавить дополнительные команды.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-215">You can then use the pipe to add additional commands.</span></span> <span data-ttu-id="8f2f2-216">Это приблизительно соответствует конвейеру Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-216">This is loosely similar to the Windows PowerShell pipeline.</span></span>

<span data-ttu-id="8f2f2-217">В целом язык поиска Log Analytics использует стиль и правила PowerShell, чтобы ИТ-специалистам было проще его изучать.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-217">In general, the Log Analytics search language tries to follow PowerShell style and guidelines to make it similar to the IT pros, and to ease the learning curve.</span></span>

<span data-ttu-id="8f2f2-218">Команды имеют форму глаголов, чтобы можно было легко понять, что именно они делают.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="8f2f2-219">Сортировать</span><span class="sxs-lookup"><span data-stu-id="8f2f2-219">Sort</span></span>
<span data-ttu-id="8f2f2-220">Команда sort позволяет задать порядок сортировки по одному или нескольким полям.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-220">The sort command allows you to define the sorting order by one or multiple fields.</span></span> <span data-ttu-id="8f2f2-221">Даже если вы не используете ее, по умолчанию применяется сортировка по времени в порядке убывания.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="8f2f2-222">Недавние результаты всегда находятся в верхней части результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-222">The most recent results are always at the top of search results.</span></span> <span data-ttu-id="8f2f2-223">Это означает, что при выполнении поиска с учетом `Type=Event EventID=1234` реально выполняется следующее:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="8f2f2-224">Это происходит так, поскольку данная процедура знакома вам по работе с журналами.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-224">That's because it is the type of experience you are familiar with in logs.</span></span> <span data-ttu-id="8f2f2-225">Например, в средстве просмотра событий Windows.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-225">For example, in the Windows Event Viewer.</span></span>

<span data-ttu-id="8f2f2-226">С помощью команды sort можно изменить способ возврата результатов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-226">You can use Sort to change the way results are returned.</span></span> <span data-ttu-id="8f2f2-227">Ниже приведены примеры того, как именно это работает.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-227">The following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="8f2f2-228">Простые примеры выше показывают работу команды: они изменяют форму результатов, возвращаемых фильтром.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-228">The simple examples above show you how commands work--they change the shape of the results that the filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="8f2f2-229">Limit и top</span><span class="sxs-lookup"><span data-stu-id="8f2f2-229">Limit and top</span></span>
<span data-ttu-id="8f2f2-230">Другой менее известной командой является LIMIT.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="8f2f2-231">Эта команда похожа на команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="8f2f2-232">По функциональности Limit аналогична команде TOP.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-232">Limit is functionally identical to the TOP command.</span></span> <span data-ttu-id="8f2f2-233">Следующие запросы возвращают одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-233">The following queries return the same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="to-search-using-top"></a><span data-ttu-id="8f2f2-234">Поиск с использованием команды top</span><span class="sxs-lookup"><span data-stu-id="8f2f2-234">To search using top</span></span>
* <span data-ttu-id="8f2f2-235">В поле поискового запроса введите `Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="8f2f2-235">In the search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="8f2f2-236">![поиск лучших результатов](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="8f2f2-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="8f2f2-237">На приведенном выше рисунке показано 358 тыс. записей с EventID=600.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-237">In the image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="8f2f2-238">Поля, аспекты и фильтры в левой части всегда отображают сведения о результатах, возвращаемых *фильтром* запроса, то есть частью запроса до первой вертикальной черты.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-238">The fields, facets, and filters on the left always show information about the results returned *by the filter portion* of the query, which is the part before any pipe character.</span></span> <span data-ttu-id="8f2f2-239">Область **Результаты** панели возвращает только 1 последний результат, так как команда в примере изменила форму результатов и преобразовала их.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-239">The **Results** pane only returns the most recent 1 result, because the example command shaped and transformed the results.</span></span>

### <a name="select"></a><span data-ttu-id="8f2f2-240">Выберите пункт</span><span class="sxs-lookup"><span data-stu-id="8f2f2-240">Select</span></span>
<span data-ttu-id="8f2f2-241">Команда SELECT похожа на команду Select-Object в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-241">The SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="8f2f2-242">Она возвращает отфильтрованные результаты, имеющие не все свои первоначальные свойства.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="8f2f2-243">Вместо этого она выбирает только заданные вами свойства.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-243">Instead, it selects only the properties that you specify.</span></span>

#### <a name="to-run-a-search-using-the-select-command"></a><span data-ttu-id="8f2f2-244">Выполнение поиска с помощью команды select</span><span class="sxs-lookup"><span data-stu-id="8f2f2-244">To run a search using the select command</span></span>
1. <span data-ttu-id="8f2f2-245">В поле поиска введите `Type=Event` и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="8f2f2-246">Щелкните **+ Дополнительно** в одном из результатов, чтобы просмотреть все свойства, которые имеют результаты.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-246">Click **+ show more** in one of the results to view all the properties that the results have.</span></span>
3. <span data-ttu-id="8f2f2-247">Выберите некоторые из них явным образом, и запрос изменяется на `Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-247">Select some of those explicitly, and the query changes to `Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="8f2f2-248">![поиск с помощью select](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="8f2f2-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="8f2f2-249">Это команда особенно полезна, когда требуется управлять выходными данными поиска и отбирать из всего набора записей только те блоки данных, которые важны для анализа.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-249">This command is particularly useful when you want to control search output and choose only the portions of data that really matter for your exploration, which often isn’t the full record.</span></span> <span data-ttu-id="8f2f2-250">Это также полезно, когда записи различных типов имеют *несколько* общих свойств, но не *все* их свойства являются общими.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="8f2f2-251">Вы можете формировать выходные данные, которые имеют более привычный вид таблицы или более удобны для экспорта в CSV-файл и последующей обработки в Excel.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-251">The, you can generate output that looks more naturally like a table, or work well when exported to a CSV file and then massaged in Excel.</span></span>

## <a name="use-the-measure-command"></a><span data-ttu-id="8f2f2-252">использование команды measure;</span><span class="sxs-lookup"><span data-stu-id="8f2f2-252">Use the measure command</span></span>
<span data-ttu-id="8f2f2-253">MEASURE является одной из наиболее универсальных команд в поиске Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-253">MEASURE is one of the most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="8f2f2-254">Она позволяет применять статистические *функции* к данным и статистически обрабатывать данные, сгруппированные по заданному полю.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-254">It allows you to apply statistical *functions* to your data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="8f2f2-255">Существует несколько статистических функций, поддерживаемых командой Measure.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="8f2f2-256">Measure count()</span><span class="sxs-lookup"><span data-stu-id="8f2f2-256">Measure count()</span></span>
<span data-ttu-id="8f2f2-257">Первой и наиболее простой в использовании статистической функцией является функция *count()* .</span><span class="sxs-lookup"><span data-stu-id="8f2f2-257">The first statistical function to work with, and one of the simplest to understand is the *count()* function.</span></span>

<span data-ttu-id="8f2f2-258">В левой части результатов любого поискового запроса, например `Type=Event`, отображаются фильтры, которые также называются аспектами.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-258">Results from any search query such as `Type=Event`, show filters also called facets on the left side of search results.</span></span> <span data-ttu-id="8f2f2-259">Эти фильтры показывают распределение значений по заданному полю для результатов выполненного поиска.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-259">The filters show a distribution of values by a given field for the results in the search executed.</span></span>

![поиск с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="8f2f2-261">Например, на приведенном выше рисунке видно поле **Computer**, показывающее, что в рамках почти 739 тыс. событий в результатах присутствует 68 уникальных и не совпадающих значений для поля **Computer**.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-261">For example, in the image above you'll see the **Computer** field and it shows that within the almost 739 thousand events in the results, there are 68 unique and distinct values for the **Computer** field in those records.</span></span> <span data-ttu-id="8f2f2-262">На плитке отображаются только 5 лучших значений, которые наиболее часто записываются в поля **Computer**, с сортировкой по количеству документов, содержащих именно это значение в данном поле.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-262">The tile only shows the top 5, which are the most common 5 values that are written in the **Computer** fields), sorted by the number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="8f2f2-263">На рисунке видно, что среди почти 369 тыс. событий 90 тыс. поступают с компьютера OpsInsights04.contoso.com, 83 тыс. — с компьютера DB03.contoso.com и т. д.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-263">In the image you can see that – among those almost 369 thousand events – 90 thousand come from the OpsInsights04.contoso.com computer, 83 thousand from the DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="8f2f2-264">Что делать, если вы хотите просмотреть все значения, а не только 5 лучших значений на плитке?</span><span class="sxs-lookup"><span data-stu-id="8f2f2-264">What if you want to see all values, since the tile only shows only the top 5?</span></span>

<span data-ttu-id="8f2f2-265">Для этого вместе с командой measure можно применить функцию count().</span><span class="sxs-lookup"><span data-stu-id="8f2f2-265">That’s what the measure command can do with the count() function.</span></span> <span data-ttu-id="8f2f2-266">Эта функция не использует никаких параметров.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="8f2f2-267">Просто укажите поле, по которому требуется выполнить группировку, в данном случае это поле **Computer** :</span><span class="sxs-lookup"><span data-stu-id="8f2f2-267">You just specify the field by which you want to group by – the **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![поиск с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="8f2f2-269">Однако **Computer** — это просто поле, используемое *в* каждом фрагменте данных. Нет никаких реляционных баз данных и никакого отдельного объекта **Computer**.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="8f2f2-270">Только значения *в* данных могут описывать, какая сущность создала их, а также ряд других характеристик и аспектов данных, — отсюда мы и получаем термин *аспект*.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-270">Just the values *in* the data can describe which entity generated them, and a number of other characteristics and aspects of the data – hence the term *facet*.</span></span> <span data-ttu-id="8f2f2-271">Однако вы точно так же можете выполнять группировку по другим полям.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="8f2f2-272">Так как исходные результаты почти 739 тыс. событий, переданных в команду measure, также имеют поле с именем **EventID**, можно применить ту же методику для группировки по этому полю и получить количество событий по EventID:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-272">Because the original results of almost 739 thousand events that are piped into the measure command also have a field called **EventID**, you can apply the same technique to group by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="8f2f2-273">Если вас не интересует реальное число записей, содержащих определенное значение, а требуется только список самих значений, можно добавить в конец команду *Select* и просто выбрать первый столбец:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-273">If you're not interested in the actual record count that contain a specific value, but instead if you only want a list of the values themselves, you can add a *Select* command at the end of it and just select the first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="8f2f2-274">После этого можно усложнить запрос и предварительно отсортировать результаты в нем или просто щелкнуть столбцы в сетке.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-274">Then you can get more intricate and pre-sort the results in the query, or you can just click the columns in the grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="to-search-using-measure-count"></a><span data-ttu-id="8f2f2-275">Поиск с использованием measure count</span><span class="sxs-lookup"><span data-stu-id="8f2f2-275">To search using measure count</span></span>
* <span data-ttu-id="8f2f2-276">В поле поискового запроса введите `Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="8f2f2-276">In the search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="8f2f2-277">Добавьте `| Select EventID` в конец запроса.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-277">Append `| Select EventID` to the end of the query.</span></span>
* <span data-ttu-id="8f2f2-278">Затем добавьте `| Sort EventID asc` в конец запроса.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-278">Finally, append `| Sort EventID asc` to the end of the query.</span></span>

<span data-ttu-id="8f2f2-279">Существует несколько важных моментов, на которые следует обратите внимание.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-279">There are a couple important points to notice and emphasize:</span></span>

<span data-ttu-id="8f2f2-280">Во-первых, отображаемые результаты больше не являются исходными необработанными результатами.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-280">First, the results you see are not the original raw results anymore.</span></span> <span data-ttu-id="8f2f2-281">Вместо этого они являются агрегированными результатами, то есть группами результатов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="8f2f2-282">Это не представляет проблемы, однако следует понимать, что взаимодействие осуществляется совершенно с иной формой данных, которая отличается от исходной необработанной формы, создаваемой в режиме реального времени в результате статистической обработки или применения статистической функции.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from the original raw shape that gets created on the fly as a result of the aggregation/statistical function.</span></span>

<span data-ttu-id="8f2f2-283">Во-вторых, в настоящее время **Measure count** возвращает только 100 лучших несовпадающих результатов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-283">Second, **Measure count** currently returns only the top 100 distinct results.</span></span> <span data-ttu-id="8f2f2-284">Это ограничение не применяется к другим статистическим функциям.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-284">This limit does not apply to the other statistical functions.</span></span> <span data-ttu-id="8f2f2-285">Поэтому обычно перед применением measure count() сначала требуется использовать более точный фильтр для поиска определенных элементов.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-285">So, you'll usually need to use a more precise filter first to search for specific items before you apply measure count().</span></span>

## <a name="use-the-max-and-min-functions-with-the-measure-command"></a><span data-ttu-id="8f2f2-286">использование функций max и min с командой measure;</span><span class="sxs-lookup"><span data-stu-id="8f2f2-286">Use the max and min functions with the measure command</span></span>
<span data-ttu-id="8f2f2-287">Существуют различные сценарии, где использование **Measure Max()** и **Measure Min()** имеет смысл.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="8f2f2-288">Однако поскольку каждая функция является противоположностью другой, мы опишем Max(), а с Min() вы сможете поэкспериментировать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="8f2f2-289">При запросе событий системы безопасности они имеют свойство **Level**, которое может изменяться.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="8f2f2-290">Например:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-290">For example:</span></span>

```
Type=SecurityEvent
```

![начало поиска с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="8f2f2-292">Если вы хотите просмотреть наибольшее значение для всех событий системы безопасности, которым назначено общее поле Computer, с группировкой по полю, можно использовать следующий код:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-292">If you want to view the highest value for all of the security events given a common Computer, the group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![поиск с помощью measure max по computer](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="8f2f2-294">Он покажет, что большинство компьютеров, имевших записи **Level**, имеют по крайней мере уровень 8, а многие из них — уровень 16.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-294">It will display that for the computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![поиск с помощью measure max для времени создания по computer](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="8f2f2-296">Эта функция хорошо работает с числами, однако она также работает с полями типа DateTime.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="8f2f2-297">Это полезно, когда требуется проверить самую последнюю или недавнюю метку времени для любого фрагмента данных, индексируемых для каждого компьютера.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-297">It is useful to check for the last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="8f2f2-298">Например, когда поступило сообщение о последнем событии системы безопасности для каждого компьютера?</span><span class="sxs-lookup"><span data-stu-id="8f2f2-298">For example: When was the most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-the-avg-function-with-the-measure-command"></a><span data-ttu-id="8f2f2-299">использование функции avg с командой measure;</span><span class="sxs-lookup"><span data-stu-id="8f2f2-299">Use the avg function with the measure command</span></span>
<span data-ttu-id="8f2f2-300">Статистическая функция Avg(), используемая с командой measure, позволяет вычислить среднее значение для некоторого поля, группируя результаты по тому же или другому полю.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-300">The Avg() statistical function used with measure allows you to calculate the average value for some field, and group results by the same or other field.</span></span> <span data-ttu-id="8f2f2-301">Это оказывается полезным в самых различных случаях, например в случае с данными о производительности.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="8f2f2-302">Мы начнем с данных о производительности.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-302">We'll start with performance data.</span></span> <span data-ttu-id="8f2f2-303">Обратите внимание, что OMS в настоящее время собирает счетчики производительности для машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="8f2f2-304">Самый простой запрос для поиска *всех* данных о производительности имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-304">To search for *all* performance data, the most basic query is:</span></span>

```
Type=Perf
```

![начало поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="8f2f2-306">Первое, что вы заметите, — это то, что в Log Analytics отображаются три представления: список, который содержит фактические записи, лежащие в основе диаграмм, таблица, которая показывает табличное представление данных счетчика производительности, и метрики, которые отображают графики для счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-306">The first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows the actual records behind the charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for the performance counters.</span></span>

<span data-ttu-id="8f2f2-307">На рисунке выше помечено два набора полей, которые обозначают следующее.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-307">In the image above, there are two sets of fields marked that indicate the following:</span></span>

* <span data-ttu-id="8f2f2-308">Первый набор определяет имя счетчика производительности Windows, имя объекта и имя экземпляра в фильтре запроса.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-308">The first set identifies Windows Performance Counter Name, Object Name, and Instance Name in the query filter.</span></span> <span data-ttu-id="8f2f2-309">Это поля, которые вы, вероятно, будете использовать в качестве аспектов и фильтров чаще всего.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-309">These are the fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="8f2f2-310">**CounterValue** — это фактическое значение счетчика.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-310">**CounterValue** is the actual value of the counter.</span></span> <span data-ttu-id="8f2f2-311">В этом примере используется значение *75*.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-311">In this example, the value is *75*.</span></span>
* <span data-ttu-id="8f2f2-312">**TimeGenerated** имеет значение 12:51 в 24-часовом формате.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="8f2f2-313">Ниже приводится представление метрик на графике.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-313">Here's a view of the metrics in a graph.</span></span>

![начало поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="8f2f2-315">После ознакомления с формой записи Perf и другими методиками поиска вы сможете использовать функцию measure Avg() для статистической обработки числовых данных этого типа.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-315">After reading about the Perf record shape, and having read about other search techniques, you can use measure Avg() to aggregate this type of numerical data.</span></span>

<span data-ttu-id="8f2f2-316">Ниже приведен простой пример.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![поиска с помощью avg по samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="8f2f2-318">В этом примере вы выбираете счетчик производительности CPU Total Time (Общее время ЦП) и получаете среднее значение по полю Computer.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-318">In this example, you select the CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="8f2f2-319">Если требуется ограничить результаты, например отображать данные только за последние 6 часов, можно использовать элемент управления фильтра времени или включить это условие в запрос следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-319">If you want to narrow down your results to only the last 6 hours, you can either use the time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="to-search-using-the-avg-function-with-the-measure-command"></a><span data-ttu-id="8f2f2-320">Поиска с использованием функции avg с командой measure</span><span class="sxs-lookup"><span data-stu-id="8f2f2-320">To search using the avg function with the measure command</span></span>
* <span data-ttu-id="8f2f2-321">В поле поиска введите `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-321">In the Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="8f2f2-322">Можно объединять и сопоставлять данные *по* разным компьютерам.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="8f2f2-323">Например, предположим, что имеется набор узлов в некоторой ферме, где каждый узел совпадает с любым другим узлом и они выполняют одинаковую работу, а также требуется грубая балансировка нагрузки.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal to any other one and they just do all the same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="8f2f2-324">Вы можете собрать все счетчики за один проход с помощью следующего запроса и получить средние значения для всей фермы.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-324">You could get their counters all in one go with the following query and get averages for the entire farm.</span></span> <span data-ttu-id="8f2f2-325">Для начала можно выбрать компьютеры, используя следующий пример:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-325">You can start by choosing the computers with the following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="8f2f2-326">Теперь, когда вы получили компьютеры, вам требуется выбрать всего два ключевых показателя эффективности (KPI): "% CPU Usage" (% загрузки ЦП) и "% Free Disk Space" (% свободного места на диске).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-326">Now that you have the computers, you also only want to select two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="8f2f2-327">Таким образом, запрос принимает следующий вид:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-327">So, that part of the query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="8f2f2-328">Теперь можно добавить компьютеры и счетчики, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-328">Now you can add computers and counters with the following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="8f2f2-329">Благодаря выбору конкретных элементов команда **measure Avg()** позволяет возвратить среднее значение не для компьютера, а для всей фермы путем группирования по CounterName.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-329">Because you have a very specific selection, the **measure Avg()** command can return the average not by computer, but across the farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="8f2f2-330">Например:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="8f2f2-331">Это позволяет получить удобное компактное представление с парой ключевых показателей эффективности вашей среды.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![группировка поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="8f2f2-333">На панели мониторинга можно использовать поисковый запрос.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-333">You can easily use the search query in a dashboard.</span></span> <span data-ttu-id="8f2f2-334">Например, можно сохранить поисковый запрос и создать на его основе панель мониторинга *Web Farm KPIs* (Ключевые показатели эффективности веб-фермы).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-334">For example, you could save the search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="8f2f2-335">Дополнительные сведения об использовании панелей мониторинга см. в статье [Создание пользовательской панели мониторинга в Log Analytics](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-335">To learn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![панель мониторинга поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-the-sum-function-with-the-measure-command"></a><span data-ttu-id="8f2f2-337">Использование функции sum с командой measure</span><span class="sxs-lookup"><span data-stu-id="8f2f2-337">Use the sum function with the measure command</span></span>
<span data-ttu-id="8f2f2-338">Функция sum аналогична другим функциям команды measure.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-338">The sum function is similar to other functions of the measure command.</span></span> <span data-ttu-id="8f2f2-339">Пример использования функции sum см. в разделе [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx) (Поиск в журналах W3C IIS в компоненте оперативной аналитики Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-339">You can see an example about how to use the sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="8f2f2-340">Функции Max() и Min() можно использовать с числами, датой и временем, а также с текстовыми строками.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="8f2f2-341">Текстовые строки сортируются в алфавитном порядке, и вы получаете первую и последнюю сроку.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="8f2f2-342">Однако функцию Sum() можно использовать только с числовыми полями.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="8f2f2-343">Это также касается и функции Avg().</span><span class="sxs-lookup"><span data-stu-id="8f2f2-343">This also applies to Avg().</span></span>

### <a name="use-the-percentile-function-with-the-measure-command"></a><span data-ttu-id="8f2f2-344">Использование функции percentile с командой measure</span><span class="sxs-lookup"><span data-stu-id="8f2f2-344">Use the percentile function with the measure command</span></span>
<span data-ttu-id="8f2f2-345">Функция вычисления процентиля используется так же, как Avg() и Sum(), то есть только для числовых полей.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-345">The percentile function is similar to Avg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="8f2f2-346">Для числового поля можно применить любой процентиль в диапазоне от 1 до 99.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-346">You can use any percentile between 1 to 99 on a numeric field.</span></span> <span data-ttu-id="8f2f2-347">Можно использовать оба варианта команды: **percentile** и **pct**.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="8f2f2-348">Рассмотрим несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-the-where-command"></a><span data-ttu-id="8f2f2-349">использование команды where.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-349">Use the where command</span></span>
<span data-ttu-id="8f2f2-350">Команда where работает как фильтр, но ее можно применить в конвейере для дальнейшей фильтрации сводных результатов, полученных с помощью команды Measure, в отличие от необработанных результатов, которые фильтруются в начале запроса.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-350">The where command works like a filter, but it can be applied in the pipeline to further filter aggregated results that have been produced by a Measure command – as opposed to raw results that are filtered at the beginning of a query.</span></span>

<span data-ttu-id="8f2f2-351">Например:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="8f2f2-352">Можно добавить еще один символ вертикальной черты "|" и команду WHERE, чтобы выбрать только те компьютеры, на которых средняя загрузка ЦП превышает 80 %, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-352">You can add another pipe "|" character and the Where command to only get computers whose average CPU is above 80%, with the following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="8f2f2-353">Если вы знакомы с Microsoft System Center Operations Manager, команду where можно определить в терминах пакета управления.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of the where command in management pack terms.</span></span> <span data-ttu-id="8f2f2-354">Если бы данный пример являлся правилом, первая часть запроса была бы источником данных, а команда where была бы определением условия.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-354">If the example were a rule, the first part of the query would be the data source and the where command would be the condition detection.</span></span>

<span data-ttu-id="8f2f2-355">Этот запрос можно использовать в качестве плитки в окне **Моя панель мониторинга**, позволяющей отслеживать чрезмерную загрузку ЦП компьютера.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-355">You can use the query as a tile in **My Dashboard**, as a monitor of sorts, to see when computer CPUs are over-utilized.</span></span> <span data-ttu-id="8f2f2-356">Дополнительные сведения о панелях мониторинга см. в статье [Создание пользовательской панели мониторинга в Log Analytics](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-356">To learn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="8f2f2-357">Вы также можете создавать и использовать панели мониторинга с помощью мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-357">You can also create and use dashboards using the mobile app.</span></span> <span data-ttu-id="8f2f2-358">Дополнительные сведения вы найдете в описании [мобильного приложения OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="8f2f2-359">На двух нижних плитках на следующем изображении представлен монитор, отображающий список и число.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-359">In the bottom two tiles of the following image, you can see the monitor displayed a list and as a number.</span></span> <span data-ttu-id="8f2f2-360">В большинстве случаев желательно, чтобы это число было равным нулю, а список был пуст.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-360">Essentially, you always want the number to be zero and the list to be empty.</span></span> <span data-ttu-id="8f2f2-361">Иное состояние указывает на наличие условия предупреждения.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="8f2f2-362">При необходимости его можно использовать для просмотра компьютеров с высокой загрузкой.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-362">If needed, you can use it to take a look at which machines are under pressure.</span></span>

![панель мониторинга на мобильном устройстве](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-the-in-operator"></a><span data-ttu-id="8f2f2-364">Использование оператора IN</span><span class="sxs-lookup"><span data-stu-id="8f2f2-364">Use the in operator</span></span>
<span data-ttu-id="8f2f2-365">Оператор *IN* и противоположный ему оператор *NOT IN* позволяют использовать вложенный поиск, то есть передавать результаты поиска в качестве аргумента в другой поисковый запрос.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-365">The *IN* operator, along with *NOT IN* allows you to use subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="8f2f2-366">Такой поисковый запрос заключается в фигурные скобки {} внутри другого поискового запроса, который называется *основным* или *внешним*.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="8f2f2-367">Результат вложенного поискового запроса, обычно представленный в виде списка значений, используется как аргумент в основном поисковом запросе.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-367">The result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="8f2f2-368">Вложенный поисковый запрос удобно использовать для сопоставления подмножества данных, которое невозможно описать непосредственно в выражении поиска, но можно получить с помощью поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-368">You can use subsearches to match subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="8f2f2-369">Например, если вы хотите найти все события, поступившие от *компьютеров, на которых не установлены обновления безопасности*, то сначала нужно составить вложенный поисковый запрос, который определит все *компьютеры, на которых не установлены обновления безопасности*, а затем выполнить поиск событий на этих узлах.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-369">For example, if you’re interested in using one search to find all events from *computers missing security updates*, then you need to design a subsearch that first identifies that *computers missing security updates* before it finds events belonging to those hosts.</span></span>

<span data-ttu-id="8f2f2-370">Составить список всех *компьютеров, на которых не установлены обновления безопасности* , можно с помощью такого запроса:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-370">So, you could express *computers currently missing required security updates* with the following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="8f2f2-372">Теперь вы получили нужный список и можете использовать созданный запрос как внутренний поиск для передачи этого списка компьютеров во внешний (основной) поисковый запрос, который будет искать события для этих компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-372">Once you have the list, you can use the search as an inner search to feed the list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="8f2f2-373">Для этого внутренний поиск заключается в фигурные скобки, а его результаты передаются во внешний поиск в качестве допустимых значений определенного фильтра (поля) с помощью оператора IN.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-373">You do this by enclosing the inner search in braces and feeding its results as possible values for a filter/field in the outer search using the IN operator.</span></span> <span data-ttu-id="8f2f2-374">Запрос будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-374">The query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="8f2f2-376">Обратите особое внимание на фильтр времени во внутреннем поисковом запросе. Он нужен потому, что компонент оценки системных обновлений создает моментальный снимок всех компьютеров каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-376">Also notice the time filter used in the inner search because the System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="8f2f2-377">Внутренний запрос будет более легким и точным, если выполнять поиск только за один день.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-377">You can make the inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="8f2f2-378">Во внешнем же поиске используется параметр выбора времени, установленный в пользовательском интерфейсе, то есть события отбираются за последние 7 дней.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-378">The outer search instead uses the time selection in the user interface, retrieving events from the last 7 days.</span></span> <span data-ttu-id="8f2f2-379">Подробные сведения об операторах времени см. в разделе [Логические операторы](#boolean-operators).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="8f2f2-380">Результаты внутреннего поиска используются только в качестве фильтра для внешнего поиска, поэтому сохраняется возможность использовать для внешнего поиска дополнительные команды.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-380">Because you really only use the results of the inner search as a filter value for the outer one, you can still apply commands in the outer search.</span></span> <span data-ttu-id="8f2f2-381">Например, полученные выше события можно сгруппировать с помощью другой команды measure:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-381">For example, you can still group the above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="8f2f2-383">Обычно требуется, чтобы внутренний запрос выполнялся быстро, так как Log Analytics устанавливает на стороне службы ограничения на время ожидания. Также важно, чтобы количество возвращаемых результатов было небольшим.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-383">Generally, you want your inner query to execute quickly because Log Analytics has service-side timeouts for it and also to return a small amount of results.</span></span> <span data-ttu-id="8f2f2-384">Если внутренний запрос возвращает много результатов, этот список будет обрезан и в итоге результаты внешнего поиска могут быть неправильными.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-384">If the inner query returns more results, the result list gets truncated, which could potentially cause the outer search to return incorrect results.</span></span>

<span data-ttu-id="8f2f2-385">Еще одно правило, которое действует в отношении внутреннего поиска: он должен возвращать *агрегированные* результаты.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-385">Another rule is that the inner search currently needs to provide *aggregated* results.</span></span> <span data-ttu-id="8f2f2-386">Другими словами, в нем должна содержаться команда *measure*. Необработанные результаты пока нельзя передавать во внешний поиск.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="8f2f2-387">Кроме того, в нем может существовать только один оператор IN, и он должен быть последним фильтром в запросе.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-387">Also, there can be only one IN operator and it must be the last filter in the query.</span></span> <span data-ttu-id="8f2f2-388">Не допускается объединение нескольких операторов IN с помощью OR. Таким образом, невозможно создать цепочку внутренних поисков — для каждого внешнего поиска возможен только один внутренний поиск.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: the important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="8f2f2-389">Но даже с учетом этих ограничений оператор IN позволяет выполнять множество видов связанных поисков, а также создавать своего рода группы (компьютеров, пользователей, файлов и т. п., в зависимости от содержимого ваших данных).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-389">Even with these limits, IN enables many kinds of correlated searches, and allows you to define something similar to groups such as computers, users, or files – whatever the fields in your data contain.</span></span> <span data-ttu-id="8f2f2-390">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-390">Here are more examples:</span></span>

<span data-ttu-id="8f2f2-391">**Все обновления, отсутствующие на компьютерах, где отключен параметр автоматического обновления.**</span><span class="sxs-lookup"><span data-stu-id="8f2f2-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="8f2f2-392">**Все события ошибок для компьютеров, на которых работает SQL Server (то есть тех, где выполнялась оценка SQL).**</span><span class="sxs-lookup"><span data-stu-id="8f2f2-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="8f2f2-393">**Все события безопасности для компьютеров, являющихся контроллерами домена (то есть тех, где выполнялась оценка AD).**</span><span class="sxs-lookup"><span data-stu-id="8f2f2-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="8f2f2-394">**С какими еще учетными записями выполнялся вход на те компьютеры, на которых использовалась учетная запись BACONLAND\jochan?**</span><span class="sxs-lookup"><span data-stu-id="8f2f2-394">**Which other accounts have logged on to the same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-the-distinct-command"></a><span data-ttu-id="8f2f2-395">Использование команды distinct</span><span class="sxs-lookup"><span data-stu-id="8f2f2-395">Use the distinct command</span></span>
<span data-ttu-id="8f2f2-396">Эта команда позволяет получить список уникальных значений для поля.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-396">As the name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="8f2f2-397">Несмотря на простоту команды, она весьма полезна.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="8f2f2-398">Аналогичные результаты можно получить с помощью команды measure count(), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-398">The same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![пример команды поиска DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="8f2f2-400">Но если вам нужен только список уникальных значений, а не число документов с каждым из этих значений, команда DISTINCT будет более правильным выбором. Она предоставляет более простой и понятный формат вывода, а также использует более короткий синтаксис, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-400">However, if all you're interested in is just a list of distinct values and not the count of documents that have that values, then DISTINCT can provide cleaner and easier to read output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![пример команды поиска DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-the-countdistinct-function-with-the-measure-command"></a><span data-ttu-id="8f2f2-402">Использование функции countdistinct с командой measure</span><span class="sxs-lookup"><span data-stu-id="8f2f2-402">Use the countdistinct function with the measure command</span></span>
<span data-ttu-id="8f2f2-403">Функция countdistinct подсчитывает количество уникальных значений в каждой группе.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-403">The countdistinct function counts the number of distinct values within each group.</span></span> <span data-ttu-id="8f2f2-404">Например, так можно подсчитать число уникальных компьютеров, создающих отчеты каждого типа.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-404">For example, it could be used to count the number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-the-measure-interval-command"></a><span data-ttu-id="8f2f2-406">Использование команды measure interval</span><span class="sxs-lookup"><span data-stu-id="8f2f2-406">Use the measure interval command</span></span>
<span data-ttu-id="8f2f2-407">Log Analytics собирает данные практически в режиме реального времени, что позволяет собирать и наглядно отображать почти любой счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="8f2f2-408">Просто введите запрос **Type: Perf** , и вы получите тысячи диаграмм для метрик в зависимости от числа счетчиков и серверов в вашей среде Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-408">Simply entering the query **Type:Perf** will return thousands of metric graphs based on the number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="8f2f2-409">Агрегирование метрик по требованию позволяет получить высокоуровневую оценку метрик в вашей среде или более подробно изучить наиболее интересные данные.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-409">With on-demand metric aggregation, you can look at the overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="8f2f2-410">Предположим, вы хотите узнать среднюю загрузку ЦП на всех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-410">Let’s say that you want to know what is the average CPU across all your computers.</span></span> <span data-ttu-id="8f2f2-411">Изучение средних значений загрузки ЦП для каждого компьютера не всегда будет полезным, так как эти результаты сглаживаются.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-411">Looking at the average CPU for every computer might not be helpful because results may get smoothed out.</span></span> <span data-ttu-id="8f2f2-412">Чтобы изучить вопрос более подробно, вы можете объединить информацию за более короткие отрезки времени, а затем изучить эту последовательность в различных представлениях.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-412">To look into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="8f2f2-413">Например, так вы можете получить почасовую оценку средней загрузки ЦП по всем компьютерам:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-413">For example, you can perform the hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![measure average interval](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="8f2f2-415">По умолчанию эти результаты будут отображаться в виде интерактивного графика с несколькими рядами данных.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-415">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="8f2f2-416">Этот график поддерживает переключение рядов (с масштабированием по оси y), масштабирование и подсказки при наведении указателя мыши.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-416">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="8f2f2-417">При необходимости вы всегда можете отобразить необработанные данные в табличном виде.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-417">The table display option is still available for viewing the raw data if necessary.</span></span>

<span data-ttu-id="8f2f2-418">Также можно сгруппировать результаты по другим полям.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-418">You can also group by other fields.</span></span> <span data-ttu-id="8f2f2-419">В этом примере мы получаем все процентные счетчики для одного конкретного компьютера и отбираем почасовые 70-е процентили по каждому счетчику.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-419">In this example, I am looking at all the % counters for one specific computer, and I want to know what is the hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="8f2f2-420">Следует заметить, что такие запросы возможны не только для счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-420">One thing to note is that these queries are not limited to performance counters.</span></span> <span data-ttu-id="8f2f2-421">Их можно применить к любой метрике.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-421">You can apply them to any metric.</span></span> <span data-ttu-id="8f2f2-422">В этом примере выполняется просмотр журналов W3C IIS.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-422">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="8f2f2-423">Мы хотим узнать максимальное время, затрачиваемое на обработку каждого запроса за 5-минутные интервалы.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-423">I want to know what is the maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="8f2f2-424">Использование нескольких статистических выражений в одном запросе</span><span class="sxs-lookup"><span data-stu-id="8f2f2-424">Use multiple aggregates in one query</span></span>
<span data-ttu-id="8f2f2-425">Для команды measure можно указать несколько статистических выражений.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-425">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="8f2f2-426">Каждому из них можно присвоить отдельный псевдоним.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-426">Each one can be aliased independently.</span></span>  <span data-ttu-id="8f2f2-427">Если вы не укажете псевдоним, в качестве имени итогового столбца будет использоваться имя соответствующей статистической функции (например, avg(CounterValue) для функции avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-427">If it is not given an alias the resulting field name will be the aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="8f2f2-429">Вот еще один пример:</span><span class="sxs-lookup"><span data-stu-id="8f2f2-429">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="8f2f2-430">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f2f2-430">Next steps</span></span>
<span data-ttu-id="8f2f2-431">Дополнительные сведения о поиске по журналам можно получить в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="8f2f2-431">For additional information about log searches, see:</span></span>

* <span data-ttu-id="8f2f2-432">Чтобы расширить возможности поиска по журналам, см. статью [Настраиваемые поля в службе Log Analytics](log-analytics-custom-fields.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-432">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
* <span data-ttu-id="8f2f2-433">Полный список полей и аспектов для поиска, доступных в Log Analytics, см. в [справочнике по поиску в журналах Log Analytics](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8f2f2-433">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>
