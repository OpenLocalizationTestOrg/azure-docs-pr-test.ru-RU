---
title: "Выполнение заданий в Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: ef63e06c0621753e0a706d6efb709b943e38ee42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="ff90d-103">Как работать с Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff90d-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="ff90d-104">Получать уведомление по электронной почте, если...</span><span class="sxs-lookup"><span data-stu-id="ff90d-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="ff90d-105">Уведомлять меня по электронной почте, если сайт выходит из строя</span><span class="sxs-lookup"><span data-stu-id="ff90d-105">Email if my site goes down</span></span>
<span data-ttu-id="ff90d-106">Настройте [веб-тест доступности](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="ff90d-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="ff90d-107">Уведомлять меня по электронной почте, если сайт перегружен</span><span class="sxs-lookup"><span data-stu-id="ff90d-107">Email if my site is overloaded</span></span>
<span data-ttu-id="ff90d-108">Настройте [оповещение](app-insights-alerts.md) для **времени ответа от сервера**.</span><span class="sxs-lookup"><span data-stu-id="ff90d-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="ff90d-109">Пороговое значение может быть в пределах от 1 до 2 секунд.</span><span class="sxs-lookup"><span data-stu-id="ff90d-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="ff90d-110">Приложение может также демонстрировать признаки нагрузки, выдавая коды ошибок.</span><span class="sxs-lookup"><span data-stu-id="ff90d-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="ff90d-111">Настройте оповещение при **неудачных запросах**.</span><span class="sxs-lookup"><span data-stu-id="ff90d-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="ff90d-112">Если вы хотите настроить оповещение при **исключениях сервера**, для просмотра данных может потребоваться [дополнительная настройка](app-insights-asp-net-exceptions.md) .</span><span class="sxs-lookup"><span data-stu-id="ff90d-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="ff90d-113">Получить уведомление по электронной почте при исключении</span><span class="sxs-lookup"><span data-stu-id="ff90d-113">Email on exceptions</span></span>
1. [<span data-ttu-id="ff90d-114">Настройте мониторинг исключений</span><span class="sxs-lookup"><span data-stu-id="ff90d-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="ff90d-115">[Установите оповещение](app-insights-alerts.md) об исключении подсчета метрики</span><span class="sxs-lookup"><span data-stu-id="ff90d-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="ff90d-116">Уведомлять меня по электронной почте о событиях в приложении</span><span class="sxs-lookup"><span data-stu-id="ff90d-116">Email on an event in my app</span></span>
<span data-ttu-id="ff90d-117">Предположим, что вы хотите получать уведомления по электронной почте при возникновении определенных событий.</span><span class="sxs-lookup"><span data-stu-id="ff90d-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="ff90d-118">Application Insights не предоставляет эту функцию напрямую, но позволяет [отправлять оповещение, если метрика превысит пороговое значение](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ff90d-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="ff90d-119">Оповещения можно настроить для [пользовательских метрик](app-insights-api-custom-events-metrics.md#trackmetric), но не для пользовательских событий.</span><span class="sxs-lookup"><span data-stu-id="ff90d-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="ff90d-120">Напишите код, который будет увеличивать метрику при возникновении соответствующего события:</span><span class="sxs-lookup"><span data-stu-id="ff90d-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="ff90d-121">или:</span><span class="sxs-lookup"><span data-stu-id="ff90d-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="ff90d-122">Так как оповещения имеют два состояния, отправьте минимальное значение, при котором оповещение должно быть отменено:</span><span class="sxs-lookup"><span data-stu-id="ff90d-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="ff90d-123">Создайте диаграмму в [обозревателе метрик](app-insights-metrics-explorer.md) , чтобы увидеть оповещение:</span><span class="sxs-lookup"><span data-stu-id="ff90d-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="ff90d-124">Теперь настройте оповещение таким образом, чтобы оно отправлялось в случае, когда метрика превышает среднее значение за короткий период:</span><span class="sxs-lookup"><span data-stu-id="ff90d-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="ff90d-125">Установите минимальный период усреднения.</span><span class="sxs-lookup"><span data-stu-id="ff90d-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="ff90d-126">Вы будете получать уведомления по электронной почте, если метрика поднимется выше или упадет ниже порогового значения.</span><span class="sxs-lookup"><span data-stu-id="ff90d-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="ff90d-127">Учитывайте следующие факторы.</span><span class="sxs-lookup"><span data-stu-id="ff90d-127">Some points to consider:</span></span>

* <span data-ttu-id="ff90d-128">Оповещение может находиться в двух состояниях: «оповещение» и «исправен».</span><span class="sxs-lookup"><span data-stu-id="ff90d-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="ff90d-129">Состояние оценивается только при получении метрики.</span><span class="sxs-lookup"><span data-stu-id="ff90d-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="ff90d-130">Электронное письмо отправляется только при изменении состояния.</span><span class="sxs-lookup"><span data-stu-id="ff90d-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="ff90d-131">Вот почему необходимо отправлять как верхнюю, так и нижнюю метрику.</span><span class="sxs-lookup"><span data-stu-id="ff90d-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="ff90d-132">Для оценки оповещениям берется среднее значений, полученных за предыдущий период.</span><span class="sxs-lookup"><span data-stu-id="ff90d-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="ff90d-133">Это происходит при каждом получении метрики, поэтому сообщения электронной почты могут отправляться чаще установленной вами периодичности.</span><span class="sxs-lookup"><span data-stu-id="ff90d-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="ff90d-134">Поскольку сообщения электронной почты отправляются и при состоянии «оповещение», и при состоянии «исправен», считайте это разовое событие условием с двумя состояниями.</span><span class="sxs-lookup"><span data-stu-id="ff90d-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="ff90d-135">Например, вместо события «задание завершено» создайте условие «задание выполняется», при котором сообщения электронной почты будут отправляться при запуске и завершении задания.</span><span class="sxs-lookup"><span data-stu-id="ff90d-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="ff90d-136">Настройте автоматические оповещения</span><span class="sxs-lookup"><span data-stu-id="ff90d-136">Set up alerts automatically</span></span>
[<span data-ttu-id="ff90d-137">Создание новых оповещений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff90d-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="ff90d-138">Использование PowerShell для управления Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff90d-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="ff90d-139">Создание новых ресурсов</span><span class="sxs-lookup"><span data-stu-id="ff90d-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="ff90d-140">Создание новых оповещений</span><span class="sxs-lookup"><span data-stu-id="ff90d-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="ff90d-141">Разделение телеметрии разных версий</span><span class="sxs-lookup"><span data-stu-id="ff90d-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="ff90d-142">Несколько ролей в приложении. Используйте единый ресурс Application Insights и выполните фильтрацию по cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="ff90d-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="ff90d-143">Подробнее</span><span class="sxs-lookup"><span data-stu-id="ff90d-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="ff90d-144">Отдельные стадии разработки, тестирования и выпуска версий. Используйте различные ресурсы Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ff90d-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="ff90d-145">Получите ключи инструментирования из файла web.config. [Подробнее](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="ff90d-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="ff90d-146">Отчеты о версиях сборки. Добавьте свойство с помощью инициализатора телеметрии.</span><span class="sxs-lookup"><span data-stu-id="ff90d-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="ff90d-147">Подробнее</span><span class="sxs-lookup"><span data-stu-id="ff90d-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="ff90d-148">Мониторинг внутренних серверов и классических приложений</span><span class="sxs-lookup"><span data-stu-id="ff90d-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="ff90d-149">[Используйте модуль пакета SDK для Windows Server](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="ff90d-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="ff90d-150">Визуализируйте данные</span><span class="sxs-lookup"><span data-stu-id="ff90d-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="ff90d-151">Панель мониторинга с метрикой для нескольких приложений</span><span class="sxs-lookup"><span data-stu-id="ff90d-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="ff90d-152">В [обозревателе метрик](app-insights-metrics-explorer.md)настройте диаграмму и сохраните ее в списке избранного.</span><span class="sxs-lookup"><span data-stu-id="ff90d-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="ff90d-153">Закрепите ее на панели мониторинга Azure.</span><span class="sxs-lookup"><span data-stu-id="ff90d-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="ff90d-154">Панель мониторинга с данными из других источников и Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff90d-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="ff90d-155">[Экспорт телеметрии в Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="ff90d-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="ff90d-156">Или</span><span class="sxs-lookup"><span data-stu-id="ff90d-156">Or</span></span>

* <span data-ttu-id="ff90d-157">Используйте SharePoint как панель мониторинга для отображения данных веб-компонентов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ff90d-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="ff90d-158">[Используйте непрерывный экспорт и Stream Analytics для экспорта в SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="ff90d-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="ff90d-159">Используйте PowerView для просмотра базы данных и создания веб-компонента SharePoint для PowerView.</span><span class="sxs-lookup"><span data-stu-id="ff90d-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="ff90d-160">Отфильтровывание анонимных или прошедших проверку подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="ff90d-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="ff90d-161">Если пользователь вошел в систему, можно установить [идентификатор пользователя, прошедшего проверку подлинности](app-insights-api-custom-events-metrics.md#authenticated-users). (Это не происходит автоматически.)</span><span class="sxs-lookup"><span data-stu-id="ff90d-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="ff90d-162">Затем можно:</span><span class="sxs-lookup"><span data-stu-id="ff90d-162">You can then:</span></span>

* <span data-ttu-id="ff90d-163">выполнить поиск по определенным идентификаторам пользователей;</span><span class="sxs-lookup"><span data-stu-id="ff90d-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="ff90d-164">выполнить фильтрацию метрики для анонимных или прошедших проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="ff90d-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="ff90d-165">Изменение имен и значений свойств</span><span class="sxs-lookup"><span data-stu-id="ff90d-165">Modify property names or values</span></span>
<span data-ttu-id="ff90d-166">Создайте [фильтр](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="ff90d-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="ff90d-167">Это позволяет изменять или фильтровать данные телеметрии перед их отправкой из приложения в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ff90d-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="ff90d-168">Вывод списка определенных пользователей и информации об их использовании</span><span class="sxs-lookup"><span data-stu-id="ff90d-168">List specific users and their usage</span></span>
<span data-ttu-id="ff90d-169">Если нужно просто выполнить [поиск конкретных пользователей](#search-specific-users), можно установить [идентификатор пользователя, прошедшего проверку подлинности](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="ff90d-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="ff90d-170">Если вы хотите получить список пользователей с данными — например, на какие страницы заходят пользователи или как часто они входят в систему, — существует два варианта действий:</span><span class="sxs-lookup"><span data-stu-id="ff90d-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="ff90d-171">[Установить идентификатор пользователя, прошедшего проверку подлинности](app-insights-api-custom-events-metrics.md#authenticated-users), [выполнить экспорт данных в базу данных](app-insights-code-sample-export-sql-stream-analytics.md) и проанализировать данные в базе данных с помощью подходящих инструментов.</span><span class="sxs-lookup"><span data-stu-id="ff90d-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="ff90d-172">Если количество пользователей невелико, отправить пользовательские события или метрики с использованием интересующих данных, таких как значение метрики и имя события, и задавать идентификатор пользователя в качестве свойства.</span><span class="sxs-lookup"><span data-stu-id="ff90d-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="ff90d-173">Для анализа просмотров страниц замените стандартный вызов JavaScript trackPageView.</span><span class="sxs-lookup"><span data-stu-id="ff90d-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="ff90d-174">Чтобы проанализировать данные телеметрии на стороне сервера, используйте инициализатор телеметрии для добавления идентификатора пользователя ко всем данным телеметрии сервера.</span><span class="sxs-lookup"><span data-stu-id="ff90d-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="ff90d-175">После этого можно фильтровать и разделять метрику и выполнять поиск по идентификатору пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff90d-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="ff90d-176">Уменьшение трафика из вашего приложения в Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff90d-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="ff90d-177">В файле [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)отключите все неиспользуемые модули, например сборщик данных счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="ff90d-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="ff90d-178">Используйте [Выборка и фильтрация](app-insights-api-filtering-sampling.md) в пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="ff90d-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="ff90d-179">На своих веб-страницах ограничьте число вызовов Ajax для каждого представления страницы.</span><span class="sxs-lookup"><span data-stu-id="ff90d-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="ff90d-180">Во фрагменте сценария после `instrumentationKey:...` вставьте `,maxAjaxCallsPerView:3` (или другое подходящее число).</span><span class="sxs-lookup"><span data-stu-id="ff90d-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="ff90d-181">Если используется [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), вычисляйте агрегированное значение для пакетов значений метрики перед отправкой результата.</span><span class="sxs-lookup"><span data-stu-id="ff90d-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="ff90d-182">Это можно сделать с помощью перегруженного метода TrackMetric().</span><span class="sxs-lookup"><span data-stu-id="ff90d-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="ff90d-183">Подробнее о [расценках и квотах](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="ff90d-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="ff90d-184">Отключение данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="ff90d-184">Disable telemetry</span></span>
<span data-ttu-id="ff90d-185">Чтобы **динамически остановить и запустить** сбор и передачу данных телеметрии с сервера:</span><span class="sxs-lookup"><span data-stu-id="ff90d-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="ff90d-186">Чтобы **отключить выбранные стандартные сборщики** , например счетчики производительности, HTTP-запросы или зависимости, удалите или закомментируйте соответствующие строки в файле [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Это можно сделать, если вы, например, хотите отправить собственные данные TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="ff90d-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="ff90d-187">Просмотр счетчиков производительности системы</span><span class="sxs-lookup"><span data-stu-id="ff90d-187">View system performance counters</span></span>
<span data-ttu-id="ff90d-188">В показатели метрики, которые можно отображать в обозревателе метрики, входит набор системных счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="ff90d-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="ff90d-189">В готовой колонке **Серверы** отображается несколько таких счетчиков.</span><span class="sxs-lookup"><span data-stu-id="ff90d-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Откройте ресурс Application Insights и щелкните "Серверы".](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="ff90d-191">Если данные счетчика производительности не отображаются</span><span class="sxs-lookup"><span data-stu-id="ff90d-191">If you see no performance counter data</span></span>
* <span data-ttu-id="ff90d-192">**Сервер IIS** на собственном компьютере или на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="ff90d-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="ff90d-193">[Установите монитор состояния](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="ff90d-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="ff90d-194">**Веб-сайт Azure** — мы еще не поддерживаем счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="ff90d-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="ff90d-195">Существует несколько метрик, которые можно получить в составе стандартной панели управления веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="ff90d-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="ff90d-196">**Сервер Unix** - [установите collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="ff90d-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="ff90d-197">Для отображения дополнительных счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="ff90d-197">To display more performance counters</span></span>
* <span data-ttu-id="ff90d-198">Сначала [добавьте новую диаграмму](app-insights-metrics-explorer.md) , чтобы посмотреть, находится ли счетчик в базовом наборе предложения.</span><span class="sxs-lookup"><span data-stu-id="ff90d-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="ff90d-199">Если его нет, [добавьте счетчик к набору, собранному модулем счетчика производительности](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="ff90d-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>
