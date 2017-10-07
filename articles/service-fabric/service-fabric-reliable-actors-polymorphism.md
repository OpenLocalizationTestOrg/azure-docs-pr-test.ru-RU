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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Полиморфизм в framework службы Reliable Actor hello
Hello службы Reliable Actor framework позволяет toobuild субъекты с использованием множества hello же методы, которые используются в объектно ориентированный проект. Один из этих методов является полиморфизм, которая позволяет типы и интерфейсы tooinherit более обобщенный родительских объектов. Наследование в framework службы Reliable Actor hello основном следует модели hello .NET с несколько дополнительных ограничений. В случае Java, Linux он соответствует модели hello Java.

## <a name="interfaces"></a>Интерфейсы
Hello службы Reliable Actor framework требует toodefine toobe по крайней мере один интерфейс, реализованный тип субъекта. Этот интерфейс не используется toogenerate класс-посредник, используются toocommunicate клиентов с вашей субъектами. Интерфейсы могут наследовать от других интерфейсов, пока каждый интерфейс реализуется типом субъекта и все его родительские элементы в конечном счете являются производными от IActor(C#) или Actor(Java). IActor(C#) и Actor(Java): hello определяемого платформой базовые интерфейсы для субъектов в hello платформы .NET и Java. Таким образом hello полиморфизм классический пример с использованием фигур может выглядеть примерно следующим образом:

![Иерархия интерфейса для формирования субъектов][shapes-interface-hierarchy]

## <a name="types"></a>Типы
Кроме того, можно создать иерархию типов субъектов, которые являются производными от базового субъекта класса hello, предоставляемых платформой hello. В случае hello фигур, может быть базовым `Shape`(C#) или `ShapeImpl`(типа):

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

Подтипы для `Shape`(C#) или `ShapeImpl`(Java) можно переопределить методы базового hello.

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

Примечание hello `ActorService` атрибут типа субъекта hello. Этот атрибут сообщает framework Reliable Actor hello, он автоматически создавать службы для размещения агентам этого типа. В некоторых случаях можно назвать toocreate базовый тип, который предназначен исключительно для совместного использования функции подтипов и никогда не будет использоваться tooinstantiate конкретных сторон. В таких случаях следует использовать hello `abstract` tooindicate ключевое слово, которое никогда не будет создавать на основе этого типа субъекта.

## <a name="next-steps"></a>Дальнейшие действия
* В разделе [как hello службы Reliable Actor framework использует платформы Service Fabric hello](service-fabric-reliable-actors-platform.md) tooprovide надежности, масштабируемости и согласованное состояние.
* Дополнительные сведения о hello [жизненного цикла субъекта](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
