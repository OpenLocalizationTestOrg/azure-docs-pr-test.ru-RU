---
title: "aaaHow по выполнению в Azure Application Insights | Документы Microsoft"
description: "Вопросы и ответы об Application Insights"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="e3f5c-103">Как работать с Application Insights</span><span class="sxs-lookup"><span data-stu-id="e3f5c-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="e3f5c-104">Получать уведомление по электронной почте, если...</span><span class="sxs-lookup"><span data-stu-id="e3f5c-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="e3f5c-105">Уведомлять меня по электронной почте, если сайт выходит из строя</span><span class="sxs-lookup"><span data-stu-id="e3f5c-105">Email if my site goes down</span></span>
<span data-ttu-id="e3f5c-106">Настройте [веб-тест доступности](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="e3f5c-107">Уведомлять меня по электронной почте, если сайт перегружен</span><span class="sxs-lookup"><span data-stu-id="e3f5c-107">Email if my site is overloaded</span></span>
<span data-ttu-id="e3f5c-108">Настройте [оповещение](app-insights-alerts.md) для **времени ответа от сервера**.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="e3f5c-109">Пороговое значение может быть в пределах от 1 до 2 секунд.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="e3f5c-110">Приложение может также демонстрировать признаки нагрузки, выдавая коды ошибок.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="e3f5c-111">Настройте оповещение при **неудачных запросах**.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="e3f5c-112">Если вы хотите tooset оповещение на **исключения сервера**, может потребоваться toodo [дополнительной настройки](app-insights-asp-net-exceptions.md) в toosee данные о заказах.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="e3f5c-113">Получить уведомление по электронной почте при исключении</span><span class="sxs-lookup"><span data-stu-id="e3f5c-113">Email on exceptions</span></span>
1. [<span data-ttu-id="e3f5c-114">Настройте мониторинг исключений</span><span class="sxs-lookup"><span data-stu-id="e3f5c-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="e3f5c-115">[Создать оповещение](app-insights-alerts.md) на hello исключение подсчета метрики</span><span class="sxs-lookup"><span data-stu-id="e3f5c-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="e3f5c-116">Уведомлять меня по электронной почте о событиях в приложении</span><span class="sxs-lookup"><span data-stu-id="e3f5c-116">Email on an event in my app</span></span>
<span data-ttu-id="e3f5c-117">Предположим, что вам нравится tooget сообщение электронной почты при возникновении определенного события.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="e3f5c-118">Application Insights не предоставляет эту функцию напрямую, но позволяет [отправлять оповещение, если метрика превысит пороговое значение](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="e3f5c-119">Оповещения можно настроить для [пользовательских метрик](app-insights-api-custom-events-metrics.md#trackmetric), но не для пользовательских событий.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="e3f5c-120">Запись некоторых tooincrease кода метрики при возникновении события hello:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="e3f5c-121">или:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="e3f5c-122">Так как предупреждения имеют два состояния, вы можете toosend низкое значение рассмотрим hello предупреждение toohave завершен:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="e3f5c-123">Создать диаграмму в [метрики обозреватель](app-insights-metrics-explorer.md) toosee вашей звуковых сигналов:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="e3f5c-124">Теперь можно задайте предупреждения toofire при hello метрика выходит за пределы mid значение на короткий промежуток времени:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="e3f5c-125">Задайте усреднение минимальный период toohello hello.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="e3f5c-126">Вы сможете получить сообщения электронной почты при hello метрика выходит за пределы и ниже порогового значения hello.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="e3f5c-127">Некоторые точки tooconsider:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-127">Some points tooconsider:</span></span>

* <span data-ttu-id="e3f5c-128">Оповещение может находиться в двух состояниях: «оповещение» и «исправен».</span><span class="sxs-lookup"><span data-stu-id="e3f5c-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="e3f5c-129">состояние Hello вычисляется только в том случае, когда поступает метрики.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="e3f5c-130">Сообщение электронной почты отправляется только в том случае, когда изменяется состояние hello.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="e3f5c-131">Именно поэтому у вас есть toosend высокой и низкой стоимости метрики.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="e3f5c-132">Предупреждение tooevaluate hello, среднее hello берется hello полученных значений через hello предшествующего периода.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="e3f5c-133">Это происходит каждый раз при получении метрики, поэтому чаще, чем период hello задать могут отправляться сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="e3f5c-134">Так как сообщения электронной почты, отправленных на «предупреждение» и «Исправен», может потребоваться tooconsider повторно говорить одноразовой события как условие с двумя состояниями.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="e3f5c-135">Например вместо события «завершена» имеют условие «задание выполняется», где получить сообщения электронной почты в hello начало и конец задания.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="e3f5c-136">Настройте автоматические оповещения</span><span class="sxs-lookup"><span data-stu-id="e3f5c-136">Set up alerts automatically</span></span>
[<span data-ttu-id="e3f5c-137">Используйте PowerShell toocreate новые предупреждения</span><span class="sxs-lookup"><span data-stu-id="e3f5c-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="e3f5c-138">Используйте PowerShell tooManage Application Insights</span><span class="sxs-lookup"><span data-stu-id="e3f5c-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="e3f5c-139">Создание новых ресурсов</span><span class="sxs-lookup"><span data-stu-id="e3f5c-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="e3f5c-140">Создание новых оповещений</span><span class="sxs-lookup"><span data-stu-id="e3f5c-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="e3f5c-141">Разделение телеметрии разных версий</span><span class="sxs-lookup"><span data-stu-id="e3f5c-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="e3f5c-142">Несколько ролей в приложении. Используйте единый ресурс Application Insights и выполните фильтрацию по cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="e3f5c-143">Подробнее</span><span class="sxs-lookup"><span data-stu-id="e3f5c-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="e3f5c-144">Отдельные стадии разработки, тестирования и выпуска версий. Используйте различные ресурсы Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="e3f5c-145">Получают ключи hello инструментирования из файла web.config. [Дополнительные сведения](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e3f5c-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="e3f5c-146">Отчеты о версиях сборки. Добавьте свойство с помощью инициализатора телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="e3f5c-147">Подробнее</span><span class="sxs-lookup"><span data-stu-id="e3f5c-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="e3f5c-148">Мониторинг внутренних серверов и классических приложений</span><span class="sxs-lookup"><span data-stu-id="e3f5c-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="e3f5c-149">[Модуль SDK для Windows Server используйте hello](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="e3f5c-150">Визуализируйте данные</span><span class="sxs-lookup"><span data-stu-id="e3f5c-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="e3f5c-151">Панель мониторинга с метрикой для нескольких приложений</span><span class="sxs-lookup"><span data-stu-id="e3f5c-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="e3f5c-152">В [обозревателе метрик](app-insights-metrics-explorer.md)настройте диаграмму и сохраните ее в списке избранного.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="e3f5c-153">Закрепите панель мониторинга Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="e3f5c-154">Панель мониторинга с данными из других источников и Application Insights</span><span class="sxs-lookup"><span data-stu-id="e3f5c-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="e3f5c-155">[Экспортировать данные телеметрии tooPower BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="e3f5c-156">Или</span><span class="sxs-lookup"><span data-stu-id="e3f5c-156">Or</span></span>

* <span data-ttu-id="e3f5c-157">Используйте SharePoint как панель мониторинга для отображения данных веб-компонентов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="e3f5c-158">[Использовать непрерывный Экспорт и Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="e3f5c-159">Использование базы данных hello tooexamine PowerView и создайте веб-части SharePoint для PowerView.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="e3f5c-160">Отфильтровывание анонимных или прошедших проверку подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="e3f5c-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="e3f5c-161">Если вход пользователей, можно задать hello [идентификатор пользователя с проверкой подлинности](app-insights-api-custom-events-metrics.md#authenticated-users). (Это не происходит автоматически.)</span><span class="sxs-lookup"><span data-stu-id="e3f5c-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="e3f5c-162">Затем можно:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-162">You can then:</span></span>

* <span data-ttu-id="e3f5c-163">выполнить поиск по определенным идентификаторам пользователей;</span><span class="sxs-lookup"><span data-stu-id="e3f5c-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="e3f5c-164">Фильтрация метрики tooeither анонимного или прошедшего проверку подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="e3f5c-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="e3f5c-165">Изменение имен и значений свойств</span><span class="sxs-lookup"><span data-stu-id="e3f5c-165">Modify property names or values</span></span>
<span data-ttu-id="e3f5c-166">Создайте [фильтр](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="e3f5c-167">Это дает возможность изменять или фильтровать данные телеметрии, перед отправкой из вашего приложения tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="e3f5c-168">Вывод списка определенных пользователей и информации об их использовании</span><span class="sxs-lookup"><span data-stu-id="e3f5c-168">List specific users and their usage</span></span>
<span data-ttu-id="e3f5c-169">Если необходимо просто слишком[поиска для конкретных пользователей](#search-specific-users), можно задать hello [идентификатор пользователя с проверкой подлинности](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="e3f5c-170">Если вы хотите получить список пользователей с данными — например, на какие страницы заходят пользователи или как часто они входят в систему, — существует два варианта действий:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="e3f5c-171">[Идентификатор прошедшего проверку подлинности пользователя набор](app-insights-api-custom-events-metrics.md#authenticated-users), [Экспорт базы данных tooa](app-insights-code-sample-export-sql-stream-analytics.md) и используйте подходящий средств tooanalyze существует данные пользователей.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="e3f5c-172">Если имеется небольшое количество пользователей, отправьте пользовательские события или метрики, с данными hello интерес как hello значение метрики или имя события и ИД пользователя параметр hello как свойство.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="e3f5c-173">tooanalyze просмотров страниц, замените hello стандартный вызов trackPageView JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="e3f5c-174">tooanalyze телеметрию на стороне сервера, используйте телеметрии инициализатора tooadd hello идентификатор tooall сервера телеметрия пользователя.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="e3f5c-175">После этого можно отфильтровывать и разделять метрики и поиск по идентификатору пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="e3f5c-176">Уменьшить трафик с моей tooApplication app Insights</span><span class="sxs-lookup"><span data-stu-id="e3f5c-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="e3f5c-177">В [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), отключите модули не требуется такой сборщик счетчика производительности hello.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="e3f5c-178">Используйте [выборки и фильтрации](app-insights-api-filtering-sampling.md) на hello SDK.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="e3f5c-179">На веб-страницах максимальное число hello вызовов Ajax для представления каждой страницы.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="e3f5c-180">В hello фрагмент скрипта после `instrumentationKey:...` , вставьте: `,maxAjaxCallsPerView:3` (или подходящий номер).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="e3f5c-181">Если вы используете [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), вычисления статистической функции hello пакетов значения метрики перед отправкой hello результат.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="e3f5c-182">Это можно сделать с помощью перегруженного метода TrackMetric().</span><span class="sxs-lookup"><span data-stu-id="e3f5c-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="e3f5c-183">Подробнее о [расценках и квотах](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="e3f5c-184">Отключение данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="e3f5c-184">Disable telemetry</span></span>
<span data-ttu-id="e3f5c-185">слишком**динамически остановить и запустить** hello сбор и передача данных телеметрии с сервера hello:</span><span class="sxs-lookup"><span data-stu-id="e3f5c-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="e3f5c-186">слишком**отключить выбранный Стандартная сборщики** - счетчики производительности, например, HTTP-запросы или зависимостей - удалить или закомментировать строку hello соответствующих строк в [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Удалось это делается, например, если требуется toosend TrackRequest данных.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="e3f5c-187">Просмотр счетчиков производительности системы</span><span class="sxs-lookup"><span data-stu-id="e3f5c-187">View system performance counters</span></span>
<span data-ttu-id="e3f5c-188">Среди hello метрик, которые можно отобразить в обозревателе метрик представляют собой набор счетчиков производительности системы.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="e3f5c-189">В готовой колонке **Серверы** отображается несколько таких счетчиков.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Откройте ресурс Application Insights и щелкните "Серверы".](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="e3f5c-191">Если данные счетчика производительности не отображаются</span><span class="sxs-lookup"><span data-stu-id="e3f5c-191">If you see no performance counter data</span></span>
* <span data-ttu-id="e3f5c-192">**Сервер IIS** на собственном компьютере или на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="e3f5c-193">[Установите монитор состояния](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="e3f5c-194">**Веб-сайт Azure** — мы еще не поддерживаем счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="e3f5c-195">Существует несколько методик, которые можно получить в составе Стандартная панель управления веб-сайте Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="e3f5c-196">**Сервер Unix** - [установите collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="e3f5c-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="e3f5c-197">toodisplay дополнительных счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="e3f5c-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="e3f5c-198">Во-первых, [добавить новую диаграмму](app-insights-metrics-explorer.md) и увидеть, если счетчик hello в hello basic устанавливается мы предлагаем.</span><span class="sxs-lookup"><span data-stu-id="e3f5c-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="e3f5c-199">В противном случае [добавить набор toohello счетчика hello, собранные модуль счетчика производительности hello](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="e3f5c-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
