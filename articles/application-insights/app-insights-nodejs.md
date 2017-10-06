---
title: "aaaMonitor Node.js служб с помощью Azure Application Insights | Документы Microsoft"
description: "Используйте Application Insights для мониторинга производительности и диагностики проблем в службах Node.js."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="afbd7-103">Мониторинг служб и приложений Node.js с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="afbd7-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="afbd7-104">[Azure Application Insights](app-insights-overview.md) отслеживает серверных служб и компонентов после их развертывания toohelp вы [обнаруживать и быстрой диагностики проблем производительности и других проблем](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="afbd7-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="afbd7-105">Используйте этот компонент для служб Node.js независимо от их расположения: в центре обработки данных, виртуальных машинах Azure и веб-приложениях, даже в сторонних общедоступных облачных средах.</span><span class="sxs-lookup"><span data-stu-id="afbd7-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="afbd7-106">tooreceive, хранения и просмотра данных наблюдения, выполните следующие инструкции tooinclude агент в коде hello и настроить соответствующий ресурс Application Insights в Azure.</span><span class="sxs-lookup"><span data-stu-id="afbd7-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="afbd7-107">Hello агент отправляет ресурса toothat данных для последующего анализа и исследования.</span><span class="sxs-lookup"><span data-stu-id="afbd7-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="afbd7-108">Hello Node.js агента можно автоматически отслеживать входящие и исходящие запросы HTTP, несколько метрик системы и исключения.</span><span class="sxs-lookup"><span data-stu-id="afbd7-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="afbd7-109">Начиная с версии v0.20, он также может отслеживать некоторые распространенные пакеты сторонних поставщиков, например `mongodb`, `mysql` и `redis`.</span><span class="sxs-lookup"><span data-stu-id="afbd7-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="afbd7-110">Все события, связанные с tooan Входящий HTTP-запрос связаны друг с другом для более быстрого устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="afbd7-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="afbd7-111">Можно отслеживать несколько аспектов приложения и системы путем инструментирования их вручную с помощью API агента hello, описанным ниже.</span><span class="sxs-lookup"><span data-stu-id="afbd7-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Пример диаграмм мониторинга производительности](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="afbd7-113">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="afbd7-113">Getting Started</span></span>

<span data-ttu-id="afbd7-114">Давайте перейдем к настройке мониторинга приложения или службы.</span><span class="sxs-lookup"><span data-stu-id="afbd7-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="afbd7-115"><a name="resource"></a> Настройка ресурса App Insights</span><span class="sxs-lookup"><span data-stu-id="afbd7-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="afbd7-116">**Чтобы начать**, у вас должна быть подписка Azure. Вы можете [создать ее бесплатно][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="afbd7-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="afbd7-117">Если в вашей организации уже есть подписка Azure, администратор может выполнить [эти инструкции] [ add-aad-user] tooadd tooit вы.</span><span class="sxs-lookup"><span data-stu-id="afbd7-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="afbd7-118">Теперь войдите toohello [портал Azure] [ portal] и создать ресурс Application Insights, как показано в следующих hello - нажмите кнопку «Создать» > «Средства разработчика» > «Application Insights».</span><span class="sxs-lookup"><span data-stu-id="afbd7-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="afbd7-119">ресурс Hello содержит конечную точку для приема данных телеметрии, хранилище для этих данных, сохраненные отчеты и панели мониторинга, правила и конфигурации оповещений и многое другое.</span><span class="sxs-lookup"><span data-stu-id="afbd7-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Создание ресурса App Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="afbd7-121">На странице создания ресурса hello выберите «Приложение Node.js» из раскрывающегося списка hello типа приложения.</span><span class="sxs-lookup"><span data-stu-id="afbd7-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="afbd7-122">Тип приложения Hello определяет набор по умолчанию hello панели мониторинга и отчеты, созданные для вас.</span><span class="sxs-lookup"><span data-stu-id="afbd7-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="afbd7-123">В любом случае беспокоиться не стоит, любой ресурс App Insights способен собирать данные независимо от используемого языка и платформы.</span><span class="sxs-lookup"><span data-stu-id="afbd7-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Форма создания ресурса App Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="afbd7-125"><a name="agent"></a>Настройка агента Node.js hello</span><span class="sxs-lookup"><span data-stu-id="afbd7-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="afbd7-126">Теперь настало время tooinclude hello агента в приложении, сбора данных.</span><span class="sxs-lookup"><span data-stu-id="afbd7-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="afbd7-127">Запуск путем копирования ключ инструментирования вашей ресурсов (здесь и далее tooas вашей `ikey`) из портала hello, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="afbd7-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="afbd7-128">Подробные сведения о приложении, система использует tooyour данных этого ключа toomap ресурсов Azure, поэтому требуется toospecify Hello их в переменной среды или toouse агента hello в коде.</span><span class="sxs-lookup"><span data-stu-id="afbd7-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![Копирование ключа инструментирования](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="afbd7-130">Добавьте зависимости hello Node.js агент библиотеки tooyour приложения через package.json.</span><span class="sxs-lookup"><span data-stu-id="afbd7-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="afbd7-131">Hello корневой папке приложения выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="afbd7-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="afbd7-132">Теперь вам требуется tooexplicitly загрузки библиотеки hello в коде.</span><span class="sxs-lookup"><span data-stu-id="afbd7-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="afbd7-133">Так как агент hello вставляет инструментирование в других библиотеках, необходимо загрузить его как можно даже перед другими раньше `require` инструкции.</span><span class="sxs-lookup"><span data-stu-id="afbd7-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="afbd7-134">tooget работу, вверху hello первый файл .js добавить:</span><span class="sxs-lookup"><span data-stu-id="afbd7-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="afbd7-135">Hello `setup` метод настраивает ключ инструментирования hello (и тем самым ресурсов Azure) toobe, используемый по умолчанию для всех отслеживаемых элементов.</span><span class="sxs-lookup"><span data-stu-id="afbd7-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="afbd7-136">Вызовите `start` после настройки toobegin по завершении сбора и отправки данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="afbd7-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="afbd7-137">Можно также предоставить через переменную среды hello APPINSIGHTS ikey\_INSTRUMENTATIONKEY, а не передается вручную слишком `setup()` или `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="afbd7-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="afbd7-138">Такой подход позволяет обеспечивать ikeys из зафиксированных исходного кода и различных ikeys toospecify для различных сред.</span><span class="sxs-lookup"><span data-stu-id="afbd7-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="afbd7-139">Дополнительные параметры настройки описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="afbd7-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="afbd7-140">Можно попробовать агента hello без отправки данных телеметрии, задав hello инструментария ключа tooany непустой строкой.</span><span class="sxs-lookup"><span data-stu-id="afbd7-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="afbd7-141"><a name="monitor"></a> Отслеживание работы приложения</span><span class="sxs-lookup"><span data-stu-id="afbd7-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="afbd7-142">агент Hello автоматически собирает данные телеметрии, сведения о среде выполнения Node.js hello и некоторые общие модули сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="afbd7-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="afbd7-143">Использование вашего приложения теперь toogenerate некоторые из этих данных.</span><span class="sxs-lookup"><span data-stu-id="afbd7-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="afbd7-144">Затем в hello [портал Azure] [ portal] Обзор toohello ресурс Application Insights, созданный ранее и выполните поиск первого несколько точек данных на шкале Обзор hello, как и после изображения hello.</span><span class="sxs-lookup"><span data-stu-id="afbd7-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="afbd7-145">Пролистайте hello диаграммы для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="afbd7-145">Click through hello charts for more details.</span></span>

![Первые точки данных](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="afbd7-147">Щелкните ссылку hello приложения карты кнопка tooview hello топологии, обнаруженных для приложения, как и после изображения hello.</span><span class="sxs-lookup"><span data-stu-id="afbd7-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="afbd7-148">Просмотрите компоненты в схеме hello для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="afbd7-148">Click through components in hello map for more details.</span></span>

![Простая схема сопоставления приложений](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="afbd7-150">Дополнительные сведения о приложении и устранения проблем с помощью hello другие представления, доступные в разделе «Сведения» hello.</span><span class="sxs-lookup"><span data-stu-id="afbd7-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Раздел изучения](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="afbd7-152">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="afbd7-152">No data?</span></span>

<span data-ttu-id="afbd7-153">Поскольку агент hello пакетов данных для отправки перед отображением элементов на портале hello могут возникать задержки.</span><span class="sxs-lookup"><span data-stu-id="afbd7-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="afbd7-154">Если вы не видите данные в ресурс повторите некоторые hello следующие исправления:</span><span class="sxs-lookup"><span data-stu-id="afbd7-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="afbd7-155">Использование приложения hello Дополнительно; выполнить дополнительные действия toogenerate дополнительные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="afbd7-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="afbd7-156">Нажмите кнопку **обновление** в представлении портала ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="afbd7-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="afbd7-157">Диаграммы автоматически сами периодически обновлять, но обновление заставляет этот toohappen немедленно.</span><span class="sxs-lookup"><span data-stu-id="afbd7-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="afbd7-158">[Необходимые порты для исходящего трафика](app-insights-ip-addresses.md) должны быть открыты.</span><span class="sxs-lookup"><span data-stu-id="afbd7-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="afbd7-159">Откройте hello [поиска](app-insights-diagnostic-search.md) плитку и искать отдельные события.</span><span class="sxs-lookup"><span data-stu-id="afbd7-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="afbd7-160">Проверьте hello [часто задаваемые вопросы о][].</span><span class="sxs-lookup"><span data-stu-id="afbd7-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="afbd7-161">Конфигурация агента</span><span class="sxs-lookup"><span data-stu-id="afbd7-161">Agent Configuration</span></span>

<span data-ttu-id="afbd7-162">Ниже приведены способы настройки hello агента и их значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="afbd7-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="afbd7-163">toofully согласовывать события в службе, быть убедиться, что tooset `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="afbd7-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="afbd7-164">Это позволит агенту hello tootrack контекст другого асинхронного обратного вызова в Node.js.</span><span class="sxs-lookup"><span data-stu-id="afbd7-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="afbd7-165">API агента</span><span class="sxs-lookup"><span data-stu-id="afbd7-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="afbd7-166">Hello API агента .NET полностью описаны [здесь](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="afbd7-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="afbd7-167">Вы можете отслеживать запроса, события, метрики или исключения с помощью клиентского приложения Node.js аналитики hello.</span><span class="sxs-lookup"><span data-stu-id="afbd7-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="afbd7-168">Hello следующий пример демонстрирует некоторые hello доступные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="afbd7-168">hello following example demonstrates some of hello available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="afbd7-169">Отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="afbd7-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="afbd7-170">Добавить пользовательское свойство tooall события</span><span class="sxs-lookup"><span data-stu-id="afbd7-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="afbd7-171">Отслеживание HTTP-запросов GET</span><span class="sxs-lookup"><span data-stu-id="afbd7-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="afbd7-172">Отслеживание времени запуска сервера</span><span class="sxs-lookup"><span data-stu-id="afbd7-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="afbd7-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="afbd7-173">More resources</span></span>

* [<span data-ttu-id="afbd7-174">Мониторинг телеметрии hello портала</span><span class="sxs-lookup"><span data-stu-id="afbd7-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="afbd7-175">Знакомство с аналитикой в Application Insights</span><span class="sxs-lookup"><span data-stu-id="afbd7-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[часто задаваемые вопросы о]: app-insights-troubleshoot-faq.md
