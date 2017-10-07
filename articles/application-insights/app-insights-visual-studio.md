---
title: "aaaDebug приложений с Azure Application Insights в Visual Studio | Документы Microsoft"
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
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="7f806-103">Отладка приложений с помощью Azure Application Insights в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f806-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="7f806-104">В Visual Studio 2015 и более поздних версиях можно анализировать производительность веб-приложения ASP.NET и диагностировать проблемы во время отладки и в рабочей среде с помощью телеметрии из [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7f806-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="7f806-105">Если вы создали веб-приложения ASP.NET с помощью Visual Studio 2017 г. или более поздней версии, уже имеет hello пакет SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7f806-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="7f806-106">В противном случае, если вы еще не сделали этого, [добавить Application Insights tooyour приложение](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="7f806-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="7f806-107">toomonitor приложения, когда он находится в производственной, обычно просмотре телеметрии Application Insights hello в hello [портал Azure](https://portal.azure.com), где можно настроить оповещения и применить высокоэффективных средств мониторинга.</span><span class="sxs-lookup"><span data-stu-id="7f806-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="7f806-108">Однако для отладки, можно также выполнить поиск и анализ телеметрии hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f806-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="7f806-109">Можно использовать Visual Studio tooanalyze телеметрии из производственного сайта и отладка выполняется на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="7f806-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="7f806-110">В последнем случае hello даже если вы еще не настроили hello SDK toosend телеметрии toohello портал Azure можно анализировать отладки запусков.</span><span class="sxs-lookup"><span data-stu-id="7f806-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="7f806-111"><a name="run"></a> Отладка проекта</span><span class="sxs-lookup"><span data-stu-id="7f806-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="7f806-112">Нажмите клавишу F5, чтобы запустить веб-приложение в режиме локальной отладки.</span><span class="sxs-lookup"><span data-stu-id="7f806-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="7f806-113">Откройте некоторые телеметрии toogenerate разным страницам.</span><span class="sxs-lookup"><span data-stu-id="7f806-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="7f806-114">В Visual Studio отображается количество hello событий, зарегистрированных модулем hello Application Insights в проект.</span><span class="sxs-lookup"><span data-stu-id="7f806-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![В Visual Studio hello Application Insights кнопка показывает во время отладки.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="7f806-116">Щелкните этот toosearch кнопку телеметрии.</span><span class="sxs-lookup"><span data-stu-id="7f806-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="7f806-117">Поиск Application Insights</span><span class="sxs-lookup"><span data-stu-id="7f806-117">Application Insights search</span></span>
<span data-ttu-id="7f806-118">в окне поиска Application Insights Hello отображаются события, которые были записаны.</span><span class="sxs-lookup"><span data-stu-id="7f806-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="7f806-119">(Если вы вошли в tooAzure при настройке Application Insights, можно выполнить поиск hello того же события в hello портал Azure.)</span><span class="sxs-lookup"><span data-stu-id="7f806-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Щелкните правой кнопкой мыши проект hello и выберите идеи приложения поиска](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="7f806-121">После выбора или отмените выбор фильтров, нажмите кнопку поиска hello в конце hello hello текстовое поле поиска.</span><span class="sxs-lookup"><span data-stu-id="7f806-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="7f806-122">Hello свободного полнотекстовый поиск работает на все поля в событиях hello.</span><span class="sxs-lookup"><span data-stu-id="7f806-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="7f806-123">Например поиск по части hello URL-адрес страницы; или hello значение свойства, такие как город клиентов; или ключевых слов в журнале трассировки.</span><span class="sxs-lookup"><span data-stu-id="7f806-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="7f806-124">Выберите любое событие toosee его подробные свойства.</span><span class="sxs-lookup"><span data-stu-id="7f806-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="7f806-125">Для запросов tooyour веб-приложения можно щелкнуть toohello кода.</span><span class="sxs-lookup"><span data-stu-id="7f806-125">For requests tooyour web app, you can click through toohello code.</span></span>

![В области сведений о запросе нажмите кнопку toohello кода](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="7f806-127">Можно также открыть связанные элементы toohelp диагностики запросов с ошибками или исключения.</span><span class="sxs-lookup"><span data-stu-id="7f806-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![В области сведений о запросе прокрутите вниз элементы toorelated](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="7f806-129">Просмотр исключений и неудачно завершенных запросов</span><span class="sxs-lookup"><span data-stu-id="7f806-129">View exceptions and failed requests</span></span>
<span data-ttu-id="7f806-130">Показать отчеты исключения в окне поиска hello.</span><span class="sxs-lookup"><span data-stu-id="7f806-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="7f806-131">(В некоторых старых типов приложения ASP.NET, у вас есть слишком[настроить отслеживание исключений](app-insights-asp-net-exceptions.md) toosee исключений, которые обрабатываются средой hello.)</span><span class="sxs-lookup"><span data-stu-id="7f806-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="7f806-132">Щелкните исключение tooget трассировку стека.</span><span class="sxs-lookup"><span data-stu-id="7f806-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="7f806-133">Если код hello приложение hello открыт в Visual Studio, можно щелкнуть через из hello трассировки стека toohello соответствующей строки кода hello.</span><span class="sxs-lookup"><span data-stu-id="7f806-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![Трассировка стека исключений](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="7f806-135">Просмотреть сводные данные о запросе и исключение в коде hello</span><span class="sxs-lookup"><span data-stu-id="7f806-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="7f806-136">В hello Code Lens строку выше каждого метода обработчика отображается число запросов hello и исключений, регистрируемых Application Insights в hello за последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="7f806-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![Трассировка стека исключений](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="7f806-138">Code Lens показывает только данные Application Insights, если у вас есть [настроены на портале Application Insights toosend телеметрии приложения toohello](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="7f806-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="7f806-139">Телеметрия Application Insights в Visual Studio CodeLens</span><span class="sxs-lookup"><span data-stu-id="7f806-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="7f806-140">Тренды</span><span class="sxs-lookup"><span data-stu-id="7f806-140">Trends</span></span>
<span data-ttu-id="7f806-141">Тренды — это средство для визуализации того, как изменяется поведение приложения со временем.</span><span class="sxs-lookup"><span data-stu-id="7f806-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="7f806-142">Выберите **исследовать тенденции телеметрии** из окна поиска Application Insights или кнопки панели инструментов hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7f806-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="7f806-143">Выберите один из пяти общие запросы tooget работы.</span><span class="sxs-lookup"><span data-stu-id="7f806-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="7f806-144">Анализировать разные наборы данных можно на основе типов данных телеметрии, диапазонов времени и других свойств.</span><span class="sxs-lookup"><span data-stu-id="7f806-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="7f806-145">toofind аномалий в данных, выберите один из вариантов аномалий hello в раскрывающемся списке «Тип представления» hello.</span><span class="sxs-lookup"><span data-stu-id="7f806-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="7f806-146">параметры фильтрации Hello hello нижней части окна hello позволяют легко toohone в на определенные подмножества телеметрии.</span><span class="sxs-lookup"><span data-stu-id="7f806-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![Тренды](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="7f806-148">[Дополнительные сведения о тенденциях](app-insights-visual-studio-trends.md)</span><span class="sxs-lookup"><span data-stu-id="7f806-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="7f806-149">Локальный мониторинг</span><span class="sxs-lookup"><span data-stu-id="7f806-149">Local monitoring</span></span>
<span data-ttu-id="7f806-150">(Из Visual Studio 2015 с обновлением 2) Если вы не еще настроили hello SDK toosend телеметрии toohello портале Application Insights (что в файле ApplicationInsights.config отсутствует ключ инструментирования) окно диагностики hello отображает телеметрии из сеанса последние отладки.</span><span class="sxs-lookup"><span data-stu-id="7f806-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="7f806-151">Это предпочтительно, если вы уже опубликовали предыдущую версию своего приложения.</span><span class="sxs-lookup"><span data-stu-id="7f806-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="7f806-152">Вы не хотите hello телеметрии из вашего отладки toobe сеансы смешивать hello телеметрии на hello портале Application Insights из опубликованного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7f806-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="7f806-153">Также полезно при наличии некоторые [пользовательского телеметрии](app-insights-api-custom-events-metrics.md) требуется toodebug перед отправкой телеметрии toohello портала.</span><span class="sxs-lookup"><span data-stu-id="7f806-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="7f806-154">*Сначала я настроил полностью портале toohello телеметрии Application Insights toosend. Но сейчас я хочу телеметрии hello toosee только в Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="7f806-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="7f806-155">В параметрах окна поиска hello нет диагностики локальный параметр toosearch даже если приложение отправляет данные телеметрии toohello портала.</span><span class="sxs-lookup"><span data-stu-id="7f806-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="7f806-156">toostop телеметрии, отправляемых toohello портала, закомментируйте строку hello `<instrumentationkey>...` из ApplicationInsights.config. Когда вы будете готовы toosend телеметрии toohello портала раскомментируйте ее.</span><span class="sxs-lookup"><span data-stu-id="7f806-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7f806-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f806-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="7f806-158">**[Добавление данных](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="7f806-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="7f806-159">Мониторинг использования, доступности, зависимостей и исключений.</span><span class="sxs-lookup"><span data-stu-id="7f806-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="7f806-160">Интеграция трассировок из платформ ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="7f806-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="7f806-161">Написание пользовательской телеметрии.</span><span class="sxs-lookup"><span data-stu-id="7f806-161">Write custom telemetry.</span></span> |![Visual studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="7f806-163">**[Работа с порталом Application Insights hello](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="7f806-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="7f806-164">Просмотр панелей мониторинга, эффективных средств диагностики и анализа, оповещений, карты динамических зависимостей приложения, а также экспортированных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="7f806-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual studio](./media/app-insights-visual-studio/62.png) |

