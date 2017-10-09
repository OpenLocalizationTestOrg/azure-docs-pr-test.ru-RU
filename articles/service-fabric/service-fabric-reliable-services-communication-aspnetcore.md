---
title: "связь aaaService с hello ASP.NET Core | Документы Microsoft"
description: "Дополнительные сведения о том, как toouse ASP.NET Core в надежных служб без отслеживания состояния и с отслеживанием состояния."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="791e1-103">ASP.NET Core в Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="791e1-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="791e1-104">ASP.NET Core — это новая кроссплатформенная среда с открытым кодом для создания современных облачных приложений с подключением к Интернету, таких как веб-приложения, приложения для Интернета вещей и серверные части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="791e1-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="791e1-105">В этой статье представлено подробное руководство toohosting служб ASP.NET Core в Service Fabric надежного обмена с помощью hello **Microsoft.ServiceFabric.AspNetCore.** * набор пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="791e1-105">This article is an in-depth guide toohosting ASP.NET Core services in Service Fabric Reliable Services using hello **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="791e1-106">Вводное руководство по ASP.NET Core в Service Fabric и инструкции по настройке среды разработки см. в статье [Создание внешнего интерфейса веб-службы для приложения с помощью ASP.NET Core](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="791e1-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="791e1-107">Hello оставшейся части этой статьи предполагается, что вы уже знакомы с ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="791e1-107">hello rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="791e1-108">Если нет, рекомендуется ознакомиться hello [основы ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="791e1-108">If not, we recommend reading through hello [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-hello-service-fabric-environment"></a><span data-ttu-id="791e1-109">ASP.NET Core в среде Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="791e1-109">ASP.NET Core in hello Service Fabric environment</span></span>

<span data-ttu-id="791e1-110">Хотя приложения ASP.NET Core можно запустить на основе .NET Core или полной версии .NET Framework, в данный момент служб Service Fabric могут выполняться только на приветствия hello полной версии .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="791e1-110">While ASP.NET Core apps can run on .NET Core or on hello full .NET Framework, Service Fabric services currently can only run on hello full .NET Framework.</span></span> <span data-ttu-id="791e1-111">Это означает, что при построении службы ASP.NET Core Service Fabric, необходимо по-прежнему нацелить Здравствуйте полной версии .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="791e1-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target hello full .NET Framework.</span></span>

<span data-ttu-id="791e1-112">ASP.NET Core можно использовать двумя различными способами в Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="791e1-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="791e1-113">**Разместить в виде гостевого исполняемого файла**.</span><span class="sxs-lookup"><span data-stu-id="791e1-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="791e1-114">Это в основном используется toorun существующие ASP.NET Core приложения в Service Fabric без изменения кода.</span><span class="sxs-lookup"><span data-stu-id="791e1-114">This is primarily used toorun existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="791e1-115">**Выполнять внутри надежной службы**.</span><span class="sxs-lookup"><span data-stu-id="791e1-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="791e1-116">Это обеспечивает более эффективную интеграцию со средой выполнения Service Fabric hello и позволяет службам с отслеживанием состояния ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="791e1-116">This allows better integration with hello Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="791e1-117">Hello оставшейся части этой статьи объясняется, как toouse ASP.NET Core внутри надежной службы с помощью hello компоненты интеграции ASP.NET Core, поставляемых вместе с hello Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="791e1-117">hello rest of this article explains how toouse ASP.NET Core inside a Reliable Service using hello ASP.NET Core integration components that ship with hello Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="791e1-118">Размещение службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="791e1-118">Service Fabric service hosting</span></span>

<span data-ttu-id="791e1-119">В Service Fabric один или несколько экземпляров и (или) реплик службы выполняются в *хост-процессе службы* — исполняемом файле, который выполняет код службы.</span><span class="sxs-lookup"><span data-stu-id="791e1-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="791e1-120">Автор службы принадлежит вам хост-процесса службы hello и Service Fabric активирует и следит за его работой.</span><span class="sxs-lookup"><span data-stu-id="791e1-120">You, as a service author, own hello service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="791e1-121">Традиционные ASP.NET (вверх tooMVC 5) — тесно связанные tooIIS через System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="791e1-121">Traditional ASP.NET (up tooMVC 5) is tightly coupled tooIIS through System.Web.dll.</span></span> <span data-ttu-id="791e1-122">ASP.NET Core позволяет разделить hello веб-сервер и веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="791e1-122">ASP.NET Core provides a separation between hello web server and your web application.</span></span> <span data-ttu-id="791e1-123">Это позволяет toobe приложения web зависимых от разных веб-серверов и также позволяет toobe серверы веб *резидентной*, что означает можно запустить на веб-сервере в процессе, как противоположность tooa процесс, владельцем которого является выделенное веб серверное программное обеспечение, такими как службы IIS.</span><span class="sxs-lookup"><span data-stu-id="791e1-123">This allows web applications toobe portable between different web servers and also allows web servers toobe *self-hosted*, which means you can start a web server in your own process, as opposed tooa process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="791e1-124">В порядке toocombine служба Service Fabric и ASP.NET, в качестве гостевой исполняемый файл или в надежной службы, необходимо будет toostart ASP.NET внутри хост-процесса службы.</span><span class="sxs-lookup"><span data-stu-id="791e1-124">In order toocombine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able toostart ASP.NET inside your service host process.</span></span> <span data-ttu-id="791e1-125">ASP.NET Core резидентным позволяет toodo это.</span><span class="sxs-lookup"><span data-stu-id="791e1-125">ASP.NET Core self-hosting allows you toodo this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="791e1-126">Размещение ASP.NET Core в Reliable Service</span><span class="sxs-lookup"><span data-stu-id="791e1-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="791e1-127">Как правило, резидентных приложений ASP.NET Core создать WebHost в точку входа приложения, например hello `static void Main()` метод в `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="791e1-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as hello `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="791e1-128">В этом случае жизненный цикл hello hello WebHost представляет связанный toohello жизненного цикла процесса hello.</span><span class="sxs-lookup"><span data-stu-id="791e1-128">In this case, hello lifecycle of hello WebHost is bound toohello lifecycle of hello process.</span></span>

![Размещение ASP.NET Core в процессе][0]

<span data-ttu-id="791e1-130">Однако точку входа приложения hello не toocreate подходящее место hello WebHost в надежной службы, так как точку входа приложения hello используется только tooregister службы тип среды выполнения Service Fabric hello, так, что возможно создание экземпляров данной службы тип.</span><span class="sxs-lookup"><span data-stu-id="791e1-130">However, hello application entry point is not hello right place toocreate a WebHost in a Reliable Service, because hello application entry point is only used tooregister a service type with hello Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="791e1-131">Hello WebHost должны создаваться в надежной службы сам.</span><span class="sxs-lookup"><span data-stu-id="791e1-131">hello WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="791e1-132">В рамках хост-процесса службы hello экземпляров службы и/или реплики можно выполнить несколько жизненные циклы.</span><span class="sxs-lookup"><span data-stu-id="791e1-132">Within hello service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="791e1-133">Экземпляр Reliable Service представлен с помощью класса службы, производного от `StatelessService` или `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="791e1-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="791e1-134">Hello стек связи для службы содержится в `ICommunicationListener` реализации в классе службы.</span><span class="sxs-lookup"><span data-stu-id="791e1-134">hello communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="791e1-135">Hello `Microsoft.ServiceFabric.Services.AspNetCore.*` пакетов NuGet содержащих реализации `ICommunicationListener` , запуск и управление hello ASP.NET Core WebHost для Kestrel или WebListener в надежной службы.</span><span class="sxs-lookup"><span data-stu-id="791e1-135">hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage hello ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Размещение ASP.NET Core в Reliable Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="791e1-137">Объекты ICommunicationListener в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="791e1-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="791e1-138">Hello `ICommunicationListener` реализации Kestrel и WebListener в hello `Microsoft.ServiceFabric.Services.AspNetCore.*` пакетами NuGet имеют схожие схемы использования, но выполнить несколько различных действий конкретных tooeach веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="791e1-138">hello `ICommunicationListener` implementations for Kestrel and WebListener in hello  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific tooeach web server.</span></span> 

<span data-ttu-id="791e1-139">Оба прослушивания связи предоставляют конструктор, принимающий hello следующие аргументы:</span><span class="sxs-lookup"><span data-stu-id="791e1-139">Both communication listeners provide a constructor that takes hello following arguments:</span></span>
 - <span data-ttu-id="791e1-140">**`ServiceContext serviceContext`**: hello `ServiceContext` объект, содержащий сведения о hello службой.</span><span class="sxs-lookup"><span data-stu-id="791e1-140">**`ServiceContext serviceContext`**: hello `ServiceContext` object that contains information about hello running service.</span></span>
 - <span data-ttu-id="791e1-141">**`string endpointName`**: имя hello `Endpoint` конфигурации в файле ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="791e1-141">**`string endpointName`**: hello name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="791e1-142">Это в первую очередь которых hello двух прослушивания связи не совпадают: WebListener **требует** `Endpoint` конфигурации, а Kestrel — нет.</span><span class="sxs-lookup"><span data-stu-id="791e1-142">This is primarily where hello two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="791e1-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**. Реализуемое лямбда-выражение, в котором создается и возвращается `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="791e1-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="791e1-144">Это позволяет tooconfigure `IWebHost` способом hello, обычно в приложении ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="791e1-144">This allows you tooconfigure `IWebHost` hello way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="791e1-145">Hello лямбда-выражение содержит URL-адрес, который создается в зависимости от интеграции Service Fabric hello параметрах, можно использовать и hello `Endpoint` вами конфигурации.</span><span class="sxs-lookup"><span data-stu-id="791e1-145">hello lambda provides a URL which is generated for you depending on hello Service Fabric integration options you use and hello `Endpoint` configuration you provide.</span></span> <span data-ttu-id="791e1-146">Что URL-адрес затем можно изменить или использовать в качестве-toostart hello веб-сервером.</span><span class="sxs-lookup"><span data-stu-id="791e1-146">That URL can then be modified or used as-is toostart hello web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="791e1-147">ПО промежуточного уровня для интеграции Service Fabric</span><span class="sxs-lookup"><span data-stu-id="791e1-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="791e1-148">Hello `Microsoft.ServiceFabric.Services.AspNetCore` пакет NuGet включает hello `UseServiceFabricIntegration` метода расширения `IWebHostBuilder` , добавляет службы структуры поддержкой по промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="791e1-148">hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes hello `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="791e1-149">Это по промежуточного слоя настраивает hello Kestrel или WebListener `ICommunicationListener` tooregister уникальный URL-адрес с hello служба именования Service Fabric, а затем проводится проверка подключении нужную службу toohello клиентов tooensure запросы клиента.</span><span class="sxs-lookup"><span data-stu-id="791e1-149">This middleware configures hello Kestrel or WebListener `ICommunicationListener` tooregister a unique service URL with hello Service Fabric Naming Service and then validates client requests tooensure clients are connecting toohello right service.</span></span> <span data-ttu-id="791e1-150">Это необходимо в среде общего узла, например Service Fabric, где несколько веб-приложений можно запускать на hello же физической или виртуальной машины, но не использует имена уникальный узлов, tooprevent клиенты по ошибке подключение не toohello в службу.</span><span class="sxs-lookup"><span data-stu-id="791e1-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on hello same physical or virtual machine but do not use unique host names, tooprevent clients from mistakenly connecting toohello wrong service.</span></span> <span data-ttu-id="791e1-151">Этот сценарий описан более подробно в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="791e1-151">This scenario is described in more detail in hello next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="791e1-152">Причина ошибочный идентификации</span><span class="sxs-lookup"><span data-stu-id="791e1-152">A case of mistaken identity</span></span>
<span data-ttu-id="791e1-153">Реплики службы, независимо от протокола, прослушивают уникальное сочетание "IP-адрес:порт".</span><span class="sxs-lookup"><span data-stu-id="791e1-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="791e1-154">После запуска прослушивание в конечной точке IP: Port реплики службы он сообщает, toohello адрес конечной точки службы именования Service Fabric где он обнаружен клиентам или другим службам.</span><span class="sxs-lookup"><span data-stu-id="791e1-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address toohello Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="791e1-155">Если приложение динамическое назначение портов, реплики службы по случайному совпадению могут использовать службы используйте hello же конечная точка IP: Port другой службы, который ранее был на hello же физической или виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="791e1-155">If services use dynamically-assigned application ports, a service replica may coincidentally use hello same IP:port endpoint of another service that was previously on hello same physical or virtual machine.</span></span> <span data-ttu-id="791e1-156">Это может вызвать клиент toomistakely подключения не toohello в службу.</span><span class="sxs-lookup"><span data-stu-id="791e1-156">This can cause a client toomistakely connect toohello wrong service.</span></span> <span data-ttu-id="791e1-157">Это может произойти в случае hello следующая последовательность событий:</span><span class="sxs-lookup"><span data-stu-id="791e1-157">This can happen if hello following sequence of events occur:</span></span>

 1. <span data-ttu-id="791e1-158">Служба А прослушивает 10.0.0.1:30000 по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="791e1-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="791e1-159">Клиент разрешает службу А и возвращает адрес 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="791e1-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="791e1-160">Службы на другой узел tooa переход.</span><span class="sxs-lookup"><span data-stu-id="791e1-160">Service A moves tooa different node.</span></span>
 4. <span data-ttu-id="791e1-161">Службы B помещается на 10.0.0.1, по случайному совпадению использует hello тот же порт 30000.</span><span class="sxs-lookup"><span data-stu-id="791e1-161">Service B is placed on 10.0.0.1 and coincidentally uses hello same port 30000.</span></span>
 5. <span data-ttu-id="791e1-162">Клиент пытается tooservice tooconnect A с 10.0.0.1:30000 кэшированных адресов.</span><span class="sxs-lookup"><span data-stu-id="791e1-162">Client attempts tooconnect tooservice A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="791e1-163">Клиент — теперь подключен успешно выполнено подключение tooservice B, не зная, что он не toohello в службу.</span><span class="sxs-lookup"><span data-stu-id="791e1-163">Client is now successfully connected tooservice B not realizing it is connected toohello wrong service.</span></span>

<span data-ttu-id="791e1-164">Это может вызвать ошибки в разное время, которые могут быть трудности toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="791e1-164">This can cause bugs at random times that can be difficult toodiagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="791e1-165">Использование уникальных URL-адресов службы</span><span class="sxs-lookup"><span data-stu-id="791e1-165">Using unique service URLs</span></span>
<span data-ttu-id="791e1-166">tooprevent этой службы можно учесть toohello конечной точки службы именования с уникальным идентификатором и проверьте, уникальный идентификатор во время запросов клиентов.</span><span class="sxs-lookup"><span data-stu-id="791e1-166">tooprevent this, services can post an endpoint toohello Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="791e1-167">Это совместное действие между службами в доверенной среде дружественного клиента.</span><span class="sxs-lookup"><span data-stu-id="791e1-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="791e1-168">Это не обеспечивает безопасную проверку подлинности службы в среде недружественного клиента.</span><span class="sxs-lookup"><span data-stu-id="791e1-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="791e1-169">В доверенной среде hello по промежуточного слоя, который добавляется по hello `UseServiceFabricIntegration` метод автоматически добавляет адрес toohello уникальный идентификатор, который отправляется toohello службы именования и проверяет этот идентификатор для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="791e1-169">In a trusted environment, hello middleware that's added by hello `UseServiceFabricIntegration` method automatically appends a unique identifier toohello address that is posted toohello Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="791e1-170">Если идентификатор hello не совпадает, по промежуточного слоя hello немедленно возвращает ответ HTTP 410-потеряно.</span><span class="sxs-lookup"><span data-stu-id="791e1-170">If hello identifier does not match, hello middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="791e1-171">Службы, использующие динамически назначаемый порт, должны использовать это ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="791e1-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="791e1-172">Службы, использующие постоянный уникальный порт, не имеют такой проблемы в совместной среде.</span><span class="sxs-lookup"><span data-stu-id="791e1-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="791e1-173">Уникальный фиксированный порт обычно используется для служб извне с выходом, хорошо известных портов для клиентских приложений tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="791e1-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications tooconnect to.</span></span> <span data-ttu-id="791e1-174">Например, большинство веб-приложений с доступом к Интернету используют порт 80 или 443 для подключений веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="791e1-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="791e1-175">В этом случае не следует включать hello уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="791e1-175">In this case, hello unique identifier should not be enabled.</span></span>

<span data-ttu-id="791e1-176">Hello следующей схеме показан поток запросов hello с по промежуточного слоя hello включен:</span><span class="sxs-lookup"><span data-stu-id="791e1-176">hello following diagram shows hello request flow with hello middleware enabled:</span></span>

![Интеграция Service Fabric ASP.NET Core][2]

<span data-ttu-id="791e1-178">Kestrel и WebListener `ICommunicationListener` реализации используют этот механизм в hello точно таким же образом.</span><span class="sxs-lookup"><span data-stu-id="791e1-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly hello same way.</span></span> <span data-ttu-id="791e1-179">Несмотря на то, что WebListener внутренне может различать запросы с учетом уникальный URL-пути, с помощью базового hello *http.sys* возможность функциональные возможности совместного использования портов *не* используемые hello WebListener `ICommunicationListener` реализацию так, как будут созданы HTTP 503 и ошибки HTTP 404 коды состояния ошибок hello сценарий, описанный ранее.</span><span class="sxs-lookup"><span data-stu-id="791e1-179">Although WebListener can internally differentiate requests based on unique URL paths using hello underlying *http.sys* port sharing feature, that functionality is *not* used by hello WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in hello scenario described earlier.</span></span> <span data-ttu-id="791e1-180">В свою очередь затрудняет очень клиентов toodetermine hello цель ошибки hello, что HTTP 503 HTTP 404 уже часто используемые tooindicate других ошибок.</span><span class="sxs-lookup"><span data-stu-id="791e1-180">That in turn makes it very difficult for clients toodetermine hello intent of hello error, as HTTP 503 and HTTP 404 are already commonly used tooindicate other errors.</span></span> <span data-ttu-id="791e1-181">Таким образом, как Kestrel и WebListener `ICommunicationListener` реализации стандартизировать hello по промежуточного слоя, предоставляемые hello `UseServiceFabricIntegration` метод расширения, чтобы клиенты нуждаются tooperform конечную точку службы заново разрешить действие в ответы HTTP 410.</span><span class="sxs-lookup"><span data-stu-id="791e1-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on hello middleware provided by hello `UseServiceFabricIntegration` extension method so that clients only need tooperform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="791e1-182">WebListener в службах Reliable Services</span><span class="sxs-lookup"><span data-stu-id="791e1-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="791e1-183">WebListener может использоваться в надежной службы путем импорта hello **Microsoft.ServiceFabric.AspNetCore.WebListener** пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="791e1-183">WebListener can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="791e1-184">Этот пакет содержит `WebListenerCommunicationListener`, реализация `ICommunicationListener`, позволяющее вам toocreate WebHost Core ASP.NET внутри надежной службы с помощью WebListener hello веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="791e1-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using WebListener as hello web server.</span></span>

<span data-ttu-id="791e1-185">WebListener основана на hello [API HTTP-сервера Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="791e1-185">WebListener is built on hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="791e1-186">В этом случае используется hello *http.sys* драйвер ядра, используемые IIS tooprocess HTTP запрашивает и перенаправлять их tooprocesses запуском веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="791e1-186">This uses hello *http.sys* kernel driver used by IIS tooprocess HTTP requests and route them tooprocesses running web applications.</span></span> <span data-ttu-id="791e1-187">Это позволяет нескольким процессам на hello одной физической или виртуальной машины toohost веб-приложений на hello же порт, однозначно уникальный URL-адрес или имя узла.</span><span class="sxs-lookup"><span data-stu-id="791e1-187">This allows multiple processes on hello same physical or virtual machine toohost web applications on hello same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="791e1-188">Эти функции полезны в Service Fabric для размещения нескольких веб-сайтов в hello одного кластера.</span><span class="sxs-lookup"><span data-stu-id="791e1-188">These features are useful in Service Fabric for hosting multiple websites in hello same cluster.</span></span>

<span data-ttu-id="791e1-189">Hello следующей схеме показано, как WebListener использует hello *http.sys* драйвер ядра в Windows для общего доступа к портам:</span><span class="sxs-lookup"><span data-stu-id="791e1-189">hello following diagram illustrates how WebListener uses hello *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="791e1-191">WebListener в службе без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="791e1-191">WebListener in a stateless service</span></span>
<span data-ttu-id="791e1-192">toouse `WebListener` в службы без отслеживания состояния, переопределите hello `CreateServiceInstanceListeners` метода и возврата `WebListenerCommunicationListener` экземпляр:</span><span class="sxs-lookup"><span data-stu-id="791e1-192">toouse `WebListener` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="791e1-193">WebListener в службе с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="791e1-193">WebListener in a stateful service</span></span>

<span data-ttu-id="791e1-194">`WebListenerCommunicationListener`в настоящее время не предназначен для использования служб с отслеживанием состояния заказа toocomplications с базовым hello *http.sys* возможность совместного использования портов.</span><span class="sxs-lookup"><span data-stu-id="791e1-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due toocomplications with hello underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="791e1-195">Дополнительные сведения см. следующий раздел на динамического выделения портов с WebListener hello.</span><span class="sxs-lookup"><span data-stu-id="791e1-195">For more information, see hello following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="791e1-196">Для служб с отслеживанием состояния Kestrel — hello, рекомендуется использовать веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="791e1-196">For stateful services, Kestrel is hello recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="791e1-197">Настройка конечной точки</span><span class="sxs-lookup"><span data-stu-id="791e1-197">Endpoint configuration</span></span>

<span data-ttu-id="791e1-198">`Endpoint` Настройка не требуется для веб-серверов, использующих Windows API HTTP-сервера, включая WebListener hello.</span><span class="sxs-lookup"><span data-stu-id="791e1-198">An `Endpoint` configuration is required for web servers that use hello Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="791e1-199">Веб-серверы, использующие API HTTP-сервера Windows hello сначала необходимо зарезервировать URL-адрес с *http.sys* (обычно это осуществляется с помощью hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) инструмента).</span><span class="sxs-lookup"><span data-stu-id="791e1-199">Web servers that use hello Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="791e1-200">Для этого действия требуются повышенные привилегии, которых по умолчанию нет у служб.</span><span class="sxs-lookup"><span data-stu-id="791e1-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="791e1-201">Здравствуйте, «http» или «https» параметры для hello `Protocol` свойство hello `Endpoint` конфигурации в *ServiceManifest.xml* используются специально tooinstruct hello tooregister среда выполнения Service Fabric URL-адрес с *http.sys* от вашего имени, с помощью hello [ *адресе* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) префикс URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="791e1-201">hello "http" or "https" options for hello `Protocol` property of hello `Endpoint` configuration in *ServiceManifest.xml* are used specifically tooinstruct hello Service Fabric runtime tooregister a URL with *http.sys* on your behalf using hello [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="791e1-202">Например, tooreserve `http://+:80` для службы, hello следующую конфигурацию следует использовать в файле ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="791e1-202">For example, tooreserve `http://+:80` for a service, hello following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="791e1-203">И имя конечной точки hello должен быть передан toohello `WebListenerCommunicationListener` конструктор:</span><span class="sxs-lookup"><span data-stu-id="791e1-203">And hello endpoint name must be passed toohello `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="791e1-204">Использование WebListener со статическим портом</span><span class="sxs-lookup"><span data-stu-id="791e1-204">Use WebListener with a static port</span></span>
<span data-ttu-id="791e1-205">toouse статический порт с WebListener, укажите номер порта hello в hello `Endpoint` конфигурации:</span><span class="sxs-lookup"><span data-stu-id="791e1-205">toouse a static port with WebListener, provide hello port number in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="791e1-206">Использование WebListener с динамическим портом</span><span class="sxs-lookup"><span data-stu-id="791e1-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="791e1-207">toouse динамически назначаемый порт с WebListener, пропустите hello `Port` свойство в hello `Endpoint` конфигурации:</span><span class="sxs-lookup"><span data-stu-id="791e1-207">toouse a dynamically assigned port with WebListener, omit hello `Port` property in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="791e1-208">Обратите внимание, что динамический порт, выделенный с помощью конфигурации `Endpoint`, предоставляет только один порт *каждому хост-процессу*.</span><span class="sxs-lookup"><span data-stu-id="791e1-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="791e1-209">Hello текущего Service Fabric модели размещения позволяет нескольким toobe экземпляры или реплики службы, размещенной в hello же процесс, то есть каждый из них будут совместно использовать же порт при выделении через hello hello `Endpoint` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="791e1-209">hello current Service Fabric hosting model allows multiple service instances and/or replicas toobe hosted in hello same process, meaning that each one will share hello same port when allocated through hello `Endpoint` configuration.</span></span> <span data-ttu-id="791e1-210">Несколько экземпляров WebListener могут совместно использовать порт, используя базовый hello *http.sys* совместного использования порта компонент, но которая не поддерживается `WebListenerCommunicationListener` из-за сложности toohello, он вводит для клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="791e1-210">Multiple WebListener instances can share a port using hello underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due toohello complications it introduces for client requests.</span></span> <span data-ttu-id="791e1-211">Для использования динамических портов Kestrel — hello, рекомендуется использовать веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="791e1-211">For dynamic port usage, Kestrel is hello recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="791e1-212">Kestrel в Reliable Services</span><span class="sxs-lookup"><span data-stu-id="791e1-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="791e1-213">Kestrel может использоваться в надежной службы путем импорта hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="791e1-213">Kestrel can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="791e1-214">Этот пакет содержит `KestrelCommunicationListener`, реализация `ICommunicationListener`, позволяющее вам toocreate WebHost Core ASP.NET внутри надежной службы с помощью Kestrel hello веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="791e1-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using Kestrel as hello web server.</span></span>

<span data-ttu-id="791e1-215">Kestrel — это кроссплатформенный веб-сервер для ASP.NET Core на основе libuv, кроссплатформенной библиотеки асинхронных операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="791e1-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="791e1-216">В отличие от WebListener, Kestrel не использует централизованный диспетчер конечных точек, такой как *http.sys*,</span><span class="sxs-lookup"><span data-stu-id="791e1-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="791e1-217">и не поддерживает совместное использование порта между несколькими процессами.</span><span class="sxs-lookup"><span data-stu-id="791e1-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="791e1-218">Каждый экземпляр Kestrel должен использовать уникальный порт.</span><span class="sxs-lookup"><span data-stu-id="791e1-218">Each instance of Kestrel must use a unique port.</span></span>

![Kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="791e1-220">Kestrel в службе без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="791e1-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="791e1-221">toouse `Kestrel` в службы без отслеживания состояния, переопределите hello `CreateServiceInstanceListeners` метода и возврата `KestrelCommunicationListener` экземпляр:</span><span class="sxs-lookup"><span data-stu-id="791e1-221">toouse `Kestrel` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="791e1-222">Kestrel в службе с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="791e1-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="791e1-223">toouse `Kestrel` в службы с отслеживанием состояния, переопределите hello `CreateServiceReplicaListeners` метода и возврата `KestrelCommunicationListener` экземпляр:</span><span class="sxs-lookup"><span data-stu-id="791e1-223">toouse `Kestrel` in a stateful service, override hello `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="791e1-224">В этом примере одноэлементный экземпляр `IReliableStateManager` предоставляется контейнер внедрения зависимостей toohello WebHost.</span><span class="sxs-lookup"><span data-stu-id="791e1-224">In this example, a singleton instance of `IReliableStateManager` is provided toohello WebHost dependency injection container.</span></span> <span data-ttu-id="791e1-225">Это не является обязательным, но позволяет toouse `IReliableStateManager` и надежного коллекций в методах действий контроллера MVC.</span><span class="sxs-lookup"><span data-stu-id="791e1-225">This is not strictly necessary, but it allows you toouse `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="791e1-226">Обратите внимание, что `Endpoint` имя конфигурации — **не** указано слишком`KestrelCommunicationListener` в службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="791e1-226">Note that an `Endpoint` configuration name is **not** provided too`KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="791e1-227">Это является более подробно описываются в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="791e1-227">This is explained in more detail in hello following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="791e1-228">Настройка конечной точки</span><span class="sxs-lookup"><span data-stu-id="791e1-228">Endpoint configuration</span></span>
<span data-ttu-id="791e1-229">`Endpoint` Конфигурация не требуется toouse Kestrel.</span><span class="sxs-lookup"><span data-stu-id="791e1-229">An `Endpoint` configuration is not required toouse Kestrel.</span></span> 

<span data-ttu-id="791e1-230">Kestrel является простой автономного веб-сервера; в отличие от WebListener (или HttpListener), не обязательно `Endpoint` конфигурации в *ServiceManifest.xml* из-за предыдущих toostarting регистрации URL-адрес не требуется.</span><span class="sxs-lookup"><span data-stu-id="791e1-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior toostarting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="791e1-231">Использование Kestrel и статического порта</span><span class="sxs-lookup"><span data-stu-id="791e1-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="791e1-232">Можно настроить статический порт в hello `Endpoint` конфигурации для использования с Kestrel ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="791e1-232">A static port can be configured in hello `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="791e1-233">Хотя это не является обязательным, это дает два потенциальных преимущества:</span><span class="sxs-lookup"><span data-stu-id="791e1-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="791e1-234">Если порт hello не попадает в диапазон портов приложения hello, он открыт через брандмауэр ОС hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="791e1-234">If hello port does not fall in hello application port range, it is opened through hello OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="791e1-235">Здравствуйте, tooyou указанного URL-адреса через `KestrelCommunicationListener` будет использовать этот порт.</span><span class="sxs-lookup"><span data-stu-id="791e1-235">hello URL provided tooyou through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="791e1-236">Если `Endpoint` будет настроен, его имя необходимо передавать в hello `KestrelCommunicationListener` конструктор:</span><span class="sxs-lookup"><span data-stu-id="791e1-236">If an `Endpoint` is configured, its name must be passed into hello `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="791e1-237">Если `Endpoint` конфигурация не используется, пропустите имя hello в hello `KestrelCommunicationListener` конструктор.</span><span class="sxs-lookup"><span data-stu-id="791e1-237">If an `Endpoint` configuration is not used, omit hello name in hello `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="791e1-238">В этом случае будет использоваться динамический порт.</span><span class="sxs-lookup"><span data-stu-id="791e1-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="791e1-239">Hello следующем разделе для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="791e1-239">See hello next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="791e1-240">Использование Kestrel и динамического порта</span><span class="sxs-lookup"><span data-stu-id="791e1-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="791e1-241">Kestrel нельзя использовать назначение автоматического порта hello из hello `Endpoint` конфигурации в файле ServiceManifest.xml, так как порт автоматическое назначение на основе `Endpoint` конфигурация назначает уникальный порт на *хост-процесса* , и один хост-процесс может содержать несколько экземпляров Kestrel.</span><span class="sxs-lookup"><span data-stu-id="791e1-241">Kestrel cannot use hello automatic port assignment from hello `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="791e1-242">Так как Kestrel не поддерживает совместное использование портов, это не будет работать, потому что каждый экземпляр Kestrel должен быть открыт на уникальном порте.</span><span class="sxs-lookup"><span data-stu-id="791e1-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="791e1-243">toouse динамическое назначение порта с Kestrel, просто пропустить hello `Endpoint` конфигурации в файле ServiceManifest.xml полностью, а не передавать toohello имя конечной точки `KestrelCommunicationListener` конструктор:</span><span class="sxs-lookup"><span data-stu-id="791e1-243">toouse dynamic port assignment with Kestrel, simply omit hello `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name toohello `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="791e1-244">В этой конфигурации `KestrelCommunicationListener` автоматически выбирает из диапазона портов приложения hello неиспользуемый порт.</span><span class="sxs-lookup"><span data-stu-id="791e1-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from hello application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="791e1-245">Сценарии и конфигурации</span><span class="sxs-lookup"><span data-stu-id="791e1-245">Scenarios and configurations</span></span>
<span data-ttu-id="791e1-246">В этом разделе описываются следующие сценарии hello и предоставляет hello рекомендуется сочетание веб-сервера, конфигурации портов, возможностей интеграции Service Fabric и прочие параметры tooachieve правильно работает служба:</span><span class="sxs-lookup"><span data-stu-id="791e1-246">This section describes hello following scenarios and provides hello recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings tooachieve a properly functioning service:</span></span>
 - <span data-ttu-id="791e1-247">Доступная извне служба ASP.NET Core без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="791e1-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="791e1-248">Служба ASP.NET Core без отслеживания состояния только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="791e1-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="791e1-249">Служба ASP.NET Core с отслеживанием состояния только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="791e1-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="791e1-250">**Извне предоставляется** понимается служба, которая предоставляет конечную точку, доступен с кластера hello, обычно через подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="791e1-250">An **externally exposed** service is one that exposes an endpoint reachable from outside hello cluster, usually through a load balancer.</span></span>

<span data-ttu-id="791e1-251">**Только для внутреннего использования** обслуживание — одна конечная точка которого доступен только в пределах кластера hello.</span><span class="sxs-lookup"><span data-stu-id="791e1-251">An **internal-only** service is one whose endpoint is only reachable from within hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="791e1-252">Службы с отслеживанием состояния, которые конечных точек обычно не должно быть предоставляются toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="791e1-252">Stateful service endpoints generally should not be exposed toohello Internet.</span></span> <span data-ttu-id="791e1-253">Кластеров, которые находятся позади подсистемы балансировки нагрузки, которые не знают о разрешения для службы Service Fabric, например hello балансировки нагрузки Azure будет невозможно tooexpose служб с отслеживанием состояния, так как hello балансировки нагрузки будет не может toolocate и направлять трафик toohello соответствующие службы с отслеживанием состояния реплики.</span><span class="sxs-lookup"><span data-stu-id="791e1-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as hello Azure Load Balancer, will be unable tooexpose stateful services because hello load balancer will not be able toolocate and route traffic toohello appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="791e1-254">Доступные извне службы ASP.NET Core без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="791e1-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="791e1-255">WebListener — hello, рекомендуется использовать веб-сервере переднего плана служб, предоставляющих конечные точки HTTP внешних, с выходом в Интернет в Windows.</span><span class="sxs-lookup"><span data-stu-id="791e1-255">WebListener is hello recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="791e1-256">Это обеспечивает более надежную защиту от атак и поддерживает функции, которые не поддерживает Kestrel (например, проверка подлинности Windows и общий доступ к портам).</span><span class="sxs-lookup"><span data-stu-id="791e1-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="791e1-257">В настоящее время Kestrel не поддерживается в качестве пограничного сервера (с доступом к Интернету).</span><span class="sxs-lookup"><span data-stu-id="791e1-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="791e1-258">Необходимо использовать обратного прокси-сервера, например IIS или Nginx toohandle трафик от hello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="791e1-258">A reverse proxy server such as IIS or Nginx must be used toohandle traffic from hello public Internet.</span></span>
 
<span data-ttu-id="791e1-259">При toohello предоставляется Интернет-службы без отслеживания состояния следует использовать хорошо известны и стабильный конечной точки, доступная через подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="791e1-259">When exposed toohello Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="791e1-260">Это URL-адрес hello предоставит toousers приложения.</span><span class="sxs-lookup"><span data-stu-id="791e1-260">This is hello URL you will provide toousers of your application.</span></span> <span data-ttu-id="791e1-261">рекомендуется следующая конфигурация Hello:</span><span class="sxs-lookup"><span data-stu-id="791e1-261">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="791e1-262">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="791e1-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="791e1-263">Веб-сервер</span><span class="sxs-lookup"><span data-stu-id="791e1-263">Web server</span></span> | <span data-ttu-id="791e1-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="791e1-264">WebListener</span></span> | <span data-ttu-id="791e1-265">Если служба hello только предоставляется tooa доверенной сети, такие как в интрасети и могут использоваться Kestrel.</span><span class="sxs-lookup"><span data-stu-id="791e1-265">If hello service is only exposed tooa trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="791e1-266">В противном случае WebListener — hello предпочтительный вариант.</span><span class="sxs-lookup"><span data-stu-id="791e1-266">Otherwise, WebListener is hello preferred option.</span></span> |
| <span data-ttu-id="791e1-267">Конфигурация порта</span><span class="sxs-lookup"><span data-stu-id="791e1-267">Port configuration</span></span> | <span data-ttu-id="791e1-268">static</span><span class="sxs-lookup"><span data-stu-id="791e1-268">static</span></span> | <span data-ttu-id="791e1-269">Хорошо известных статический порт должны быть настроены в hello `Endpoints` конфигурация ServiceManifest.xml, например 80 для HTTP и 443 для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="791e1-269">A well-known static port should be configured in hello `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="791e1-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="791e1-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="791e1-271">None</span><span class="sxs-lookup"><span data-stu-id="791e1-271">None</span></span> | <span data-ttu-id="791e1-272">Hello `ServiceFabricIntegrationOptions.None` параметр должен использоваться при настройке Service Fabric интеграции по промежуточного слоя, чтобы служба hello не будет пытаться toovalidate входящие запросы на уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="791e1-272">hello `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that hello service does not attempt toovalidate incoming requests for a unique identifier.</span></span> <span data-ttu-id="791e1-273">Внешние пользователи приложения не знает hello уникальных идентификационных данных используется по промежуточного слоя hello.</span><span class="sxs-lookup"><span data-stu-id="791e1-273">External users of your application will not know hello unique identifying information used by hello middleware.</span></span> |
| <span data-ttu-id="791e1-274">Число экземпляров</span><span class="sxs-lookup"><span data-stu-id="791e1-274">Instance Count</span></span> | <span data-ttu-id="791e1-275">-1</span><span class="sxs-lookup"><span data-stu-id="791e1-275">-1</span></span> | <span data-ttu-id="791e1-276">В типичные случаи использования, необходимо задать значение количества экземпляров hello слишком «-1», чтобы экземпляр доступен на всех узлах, получать трафик от подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="791e1-276">In typical use cases, hello instance count setting should be set too"-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="791e1-277">Если несколько служб извне предоставляется hello же набор узлов, следует использовать уникальны, но стабильный URL-пути.</span><span class="sxs-lookup"><span data-stu-id="791e1-277">If multiple externally exposed services share hello same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="791e1-278">Это можно сделать, изменив hello URL-адреса, указанные при настройке IWebHost.</span><span class="sxs-lookup"><span data-stu-id="791e1-278">This can be accomplished by modifying hello URL provided when configuring IWebHost.</span></span> <span data-ttu-id="791e1-279">Обратите внимание, что это применимо только tooWebListener.</span><span class="sxs-lookup"><span data-stu-id="791e1-279">Note this applies tooWebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="791e1-280">Служба ASP.NET Core без отслеживания состояния только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="791e1-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="791e1-281">Службы без сохранения состояния, которые вызываются только из внутри кластера hello должен использовать уникальный URL-адреса и динамически назначаемые порты tooensure взаимодействие между несколькими службами.</span><span class="sxs-lookup"><span data-stu-id="791e1-281">Stateless services that are only called from within hello cluster should use unique URLs and dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="791e1-282">рекомендуется следующая конфигурация Hello:</span><span class="sxs-lookup"><span data-stu-id="791e1-282">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="791e1-283">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="791e1-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="791e1-284">Веб-сервер</span><span class="sxs-lookup"><span data-stu-id="791e1-284">Web server</span></span> | <span data-ttu-id="791e1-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="791e1-285">Kestrel</span></span> | <span data-ttu-id="791e1-286">Несмотря на то, что WebListener может использоваться для внутренней службы без сохранения состояния, Kestrel является hello рекомендуется server tooallow несколько tooshare экземпляров службы узла.</span><span class="sxs-lookup"><span data-stu-id="791e1-286">Although WebListener may be used for internal stateless services, Kestrel is hello recommended server tooallow multiple service instances tooshare a host.</span></span>  |
| <span data-ttu-id="791e1-287">Конфигурация порта</span><span class="sxs-lookup"><span data-stu-id="791e1-287">Port configuration</span></span> | <span data-ttu-id="791e1-288">динамическое назначение</span><span class="sxs-lookup"><span data-stu-id="791e1-288">dynamically assigned</span></span> | <span data-ttu-id="791e1-289">Множество реплик службы с отслеживанием состояния могут совместно использовать хост-процесс или операционную систему, и поэтому для них требуются уникальные порты.</span><span class="sxs-lookup"><span data-stu-id="791e1-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="791e1-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="791e1-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="791e1-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="791e1-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="791e1-292">Динамическое назначение порта этот параметр запрещает проблема с идентификацией hello ошибочно описано выше.</span><span class="sxs-lookup"><span data-stu-id="791e1-292">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="791e1-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="791e1-293">InstanceCount</span></span> | <span data-ttu-id="791e1-294">любой</span><span class="sxs-lookup"><span data-stu-id="791e1-294">any</span></span> | <span data-ttu-id="791e1-295">необходимые toooperate hello tooany значение службы можно задать значение количества экземпляров Hello.</span><span class="sxs-lookup"><span data-stu-id="791e1-295">hello instance count setting can be set tooany value necessary toooperate hello service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="791e1-296">Служба ASP.NET Core с отслеживанием состояния только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="791e1-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="791e1-297">С отслеживанием состояния служб, которые вызываются только из внутри кластера hello следует использовать динамически назначаемые порты tooensure взаимодействие между несколькими службами.</span><span class="sxs-lookup"><span data-stu-id="791e1-297">Stateful services that are only called from within hello cluster should use dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="791e1-298">рекомендуется следующая конфигурация Hello:</span><span class="sxs-lookup"><span data-stu-id="791e1-298">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="791e1-299">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="791e1-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="791e1-300">Веб-сервер</span><span class="sxs-lookup"><span data-stu-id="791e1-300">Web server</span></span> | <span data-ttu-id="791e1-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="791e1-301">Kestrel</span></span> | <span data-ttu-id="791e1-302">Hello `WebListenerCommunicationListener` не предназначен для использования служб с отслеживанием состояния, в которых реплики совместно используют хост-процесса.</span><span class="sxs-lookup"><span data-stu-id="791e1-302">hello `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="791e1-303">Конфигурация порта</span><span class="sxs-lookup"><span data-stu-id="791e1-303">Port configuration</span></span> | <span data-ttu-id="791e1-304">динамическое назначение</span><span class="sxs-lookup"><span data-stu-id="791e1-304">dynamically assigned</span></span> | <span data-ttu-id="791e1-305">Множество реплик службы с отслеживанием состояния могут совместно использовать хост-процесс или операционную систему, и поэтому для них требуются уникальные порты.</span><span class="sxs-lookup"><span data-stu-id="791e1-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="791e1-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="791e1-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="791e1-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="791e1-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="791e1-308">Динамическое назначение порта этот параметр запрещает проблема с идентификацией hello ошибочно описано выше.</span><span class="sxs-lookup"><span data-stu-id="791e1-308">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="791e1-309">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="791e1-309">Next steps</span></span>
[<span data-ttu-id="791e1-310">Отладка приложения Service Fabric с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="791e1-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
