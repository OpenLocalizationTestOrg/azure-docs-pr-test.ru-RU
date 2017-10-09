---
title: "aaaAzure корреляции телеметрии аналитики приложений | Документы Microsoft"
description: "Корреляция данных телеметрии Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Корреляция данных телеметрии в Application Insights

В Здравствуй, мир micro службы каждой логической операции требует работу с разными компонентами службы hello. Служба [Application Insights](app-insights-overview.md) может отдельно отслеживать каждый из этих компонентов. Hello веб-приложения компонента взаимодействует с учетными данными пользователя toovalidate компонент поставщика проверки подлинности и с данными tooget hello API компонентов для визуализации. компонент API Hello в свою очередь можно запрашивать данные из других служб и использовать компоненты поставщика кэша и уведомить hello выставления счетов компонентом, об этом вызове. Application Insights поддерживает распределенную корреляцию данных телеметрии. Она позволяет toodetect, какой компонент отвечает за сбоями или снижения производительности.

В этой статье описываются hello использует модель, toocorrelate телеметрии Application Insights отправлены в нескольких компонентах. Рассматриваются методы распространения контекста hello и протоколов. Она также охватывает hello реализации концепций корреляции hello на разных языках и платформах.

## <a name="telemetry-correlation-data-model"></a>Модель корреляции данных телеметрии

Application Insights определяет [модель данных](application-insights-data-model.md) для распределенной корреляции данных телеметрии. tooassociate телеметрии с логической операции hello, каждый элемент телеметрии имеет поле контекста с именем `operation_Id`. Этот идентификатор совместно используется каждый элемент данных телеметрии в трассировке распределенных hello. Поэтому даже в случае потери телеметрии из одного уровня вы по-прежнему можете связывать данные телеметрии, сообщаемые другими компонентами.

Распределенные логической операции обычно состоит из набора операций меньше - запросов, обрабатываемых одним из компонентов hello. Эти операции определяются [телеметрией запросов](application-insights-data-model-request-telemetry.md). Каждый элемент телеметрии запросов имеет собственный уникальный `id`, который его глобально идентифицирует. И все данные телеметрии - трассировок, исключения, связанного с этим запросом и т.д. необходимо задать hello `operation_parentId` toohello значение hello запроса `id`.

Каждый исходящий операции, например, http вызов tooanother компонента, представленного объектом [телеметрии зависимости](application-insights-data-model-dependency-telemetry.md). Телеметрия зависимостей также определяет собственный `id`, который является глобально уникальным. Телеметрия запросов, инициированная этим вызовом зависимостей, использует его в качестве `operation_parentId`.

Можно создать представление hello использования распределенной логической операции `operation_Id`, `operation_parentId`, и `request.id` с `dependency.id`. Эти поля также определять порядок причинно-следственных связей hello вызовов телеметрии.

В среде служб micro трассировки из компонентов может перейти в различных хранилищах toohello. Каждый компонент может иметь свой собственный ключ инструментирования в Application Insights. tooget данные телеметрии для логическую операцию hello, требуются tooquery данные из каждого хранилища. При огромное число систем хранения данных необходимо toohave подсказку о том, где toolook Далее.

Application Insights, модели анализа данных определяет два поля toosolve этой проблемы: `request.source` и `dependency.target`. Первое поле Hello определяет hello компонент, который инициировал запрос hello зависимостей, а hello второй определяет какой компонент вернул ответ hello вызова зависимостей hello.


## <a name="example"></a>Пример

Рассмотрим пример приложения STOCK цен, показывающая hello текущего рыночной цены акций, с помощью внешнего API hello вызывается API биржевые СВОДКИ. Hello ЦЕНЫ АКЦИЙ приложения имеет страницу `Stock page` открываемые hello клиента веб-браузера с помощью `GET /Home/Stock`. запросы приложения Hello hello STOCK API с помощью вызова HTTP `GET /api/stock/value`.

Вы можете проанализировать итоговые данные телеметрии, выполнив запрос:

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

В примечании представление hello результат, что все данные телеметрии элементы обычно имеют корневой hello `operation_Id`. При вызове метода ajax сделанных страница hello — новый уникальный идентификатор `qJSXU` телеметрия зависимостей назначенный toohello и идентификатор элемента pageView используется как `operation_ParentId`. В свою очередь запрос сервера использует идентификатор AJAX в качестве `operation_ParentId`, и т. д.

| itemType   | name                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Stock page                |              | STYz               | STYz         |
| dependency | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| запрос    | GET Home/Stock            | KqKwlrSt9PA= | qJSXU              | STYz         |
| dependency | GET /api/stock/value      | bBrf2L7mm2g= | KqKwlrSt9PA=       | STYz         |

Теперь, когда hello вызовов `GET /api/stock/value` внесенные tooan внешней службы требуется удостоверение hello tooknow этого сервера. Поэтому можно соответствующим образом задать поле `dependency.target`. Если внешняя служба hello не поддерживает мониторинг - `target` задается имя узла toohello hello службы как `stock-prices-api.com`. Однако если этой службы определяет себя, возвращая предварительно определенный заголовок HTTP - `target` содержит удостоверение службы hello, позволяющий toobuild распределенных трассировки Application Insights, запрашивая данные телеметрии из этой службы. 

## <a name="correlation-headers"></a>Заголовки корреляции

Мы работаем над предложение RFC для hello [корреляции протокол HTTP](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md). Это предложение определяет два заголовка:

- `Request-Id`выполнение hello глобально уникальный идентификатор вызова hello
- `Correlation-Context`-выполнение hello имя пары коллекции значение свойства трассировки распределенного hello

Стандартная Hello также определяет две схемы из `Request-Id` поколения - плоской и иерархической. Схема неструктурированного hello, производится с известным `Id` ключ, определенный для hello `Correlation-Context` коллекции.

Application Insights определяет hello [расширения](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) для корреляции hello протокол HTTP. Она использует `Request-Context` имя пары "значение" hello toopropagate коллекцию свойств, используемых hello непосредственного вызывающего или вызываемого объекта. Пакет SDK для Application Insights использует этот заголовок tooset `dependency.target` и `request.source` поля.

## <a name="open-tracing-and-application-insights"></a>OpenTracing и Application Insights

Модели данных [OpenTracing](http://opentracing.io/) и Application Insights выглядят следующим образом: 

- `request`, `pageView` сопоставляет слишком**диапазон** с`span.kind = server`
- `dependency`Сопоставляет слишком**диапазон** с`span.kind = client`
- `id`из `request` и `dependency` сопоставляет слишком**Span.Id**
- `operation_Id`Сопоставляет слишком**числовое обозначение TraceId**
- `operation_ParentId`Сопоставляет слишком**ссылки** типа`ChileOf`

В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.

Определения основных понятий OpenTracing см. в [спецификации](https://github.com/opentracing/specification/blob/master/specification.md) и [соглашениях о семантике](https://github.com/opentracing/specification/blob/master/semantic_conventions.md).


## <a name="telemetry-correlation-in-net"></a>Корреляция данных телеметрии в .NET

Со временем .NET определено несколько способов toocorrelate телеметрии и диагностики журналы. Отсутствует `System.Diagnostics.CorrelationManager` разрешение tootrack [LogicalOperationStack и ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx). `System.Diagnostics.Tracing.EventSource`и Windows ETW определить метод hello [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx). `ILogger` использует [области журналов](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes). WCF и HTTP подключают распространение "текущего" контекста.

Однако эти методы не обеспечивали поддержку автоматической распределенной трассировки. `DiagnosticsSource`выполняется toosupport способом автоматически кросс-машины корреляции. Библиотеки .NET поддержки диагностики источников и разрешить автоматическое межкомпьютерные распространение hello корреляции контекста через hello транспортного протокола, например http.

Hello [руководство tooActivities](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) в диагностике источника объясняет основы hello отслеживание действий. 

ASP.NET Core 2.0 поддерживает извлечение заголовков Http и запуск нового действия "hello". 

`System.Net.HttpClient`начальной версии `<fill in>` поддерживает автоматическое внедрение hello корреляции заголовки Http и отслеживания hello вызовов http как действие.

Новый модуль Http [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) для hello классический ASP.NET. Этот модуль реализует корреляцию данных телеметрии с помощью DiagnosticsSource. Он запускает действие, исходя их заголовков входящего запроса. Он также сопоставляет телеметрии из hello разные этапы обработки запроса. Даже в тех случаях, hello при запуске каждого из этапов обработки IIS в потоках различных управление.

Начальной версии пакета SDK аналитики приложений `2.4.0-beta1` использует телеметрии toocollect DiagnosticsSource и активности и связать его с текущим действием hello. 

## <a name="next-steps"></a>Дальнейшие действия

- [API Application Insights для пользовательских событий и метрик](app-insights-api-custom-events-metrics.md)
- Подключите все компоненты своей микрослужбы с помощью Application Insights. Ознакомьтесь со сведениями о [поддерживаемых платформах](app-insights-platforms.md).
- В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.
- Узнайте, каким образом слишком[расширения и фильтровать данные телеметрии](app-insights-api-filtering-sampling.md).
