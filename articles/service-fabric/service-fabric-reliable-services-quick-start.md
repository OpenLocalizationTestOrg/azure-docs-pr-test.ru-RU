---
title: "aaaCreate первого приложения Service Fabric в C# | Документы Microsoft"
description: "Введение toocreating приложении Microsoft Azure Service Fabric с служб без отслеживания состояния и с отслеживанием состояния."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Приступая к работе с надежными службами
> [!div class="op_single_selector"]
> * [C# в Windows](service-fabric-reliable-services-quick-start.md)
> * [Java в Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Приложение Azure Service Fabric содержит одну или несколько служб, которые выполняют код. В этом руководстве показано, как toocreate без сохранения состояния и с отслеживанием состояния приложения Service Fabric с [надежного обмена](service-fabric-reliable-services-introduction.md).  В этом видеоролике Microsoft Virtual Academy также показано, как toocreate без сохранения состояния надежной службы:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Основные понятия
tooget к работе с надежного обмена, можно только необходимые toounderstand несколько основных понятий.

* **Тип службы**. Это ваша реализация службы. Определяется класс hello написании, расширяющий `StatelessService` и любой другой код или зависимости, используемый в этом документе, а также имя и номер версии.
* **Именованный экземпляр службы**: toorun службы, можно создавать именованные экземпляры типа службы, гораздо как при создании экземпляра объекта типа класса. Экземпляр службы имеет имя в форме hello URI с помощью hello» структуры: /» схемы, такие как «структуры: / MyApp/MyService».
* **Узел службы**: hello именованных экземпляров службы, создайте toorun потребность в хост-процесса. узел службы Hello — просто процесса, где можно запускать экземпляры службы.
* **Регистрации службы**. Регистрация объединяет все элементы. Hello службы тип должен быть зарегистрирован с hello Service Fabric среды выполнения службы размещения tooallow Service Fabric toocreate его экземпляры toorun.  

## <a name="create-a-stateless-service"></a>Создание службы без отслеживания состояния
Службы без отслеживания состояния — это тип службы, которая в данный момент нормы hello в облачных приложений. Он считается без сохранения состояния, поскольку сама служба hello не содержит данных, которые должны toobe хранятся надежно или высокой надежности. Когда экземпляр службы без отслеживания состояния завершает работу, все данные о его внутреннем состоянии будут утрачены. В этот тип службы, состояние должно быть сохраненного tooan внешнем хранилище, например Azure таблицы или базы данных SQL, для него toobe внесенные высокой доступности и надежности.

Запустите Visual Studio 2015 или Visual Studio 2017 от имени администратора и создайте проект приложения Service Fabric с именем *HelloWorld*.

![Используйте поле диалогового окна toocreate нового приложения Service Fabric для hello нового проекта](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Затем создайте проект службы без отслеживания состояния с именем *HelloWorldStateless*.

![Hello второго диалогового окна создания проекта службы без отслеживания состояния](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

Теперь решение содержит два проекта:

* *HelloWorld*. Это hello *приложения* проект, содержащий ваш *службы*. Он также содержит манифест приложения hello, описывающий приложения hello, а также несколько сценариев PowerShell, которые помогают toodeploy приложения.
* *HelloWorldStateless*. Это проект службы hello. Он содержит реализацию службы без отслеживания состояния hello.

## <a name="implement-hello-service"></a>Реализация службы hello
Откройте hello **HelloWorldStateless.cs** файла в проекте службы hello. В Service Fabric служба может выполнять любую бизнес-логику. API-Интерфейс службы Hello предоставляет две точки входа для кода:

* Вызывается метод *RunAsync*с открытой точкой входа, в котором можно начать выполнение любой рабочей нагрузки, например длительных вычислений.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Точка входа для обмена данными, к которой можно подключить любой стек связи, например ASP.NET Core. С ее помощью вы можете получать запросы от пользователей и других служб.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

В этом учебнике мы будем уделять hello `RunAsync()` метод точки входа. Используя его, вы можете сразу же начать выполнение кода.
шаблон проекта Hello включает пример реализации `RunAsync()` , увеличивает последовательного count.

> [!NOTE]
> Дополнительные сведения о как стека toowork взаимодействия см. [веб-API службы фабрики служб с резидентным OWIN](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

Hello платформа вызывает этот метод при помещенных и готов tooexecute является экземпляр службы. Для службы без отслеживания состояния, это просто означает при открытии hello экземпляр службы. Токен отмены, который предоставляется toocoordinate при закрытии toobe вашего экземпляра службы. В Service Fabric этого цикла открыть/закрыть экземпляра службы может выполняться много раз за время жизни hello hello службы в целом. Это может происходить по ряду причин.

* система Hello перемещает экземпляров служб для распределения ресурсов.
* В коде возникают ошибки.
* обновляется Hello приложения или системы.
* Базовое оборудование Hello возникает сбой.

Это согласование находится под управлением системы tookeep hello службы высокой доступности и правильно балансировкой.

Реализация `RunAsync()` не должна использовать синхронную блокировку. Реализация RunAsync должен вернуть задачу или Ожидание на любые долго выполняющиеся или блокирующие операции tooallow hello среды выполнения toocontinue. Примечание в hello `while(true)` цикл в предыдущем примере hello, возвращающие задачи `await Task.Delay()` используется. Если для рабочей нагрузки требуется синхронная блокировка, то в своей реализации `RunAsync` следует запланировать новую задачу с `Task.Run()`.

Отмена рабочей нагрузки является совместной усилий под управлением hello, предоставленный токен отмены. Hello система будет ожидать вашего tooend задачи (от успешного завершения, отмены или сбоя) перед переходом. Это hello важные toohonor отмены маркера, Готово любой работы и завершить работу `RunAsync()` максимально быстро при hello система запрашивает отмену.

В этом примере службы без отслеживания состояния hello число хранится в локальной переменной. Но так как службы без отслеживания состояния, hello значение, которое хранится существует только для текущего жизненного цикла hello его экземпляра службы. Если служба hello перемещает или перезагружается, значение hello теряются.

## <a name="create-a-stateful-service"></a>Создание службы с отслеживанием состояния
Service Fabric представляет новый вид службы с отслеживанием состояния. Службы с отслеживанием состояния могут сохранять состояние надежно внутри hello самой службы, совместно с hello код, который использует его. Состояние высокой надежности с помощью Service Fabric без внешнего хранилища hello необходимость toopersist состояния tooan.

tooconvert значение счетчика из без сохранения состояния toohighly доступны и постоянные, даже в том случае, когда служба hello перемещает или перезапуска необходимо службы с отслеживанием состояния.

В hello же *HelloWorld* приложения, можно добавить новую службу, щелкнув ссылки на службы hello в проект приложения hello и выбрав **Добавить -> Новая служба Service Fabric**.

![Добавление службы tooyour приложения Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Выберите **Служба с отслеживанием состояния** и присвойте имя *HelloWorldStateful*. Нажмите кнопку **ОК**.

![Используйте поле диалогового окна toocreate новой службы с отслеживанием состояния Service Fabric для hello нового проекта](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

Приложения должны появиться две службы: hello службы без отслеживания состояния *HelloWorldStateless* и службы с отслеживанием состояния hello *HelloWorldStateful*.

Службы с отслеживанием состояния имеет hello одной точки входа как службы без отслеживания состояния. Hello основное отличие заключается в доступности hello *поставщик состояния* , надежно сохранять состояние. Service Fabric поставляется с именем реализации поставщика состояния [надежного коллекции](service-fabric-reliable-services-reliable-collections.md), позволяет создавать надежные диспетчер состояния структуры реплицированные данные через hello. Служба Reliable Service с отслеживанием состояния использует этот поставщик состояний по умолчанию.

Откройте **HelloWorldStateful.cs** в *HelloWorldStateful*, который содержит следующий метод RunAsync hello:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()` работает одинаково в службах с отслеживанием и без отслеживания состояния. Тем не менее, в службы с отслеживанием состояния, платформа hello выполняет дополнительные действия от имени пользователя перед запуском `RunAsync()`. Эта работа может включать гарантирует, что hello надежного диспетчер состояния и надежного коллекции будут готовы toouse.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Надежные коллекций и hello надежного диспетчер состояния
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) является реализацией словаря, которые можно использовать tooreliably сохранение состояния в службе hello. С помощью Service Fabric и надежного коллекций можно хранить данные непосредственно в службе без необходимости hello внешнем постоянное хранилище. Надежные коллекции Reliable Collections делают данные высокодоступными. Service Fabric выполняет эту задачу, автоматически создавая несколько *реплик* службы и управляя ими. Он также предоставляет API, который абстрагирует дальней hello сложности решения этих реплик и их состояниями.

В Reliable Collections можно хранить любые типы объектов .NET, включая пользовательские типы. Необходимо только учитывать следующее.

* Service Fabric делает ваш штат обеспечивает высокую доступность *репликации* состояние между узлами и коллекций надежного хранения toolocal диска данных для каждой реплики. Это означает, что все объекты, хранящиеся в Reliable Collections, должны поддерживать *сериализацию*. По умолчанию использовать надежные коллекций [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) для сериализации, в этом случае важно toomake убедиться, что типы имеют [поддерживаемые hello сериализатор контракта данных](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) при использовании по умолчанию hello сериализатор.
* Когда вы зафиксируете транзакции в Reliable Collections, объекты реплицируются и становятся высокодоступными. Объекты, сохраненные в Reliable Collections, хранятся в локальной памяти вашей службы. Это означает, что имеется объект toohello локальную ссылку.
  
   Очень важно, что не размещают локальные экземпляры этих объектов без выполнения операции обновления на коллекцию надежных hello в транзакции. Это так, как изменения toolocal экземпляры объектов, не будут автоматически реплицироваться. Необходимо повторно вставить hello объекта обратно в словарь hello или использовать один из hello *обновление* методы в словаре hello.

Hello надежного диспетчер состояния управляет надежного коллекций. Вы можете просто запросить hello надежного диспетчер состояния надежного коллекции по имени в любое время и в любом месте в службе. Hello надежного диспетчер состояния гарантирует снова получить ссылку. Не рекомендуется сохранить ссылки tooreliable коллекции экземпляров в переменные-члены класса или свойств. Tooensure, ссылка hello необходимо уделить особое tooan экземпляра в любое время жизненного цикла службы hello. Hello надежного диспетчер состояний обрабатывает эту работу для вас и оптимизирован для повторные визиты.

### <a name="transactional-and-asynchronous-operations"></a>Транзакционные и асинхронные операции
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Надежные коллекции имеют многие hello и те же операции, их `System.Collections.Generic` и `System.Collections.Concurrent` аналоги за исключением LINQ. Операции в надежных коллекциях являются асинхронными. Это так, как операции записи с коллекциями надежного выполнения tooreplicate операций ввода-вывода и сохранения данных toodisk.

Операции Reliable Collections являются *транзакционными*, так что вы можете сохранять согласованное состояние между несколькими Reliable Collections и операциями. Например может вывода из очереди рабочего элемента из надежной очереди, выполняют операцию над его и сохранить результат hello в словаре надежные, все в одной транзакции. Это рассматривается как атомарную операцию, и гарантирует, что hello вся операция завершится успешно или будет произведен откат всей операции hello. Если ошибка возникает после dequeue hello элемента, но перед сохранением результат hello, откат всей транзакции hello и hello элемент остается в очереди hello для обработки.

## <a name="run-hello-application"></a>Запустите приложение hello
Теперь мы возвращаем toohello *HelloWorld* приложения. Теперь вы можете построить и развернуть свои службы. При нажатии клавиши **F5**, приложение будет tooyour встроенного и развернутого локального кластера.

После hello службы запущены, можно просмотреть события трассировки событий для Windows (ETW) создается hello в **события диагностики** окна. Обратите внимание, что отображаются события hello hello без сохранения состояния службы и службы с отслеживанием состояния hello в приложение hello. Вы можете приостановить поток hello, щелкнув hello **приостановить** кнопки. Затем можно проверить данные сообщения hello, развернув это сообщение.

> [!NOTE]
> Перед запуском приложения hello, убедитесь, что имеется локальная разработка кластера под управлением. Извлечение hello [руководство по началу работы](service-fabric-get-started.md) сведения о настройке локальной среде.
> 
> 

![Просмотр событий диагностики в Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Дальнейшие действия
[Отладка приложения Service Fabric с помощью Visual Studio](service-fabric-debugging-your-application.md)

[Приступая к работе со службами веб-API Service Fabric с саморазмещением OWIN](service-fabric-reliable-services-communication-webapi.md)

[Дополнительные сведения о надежных коллекциях](service-fabric-reliable-services-reliable-collections.md)

[Развертывание приложения](service-fabric-deploy-remove-applications.md)

[Обновление приложения](service-fabric-application-upgrade.md)

[Справочник разработчика по надежным службам](https://msdn.microsoft.com/library/azure/dn706529.aspx)

