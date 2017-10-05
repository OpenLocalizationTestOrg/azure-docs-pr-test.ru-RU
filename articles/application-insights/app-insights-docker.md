---
title: "Мониторинг приложений Docker в Azure Application Insights | Документация Майкрософт"
description: "Счетчики производительности, события и исключения Docker могут отображаться в Application Insights вместе с данными телеметрии из контейнерных приложений."
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
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="41cb9-103">Мониторинг приложений Docker в Application Insights</span><span class="sxs-lookup"><span data-stu-id="41cb9-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="41cb9-104">События жизненного цикла и счетчики производительности из контейнеров [Docker](https://www.docker.com/) можно выводить в виде диаграмм в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="41cb9-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="41cb9-105">Установите образ [Application Insights](app-insights-overview.md) в контейнер в узле. Он будет отображать счетчики производительности для этого узла, а также для других образов.</span><span class="sxs-lookup"><span data-stu-id="41cb9-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="41cb9-106">С помощью Docker ваши приложения распространяются в упрощенных контейнерах со всеми зависимостями.</span><span class="sxs-lookup"><span data-stu-id="41cb9-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="41cb9-107">Их можно запустить на любом хост-компьютере с модулем Docker.</span><span class="sxs-lookup"><span data-stu-id="41cb9-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="41cb9-108">При запуске [образа Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) в узле Docker вы получите следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="41cb9-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="41cb9-109">Сведения о телеметрии жизненного цикла для всех контейнеров, запущенных на узле, — запуск, остановка и т. д.</span><span class="sxs-lookup"><span data-stu-id="41cb9-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="41cb9-110">Счетчики производительности для всех контейнеров.</span><span class="sxs-lookup"><span data-stu-id="41cb9-110">Performance counters for all the containers.</span></span> <span data-ttu-id="41cb9-111">ЦП, память, использование сети и многое другое.</span><span class="sxs-lookup"><span data-stu-id="41cb9-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="41cb9-112">Если вы [установили пакет SDK для Application Insights для Java](app-insights-java-live.md) в приложениях, выполняющихся в контейнерах, у всех данных телеметрии этих приложений будут дополнительные свойства, идентифицирующие контейнер и хост-компьютер.</span><span class="sxs-lookup"><span data-stu-id="41cb9-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="41cb9-113">Например, если имеются экземпляры приложения, запущенные на нескольких узлах, вы легко сможете отфильтровать данные телеметрии приложения по узлу.</span><span class="sxs-lookup"><span data-stu-id="41cb9-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![пример](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="41cb9-115">Настройка ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="41cb9-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="41cb9-116">Выполните вход на [портал Microsoft Azure](https://azure.com) и [создайте ресурс Application Insights](app-insights-create-new-resource.md) для своего приложения или откройте имеющийся.</span><span class="sxs-lookup"><span data-stu-id="41cb9-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="41cb9-117">*Какой ресурс использовать?*</span><span class="sxs-lookup"><span data-stu-id="41cb9-117">*Which resource should I use?*</span></span> <span data-ttu-id="41cb9-118">Если приложения, которые выполняются на узле, были созданы другим разработчиком, вам потребуется [создать новый ресурс Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="41cb9-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="41cb9-119">Там вы можете просматривать и анализировать данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="41cb9-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="41cb9-120">(Выберите тип приложения "Общее".)</span><span class="sxs-lookup"><span data-stu-id="41cb9-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="41cb9-121">Но если разработчиком приложений являетесь вы, мы надеемся, что вы [добавили пакет SDK для Application Insights](app-insights-java-live.md) в каждое из них.</span><span class="sxs-lookup"><span data-stu-id="41cb9-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="41cb9-122">Если все они действительно являются компонентами одного бизнес-приложения, вы можете настроить их на отправку данных телеметрии в один ресурс, а затем использовать этот ресурс для отображения данных о производительности и жизненном цикле Docker.</span><span class="sxs-lookup"><span data-stu-id="41cb9-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="41cb9-123">Третий сценарий — вы разработали большинство приложений, но используете отдельные ресурсы для отображения их телеметрии.</span><span class="sxs-lookup"><span data-stu-id="41cb9-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="41cb9-124">В этом случае, возможно, вам потребуется создать отдельный ресурс для данных Docker.</span><span class="sxs-lookup"><span data-stu-id="41cb9-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="41cb9-125">Добавьте плитку Docker. Выберите **Добавить плитку**, перетащите плитку Docker из коллекции, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="41cb9-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![пример](./media/app-insights-docker/03.png)
3. <span data-ttu-id="41cb9-127">Щелкните раскрывающийся список **Основные компоненты** и скопируйте ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="41cb9-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="41cb9-128">Этот ключ указывает пакету SDK, куда отправлять данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="41cb9-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![пример](./media/app-insights-docker/02-props.png)

<span data-ttu-id="41cb9-130">Не закрывайте это окно браузера: скоро вы будете просматривать в нем данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="41cb9-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="41cb9-131">Запуск монитора Application Insights на узле</span><span class="sxs-lookup"><span data-stu-id="41cb9-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="41cb9-132">Теперь, когда вы создали ресурс для отображения данных телеметрии, можно настроить контейнерное приложение, которое будет собирать и отправлять их.</span><span class="sxs-lookup"><span data-stu-id="41cb9-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="41cb9-133">Подключитесь к узлу Docker.</span><span class="sxs-lookup"><span data-stu-id="41cb9-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="41cb9-134">Включите свой ключ инструментирования в следующую команду и выполните ее:</span><span class="sxs-lookup"><span data-stu-id="41cb9-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="41cb9-135">Для каждого узла Docker требуется только один образ Application Insights.</span><span class="sxs-lookup"><span data-stu-id="41cb9-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="41cb9-136">Если приложение развертывается на нескольких узлах Docker, выполните эту команду на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="41cb9-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="41cb9-137">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="41cb9-137">Update your app</span></span>
<span data-ttu-id="41cb9-138">Если приложение инструментируется с помощью [пакета SDK для Application Insights для Java](app-insights-java-get-started.md), добавьте следующую строку в файл ApplicationInsights.xml в проекте после элемента `<TelemetryInitializers>`:</span><span class="sxs-lookup"><span data-stu-id="41cb9-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="41cb9-139">Это добавляет сведения телеметрии Docker, такие как контейнер и идентификатор узла, в каждый элемент, отправляемый из приложения.</span><span class="sxs-lookup"><span data-stu-id="41cb9-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="41cb9-140">Просмотр телеметрии</span><span class="sxs-lookup"><span data-stu-id="41cb9-140">View your telemetry</span></span>
<span data-ttu-id="41cb9-141">Вернитесь к ресурсу Application Insights на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="41cb9-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="41cb9-142">Щелкните плитку Docker.</span><span class="sxs-lookup"><span data-stu-id="41cb9-142">Click through the Docker tile.</span></span>

<span data-ttu-id="41cb9-143">Вскоре вы увидите данные, поступающие из приложения Docker, особенно при наличии других контейнеров, работающих в модуле Docker.</span><span class="sxs-lookup"><span data-stu-id="41cb9-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="41cb9-144">Ниже приведены примеры представлений данных.</span><span class="sxs-lookup"><span data-stu-id="41cb9-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="41cb9-145">Счетчики производительности узла, активность образа</span><span class="sxs-lookup"><span data-stu-id="41cb9-145">Perf counters by host, activity by image</span></span>
![пример](./media/app-insights-docker/10.png)

![пример](./media/app-insights-docker/11.png)

<span data-ttu-id="41cb9-148">Щелкните имя любого узла или образа, чтобы получить подробные данные.</span><span class="sxs-lookup"><span data-stu-id="41cb9-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="41cb9-149">Чтобы настроить представление, щелкните любую диаграмму, заголовок сетки или нажмите кнопку «Добавить диаграмму».</span><span class="sxs-lookup"><span data-stu-id="41cb9-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="41cb9-150">[Ознакомьтесь с дополнительными сведениями об обозревателе метрик](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="41cb9-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="41cb9-151">События контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="41cb9-151">Docker container events</span></span>
![пример](./media/app-insights-docker/13.png)

<span data-ttu-id="41cb9-153">Для анализа отдельных событий щелкните [Поиск](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="41cb9-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="41cb9-154">Найдите и отфильтруйте нужные вам события.</span><span class="sxs-lookup"><span data-stu-id="41cb9-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="41cb9-155">Щелкните любое событие, чтобы просмотреть подробные данные.</span><span class="sxs-lookup"><span data-stu-id="41cb9-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="41cb9-156">Исключения по имени контейнера</span><span class="sxs-lookup"><span data-stu-id="41cb9-156">Exceptions by container name</span></span>
![пример](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="41cb9-158">Добавление контекста Docker в телеметрию приложения</span><span class="sxs-lookup"><span data-stu-id="41cb9-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="41cb9-159">Запрос данных телеметрии, отправленный из приложения, инструментированного с помощью пакета SDK AI, с дополнительным контекстом Docker:</span><span class="sxs-lookup"><span data-stu-id="41cb9-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![пример](./media/app-insights-docker/16.png)

<span data-ttu-id="41cb9-161">Счетчики производительности для загруженности процессора и доступной памяти, насыщенные, дополненные и сгруппированные по имени контейнера Docker:</span><span class="sxs-lookup"><span data-stu-id="41cb9-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![пример](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="41cb9-163">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="41cb9-163">Q & A</span></span>
<span data-ttu-id="41cb9-164">*Какие возможности Application Insights отсутствуют в Docker?*</span><span class="sxs-lookup"><span data-stu-id="41cb9-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="41cb9-165">Подробные показатели счетчиков производительности по контейнерам и образам.</span><span class="sxs-lookup"><span data-stu-id="41cb9-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="41cb9-166">Интегрированные данные контейнера и приложения на одной панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="41cb9-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="41cb9-167">[Экспорт данных телеметрии](app-insights-export-telemetry.md) в базу данных, Power BI или другую панель мониторинга для дальнейшего анализа.</span><span class="sxs-lookup"><span data-stu-id="41cb9-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="41cb9-168">*Как получить данные телеметрии из самого приложения?*</span><span class="sxs-lookup"><span data-stu-id="41cb9-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="41cb9-169">Установите пакет SDK Application Insights в приложении.</span><span class="sxs-lookup"><span data-stu-id="41cb9-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="41cb9-170">Узнайте, как это сделать в [веб-приложениях Java](app-insights-java-get-started.md) и [Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="41cb9-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="41cb9-171">Видео</span><span class="sxs-lookup"><span data-stu-id="41cb9-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="41cb9-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41cb9-172">Next steps</span></span>

* [<span data-ttu-id="41cb9-173">Application Insights для Java</span><span class="sxs-lookup"><span data-stu-id="41cb9-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="41cb9-174">Application Insights для Node.js</span><span class="sxs-lookup"><span data-stu-id="41cb9-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="41cb9-175">Application Insights для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="41cb9-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
