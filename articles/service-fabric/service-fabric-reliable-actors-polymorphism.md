---
title: "aaaPolymorphism в framework службы Reliable Actor hello | Документы Microsoft"
description: "Постройте иерархии .NET интерфейсов и типов в функции tooreuse framework службы Reliable Actor hello и определения интерфейсов API."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="49e41-103">Полиморфизм в framework службы Reliable Actor hello</span><span class="sxs-lookup"><span data-stu-id="49e41-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="49e41-104">Hello службы Reliable Actor framework позволяет toobuild субъекты с использованием множества hello же методы, которые используются в объектно ориентированный проект.</span><span class="sxs-lookup"><span data-stu-id="49e41-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="49e41-105">Один из этих методов является полиморфизм, которая позволяет типы и интерфейсы tooinherit более обобщенный родительских объектов.</span><span class="sxs-lookup"><span data-stu-id="49e41-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="49e41-106">Наследование в framework службы Reliable Actor hello основном следует модели hello .NET с несколько дополнительных ограничений.</span><span class="sxs-lookup"><span data-stu-id="49e41-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="49e41-107">В случае Java, Linux он соответствует модели hello Java.</span><span class="sxs-lookup"><span data-stu-id="49e41-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="49e41-108">Интерфейсы</span><span class="sxs-lookup"><span data-stu-id="49e41-108">Interfaces</span></span>
<span data-ttu-id="49e41-109">Hello службы Reliable Actor framework требует toodefine toobe по крайней мере один интерфейс, реализованный тип субъекта.</span><span class="sxs-lookup"><span data-stu-id="49e41-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="49e41-110">Этот интерфейс не используется toogenerate класс-посредник, используются toocommunicate клиентов с вашей субъектами.</span><span class="sxs-lookup"><span data-stu-id="49e41-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="49e41-111">Интерфейсы могут наследовать от других интерфейсов, пока каждый интерфейс реализуется типом субъекта и все его родительские элементы в конечном счете являются производными от IActor(C#) или Actor(Java).</span><span class="sxs-lookup"><span data-stu-id="49e41-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="49e41-112">IActor(C#) и Actor(Java): hello определяемого платформой базовые интерфейсы для субъектов в hello платформы .NET и Java.</span><span class="sxs-lookup"><span data-stu-id="49e41-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="49e41-113">Таким образом hello полиморфизм классический пример с использованием фигур может выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="49e41-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![Иерархия интерфейса для формирования субъектов][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="49e41-115">Типы</span><span class="sxs-lookup"><span data-stu-id="49e41-115">Types</span></span>
<span data-ttu-id="49e41-116">Кроме того, можно создать иерархию типов субъектов, которые являются производными от базового субъекта класса hello, предоставляемых платформой hello.</span><span class="sxs-lookup"><span data-stu-id="49e41-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="49e41-117">В случае hello фигур, может быть базовым `Shape`(C#) или `ShapeImpl`(типа):</span><span class="sxs-lookup"><span data-stu-id="49e41-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

<span data-ttu-id="49e41-118">Подтипы для `Shape`(C#) или `ShapeImpl`(Java) можно переопределить методы базового hello.</span><span class="sxs-lookup"><span data-stu-id="49e41-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

<span data-ttu-id="49e41-119">Примечание hello `ActorService` атрибут типа субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="49e41-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="49e41-120">Этот атрибут сообщает framework Reliable Actor hello, он автоматически создавать службы для размещения агентам этого типа.</span><span class="sxs-lookup"><span data-stu-id="49e41-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="49e41-121">В некоторых случаях можно назвать toocreate базовый тип, который предназначен исключительно для совместного использования функции подтипов и никогда не будет использоваться tooinstantiate конкретных сторон.</span><span class="sxs-lookup"><span data-stu-id="49e41-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="49e41-122">В таких случаях следует использовать hello `abstract` tooindicate ключевое слово, которое никогда не будет создавать на основе этого типа субъекта.</span><span class="sxs-lookup"><span data-stu-id="49e41-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49e41-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49e41-123">Next steps</span></span>
* <span data-ttu-id="49e41-124">В разделе [как hello службы Reliable Actor framework использует платформы Service Fabric hello](service-fabric-reliable-actors-platform.md) tooprovide надежности, масштабируемости и согласованное состояние.</span><span class="sxs-lookup"><span data-stu-id="49e41-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="49e41-125">Дополнительные сведения о hello [жизненного цикла субъекта](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="49e41-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
