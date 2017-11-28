---
title: "Анализ использования веб-приложений с помощью Azure Application Insights | Документы Майкрософт"
description: "Изучение пользователей и их действий с веб-приложением."
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
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="36131-103">Анализ использования для веб-приложений с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="36131-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="36131-104">Какие функции веб-приложения наиболее популярны?</span><span class="sxs-lookup"><span data-stu-id="36131-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="36131-105">Достигают ли пользователи своих целей с помощью вашего приложения?</span><span class="sxs-lookup"><span data-stu-id="36131-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="36131-106">Уходят ли они в определенные моменты и возвращаются ли после этого?</span><span class="sxs-lookup"><span data-stu-id="36131-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="36131-107">[Azure Application Insights](app-insights-overview.md) помогает получить важные сведения о том, как люди используют ваше веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="36131-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="36131-108">Каждый раз, обновив приложение, можно оценить, насколько хорошо оно подходит пользователям.</span><span class="sxs-lookup"><span data-stu-id="36131-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="36131-109">Обладая такими сведениями, можно принять решения на основе данных по дальнейшим циклам разработки.</span><span class="sxs-lookup"><span data-stu-id="36131-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="36131-110">Отправка телеметрии из приложения</span><span class="sxs-lookup"><span data-stu-id="36131-110">Send telemetry from your app</span></span>

<span data-ttu-id="36131-111">Максимальное удобство работы достигается путем установки Application Insights как в серверном коде приложения, так и на веб-страницах.</span><span class="sxs-lookup"><span data-stu-id="36131-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="36131-112">Клиентские и серверные компоненты приложения отправляют данные телеметрии на портал Azure для анализа.</span><span class="sxs-lookup"><span data-stu-id="36131-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="36131-113">**Серверный код:** установите соответствующий модуль для своего приложения [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md) или приложения [иного типа](app-insights-platforms.md).</span><span class="sxs-lookup"><span data-stu-id="36131-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="36131-114">*Не хотите устанавливать серверный код? Просто [создайте ресурс Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="36131-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="36131-115">**Код веб-страницы:** откройте [портал Azure](https://portal.azure.com), откройте ресурс Application Insights для приложения, а затем выберите **Начало работы > Мониторинг и диагностика приложения на стороне клиента**.</span><span class="sxs-lookup"><span data-stu-id="36131-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Скопируйте скрипт в заголовок главной веб-страницы.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="36131-117">**Получение данных телеметрии:** запустите проект в режиме отладки на несколько минут, а затем просмотрите результаты в колонке "Обзор" в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36131-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="36131-118">Опубликуйте ваше приложение для отслеживания его производительности и узнайте, что делают с ним пользователи.</span><span class="sxs-lookup"><span data-stu-id="36131-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="36131-119">Добавление идентификатора пользователя и сеанса к телеметрии</span><span class="sxs-lookup"><span data-stu-id="36131-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="36131-120">Для долговременного отслеживания пользователей Application Insights требуется способ их идентификации.</span><span class="sxs-lookup"><span data-stu-id="36131-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="36131-121">Инструмент "События" — это единственный инструмент использования, не требующий идентификатор пользователя или сеанса.</span><span class="sxs-lookup"><span data-stu-id="36131-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="36131-122">Приступите к отправке этих идентификаторов [сюда](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="36131-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="36131-123">Изучение демографических данных об использовании и статистики</span><span class="sxs-lookup"><span data-stu-id="36131-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="36131-124">Узнайте, когда люди используют ваше приложение, какие страницы им наиболее интересны, где находятся ваши пользователи, какие браузеры и операционные системы они используют.</span><span class="sxs-lookup"><span data-stu-id="36131-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="36131-125">Отчеты о пользователях и сеансах позволяют фильтровать данные по страницам или пользовательским событиям, а также разделять их по свойствам, таким как расположение, среда и страница.</span><span class="sxs-lookup"><span data-stu-id="36131-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="36131-126">Можно также добавить собственные фильтры.</span><span class="sxs-lookup"><span data-stu-id="36131-126">You can also add your own filters.</span></span>

![Пользователи](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="36131-128">Аналитические сведения справа позволяют выделять важные закономерности в наборе данных.</span><span class="sxs-lookup"><span data-stu-id="36131-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="36131-129">В отчете **Пользователи** подсчитывается количество уникальных пользователей, которые обращаются к страницам в выбранные периоды времени.</span><span class="sxs-lookup"><span data-stu-id="36131-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="36131-130">(Пользователи подсчитываются с помощью файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="36131-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="36131-131">Если какой-либо пользователь обращается к вашему сайту, используя различные браузеры или клиентские компьютеры, или очищает файлы cookie, то он будет учтен более одного раза.)</span><span class="sxs-lookup"><span data-stu-id="36131-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="36131-132">В отчете **Сеансы** подсчитывается количество пользовательских сеансов, обращающихся к узлу.</span><span class="sxs-lookup"><span data-stu-id="36131-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="36131-133">Сеанс — это период действий пользователя, завершающийся периодом бездействия более получаса.</span><span class="sxs-lookup"><span data-stu-id="36131-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="36131-134">Дополнительные сведения об инструментах "Пользователи", "Сеансы" и "События".</span><span class="sxs-lookup"><span data-stu-id="36131-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="36131-135">Просмотры страниц</span><span class="sxs-lookup"><span data-stu-id="36131-135">Page views</span></span>

<span data-ttu-id="36131-136">В колонке "Использование" щелкайте "Просмотры страницы", чтобы получить статистику по наиболее популярным страницам.</span><span class="sxs-lookup"><span data-stu-id="36131-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![В колонке обзора щелкните диаграмму "Просмотры страниц"](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="36131-138">Приведенный выше пример взят с игрового веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="36131-138">The example above is from a games web site.</span></span> <span data-ttu-id="36131-139">На диаграммах можно сразу же увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="36131-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="36131-140">Использование не увеличилось за прошлую неделю.</span><span class="sxs-lookup"><span data-stu-id="36131-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="36131-141">Возможно, стоит задуматься о поисковой оптимизации?</span><span class="sxs-lookup"><span data-stu-id="36131-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="36131-142">"Теннис" является наиболее популярной игрой.</span><span class="sxs-lookup"><span data-stu-id="36131-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="36131-143">Этой странице следует отдать приоритет в улучшениях.</span><span class="sxs-lookup"><span data-stu-id="36131-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="36131-144">В среднем пользователи посещают страницу "Теннис" примерно три раза в неделю.</span><span class="sxs-lookup"><span data-stu-id="36131-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="36131-145">(Сеансов примерно в три раза больше, чем пользователей.)</span><span class="sxs-lookup"><span data-stu-id="36131-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="36131-146">Большинство пользователей посещают сайт в рабочие дни и часы.</span><span class="sxs-lookup"><span data-stu-id="36131-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="36131-147">Возможно, следует добавить на веб-страницу кнопку для быстрого ее скрытия.</span><span class="sxs-lookup"><span data-stu-id="36131-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="36131-148">В [заметках](app-insights-annotations.md) на диаграмме указывается, когда были развернуты новые версии веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="36131-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="36131-149">Последние развернутые версии не оказали заметного влияния на использование.</span><span class="sxs-lookup"><span data-stu-id="36131-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="36131-150">Что делать, если вы хотите более подробно изучить трафик своего сайта, например, разделив его по пользовательскому свойству, которое сайт отправляет в данных телеметрии просмотра страниц?</span><span class="sxs-lookup"><span data-stu-id="36131-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="36131-151">Откройте инструмент **События** в меню ресурса Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36131-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="36131-152">Этот инструмент позволяет проанализировать, сколько просмотров страниц и пользовательских событий было отправлено из приложения, используя разнообразные параметры фильтров, когорт и сегментов.</span><span class="sxs-lookup"><span data-stu-id="36131-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="36131-153">Из раскрывающегося списка "Которые использовали" выберите "Any Page View" (Просмотр любой страницы).</span><span class="sxs-lookup"><span data-stu-id="36131-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="36131-154">Из раскрывающегося списка "Разделение по" выберите свойство, по которому нужно разделить данные телеметрии просмотра страниц.</span><span class="sxs-lookup"><span data-stu-id="36131-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="36131-155">Период удержания — сколько пользователей вернулось?</span><span class="sxs-lookup"><span data-stu-id="36131-155">Retention - how many users come back?</span></span>

<span data-ttu-id="36131-156">Период удержания помогает понять, как часто пользователи возвращаются к использованию своего приложения. Для этого используются когорты пользователей, которые выполнили какое-либо коммерческое действие во время определенного горизонта планирования.</span><span class="sxs-lookup"><span data-stu-id="36131-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="36131-157">Поймите, какие именно функции заставляют пользователей возвращаться чаще, чем другие.</span><span class="sxs-lookup"><span data-stu-id="36131-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="36131-158">Сформируйте гипотезу на основе данных реальных пользователей.</span><span class="sxs-lookup"><span data-stu-id="36131-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="36131-159">Определите, является ли период удержания проблемой для вашего продукта.</span><span class="sxs-lookup"><span data-stu-id="36131-159">Determine whether retention is a problem in your product</span></span> 

![Сохранение](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="36131-161">Помимо прочего, элементы управления периодом удержания позволяют определить конкретные события и диапазон времени для вычисления периода удержания.</span><span class="sxs-lookup"><span data-stu-id="36131-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="36131-162">График в середине дает визуальное представление об общем проценте удержания за указанный диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="36131-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="36131-163">График внизу отображает период удержания отдельных пользователей за заданный период времени.</span><span class="sxs-lookup"><span data-stu-id="36131-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="36131-164">Такой уровень детализации позволяет лучше понять, что ваши пользователи делают и что может повлиять на возвращение пользователей.</span><span class="sxs-lookup"><span data-stu-id="36131-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

<span data-ttu-id="36131-165">[Дополнительные сведения об инструменте "Хранение"](app-insights-usage-retention.md).</span><span class="sxs-lookup"><span data-stu-id="36131-165">[More about the Retention tool](app-insights-usage-retention.md)</span></span>

## <a name="custom-business-events"></a><span data-ttu-id="36131-166">Пользовательские бизнес-события</span><span class="sxs-lookup"><span data-stu-id="36131-166">Custom business events</span></span>

<span data-ttu-id="36131-167">Чтобы получить четкое представление о действиях пользователей с веб-приложением, полезно добавить строки кода для ведения журнала пользовательских событий.</span><span class="sxs-lookup"><span data-stu-id="36131-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="36131-168">Эти события могут отслеживать что угодно, начиная с детализированных действий пользователя (например, нажатие определенных кнопок) и заканчивая более серьезными бизнес-событиями (например, совершение покупки или победа в игре).</span><span class="sxs-lookup"><span data-stu-id="36131-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="36131-169">Хотя в некоторых случаях просмотры страниц могут представлять собой полезные события, но в целом это не так.</span><span class="sxs-lookup"><span data-stu-id="36131-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="36131-170">Пользователь может открыть страницу продукта, не приобретая его.</span><span class="sxs-lookup"><span data-stu-id="36131-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="36131-171">С помощью специальных бизнес-событий можно создать диаграмму перемещения пользователей по сайту.</span><span class="sxs-lookup"><span data-stu-id="36131-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="36131-172">Можно узнать их предпочтения относительно различных параметров, а также определить, где они покидают сайт или испытывают сложности.</span><span class="sxs-lookup"><span data-stu-id="36131-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="36131-173">Обладая такими сведениями, можно принимать обоснованные решения о приоритетах для невыполненной работы по разработке.</span><span class="sxs-lookup"><span data-stu-id="36131-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="36131-174">Журнал событий можно вести на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="36131-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="36131-175">Или на стороне сервера веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="36131-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="36131-176">В эти события можно вложить значения свойств, чтобы события можно было фильтровать или разделять при изучении на портале.</span><span class="sxs-lookup"><span data-stu-id="36131-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="36131-177">Кроме того, в каждое событие вкладывается стандартный набор свойств, например идентификатор анонимного пользователя, который позволяет выполнять трассировку последовательности действий отдельного пользователя.</span><span class="sxs-lookup"><span data-stu-id="36131-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="36131-178">Узнайте больше о [пользовательских событиях](app-insights-api-custom-events-metrics.md#trackevent) и [свойствах](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="36131-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="36131-179">Анализ событий</span><span class="sxs-lookup"><span data-stu-id="36131-179">Slice and dice events</span></span>

<span data-ttu-id="36131-180">В инструментах "Пользователи", "Сеансы" и "События" можно анализировать пользовательские события по пользователю, имени события и свойствам.</span><span class="sxs-lookup"><span data-stu-id="36131-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="36131-181">![Пользователи](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="36131-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="36131-182">Разработка телеметрии приложения</span><span class="sxs-lookup"><span data-stu-id="36131-182">Design the telemetry with the app</span></span>

<span data-ttu-id="36131-183">При разработке каждого компонента приложения обдумайте, как вы будете измерять его успех у пользователей.</span><span class="sxs-lookup"><span data-stu-id="36131-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="36131-184">Решите, какие бизнес-события необходимо записывать, и с самого начала запрограммируйте вызовы отслеживания для этих событий в приложении.</span><span class="sxs-lookup"><span data-stu-id="36131-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="36131-185">Тестирование A или B </span><span class="sxs-lookup"><span data-stu-id="36131-185">A | B Testing</span></span>
<span data-ttu-id="36131-186">Если неизвестно, какой вариант функции будет более эффективен, выпустите их оба, чтобы каждый из них был доступен для разных пользователей.</span><span class="sxs-lookup"><span data-stu-id="36131-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="36131-187">Измерьте успешность каждого варианта, а затем перейдите к единой версии.</span><span class="sxs-lookup"><span data-stu-id="36131-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="36131-188">В рамках этого способа необходимо вложить разные значения свойств во все данные телеметрии, отправляемые каждой версией приложения.</span><span class="sxs-lookup"><span data-stu-id="36131-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="36131-189">Для этого нужно определить свойства в активном контексте телеметрии TelemetryContext.</span><span class="sxs-lookup"><span data-stu-id="36131-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="36131-190">Эти свойства по умолчанию добавляются к каждому сообщению телеметрии, которое отправляет приложение, — не только к настраиваемым сообщениям, но также к стандартным данным телеметрии.</span><span class="sxs-lookup"><span data-stu-id="36131-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="36131-191">Чтобы сравнить различные версии, на портале Application Insights можно отфильтровать и разделить данные по значениям свойств.</span><span class="sxs-lookup"><span data-stu-id="36131-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="36131-192">Для этого следует [настроить инициализатор телеметрии](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="36131-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="36131-193">В инициализаторе веб-приложения, например Global.asax.cs, добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="36131-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="36131-194">Все новые клиенты телеметрии автоматически добавляют указанное значение свойства.</span><span class="sxs-lookup"><span data-stu-id="36131-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="36131-195">Отдельные события телеметрии могут переопределять значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36131-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36131-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36131-196">Next steps</span></span>
   - [<span data-ttu-id="36131-197">Пользователи, сеансы, события</span><span class="sxs-lookup"><span data-stu-id="36131-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="36131-198">Воронки</span><span class="sxs-lookup"><span data-stu-id="36131-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="36131-199">Сохранение</span><span class="sxs-lookup"><span data-stu-id="36131-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="36131-200">Средство "Маршруты пользователей"</span><span class="sxs-lookup"><span data-stu-id="36131-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="36131-201">Книги</span><span class="sxs-lookup"><span data-stu-id="36131-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="36131-202">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="36131-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
