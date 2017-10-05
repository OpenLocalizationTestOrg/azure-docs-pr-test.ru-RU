---
title: "Мониторинг служб Node.js с помощью Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: ee65207e546c7050cc7bf35c36624fc49ad9eec4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="5ac22-103">Мониторинг служб и приложений Node.js с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="5ac22-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="5ac22-104">[Azure Application Insights](app-insights-overview.md) отслеживает развернутые службы и компоненты серверной части для [обнаружения и быстрой диагностики проблем производительности, а также других проблем](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="5ac22-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them to help you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="5ac22-105">Используйте этот компонент для служб Node.js независимо от их расположения: в центре обработки данных, виртуальных машинах Azure и веб-приложениях, даже в сторонних общедоступных облачных средах.</span><span class="sxs-lookup"><span data-stu-id="5ac22-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="5ac22-106">Для получения, хранения и анализа данных мониторинга выполните приведенные ниже инструкции, чтобы включить агент в код, а также настроить соответствующий ресурс Application Insights в Azure.</span><span class="sxs-lookup"><span data-stu-id="5ac22-106">To receive, store, and explore your monitoring data, follow the following instructions to include an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="5ac22-107">Агент отправляет данные в этот ресурс для дальнейшего анализа и исследования.</span><span class="sxs-lookup"><span data-stu-id="5ac22-107">The agent sends data to that resource for further analysis and exploration.</span></span>

<span data-ttu-id="5ac22-108">Агент Node.js может автоматически отслеживать входящие и исходящие HTTP-запросы, несколько системных метрик и исключения.</span><span class="sxs-lookup"><span data-stu-id="5ac22-108">The Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="5ac22-109">Начиная с версии v0.20, он также может отслеживать некоторые распространенные пакеты сторонних поставщиков, например `mongodb`, `mysql` и `redis`.</span><span class="sxs-lookup"><span data-stu-id="5ac22-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="5ac22-110">Все события, связанные с входящим HTTP-запросом, коррелируют для быстрого устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="5ac22-110">All events related to an incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="5ac22-111">Вы можете отслеживать несколько аспектов приложения и системы, инструментируя их вручную с помощью агента API, с которым вы ознакомитесь далее.</span><span class="sxs-lookup"><span data-stu-id="5ac22-111">You can monitor more aspects of your app and system by manually instrumenting them using the agent API described later.</span></span>

![Пример диаграмм мониторинга производительности](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="5ac22-113">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="5ac22-113">Getting Started</span></span>

<span data-ttu-id="5ac22-114">Давайте перейдем к настройке мониторинга приложения или службы.</span><span class="sxs-lookup"><span data-stu-id="5ac22-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="5ac22-115"><a name="resource"></a> Настройка ресурса App Insights</span><span class="sxs-lookup"><span data-stu-id="5ac22-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="5ac22-116">**Чтобы начать**, у вас должна быть подписка Azure. Вы можете [создать ее бесплатно][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="5ac22-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="5ac22-117">Если у вашей организации уже есть подписка Azure, администратору необходимо выполнить [эти инструкции][add-aad-user], чтобы добавить вас в эту подписку.</span><span class="sxs-lookup"><span data-stu-id="5ac22-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] to add you to it.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="5ac22-118">Теперь войдите [на портал Azure][portal] и создайте ресурс Application Insights, как показано далее. Щелкните "Создать" > "Средства разработчика" > "Application Insights".</span><span class="sxs-lookup"><span data-stu-id="5ac22-118">Now log in to the [Azure portal][portal] and create an Application Insights resource as illustrated in the following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="5ac22-119">Ресурс содержит конечную точку для приема данных телеметрии, хранилище для этих данных, сохраненные отчеты и панели мониторинга, настройки правил и оповещений и т. д.</span><span class="sxs-lookup"><span data-stu-id="5ac22-119">The resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Создание ресурса App Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="5ac22-121">На странице создания ресурса выберите "Приложение Node.js" из раскрывающегося списка типов приложения.</span><span class="sxs-lookup"><span data-stu-id="5ac22-121">On the resource creation page, choose "Node.js Application" from the application type drop-down.</span></span> <span data-ttu-id="5ac22-122">От типа приложения зависит набор панелей мониторинга и отчетов по умолчанию, которые вы получите.</span><span class="sxs-lookup"><span data-stu-id="5ac22-122">The app type determines the default set of dashboards and reports created for you.</span></span> <span data-ttu-id="5ac22-123">В любом случае беспокоиться не стоит, любой ресурс App Insights способен собирать данные независимо от используемого языка и платформы.</span><span class="sxs-lookup"><span data-stu-id="5ac22-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Форма создания ресурса App Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="5ac22-125"><a name="agent"></a> Настройка агента Node.js</span><span class="sxs-lookup"><span data-stu-id="5ac22-125"><a name="agent"></a> Set up the Node.js agent</span></span>

<span data-ttu-id="5ac22-126">Теперь пришло время включить агент в приложение, чтобы он мог собирать данные.</span><span class="sxs-lookup"><span data-stu-id="5ac22-126">Now it's time to include the agent in your app so it can gather data.</span></span>
<span data-ttu-id="5ac22-127">Для начала скопируйте ключ инструментирования ресурса (далее — `ikey`) на портале, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5ac22-127">Start by copying your resource's Instrumentation Key (hereinafter referred to as your `ikey`) from the portal as shown below.</span></span> <span data-ttu-id="5ac22-128">Система App Insights будет использовать этот ключ, чтобы сопоставить данные с ресурсом Azure, поэтому вам необходимо указать его в переменной среды или коде, который будет использовать агент.</span><span class="sxs-lookup"><span data-stu-id="5ac22-128">The App Insights system uses this key to map data to your Azure resource so you need to specify it in an environment variable or your code for the agent to use.</span></span>  

![Копирование ключа инструментирования](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="5ac22-130">Затем добавьте библиотеку агента Node.js в зависимости приложения с помощью файла package.json.</span><span class="sxs-lookup"><span data-stu-id="5ac22-130">Next, add the Node.js agent library to your app's dependencies via package.json.</span></span> <span data-ttu-id="5ac22-131">Из корневой папки приложения выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5ac22-131">From the root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="5ac22-132">Теперь вам необходимо явным образом загрузить библиотеку в код.</span><span class="sxs-lookup"><span data-stu-id="5ac22-132">Now you need to explicitly load the library in your code.</span></span> <span data-ttu-id="5ac22-133">Так как агент внедряет инструментирование во многие другие библиотеки, вам необходимо загрузить ее как можно раньше, даже до выполнения других инструкций `require`.</span><span class="sxs-lookup"><span data-stu-id="5ac22-133">Because the agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="5ac22-134">Чтобы приступить, добавьте в верхнюю часть первого JS-файла следующее:</span><span class="sxs-lookup"><span data-stu-id="5ac22-134">To get started, at the top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="5ac22-135">Метод `setup` настраивает ключ инструментирования (а значит и ресурс Azure), который будет использоваться по умолчанию для всех отслеживаемых элементов.</span><span class="sxs-lookup"><span data-stu-id="5ac22-135">The `setup` method configures the instrumentation key (and thus Azure resource) to be used by default for all tracked items.</span></span> <span data-ttu-id="5ac22-136">После завершения настройки вызовите `start`, чтобы начать сбор данных телеметрии и их отправку.</span><span class="sxs-lookup"><span data-stu-id="5ac22-136">Call `start` after configuration is finished to begin gathering and sending telemetry data.</span></span>

<span data-ttu-id="5ac22-137">Вы также можете предоставить ключ ikey через переменную среды APPINSIGHTS\_INSTRUMENTATIONKEY, вместо того чтобы передавать его вручную в `setup()` или `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="5ac22-137">You can also provide an ikey via the environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually to  `setup()` or `getClient()`.</span></span> <span data-ttu-id="5ac22-138">Это позволит хранить ключи ikey вне выделенного исходного кода и указать различные ключи ikey для разных сред.</span><span class="sxs-lookup"><span data-stu-id="5ac22-138">This practice lets you keep ikeys out of committed source code and to specify different ikeys for different environments.</span></span>

<span data-ttu-id="5ac22-139">Дополнительные параметры настройки описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="5ac22-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="5ac22-140">Вы можете использовать агент, не отправляя данные телеметрии. Для этого настройте ключ инструментирования в качестве любой заполненной строки.</span><span class="sxs-lookup"><span data-stu-id="5ac22-140">You can try the agent without sending telemetry by setting the instrumentation key to any non-empty string.</span></span>

### <span data-ttu-id="5ac22-141"><a name="monitor"></a> Отслеживание работы приложения</span><span class="sxs-lookup"><span data-stu-id="5ac22-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="5ac22-142">Агент автоматически собирает данные телеметрии среды выполнения Node.js и некоторых распространенных модулей сторонних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="5ac22-142">The agent automatically gathers telemetry about the Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="5ac22-143">Используйте приложение для создания этих данных.</span><span class="sxs-lookup"><span data-stu-id="5ac22-143">Use your application now to generate some of this data.</span></span>

<span data-ttu-id="5ac22-144">Затем на [портале Azure][portal] перейдите к созданному ранее ресурсу Application Insights и найдите минимальное количество точек данных на временной шкале обзора, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="5ac22-144">Then, in the [Azure portal][portal] browse to the Application Insights resource you created earlier and look for your first few data points in the Overview timeline, as in the following image.</span></span> <span data-ttu-id="5ac22-145">Чтобы получить дополнительные сведения, щелкните диаграммы.</span><span class="sxs-lookup"><span data-stu-id="5ac22-145">Click through the charts for more details.</span></span>

![Первые точки данных](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="5ac22-147">Нажмите кнопку схемы сопоставления приложений, чтобы просмотреть топологию, обнаруженную для приложения, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="5ac22-147">Click the Application map button to view the topology discovered for your app, as in the following image.</span></span> <span data-ttu-id="5ac22-148">Чтобы получить дополнительные сведения, щелкайте компоненты на карте.</span><span class="sxs-lookup"><span data-stu-id="5ac22-148">Click through components in the map for more details.</span></span>

![Простая схема сопоставления приложений](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="5ac22-150">Чтобы узнать больше о приложении и методах устранения неполадок, используйте другие представления, доступные в разделе изучения.</span><span class="sxs-lookup"><span data-stu-id="5ac22-150">Learn more about your app and troubleshoot problems using the other views available under the "Investigate" section.</span></span>

![Раздел изучения](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="5ac22-152">Данные отсутствуют?</span><span class="sxs-lookup"><span data-stu-id="5ac22-152">No data?</span></span>

<span data-ttu-id="5ac22-153">Так как агент упаковывает данные для передачи, возможна некоторая задержка отображения элементов на портале.</span><span class="sxs-lookup"><span data-stu-id="5ac22-153">Because the agent batches data for submission there may be a delay before items are displayed in the portal.</span></span> <span data-ttu-id="5ac22-154">Если данные в ресурсе не отображаются, попробуйте сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="5ac22-154">If you don't see data in your resource try some of the following fixes:</span></span>

* <span data-ttu-id="5ac22-155">Выполните больше действий в приложении, чтобы получить больше данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="5ac22-155">Use the application some more; take more actions to generate more telemetry.</span></span>
* <span data-ttu-id="5ac22-156">Нажмите кнопку **обновления** в представлении ресурса на портале.</span><span class="sxs-lookup"><span data-stu-id="5ac22-156">Click **Refresh** in the portal resource view.</span></span> <span data-ttu-id="5ac22-157">Диаграммы и так периодически автоматически обновляются, но если вы нажмете эту кнопку, обновление будет выполнено сразу же.</span><span class="sxs-lookup"><span data-stu-id="5ac22-157">Charts automatically refresh themselves periodically but refreshing forces this to happen immediately.</span></span>
* <span data-ttu-id="5ac22-158">[Необходимые порты для исходящего трафика](app-insights-ip-addresses.md) должны быть открыты.</span><span class="sxs-lookup"><span data-stu-id="5ac22-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="5ac22-159">Откройте плитку [поиска](app-insights-diagnostic-search.md), чтобы найти отдельные события.</span><span class="sxs-lookup"><span data-stu-id="5ac22-159">Open the [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="5ac22-160">Просмотрите [часто задаваемые вопросы][].</span><span class="sxs-lookup"><span data-stu-id="5ac22-160">Check the [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="5ac22-161">Конфигурация агента</span><span class="sxs-lookup"><span data-stu-id="5ac22-161">Agent Configuration</span></span>

<span data-ttu-id="5ac22-162">Ниже представлены методы настройки агента, а также их значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5ac22-162">Following are the agent's configuration methods and their default values.</span></span>

<span data-ttu-id="5ac22-163">Чтобы полностью сопоставить события в службе, задайте `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="5ac22-163">To fully correlate events in a service, be sure to set `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="5ac22-164">Благодаря этому агент будет отслеживать контекст в асинхронных обратных вызовах в службе Node.js.</span><span class="sxs-lookup"><span data-stu-id="5ac22-164">This allows the agent to track context across asynchronous callbacks in Node.js.</span></span>

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

## <a name="agent-api"></a><span data-ttu-id="5ac22-165">API агента</span><span class="sxs-lookup"><span data-stu-id="5ac22-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="5ac22-166">API агента для .NET полностью описан [здесь](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5ac22-166">The .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="5ac22-167">Вы можете отслеживать любой запрос, событие, метрику или исключение с помощью клиента Node.js для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5ac22-167">You can track any request, event, metric, or exception using the Application Insights Node.js client.</span></span> <span data-ttu-id="5ac22-168">В примере ниже приведены некоторые доступные интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="5ac22-168">The following example demonstrates some of the available APIs.</span></span>

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
  client.trackRequest(req, res); // Place at the beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="5ac22-169">Отслеживание зависимостей</span><span class="sxs-lookup"><span data-stu-id="5ac22-169">Track your dependencies</span></span>

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

### <a name="add-a-custom-property-to-all-events"></a><span data-ttu-id="5ac22-170">Добавление пользовательского свойства во все события</span><span class="sxs-lookup"><span data-stu-id="5ac22-170">Add a custom property to all events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="5ac22-171">Отслеживание HTTP-запросов GET</span><span class="sxs-lookup"><span data-stu-id="5ac22-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="5ac22-172">Отслеживание времени запуска сервера</span><span class="sxs-lookup"><span data-stu-id="5ac22-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="5ac22-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5ac22-173">More resources</span></span>

* [<span data-ttu-id="5ac22-174">Навигация и панели мониторинга на портале Application Insights</span><span class="sxs-lookup"><span data-stu-id="5ac22-174">Monitor your telemetry in the portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="5ac22-175">Знакомство с аналитикой в Application Insights</span><span class="sxs-lookup"><span data-stu-id="5ac22-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
<span data-ttu-id="5ac22-176">[часто задаваемые вопросы]: app-insights-troubleshoot-faq.md</span><span class="sxs-lookup"><span data-stu-id="5ac22-176">[FAQ]: app-insights-troubleshoot-faq.md</span></span>
