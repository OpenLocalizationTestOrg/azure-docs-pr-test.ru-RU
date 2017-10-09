---
title: "Управление состоянием субъекты aaaReliable | Документы Microsoft"
description: "Описание управления, сохранения и репликации субъектов Reliable Actors для обеспечения высокого уровня доступности."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a>Управление состоянием субъектов Reliable Actors
Субъекты Reliable Actors — это однопотоковые объекты для инкапсуляции логики и состояния. Поскольку субъекты выполняются в надежной службы, они надежно сохранять состояние при помощи hello же механизмов сохраняемости и репликации, которые использует надежные службы. Таким образом, субъектами не потеряли свое состояние после сбоев при повторной активации после сборки мусора или при их перемещении между узлами кластера из-за tooresource балансировки или обновления.

## <a name="state-persistence-and-replication"></a>Сохранение состояния и репликация
Все службы Reliable Actor считаются *с отслеживанием состояния* потому, что каждый экземпляр субъекта сопоставляется tooa уникального идентификатора. Это означает, что этой toohello повторные вызовы же идентификатор субъекта, перенаправленные toohello того же экземпляра субъекта. Без сохранения состояния системы, напротив, клиент вызывает не гарантируется toohello toobe направлено сервере каждый раз. Поэтому службы субъектов всегда отслеживают состояние.

Несмотря на то что субъекты отслеживают состояние, это не означает, что они надежно хранят состояние. Субъекты можно выбрать уровень hello сохранения состояния и репликации на основе своих данных требования к хранилищу.

* **Постоянное состояние**: состояние является сохраненного toodisk и реплицированных too3 или нескольких реплик. Этот вариант hello наиболее устойчивые состояния хранилища, где можно сохранить состояние до завершения создания кластера сбоя.
* **Непостоянное состояние**: состояние реплицированных too3 или нескольких реплик и хранятся только в памяти. Это обеспечивает устойчивость в случае сбоя узла, сбоя субъекта и во время обновления и балансировки ресурсов. Тем не менее не сохраненные toodisk. Поэтому если одновременно будут потеряны все реплики, состояние hello также теряется.
* **Не сохраненное состояние**: состояние не реплицируются и не запись toodisk. Этот уровень предназначен для субъектов, которые просто не должны toomaintain состояние надежно.

Каждый уровень сохраняемости — это просто другая конфигурация *поставщика состояний* и *репликации* службы. Независимо от того, имеется ли состояние записывается toodisk зависит от поставщика состояний hello--компонента hello в надежной службы, которая сохраняет состояние. А репликация зависит от того, на скольких репликах развертывается служба. С помощью надежного обмена оба hello поставщика состояний и счетчик реплики можно легко установить вручную. Hello субъекта framework предоставляет атрибут, что при использовании на субъект, автоматически выбирает поставщика состояния по умолчанию и автоматически создает параметры для tooachieve число реплики, одно из этих трех параметров сохраняемости. производный класс не наследуется атрибут statepersistence отвечает за хранение Hello, каждого типа субъекта необходимо предоставить свой уровень statepersistence отвечает за хранение.

### <a name="persisted-state"></a>Сохраненное состояние
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
Этот параметр использует поставщик состояния, который хранит данные на диске и автоматически устанавливает too3 число реплики службы hello.

### <a name="volatile-state"></a>Непостоянное состояние
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
Этот параметр использует поставщика в памяти — только состояния и наборы hello too3 число реплик.

### <a name="no-persisted-state"></a>Несохраняемое состояние
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
Этот параметр использует поставщика в памяти — только состояния и наборы hello too1 число реплик.

### <a name="defaults-and-generated-settings"></a>Значения по умолчанию и созданные параметры
При использовании hello `StatePersistence` атрибут поставщика состояний автоматически выбирается во время выполнения при запуске службы субъекта hello. Hello числа реплик, однако задается во время компиляции hello субъекта Visual Studio средства построения. Hello средства построения автоматически создавать *службу по умолчанию* для hello службы субъекта в файле ApplicationManifest.xml. Параметры создаются для **минимального размера набора реплик** и **целевого размера набора реплик**.

Вы можете изменить эти параметры вручную. Но каждый раз hello `StatePersistence` атрибут изменяется, то параметры hello будут toohello реплики набора размер значения по умолчанию выбран hello `StatePersistence` атрибут, переопределяя все предыдущие значения. Другими словами, являются hello значения, заданные в файле ServiceManifest.xml *только* переопределено во время построения, при изменении hello `StatePersistence` значение атрибута.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a>Диспетчер состояний:
У каждого экземпляра субъекта есть собственный диспетчер состояний: структура данных, подобная словарю, которая надежно хранит пары "ключ — значение". диспетчер состояния Hello является оболочкой вокруг поставщика состояний. Его можно использовать toostore данных независимо от того, используется параметр сохраняемости. Он не предоставляет никаких гарантий, работающей субъекта-службы может быть изменена из tooa параметр неустойчивого состояния (в памяти — только), хранящихся параметр состояния через последовательного обновления при сохранении данных. Однако это число возможных toochange реплики для запущенной службы.

Ключи диспетчера состояний должны быть строками. Значения являются универсальными и могут быть любого типа, в том числе пользовательского. Значения, хранящиеся в диспетчере состояния hello должна быть сериализуемым контракта данных, поскольку они могут передаваться по узлы tooother hello сети во время репликации и может записываться toodisk, в зависимости от настройки сохраняемости состояния субъекта.

диспетчер состояния Hello предоставляет управление состоянием, аналогичные toothose найден в словаре надежные общие методы словаря.

### <a name="accessing-state"></a>Доступ к состоянию
Состояние может осуществляться через диспетчер состояния hello по ключу. Методы диспетчера состояний асинхронны, так как они могут потребовать дискового ввода-вывода, если у субъектов сохраняемое состояние. При первом доступе объекты состояния кэшируются в памяти. Повторные операции доступа к объектам обращаются к объектам непосредственно из памяти и возвращают данные синхронно без дискового ввода-вывода или асинхронного переключения контекста. Объект состояния удаляется из кэша hello в hello в следующих случаях:

* Метод субъекта выдает необработанное исключение после извлекает из диспетчера состояний hello объект.
* Субъект повторно активируется после отключения или из-за сбоя.
* страницы поставщика состояния Hello состояния toodisk. Это поведение зависит от реализации поставщика состояния hello. поставщик состояния по умолчанию Hello для hello `Persisted` задано это поведение.

Состояние можно получить с помощью стандартного *получить* операцию, создающую `KeyNotFoundException`(C#) или `NoSuchElementException`(Java), если запись не существует для ключа hello:

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

Получить состояние можно также используя метод *TryGet*. Он не вызывает исключение, если для ключа запись не существует.

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a>Сохранение состояния
методы получения диспетчера состояния Hello возвращать объект tooan ссылки в локальной памяти. Изменение этого объекта в локальной памяти сама по себе не приводит к его toobe сохранены. Когда извлекается из диспетчер состояния hello и изменить объект, он должен быть повторно hello состояния диспетчера toobe сохранены.

Можно вставить состояние с помощью безусловный *задать*, которой hello эквивалент hello `dictionary["key"] = value` синтаксис:

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

Состояние можно добавить с помощью метода *Add*, Этот метод создает исключение `InvalidOperationException`(C#) или `IllegalStateException`(Java), когда он пытается tooadd ключ, который уже существует.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

Состояние также можно добавить с помощью метода *TryAdd*, Этот метод не исключение, когда он пытается tooadd ключ, который уже существует.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

В конце метода субъекта hello диспетчер состояний hello автоматически сохраняет любые значения, которые были добавлены или изменены операцией insert или update. «Сохранить» можно включить сохранение toodisk и репликации, в зависимости от параметров hello. Значения, которые не были изменены, не сохраняются и не реплицируются. Если значения не были изменены, hello операция сохранения не выполняет никаких действий. При ошибке сохранения, hello измененном состоянии удаляются, а исходное состояние hello перезагружается.

Можно также сохранить состояние вручную путем вызова hello `SaveStateAsync` hello субъекта базовый метод:

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a>Удаление состояния
Можно удалить состояние без возможности восстановления из диспетчера состояния субъекта, вызывающему Привет *удалить* метод. Этот метод создает исключение `KeyNotFoundException`(C#) или `NoSuchElementException`(Java), когда он пытается tooremove ключ, который не существует.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

Можно также удалить состояние без возможности восстановления с помощью hello *TryRemove* метод. Этот метод не исключение, когда он пытается tooremove ключ, который не существует.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия

Состояние, которое хранится в службы Reliable Actor должно быть сериализовано перед его письменного toodisk и реплицируются для обеспечения высокой доступности. Узнайте больше о [сериализации типа субъекта](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

Затем ознакомьтесь с [диагностикой и мониторингом производительности субъекта](service-fabric-reliable-actors-diagnostics.md).
