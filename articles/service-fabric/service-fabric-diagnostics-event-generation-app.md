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
# <a name="application-and-service-level-event-and-log-generation"></a>Создание событий и журналов на уровне приложений и служб

## <a name="instrumenting-hello-code-with-custom-events"></a>Инструментирование кода hello с помощью пользовательских событий

Инструментирование кода hello является основой hello для большинства других аспектов мониторинга служб. Инструментирование является единственным способом hello, известно дает сбой, что toodiagnose, требующие toobe фиксированной. Хотя технически возможных tooconnect отладчик tooa рабочей службе, не принято. Поэтому вам нужны подробные данные инструментирования.

Некоторые решения выполняют инструментирование кода автоматически. Они могут вполне успешно работать, но почти всегда требуется инструментирование вручную. В конце hello должен иметь достаточно сведений, tooforensically отладки приложения hello. В этом документе описаны различные подходы tooinstrumenting кода, и если toochoose один подход на другое.

## <a name="eventsource"></a>EventSource
Если вы создаете решение Service Fabric из шаблона в Visual Studio, в нем создается класс **ServiceEventSource** или **ActorEventSource**, производный от **EventSource**. При этом создается шаблон, в который вы можете добавлять события для конкретного приложения или службы. Hello **EventSource** имя **должен** быть уникальным и должно быть заменено из строки шаблона по умолчанию hello MyCompany -&lt;решения&gt; - &lt; проект&gt;. Наличие нескольких **EventSource** определений, использующих hello же причины имя ошибку во время выполнения. У каждого определенного события должен быть уникальный идентификатор. Если идентификатор не является уникальным, происходит сбой во время выполнения. В некоторых организациях preassign диапазоны значений идентификаторов tooavoid конфликтов между отдельные группы разработчиков. Дополнительные сведения см. в разделе [блога Вэнс элемента](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) или hello [документации MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>Использование структурированных событий EventSource

Каждое из событий hello в примерах кода hello в этом разделе определяются для определенного случая, например, при регистрации типа службы. Когда определить сообщения в варианте использования, данные можно упаковать с текстом hello ошибки hello и вы можете более легко выполнять поиск и фильтр на основе имен hello или значениям hello указанные свойства. Структурирование вывод инструментария hello позволяет проще tooconsume, но требуется более сложная и время toodefine новое событие для каждого варианта использования. Некоторые определения событий могут совместно использоваться hello всего приложения. Например, запуск или остановка метода применяются многократно во многих службах в рамках приложения. Специализированная служба, например система обработки заказов, может использовать событие **CreateOrder**, включающее собственное уникальное событие. Такой подход будет порождать множество событий и может потребовать согласования идентификаторов между командами проектов. 

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

### <a name="using-eventsource-generically"></a>Универсальное использование EventSource

Так как определение конкретных событий может вызвать трудности, многие разработчики определяют несколько событий с общим набором параметров, информация о которых обычно выводится в строковом формате. Большая часть аспект hello структурированные теряется, а он является более сложным toosearch и фильтровать результаты hello. При таком подходе определены несколько событий, которые обычно соответствуют уровни ведения журнала toohello. Следующий фрагмент кода Hello определяет отладки и сообщение об ошибке:

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

Хорошие результаты может дать гибридный подход, сочетающий структурированное и универсальное инструментирование. Структурированное инструментирование используется для уведомления об ошибках и метриках. Универсальные события можно использовать для hello подробное ведение журнала, используемые инженеров по устранению неполадок.

## <a name="aspnet-core-logging"></a>Ведение журнала ASP.NET Core

Важные toocarefully плана, как будет инструментировать код. план правой инструментария Hello поможет вам избежать потенциально дестабилизации базы кода, а затем при необходимости tooreinstrument кода hello. риск tooreduce, вы можете выбрать библиотеку инструментирования как [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), который является частью Microsoft ASP.NET Core. ASP.NET Core имеет [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) интерфейс, который можно использовать с поставщиком hello по своему усмотрению, сводя к минимуму влияние hello на существующий код. Можно использовать код hello в ASP.NET Core в Windows и Linux и в hello полной платформы .NET Framework, стандартизованные инструментирования кода. Это подробнее рассматривается ниже:

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Использование Microsoft.Extensions.Logging в Service Fabric

1. Добавьте hello Microsoft.Extensions.Logging NuGet пакета toohello проекта требуется tooinstrument. Кроме того, добавьте все пакеты поставщика (пакета стороннего производителя, см. следующий пример hello). Дополнительные сведения см. в разделе [Introduction to Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) (Вводные сведения о ведении журналов в ASP.NET Core).
2. Добавить **с помощью** директив для файла службы tooyour Microsoft.Extensions.Logging.
3. Определите частную переменную в классе службы.

  ```csharp
  private ILogger _logger = null;

  ```
4. В конструкторе hello класса службы добавьте следующий код:

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Запустите инструментирование кода в методах. Вот несколько примеров.

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Использование других поставщиков ведения журнала

Некоторые сторонние поставщики использовать hello подход, описанный в hello предшествующий раздела, включая [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), и [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). Вы можете подключить любой из них к подсистеме ведения журналов ASP.NET Core или использовать их отдельно. Serilog предоставляет возможность создавать дополнительные свойства для сообщений, отправляемых из средства ведения журнала. Эта функция может быть полезно toooutput hello службы имя, тип и сведения о секции. toouse эту возможность с помощью hello инфраструктуры ASP.NET Core, выполните следующие действия:

1. Добавьте hello Serilog, Serilog.Extensions.Logging, и Serilog.Sinks.Observable NuGet пакеты toohello проекта. Следующий пример hello необходимо также добавьте Serilog.Sinks.Literate. Более правильный подход показан далее в этой статье.
2. В Serilog создайте экземпляр средства ведения журнала LoggerConfiguration и hello.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Добавьте конструктор Serilog.ILogger аргумент toohello службы и передайте hello вновь созданные средства ведения журнала.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. В конструктор служб hello, добавьте следующий код, создающий hello enrichers свойство для hello hello **ServiceTypeName**, **ServiceName**, **PartitionId**и  **InstanceId** свойства службы hello. Он также добавляет свойство enricher toohello фабрики ASP.NET Core ведения журнала, чтобы можно было использовать в коде Microsoft.Extensions.Logging.ILogger.

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

5. Hello инструментирования кода hello таким же, как при использовании ASP.NET Core без Serilog.

  >[!NOTE]
  >Рекомендуется не использовать статический hello Log.Logger с предшествующей пример hello. Service Fabric можно разместить несколько экземпляров hello же службы типа внутри одного процесса. При использовании статического Log.Logger hello, hello последней записи enrichers hello свойства будут выведены значения для всех экземпляров, работающих под управлением. Это — еще одна причина, почему hello _logger переменная является переменной закрытого члена класса службы hello. Кроме того необходимо внести hello _logger доступных toocommon код, который может использоваться между службами.

## <a name="choosing-a-logging-provider"></a>Выбор поставщика ведения журнала

Если для вашего приложения требуется высокая производительность, рекомендуется остановить выбор на **EventSource**. **EventSource** *обычно* использует меньше ресурсов и работает лучше, чем ASP.NET Core ведения журнала или любой из доступных решений сторонних hello.  Для многих служб это не проблема, но для высокопроизводительных служб **EventSource** будет наилучшим выбором. Однако tooget структурированные ведения журнала, эти преимущества **EventSource** требует больших затрат из вашей командой разработчиков. Если это возможно, выполните быстрый прототип несколько параметров ведения журнала и выберите hello, который лучше всего соответствует вашим потребностям.

## <a name="next-steps"></a>Дальнейшие действия

После выбора вашей tooinstrument поставщика ведения журналов приложений и служб, журналы и события должны toobe статистическую обработку, прежде чем передавать их tooany платформа анализа. Узнайте, как [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) и [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter понять hello рекомендуемые параметры.
