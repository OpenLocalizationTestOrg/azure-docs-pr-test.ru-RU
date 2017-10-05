---
title: "Анализ пользователей, сеансов и событий в Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="2d7cc-103">Анализ пользователей, сеансов и событий в Application Insights</span><span class="sxs-lookup"><span data-stu-id="2d7cc-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="2d7cc-104">Узнайте, когда люди используют ваше веб-приложение, какие страницы им наиболее интересны, где находятся ваши пользователи, какие браузеры и операционные системы они используют.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="2d7cc-105">Анализируйте данные коммерческой телеметрии и телеметрии использования с помощью [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d7cc-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="2d7cc-106">Начало работы</span><span class="sxs-lookup"><span data-stu-id="2d7cc-106">Get started</span></span>

<span data-ttu-id="2d7cc-107">Если вы еще не видите данных в колонках "Пользователи", "Сеансы" или "События" на портале Application Insights, [узнайте, как приступить к работе с инструментами для данных об использовании](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d7cc-107">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="2d7cc-108">Инструменты сегментирования "Пользователи", "Сеансы" и "События"</span><span class="sxs-lookup"><span data-stu-id="2d7cc-108">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="2d7cc-109">В трех колонках данных об использовании для анализа данных телеметрии веб-приложения с трех точек зрения используется один и тот же инструмент.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-109">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="2d7cc-110">С помощью фильтрации и разделения данных можно обнаружить дополнительную информацию об относительном использовании различных страниц и компонентов.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-110">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="2d7cc-111">**Инструмент "Пользователи"**. Узнайте, сколько пользователей использует ваше приложение и его компоненты.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="2d7cc-112">Пользователи подсчитываются по анонимным идентификаторам, которые хранятся в файлах cookie браузера.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="2d7cc-113">Отдельный пользователь, использующий разные браузеры или компьютеры, будет учтен как несколько пользователей.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="2d7cc-114">**Инструмент "Сеансы"**. Узнайте, в скольких сеансах действий пользователей участвовали определенные страницы и компоненты приложения.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="2d7cc-115">Сеанс начинает учитываться после получаса бездействия пользователя или непрерывного использования в течение 24 часов.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="2d7cc-116">**Инструмент "События"**. Узнайте, как часто используются определенные страницы и компоненты приложения.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="2d7cc-117">Просмотр страницы учитывается, когда браузер загружает страницу из приложения, если вы [инструментировали ее](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="2d7cc-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="2d7cc-118">Пользовательское событие представляет какое-либо отдельное событие, произошедшее в приложении. Как правило, это взаимодействие с пользователем, например нажатие кнопки, или выполнение какой-либо задачи.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="2d7cc-119">В приложение следует добавить код для [создания пользовательских событий](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="2d7cc-119">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Инструмент для данных об использовании](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="2d7cc-121">Запросы для определенных пользователей</span><span class="sxs-lookup"><span data-stu-id="2d7cc-121">Querying for Certain Users</span></span> 

<span data-ttu-id="2d7cc-122">Изучите различные группы пользователей, настроив параметры запроса в верхней части инструмента "Пользователи".</span><span class="sxs-lookup"><span data-stu-id="2d7cc-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span> 

* <span data-ttu-id="2d7cc-123">"Которые использовали": выберите пользовательские события и просмотры страниц.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="2d7cc-124">"Во время": выберите диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="2d7cc-125">"По": выберите способ сегментирования данных — за период времени или по другому свойству, например браузеру или городу.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-125">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="2d7cc-126">"Разделение по": выберите свойство для разделения или сегментирования данных.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-126">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="2d7cc-127">"Добавить фильтры": уточните запрос, ограничив его определенными пользователями, сеансами или событиями на основе их свойств, таких как браузер или город.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-127">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="2d7cc-128">Сохранение и предоставление отчетов</span><span class="sxs-lookup"><span data-stu-id="2d7cc-128">Saving and sharing reports</span></span> 
<span data-ttu-id="2d7cc-129">Отчеты "Пользователи" можно сохранить как частные, предназначенные только для вас, в разделе "Мои отчеты", или предоставить их всем остальным пользователям, обладающим доступом к ресурсу Application Insights, сохранив в разделе "Shared Reports" (Общие отчеты).</span><span class="sxs-lookup"><span data-stu-id="2d7cc-129">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>  
 
<span data-ttu-id="2d7cc-130">При сохранении отчета или редактировании его свойств выберите "Текущий относительный диапазон времени", чтобы сохранить отчет с постоянно обновляемыми данными за фиксированный период времени.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-130">While saving a report or editing its properties, choose "Current Relative Time Range" to save a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="2d7cc-131">Выберите "Текущий абсолютный диапазон времени", чтобы сохранить отчет с фиксированным набором данных.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-131">Choose "Current Absolute Time Range" to save a report with a fixed set of data.</span></span> <span data-ttu-id="2d7cc-132">Следует помнить, что данные в Application Insights хранятся только 90 дней. Поэтому, если после сохранения отчета с абсолютным диапазоном времени прошло больше 90 дней, он будет отображаться пустым.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, the report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="2d7cc-133">Примеры экземпляров</span><span class="sxs-lookup"><span data-stu-id="2d7cc-133">Example instances</span></span>

<span data-ttu-id="2d7cc-134">В разделе примеров экземпляров отображаются сведения о небольшом количестве отдельных пользователей, сеансов и событий, которые соответствуют текущему запросу.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-134">The Example instances section shows information about a handful of individual users, sessions, or events that are matched by the current query.</span></span> <span data-ttu-id="2d7cc-135">Учитывая и изучая поведение отдельных экземпляров помимо агрегатов, можно узнать, как люди на самом деле используют приложение.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-135">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="2d7cc-136">Аналитика</span><span class="sxs-lookup"><span data-stu-id="2d7cc-136">Insights</span></span> 

<span data-ttu-id="2d7cc-137">На боковой панели "Аналитика" показаны большие кластеры пользователей, обладающих общими свойствами.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-137">The Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="2d7cc-138">Эти кластеры могут показать неожиданные тенденции в использовании приложения людьми.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="2d7cc-139">Например, может оказаться, что 40 % использования приложения получено за счет людей, пользующихся одной функцией.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-139">For example, if 40% of all of the usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="2d7cc-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2d7cc-140">Next steps</span></span>
- <span data-ttu-id="2d7cc-141">Чтобы обеспечить оптимальное использование, начните отправлять [пользовательские события](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) или [сведения о просмотрах страниц](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="2d7cc-141">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="2d7cc-142">Если вы уже сделали это, изучите инструменты использования, чтобы узнать, как пользователи используют службу.</span><span class="sxs-lookup"><span data-stu-id="2d7cc-142">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="2d7cc-143">Воронки</span><span class="sxs-lookup"><span data-stu-id="2d7cc-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="2d7cc-144">Сохранение</span><span class="sxs-lookup"><span data-stu-id="2d7cc-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="2d7cc-145">Средство "Маршруты пользователей"</span><span class="sxs-lookup"><span data-stu-id="2d7cc-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="2d7cc-146">Книги</span><span class="sxs-lookup"><span data-stu-id="2d7cc-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="2d7cc-147">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="2d7cc-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

