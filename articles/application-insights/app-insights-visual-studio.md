---
title: "Отладка приложений с помощью Azure Application Insights в Visual Studio |Документы Майкрософт"
description: "Анализ производительности веб-приложения и диагностика во время отладки и в рабочей среде."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="0ba42-103">Отладка приложений с помощью Azure Application Insights в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ba42-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="0ba42-104">В Visual Studio 2015 и более поздних версиях можно анализировать производительность веб-приложения ASP.NET и диагностировать проблемы во время отладки и в рабочей среде с помощью телеметрии из [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ba42-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="0ba42-105">Если вы создали веб-приложение ASP.NET с помощью Visual Studio 2017 или более поздней версии, оно уже содержит пакет SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ba42-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="0ba42-106">Если вы используете другую версию, [добавьте Application Insights в свое приложение](app-insights-asp-net.md), если вы еще это не сделали.</span><span class="sxs-lookup"><span data-stu-id="0ba42-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="0ba42-107">Чтобы отслеживать приложение в рабочей среде, можно просматривать данные телеметрии Application Insights на [портале](https://portal.azure.com) (там же можно настроить оповещения и применить эффективные средства мониторинга).</span><span class="sxs-lookup"><span data-stu-id="0ba42-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="0ba42-108">Но для приложения в состоянии отладки можно также искать и анализировать данные телеметрии в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ba42-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="0ba42-109">С помощью Visual Studio вы можете анализировать телеметрию рабочего сайта и выполнения отладки на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="0ba42-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="0ba42-110">В последнем случае вы можете анализировать выполнения отладки, даже если вы еще не настроили пакет SDK для отправки данных телеметрии на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0ba42-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="0ba42-111"><a name="run"></a> Отладка проекта</span><span class="sxs-lookup"><span data-stu-id="0ba42-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="0ba42-112">Нажмите клавишу F5, чтобы запустить веб-приложение в режиме локальной отладки.</span><span class="sxs-lookup"><span data-stu-id="0ba42-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="0ba42-113">Откройте разные страницы, чтобы создать некоторый объем данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0ba42-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="0ba42-114">В Visual Studio вы видите число событий, которые были зарегистрированы модулем Application Insights в вашем проекте.</span><span class="sxs-lookup"><span data-stu-id="0ba42-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![В Visual Studio кнопка Application Insights доступна во время отладки.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="0ba42-116">Нажмите эту кнопку для поиска данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0ba42-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="0ba42-117">Поиск Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ba42-117">Application Insights search</span></span>
<span data-ttu-id="0ba42-118">В окне поиска Application Insights отображаются события, которые были зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="0ba42-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="0ba42-119">(Если во время настройки Application Insights вы вошли в Azure, эти же события вы можете найти на портале Azure.)</span><span class="sxs-lookup"><span data-stu-id="0ba42-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![Щелкните проект правой кнопкой мыши и последовательно выберите пункты "Application Insights" и "Поиск".](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="0ba42-121">Выберите фильтры или отмените их выбор. Нажмите кнопку поиска в конце текстового поля поиска.</span><span class="sxs-lookup"><span data-stu-id="0ba42-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="0ba42-122">Бесплатный полнотекстовый поиск охватывает все поля в журнале событий.</span><span class="sxs-lookup"><span data-stu-id="0ba42-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="0ba42-123">Например, можно выполнить поиск по фрагменту URL-адреса страницы, а также по значению свойства (например, город клиента) или ключевым словам в журнале трассировки.</span><span class="sxs-lookup"><span data-stu-id="0ba42-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="0ba42-124">Выберите любое событие, чтобы подробно просмотреть его свойства.</span><span class="sxs-lookup"><span data-stu-id="0ba42-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="0ba42-125">Чтобы выполнить запрос к веб-приложению, щелкните код.</span><span class="sxs-lookup"><span data-stu-id="0ba42-125">For requests to your web app, you can click through to the code.</span></span>

![В разделе сведений о запросе щелкните код](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="0ba42-127">Чтобы продиагностировать невыполненные запросы или исключения, вы можете открыть связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="0ba42-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![В разделе сведений о запросе прокрутите страницу вниз до связанных элементов](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="0ba42-129">Просмотр исключений и неудачно завершенных запросов</span><span class="sxs-lookup"><span data-stu-id="0ba42-129">View exceptions and failed requests</span></span>
<span data-ttu-id="0ba42-130">Отчеты об исключениях отображаются в окне поиска.</span><span class="sxs-lookup"><span data-stu-id="0ba42-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="0ba42-131">В некоторых типах приложений ASP.NET предыдущих версий необходимо [настроить отслеживание исключений](app-insights-asp-net-exceptions.md), чтобы просматривать исключения, которые обрабатываются платформой.</span><span class="sxs-lookup"><span data-stu-id="0ba42-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="0ba42-132">Щелкните исключение, чтобы просмотреть трассировку стека.</span><span class="sxs-lookup"><span data-stu-id="0ba42-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="0ba42-133">Если код приложения открыт в среде Visual Studio, можно щелкнуть трассировку стека в соответствующей строке кода.</span><span class="sxs-lookup"><span data-stu-id="0ba42-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![Трассировка стека исключений](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="0ba42-135">Просмотр сводки по запросам и исключениям в коде</span><span class="sxs-lookup"><span data-stu-id="0ba42-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="0ba42-136">В строке CodeLens над каждым методом-обработчиком указано число запросов и исключений, зарегистрированных Application Insights за последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="0ba42-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![Трассировка стека исключений](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="0ba42-138">Группа связанных элементов кода показывает данные Application Insights, только если вы [настроили приложение для отправки данных телеметрии на портал Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="0ba42-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="0ba42-139">Телеметрия Application Insights в Visual Studio CodeLens</span><span class="sxs-lookup"><span data-stu-id="0ba42-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="0ba42-140">Тренды</span><span class="sxs-lookup"><span data-stu-id="0ba42-140">Trends</span></span>
<span data-ttu-id="0ba42-141">Тренды — это средство для визуализации того, как изменяется поведение приложения со временем.</span><span class="sxs-lookup"><span data-stu-id="0ba42-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="0ba42-142">Нажмите кнопку **Обзор трендов телеметрии** на панели инструментов Application Insights или в окне поиска Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ba42-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="0ba42-143">Выберите один из пяти стандартных запросов, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="0ba42-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="0ba42-144">Анализировать разные наборы данных можно на основе типов данных телеметрии, диапазонов времени и других свойств.</span><span class="sxs-lookup"><span data-stu-id="0ba42-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="0ba42-145">Чтобы найти аномалии в данных, выберите один из вариантов аномалий в раскрывающемся списке "Тип представления".</span><span class="sxs-lookup"><span data-stu-id="0ba42-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="0ba42-146">Параметры фильтрации в нижней части окна позволяют легко находить конкретные подмножества данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0ba42-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![Тренды](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="0ba42-148">[Дополнительные сведения о тенденциях](app-insights-visual-studio-trends.md)</span><span class="sxs-lookup"><span data-stu-id="0ba42-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="0ba42-149">Локальный мониторинг</span><span class="sxs-lookup"><span data-stu-id="0ba42-149">Local monitoring</span></span>
<span data-ttu-id="0ba42-150">(Относится к Visual Studio 2015 с обновлением 2) Если ваш пакет SDK не отправляет данные телеметрии на портал Application Insights (то есть в файле ApplicationInsights.config нет ключа инструментирования), в окне диагностики выводятся данные телеметрии, полученные в ходе последнего сеанса отладки.</span><span class="sxs-lookup"><span data-stu-id="0ba42-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="0ba42-151">Это предпочтительно, если вы уже опубликовали предыдущую версию своего приложения.</span><span class="sxs-lookup"><span data-stu-id="0ba42-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="0ba42-152">Кроме того, не рекомендуется, чтобы данные телеметрии, полученные на ваших сеансах отладки, смешивались с данными телеметрии на портале Application Insights, полученными от опубликованного приложения.</span><span class="sxs-lookup"><span data-stu-id="0ba42-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="0ba42-153">Это также полезно, если у вас есть [данные пользовательской телеметрии](app-insights-api-custom-events-metrics.md) , которые необходимо отладить перед отправкой на портал.</span><span class="sxs-lookup"><span data-stu-id="0ba42-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="0ba42-154">*Сначала мы полностью настроили Application Insights для отправки данных телеметрии на портал. Но теперь нужно, чтобы данные телеметрии отображались только в Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="0ba42-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="0ba42-155">В параметрах окна поиска можно включить поиск локальной диагностики, который будет выполняться, даже если ваше приложение отправляет данные телеметрии на портал.</span><span class="sxs-lookup"><span data-stu-id="0ba42-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="0ba42-156">Чтобы остановить отправку данных телеметрии на портал, закомментируйте строку `<instrumentationkey>...` в файле ApplicationInsights.config. Когда данные телеметрии будут готовы к отправке на портал, раскомментируйте ее.</span><span class="sxs-lookup"><span data-stu-id="0ba42-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0ba42-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ba42-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="0ba42-158">**[Добавление данных](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="0ba42-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="0ba42-159">Мониторинг использования, доступности, зависимостей и исключений.</span><span class="sxs-lookup"><span data-stu-id="0ba42-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="0ba42-160">Интеграция трассировок из платформ ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="0ba42-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="0ba42-161">Написание пользовательской телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0ba42-161">Write custom telemetry.</span></span> |![Visual studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="0ba42-163">**[Работа с порталом Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="0ba42-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="0ba42-164">Просмотр панелей мониторинга, эффективных средств диагностики и анализа, оповещений, карты динамических зависимостей приложения, а также экспортированных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0ba42-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual studio](./media/app-insights-visual-studio/62.png) |

