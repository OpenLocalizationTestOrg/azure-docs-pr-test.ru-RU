---
title: "пользовательские операции aaaTrack с помощью пакета SDK .NET Azure Application Insights | Документы Microsoft"
description: "Отслеживание пользовательских операций с помощью пакета SDK .NET Azure Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>Отслеживание пользовательских операций с помощью пакета SDK Application Insights для .NET

Azure пакеты SDK Application Insights автоматически служб отслеживания входящих HTTP запрашивает и вызывает toodependent, например HTTP-запросы и запросы SQL. Отслеживание и корреляцию запросов и зависимостей позволяют получить видимость всего приложения hello скорости реагирования и надежность на все микрослужбами, объединяющие этого приложения. 

Существует класс шаблонов приложений, которые в принципе не поддерживаются. Для надлежащего мониторинга таких шаблонов требуется инструментирование кода вручную. В этой статье описывается несколько шаблонов, которые могут потребовать ручного инструментирования, например обработка пользовательской очереди сообщений и выполнение продолжительных фоновых задач.

Этот документ содержит инструкции по как tootrack пользовательских операций с hello пакет SDK Application Insights. Эта документация предназначена для:

- Application Insights для .NET (базовый пакет SDK) версии 2.4 или более поздней версии;
- Application Insights для веб-приложений (выполнение ASP.NET) версии 2.4 или более поздней версии;
- Application Insights для ASP.NET Core версии 2.1 или более поздней версии.

## <a name="overview"></a>Обзор
Операция — это логический элемент работы, выполняемый приложением. У нее есть имя, время запуска, длительность, результат и контекст выполнения, такой как имя пользователя, свойства и результат. Если операция A была инициирована операцией B, то операция B является родительской для A. У операции может быть только одна родительская операция, но множество дочерних операций. Дополнительные сведения об операциях и корреляции телеметрии см. в разделе [Корреляция данных телеметрии в Application Insights](application-insights-correlation.md).

Описывается операция hello в hello пакет SDK для .NET Application Insights, hello абстрактный класс [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) и его потомков [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) и [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>Отслеживание входящих операций 
Hello web Application Insights SDK автоматически собирает HTTP-запросов для приложения ASP.NET, работающие в конвейере служб IIS и всех приложений ASP.NET Core. Существуют решения для других платформ, поддержка которых осуществляется силами сообщества разработчиков. Тем не менее если приложение hello не поддерживается ни одним hello standard или общественный решений, можно инструментировать его вручную.

Другой пример, в котором требуется настраиваемое отслеживание — работник hello, получающий элементы из очереди hello. Для некоторых очередей hello вызывать tooadd сообщение, которое toothis очереди отслеживается в качестве зависимости. Однако операции высокого уровня hello, описывающий обработку сообщения не собираются автоматически.

Давайте посмотрим, как можно отслеживать такие операции.

На высоком уровне задачу hello — toocreate `RequestTelemetry` и известные свойства. По завершении операции hello отслеживать телеметрии hello. Привет, следующий пример демонстрирует эту задачу.

### <a name="http-request-in-owin-self-hosted-app"></a>HTTP-запрос в резидентном приложении Owin
В этом примере мы следовать hello [протокол HTTP для корреляции](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md). Следует ожидать tooreceive заголовки, которые описаны.

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

Hello протокол HTTP для корреляции также объявляет hello `Correlation-Context` заголовок. Однако здесь он опускается для простоты.

## <a name="queue-instrumentation"></a>Инструментирование очереди
Для соединения по протоколу HTTP мы создали протокол toopass сведения о корреляции. С помощью протоколов некоторые очереди можно передать дополнительные метаданные вместе с приветственное сообщение, а также с другими пользователями, которые вы не можете.

### <a name="service-bus-queue"></a>Очередь служебной шины
С hello Azure [очереди Service Bus](../service-bus-messaging/index.md), можно передать контейнер свойств, а также приветственное сообщение. Мы используем toopass hello, идентификатор корреляции.

очередь Service Bus Hello использует протоколы на основе TCP. Application Insights не предусматривает автоматическое отслеживание операций с очередями, поэтому мы отслеживаем их вручную. Hello dequeue операция API принудительного типа, и мы tootrack его.

#### <a name="enqueue"></a>Постановка в очередь

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a>Process
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a>Очередь службы хранилища Azure
Следующий пример показывает как Hello tootrack hello [очереди службы хранилища Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) операции и согласовывать телеметрии между производителем hello, потребитель hello и хранилища Azure. 

очередь хранилища Hello есть HTTP API. Все вызовы toohello очереди отслеживаемых hello сборщика зависимостей аналитики приложений для HTTP-запросов.
Убедитесь, что в `applicationInsights.config` есть `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer`. Если вас его нет, добавьте его программными средствами, как описано в [фильтрацию и предварительной обработки в Azure пакет SDK Application Insights hello](app-insights-api-filtering-sampling.md).

При настройке ApplicationInsights вручную убедитесь, что вы создали и инициализировали `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` так же, как указано ниже.
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

Также может потребоваться идентификатор операции toocorrelate hello Application Insights с идентификатором hello хранилища запросов. Сведения о том, как tooset и get хранилища запросов клиента и код запроса сервера см. в разделе [мониторинг, диагностика и устранение неполадок хранилища Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).

#### <a name="enqueue"></a>Постановка в очередь
Поскольку очереди хранилища поддерживает hello HTTP API, все операции с очередью hello, автоматически отслеживаются контекстом Application Insights. Во многих случаях этого инструментария должно быть достаточно. Однако toocorrelate трассировки на стороне получателя hello и производитель трассировок, необходимо передать некоторый контекст для корреляции аналогично toohow мы это можно сделать в hello протокол HTTP для корреляции. 

В этом примере мы отслеживания hello необязательно `Enqueue` операции. Вы можете:

 - **Сопоставлять повторных попыток (если таковые имеются)**: все они имеют один общий родительский объект, hello `Enqueue` операции. В противном случае они выполняется отслеживаются в качестве дочерних элементов hello входящего запроса. При наличии нескольких логических запросов toohello очереди, бывает сложно toofind какие вызов завершился повторных попыток.
 - **Сопоставить журналы службы хранилища Azure (при необходимости)**: они сопоставляются с данными телеметрии Application Insights.

Hello `Enqueue` операции является дочерним hello родительской операции (например, входящие HTTP-запроса). вызов зависимостей Hello HTTP является потомком hello hello `Enqueue` операции и hello внучатый hello входящего запроса:

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

сообщает tooreduce hello объем телеметрии приложения или если вы не хотите tootrack hello `Enqueue` операции по другим причинам, используйте hello `Activity` API напрямую:

- Создание (и запустить) новый `Activity` вместо запуска операции hello Application Insights. Это сделать *не* требуется tooassign все свойства на его, за исключением имени операции hello.
- Сериализовать `yourActivity.Id` в полезные данные сообщения hello вместо `operation.Telemetry.Id`. Кроме того, можно использовать `Activity.Current.Id`.


#### <a name="dequeue"></a>Выведение из очереди
Аналогичным образом слишком`Enqueue`, фактический запрос toohello хранилища очереди HTTP, автоматически отслеживаются контекстом Application Insights. Здравствуйте, однако `Enqueue` предположительно выполняется в контексте родительского hello, например контекст входящего запроса. Пакеты SDK Application Insights автоматически сопоставлять такая операция (и его часть HTTP) с родительским запросом hello и данные других телеметрии, отправленные в hello же области.

Hello `Dequeue` операция является непростой задачей. пакет SDK для Application Insights Hello автоматически отслеживает HTTP-запросов. Тем не менее он не знает hello корреляции контекста, пока не анализируется приветственное сообщение. Это не возможные toocorrelate hello HTTP запроса tooget приветственных сообщений hello остальные телеметрии hello.

Во многих случаях бывает полезным toocorrelate hello HTTP запроса и для других трассировок, а также toohello очереди. Hello следующем примере показано, как toodo его:

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a>Process

В следующем примере hello, мы трассировки входящего сообщения в определенном аналогично toohow мы отслеживать входящие HTTP запроса:

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

Другие операции очереди также можно инструментировать. Операцию заглядывания следует инструментировать так же, как операцию выведения из очереди. Инструментировать операции управления очередью необязательно. Application Insights отслеживает такие операции, как HTTP, и в большинстве случаев этого достаточно.

При инструментировании удаления сообщений, убедитесь, что операции hello задания идентификаторов (корреляция). Кроме того, можно использовать hello `Activity` API. Затем не требуется tooset операции идентификаторы для элементов телеметрии hello, так как Application Insights делает это для вас:

- Создайте новый `Activity` после элемента из очереди hello.
- Используйте `Activity.SetParentId(message.ParentId)` toocorrelate потребитель и производитель журналы.
- Запуск hello `Activity`.
- Отслеживайте операции выведения из очереди, обработки и удаления с помощью вспомогательных методов `Start/StopOperation`. Сделать это из hello же асинхронной управления потоком (контекст выполнения). Таким образом они будут сопоставлены должным образом.
- Остановка hello `Activity`.
- Используйте `Start/StopOperation` или вручную вызовите телеметрию `Track`.

### <a name="batch-processing"></a>Пакетная обработка
Некоторые очереди поддерживают вывод из очереди нескольких сообщений с помощью одного запроса. Обработка таких сообщений предположительно независим и принадлежит toohello различных логических операций. В этом случае это не hello возможных toocorrelate `Dequeue` обработки сообщений tooparticular операции.

Обработка каждого сообщения должна выполняться в собственном асинхронном потоке управления. Дополнительные сведения см. в разделе hello [исходящие зависимости отслеживания](#outgoing-dependencies-tracking) раздела.

## <a name="long-running-background-tasks"></a>Длительные фоновые задачи
Некоторые приложения запускают длительные операции, которые могут быть вызваны запросами пользователей. С точки зрения трассировка и инструментирование hello не отличается от инструментария запроса или зависимостей: 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

В этом примере мы используем `telemetryClient.StartOperation` toocreate `RequestTelemetry` и заполнения hello корреляции контекста. Предположим, что у вас есть родительского операцию, которая была создана с входящими запросами, которые запланированную операцию hello. При условии, что `BackgroundTask` запускается в Здравствуйте же асинхронного потока управления как входящий запрос, он связан с этим операция родительского. `BackgroundTask`и все элементы вложенного телеметрии автоматически связаны с запросом hello, вызвавшей ее, даже в том случае, после завершения запроса hello.

При запуске задачу hello из hello фоновый поток, который не имеет любой операции (`Activity`) связанные с ней `BackgroundTask` не имеет любого родительского элемента. Тем не менее у нее могут быть вложенные операции. Все элементы телеметрии, полученные от задачу hello становятся коррелированные toohello `RequestTelemetry` в `BackgroundTask`.

## <a name="outgoing-dependencies-tracking"></a>Отслеживание исходящих зависимостей
Можно отслеживать собственный тип зависимостей или операцию, не поддерживаемую Application Insights.

Hello `Enqueue` метод в очередь Service Bus hello или очередь hello хранилища можно использовать в качестве примеров таких настраиваемое отслеживание.

общий подход Hello для отслеживания пользовательских зависимостей является:

- Вызовите hello `TelemetryClient.StartOperation` метод (расширения), который заполняет hello `DependencyTelemetry` свойства, необходимые для корреляции и некоторые другие свойства (время начала метка, длительность).
- Настроить другие настраиваемые свойства hello `DependencyTelemetry`, такие как имя hello и любом другом контексте требуется.
- Создайте вызов зависимости и дождитесь его выполнения.
- Остановить операцию hello с `StopOperation` после его завершения.
- Выполните обработку исключений.

`StopOperation`только останавливает операцию hello, который был запущен. Если hello текущей операции не соответствует hello один требуется toostop, `StopOperation` не выполняет никаких действий. Такая ситуация может возникнуть, если запустить несколько операций в параллельном режиме в hello того же контекста выполнения:

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

Всегда необходимо убедиться в том, что выполнен вызов `StartOperation` и задача выполняется в своем собственном контексте.
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия

- Основы hello объекта [телеметрии корреляции](application-insights-correlation.md) в Application Insights.
- В разделе hello [модели данных](application-insights-data-model.md) для Application Insights типы и модели данных.
- Настраиваемый отчет [событий и метрик](app-insights-api-custom-events-metrics.md) tooApplication аналитики.
- Изучите стандартную [конфигурацию](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) коллекции свойств контекста.
- Проверьте hello [руководство пользователя System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee как корреляции телеметрии.
