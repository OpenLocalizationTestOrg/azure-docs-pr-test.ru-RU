---
title: "Использование портала поиска по журналам в Azure Log Analytics | Документация Майкрософт"
description: "Эта статья содержит руководство, в котором описывается, как создать поиски по журналам и анализировать данные, хранящиеся в рабочей области Log Analytics, с помощью портала поиска по журналам.  Это руководство включает в себя выполнение некоторых простых запросов с целью возврата различных типов данных и анализа результатов."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 6fc556ceb34cde26d5f3789a2397cdaa34b0b84d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="30877-104">Создание поисков по журналам в Azure Log Analytics с помощью портала поиска по журналам</span><span class="sxs-lookup"><span data-stu-id="30877-104">Create log searches in Azure Log Analytics using the Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="30877-105">В этой статье описываются портал поиска по журналам в Azure Log Analytics с использованием нового языка запросов.</span><span class="sxs-lookup"><span data-stu-id="30877-105">This article describes the Log Search portal in Azure Log Analytics using the new query language.</span></span>  <span data-ttu-id="30877-106">Дополнительные сведения о новом языке и процедурах обновления рабочей области см. в [этой статье](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="30877-106">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="30877-107">Если вы еще не перевели рабочую область на новый язык запросов, используйте информацию из статьи [Поиск данных по журналам](log-analytics-log-searches.md), чтобы узнать текущую версию портала поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="30877-107">If your workspace hasn't been upgraded to the new query language, you should refer to [Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on the current version of the Log Search portal.</span></span>

<span data-ttu-id="30877-108">Эта статья содержит руководство, в котором описывается, как создать поиски по журналам и анализировать данные, хранящиеся в рабочей области Log Analytics, с помощью портала поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="30877-108">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="30877-109">Это руководство включает в себя выполнение некоторых простых запросов с целью возврата различных типов данных и анализа результатов.</span><span class="sxs-lookup"><span data-stu-id="30877-109">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="30877-110">Здесь рассматривается изменение запроса с помощью функций на портале поиска по журналам, а не напрямую.</span><span class="sxs-lookup"><span data-stu-id="30877-110">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="30877-111">Дополнительные сведения об изменении запроса напрямую см. в [справочнике по языку запросов](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="30877-111">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="30877-112">Чтобы создать поиски на портале расширенной аналитики, а не на портале поиска по журналам, ознакомьтесь со статьей [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587) (Начало работы с порталом аналитики).</span><span class="sxs-lookup"><span data-stu-id="30877-112">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="30877-113">Оба портала используют тот же язык запросов для доступа к одним и тем же данным в рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="30877-113">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30877-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="30877-114">Prerequisites</span></span>
<span data-ttu-id="30877-115">Это руководство предполагает наличие рабочей области Log Analytics с хотя бы одним подключенным источником, который генерирует данные для анализа запросов.</span><span class="sxs-lookup"><span data-stu-id="30877-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="30877-116">Если у вас нет рабочей области, вы можете создать ее бесплатно, выполнив действия, описанные в статье [Начало работы с рабочей областью Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="30877-116">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="30877-117">Подключите хотя бы один агент [Windows](log-analytics-windows-agents.md) или [Linux](log-analytics-linux-agents.md) к рабочей области.</span><span class="sxs-lookup"><span data-stu-id="30877-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="30877-118">Открытие портала поиска по журналам</span><span class="sxs-lookup"><span data-stu-id="30877-118">Open the Log Search portal</span></span>
<span data-ttu-id="30877-119">Откройте портал поиска по журналам, используя</span><span class="sxs-lookup"><span data-stu-id="30877-119">Start by opening the Log Search portal.</span></span>  <span data-ttu-id="30877-120">портал Azure или портал OMS.</span><span class="sxs-lookup"><span data-stu-id="30877-120">You can access it in either the Azure portal or the OMS portal.</span></span>

1. <span data-ttu-id="30877-121">Перейдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30877-121">Open the Azure portal.</span></span>
2. <span data-ttu-id="30877-122">Перейдите к Log Analytics и выберите рабочую область.</span><span class="sxs-lookup"><span data-stu-id="30877-122">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="30877-123">Выберите **Поиск по журналу**, чтобы остаться на портале Azure или запустите портал OMS, выбрав **Портал OMS** и нажав кнопку "Поиск по журналу".</span><span class="sxs-lookup"><span data-stu-id="30877-123">Either select **Log Search** to stay in the Azure portal or launch the OMS portal by selecting **OMS Portal** and then clicking the Log Search button.</span></span>

![Кнопка поиска по журналу](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="30877-125">Создание простого поиска</span><span class="sxs-lookup"><span data-stu-id="30877-125">Create a simple search</span></span>
<span data-ttu-id="30877-126">Самый быстрый способ получить некоторые данные для работы — создать простой запрос, который возвращает все записи в таблице.</span><span class="sxs-lookup"><span data-stu-id="30877-126">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="30877-127">Если у вас есть клиенты Windows или Linux, подключенные к рабочей области, у вас будут данные в таблице событий (Windows) или таблице системного журнала (Linux).</span><span class="sxs-lookup"><span data-stu-id="30877-127">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="30877-128">Введите один из следующих запросов в поле поиска и нажмите кнопку поиска.</span><span class="sxs-lookup"><span data-stu-id="30877-128">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="30877-129">Данные возвращаются в представлении списка по умолчанию. Вы можете просмотреть общее количество возвращенных записей.</span><span class="sxs-lookup"><span data-stu-id="30877-129">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Простой запрос](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="30877-131">Отображаются только первые несколько свойств каждой записи.</span><span class="sxs-lookup"><span data-stu-id="30877-131">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="30877-132">Щелкните **Показать больше**, чтобы отобразить все свойства конкретной записи.</span><span class="sxs-lookup"><span data-stu-id="30877-132">Click **show more** to display all properties for a particular record.</span></span>

![Сведения о записи](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="30877-134">Задание промежутка времени</span><span class="sxs-lookup"><span data-stu-id="30877-134">Set the time scope</span></span>
<span data-ttu-id="30877-135">Все записи, собранные Log Analytics, имеют свойство **TimeGenerated**, содержащее дату и время создания записи.</span><span class="sxs-lookup"><span data-stu-id="30877-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="30877-136">Запрос на портале поиска по журналам возвращает только записи со свойством **TimeGenerated** за промежуток времени, отображаемый в левой области экрана.</span><span class="sxs-lookup"><span data-stu-id="30877-136">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="30877-137">Фильтр времени можно изменить, выбрав раскрывающий список или переместив ползунок.</span><span class="sxs-lookup"><span data-stu-id="30877-137">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="30877-138">С помощью ползунка можно отобразить гистограмму, на которой показано относительное количество записей для каждого промежутка времени в диапазоне.</span><span class="sxs-lookup"><span data-stu-id="30877-138">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="30877-139">Этот промежуток варьируется в зависимости от диапазона.</span><span class="sxs-lookup"><span data-stu-id="30877-139">This segment will vary depending on the range.</span></span>

<span data-ttu-id="30877-140">Промежуток времени по умолчанию составляет **1 день**.</span><span class="sxs-lookup"><span data-stu-id="30877-140">The default time scope is **1 day**.</span></span>  <span data-ttu-id="30877-141">Измените это значение на **7 дней**, и общее число записей должно увеличиться.</span><span class="sxs-lookup"><span data-stu-id="30877-141">Change this value to **7 days**, and the total number of records should increase.</span></span>

![Промежуток времени создания данных](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="30877-143">Фильтрация результатов запроса</span><span class="sxs-lookup"><span data-stu-id="30877-143">Filter results of the query</span></span>
<span data-ttu-id="30877-144">В левой области экрана расположена панель фильтров, которая позволяет добавить фильтрацию к запросу, не изменяя его напрямую.</span><span class="sxs-lookup"><span data-stu-id="30877-144">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="30877-145">Несколько свойств возвращаемых записей отображаются с 10 основными значениями с количеством записей.</span><span class="sxs-lookup"><span data-stu-id="30877-145">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="30877-146">При работе с **событиями** установите флажок рядом с **Ошибка** в разделе **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="30877-146">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="30877-147">Если вы работаете с **системным журналом**, установите флажок рядом с **Ошибка** в разделе **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="30877-147">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="30877-148">Это позволит изменить запрос на один из указанных ниже, чтобы ограничить результаты событиями ошибки.</span><span class="sxs-lookup"><span data-stu-id="30877-148">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Фильтр](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="30877-150">Добавьте свойства на панель фильтров, выбрав **Добавить в фильтры** в меню свойств одной из записей.</span><span class="sxs-lookup"><span data-stu-id="30877-150">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Меню добавления в фильтры](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="30877-152">Вы можете задать тот же фильтр, выбрав **Фильтр** в меню свойств записи со значением, которое необходимо отфильтровать.</span><span class="sxs-lookup"><span data-stu-id="30877-152">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="30877-153">Для свойств, имена которых выделены синим цветом, доступен только параметр **Фильтр**.</span><span class="sxs-lookup"><span data-stu-id="30877-153">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="30877-154">Это *доступные для поиска* поля, индексируемые для условий поиска.</span><span class="sxs-lookup"><span data-stu-id="30877-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="30877-155">Поля, выделенные серым цветом, — это поля *с возможностью поиска произвольного текста*, имеющие только параметр **Показать ссылки**.</span><span class="sxs-lookup"><span data-stu-id="30877-155">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="30877-156">Этот параметр возвращает записи, имеющие это значение в любом свойстве.</span><span class="sxs-lookup"><span data-stu-id="30877-156">This option returns records that have that value in any property.</span></span>

![Меню фильтра](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="30877-158">Вы можете группировать результаты по одному свойству, выбрав параметр **Группировать по** в меню записи.</span><span class="sxs-lookup"><span data-stu-id="30877-158">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="30877-159">Это позволит добавить оператор [суммирования](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) к запросу, который отображает результаты на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="30877-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="30877-160">Вы можете сгруппировать по нескольким свойствам, однако необходимо будет изменить запрос напрямую.</span><span class="sxs-lookup"><span data-stu-id="30877-160">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="30877-161">Выберите меню записи рядом со свойством **Компьютер** и выберите **Group by 'Computer'** (Группировать по компьютеру).</span><span class="sxs-lookup"><span data-stu-id="30877-161">Select the record menu next the the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Группировка по компьютеру](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="30877-163">Работа с результатами</span><span class="sxs-lookup"><span data-stu-id="30877-163">Work with results</span></span>
<span data-ttu-id="30877-164">Портал поиска по журналам имеет множество функций для работы с результатами запроса.</span><span class="sxs-lookup"><span data-stu-id="30877-164">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="30877-165">Вы можете сортировать, фильтровать и группировать результаты, чтобы анализировать данные, не изменяя фактический запрос.</span><span class="sxs-lookup"><span data-stu-id="30877-165">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="30877-166">По умолчанию результаты запроса не сортируются.</span><span class="sxs-lookup"><span data-stu-id="30877-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="30877-167">Чтобы просмотреть данные в табличном представлении, которое предоставляет дополнительные параметры для фильтрации и сортировки, щелкните **Таблица**.</span><span class="sxs-lookup"><span data-stu-id="30877-167">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Табличное представление](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="30877-169">Щелкните стрелку рядом с записью, чтобы просмотреть сведения для этой записи.</span><span class="sxs-lookup"><span data-stu-id="30877-169">Click the arrow by a record to view the details for that record.</span></span>

![Сортировка результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="30877-171">Выполните сортировку по любому полю, щелкнув заголовок соответствующего столбца.</span><span class="sxs-lookup"><span data-stu-id="30877-171">Sort on any field by clicking on its column header.</span></span>

![Сортировка результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="30877-173">Отфильтруйте результаты по определенному значению в столбце с помощью кнопки "Фильтр", а затем укажите условия фильтра.</span><span class="sxs-lookup"><span data-stu-id="30877-173">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Фильтрация результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="30877-175">Сгруппируйте по столбцу, перетащив заголовок соответствующего столбца в верхнюю часть результатов.</span><span class="sxs-lookup"><span data-stu-id="30877-175">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="30877-176">Вы можете сгруппировать по нескольким полям, перетащив несколько столбцов в верхнюю часть результатов.</span><span class="sxs-lookup"><span data-stu-id="30877-176">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Группирование результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="30877-178">Работа с данными о производительности</span><span class="sxs-lookup"><span data-stu-id="30877-178">Work with performance data</span></span>
<span data-ttu-id="30877-179">Данные о производительности для агентов Windows и Linux хранятся в рабочей области Log Analytics в таблице **Производительность**.</span><span class="sxs-lookup"><span data-stu-id="30877-179">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="30877-180">Записи о производительности выглядят как любые другие записи. Мы можем создать простой запрос, который возвращает все записи о производительности, а также события.</span><span class="sxs-lookup"><span data-stu-id="30877-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Данные о производительности](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="30877-182">Возвращать миллионы записей для всех объектов и счетчиков производительности не очень полезно.</span><span class="sxs-lookup"><span data-stu-id="30877-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="30877-183">Вы можете воспользоваться методами, используемыми выше, чтобы отфильтровать данные. Или просто введите указанный ниже запрос непосредственно в поле поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="30877-183">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="30877-184">В результате будут возвращены только записи использования процессора для компьютеров Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="30877-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Использование процессора](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="30877-186">Это ограничивает данные до определенного счетчика, но это не помещает их в особенно удобный формат.</span><span class="sxs-lookup"><span data-stu-id="30877-186">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="30877-187">Данные можно отобразить на графике, однако сначала необходимо сгруппировать их по компьютеру или времени создания.</span><span class="sxs-lookup"><span data-stu-id="30877-187">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="30877-188">Чтобы сгруппировать по нескольким полям, необходимо изменить запрос напрямую следующим образом.</span><span class="sxs-lookup"><span data-stu-id="30877-188">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="30877-189">Для вычисления среднего значения за каждый час используется функция [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) для свойства **CounterValue**.</span><span class="sxs-lookup"><span data-stu-id="30877-189">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Диаграмма данных о производительности](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="30877-191">Теперь, когда данные сгруппированы подходящим образом, их можно отобразить на визуальной диаграмме, добавив оператор [обработки](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator).</span><span class="sxs-lookup"><span data-stu-id="30877-191">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![График](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="30877-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30877-193">Next steps</span></span>

- <span data-ttu-id="30877-194">Дополнительные сведения о языке запросов Log Analytics см. в статье [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079) (Начало работы с порталом аналитики).</span><span class="sxs-lookup"><span data-stu-id="30877-194">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="30877-195">Изучите пошаговое руководство по использованию [портала расширенной аналитики](https://go.microsoft.com/fwlink/?linkid=856587), который позволяет выполнять те же запросы и получать доступ к тем же данным, что и портал поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="30877-195">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>
