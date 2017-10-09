---
title: "aaaMonitor производительности Azure веб-приложения | Документы Microsoft"
description: "Мониторинг производительности веб-приложений Azure. Диаграммы времени загрузки и ответа, информация о зависимостях и настройка оповещений о производительности."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="1d76c-104">Мониторинг производительности веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="1d76c-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="1d76c-105">В hello [портала Azure](https://portal.azure.com) можно настроить наблюдение за производительностью приложений вашей [веб-приложениях Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d76c-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="1d76c-106">[Azure Application Insights](app-insights-overview.md) инструментирует toosend данные телеметрии вашего приложения о toohello его действия служба Application Insights, где он хранится и проанализированы.</span><span class="sxs-lookup"><span data-stu-id="1d76c-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="1d76c-107">Нет, можно использовать диаграммы метрик и средства поиска toohelp диагностики проблем, повышения производительности и оценить использование.</span><span class="sxs-lookup"><span data-stu-id="1d76c-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="1d76c-108">Инструментирование во время выполнения и во время сборки</span><span class="sxs-lookup"><span data-stu-id="1d76c-108">Run time or build time</span></span>
<span data-ttu-id="1d76c-109">Вы можете настроить отслеживание посредством инструментирования приложение hello одним из двух способов:</span><span class="sxs-lookup"><span data-stu-id="1d76c-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="1d76c-110">**Во время выполнения.** Вы можете добавить расширение для мониторинга производительности уже во время работы вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1d76c-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="1d76c-111">Он не требуется toorebuild или переустановите приложение.</span><span class="sxs-lookup"><span data-stu-id="1d76c-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="1d76c-112">Вы получаете стандартный набор пакетов для отслеживания времени отклика, частоты успешных выполнений, исключений, зависимостей и т. д.</span><span class="sxs-lookup"><span data-stu-id="1d76c-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="1d76c-113">**Во время сборки.** Вы можете добавить пакет в код своего приложения на этапе разработки.</span><span class="sxs-lookup"><span data-stu-id="1d76c-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="1d76c-114">Этот способ является более гибким решением.</span><span class="sxs-lookup"><span data-stu-id="1d76c-114">This option is more versatile.</span></span> <span data-ttu-id="1d76c-115">В дополнение toohello же стандартных пакетов, можно написать код toocustomize hello телеметрии или toosend собственные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="1d76c-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="1d76c-116">Войти в определенных действий или запись событий в соответствии с семантикой toohello домена приложения.</span><span class="sxs-lookup"><span data-stu-id="1d76c-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="1d76c-117">Инструментирование во время выполнения с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="1d76c-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="1d76c-118">Если вы уже используете веб-приложения в Azure, то наверняка получили определенные сведения мониторинга, касающиеся частоты запросов и ошибок.</span><span class="sxs-lookup"><span data-stu-id="1d76c-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="1d76c-119">Добавьте дополнительные, например время отклика, мониторинга toodependencies вызовы, смарт-обнаружение и hello мощный язык запросов анализа журналов tooget Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1d76c-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="1d76c-120">**Выберите Application Insights** панели hello Azure управления для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1d76c-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![В разделе "Мониторинг" выберите пункт Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="1d76c-122">Выберите toocreate новый ресурс, если вы уже настроенных ресурс Application Insights для этого приложения другой маршрут.</span><span class="sxs-lookup"><span data-stu-id="1d76c-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="1d76c-123">**Выполните инструментирование веб-приложения** после установки Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1d76c-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Инструментирование веб-приложения](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="1d76c-125">**Включите мониторинг на стороне клиента** для получения сведений о просмотрах страниц и данных телеметрии пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d76c-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="1d76c-126">Выберите элементы "Параметры > Параметры приложения".</span><span class="sxs-lookup"><span data-stu-id="1d76c-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="1d76c-127">В разделе "Параметры приложения" добавьте новую пару "ключ — значение":</span><span class="sxs-lookup"><span data-stu-id="1d76c-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="1d76c-128">Ключ: `APPINSIGHTS_JAVASCRIPT_ENABLED`.</span><span class="sxs-lookup"><span data-stu-id="1d76c-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="1d76c-129">Значение: `true`</span><span class="sxs-lookup"><span data-stu-id="1d76c-129">Value: `true`</span></span>
   * <span data-ttu-id="1d76c-130">**Сохранить** hello параметры и **перезапустите** приложения.</span><span class="sxs-lookup"><span data-stu-id="1d76c-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="1d76c-131">**Отслеживайте работу приложения**.</span><span class="sxs-lookup"><span data-stu-id="1d76c-131">**Monitor your app**.</span></span>  <span data-ttu-id="1d76c-132">[Данные hello Expore](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="1d76c-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="1d76c-133">Более поздней версии Если требуется, можно построить приложение hello с помощью Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1d76c-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="1d76c-134">*Как удалить Application Insights, или переключиться toosending tooanother ресурсов?*</span><span class="sxs-lookup"><span data-stu-id="1d76c-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="1d76c-135">В колонке управления Привет открыть web приложения Azure и средств разработки откройте **расширения**.</span><span class="sxs-lookup"><span data-stu-id="1d76c-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="1d76c-136">Удалите расширение Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="1d76c-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="1d76c-137">Затем в разделе наблюдения, выберите Application Insights и создайте или выберите ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="1d76c-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="1d76c-138">Создать приложение hello с Application Insights</span><span class="sxs-lookup"><span data-stu-id="1d76c-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="1d76c-139">Установите пакет SDK в свое приложение, чтобы воспользоваться более подробными сведениями телеметрии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1d76c-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="1d76c-140">В частности, можно собирать журналы трассировки, [написать код пользовательской телеметрии](app-insights-api-custom-events-metrics.md) и получать более подробные отчеты об исключениях.</span><span class="sxs-lookup"><span data-stu-id="1d76c-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="1d76c-141">**В Visual Studio** (2013 года с обновлением 2 или более поздней версии) настройте Application Insights для проекта.</span><span class="sxs-lookup"><span data-stu-id="1d76c-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="1d76c-142">Щелкните правой кнопкой мыши hello веб-проекта и выберите **Добавить > Application Insights** или **настроить Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="1d76c-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Щелкните правой кнопкой мыши hello веб-проекта и нажмите кнопку Добавить или настроить Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="1d76c-144">В ответ на вопрос toosign в, используйте hello учетные данные для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="1d76c-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="1d76c-145">Операция Hello оказывает влияние на два.</span><span class="sxs-lookup"><span data-stu-id="1d76c-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="1d76c-146">Создает ресурс Application Insights, в котором выполняется отображение, хранение и анализ данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="1d76c-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="1d76c-147">Добавляет hello NuGet аналитики приложений tooyour кода пакета (если она еще не существует) и настраивает его toohello телеметрии toosend ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1d76c-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="1d76c-148">**Тестирование телеметрии hello** , выполняемого приложения hello в компьютере разработки (F5).</span><span class="sxs-lookup"><span data-stu-id="1d76c-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="1d76c-149">**Публикация приложения hello** tooAzure в hello обычным способом.</span><span class="sxs-lookup"><span data-stu-id="1d76c-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="1d76c-150">*Как переключаться toosending tooa другого ресурса Application Insights?*</span><span class="sxs-lookup"><span data-stu-id="1d76c-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="1d76c-151">В Visual Studio, щелкните правой кнопкой мыши проект hello, выберите **настроить Application Insights** и выберите ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="1d76c-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="1d76c-152">Параметр toocreate hello получить новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="1d76c-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="1d76c-153">заново собрать или повторно развернуть ресурс.</span><span class="sxs-lookup"><span data-stu-id="1d76c-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="1d76c-154">Просмотр данных hello</span><span class="sxs-lookup"><span data-stu-id="1d76c-154">Explore hello data</span></span>
1. <span data-ttu-id="1d76c-155">В колонке hello Application Insights для вашего веб-приложения управления панели отображается Live метрик, которые показывает запросов и ошибок в секунду или две из них происходит.</span><span class="sxs-lookup"><span data-stu-id="1d76c-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="1d76c-156">Эти отображаемые данные очень полезны в случае повторной публикации приложения, так как любые проблемы можно увидеть немедленно.</span><span class="sxs-lookup"><span data-stu-id="1d76c-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="1d76c-157">Пролистайте toohello полный ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1d76c-157">Click through toohello full Application Insights resource.</span></span>

    ![Щелкните](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="1d76c-159">Вы также можете перейти непосредственно по ссылке из ресурсов навигации Azure.</span><span class="sxs-lookup"><span data-stu-id="1d76c-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="1d76c-160">Пролистайте любой диаграммы tooget более подробно:</span><span class="sxs-lookup"><span data-stu-id="1d76c-160">Click through any chart tooget more detail:</span></span>
   
    ![В колонке Обзор hello Application Insights щелкните диаграмму](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="1d76c-162">Вы можете [настроить колонки метрик](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="1d76c-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="1d76c-163">Переходите дальнейшей toosee отдельные события и их свойств.</span><span class="sxs-lookup"><span data-stu-id="1d76c-163">Click through further toosee individual events and their properties:</span></span>
   
    ![Нажмите кнопку tooopen тип события, поиска, отфильтрованные по этому типу](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="1d76c-165">Обратите внимание, «...» Здравствуйте, tooopen ссылку все свойства.</span><span class="sxs-lookup"><span data-stu-id="1d76c-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="1d76c-166">Вы можете [настроить поисковые запросы](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="1d76c-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="1d76c-167">Для расширенного поиска по телеметрии использовать hello [языка запросов анализа журналов](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="1d76c-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="1d76c-168">Дополнительные данные телеметрии</span><span class="sxs-lookup"><span data-stu-id="1d76c-168">More telemetry</span></span>

* [<span data-ttu-id="1d76c-169">Данные о загрузке веб-страницы</span><span class="sxs-lookup"><span data-stu-id="1d76c-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="1d76c-170">Пользовательская телеметрия</span><span class="sxs-lookup"><span data-stu-id="1d76c-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="1d76c-171">Видео</span><span class="sxs-lookup"><span data-stu-id="1d76c-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="1d76c-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d76c-172">Next steps</span></span>
* <span data-ttu-id="1d76c-173">[Запустите профилировщик hello в работающем приложении](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="1d76c-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="1d76c-174">[Функции Azure.](https://github.com/christopheranderson/azure-functions-app-insights-sample) Отслеживайте функции Azure с помощью Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1d76c-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="1d76c-175">[Включение диагностики Azure](app-insights-azure-diagnostics.md) tooApplication toobe отправлено аналитики.</span><span class="sxs-lookup"><span data-stu-id="1d76c-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="1d76c-176">[Отслеживать показатели работоспособности службы](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="1d76c-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="1d76c-177">[Получайте уведомления](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) при возникновении операционных событий или превышении пороговых значений метрик.</span><span class="sxs-lookup"><span data-stu-id="1d76c-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="1d76c-178">Используйте [Application Insights для приложений JavaScript и веб-страницы](app-insights-javascript.md) tooget телеметрии клиента с помощью браузеров hello, посетите веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="1d76c-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="1d76c-179">[Настройка доступности веб-тесты](app-insights-monitor-web-app-availability.md) toobe оповещение, если сайт не работает.</span><span class="sxs-lookup"><span data-stu-id="1d76c-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

