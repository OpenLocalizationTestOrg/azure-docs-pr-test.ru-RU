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
# <a name="actor-events"></a>События субъекта
Субъект события предоставляют уведомления оптимальным способом toosend от клиентов toohello hello субъекта. Они предназначены для взаимодействия между субъектом и клиентами, и их не следует использовать для обмена данными между субъектами.

Hello следующем коде фрагменты Показать, как события toouse субъекта в приложении.

Определите интерфейс, который описывает события hello опубликованный hello actor. Этот интерфейс должен быть производным от hello `IActorEvents` интерфейса. аргументы Hello hello методов должны быть [контракта данных, сериализуемые](service-fabric-reliable-actors-notes-on-actor-type-serialization.md). Hello методы должны возвращать значение void, как событие уведомления — это один из способов и все усилия.

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
Объявление событий hello, опубликованный actor hello в интерфейсе hello субъекта.

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
На стороне клиента hello Реализуйте обработчик событий hello.

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

На клиентском компьютере hello создать субъект toohello прокси-сервера, который публикует события hello и подписываться tooits события.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

В событии hello переход на другой ресурс hello субъект может переключиться tooa другого процесса или узла. Hello субъекта прокси-сервер управляет hello активных подписок и автоматически подписывается их повторно. Можно управлять hello интервал повторной подписки через hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API. toounsubscribe hello используйте `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.

Субъект hello просто публикация событий hello мере их возникновения. Если подписчики toohello события, среда выполнения субъекты hello будет отправлено их hello уведомление.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>Дальнейшие действия
* [Повторный вход субъекта](service-fabric-reliable-actors-reentrancy.md)
* [Диагностика и мониторинг производительности в Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Справочная документация по API субъектов](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Пример кода C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Пример кода C# .NET Core](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Пример кода Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)
