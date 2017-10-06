---
title: "aaaDependency отслеживания в Azure Application Insights | Документы Microsoft"
description: "Анализ использования, доступности и производительности локального приложения или веб-приложения Microsoft Azure с помощью Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Настройка Application Insights: отслеживание зависимостей
*Зависимость* – это внешний компонент, который вызывается приложением. Как правило, это служба, вызываемая с использованием HTTP, база данных или файловая система. [Application Insights](app-insights-overview.md) измеряет время, в течение которого приложение ожидает зависимости, и определяет, как часто происходит сбой вызова зависимости. Проверка конкретных вызовов и связывать их toorequests и исключения.

![примеры диаграмм](./media/app-insights-asp-net-dependencies/10-intro.png)

монитор зависимостей out of box Hello в настоящее время отображает типы toothese вызовы зависимостей:

* сервер;
  * базы данных SQL;
  * веб-службы и службы WCF ASP.NET, использующие привязки на основе HTTP;
  * локальные или удаленные HTTP-вызовы;
  * Azure Cosmos DB, таблица, хранилище BLOB-объектов и очередь.
* Веб-страницы
  * Вызовы AJAX

Мониторинг работает с помощью [инструментирования байт-кода](https://msdn.microsoft.com/library/z9z62c29.aspx) вокруг выбранных методов. Снижение производительности при этом сводится к минимуму.

Можно также написать собственную SDK вызывает toomonitor другие зависимости, как в коде клиента и сервера hello, с помощью hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

## <a name="set-up-dependency-monitoring"></a>Настройка мониторинга зависимостей
Сведения о частичных зависимостей собираются автоматически hello [пакет SDK Application Insights](app-insights-asp-net.md). tooget полные данные, установить соответствующий агент hello для сервера узла hello.

| Платформа | Установить |
| --- | --- |
| Сервер IIS |Либо [установите монитор состояния на сервере](app-insights-monitor-performance-live-website-now.md) или [обновление вашего приложения too.NET framework 4.6 или более поздней версии](http://go.microsoft.com/fwlink/?LinkId=528259) и установить hello [пакет SDK Application Insights](app-insights-asp-net.md) в вашем приложении. |
| Веб-приложение Azure |На панели управления приложения web [Привет открыть колонку Application Insights в панели управления web app](app-insights-azure-web-apps.md) и выберите "установить" при появлении соответствующего запроса. |
| Облачная служба Azure |[Используйте задачу при запуске](app-insights-cloudservices.md) или [установите платформу .NET Framework 4.6 или более поздней версии](../cloud-services/cloud-services-dotnet-install-dotnet.md). |

## <a name="where-toofind-dependency-data"></a>Где toofind зависимостей данных
* [Схема сопоставления приложений](#application-map) наглядно представляет зависимости между приложением и смежными компонентами.
* [Колонки "Производительность", "Браузер" и "Сбой"](#performance-and-blades) отображают данные зависимостей сервера.
* [Колонка "Браузеры"](#ajax-calls) содержит вызовы AJAX из браузеров ваших пользователей.
* [Пролистайте от медленно или неудачных запросов](#diagnose-slow-requests) toocheck вызывает их зависимостей.
* [Аналитика](#analytics) можно указывать данные, используемые tooquery зависимостей.

## <a name="application-map"></a>Схема сопоставления приложений
Схема сопоставления приложений выступает в качестве зависимости toodiscovering наглядные пособия между компонентами приложения hello. Оно создается автоматически на основе hello телеметрии из приложения. Этот пример вызовы AJAX с помощью обозревателя скриптов hello и вызовы REST с сервера hello приложения tootwo внешние службы.

![Схема сопоставления приложений](./media/app-insights-asp-net-dependencies/08.png)

* **Переход от поля hello** toorelevant зависимостей и других диаграмм.
* **ПИН-кода hello карты** toohello [мониторинга](app-insights-dashboards.md), где он будет полностью функционален.

[Подробнее](app-insights-app-map.md).

## <a name="performance-and-failure-blades"></a>Колонки "Производительность" и "Сбой"
Колонка Hello производительности показывает продолжительность hello вызовов зависимостей, приложение hello server. Она содержит сводную диаграмму и таблицу, разбитую по вызовам.

![Диаграммы зависимостей в колонке "Производительность"](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

Пролистайте hello сводных диаграмм или hello таблицы элементов toosearch необработанные вхождения этих вызовов.

![Экземпляры вызовов зависимостей](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**Количествами не пройденных** отображаются на hello **сбоев** колонку. Сбой является любой код возврата, не находится в диапазоне 200 hello-399, или unknown.

> [!NOTE]
> **100% failures?** (100 % сбоев?) — вероятно, означает, что вы получаете только неполные данные зависимостей. Требуется слишком[настроить соответствующие tooyour платформы наблюдения зависимостей](#set-up-dependency-monitoring).
>
>

## <a name="ajax-calls"></a>Вызовы AJAX
Hello браузеры колонке показывает продолжительность hello и частота сбоев AJAX вызывает из [JavaScript на веб-страницах](app-insights-javascript.md). Они отображаются как зависимости.

## <a name="diagnosis"></a> Диагностика медленных запросов
Каждое событие запрос связан с вызовы зависимостей hello, исключения и другие события, которые отслеживаются во время обработки приложения hello запроса. Поэтому если некоторые запросы выполняются плохо, можно выяснить, является ли из-за tooslow ответов от зависимости.

Давайте подробно рассмотрим подобный пример.

### <a name="tracing-from-requests-toodependencies"></a>Трассировка из toodependencies запросов
Откройте колонку производительности hello и посмотрите на сетку hello запросов:

![Список запросов со средними значениями и их количеством](./media/app-insights-asp-net-dependencies/02-reqs.png)

Основные Hello один занимает очень много времени. Давайте посмотрим, если мы можно выяснить расходуется время hello.

Щелкните отдельный запрос событий toosee строки:

![Список вхождений запросов](./media/app-insights-asp-net-dependencies/03-instances.png)

Щелкните любой экземпляр tooinspect долго выполняющихся его дальнейшее и прокрутите вниз запроса связанных toothis вызовы удаленных зависимостей toohello:

![Найти зависимости tooRemote вызовы, определите необычные длительность](./media/app-insights-asp-net-dependencies/04-dependencies.png)

Он будет выглядеть большинство hello время обслуживания, этот запрос, затраченное на вызов tooa локальной службы.

Выберите Дополнительные сведения, tooget строки:

![Пролистайте, причиной hello tooidentify удаленных зависимостей](./media/app-insights-asp-net-dependencies/05-detail.png)

Похоже, именно здесь находится hello проблему. Мы детальные hello проблемы, так что теперь мы просто нужно toofind, почему этот вызов занимает так много времени.

### <a name="request-timeline"></a>Временная шкала запроса
В другом случае вызов зависимости не имеет большую длительность. Но путем переключения toohello представлении временной шкалы, можно увидеть место возникновения задержки hello в нашей внутренней обработки:

![Найти зависимости tooRemote вызовы, определите необычные длительность](./media/app-insights-asp-net-dependencies/04-1.png)

Похоже, что toobe большой разрыв после первого вызова зависимостей hello, поэтому мы следует обратить внимание на наши toosee код причины, т. е.

### <a name="profile-your-live-site"></a>Выполните профилирование активного сайта

Не знаете, где временем hello? Hello [профилировщик Application Insights](app-insights-profiler.md) трассировки HTTP вызывает динамическую сайта tooyour и показано, какие функции в коде заняло hello наибольшее время.

## <a name="failed-requests"></a>Failed requests (Неудачные запросы)
Невыполненные запросы также могут быть связаны с toodependencies вызовов со сбоем. Опять же возможна детализация tootrack hello проблемы.

![Щелкните диаграмму hello неудачных запросов](./media/app-insights-asp-net-dependencies/06-fail.png)

Пролистайте tooan вхождения невыполненных запросов и просмотрите его связанные события.

![Выберите тип запроса, щелкните hello экземпляр tooget tooa другое представление Здравствуйте же экземпляр, нажмите кнопку tooget сведения об исключении.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Аналитика
Вы можете отслеживать зависимостей в hello [языка запросов анализа журналов](https://docs.loganalytics.io/). Ниже приведены некоторые примеры.

* Поиск неудачно завершенных вызовов зависимостей:

```

    dependencies | where success != "True" | take 10
```

* Поиск вызовов AJAX:

```

    dependencies | where client_Type == "Browser" | take 10
```

* Поиск вызовов зависимостей, связанных с запросами:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* Поиск вызовов AJAX, связанных с представлениями страницы:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>Пользовательское отслеживание зависимостей
стандартный модуль Отслеживание зависимостей Hello автоматически обнаруживает внешние зависимости, такие как базы данных и API-интерфейсов REST. Однако может потребоваться некоторые дополнительные компоненты toobe исчислялся hello таким же способом.

Можно написать код, который отправляет сведения о зависимостях, с помощью hello же [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) используются стандартные модули hello.

Например при создании кода со сборкой, не написанного пользователем, удалось времени всех tooit hello вызовов toofind out какие вклад делает ответ tooyour времени. Отправить эти данные отображаются в форме диаграммы зависимости hello Application Insights toohave его с помощью `TrackDependency`.

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

Tooswitch выключить модуля отслеживания стандартных зависимостей hello, удалить tooDependencyTrackingTelemetryModule ссылка hello в [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).

## <a name="troubleshooting"></a>Устранение неполадок
*Флаг успешной зависимости всегда показывает значение true или false.*

*SQL-запрос отображается не полностью.*

* Обновите toohello последнюю версию пакета SDK для hello. Если используемая версия .NET меньше 4.6:
  * Узла IIS: установите [агент аналитики приложений](app-insights-monitor-performance-live-website-now.md) на серверах узла hello.
  * Веб-приложение Azure: Откройте Application Insights в панели управления hello web app, а установите Application Insights.

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Дальнейшие действия
* [Исключения](app-insights-asp-net-exceptions.md)
* [Данные пользователей и страниц](app-insights-javascript.md)
* [Доступность](app-insights-monitor-web-app-availability.md)
