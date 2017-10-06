---
title: "aaaEvents в микрослужбами Azure на основе субъектов | Документы Microsoft"
description: "Введение tooevents для службы структуры службы Reliable Actor."
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
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="9a161-103">События субъекта</span><span class="sxs-lookup"><span data-stu-id="9a161-103">Actor events</span></span>
<span data-ttu-id="9a161-104">Субъект события предоставляют уведомления оптимальным способом toosend от клиентов toohello hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="9a161-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="9a161-105">Они предназначены для взаимодействия между субъектом и клиентами, и их не следует использовать для обмена данными между субъектами.</span><span class="sxs-lookup"><span data-stu-id="9a161-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="9a161-106">Hello следующем коде фрагменты Показать, как события toouse субъекта в приложении.</span><span class="sxs-lookup"><span data-stu-id="9a161-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="9a161-107">Определите интерфейс, который описывает события hello опубликованный hello actor.</span><span class="sxs-lookup"><span data-stu-id="9a161-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="9a161-108">Этот интерфейс должен быть производным от hello `IActorEvents` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9a161-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="9a161-109">аргументы Hello hello методов должны быть [контракта данных, сериализуемые](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="9a161-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="9a161-110">Hello методы должны возвращать значение void, как событие уведомления — это один из способов и все усилия.</span><span class="sxs-lookup"><span data-stu-id="9a161-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="9a161-111">Объявление событий hello, опубликованный actor hello в интерфейсе hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="9a161-111">Declare hello events published by hello actor in hello actor interface.</span></span>

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
<span data-ttu-id="9a161-112">На стороне клиента hello Реализуйте обработчик событий hello.</span><span class="sxs-lookup"><span data-stu-id="9a161-112">On hello client side, implement hello event handler.</span></span>

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

<span data-ttu-id="9a161-113">На клиентском компьютере hello создать субъект toohello прокси-сервера, который публикует события hello и подписываться tooits события.</span><span class="sxs-lookup"><span data-stu-id="9a161-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="9a161-114">В событии hello переход на другой ресурс hello субъект может переключиться tooa другого процесса или узла.</span><span class="sxs-lookup"><span data-stu-id="9a161-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="9a161-115">Hello субъекта прокси-сервер управляет hello активных подписок и автоматически подписывается их повторно.</span><span class="sxs-lookup"><span data-stu-id="9a161-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="9a161-116">Можно управлять hello интервал повторной подписки через hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="9a161-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="9a161-117">toounsubscribe hello используйте `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="9a161-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="9a161-118">Субъект hello просто публикация событий hello мере их возникновения.</span><span class="sxs-lookup"><span data-stu-id="9a161-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="9a161-119">Если подписчики toohello события, среда выполнения субъекты hello будет отправлено их hello уведомление.</span><span class="sxs-lookup"><span data-stu-id="9a161-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="9a161-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a161-120">Next steps</span></span>
* [<span data-ttu-id="9a161-121">Повторный вход субъекта</span><span class="sxs-lookup"><span data-stu-id="9a161-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="9a161-122">Диагностика и мониторинг производительности в Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="9a161-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="9a161-123">Справочная документация по API субъектов</span><span class="sxs-lookup"><span data-stu-id="9a161-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="9a161-124">Пример кода C#</span><span class="sxs-lookup"><span data-stu-id="9a161-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="9a161-125">Пример кода C# .NET Core</span><span class="sxs-lookup"><span data-stu-id="9a161-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="9a161-126">Пример кода Java</span><span class="sxs-lookup"><span data-stu-id="9a161-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
