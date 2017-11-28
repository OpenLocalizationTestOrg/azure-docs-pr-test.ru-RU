---
title: "Отслеживание пользовательских операций с помощью пакета SDK Azure Application Insights для .NET | Документы Майкрософт"
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
ms.openlocfilehash: b31d38fe2f7060597956a1ee9c66f43ce39d7240
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="f6b6b-103">Отслеживание пользовательских операций с помощью пакета SDK Application Insights для .NET</span><span class="sxs-lookup"><span data-stu-id="f6b6b-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="f6b6b-104">Пакеты SDK Azure Application Insights автоматически отслеживают входящие HTTP-запросы и вызовы зависимых служб, в том числе HTTP-запросы и SQL-запросы.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls to dependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="f6b6b-105">Отслеживание и корреляция запросов и зависимостей позволяет контролировать скорость реагирования приложения в целом, а также надежность всех микрослужб, составляющих это приложение.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-105">Tracking and correlation of requests and dependencies give you visibility into the whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="f6b6b-106">Существует класс шаблонов приложений, которые в принципе не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="f6b6b-107">Для надлежащего мониторинга таких шаблонов требуется инструментирование кода вручную.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="f6b6b-108">В этой статье описывается несколько шаблонов, которые могут потребовать ручного инструментирования, например обработка пользовательской очереди сообщений и выполнение продолжительных фоновых задач.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="f6b6b-109">В данном документе представлены инструкции по организации отслеживания пользовательских операций с помощью пакета SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-109">This document provides guidance on how to track custom operations with the Application Insights SDK.</span></span> <span data-ttu-id="f6b6b-110">Эта документация предназначена для:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="f6b6b-111">Application Insights для .NET (базовый пакет SDK) версии 2.4 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="f6b6b-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="f6b6b-112">Application Insights для веб-приложений (выполнение ASP.NET) версии 2.4 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="f6b6b-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="f6b6b-113">Application Insights для ASP.NET Core версии 2.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="f6b6b-114">Обзор</span><span class="sxs-lookup"><span data-stu-id="f6b6b-114">Overview</span></span>
<span data-ttu-id="f6b6b-115">Операция — это логический элемент работы, выполняемый приложением.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="f6b6b-116">У нее есть имя, время запуска, длительность, результат и контекст выполнения, такой как имя пользователя, свойства и результат.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="f6b6b-117">Если операция A была инициирована операцией B, то операция B является родительской для A. У операции может быть только одна родительская операция, но множество дочерних операций.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="f6b6b-118">Дополнительные сведения об операциях и корреляции телеметрии см. в разделе [Корреляция данных телеметрии в Application Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="f6b6b-119">В пакете SDK Application Insights для .NET операция описывается абстрактным классом [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) и его потомками [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) и [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-119">In the Application Insights .NET SDK, the operation is described by the abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="f6b6b-120">Отслеживание входящих операций</span><span class="sxs-lookup"><span data-stu-id="f6b6b-120">Incoming operations tracking</span></span> 
<span data-ttu-id="f6b6b-121">Пакет SDK Application Insights автоматически собирает HTTP-запросы для приложений ASP.NET, которые выполняются в конвейере служб IIS, и всех приложений ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-121">The Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="f6b6b-122">Существуют решения для других платформ, поддержка которых осуществляется силами сообщества разработчиков.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="f6b6b-123">Однако если приложение не поддерживается ни одним стандартным решением или решением сообщества разработчиков, его можно инструментировать вручную.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-123">However, if the application isn't supported by any of the standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="f6b6b-124">Другой пример, в котором требуется настраиваемое отслеживание, — это рабочая роль, которая получает элементы из очереди.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-124">Another example that requires custom tracking is the worker that receives items from the queue.</span></span> <span data-ttu-id="f6b6b-125">Для некоторых очередей вызов для добавления сообщения в эту очередь отслеживается как зависимость.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-125">For some queues, the call to add a message to this queue is tracked as a dependency.</span></span> <span data-ttu-id="f6b6b-126">Однако операции высокого уровня, описывающие обработку сообщения, не собираются автоматически.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-126">However, the high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="f6b6b-127">Давайте посмотрим, как можно отслеживать такие операции.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="f6b6b-128">На высоком уровне задачей является создание `RequestTelemetry` и настройка известных свойств.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-128">On a high level, the task is to create `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="f6b6b-129">После завершения этой операции можно отслеживать данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-129">After the operation is finished, you track the telemetry.</span></span> <span data-ttu-id="f6b6b-130">Эта задача показана в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-130">The following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="f6b6b-131">HTTP-запрос в резидентном приложении Owin</span><span class="sxs-lookup"><span data-stu-id="f6b6b-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="f6b6b-132">В этом примере мы следуем [протоколу HTTP для корреляции](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-132">In this example, we follow the [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="f6b6b-133">Следует ожидать заголовки, которые в нем описаны.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-133">You should expect to receive headers that are described there.</span></span>

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

        // If there is a Request-Id received from the upstream service, set the telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process the request.
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

            // Now it's time to stop the operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns the root ID from the '|' to the first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="f6b6b-134">Протокол HTTP для корреляции также объявляет заголовок `Correlation-Context`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-134">The HTTP Protocol for Correlation also declares the `Correlation-Context` header.</span></span> <span data-ttu-id="f6b6b-135">Однако здесь он опускается для простоты.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="f6b6b-136">Инструментирование очереди</span><span class="sxs-lookup"><span data-stu-id="f6b6b-136">Queue instrumentation</span></span>
<span data-ttu-id="f6b6b-137">Для HTTP-подключений мы создали протокол для передачи данных корреляции.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-137">For HTTP communication, we've created a protocol to pass correlation details.</span></span> <span data-ttu-id="f6b6b-138">Одни протоколы очереди позволяют передавать дополнительные метаданные вместе с сообщением, а другие — нет.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-138">With some queues' protocols, you can pass additional metadata along with the message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="f6b6b-139">Очередь служебной шины</span><span class="sxs-lookup"><span data-stu-id="f6b6b-139">Service Bus queue</span></span>
<span data-ttu-id="f6b6b-140">С помощью [очереди служебной шины](../service-bus-messaging/index.md) Azure вместе с сообщением можно передать контейнер свойств.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-140">With the Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with the message.</span></span> <span data-ttu-id="f6b6b-141">Мы используем его для передачи идентификатора корреляции.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-141">We use it to pass the correlation ID.</span></span>

<span data-ttu-id="f6b6b-142">Очередь служебной шины использует протоколы на основе TCP.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-142">The Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="f6b6b-143">Application Insights не предусматривает автоматическое отслеживание операций с очередями, поэтому мы отслеживаем их вручную.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="f6b6b-144">Операция вывода из очереди представляет собой API отправки и не поддерживает отслеживание.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-144">The dequeue operation is a push-style API, and we're unable to track it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="f6b6b-145">Постановка в очередь</span><span class="sxs-lookup"><span data-stu-id="f6b6b-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes the telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows the property bag to pass along with the message.
    // We will use them to pass our correlation identifiers (and other context)
    // to the consumer.
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

#### <a name="process"></a><span data-ttu-id="f6b6b-146">Process</span><span class="sxs-lookup"><span data-stu-id="f6b6b-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After the message is taken from the queue, create RequestTelemetry to track its processing.
    // It might also make sense to get the name from the message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
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

### <a name="azure-storage-queue"></a><span data-ttu-id="f6b6b-147">Очередь службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="f6b6b-147">Azure Storage queue</span></span>
<span data-ttu-id="f6b6b-148">В следующем примере показано, как отслеживать операции [очереди службы хранилища Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) и сопоставлять данные телеметрии производителя, потребителя и службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-148">The following example shows how to track the [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between the producer, the consumer, and Azure Storage.</span></span> 

<span data-ttu-id="f6b6b-149">Очередь службы хранилища использует API HTTP.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-149">The Storage queue has an HTTP API.</span></span> <span data-ttu-id="f6b6b-150">Все вызовы, отправляемые к очереди, отслеживаются сборщиком зависимостей Application Insights на наличие HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-150">All calls to the queue are tracked by the Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="f6b6b-151">Убедитесь, что в `applicationInsights.config` есть `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="f6b6b-152">В противном случае добавьте его программно, как описано в разделе [Фильтрация и предварительная обработка данных телеметрии в пакете SDK для Application Insights](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in the Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="f6b6b-153">При настройке ApplicationInsights вручную убедитесь, что вы создали и инициализировали `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` так же, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection to some domains by adding it to the excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on the Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget to dispose of the module during application shutdown.
```

<span data-ttu-id="f6b6b-154">Кроме того, может потребоваться сопоставить идентификатор операции Application Insights с идентификатором запроса службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-154">You also might want to correlate the Application Insights operation ID with the Storage request ID.</span></span> <span data-ttu-id="f6b6b-155">Сведения о том, как настроить и получить идентификатор клиента для запроса службы хранилища и идентификатор запроса сервера, см. в разделе [Мониторинг, диагностика и устранение неполадок с хранилищем Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-155">For information on how to set and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="f6b6b-156">Постановка в очередь</span><span class="sxs-lookup"><span data-stu-id="f6b6b-156">Enqueue</span></span>
<span data-ttu-id="f6b6b-157">Так как очереди службы хранилища Azure поддерживают API HTTP, все операции с очередью автоматически отслеживаются Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-157">Because Storage queues support the HTTP API, all operations with the queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="f6b6b-158">Во многих случаях этого инструментария должно быть достаточно.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="f6b6b-159">Однако для сопоставления трассировок на стороне потребителя с трассировками производителя необходимо передать некоторый контекст корреляции, точно так же, как мы сделали это для протокола HTTP для корреляции.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-159">However, to correlate traces on the consumer side with producer traces, you must pass some correlation context similarly to how we do it in the HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="f6b6b-160">В этом примере мы отслеживаем необязательную операцию `Enqueue`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-160">In this example, we track the optional `Enqueue` operation.</span></span> <span data-ttu-id="f6b6b-161">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="f6b6b-161">You can:</span></span>

 - <span data-ttu-id="f6b6b-162">**Сопоставить повторные попытки (если таковые имеются)**: все они имеют одну общую родительскую операцию, `Enqueue`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-162">**Correlate retries (if any)**: They all have one common parent that's the `Enqueue` operation.</span></span> <span data-ttu-id="f6b6b-163">В противном случае они отслеживаются как дочерние элементы входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-163">Otherwise, they're tracked as children of the incoming request.</span></span> <span data-ttu-id="f6b6b-164">В случае нескольких логических запросов к очереди может оказаться затруднительным определить, какой вызов совершался повторно.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-164">If there are multiple logical requests to the queue, it might be difficult to find which call resulted in retries.</span></span>
 - <span data-ttu-id="f6b6b-165">**Сопоставить журналы службы хранилища Azure (при необходимости)**: они сопоставляются с данными телеметрии Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="f6b6b-166">Операция `Enqueue` является дочерним элементом родительской операции (например, входящего HTTP-запроса).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-166">The `Enqueue` operation is the child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="f6b6b-167">Вызовов зависимости HTTP является дочерним элементом операции `Enqueue` и внучатым элементом входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-167">The HTTP dependency call is the child of the `Enqueue` operation and the grandchild of the incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose to pass payload serialized to JSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message to process'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id to the OperationContext to correlate Storage logs and Application Insights telemetry.
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

<span data-ttu-id="f6b6b-168">Чтобы сократить объем данных телеметрии, передаваемой приложением, или если не требуется отслеживать операцию `Enqueue` по иным причинам, можно напрямую использовать API `Activity`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-168">To reduce the amount of telemetry your application reports or if you don't want to track the `Enqueue` operation for other reasons, use the `Activity` API directly:</span></span>

- <span data-ttu-id="f6b6b-169">Создайте (и запустите) новый элемент `Activity` вместо запуска операции Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-169">Create (and start) a new `Activity` instead of starting the Application Insights operation.</span></span> <span data-ttu-id="f6b6b-170">*Не* нужно назначать в нем какие-либо свойства, за исключением имени операции.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-170">You do *not* need to assign any properties on it except the operation name.</span></span>
- <span data-ttu-id="f6b6b-171">Сериализируйте `yourActivity.Id` в полезные данные сообщения вместо `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-171">Serialize `yourActivity.Id` into the message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="f6b6b-172">Кроме того, можно использовать `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="f6b6b-173">Выведение из очереди</span><span class="sxs-lookup"><span data-stu-id="f6b6b-173">Dequeue</span></span>
<span data-ttu-id="f6b6b-174">Так же, как и `Enqueue`, фактические HTTP-запросы к очереди службы хранилища Azure автоматически отслеживаются Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-174">Similarly to `Enqueue`, an actual HTTP request to the Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="f6b6b-175">Однако операция `Enqueue` предположительно выполняется в контексте родительского элемента, такого как контекст входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-175">However, the `Enqueue` operation presumably happens in the parent context, such as an incoming request context.</span></span> <span data-ttu-id="f6b6b-176">Пакеты SDK Application Insights автоматически сопоставляют такие операции (и их части HTTP) с родительским запросом и другими данными телеметрии, переданными в той же области.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with the parent request and other telemetry reported in the same scope.</span></span>

<span data-ttu-id="f6b6b-177">С операцией `Dequeue` все не так просто.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-177">The `Dequeue` operation is tricky.</span></span> <span data-ttu-id="f6b6b-178">Пакет SDK Application Insights автоматически отслеживает HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-178">The Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="f6b6b-179">Тем не менее ему не известен контекст корреляции, пока выполняется анализ сообщения.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-179">However, it doesn't know the correlation context until the message is parsed.</span></span> <span data-ttu-id="f6b6b-180">Невозможно сопоставить HTTP-запрос для получения сообщения с остальной частью данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-180">It's not possible to correlate the HTTP request to get the message with the rest of the telemetry.</span></span>

<span data-ttu-id="f6b6b-181">Зачастую может быть удобно сопоставить HTTP-запрос с очередью и другими трассировками.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-181">In many cases, it might be useful to correlate the HTTP request to the queue with other traces as well.</span></span> <span data-ttu-id="f6b6b-182">В следующем примере показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-182">The following example demonstrates how to do it:</span></span>

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

            // If there is a message, we want to correlate the Dequeue operation with processing.
            // However, we will only know what correlation ID to use after we get it from the message,
            // so we will report telemetry after we know the IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete the message.
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

#### <a name="process"></a><span data-ttu-id="f6b6b-183">Process</span><span class="sxs-lookup"><span data-stu-id="f6b6b-183">Process</span></span>

<span data-ttu-id="f6b6b-184">В следующем примере мы отслеживаем входящее сообщение таким же образом, как мы выполняли трассировку входящего HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-184">In the following example, we trace an incoming message in a manner similarly to how we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After the message is dequeued from the queue, create RequestTelemetry to track its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense to get the name from the message.
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

<span data-ttu-id="f6b6b-185">Другие операции очереди также можно инструментировать.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="f6b6b-186">Операцию заглядывания следует инструментировать так же, как операцию выведения из очереди.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="f6b6b-187">Инструментировать операции управления очередью необязательно.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="f6b6b-188">Application Insights отслеживает такие операции, как HTTP, и в большинстве случаев этого достаточно.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="f6b6b-189">При инструментировании удаления сообщения убедитесь в том, что заданы идентификаторы операции (корреляция).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-189">When you instrument message deletion, make sure you set the operation (correlation) identifiers.</span></span> <span data-ttu-id="f6b6b-190">Кроме того, можно использовать API `Activity`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-190">Alternatively, you can use the `Activity` API.</span></span> <span data-ttu-id="f6b6b-191">Это не требует задания идентификаторов операций для элементов телеметрии, так как Application Insights делает это автоматически.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-191">Then you don't need to set operation identifiers on the telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="f6b6b-192">Получив элемент из очереди, создайте `Activity`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-192">Create a new `Activity` after you've got an item from the queue.</span></span>
- <span data-ttu-id="f6b6b-193">Используйте `Activity.SetParentId(message.ParentId)` для сопоставления журналов потребителя и производителя.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-193">Use `Activity.SetParentId(message.ParentId)` to correlate consumer and producer logs.</span></span>
- <span data-ttu-id="f6b6b-194">Запустите `Activity`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-194">Start the `Activity`.</span></span>
- <span data-ttu-id="f6b6b-195">Отслеживайте операции выведения из очереди, обработки и удаления с помощью вспомогательных методов `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="f6b6b-196">Это необходимо выполнить из одного и того же асинхронного потока управления (контекста выполнения).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-196">Do it from the same asynchronous control flow (execution context).</span></span> <span data-ttu-id="f6b6b-197">Таким образом они будут сопоставлены должным образом.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="f6b6b-198">Остановите `Activity`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-198">Stop the `Activity`.</span></span>
- <span data-ttu-id="f6b6b-199">Используйте `Start/StopOperation` или вручную вызовите телеметрию `Track`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="f6b6b-200">Пакетная обработка</span><span class="sxs-lookup"><span data-stu-id="f6b6b-200">Batch processing</span></span>
<span data-ttu-id="f6b6b-201">Некоторые очереди поддерживают вывод из очереди нескольких сообщений с помощью одного запроса.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="f6b6b-202">Обработка таких сообщений предположительно является независимой и относится к разным логическим операциям.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-202">Processing such messages is presumably independent and belongs to the different logical operations.</span></span> <span data-ttu-id="f6b6b-203">В этом случае невозможно сопоставить операцию `Dequeue` с обработкой конкретного сообщения.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-203">In this case, it's not possible to correlate the `Dequeue` operation to particular message processing.</span></span>

<span data-ttu-id="f6b6b-204">Обработка каждого сообщения должна выполняться в собственном асинхронном потоке управления.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="f6b6b-205">Дополнительные сведения см. в разделе [Отслеживание исходящих зависимостей](#outgoing-dependencies-tracking).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-205">For more information, see the [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="f6b6b-206">Длительные фоновые задачи</span><span class="sxs-lookup"><span data-stu-id="f6b6b-206">Long-running background tasks</span></span>
<span data-ttu-id="f6b6b-207">Некоторые приложения запускают длительные операции, которые могут быть вызваны запросами пользователей.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="f6b6b-208">С точки зрения трассировки и инструментирования это ничем не отличается от инструментирования запроса или зависимости.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-208">From the tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

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
            // Process the task.
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

<span data-ttu-id="f6b6b-209">В этом примере мы используем `telemetryClient.StartOperation` для создания `RequestTelemetry` и заполнения контекста корреляции.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-209">In this example, we use `telemetryClient.StartOperation` to create `RequestTelemetry` and fill the correlation context.</span></span> <span data-ttu-id="f6b6b-210">Предположим, имеется родительская операция, которая была создана входящими запросами, запланировавшими эту операцию.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-210">Let's say you have a parent operation that was created by incoming requests that scheduled the operation.</span></span> <span data-ttu-id="f6b6b-211">Так как `BackgroundTask` запускается в том же асинхронном потоке управления, что и входящий запрос, он сопоставляется с этой родительской операцией.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-211">As long as `BackgroundTask` starts in the same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="f6b6b-212">`BackgroundTask` и все вложенные элементы телеметрии автоматически сопоставляются с запросом, вызвавшим ее, даже после завершения запроса.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-212">`BackgroundTask` and all nested telemetry items are automatically correlated with the request that caused it, even after the request ends.</span></span>

<span data-ttu-id="f6b6b-213">Если задача запущена из фонового потока, с которым не связана ни одна операция (`Activity`), у задачи `BackgroundTask` отсутствуют какие-либо родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-213">When the task starts from the background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="f6b6b-214">Тем не менее у нее могут быть вложенные операции.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-214">However, it can have nested operations.</span></span> <span data-ttu-id="f6b6b-215">Все элементы телеметрии, полученные от этой задачи, сопоставляются с элементом `RequestTelemetry`, созданным в `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-215">All telemetry items reported from the task are correlated to the `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="f6b6b-216">Отслеживание исходящих зависимостей</span><span class="sxs-lookup"><span data-stu-id="f6b6b-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="f6b6b-217">Можно отслеживать собственный тип зависимостей или операцию, не поддерживаемую Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="f6b6b-218">Примером такого настраиваемого отслеживания может служить метод `Enqueue` в очереди служебной шины или очереди службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-218">The `Enqueue` method in the Service Bus queue or the Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="f6b6b-219">Общий подход к настраиваемому отслеживанию зависимостей заключается в следующем.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-219">The general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="f6b6b-220">Вызовите метод `TelemetryClient.StartOperation` (расширение), который заполняет свойства `DependencyTelemetry`, необходимые для корреляции, и ряд других свойств (метка времени запуска, длительность).</span><span class="sxs-lookup"><span data-stu-id="f6b6b-220">Call the `TelemetryClient.StartOperation` (extension) method that fills the `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="f6b6b-221">Задайте другие настраиваемые свойства `DependencyTelemetry`, например имя и любой контекст, который требуется.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-221">Set other custom properties on the `DependencyTelemetry`, such as the name and any other context you need.</span></span>
- <span data-ttu-id="f6b6b-222">Создайте вызов зависимости и дождитесь его выполнения.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="f6b6b-223">Остановите операцию после завершения с помощью `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-223">Stop the operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="f6b6b-224">Выполните обработку исключений.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-224">Handle exceptions.</span></span>

<span data-ttu-id="f6b6b-225">`StopOperation` останавливает только операцию, которая была запущена.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-225">`StopOperation` only stops the operation that was started.</span></span> <span data-ttu-id="f6b6b-226">Если текущая выполняемая операция не совпадает с операцией, которую нужно остановить, то `StopOperation` не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-226">If the current running operation doesn't match the one you want to stop, `StopOperation` does nothing.</span></span> <span data-ttu-id="f6b6b-227">Это может произойти в случае, если в одном и том же контексте выполнения параллельно запущено несколько операций.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-227">This situation might happen if you start multiple operations in parallel in the same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for the first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="f6b6b-228">Всегда необходимо убедиться в том, что выполнен вызов `StartOperation` и задача выполняется в своем собственном контексте.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="f6b6b-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6b6b-229">Next steps</span></span>

- <span data-ttu-id="f6b6b-230">Изучите основы [корреляции данных телеметрии](application-insights-correlation.md) в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-230">Learn the basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="f6b6b-231">В [этой статье](application-insights-data-model.md) представлены типы данных и модель данных для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-231">See the [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="f6b6b-232">Передача настраиваемых [событий и метрик](app-insights-api-custom-events-metrics.md) в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) to Application Insights.</span></span>
- <span data-ttu-id="f6b6b-233">Изучите стандартную [конфигурацию](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) коллекции свойств контекста.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="f6b6b-234">Ознакомьтесь с [руководством пользователя по System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md), чтобы узнать, как осуществляется корреляция данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-234">Check the [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) to see how we correlate telemetry.</span></span>
