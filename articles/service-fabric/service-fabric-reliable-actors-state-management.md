---
title: "Управление состоянием Reliable Actors | Документация Майкрософт"
description: "Описание управления, сохранения и репликации субъектов Reliable Actors для обеспечения высокого уровня доступности."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: aca8cf2b94e8b746a5cac6af021c7221a29b7345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="79bfe-103">Управление состоянием субъектов Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="79bfe-103">Reliable Actors state management</span></span>
<span data-ttu-id="79bfe-104">Субъекты Reliable Actors — это однопотоковые объекты для инкапсуляции логики и состояния.</span><span class="sxs-lookup"><span data-stu-id="79bfe-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="79bfe-105">Так как субъекты выполняются в службах Reliable Services, они могут поддерживать состояние, используя те же механизмы сохранения и репликации, которые применяются службами Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="79bfe-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="79bfe-106">При этом субъекты не теряют свое состояние после сбоев, повторной активации после сборки мусора или перемещения между узлами в кластере из-за балансировки ресурсов или обновления.</span><span class="sxs-lookup"><span data-stu-id="79bfe-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="79bfe-107">Сохранение состояния и репликация</span><span class="sxs-lookup"><span data-stu-id="79bfe-107">State persistence and replication</span></span>
<span data-ttu-id="79bfe-108">Все субъекты Reliable Actors *отслеживают состояние* , так как каждый экземпляр субъекта сопоставляется с уникальным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="79bfe-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="79bfe-109">Это означает, что повторные вызовы одного идентификатора субъекта направляются в один и тот же экземпляр субъекта.</span><span class="sxs-lookup"><span data-stu-id="79bfe-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="79bfe-110">Это отличается от системы без отслеживания состояния, в которой не гарантируется, что клиентские вызовы будут каждый раз направляться на один и тот же сервер.</span><span class="sxs-lookup"><span data-stu-id="79bfe-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="79bfe-111">Поэтому службы субъектов всегда отслеживают состояние.</span><span class="sxs-lookup"><span data-stu-id="79bfe-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="79bfe-112">Несмотря на то что субъекты отслеживают состояние, это не означает, что они надежно хранят состояние.</span><span class="sxs-lookup"><span data-stu-id="79bfe-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="79bfe-113">Субъекты могут выбрать уровень сохранения и репликации состояния на основе их требований к хранению данных:</span><span class="sxs-lookup"><span data-stu-id="79bfe-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="79bfe-114">**Сохраняемое состояние:** состояние сохраняется на диске и реплицируется на 3 или более реплик.</span><span class="sxs-lookup"><span data-stu-id="79bfe-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span></span> <span data-ttu-id="79bfe-115">Это самый устойчивый вариант хранения состояния, при котором оно может сохраниться даже после полного сбоя кластера.</span><span class="sxs-lookup"><span data-stu-id="79bfe-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="79bfe-116">**Непостоянное состояние:** состояние реплицируется на 3 или более реплик и хранится только в памяти.</span><span class="sxs-lookup"><span data-stu-id="79bfe-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="79bfe-117">Это обеспечивает устойчивость в случае сбоя узла, сбоя субъекта и во время обновления и балансировки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="79bfe-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="79bfe-118">Однако состояние не сохраняется на диск,</span><span class="sxs-lookup"><span data-stu-id="79bfe-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="79bfe-119">поэтому если все реплики будут потеряны одновременно, состояние также теряется.</span><span class="sxs-lookup"><span data-stu-id="79bfe-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="79bfe-120">**Несохраняемое состояние:** состояние не реплицируется и не записывается на диск.</span><span class="sxs-lookup"><span data-stu-id="79bfe-120">**No persisted state**: State is not replicated or written to disk.</span></span> <span data-ttu-id="79bfe-121">Этот уровень предназначен для субъектов, которым просто не требуется надежно хранить состояние.</span><span class="sxs-lookup"><span data-stu-id="79bfe-121">This level is for actors that simply don't need to maintain state reliably.</span></span>

<span data-ttu-id="79bfe-122">Каждый уровень сохраняемости — это просто другая конфигурация *поставщика состояний* и *репликации* службы.</span><span class="sxs-lookup"><span data-stu-id="79bfe-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="79bfe-123">Записывается ли состояние на диск, зависит от поставщика состояний — компонента Reliable Service, который хранит состояние.</span><span class="sxs-lookup"><span data-stu-id="79bfe-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="79bfe-124">А репликация зависит от того, на скольких репликах развертывается служба.</span><span class="sxs-lookup"><span data-stu-id="79bfe-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="79bfe-125">Как и в случае со службами Reliable Services, поставщик состояний и число реплик можно легко настроить вручную.</span><span class="sxs-lookup"><span data-stu-id="79bfe-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="79bfe-126">Платформа субъектов предоставляет атрибут, который при использовании с субъектом автоматически выбирает поставщик состояний по умолчанию и создает параметры числа реплик для достижения одного из этих трех параметров сохраняемости.</span><span class="sxs-lookup"><span data-stu-id="79bfe-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span> <span data-ttu-id="79bfe-127">Производный класс не наследует атрибут StatePersistence, каждый тип субъекта должен предоставлять собственный уровень StatePersistence.</span><span class="sxs-lookup"><span data-stu-id="79bfe-127">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="79bfe-128">Сохраненное состояние</span><span class="sxs-lookup"><span data-stu-id="79bfe-128">Persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
<span data-ttu-id="79bfe-129">Этот параметр использует поставщик состояний, который хранит данные на диске, и автоматически задает 3 реплики службы.</span><span class="sxs-lookup"><span data-stu-id="79bfe-129">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="79bfe-130">Непостоянное состояние</span><span class="sxs-lookup"><span data-stu-id="79bfe-130">Volatile state</span></span>
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="79bfe-131">Этот параметр использует поставщик состояний только в памяти и настраивает 3 реплики.</span><span class="sxs-lookup"><span data-stu-id="79bfe-131">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="79bfe-132">Несохраняемое состояние</span><span class="sxs-lookup"><span data-stu-id="79bfe-132">No persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="79bfe-133">Этот параметр использует поставщик состояний только в памяти и настраивает 1 реплику.</span><span class="sxs-lookup"><span data-stu-id="79bfe-133">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="79bfe-134">Значения по умолчанию и созданные параметры</span><span class="sxs-lookup"><span data-stu-id="79bfe-134">Defaults and generated settings</span></span>
<span data-ttu-id="79bfe-135">При использовании атрибута `StatePersistence` поставщик состояний автоматически выбирается во время выполнения при запуске службы субъекта.</span><span class="sxs-lookup"><span data-stu-id="79bfe-135">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="79bfe-136">Однако число реплик задается средствами построения субъекта Visual Studio во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="79bfe-136">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="79bfe-137">Средства построения автоматически создают *службу по умолчанию* для службы субъекта в ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="79bfe-137">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="79bfe-138">Параметры создаются для **минимального размера набора реплик** и **целевого размера набора реплик**.</span><span class="sxs-lookup"><span data-stu-id="79bfe-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="79bfe-139">Вы можете изменить эти параметры вручную.</span><span class="sxs-lookup"><span data-stu-id="79bfe-139">You can change these parameters manually.</span></span> <span data-ttu-id="79bfe-140">Однако при каждом изменении атрибута `StatePersistence` параметрам будут присвоены значения размера набора реплик по умолчанию для выбранного атрибута `StatePersistence`, а все предыдущие значения будут переопределены.</span><span class="sxs-lookup"><span data-stu-id="79bfe-140">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="79bfe-141">Другими словами, указанные в файле ServiceManifest.xml значения будут переопределены *только* во время сборки при изменении значения атрибута `StatePersistence`.</span><span class="sxs-lookup"><span data-stu-id="79bfe-141">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a><span data-ttu-id="79bfe-142">Диспетчер состояний:</span><span class="sxs-lookup"><span data-stu-id="79bfe-142">State manager</span></span>
<span data-ttu-id="79bfe-143">У каждого экземпляра субъекта есть собственный диспетчер состояний: структура данных, подобная словарю, которая надежно хранит пары "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="79bfe-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="79bfe-144">Диспетчер состояний — это оболочка вокруг поставщика состояний.</span><span class="sxs-lookup"><span data-stu-id="79bfe-144">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="79bfe-145">Его можно использовать для хранения данных независимо от того, какой параметр сохраняемости применяется,</span><span class="sxs-lookup"><span data-stu-id="79bfe-145">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="79bfe-146">но он не предоставляет никаких гарантий, что для работающей службы субъекта можно изменить параметр непостоянного состояния (только в памяти) на сохраняемое состояние с помощью последовательного обновления при сохранении данных.</span><span class="sxs-lookup"><span data-stu-id="79bfe-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="79bfe-147">Тем не менее, можно изменить количество реплик для запущенной службы.</span><span class="sxs-lookup"><span data-stu-id="79bfe-147">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="79bfe-148">Ключи диспетчера состояний должны быть строками.</span><span class="sxs-lookup"><span data-stu-id="79bfe-148">State manager keys must be strings.</span></span> <span data-ttu-id="79bfe-149">Значения являются универсальными и могут быть любого типа, в том числе пользовательского.</span><span class="sxs-lookup"><span data-stu-id="79bfe-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="79bfe-150">Значения, хранящиеся в диспетчере состояний, должны быть сериализуемыми контрактом данных, так как они могут передаваться по сети другим узлам во время репликации и быть записаны на диск в зависимости от параметра сохранения состояния субъекта.</span><span class="sxs-lookup"><span data-stu-id="79bfe-150">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="79bfe-151">Диспетчер состояний предоставляет общие методы словаря для управления состоянием, аналогичные используемым в надежном словаре.</span><span class="sxs-lookup"><span data-stu-id="79bfe-151">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="79bfe-152">Доступ к состоянию</span><span class="sxs-lookup"><span data-stu-id="79bfe-152">Accessing state</span></span>
<span data-ttu-id="79bfe-153">Доступ к состоянию можно получить через диспетчер состояний по ключу.</span><span class="sxs-lookup"><span data-stu-id="79bfe-153">State can be accessed through the state manager by key.</span></span> <span data-ttu-id="79bfe-154">Методы диспетчера состояний асинхронны, так как они могут потребовать дискового ввода-вывода, если у субъектов сохраняемое состояние.</span><span class="sxs-lookup"><span data-stu-id="79bfe-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="79bfe-155">При первом доступе объекты состояния кэшируются в памяти.</span><span class="sxs-lookup"><span data-stu-id="79bfe-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="79bfe-156">Повторные операции доступа к объектам обращаются к объектам непосредственно из памяти и возвращают данные синхронно без дискового ввода-вывода или асинхронного переключения контекста.</span><span class="sxs-lookup"><span data-stu-id="79bfe-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="79bfe-157">Объект состояния удаляется из кэша в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="79bfe-157">A state object is removed from the cache in the following cases:</span></span>

* <span data-ttu-id="79bfe-158">Метод субъекта вызывает необработанное исключение после извлечения объекта из диспетчера состояний.</span><span class="sxs-lookup"><span data-stu-id="79bfe-158">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span></span>
* <span data-ttu-id="79bfe-159">Субъект повторно активируется после отключения или из-за сбоя.</span><span class="sxs-lookup"><span data-stu-id="79bfe-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="79bfe-160">Поставщик состояния записывает состояние на диск.</span><span class="sxs-lookup"><span data-stu-id="79bfe-160">The state provider pages state to disk.</span></span> <span data-ttu-id="79bfe-161">Поведение зависит от реализации поставщика состояний.</span><span class="sxs-lookup"><span data-stu-id="79bfe-161">This behavior depends on the state provider implementation.</span></span> <span data-ttu-id="79bfe-162">Поставщик состояний по умолчанию для параметра `Persisted` применяет такое поведение.</span><span class="sxs-lookup"><span data-stu-id="79bfe-162">The default state provider for the `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="79bfe-163">Получить состояние можно с помощью стандартной операции *Get*, которая порождает исключение `KeyNotFoundException`(C#) или `NoSuchElementException`(Java), если для ключа запись не существует.</span><span class="sxs-lookup"><span data-stu-id="79bfe-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

<span data-ttu-id="79bfe-164">Получить состояние можно также используя метод *TryGet*. Он не вызывает исключение, если для ключа запись не существует.</span><span class="sxs-lookup"><span data-stu-id="79bfe-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a><span data-ttu-id="79bfe-165">Сохранение состояния</span><span class="sxs-lookup"><span data-stu-id="79bfe-165">Saving state</span></span>
<span data-ttu-id="79bfe-166">Методы извлечения диспетчера состояний возвращают ссылку на объект в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="79bfe-166">The state manager retrieval methods return a reference to an object in local memory.</span></span> <span data-ttu-id="79bfe-167">Изменение этого объекта только в локальной памяти не приводит к его длительному сохранению.</span><span class="sxs-lookup"><span data-stu-id="79bfe-167">Modifying this object in local memory alone does not cause it to be saved durably.</span></span> <span data-ttu-id="79bfe-168">Когда объект извлекается из диспетчера состояний и изменяется, его необходимо снова вставить в диспетчер состояний для постоянного сохранения.</span><span class="sxs-lookup"><span data-stu-id="79bfe-168">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span></span>

<span data-ttu-id="79bfe-169">Состояние можно вставить с помощью безусловной операции *Set*, которая эквивалента синтаксису `dictionary["key"] = value`.</span><span class="sxs-lookup"><span data-stu-id="79bfe-169">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

<span data-ttu-id="79bfe-170">Состояние можно добавить с помощью метода *Add*,</span><span class="sxs-lookup"><span data-stu-id="79bfe-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="79bfe-171">который порождает исключение `InvalidOperationException`(C#) или `IllegalStateException`(Java) при попытке добавить ключ, который уже существует.</span><span class="sxs-lookup"><span data-stu-id="79bfe-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

<span data-ttu-id="79bfe-172">Состояние также можно добавить с помощью метода *TryAdd*,</span><span class="sxs-lookup"><span data-stu-id="79bfe-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="79bfe-173">который не вызывает исключение при попытке добавить уже существующий ключ.</span><span class="sxs-lookup"><span data-stu-id="79bfe-173">This method does not throw when it tries to add a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

<span data-ttu-id="79bfe-174">В конце метода субъекта диспетчер состояний автоматически сохраняет все значения, которые были добавлены или изменены с помощью операции вставки или обновления.</span><span class="sxs-lookup"><span data-stu-id="79bfe-174">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="79bfe-175">"Сохранение" может включать в себя сохранение на диск и репликацию в зависимости от используемых параметров.</span><span class="sxs-lookup"><span data-stu-id="79bfe-175">A "save" can include persisting to disk and replication, depending on the settings used.</span></span> <span data-ttu-id="79bfe-176">Значения, которые не были изменены, не сохраняются и не реплицируются.</span><span class="sxs-lookup"><span data-stu-id="79bfe-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="79bfe-177">Если значения не были изменены, операция сохранения не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="79bfe-177">If no values have been modified, the save operation does nothing.</span></span> <span data-ttu-id="79bfe-178">При сбое сохранения измененное состояние удаляется и загружается исходное состояние.</span><span class="sxs-lookup"><span data-stu-id="79bfe-178">If saving fails, the modified state is discarded and the original state is reloaded.</span></span>

<span data-ttu-id="79bfe-179">Состояние также можно сохранить вручную, вызвав метод `SaveStateAsync` в базовом субъекте:</span><span class="sxs-lookup"><span data-stu-id="79bfe-179">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span></span>

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a><span data-ttu-id="79bfe-180">Удаление состояния</span><span class="sxs-lookup"><span data-stu-id="79bfe-180">Removing state</span></span>
<span data-ttu-id="79bfe-181">Состояние можно удалить из диспетчера состояний субъекта без возможности восстановления, вызвав метод *Remove*.</span><span class="sxs-lookup"><span data-stu-id="79bfe-181">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span></span> <span data-ttu-id="79bfe-182">Этот метод вызывает исключение `KeyNotFoundException`(C#) или `NoSuchElementException`(Java) при попытке удалить ключ, который не существует.</span><span class="sxs-lookup"><span data-stu-id="79bfe-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

<span data-ttu-id="79bfe-183">Состояние также можно удалить без возможности восстановления с помощью метода *TryRemove*,</span><span class="sxs-lookup"><span data-stu-id="79bfe-183">You can also remove state permanently by using the *TryRemove* method.</span></span> <span data-ttu-id="79bfe-184">который не вызывает исключение при попытке удалить несуществующий ключ.</span><span class="sxs-lookup"><span data-stu-id="79bfe-184">This method does not throw when it tries to remove a key that does not exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="79bfe-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79bfe-185">Next steps</span></span>

<span data-ttu-id="79bfe-186">Состояние, которое хранится в Reliable Actors, должно быть сериализовано перед записью на диск и реплицировано для обеспечения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="79bfe-186">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span></span> <span data-ttu-id="79bfe-187">Узнайте больше о [сериализации типа субъекта](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="79bfe-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="79bfe-188">Затем ознакомьтесь с [диагностикой и мониторингом производительности субъекта](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="79bfe-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
