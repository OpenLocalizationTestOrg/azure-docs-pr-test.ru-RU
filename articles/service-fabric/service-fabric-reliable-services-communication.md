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
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Как toouse hello надежные службы связи API-интерфейсы
Обмен данными между службами совершенно не влияет на работу платформы Azure Service Fabric. Все протоколы и стеки являются допустимыми, из UDP tooHTTP. Он работает toochoose разработчика службы toohello взаимодействие служб. Платформа приложения Hello надежные службы предоставляет встроенного соединения с накоплением и API-интерфейсы, которые можно использовать toobuild компоненты пользовательского взаимодействия.

## <a name="set-up-service-communication"></a>Настройка обмена данными между службами
Hello надежные API служб использует простой интерфейс для взаимодействия служб. просто tooopen конечную точку для службы, реализация этого интерфейса:

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

Затем добавьте реализацию прослушивателя связи, вернув его в переопределении метода класса на основе службы.

Для служб без отслеживания состояния:

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

Для служб с отслеживанием состояния:

> [!NOTE]
> Сейчас Java не поддерживает службы Reliable Services с отслеживанием состояния.
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

В обоих случаях возвращается коллекция прослушивателей. Это позволяет вашей службы toolisten несколько конечных точек, потенциально по разным протоколам, с помощью нескольких прослушивателей. Например, можно использовать прослушиватель HTTP и отдельный прослушиватель WebSocket. Каждый прослушиватель получает имя и hello результирующей коллекцией *имя: адрес* пары представляются в виде объекта JSON, когда клиент запрашивает hello адреса ожидания передачи данных для экземпляра службы или секции.

В службы без отслеживания состояния переопределение hello возвращает коллекцию ServiceInstanceListeners. Объект `ServiceInstanceListener` содержит toocreate функция `ICommunicationListener(C#) / CommunicationListener(Java)` и присваивает ему имя. Для служб с отслеживанием состояния переопределение hello возвращает коллекцию ServiceReplicaListeners. Это немного отличается от аналога без сохранения состояния, так как `ServiceReplicaListener` имеет параметр tooopen `ICommunicationListener` во вторичных репликах. Это позволяет не только использовать несколько прослушивателей связи в одной службе, но также указывать, какие прослушиватели принимают запросы для вторичных реплик, а какие — прослушивают только первичные реплики.

Например, у вас есть прослушиватель ServiceRemotingListener, который принимает вызовы RPC только для первичных реплик, и настраиваемый прослушиватель, который принимает запросы на чтение для вторичных реплик по протоколу HTTP:

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
> При создании нескольких прослушивателей для службы каждому прослушивателю **необходимо** присвоить уникальное имя.
>
>

Наконец, описывающие hello конечных точек, которые требуются для службы hello в hello [манифест службы](service-fabric-application-model.md) в разделе "hello" в конечных точках.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

прослушиватель Hello связи могут обращаться к ресурсам hello конечной точки, выделенных tooit из hello `CodePackageActivationContext` в hello `ServiceContext`. Hello прослушивателя, затем можно запустить прослушивание запросов при его открытии.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Конечная точка ресурсы общих toohello всей службы пакета и они выделяются с помощью Service Fabric при активации пакета службы hello. Несколько реплик службы, размещенной в hello, могут совместно использовать одинаковые ServiceHost hello же порт. Это означает, что прослушиватель hello связи должны поддерживать совместное использование порта. Это можно сделать — для hello связи прослушивателя toouse hello секции идентификатор и идентификатор реплики или экземпляра при формировании адреса прослушивания hello рекомендуемые Hello.
>
>

### <a name="service-address-registration"></a>Регистрация адреса службы
Системная служба вызывается hello *службы имен* работает на кластеров Service Fabric. Hello службы имен является регистратор служб и их адреса, которые прослушивает каждого экземпляра или реплики службы hello. Здравствуйте, когда `OpenAsync(C#) / openAsync(Java)` метод `ICommunicationListener(C#) / CommunicationListener(Java)` завершения его возвращаемый значение возвращает зарегистрирован в hello Naming Service. Это возвращает значение, которое возвращает строку, значение которого может быть любым во всех опубликованных в hello именования в службе. Это строковое значение определяет, видят клиенты при просят для адреса службе hello hello Naming Service.

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

Service Fabric предоставляет API-интерфейсы, позволяющие клиентам и других служб toothen запрашивает этот адрес по имени службы. Это важно, потому что адресом службы hello не является статическим. Службы будут перемещены в кластере hello в целях балансировки и доступности ресурсов. Это механизм hello, разрешить клиентам tooresolve Здравствуй прослушивает адрес службы.

> [!NOTE]
> Полное Пошаговое руководство для toowrite прослушиватель связи. в статье [веб-API службы фабрики служб с резидентным OWIN](service-fabric-reliable-services-communication-webapi.md) C#, в то время как для Java можно написать собственную реализацию сервера HTTP, в разделе EchoServer приложения Пример в https://github.com/Azure-Samples/service-fabric-java-getting-started.
>
>

## <a name="communicating-with-a-service"></a>Взаимодействие со службой
Hello надежные API службы предоставляет следующие библиотеки toowrite клиентов, взаимодействующих со службами hello.

### <a name="service-endpoint-resolution"></a>Разрешение конечной точки службы
Hello первый шаг toocommunication со службой — tooresolve hello секции или экземпляр службы hello нужные tootalk для адреса конечной точки. Hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` служебный класс имеет базовый примитив, который позволяет клиентам определить hello конечную точку службы во время выполнения. В терминологии Service Fabric hello процесс определения hello конечную точку службы — hello ссылка tooas *разрешения конечной точки службы*.

tooservices tooconnect в кластере, ServicePartitionResolver могут создаваться с использованием параметров по умолчанию. Это hello, рекомендуется использование в большинстве ситуаций:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooservices tooconnect в другом кластере, ServicePartitionResolver создаются с помощью набора конечных точек кластера шлюза. Обратите внимание, что конечные точки шлюза просто различные конечные точки для подключения toohello одного кластера. Например:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

Кроме того `ServicePartitionResolver` можно задать функцию для создания `FabricClient` toouse внутренним образом:

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

`FabricClient`Представляет объект hello, используемые toocommunicate с hello кластера Service Fabric для выполнения различных операций управления на кластере hello. Это полезно, когда требуется больший контроль над тем, как класс ServicePartitionResolver взаимодействует с кластером. `FabricClient`выполняет кэширование внутренним образом и является обычно предъявляют toocreate, поэтому очень важно tooreuse `FabricClient` максимально экземпляров.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

Разрешения метода, то используется tooretrieve hello адрес службы или служебного раздела для секционированных служб.

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

Адрес службы можно устранить с помощью ServicePartitionResolver, но больше работы требуется tooensure hello разрешить адрес может быть использован неправильно. Клиент должен toodetect ли попытка подключения hello сбой из-за временной ошибки и могут быть повторены (например, служба перемещен или временно недоступен), или постоянной ошибкой (например, служба была удалена или hello запрошенный ресурс больше не существует). Экземпляры или реплики службы могут перемещаться из toonode узла в любое время по нескольким причинам. Код клиента пытается tooconnect времени hello Hello адрес службы, разрешаются с помощью ServicePartitionResolver может быть устаревшим. В этом случае снова hello клиенту адрес hello toore разрешения. Предоставление hello предыдущих `ResolvedServicePartition` указывает, hello tootry потребностей Сопоставитель еще раз, а не просто получить кэшированных адресов.

Как правило hello клиентского кода должны недоступны hello ServicePartitionResolver напрямую. Он создается и передается на toocommunication фабрик клиента в hello надежные API служб. Hello фабрики для внутреннего использования распознавателя hello toogenerate клиентского объекта, который можно использовать toocommunicate со службами.

### <a name="communication-clients-and-factories"></a>Клиенты и фабрики связи
Библиотека фабрики связи Hello реализует типичный шаблон повторных попыток обработки сбоев, облегчающая конечных точек службы выполняется повторная попытка подключения tooresolved. Библиотека фабрики Hello предоставляет механизм повторов hello, предоставляют обработчики ошибок hello.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Определяет hello базовый интерфейс, реализуемый связи клиента фабрику, которая создает клиентов, которые могут взаимодействовать tooa служба Service Fabric. Здравствуйте, реализация hello CommunicationClientFactory зависит от используемой службой Service Fabric hello, где hello клиенту toocommunicate стек связи hello. Hello надежные API служб предоставляет `CommunicationClientFactoryBase<TCommunicationClient>`. Это предоставляет базовую реализацию интерфейса CommunicationClientFactory hello и выполняет задачи, общие стеками связи tooall hello. (Эти задачи включают в себя использование toodetermine ServicePartitionResolver hello конечной точки службы). Клиенты обычно применение hello абстрактный CommunicationClientFactoryBase класса toohandle, определенного toohello стека связи.

Hello связи клиента просто получает адрес и использует его tooconnect tooa службы. Hello клиент может использовать любой протокол, ему.

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

Фабрика клиента Hello в основном отвечает за создание связи клиентов. Для клиентов, которые не поддерживать постоянное подключение, таких как HTTP-клиента фабрика hello достаточно toocreate и возврата hello клиента. Другие протоколы, позволяющие поддерживать постоянное подключение, таких как некоторые двоичные протоколы, также должен быть проверен с toodetermine фабрики hello ли подключение hello должно toobe при повторном создании.  

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

Наконец обработчик исключений отвечает за определение tootake какие действия при возникновении исключения. Исключения делятся на **повторяемые** и **неповторяемые**.

* **Без возможности повторной попытки** исключения просто получить повторно задней toohello вызывающего объекта.
* **Повторяемые** исключения далее классифицируются как **временные** и **невременные**.
  * **Временные** исключения, которые могут быть повторены просто без повторного разрешения hello адрес конечной точки службы. Сюда относится временных проблем с сетью или сообщения об ошибках службы, отличных от тех, которые указывают на адрес конечной точки службы hello не существует.
  * **Не временной** исключения, которые требуется повторно разрешить адрес toobe hello службы конечной точки. К ним относятся исключения, указывающие, что конечная точка службы hello не удалось связаться, о том, что служба hello перемещено tooa другой узел.

Hello `TryHandleException` принимает решение о данного исключения. Если он **не знает** toomake какие решения об исключении, он должен возвращать **false**. Если он **знать** какие toomake принятия решений, оно должно соответствующим образом задать результат hello и вернуть **true**.

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
### <a name="putting-it-all-together"></a>Сборка
С `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, и `IExceptionHandler(C#) / ExceptionHandler(Java)` построенная на основе протокола связи, `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` создает оболочку вместе, а также обработки сбоев hello и цикл разрешение адрес раздела службы вокруг этих компонентов.

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

## <a name="next-steps"></a>Дальнейшие действия
* Пример обмена данными по протоколу HTTP между службами представлен в [примере проекта C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) или [Java на сайте GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Удаленное взаимодействие службы с Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [Начало работы со службами веб-API Microsoft Azure Service Fabric с саморазмещением OWIN](service-fabric-reliable-services-communication-webapi.md)
* [Коммуникационный стек WCF для надежных служб](service-fabric-reliable-services-communication-wcf.md)
