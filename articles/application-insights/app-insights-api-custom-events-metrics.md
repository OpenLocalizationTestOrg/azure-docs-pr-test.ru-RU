---
title: "aaaApplication аналитики API пользовательские события и метрики | Документы Microsoft"
description: "Вставить несколько строк кода в tootrack устройства или классического приложения, веб-страницы или службы, использование и диагностировать проблемы."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>API Application Insights для пользовательских событий и метрик

Вставить несколько строк кода в ваш приложения toofind out действиями пользователей с ним или toohelp диагностировать проблемы. Вы можете отправлять телеметрию из устройств и классических приложений, веб-клиентов и веб-серверов. Используйте hello [Azure Application Insights](app-insights-overview.md) основной API телеметрии toosend пользовательские события и метрики и версий стандартной телеметрии. Этот API является hello же API-Интерфейсом этого стандарта hello, используемое сборщики данных Application Insights.

## <a name="api-summary"></a>Сводные данные API
Hello API единообразно для всех платформ, помимо несколько небольшие вариации.

| Метод | Область использования |
| --- | --- |
| [`TrackPageView`](#page-views) |Страницы, экраны, колонки или формы. |
| [`TrackEvent`](#trackevent) |Действия пользователя и другие события. Использовать поведение или toomonitor производительности tootrack пользователя. |
| [`TrackMetric`](#trackmetric) |Показатели производительности, такие как длина очереди не события, связанные с toospecific. |
| [`TrackException`](#trackexception) |Регистрация исключений для диагностики. Трассировки, где они происходят в отношение tooother события и трассировки стека. |
| [`TrackRequest`](#trackrequest) |Ведение журнала hello частота и длительность запросов к серверу для анализа производительности. |
| [`TrackTrace`](#tracktrace) |Сообщения журналов диагностики. Можно также использовать журналы сторонних приложений. |
| [`TrackDependency`](#trackdependency) |Длительность hello ведения журнала и частоты вызовов tooexternal компонентов, от которых зависит приложение. |

Вы можете [присоедините свойства и метрики](#properties) toomost этих вызовов телеметрии.

## <a name="prep"></a>Перед началом работы
Если у вас еще нет ссылки на пакет SDK Application Insights, выполните указанные ниже действия.

* Добавьте проект tooyour hello пакет SDK Application Insights.

  * [проект ASP.NET;](app-insights-asp-net.md)
  * [проект Java;](app-insights-java-get-started.md)
  * [JavaScript на каждой веб-странице.](app-insights-javascript.md) 
* В программный код устройства или веб-сервера необходимо добавить:

    *C#:* `using Microsoft.ApplicationInsights;`

    *Visual Basic:* `Imports Microsoft.ApplicationInsights`

    *Java:* `import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Создание экземпляра TelemetryClient
Создайте экземпляр `TelemetryClient` (за исключением JavaScript на веб-страницах).

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

Класс TelemetryClient является потокобезопасным.

Рекомендуется использовать экземпляр TelemetryClient для каждого модуля приложения. Для экземпляра может иметь один экземпляр TelemetryClient в web service tooreport входящих HTTP-запросы, а другой в по промежуточного слоя класс tooreport бизнес-логики событий. Например, можно задать свойства `TelemetryClient.Context.User.Id` tootrack пользователей и сеансов, или `TelemetryClient.Context.Device.Id` tooidentify hello машины. Эта информация является tooall присоединенные события, которые hello отправляет экземпляра.

## <a name="trackevent"></a>TrackEvent (Отслеживание событий)
В Application Insights *пользовательское событие* — это точка данных, которую можно отобразить как суммарное значение в [обозревателе метрик](app-insights-metrics-explorer.md), а также как отдельные значения на вкладке [поиска по журналу диагностики](app-insights-diagnostic-search.md). (Это не связанных tooMVC или других framework» событий.»)

Вставить `TrackEvent` вызывает в ваш код toocount различных событий. как часто пользователи выбирают определенный компонент, как часто они достигают определенных целей, а также как часто возникают те или иные ошибки.

Например в приложении игрового отправьте событие, когда пользователь wins игры hello:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Просмотр событий в портал Microsoft Azure hello
Откройте toosee число событий, [обозревателя метрик](app-insights-metrics-explorer.md) , добавить новую диаграмму и, при необходимости выберите **события**.  

![Просмотр количества пользовательских событий](./media/app-insights-api-custom-events-metrics/01-custom.png)

счетчики hello toocompare различных событий установите тип диаграммы hello слишком**сетки**и группы, имя события:

![Выберите тип диаграммы hello и группирование](./media/app-insights-api-custom-events-metrics/07-grid.png)

В сетке hello, щелкая событий имя toosee отдельные копии этого события. toosee более подробно описывается - щелкните любое событие, в списке hello.

![Детализация hello события](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus на определенные события в поиска или обозревателя метрик набор hello колонке фильтра toohello имена событий вы заинтересованы в:

![Откройте "Фильтры", разверните пункт "Имя события" и выберите одно или несколько значений.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Пользовательские события в службе аналитики

Hello телеметрии доступен в hello `customEvents` в таблицу [приложения аналитика Analytics](app-insights-analytics.md). Каждая строка представляет вызов слишком`trackEvent(..)` в вашем приложении. 

Если [выборки](app-insights-sampling.md) находится в операции, свойство itemCount hello показывает значение больше 1. Для примера itemCount == 10 означает, что из tootrackEvent() 10 вызовов hello выборки процесса передаются только один из них. tooget правильное число пользовательских событий, следует использовать таким образом использовать код, например `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric (Отслеживание метрик)

Application Insights можно диаграммы метрик, которые не являются tooparticular присоединенные события. Например, можно отслеживать длину очереди через регулярные промежутки времени. Метрики hello отдельные измерения представляют интерес, меньше, чем hello вариантов и трендов и поэтому статистические диаграммы могут применяться.

Порядок toosend метрики аналитики tooApplication, можете воспользоваться hello `TrackMetric(..)` API. Существует два способа toosend метрики: 

* Отдельное значение. Каждый раз при выполнении измерения в приложении, следует отправить соответствующее значение hello tooApplication аналитики. Например пусть метрики, описывающие hello количество элементов в контейнере. Во время конкретного периода времени Вначале переведите трех элементов в контейнере hello и затем удалите два элемента. Соответственно, вызовите `TrackMetric` дважды: сначала при передаче значения hello `3` и затем hello значение `-2`. Application Insights сохраняет оба значения от вашего имени. 

* Агрегирование. При работе с метриками отдельные измерения редко представляют интерес. Вместо этого обычно важна сводка того, что произошло за определенный период времени. Такая сводка называется _агрегированием_. В приведенном выше примере hello, является статистическим выражением суммы метрики hello для этого периода времени `1` и число hello значения метрики hello `2`. При использовании подхода hello статистической обработки, можно вызвать только `TrackMetric` один раз за время периода и отправить hello статистические значения. Это рекомендованный подход, поскольку он может значительно снизить стоимость hello и производительности издержки, отправляя меньшее количество данных указывает tooApplication аналитики, при сборе вся необходимая информация по-прежнему hello.

### <a name="examples"></a>Примеры:

#### <a name="single-values"></a>Отдельные значения

toosend одиночное значение метрики:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Агрегированные метрики

Рекомендуется перед их отправкой из вашего приложения, tooreduce пропускной способности, производительности, стоимости и tooimprove tooaggregate метрики.
Ниже представлен пример кода для агрегирования.

*C#*

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>Пользовательские метрики в обозревателе метрик

результаты toosee hello, откройте обозреватель метрик и добавить новую диаграмму. Изменение диаграммы tooshow hello вашей метрики.

> [!NOTE]
> В списке доступных метрик hello вашей пользовательской метрики может занять несколько минут tooappear.
>

![Добавьте новую диаграмму или выберите существующую, а в поле Custom (Пользовательские) выберите свою метрику](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Настраиваемые метрики в аналитике

Hello телеметрии доступен в hello `customMetrics` в таблицу [приложения аналитика Analytics](app-insights-analytics.md). Каждая строка представляет вызов слишком`trackMetric(..)` в вашем приложении.
* `valueSum`— Это сумма hello hello измерений. Среднее значение hello tooget, деление на `valueCount`.
* `valueCount`-hello число измерений, которые были сведены в это `trackMetric(..)` вызова.

## <a name="page-views"></a>Просмотры страниц
В устройстве или приложении веб-страницы телеметрия просмотров страницы отображается по умолчанию при загрузке каждого экрана или страницы. Однако можно изменить, представления страниц tootrack время дополнительные или другие. Например приложение, которое отображает вкладки или колонок, может потребоваться tootrack страницы всякий раз, когда пользователь hello открывается новая колонка.

![Область "Использование" в колонке "Обзор"](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Данные пользователя и сеанса отправляется как свойства вместе с просмотров страниц, поэтому hello пользователей и сеансов диаграммы поступать в активном состоянии при отсутствии телеметрии просмотров страниц.

### <a name="custom-page-views"></a>Пользовательские данные о просмотре страницы
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


При наличии нескольких вкладок в разных HTML-страницы, можно указать URL-адрес hello слишком:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Время просмотра страниц
По умолчанию hello раз отмечено как **время загрузки страницы** отсчитываются от при hello браузер отправляет запрос hello, пока не будет вызван события загрузки страницы браузера hello.

Вместо этого вы можете выбрать один из таких вариантов:

* Задать явные длительность в hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) вызова: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Использовать вызовы времени представление страницы приветствия `startTrackPage` и `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Здравствуйте, имя, которое используется как первый параметр hello связывает hello запуска и остановки вызовы. По умолчанию toohello имени текущей страницы.

Hello длительности, отображаемых в обозревателе метрик являются производными от hello интервал между hello полученный загрузки страницы, запускать и останавливать вызовов. Он работает tooyou какие интервал фактически времени.

### <a name="page-telemetry-in-analytics"></a>Телеметрия страниц в службе аналитики

В [службе аналитики](app-insights-analytics.md) две таблицы содержат данные по операциям в браузере.

* Hello `pageViews` таблица содержит данные о hello URL-адрес и заголовок страницы
* Hello `browserTimings` таблице содержатся данные о производительности клиента, такие как время, затраченное tooprocess hello hello входящих данных

toofind как долго браузера hello принимает tooprocess различные страницы:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

toodiscover popularities hello различных браузеров:

```
pageViews | summarize count() by client_Browser
```

tooassociate представления tooAJAX обращениями к страницам, соединения с зависимостями:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest (Отслеживание запросов)
сервер Hello SDK использует TrackRequest toolog HTTP-запросов.

Можно также вызвать ее самостоятельно Если требуется toosimulate запросы в контексте, где отсутствует служба модуля hello web работает.

Однако рекомендуется использовать hello телеметрии запроса toosend способом — где hello запрос выступает в качестве <a href="#operation-context">контекст операции</a>.

## <a name="operation-context"></a>Контекст операции
Можно связать элементы телеметрии путем присоединения toothem общие идентификатором операции. стандартный модуль отслеживания запроса Hello делает это для исключения и другие события, которые отправляются во время обработки HTTP-запроса. В [поиска](app-insights-diagnostic-search.md) и [Analytics](app-insights-analytics.md), можно использовать поиск tooeasily идентификатор hello все события, связанные с запросом hello.

Hello простым способом tooset hello идентификатор — tooset контекст операции с помощью этого шаблона:

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Вместе с установкой контекст операции `StartOperation` создает элемент телеметрии указанного типа hello. Он отправляет данные телеметрии hello элементов при реализации операции hello, или если явным образом вызвать `StopOperation`. Если вы используете `RequestTelemetry` как тип телеметрии hello, его длительность устанавливается интервал toohello истекло время ожидания между start и stop.

Контексты операции не могут быть вложенными. Если уже контекст операции, то его идентификатор связан с все hello содержатся элементы, включая hello элемент, созданный с `StartOperation`.

В поле поиска контекст операции hello — hello используется toocreate **связанные элементы** списка:

![Связанные элементы](./media/app-insights-api-custom-events-metrics/21.png)

Дополнительные сведения об отслеживании пользовательских операций см. в разделе [application-insights-custom-operations-tracking.md].

### <a name="requests-in-analytics"></a>Запросы в аналитике 

В [приложения аналитика Analytics](app-insights-analytics.md), запрашивает Показать вверх в hello `requests` таблицы.

Если [выборки](app-insights-sampling.md) — в операции, свойство itemCount hello покажет значение больше 1. Для примера itemCount == 10 означает, что из tootrackRequest() 10 вызовов hello выборки процесса передаются только один из них. tooget правильного числа запросов, а Средняя длительность, разбитых на имена запроса, можно использовать следующий код:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException (Отслеживание исключений)
Отправьте аналитики tooApplication исключения:

* слишком[их](app-insights-metrics-explorer.md), как показатель частоты hello проблемы.
* слишком[проверьте отдельные копии](app-insights-diagnostic-search.md).

Hello отчеты включают hello трассировки стека.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

пакеты SDK Hello перехватывать исключения, многие автоматически, поэтому не всегда нужно toocall TrackException явным образом.

* ASP.NET: [писать код исключения toocatch](app-insights-asp-net-exceptions.md).
* J2EE: [исключения перехватываются автоматически](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: исключения перехватываются автоматически. Если вы хотите toodisable автоматический сбор сведений, добавьте фрагмента кода toohello строки, которые можно вставить в веб-страницы:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Исключения в службе аналитики

В [приложения аналитика Analytics](app-insights-analytics.md), отображаются в hello исключения `exceptions` таблицы.

Если [выборки](app-insights-sampling.md) — в операции hello `itemCount` свойств отображается значение больше 1. Для примера itemCount == 10 означает, что из tootrackException() 10 вызовов hello выборки процесса передаются только один из них. tooget правильное число исключений, разбитых на тип исключения, можно использовать следующий код:

```
exceptions | summarize sum(itemCount) by type
```

Большинство важных сведений стека уже извлеченные в отдельные переменные, но вы можете извлечь друг от друга hello hello `details` дополнительные tooget структуры. Так как эта структура является динамическим, необходимо привести тип результата toohello hello, ожидаемых. Например:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

исключения tooassociate с их связанные запросы соединения:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace (Отслеживание трассировки)
Используйте TrackTrace toohelp диагностики проблем, отправляя tooApplication «цепочка навигации» дополнительная информация. Вы можете отправлять блоки диагностических данных и проверять их с помощью [поиска по журналу диагностики](app-insights-diagnostic-search.md).

[Журнал адаптеров](app-insights-asp-net-trace-logs.md) использовать этот портал toohello журналы сторонних toosend API.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


Вы можете выполнять поиск содержимого сообщения, но (в отличие от значений свойств) не можете фильтровать его.

ограничения на размер Hello `message` гораздо выше, чем максимально hello свойства.
Преимуществом TrackTrace является относительно большие объемы данных можно поместить в сообщение hello. например данных POST.  

Кроме того можно добавить сообщение tooyour уровня серьезности. И, как и другие данные телеметрии, вы можете добавить toohelp значения свойств, фильтровать или поиска для разных наборов трассировок. Например:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

В [поиска](app-insights-diagnostic-search.md), можно затем легко отфильтровать все сообщения hello уровня серьезности конкретного, относящиеся tooa определенной базы данных.


### <a name="traces-in-analytics"></a>Трассировки в службе аналитики

В [приложения аналитика Analytics](app-insights-analytics.md), звонит tooTrackTrace Показать hello `traces` таблицы.

Если [выборки](app-insights-sampling.md) находится в операции, свойство itemCount hello показывает значение больше 1. Для примера itemCount == 10 означает, что 10 вызывает слишком`trackTrace()`, процесс выборки hello передаются только в одной из них. tooget правильного числа вызовов трассировки, следует использовать таким образом кода например `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency (Отслеживание зависимостей)
Используйте hello TrackDependency вызовите tootrack hello отклика и частоты успешных вызовов tooan внешним фрагментам кода. Hello результаты отображаются в форме диаграммы зависимости hello hello портала.

```C#
var success = false;
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

Помните, сервера hello, пакеты SDK включают [зависимостей модуля](app-insights-asp-net-dependencies.md) , обнаруживает и отслеживает определенные вызовы зависимостей автоматически — например, toodatabases и API-интерфейсов REST. У вас есть tooinstall агент на модуле hello server toomake работы. Используйте этот вызов не перехватывать вызовы tootrack, hello автоматического отслеживания, или если вы не хотите tooinstall hello агента.

изменить tooturn off hello стандартного модуля Отслеживание зависимостей, [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) и удалить ссылку hello слишком`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Зависимости в службе аналитики

В [приложения аналитика Analytics](app-insights-analytics.md), trackDependency вызовы отображаются в hello `dependencies` таблицы.

Если [выборки](app-insights-sampling.md) находится в операции, свойство itemCount hello показывает значение больше 1. Для примера itemCount == 10 означает, что из tootrackDependency() 10 вызовов hello выборки процесса передаются только один из них. tooget правильное количество зависимостей, разбитых на целевого компонента, можно использовать следующий код:

```
dependencies | summarize sum(itemCount) by target
```

зависимости tooassociate с их связанные запросы соединения:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Очистка данных
Как правило hello SDK отправляет данные, в некоторых случаях выбрана toominimize hello влияние на пользователей hello. Однако в некоторых случаях может потребоваться tooflush hello буфера — например, при использовании hello SDK в приложении, которое завершает работу.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Обратите внимание, что функции hello асинхронной для hello [телеметрии канала сервера](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>Прошедшие проверку пользователи
В веб-приложении пользователи по умолчанию идентифицируются файлами cookie. Пользователь может быть учтен более одного раза при доступе к приложению с другого компьютера или браузера либо при удалении файлов cookie.

Если пользователи входят в приложении tooyour, можно получить более точный подсчет, установив идентификатор пользователя с проверкой подлинности hello в коде hello браузера:

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

Например, в веб-приложении MVC ASP.NET.

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

Это не значит необходимые toouse hello фактическое учетное имя пользователя. Он имеет только toobe идентификатор, уникальный toothat пользователя. Он не должен содержать пробелы или знаки hello `,;=|`.

Идентификатор пользователя Hello также задать в файле cookie сеанса и отправки toohello сервера. Если установлен SDK сервера hello, hello проверку подлинности пользователя, которого код отправляется как часть свойств контекста hello телеметрии клиента и сервера. Затем можно выполнить фильтрацию и поиск.

Приложения в учетные записи групп пользователей можно также передать идентификатор учетной записи hello (с hello же ограничения на символы).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

В [обозревателе метрик](app-insights-metrics-explorer.md) можно создать диаграмму для отображения количества **пользователей, прошедших проверку подлинности**, а также **учетных записей пользователей**.

Кроме того, можно [выполнить поиск](app-insights-diagnostic-search.md) точек данных клиентов с определенными именами пользователей и учетными записями.

## <a name="properties"></a>Фильтрация, поиск и сегментация данных с помощью свойств
Можно присоединить измерениях и свойства tooyour событий (и также toometrics, представления страниц, исключения и другие данные телеметрии).

*Свойства* представляют собой строковые значения, которые используются toofilter телеметрии в отчетах об использовании hello. Например если ваше приложение предоставляет несколько игр, можно присоединить hello имя события игры tooeach hello, можно увидеть, какие игры популярные.

Имеется ограничение в 8192 hello длина строки. (Если вы хотите toosend больших объемов данных, используйте параметр сообщение hello [TrackTrace](#track-trace).)

*Метрики* являются числовыми значениями, которые могут быть представлены в графическом виде. Например может потребоваться toosee при наличии постепенное увеличение hello оценки, которые достижения вашего игр. Hello диаграмм сегментации отдельные свойства, которые отправляются с событием hello, чтобы вы могли получить приветствия или с накоплением графики для различных игр.

Для значения метрики toobe правильно отображается они должны быть больше или равно too0.

Некоторые [ограничения на число свойств, значений свойств и показатели hello](#limits) , который можно использовать.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Будьте внимательны toolog не личные сведения в свойствах.
>
>

*При использовании метрик*выберите hello метрики из hello, откройте обозреватель метрик **настраиваемый** группы:

![Откройте обозреватель метрик, диаграммы выберите hello и выберите метрики hello](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Если ваш метрики отсутствует или hello **настраиваемый** заголовок колонки выбора закрыть hello не существует и повторите попытку позже. Метрики иногда может занять один час toobe статистическую обработку через конвейер hello.

*При использовании свойств и метрики*, сегмент метрика hello свойством hello:

![Задать группирования, а затем выберите свойство hello в списке Group by](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*В поиске диагностики*, можно просмотреть свойства hello и метриках отдельные вхождения события.

![Выберите экземпляр, а затем выберите "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Используйте hello **поиска** поле toosee вхождений событий, имеющих определенное значение свойства.

![Введите слово в поле поиска](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Дополнительные сведения о выражениях поиска.](app-insights-diagnostic-search.md)

### <a name="alternative-way-tooset-properties-and-metrics"></a>Альтернативный способ tooset свойства и метрики
Если он является более удобным, можно собирать параметров hello события в отдельном объекте:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Не используйте hello того же экземпляра элемента телеметрии (`event` в этом примере) toocall Track*() несколько раз. Это может привести к toobe телеметрии, отправленные с неправильной конфигурацией.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Пользовательские измерения и свойства в службе аналитики

В [Analytics](app-insights-analytics.md), настраиваемых метрик и свойства отображаются в hello `customMeasurements` и `customDimensions` атрибуты каждой записи телеметрии.

Например при добавлении свойства с именем «игры» tooyour телеметрии запроса этот запрос подсчитывающей hello различных значений «игра» и Показать среднее hello hello пользовательские метрики «оценка»:

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Обратите внимание на указанные ниже моменты.

* При извлечении значения из hello customDimensions или customMeasurements JSON имеет динамический тип и поэтому необходимо привести `tostring` или `todouble`.
* Учетная запись tootake вероятность hello [выборки](app-insights-sampling.md), следует использовать `sum(itemCount)`, а не `count()`.



## <a name="timed"></a> События времени
Иногда требуется toochart понадобившееся tooperform действие. Например, может потребоваться tooknow как долго выполнять пользователи tooconsider вариантов в игру. Для этого можно использовать параметр измерения hello.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Свойства по умолчанию для настраиваемой телеметрии
Если требуется tooset значения свойств по умолчанию для некоторых hello пользовательских событий, которые пишутся, можно установить их на экземпляр TelemetryClient. Они представляют подключенных tooevery телеметрии элементов, отправляемых с клиента.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Вызовы отдельных телеметрии можно переопределить значения по умолчанию hello в словарях их свойства.

*Для веб-клиентов JavaScript*[используйте инициализаторы телеметрии JavaScript](#js-initializer).

*Данные телеметрии tooall свойства tooadd*, включая hello данные из стандартной коллекции модулей, [реализовать `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Выборка, фильтрация и обработка данных телеметрии
Можно написать код tooprocess телеметрии перед отправкой из пакета SDK для hello. Обработка Hello включает в себя данные, отправленные из модулей стандартной телеметрии hello, например коллекции запроса HTTP и коллекция зависимостей.

[Добавить свойства](app-insights-api-filtering-sampling.md#add-properties) tootelemetry путем реализации `ITelemetryInitializer`. Например, можно добавить номера версий или значения, вычисленные на основе других свойств.

[Фильтрация](app-insights-api-filtering-sampling.md#filtering) можно изменить или отменить телеметрии перед отправкой из пакета SDK для hello путем реализации `ITelemetryProcesor`. Управлять что отправлено или удалены, но у tooaccount для hello влияет на показатели. В зависимости от того, каким образом удалить элементы то можно потерять toonavigate возможность hello между связанных элементов.

[Выборка](app-insights-api-filtering-sampling.md) является упакованных решения tooreduce hello объем данных, передаваемых через портал toohello приложения. Это происходит не затрагивая hello отображаются метрики. И это делается без влияния на ваши возможности toodiagnose проблемы с помощью перехода между элементами, такими как исключения, запросы и представления страницы.

[Подробнее](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Отключение телеметрии
слишком*динамически остановить и запустить* hello сбор и передача данных телеметрии:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

слишком*отключить выбранный Стандартная сборщики*— например, счетчики производительности, HTTP-запросы или зависимости — удалите или закомментируйте hello соответствующих строк в [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Это можно сделать, например, если требуется toosend TrackRequest данных.

## <a name="debug"></a>Режим разработчика
Во время отладки, бывает полезно toohave телеметрии ускорено через конвейер hello, так что можно сразу же увидеть результаты. Можно также получить дополнительные сообщения, которые помогают трассировку проблемах, связанных с телеметрии hello. Отключите этот режим в рабочей среде, так как он может замедлить работу приложения.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>Задание ключа hello инструментирования для выбранного пользовательского телеметрии
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> Динамический ключ инструментирования
Смешивание копирование телеметрии из разработки, тестирования и рабочих средах tooavoid вы можете [создать отдельные ресурсы Application Insights](app-insights-create-new-resource.md) и изменить свои ключи, в зависимости от среды hello.

Вместо получения hello ключ инструментирования из файла конфигурации hello, можно задать в коде. Установите раздел hello в метод инициализации, например global.aspx.cs в службы ASP.NET.

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



Веб-страницы, может потребоваться tooset его из hello веб-сервере состояния, а не кодирование буквально в сценарий hello. Например, на веб-странице, созданной в приложении ASP.NET.

*JavaScript в Razor*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>Класс TelemetryContext
Экземпляр TelemetryClient включает свойство Context, содержащее несколько значений, которые отправляются вместе со всеми данными телеметрии. Обычно задаются модулями стандартной телеметрии hello, но можно также установить их самостоятельно. Например:

    telemetry.Context.Operation.Name = "MyOperationName";

Если установить эти значения самостоятельно, рассмотрите возможность удаления hello соответствующую строку из [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), чтобы не перепутать значения и hello стандартных значений.

* **Компонент**: hello приложения и его версии.
* **Устройство**: данные об устройстве hello, где выполняется приложение hello. (В веб-приложениях это hello сервере или клиентском устройстве, которые отправляются данные телеметрии hello.)
* **InstrumentationKey**: hello ресурс Application Insights в Azure, в которой отображаются данные телеметрии hello. Обычно этот ресурс получают из файла ApplicationInsights.config.
* **Расположение**: hello географическое расположение устройств hello.
* **Операция**: В веб-приложениях hello текущего HTTP-запроса. В других типов приложений можно задать этот toogroup событий друг с другом.
  * **Id:** созданное значение, которое сопоставляет различные события, чтобы при проверке любого события в поиске по журналу диагностики можно было найти связанные элементы.
  * **Имя**: идентификатор, обычно hello URL-адрес hello HTTP-запроса.
  * **SyntheticSource**: Если не null или пустым, строка, указывающая источник hello hello запроса было определено как робот или веб-теста. По умолчанию он исключается из вычислений в обозревателе метрик.
* **Properties:** свойства, которые отправляются со всеми данными телеметрии. Это значение можно переопределить в отдельных вызовах Track*.
* **Сеанс**: hello пользовательского сеанса. Идентификатор Hello задан tooa создается значение, которое меняется, когда пользователь hello не было активных некоторое время.
* **User:** информация о пользователе.

## <a name="limits"></a>Ограничения
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

попадание ограничение частоты данных hello, используйте tooavoid [выборки](app-insights-sampling.md).

toodetermine содержится много данных, в статье [хранение данных и конфиденциальности](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Справочная документация
* [Справочник по ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)
* [Справочник по Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [Справочник по JavaScript](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Android SDK](https://github.com/Microsoft/ApplicationInsights-Android)
* [iOS SDK](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>Код пакета SDK
* [Базовый пакет SDK для ASP.NET](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Пакеты Windows Server](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Пакет SDK для Java](https://github.com/Microsoft/ApplicationInsights-Java)
* [Пакет SDK для JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)
* [Все платформы](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Вопросы
* *Какие исключения могут создаваться при вызовах Track_()?*

    Отсутствует. Не требуется toowrap их в конструкции try-catch. Если пакет SDK для hello сталкивается с проблемами, он сообщения в журнал в выходных данных консоли отладки hello и — если hello сообщения поступают через--диагностики поиска.
* *Есть ли tooget данных API-интерфейса REST с hello портала?*

    Да, hello [API доступа к данным](https://dev.applicationinsights.io/). Другие способы tooextract данные включают [Экспорт из Analytics tooPower BI](app-insights-export-power-bi.md) и [непрерывный Экспорт](app-insights-export-telemetry.md).

## <a name="next"></a>Дальнейшие действия
* [Поиск в Application Insights](app-insights-diagnostic-search.md)

* [Устранение неполадок](app-insights-troubleshoot-faq.md)


