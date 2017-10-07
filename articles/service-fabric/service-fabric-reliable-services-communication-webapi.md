---
title: "aaaService связь с веб-API ASP.NET hello | Документы Microsoft"
description: "Узнайте, как с помощью пошаговые связь со службой tooimplement hello веб-API ASP.NET с OWIN Резидентное размещение в hello надежные API служб."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Приступая к работе со службами веб-API Service Fabric с саморазмещением OWIN
Azure Service Fabric помещает hello power в руках, когда нужно решить, как будет toocommunicate вашей службы с пользователями и друг с другом. Это руководство посвящено реализации взаимодействия служб с помощью веб-API ASP.NET с саморазмещением Open Web Interface for .NET (OWIN) в API Reliable Services на платформе Service Fabric. Мы будем глубокое понимание hello подключаемые связи надежные службы API. Мы будем использовать веб-API в tooshow пошаговый пример вы как tooset слушателя пользовательского взаимодействия.

## <a name="introduction-tooweb-api-in-service-fabric"></a>Введение tooWeb API в Service Fabric
Веб-API ASP.NET — популярный и мощная платформа для создания HTTP API-интерфейсы поверх hello .NET Framework. Если вы не знакомы с hello framework, см. раздел [Приступая к работе с ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn дополнительные.

Веб-API в Service Fabric hello же веб-API ASP.NET вы хорошо знакомую и любимую. Hello различие заключается в том, как вы *узла* приложения веб-API. Этот процесс не предусматривает использование Microsoft IIS. toobetter понять разницу hello, давайте разбить на две части:

1. Hello веб-API приложения (включая контроллеры и модели)
2. узел Hello (hello веб-сервера, обычно IIS)

Само приложение веб-API не меняется. Оно ничем не отличается от веб-API приложения, созданные в предыдущих hello и должен быть перемещения может toosimply через большую часть кода приложения. Но если размещения в IIS, используется для размещения приложения hello может быть немного отличается от том, что вы привыкли. Прежде чем мы получаем toohello размещение часть, начнем с чего-либо более привычной: hello приложения веб-API.

## <a name="create-hello-application"></a>Создание приложения hello
Для начала создайте в Visual Studio 2015 приложение Service Fabric с одной службой без отслеживания состояния.

Шаблон Visual Studio для службы без отслеживания состояния, с помощью веб-API — доступные tooyou. В этом руководстве мы с нуля создадим проект веб-API, который покажет, какие результаты можно получить, выбрав этот шаблон.

Выберите пустой проект toolearn службы без отслеживания состояния как toobuild проект веб-API с нуля, или начала можно использовать службы без отслеживания состояния hello шаблона веб-API и следуйте.  

Hello первым шагом является toopull в некоторые пакеты NuGet для веб-API. пакет Hello, мы хотим toouse — Microsoft.AspNet.WebApi.OwinSelfHost. Этот пакет содержит все необходимые пакеты веб-API hello и hello *узла* пакетов. Это будет важно в дальнейшем.

После установки пакетов hello можно начать создавать hello базовая структура проекта веб-API. Если используется веб-API, структура проекта hello похожа на. Начните с добавления каталога `Controllers` и контроллера простых значений.

**ValuesController.cs**

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

Добавьте класс запуска на корневой tooregister hello проекта hello маршрутизации, форматирования и настройки установки. Это также где подключает веб-API toohello *узла*, которой будет пересмотрено попытку позже. 

**Startup.cs.**

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

Вот и все части приложения hello. На этом этапе мы настроили просто hello основные веб-API макет проекта. Таким образом не должен выглядеть сильно отличается от проектов веб-API, которые в прошлом hello вы написали или от hello базового шаблона веб-API. Бизнес-логики попадают в контроллерах hello и модели в обычном режиме.

Какие шаги по размещению следует выполнить для реального запуска?

## <a name="service-hosting"></a>Размещение службы
В Service Fabric служба запускается в *хост-процессе службы*— исполняемом файле, который выполняет код службы. При написании службы с помощью hello надежные API служб проект службы просто компилирует tooan исполняемый файл, который регистрирует тип службы и выполняет код. Так происходит в большинстве случаев при написании службы для Service Fabric на платформе .NET. При открытии Program.cs в проекте службы без отслеживания состояния hello, вы увидите:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Если выглядящий подозрительно hello запись точки tooa консольного приложения, то, так как он является.

Дополнительные сведения об hello хост-процесса службы и службы регистрации выходят за рамки данной статьи hello. Но это tooknow важные для теперь, когда *код службы выполняется в собственном процессе*.

## <a name="self-host-web-api-with-an-owin-host"></a>Саморазмещение веб-API с использованием хоста OWIN
Учитывая, что код приложения веб-API размещается в отдельном процессе, как подсоединить его tooa веб-сервер? Для этого есть [OWIN](http://owin.org/). OWIN — это просто контракт между веб-приложениями .NET и веб-серверами. В большинстве случаев при использовании ASP.NET (вверх tooMVC 5) hello веб-приложения является тесно связанные tooIIS через System.Web. Однако веб-API реализует OWIN, можно создать веб-приложение, которое связано с hello веб-сервера, на котором она размещена. Таким образом вы можете использовать *тестовый* веб-сервер OWIN, который можно запускать отдельным процессом. Это идеально подходит с hello Service Fabric модели размещения которых мы писали выше.

В этой статье мы будем использовать Katana как hello OWIN узла для веб-API приложения hello. Katana представляет собой реализацию узла OWIN открытым исходным кодом, построенных на [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) и hello Windows [API HTTP-сервера](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> Дополнительные сведения о Katana, последовательно выберите toohello toolearn [Katana сайта](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Краткий обзор того, как toouse Katana tooself узла веб-API, в разделе [OWIN используйте tooSelf узла веб-API ASP.NET 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-hello-web-server"></a>Установить веб-сервер hello
Hello надежные API служб предоставляет точку входа связи, где можно подключить стеками связи, позволяющие пользователям и клиентам tooconnect toohello службы:

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

Hello веб-сервера (и другие стек связи, используемого в будущем, таких как WebSockets hello) следует использовать интерфейс toointegrate hello ICommunicationListener правильно с системой hello. Hello причины этого станет яснее в hello следующие шаги.

Сначала создайте класс с именем OwinCommunicationListener, который реализует ICommunicationListener:

**OwinCommunicationListener.cs**

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

интерфейс ICommunicationListener Hello предоставляет три toomanage методы прослушиватель связи для службы:

* *OpenAsync* запуск прослушивания запросов.
* *CloseAsync* остановка прослушивания запросов, завершение всех активных запросов и правильное завершение работы.
* *Abort* отмена всех операций и немедленная остановка.

tooget к работе, добавьте закрытым членам класса, для прослушивателя hello действий потребуется toofunction. Они будет инициализирована при помощи конструктора hello и использовать при настройке hello прослушивания URL-адрес.

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a>Реализация OpenAsync
tooset копирование hello веб-сервера необходимы два блока данных:

* *Префикс пути URL-адреса*. Хотя это необязательно, это хорошо подходит для вас tooset этого теперь вверх, чтобы безопасно размещать несколько веб-служб в приложении.
* *Порт*.

Прежде чем вы получить порт для веб-сервера hello, важно понимать, что Service Fabric предоставляет слой приложений, который служит буфером между приложением и hello базовой операционной системы, на котором работает. Таким образом, Service Fabric предоставляет tooconfigure способом *конечные точки* для служб. Service Fabric гарантирует, что конечные точки будут доступны для toouse вашей службы. Таким образом, не имеют tooconfigure их самостоятельно в hello базовой среды операционной системы. Можно легко размещать приложения Service Fabric в разных средах без необходимости toomake tooyour любого изменения приложения. (Например, можно разместить hello одного приложения в Azure или в собственном центре обработки данных.)

Настройте конечную точку HTTP в файле PackageRoot\ServiceManifest.xml:

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Этот шаг важен, так как выполняется хост-процесса службы hello ограниченными учетными данными (Network Service в Windows). Это означает, что служба не будет иметь доступ tooset доступ к конечной точке HTTP сам по себе. С помощью конфигурации конечной точки hello, Service Fabric знает tooset копирование hello правильный список управления доступом (ACL) для hello, который будет прослушивать URL-адрес, hello службы. Service Fabric также предоставляет стандартный место tooconfigure конечных точек.

Теперь в OwinCommunicationListener.cs можно начать реализацию OpenAsync. Это связано с начала hello веб-сервера. Во-первых получать сведения о конечных точках hello и создавать hello URL-адрес, который будет прослушивать служба hello. Hello URL-адрес будет различаться в зависимости от того, используется ли прослушиватель hello в службы без отслеживания состояния или службы с отслеживанием состояния. Для службы с отслеживанием состояния hello прослушивателю toocreate уникальный адрес для каждой реплики службы с отслеживанием состояния он прослушивает. Для службы без сохранения состояния hello адрес может быть гораздо проще. 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

Обратите внимание, что здесь используется адрес «http://+». Это toomake том, что этот hello веб-сервер прослушивает все доступные адреса, включая localhost, полное доменное имя или IP-машины hello.

Hello OpenAsync реализация является одной из важнейших причин hello почему hello веб-сервер (или любой стек связи) реализуется как ICommunicationListener, а не только его открытия непосредственно из `RunAsync()` в службе hello. Hello возвращает OpenAsync значение что прослушивает адрес hello, hello веб-сервера. При возвращении этот адрес toohello системы, он регистрирует адрес hello hello службе. Service Fabric предоставляет API, который позволяет клиентам и других служб toothen запрашивает этот адрес по имени службы. Это важно, потому что адресом службы hello не является статическим. Службы будут перемещены в кластере hello в целях балансировки и доступности ресурсов. Это механизм hello, которая позволяет клиентам tooresolve Здравствуй прослушивает адрес службы.

С учетом OpenAsync начинается hello веб-сервера и возвращает адрес hello, который он прослушивает. Обратите внимание, прослушивает «http://+», но перед OpenAsync возвращает адрес hello, Здравствуйте, «+» заменяется hello IP-адрес или полное доменное имя hello узла, на котором она расположена в настоящее время. Hello адрес, который возвращается этим методом является то, что зарегистрирован в системе hello. Его увидят клиенты и другие службы при запросе адреса службы. Для клиентов toocorrectly подключения tooit, они должны фактических IP-адрес или полное доменное имя в адрес hello.

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

Обратите внимание, что это ссылается на класс запуска hello, который был передан в toohello OwinCommunicationListener в конструкторе hello. Этот экземпляр запуска используется hello web server toobootstrap hello приложения веб-API.

Hello `ServiceEventSource.Current.Message()` строке будет отображаться в окне событий диагностики hello позже, при запуске приложения tooconfirm hello hello веб-сервера успешно запущена.

## <a name="implement-closeasync-and-abort"></a>Реализация CloseAsync и Abort
Наконец, реализации CloseAsync и Abort toostop hello веб-сервера. Hello веб-сервер может быть остановлена, удалив hello server дескриптор, который был создан во время OpenAsync.

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

В этом примере реализация CloseAsync и Abort просто остановить hello веб-сервера. Вы можете отказаться от tooperform более легко скоординированного выключение hello веб-сервера в CloseAsync. Например hello завершение работы может ожидать завершилось, прежде чем вернуть hello toobe активных запросов.

## <a name="start-hello-web-server"></a>Запустите веб-сервер hello
Теперь вы готовы toocreate и возвращать экземпляр OwinCommunicationListener toostart hello веб-сервера. Обратно в hello класс службы (WebService.cs), переопределите hello `CreateServiceInstanceListeners()` метод:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

Это где hello веб-API *приложения* и hello OWIN *узла* наконец соответствуют. Получает экземпляр hello Hello узла (OwinCommunicationListener) *приложения* (веб-API) через hello класс запуска. Его жизненным циклом управляет Service Fabric. Такого же шаблона можно придерживаться при использовании любого стека связи.

## <a name="put-it-all-together"></a>Сборка
В этом примере не требуется toodo что-либо в hello `RunAsync()` метода, так что переопределение просто может быть удалено.

Реализация Hello окончательного службы должны быть очень простыми. Требуется только toocreate hello связи прослушиватель:

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

Полный Hello `OwinCommunicationListener` класса:

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

Теперь, когда все составляющие hello поместил в месте, проекта должен выглядеть типичное приложение веб-API с узлом OWIN и надежные API служб точки входа.

## <a name="run-and-connect-through-a-web-browser"></a>Запуск и подключение через веб-браузер
Если это еще не сделано, [настройте среду разработки](service-fabric-get-started.md).

Теперь можно построить и развернуть службу. Нажмите клавишу **F5** в toobuild Visual Studio и развертывать приложение hello. В окне приветствия события диагностики, вы увидите сообщение, указывающее, открыт на http://localhost:8281 веб-сервера hello /.

> [!NOTE]
> Если hello порт уже открыт другим процессом на компьютере, появится сообщение об ошибке. Это означает, что не удалось открыть прослушиватель hello. Если это так hello, попробуйте использовать другой порт для hello конфигурации конечной точки в файле ServiceManifest.xml.
> 
> 

После установки службы hello, откройте браузер и перейдите в слишком[http://localhost:8281, значения или api](http://localhost:8281/api/values) tootest его.

## <a name="scale-it-out"></a>Масштабирование
Горизонтальное масштабирование без сохранения состояния веб-приложений обычно означает добавление нескольких компьютеров и скорость hello веб-приложений на них вращения. Service Fabric orchestration engine это можно сделать для вас при каждом добавлении новых узлов кластера tooa. При создании экземпляров службы без сохранения состояния, можно указать номер hello экземпляров требуется toocreate. Service Fabric помещает соответствующее количество экземпляров на узлах в кластере hello. И он проверяет toocreate не более одного экземпляра на любом узле. Можно также указать tooalways Service Fabric создавать экземпляры на каждом узле, указав **-1** по количеству экземпляров hello. Это гарантирует, что при каждом добавлении tooscale узлы из кластера экземпляра без сохранения состояния службы создается на новых узлах hello. Это значение является свойством экземпляра службы hello, поэтому оно задается при создании экземпляра службы. Его можно задать с помощью PowerShell:

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

Его также можно задать при определении службы по умолчанию в проекте службы без отслеживания состояния в Visual Studio.

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

Дополнительные сведения о статье toocreate приложений и экземпляров службы [развернуть приложение](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Дальнейшие действия
[Отладка приложения Service Fabric с помощью Visual Studio](service-fabric-debugging-your-application.md)

