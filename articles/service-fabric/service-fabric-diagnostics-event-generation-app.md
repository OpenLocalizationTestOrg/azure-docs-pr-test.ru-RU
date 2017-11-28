---
title: "Мониторинг на уровне приложений службы Azure Service Fabric | Документы Майкрософт"
description: "Сведения о журналах и событиях на уровне приложений и служб, используемых для мониторинга и диагностики кластеров Azure Service Fabric."
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
ms.openlocfilehash: 3c472904641108b7383cd0f1416c47460f8de11a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="9cdf5-103">Создание событий и журналов на уровне приложений и служб</span><span class="sxs-lookup"><span data-stu-id="9cdf5-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-the-code-with-custom-events"></a><span data-ttu-id="9cdf5-104">Инструментирование кода с помощью пользовательских событий</span><span class="sxs-lookup"><span data-stu-id="9cdf5-104">Instrumenting the code with custom events</span></span>

<span data-ttu-id="9cdf5-105">В основе большинства других аспектов мониторинга служб лежит инструментирование кода.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-105">Instrumenting the code is the basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="9cdf5-106">Инструментирование — это единственный способ выяснить, что какой-то компонент работает неправильно, и диагностировать проблему для ее дальнейшего исправления.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-106">Instrumentation is the only way you can know that something is wrong, and to diagnose what needs to be fixed.</span></span> <span data-ttu-id="9cdf5-107">Технически есть возможность подключить отладчик к рабочей службе, но обычно так никто не делает.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-107">Although technically it's possible to connect a debugger to a production service, it's not a common practice.</span></span> <span data-ttu-id="9cdf5-108">Поэтому вам нужны подробные данные инструментирования.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="9cdf5-109">Некоторые решения выполняют инструментирование кода автоматически.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="9cdf5-110">Они могут вполне успешно работать, но почти всегда требуется инструментирование вручную.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="9cdf5-111">В итоге у вас должно быть достаточно информации для экспертной отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-111">In the end, you must have enough information to forensically debug the application.</span></span> <span data-ttu-id="9cdf5-112">В этом документе описываются различные подходы к инструментированию кода и преимущества этих подходов для разных ситуаций.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-112">This document describes different approaches to instrumenting your code, and when to choose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="9cdf5-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="9cdf5-113">EventSource</span></span>
<span data-ttu-id="9cdf5-114">Если вы создаете решение Service Fabric из шаблона в Visual Studio, в нем создается класс **ServiceEventSource** или **ActorEventSource**, производный от **EventSource**.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="9cdf5-115">При этом создается шаблон, в который вы можете добавлять события для конкретного приложения или службы.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="9cdf5-116">Имя **EventSource** **должно** быть уникальным, поэтому потребуется изменить стандартное имя MyCompany-&lt;решение&gt;-&lt;проект&gt;.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-116">The **EventSource** name **must** be unique, and should be renamed from the default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="9cdf5-117">Наличие нескольких определений **EventSource** с одинаковым именем приведет к возникновению проблемы во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-117">Having multiple **EventSource** definitions that use the same name causes an issue at run time.</span></span> <span data-ttu-id="9cdf5-118">У каждого определенного события должен быть уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="9cdf5-119">Если идентификатор не является уникальным, происходит сбой во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="9cdf5-120">Некоторые организации предварительно назначают для идентификаторов диапазоны значений, чтобы избежать конфликтов между командами разработчиков.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-120">Some organizations preassign ranges of values for identifiers to avoid conflicts between separate development teams.</span></span> <span data-ttu-id="9cdf5-121">Дополнительные сведения см. в [блоге Вэнса (Vance)](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) или в [документации MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="9cdf5-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or the [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="9cdf5-122">Использование структурированных событий EventSource</span><span class="sxs-lookup"><span data-stu-id="9cdf5-122">Using structured EventSource events</span></span>

<span data-ttu-id="9cdf5-123">Каждое из событий в примерах кода в этом разделе определено для конкретной ситуации, например для регистрации типа службы.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-123">Each of the events in the code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="9cdf5-124">Если вы определяете сообщения по сценариям использования, в них можно добавить текст сообщения об ошибке. Кроме того, вам будет легче искать или фильтровать сообщения по именам или значениям заданных свойств.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-124">When you define messages by use case, data can be packaged with the text of the error, and you can more easily search and filter based on the names or values of the specified properties.</span></span> <span data-ttu-id="9cdf5-125">Структурирование выходных данных инструментирования упрощает их использование, но чтобы определить новое событие для каждого варианта использования, требуется больше умственной работы и времени.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-125">Structuring the instrumentation output makes it easier to consume, but requires more thought and time to define a new event for each use case.</span></span> <span data-ttu-id="9cdf5-126">Некоторые определения событий могут быть общими для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-126">Some event definitions can be shared across the entire application.</span></span> <span data-ttu-id="9cdf5-127">Например, запуск или остановка метода применяются многократно во многих службах в рамках приложения.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="9cdf5-128">Специализированная служба, например система обработки заказов, может использовать событие **CreateOrder**, включающее собственное уникальное событие.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="9cdf5-129">Такой подход будет порождать множество событий и может потребовать согласования идентификаторов между командами проектов.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The instance constructor is private to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // The ServiceTypeRegistered event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // The ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="9cdf5-130">Универсальное использование EventSource</span><span class="sxs-lookup"><span data-stu-id="9cdf5-130">Using EventSource generically</span></span>

<span data-ttu-id="9cdf5-131">Так как определение конкретных событий может вызвать трудности, многие разработчики определяют несколько событий с общим набором параметров, информация о которых обычно выводится в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="9cdf5-132">При этом они теряют преимущества структурированности, что усложняет поиск и фильтрацию результатов.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-132">Much of the structured aspect is lost, and it's more difficult to search and filter the results.</span></span> <span data-ttu-id="9cdf5-133">При таком подходе обычно определяется небольшое число событий, соответствующих уровням ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-133">In this approach, a few events that usually correspond to the logging levels are defined.</span></span> <span data-ttu-id="9cdf5-134">В приведенном ниже фрагменте кода определяются отладочное сообщение и сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-134">The following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The Instance constructor is private, to enforce singleton semantics.
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

<span data-ttu-id="9cdf5-135">Хорошие результаты может дать гибридный подход, сочетающий структурированное и универсальное инструментирование.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="9cdf5-136">Структурированное инструментирование используется для уведомления об ошибках и метриках.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="9cdf5-137">Универсальные события можно использовать для подробного ведения журнала, который используется инженерами для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-137">Generic events can be used for the detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="9cdf5-138">Ведение журнала ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9cdf5-138">ASP.NET Core logging</span></span>

<span data-ttu-id="9cdf5-139">Очень важно тщательно спланировать методы инструментирования кода.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-139">It's important to carefully plan how you will instrument your code.</span></span> <span data-ttu-id="9cdf5-140">Правильный план инструментирования позволит избежать потенциальной дестабилизации базы кода, которая повлечет за собой повторное инструментрирование кода.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-140">The right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing to reinstrument the code.</span></span> <span data-ttu-id="9cdf5-141">Чтобы снизить риск, вы можете применить библиотеку инструментирования, например [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), которая входит в Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-141">To reduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="9cdf5-142">ASP.NET Core предоставляет интерфейс [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger), который можно подключить к любому поставщику, с минимальными изменениями существующего кода.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with the provider of your choice, while minimizing the effect on existing code.</span></span> <span data-ttu-id="9cdf5-143">Код ASP.NET Core можно использовать на платформах Windows, Linux и в полной версии .NET Framework, то есть код инструментирования будет полностью стандартизирован.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-143">You can use the code in ASP.NET Core on Windows and Linux, and in the full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="9cdf5-144">Это подробнее рассматривается ниже:</span><span class="sxs-lookup"><span data-stu-id="9cdf5-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="9cdf5-145">Использование Microsoft.Extensions.Logging в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9cdf5-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="9cdf5-146">Добавьте пакет NuGet Microsoft.Extensions.Logging в инструментируемый проект.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-146">Add the Microsoft.Extensions.Logging NuGet package to the project you want to instrument.</span></span> <span data-ttu-id="9cdf5-147">Также добавьте все необходимые пакеты поставщиков (в следующем примере показано использование пакета стороннего разработчика).</span><span class="sxs-lookup"><span data-stu-id="9cdf5-147">Also, add any provider packages (for a third-party package, see the following example).</span></span> <span data-ttu-id="9cdf5-148">Дополнительные сведения см. в разделе [Introduction to Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) (Вводные сведения о ведении журналов в ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="9cdf5-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="9cdf5-149">Добавьте в файл службы директиву **using** для Microsoft.Extensions.Logging.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-149">Add a **using** directive for Microsoft.Extensions.Logging to your service file.</span></span>
3. <span data-ttu-id="9cdf5-150">Определите частную переменную в классе службы.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="9cdf5-151">Добавьте в конструктор класса службы приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-151">In the constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="9cdf5-152">Запустите инструментирование кода в методах.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="9cdf5-153">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and the duration of the request.
  // Later in the article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="9cdf5-154">Использование других поставщиков ведения журнала</span><span class="sxs-lookup"><span data-stu-id="9cdf5-154">Using other logging providers</span></span>

<span data-ttu-id="9cdf5-155">Некоторые сторонние поставщики, например [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/) и [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging), используют подход, описанный в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-155">Some third-party providers use the approach described in the preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="9cdf5-156">Вы можете подключить любой из них к подсистеме ведения журналов ASP.NET Core или использовать их отдельно.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="9cdf5-157">Serilog предоставляет возможность создавать дополнительные свойства для сообщений, отправляемых из средства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="9cdf5-158">Эту функцию можно использовать для вывода информации об имени и типе службы, а также секционировании.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-158">This feature can be useful to output the service name, type, and partition information.</span></span> <span data-ttu-id="9cdf5-159">Чтобы использовать эту возможность в инфраструктуре ASP.NET Core, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-159">To use this capability in the ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="9cdf5-160">Добавьте в проект пакеты NuGet Serilog, Serilog.Extensions.Logging и Serilog.Sinks.Observable.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-160">Add the Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages to the project.</span></span> <span data-ttu-id="9cdf5-161">Для следующего примера добавьте также Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-161">For the next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="9cdf5-162">Более правильный подход показан далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="9cdf5-163">В SeriLog создайте LoggerConfiguration и экземпляр средства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-163">In Serilog, create a LoggerConfiguration and the logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="9cdf5-164">Добавьте аргумент Serilog.ILogger в конструктор службы и передайте созданное средство ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-164">Add a Serilog.ILogger argument to the service constructor, and pass the newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="9cdf5-165">В конструктор службы добавьте приведенный ниже код, который создает расширения для свойств **ServiceTypeName**, **ServiceName**, **PartitionId** и **InstanceId** службы.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-165">In the service constructor, add the following code, which creates the property enrichers for the **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of the service.</span></span> <span data-ttu-id="9cdf5-166">Он также добавляет дополнительные свойства в фабрику ведения журналов ASP.NET Core, что позволяет использовать Microsoft.Extensions.Logging.ILogger в коде.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-166">It also adds a property enricher to the ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="9cdf5-167">Инструментирование кода выполняется так же, как в ASP.NET Core без SeriLog.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-167">Instrument the code the same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="9cdf5-168">Мы рекомендуем в предыдущем примере не использовать статический аргумент Log.Logger.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-168">We recommend that you don't use the static Log.Logger with the preceding example.</span></span> <span data-ttu-id="9cdf5-169">Service Fabric позволяет разместить в одном процессе несколько экземпляров службы одного типа.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-169">Service Fabric can host multiple instances of the same service type within a single process.</span></span> <span data-ttu-id="9cdf5-170">Если вы примените статический аргумент Log.Logger, последний модуль записи дополнительных свойств покажет значения для всех запущенных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-170">If you use the static Log.Logger, the last writer of the property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="9cdf5-171">Это одна из причин, по которой переменная _logger является частным членом класса службы.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-171">This is one reason why the _logger variable is a private member variable of the service class.</span></span> <span data-ttu-id="9cdf5-172">Кроме того, переменная _logger должна быть доступна в общем коде, который может использоваться несколькими службами.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-172">Also, you must make the _logger available to common code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="9cdf5-173">Выбор поставщика ведения журнала</span><span class="sxs-lookup"><span data-stu-id="9cdf5-173">Choosing a logging provider</span></span>

<span data-ttu-id="9cdf5-174">Если для вашего приложения требуется высокая производительность, рекомендуется остановить выбор на **EventSource**.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="9cdf5-175">**EventSource** *обычно* использует меньше ресурсов и работает лучше, чем подсистема ведения журнала ASP.NET Core или любое из доступных решений сторонних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of the available third-party solutions.</span></span>  <span data-ttu-id="9cdf5-176">Для многих служб это не проблема, но для высокопроизводительных служб **EventSource** будет наилучшим выбором.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="9cdf5-177">Однако чтобы использовать в **EventSource** преимущества структурированного ведения журнала, потребуются большие усилия команды разработчиков.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-177">However, to get these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="9cdf5-178">По возможности, создайте легко реализуемые модели нескольких параметров ведения журнала, а затем выберите ту модель, которая лучше всего соответствует требованиям.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-178">If possible, do a quick prototype of a few logging options, and then choose the one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cdf5-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9cdf5-179">Next steps</span></span>

<span data-ttu-id="9cdf5-180">После выбора поставщика ведения журнала для инструментирования приложений и служб вам потребуется агрегировать журналы и события перед отправкой в любую платформу аналитики.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-180">Once you have chosen your logging provider to instrument your applications and services, your logs and events need to be aggregated before they can be sent to any analysis platform.</span></span> <span data-ttu-id="9cdf5-181">Прочтите статьи об [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) и [WAD](service-fabric-diagnostics-event-aggregation-wad.md), чтобы лучше понять некоторые рекомендуемые варианты.</span><span class="sxs-lookup"><span data-stu-id="9cdf5-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) to better understand some of the recommended options.</span></span>
