---
title: "aaaAzure Application Insights для ASP.NET Core | Документы Microsoft"
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
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="4707c-103">Application Insights для ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4707c-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="4707c-104">[Application Insights](app-insights-overview.md) позволяет осуществлять мониторинг доступности, производительности и использования вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4707c-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="4707c-105">Отзыв hello, получаемых о hello производительность и эффективность работы приложения в hello подстановки можно сделать правильный выбор hello направления проектирования hello в каждом жизненного цикла разработки.</span><span class="sxs-lookup"><span data-stu-id="4707c-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![Пример](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="4707c-107">Вам потребуется подписка [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="4707c-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="4707c-108">Войдите, используя учетную запись Майкрософт, которая уже может быть у вас для Windows, XBox Live или других облачных служб Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4707c-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="4707c-109">В группу могут входить tooAzure организации подписки: попросите владельца tooadd hello tooit с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4707c-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4707c-110">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="4707c-110">Getting started</span></span>

* <span data-ttu-id="4707c-111">В обозревателе решений Visual Studio щелкните проект правой кнопкой мыши и выберите **Настроить Application Insights** или **Добавить > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="4707c-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="4707c-112">[Подробнее](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="4707c-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="4707c-113">Если вы не видите эти команды меню, выполните hello [вручную getting Started руководства](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="4707c-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="4707c-114">Может потребоваться toodo это если проект был создан с помощью версии Visual Studio до 2017 г.</span><span class="sxs-lookup"><span data-stu-id="4707c-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="4707c-115">Работа с Application Insights</span><span class="sxs-lookup"><span data-stu-id="4707c-115">Using Application Insights</span></span>
<span data-ttu-id="4707c-116">Вход в hello [портал Microsoft Azure](https://portal.azure.com)выберите **все ресурсы** или **Application Insights**, а затем выберите приложение создано toomonitor ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="4707c-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="4707c-117">В отдельном окне браузера некоторое время поработайте с приложением.</span><span class="sxs-lookup"><span data-stu-id="4707c-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="4707c-118">Вы увидите данные в Application Insights диаграммы hello.</span><span class="sxs-lookup"><span data-stu-id="4707c-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="4707c-119">(Может потребоваться tooclick обновления.) Во время разработки объем этих данных будет небольшим, однако эти диаграммы станут по-настоящему полезными после публикации приложения, когда их будет использовать много пользователей.</span><span class="sxs-lookup"><span data-stu-id="4707c-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="4707c-120">страница обзора Hello отображаются графики производительности: время ответа сервера, время загрузки страницы, а также счетчики запросов с ошибками.</span><span class="sxs-lookup"><span data-stu-id="4707c-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="4707c-121">Щелкните любой диаграммы toosee дополнительные диаграммы и данных.</span><span class="sxs-lookup"><span data-stu-id="4707c-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="4707c-122">Представления в портале hello делятся на три основные категории:</span><span class="sxs-lookup"><span data-stu-id="4707c-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="4707c-123">[Обозреватель метрик](app-insights-metrics-explorer.md) показано диаграмм и таблиц, метрики и счетчиков, например, время отклика, сбоев или метрики, созданных вами самостоятельно с hello [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4707c-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="4707c-124">Фильтр и сегмент данных hello путем лучшего понимания приложения и его пользователей tooget значения свойства.</span><span class="sxs-lookup"><span data-stu-id="4707c-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="4707c-125">[Поиск обозреватель](app-insights-diagnostic-search.md) перечислены отдельные события, такие как определенные запросы, исключения, журнала трассировки или события, созданные самостоятельно с hello [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4707c-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="4707c-126">Фильтрации и поиска в событиях hello и переходов между проблемы tooinvestigate связанные события.</span><span class="sxs-lookup"><span data-stu-id="4707c-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="4707c-127">[Analytics](app-insights-analytics.md) позволяет выполнять SQL-подобные запросы данных телеметрии и является мощным средством диагностики и анализа.</span><span class="sxs-lookup"><span data-stu-id="4707c-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="4707c-128">Оповещения</span><span class="sxs-lookup"><span data-stu-id="4707c-128">Alerts</span></span>
* <span data-ttu-id="4707c-129">Вы автоматически получаете [оповещения превентивной диагностики](app-insights-proactive-diagnostics.md), которые сообщают о необычных изменениях в частоте сбоев и других метриках.</span><span class="sxs-lookup"><span data-stu-id="4707c-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="4707c-130">Настройка [тестов доступности](app-insights-monitor-web-app-availability.md) tootest веб-узла постоянно местоположений по всему миру и получите сообщение электронной почты, сразу после сбоя теста.</span><span class="sxs-lookup"><span data-stu-id="4707c-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="4707c-131">Настройка [метрики оповещений](app-insights-monitor-web-app-availability.md) tooknow Если метрик, таких как время ответа или исключение ставки выходит за допустимые границы.</span><span class="sxs-lookup"><span data-stu-id="4707c-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="4707c-132">Видео</span><span class="sxs-lookup"><span data-stu-id="4707c-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="4707c-133">Открытый исходный код</span><span class="sxs-lookup"><span data-stu-id="4707c-133">Open source</span></span>
[<span data-ttu-id="4707c-134">Читать и оставлять toohello кода</span><span class="sxs-lookup"><span data-stu-id="4707c-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="4707c-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4707c-135">Next steps</span></span>
* <span data-ttu-id="4707c-136">[Добавить веб-страницы телеметрии tooyour](app-insights-javascript.md) toomonitor страниц об использовании и производительности.</span><span class="sxs-lookup"><span data-stu-id="4707c-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="4707c-137">[Мониторинг зависимостей](app-insights-asp-net-dependencies.md) toosee Если REST, SQL или другим внешним ресурсам замедляют вы работу.</span><span class="sxs-lookup"><span data-stu-id="4707c-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="4707c-138">[Используйте hello API](app-insights-api-custom-events-metrics.md) toosend собственные события и метрики для более подробного представления производительности и использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="4707c-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="4707c-139">[Проверяет доступность](app-insights-monitor-web-app-availability.md) проверьте приложение постоянно из вокруг Здравствуй, мир.</span><span class="sxs-lookup"><span data-stu-id="4707c-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

