---
title: "Субъекты на Service Fabric aaaReliable | Документы Microsoft"
description: "Описывает, как службы Reliable Actor, располагаются на надежные службы и использовать функции hello платформы Service Fabric hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Использование службы Reliable Actor hello платформы Service Fabric
В этой статье объясняется, как работают службы Reliable Actor на платформе Azure Service Fabric hello. Запуск службы Reliable Actor в платформу, которая размещается в реализацию с отслеживанием состояния надежные службы с именем hello *службу субъектов*. службу субъектов Hello содержит все hello toomanage необходимые компоненты hello, жизненный цикл и диспетчеризации для вашего субъекты сообщение:

* Hello субъекта среда выполнения управляет жизненным циклом, сборщик мусора и регулирует доступ одним потоком.
* Прослушиватель субъекта службы удаленного взаимодействия принимает вызовы tooactors удаленного доступа и отправляет их tooa диспетчер tooroute toohello субъект, соответствующий экземпляр.
* Поставщик состояния субъекта Hello включает поставщики состояния (например, поставщик состояния hello надежного коллекций) и предоставляет адаптер для управления состоянием субъекта.

Эти компоненты вместе формы hello Reliable Actor framework.

## <a name="service-layering"></a>Структура служб
Так как саму службу hello субъекта является надежной службы, все hello [модель приложения](service-fabric-application-model.md), жизненный цикл, [упаковки](service-fabric-package-apps.md), [развертывания](service-fabric-deploy-remove-applications.md), обновление и масштабирование понятия Надежные службы применяются hello и теми же службами tooactor способом. 

![Структура службы субъектов][1]

Hello предыдущей схеме показаны hello отношения между структурой приложения Service Fabric hello и пользовательского кода. Синий элементы представляют собой платформу приложения hello надежного обмена, оранжевый представляет framework Reliable Actor hello и зеленым цветом в пользовательском коде.

В надежные службы к службе наследует hello `StatefulService` класса. производный от `StatefulServiceBase` (или `StatelessService` для служб без отслеживания состояния). В службы Reliable Actor использовать службу субъектов hello. службу субъектов Hello имеет различную реализацию hello `StatefulServiceBase` класс реализует шаблону субъекта hello, работают на субъекты. Так как саму службу hello субъекта является только реализация `StatefulServiceBase`, можно написать собственную службу, производный от `ActorService` и компоненты на уровне службы реализуйте hello же так, как при наследовании `StatefulService`, такие как:

* резервное копирование и восстановление службы;
* общие функции для всех субъектов, например автоматическое выключение;
* Удаленные вызовы процедур на самой службы субъекта hello и на каждый отдельный субъект.

> [!NOTE]
> В настоящее время службы с отслеживанием состояния не поддерживаются в Java или Linux.

### <a name="using-hello-actor-service"></a>С помощью службы субъекта hello
Субъект экземпляры имеют службу субъектов toohello доступ, в которой они выполняются. Через службу субъектов hello экземпляры субъекта программными средствами можно получить контекст службы hello. контекст службы Hello имеет секции с Идентификатором hello, имя службы, имя приложения и другие сведения от платформы Service Fabric.

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


Как и все надежные службы необходимо зарегистрировать службу hello субъекта с типом службы в среде выполнения Service Fabric hello. Для службы субъекта hello toorun экземпляры субъекта, тип субъекта также должен быть зарегистрирован со службой субъекта hello. Hello `ActorRuntime` метод регистрации выполняет это действие для субъектов. В простейшем случае hello можно зарегистрировать только тип субъекта и службу субъектов hello с параметрами по умолчанию будет использоваться неявно:

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

Кроме того можно использовать лямбда-выражения, предоставленные службой hello регистрации метод tooconstruct hello субъекта. Можно затем настроить службу субъектов hello и явно создает субъект экземпляров, в которых можно ввести субъекта tooyour зависимости через ее конструктор:

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a>Методы службы субъектов
Здравствуйте, служба реализует субъекта `IActorService` (C#) или `ActorService` (Java), который в свою очередь реализует `IService` (C#) или `Service` (Java). Это интерфейс hello, используемой в удаленном взаимодействии надежного обмена, разрешающее удаленных вызовов процедур на методы службы. Он содержит методы уровня службы, которые можно вызывать удаленно с помощью удаленных взаимодействий служб.

#### <a name="enumerating-actors"></a>Перечисление субъектов
Hello субъекта service позволяет клиенту tooenumerate метаданные о hello субъектов, размещение службы hello. Поскольку службу субъектов hello секционированных службы с отслеживанием состояния, перечисление выполняется на каждую секцию. Поскольку каждая секция может содержать много субъекты, перечисление hello возвращается как набор результатов по страницам. страницы приветствия перебор, пока не будут считаны все страницы. Следующий пример показывает как Hello toocreate список всех активных субъекты одной секции службу субъектов:

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a>Удаление субъектов
службу субъектов Hello также предоставляет функцию для удаления субъектов:

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

Дополнительные сведения об удалении субъекты и их состояния см. в разделе hello [субъекта жизненным циклом документации](service-fabric-reliable-actors-lifecycle.md).

### <a name="custom-actor-service"></a>Пользовательская служба субъектов
С помощью лямбда-выражения регистрации hello субъекта, можно зарегистрировать собственную службу пользовательского субъекта, производный от `ActorService` (C#) и `FabricActorService` (Java). и реализовать в ней собственные функции уровня службы. Для этого нужно написать класс службы, наследующий класс `ActorService` (C#) или `FabricActorService` (Java). Службы пользовательского субъект наследует все функциональные возможности среды выполнения hello субъекта из `ActorService` (C#) или `FabricActorService` (Java) и может быть используется tooimplement методы службы.

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a>Реализация резервного копирования и восстановления субъектов
 В следующем примере hello, hello пользовательских субъекта служба предоставляет метод tooback данные субъекта, используя преимущества hello удаленного взаимодействия прослушиватель уже присутствует в `ActorService`:

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


В этом примере `IMyActorService` — это контракт удаленного взаимодействия, который реализует класс `IService` (C#) и `Service` (Java), а затем реализуется классом `MyActorService`. Путем добавления этого контракта удаленного взаимодействия, методы `IMyActorService` , теперь также доступны tooa клиента путем создания прокси-сервер удаленного доступа через `ActorServiceProxy`:

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a>Модель приложения
Служб субъекта являются надежного обмена, поэтому модель приложения hello Здравствуйте, одинаково. Однако средства построения framework субъекта hello создан некоторые файлы модели приложения hello.

### <a name="service-manifest"></a>Манифест службы
средства построения framework субъекта Hello автоматически создавать hello содержимое файла ServiceManifest.xml службу субъектов. Этот файл содержит:

* Тип службы субъектов. Имя типа Hello создается основании актер проекта. На основе hello сохраняемости атрибута на ваш субъекта, hello флаг HasPersistedState также настраивается соответствующим образом.
* Пакет кода.
* Пакет конфигурации.
* Ресурсы и конечные точки.

### <a name="application-manifest"></a>Манифест приложения
средства построения framework субъекта Hello автоматически создать определение службы по умолчанию для службы субъекта. средства построения Hello заполнения свойств службы по умолчанию hello:

* Счетчик реплики набора определяется атрибутом сохраняемости hello на ваш субъекта. Изменения каждого атрибута сохраняемости время hello на ваш субъекта, соответствующим образом Сброс счетчика набора реплик hello в определении службы по умолчанию hello.
* Схемы секционирования и диапазона задаются tooUniform Int64 с полный диапазон ключа hello Int64.

## <a name="service-fabric-partition-concepts-for-actors"></a>Основные понятия о секции Service Fabric для субъектов
Службы субъектов — это секционированные службы с отслеживанием состояния. Каждая секция службы субъектов содержит набор субъектов. Секции службы автоматически распределяются между несколькими узлами Service Fabric. В результате распространяются экземпляры субъектов.

![Секционирование и распределение субъектов][5]

Службы Reliable Services создаются с использованием различных схем и диапазонов ключей секционирования. Служба субъектов Hello использует схему секционирования Int64 hello с субъектами toopartitions hello полный Int64 диапазона ключей toomap.

### <a name="actor-id"></a>Идентификатор субъекта
Каждый субъект, созданный в службе hello имеет уникальный идентификатор, связанный с ним, представленный hello `ActorId` класса. `ActorId`является непрозрачным значением идентификатора, который может использоваться для равномерного распределения субъекты секциях hello службы, создавая произвольные идентификаторы:

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


Каждый `ActorId` — хэшированное tooan Int64. Именно поэтому hello субъекта службы должен использовать схему секционирования Int64 с полный диапазон ключа hello Int64. Тем не менее для `ActorID` можно использовать пользовательские значения идентификаторов, включая строковые значения, а также GUID или UUID и значения типа Int64.

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

При использовании строк и идентификаторов GUID/UUID значения hello: Хешированные tooan Int64. Тем не менее, когда явно предоставляется Int64 tooan `ActorId`, hello Int64 сопоставит непосредственно tooa секции без дальнейшей хэширования. Можно использовать этот метод toocontrol, которой субъекты hello раздела помещаются в.

## <a name="next-steps"></a>Дальнейшие действия
* [Управление состоянием субъекта](service-fabric-reliable-actors-state-management.md)
* [Жизненный цикл субъектов и сбор мусора](service-fabric-reliable-actors-lifecycle.md)
* [Справочная документация по API субъектов](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Пример кода .NET](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Пример кода Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
