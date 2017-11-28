---
title: "Таймеры и напоминания Reliable Actors | Документация Майкрософт"
description: "Общие сведения о таймерах и напоминаниях для надежных субъектов Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 06b026ce06e0f16a77ac238de0af2263f272933c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="6a9dd-103">Таймеры и напоминания субъекта</span><span class="sxs-lookup"><span data-stu-id="6a9dd-103">Actor timers and reminders</span></span>
<span data-ttu-id="6a9dd-104">Субъекты могут планировать для себя периодические операции, регистрируя таймеры или напоминания.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="6a9dd-105">В этой статье показано, как использовать таймеры и напоминания, а также объясняются различия между ними.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="6a9dd-106">Таймеры субъектов</span><span class="sxs-lookup"><span data-stu-id="6a9dd-106">Actor timers</span></span>
<span data-ttu-id="6a9dd-107">Таймеры субъекта обеспечивают простую оболочку для таймера .NET или Java, чтобы методы обратного вызова учитывали гарантии пошагового параллелизма, предоставляемые средой выполнения Actors.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="6a9dd-108">Субъекты могут использовать методы `RegisterTimer`(C#) или `registerTimer`(Java) и `UnregisterTimer`(C#) или `unregisterTimer`(Java) в своем базовом классе для регистрации и отмены регистрации своих таймеров.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="6a9dd-109">В приведенном ниже примере показано использование интерфейсов API таймера.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="6a9dd-110">Эти интерфейсы API очень похожи на таймер .NET или Java.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="6a9dd-111">В этом примере при срабатывании таймера среда выполнения Actors вызовет метод `MoveObject`(C#) или `moveObject`(Java).</span><span class="sxs-lookup"><span data-stu-id="6a9dd-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="6a9dd-112">Этот метод гарантированно учитывает пошаговый параллелизм.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="6a9dd-113">Это означает, что никакие другие методы субъектов или обратные вызовы таймеров или напоминаний не будут выполняться до завершения этого обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="6a9dd-114">Следующий период таймера начинается после завершения выполнения обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="6a9dd-115">Это подразумевает, что таймер останавливается во время выполнения обратного вызова и запускается по завершении обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="6a9dd-116">Среда выполнения субъектов сохраняет изменения, внесенные в диспетчере состояния субъекта, по завершении обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="6a9dd-117">В случае ошибки при сохранении состояния объект данного субъекта отключается и активным становится новый экземпляр.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="6a9dd-118">При отключении субъекта в процессе сборки мусора все таймеры останавливаются.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="6a9dd-119">После этого обратные вызовы таймеров не выполняются.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="6a9dd-120">Кроме того, среда выполнения Actors не сохраняет никаких сведений о таймерах, запущенных до отключения.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="6a9dd-121">Регистрация таймеров, которые понадобятся субъекту при повторной активации в будущем, возлагается на субъект.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="6a9dd-122">Дополнительные сведения см. в статье [Сборка мусора и субъекты](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="6a9dd-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="6a9dd-123">Напоминания для субъекта</span><span class="sxs-lookup"><span data-stu-id="6a9dd-123">Actor reminders</span></span>
<span data-ttu-id="6a9dd-124">Напоминания — это механизм для срабатывания постоянных обратных вызовов по субъекту в заданные моменты времени.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="6a9dd-125">Их функциональные возможности аналогичны таймерам.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="6a9dd-126">В отличие от таймеров, напоминания активируются при любых обстоятельствах, пока субъект явно не отменит их регистрацию или не удалит их.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="6a9dd-127">В частности, напоминания срабатывают независимо от отключения субъектов и отработки отказов, так как в среде выполнения Actors сохраняются сведения о напоминаниях субъекта.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="6a9dd-128">Чтобы зарегистрировать напоминание, субъект вызывает метод `RegisterReminderAsync` , предоставленный в базовом классе, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="6a9dd-129">В этом примере `"Pay cell phone bill"` — имя напоминания.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="6a9dd-130">Это строка, которую субъект использует для уникальной идентификации напоминания.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="6a9dd-131">`BitConverter.GetBytes(amountInDollars)`(C#) — контекст, связанный с напоминанием.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="6a9dd-132">Он будет передан обратно субъекту в качестве аргумента обратного вызова напоминания, т. е. `IRemindable.ReceiveReminderAsync`(C#) или `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="6a9dd-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="6a9dd-133">Субъекты, использующие напоминания, должны реализовать интерфейс `IRemindable` (см. пример ниже).</span><span class="sxs-lookup"><span data-stu-id="6a9dd-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="6a9dd-134">При активации напоминания среда выполнения Reliable Actors вызовет метод субъекта `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="6a9dd-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="6a9dd-135">Субъект может зарегистрировать несколько напоминаний, и метод `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java) будет вызываться при активации любого из них.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="6a9dd-136">Субъект с помощью имени напоминания, переданного методу `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java), может выяснить, какое напоминание сработало.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="6a9dd-137">Когда вызов `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java) будет завершен, среда выполнения Actors сохранит состояние субъекта.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="6a9dd-138">В случае ошибки при сохранении состояния объект данного субъекта отключается и активным становится новый экземпляр.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="6a9dd-139">Чтобы отменить регистрацию напоминания, субъект вызывает метод `UnregisterReminderAsync`(C#) или `unregisterReminderAsync`(Java) (см. пример ниже).</span><span class="sxs-lookup"><span data-stu-id="6a9dd-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="6a9dd-140">Как показано выше, метод `UnregisterReminderAsync`(C#) или `unregisterReminderAsync`(Java) принимает интерфейс `IActorReminder`(C#) или `ActorReminder`(Java)</span><span class="sxs-lookup"><span data-stu-id="6a9dd-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="6a9dd-141">Базовый класс субъекта поддерживает метод `GetReminder`(C#) или `getReminder`(Java), с помощью которого можно получить интерфейс `IActorReminder`(C#) или `ActorReminder`(Java), передав имя напоминания.</span><span class="sxs-lookup"><span data-stu-id="6a9dd-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="6a9dd-142">Это удобно, так как субъекту не требуется сохранять интерфейс `IActorReminder`(C#) или `ActorReminder`(Java), возвращенный вызовом метода `RegisterReminder`(C#) или `registerReminder`(Java).</span><span class="sxs-lookup"><span data-stu-id="6a9dd-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a9dd-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a9dd-143">Next Steps</span></span>
<span data-ttu-id="6a9dd-144">Ознакомьтесь с событиями Reliable Actors и повторным входом:</span><span class="sxs-lookup"><span data-stu-id="6a9dd-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="6a9dd-145">События субъекта</span><span class="sxs-lookup"><span data-stu-id="6a9dd-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="6a9dd-146">Повторный вход субъекта</span><span class="sxs-lookup"><span data-stu-id="6a9dd-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
