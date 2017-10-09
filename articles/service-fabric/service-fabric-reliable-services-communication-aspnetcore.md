---
title: "связь aaaService с hello ASP.NET Core | Документы Microsoft"
description: "Дополнительные сведения о том, как toouse ASP.NET Core в надежных служб без отслеживания состояния и с отслеживанием состояния."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>ASP.NET Core в Service Fabric Reliable Services

ASP.NET Core — это новая кроссплатформенная среда с открытым кодом для создания современных облачных приложений с подключением к Интернету, таких как веб-приложения, приложения для Интернета вещей и серверные части мобильных приложений. 

В этой статье представлено подробное руководство toohosting служб ASP.NET Core в Service Fabric надежного обмена с помощью hello **Microsoft.ServiceFabric.AspNetCore.** * набор пакетов NuGet.

Вводное руководство по ASP.NET Core в Service Fabric и инструкции по настройке среды разработки см. в статье [Создание внешнего интерфейса веб-службы для приложения с помощью ASP.NET Core](service-fabric-add-a-web-frontend.md).

Hello оставшейся части этой статьи предполагается, что вы уже знакомы с ASP.NET Core. Если нет, рекомендуется ознакомиться hello [основы ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>ASP.NET Core в среде Service Fabric hello

Хотя приложения ASP.NET Core можно запустить на основе .NET Core или полной версии .NET Framework, в данный момент служб Service Fabric могут выполняться только на приветствия hello полной версии .NET Framework. Это означает, что при построении службы ASP.NET Core Service Fabric, необходимо по-прежнему нацелить Здравствуйте полной версии .NET Framework.

ASP.NET Core можно использовать двумя различными способами в Service Fabric:
 - **Разместить в виде гостевого исполняемого файла**. Это в основном используется toorun существующие ASP.NET Core приложения в Service Fabric без изменения кода.
 - **Выполнять внутри надежной службы**. Это обеспечивает более эффективную интеграцию со средой выполнения Service Fabric hello и позволяет службам с отслеживанием состояния ASP.NET Core.

Hello оставшейся части этой статьи объясняется, как toouse ASP.NET Core внутри надежной службы с помощью hello компоненты интеграции ASP.NET Core, поставляемых вместе с hello Service Fabric SDK. 

## <a name="service-fabric-service-hosting"></a>Размещение службы Service Fabric

В Service Fabric один или несколько экземпляров и (или) реплик службы выполняются в *хост-процессе службы* — исполняемом файле, который выполняет код службы. Автор службы принадлежит вам хост-процесса службы hello и Service Fabric активирует и следит за его работой.

Традиционные ASP.NET (вверх tooMVC 5) — тесно связанные tooIIS через System.Web.dll. ASP.NET Core позволяет разделить hello веб-сервер и веб-приложения. Это позволяет toobe приложения web зависимых от разных веб-серверов и также позволяет toobe серверы веб *резидентной*, что означает можно запустить на веб-сервере в процессе, как противоположность tooa процесс, владельцем которого является выделенное веб серверное программное обеспечение, такими как службы IIS. 

В порядке toocombine служба Service Fabric и ASP.NET, в качестве гостевой исполняемый файл или в надежной службы, необходимо будет toostart ASP.NET внутри хост-процесса службы. ASP.NET Core резидентным позволяет toodo это.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>Размещение ASP.NET Core в Reliable Service
Как правило, резидентных приложений ASP.NET Core создать WebHost в точку входа приложения, например hello `static void Main()` метод в `Program.cs`. В этом случае жизненный цикл hello hello WebHost представляет связанный toohello жизненного цикла процесса hello.

![Размещение ASP.NET Core в процессе][0]

Однако точку входа приложения hello не toocreate подходящее место hello WebHost в надежной службы, так как точку входа приложения hello используется только tooregister службы тип среды выполнения Service Fabric hello, так, что возможно создание экземпляров данной службы тип. Hello WebHost должны создаваться в надежной службы сам. В рамках хост-процесса службы hello экземпляров службы и/или реплики можно выполнить несколько жизненные циклы. 

Экземпляр Reliable Service представлен с помощью класса службы, производного от `StatelessService` или `StatefulService`. Hello стек связи для службы содержится в `ICommunicationListener` реализации в классе службы. Hello `Microsoft.ServiceFabric.Services.AspNetCore.*` пакетов NuGet содержащих реализации `ICommunicationListener` , запуск и управление hello ASP.NET Core WebHost для Kestrel или WebListener в надежной службы.

![Размещение ASP.NET Core в Reliable Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a>Объекты ICommunicationListener в ASP.NET Core
Hello `ICommunicationListener` реализации Kestrel и WebListener в hello `Microsoft.ServiceFabric.Services.AspNetCore.*` пакетами NuGet имеют схожие схемы использования, но выполнить несколько различных действий конкретных tooeach веб-сервера. 

Оба прослушивания связи предоставляют конструктор, принимающий hello следующие аргументы:
 - **`ServiceContext serviceContext`**: hello `ServiceContext` объект, содержащий сведения о hello службой.
 - **`string endpointName`**: имя hello `Endpoint` конфигурации в файле ServiceManifest.xml. Это в первую очередь которых hello двух прослушивания связи не совпадают: WebListener **требует** `Endpoint` конфигурации, а Kestrel — нет.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**. Реализуемое лямбда-выражение, в котором создается и возвращается `IWebHost`. Это позволяет tooconfigure `IWebHost` способом hello, обычно в приложении ASP.NET Core. Hello лямбда-выражение содержит URL-адрес, который создается в зависимости от интеграции Service Fabric hello параметрах, можно использовать и hello `Endpoint` вами конфигурации. Что URL-адрес затем можно изменить или использовать в качестве-toostart hello веб-сервером.

## <a name="service-fabric-integration-middleware"></a>ПО промежуточного уровня для интеграции Service Fabric
Hello `Microsoft.ServiceFabric.Services.AspNetCore` пакет NuGet включает hello `UseServiceFabricIntegration` метода расширения `IWebHostBuilder` , добавляет службы структуры поддержкой по промежуточного слоя. Это по промежуточного слоя настраивает hello Kestrel или WebListener `ICommunicationListener` tooregister уникальный URL-адрес с hello служба именования Service Fabric, а затем проводится проверка подключении нужную службу toohello клиентов tooensure запросы клиента. Это необходимо в среде общего узла, например Service Fabric, где несколько веб-приложений можно запускать на hello же физической или виртуальной машины, но не использует имена уникальный узлов, tooprevent клиенты по ошибке подключение не toohello в службу. Этот сценарий описан более подробно в следующем разделе hello.

### <a name="a-case-of-mistaken-identity"></a>Причина ошибочный идентификации
Реплики службы, независимо от протокола, прослушивают уникальное сочетание "IP-адрес:порт". После запуска прослушивание в конечной точке IP: Port реплики службы он сообщает, toohello адрес конечной точки службы именования Service Fabric где он обнаружен клиентам или другим службам. Если приложение динамическое назначение портов, реплики службы по случайному совпадению могут использовать службы используйте hello же конечная точка IP: Port другой службы, который ранее был на hello же физической или виртуальной машины. Это может вызвать клиент toomistakely подключения не toohello в службу. Это может произойти в случае hello следующая последовательность событий:

 1. Служба А прослушивает 10.0.0.1:30000 по протоколу HTTP. 
 2. Клиент разрешает службу А и возвращает адрес 10.0.0.1:30000.
 3. Службы на другой узел tooa переход.
 4. Службы B помещается на 10.0.0.1, по случайному совпадению использует hello тот же порт 30000.
 5. Клиент пытается tooservice tooconnect A с 10.0.0.1:30000 кэшированных адресов.
 6. Клиент — теперь подключен успешно выполнено подключение tooservice B, не зная, что он не toohello в службу.

Это может вызвать ошибки в разное время, которые могут быть трудности toodiagnose. 

### <a name="using-unique-service-urls"></a>Использование уникальных URL-адресов службы
tooprevent этой службы можно учесть toohello конечной точки службы именования с уникальным идентификатором и проверьте, уникальный идентификатор во время запросов клиентов. Это совместное действие между службами в доверенной среде дружественного клиента. Это не обеспечивает безопасную проверку подлинности службы в среде недружественного клиента.

В доверенной среде hello по промежуточного слоя, который добавляется по hello `UseServiceFabricIntegration` метод автоматически добавляет адрес toohello уникальный идентификатор, который отправляется toohello службы именования и проверяет этот идентификатор для каждого запроса. Если идентификатор hello не совпадает, по промежуточного слоя hello немедленно возвращает ответ HTTP 410-потеряно.

Службы, использующие динамически назначаемый порт, должны использовать это ПО промежуточного слоя.

Службы, использующие постоянный уникальный порт, не имеют такой проблемы в совместной среде. Уникальный фиксированный порт обычно используется для служб извне с выходом, хорошо известных портов для клиентских приложений tooconnect для. Например, большинство веб-приложений с доступом к Интернету используют порт 80 или 443 для подключений веб-браузера. В этом случае не следует включать hello уникальный идентификатор.

Hello следующей схеме показан поток запросов hello с по промежуточного слоя hello включен:

![Интеграция Service Fabric ASP.NET Core][2]

Kestrel и WebListener `ICommunicationListener` реализации используют этот механизм в hello точно таким же образом. Несмотря на то, что WebListener внутренне может различать запросы с учетом уникальный URL-пути, с помощью базового hello *http.sys* возможность функциональные возможности совместного использования портов *не* используемые hello WebListener `ICommunicationListener` реализацию так, как будут созданы HTTP 503 и ошибки HTTP 404 коды состояния ошибок hello сценарий, описанный ранее. В свою очередь затрудняет очень клиентов toodetermine hello цель ошибки hello, что HTTP 503 HTTP 404 уже часто используемые tooindicate других ошибок. Таким образом, как Kestrel и WebListener `ICommunicationListener` реализации стандартизировать hello по промежуточного слоя, предоставляемые hello `UseServiceFabricIntegration` метод расширения, чтобы клиенты нуждаются tooperform конечную точку службы заново разрешить действие в ответы HTTP 410.

## <a name="weblistener-in-reliable-services"></a>WebListener в службах Reliable Services
WebListener может использоваться в надежной службы путем импорта hello **Microsoft.ServiceFabric.AspNetCore.WebListener** пакет NuGet. Этот пакет содержит `WebListenerCommunicationListener`, реализация `ICommunicationListener`, позволяющее вам toocreate WebHost Core ASP.NET внутри надежной службы с помощью WebListener hello веб-сервер.

WebListener основана на hello [API HTTP-сервера Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx). В этом случае используется hello *http.sys* драйвер ядра, используемые IIS tooprocess HTTP запрашивает и перенаправлять их tooprocesses запуском веб-приложений. Это позволяет нескольким процессам на hello одной физической или виртуальной машины toohost веб-приложений на hello же порт, однозначно уникальный URL-адрес или имя узла. Эти функции полезны в Service Fabric для размещения нескольких веб-сайтов в hello одного кластера.

Hello следующей схеме показано, как WebListener использует hello *http.sys* драйвер ядра в Windows для общего доступа к портам:

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>WebListener в службе без отслеживания состояния
toouse `WebListener` в службы без отслеживания состояния, переопределите hello `CreateServiceInstanceListeners` метода и возврата `WebListenerCommunicationListener` экземпляр:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a>WebListener в службе с отслеживанием состояния

`WebListenerCommunicationListener`в настоящее время не предназначен для использования служб с отслеживанием состояния заказа toocomplications с базовым hello *http.sys* возможность совместного использования портов. Дополнительные сведения см. следующий раздел на динамического выделения портов с WebListener hello. Для служб с отслеживанием состояния Kestrel — hello, рекомендуется использовать веб-сервер.

### <a name="endpoint-configuration"></a>Настройка конечной точки

`Endpoint` Настройка не требуется для веб-серверов, использующих Windows API HTTP-сервера, включая WebListener hello. Веб-серверы, использующие API HTTP-сервера Windows hello сначала необходимо зарезервировать URL-адрес с *http.sys* (обычно это осуществляется с помощью hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) инструмента). Для этого действия требуются повышенные привилегии, которых по умолчанию нет у служб. Здравствуйте, «http» или «https» параметры для hello `Protocol` свойство hello `Endpoint` конфигурации в *ServiceManifest.xml* используются специально tooinstruct hello tooregister среда выполнения Service Fabric URL-адрес с *http.sys* от вашего имени, с помощью hello [ *адресе* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) префикс URL-адреса.

Например, tooreserve `http://+:80` для службы, hello следующую конфигурацию следует использовать в файле ServiceManifest.xml:

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

И имя конечной точки hello должен быть передан toohello `WebListenerCommunicationListener` конструктор:

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a>Использование WebListener со статическим портом
toouse статический порт с WebListener, укажите номер порта hello в hello `Endpoint` конфигурации:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>Использование WebListener с динамическим портом
toouse динамически назначаемый порт с WebListener, пропустите hello `Port` свойство в hello `Endpoint` конфигурации:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

Обратите внимание, что динамический порт, выделенный с помощью конфигурации `Endpoint`, предоставляет только один порт *каждому хост-процессу*. Hello текущего Service Fabric модели размещения позволяет нескольким toobe экземпляры или реплики службы, размещенной в hello же процесс, то есть каждый из них будут совместно использовать же порт при выделении через hello hello `Endpoint` конфигурации. Несколько экземпляров WebListener могут совместно использовать порт, используя базовый hello *http.sys* совместного использования порта компонент, но которая не поддерживается `WebListenerCommunicationListener` из-за сложности toohello, он вводит для клиентских запросов. Для использования динамических портов Kestrel — hello, рекомендуется использовать веб-сервер.

## <a name="kestrel-in-reliable-services"></a>Kestrel в Reliable Services
Kestrel может использоваться в надежной службы путем импорта hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** пакет NuGet. Этот пакет содержит `KestrelCommunicationListener`, реализация `ICommunicationListener`, позволяющее вам toocreate WebHost Core ASP.NET внутри надежной службы с помощью Kestrel hello веб-сервер.

Kestrel — это кроссплатформенный веб-сервер для ASP.NET Core на основе libuv, кроссплатформенной библиотеки асинхронных операций ввода-вывода. В отличие от WebListener, Kestrel не использует централизованный диспетчер конечных точек, такой как *http.sys*, и не поддерживает совместное использование порта между несколькими процессами. Каждый экземпляр Kestrel должен использовать уникальный порт.

![Kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>Kestrel в службе без отслеживания состояния
toouse `Kestrel` в службы без отслеживания состояния, переопределите hello `CreateServiceInstanceListeners` метода и возврата `KestrelCommunicationListener` экземпляр:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a>Kestrel в службе с отслеживанием состояния
toouse `Kestrel` в службы с отслеживанием состояния, переопределите hello `CreateServiceReplicaListeners` метода и возврата `KestrelCommunicationListener` экземпляр:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

В этом примере одноэлементный экземпляр `IReliableStateManager` предоставляется контейнер внедрения зависимостей toohello WebHost. Это не является обязательным, но позволяет toouse `IReliableStateManager` и надежного коллекций в методах действий контроллера MVC.

Обратите внимание, что `Endpoint` имя конфигурации — **не** указано слишком`KestrelCommunicationListener` в службы с отслеживанием состояния. Это является более подробно описываются в следующем разделе hello.

### <a name="endpoint-configuration"></a>Настройка конечной точки
`Endpoint` Конфигурация не требуется toouse Kestrel. 

Kestrel является простой автономного веб-сервера; в отличие от WebListener (или HttpListener), не обязательно `Endpoint` конфигурации в *ServiceManifest.xml* из-за предыдущих toostarting регистрации URL-адрес не требуется. 

#### <a name="use-kestrel-with-a-static-port"></a>Использование Kestrel и статического порта
Можно настроить статический порт в hello `Endpoint` конфигурации для использования с Kestrel ServiceManifest.xml. Хотя это не является обязательным, это дает два потенциальных преимущества:
 1. Если порт hello не попадает в диапазон портов приложения hello, он открыт через брандмауэр ОС hello Service Fabric.
 2. Здравствуйте, tooyou указанного URL-адреса через `KestrelCommunicationListener` будет использовать этот порт.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

Если `Endpoint` будет настроен, его имя необходимо передавать в hello `KestrelCommunicationListener` конструктор: 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

Если `Endpoint` конфигурация не используется, пропустите имя hello в hello `KestrelCommunicationListener` конструктор. В этом случае будет использоваться динамический порт. Hello следующем разделе для получения дополнительной информации.

#### <a name="use-kestrel-with-a-dynamic-port"></a>Использование Kestrel и динамического порта
Kestrel нельзя использовать назначение автоматического порта hello из hello `Endpoint` конфигурации в файле ServiceManifest.xml, так как порт автоматическое назначение на основе `Endpoint` конфигурация назначает уникальный порт на *хост-процесса* , и один хост-процесс может содержать несколько экземпляров Kestrel. Так как Kestrel не поддерживает совместное использование портов, это не будет работать, потому что каждый экземпляр Kestrel должен быть открыт на уникальном порте.

toouse динамическое назначение порта с Kestrel, просто пропустить hello `Endpoint` конфигурации в файле ServiceManifest.xml полностью, а не передавать toohello имя конечной точки `KestrelCommunicationListener` конструктор:

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

В этой конфигурации `KestrelCommunicationListener` автоматически выбирает из диапазона портов приложения hello неиспользуемый порт.

## <a name="scenarios-and-configurations"></a>Сценарии и конфигурации
В этом разделе описываются следующие сценарии hello и предоставляет hello рекомендуется сочетание веб-сервера, конфигурации портов, возможностей интеграции Service Fabric и прочие параметры tooachieve правильно работает служба:
 - Доступная извне служба ASP.NET Core без отслеживания состояния
 - Служба ASP.NET Core без отслеживания состояния только для внутреннего использования
 - Служба ASP.NET Core с отслеживанием состояния только для внутреннего использования

**Извне предоставляется** понимается служба, которая предоставляет конечную точку, доступен с кластера hello, обычно через подсистему балансировки нагрузки.

**Только для внутреннего использования** обслуживание — одна конечная точка которого доступен только в пределах кластера hello.

> [!NOTE]
> Службы с отслеживанием состояния, которые конечных точек обычно не должно быть предоставляются toohello Интернета. Кластеров, которые находятся позади подсистемы балансировки нагрузки, которые не знают о разрешения для службы Service Fabric, например hello балансировки нагрузки Azure будет невозможно tooexpose служб с отслеживанием состояния, так как hello балансировки нагрузки будет не может toolocate и направлять трафик toohello соответствующие службы с отслеживанием состояния реплики. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>Доступные извне службы ASP.NET Core без отслеживания состояния
WebListener — hello, рекомендуется использовать веб-сервере переднего плана служб, предоставляющих конечные точки HTTP внешних, с выходом в Интернет в Windows. Это обеспечивает более надежную защиту от атак и поддерживает функции, которые не поддерживает Kestrel (например, проверка подлинности Windows и общий доступ к портам). 

В настоящее время Kestrel не поддерживается в качестве пограничного сервера (с доступом к Интернету). Необходимо использовать обратного прокси-сервера, например IIS или Nginx toohandle трафик от hello общедоступный Интернет.
 
При toohello предоставляется Интернет-службы без отслеживания состояния следует использовать хорошо известны и стабильный конечной точки, доступная через подсистему балансировки нагрузки. Это URL-адрес hello предоставит toousers приложения. рекомендуется следующая конфигурация Hello:

|  |  | **Примечания** |
| --- | --- | --- |
| Веб-сервер | WebListener | Если служба hello только предоставляется tooa доверенной сети, такие как в интрасети и могут использоваться Kestrel. В противном случае WebListener — hello предпочтительный вариант. |
| Конфигурация порта | static | Хорошо известных статический порт должны быть настроены в hello `Endpoints` конфигурация ServiceManifest.xml, например 80 для HTTP и 443 для HTTPS. |
| ServiceFabricIntegrationOptions | None | Hello `ServiceFabricIntegrationOptions.None` параметр должен использоваться при настройке Service Fabric интеграции по промежуточного слоя, чтобы служба hello не будет пытаться toovalidate входящие запросы на уникальный идентификатор. Внешние пользователи приложения не знает hello уникальных идентификационных данных используется по промежуточного слоя hello. |
| Число экземпляров | -1 | В типичные случаи использования, необходимо задать значение количества экземпляров hello слишком «-1», чтобы экземпляр доступен на всех узлах, получать трафик от подсистемы балансировки нагрузки. |

Если несколько служб извне предоставляется hello же набор узлов, следует использовать уникальны, но стабильный URL-пути. Это можно сделать, изменив hello URL-адреса, указанные при настройке IWebHost. Обратите внимание, что это применимо только tooWebListener.

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a>Служба ASP.NET Core без отслеживания состояния только для внутреннего использования
Службы без сохранения состояния, которые вызываются только из внутри кластера hello должен использовать уникальный URL-адреса и динамически назначаемые порты tooensure взаимодействие между несколькими службами. рекомендуется следующая конфигурация Hello:

|  |  | **Примечания** |
| --- | --- | --- |
| Веб-сервер | Kestrel | Несмотря на то, что WebListener может использоваться для внутренней службы без сохранения состояния, Kestrel является hello рекомендуется server tooallow несколько tooshare экземпляров службы узла.  |
| Конфигурация порта | динамическое назначение | Множество реплик службы с отслеживанием состояния могут совместно использовать хост-процесс или операционную систему, и поэтому для них требуются уникальные порты. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Динамическое назначение порта этот параметр запрещает проблема с идентификацией hello ошибочно описано выше. |
| InstanceCount | любой | необходимые toooperate hello tooany значение службы можно задать значение количества экземпляров Hello. |

### <a name="internal-only-stateful-aspnet-core-service"></a>Служба ASP.NET Core с отслеживанием состояния только для внутреннего использования
С отслеживанием состояния служб, которые вызываются только из внутри кластера hello следует использовать динамически назначаемые порты tooensure взаимодействие между несколькими службами. рекомендуется следующая конфигурация Hello:

|  |  | **Примечания** |
| --- | --- | --- |
| Веб-сервер | Kestrel | Hello `WebListenerCommunicationListener` не предназначен для использования служб с отслеживанием состояния, в которых реплики совместно используют хост-процесса. |
| Конфигурация порта | динамическое назначение | Множество реплик службы с отслеживанием состояния могут совместно использовать хост-процесс или операционную систему, и поэтому для них требуются уникальные порты. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Динамическое назначение порта этот параметр запрещает проблема с идентификацией hello ошибочно описано выше. |

## <a name="next-steps"></a>Дальнейшие действия
[Отладка приложения Service Fabric с помощью Visual Studio](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
