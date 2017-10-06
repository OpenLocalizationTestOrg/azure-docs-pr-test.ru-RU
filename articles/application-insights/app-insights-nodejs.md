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
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Мониторинг служб и приложений Node.js с помощью Application Insights

[Azure Application Insights](app-insights-overview.md) отслеживает серверных служб и компонентов после их развертывания toohelp вы [обнаруживать и быстрой диагностики проблем производительности и других проблем](app-insights-detect-triage-diagnose.md). Используйте этот компонент для служб Node.js независимо от их расположения: в центре обработки данных, виртуальных машинах Azure и веб-приложениях, даже в сторонних общедоступных облачных средах.

tooreceive, хранения и просмотра данных наблюдения, выполните следующие инструкции tooinclude агент в коде hello и настроить соответствующий ресурс Application Insights в Azure. Hello агент отправляет ресурса toothat данных для последующего анализа и исследования.

Hello Node.js агента можно автоматически отслеживать входящие и исходящие запросы HTTP, несколько метрик системы и исключения. Начиная с версии v0.20, он также может отслеживать некоторые распространенные пакеты сторонних поставщиков, например `mongodb`, `mysql` и `redis`. Все события, связанные с tooan Входящий HTTP-запрос связаны друг с другом для более быстрого устранения неполадок.

Можно отслеживать несколько аспектов приложения и системы путем инструментирования их вручную с помощью API агента hello, описанным ниже.

![Пример диаграмм мониторинга производительности](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Приступая к работе

Давайте перейдем к настройке мониторинга приложения или службы.

### <a name="resource"></a> Настройка ресурса App Insights

**Чтобы начать**, у вас должна быть подписка Azure. Вы можете [создать ее бесплатно][azure-free-offer]. Если в вашей организации уже есть подписка Azure, администратор может выполнить [эти инструкции] [ add-aad-user] tooadd tooit вы.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

Теперь войдите toohello [портал Azure] [ portal] и создать ресурс Application Insights, как показано в следующих hello - нажмите кнопку «Создать» > «Средства разработчика» > «Application Insights». ресурс Hello содержит конечную точку для приема данных телеметрии, хранилище для этих данных, сохраненные отчеты и панели мониторинга, правила и конфигурации оповещений и многое другое.

![Создание ресурса App Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

На странице создания ресурса hello выберите «Приложение Node.js» из раскрывающегося списка hello типа приложения. Тип приложения Hello определяет набор по умолчанию hello панели мониторинга и отчеты, созданные для вас. В любом случае беспокоиться не стоит, любой ресурс App Insights способен собирать данные независимо от используемого языка и платформы.

![Форма создания ресурса App Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Настройка агента Node.js hello

Теперь настало время tooinclude hello агента в приложении, сбора данных.
Запуск путем копирования ключ инструментирования вашей ресурсов (здесь и далее tooas вашей `ikey`) из портала hello, как показано ниже. Подробные сведения о приложении, система использует tooyour данных этого ключа toomap ресурсов Azure, поэтому требуется toospecify Hello их в переменной среды или toouse агента hello в коде.  

![Копирование ключа инструментирования](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

Добавьте зависимости hello Node.js агент библиотеки tooyour приложения через package.json. Hello корневой папке приложения выполните следующую команду:

```bash
npm install applicationinsights --save
```

Теперь вам требуется tooexplicitly загрузки библиотеки hello в коде. Так как агент hello вставляет инструментирование в других библиотеках, необходимо загрузить его как можно даже перед другими раньше `require` инструкции. tooget работу, вверху hello первый файл .js добавить:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Hello `setup` метод настраивает ключ инструментирования hello (и тем самым ресурсов Azure) toobe, используемый по умолчанию для всех отслеживаемых элементов. Вызовите `start` после настройки toobegin по завершении сбора и отправки данных телеметрии.

Можно также предоставить через переменную среды hello APPINSIGHTS ikey\_INSTRUMENTATIONKEY, а не передается вручную слишком `setup()` или `getClient()`. Такой подход позволяет обеспечивать ikeys из зафиксированных исходного кода и различных ikeys toospecify для различных сред.

Дополнительные параметры настройки описаны ниже.

Можно попробовать агента hello без отправки данных телеметрии, задав hello инструментария ключа tooany непустой строкой.

### <a name="monitor"></a> Отслеживание работы приложения

агент Hello автоматически собирает данные телеметрии, сведения о среде выполнения Node.js hello и некоторые общие модули сторонних разработчиков. Использование вашего приложения теперь toogenerate некоторые из этих данных.

Затем в hello [портал Azure] [ portal] Обзор toohello ресурс Application Insights, созданный ранее и выполните поиск первого несколько точек данных на шкале Обзор hello, как и после изображения hello. Пролистайте hello диаграммы для получения дополнительных сведений.

![Первые точки данных](./media/app-insights-nodejs/12-first-perf.png)

Щелкните ссылку hello приложения карты кнопка tooview hello топологии, обнаруженных для приложения, как и после изображения hello. Просмотрите компоненты в схеме hello для получения дополнительных сведений.

![Простая схема сопоставления приложений](./media/app-insights-nodejs/06-appinsights_appmap.png)

Дополнительные сведения о приложении и устранения проблем с помощью hello другие представления, доступные в разделе «Сведения» hello.

![Раздел изучения](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>Данные отсутствуют?

Поскольку агент hello пакетов данных для отправки перед отображением элементов на портале hello могут возникать задержки. Если вы не видите данные в ресурс повторите некоторые hello следующие исправления:

* Использование приложения hello Дополнительно; выполнить дополнительные действия toogenerate дополнительные телеметрии.
* Нажмите кнопку **обновление** в представлении портала ресурсов hello. Диаграммы автоматически сами периодически обновлять, но обновление заставляет этот toohappen немедленно.
* [Необходимые порты для исходящего трафика](app-insights-ip-addresses.md) должны быть открыты.
* Откройте hello [поиска](app-insights-diagnostic-search.md) плитку и искать отдельные события.
* Проверьте hello [часто задаваемые вопросы о][].


## <a name="agent-configuration"></a>Конфигурация агента

Ниже приведены способы настройки hello агента и их значения по умолчанию.

toofully согласовывать события в службе, быть убедиться, что tooset `.setAutoDependencyCorrelation(true)`. Это позволит агенту hello tootrack контекст другого асинхронного обратного вызова в Node.js.

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

## <a name="agent-api"></a>API агента

<!-- TODO: Fully document agent API. -->

Hello API агента .NET полностью описаны [здесь](app-insights-api-custom-events-metrics.md).

Вы можете отслеживать запроса, события, метрики или исключения с помощью клиентского приложения Node.js аналитики hello. Hello следующий пример демонстрирует некоторые hello доступные интерфейсы API.

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

### <a name="track-your-dependencies"></a>Отслеживание зависимостей

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

### <a name="add-a-custom-property-tooall-events"></a>Добавить пользовательское свойство tooall события

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>Отслеживание HTTP-запросов GET

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Отслеживание времени запуска сервера

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Дополнительные ресурсы

* [Мониторинг телеметрии hello портала](app-insights-dashboards.md)
* [Знакомство с аналитикой в Application Insights](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[часто задаваемые вопросы о]: app-insights-troubleshoot-faq.md
