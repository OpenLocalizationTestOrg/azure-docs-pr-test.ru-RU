---
title: "aaaOverview микрослужбами Azure на основе субъектов жизненного цикла | Документы Microsoft"
description: "Описание жизненного цикла Reliable Actors Service Fabric, сбора мусора и ручного удаления субъектов и их состояний."
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="118ee-103">Жизненный цикл субъектов, автоматическая сборка мусора и удаление вручную</span><span class="sxs-lookup"><span data-stu-id="118ee-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="118ee-104">Субъект активируется hello первый раз выполняется вызов tooany его методов.</span><span class="sxs-lookup"><span data-stu-id="118ee-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="118ee-105">Субъект — отключено (собраны как мусор средой выполнения субъекты hello), если он не используется для настроенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="118ee-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="118ee-106">Субъект и его состояние можно также удалить вручную в любое время.</span><span class="sxs-lookup"><span data-stu-id="118ee-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="118ee-107">Активация субъекта</span><span class="sxs-lookup"><span data-stu-id="118ee-107">Actor activation</span></span>
<span data-ttu-id="118ee-108">При активации субъекта происходит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="118ee-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="118ee-109">При поступлении вызова для субъекта, который еще не активен, создается новый субъект.</span><span class="sxs-lookup"><span data-stu-id="118ee-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="118ee-110">состояния субъекта Hello загружается в том случае, если он отслеживает состояние.</span><span class="sxs-lookup"><span data-stu-id="118ee-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="118ee-111">Hello `OnActivateAsync` (C#) или `onActivateAsync` вызывается метод (Java), (который можно переопределить в реализации hello субъекта).</span><span class="sxs-lookup"><span data-stu-id="118ee-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="118ee-112">Субъект Hello считается активным.</span><span class="sxs-lookup"><span data-stu-id="118ee-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="118ee-113">Деактивации субъекта</span><span class="sxs-lookup"><span data-stu-id="118ee-113">Actor deactivation</span></span>
<span data-ttu-id="118ee-114">При отключении субъект происходит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="118ee-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="118ee-115">Если субъект не используется для некоторого периода времени, он удаляется из таблицы активных субъекты hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="118ee-116">Hello `OnDeactivateAsync` (C#) или `onDeactivateAsync` вызывается метод (Java), (который можно переопределить в реализации hello субъекта).</span><span class="sxs-lookup"><span data-stu-id="118ee-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="118ee-117">Это приведет к очистке всех hello таймеры для субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="118ee-118">Операции с субъектом, такие как изменение состояния, не должны вызываться из этого метода.</span><span class="sxs-lookup"><span data-stu-id="118ee-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="118ee-119">Hello субъекты структуры создаваемых средой выполнения некоторых [события, связанные tooactor активация и деактивация](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="118ee-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="118ee-120">Они полезны при диагностике и мониторинге производительности.</span><span class="sxs-lookup"><span data-stu-id="118ee-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="118ee-121">Сборка мусора и субъекты</span><span class="sxs-lookup"><span data-stu-id="118ee-121">Actor garbage collection</span></span>
<span data-ttu-id="118ee-122">При отключении субъект ссылки toohello субъекта, освобождаются, и может быть сборщиком мусора обычно hello общеязыковая среда выполнения (CLR) или java сборщика мусора виртуальной машины (JVM).</span><span class="sxs-lookup"><span data-stu-id="118ee-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="118ee-123">Сборка мусора только очищает hello объекта субъекта. Это осуществляется **не** удалить состояние, сохраненное в диспетчер состояния субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="118ee-124">Hello Далее время hello субъект активируется, создается новый объект субъекта и восстанавливается его состояние.</span><span class="sxs-lookup"><span data-stu-id="118ee-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="118ee-125">Что считается «используются» hello с целью деактивации и сборка мусора?</span><span class="sxs-lookup"><span data-stu-id="118ee-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="118ee-126">Получение вызова</span><span class="sxs-lookup"><span data-stu-id="118ee-126">Receiving a call</span></span>
* <span data-ttu-id="118ee-127">`IRemindable.ReceiveReminderAsync`метод, вызываемый (применимо только в том случае, если субъект hello использует напоминания)</span><span class="sxs-lookup"><span data-stu-id="118ee-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="118ee-128">Если субъект hello использует таймеры и его таймера обратный вызов выполняется, он не **не** количество как «используются».</span><span class="sxs-lookup"><span data-stu-id="118ee-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="118ee-129">Прежде чем углубляться в подробности hello деактивации, очень важно toodefine hello следующими условиями:</span><span class="sxs-lookup"><span data-stu-id="118ee-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="118ee-130">*Интервал сканирования*.</span><span class="sxs-lookup"><span data-stu-id="118ee-130">*Scan interval*.</span></span> <span data-ttu-id="118ee-131">Это интервал приветствия, на какие hello субъекты среды выполнения просматривает свою таблицу Active субъекты для субъектов, которые могут быть деактивированы и сборщиком мусора.</span><span class="sxs-lookup"><span data-stu-id="118ee-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="118ee-132">значение по умолчанию Hello — 1 минута.</span><span class="sxs-lookup"><span data-stu-id="118ee-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="118ee-133">*Время ожидания в состоянии простоя*.</span><span class="sxs-lookup"><span data-stu-id="118ee-133">*Idle timeout*.</span></span> <span data-ttu-id="118ee-134">Это интервал времени, что субъект должен tooremain неиспользуемые hello (простоя), прежде чем он может быть отключен и сборщиком мусора.</span><span class="sxs-lookup"><span data-stu-id="118ee-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="118ee-135">значение по умолчанию Hello составляет 60 минут.</span><span class="sxs-lookup"><span data-stu-id="118ee-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="118ee-136">Как правило необязательно toochange эти значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="118ee-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="118ee-137">При необходимости этот период времени можно изменить, вызвав метод `ActorServiceSettings` при регистрации [службы субъектов](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="118ee-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
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
    }
}
```
<span data-ttu-id="118ee-138">Для каждого активного субъект среда выполнения субъекта hello хранит информацию о hello количество времени, который он был неактивен (т. е. не используется).</span><span class="sxs-lookup"><span data-stu-id="118ee-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="118ee-139">Среда выполнения субъекта Hello проверяет каждой из сторон hello каждый `ScanIntervalInSeconds` toosee, если он может быть мусора собираются и собирает его, если не используется `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="118ee-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="118ee-140">Каждый раз, когда используется субъект, его время простоя — too0 сброса.</span><span class="sxs-lookup"><span data-stu-id="118ee-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="118ee-141">После этого субъекта hello может быть мусора только в том случае, если он снова будет бездействовать для `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="118ee-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="118ee-142">Помните, что субъект считается toohave уже используется, если выполняется метод интерфейса субъекта или обратный вызов напоминания субъекта.</span><span class="sxs-lookup"><span data-stu-id="118ee-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="118ee-143">Субъект — **не** считается toohave было использовано, если выполнено его обратный вызов таймера.</span><span class="sxs-lookup"><span data-stu-id="118ee-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="118ee-144">Hello следующей диаграмме показан жизненный цикл hello tooillustrate один субъект этих понятий.</span><span class="sxs-lookup"><span data-stu-id="118ee-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![Пример времени простоя][1]

<span data-ttu-id="118ee-146">Hello примере показаны влияние hello вызовов субъекта, напоминаний и таймеров времени существования этого субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="118ee-147">следует упомянуть приведены следующие моменты, касающиеся hello пример Hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="118ee-148">Данного IdleTimeout заданы и too5 и 10 соответственно.</span><span class="sxs-lookup"><span data-stu-id="118ee-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="118ee-149">(Единицы не имеет значения, поскольку нашей целью является только tooillustrate понятие hello.)</span><span class="sxs-lookup"><span data-stu-id="118ee-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="118ee-150">Поиск Hello субъекты toobe мусора происходит на T = 0, 5, 10, 15, 20, 25, в соответствии с определением hello сканирования интервал, равный 5.</span><span class="sxs-lookup"><span data-stu-id="118ee-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="118ee-151">Таймер срабатывает при T = 4, 8, 12, 16, 20 и 24, после чего выполняется обратный вызов.</span><span class="sxs-lookup"><span data-stu-id="118ee-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="118ee-152">Он не влияет на время простоя hello объекта субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="118ee-153">Для вызова метода субъекта в T = 7 сбрасывает too0 hello время простоя и задержки hello сборку мусора для субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="118ee-154">Выполняет обратный вызов напоминания субъекта в T = 14 и дальнейшей задержки hello сборку мусора для субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="118ee-155">Во время hello просмотра сборки мусора в T = 25 время простоя hello субъекта наконец превышает hello тайм-аут простоя 10 и субъект hello выполняет сборку мусора.</span><span class="sxs-lookup"><span data-stu-id="118ee-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="118ee-156">Субъект никогда не удаляется сборщиком мусора, если выполняется какой-либо из его методов, независимо от того, сколько времени занимает выполнение этого метода.</span><span class="sxs-lookup"><span data-stu-id="118ee-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="118ee-157">Как упоминалось ранее, hello выполнение методов интерфейса субъекта и обратные вызовы напоминание предотвращает сбор мусора, сбросив too0 время простоя hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="118ee-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="118ee-158">выполнение Hello обратные вызовы таймера не сбрасывает too0 hello время простоя.</span><span class="sxs-lookup"><span data-stu-id="118ee-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="118ee-159">Тем не менее hello сборку мусора для субъекта hello откладывается до завершения выполнения обратного вызова таймера hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="118ee-160">Удаление субъектов и их состояние</span><span class="sxs-lookup"><span data-stu-id="118ee-160">Deleting actors and their state</span></span>
<span data-ttu-id="118ee-161">Сборку мусора для отключенного субъекты только очищает hello объекта субъекта, но не удаляет данные, хранящиеся в диспетчере состояния субъекта.</span><span class="sxs-lookup"><span data-stu-id="118ee-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="118ee-162">При субъект активировать повторно, его данные снова становится tooit, доступные через диспетчер состояния hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="118ee-163">В случаях, где субъекты хранить данные в диспетчер состояний и являются отключены, но никогда не включается повторно возможно, необходимые tooclean копии своих данных.</span><span class="sxs-lookup"><span data-stu-id="118ee-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="118ee-164">Hello [службу субъектов](service-fabric-reliable-actors-platform.md) предоставляет функцию для удаления субъектов из удаленного вызывающего объекта:</span><span class="sxs-lookup"><span data-stu-id="118ee-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="118ee-165">Удаление субъект имеет следующие эффекты в зависимости от того, является ли субъект hello активна в данный момент hello.</span><span class="sxs-lookup"><span data-stu-id="118ee-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="118ee-166">**Активный субъект**</span><span class="sxs-lookup"><span data-stu-id="118ee-166">**Active Actor**</span></span>
  * <span data-ttu-id="118ee-167">Субъект удаляется из списка активных субъектов и деактивируется.</span><span class="sxs-lookup"><span data-stu-id="118ee-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="118ee-168">Состояние субъекта удаляется окончательно.</span><span class="sxs-lookup"><span data-stu-id="118ee-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="118ee-169">**Неактивный субъект**</span><span class="sxs-lookup"><span data-stu-id="118ee-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="118ee-170">Состояние субъекта удаляется окончательно.</span><span class="sxs-lookup"><span data-stu-id="118ee-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="118ee-171">Обратите внимание, что субъект не удается вызвать удалить на себя от одного из его методов субъекта, так как субъект hello не может быть удален во время выполнения в контексте вызова субъекта, в какие hello среды выполнения получил блокировку вокруг hello субъекта вызов tooenforce однопоточного доступа.</span><span class="sxs-lookup"><span data-stu-id="118ee-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="118ee-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="118ee-172">Next steps</span></span>
* [<span data-ttu-id="118ee-173">Таймеры и напоминания субъекта</span><span class="sxs-lookup"><span data-stu-id="118ee-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="118ee-174">События субъекта</span><span class="sxs-lookup"><span data-stu-id="118ee-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="118ee-175">Повторный вход субъекта</span><span class="sxs-lookup"><span data-stu-id="118ee-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="118ee-176">Диагностика и мониторинг производительности в Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="118ee-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="118ee-177">Справочная документация по API субъектов</span><span class="sxs-lookup"><span data-stu-id="118ee-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="118ee-178">Пример кода C#</span><span class="sxs-lookup"><span data-stu-id="118ee-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="118ee-179">Пример кода Java</span><span class="sxs-lookup"><span data-stu-id="118ee-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
