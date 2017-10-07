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
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>Жизненный цикл субъектов, автоматическая сборка мусора и удаление вручную
Субъект активируется hello первый раз выполняется вызов tooany его методов. Субъект — отключено (собраны как мусор средой выполнения субъекты hello), если он не используется для настроенного периода времени. Субъект и его состояние можно также удалить вручную в любое время.

## <a name="actor-activation"></a>Активация субъекта
При активации субъекта происходит hello следующее:

* При поступлении вызова для субъекта, который еще не активен, создается новый субъект.
* состояния субъекта Hello загружается в том случае, если он отслеживает состояние.
* Hello `OnActivateAsync` (C#) или `onActivateAsync` вызывается метод (Java), (который можно переопределить в реализации hello субъекта).
* Субъект Hello считается активным.

## <a name="actor-deactivation"></a>Деактивации субъекта
При отключении субъект происходит hello следующее:

* Если субъект не используется для некоторого периода времени, он удаляется из таблицы активных субъекты hello.
* Hello `OnDeactivateAsync` (C#) или `onDeactivateAsync` вызывается метод (Java), (который можно переопределить в реализации hello субъекта). Это приведет к очистке всех hello таймеры для субъекта hello. Операции с субъектом, такие как изменение состояния, не должны вызываться из этого метода.

> [!TIP]
> Hello субъекты структуры создаваемых средой выполнения некоторых [события, связанные tooactor активация и деактивация](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters). Они полезны при диагностике и мониторинге производительности.
>
>

### <a name="actor-garbage-collection"></a>Сборка мусора и субъекты
При отключении субъект ссылки toohello субъекта, освобождаются, и может быть сборщиком мусора обычно hello общеязыковая среда выполнения (CLR) или java сборщика мусора виртуальной машины (JVM). Сборка мусора только очищает hello объекта субъекта. Это осуществляется **не** удалить состояние, сохраненное в диспетчер состояния субъекта hello. Hello Далее время hello субъект активируется, создается новый объект субъекта и восстанавливается его состояние.

Что считается «используются» hello с целью деактивации и сборка мусора?

* Получение вызова
* `IRemindable.ReceiveReminderAsync`метод, вызываемый (применимо только в том случае, если субъект hello использует напоминания)

> [!NOTE]
> Если субъект hello использует таймеры и его таймера обратный вызов выполняется, он не **не** количество как «используются».
>
>

Прежде чем углубляться в подробности hello деактивации, очень важно toodefine hello следующими условиями:

* *Интервал сканирования*. Это интервал приветствия, на какие hello субъекты среды выполнения просматривает свою таблицу Active субъекты для субъектов, которые могут быть деактивированы и сборщиком мусора. значение по умолчанию Hello — 1 минута.
* *Время ожидания в состоянии простоя*. Это интервал времени, что субъект должен tooremain неиспользуемые hello (простоя), прежде чем он может быть отключен и сборщиком мусора. значение по умолчанию Hello составляет 60 минут.

Как правило необязательно toochange эти значения по умолчанию. При необходимости этот период времени можно изменить, вызвав метод `ActorServiceSettings` при регистрации [службы субъектов](service-fabric-reliable-actors-platform.md):

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
Для каждого активного субъект среда выполнения субъекта hello хранит информацию о hello количество времени, который он был неактивен (т. е. не используется). Среда выполнения субъекта Hello проверяет каждой из сторон hello каждый `ScanIntervalInSeconds` toosee, если он может быть мусора собираются и собирает его, если не используется `IdleTimeoutInSeconds`.

Каждый раз, когда используется субъект, его время простоя — too0 сброса. После этого субъекта hello может быть мусора только в том случае, если он снова будет бездействовать для `IdleTimeoutInSeconds`. Помните, что субъект считается toohave уже используется, если выполняется метод интерфейса субъекта или обратный вызов напоминания субъекта. Субъект — **не** считается toohave было использовано, если выполнено его обратный вызов таймера.

Hello следующей диаграмме показан жизненный цикл hello tooillustrate один субъект этих понятий.

![Пример времени простоя][1]

Hello примере показаны влияние hello вызовов субъекта, напоминаний и таймеров времени существования этого субъекта hello. следует упомянуть приведены следующие моменты, касающиеся hello пример Hello.

* Данного IdleTimeout заданы и too5 и 10 соответственно. (Единицы не имеет значения, поскольку нашей целью является только tooillustrate понятие hello.)
* Поиск Hello субъекты toobe мусора происходит на T = 0, 5, 10, 15, 20, 25, в соответствии с определением hello сканирования интервал, равный 5.
* Таймер срабатывает при T = 4, 8, 12, 16, 20 и 24, после чего выполняется обратный вызов. Он не влияет на время простоя hello объекта субъекта hello.
* Для вызова метода субъекта в T = 7 сбрасывает too0 hello время простоя и задержки hello сборку мусора для субъекта hello.
* Выполняет обратный вызов напоминания субъекта в T = 14 и дальнейшей задержки hello сборку мусора для субъекта hello.
* Во время hello просмотра сборки мусора в T = 25 время простоя hello субъекта наконец превышает hello тайм-аут простоя 10 и субъект hello выполняет сборку мусора.

Субъект никогда не удаляется сборщиком мусора, если выполняется какой-либо из его методов, независимо от того, сколько времени занимает выполнение этого метода. Как упоминалось ранее, hello выполнение методов интерфейса субъекта и обратные вызовы напоминание предотвращает сбор мусора, сбросив too0 время простоя hello субъекта. выполнение Hello обратные вызовы таймера не сбрасывает too0 hello время простоя. Тем не менее hello сборку мусора для субъекта hello откладывается до завершения выполнения обратного вызова таймера hello.

## <a name="deleting-actors-and-their-state"></a>Удаление субъектов и их состояние
Сборку мусора для отключенного субъекты только очищает hello объекта субъекта, но не удаляет данные, хранящиеся в диспетчере состояния субъекта. При субъект активировать повторно, его данные снова становится tooit, доступные через диспетчер состояния hello. В случаях, где субъекты хранить данные в диспетчер состояний и являются отключены, но никогда не включается повторно возможно, необходимые tooclean копии своих данных.

Hello [службу субъектов](service-fabric-reliable-actors-platform.md) предоставляет функцию для удаления субъектов из удаленного вызывающего объекта:

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

Удаление субъект имеет следующие эффекты в зависимости от того, является ли субъект hello активна в данный момент hello.

* **Активный субъект**
  * Субъект удаляется из списка активных субъектов и деактивируется.
  * Состояние субъекта удаляется окончательно.
* **Неактивный субъект**
  * Состояние субъекта удаляется окончательно.

Обратите внимание, что субъект не удается вызвать удалить на себя от одного из его методов субъекта, так как субъект hello не может быть удален во время выполнения в контексте вызова субъекта, в какие hello среды выполнения получил блокировку вокруг hello субъекта вызов tooenforce однопоточного доступа.

## <a name="next-steps"></a>Дальнейшие действия
* [Таймеры и напоминания субъекта](service-fabric-reliable-actors-timers-reminders.md)
* [События субъекта](service-fabric-reliable-actors-events.md)
* [Повторный вход субъекта](service-fabric-reliable-actors-reentrancy.md)
* [Диагностика и мониторинг производительности в Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Справочная документация по API субъектов](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Пример кода C#](https://github.com/Azure/servicefabric-samples)
* [Пример кода Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
