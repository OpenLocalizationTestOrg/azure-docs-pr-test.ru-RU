---
title: "портал поиска журналов aaaUsing hello в службе анализа журналов Azure | Документы Microsoft"
description: "Эта статья содержит учебник, в котором описано, как toocreate входа поиск и анализировать данные, хранящиеся в рабочей области аналитики журналов с помощью портала hello поиска журналов.  Hello учебник включает выполнение некоторых простых запросов tooreturn различные типы данных и анализ результатов."
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
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="16ebc-104">Создание запросов поиска журналов в Azure Log Analytics с помощью портала hello поиска журналов</span><span class="sxs-lookup"><span data-stu-id="16ebc-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="16ebc-105">В этой статье описывается hello портала поиска журналов в Azure Log Analytics с помощью hello новый язык запросов.</span><span class="sxs-lookup"><span data-stu-id="16ebc-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="16ebc-106">Можно узнать больше о новом языке hello и получить tooupgrade процедуры hello в рабочей области [обновление поиск журнала toonew рабочей области Azure Log Analytics](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="16ebc-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="16ebc-107">Если в рабочей области не был обновленного toohello новый язык запросов, вы должны обращаться слишком[найти данные с помощью запросов поиска журналов в службе анализа журналов](log-analytics-log-searches.md) сведения о текущей версии hello hello портала поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="16ebc-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="16ebc-108">Эта статья содержит учебник, в котором описано, как toocreate входа поиск и анализировать данные, хранящиеся в рабочей области аналитики журналов с помощью портала hello поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="16ebc-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="16ebc-109">Hello учебник включает выполнение некоторых простых запросов tooreturn различные типы данных и анализ результатов.</span><span class="sxs-lookup"><span data-stu-id="16ebc-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="16ebc-110">Этот раздел посвящен функции hello портала поиска журналов для изменения запроса hello, а не непосредственное изменение.</span><span class="sxs-lookup"><span data-stu-id="16ebc-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="16ebc-111">Для непосредственного редактирования запросов hello подробнее hello [Справочник по языку запросов](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="16ebc-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="16ebc-112">Поиск toocreate hello портале Advanced Analytics вместо hello портала поиска журналов, в разделе [Приступая к работе с портала службы анализа hello](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="16ebc-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="16ebc-113">Использовать оба порталы hello tooaccess языка hello и тех же данных в рабочей области аналитики журналов hello того же запроса.</span><span class="sxs-lookup"><span data-stu-id="16ebc-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16ebc-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="16ebc-114">Prerequisites</span></span>
<span data-ttu-id="16ebc-115">Предполагается наличие рабочей области аналитики журналов с по крайней мере одного подключенного источника, формирует данные для запросов tooanalyze hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="16ebc-116">Если у вас нет рабочей области, можно создать бесплатно с помощью процедуры hello на [приступить к работе с рабочей областью аналитики журналов](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="16ebc-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="16ebc-117">Подключитесь по крайней мере одну [агент Windows](log-analytics-windows-agents.md) или один [агент Linux](log-analytics-linux-agents.md) toohello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="16ebc-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="16ebc-118">Привет открыть портал поиска журналов</span><span class="sxs-lookup"><span data-stu-id="16ebc-118">Open hello Log Search portal</span></span>
<span data-ttu-id="16ebc-119">Сначала откройте портал hello поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="16ebc-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="16ebc-120">Его можно использовать в hello портал Azure или портал OMS hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="16ebc-121">Здравствуйте, откройте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="16ebc-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="16ebc-122">TooLog аналитика перейдите и выберите рабочую область.</span><span class="sxs-lookup"><span data-stu-id="16ebc-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="16ebc-123">Выберите **поиска журналов** toostay в hello Azure portal или запустите hello портал OMS, выбрав **портал OMS** и затем нажать кнопку поиска журналов hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![Кнопка поиска по журналу](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="16ebc-125">Создание простого поиска</span><span class="sxs-lookup"><span data-stu-id="16ebc-125">Create a simple search</span></span>
<span data-ttu-id="16ebc-126">самый быстрый способ tooretrieve Hello toowork некоторых данных с является простой запрос, который возвращает все записи в таблице.</span><span class="sxs-lookup"><span data-stu-id="16ebc-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="16ebc-127">Если у вас есть любой рабочей tooyour подключенных клиентов Windows или Linux, вы получите данные в либо hello событий (Windows) или таблицу Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="16ebc-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="16ebc-128">Введите один hello, следующие запросы в поле поиска hello и нажмите кнопку поиска hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="16ebc-129">Данные возвращаются в виде списка по умолчанию hello и можно увидеть количество записей, были возвращены.</span><span class="sxs-lookup"><span data-stu-id="16ebc-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![Простой запрос](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="16ebc-131">Только hello первый несколькими свойствами каждой записи отображаются.</span><span class="sxs-lookup"><span data-stu-id="16ebc-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="16ebc-132">Нажмите кнопку **Показать больше** toodisplay все свойства для конкретной записи.</span><span class="sxs-lookup"><span data-stu-id="16ebc-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![Сведения о записи](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="16ebc-134">Настройка области времени hello</span><span class="sxs-lookup"><span data-stu-id="16ebc-134">Set hello time scope</span></span>
<span data-ttu-id="16ebc-135">Каждая запись, собранные службой аналитики журналов имеет **TimeGenerated** свойство, которое содержит hello дату и время создания этой записи hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="16ebc-136">Запрос поиска журналов портале hello возвращает только записи с **TimeGenerated** в пределах области hello времени, отображаемого на hello слева от оператора экран приветствия.</span><span class="sxs-lookup"><span data-stu-id="16ebc-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="16ebc-137">Можно изменить фильтр времени hello, выбрав раскрывающийся список hello или изменив ползунок hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="16ebc-138">Hello ползунка выводится Гистограмма, показывающая hello относительное количество записей для каждого сегмента времени в пределах диапазона hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="16ebc-139">Этот сегмент будет зависеть от диапазона hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="16ebc-140">область времени по умолчанию Hello — **1 день**.</span><span class="sxs-lookup"><span data-stu-id="16ebc-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="16ebc-141">Измените это значение слишком**7 дней**, и общее количество записей hello следует увеличить.</span><span class="sxs-lookup"><span data-stu-id="16ebc-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![Промежуток времени создания данных](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="16ebc-143">Фильтровать результаты запроса hello</span><span class="sxs-lookup"><span data-stu-id="16ebc-143">Filter results of hello query</span></span>
<span data-ttu-id="16ebc-144">На hello левой стороны экрана приветствия — панель фильтра hello, позволяющий tooadd фильтрации запроса toohello без непосредственное изменение.</span><span class="sxs-lookup"><span data-stu-id="16ebc-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="16ebc-145">Несколько свойств, возвращаемых записей hello отображаются вместе со значениями десять top с числом записей.</span><span class="sxs-lookup"><span data-stu-id="16ebc-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="16ebc-146">При работе с **событий**, выберите hello флажок и далее слишком**ошибка** под **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="16ebc-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="16ebc-147">При работе с **Syslog**, выберите hello флажок и далее слишком**err** под **УРОВЕНЬ_СЕРЬЕЗНОСТИ_ОШИБКИ**.</span><span class="sxs-lookup"><span data-stu-id="16ebc-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="16ebc-148">При этом изменяется запрос hello tooone из следующих toolimit hello hello результаты tooerror события.</span><span class="sxs-lookup"><span data-stu-id="16ebc-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Фильтр](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="16ebc-150">Добавить свойства toohello фильтр области, выбрав **добавить toofilters** hello свойства меню на одной из записей hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Добавить toofilter меню](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="16ebc-152">Можно задать hello же отфильтровать, выбрав **фильтра** меню свойств hello запись со значением hello требуется toofilter.</span><span class="sxs-lookup"><span data-stu-id="16ebc-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="16ebc-153">Только у вас есть hello **фильтра** параметр для свойства с их именами синим цветом.</span><span class="sxs-lookup"><span data-stu-id="16ebc-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="16ebc-154">Это *доступные для поиска* поля, индексируемые для условий поиска.</span><span class="sxs-lookup"><span data-stu-id="16ebc-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="16ebc-155">Поля серым цветом, *произвольный текст для поиска* поля, имеющие только hello **Показать ссылки** параметр.</span><span class="sxs-lookup"><span data-stu-id="16ebc-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="16ebc-156">Этот параметр возвращает записи, имеющие это значение в любом свойстве.</span><span class="sxs-lookup"><span data-stu-id="16ebc-156">This option returns records that have that value in any property.</span></span>

![Меню фильтра](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="16ebc-158">Результаты hello на одном свойстве можно сгруппировать, нажав кнопку hello **Group by** в меню записи hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="16ebc-159">При этом будет добавлено [суммировать](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) запрос tooyour оператор, который отображает результаты hello в диаграмме.</span><span class="sxs-lookup"><span data-stu-id="16ebc-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="16ebc-160">Можно сгруппировать в несколько свойств, но потребовалось бы tooedit hello запроса напрямую.</span><span class="sxs-lookup"><span data-stu-id="16ebc-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="16ebc-161">Выберите hello записей меню Далее hello hello **компьютера** свойство и выберите **Group by «Компьютер»**.</span><span class="sxs-lookup"><span data-stu-id="16ebc-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![Группировка по компьютеру](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="16ebc-163">Работа с результатами</span><span class="sxs-lookup"><span data-stu-id="16ebc-163">Work with results</span></span>
<span data-ttu-id="16ebc-164">портал поиска журналов Hello имеет множество функций для работы с hello результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="16ebc-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="16ebc-165">Можно сортировать, фильтр и группирование результатов tooanalyze hello данных без изменения настоящего запроса hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="16ebc-166">По умолчанию результаты запроса не сортируются.</span><span class="sxs-lookup"><span data-stu-id="16ebc-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="16ebc-167">tooview hello данных в виде таблицы, которая предоставляет дополнительные параметры для фильтрации и сортировки, щелкните **таблицы**.</span><span class="sxs-lookup"><span data-stu-id="16ebc-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Табличное представление](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="16ebc-169">Нажмите стрелку hello характеристики hello записей tooview для этой записи.</span><span class="sxs-lookup"><span data-stu-id="16ebc-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![Сортировка результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="16ebc-171">Выполните сортировку по любому полю, щелкнув заголовок соответствующего столбца.</span><span class="sxs-lookup"><span data-stu-id="16ebc-171">Sort on any field by clicking on its column header.</span></span>

![Сортировка результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="16ebc-173">Фильтровать результаты hello на конкретное значение в столбце hello, нажав кнопку "Фильтр" hello и предоставляя условие фильтра.</span><span class="sxs-lookup"><span data-stu-id="16ebc-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![Фильтрация результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="16ebc-175">Группировать по столбцу, перетащив его столбца заголовок toohello вверху hello результаты.</span><span class="sxs-lookup"><span data-stu-id="16ebc-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="16ebc-176">Можно группировать по нескольким полям, перетащив верхней toohello несколько столбцов.</span><span class="sxs-lookup"><span data-stu-id="16ebc-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![Группирование результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="16ebc-178">Работа с данными о производительности</span><span class="sxs-lookup"><span data-stu-id="16ebc-178">Work with performance data</span></span>
<span data-ttu-id="16ebc-179">Данные о производительности для Windows и Linux агенты хранится в рабочей области аналитики журналов hello hello **производительности** таблицы.</span><span class="sxs-lookup"><span data-stu-id="16ebc-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="16ebc-180">Записи о производительности выглядят как любые другие записи. Мы можем создать простой запрос, который возвращает все записи о производительности, а также события.</span><span class="sxs-lookup"><span data-stu-id="16ebc-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Данные о производительности](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="16ebc-182">Возвращать миллионы записей для всех объектов и счетчиков производительности не очень полезно.</span><span class="sxs-lookup"><span data-stu-id="16ebc-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="16ebc-183">Запрашивать такие же методы, используемые выше toofilter hello данных или просто ввести следующие hello hello можно использовать непосредственно в поле поиска журнала hello.</span><span class="sxs-lookup"><span data-stu-id="16ebc-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="16ebc-184">В результате будут возвращены только записи использования процессора для компьютеров Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="16ebc-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Использование процессора](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="16ebc-186">Это ограничивает hello данных tooa определенного счетчика, но она по-прежнему не поместить его в форму, которая особенно полезна.</span><span class="sxs-lookup"><span data-stu-id="16ebc-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="16ebc-187">Можно отобразить данные hello в виде графика, но сначала необходимо toogroup его по компьютеру и TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="16ebc-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="16ebc-188">toogroup по нескольким полям необходимо toomodify hello запроса напрямую, поэтому изменение hello запроса toohello следующие.</span><span class="sxs-lookup"><span data-stu-id="16ebc-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="16ebc-189">В этом случае используется hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) функции hello **значения CounterValue** среднее значение свойства toocalculate hello за каждый час.</span><span class="sxs-lookup"><span data-stu-id="16ebc-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Диаграмма данных о производительности](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="16ebc-191">Теперь, когда данные hello подходящим образом группируются, можно отобразить его в visual диаграммы путем добавления hello [визуализации](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) оператор.</span><span class="sxs-lookup"><span data-stu-id="16ebc-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![График](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="16ebc-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16ebc-193">Next steps</span></span>

- <span data-ttu-id="16ebc-194">Дополнительные сведения о языке запросов анализа журналов hello в [Приступая к работе с портала службы анализа hello](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="16ebc-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="16ebc-195">Перемещайтесь учебника при помощи hello [Advanced Analytics портала](https://go.microsoft.com/fwlink/?linkid=856587) позволяющее toorun hello же запросы и доступа hello и тех же данных как портал hello поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="16ebc-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
