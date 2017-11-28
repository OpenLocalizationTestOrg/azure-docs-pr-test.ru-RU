---
title: "Общие сведения о связи служб aaaReliable | Документы Microsoft"
description: "Обзор модель взаимодействия hello надежные службы, включая открытие прослушивателей для служб, разрешает конечные точки и взаимодействия между службами."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="65c94-103">Как toouse hello надежные службы связи API-интерфейсы</span><span class="sxs-lookup"><span data-stu-id="65c94-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="65c94-104">Обмен данными между службами совершенно не влияет на работу платформы Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="65c94-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="65c94-105">Все протоколы и стеки являются допустимыми, из UDP tooHTTP.</span><span class="sxs-lookup"><span data-stu-id="65c94-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="65c94-106">Он работает toochoose разработчика службы toohello взаимодействие служб.</span><span class="sxs-lookup"><span data-stu-id="65c94-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="65c94-107">Платформа приложения Hello надежные службы предоставляет встроенного соединения с накоплением и API-интерфейсы, которые можно использовать toobuild компоненты пользовательского взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="65c94-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="65c94-108">Настройка обмена данными между службами</span><span class="sxs-lookup"><span data-stu-id="65c94-108">Set up service communication</span></span>
<span data-ttu-id="65c94-109">Hello надежные API служб использует простой интерфейс для взаимодействия служб.</span><span class="sxs-lookup"><span data-stu-id="65c94-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="65c94-110">просто tooopen конечную точку для службы, реализация этого интерфейса:</span><span class="sxs-lookup"><span data-stu-id="65c94-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="65c94-111">Затем добавьте реализацию прослушивателя связи, вернув его в переопределении метода класса на основе службы.</span><span class="sxs-lookup"><span data-stu-id="65c94-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="65c94-112">Для служб без отслеживания состояния:</span><span class="sxs-lookup"><span data-stu-id="65c94-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="65c94-113">Для служб с отслеживанием состояния:</span><span class="sxs-lookup"><span data-stu-id="65c94-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="65c94-114">Сейчас Java не поддерживает службы Reliable Services с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="65c94-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="65c94-115">В обоих случаях возвращается коллекция прослушивателей.</span><span class="sxs-lookup"><span data-stu-id="65c94-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="65c94-116">Это позволяет вашей службы toolisten несколько конечных точек, потенциально по разным протоколам, с помощью нескольких прослушивателей.</span><span class="sxs-lookup"><span data-stu-id="65c94-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="65c94-117">Например, можно использовать прослушиватель HTTP и отдельный прослушиватель WebSocket.</span><span class="sxs-lookup"><span data-stu-id="65c94-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="65c94-118">Каждый прослушиватель получает имя и hello результирующей коллекцией *имя: адрес* пары представляются в виде объекта JSON, когда клиент запрашивает hello адреса ожидания передачи данных для экземпляра службы или секции.</span><span class="sxs-lookup"><span data-stu-id="65c94-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="65c94-119">В службы без отслеживания состояния переопределение hello возвращает коллекцию ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="65c94-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="65c94-120">Объект `ServiceInstanceListener` содержит toocreate функция `ICommunicationListener(C#) / CommunicationListener(Java)` и присваивает ему имя.</span><span class="sxs-lookup"><span data-stu-id="65c94-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="65c94-121">Для служб с отслеживанием состояния переопределение hello возвращает коллекцию ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="65c94-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="65c94-122">Это немного отличается от аналога без сохранения состояния, так как `ServiceReplicaListener` имеет параметр tooopen `ICommunicationListener` во вторичных репликах.</span><span class="sxs-lookup"><span data-stu-id="65c94-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="65c94-123">Это позволяет не только использовать несколько прослушивателей связи в одной службе, но также указывать, какие прослушиватели принимают запросы для вторичных реплик, а какие — прослушивают только первичные реплики.</span><span class="sxs-lookup"><span data-stu-id="65c94-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="65c94-124">Например, у вас есть прослушиватель ServiceRemotingListener, который принимает вызовы RPC только для первичных реплик, и настраиваемый прослушиватель, который принимает запросы на чтение для вторичных реплик по протоколу HTTP:</span><span class="sxs-lookup"><span data-stu-id="65c94-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="65c94-125">При создании нескольких прослушивателей для службы каждому прослушивателю **необходимо** присвоить уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="65c94-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="65c94-126">Наконец, описывающие hello конечных точек, которые требуются для службы hello в hello [манифест службы](service-fabric-application-model.md) в разделе "hello" в конечных точках.</span><span class="sxs-lookup"><span data-stu-id="65c94-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="65c94-127">прослушиватель Hello связи могут обращаться к ресурсам hello конечной точки, выделенных tooit из hello `CodePackageActivationContext` в hello `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="65c94-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="65c94-128">Hello прослушивателя, затем можно запустить прослушивание запросов при его открытии.</span><span class="sxs-lookup"><span data-stu-id="65c94-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="65c94-129">Конечная точка ресурсы общих toohello всей службы пакета и они выделяются с помощью Service Fabric при активации пакета службы hello.</span><span class="sxs-lookup"><span data-stu-id="65c94-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="65c94-130">Несколько реплик службы, размещенной в hello, могут совместно использовать одинаковые ServiceHost hello же порт.</span><span class="sxs-lookup"><span data-stu-id="65c94-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="65c94-131">Это означает, что прослушиватель hello связи должны поддерживать совместное использование порта.</span><span class="sxs-lookup"><span data-stu-id="65c94-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="65c94-132">Это можно сделать — для hello связи прослушивателя toouse hello секции идентификатор и идентификатор реплики или экземпляра при формировании адреса прослушивания hello рекомендуемые Hello.</span><span class="sxs-lookup"><span data-stu-id="65c94-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="65c94-133">Регистрация адреса службы</span><span class="sxs-lookup"><span data-stu-id="65c94-133">Service address registration</span></span>
<span data-ttu-id="65c94-134">Системная служба вызывается hello *службы имен* работает на кластеров Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="65c94-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="65c94-135">Hello службы имен является регистратор служб и их адреса, которые прослушивает каждого экземпляра или реплики службы hello.</span><span class="sxs-lookup"><span data-stu-id="65c94-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="65c94-136">Здравствуйте, когда `OpenAsync(C#) / openAsync(Java)` метод `ICommunicationListener(C#) / CommunicationListener(Java)` завершения его возвращаемый значение возвращает зарегистрирован в hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="65c94-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="65c94-137">Это возвращает значение, которое возвращает строку, значение которого может быть любым во всех опубликованных в hello именования в службе.</span><span class="sxs-lookup"><span data-stu-id="65c94-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="65c94-138">Это строковое значение определяет, видят клиенты при просят для адреса службе hello hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="65c94-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="65c94-139">Service Fabric предоставляет API-интерфейсы, позволяющие клиентам и других служб toothen запрашивает этот адрес по имени службы.</span><span class="sxs-lookup"><span data-stu-id="65c94-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="65c94-140">Это важно, потому что адресом службы hello не является статическим.</span><span class="sxs-lookup"><span data-stu-id="65c94-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="65c94-141">Службы будут перемещены в кластере hello в целях балансировки и доступности ресурсов.</span><span class="sxs-lookup"><span data-stu-id="65c94-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="65c94-142">Это механизм hello, разрешить клиентам tooresolve Здравствуй прослушивает адрес службы.</span><span class="sxs-lookup"><span data-stu-id="65c94-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="65c94-143">Полное Пошаговое руководство для toowrite прослушиватель связи. в статье [веб-API службы фабрики служб с резидентным OWIN](service-fabric-reliable-services-communication-webapi.md) C#, в то время как для Java можно написать собственную реализацию сервера HTTP, в разделе EchoServer приложения Пример в https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="65c94-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="65c94-144">Взаимодействие со службой</span><span class="sxs-lookup"><span data-stu-id="65c94-144">Communicating with a service</span></span>
<span data-ttu-id="65c94-145">Hello надежные API службы предоставляет следующие библиотеки toowrite клиентов, взаимодействующих со службами hello.</span><span class="sxs-lookup"><span data-stu-id="65c94-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="65c94-146">Разрешение конечной точки службы</span><span class="sxs-lookup"><span data-stu-id="65c94-146">Service endpoint resolution</span></span>
<span data-ttu-id="65c94-147">Hello первый шаг toocommunication со службой — tooresolve hello секции или экземпляр службы hello нужные tootalk для адреса конечной точки.</span><span class="sxs-lookup"><span data-stu-id="65c94-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="65c94-148">Hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` служебный класс имеет базовый примитив, который позволяет клиентам определить hello конечную точку службы во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="65c94-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="65c94-149">В терминологии Service Fabric hello процесс определения hello конечную точку службы — hello ссылка tooas *разрешения конечной точки службы*.</span><span class="sxs-lookup"><span data-stu-id="65c94-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="65c94-150">tooservices tooconnect в кластере, ServicePartitionResolver могут создаваться с использованием параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="65c94-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="65c94-151">Это hello, рекомендуется использование в большинстве ситуаций:</span><span class="sxs-lookup"><span data-stu-id="65c94-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="65c94-152">tooservices tooconnect в другом кластере, ServicePartitionResolver создаются с помощью набора конечных точек кластера шлюза.</span><span class="sxs-lookup"><span data-stu-id="65c94-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="65c94-153">Обратите внимание, что конечные точки шлюза просто различные конечные точки для подключения toohello одного кластера.</span><span class="sxs-lookup"><span data-stu-id="65c94-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="65c94-154">Например:</span><span class="sxs-lookup"><span data-stu-id="65c94-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="65c94-155">Кроме того `ServicePartitionResolver` можно задать функцию для создания `FabricClient` toouse внутренним образом:</span><span class="sxs-lookup"><span data-stu-id="65c94-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="65c94-156">`FabricClient`Представляет объект hello, используемые toocommunicate с hello кластера Service Fabric для выполнения различных операций управления на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="65c94-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="65c94-157">Это полезно, когда требуется больший контроль над тем, как класс ServicePartitionResolver взаимодействует с кластером.</span><span class="sxs-lookup"><span data-stu-id="65c94-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="65c94-158">`FabricClient`выполняет кэширование внутренним образом и является обычно предъявляют toocreate, поэтому очень важно tooreuse `FabricClient` максимально экземпляров.</span><span class="sxs-lookup"><span data-stu-id="65c94-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="65c94-159">Разрешения метода, то используется tooretrieve hello адрес службы или служебного раздела для секционированных служб.</span><span class="sxs-lookup"><span data-stu-id="65c94-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="65c94-160">Адрес службы можно устранить с помощью ServicePartitionResolver, но больше работы требуется tooensure hello разрешить адрес может быть использован неправильно.</span><span class="sxs-lookup"><span data-stu-id="65c94-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="65c94-161">Клиент должен toodetect ли попытка подключения hello сбой из-за временной ошибки и могут быть повторены (например, служба перемещен или временно недоступен), или постоянной ошибкой (например, служба была удалена или hello запрошенный ресурс больше не существует).</span><span class="sxs-lookup"><span data-stu-id="65c94-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="65c94-162">Экземпляры или реплики службы могут перемещаться из toonode узла в любое время по нескольким причинам.</span><span class="sxs-lookup"><span data-stu-id="65c94-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="65c94-163">Код клиента пытается tooconnect времени hello Hello адрес службы, разрешаются с помощью ServicePartitionResolver может быть устаревшим.</span><span class="sxs-lookup"><span data-stu-id="65c94-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="65c94-164">В этом случае снова hello клиенту адрес hello toore разрешения.</span><span class="sxs-lookup"><span data-stu-id="65c94-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="65c94-165">Предоставление hello предыдущих `ResolvedServicePartition` указывает, hello tootry потребностей Сопоставитель еще раз, а не просто получить кэшированных адресов.</span><span class="sxs-lookup"><span data-stu-id="65c94-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="65c94-166">Как правило hello клиентского кода должны недоступны hello ServicePartitionResolver напрямую.</span><span class="sxs-lookup"><span data-stu-id="65c94-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="65c94-167">Он создается и передается на toocommunication фабрик клиента в hello надежные API служб.</span><span class="sxs-lookup"><span data-stu-id="65c94-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="65c94-168">Hello фабрики для внутреннего использования распознавателя hello toogenerate клиентского объекта, который можно использовать toocommunicate со службами.</span><span class="sxs-lookup"><span data-stu-id="65c94-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="65c94-169">Клиенты и фабрики связи</span><span class="sxs-lookup"><span data-stu-id="65c94-169">Communication clients and factories</span></span>
<span data-ttu-id="65c94-170">Библиотека фабрики связи Hello реализует типичный шаблон повторных попыток обработки сбоев, облегчающая конечных точек службы выполняется повторная попытка подключения tooresolved.</span><span class="sxs-lookup"><span data-stu-id="65c94-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="65c94-171">Библиотека фабрики Hello предоставляет механизм повторов hello, предоставляют обработчики ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="65c94-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="65c94-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Определяет hello базовый интерфейс, реализуемый связи клиента фабрику, которая создает клиентов, которые могут взаимодействовать tooa служба Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="65c94-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="65c94-173">Здравствуйте, реализация hello CommunicationClientFactory зависит от используемой службой Service Fabric hello, где hello клиенту toocommunicate стек связи hello.</span><span class="sxs-lookup"><span data-stu-id="65c94-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="65c94-174">Hello надежные API служб предоставляет `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="65c94-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="65c94-175">Это предоставляет базовую реализацию интерфейса CommunicationClientFactory hello и выполняет задачи, общие стеками связи tooall hello.</span><span class="sxs-lookup"><span data-stu-id="65c94-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="65c94-176">(Эти задачи включают в себя использование toodetermine ServicePartitionResolver hello конечной точки службы).</span><span class="sxs-lookup"><span data-stu-id="65c94-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="65c94-177">Клиенты обычно применение hello абстрактный CommunicationClientFactoryBase класса toohandle, определенного toohello стека связи.</span><span class="sxs-lookup"><span data-stu-id="65c94-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="65c94-178">Hello связи клиента просто получает адрес и использует его tooconnect tooa службы.</span><span class="sxs-lookup"><span data-stu-id="65c94-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="65c94-179">Hello клиент может использовать любой протокол, ему.</span><span class="sxs-lookup"><span data-stu-id="65c94-179">hello client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="65c94-180">Фабрика клиента Hello в основном отвечает за создание связи клиентов.</span><span class="sxs-lookup"><span data-stu-id="65c94-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="65c94-181">Для клиентов, которые не поддерживать постоянное подключение, таких как HTTP-клиента фабрика hello достаточно toocreate и возврата hello клиента.</span><span class="sxs-lookup"><span data-stu-id="65c94-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="65c94-182">Другие протоколы, позволяющие поддерживать постоянное подключение, таких как некоторые двоичные протоколы, также должен быть проверен с toodetermine фабрики hello ли подключение hello должно toobe при повторном создании.</span><span class="sxs-lookup"><span data-stu-id="65c94-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="65c94-183">Наконец обработчик исключений отвечает за определение tootake какие действия при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="65c94-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="65c94-184">Исключения делятся на **повторяемые** и **неповторяемые**.</span><span class="sxs-lookup"><span data-stu-id="65c94-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="65c94-185">**Без возможности повторной попытки** исключения просто получить повторно задней toohello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="65c94-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="65c94-186">**Повторяемые** исключения далее классифицируются как **временные** и **невременные**.</span><span class="sxs-lookup"><span data-stu-id="65c94-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="65c94-187">**Временные** исключения, которые могут быть повторены просто без повторного разрешения hello адрес конечной точки службы.</span><span class="sxs-lookup"><span data-stu-id="65c94-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="65c94-188">Сюда относится временных проблем с сетью или сообщения об ошибках службы, отличных от тех, которые указывают на адрес конечной точки службы hello не существует.</span><span class="sxs-lookup"><span data-stu-id="65c94-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="65c94-189">**Не временной** исключения, которые требуется повторно разрешить адрес toobe hello службы конечной точки.</span><span class="sxs-lookup"><span data-stu-id="65c94-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="65c94-190">К ним относятся исключения, указывающие, что конечная точка службы hello не удалось связаться, о том, что служба hello перемещено tooa другой узел.</span><span class="sxs-lookup"><span data-stu-id="65c94-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="65c94-191">Hello `TryHandleException` принимает решение о данного исключения.</span><span class="sxs-lookup"><span data-stu-id="65c94-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="65c94-192">Если он **не знает** toomake какие решения об исключении, он должен возвращать **false**.</span><span class="sxs-lookup"><span data-stu-id="65c94-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="65c94-193">Если он **знать** какие toomake принятия решений, оно должно соответствующим образом задать результат hello и вернуть **true**.</span><span class="sxs-lookup"><span data-stu-id="65c94-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="65c94-194">Сборка</span><span class="sxs-lookup"><span data-stu-id="65c94-194">Putting it all together</span></span>
<span data-ttu-id="65c94-195">С `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, и `IExceptionHandler(C#) / ExceptionHandler(Java)` построенная на основе протокола связи, `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` создает оболочку вместе, а также обработки сбоев hello и цикл разрешение адрес раздела службы вокруг этих компонентов.</span><span class="sxs-lookup"><span data-stu-id="65c94-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="65c94-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65c94-196">Next steps</span></span>
* <span data-ttu-id="65c94-197">Пример обмена данными по протоколу HTTP между службами представлен в [примере проекта C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) или [Java на сайте GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="65c94-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="65c94-198">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="65c94-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="65c94-199">Начало работы со службами веб-API Microsoft Azure Service Fabric с саморазмещением OWIN</span><span class="sxs-lookup"><span data-stu-id="65c94-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="65c94-200">Коммуникационный стек WCF для надежных служб</span><span class="sxs-lookup"><span data-stu-id="65c94-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
