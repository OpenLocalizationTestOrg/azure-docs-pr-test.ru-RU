---
title: "События в микрослужбах Azure на основе субъектов | Документация Майкрософт"
description: "Общие сведения о событиях для Reliable Actors Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: d936670c548ff709fc2e935d3f28d94e4bde8a04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="actor-events"></a><span data-ttu-id="3cff1-103">События субъекта</span><span class="sxs-lookup"><span data-stu-id="3cff1-103">Actor events</span></span>
<span data-ttu-id="3cff1-104">События субъекта — это способ отправки уведомлений от субъекта клиентам без гарантии доставки.</span><span class="sxs-lookup"><span data-stu-id="3cff1-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="3cff1-105">Они предназначены для взаимодействия между субъектом и клиентами, и их не следует использовать для обмена данными между субъектами.</span><span class="sxs-lookup"><span data-stu-id="3cff1-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="3cff1-106">В следующих фрагментах кода показано, как использовать события субъекта в приложении.</span><span class="sxs-lookup"><span data-stu-id="3cff1-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="3cff1-107">Определите интерфейс, который описывает события, публикуемые субъектом.</span><span class="sxs-lookup"><span data-stu-id="3cff1-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="3cff1-108">Он должен быть производным от интерфейса `IActorEvents` .</span><span class="sxs-lookup"><span data-stu-id="3cff1-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="3cff1-109">Аргументы методов должны относиться к типу [сериализуемых контрактов данных](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="3cff1-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="3cff1-110">Методы не должны ничего возвращать, так как уведомления являются однонаправленными и их доставка не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="3cff1-110">The methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="3cff1-111">Объявите события, публикуемые субъектом, в интерфейсе субъекта.</span><span class="sxs-lookup"><span data-stu-id="3cff1-111">Declare the events published by the actor in the actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="3cff1-112">На стороне клиента реализуйте обработчик событий.</span><span class="sxs-lookup"><span data-stu-id="3cff1-112">On the client side, implement the event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="3cff1-113">Также на стороне клиента создайте прокси-сервер для субъекта, который публикует события, и подпишитесь на его события.</span><span class="sxs-lookup"><span data-stu-id="3cff1-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="3cff1-114">В случае отработки отказа субъект может переключиться на другой процесс или узел.</span><span class="sxs-lookup"><span data-stu-id="3cff1-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="3cff1-115">Прокси-сервер субъекта управляет активными подписками и автоматически повторно выполняет подписывание на них.</span><span class="sxs-lookup"><span data-stu-id="3cff1-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="3cff1-116">Чтобы изменить интервал между повторными операциями подписывания, используйте API `ActorProxyEventExtensions.SubscribeAsync<TEvent>` .</span><span class="sxs-lookup"><span data-stu-id="3cff1-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="3cff1-117">Для отмены подписки используйте API `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` .</span><span class="sxs-lookup"><span data-stu-id="3cff1-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="3cff1-118">На стороне субъекта достаточно просто публиковать события, когда они происходят.</span><span class="sxs-lookup"><span data-stu-id="3cff1-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="3cff1-119">При наличии подписчиков на событие субъекта среда выполнения будет отправлять им уведомление.</span><span class="sxs-lookup"><span data-stu-id="3cff1-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="3cff1-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3cff1-120">Next steps</span></span>
* [<span data-ttu-id="3cff1-121">Повторный вход субъекта</span><span class="sxs-lookup"><span data-stu-id="3cff1-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="3cff1-122">Диагностика и мониторинг производительности в Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="3cff1-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="3cff1-123">Справочная документация по API субъектов</span><span class="sxs-lookup"><span data-stu-id="3cff1-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="3cff1-124">Пример кода C#</span><span class="sxs-lookup"><span data-stu-id="3cff1-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="3cff1-125">Пример кода C# .NET Core</span><span class="sxs-lookup"><span data-stu-id="3cff1-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="3cff1-126">Пример кода Java</span><span class="sxs-lookup"><span data-stu-id="3cff1-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
