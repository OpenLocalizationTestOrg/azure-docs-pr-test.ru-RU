---
title: "Анализ aaaUsage для веб-приложений с помощью Azure Application Insights | Документы Microsoft"
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="4314e-103">Анализ использования для веб-приложений с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="4314e-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="4314e-104">Какие функции веб-приложения наиболее популярны?</span><span class="sxs-lookup"><span data-stu-id="4314e-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="4314e-105">Достигают ли пользователи своих целей с помощью вашего приложения?</span><span class="sxs-lookup"><span data-stu-id="4314e-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="4314e-106">Уходят ли они в определенные моменты и возвращаются ли после этого?</span><span class="sxs-lookup"><span data-stu-id="4314e-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="4314e-107">[Azure Application Insights](app-insights-overview.md) помогает получить важные сведения о том, как люди используют ваше веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="4314e-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="4314e-108">Каждый раз, обновив приложение, можно оценить, насколько хорошо оно подходит пользователям.</span><span class="sxs-lookup"><span data-stu-id="4314e-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="4314e-109">Обладая такими сведениями, можно принять решения на основе данных по дальнейшим циклам разработки.</span><span class="sxs-lookup"><span data-stu-id="4314e-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="4314e-110">Отправка телеметрии из приложения</span><span class="sxs-lookup"><span data-stu-id="4314e-110">Send telemetry from your app</span></span>

<span data-ttu-id="4314e-111">максимальное удобство Hello получается путем установки Application Insights, и в коде приложения сервера, так и на веб-страницах.</span><span class="sxs-lookup"><span data-stu-id="4314e-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="4314e-112">Hello клиентские и серверные компоненты приложения отправить назад toohello телеметрии портала Azure для анализа.</span><span class="sxs-lookup"><span data-stu-id="4314e-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="4314e-113">**Код сервера:** Install hello соответствующий модуль для вашей [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), или [других](app-insights-platforms.md) приложения.</span><span class="sxs-lookup"><span data-stu-id="4314e-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="4314e-114">*Не хотите tooinstall серверного кода? Просто [создайте ресурс Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="4314e-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="4314e-115">**Код веб-страницы:** Привет открыть [портал Azure](https://portal.azure.com), откройте hello ресурс Application Insights для своего приложения, а затем **Приступая к работе > мониторинг и диагностика клиентского**.</span><span class="sxs-lookup"><span data-stu-id="4314e-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Скопируйте скрипт hello в head hello главной страницы.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="4314e-117">**Получение телеметрии:** запуска проекта в режиме отладки в течение нескольких минут, а затем найдите для результатов в колонке Обзор hello в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4314e-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="4314e-118">Публикация вашего приложения toomonitor производительность приложения и узнать, что делают ваши пользователи вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="4314e-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="4314e-119">Добавление идентификатора пользователя и сеанса к телеметрии</span><span class="sxs-lookup"><span data-stu-id="4314e-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="4314e-120">Пользователи tootrack со временем, Application Insights требуется tooidentify способ их.</span><span class="sxs-lookup"><span data-stu-id="4314e-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="4314e-121">Hello событий, которые оно hello единственное средство использования, не требуется идентификатор пользователя или идентификатор сеанса.</span><span class="sxs-lookup"><span data-stu-id="4314e-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="4314e-122">Приступите к отправке этих идентификаторов [сюда](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="4314e-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="4314e-123">Изучение демографических данных об использовании и статистики</span><span class="sxs-lookup"><span data-stu-id="4314e-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="4314e-124">Узнайте, когда люди используют ваше приложение, какие страницы им наиболее интересны, где находятся ваши пользователи, какие браузеры и операционные системы они используют.</span><span class="sxs-lookup"><span data-stu-id="4314e-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="4314e-125">отчеты пользователей и сеансов Hello фильтр к свои данным страницами и пользовательские события и их сегментировать, свойства, такие как расположение, среды и страницы.</span><span class="sxs-lookup"><span data-stu-id="4314e-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="4314e-126">Можно также добавить собственные фильтры.</span><span class="sxs-lookup"><span data-stu-id="4314e-126">You can also add your own filters.</span></span>

![Пользователи](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="4314e-128">Важные сведения о hello правой отметить содержательные закономерности в hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="4314e-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="4314e-129">Hello **пользователей** отчетов подсчитывает количество уникальных пользователей, получающих доступ к страницам в период выбранный момент времени в hello.</span><span class="sxs-lookup"><span data-stu-id="4314e-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="4314e-130">(Пользователи подсчитываются с помощью файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="4314e-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="4314e-131">Если какой-либо пользователь обращается к вашему сайту, используя различные браузеры или клиентские компьютеры, или очищает файлы cookie, то он будет учтен более одного раза.)</span><span class="sxs-lookup"><span data-stu-id="4314e-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="4314e-132">Hello **сеансы** hello число пользовательских сеансов, которые обращаются к сайту учитываются в отчете.</span><span class="sxs-lookup"><span data-stu-id="4314e-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="4314e-133">Сеанс — это период действий пользователя, завершающийся периодом бездействия более получаса.</span><span class="sxs-lookup"><span data-stu-id="4314e-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="4314e-134">Дополнительные сведения о средствах hello пользователям, сеансам и события</span><span class="sxs-lookup"><span data-stu-id="4314e-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="4314e-135">Просмотры страниц</span><span class="sxs-lookup"><span data-stu-id="4314e-135">Page views</span></span>

<span data-ttu-id="4314e-136">Из колонки использования hello переходите tooget плитки представления страницы приветствия декомпозиция наиболее популярных веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="4314e-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![Из колонки Обзор hello щелкните hello страницы представления диаграммы](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="4314e-138">пример Hello выше является игры веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="4314e-138">hello example above is from a games web site.</span></span> <span data-ttu-id="4314e-139">Из диаграммы hello мгновенно видно:</span><span class="sxs-lookup"><span data-stu-id="4314e-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="4314e-140">Использование не значительно hello прошлой неделе.</span><span class="sxs-lookup"><span data-stu-id="4314e-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="4314e-141">Возможно, стоит задуматься о поисковой оптимизации?</span><span class="sxs-lookup"><span data-stu-id="4314e-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="4314e-142">Теннис является наиболее популярные игры страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="4314e-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="4314e-143">Рассмотрим дальнейшего улучшения toothis страницы.</span><span class="sxs-lookup"><span data-stu-id="4314e-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="4314e-144">В среднем пользователей на странице приветствия Теннис примерно в три раза в неделю.</span><span class="sxs-lookup"><span data-stu-id="4314e-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="4314e-145">(Сеансов примерно в три раза больше, чем пользователей.)</span><span class="sxs-lookup"><span data-stu-id="4314e-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="4314e-146">Большинство пользователей узле hello во время hello США рабочей недели, а также в рабочие часы.</span><span class="sxs-lookup"><span data-stu-id="4314e-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="4314e-147">Возможно должен предоставить кнопка «быстрый скрыть» на веб-странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="4314e-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="4314e-148">Hello [заметки](app-insights-annotations.md) на диаграмме hello Показать, когда новые версии hello веб-сайта были развернуты.</span><span class="sxs-lookup"><span data-stu-id="4314e-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="4314e-149">Ни один из последних развертываний hello было заметно влияет на использование.</span><span class="sxs-lookup"><span data-stu-id="4314e-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="4314e-150">Что делать, если хотите сайта tooyour трафика hello tooinvestigate более подробно, например разбиение по пользовательское свойство, которое отправляет его телеметрии просмотров страниц веб-узла?</span><span class="sxs-lookup"><span data-stu-id="4314e-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="4314e-151">Откройте hello **события** средства в меню ресурса Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="4314e-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="4314e-152">Этот инструмент позволяет проанализировать, сколько просмотров страниц и пользовательских событий было отправлено из приложения, используя разнообразные параметры фильтров, когорт и сегментов.</span><span class="sxs-lookup"><span data-stu-id="4314e-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="4314e-153">В hello «, используемая» раскрывающийся список выберите «View Any страницы».</span><span class="sxs-lookup"><span data-stu-id="4314e-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="4314e-154">В раскрывающемся списке «Разбиение по» hello выберите какие toosplit телеметрии просмотреть страницу свойств.</span><span class="sxs-lookup"><span data-stu-id="4314e-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="4314e-155">Период удержания — сколько пользователей вернулось?</span><span class="sxs-lookup"><span data-stu-id="4314e-155">Retention - how many users come back?</span></span>

<span data-ttu-id="4314e-156">Хранения поможет вам понять, как часто пользователи возвращают toouse свои приложения с учетом последователей пользователей, которые выполнены какие-либо действия бизнес в течение определенного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="4314e-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="4314e-157">Понимать, какие функции привести к пользователям назад toocome сильнее, чем другие</span><span class="sxs-lookup"><span data-stu-id="4314e-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="4314e-158">Сформируйте гипотезу на основе данных реальных пользователей.</span><span class="sxs-lookup"><span data-stu-id="4314e-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="4314e-159">Определите, является ли период удержания проблемой для вашего продукта.</span><span class="sxs-lookup"><span data-stu-id="4314e-159">Determine whether retention is a problem in your product</span></span> 

![Сохранение](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="4314e-161">элементы управления хранения Hello в верхней части разрешить вы toodefine определенных событий и хранения toocalculate диапазона времени.</span><span class="sxs-lookup"><span data-stu-id="4314e-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="4314e-162">Hello график в середине hello дает визуальное представление hello общий процент удержания указанный диапазон времени hello.</span><span class="sxs-lookup"><span data-stu-id="4314e-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="4314e-163">График Hello на нижней hello представляет отдельных хранения в определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="4314e-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="4314e-164">Такой уровень детализации позволяет toounderstand делают какие ваши пользователи, а также то, что может повлиять на пользователей на более подробные гранулярности.</span><span class="sxs-lookup"><span data-stu-id="4314e-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="4314e-165">Дополнительные сведения о средство хранения hello</span><span class="sxs-lookup"><span data-stu-id="4314e-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="4314e-166">Пользовательские бизнес-события</span><span class="sxs-lookup"><span data-stu-id="4314e-166">Custom business events</span></span>

<span data-ttu-id="4314e-167">tooget, следует четко понимать, какие пользователи с веб-приложения, это полезно tooinsert строк кода toolog пользовательских событий.</span><span class="sxs-lookup"><span data-stu-id="4314e-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="4314e-168">Эти события можно отследить все подробные пользовательского действия, например на нажатие конкретных кнопок, toomore значительные бизнес-события, например покупкой или выиграть игры.</span><span class="sxs-lookup"><span data-stu-id="4314e-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="4314e-169">Хотя в некоторых случаях просмотры страниц могут представлять собой полезные события, но в целом это не так.</span><span class="sxs-lookup"><span data-stu-id="4314e-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="4314e-170">Пользователь может открывать страницу продукта без приобретения hello продукта.</span><span class="sxs-lookup"><span data-stu-id="4314e-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="4314e-171">С помощью специальных бизнес-событий можно создать диаграмму перемещения пользователей по сайту.</span><span class="sxs-lookup"><span data-stu-id="4314e-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="4314e-172">Можно узнать их предпочтения относительно различных параметров, а также определить, где они покидают сайт или испытывают сложности.</span><span class="sxs-lookup"><span data-stu-id="4314e-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="4314e-173">Обладая такими сведениями могли принимать обоснованные решения о приоритетах hello в невыполненной работе разработки.</span><span class="sxs-lookup"><span data-stu-id="4314e-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="4314e-174">События могут регистрироваться hello веб-странице:</span><span class="sxs-lookup"><span data-stu-id="4314e-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="4314e-175">Или на стороне сервера hello hello веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="4314e-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="4314e-176">События toothese значения свойств, можно прикрепить таким образом, можно фильтровать или разделить hello события при их исследовать hello портала.</span><span class="sxs-lookup"><span data-stu-id="4314e-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="4314e-177">Кроме того стандартный набор свойств — tooeach присоединенные события, например идентификатор анонимного пользователя, который позволяет вам tootrace hello последовательность действий для отдельного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4314e-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="4314e-178">Узнайте больше о [пользовательских событиях](app-insights-api-custom-events-metrics.md#trackevent) и [свойствах](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="4314e-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="4314e-179">Анализ событий</span><span class="sxs-lookup"><span data-stu-id="4314e-179">Slice and dice events</span></span>

<span data-ttu-id="4314e-180">В средствах hello пользователям, сеансам и события можно плоскостных и объемных срезов пользовательские события, пользователя, имя события и свойства.</span><span class="sxs-lookup"><span data-stu-id="4314e-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="4314e-181">![Пользователи](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="4314e-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="4314e-182">Данные телеметрии hello разработки с помощью приложения hello</span><span class="sxs-lookup"><span data-stu-id="4314e-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="4314e-183">При конструировании каждого компонента приложения, рассмотрим, как будет toomeasure его успешное выполнение с пользователями.</span><span class="sxs-lookup"><span data-stu-id="4314e-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="4314e-184">Решите, запуска бизнес-событий необходимо toorecord, а также кода hello вызовов для этих событий отслеживания в ваше приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4314e-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="4314e-185">Тестирование A или B </span><span class="sxs-lookup"><span data-stu-id="4314e-185">A | B Testing</span></span>
<span data-ttu-id="4314e-186">Если вы не знаете, какой вариант компонента будет более эффективен, освободить оба параметра, делая каждого доступного toodifferent пользователей.</span><span class="sxs-lookup"><span data-stu-id="4314e-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="4314e-187">Успех hello каждого измерения, а затем переместите tooa единой версии.</span><span class="sxs-lookup"><span data-stu-id="4314e-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="4314e-188">Этот прием присоединить телеметрии hello tooall значений различных свойств, отправляемый по каждой версии приложения.</span><span class="sxs-lookup"><span data-stu-id="4314e-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="4314e-189">Это можно сделать путем определения свойств в hello active TelemetryContext.</span><span class="sxs-lookup"><span data-stu-id="4314e-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="4314e-190">Эти свойства по умолчанию добавляются, отправляет сообщения tooevery телеметрии, приложение hello - не только на пользовательские сообщения, но также стандартной телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="4314e-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="4314e-191">На портале Application Insights hello фильтрации и разбить данные на значения свойств hello, таким образом, как разные версии toocompare hello.</span><span class="sxs-lookup"><span data-stu-id="4314e-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="4314e-192">toodo, [Настройка инициализатор телеметрии](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="4314e-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="4314e-193">В инициализаторе приложения hello web например Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="4314e-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="4314e-194">Все новые TelemetryClients автоматически добавляют заданного значения свойства hello.</span><span class="sxs-lookup"><span data-stu-id="4314e-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="4314e-195">События телеметрии отдельных можно переопределить значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="4314e-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4314e-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4314e-196">Next steps</span></span>
   - [<span data-ttu-id="4314e-197">Пользователи, сеансы, события</span><span class="sxs-lookup"><span data-stu-id="4314e-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="4314e-198">Воронки</span><span class="sxs-lookup"><span data-stu-id="4314e-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="4314e-199">Сохранение</span><span class="sxs-lookup"><span data-stu-id="4314e-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="4314e-200">Средство "Маршруты пользователей"</span><span class="sxs-lookup"><span data-stu-id="4314e-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="4314e-201">Книги</span><span class="sxs-lookup"><span data-stu-id="4314e-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="4314e-202">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="4314e-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
