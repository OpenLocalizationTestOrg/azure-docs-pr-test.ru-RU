---
title: "Примечания aaaReliable субъектов субъекта введите сериализации | Документы Microsoft"
description: "Обсуждаются основные требования для определения сериализуемые классы, которые могут быть используется toodefine состояний службы Reliable Actor структуры службы и интерфейсы"
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
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="bf1c8-103">Примечания о сериализации типов надежных субъектов Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bf1c8-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="bf1c8-104">аргументы Hello всех методов, типами результата задачи hello, возвращенные каждым методом в интерфейсе субъекта и объектов, хранящихся в диспетчер состояния субъекта должно быть [контракта данных, сериализуемые](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf1c8-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="bf1c8-105">Это также применимо аргументы toohello hello методов, определенных в [интерфейсах событий субъекта](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="bf1c8-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="bf1c8-106">(Методы интерфейсов для событий субъектов всегда возвращают значение void.)</span><span class="sxs-lookup"><span data-stu-id="bf1c8-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="bf1c8-107">Пользовательские типы данных</span><span class="sxs-lookup"><span data-stu-id="bf1c8-107">Custom data types</span></span>
<span data-ttu-id="bf1c8-108">В этом примере следующий интерфейс субъекта hello определяет метод, который возвращает тип пользовательских данных с именем `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="bf1c8-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="bf1c8-109">интерфейс Hello реализуется субъекта, использует диспетчер toostore hello состояние `VoicemailBox` объекта:</span><span class="sxs-lookup"><span data-stu-id="bf1c8-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="bf1c8-110">В этом примере hello `VoicemailBox` объект сериализуется при:</span><span class="sxs-lookup"><span data-stu-id="bf1c8-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="bf1c8-111">Hello объекта передается между экземпляром субъекта и вызывающий объект.</span><span class="sxs-lookup"><span data-stu-id="bf1c8-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="bf1c8-112">Hello объекта сохраняется в диспетчер состояния hello месте сохраненного toodisk и реплицировать tooother узлов.</span><span class="sxs-lookup"><span data-stu-id="bf1c8-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="bf1c8-113">Hello Reliable Actor платформа использует сериализации DataContract.</span><span class="sxs-lookup"><span data-stu-id="bf1c8-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="bf1c8-114">Таким образом, hello пользовательских объектов данных и их члены, должен быть помечен hello **DataContract** и **DataMember** соответственно.</span><span class="sxs-lookup"><span data-stu-id="bf1c8-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="bf1c8-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf1c8-115">Next steps</span></span>
* [<span data-ttu-id="bf1c8-116">Жизненный цикл субъектов и сбор мусора</span><span class="sxs-lookup"><span data-stu-id="bf1c8-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="bf1c8-117">Таймеры и напоминания субъекта</span><span class="sxs-lookup"><span data-stu-id="bf1c8-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="bf1c8-118">События субъекта</span><span class="sxs-lookup"><span data-stu-id="bf1c8-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="bf1c8-119">Повторный вход субъекта</span><span class="sxs-lookup"><span data-stu-id="bf1c8-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="bf1c8-120">Полиморфизм субъекта и объектно-ориентированные шаблоны проектирования</span><span class="sxs-lookup"><span data-stu-id="bf1c8-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="bf1c8-121">Диагностика и мониторинг производительности в Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="bf1c8-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
