---
title: "Мониторинг уровня приложения службы структуры aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о приложении журналы событий на уровне службы и использования и toomonitor диагностики Azure Service Fabric кластеров."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="2c88d-103">Создание событий и журналов на уровне приложений и служб</span><span class="sxs-lookup"><span data-stu-id="2c88d-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="2c88d-104">Инструментирование кода hello с помощью пользовательских событий</span><span class="sxs-lookup"><span data-stu-id="2c88d-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="2c88d-105">Инструментирование кода hello является основой hello для большинства других аспектов мониторинга служб.</span><span class="sxs-lookup"><span data-stu-id="2c88d-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="2c88d-106">Инструментирование является единственным способом hello, известно дает сбой, что toodiagnose, требующие toobe фиксированной.</span><span class="sxs-lookup"><span data-stu-id="2c88d-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="2c88d-107">Хотя технически возможных tooconnect отладчик tooa рабочей службе, не принято.</span><span class="sxs-lookup"><span data-stu-id="2c88d-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="2c88d-108">Поэтому вам нужны подробные данные инструментирования.</span><span class="sxs-lookup"><span data-stu-id="2c88d-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="2c88d-109">Некоторые решения выполняют инструментирование кода автоматически.</span><span class="sxs-lookup"><span data-stu-id="2c88d-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="2c88d-110">Они могут вполне успешно работать, но почти всегда требуется инструментирование вручную.</span><span class="sxs-lookup"><span data-stu-id="2c88d-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="2c88d-111">В конце hello должен иметь достаточно сведений, tooforensically отладки приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="2c88d-112">В этом документе описаны различные подходы tooinstrumenting кода, и если toochoose один подход на другое.</span><span class="sxs-lookup"><span data-stu-id="2c88d-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="2c88d-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="2c88d-113">EventSource</span></span>
<span data-ttu-id="2c88d-114">Если вы создаете решение Service Fabric из шаблона в Visual Studio, в нем создается класс **ServiceEventSource** или **ActorEventSource**, производный от **EventSource**.</span><span class="sxs-lookup"><span data-stu-id="2c88d-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="2c88d-115">При этом создается шаблон, в который вы можете добавлять события для конкретного приложения или службы.</span><span class="sxs-lookup"><span data-stu-id="2c88d-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="2c88d-116">Hello **EventSource** имя **должен** быть уникальным и должно быть заменено из строки шаблона по умолчанию hello MyCompany -&lt;решения&gt; - &lt; проект&gt;.</span><span class="sxs-lookup"><span data-stu-id="2c88d-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="2c88d-117">Наличие нескольких **EventSource** определений, использующих hello же причины имя ошибку во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2c88d-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="2c88d-118">У каждого определенного события должен быть уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="2c88d-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="2c88d-119">Если идентификатор не является уникальным, происходит сбой во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2c88d-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="2c88d-120">В некоторых организациях preassign диапазоны значений идентификаторов tooavoid конфликтов между отдельные группы разработчиков.</span><span class="sxs-lookup"><span data-stu-id="2c88d-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="2c88d-121">Дополнительные сведения см. в разделе [блога Вэнс элемента](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) или hello [документации MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="2c88d-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="2c88d-122">Использование структурированных событий EventSource</span><span class="sxs-lookup"><span data-stu-id="2c88d-122">Using structured EventSource events</span></span>

<span data-ttu-id="2c88d-123">Каждое из событий hello в примерах кода hello в этом разделе определяются для определенного случая, например, при регистрации типа службы.</span><span class="sxs-lookup"><span data-stu-id="2c88d-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="2c88d-124">Когда определить сообщения в варианте использования, данные можно упаковать с текстом hello ошибки hello и вы можете более легко выполнять поиск и фильтр на основе имен hello или значениям hello указанные свойства.</span><span class="sxs-lookup"><span data-stu-id="2c88d-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="2c88d-125">Структурирование вывод инструментария hello позволяет проще tooconsume, но требуется более сложная и время toodefine новое событие для каждого варианта использования.</span><span class="sxs-lookup"><span data-stu-id="2c88d-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="2c88d-126">Некоторые определения событий могут совместно использоваться hello всего приложения.</span><span class="sxs-lookup"><span data-stu-id="2c88d-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="2c88d-127">Например, запуск или остановка метода применяются многократно во многих службах в рамках приложения.</span><span class="sxs-lookup"><span data-stu-id="2c88d-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="2c88d-128">Специализированная служба, например система обработки заказов, может использовать событие **CreateOrder**, включающее собственное уникальное событие.</span><span class="sxs-lookup"><span data-stu-id="2c88d-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="2c88d-129">Такой подход будет порождать множество событий и может потребовать согласования идентификаторов между командами проектов.</span><span class="sxs-lookup"><span data-stu-id="2c88d-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="2c88d-130">Универсальное использование EventSource</span><span class="sxs-lookup"><span data-stu-id="2c88d-130">Using EventSource generically</span></span>

<span data-ttu-id="2c88d-131">Так как определение конкретных событий может вызвать трудности, многие разработчики определяют несколько событий с общим набором параметров, информация о которых обычно выводится в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="2c88d-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="2c88d-132">Большая часть аспект hello структурированные теряется, а он является более сложным toosearch и фильтровать результаты hello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="2c88d-133">При таком подходе определены несколько событий, которые обычно соответствуют уровни ведения журнала toohello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="2c88d-134">Следующий фрагмент кода Hello определяет отладки и сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="2c88d-134">hello following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

<span data-ttu-id="2c88d-135">Хорошие результаты может дать гибридный подход, сочетающий структурированное и универсальное инструментирование.</span><span class="sxs-lookup"><span data-stu-id="2c88d-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="2c88d-136">Структурированное инструментирование используется для уведомления об ошибках и метриках.</span><span class="sxs-lookup"><span data-stu-id="2c88d-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="2c88d-137">Универсальные события можно использовать для hello подробное ведение журнала, используемые инженеров по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="2c88d-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="2c88d-138">Ведение журнала ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="2c88d-138">ASP.NET Core logging</span></span>

<span data-ttu-id="2c88d-139">Важные toocarefully плана, как будет инструментировать код.</span><span class="sxs-lookup"><span data-stu-id="2c88d-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="2c88d-140">план правой инструментария Hello поможет вам избежать потенциально дестабилизации базы кода, а затем при необходимости tooreinstrument кода hello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="2c88d-141">риск tooreduce, вы можете выбрать библиотеку инструментирования как [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), который является частью Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2c88d-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="2c88d-142">ASP.NET Core имеет [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) интерфейс, который можно использовать с поставщиком hello по своему усмотрению, сводя к минимуму влияние hello на существующий код.</span><span class="sxs-lookup"><span data-stu-id="2c88d-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="2c88d-143">Можно использовать код hello в ASP.NET Core в Windows и Linux и в hello полной платформы .NET Framework, стандартизованные инструментирования кода.</span><span class="sxs-lookup"><span data-stu-id="2c88d-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="2c88d-144">Это подробнее рассматривается ниже:</span><span class="sxs-lookup"><span data-stu-id="2c88d-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="2c88d-145">Использование Microsoft.Extensions.Logging в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2c88d-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="2c88d-146">Добавьте hello Microsoft.Extensions.Logging NuGet пакета toohello проекта требуется tooinstrument.</span><span class="sxs-lookup"><span data-stu-id="2c88d-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="2c88d-147">Кроме того, добавьте все пакеты поставщика (пакета стороннего производителя, см. следующий пример hello).</span><span class="sxs-lookup"><span data-stu-id="2c88d-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="2c88d-148">Дополнительные сведения см. в разделе [Introduction to Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) (Вводные сведения о ведении журналов в ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="2c88d-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="2c88d-149">Добавить **с помощью** директив для файла службы tooyour Microsoft.Extensions.Logging.</span><span class="sxs-lookup"><span data-stu-id="2c88d-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="2c88d-150">Определите частную переменную в классе службы.</span><span class="sxs-lookup"><span data-stu-id="2c88d-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="2c88d-151">В конструкторе hello класса службы добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="2c88d-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="2c88d-152">Запустите инструментирование кода в методах.</span><span class="sxs-lookup"><span data-stu-id="2c88d-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="2c88d-153">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="2c88d-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="2c88d-154">Использование других поставщиков ведения журнала</span><span class="sxs-lookup"><span data-stu-id="2c88d-154">Using other logging providers</span></span>

<span data-ttu-id="2c88d-155">Некоторые сторонние поставщики использовать hello подход, описанный в hello предшествующий раздела, включая [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), и [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="2c88d-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="2c88d-156">Вы можете подключить любой из них к подсистеме ведения журналов ASP.NET Core или использовать их отдельно.</span><span class="sxs-lookup"><span data-stu-id="2c88d-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="2c88d-157">Serilog предоставляет возможность создавать дополнительные свойства для сообщений, отправляемых из средства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="2c88d-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="2c88d-158">Эта функция может быть полезно toooutput hello службы имя, тип и сведения о секции.</span><span class="sxs-lookup"><span data-stu-id="2c88d-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="2c88d-159">toouse эту возможность с помощью hello инфраструктуры ASP.NET Core, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2c88d-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="2c88d-160">Добавьте hello Serilog, Serilog.Extensions.Logging, и Serilog.Sinks.Observable NuGet пакеты toohello проекта.</span><span class="sxs-lookup"><span data-stu-id="2c88d-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="2c88d-161">Следующий пример hello необходимо также добавьте Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="2c88d-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="2c88d-162">Более правильный подход показан далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="2c88d-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="2c88d-163">В Serilog создайте экземпляр средства ведения журнала LoggerConfiguration и hello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="2c88d-164">Добавьте конструктор Serilog.ILogger аргумент toohello службы и передайте hello вновь созданные средства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="2c88d-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="2c88d-165">В конструктор служб hello, добавьте следующий код, создающий hello enrichers свойство для hello hello **ServiceTypeName**, **ServiceName**, **PartitionId**и  **InstanceId** свойства службы hello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="2c88d-166">Он также добавляет свойство enricher toohello фабрики ASP.NET Core ведения журнала, чтобы можно было использовать в коде Microsoft.Extensions.Logging.ILogger.</span><span class="sxs-lookup"><span data-stu-id="2c88d-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. <span data-ttu-id="2c88d-167">Hello инструментирования кода hello таким же, как при использовании ASP.NET Core без Serilog.</span><span class="sxs-lookup"><span data-stu-id="2c88d-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="2c88d-168">Рекомендуется не использовать статический hello Log.Logger с предшествующей пример hello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="2c88d-169">Service Fabric можно разместить несколько экземпляров hello же службы типа внутри одного процесса.</span><span class="sxs-lookup"><span data-stu-id="2c88d-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="2c88d-170">При использовании статического Log.Logger hello, hello последней записи enrichers hello свойства будут выведены значения для всех экземпляров, работающих под управлением.</span><span class="sxs-lookup"><span data-stu-id="2c88d-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="2c88d-171">Это — еще одна причина, почему hello _logger переменная является переменной закрытого члена класса службы hello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="2c88d-172">Кроме того необходимо внести hello _logger доступных toocommon код, который может использоваться между службами.</span><span class="sxs-lookup"><span data-stu-id="2c88d-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="2c88d-173">Выбор поставщика ведения журнала</span><span class="sxs-lookup"><span data-stu-id="2c88d-173">Choosing a logging provider</span></span>

<span data-ttu-id="2c88d-174">Если для вашего приложения требуется высокая производительность, рекомендуется остановить выбор на **EventSource**.</span><span class="sxs-lookup"><span data-stu-id="2c88d-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="2c88d-175">**EventSource** *обычно* использует меньше ресурсов и работает лучше, чем ASP.NET Core ведения журнала или любой из доступных решений сторонних hello.</span><span class="sxs-lookup"><span data-stu-id="2c88d-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="2c88d-176">Для многих служб это не проблема, но для высокопроизводительных служб **EventSource** будет наилучшим выбором.</span><span class="sxs-lookup"><span data-stu-id="2c88d-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="2c88d-177">Однако tooget структурированные ведения журнала, эти преимущества **EventSource** требует больших затрат из вашей командой разработчиков.</span><span class="sxs-lookup"><span data-stu-id="2c88d-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="2c88d-178">Если это возможно, выполните быстрый прототип несколько параметров ведения журнала и выберите hello, который лучше всего соответствует вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="2c88d-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c88d-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c88d-179">Next steps</span></span>

<span data-ttu-id="2c88d-180">После выбора вашей tooinstrument поставщика ведения журналов приложений и служб, журналы и события должны toobe статистическую обработку, прежде чем передавать их tooany платформа анализа.</span><span class="sxs-lookup"><span data-stu-id="2c88d-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="2c88d-181">Узнайте, как [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) и [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter понять hello рекомендуемые параметры.</span><span class="sxs-lookup"><span data-stu-id="2c88d-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
