---
title: "aaaReentrancy в микрослужбами Azure на основе субъектов | Документы Microsoft"
description: "Введение tooreentrancy для Service Fabric Reliable Actors"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a>Повторный вход надежных субъектов
Среда выполнения службы Reliable Actor Hello, по умолчанию разрешает повторный вход на основе контекста логических вызовов. Это делает возможным повторные входы toobe субъекты, если они находятся в hello же вызывать цепочку контекста. Например субъект A отправляет сообщение tooActor B, который отправляет сообщение tooActor C. Как часть обработки сообщений hello Если субъект C вызывает субъекта A, приветственное сообщение реентерабельным, поэтому ему будет разрешен. Любые другие сообщения, являющиеся частью другого контекста вызова, будут заблокированы на субъекте A до тех пор, пока он не завершит обработку.

Существует два варианта для субъекта повторного входа, определенные в hello `ActorReentrancyMode` перечисления:

* `LogicalCallContext` (поведение по умолчанию);
* `Disallowed` — отключает повторный вход.

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
Повторный вход можно настроить в параметрах `ActorService`во время регистрации. параметр Hello применяется tooall субъекта экземпляров, созданных в службу субъектов hello.

Hello рассмотрим службу субъектов, задает режим повторного входа hello слишком`ActorReentrancyMode.Disallowed`. В этом случае, если субъект отправляет субъект tooanother повторные входящие сообщения, исключение типа `FabricException` будет создано.

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о повторный вход в hello [справочная документация по API субъекта](https://msdn.microsoft.com/library/azure/dn971626.aspx)
