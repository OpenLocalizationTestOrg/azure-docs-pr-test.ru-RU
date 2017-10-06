---
title: "Анализ aaaUser, сеансов и событий в Azure Application Insights | Документы Microsoft"
description: "Демографический анализ пользователей веб-приложения."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="e5fe7-103">Анализ пользователей, сеансов и событий в Application Insights</span><span class="sxs-lookup"><span data-stu-id="e5fe7-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="e5fe7-104">Узнайте, когда люди используют ваше веб-приложение, какие страницы им наиболее интересны, где находятся ваши пользователи, какие браузеры и операционные системы они используют.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="e5fe7-105">Анализируйте данные коммерческой телеметрии и телеметрии использования с помощью [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5fe7-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="e5fe7-106">Начало работы</span><span class="sxs-lookup"><span data-stu-id="e5fe7-106">Get started</span></span>

<span data-ttu-id="e5fe7-107">Если вы еще не видите данных hello пользователей, сеансы или колонках события на портале Application Insights hello, [узнать, как tooget к работе со средствами использования hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5fe7-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="e5fe7-108">Средство сегментацию пользователей, сеансы и события Hello</span><span class="sxs-lookup"><span data-stu-id="e5fe7-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="e5fe7-109">Три hello использования колонки используйте hello же средство tooslice и поперечные срезы данных телеметрии из веб-приложения с точки зрения три.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="e5fe7-110">Фильтрацию и разбиение данных hello, который позволяет выявлять дополнительная информация об использовании относительных hello разных страниц и компонентов.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="e5fe7-111">**Инструмент "Пользователи"**. Узнайте, сколько пользователей использует ваше приложение и его компоненты.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="e5fe7-112">Пользователи подсчитываются по анонимным идентификаторам, которые хранятся в файлах cookie браузера.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="e5fe7-113">Отдельный пользователь, использующий разные браузеры или компьютеры, будет учтен как несколько пользователей.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="e5fe7-114">**Инструмент "Сеансы"**. Узнайте, в скольких сеансах действий пользователей участвовали определенные страницы и компоненты приложения.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="e5fe7-115">Сеанс начинает учитываться после получаса бездействия пользователя или непрерывного использования в течение 24 часов.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="e5fe7-116">**Инструмент "События"**. Узнайте, как часто используются определенные страницы и компоненты приложения.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="e5fe7-117">Просмотр страницы учитывается, когда браузер загружает страницу из приложения, если вы [инструментировали ее](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="e5fe7-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="e5fe7-118">Пользовательское событие представляет один экземпляр из-за некоторого события в приложении часто взаимодействие с пользователем, как кнопки, нажмите кнопку или hello завершения некоторых задач.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="e5fe7-119">Вставьте код в приложении слишком[создавать пользовательские события](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="e5fe7-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Инструмент для данных об использовании](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="e5fe7-121">Запросы для определенных пользователей</span><span class="sxs-lookup"><span data-stu-id="e5fe7-121">Querying for Certain Users</span></span> 

<span data-ttu-id="e5fe7-122">Просмотр различных групп пользователей, настраивая параметры запроса hello вверху hello hello пользователей средство:</span><span class="sxs-lookup"><span data-stu-id="e5fe7-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="e5fe7-123">"Которые использовали": выберите пользовательские события и просмотры страниц.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="e5fe7-124">"Во время": выберите диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="e5fe7-125">: Определить, как toobucket hello данных, в течение заданного времени или другое свойство, например браузера или город.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="e5fe7-126">Разбиение по: Выберите свойства, какие данные hello toosplit или сегмента.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="e5fe7-127">Добавьте фильтры: Ограничить hello запрос toocertain пользователей, сеансы или события на основе их свойств, таких как браузер или город.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="e5fe7-128">Сохранение и предоставление отчетов</span><span class="sxs-lookup"><span data-stu-id="e5fe7-128">Saving and sharing reports</span></span> 
<span data-ttu-id="e5fe7-129">Можно сохранить отчеты пользователей, либо закрытым tooyou точно так же, в разделе "Мои отчеты" hello, или общими для всех остальных с toothis доступа ресурс Application Insights в hello раздел общих отчетов.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="e5fe7-130">При сохранении отчета или изменить свойства, выберите toosave «Текущий относительный диапазон времени», отчет будет постоянно обновляются данные, возвращаясь некоторые фиксированный промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="e5fe7-131">Выберите «Текущий абсолютный диапазон времени» toosave фиксированный набор данных отчета.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="e5fe7-132">Следует помнить, что данные в Application Insights сохраняется только 90 дней, поэтому если более чем за 90 дней, прошедших с отчетом с диапазоном абсолютное время был сохранен, будет выведен пустой отчет hello.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="e5fe7-133">Примеры экземпляров</span><span class="sxs-lookup"><span data-stu-id="e5fe7-133">Example instances</span></span>

<span data-ttu-id="e5fe7-134">Hello экземпляров примера в разделе отображаются сведения о небольшое число отдельных пользователей, сеансов и события, которые соответствуют условиям для hello текущего запроса.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="e5fe7-135">Анализ и изучение поведения hello лиц в tooaggregates сложения можно получить представление о том, как фактически используется приложение.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="e5fe7-136">Аналитика</span><span class="sxs-lookup"><span data-stu-id="e5fe7-136">Insights</span></span> 

<span data-ttu-id="e5fe7-137">Боковая панель аналитики Hello показывает больших кластеров пользователей, которые совместно используют общие свойства.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="e5fe7-138">Эти кластеры могут показать неожиданные тенденции в использовании приложения людьми.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="e5fe7-139">Например, если 40% всех hello использования приложения поступают из людей, использующих один компонент.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="e5fe7-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5fe7-140">Next steps</span></span>
- <span data-ttu-id="e5fe7-141">опыт использования tooenable, начать отправку [пользовательские события](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) или [просмотры страниц](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="e5fe7-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="e5fe7-142">При отправке уже, пользовательские события и представления страницы, просмотр hello использования средств toolearn как пользователям использовать эту службу.</span><span class="sxs-lookup"><span data-stu-id="e5fe7-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="e5fe7-143">Воронки</span><span class="sxs-lookup"><span data-stu-id="e5fe7-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="e5fe7-144">Сохранение</span><span class="sxs-lookup"><span data-stu-id="e5fe7-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="e5fe7-145">Средство "Маршруты пользователей"</span><span class="sxs-lookup"><span data-stu-id="e5fe7-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="e5fe7-146">Книги</span><span class="sxs-lookup"><span data-stu-id="e5fe7-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="e5fe7-147">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="e5fe7-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

