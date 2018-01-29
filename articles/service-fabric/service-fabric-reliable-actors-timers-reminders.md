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
ms.date: 11/02/2017
ms.author: vturecek
ms.openlocfilehash: f61743a7925c26767118dcb2d18799c26f880156
ms.sourcegitcommit: c7215d71e1cdeab731dd923a9b6b6643cee6eb04
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="actor-timers-and-reminders"></a>Таймеры и напоминания субъекта
Субъекты могут планировать для себя периодические операции, регистрируя таймеры или напоминания. В этой статье показано, как использовать таймеры и напоминания, а также объясняются различия между ними.

## <a name="actor-timers"></a>Таймеры субъектов
Таймеры субъекта обеспечивают простую оболочку для таймера .NET или Java, чтобы методы обратного вызова учитывали гарантии пошагового параллелизма, предоставляемые средой выполнения Actors.

Субъекты могут использовать методы `RegisterTimer`(C#) или `registerTimer`(Java) и `UnregisterTimer`(C#) или `unregisterTimer`(Java) в своем базовом классе для регистрации и отмены регистрации своих таймеров. В приведенном ниже примере показано использование интерфейсов API таймера. Эти интерфейсы API очень похожи на таймер .NET или Java. В этом примере при срабатывании таймера среда выполнения Actors вызовет метод `MoveObject`(C#) или `moveObject`(Java). Этот метод гарантированно учитывает пошаговый параллелизм. Это означает, что никакие другие методы субъектов или обратные вызовы таймеров или напоминаний не будут выполняться до завершения этого обратного вызова.

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

Следующий период таймера начинается после завершения выполнения обратного вызова. Это подразумевает, что таймер останавливается во время выполнения обратного вызова и запускается по завершении обратного вызова.

Среда выполнения субъектов сохраняет изменения, внесенные в диспетчере состояния субъекта, по завершении обратного вызова. В случае ошибки при сохранении состояния объект данного субъекта отключается и активным становится новый экземпляр.

При отключении субъекта в процессе сборки мусора все таймеры останавливаются. После этого обратные вызовы таймеров не выполняются. Кроме того, среда выполнения Actors не сохраняет никаких сведений о таймерах, запущенных до отключения. Регистрация таймеров, которые понадобятся субъекту при повторной активации в будущем, возлагается на субъект. Дополнительные сведения см. в статье [Сборка мусора и субъекты](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Напоминания для субъекта
Напоминания — это механизм для срабатывания постоянных обратных вызовов по субъекту в заданные моменты времени. Их функциональные возможности аналогичны таймерам. В отличие от таймеров, напоминания активируются при любых обстоятельствах, пока субъект явно не отменит их регистрацию или не удалит их. В частности, напоминания срабатываются независимо от отключения субъектов и отработки отказов, так как в среде выполнения Actors сохраняются данные напоминаний субъекта, для которых используется его поставщик состояний. Обратите внимание, что надежность напоминания зависит от гарантий надежности состояния, предоставленных поставщиком состояний субъекта. Это означает, что для субъектов, наличие сведений о состоянии которых имеет значение None, напоминания не будет отправляться после отработки отказа. 

Чтобы зарегистрировать напоминание, субъект вызывает метод `RegisterReminderAsync` , предоставленный в базовом классе, как показано в примере ниже.

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

В этом примере `"Pay cell phone bill"` — имя напоминания. Это строка, которую субъект использует для уникальной идентификации напоминания. `BitConverter.GetBytes(amountInDollars)`(C#) — контекст, связанный с напоминанием. Он будет передан обратно субъекту в качестве аргумента обратного вызова напоминания, т. е. `IRemindable.ReceiveReminderAsync`(C#) или `Remindable.receiveReminderAsync`(Java).

Субъекты, использующие напоминания, должны реализовать интерфейс `IRemindable` (см. пример ниже).

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

При активации напоминания среда выполнения Reliable Actors вызовет метод субъекта `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java). Субъект может зарегистрировать несколько напоминаний, и метод `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java) будет вызываться при активации любого из них. Субъект с помощью имени напоминания, переданного методу `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java), может выяснить, какое напоминание сработало.

Когда вызов `ReceiveReminderAsync`(C#) или `receiveReminderAsync`(Java) будет завершен, среда выполнения Actors сохранит состояние субъекта. В случае ошибки при сохранении состояния объект данного субъекта отключается и активным становится новый экземпляр.

Чтобы отменить регистрацию напоминания, субъект вызывает метод `UnregisterReminderAsync`(C#) или `unregisterReminderAsync`(Java) (см. пример ниже).

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Как показано выше, метод `UnregisterReminderAsync`(C#) или `unregisterReminderAsync`(Java) принимает интерфейс `IActorReminder`(C#) или `ActorReminder`(Java) Базовый класс субъекта поддерживает метод `GetReminder`(C#) или `getReminder`(Java), с помощью которого можно получить интерфейс `IActorReminder`(C#) или `ActorReminder`(Java), передав имя напоминания. Это удобно, так как субъекту не требуется сохранять интерфейс `IActorReminder`(C#) или `ActorReminder`(Java), возвращенный вызовом метода `RegisterReminder`(C#) или `registerReminder`(Java).

## <a name="next-steps"></a>Дальнейшие действия
Ознакомьтесь с событиями Reliable Actors и повторным входом:
* [События субъекта](service-fabric-reliable-actors-events.md)
* [Повторный вход субъекта](service-fabric-reliable-actors-reentrancy.md)
