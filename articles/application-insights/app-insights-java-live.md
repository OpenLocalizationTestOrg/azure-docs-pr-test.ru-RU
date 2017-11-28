---
title: "aaaApplication Insights для Java веб-приложений, которые уже находятся в режиме реального времени"
description: "Начните отслеживать веб-приложение, которое уже выполняется на вашем сервере."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="22fa7-103">Application Insights для уже действующих веб-приложений Java</span><span class="sxs-lookup"><span data-stu-id="22fa7-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="22fa7-104">Если у вас есть веб-приложения, которая запущена на сервере J2EE, можно приступать к мониторингу его с [Application Insights](app-insights-overview.md) без hello toomake изменениями кода или повторную компиляцию проекта.</span><span class="sxs-lookup"><span data-stu-id="22fa7-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="22fa7-105">Этот параметр получение сведений о запросы HTTP, отправленные tooyour сервера, необработанные исключения и счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="22fa7-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="22fa7-106">Вам потребуется подписка слишком[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="22fa7-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="22fa7-107">процедура Hello на этой странице добавляет hello SDK tooyour веб-приложения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="22fa7-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="22fa7-108">Этот инструментарий среды выполнения полезно в том случае, если вы не желаете tooupdate или перестроить исходный код.</span><span class="sxs-lookup"><span data-stu-id="22fa7-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="22fa7-109">Но если это возможно, мы рекомендуем вам [Добавление hello SDK toohello исходного кода](app-insights-java-get-started.md) вместо него.</span><span class="sxs-lookup"><span data-stu-id="22fa7-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="22fa7-110">Который предоставляет дополнительные параметры, такие как записи действий пользователей tootrack кода.</span><span class="sxs-lookup"><span data-stu-id="22fa7-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="22fa7-111">1. Получение ключа инструментирования Application Insights</span><span class="sxs-lookup"><span data-stu-id="22fa7-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="22fa7-112">Войдите в toohello [портал Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="22fa7-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="22fa7-113">Создайте новый ресурс Application Insights и задайте hello приложения типа tooJava веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="22fa7-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![Введите имя, выберите веб-приложение Java и нажмите кнопку "Создать"](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="22fa7-115">Hello ресурс создается через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="22fa7-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="22fa7-116">Откройте новый ресурс hello и получите свой ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="22fa7-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="22fa7-117">Вам потребуется toopaste этот ключ в проект кода чуть ниже.</span><span class="sxs-lookup"><span data-stu-id="22fa7-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![Обзор нового ресурса hello нажмите кнопку Свойства и скопируйте hello ключ инструментирования](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="22fa7-119">2. Загрузите пакет SDK для hello</span><span class="sxs-lookup"><span data-stu-id="22fa7-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="22fa7-120">Загрузите hello [пакет SDK Application Insights для Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="22fa7-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="22fa7-121">На сервере Извлеките hello содержимое SDK toohello каталог, из которого загружаются двоичных файлов проекта.</span><span class="sxs-lookup"><span data-stu-id="22fa7-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="22fa7-122">В случае с Tomcat обычно это каталог `webapps/<your_app_name>/WEB-INF/lib`.</span><span class="sxs-lookup"><span data-stu-id="22fa7-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="22fa7-123">Обратите внимание, что toorepeat это на каждом экземпляре сервера и для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="22fa7-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="22fa7-124">3. Добавление XML-файла Application Insights</span><span class="sxs-lookup"><span data-stu-id="22fa7-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="22fa7-125">Создание ApplicationInsights.xml в папке hello, в которую добавляется hello SDK.</span><span class="sxs-lookup"><span data-stu-id="22fa7-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="22fa7-126">В ней хранятся hello следующий XML.</span><span class="sxs-lookup"><span data-stu-id="22fa7-126">Put into it hello following XML.</span></span>

<span data-ttu-id="22fa7-127">Заменить ключ инструментирования hello, полученного от hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="22fa7-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="22fa7-128">ключ инструментирования Hello отправляется вместе с каждого элемента телеметрии и сообщает toodisplay Application Insights в ресурс.</span><span class="sxs-lookup"><span data-stu-id="22fa7-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="22fa7-129">Hello HTTP-запроса компонент является необязательным.</span><span class="sxs-lookup"><span data-stu-id="22fa7-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="22fa7-130">Он автоматически отправляет телеметрии о запросах и портал toohello времени ответа.</span><span class="sxs-lookup"><span data-stu-id="22fa7-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="22fa7-131">Корреляция событий является компонентом запроса HTTP toohello сложения.</span><span class="sxs-lookup"><span data-stu-id="22fa7-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="22fa7-132">Он назначает tooeach идентификатор запроса, полученных сервером hello и добавляет этот идентификатор как элемент свойства tooevery телеметрии как свойство hello «Operation.Id».</span><span class="sxs-lookup"><span data-stu-id="22fa7-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="22fa7-133">Позволяет toocorrelate hello телеметрии, связанные с каждым запросом, можно установить фильтр в [диагностики поиска](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="22fa7-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="22fa7-134">4. Добавление фильтра HTTP</span><span class="sxs-lookup"><span data-stu-id="22fa7-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="22fa7-135">Найдите и откройте файл web.xml hello в проекте, а следующий фрагмент кода hello узел веб-приложения и где настраиваются фильтры приложения hello слияния.</span><span class="sxs-lookup"><span data-stu-id="22fa7-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="22fa7-136">Прежде чем все остальные фильтры должны сопоставляться tooget hello наиболее точные результаты, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="22fa7-137">5. Проверка исключений брандмауэра</span><span class="sxs-lookup"><span data-stu-id="22fa7-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="22fa7-138">Может потребоваться слишком[задавать исключения выходных данных toosend](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="22fa7-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="22fa7-139">6. Перезапуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="22fa7-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="22fa7-140">7. Просмотр данных телеметрии в Application Insights</span><span class="sxs-lookup"><span data-stu-id="22fa7-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="22fa7-141">Вернуть ресурс Application Insights tooyour в [портал Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22fa7-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="22fa7-142">Данные телеметрии об HTTP-запросов отображается на колонки Обзор hello.</span><span class="sxs-lookup"><span data-stu-id="22fa7-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="22fa7-143">(Если данные отсутствуют, подождите несколько секунд и нажмите кнопку обновления).</span><span class="sxs-lookup"><span data-stu-id="22fa7-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![пример данных](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="22fa7-145">Нажмите кнопку через любой toosee диаграммы более подробные показатели.</span><span class="sxs-lookup"><span data-stu-id="22fa7-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="22fa7-146">И при просмотре свойств hello запроса, можно просмотреть события телеметрии hello, связанные с ним, такие как запросы и исключения.</span><span class="sxs-lookup"><span data-stu-id="22fa7-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="22fa7-147">Дополнительные сведения о метриках.</span><span class="sxs-lookup"><span data-stu-id="22fa7-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="22fa7-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22fa7-148">Next steps</span></span>
* <span data-ttu-id="22fa7-149">[Добавить веб-страницы телеметрии tooyour](app-insights-javascript.md) toomonitor страницы представлений и метрики пользователь.</span><span class="sxs-lookup"><span data-stu-id="22fa7-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="22fa7-150">[Настройка веб-тестов](app-insights-monitor-web-app-availability.md) toomake убедиться, что приложение остается динамической и отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="22fa7-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="22fa7-151">Журнал трассировки</span><span class="sxs-lookup"><span data-stu-id="22fa7-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="22fa7-152">[Поиск событий и журналов](app-insights-diagnostic-search.md) toohelp диагностики проблем.</span><span class="sxs-lookup"><span data-stu-id="22fa7-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

