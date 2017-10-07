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
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="ab32f-103">Повторный вход надежных субъектов</span><span class="sxs-lookup"><span data-stu-id="ab32f-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="ab32f-104">Среда выполнения службы Reliable Actor Hello, по умолчанию разрешает повторный вход на основе контекста логических вызовов.</span><span class="sxs-lookup"><span data-stu-id="ab32f-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="ab32f-105">Это делает возможным повторные входы toobe субъекты, если они находятся в hello же вызывать цепочку контекста.</span><span class="sxs-lookup"><span data-stu-id="ab32f-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="ab32f-106">Например субъект A отправляет сообщение tooActor B, который отправляет сообщение tooActor C. Как часть обработки сообщений hello Если субъект C вызывает субъекта A, приветственное сообщение реентерабельным, поэтому ему будет разрешен.</span><span class="sxs-lookup"><span data-stu-id="ab32f-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="ab32f-107">Любые другие сообщения, являющиеся частью другого контекста вызова, будут заблокированы на субъекте A до тех пор, пока он не завершит обработку.</span><span class="sxs-lookup"><span data-stu-id="ab32f-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="ab32f-108">Существует два варианта для субъекта повторного входа, определенные в hello `ActorReentrancyMode` перечисления:</span><span class="sxs-lookup"><span data-stu-id="ab32f-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="ab32f-109">`LogicalCallContext` (поведение по умолчанию);</span><span class="sxs-lookup"><span data-stu-id="ab32f-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="ab32f-110">`Disallowed` — отключает повторный вход.</span><span class="sxs-lookup"><span data-stu-id="ab32f-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="ab32f-111">Повторный вход можно настроить в параметрах `ActorService`во время регистрации.</span><span class="sxs-lookup"><span data-stu-id="ab32f-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="ab32f-112">параметр Hello применяется tooall субъекта экземпляров, созданных в службу субъектов hello.</span><span class="sxs-lookup"><span data-stu-id="ab32f-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="ab32f-113">Hello рассмотрим службу субъектов, задает режим повторного входа hello слишком`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="ab32f-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="ab32f-114">В этом случае, если субъект отправляет субъект tooanother повторные входящие сообщения, исключение типа `FabricException` будет создано.</span><span class="sxs-lookup"><span data-stu-id="ab32f-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="ab32f-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab32f-115">Next steps</span></span>
* <span data-ttu-id="ab32f-116">Дополнительные сведения о повторный вход в hello [справочная документация по API субъекта](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="ab32f-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
