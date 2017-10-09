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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="948cb-103">Отслеживание пользовательских операций с помощью пакета SDK Application Insights для .NET</span><span class="sxs-lookup"><span data-stu-id="948cb-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="948cb-104">Azure пакеты SDK Application Insights автоматически служб отслеживания входящих HTTP запрашивает и вызывает toodependent, например HTTP-запросы и запросы SQL.</span><span class="sxs-lookup"><span data-stu-id="948cb-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="948cb-105">Отслеживание и корреляцию запросов и зависимостей позволяют получить видимость всего приложения hello скорости реагирования и надежность на все микрослужбами, объединяющие этого приложения.</span><span class="sxs-lookup"><span data-stu-id="948cb-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="948cb-106">Существует класс шаблонов приложений, которые в принципе не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="948cb-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="948cb-107">Для надлежащего мониторинга таких шаблонов требуется инструментирование кода вручную.</span><span class="sxs-lookup"><span data-stu-id="948cb-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="948cb-108">В этой статье описывается несколько шаблонов, которые могут потребовать ручного инструментирования, например обработка пользовательской очереди сообщений и выполнение продолжительных фоновых задач.</span><span class="sxs-lookup"><span data-stu-id="948cb-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="948cb-109">Этот документ содержит инструкции по как tootrack пользовательских операций с hello пакет SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="948cb-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="948cb-110">Эта документация предназначена для:</span><span class="sxs-lookup"><span data-stu-id="948cb-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="948cb-111">Application Insights для .NET (базовый пакет SDK) версии 2.4 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="948cb-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="948cb-112">Application Insights для веб-приложений (выполнение ASP.NET) версии 2.4 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="948cb-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="948cb-113">Application Insights для ASP.NET Core версии 2.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="948cb-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="948cb-114">Обзор</span><span class="sxs-lookup"><span data-stu-id="948cb-114">Overview</span></span>
<span data-ttu-id="948cb-115">Операция — это логический элемент работы, выполняемый приложением.</span><span class="sxs-lookup"><span data-stu-id="948cb-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="948cb-116">У нее есть имя, время запуска, длительность, результат и контекст выполнения, такой как имя пользователя, свойства и результат.</span><span class="sxs-lookup"><span data-stu-id="948cb-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="948cb-117">Если операция A была инициирована операцией B, то операция B является родительской для A. У операции может быть только одна родительская операция, но множество дочерних операций.</span><span class="sxs-lookup"><span data-stu-id="948cb-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="948cb-118">Дополнительные сведения об операциях и корреляции телеметрии см. в разделе [Корреляция данных телеметрии в Application Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="948cb-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="948cb-119">Описывается операция hello в hello пакет SDK для .NET Application Insights, hello абстрактный класс [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) и его потомков [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) и [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="948cb-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="948cb-120">Отслеживание входящих операций</span><span class="sxs-lookup"><span data-stu-id="948cb-120">Incoming operations tracking</span></span> 
<span data-ttu-id="948cb-121">Hello web Application Insights SDK автоматически собирает HTTP-запросов для приложения ASP.NET, работающие в конвейере служб IIS и всех приложений ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="948cb-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="948cb-122">Существуют решения для других платформ, поддержка которых осуществляется силами сообщества разработчиков.</span><span class="sxs-lookup"><span data-stu-id="948cb-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="948cb-123">Тем не менее если приложение hello не поддерживается ни одним hello standard или общественный решений, можно инструментировать его вручную.</span><span class="sxs-lookup"><span data-stu-id="948cb-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="948cb-124">Другой пример, в котором требуется настраиваемое отслеживание — работник hello, получающий элементы из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="948cb-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="948cb-125">Для некоторых очередей hello вызывать tooadd сообщение, которое toothis очереди отслеживается в качестве зависимости.</span><span class="sxs-lookup"><span data-stu-id="948cb-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="948cb-126">Однако операции высокого уровня hello, описывающий обработку сообщения не собираются автоматически.</span><span class="sxs-lookup"><span data-stu-id="948cb-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="948cb-127">Давайте посмотрим, как можно отслеживать такие операции.</span><span class="sxs-lookup"><span data-stu-id="948cb-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="948cb-128">На высоком уровне задачу hello — toocreate `RequestTelemetry` и известные свойства.</span><span class="sxs-lookup"><span data-stu-id="948cb-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="948cb-129">По завершении операции hello отслеживать телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="948cb-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="948cb-130">Привет, следующий пример демонстрирует эту задачу.</span><span class="sxs-lookup"><span data-stu-id="948cb-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="948cb-131">HTTP-запрос в резидентном приложении Owin</span><span class="sxs-lookup"><span data-stu-id="948cb-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="948cb-132">В этом примере мы следовать hello [протокол HTTP для корреляции](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="948cb-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="948cb-133">Следует ожидать tooreceive заголовки, которые описаны.</span><span class="sxs-lookup"><span data-stu-id="948cb-133">You should expect tooreceive headers that are described there.</span></span>

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

<span data-ttu-id="948cb-134">Hello протокол HTTP для корреляции также объявляет hello `Correlation-Context` заголовок.</span><span class="sxs-lookup"><span data-stu-id="948cb-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="948cb-135">Однако здесь он опускается для простоты.</span><span class="sxs-lookup"><span data-stu-id="948cb-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="948cb-136">Инструментирование очереди</span><span class="sxs-lookup"><span data-stu-id="948cb-136">Queue instrumentation</span></span>
<span data-ttu-id="948cb-137">Для соединения по протоколу HTTP мы создали протокол toopass сведения о корреляции.</span><span class="sxs-lookup"><span data-stu-id="948cb-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="948cb-138">С помощью протоколов некоторые очереди можно передать дополнительные метаданные вместе с приветственное сообщение, а также с другими пользователями, которые вы не можете.</span><span class="sxs-lookup"><span data-stu-id="948cb-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="948cb-139">Очередь служебной шины</span><span class="sxs-lookup"><span data-stu-id="948cb-139">Service Bus queue</span></span>
<span data-ttu-id="948cb-140">С hello Azure [очереди Service Bus](../service-bus-messaging/index.md), можно передать контейнер свойств, а также приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="948cb-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="948cb-141">Мы используем toopass hello, идентификатор корреляции.</span><span class="sxs-lookup"><span data-stu-id="948cb-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="948cb-142">очередь Service Bus Hello использует протоколы на основе TCP.</span><span class="sxs-lookup"><span data-stu-id="948cb-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="948cb-143">Application Insights не предусматривает автоматическое отслеживание операций с очередями, поэтому мы отслеживаем их вручную.</span><span class="sxs-lookup"><span data-stu-id="948cb-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="948cb-144">Hello dequeue операция API принудительного типа, и мы tootrack его.</span><span class="sxs-lookup"><span data-stu-id="948cb-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="948cb-145">Постановка в очередь</span><span class="sxs-lookup"><span data-stu-id="948cb-145">Enqueue</span></span>

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

#### <a name="process"></a><span data-ttu-id="948cb-146">Process</span><span class="sxs-lookup"><span data-stu-id="948cb-146">Process</span></span>
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

### <a name="azure-storage-queue"></a><span data-ttu-id="948cb-147">Очередь службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="948cb-147">Azure Storage queue</span></span>
<span data-ttu-id="948cb-148">Следующий пример показывает как Hello tootrack hello [очереди службы хранилища Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) операции и согласовывать телеметрии между производителем hello, потребитель hello и хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="948cb-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="948cb-149">очередь хранилища Hello есть HTTP API.</span><span class="sxs-lookup"><span data-stu-id="948cb-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="948cb-150">Все вызовы toohello очереди отслеживаемых hello сборщика зависимостей аналитики приложений для HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="948cb-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="948cb-151">Убедитесь, что в `applicationInsights.config` есть `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="948cb-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="948cb-152">Если вас его нет, добавьте его программными средствами, как описано в [фильтрацию и предварительной обработки в Azure пакет SDK Application Insights hello](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="948cb-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="948cb-153">При настройке ApplicationInsights вручную убедитесь, что вы создали и инициализировали `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` так же, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="948cb-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="948cb-154">Также может потребоваться идентификатор операции toocorrelate hello Application Insights с идентификатором hello хранилища запросов.</span><span class="sxs-lookup"><span data-stu-id="948cb-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="948cb-155">Сведения о том, как tooset и get хранилища запросов клиента и код запроса сервера см. в разделе [мониторинг, диагностика и устранение неполадок хранилища Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="948cb-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="948cb-156">Постановка в очередь</span><span class="sxs-lookup"><span data-stu-id="948cb-156">Enqueue</span></span>
<span data-ttu-id="948cb-157">Поскольку очереди хранилища поддерживает hello HTTP API, все операции с очередью hello, автоматически отслеживаются контекстом Application Insights.</span><span class="sxs-lookup"><span data-stu-id="948cb-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="948cb-158">Во многих случаях этого инструментария должно быть достаточно.</span><span class="sxs-lookup"><span data-stu-id="948cb-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="948cb-159">Однако toocorrelate трассировки на стороне получателя hello и производитель трассировок, необходимо передать некоторый контекст для корреляции аналогично toohow мы это можно сделать в hello протокол HTTP для корреляции.</span><span class="sxs-lookup"><span data-stu-id="948cb-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="948cb-160">В этом примере мы отслеживания hello необязательно `Enqueue` операции.</span><span class="sxs-lookup"><span data-stu-id="948cb-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="948cb-161">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="948cb-161">You can:</span></span>

 - <span data-ttu-id="948cb-162">**Сопоставлять повторных попыток (если таковые имеются)**: все они имеют один общий родительский объект, hello `Enqueue` операции.</span><span class="sxs-lookup"><span data-stu-id="948cb-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="948cb-163">В противном случае они выполняется отслеживаются в качестве дочерних элементов hello входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="948cb-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="948cb-164">При наличии нескольких логических запросов toohello очереди, бывает сложно toofind какие вызов завершился повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="948cb-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="948cb-165">**Сопоставить журналы службы хранилища Azure (при необходимости)**: они сопоставляются с данными телеметрии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="948cb-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="948cb-166">Hello `Enqueue` операции является дочерним hello родительской операции (например, входящие HTTP-запроса).</span><span class="sxs-lookup"><span data-stu-id="948cb-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="948cb-167">вызов зависимостей Hello HTTP является потомком hello hello `Enqueue` операции и hello внучатый hello входящего запроса:</span><span class="sxs-lookup"><span data-stu-id="948cb-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

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

<span data-ttu-id="948cb-168">сообщает tooreduce hello объем телеметрии приложения или если вы не хотите tootrack hello `Enqueue` операции по другим причинам, используйте hello `Activity` API напрямую:</span><span class="sxs-lookup"><span data-stu-id="948cb-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="948cb-169">Создание (и запустить) новый `Activity` вместо запуска операции hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="948cb-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="948cb-170">Это сделать *не* требуется tooassign все свойства на его, за исключением имени операции hello.</span><span class="sxs-lookup"><span data-stu-id="948cb-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="948cb-171">Сериализовать `yourActivity.Id` в полезные данные сообщения hello вместо `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="948cb-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="948cb-172">Кроме того, можно использовать `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="948cb-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="948cb-173">Выведение из очереди</span><span class="sxs-lookup"><span data-stu-id="948cb-173">Dequeue</span></span>
<span data-ttu-id="948cb-174">Аналогичным образом слишком`Enqueue`, фактический запрос toohello хранилища очереди HTTP, автоматически отслеживаются контекстом Application Insights.</span><span class="sxs-lookup"><span data-stu-id="948cb-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="948cb-175">Здравствуйте, однако `Enqueue` предположительно выполняется в контексте родительского hello, например контекст входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="948cb-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="948cb-176">Пакеты SDK Application Insights автоматически сопоставлять такая операция (и его часть HTTP) с родительским запросом hello и данные других телеметрии, отправленные в hello же области.</span><span class="sxs-lookup"><span data-stu-id="948cb-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="948cb-177">Hello `Dequeue` операция является непростой задачей.</span><span class="sxs-lookup"><span data-stu-id="948cb-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="948cb-178">пакет SDK для Application Insights Hello автоматически отслеживает HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="948cb-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="948cb-179">Тем не менее он не знает hello корреляции контекста, пока не анализируется приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="948cb-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="948cb-180">Это не возможные toocorrelate hello HTTP запроса tooget приветственных сообщений hello остальные телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="948cb-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="948cb-181">Во многих случаях бывает полезным toocorrelate hello HTTP запроса и для других трассировок, а также toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="948cb-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="948cb-182">Hello следующем примере показано, как toodo его:</span><span class="sxs-lookup"><span data-stu-id="948cb-182">hello following example demonstrates how toodo it:</span></span>

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

#### <a name="process"></a><span data-ttu-id="948cb-183">Process</span><span class="sxs-lookup"><span data-stu-id="948cb-183">Process</span></span>

<span data-ttu-id="948cb-184">В следующем примере hello, мы трассировки входящего сообщения в определенном аналогично toohow мы отслеживать входящие HTTP запроса:</span><span class="sxs-lookup"><span data-stu-id="948cb-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

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

<span data-ttu-id="948cb-185">Другие операции очереди также можно инструментировать.</span><span class="sxs-lookup"><span data-stu-id="948cb-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="948cb-186">Операцию заглядывания следует инструментировать так же, как операцию выведения из очереди.</span><span class="sxs-lookup"><span data-stu-id="948cb-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="948cb-187">Инструментировать операции управления очередью необязательно.</span><span class="sxs-lookup"><span data-stu-id="948cb-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="948cb-188">Application Insights отслеживает такие операции, как HTTP, и в большинстве случаев этого достаточно.</span><span class="sxs-lookup"><span data-stu-id="948cb-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="948cb-189">При инструментировании удаления сообщений, убедитесь, что операции hello задания идентификаторов (корреляция).</span><span class="sxs-lookup"><span data-stu-id="948cb-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="948cb-190">Кроме того, можно использовать hello `Activity` API.</span><span class="sxs-lookup"><span data-stu-id="948cb-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="948cb-191">Затем не требуется tooset операции идентификаторы для элементов телеметрии hello, так как Application Insights делает это для вас:</span><span class="sxs-lookup"><span data-stu-id="948cb-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="948cb-192">Создайте новый `Activity` после элемента из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="948cb-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="948cb-193">Используйте `Activity.SetParentId(message.ParentId)` toocorrelate потребитель и производитель журналы.</span><span class="sxs-lookup"><span data-stu-id="948cb-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="948cb-194">Запуск hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="948cb-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="948cb-195">Отслеживайте операции выведения из очереди, обработки и удаления с помощью вспомогательных методов `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="948cb-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="948cb-196">Сделать это из hello же асинхронной управления потоком (контекст выполнения).</span><span class="sxs-lookup"><span data-stu-id="948cb-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="948cb-197">Таким образом они будут сопоставлены должным образом.</span><span class="sxs-lookup"><span data-stu-id="948cb-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="948cb-198">Остановка hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="948cb-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="948cb-199">Используйте `Start/StopOperation` или вручную вызовите телеметрию `Track`.</span><span class="sxs-lookup"><span data-stu-id="948cb-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="948cb-200">Пакетная обработка</span><span class="sxs-lookup"><span data-stu-id="948cb-200">Batch processing</span></span>
<span data-ttu-id="948cb-201">Некоторые очереди поддерживают вывод из очереди нескольких сообщений с помощью одного запроса.</span><span class="sxs-lookup"><span data-stu-id="948cb-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="948cb-202">Обработка таких сообщений предположительно независим и принадлежит toohello различных логических операций.</span><span class="sxs-lookup"><span data-stu-id="948cb-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="948cb-203">В этом случае это не hello возможных toocorrelate `Dequeue` обработки сообщений tooparticular операции.</span><span class="sxs-lookup"><span data-stu-id="948cb-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="948cb-204">Обработка каждого сообщения должна выполняться в собственном асинхронном потоке управления.</span><span class="sxs-lookup"><span data-stu-id="948cb-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="948cb-205">Дополнительные сведения см. в разделе hello [исходящие зависимости отслеживания](#outgoing-dependencies-tracking) раздела.</span><span class="sxs-lookup"><span data-stu-id="948cb-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="948cb-206">Длительные фоновые задачи</span><span class="sxs-lookup"><span data-stu-id="948cb-206">Long-running background tasks</span></span>
<span data-ttu-id="948cb-207">Некоторые приложения запускают длительные операции, которые могут быть вызваны запросами пользователей.</span><span class="sxs-lookup"><span data-stu-id="948cb-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="948cb-208">С точки зрения трассировка и инструментирование hello не отличается от инструментария запроса или зависимостей:</span><span class="sxs-lookup"><span data-stu-id="948cb-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

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

<span data-ttu-id="948cb-209">В этом примере мы используем `telemetryClient.StartOperation` toocreate `RequestTelemetry` и заполнения hello корреляции контекста.</span><span class="sxs-lookup"><span data-stu-id="948cb-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="948cb-210">Предположим, что у вас есть родительского операцию, которая была создана с входящими запросами, которые запланированную операцию hello.</span><span class="sxs-lookup"><span data-stu-id="948cb-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="948cb-211">При условии, что `BackgroundTask` запускается в Здравствуйте же асинхронного потока управления как входящий запрос, он связан с этим операция родительского.</span><span class="sxs-lookup"><span data-stu-id="948cb-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="948cb-212">`BackgroundTask`и все элементы вложенного телеметрии автоматически связаны с запросом hello, вызвавшей ее, даже в том случае, после завершения запроса hello.</span><span class="sxs-lookup"><span data-stu-id="948cb-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="948cb-213">При запуске задачу hello из hello фоновый поток, который не имеет любой операции (`Activity`) связанные с ней `BackgroundTask` не имеет любого родительского элемента.</span><span class="sxs-lookup"><span data-stu-id="948cb-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="948cb-214">Тем не менее у нее могут быть вложенные операции.</span><span class="sxs-lookup"><span data-stu-id="948cb-214">However, it can have nested operations.</span></span> <span data-ttu-id="948cb-215">Все элементы телеметрии, полученные от задачу hello становятся коррелированные toohello `RequestTelemetry` в `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="948cb-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="948cb-216">Отслеживание исходящих зависимостей</span><span class="sxs-lookup"><span data-stu-id="948cb-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="948cb-217">Можно отслеживать собственный тип зависимостей или операцию, не поддерживаемую Application Insights.</span><span class="sxs-lookup"><span data-stu-id="948cb-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="948cb-218">Hello `Enqueue` метод в очередь Service Bus hello или очередь hello хранилища можно использовать в качестве примеров таких настраиваемое отслеживание.</span><span class="sxs-lookup"><span data-stu-id="948cb-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="948cb-219">общий подход Hello для отслеживания пользовательских зависимостей является:</span><span class="sxs-lookup"><span data-stu-id="948cb-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="948cb-220">Вызовите hello `TelemetryClient.StartOperation` метод (расширения), который заполняет hello `DependencyTelemetry` свойства, необходимые для корреляции и некоторые другие свойства (время начала метка, длительность).</span><span class="sxs-lookup"><span data-stu-id="948cb-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="948cb-221">Настроить другие настраиваемые свойства hello `DependencyTelemetry`, такие как имя hello и любом другом контексте требуется.</span><span class="sxs-lookup"><span data-stu-id="948cb-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="948cb-222">Создайте вызов зависимости и дождитесь его выполнения.</span><span class="sxs-lookup"><span data-stu-id="948cb-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="948cb-223">Остановить операцию hello с `StopOperation` после его завершения.</span><span class="sxs-lookup"><span data-stu-id="948cb-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="948cb-224">Выполните обработку исключений.</span><span class="sxs-lookup"><span data-stu-id="948cb-224">Handle exceptions.</span></span>

<span data-ttu-id="948cb-225">`StopOperation`только останавливает операцию hello, который был запущен.</span><span class="sxs-lookup"><span data-stu-id="948cb-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="948cb-226">Если hello текущей операции не соответствует hello один требуется toostop, `StopOperation` не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="948cb-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="948cb-227">Такая ситуация может возникнуть, если запустить несколько операций в параллельном режиме в hello того же контекста выполнения:</span><span class="sxs-lookup"><span data-stu-id="948cb-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

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

<span data-ttu-id="948cb-228">Всегда необходимо убедиться в том, что выполнен вызов `StartOperation` и задача выполняется в своем собственном контексте.</span><span class="sxs-lookup"><span data-stu-id="948cb-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="948cb-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="948cb-229">Next steps</span></span>

- <span data-ttu-id="948cb-230">Основы hello объекта [телеметрии корреляции](application-insights-correlation.md) в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="948cb-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="948cb-231">В разделе hello [модели данных](application-insights-data-model.md) для Application Insights типы и модели данных.</span><span class="sxs-lookup"><span data-stu-id="948cb-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="948cb-232">Настраиваемый отчет [событий и метрик](app-insights-api-custom-events-metrics.md) tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="948cb-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="948cb-233">Изучите стандартную [конфигурацию](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) коллекции свойств контекста.</span><span class="sxs-lookup"><span data-stu-id="948cb-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="948cb-234">Проверьте hello [руководство пользователя System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee как корреляции телеметрии.</span><span class="sxs-lookup"><span data-stu-id="948cb-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
