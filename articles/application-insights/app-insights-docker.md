---
title: "приложения aaaMonitor Docker в Azure Application Insights | Документы Microsoft"
description: "Docker счетчики производительности, событий и исключений могут отображаться на Application Insights вместе с hello телеметрии из hello контейнерных приложений."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="7bc8f-103">Мониторинг приложений Docker в Application Insights</span><span class="sxs-lookup"><span data-stu-id="7bc8f-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="7bc8f-104">События жизненного цикла и счетчики производительности из контейнеров [Docker](https://www.docker.com/) можно выводить в виде диаграмм в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="7bc8f-105">Установка hello [Application Insights](app-insights-overview.md) образ контейнера в узле, который отображает счетчики производительности для узла hello, как хорошо как для hello других изображений.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="7bc8f-106">С помощью Docker ваши приложения распространяются в упрощенных контейнерах со всеми зависимостями.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="7bc8f-107">Их можно запустить на любом хост-компьютере с модулем Docker.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="7bc8f-108">При запуске hello [Application Insights изображение](https://hub.docker.com/r/microsoft/applicationinsights/) на узле Docker, вы получаете следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7bc8f-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="7bc8f-109">Жизненный цикл данных телеметрии о всех запущенных контейнеров hello на узле hello - запуск, остановку и т. д.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="7bc8f-110">Счетчики производительности для всех контейнеров hello.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="7bc8f-111">ЦП, память, использование сети и многое другое.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="7bc8f-112">Если вы [установлен пакет SDK Application Insights для Java](app-insights-java-live.md) в hello приложений, выполняющихся в контейнерах hello, все данные телеметрии hello этих приложений будут иметь дополнительные свойства, идентифицирующий контейнера hello и хост-компьютера.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="7bc8f-113">Например, если имеются экземпляры приложения, запущенные на нескольких узлах, вы легко сможете отфильтровать данные телеметрии приложения по узлу.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![пример](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="7bc8f-115">Настройка ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="7bc8f-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="7bc8f-116">Вход в [портал Microsoft Azure](https://azure.com) и открыть ресурс Application Insights hello для вашего приложения; или [создайте новую](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7bc8f-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="7bc8f-117">*Какой ресурс использовать?*</span><span class="sxs-lookup"><span data-stu-id="7bc8f-117">*Which resource should I use?*</span></span> <span data-ttu-id="7bc8f-118">Если были разработаны hello приложений, работающих на узле другим пользователем, то нужно слишком[создать новый ресурс Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7bc8f-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="7bc8f-119">Это, где Просмотр и анализ телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="7bc8f-120">(Выберите «Общие» для типа приложения hello).</span><span class="sxs-lookup"><span data-stu-id="7bc8f-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="7bc8f-121">Но если вы разработчик приложения hello hello, затем мы надеемся, что вы [добавить пакет SDK Application Insights](app-insights-java-live.md) tooeach из них.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="7bc8f-122">Если они все компоненты действительно одной бизнес-приложения, то можно настроить все из них toosend телеметрии tooone ресурсов, и будет использовать те же самые ресурсов toodisplay hello Docker жизненный цикл и производительности данные.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="7bc8f-123">Третий сценарий, разработанных большинство приложений hello, что вы используете отдельные ресурсы toodisplay их телеметрии.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="7bc8f-124">В этом случае вы, вероятно, также требуется toocreate отдельный ресурс для hello данных Docker.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="7bc8f-125">Добавить плитку Docker hello: выберите **добавить плитку**, перетащите hello Docker плитки из галереи hello и нажмите кнопку **сделать**.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![пример](./media/app-insights-docker/03.png)
3. <span data-ttu-id="7bc8f-127">Нажмите кнопку hello **Essentials** раскрывающийся список и скопируйте ключ инструментирования hello.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="7bc8f-128">Используйте этот tootell hello SDK где toosend его телеметрии.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![пример](./media/app-insights-docker/02-props.png)

<span data-ttu-id="7bc8f-130">Оставьте это окно браузера под рукой, как вы сможете вернуться tooit скоро toolook в телеметрии.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="7bc8f-131">Запустить монитор hello Application Insights на узле</span><span class="sxs-lookup"><span data-stu-id="7bc8f-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="7bc8f-132">Теперь, когда у вас есть где-нибудь toodisplay hello телеметрии, можно настроить приложение hello контейнерах, который будет собирать и отправлять их.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="7bc8f-133">Подключите узел Docker tooyour.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="7bc8f-134">Включите свой ключ инструментирования в следующую команду и выполните ее:</span><span class="sxs-lookup"><span data-stu-id="7bc8f-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="7bc8f-135">Для каждого узла Docker требуется только один образ Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="7bc8f-136">Если приложение развертывается на нескольких узлах Docker, затем повторите команду hello на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="7bc8f-137">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="7bc8f-137">Update your app</span></span>
<span data-ttu-id="7bc8f-138">Если приложение инструментируется hello [пакет SDK Application Insights для Java](app-insights-java-get-started.md), добавить следующие строки в файл ApplicationInsights.xml hello в вашем проекте, в списке hello hello `<TelemetryInitializers>` элемента:</span><span class="sxs-lookup"><span data-stu-id="7bc8f-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="7bc8f-139">Это добавляет сведения о Docker, например контейнером и узлом идентификатор tooevery телеметрии item отправляемых из приложения.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="7bc8f-140">Просмотр телеметрии</span><span class="sxs-lookup"><span data-stu-id="7bc8f-140">View your telemetry</span></span>
<span data-ttu-id="7bc8f-141">Вы можете вернуться tooyour ресурс Application Insights в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="7bc8f-142">Пролистайте hello Docker плитки.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="7bc8f-143">Скоро появится данных, поступающих из приложения hello Docker, особенно в том случае, если у вас есть другие контейнеры, работающих на ваш подсистемы Docker.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="7bc8f-144">Ниже приведены некоторые hello представления, которые можно получить.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="7bc8f-145">Счетчики производительности узла, активность образа</span><span class="sxs-lookup"><span data-stu-id="7bc8f-145">Perf counters by host, activity by image</span></span>
![пример](./media/app-insights-docker/10.png)

![пример](./media/app-insights-docker/11.png)

<span data-ttu-id="7bc8f-148">Щелкните имя любого узла или образа, чтобы получить подробные данные.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="7bc8f-149">представление toocustomize hello, щелкните любой диаграммы, заголовок сетки hello, или добавить диаграмму следует использовать.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="7bc8f-150">[Ознакомьтесь с дополнительными сведениями об обозревателе метрик](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="7bc8f-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="7bc8f-151">События контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="7bc8f-151">Docker container events</span></span>
![пример](./media/app-insights-docker/13.png)

<span data-ttu-id="7bc8f-153">tooinvestigate отдельные события, щелкните [поиска](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="7bc8f-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="7bc8f-154">Поиск и фильтрация событий toofind hello.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="7bc8f-155">Выберите любое событие tooget более подробно.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="7bc8f-156">Исключения по имени контейнера</span><span class="sxs-lookup"><span data-stu-id="7bc8f-156">Exceptions by container name</span></span>
![пример](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="7bc8f-158">Docker контекст добавлен tooapp телеметрии</span><span class="sxs-lookup"><span data-stu-id="7bc8f-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="7bc8f-159">Запрос телеметрии передается из приложения hello встроены AI SDK, также Docker контекста:</span><span class="sxs-lookup"><span data-stu-id="7bc8f-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![пример](./media/app-insights-docker/16.png)

<span data-ttu-id="7bc8f-161">Счетчики производительности для загруженности процессора и доступной памяти, насыщенные, дополненные и сгруппированные по имени контейнера Docker:</span><span class="sxs-lookup"><span data-stu-id="7bc8f-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![пример](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="7bc8f-163">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="7bc8f-163">Q & A</span></span>
<span data-ttu-id="7bc8f-164">*Какие возможности Application Insights отсутствуют в Docker?*</span><span class="sxs-lookup"><span data-stu-id="7bc8f-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="7bc8f-165">Подробные показатели счетчиков производительности по контейнерам и образам.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="7bc8f-166">Интегрированные данные контейнера и приложения на одной панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="7bc8f-167">[Экспортировать данные телеметрии](app-insights-export-telemetry.md) для дальнейшего анализа tooa базы данных Power BI или другие панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="7bc8f-168">*Получение телеметрии из самого приложения hello*</span><span class="sxs-lookup"><span data-stu-id="7bc8f-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="7bc8f-169">Установите пакет SDK Application Insights hello в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7bc8f-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="7bc8f-170">Узнайте, как это сделать в [веб-приложениях Java](app-insights-java-get-started.md) и [Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="7bc8f-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="7bc8f-171">Видео</span><span class="sxs-lookup"><span data-stu-id="7bc8f-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="7bc8f-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7bc8f-172">Next steps</span></span>

* [<span data-ttu-id="7bc8f-173">Application Insights для Java</span><span class="sxs-lookup"><span data-stu-id="7bc8f-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="7bc8f-174">Application Insights для Node.js</span><span class="sxs-lookup"><span data-stu-id="7bc8f-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="7bc8f-175">Application Insights для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7bc8f-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
