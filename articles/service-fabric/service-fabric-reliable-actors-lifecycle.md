---
title: "Обзор жизненного цикла микрослужб Azure на основе субъектов | Документация Майкрософт"
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
ms.openlocfilehash: 75b7b77a0bef2051599a4f61183109cfb2ffff3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="b99de-103">Жизненный цикл субъектов, автоматическая сборка мусора и удаление вручную</span><span class="sxs-lookup"><span data-stu-id="b99de-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="b99de-104">Субъект активируется при первом вызове любого из его методов.</span><span class="sxs-lookup"><span data-stu-id="b99de-104">An actor is activated the first time a call is made to any of its methods.</span></span> <span data-ttu-id="b99de-105">Субъект деактивируется, если он не используется в течение заданного периода времени (при этом среда выполнения субъектов собирает мусор).</span><span class="sxs-lookup"><span data-stu-id="b99de-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="b99de-106">Субъект и его состояние можно также удалить вручную в любое время.</span><span class="sxs-lookup"><span data-stu-id="b99de-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="b99de-107">Активация субъекта</span><span class="sxs-lookup"><span data-stu-id="b99de-107">Actor activation</span></span>
<span data-ttu-id="b99de-108">При активации субъекта происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="b99de-108">When an actor is activated, the following occurs:</span></span>

* <span data-ttu-id="b99de-109">При поступлении вызова для субъекта, который еще не активен, создается новый субъект.</span><span class="sxs-lookup"><span data-stu-id="b99de-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="b99de-110">Загружается состояние субъекта (если это субъект с отслеживанием состояния).</span><span class="sxs-lookup"><span data-stu-id="b99de-110">The actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="b99de-111">Вызывается метод `OnActivateAsync` (C#) или `onActivateAsync` (Java) (он может быть переопределен в реализации субъекта).</span><span class="sxs-lookup"><span data-stu-id="b99de-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span>
* <span data-ttu-id="b99de-112">После этого субъект считается активным.</span><span class="sxs-lookup"><span data-stu-id="b99de-112">The actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="b99de-113">Деактивации субъекта</span><span class="sxs-lookup"><span data-stu-id="b99de-113">Actor deactivation</span></span>
<span data-ttu-id="b99de-114">При деактивации субъекта происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="b99de-114">When an actor is deactivated, the following occurs:</span></span>

* <span data-ttu-id="b99de-115">Если субъект не используется в течение некоторого периода времени, он удаляется из таблицы активных субъектов.</span><span class="sxs-lookup"><span data-stu-id="b99de-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span></span>
* <span data-ttu-id="b99de-116">Вызывается метод `OnDeactivateAsync` (C#) или `onDeactivateAsync` (Java) (он может быть переопределен в реализации субъекта).</span><span class="sxs-lookup"><span data-stu-id="b99de-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span> <span data-ttu-id="b99de-117">Это приводит к сбросу все таймеров для субъекта.</span><span class="sxs-lookup"><span data-stu-id="b99de-117">This clears all the timers for the actor.</span></span> <span data-ttu-id="b99de-118">Операции с субъектом, такие как изменение состояния, не должны вызываться из этого метода.</span><span class="sxs-lookup"><span data-stu-id="b99de-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="b99de-119">Среда выполнения субъектов Service Fabric генерирует некоторые [события, связанные с активацией и деактивацией субъектов](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="b99de-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="b99de-120">Они полезны при диагностике и мониторинге производительности.</span><span class="sxs-lookup"><span data-stu-id="b99de-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="b99de-121">Сборка мусора и субъекты</span><span class="sxs-lookup"><span data-stu-id="b99de-121">Actor garbage collection</span></span>
<span data-ttu-id="b99de-122">При деактивации субъекта ссылки на объект субъекта освобождаются и могут удаляться сборщиком мусора среды CLR или виртуальной машины Java в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="b99de-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="b99de-123">Сборщик мусора удаляет только объект субъекта; он **не** удаляет состояние, сохраненное в диспетчере состояний субъектов.</span><span class="sxs-lookup"><span data-stu-id="b99de-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span></span> <span data-ttu-id="b99de-124">При следующей активации субъекта создается новый объект субъекта и восстанавливается его состояние.</span><span class="sxs-lookup"><span data-stu-id="b99de-124">The next time the actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="b99de-125">Что считается "использованием" субъекта в контексте деактивации и сборки мусора?</span><span class="sxs-lookup"><span data-stu-id="b99de-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="b99de-126">Получение вызова</span><span class="sxs-lookup"><span data-stu-id="b99de-126">Receiving a call</span></span>
* <span data-ttu-id="b99de-127">`IRemindable.ReceiveReminderAsync` (применимо только в том случае, если субъект использует напоминания).</span><span class="sxs-lookup"><span data-stu-id="b99de-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="b99de-128">Если субъект использует таймеры и выполняется обратный вызов по таймеру, он **не** считается "используемым".</span><span class="sxs-lookup"><span data-stu-id="b99de-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="b99de-129">Прежде чем перейти к подробному рассмотрению деактивации, важно определить два понятия:</span><span class="sxs-lookup"><span data-stu-id="b99de-129">Before we go into the details of deactivation, it is important to define the following terms:</span></span>

* <span data-ttu-id="b99de-130">*Интервал сканирования*.</span><span class="sxs-lookup"><span data-stu-id="b99de-130">*Scan interval*.</span></span> <span data-ttu-id="b99de-131">Это интервал, с которым среда выполнения проверяет таблицу активных субъектов, чтобы определить, какие субъекты можно деактивировать и удалить во время сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="b99de-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="b99de-132">По умолчанию интервал равен 1 минуте.</span><span class="sxs-lookup"><span data-stu-id="b99de-132">The default value for this is 1 minute.</span></span>
* <span data-ttu-id="b99de-133">*Время ожидания в состоянии простоя*.</span><span class="sxs-lookup"><span data-stu-id="b99de-133">*Idle timeout*.</span></span> <span data-ttu-id="b99de-134">Это период времени, в течение которого субъект должен находиться в неиспользуемом состоянии (в состоянии простоя) до того, как он будет деактивирован и удален сборщиком мусора.</span><span class="sxs-lookup"><span data-stu-id="b99de-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="b99de-135">По умолчанию это время равно 60 минутам.</span><span class="sxs-lookup"><span data-stu-id="b99de-135">The default value for this is 60 minutes.</span></span>

<span data-ttu-id="b99de-136">Как правило, эти значения изменять не требуется.</span><span class="sxs-lookup"><span data-stu-id="b99de-136">Typically, you do not need to change these defaults.</span></span> <span data-ttu-id="b99de-137">При необходимости этот период времени можно изменить, вызвав метод `ActorServiceSettings` при регистрации [службы субъектов](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="b99de-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

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
<span data-ttu-id="b99de-138">Для каждого активного субъекта среда выполнения субъектов хранит информацию о времени, в течение которого он простаивает (не используется).</span><span class="sxs-lookup"><span data-stu-id="b99de-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="b99de-139">Среда проверяет каждый субъект с интервалом `ScanIntervalInSeconds`, чтобы узнать, можно ли его удалить во время сборки мусора, и удаляет его, если он не используется в течение интервала времени, равного `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="b99de-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="b99de-140">При каждом использовании субъекта его время ожидания в состоянии простоя обнуляется.</span><span class="sxs-lookup"><span data-stu-id="b99de-140">Anytime an actor is used, its idle time is reset to 0.</span></span> <span data-ttu-id="b99de-141">После этого субъект может быть удален сборщиком мусора только после бездействия в течение интервала времени, равного `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="b99de-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="b99de-142">Считается, что субъект был использован, если метод вызван через интерфейс субъекта или если выполнен обратный вызов по напоминанию.</span><span class="sxs-lookup"><span data-stu-id="b99de-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="b99de-143">**Не** считается, что субъект был использован, если выполняется обратный вызов по таймеру.</span><span class="sxs-lookup"><span data-stu-id="b99de-143">An actor is **not** considered to have been used if its timer callback is executed.</span></span>

<span data-ttu-id="b99de-144">На следующей схеме показан жизненный цикл одного субъекта, демонстрирующий описанные принципы.</span><span class="sxs-lookup"><span data-stu-id="b99de-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span></span>

![Пример времени простоя][1]

<span data-ttu-id="b99de-146">В примере показано влияние вызова методов субъекта, напоминаний и таймеров на время жизни субъекта.</span><span class="sxs-lookup"><span data-stu-id="b99de-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span></span> <span data-ttu-id="b99de-147">Обратите внимание на следующие важные моменты:</span><span class="sxs-lookup"><span data-stu-id="b99de-147">The following points about the example are worth mentioning:</span></span>

* <span data-ttu-id="b99de-148">ScanInterval и IdleTimeout установлены в 5 и 10 соответственно.</span><span class="sxs-lookup"><span data-stu-id="b99de-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span></span> <span data-ttu-id="b99de-149">(Единицы не имеют значения, поскольку наша цель — лишь проиллюстрировать концепцию.)</span><span class="sxs-lookup"><span data-stu-id="b99de-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span></span>
* <span data-ttu-id="b99de-150">Поиск субъектов, которые нужно удалить во время сборки мусора, происходит при T = 0, 5, 10, 15, 20 и 25, так как интервал сканирования равен 5.</span><span class="sxs-lookup"><span data-stu-id="b99de-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span></span>
* <span data-ttu-id="b99de-151">Таймер срабатывает при T = 4, 8, 12, 16, 20 и 24, после чего выполняется обратный вызов.</span><span class="sxs-lookup"><span data-stu-id="b99de-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="b99de-152">Это не влияет на время простоя субъекта.</span><span class="sxs-lookup"><span data-stu-id="b99de-152">It does not impact the idle time of the actor.</span></span>
* <span data-ttu-id="b99de-153">Вызов метода субъекта при T = 7 обнуляет время ожидания в состоянии простоя и откладывает удаление субъекта при сборке мусора.</span><span class="sxs-lookup"><span data-stu-id="b99de-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="b99de-154">При T = 14 выполняется обратный вызов по напоминанию, что снова откладывает удаление субъекта при сборке мусора.</span><span class="sxs-lookup"><span data-stu-id="b99de-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="b99de-155">На момент поиска объектов, которые можно удалить при сборке мусора, при T = 25 время простоя субъекта превышает заданное значение IdleTimeout (10) и субъект удаляется сборщиком мусора.</span><span class="sxs-lookup"><span data-stu-id="b99de-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span></span>

<span data-ttu-id="b99de-156">Субъект никогда не удаляется сборщиком мусора, если выполняется какой-либо из его методов, независимо от того, сколько времени занимает выполнение этого метода.</span><span class="sxs-lookup"><span data-stu-id="b99de-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="b99de-157">Как упоминалось ранее, выполнение методов, определенных в интерфейсе субъекта, и обратных вызовов по напоминанию предотвращает сборку мусора, так как время простоя субъекта обнуляется.</span><span class="sxs-lookup"><span data-stu-id="b99de-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span></span> <span data-ttu-id="b99de-158">Выполнение обратных вызовов по таймеру не обнуляет время простоя.</span><span class="sxs-lookup"><span data-stu-id="b99de-158">The execution of timer callbacks does not reset the idle time to 0.</span></span> <span data-ttu-id="b99de-159">Однако сборка мусора для субъекта откладывается до завершения выполнения функции обратного вызова по таймеру.</span><span class="sxs-lookup"><span data-stu-id="b99de-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="b99de-160">Удаление субъектов и их состояние</span><span class="sxs-lookup"><span data-stu-id="b99de-160">Deleting actors and their state</span></span>
<span data-ttu-id="b99de-161">При удалении деактивированных субъектов удаляется только объект субъекта; из диспетчера состояний субъекта данные не удаляются.</span><span class="sxs-lookup"><span data-stu-id="b99de-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="b99de-162">При повторной активации субъекта его данные снова становятся доступны в диспетчере состояний.</span><span class="sxs-lookup"><span data-stu-id="b99de-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span></span> <span data-ttu-id="b99de-163">Если субъекты, данные которых хранятся в диспетчере состояний, деактивируются и больше не активируются, может возникнуть необходимость в удалении связанных с ними данных.</span><span class="sxs-lookup"><span data-stu-id="b99de-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span></span>

<span data-ttu-id="b99de-164">В [службе субъектов](service-fabric-reliable-actors-platform.md) имеется функция удаления субъектов с помощью удаленного вызывающего объекта:</span><span class="sxs-lookup"><span data-stu-id="b99de-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

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

<span data-ttu-id="b99de-165">При удалении субъекта происходит следующее (в зависимости от того, были ли он активен в момент удаления):</span><span class="sxs-lookup"><span data-stu-id="b99de-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span></span>

* <span data-ttu-id="b99de-166">**Активный субъект**</span><span class="sxs-lookup"><span data-stu-id="b99de-166">**Active Actor**</span></span>
  * <span data-ttu-id="b99de-167">Субъект удаляется из списка активных субъектов и деактивируется.</span><span class="sxs-lookup"><span data-stu-id="b99de-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="b99de-168">Состояние субъекта удаляется окончательно.</span><span class="sxs-lookup"><span data-stu-id="b99de-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="b99de-169">**Неактивный субъект**</span><span class="sxs-lookup"><span data-stu-id="b99de-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="b99de-170">Состояние субъекта удаляется окончательно.</span><span class="sxs-lookup"><span data-stu-id="b99de-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="b99de-171">Обратите внимание, что субъект не может удалить себя, воспользовавшись одним из собственных методов, поскольку нельзя удалить субъект, выполняемый в контексте вызова субъектов, где для обеспечения однопоточного доступа среда выполнения блокирует вызов субъекта.</span><span class="sxs-lookup"><span data-stu-id="b99de-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b99de-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b99de-172">Next steps</span></span>
* [<span data-ttu-id="b99de-173">Таймеры и напоминания субъекта</span><span class="sxs-lookup"><span data-stu-id="b99de-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="b99de-174">События субъекта</span><span class="sxs-lookup"><span data-stu-id="b99de-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="b99de-175">Повторный вход субъекта</span><span class="sxs-lookup"><span data-stu-id="b99de-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="b99de-176">Диагностика и мониторинг производительности в Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="b99de-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="b99de-177">Справочная документация по API субъектов</span><span class="sxs-lookup"><span data-stu-id="b99de-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="b99de-178">Пример кода C#</span><span class="sxs-lookup"><span data-stu-id="b99de-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="b99de-179">Пример кода Java</span><span class="sxs-lookup"><span data-stu-id="b99de-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
