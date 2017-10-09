---
title: "aaaCreate вашего первого на основе субъектов Azure микрослужбу в C# | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги создания, отладки и развертывания простой службы на основе субъектов, с помощью службы структуры службы Reliable Actor hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="9a4d6-103">Приступая к работе с Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="9a4d6-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a4d6-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="9a4d6-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="9a4d6-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="9a4d6-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="9a4d6-106">В этой статье объясняется hello основные сведения о службе Azure Fabric службы Reliable actor и описан процесс создания, отладки и развертывания простого Reliable Actor приложения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="9a4d6-107">Установка и настройка</span><span class="sxs-lookup"><span data-stu-id="9a4d6-107">Installation and setup</span></span>
<span data-ttu-id="9a4d6-108">Прежде чем начать, проверьте наличие на компьютере среды разработки Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="9a4d6-109">Если вам требуется tooset его, см. Подробные инструкции по [как tooset среды разработки hello](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9a4d6-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="9a4d6-110">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="9a4d6-110">Basic concepts</span></span>
<span data-ttu-id="9a4d6-111">tooget выполнению службы Reliable Actor, нужно только необходимые toounderstand несколько основных понятий.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="9a4d6-112">**Служба субъекта**.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-112">**Actor service**.</span></span> <span data-ttu-id="9a4d6-113">Службы Reliable Actor упакованы в надежные службы, которая может быть развернута в инфраструктуре Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="9a4d6-114">Экземпляры субъектов активируются в именованном экземпляре службы.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="9a4d6-115">**Регистрация субъекта**.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-115">**Actor registration**.</span></span> <span data-ttu-id="9a4d6-116">Как с помощью надежного обмена службы Reliable Actor должен toobe зарегистрирована среда выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="9a4d6-117">Кроме того тип субъекта hello должен toobe зарегистрирован со средой выполнения hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="9a4d6-118">**Интерфейс субъекта**.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-118">**Actor interface**.</span></span> <span data-ttu-id="9a4d6-119">интерфейс Hello субъекта является toodefine используется строго типизированный открытый интерфейс субъекта.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="9a4d6-120">В hello терминологии модели Reliable Actor hello субъекта интерфейс определяет hello может понять и обрабатывать типы сообщений, которые hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="9a4d6-121">интерфейс Hello субъекта используется другим субъектам и клиентские приложения слишком «отправить» (асинхронно) субъекта toohello сообщений.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="9a4d6-122">Субъекты Reliable Actors могут реализовывать несколько интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="9a4d6-123">**Класс ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-123">**ActorProxy class**.</span></span> <span data-ttu-id="9a4d6-124">Hello класс ActorProxy используется tooinvoke клиентского приложения hello методы, предоставляемые через интерфейс hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="9a4d6-125">Hello ActorProxy класс предоставляет две важные функции:</span><span class="sxs-lookup"><span data-stu-id="9a4d6-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="9a4d6-126">Разрешение имен: это может toolocate hello субъекта в кластере hello (поиск hello узел кластера hello, где размещается).</span><span class="sxs-lookup"><span data-stu-id="9a4d6-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="9a4d6-127">Обработка сбоев: он повторите вызовы методов и повторно разрешить расположение субъекта hello после, например, сбой, который требует toobe субъекта hello переместить tooanother узел в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="9a4d6-128">следующие правила, которые относятся интерфейсы tooactor Hello, следует отметить:</span><span class="sxs-lookup"><span data-stu-id="9a4d6-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="9a4d6-129">методы интерфейса субъекта не могут быть перегружены;</span><span class="sxs-lookup"><span data-stu-id="9a4d6-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="9a4d6-130">методы интерфейса субъекта не должны иметь выходных, ссылочных или необязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="9a4d6-131">универсальные интерфейсы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="9a4d6-132">Создание проекта в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a4d6-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="9a4d6-133">Запустите Visual Studio 2015 или Visual Studio 2017 от имени администратора и создайте проект приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Средства Service Fabric для Visual Studio — новый проект][1]

<span data-ttu-id="9a4d6-135">Hello Далее диалогового окна можно выбрать hello типа проекта, которые должны toocreate.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Шаблоны проекта Service Fabric][5]

<span data-ttu-id="9a4d6-137">Для проекта "HelloWorld" hello воспользуемся служба Service Fabric службы Reliable Actor hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="9a4d6-138">После создания решения hello, вы увидите hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="9a4d6-138">After you have created hello solution, you should see hello following structure:</span></span>

![Структура проекта Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="9a4d6-140">Простые стандартные блоки в решении на базе надежных субъектов</span><span class="sxs-lookup"><span data-stu-id="9a4d6-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="9a4d6-141">Как правило, решение на основе модели Reliable Actors состоит из трех проектов.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="9a4d6-142">**проект приложения Hello (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="9a4d6-143">Это проект hello, которая упаковывает всех служб hello вместе для развертывания.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="9a4d6-144">Он содержит hello *ApplicationManifest.xml* и скриптов PowerShell для управления приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="9a4d6-145">**интерфейс Hello проекта (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="9a4d6-146">Это hello проект, который содержит определение интерфейса hello для субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="9a4d6-147">В проекте MyActor.Interfaces hello можно определить hello интерфейсы, которые будут использоваться с субъектами hello в решении hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="9a4d6-148">Субъект интерфейсов могут быть определены в любой проект с любым именем, однако hello интерфейс определяет контракт hello субъекта, который совместно используется hello субъекта реализация и вызов hello субъект, поэтому он обычно toodefine смысле клиентов hello в сборку, являющуюся отделить от реализации субъекта hello и может совместно использоваться несколькими проектами.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="9a4d6-149">**проект службы субъекта Hello (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="9a4d6-150">Это — hello проекта, используемого toodefine hello Service Fabric служба, которая является постоянной toohost hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="9a4d6-151">Он содержит реализацию hello hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="9a4d6-152">Коллекция субъекта реализуется класс, производный от базового типа hello `Actor` и реализует hello интерфейсы, определенные в проекте MyActor.Interfaces hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="9a4d6-153">Класс субъекта также должен реализовывать конструктор, принимающий `ActorService` экземпляра и `ActorId` и передает их toohello базового `Actor` класса.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="9a4d6-154">Это позволяет внедрять зависимости платформы как зависимости конструктора.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="9a4d6-155">необходимо зарегистрировать службу Hello субъекта с типом службы в среде выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="9a4d6-156">В порядок hello toorun службу субъектов субъекта экземпляры, тип субъекта также должен быть зарегистрирован с hello службу субъектов.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="9a4d6-157">Hello `ActorRuntime` метод регистрации выполняет это действие для субъектов.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

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

<span data-ttu-id="9a4d6-158">Если у вас есть только одно определение субъекта начать новый проект в Visual Studio, регистрацию hello включается по умолчанию в коде hello, создаваемый Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="9a4d6-159">При указании других сторон в службе hello требуется tooadd hello субъекта регистрации с помощью:</span><span class="sxs-lookup"><span data-stu-id="9a4d6-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="9a4d6-160">Hello субъекты структуры службы среда выполнения выдает некоторые [события и счетчики производительности, связанные с методами tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="9a4d6-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="9a4d6-161">Они полезны при диагностике и мониторинге производительности.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="9a4d6-162">Отладка</span><span class="sxs-lookup"><span data-stu-id="9a4d6-162">Debugging</span></span>
<span data-ttu-id="9a4d6-163">Hello средств Service Fabric для Visual Studio поддерживает отладку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="9a4d6-164">Можно запустить сеанс отладки, hello нажатие клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="9a4d6-165">Visual Studio скомпилирует (при необходимости) пакеты.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="9a4d6-166">Он также развертывает приложение hello hello локальном кластере Service Fabric и присоединяет отладчик hello.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="9a4d6-167">Во время развертывания hello, вы увидите ход выполнения hello в hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="9a4d6-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Окно вывода отладки Service Fabric][3]

## <a name="next-steps"></a><span data-ttu-id="9a4d6-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a4d6-169">Next steps</span></span>
<span data-ttu-id="9a4d6-170">Дополнительные сведения о [использование платформы Service Fabric hello службы Reliable Actor](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="9a4d6-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
