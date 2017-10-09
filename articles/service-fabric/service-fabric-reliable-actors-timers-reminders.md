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
# <a name="actor-timers-and-reminders"></a>Таймеры и напоминания субъекта
Субъекты могут планировать для себя периодические операции, регистрируя таймеры или напоминания. В этой статье показано, как toouse таймеров и напоминания описаны hello различия между ними.

## <a name="actor-timers"></a>Таймеры субъектов
Субъект таймеров обеспечивают Простая оболочка tooensure таймера .NET или Java, методы обратного вызова hello учитывают гарантирует параллелизма, основанного на включение hello, hello субъекты, среда выполнения предоставляет.

Субъекты можно использовать hello `RegisterTimer`(C#) или `registerTimer`(Java) и `UnregisterTimer`(C#) или `unregisterTimer`методы (Java) на своей основы класса tooregister и отменять регистрацию их таймеров. Hello приведенном ниже примере показано использование hello API таймера. Hello API-интерфейсы, схожий таймера toohello .NET или Java таймера. В этом примере при hello таймера истекает, hello субъекты среда выполнения будет вызывать метод hello `MoveObject`(C#) или `moveObject`метод (Java). метод Hello гарантируется toorespect hello основанных параллелизма. Это означает, что никакие другие методы субъектов или обратные вызовы таймеров или напоминаний не будут выполняться до завершения этого обратного вызова.

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

Hello следующего периода hello таймера запускается после выполнения завершения обратного вызова hello. Это означает, что в этом hello таймер останавливается во время обратного вызова hello выполняется и запускается при завершении обратного вызова hello.

Среда выполнения субъекты Hello сохраняет изменения, внесенные toohello субъекта диспетчер состояния при завершении обратного вызова hello. Если произошла ошибка при сохранении состояния hello, этот объект субъекта, будут отключены и новый экземпляр будет активирована.

Все таймеры, останавливаются при отключении hello субъекта в процессе сборки мусора. После этого обратные вызовы таймеров не выполняются. Кроме того среда выполнения субъекты hello не сохраняют никакой информации о hello таймеры, которые запущены, прежде чем деактивации. Он работает tooregister субъекта toohello все таймеры, которые ему необходимы при повторной активации в будущем hello. Дополнительные сведения см в подразделе hello о [субъекта мусора](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Напоминания для субъекта
Напоминания, tootrigger механизм постоянные обратные вызовы на субъекта в определенное время. Их функциональные возможности, аналогичные tootimers. Но в отличие от таймеры, напоминания активируются при всех обстоятельствах до субъекта hello явно отменяет регистрацию их или hello субъекта явно удалены. В частности напоминания активируются по субъекта деактивации и отработки отказа из-за выполнения субъекты hello сохраняет сведения о напоминаниях hello субъекта.

tooregister напоминание субъект вызывает hello `RegisterReminderAsync` метод в базовом классе, hello, как показано в следующий пример hello:

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

В этом примере `"Pay cell phone bill"` является именем напоминание hello. Это строка, которая использует субъекта hello toouniquely идентификации напоминание. `BitConverter.GetBytes(amountInDollars)`(C#) — hello контекст, который связан с напоминанием hello. Оно передается назад toohello субъекта как обратный напоминание toohello аргумент, т. е. `IRemindable.ReceiveReminderAsync`(C#) или `Remindable.receiveReminderAsync`(Java).

Субъектов, использующих напоминания должен реализовывать hello `IRemindable` интерфейс, как показано в приведенном ниже примере hello.

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

Если оповещение инициируется, среда выполнения службы Reliable Actor hello будут вызывать hello `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java) метод для hello субъекта. Субъект можно зарегистрировать несколько напоминаний и hello `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java) метод вызывается, если любой из этих напоминания инициируется. Hello субъекта можно использовать имя напоминание hello, которое передается в toohello `ReceiveReminderAsync`(C#) или `receiveReminderAsync`toofigure метод (Java), какие сработало оповещение.

Hello субъекты среда выполнения сохраняет состояние hello субъекта при hello `ReceiveReminderAsync`(C#) или `receiveReminderAsync`завершения вызова (Java). Если произошла ошибка при сохранении состояния hello, этот объект субъекта, будут отключены и новый экземпляр будет активирована.

toounregister напоминание субъект вызывает hello `UnregisterReminderAsync`(C#) или `unregisterReminderAsync`(Java) метода, как показано в следующих примерах hello.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Здравствуйте, как показано выше, `UnregisterReminderAsync`(C#) или `unregisterReminderAsync`(Java) метод принимает `IActorReminder`(C#) или `ActorReminder`(Java) интерфейса. Здравствуйте поддерживает базовый класс субъекта `GetReminder`(C#) или `getReminder`метод (Java), который может быть hello используется tooretrieve `IActorReminder`(C#) или `ActorReminder`интерфейса (Java), передав имя напоминание hello. Это удобно, так как субъект hello не обязательно toopersist hello `IActorReminder`(C#) или `ActorReminder`интерфейс (Java), который был возвращен из hello `RegisterReminder`(C#) или `registerReminder`вызова метода (Java).

## <a name="next-steps"></a>Дальнейшие действия
Ознакомьтесь с событиями Reliable Actors и повторным входом:
* [События субъекта](service-fabric-reliable-actors-events.md)
* [Повторный вход субъекта](service-fabric-reliable-actors-reentrancy.md)
