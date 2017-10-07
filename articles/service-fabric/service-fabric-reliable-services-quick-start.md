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
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="b3b73-103">Приступая к работе с надежными службами</span><span class="sxs-lookup"><span data-stu-id="b3b73-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3b73-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="b3b73-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="b3b73-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="b3b73-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="b3b73-106">Приложение Azure Service Fabric содержит одну или несколько служб, которые выполняют код.</span><span class="sxs-lookup"><span data-stu-id="b3b73-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="b3b73-107">В этом руководстве показано, как toocreate без сохранения состояния и с отслеживанием состояния приложения Service Fabric с [надежного обмена](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b3b73-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="b3b73-108">В этом видеоролике Microsoft Virtual Academy также показано, как toocreate без сохранения состояния надежной службы:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="b3b73-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="b3b73-109">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="b3b73-109">Basic concepts</span></span>
<span data-ttu-id="b3b73-110">tooget к работе с надежного обмена, можно только необходимые toounderstand несколько основных понятий.</span><span class="sxs-lookup"><span data-stu-id="b3b73-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="b3b73-111">**Тип службы**. Это ваша реализация службы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="b3b73-112">Определяется класс hello написании, расширяющий `StatelessService` и любой другой код или зависимости, используемый в этом документе, а также имя и номер версии.</span><span class="sxs-lookup"><span data-stu-id="b3b73-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="b3b73-113">**Именованный экземпляр службы**: toorun службы, можно создавать именованные экземпляры типа службы, гораздо как при создании экземпляра объекта типа класса.</span><span class="sxs-lookup"><span data-stu-id="b3b73-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="b3b73-114">Экземпляр службы имеет имя в форме hello URI с помощью hello» структуры: /» схемы, такие как «структуры: / MyApp/MyService».</span><span class="sxs-lookup"><span data-stu-id="b3b73-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="b3b73-115">**Узел службы**: hello именованных экземпляров службы, создайте toorun потребность в хост-процесса.</span><span class="sxs-lookup"><span data-stu-id="b3b73-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="b3b73-116">узел службы Hello — просто процесса, где можно запускать экземпляры службы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="b3b73-117">**Регистрации службы**. Регистрация объединяет все элементы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="b3b73-118">Hello службы тип должен быть зарегистрирован с hello Service Fabric среды выполнения службы размещения tooallow Service Fabric toocreate его экземпляры toorun.</span><span class="sxs-lookup"><span data-stu-id="b3b73-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="b3b73-119">Создание службы без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="b3b73-119">Create a stateless service</span></span>
<span data-ttu-id="b3b73-120">Службы без отслеживания состояния — это тип службы, которая в данный момент нормы hello в облачных приложений.</span><span class="sxs-lookup"><span data-stu-id="b3b73-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="b3b73-121">Он считается без сохранения состояния, поскольку сама служба hello не содержит данных, которые должны toobe хранятся надежно или высокой надежности.</span><span class="sxs-lookup"><span data-stu-id="b3b73-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="b3b73-122">Когда экземпляр службы без отслеживания состояния завершает работу, все данные о его внутреннем состоянии будут утрачены.</span><span class="sxs-lookup"><span data-stu-id="b3b73-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="b3b73-123">В этот тип службы, состояние должно быть сохраненного tooan внешнем хранилище, например Azure таблицы или базы данных SQL, для него toobe внесенные высокой доступности и надежности.</span><span class="sxs-lookup"><span data-stu-id="b3b73-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="b3b73-124">Запустите Visual Studio 2015 или Visual Studio 2017 от имени администратора и создайте проект приложения Service Fabric с именем *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="b3b73-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Используйте поле диалогового окна toocreate нового приложения Service Fabric для hello нового проекта](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="b3b73-126">Затем создайте проект службы без отслеживания состояния с именем *HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="b3b73-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Hello второго диалогового окна создания проекта службы без отслеживания состояния](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="b3b73-128">Теперь решение содержит два проекта:</span><span class="sxs-lookup"><span data-stu-id="b3b73-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="b3b73-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="b3b73-129">*HelloWorld*.</span></span> <span data-ttu-id="b3b73-130">Это hello *приложения* проект, содержащий ваш *службы*.</span><span class="sxs-lookup"><span data-stu-id="b3b73-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="b3b73-131">Он также содержит манифест приложения hello, описывающий приложения hello, а также несколько сценариев PowerShell, которые помогают toodeploy приложения.</span><span class="sxs-lookup"><span data-stu-id="b3b73-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="b3b73-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="b3b73-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="b3b73-133">Это проект службы hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-133">This is hello service project.</span></span> <span data-ttu-id="b3b73-134">Он содержит реализацию службы без отслеживания состояния hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="b3b73-135">Реализация службы hello</span><span class="sxs-lookup"><span data-stu-id="b3b73-135">Implement hello service</span></span>
<span data-ttu-id="b3b73-136">Откройте hello **HelloWorldStateless.cs** файла в проекте службы hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="b3b73-137">В Service Fabric служба может выполнять любую бизнес-логику.</span><span class="sxs-lookup"><span data-stu-id="b3b73-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="b3b73-138">API-Интерфейс службы Hello предоставляет две точки входа для кода:</span><span class="sxs-lookup"><span data-stu-id="b3b73-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="b3b73-139">Вызывается метод *RunAsync*с открытой точкой входа, в котором можно начать выполнение любой рабочей нагрузки, например длительных вычислений.</span><span class="sxs-lookup"><span data-stu-id="b3b73-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="b3b73-140">Точка входа для обмена данными, к которой можно подключить любой стек связи, например ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="b3b73-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="b3b73-141">С ее помощью вы можете получать запросы от пользователей и других служб.</span><span class="sxs-lookup"><span data-stu-id="b3b73-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="b3b73-142">В этом учебнике мы будем уделять hello `RunAsync()` метод точки входа.</span><span class="sxs-lookup"><span data-stu-id="b3b73-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="b3b73-143">Используя его, вы можете сразу же начать выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="b3b73-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="b3b73-144">шаблон проекта Hello включает пример реализации `RunAsync()` , увеличивает последовательного count.</span><span class="sxs-lookup"><span data-stu-id="b3b73-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="b3b73-145">Дополнительные сведения о как стека toowork взаимодействия см. [веб-API службы фабрики служб с резидентным OWIN](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="b3b73-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="b3b73-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="b3b73-146">RunAsync</span></span>
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

<span data-ttu-id="b3b73-147">Hello платформа вызывает этот метод при помещенных и готов tooexecute является экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="b3b73-148">Для службы без отслеживания состояния, это просто означает при открытии hello экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="b3b73-149">Токен отмены, который предоставляется toocoordinate при закрытии toobe вашего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="b3b73-150">В Service Fabric этого цикла открыть/закрыть экземпляра службы может выполняться много раз за время жизни hello hello службы в целом.</span><span class="sxs-lookup"><span data-stu-id="b3b73-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="b3b73-151">Это может происходить по ряду причин.</span><span class="sxs-lookup"><span data-stu-id="b3b73-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="b3b73-152">система Hello перемещает экземпляров служб для распределения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b3b73-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="b3b73-153">В коде возникают ошибки.</span><span class="sxs-lookup"><span data-stu-id="b3b73-153">Faults occur in your code.</span></span>
* <span data-ttu-id="b3b73-154">обновляется Hello приложения или системы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="b3b73-155">Базовое оборудование Hello возникает сбой.</span><span class="sxs-lookup"><span data-stu-id="b3b73-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="b3b73-156">Это согласование находится под управлением системы tookeep hello службы высокой доступности и правильно балансировкой.</span><span class="sxs-lookup"><span data-stu-id="b3b73-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="b3b73-157">Реализация `RunAsync()` не должна использовать синхронную блокировку.</span><span class="sxs-lookup"><span data-stu-id="b3b73-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="b3b73-158">Реализация RunAsync должен вернуть задачу или Ожидание на любые долго выполняющиеся или блокирующие операции tooallow hello среды выполнения toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b3b73-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="b3b73-159">Примечание в hello `while(true)` цикл в предыдущем примере hello, возвращающие задачи `await Task.Delay()` используется.</span><span class="sxs-lookup"><span data-stu-id="b3b73-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="b3b73-160">Если для рабочей нагрузки требуется синхронная блокировка, то в своей реализации `RunAsync` следует запланировать новую задачу с `Task.Run()`.</span><span class="sxs-lookup"><span data-stu-id="b3b73-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="b3b73-161">Отмена рабочей нагрузки является совместной усилий под управлением hello, предоставленный токен отмены.</span><span class="sxs-lookup"><span data-stu-id="b3b73-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="b3b73-162">Hello система будет ожидать вашего tooend задачи (от успешного завершения, отмены или сбоя) перед переходом.</span><span class="sxs-lookup"><span data-stu-id="b3b73-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="b3b73-163">Это hello важные toohonor отмены маркера, Готово любой работы и завершить работу `RunAsync()` максимально быстро при hello система запрашивает отмену.</span><span class="sxs-lookup"><span data-stu-id="b3b73-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="b3b73-164">В этом примере службы без отслеживания состояния hello число хранится в локальной переменной.</span><span class="sxs-lookup"><span data-stu-id="b3b73-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="b3b73-165">Но так как службы без отслеживания состояния, hello значение, которое хранится существует только для текущего жизненного цикла hello его экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="b3b73-166">Если служба hello перемещает или перезагружается, значение hello теряются.</span><span class="sxs-lookup"><span data-stu-id="b3b73-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="b3b73-167">Создание службы с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="b3b73-167">Create a stateful service</span></span>
<span data-ttu-id="b3b73-168">Service Fabric представляет новый вид службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="b3b73-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="b3b73-169">Службы с отслеживанием состояния могут сохранять состояние надежно внутри hello самой службы, совместно с hello код, который использует его.</span><span class="sxs-lookup"><span data-stu-id="b3b73-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="b3b73-170">Состояние высокой надежности с помощью Service Fabric без внешнего хранилища hello необходимость toopersist состояния tooan.</span><span class="sxs-lookup"><span data-stu-id="b3b73-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="b3b73-171">tooconvert значение счетчика из без сохранения состояния toohighly доступны и постоянные, даже в том случае, когда служба hello перемещает или перезапуска необходимо службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="b3b73-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="b3b73-172">В hello же *HelloWorld* приложения, можно добавить новую службу, щелкнув ссылки на службы hello в проект приложения hello и выбрав **Добавить -> Новая служба Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="b3b73-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Добавление службы tooyour приложения Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="b3b73-174">Выберите **Служба с отслеживанием состояния** и присвойте имя *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="b3b73-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="b3b73-175">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b3b73-175">Click **OK**.</span></span>

![Используйте поле диалогового окна toocreate новой службы с отслеживанием состояния Service Fabric для hello нового проекта](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="b3b73-177">Приложения должны появиться две службы: hello службы без отслеживания состояния *HelloWorldStateless* и службы с отслеживанием состояния hello *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="b3b73-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="b3b73-178">Службы с отслеживанием состояния имеет hello одной точки входа как службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="b3b73-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="b3b73-179">Hello основное отличие заключается в доступности hello *поставщик состояния* , надежно сохранять состояние.</span><span class="sxs-lookup"><span data-stu-id="b3b73-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="b3b73-180">Service Fabric поставляется с именем реализации поставщика состояния [надежного коллекции](service-fabric-reliable-services-reliable-collections.md), позволяет создавать надежные диспетчер состояния структуры реплицированные данные через hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="b3b73-181">Служба Reliable Service с отслеживанием состояния использует этот поставщик состояний по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b3b73-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="b3b73-182">Откройте **HelloWorldStateful.cs** в *HelloWorldStateful*, который содержит следующий метод RunAsync hello:</span><span class="sxs-lookup"><span data-stu-id="b3b73-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

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

### <a name="runasync"></a><span data-ttu-id="b3b73-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="b3b73-183">RunAsync</span></span>
<span data-ttu-id="b3b73-184">`RunAsync()` работает одинаково в службах с отслеживанием и без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="b3b73-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="b3b73-185">Тем не менее, в службы с отслеживанием состояния, платформа hello выполняет дополнительные действия от имени пользователя перед запуском `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="b3b73-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="b3b73-186">Эта работа может включать гарантирует, что hello надежного диспетчер состояния и надежного коллекции будут готовы toouse.</span><span class="sxs-lookup"><span data-stu-id="b3b73-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="b3b73-187">Надежные коллекций и hello надежного диспетчер состояния</span><span class="sxs-lookup"><span data-stu-id="b3b73-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="b3b73-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) является реализацией словаря, которые можно использовать tooreliably сохранение состояния в службе hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="b3b73-189">С помощью Service Fabric и надежного коллекций можно хранить данные непосредственно в службе без необходимости hello внешнем постоянное хранилище.</span><span class="sxs-lookup"><span data-stu-id="b3b73-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="b3b73-190">Надежные коллекции Reliable Collections делают данные высокодоступными.</span><span class="sxs-lookup"><span data-stu-id="b3b73-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="b3b73-191">Service Fabric выполняет эту задачу, автоматически создавая несколько *реплик* службы и управляя ими.</span><span class="sxs-lookup"><span data-stu-id="b3b73-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="b3b73-192">Он также предоставляет API, который абстрагирует дальней hello сложности решения этих реплик и их состояниями.</span><span class="sxs-lookup"><span data-stu-id="b3b73-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="b3b73-193">В Reliable Collections можно хранить любые типы объектов .NET, включая пользовательские типы. Необходимо только учитывать следующее.</span><span class="sxs-lookup"><span data-stu-id="b3b73-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="b3b73-194">Service Fabric делает ваш штат обеспечивает высокую доступность *репликации* состояние между узлами и коллекций надежного хранения toolocal диска данных для каждой реплики.</span><span class="sxs-lookup"><span data-stu-id="b3b73-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="b3b73-195">Это означает, что все объекты, хранящиеся в Reliable Collections, должны поддерживать *сериализацию*.</span><span class="sxs-lookup"><span data-stu-id="b3b73-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="b3b73-196">По умолчанию использовать надежные коллекций [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) для сериализации, в этом случае важно toomake убедиться, что типы имеют [поддерживаемые hello сериализатор контракта данных](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) при использовании по умолчанию hello сериализатор.</span><span class="sxs-lookup"><span data-stu-id="b3b73-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="b3b73-197">Когда вы зафиксируете транзакции в Reliable Collections, объекты реплицируются и становятся высокодоступными.</span><span class="sxs-lookup"><span data-stu-id="b3b73-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="b3b73-198">Объекты, сохраненные в Reliable Collections, хранятся в локальной памяти вашей службы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="b3b73-199">Это означает, что имеется объект toohello локальную ссылку.</span><span class="sxs-lookup"><span data-stu-id="b3b73-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="b3b73-200">Очень важно, что не размещают локальные экземпляры этих объектов без выполнения операции обновления на коллекцию надежных hello в транзакции.</span><span class="sxs-lookup"><span data-stu-id="b3b73-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="b3b73-201">Это так, как изменения toolocal экземпляры объектов, не будут автоматически реплицироваться.</span><span class="sxs-lookup"><span data-stu-id="b3b73-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="b3b73-202">Необходимо повторно вставить hello объекта обратно в словарь hello или использовать один из hello *обновление* методы в словаре hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="b3b73-203">Hello надежного диспетчер состояния управляет надежного коллекций.</span><span class="sxs-lookup"><span data-stu-id="b3b73-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="b3b73-204">Вы можете просто запросить hello надежного диспетчер состояния надежного коллекции по имени в любое время и в любом месте в службе.</span><span class="sxs-lookup"><span data-stu-id="b3b73-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="b3b73-205">Hello надежного диспетчер состояния гарантирует снова получить ссылку.</span><span class="sxs-lookup"><span data-stu-id="b3b73-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="b3b73-206">Не рекомендуется сохранить ссылки tooreliable коллекции экземпляров в переменные-члены класса или свойств.</span><span class="sxs-lookup"><span data-stu-id="b3b73-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="b3b73-207">Tooensure, ссылка hello необходимо уделить особое tooan экземпляра в любое время жизненного цикла службы hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="b3b73-208">Hello надежного диспетчер состояний обрабатывает эту работу для вас и оптимизирован для повторные визиты.</span><span class="sxs-lookup"><span data-stu-id="b3b73-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="b3b73-209">Транзакционные и асинхронные операции</span><span class="sxs-lookup"><span data-stu-id="b3b73-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="b3b73-210">Надежные коллекции имеют многие hello и те же операции, их `System.Collections.Generic` и `System.Collections.Concurrent` аналоги за исключением LINQ.</span><span class="sxs-lookup"><span data-stu-id="b3b73-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="b3b73-211">Операции в надежных коллекциях являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="b3b73-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="b3b73-212">Это так, как операции записи с коллекциями надежного выполнения tooreplicate операций ввода-вывода и сохранения данных toodisk.</span><span class="sxs-lookup"><span data-stu-id="b3b73-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="b3b73-213">Операции Reliable Collections являются *транзакционными*, так что вы можете сохранять согласованное состояние между несколькими Reliable Collections и операциями.</span><span class="sxs-lookup"><span data-stu-id="b3b73-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="b3b73-214">Например может вывода из очереди рабочего элемента из надежной очереди, выполняют операцию над его и сохранить результат hello в словаре надежные, все в одной транзакции.</span><span class="sxs-lookup"><span data-stu-id="b3b73-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="b3b73-215">Это рассматривается как атомарную операцию, и гарантирует, что hello вся операция завершится успешно или будет произведен откат всей операции hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="b3b73-216">Если ошибка возникает после dequeue hello элемента, но перед сохранением результат hello, откат всей транзакции hello и hello элемент остается в очереди hello для обработки.</span><span class="sxs-lookup"><span data-stu-id="b3b73-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="b3b73-217">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="b3b73-217">Run hello application</span></span>
<span data-ttu-id="b3b73-218">Теперь мы возвращаем toohello *HelloWorld* приложения.</span><span class="sxs-lookup"><span data-stu-id="b3b73-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="b3b73-219">Теперь вы можете построить и развернуть свои службы.</span><span class="sxs-lookup"><span data-stu-id="b3b73-219">You can now build and deploy your services.</span></span> <span data-ttu-id="b3b73-220">При нажатии клавиши **F5**, приложение будет tooyour встроенного и развернутого локального кластера.</span><span class="sxs-lookup"><span data-stu-id="b3b73-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="b3b73-221">После hello службы запущены, можно просмотреть события трассировки событий для Windows (ETW) создается hello в **события диагностики** окна.</span><span class="sxs-lookup"><span data-stu-id="b3b73-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="b3b73-222">Обратите внимание, что отображаются события hello hello без сохранения состояния службы и службы с отслеживанием состояния hello в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b3b73-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="b3b73-223">Вы можете приостановить поток hello, щелкнув hello **приостановить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b3b73-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="b3b73-224">Затем можно проверить данные сообщения hello, развернув это сообщение.</span><span class="sxs-lookup"><span data-stu-id="b3b73-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="b3b73-225">Перед запуском приложения hello, убедитесь, что имеется локальная разработка кластера под управлением.</span><span class="sxs-lookup"><span data-stu-id="b3b73-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="b3b73-226">Извлечение hello [руководство по началу работы](service-fabric-get-started.md) сведения о настройке локальной среде.</span><span class="sxs-lookup"><span data-stu-id="b3b73-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Просмотр событий диагностики в Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="b3b73-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b3b73-228">Next steps</span></span>
[<span data-ttu-id="b3b73-229">Отладка приложения Service Fabric с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b3b73-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="b3b73-230">Приступая к работе со службами веб-API Service Fabric с саморазмещением OWIN</span><span class="sxs-lookup"><span data-stu-id="b3b73-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="b3b73-231">Дополнительные сведения о надежных коллекциях</span><span class="sxs-lookup"><span data-stu-id="b3b73-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="b3b73-232">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="b3b73-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="b3b73-233">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="b3b73-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="b3b73-234">Справочник разработчика по надежным службам</span><span class="sxs-lookup"><span data-stu-id="b3b73-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

