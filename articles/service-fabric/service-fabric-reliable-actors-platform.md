---
title: "Субъекты на Service Fabric aaaReliable | Документы Microsoft"
description: "Описывает, как службы Reliable Actor, располагаются на надежные службы и использовать функции hello платформы Service Fabric hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="0fff5-103">Использование службы Reliable Actor hello платформы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0fff5-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="0fff5-104">В этой статье объясняется, как работают службы Reliable Actor на платформе Azure Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="0fff5-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="0fff5-105">Запуск службы Reliable Actor в платформу, которая размещается в реализацию с отслеживанием состояния надежные службы с именем hello *службу субъектов*.</span><span class="sxs-lookup"><span data-stu-id="0fff5-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="0fff5-106">службу субъектов Hello содержит все hello toomanage необходимые компоненты hello, жизненный цикл и диспетчеризации для вашего субъекты сообщение:</span><span class="sxs-lookup"><span data-stu-id="0fff5-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="0fff5-107">Hello субъекта среда выполнения управляет жизненным циклом, сборщик мусора и регулирует доступ одним потоком.</span><span class="sxs-lookup"><span data-stu-id="0fff5-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="0fff5-108">Прослушиватель субъекта службы удаленного взаимодействия принимает вызовы tooactors удаленного доступа и отправляет их tooa диспетчер tooroute toohello субъект, соответствующий экземпляр.</span><span class="sxs-lookup"><span data-stu-id="0fff5-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="0fff5-109">Поставщик состояния субъекта Hello включает поставщики состояния (например, поставщик состояния hello надежного коллекций) и предоставляет адаптер для управления состоянием субъекта.</span><span class="sxs-lookup"><span data-stu-id="0fff5-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="0fff5-110">Эти компоненты вместе формы hello Reliable Actor framework.</span><span class="sxs-lookup"><span data-stu-id="0fff5-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="0fff5-111">Структура служб</span><span class="sxs-lookup"><span data-stu-id="0fff5-111">Service layering</span></span>
<span data-ttu-id="0fff5-112">Так как саму службу hello субъекта является надежной службы, все hello [модель приложения](service-fabric-application-model.md), жизненный цикл, [упаковки](service-fabric-package-apps.md), [развертывания](service-fabric-deploy-remove-applications.md), обновление и масштабирование понятия Надежные службы применяются hello и теми же службами tooactor способом.</span><span class="sxs-lookup"><span data-stu-id="0fff5-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![Структура службы субъектов][1]

<span data-ttu-id="0fff5-114">Hello предыдущей схеме показаны hello отношения между структурой приложения Service Fabric hello и пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="0fff5-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="0fff5-115">Синий элементы представляют собой платформу приложения hello надежного обмена, оранжевый представляет framework Reliable Actor hello и зеленым цветом в пользовательском коде.</span><span class="sxs-lookup"><span data-stu-id="0fff5-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="0fff5-116">В надежные службы к службе наследует hello `StatefulService` класса.</span><span class="sxs-lookup"><span data-stu-id="0fff5-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="0fff5-117">производный от `StatefulServiceBase` (или `StatelessService` для служб без отслеживания состояния).</span><span class="sxs-lookup"><span data-stu-id="0fff5-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="0fff5-118">В службы Reliable Actor использовать службу субъектов hello.</span><span class="sxs-lookup"><span data-stu-id="0fff5-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="0fff5-119">службу субъектов Hello имеет различную реализацию hello `StatefulServiceBase` класс реализует шаблону субъекта hello, работают на субъекты.</span><span class="sxs-lookup"><span data-stu-id="0fff5-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="0fff5-120">Так как саму службу hello субъекта является только реализация `StatefulServiceBase`, можно написать собственную службу, производный от `ActorService` и компоненты на уровне службы реализуйте hello же так, как при наследовании `StatefulService`, такие как:</span><span class="sxs-lookup"><span data-stu-id="0fff5-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="0fff5-121">резервное копирование и восстановление службы;</span><span class="sxs-lookup"><span data-stu-id="0fff5-121">Service backup and restore.</span></span>
* <span data-ttu-id="0fff5-122">общие функции для всех субъектов, например автоматическое выключение;</span><span class="sxs-lookup"><span data-stu-id="0fff5-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="0fff5-123">Удаленные вызовы процедур на самой службы субъекта hello и на каждый отдельный субъект.</span><span class="sxs-lookup"><span data-stu-id="0fff5-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="0fff5-124">В настоящее время службы с отслеживанием состояния не поддерживаются в Java или Linux.</span><span class="sxs-lookup"><span data-stu-id="0fff5-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="0fff5-125">С помощью службы субъекта hello</span><span class="sxs-lookup"><span data-stu-id="0fff5-125">Using hello actor service</span></span>
<span data-ttu-id="0fff5-126">Субъект экземпляры имеют службу субъектов toohello доступ, в которой они выполняются.</span><span class="sxs-lookup"><span data-stu-id="0fff5-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="0fff5-127">Через службу субъектов hello экземпляры субъекта программными средствами можно получить контекст службы hello.</span><span class="sxs-lookup"><span data-stu-id="0fff5-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="0fff5-128">контекст службы Hello имеет секции с Идентификатором hello, имя службы, имя приложения и другие сведения от платформы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0fff5-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="0fff5-129">Как и все надежные службы необходимо зарегистрировать службу hello субъекта с типом службы в среде выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="0fff5-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="0fff5-130">Для службы субъекта hello toorun экземпляры субъекта, тип субъекта также должен быть зарегистрирован со службой субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="0fff5-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="0fff5-131">Hello `ActorRuntime` метод регистрации выполняет это действие для субъектов.</span><span class="sxs-lookup"><span data-stu-id="0fff5-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="0fff5-132">В простейшем случае hello можно зарегистрировать только тип субъекта и службу субъектов hello с параметрами по умолчанию будет использоваться неявно:</span><span class="sxs-lookup"><span data-stu-id="0fff5-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="0fff5-133">Кроме того можно использовать лямбда-выражения, предоставленные службой hello регистрации метод tooconstruct hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="0fff5-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="0fff5-134">Можно затем настроить службу субъектов hello и явно создает субъект экземпляров, в которых можно ввести субъекта tooyour зависимости через ее конструктор:</span><span class="sxs-lookup"><span data-stu-id="0fff5-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="0fff5-135">Методы службы субъектов</span><span class="sxs-lookup"><span data-stu-id="0fff5-135">Actor service methods</span></span>
<span data-ttu-id="0fff5-136">Здравствуйте, служба реализует субъекта `IActorService` (C#) или `ActorService` (Java), который в свою очередь реализует `IService` (C#) или `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="0fff5-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="0fff5-137">Это интерфейс hello, используемой в удаленном взаимодействии надежного обмена, разрешающее удаленных вызовов процедур на методы службы.</span><span class="sxs-lookup"><span data-stu-id="0fff5-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="0fff5-138">Он содержит методы уровня службы, которые можно вызывать удаленно с помощью удаленных взаимодействий служб.</span><span class="sxs-lookup"><span data-stu-id="0fff5-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="0fff5-139">Перечисление субъектов</span><span class="sxs-lookup"><span data-stu-id="0fff5-139">Enumerating actors</span></span>
<span data-ttu-id="0fff5-140">Hello субъекта service позволяет клиенту tooenumerate метаданные о hello субъектов, размещение службы hello.</span><span class="sxs-lookup"><span data-stu-id="0fff5-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="0fff5-141">Поскольку службу субъектов hello секционированных службы с отслеживанием состояния, перечисление выполняется на каждую секцию.</span><span class="sxs-lookup"><span data-stu-id="0fff5-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="0fff5-142">Поскольку каждая секция может содержать много субъекты, перечисление hello возвращается как набор результатов по страницам.</span><span class="sxs-lookup"><span data-stu-id="0fff5-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="0fff5-143">страницы приветствия перебор, пока не будут считаны все страницы.</span><span class="sxs-lookup"><span data-stu-id="0fff5-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="0fff5-144">Следующий пример показывает как Hello toocreate список всех активных субъекты одной секции службу субъектов:</span><span class="sxs-lookup"><span data-stu-id="0fff5-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="0fff5-145">Удаление субъектов</span><span class="sxs-lookup"><span data-stu-id="0fff5-145">Deleting actors</span></span>
<span data-ttu-id="0fff5-146">службу субъектов Hello также предоставляет функцию для удаления субъектов:</span><span class="sxs-lookup"><span data-stu-id="0fff5-146">hello actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="0fff5-147">Дополнительные сведения об удалении субъекты и их состояния см. в разделе hello [субъекта жизненным циклом документации](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="0fff5-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="0fff5-148">Пользовательская служба субъектов</span><span class="sxs-lookup"><span data-stu-id="0fff5-148">Custom actor service</span></span>
<span data-ttu-id="0fff5-149">С помощью лямбда-выражения регистрации hello субъекта, можно зарегистрировать собственную службу пользовательского субъекта, производный от `ActorService` (C#) и `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="0fff5-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="0fff5-150">и реализовать в ней собственные функции уровня службы. Для этого нужно написать класс службы, наследующий класс `ActorService` (C#) или `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="0fff5-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="0fff5-151">Службы пользовательского субъект наследует все функциональные возможности среды выполнения hello субъекта из `ActorService` (C#) или `FabricActorService` (Java) и может быть используется tooimplement методы службы.</span><span class="sxs-lookup"><span data-stu-id="0fff5-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="0fff5-152">Реализация резервного копирования и восстановления субъектов</span><span class="sxs-lookup"><span data-stu-id="0fff5-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="0fff5-153">В следующем примере hello, hello пользовательских субъекта служба предоставляет метод tooback данные субъекта, используя преимущества hello удаленного взаимодействия прослушиватель уже присутствует в `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="0fff5-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="0fff5-154">В этом примере `IMyActorService` — это контракт удаленного взаимодействия, который реализует класс `IService` (C#) и `Service` (Java), а затем реализуется классом `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="0fff5-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="0fff5-155">Путем добавления этого контракта удаленного взаимодействия, методы `IMyActorService` , теперь также доступны tooa клиента путем создания прокси-сервер удаленного доступа через `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="0fff5-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="0fff5-156">Модель приложения</span><span class="sxs-lookup"><span data-stu-id="0fff5-156">Application model</span></span>
<span data-ttu-id="0fff5-157">Служб субъекта являются надежного обмена, поэтому модель приложения hello Здравствуйте, одинаково.</span><span class="sxs-lookup"><span data-stu-id="0fff5-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="0fff5-158">Однако средства построения framework субъекта hello создан некоторые файлы модели приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0fff5-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="0fff5-159">Манифест службы</span><span class="sxs-lookup"><span data-stu-id="0fff5-159">Service manifest</span></span>
<span data-ttu-id="0fff5-160">средства построения framework субъекта Hello автоматически создавать hello содержимое файла ServiceManifest.xml службу субъектов.</span><span class="sxs-lookup"><span data-stu-id="0fff5-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="0fff5-161">Этот файл содержит:</span><span class="sxs-lookup"><span data-stu-id="0fff5-161">This file includes:</span></span>

* <span data-ttu-id="0fff5-162">Тип службы субъектов.</span><span class="sxs-lookup"><span data-stu-id="0fff5-162">Actor service type.</span></span> <span data-ttu-id="0fff5-163">Имя типа Hello создается основании актер проекта.</span><span class="sxs-lookup"><span data-stu-id="0fff5-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="0fff5-164">На основе hello сохраняемости атрибута на ваш субъекта, hello флаг HasPersistedState также настраивается соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="0fff5-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="0fff5-165">Пакет кода.</span><span class="sxs-lookup"><span data-stu-id="0fff5-165">Code package.</span></span>
* <span data-ttu-id="0fff5-166">Пакет конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0fff5-166">Config package.</span></span>
* <span data-ttu-id="0fff5-167">Ресурсы и конечные точки.</span><span class="sxs-lookup"><span data-stu-id="0fff5-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="0fff5-168">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="0fff5-168">Application manifest</span></span>
<span data-ttu-id="0fff5-169">средства построения framework субъекта Hello автоматически создать определение службы по умолчанию для службы субъекта.</span><span class="sxs-lookup"><span data-stu-id="0fff5-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="0fff5-170">средства построения Hello заполнения свойств службы по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="0fff5-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="0fff5-171">Счетчик реплики набора определяется атрибутом сохраняемости hello на ваш субъекта.</span><span class="sxs-lookup"><span data-stu-id="0fff5-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="0fff5-172">Изменения каждого атрибута сохраняемости время hello на ваш субъекта, соответствующим образом Сброс счетчика набора реплик hello в определении службы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="0fff5-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="0fff5-173">Схемы секционирования и диапазона задаются tooUniform Int64 с полный диапазон ключа hello Int64.</span><span class="sxs-lookup"><span data-stu-id="0fff5-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="0fff5-174">Основные понятия о секции Service Fabric для субъектов</span><span class="sxs-lookup"><span data-stu-id="0fff5-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="0fff5-175">Службы субъектов — это секционированные службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="0fff5-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="0fff5-176">Каждая секция службы субъектов содержит набор субъектов.</span><span class="sxs-lookup"><span data-stu-id="0fff5-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="0fff5-177">Секции службы автоматически распределяются между несколькими узлами Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0fff5-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="0fff5-178">В результате распространяются экземпляры субъектов.</span><span class="sxs-lookup"><span data-stu-id="0fff5-178">Actor instances are distributed as a result.</span></span>

![Секционирование и распределение субъектов][5]

<span data-ttu-id="0fff5-180">Службы Reliable Services создаются с использованием различных схем и диапазонов ключей секционирования.</span><span class="sxs-lookup"><span data-stu-id="0fff5-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="0fff5-181">Служба субъектов Hello использует схему секционирования Int64 hello с субъектами toopartitions hello полный Int64 диапазона ключей toomap.</span><span class="sxs-lookup"><span data-stu-id="0fff5-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="0fff5-182">Идентификатор субъекта</span><span class="sxs-lookup"><span data-stu-id="0fff5-182">Actor ID</span></span>
<span data-ttu-id="0fff5-183">Каждый субъект, созданный в службе hello имеет уникальный идентификатор, связанный с ним, представленный hello `ActorId` класса.</span><span class="sxs-lookup"><span data-stu-id="0fff5-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="0fff5-184">`ActorId`является непрозрачным значением идентификатора, который может использоваться для равномерного распределения субъекты секциях hello службы, создавая произвольные идентификаторы:</span><span class="sxs-lookup"><span data-stu-id="0fff5-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="0fff5-185">Каждый `ActorId` — хэшированное tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="0fff5-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="0fff5-186">Именно поэтому hello субъекта службы должен использовать схему секционирования Int64 с полный диапазон ключа hello Int64.</span><span class="sxs-lookup"><span data-stu-id="0fff5-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="0fff5-187">Тем не менее для `ActorID` можно использовать пользовательские значения идентификаторов, включая строковые значения, а также GUID или UUID и значения типа Int64.</span><span class="sxs-lookup"><span data-stu-id="0fff5-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="0fff5-188">При использовании строк и идентификаторов GUID/UUID значения hello: Хешированные tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="0fff5-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="0fff5-189">Тем не менее, когда явно предоставляется Int64 tooan `ActorId`, hello Int64 сопоставит непосредственно tooa секции без дальнейшей хэширования.</span><span class="sxs-lookup"><span data-stu-id="0fff5-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="0fff5-190">Можно использовать этот метод toocontrol, которой субъекты hello раздела помещаются в.</span><span class="sxs-lookup"><span data-stu-id="0fff5-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fff5-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0fff5-191">Next steps</span></span>
* [<span data-ttu-id="0fff5-192">Управление состоянием субъекта</span><span class="sxs-lookup"><span data-stu-id="0fff5-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="0fff5-193">Жизненный цикл субъектов и сбор мусора</span><span class="sxs-lookup"><span data-stu-id="0fff5-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="0fff5-194">Справочная документация по API субъектов</span><span class="sxs-lookup"><span data-stu-id="0fff5-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="0fff5-195">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="0fff5-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="0fff5-196">Пример кода Java</span><span class="sxs-lookup"><span data-stu-id="0fff5-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
