---
title: "ссылка aaaApplicationInsights.config - Azure | Документы Microsoft"
description: "Включение или отключение модулей сбора данных и добавление счетчиков производительности, а также других параметров."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Настройка hello пакет SDK Application Insights с ApplicationInsights.config или XML-файла
пакет SDK для Application Insights .NET Hello состоит из нескольких пакетов NuGet. [Базовый пакет](http://www.nuget.org/packages/Microsoft.ApplicationInsights) предоставляет hello API для отправки телеметрии Application Insights hello. [Дополнительные пакеты](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) предоставляют *модули* и *инициализаторы* телеметрии для автоматического отслеживания телеметрии вашего приложения и его контекста. Перемещая hello файл конфигурации, можно включить или отключить модули телеметрии и инициализаторы и задать параметры для некоторых из них.

файл конфигурации Hello называется `ApplicationInsights.config` или `ApplicationInsights.xml`, в зависимости от типа приложения hello. Она автоматически добавляется tooyour проекта при вы [установки большинства версий пакета SDK для hello][start]. Также добавляется tooa веб-приложения с [монитор состояния на сервере IIS][redfield], или при выборе аналитики приложения hello [расширения для веб-сайта Azure или виртуальной Машины](app-insights-azure-web-apps.md).

Нет hello toocontrol эквивалентный файл [SDK веб-странице][client].

В этом документе описаны разделы hello, отображаемые в конфигурации hello файла, как они управляют компонентами hello hello SDK, и какие пакеты NuGet загрузки этих компонентов.

## <a name="telemetry-modules-aspnet"></a>Модули телеметрии (ASP.NET)
Каждый модуль телеметрии собирает конкретного типа данных и использует hello основных данных hello toosend API. Hello модули устанавливаются различные пакеты NuGet, которые также добавить требуемые строки toohello hello config-файла.

Есть такой узел в файле конфигурации hello для каждого модуля. toodisable модуля, удалите узел hello или закомментируйте его.

### <a name="dependency-tracking"></a>Отслеживание зависимостей
[Отслеживание зависимостей](app-insights-asp-net-dependencies.md) собирает данные телеметрии об обращениях приложение делает toodatabases и внешних служб и баз данных. tooallow toowork этот модуль на сервере IIS, необходимо слишком[установите монитор состояния][redfield]. toouse его в веб-приложениях Azure или на виртуальных машинах, [выберите расширение Application Insights hello](app-insights-azure-web-apps.md).

Можно также написать собственную слежения кода с помощью hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .

### <a name="performance-collector"></a>Сборщик данных производительности
[Собирает данные счетчиков производительности системы](app-insights-performance-counters.md), например ЦП, памяти и сетевой нагрузки из установок IIS. Можно указать, какие счетчики toocollect, включая счетчики производительности, которые вы настроили самостоятельно.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .

### <a name="application-insights-diagnostics-telemetry"></a>Телеметрия диагностики Application Insights
Hello `DiagnosticsTelemetryModule` сообщает об ошибках в hello сам код инструментирования Application Insights. Например если код hello не может получить доступ к счетчики производительности или `ITelemetryInitializer` приводит к возникновению исключения. Отслеживается этим модулем телеметрии трассировки отображается в hello [диагностики поиска][diagnostic]. Отправляет toodc.services.vsallin.net диагностических данных.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . При установке этого пакета только файл ApplicationInsights.config hello не создается автоматически.

### <a name="developer-mode"></a>Режим разработчика
`DeveloperModeWithDebuggerAttachedTelemetryModule`принудительно вызывает hello Application Insights `TelemetryChannel` toosend немедленно, данных телеметрии одного элемента за раз, когда отладчик находится присоединенного toohello процесс приложения. Это уменьшает hello промежуток времени между hello момент, когда приложение отслеживает телеметрии и когда он появится на портале Application Insights hello. Это вызывает значительную нагрузку на процессор и пропускную способность сети.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) 

### <a name="web-request-tracking"></a>Отслеживание веб-запросов
Отчеты hello [время и результат код ответа](app-insights-asp-net.md) HTTP-запросов.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) 

### <a name="exception-tracking"></a>Отслеживание исключений
`ExceptionTrackingTelemetryModule` отслеживает количество необработанных исключений в вашем веб-приложении. Ознакомьтесь со статьей [Ошибки и исключения][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) 
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` отслеживает [незамеченные исключения задач](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` отслеживает необработанные исключения для рабочих ролей, служб Windows и консольных приложений.
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .

### <a name="eventsource-tracking"></a>Отслеживание EventSource
`EventSourceTelemetryModule`позволяет tooconfigure toobe события EventSource отправлен tooApplication аналитики как трассировок. Сведения об отслеживании событий EventSource см. в разделе [Использование событий EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>Трассировка событий Windows
`EtwCollectorTelemetryModule`позволяет tooconfigure события из переданного tooApplication аналитики в качестве трассировки toobe поставщиков трассировки событий Windows. Сведения об отслеживании событий трассировки событий Windows см. в разделе [Использование событий трассировки событий Windows](app-insights-asp-net-trace-logs.md#using-etw-events).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
пакет Microsoft.ApplicationInsights Hello предоставляет hello [основные API](https://msdn.microsoft.com/library/mt420197.aspx) из пакета SDK для hello. Hello другие модули телеметрии этот метод следует использовать, и вы также можете [toodefine использовать собственные телеметрии](app-insights-api-custom-events-metrics.md).

* Нет записей в файле ApplicationInsights.config.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Если просто установить этот пакет NuGet, CONFIG-файл не создается.

## <a name="telemetry-channel"></a>Канал телеметрии
Hello телеметрии канала управляет буферизацией и передачу данных телеметрии toohello служба Application Insights.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`— hello канал по умолчанию для служб. Он создает буфер данных в памяти.
* `Microsoft.ApplicationInsights.PersistenceChannel` — альтернатива для консольных приложений. Он может сэкономить любое хранилище данных unflushed toopersistent при закрывает приложение и отправит его при запуске приложение hello, еще раз.

## <a name="telemetry-initializers-aspnet"></a>Инициализаторы телеметрии (ASP.NET)
Инициализаторы телеметрии задают свойства контекста, которые отправляются вместе с каждым элементом телеметрии.

Вы можете [написать собственные инициализаторы](app-insights-api-filtering-sampling.md#add-properties) tooset свойства контекста.

Стандартная инициализаторы Hello установлено либо hello пакетов WindowsServer NuGet или веб:

* `AccountIdTelemetryInitializer`Задает свойство AccountId hello.
* `AuthenticatedUserIdTelemetryInitializer`Задает свойство AuthenticatedUserId hello как набор с hello JavaScript SDK.
* `AzureRoleEnvironmentTelemetryInitializer`обновления hello `RoleName` и `RoleInstance` свойства hello `Device` контекст для всех элементов телеметрии с помощью данных, извлеченных из среды выполнения Azure hello.
* `BuildInfoConfigComponentVersionTelemetryInitializer`обновления hello `Version` свойство hello `Component` контекст для всех элементов телеметрии со значением hello, извлеченным из hello `BuildInfo.config` файл создан с помощью MS Build.
* `ClientIpHeaderTelemetryInitializer`обновления `Ip` свойство hello `Location` контекст всех элементов телеметрии на основании hello `X-Forwarded-For` заголовок HTTP запроса hello.
* `DeviceTelemetryInitializer`следующие свойства объекта hello hello обновления `Device` контекст для всех элементов телеметрии.
  * `Type`задано слишком «PC»
  * `Id`имеет значение toohello доменное имя компьютера hello, где работает веб-приложение hello.
  * `OemName`имеет значение toohello значение, извлеченное из hello `Win32_ComputerSystem.Manufacturer` поля с помощью инструментария WMI.
  * `Model`имеет значение toohello значение, извлеченное из hello `Win32_ComputerSystem.Model` поля с помощью инструментария WMI.
  * `NetworkType`имеет значение toohello значение, извлеченное из hello `NetworkInterface`.
  * `Language`задается имя toohello hello `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`обновления hello `RoleInstance` свойство hello `Device` контекст для всех элементов телеметрии с доменным именем hello hello компьютера, где выполняется веб-приложение hello.
* `OperationNameTelemetryInitializer`обновления hello `Name` свойство hello `RequestTelemetry` и hello `Name` свойство hello `Operation` контекст всех элементов телеметрии зависимости от метода hello HTTP, а также имена hello вызванный tooprocess контроллера и действия ASP.NET MVC запрос.
* `OperationIdTelemetryInitializer`или `OperationCorrelationTelemetryInitializer` обновления hello `Operation.Id` контекстное свойство всех элементов телеметрии отслеживаются во время обработки запроса с hello автоматически создается `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`обновления hello `Id` свойство hello `Session` контекст для всех элементов телеметрии с значение, извлеченное из hello `ai_session` cookie созданные hello код инструментирования ApplicationInsights JavaScript, выполняются в браузере пользователя hello.
* `SyntheticTelemetryInitializer`или `SyntheticUserAgentTelemetryInitializer` обновления hello `User`, `Session` и `Operation` контекстов свойств всех элементов телеметрии отслеживаются при обработке запроса от искусственного источника, например доступности тестирования или выполните поиск программ-роботов ядра. По умолчанию [обозреватель метрик](app-insights-metrics-explorer.md) не отображает данные телеметрии искусственных источников.

    Hello `<Filters>` задать определение свойств запросов на hello.
* `UserAgentTelemetryInitializer`обновления hello `UserAgent` свойство hello `User` контекст всех элементов телеметрии на основании hello `User-Agent` заголовок HTTP запроса hello.
* `UserTelemetryInitializer`обновления hello `Id` и `AcquisitionDate` свойства `User` контекст для всех элементов телеметрии со значения, извлеченные из hello `ai_user` куки-файл, созданный код инструментирования Application Insights JavaScript hello, выполняемый в hello браузер пользователя.
* `WebTestTelemetryInitializer`для HTTP-запросы, поставляемые с наборами hello идентификатор пользователя, идентификатор сеанса и свойства источника искусственных [тестов доступности](app-insights-monitor-web-app-availability.md).
  Hello `<Filters>` задать определение свойств запросов на hello.

Для приложений .NET, работающих в Service Fabric, можно включить hello `Microsoft.ApplicationInsights.ServiceFabric` пакет NuGet. Этот пакет включает в себя `FabricTelemetryInitializer`, который добавляет элементы tootelemetry свойств Service Fabric. Дополнительные сведения см. в разделе hello [странице GitHub](https://go.microsoft.com/fwlink/?linkid=848457) о свойствах hello, добавленные в этот пакет NuGet.

## <a name="telemetry-processors-aspnet"></a>Обработчики данных телеметрии (ASP.NET)
Процессоры телеметрии можно фильтровать и изменения каждого элемента телеметрии непосредственно перед отправкой с портала toohello hello SDK.

Вы можете [написать собственные обработчики данных телеметрии](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Обработчик адаптивной выборки телеметрии (начиная с версии 2.0.0-beta3)
Эта функция включена по умолчанию. Если приложение отправляет слишком много телеметрических данных, обработчик удаляет часть из них.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

параметр Hello предоставляет цели hello, Здравствуйте, алгоритм пытается tooachieve. Каждый экземпляр hello работы пакета SDK для независимо друг от друга, поэтому если сервер находится в кластере из нескольких компьютеров, hello фактический объем телеметрии будут умножены соответствующим образом.

[Дополнительная информация о выборке](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>Обработчик выборки телеметрии с фиксированной частотой (начиная с версии 2.0.0-beta1)
Также имеется стандартный [обработчик выборочной телеметрии](app-insights-api-filtering-sampling.md) (начиная с версии 2.0.1):

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Параметры канала (Java)
Эти параметры влияют как следует хранить и очистка hello данные телеметрии, которые она собирает hello Java SDK.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
количество элементов телеметрии, которые могут храниться в хранилище в памяти hello SDK Hello. При достижении этого количества буфера телеметрии hello -, hello телеметрии элементы передаются серверу toohello Application Insights.

* Мин. значение: 1.
* Макс. значение: 1000.
* Значение по умолчанию: 500.

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Определяет, как часто hello данные, хранящиеся в хранилище в памяти hello должна быть сброшены (отправленных tooApplication аналитики).

* Мин. значение: 1.
* Макс. значение: 300.
* Значение по умолчанию: 5.

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Определяет hello максимальный размер в Мегабайтах, который выделяется toohello постоянное хранилище на локальном диске hello. Это хранилище используется для сохранения элементов телеметрии, сбой конечной точки Application Insights toohello toobe передачи. При выполнении размер хранилища hello новые элементы данных телеметрии, будут отменены.

* Мин. значение: 1.
* Макс. значение: 100.
* Значение по умолчанию: 10.

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Определяет ресурс Application Insights hello, в котором отображается данных. Обычно создается отдельный ресурс с отдельным ключом инструментирования для каждого приложения.

Если нужно tooset hello ключ динамически — например, если требуется toosend результаты из ресурсов приложения toodifferent - можно опустить hello ключ из файла конфигурации hello и установите его в коде.

ключ hello tooset для всех экземпляров TelemetryClient, включая модули стандартной телеметрии, настройте раздел hello TelemetryConfiguration.Active. Задайте ключ в методе инициализации, таком как global.aspx.cs, в службе ASP.NET:

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Если необходимо просто toosend определенный набор событий tooa различных ресурсов, можно задать ключ hello для конкретных TelemetryClient:

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

новый ключ tooget [Создание ресурса на портале Application Insights hello][new].

## <a name="next-steps"></a>Дальнейшие действия
[Дополнительные сведения об hello API][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
