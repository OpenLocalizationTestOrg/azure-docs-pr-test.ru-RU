---
title: "Взаимодействие со службами через ASP.NET Core | Документация Майкрософт"
description: "Сведения об использовании ASP.NET Core в службах Reliable Services c отслеживанием и без отслеживания состояния."
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
ms.openlocfilehash: 8ac4d409f7363e8b4ae98be659a627ac8db8d787
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="cc61a-103">ASP.NET Core в Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cc61a-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="cc61a-104">ASP.NET Core — это новая кроссплатформенная среда с открытым кодом для создания современных облачных приложений с подключением к Интернету, таких как веб-приложения, приложения для Интернета вещей и серверные части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="cc61a-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="cc61a-105">Эта статья представляет собой подробное руководство по размещению служб ASP.NET Core в Service Fabric Reliable Services с использованием набора пакетов NuGet **Microsoft.ServiceFabric.AspNetCore.***.</span><span class="sxs-lookup"><span data-stu-id="cc61a-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="cc61a-106">Вводное руководство по ASP.NET Core в Service Fabric и инструкции по настройке среды разработки см. в статье [Создание внешнего интерфейса веб-службы для приложения с помощью ASP.NET Core](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="cc61a-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="cc61a-107">В оставшейся части этой статьи предполагается, что вы знакомы с размещением в ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="cc61a-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="cc61a-108">В противном случае мы рекомендуем ознакомиться с [базовыми понятиями ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="cc61a-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="cc61a-109">ASP.NET Core в среде Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cc61a-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="cc61a-110">Хотя приложения ASP.NET Core можно запускать на .NET Core или полной версии платформы .NET Framework, службы Service Fabric в настоящее время могут работать только на полной версии .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cc61a-110">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="cc61a-111">Это значит, что при создании службы ASP.NET Core Service Fabric по-прежнему необходимо ориентироваться на полную версию .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cc61a-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="cc61a-112">ASP.NET Core можно использовать двумя различными способами в Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="cc61a-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="cc61a-113">**Разместить в виде гостевого исполняемого файла**.</span><span class="sxs-lookup"><span data-stu-id="cc61a-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="cc61a-114">В основном это используется для запуска существующих приложений ASP.NET Core в Service Fabric без изменения кода.</span><span class="sxs-lookup"><span data-stu-id="cc61a-114">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="cc61a-115">**Выполнять внутри надежной службы**.</span><span class="sxs-lookup"><span data-stu-id="cc61a-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="cc61a-116">Это обеспечивает более эффективную интеграцию со средой выполнения Service Fabric и позволяет использовать службы ASP.NET Core с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="cc61a-116">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="cc61a-117">Далее в этой статье объясняется, как использовать ASP.NET Core внутри Reliable Service с помощью компонентов интеграции ASP.NET, поставляемых с пакетом SDK для Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cc61a-117">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="cc61a-118">Размещение службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cc61a-118">Service Fabric service hosting</span></span>

<span data-ttu-id="cc61a-119">В Service Fabric один или несколько экземпляров и (или) реплик службы выполняются в *хост-процессе службы* — исполняемом файле, который выполняет код службы.</span><span class="sxs-lookup"><span data-stu-id="cc61a-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="cc61a-120">Создателю службы принадлежит хост-процесс службы, который Service Fabric активирует и отслеживает.</span><span class="sxs-lookup"><span data-stu-id="cc61a-120">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="cc61a-121">Обычно ASP.NET (до MVC 5) тесно связан с IIS через System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="cc61a-121">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="cc61a-122">ASP.NET Core разделяет веб-сервер и веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="cc61a-122">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="cc61a-123">Это позволяет переносить веб-приложение между различными веб-серверами, а также позволяет веб-серверам быть *автономно размещаемыми*. Это означает, что веб-сервер можно запустить в собственном процессе, в отличие от процесса, который принадлежит выделенному ПО веб-сервера, такому как IIS.</span><span class="sxs-lookup"><span data-stu-id="cc61a-123">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="cc61a-124">Чтобы объединить службу Service Fabric и ASP.NET в Reliable Service или в качестве гостевого исполняемого приложения, необходимо запустить ASP.NET в хост-процессе службы.</span><span class="sxs-lookup"><span data-stu-id="cc61a-124">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="cc61a-125">Автономное размещение ASP.NET Core позволяет это сделать.</span><span class="sxs-lookup"><span data-stu-id="cc61a-125">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="cc61a-126">Размещение ASP.NET Core в Reliable Service</span><span class="sxs-lookup"><span data-stu-id="cc61a-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="cc61a-127">Как правило, автономно размещаемые приложения ASP.NET Core создают WebHost в точке входа приложения, например метод `static void Main()` в `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="cc61a-128">В таком случае жизненный цикл WebHost привязан к жизненному циклу процесса.</span><span class="sxs-lookup"><span data-stu-id="cc61a-128">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![Размещение ASP.NET Core в процессе][0]

<span data-ttu-id="cc61a-130">Точка входа приложения не подходит для создания WebHost в Reliable Service, так как она используется только для регистрации типа службы в среде выполнения Reliable Service, чтобы иметь возможность создавать экземпляры этого типа службы.</span><span class="sxs-lookup"><span data-stu-id="cc61a-130">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="cc61a-131">WebHost должен быть создан в Reliable Service автоматически.</span><span class="sxs-lookup"><span data-stu-id="cc61a-131">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="cc61a-132">В хост-процессе службы экземпляры службы и (или) реплики могут проходить несколько жизненных циклов.</span><span class="sxs-lookup"><span data-stu-id="cc61a-132">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="cc61a-133">Экземпляр Reliable Service представлен с помощью класса службы, производного от `StatelessService` или `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="cc61a-134">Стек связи для службы содержится в реализации `ICommunicationListener` класса службы.</span><span class="sxs-lookup"><span data-stu-id="cc61a-134">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="cc61a-135">Пакеты NuGet `Microsoft.ServiceFabric.Services.AspNetCore.*` содержат реализации `ICommunicationListener`, которые запускают и администрируют ASP.NET Core WebHost для Kestrel или WebListener в Reliable Service.</span><span class="sxs-lookup"><span data-stu-id="cc61a-135">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Размещение ASP.NET Core в Reliable Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="cc61a-137">Объекты ICommunicationListener в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cc61a-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="cc61a-138">Реализации `ICommunicationListener` Kestrel и WebListener в пакетах NuGet `Microsoft.ServiceFabric.Services.AspNetCore.*` имеют похожие шаблоны использования, но выполняют несколько различные действия для каждого веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="cc61a-138">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="cc61a-139">Оба прослушивателя связи предоставляют конструктор, который принимает следующие аргументы:</span><span class="sxs-lookup"><span data-stu-id="cc61a-139">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="cc61a-140">**`ServiceContext serviceContext`**. Объект `ServiceContext`, содержащий сведения о выполняемой службе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-140">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="cc61a-141">**`string endpointName`**. Имя конфигурации `Endpoint` в файле ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="cc61a-141">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="cc61a-142">Это основное отличие прослушивателей связи: для WebListener **требуется** конфигурация `Endpoint`, а для Kestrel — нет.</span><span class="sxs-lookup"><span data-stu-id="cc61a-142">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="cc61a-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**. Реализуемое лямбда-выражение, в котором создается и возвращается `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="cc61a-144">Это позволяет настроить `IWebHost` так же, как в приложении ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="cc61a-144">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="cc61a-145">Лямбда-выражение содержит URL-адрес, который создается в зависимости от используемых параметров интеграции Service Fabric и предоставляемой конфигурации `Endpoint`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-145">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="cc61a-146">Этот URL-адрес можно изменить или использовать "как есть" для запуска веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="cc61a-146">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="cc61a-147">ПО промежуточного уровня для интеграции Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cc61a-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="cc61a-148">Пакет NuGet `Microsoft.ServiceFabric.Services.AspNetCore` содержит метод расширения `UseServiceFabricIntegration` в `IWebHostBuilder`, который добавляет ПО промежуточного слоя, поддерживающее Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cc61a-148">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="cc61a-149">Это ПО промежуточного слоя настраивает `ICommunicationListener` Kestrel или WebListener, чтобы зарегистрировать уникальный URL-адрес службы с помощью службы именования Service Fabric, а затем проверяет запросы клиентов, чтобы клиенты подключались к правильной службе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-149">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="cc61a-150">Это необходимо в среде общего узла, например Service Fabric, где несколько веб-приложений могут работать на одном физическом компьютере или виртуальной машине, но не используют уникальные имена узлов, чтобы предотвратить ошибочные подключения клиентов к неверной службе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="cc61a-151">Данный сценарий описан более подробно в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-151">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="cc61a-152">Причина ошибочный идентификации</span><span class="sxs-lookup"><span data-stu-id="cc61a-152">A case of mistaken identity</span></span>
<span data-ttu-id="cc61a-153">Реплики службы, независимо от протокола, прослушивают уникальное сочетание "IP-адрес:порт".</span><span class="sxs-lookup"><span data-stu-id="cc61a-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="cc61a-154">Начав прослушивать, реплика службы конечной точки "IP-адрес:порт" сообщает адрес этой конечной точки службе именования Service Fabric, в которой его могут обнаружить клиенты или другие службы.</span><span class="sxs-lookup"><span data-stu-id="cc61a-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="cc61a-155">Если службы используют динамически назначаемые порты приложения, реплика службы может случайно использовать ту же конечную точку "IP-адрес:порт" другой службы, которая ранее находилась на том же физическом компьютере или виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="cc61a-155">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="cc61a-156">Это может привести к ошибочному подключению клиента к неверной службе,</span><span class="sxs-lookup"><span data-stu-id="cc61a-156">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="cc61a-157">что может произойти, если возникает следующая последовательность событий:</span><span class="sxs-lookup"><span data-stu-id="cc61a-157">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="cc61a-158">Служба А прослушивает 10.0.0.1:30000 по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="cc61a-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="cc61a-159">Клиент разрешает службу А и возвращает адрес 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="cc61a-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="cc61a-160">Служба А перемещается на другой узел.</span><span class="sxs-lookup"><span data-stu-id="cc61a-160">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="cc61a-161">Служба Б помещается в 10.0.0.1 и случайно использует тот же порт 30000.</span><span class="sxs-lookup"><span data-stu-id="cc61a-161">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="cc61a-162">Клиент пытается подключиться к службе А с помощью кэшированного адреса 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="cc61a-162">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="cc61a-163">Теперь клиент подключен к службе Б, не зная, что подключен к неверной службе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-163">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="cc61a-164">Это может периодически вызывать ошибки, которые трудно диагностировать.</span><span class="sxs-lookup"><span data-stu-id="cc61a-164">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="cc61a-165">Использование уникальных URL-адресов службы</span><span class="sxs-lookup"><span data-stu-id="cc61a-165">Using unique service URLs</span></span>
<span data-ttu-id="cc61a-166">Во избежание этого службы могут разместить конечную точку в службе имен с уникальным идентификатором, а затем проверять его во время обработки клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="cc61a-166">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="cc61a-167">Это совместное действие между службами в доверенной среде дружественного клиента.</span><span class="sxs-lookup"><span data-stu-id="cc61a-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="cc61a-168">Это не обеспечивает безопасную проверку подлинности службы в среде недружественного клиента.</span><span class="sxs-lookup"><span data-stu-id="cc61a-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="cc61a-169">В доверенной среде ПО промежуточного слоя, которое добавляется с помощью метода `UseServiceFabricIntegration`, автоматически добавляет уникальный идентификатор к адресу, размещенному в службе именования, и проверяет этот идентификатор в каждом запросе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-169">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="cc61a-170">Если идентификатор не совпадает, ПО промежуточного слоя немедленно возвращает ответ HTTP 410 — потеряно.</span><span class="sxs-lookup"><span data-stu-id="cc61a-170">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="cc61a-171">Службы, использующие динамически назначаемый порт, должны использовать это ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="cc61a-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="cc61a-172">Службы, использующие постоянный уникальный порт, не имеют такой проблемы в совместной среде.</span><span class="sxs-lookup"><span data-stu-id="cc61a-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="cc61a-173">Постоянный уникальный порт обычно используется для внешних служб, которым необходим известный порт для подключения клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="cc61a-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="cc61a-174">Например, большинство веб-приложений с доступом к Интернету используют порт 80 или 443 для подключений веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="cc61a-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="cc61a-175">В этом случае не следует включать уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="cc61a-175">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="cc61a-176">На схеме ниже показан поток запроса с включенным ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="cc61a-176">The following diagram shows the request flow with the middleware enabled:</span></span>

![Интеграция Service Fabric ASP.NET Core][2]

<span data-ttu-id="cc61a-178">Реализации `ICommunicationListener` Kestrel и WebListener используют этот механизм точно таким же образом.</span><span class="sxs-lookup"><span data-stu-id="cc61a-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="cc61a-179">Несмотря на то что WebListener может внутренне различать запросы на основе уникальных URL-адресов с помощью базовой функции совместного использования портов *http.sys*, эта функция *не* используется реализацией `ICommunicationListener` WebListener, так как это приведет к ошибкам с кодами состояния HTTP 503 и HTTP 404 в сценарии, описанном выше.</span><span class="sxs-lookup"><span data-stu-id="cc61a-179">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="cc61a-180">В свою очередь для клиентов это усложняет определение причины ошибки, так как HTTP 503 и HTTP 404 часто используются для указания других ошибок.</span><span class="sxs-lookup"><span data-stu-id="cc61a-180">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="cc61a-181">Таким образом, реализации `ICommunicationListener` Kestrel и WebListener стандартизируют ПО промежуточного слоя, предоставляемое методом расширения `UseServiceFabricIntegration`, чтобы клиенты выполняли только одно действие повторного разрешения конечной точки службы в ответах HTTP 410.</span><span class="sxs-lookup"><span data-stu-id="cc61a-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="cc61a-182">WebListener в службах Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cc61a-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="cc61a-183">WebListener можно использовать в Reliable Service, импортировав пакет NuGet **Microsoft.ServiceFabric.AspNetCore.WebListener**.</span><span class="sxs-lookup"><span data-stu-id="cc61a-183">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="cc61a-184">Этот пакет содержит `WebListenerCommunicationListener`, реализацию `ICommunicationListener`, которая позволяет создавать WebHost ASP.NET Core внутри Reliable Service с помощью WebListener в качестве веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="cc61a-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="cc61a-185">WebListener основан на [API сервера HTTP Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="cc61a-185">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="cc61a-186">При этом используется драйвер ядра *http.sys*, применяемый IIS для обработки HTTP-запросов и их перенаправления в процессы, выполняющие веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cc61a-186">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="cc61a-187">Это позволяет нескольким процессам на одном физическом компьютере или виртуальной машине размещать на одном порту веб-приложения, которые отличаются уникальным URL-адресом или именем узла.</span><span class="sxs-lookup"><span data-stu-id="cc61a-187">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="cc61a-188">Эти функции в Service Fabric полезны для размещения нескольких веб-сайтов в одном кластере.</span><span class="sxs-lookup"><span data-stu-id="cc61a-188">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="cc61a-189">На следующей схеме показано, как WebListener использует драйвер ядра *http.sys* в Windows для совместного использования портов:</span><span class="sxs-lookup"><span data-stu-id="cc61a-189">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="cc61a-191">WebListener в службе без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="cc61a-191">WebListener in a stateless service</span></span>
<span data-ttu-id="cc61a-192">Для использования `WebListener` в службе без отслеживания состояния переопределите метод `CreateServiceInstanceListeners` и верните экземпляр `WebListenerCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="cc61a-192">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

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

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="cc61a-193">WebListener в службе с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="cc61a-193">WebListener in a stateful service</span></span>

<span data-ttu-id="cc61a-194">`WebListenerCommunicationListener` в настоящее время не предназначен для использования в службах с отслеживанием состояния из-за сложности с базовой функцией совместного использования портов *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="cc61a-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="cc61a-195">Дополнительные сведения о динамическом назначении портов WebListener см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-195">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="cc61a-196">Для служб с отслеживанием состояния рекомендуемым веб-сервером является Kestrel.</span><span class="sxs-lookup"><span data-stu-id="cc61a-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="cc61a-197">Настройка конечной точки</span><span class="sxs-lookup"><span data-stu-id="cc61a-197">Endpoint configuration</span></span>

<span data-ttu-id="cc61a-198">Для веб-серверов, использующих API сервера HTTP Windows (включая WebListener), требуется конфигурация `Endpoint`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="cc61a-199">Для веб-серверов, использующих API сервера HTTP Windows, сначала необходимо зарезервировать URL-адрес в *http.sys* (обычно это осуществляется с помощью средства [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx)).</span><span class="sxs-lookup"><span data-stu-id="cc61a-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="cc61a-200">Для этого действия требуются повышенные привилегии, которых по умолчанию нет у служб.</span><span class="sxs-lookup"><span data-stu-id="cc61a-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="cc61a-201">Параметры HTTP или HTTPS для свойства `Protocol` конфигурации `Endpoint` в файле *ServiceManifest.xml* используются специально для того, чтобы сообщить среде выполнения Service Fabric о необходимости регистрации URL-адреса в *http.sys* от вашего имени с помощью [*надежного шаблона*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) префикса URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="cc61a-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="cc61a-202">Например, чтобы зарезервировать `http://+:80` для службы, в файле ServiceManifest.xml следует использовать следующую конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="cc61a-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

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

<span data-ttu-id="cc61a-203">Также необходимо передать имя конечной точки в конструктор `WebListenerCommunicationListener`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-203">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

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

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="cc61a-204">Использование WebListener со статическим портом</span><span class="sxs-lookup"><span data-stu-id="cc61a-204">Use WebListener with a static port</span></span>
<span data-ttu-id="cc61a-205">Чтобы использовать статический порт с WebListener, укажите номер порта в конфигурации `Endpoint`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-205">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="cc61a-206">Использование WebListener с динамическим портом</span><span class="sxs-lookup"><span data-stu-id="cc61a-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="cc61a-207">Чтобы использовать динамически назначаемый порт с WebListener, опустите свойство `Port` в конфигурации `Endpoint`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-207">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="cc61a-208">Обратите внимание, что динамический порт, выделенный с помощью конфигурации `Endpoint`, предоставляет только один порт *каждому хост-процессу*.</span><span class="sxs-lookup"><span data-stu-id="cc61a-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="cc61a-209">Текущая модель размещения Service Fabric позволяет размещать в одном процессе несколько экземпляров службы и (или) реплик. Это означает, что они будут совместно использовать один и тот же порт при выделении с помощью конфигурации `Endpoint`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="cc61a-210">Множество экземпляров WebListener могут совместно использовать порт с помощью базовой функции совместного использования портов *http.sys*. Это не поддерживается `WebListenerCommunicationListener` из-за сложности обработки клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="cc61a-210">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="cc61a-211">Для использования динамических портов рекомендуемым веб-сервером является Kestrel.</span><span class="sxs-lookup"><span data-stu-id="cc61a-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="cc61a-212">Kestrel в Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cc61a-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="cc61a-213">Kestrel можно использовать в Reliable Service, импортировав пакет NuGet **Microsoft.ServiceFabric.AspNetCore.Kestrel**.</span><span class="sxs-lookup"><span data-stu-id="cc61a-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="cc61a-214">Этот пакет содержит `KestrelCommunicationListener`, реализацию `ICommunicationListener`, которая позволяет создавать WebHost ASP.NET Core внутри Reliable Service с помощью Kestrel в качестве веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="cc61a-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="cc61a-215">Kestrel — это кроссплатформенный веб-сервер для ASP.NET Core на основе libuv, кроссплатформенной библиотеки асинхронных операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="cc61a-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="cc61a-216">В отличие от WebListener, Kestrel не использует централизованный диспетчер конечных точек, такой как *http.sys*,</span><span class="sxs-lookup"><span data-stu-id="cc61a-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="cc61a-217">и не поддерживает совместное использование порта между несколькими процессами.</span><span class="sxs-lookup"><span data-stu-id="cc61a-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="cc61a-218">Каждый экземпляр Kestrel должен использовать уникальный порт.</span><span class="sxs-lookup"><span data-stu-id="cc61a-218">Each instance of Kestrel must use a unique port.</span></span>

![Kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="cc61a-220">Kestrel в службе без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="cc61a-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="cc61a-221">Для использования `Kestrel` в службе без отслеживания состояния переопределите метод `CreateServiceInstanceListeners` и верните экземпляр `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="cc61a-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="cc61a-222">Kestrel в службе с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="cc61a-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="cc61a-223">Для использования `Kestrel` в службе с отслеживанием состояния переопределите метод `CreateServiceReplicaListeners` и верните экземпляр `KestrelCommunicationListener`:</span><span class="sxs-lookup"><span data-stu-id="cc61a-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

<span data-ttu-id="cc61a-224">В этом примере одноэлементный экземпляр `IReliableStateManager` предоставляется контейнеру внедрения зависимостей WebHost.</span><span class="sxs-lookup"><span data-stu-id="cc61a-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="cc61a-225">Это не является обязательным, но позволяет использовать `IReliableStateManager` и надежные коллекции в методах действий контроллера MVC.</span><span class="sxs-lookup"><span data-stu-id="cc61a-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="cc61a-226">Обратите внимание, что имя конфигурации `Endpoint` **не** предоставляется `KestrelCommunicationListener` в службе с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="cc61a-226">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="cc61a-227">Это объясняется более подробно в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="cc61a-228">Настройка конечной точки</span><span class="sxs-lookup"><span data-stu-id="cc61a-228">Endpoint configuration</span></span>
<span data-ttu-id="cc61a-229">Для использования Kestrel конфигурация `Endpoint` не требуется.</span><span class="sxs-lookup"><span data-stu-id="cc61a-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="cc61a-230">Kestrel является простым автономным веб-сервером, для которого, в отличие от WebListener (или HttpListener), не требуется конфигурация `Endpoint` в файле *ServiceManifest.xml*, так как для запуска регистрация URL-адреса не требуется.</span><span class="sxs-lookup"><span data-stu-id="cc61a-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="cc61a-231">Использование Kestrel и статического порта</span><span class="sxs-lookup"><span data-stu-id="cc61a-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="cc61a-232">Можно настроить статический порт в конфигурации `Endpoint` файла ServiceManifest.xml для использования с Kestrel.</span><span class="sxs-lookup"><span data-stu-id="cc61a-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="cc61a-233">Хотя это не является обязательным, это дает два потенциальных преимущества:</span><span class="sxs-lookup"><span data-stu-id="cc61a-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="cc61a-234">Если порт не попадает в диапазон портов для приложений, он открывается в брандмауэре ОС с помощью Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cc61a-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="cc61a-235">URL-адрес, предоставленный с помощью `KestrelCommunicationListener`, будет использовать этот порт.</span><span class="sxs-lookup"><span data-stu-id="cc61a-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="cc61a-236">Если `Endpoint` настроена, ее имя необходимо передать в конструктор `KestrelCommunicationListener`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="cc61a-237">Если конфигурация `Endpoint` не используется, не указывайте имя конечной точки в конструкторе `KestrelCommunicationListener`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="cc61a-238">В этом случае будет использоваться динамический порт.</span><span class="sxs-lookup"><span data-stu-id="cc61a-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="cc61a-239">Этот процесс описан в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="cc61a-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="cc61a-240">Использование Kestrel и динамического порта</span><span class="sxs-lookup"><span data-stu-id="cc61a-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="cc61a-241">Kestrel не может использовать автоматическое назначение порта из конфигурации `Endpoint` в файле ServiceManifest.xml, так как автоматическое назначение порта из конфигурации `Endpoint` назначает уникальный порт каждому *хост-процессу*. В результате один хост-процесс может содержать несколько экземпляров Kestrel.</span><span class="sxs-lookup"><span data-stu-id="cc61a-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="cc61a-242">Так как Kestrel не поддерживает совместное использование портов, это не будет работать, потому что каждый экземпляр Kestrel должен быть открыт на уникальном порте.</span><span class="sxs-lookup"><span data-stu-id="cc61a-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="cc61a-243">Чтобы использовать динамическое назначение порта в Kestrel, достаточно полностью опустить конфигурацию `Endpoint` в файле ServiceManifest.xml и не передавать имя конечной точки в конструктор `KestrelCommunicationListener`.</span><span class="sxs-lookup"><span data-stu-id="cc61a-243">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="cc61a-244">В этой конфигурации `KestrelCommunicationListener` автоматически выберет неиспользуемый порт из диапазона портов приложения.</span><span class="sxs-lookup"><span data-stu-id="cc61a-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="cc61a-245">Сценарии и конфигурации</span><span class="sxs-lookup"><span data-stu-id="cc61a-245">Scenarios and configurations</span></span>
<span data-ttu-id="cc61a-246">В этом разделе описаны следующие сценарии и приведено рекомендуемое сочетание веб-сервера, конфигурации порта, параметров интеграции Service Fabric и прочих параметров для обеспечения правильной работы службы.</span><span class="sxs-lookup"><span data-stu-id="cc61a-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="cc61a-247">Доступная извне служба ASP.NET Core без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="cc61a-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="cc61a-248">Служба ASP.NET Core без отслеживания состояния только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="cc61a-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="cc61a-249">Служба ASP.NET Core с отслеживанием состояния только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="cc61a-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="cc61a-250">**Доступная извне** служба предоставляет конечную точку, доступную за пределами кластера, обычно через балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc61a-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="cc61a-251">Служба **только для внутреннего использования** — это служба, конечная точка которой доступна только в пределах кластера.</span><span class="sxs-lookup"><span data-stu-id="cc61a-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="cc61a-252">Конечные точки службы с отслеживанием состояния не следует делать доступными в Интернете.</span><span class="sxs-lookup"><span data-stu-id="cc61a-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="cc61a-253">Кластеры, находящиеся за балансировщиками нагрузки, которые не поддерживают разрешение служб Service Fabric (например, Azure Load Balancer), не смогут предоставить службы с отслеживанием состояния, так как балансировщик нагрузки не сможет обнаруживать и направлять трафик в соответствующую реплику службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="cc61a-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="cc61a-254">Доступные извне службы ASP.NET Core без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="cc61a-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="cc61a-255">WebListener является рекомендуемым веб-сервером для внешних служб, которые предоставляют внешние конечные точки HTTP Windows с доступом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="cc61a-255">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="cc61a-256">Это обеспечивает более надежную защиту от атак и поддерживает функции, которые не поддерживает Kestrel (например, проверка подлинности Windows и общий доступ к портам).</span><span class="sxs-lookup"><span data-stu-id="cc61a-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="cc61a-257">В настоящее время Kestrel не поддерживается в качестве пограничного сервера (с доступом к Интернету).</span><span class="sxs-lookup"><span data-stu-id="cc61a-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="cc61a-258">Для обработки трафика из общедоступного Интернета необходимо использовать обратный прокси-сервер, например IIS или Nginx.</span><span class="sxs-lookup"><span data-stu-id="cc61a-258">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="cc61a-259">Доступная через Интернет, служба без отслеживания состояния должна использовать хорошо известную и стабильную конечную точку, доступную через балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc61a-259">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="cc61a-260">Это URL-адрес, который будет предоставляться пользователям приложения.</span><span class="sxs-lookup"><span data-stu-id="cc61a-260">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="cc61a-261">Рекомендуется следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="cc61a-261">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="cc61a-262">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="cc61a-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc61a-263">Веб-сервер</span><span class="sxs-lookup"><span data-stu-id="cc61a-263">Web server</span></span> | <span data-ttu-id="cc61a-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="cc61a-264">WebListener</span></span> | <span data-ttu-id="cc61a-265">Если служба доступна только в доверенной сети, такой как интрасеть, можно использовать Kestrel.</span><span class="sxs-lookup"><span data-stu-id="cc61a-265">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="cc61a-266">В противном случае WebListener является предпочтительным вариантом.</span><span class="sxs-lookup"><span data-stu-id="cc61a-266">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="cc61a-267">Конфигурация порта</span><span class="sxs-lookup"><span data-stu-id="cc61a-267">Port configuration</span></span> | <span data-ttu-id="cc61a-268">static</span><span class="sxs-lookup"><span data-stu-id="cc61a-268">static</span></span> | <span data-ttu-id="cc61a-269">Хорошо известный статический порт необходимо настроить в конфигурации `Endpoints` файла ServiceManifest.xml, например 80 для HTTP и 443 для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cc61a-269">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="cc61a-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="cc61a-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="cc61a-271">None</span><span class="sxs-lookup"><span data-stu-id="cc61a-271">None</span></span> | <span data-ttu-id="cc61a-272">Параметр `ServiceFabricIntegrationOptions.None` должен использоваться при настройке ПО промежуточного слоя интеграции Service Fabric, чтобы служба не пыталась проверять входящие запросы для уникального идентификатора.</span><span class="sxs-lookup"><span data-stu-id="cc61a-272">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="cc61a-273">Внешние пользователи приложения не будут знать уникальные идентификаторы, используемые ПО промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="cc61a-273">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="cc61a-274">Число экземпляров</span><span class="sxs-lookup"><span data-stu-id="cc61a-274">Instance Count</span></span> | <span data-ttu-id="cc61a-275">-1</span><span class="sxs-lookup"><span data-stu-id="cc61a-275">-1</span></span> | <span data-ttu-id="cc61a-276">При стандартных вариантах использования значение количества экземпляров должно быть равно "-1", чтобы экземпляр становился доступным на всех узлах, получающих трафик от балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc61a-276">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="cc61a-277">Если несколько служб, предоставляемых извне, совместно используют один и тот же набор узлов, следует использовать уникальный, но стабильный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="cc61a-277">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="cc61a-278">Это можно сделать, изменив URL-адрес, указанный при настройке IWebHost.</span><span class="sxs-lookup"><span data-stu-id="cc61a-278">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="cc61a-279">Обратите внимание, что это относится только к WebListener.</span><span class="sxs-lookup"><span data-stu-id="cc61a-279">Note this applies to WebListener only.</span></span>

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

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="cc61a-280">Служба ASP.NET Core без отслеживания состояния только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="cc61a-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="cc61a-281">Службы без отслеживания состояния, которые вызываются только из кластера, должны использовать уникальные URL-адреса и динамически назначаемые порты для обеспечения взаимодействия между несколькими службами.</span><span class="sxs-lookup"><span data-stu-id="cc61a-281">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="cc61a-282">Рекомендуется следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="cc61a-282">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="cc61a-283">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="cc61a-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc61a-284">Веб-сервер</span><span class="sxs-lookup"><span data-stu-id="cc61a-284">Web server</span></span> | <span data-ttu-id="cc61a-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="cc61a-285">Kestrel</span></span> | <span data-ttu-id="cc61a-286">Несмотря на то что WebListener может использоваться для внутренних служб без отслеживания состояния, Kestrel является рекомендуемым сервером для разрешения совместного использования узла несколькими экземплярами службы.</span><span class="sxs-lookup"><span data-stu-id="cc61a-286">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="cc61a-287">Конфигурация порта</span><span class="sxs-lookup"><span data-stu-id="cc61a-287">Port configuration</span></span> | <span data-ttu-id="cc61a-288">динамическое назначение</span><span class="sxs-lookup"><span data-stu-id="cc61a-288">dynamically assigned</span></span> | <span data-ttu-id="cc61a-289">Множество реплик службы с отслеживанием состояния могут совместно использовать хост-процесс или операционную систему, и поэтому для них требуются уникальные порты.</span><span class="sxs-lookup"><span data-stu-id="cc61a-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="cc61a-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="cc61a-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="cc61a-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="cc61a-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="cc61a-292">При динамическом назначении порта этот параметр предотвращает ошибочную идентификацию, описанную ранее.</span><span class="sxs-lookup"><span data-stu-id="cc61a-292">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="cc61a-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="cc61a-293">InstanceCount</span></span> | <span data-ttu-id="cc61a-294">любой</span><span class="sxs-lookup"><span data-stu-id="cc61a-294">any</span></span> | <span data-ttu-id="cc61a-295">Для параметра количества экземпляров может быть присвоено любое значение, необходимое для работы службы.</span><span class="sxs-lookup"><span data-stu-id="cc61a-295">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="cc61a-296">Служба ASP.NET Core с отслеживанием состояния только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="cc61a-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="cc61a-297">Службы с отслеживанием состояния, которые вызываются только из кластера, должны использовать динамически назначаемые порты для обеспечения взаимодействия между несколькими службами.</span><span class="sxs-lookup"><span data-stu-id="cc61a-297">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="cc61a-298">Рекомендуется следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="cc61a-298">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="cc61a-299">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="cc61a-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc61a-300">Веб-сервер</span><span class="sxs-lookup"><span data-stu-id="cc61a-300">Web server</span></span> | <span data-ttu-id="cc61a-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="cc61a-301">Kestrel</span></span> | <span data-ttu-id="cc61a-302">`WebListenerCommunicationListener` не предназначен для служб с отслеживанием состояния, в которых реплики совместно используют хост-процесс.</span><span class="sxs-lookup"><span data-stu-id="cc61a-302">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="cc61a-303">Конфигурация порта</span><span class="sxs-lookup"><span data-stu-id="cc61a-303">Port configuration</span></span> | <span data-ttu-id="cc61a-304">динамическое назначение</span><span class="sxs-lookup"><span data-stu-id="cc61a-304">dynamically assigned</span></span> | <span data-ttu-id="cc61a-305">Множество реплик службы с отслеживанием состояния могут совместно использовать хост-процесс или операционную систему, и поэтому для них требуются уникальные порты.</span><span class="sxs-lookup"><span data-stu-id="cc61a-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="cc61a-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="cc61a-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="cc61a-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="cc61a-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="cc61a-308">При динамическом назначении порта этот параметр предотвращает ошибочную идентификацию, описанную ранее.</span><span class="sxs-lookup"><span data-stu-id="cc61a-308">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cc61a-309">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc61a-309">Next steps</span></span>
[<span data-ttu-id="cc61a-310">Отладка приложения Service Fabric с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc61a-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
