---
title: "Управление состоянием субъекты aaaReliable | Документы Microsoft"
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
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="62820-103">Управление состоянием субъектов Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="62820-103">Reliable Actors state management</span></span>
<span data-ttu-id="62820-104">Субъекты Reliable Actors — это однопотоковые объекты для инкапсуляции логики и состояния.</span><span class="sxs-lookup"><span data-stu-id="62820-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="62820-105">Поскольку субъекты выполняются в надежной службы, они надежно сохранять состояние при помощи hello же механизмов сохраняемости и репликации, которые использует надежные службы.</span><span class="sxs-lookup"><span data-stu-id="62820-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="62820-106">Таким образом, субъектами не потеряли свое состояние после сбоев при повторной активации после сборки мусора или при их перемещении между узлами кластера из-за tooresource балансировки или обновления.</span><span class="sxs-lookup"><span data-stu-id="62820-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="62820-107">Сохранение состояния и репликация</span><span class="sxs-lookup"><span data-stu-id="62820-107">State persistence and replication</span></span>
<span data-ttu-id="62820-108">Все службы Reliable Actor считаются *с отслеживанием состояния* потому, что каждый экземпляр субъекта сопоставляется tooa уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="62820-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="62820-109">Это означает, что этой toohello повторные вызовы же идентификатор субъекта, перенаправленные toohello того же экземпляра субъекта.</span><span class="sxs-lookup"><span data-stu-id="62820-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="62820-110">Без сохранения состояния системы, напротив, клиент вызывает не гарантируется toohello toobe направлено сервере каждый раз.</span><span class="sxs-lookup"><span data-stu-id="62820-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="62820-111">Поэтому службы субъектов всегда отслеживают состояние.</span><span class="sxs-lookup"><span data-stu-id="62820-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="62820-112">Несмотря на то что субъекты отслеживают состояние, это не означает, что они надежно хранят состояние.</span><span class="sxs-lookup"><span data-stu-id="62820-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="62820-113">Субъекты можно выбрать уровень hello сохранения состояния и репликации на основе своих данных требования к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="62820-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="62820-114">**Постоянное состояние**: состояние является сохраненного toodisk и реплицированных too3 или нескольких реплик.</span><span class="sxs-lookup"><span data-stu-id="62820-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="62820-115">Этот вариант hello наиболее устойчивые состояния хранилища, где можно сохранить состояние до завершения создания кластера сбоя.</span><span class="sxs-lookup"><span data-stu-id="62820-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="62820-116">**Непостоянное состояние**: состояние реплицированных too3 или нескольких реплик и хранятся только в памяти.</span><span class="sxs-lookup"><span data-stu-id="62820-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="62820-117">Это обеспечивает устойчивость в случае сбоя узла, сбоя субъекта и во время обновления и балансировки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="62820-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="62820-118">Тем не менее не сохраненные toodisk.</span><span class="sxs-lookup"><span data-stu-id="62820-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="62820-119">Поэтому если одновременно будут потеряны все реплики, состояние hello также теряется.</span><span class="sxs-lookup"><span data-stu-id="62820-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="62820-120">**Не сохраненное состояние**: состояние не реплицируются и не запись toodisk.</span><span class="sxs-lookup"><span data-stu-id="62820-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="62820-121">Этот уровень предназначен для субъектов, которые просто не должны toomaintain состояние надежно.</span><span class="sxs-lookup"><span data-stu-id="62820-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="62820-122">Каждый уровень сохраняемости — это просто другая конфигурация *поставщика состояний* и *репликации* службы.</span><span class="sxs-lookup"><span data-stu-id="62820-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="62820-123">Независимо от того, имеется ли состояние записывается toodisk зависит от поставщика состояний hello--компонента hello в надежной службы, которая сохраняет состояние.</span><span class="sxs-lookup"><span data-stu-id="62820-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="62820-124">А репликация зависит от того, на скольких репликах развертывается служба.</span><span class="sxs-lookup"><span data-stu-id="62820-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="62820-125">С помощью надежного обмена оба hello поставщика состояний и счетчик реплики можно легко установить вручную.</span><span class="sxs-lookup"><span data-stu-id="62820-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="62820-126">Hello субъекта framework предоставляет атрибут, что при использовании на субъект, автоматически выбирает поставщика состояния по умолчанию и автоматически создает параметры для tooachieve число реплики, одно из этих трех параметров сохраняемости.</span><span class="sxs-lookup"><span data-stu-id="62820-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="62820-127">производный класс не наследуется атрибут statepersistence отвечает за хранение Hello, каждого типа субъекта необходимо предоставить свой уровень statepersistence отвечает за хранение.</span><span class="sxs-lookup"><span data-stu-id="62820-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="62820-128">Сохраненное состояние</span><span class="sxs-lookup"><span data-stu-id="62820-128">Persisted state</span></span>
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
<span data-ttu-id="62820-129">Этот параметр использует поставщик состояния, который хранит данные на диске и автоматически устанавливает too3 число реплики службы hello.</span><span class="sxs-lookup"><span data-stu-id="62820-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="62820-130">Непостоянное состояние</span><span class="sxs-lookup"><span data-stu-id="62820-130">Volatile state</span></span>
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
<span data-ttu-id="62820-131">Этот параметр использует поставщика в памяти — только состояния и наборы hello too3 число реплик.</span><span class="sxs-lookup"><span data-stu-id="62820-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="62820-132">Несохраняемое состояние</span><span class="sxs-lookup"><span data-stu-id="62820-132">No persisted state</span></span>
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
<span data-ttu-id="62820-133">Этот параметр использует поставщика в памяти — только состояния и наборы hello too1 число реплик.</span><span class="sxs-lookup"><span data-stu-id="62820-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="62820-134">Значения по умолчанию и созданные параметры</span><span class="sxs-lookup"><span data-stu-id="62820-134">Defaults and generated settings</span></span>
<span data-ttu-id="62820-135">При использовании hello `StatePersistence` атрибут поставщика состояний автоматически выбирается во время выполнения при запуске службы субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="62820-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="62820-136">Hello числа реплик, однако задается во время компиляции hello субъекта Visual Studio средства построения.</span><span class="sxs-lookup"><span data-stu-id="62820-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="62820-137">Hello средства построения автоматически создавать *службу по умолчанию* для hello службы субъекта в файле ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="62820-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="62820-138">Параметры создаются для **минимального размера набора реплик** и **целевого размера набора реплик**.</span><span class="sxs-lookup"><span data-stu-id="62820-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="62820-139">Вы можете изменить эти параметры вручную.</span><span class="sxs-lookup"><span data-stu-id="62820-139">You can change these parameters manually.</span></span> <span data-ttu-id="62820-140">Но каждый раз hello `StatePersistence` атрибут изменяется, то параметры hello будут toohello реплики набора размер значения по умолчанию выбран hello `StatePersistence` атрибут, переопределяя все предыдущие значения.</span><span class="sxs-lookup"><span data-stu-id="62820-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="62820-141">Другими словами, являются hello значения, заданные в файле ServiceManifest.xml *только* переопределено во время построения, при изменении hello `StatePersistence` значение атрибута.</span><span class="sxs-lookup"><span data-stu-id="62820-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="62820-142">Диспетчер состояний:</span><span class="sxs-lookup"><span data-stu-id="62820-142">State manager</span></span>
<span data-ttu-id="62820-143">У каждого экземпляра субъекта есть собственный диспетчер состояний: структура данных, подобная словарю, которая надежно хранит пары "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="62820-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="62820-144">диспетчер состояния Hello является оболочкой вокруг поставщика состояний.</span><span class="sxs-lookup"><span data-stu-id="62820-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="62820-145">Его можно использовать toostore данных независимо от того, используется параметр сохраняемости.</span><span class="sxs-lookup"><span data-stu-id="62820-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="62820-146">Он не предоставляет никаких гарантий, работающей субъекта-службы может быть изменена из tooa параметр неустойчивого состояния (в памяти — только), хранящихся параметр состояния через последовательного обновления при сохранении данных.</span><span class="sxs-lookup"><span data-stu-id="62820-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="62820-147">Однако это число возможных toochange реплики для запущенной службы.</span><span class="sxs-lookup"><span data-stu-id="62820-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="62820-148">Ключи диспетчера состояний должны быть строками.</span><span class="sxs-lookup"><span data-stu-id="62820-148">State manager keys must be strings.</span></span> <span data-ttu-id="62820-149">Значения являются универсальными и могут быть любого типа, в том числе пользовательского.</span><span class="sxs-lookup"><span data-stu-id="62820-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="62820-150">Значения, хранящиеся в диспетчере состояния hello должна быть сериализуемым контракта данных, поскольку они могут передаваться по узлы tooother hello сети во время репликации и может записываться toodisk, в зависимости от настройки сохраняемости состояния субъекта.</span><span class="sxs-lookup"><span data-stu-id="62820-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="62820-151">диспетчер состояния Hello предоставляет управление состоянием, аналогичные toothose найден в словаре надежные общие методы словаря.</span><span class="sxs-lookup"><span data-stu-id="62820-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="62820-152">Доступ к состоянию</span><span class="sxs-lookup"><span data-stu-id="62820-152">Accessing state</span></span>
<span data-ttu-id="62820-153">Состояние может осуществляться через диспетчер состояния hello по ключу.</span><span class="sxs-lookup"><span data-stu-id="62820-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="62820-154">Методы диспетчера состояний асинхронны, так как они могут потребовать дискового ввода-вывода, если у субъектов сохраняемое состояние.</span><span class="sxs-lookup"><span data-stu-id="62820-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="62820-155">При первом доступе объекты состояния кэшируются в памяти.</span><span class="sxs-lookup"><span data-stu-id="62820-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="62820-156">Повторные операции доступа к объектам обращаются к объектам непосредственно из памяти и возвращают данные синхронно без дискового ввода-вывода или асинхронного переключения контекста.</span><span class="sxs-lookup"><span data-stu-id="62820-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="62820-157">Объект состояния удаляется из кэша hello в hello в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="62820-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="62820-158">Метод субъекта выдает необработанное исключение после извлекает из диспетчера состояний hello объект.</span><span class="sxs-lookup"><span data-stu-id="62820-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="62820-159">Субъект повторно активируется после отключения или из-за сбоя.</span><span class="sxs-lookup"><span data-stu-id="62820-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="62820-160">страницы поставщика состояния Hello состояния toodisk.</span><span class="sxs-lookup"><span data-stu-id="62820-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="62820-161">Это поведение зависит от реализации поставщика состояния hello.</span><span class="sxs-lookup"><span data-stu-id="62820-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="62820-162">поставщик состояния по умолчанию Hello для hello `Persisted` задано это поведение.</span><span class="sxs-lookup"><span data-stu-id="62820-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="62820-163">Состояние можно получить с помощью стандартного *получить* операцию, создающую `KeyNotFoundException`(C#) или `NoSuchElementException`(Java), если запись не существует для ключа hello:</span><span class="sxs-lookup"><span data-stu-id="62820-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

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

<span data-ttu-id="62820-164">Получить состояние можно также используя метод *TryGet*. Он не вызывает исключение, если для ключа запись не существует.</span><span class="sxs-lookup"><span data-stu-id="62820-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="62820-165">Сохранение состояния</span><span class="sxs-lookup"><span data-stu-id="62820-165">Saving state</span></span>
<span data-ttu-id="62820-166">методы получения диспетчера состояния Hello возвращать объект tooan ссылки в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="62820-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="62820-167">Изменение этого объекта в локальной памяти сама по себе не приводит к его toobe сохранены.</span><span class="sxs-lookup"><span data-stu-id="62820-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="62820-168">Когда извлекается из диспетчер состояния hello и изменить объект, он должен быть повторно hello состояния диспетчера toobe сохранены.</span><span class="sxs-lookup"><span data-stu-id="62820-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="62820-169">Можно вставить состояние с помощью безусловный *задать*, которой hello эквивалент hello `dictionary["key"] = value` синтаксис:</span><span class="sxs-lookup"><span data-stu-id="62820-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="62820-170">Состояние можно добавить с помощью метода *Add*,</span><span class="sxs-lookup"><span data-stu-id="62820-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="62820-171">Этот метод создает исключение `InvalidOperationException`(C#) или `IllegalStateException`(Java), когда он пытается tooadd ключ, который уже существует.</span><span class="sxs-lookup"><span data-stu-id="62820-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="62820-172">Состояние также можно добавить с помощью метода *TryAdd*,</span><span class="sxs-lookup"><span data-stu-id="62820-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="62820-173">Этот метод не исключение, когда он пытается tooadd ключ, который уже существует.</span><span class="sxs-lookup"><span data-stu-id="62820-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="62820-174">В конце метода субъекта hello диспетчер состояний hello автоматически сохраняет любые значения, которые были добавлены или изменены операцией insert или update.</span><span class="sxs-lookup"><span data-stu-id="62820-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="62820-175">«Сохранить» можно включить сохранение toodisk и репликации, в зависимости от параметров hello.</span><span class="sxs-lookup"><span data-stu-id="62820-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="62820-176">Значения, которые не были изменены, не сохраняются и не реплицируются.</span><span class="sxs-lookup"><span data-stu-id="62820-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="62820-177">Если значения не были изменены, hello операция сохранения не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="62820-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="62820-178">При ошибке сохранения, hello измененном состоянии удаляются, а исходное состояние hello перезагружается.</span><span class="sxs-lookup"><span data-stu-id="62820-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="62820-179">Можно также сохранить состояние вручную путем вызова hello `SaveStateAsync` hello субъекта базовый метод:</span><span class="sxs-lookup"><span data-stu-id="62820-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="62820-180">Удаление состояния</span><span class="sxs-lookup"><span data-stu-id="62820-180">Removing state</span></span>
<span data-ttu-id="62820-181">Можно удалить состояние без возможности восстановления из диспетчера состояния субъекта, вызывающему Привет *удалить* метод.</span><span class="sxs-lookup"><span data-stu-id="62820-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="62820-182">Этот метод создает исключение `KeyNotFoundException`(C#) или `NoSuchElementException`(Java), когда он пытается tooremove ключ, который не существует.</span><span class="sxs-lookup"><span data-stu-id="62820-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

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

<span data-ttu-id="62820-183">Можно также удалить состояние без возможности восстановления с помощью hello *TryRemove* метод.</span><span class="sxs-lookup"><span data-stu-id="62820-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="62820-184">Этот метод не исключение, когда он пытается tooremove ключ, который не существует.</span><span class="sxs-lookup"><span data-stu-id="62820-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="62820-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62820-185">Next steps</span></span>

<span data-ttu-id="62820-186">Состояние, которое хранится в службы Reliable Actor должно быть сериализовано перед его письменного toodisk и реплицируются для обеспечения высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="62820-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="62820-187">Узнайте больше о [сериализации типа субъекта](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="62820-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="62820-188">Затем ознакомьтесь с [диагностикой и мониторингом производительности субъекта](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="62820-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
