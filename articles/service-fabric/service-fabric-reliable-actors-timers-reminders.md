---
title: "aaaReliable субъекты таймеров и напоминания | Документы Microsoft"
description: "Введение tootimers и напоминания о Service Fabric службы Reliable Actor."
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
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="27510-103">Таймеры и напоминания субъекта</span><span class="sxs-lookup"><span data-stu-id="27510-103">Actor timers and reminders</span></span>
<span data-ttu-id="27510-104">Субъекты могут планировать для себя периодические операции, регистрируя таймеры или напоминания.</span><span class="sxs-lookup"><span data-stu-id="27510-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="27510-105">В этой статье показано, как toouse таймеров и напоминания описаны hello различия между ними.</span><span class="sxs-lookup"><span data-stu-id="27510-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="27510-106">Таймеры субъектов</span><span class="sxs-lookup"><span data-stu-id="27510-106">Actor timers</span></span>
<span data-ttu-id="27510-107">Субъект таймеров обеспечивают Простая оболочка tooensure таймера .NET или Java, методы обратного вызова hello учитывают гарантирует параллелизма, основанного на включение hello, hello субъекты, среда выполнения предоставляет.</span><span class="sxs-lookup"><span data-stu-id="27510-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="27510-108">Субъекты можно использовать hello `RegisterTimer`(C#) или `registerTimer`(Java) и `UnregisterTimer`(C#) или `unregisterTimer`методы (Java) на своей основы класса tooregister и отменять регистрацию их таймеров.</span><span class="sxs-lookup"><span data-stu-id="27510-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="27510-109">Hello приведенном ниже примере показано использование hello API таймера.</span><span class="sxs-lookup"><span data-stu-id="27510-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="27510-110">Hello API-интерфейсы, схожий таймера toohello .NET или Java таймера.</span><span class="sxs-lookup"><span data-stu-id="27510-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="27510-111">В этом примере при hello таймера истекает, hello субъекты среда выполнения будет вызывать метод hello `MoveObject`(C#) или `moveObject`метод (Java).</span><span class="sxs-lookup"><span data-stu-id="27510-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="27510-112">метод Hello гарантируется toorespect hello основанных параллелизма.</span><span class="sxs-lookup"><span data-stu-id="27510-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="27510-113">Это означает, что никакие другие методы субъектов или обратные вызовы таймеров или напоминаний не будут выполняться до завершения этого обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="27510-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

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
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

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
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
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

<span data-ttu-id="27510-114">Hello следующего периода hello таймера запускается после выполнения завершения обратного вызова hello.</span><span class="sxs-lookup"><span data-stu-id="27510-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="27510-115">Это означает, что в этом hello таймер останавливается во время обратного вызова hello выполняется и запускается при завершении обратного вызова hello.</span><span class="sxs-lookup"><span data-stu-id="27510-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="27510-116">Среда выполнения субъекты Hello сохраняет изменения, внесенные toohello субъекта диспетчер состояния при завершении обратного вызова hello.</span><span class="sxs-lookup"><span data-stu-id="27510-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="27510-117">Если произошла ошибка при сохранении состояния hello, этот объект субъекта, будут отключены и новый экземпляр будет активирована.</span><span class="sxs-lookup"><span data-stu-id="27510-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="27510-118">Все таймеры, останавливаются при отключении hello субъекта в процессе сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="27510-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="27510-119">После этого обратные вызовы таймеров не выполняются.</span><span class="sxs-lookup"><span data-stu-id="27510-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="27510-120">Кроме того среда выполнения субъекты hello не сохраняют никакой информации о hello таймеры, которые запущены, прежде чем деактивации.</span><span class="sxs-lookup"><span data-stu-id="27510-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="27510-121">Он работает tooregister субъекта toohello все таймеры, которые ему необходимы при повторной активации в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="27510-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="27510-122">Дополнительные сведения см в подразделе hello о [субъекта мусора](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="27510-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="27510-123">Напоминания для субъекта</span><span class="sxs-lookup"><span data-stu-id="27510-123">Actor reminders</span></span>
<span data-ttu-id="27510-124">Напоминания, tootrigger механизм постоянные обратные вызовы на субъекта в определенное время.</span><span class="sxs-lookup"><span data-stu-id="27510-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="27510-125">Их функциональные возможности, аналогичные tootimers.</span><span class="sxs-lookup"><span data-stu-id="27510-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="27510-126">Но в отличие от таймеры, напоминания активируются при всех обстоятельствах до субъекта hello явно отменяет регистрацию их или hello субъекта явно удалены.</span><span class="sxs-lookup"><span data-stu-id="27510-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="27510-127">В частности напоминания активируются по субъекта деактивации и отработки отказа из-за выполнения субъекты hello сохраняет сведения о напоминаниях hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="27510-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="27510-128">tooregister напоминание субъект вызывает hello `RegisterReminderAsync` метод в базовом классе, hello, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="27510-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

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
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="27510-129">В этом примере `"Pay cell phone bill"` является именем напоминание hello.</span><span class="sxs-lookup"><span data-stu-id="27510-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="27510-130">Это строка, которая использует субъекта hello toouniquely идентификации напоминание.</span><span class="sxs-lookup"><span data-stu-id="27510-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="27510-131">`BitConverter.GetBytes(amountInDollars)`(C#) — hello контекст, который связан с напоминанием hello.</span><span class="sxs-lookup"><span data-stu-id="27510-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="27510-132">Оно передается назад toohello субъекта как обратный напоминание toohello аргумент, т. е. `IRemindable.ReceiveReminderAsync`(C#) или `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="27510-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="27510-133">Субъектов, использующих напоминания должен реализовывать hello `IRemindable` интерфейс, как показано в приведенном ниже примере hello.</span><span class="sxs-lookup"><span data-stu-id="27510-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

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

<span data-ttu-id="27510-134">Если оповещение инициируется, среда выполнения службы Reliable Actor hello будут вызывать hello `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java) метод для hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="27510-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="27510-135">Субъект можно зарегистрировать несколько напоминаний и hello `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java) метод вызывается, если любой из этих напоминания инициируется.</span><span class="sxs-lookup"><span data-stu-id="27510-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="27510-136">Hello субъекта можно использовать имя напоминание hello, которое передается в toohello `ReceiveReminderAsync`(C#) или `receiveReminderAsync`toofigure метод (Java), какие сработало оповещение.</span><span class="sxs-lookup"><span data-stu-id="27510-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="27510-137">Hello субъекты среда выполнения сохраняет состояние hello субъекта при hello `ReceiveReminderAsync`(C#) или `receiveReminderAsync`завершения вызова (Java).</span><span class="sxs-lookup"><span data-stu-id="27510-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="27510-138">Если произошла ошибка при сохранении состояния hello, этот объект субъекта, будут отключены и новый экземпляр будет активирована.</span><span class="sxs-lookup"><span data-stu-id="27510-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="27510-139">toounregister напоминание субъект вызывает hello `UnregisterReminderAsync`(C#) или `unregisterReminderAsync`(Java) метода, как показано в следующих примерах hello.</span><span class="sxs-lookup"><span data-stu-id="27510-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="27510-140">Здравствуйте, как показано выше, `UnregisterReminderAsync`(C#) или `unregisterReminderAsync`(Java) метод принимает `IActorReminder`(C#) или `ActorReminder`(Java) интерфейса.</span><span class="sxs-lookup"><span data-stu-id="27510-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="27510-141">Здравствуйте поддерживает базовый класс субъекта `GetReminder`(C#) или `getReminder`метод (Java), который может быть hello используется tooretrieve `IActorReminder`(C#) или `ActorReminder`интерфейса (Java), передав имя напоминание hello.</span><span class="sxs-lookup"><span data-stu-id="27510-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="27510-142">Это удобно, так как субъект hello не обязательно toopersist hello `IActorReminder`(C#) или `ActorReminder`интерфейс (Java), который был возвращен из hello `RegisterReminder`(C#) или `registerReminder`вызова метода (Java).</span><span class="sxs-lookup"><span data-stu-id="27510-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27510-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27510-143">Next Steps</span></span>
<span data-ttu-id="27510-144">Ознакомьтесь с событиями Reliable Actors и повторным входом:</span><span class="sxs-lookup"><span data-stu-id="27510-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="27510-145">События субъекта</span><span class="sxs-lookup"><span data-stu-id="27510-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="27510-146">Повторный вход субъекта</span><span class="sxs-lookup"><span data-stu-id="27510-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
