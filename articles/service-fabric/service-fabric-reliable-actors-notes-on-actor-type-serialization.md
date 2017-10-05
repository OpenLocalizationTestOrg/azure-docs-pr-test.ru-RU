---
title: "Reliable Actors: примечания о сериализации типов субъектов | Документация Майкрософт"
description: "В этой статье приведены сведения о базовых требованиях к определению сериализуемых классов, которые можно использовать для определения интерфейсов и состояний Reliable Actors в Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4b48b893e5a3bf5620f00a336576efe1ad63def8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="94025-103">Примечания о сериализации типов надежных субъектов Service Fabric</span><span class="sxs-lookup"><span data-stu-id="94025-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="94025-104">Аргументы всех методов, типы результатов задач, возвращаемых каждым методом в интерфейсе субъекта, и объекты, хранящиеся в диспетчере состояния субъекта, должны быть [сериализуемыми в контракт данных](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="94025-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="94025-105">Это также относится к аргументам методов, определенных в [интерфейсах событий субъекта](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="94025-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="94025-106">(Методы интерфейсов для событий субъектов всегда возвращают значение void.)</span><span class="sxs-lookup"><span data-stu-id="94025-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="94025-107">Пользовательские типы данных</span><span class="sxs-lookup"><span data-stu-id="94025-107">Custom data types</span></span>
<span data-ttu-id="94025-108">В этом примере приведенный ниже интерфейс субъекта определяет метод, возвращающий пользовательский тип данных `VoicemailBox`.</span><span class="sxs-lookup"><span data-stu-id="94025-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

<span data-ttu-id="94025-109">Этот интерфейс реализован субъектом, который использует диспетчер состояния для хранения объекта `VoicemailBox`.</span><span class="sxs-lookup"><span data-stu-id="94025-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

<span data-ttu-id="94025-110">В этом примере объект `VoicemailBox` сериализуется в следующих случаях.</span><span class="sxs-lookup"><span data-stu-id="94025-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="94025-111">Объект передается между экземпляром субъекта и вызывающим объектом.</span><span class="sxs-lookup"><span data-stu-id="94025-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="94025-112">Объект сохраняется в диспетчере состояния, где он сохраняется на диске и реплицируется на другие узлы.</span><span class="sxs-lookup"><span data-stu-id="94025-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="94025-113">Платформа Reliable Actors использует сериализацию DataContract.</span><span class="sxs-lookup"><span data-stu-id="94025-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="94025-114">Поэтому пользовательские объекты данных и их элементы должны быть аннотированы атрибутами **DataContract** и **DataMember**, соответственно.</span><span class="sxs-lookup"><span data-stu-id="94025-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a><span data-ttu-id="94025-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="94025-115">Next steps</span></span>
* [<span data-ttu-id="94025-116">Жизненный цикл субъектов и сбор мусора</span><span class="sxs-lookup"><span data-stu-id="94025-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="94025-117">Таймеры и напоминания субъекта</span><span class="sxs-lookup"><span data-stu-id="94025-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="94025-118">События субъекта</span><span class="sxs-lookup"><span data-stu-id="94025-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="94025-119">Повторный вход субъекта</span><span class="sxs-lookup"><span data-stu-id="94025-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="94025-120">Полиморфизм субъекта и объектно-ориентированные шаблоны проектирования</span><span class="sxs-lookup"><span data-stu-id="94025-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="94025-121">Диагностика и мониторинг производительности в Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="94025-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
