---
title: "веб-интерфейса для приложения Azure Service Fabric с помощью ASP.NET Core aaaCreate | Документы Microsoft"
description: "Предоставлять веб-приложения toohello Service Fabric с помощью проекта ASP.NET Core и связи между службами через службу удаленного взаимодействия."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="58073-103">Создание внешнего интерфейса веб-службы для приложения с помощью ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="58073-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="58073-104">По умолчанию службы Azure Service Fabric не предоставляют toohello общедоступный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="58073-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="58073-105">tooexpose клиентов tooHTTP функциональные возможности приложения, у вас есть toocreate веб-узел проекта tooact в качестве точки входа, а затем взаимодействовать с ней tooyour отдельных служб.</span><span class="sxs-lookup"><span data-stu-id="58073-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="58073-106">В этом учебнике мы взять с момента остановки в hello [создание первого приложения в Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) учебника и добавить в веб-службу ASP.NET Core перед службы с отслеживанием состояния счетчика hello.</span><span class="sxs-lookup"><span data-stu-id="58073-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="58073-107">Выполните соответствующие указания в этом руководстве, если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="58073-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="58073-108">Настройте среду для ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="58073-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="58073-109">Требуется Visual Studio 2017 г toofollow вместе с учебником.</span><span class="sxs-lookup"><span data-stu-id="58073-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="58073-110">Подойдет любой выпуск.</span><span class="sxs-lookup"><span data-stu-id="58073-110">Any edition will do.</span></span> 

 - <span data-ttu-id="58073-111">Установите [Visual Studio 2017](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="58073-111">[Install Visual Studio 2017](https://www.visualstudio.com/)</span></span>

<span data-ttu-id="58073-112">приложения ASP.NET Core Service Fabric toodevelop, должно быть hello, следуя рабочей нагрузки:</span><span class="sxs-lookup"><span data-stu-id="58073-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="58073-113">**разработка Azure** (в разделе *Web & Cloud* (Сеть и облако));</span><span class="sxs-lookup"><span data-stu-id="58073-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="58073-114">**ASP.NET и веб-разработка** (в разделе *Web & Cloud* (Сеть и облако));</span><span class="sxs-lookup"><span data-stu-id="58073-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="58073-115">**кроссплатформенная разработка .NET Core** (в разделе *Other Toolsets* (Другие наборы средств)).</span><span class="sxs-lookup"><span data-stu-id="58073-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="58073-116">Hello .NET основные инструменты для Visual Studio 2015 больше не обновляются, но если вы все еще используете Visual Studio 2015, вам нужно toohave [.NET Core VS 2015 средства предварительного просмотра 2](https://www.microsoft.com/net/download/core) установлен.</span><span class="sxs-lookup"><span data-stu-id="58073-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="58073-117">Добавление приложения ASP.NET Core service tooyour</span><span class="sxs-lookup"><span data-stu-id="58073-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="58073-118">ASP.NET Core — это платформа разработки упрощенных кросс платформенных веб-, можно использовать toocreate современного пользовательского веб-интерфейса и веб-API.</span><span class="sxs-lookup"><span data-stu-id="58073-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="58073-119">Давайте добавим существующее приложение tooour проекта веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="58073-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="58073-120">В обозревателе решений щелкните правой кнопкой мыши **службы** в проект приложения hello и выберите **Добавить > Новая служба Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="58073-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Добавление нового tooan существующего приложения службы][vs-add-new-service]
2. <span data-ttu-id="58073-122">На hello **создать службу** выберите **ASP.NET Core** и присвойте ему имя.</span><span class="sxs-lookup"><span data-stu-id="58073-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Выбор веб-службы ASP.NET в диалоговое окно создания службы hello][vs-new-service-dialog]

3. <span data-ttu-id="58073-124">Следующая страница Hello предоставляет набор ASP.NET Core шаблоны проектов.</span><span class="sxs-lookup"><span data-stu-id="58073-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="58073-125">Обратите внимание, что они являются hello же варианты, которые появляются при создании проекта ASP.NET Core вне приложения Service Fabric, с помощью небольшого количества tooregister дополнительного кода hello службы среды выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="58073-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="58073-126">В этом руководстве мы будем использовать **веб-API**.</span><span class="sxs-lookup"><span data-stu-id="58073-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="58073-127">Тем не менее, можно применить hello же понятия toobuilding полного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="58073-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![Выбор типа проекта ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="58073-129">После создания проекта веб-API в вашем приложении будут две службы.</span><span class="sxs-lookup"><span data-stu-id="58073-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="58073-130">Как вы по-прежнему toobuild приложения, можно добавить дополнительные службы в точности hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="58073-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="58073-131">Каждая из этих служб может быть отдельно обновлена, в том числе до определенной версии.</span><span class="sxs-lookup"><span data-stu-id="58073-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="58073-132">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="58073-132">Run hello application</span></span>
<span data-ttu-id="58073-133">Общее представление о том, что мы сделали, давайте tooget развертывания нового приложения hello и предоставляет поведение по умолчанию hello, hello шаблона веб-API ASP.NET Core рассмотреть take.</span><span class="sxs-lookup"><span data-stu-id="58073-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="58073-134">Нажмите клавишу F5 в Visual Studio приложение hello toodebug.</span><span class="sxs-lookup"><span data-stu-id="58073-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="58073-135">После завершения развертывания Visual Studio запускает браузер toohello корень hello службы веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="58073-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="58073-136">шаблон веб-API ASP.NET Core Hello не предоставляет поведение по умолчанию для корневого hello, должно появиться сообщение об ошибке 404 в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="58073-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="58073-137">Добавить `/api/values` toohello расположение в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="58073-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="58073-138">При этом вызывается hello `Get` метод hello ValuesController в шаблоне hello веб-API.</span><span class="sxs-lookup"><span data-stu-id="58073-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="58073-139">Он возвращает ответ по умолчанию hello, предоставляемого шаблоном hello — массив JSON, который содержит две строки:</span><span class="sxs-lookup"><span data-stu-id="58073-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![Значения по умолчанию, возвращаемые шаблоном веб-API ASP.NET Core][browser-aspnet-template-values]
   
    <span data-ttu-id="58073-141">Hello конце учебника hello этой странице будет представлен hello самое последнее значение счетчика из нашей службы с отслеживанием состояния вместо hello строки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="58073-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="58073-142">Подключение служб hello</span><span class="sxs-lookup"><span data-stu-id="58073-142">Connect hello services</span></span>
<span data-ttu-id="58073-143">Service Fabric позволяет пользователям самим определять способ взаимодействия со службами Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="58073-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="58073-144">В одном приложении можно иметь службы, доступные по TCP, другие службы, которые доступны через HTTP REST API, и третьи службы, которые доступны через веб-сокеты.</span><span class="sxs-lookup"><span data-stu-id="58073-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="58073-145">Основные сведения о доступные варианты hello, а также соотношение hello. в разделе [взаимодействия со службами](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="58073-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="58073-146">В этом руководстве мы используем [удаленного взаимодействия службы структуры службы](service-fabric-reliable-services-communication-remoting.md), предоставленный в hello SDK.</span><span class="sxs-lookup"><span data-stu-id="58073-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="58073-147">В hello подход службы удаленного взаимодействия (основанный на удаленных вызовов процедур или RPC) определить интерфейс tooact как hello открытый контракт для службы hello.</span><span class="sxs-lookup"><span data-stu-id="58073-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="58073-148">Затем использовать этот интерфейс toogenerate класс-посредник для взаимодействия со службой hello.</span><span class="sxs-lookup"><span data-stu-id="58073-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="58073-149">Создать интерфейс hello удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="58073-149">Create hello remoting interface</span></span>
<span data-ttu-id="58073-150">Давайте начнем с создания интерфейса tooact hello как hello контракт между службой с отслеживанием состояния hello и другие службы, в этом вариантов hello веб-проекта ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="58073-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="58073-151">Этот интерфейс должен быть одинаков для всех служб, которые его используют toomake вызовы RPC, поэтому мы создадим в отдельном проекте библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="58073-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="58073-152">В обозревателе решений щелкните решение правой кнопкой мыши и выберите **В браузере добавьте к адресу путь** > **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="58073-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="58073-153">Выберите hello **Visual C#** запись в hello слева на панели навигации и выберите hello **библиотеки классов** шаблона.</span><span class="sxs-lookup"><span data-stu-id="58073-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="58073-154">Убедитесь, эта версия .NET Framework hello задано слишком**4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="58073-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![Создание проекта интерфейса для службы с отслеживанием состояния][vs-add-class-library-project]

3. <span data-ttu-id="58073-156">Установка hello **Microsoft.ServiceFabric.Services.Remoting** пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="58073-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="58073-157">Поиск **Microsoft.ServiceFabric.Services.Remoting** в hello NuGet пакета диспетчера и установить его для всех проектов в решении hello, использующих службы удаленного взаимодействия, включая:</span><span class="sxs-lookup"><span data-stu-id="58073-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="58073-158">проект библиотеки классов Hello, содержащий интерфейс службы hello</span><span class="sxs-lookup"><span data-stu-id="58073-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="58073-159">проект службы с отслеживанием состояния Hello</span><span class="sxs-lookup"><span data-stu-id="58073-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="58073-160">проект веб-службы ASP.NET Core Hello</span><span class="sxs-lookup"><span data-stu-id="58073-160">hello ASP.NET Core web service project</span></span>
   
    ![При добавлении пакета NuGet службы hello][vs-services-nuget-package]

4. <span data-ttu-id="58073-162">В библиотеке классов hello, создать интерфейс с одним методом `GetCountAsync`, и расширения интерфейса hello из `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="58073-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="58073-163">Hello интерфейс удаленного доступа должен быть производным от этого интерфейса tooindicate, это интерфейс службы удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="58073-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="58073-164">Реализуйте интерфейс hello в вашей службы с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="58073-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="58073-165">Теперь, когда мы определили интерфейс hello, нам нужно tooimplement в hello службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="58073-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="58073-166">В службе с отслеживанием состояния добавьте ссылку toohello проект библиотеки классов, содержащий интерфейс hello.</span><span class="sxs-lookup"><span data-stu-id="58073-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![Добавление проекта библиотеки классов toohello ссылку в hello службы с отслеживанием состояния][vs-add-class-library-reference]
2. <span data-ttu-id="58073-168">Найдите hello класс, наследующий от `StatefulService`, такие как `MyStatefulService`и расширить tooimplement hello `ICounter` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58073-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="58073-169">Теперь реализуют hello единственный метод, который определен в hello `ICounter` интерфейса `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="58073-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="58073-170">Предоставлять службы с отслеживанием состояния hello, с помощью прослушиватель службы удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="58073-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="58073-171">С hello `ICounter` интерфейс реализован, hello последний шаг — tooopen hello службы удаленного взаимодействия коммуникационный канал.</span><span class="sxs-lookup"><span data-stu-id="58073-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="58073-172">Для служб с отслеживанием состояния Service Fabric предоставляет переопределяемый метод `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="58073-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="58073-173">В этом методе можно указать один или несколько прослушивателей связи, на основе типа hello взаимодействия, что требуется tooenable для службы.</span><span class="sxs-lookup"><span data-stu-id="58073-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="58073-174">вызывается Hello эквивалентный метод для открытия службы toostateless канала связи `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="58073-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="58073-175">В этом случае мы заменить существующий hello `CreateServiceReplicaListeners` метод и предоставить экземпляр `ServiceRemotingListener`, который создает конечную точку RPC может быть вызван из клиентов через `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="58073-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="58073-176">Hello `CreateServiceRemotingListener` метод расширения в hello `IService` интерфейс позволяет tooeasily создания `ServiceRemotingListener` со всеми параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="58073-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="58073-177">toouse этот метод расширения, убедитесь в наличии hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` импортированные пространства имен.</span><span class="sxs-lookup"><span data-stu-id="58073-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="58073-178">Использовать класс toointeract hello ServiceProxy со службой hello</span><span class="sxs-lookup"><span data-stu-id="58073-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="58073-179">Наши службы с отслеживанием состояния — это теперь готовы tooreceive трафик от других служб через RPC.</span><span class="sxs-lookup"><span data-stu-id="58073-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="58073-180">Поэтому все, что остается состоит в добавлении toocommunicate кода hello с ним из веб-службы ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="58073-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="58073-181">В проекте ASP.NET, добавить библиотека классов toohello ссылку, которая содержит hello `ICounter` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58073-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="58073-182">Ранее вы добавили hello **Microsoft.ServiceFabric.Services.Remoting** проекта ASP.NET toohello пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="58073-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="58073-183">Этот пакет содержит hello `ServiceProxy` класс, который можно использовать toomake RPC вызывает toohello службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="58073-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="58073-184">Убедитесь, что при установке этого пакета NuGet в проект веб-службы ASP.NET Core hello.</span><span class="sxs-lookup"><span data-stu-id="58073-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="58073-185">В hello **контроллеров** папки, откройте hello `ValuesController` класса.</span><span class="sxs-lookup"><span data-stu-id="58073-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="58073-186">Обратите внимание, что hello `Get` метод в данный момент просто возвращает массив жестко заданная строка «значение1» и «значение2»--соответствует мы видели ранее в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="58073-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="58073-187">Замените эту реализацию hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="58073-187">Replace this implementation with hello following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="58073-188">Первая строка кода Hello является ключом hello один.</span><span class="sxs-lookup"><span data-stu-id="58073-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="58073-189">toocreate hello ICounter прокси toohello службы с отслеживанием состояния, требуется tooprovide два блока данных: имя идентификатора и hello секции hello службы.</span><span class="sxs-lookup"><span data-stu-id="58073-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="58073-190">Секционирования службы с отслеживанием состояния tooscale можно использовать, разбив их состояние в разные сегменты на основе ключа, определяющие, как код потребителя или почтовый индекс.</span><span class="sxs-lookup"><span data-stu-id="58073-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="58073-191">В данном тривиальные службы с отслеживанием состояния hello имеет только одну секцию, поэтому hello ключ не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="58073-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="58073-192">Любую клавишу, указываемое приведет toohello одной секции.</span><span class="sxs-lookup"><span data-stu-id="58073-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="58073-193">toolearn Дополнительные сведения о секционировании служб, в разделе [как toopartition надежного служб Service Fabric](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="58073-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="58073-194">Имя службы Hello является URI структуры формы hello: /&lt;имя_приложения&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="58073-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="58073-195">С эти два блока данных Service Fabric можно однозначно определить hello компьютере, на который должны отправляться запросы.</span><span class="sxs-lookup"><span data-stu-id="58073-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="58073-196">Hello `ServiceProxy` класс также легко обрабатывает hello случай, когда hello компьютер, на котором размещена раздела с отслеживанием состояния службы hello выходит из строя, и другой компьютер должен быть повышенным уровнем tootake его место.</span><span class="sxs-lookup"><span data-stu-id="58073-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="58073-197">Эта абстракция делает написание hello toodeal кода клиента с другими службами, которые значительно проще.</span><span class="sxs-lookup"><span data-stu-id="58073-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="58073-198">После получения hello прокси-сервера, достаточно вызвать hello `GetCountAsync` метод и возвращает ее результат.</span><span class="sxs-lookup"><span data-stu-id="58073-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="58073-199">Нажмите клавишу F5, снова toorun hello изменения приложения.</span><span class="sxs-lookup"><span data-stu-id="58073-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="58073-200">Как и прежде, Visual Studio автоматически запускает корневой toohello браузера hello hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="58073-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="58073-201">Добавить путь «api или значения» hello, и вы увидите hello возвращается текущее значение счетчика.</span><span class="sxs-lookup"><span data-stu-id="58073-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![значение счетчика с отслеживанием состояния Hello, отображенные в браузере hello][browser-aspnet-counter-value]
   
    <span data-ttu-id="58073-203">Обновите браузер hello периодически toosee hello счетчик значение обновления.</span><span class="sxs-lookup"><span data-stu-id="58073-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="58073-204">Kestrel и WebListener</span><span class="sxs-lookup"><span data-stu-id="58073-204">Kestrel and WebListener</span></span>

<span data-ttu-id="58073-205">Hello стандартного ASP.NET Core веб-сервера, известный как Kestrel, является [не поддерживается для обработки прямой Интернет-трафик](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="58073-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="58073-206">В результате hello шаблон службы без отслеживания состояния ASP.NET Core для Service Fabric использует [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="58073-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="58073-207">toolearn Дополнительные сведения о Kestrel и WebListener в служб Service Fabric см. слишком[ASP.NET Core в Service Fabric надежного обмена](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="58073-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="58073-208">Подключение службы Reliable Actor tooa</span><span class="sxs-lookup"><span data-stu-id="58073-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="58073-209">В этом руководстве описывается добавление веб-интерфейса для обеспечения связи со службой с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="58073-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="58073-210">Тем не менее вы можете использовать схожий tooactors tootalk модели.</span><span class="sxs-lookup"><span data-stu-id="58073-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="58073-211">При создании проекта Reliable Actor Visual Studio автоматически создает проект интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58073-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="58073-212">Можно использовать этот интерфейс toogenerate прокси-сервер субъекта в проект toocommunicate hello web с hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="58073-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="58073-213">канал связи Hello предоставляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="58073-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="58073-214">Таким образом не требуется что-либо toodo, является эквивалентные tooestablishing `ServiceRemotingListener` как это было сделано для службы с отслеживанием состояния hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="58073-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="58073-215">Как работают веб-службы на локальном кластере</span><span class="sxs-lookup"><span data-stu-id="58073-215">How web services work on your local cluster</span></span>
<span data-ttu-id="58073-216">Как правило можно развернуть точно hello же Service Fabric приложения tooa несколькими компьютерами кластера, которые развернуты на локальный кластер и быть высокой уверенности, что он работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="58073-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="58073-217">Это происходит потому локального кластера является просто пяти узла конфигурации, свернут tooa одного компьютера.</span><span class="sxs-lookup"><span data-stu-id="58073-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="58073-218">Что касается служб tooweb, однако есть одно ключевые особенности организации.</span><span class="sxs-lookup"><span data-stu-id="58073-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="58073-219">При кластера находится за подсистемой балансировки нагрузки, как и в Azure, необходимо убедиться, что веб-служб развертываются на каждом компьютере, так как Подсистема балансировки нагрузки hello просто циклическое трафик между компьютерами hello.</span><span class="sxs-lookup"><span data-stu-id="58073-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="58073-220">Это можно сделать, установка hello `InstanceCount` для hello службы toohello специальное значение «-1».</span><span class="sxs-lookup"><span data-stu-id="58073-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="58073-221">Напротив, при локальном запуске веб-службы необходимо tooensure работает, только один экземпляр службы hello.</span><span class="sxs-lookup"><span data-stu-id="58073-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="58073-222">В противном случае возникнут конфликтов в нескольких процессах, которые прослушивают hello же путь и порт.</span><span class="sxs-lookup"><span data-stu-id="58073-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="58073-223">В результате число экземпляр службы web hello должно быть задано слишком «1» для локального развертывания.</span><span class="sxs-lookup"><span data-stu-id="58073-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="58073-224">tooconfigure разные значения для отдельной среды. в статье toolearn [Управление параметрами приложения для нескольких сред](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="58073-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="58073-225">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58073-225">Next steps</span></span>
<span data-ttu-id="58073-226">Теперь, когда вы настроили веб-интерфейс для приложения с помощью ASP.NET Core, получите дополнительные сведения о работе ASP.NET Core с Service Fabric в статье о [ASP.NET Core в Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="58073-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="58073-227">Далее, [Дополнительные сведения о взаимодействии со службами](service-fabric-connect-and-communicate-with-services.md) вообще tooget a завершения рисунок из как службы связи работает в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="58073-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="58073-228">После полного понимания того, как работает связь со службой, [создать кластер в Azure и развертывание облачных приложений toohello](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="58073-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
