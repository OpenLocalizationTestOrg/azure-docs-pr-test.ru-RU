---
title: "Azure Application Insights для ASP.NET Core | Документация Майкрософт"
description: "Отслеживайте доступность, производительность и использование веб-приложений."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d86495eea467977f6c079de72e2b49a2a1da2b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="0245d-103">Application Insights для ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="0245d-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="0245d-104">[Application Insights](app-insights-overview.md) позволяет осуществлять мониторинг доступности, производительности и использования вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0245d-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="0245d-105">Благодаря получаемым данным о производительности и эффективности работы приложения на практике вы можете принимать осознанные решения о направлении разработки в каждом жизненном цикле.</span><span class="sxs-lookup"><span data-stu-id="0245d-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span></span>

![Пример](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="0245d-107">Вам потребуется подписка [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="0245d-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="0245d-108">Войдите, используя учетную запись Майкрософт, которая уже может быть у вас для Windows, XBox Live или других облачных служб Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0245d-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="0245d-109">Возможно, у вашей группы есть подписка организации Azure: попросите ее владельца добавить вас к ней с помощью вашей учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0245d-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0245d-110">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="0245d-110">Getting started</span></span>

* <span data-ttu-id="0245d-111">В обозревателе решений Visual Studio щелкните проект правой кнопкой мыши и выберите **Настроить Application Insights** или **Добавить > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="0245d-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="0245d-112">[Подробнее](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="0245d-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="0245d-113">Если вы не видите эти пункты меню, следуйте указаниям в [руководстве по началу работы вручную](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="0245d-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="0245d-114">Это может потребоваться, если проект был создан в версии Visual Studio, предшествующей Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="0245d-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="0245d-115">Работа с Application Insights</span><span class="sxs-lookup"><span data-stu-id="0245d-115">Using Application Insights</span></span>
<span data-ttu-id="0245d-116">Войдите на [портал Microsoft Azure](https://portal.azure.com), выберите **Все ресурсы** или **Application Insights** и выберите ресурс, созданный для отслеживания работы приложения.</span><span class="sxs-lookup"><span data-stu-id="0245d-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span></span>

<span data-ttu-id="0245d-117">В отдельном окне браузера некоторое время поработайте с приложением.</span><span class="sxs-lookup"><span data-stu-id="0245d-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="0245d-118">Вы увидите, что в диаграммах Application Insights появятся данные.</span><span class="sxs-lookup"><span data-stu-id="0245d-118">You'll see data appearing in the Application Insights charts.</span></span> <span data-ttu-id="0245d-119">(Возможно, потребуется нажать кнопку "Обновить".) Во время разработки объем этих данных будет небольшим, однако эти диаграммы станут по-настоящему полезными после публикации приложения, когда их будет использовать много пользователей.</span><span class="sxs-lookup"><span data-stu-id="0245d-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="0245d-120">На странице обзора отображаются ключевые диаграммы: время ответа сервера, время загрузки страницы и количество неудачных запросов.</span><span class="sxs-lookup"><span data-stu-id="0245d-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="0245d-121">Щелкните любую диаграмму, чтобы просмотреть другие диаграммы и данные.</span><span class="sxs-lookup"><span data-stu-id="0245d-121">Click any chart to see more charts and data.</span></span>

<span data-ttu-id="0245d-122">Представления на портале делятся на три основные категории.</span><span class="sxs-lookup"><span data-stu-id="0245d-122">Views in the portal fall into three main categories:</span></span>

* <span data-ttu-id="0245d-123">[Обозреватель метрик](app-insights-metrics-explorer.md) выводит на экран графики, таблицы метрик и счетчики, такие как время ответа, доля сбоев или метрики, которые вы создаете самостоятельно с помощью [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0245d-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="0245d-124">Вы можете выполнить фильтрацию и сегментацию данных по значениям свойств, чтобы лучше понять, как работает приложение и его пользователи.</span><span class="sxs-lookup"><span data-stu-id="0245d-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span></span>
* <span data-ttu-id="0245d-125">[Обозреватель поиска](app-insights-diagnostic-search.md) перечисляет отдельные события, такие как определенные запросы, исключения, трассировки журналов или события, которые вы создаете самостоятельно с помощью [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0245d-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="0245d-126">Вы можете выполнить фильтрацию и поиск в событиях и переходить между связанными событиями для выявления проблем.</span><span class="sxs-lookup"><span data-stu-id="0245d-126">Filter and search in the events, and navigate among related events to investigate issues.</span></span>
* <span data-ttu-id="0245d-127">[Analytics](app-insights-analytics.md) позволяет выполнять SQL-подобные запросы данных телеметрии и является мощным средством диагностики и анализа.</span><span class="sxs-lookup"><span data-stu-id="0245d-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="0245d-128">Оповещения</span><span class="sxs-lookup"><span data-stu-id="0245d-128">Alerts</span></span>
* <span data-ttu-id="0245d-129">Вы автоматически получаете [оповещения превентивной диагностики](app-insights-proactive-diagnostics.md), которые сообщают о необычных изменениях в частоте сбоев и других метриках.</span><span class="sxs-lookup"><span data-stu-id="0245d-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="0245d-130">Настройте [тесты доступности](app-insights-monitor-web-app-availability.md) для постоянного тестирования веб-сайта из расположений по всему миру и немедленного получения сообщений электронной почты в случае сбоя проверки.</span><span class="sxs-lookup"><span data-stu-id="0245d-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="0245d-131">Настройте [оповещения о метриках](app-insights-monitor-web-app-availability.md) , чтобы получать оповещение о выходе метрик, таких как время отклика или доля исключений, за допустимые границы.</span><span class="sxs-lookup"><span data-stu-id="0245d-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="0245d-132">Видео</span><span class="sxs-lookup"><span data-stu-id="0245d-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="0245d-133">Открытый исходный код</span><span class="sxs-lookup"><span data-stu-id="0245d-133">Open source</span></span>
[<span data-ttu-id="0245d-134">Чтение кода и дополнительные наработки</span><span class="sxs-lookup"><span data-stu-id="0245d-134">Read and contribute to the code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="0245d-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0245d-135">Next steps</span></span>
* <span data-ttu-id="0245d-136">[Добавьте данные телеметрии на веб-страницы](app-insights-javascript.md) для мониторинга использования и производительности страниц.</span><span class="sxs-lookup"><span data-stu-id="0245d-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span></span>
* <span data-ttu-id="0245d-137">[Отслеживайте зависимости](app-insights-asp-net-dependencies.md) , чтобы выяснить, что стало причиной медленной работы: REST, SQL или другие внешние ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0245d-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="0245d-138">[Используйте API](app-insights-api-custom-events-metrics.md) для отправки собственных событий и метрик для более четкого представления о производительности и использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="0245d-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="0245d-139">[Тесты доступности](app-insights-monitor-web-app-availability.md) позволяют постоянно проверять работу приложения из всех точек мира.</span><span class="sxs-lookup"><span data-stu-id="0245d-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span></span> 

