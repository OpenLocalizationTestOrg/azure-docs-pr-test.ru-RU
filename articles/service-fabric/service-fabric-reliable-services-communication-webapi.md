---
title: "aaaService связь с веб-API ASP.NET hello | Документы Microsoft"
description: "Узнайте, как с помощью пошаговые связь со службой tooimplement hello веб-API ASP.NET с OWIN Резидентное размещение в hello надежные API служб."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="933dc-103">Приступая к работе со службами веб-API Service Fabric с саморазмещением OWIN</span><span class="sxs-lookup"><span data-stu-id="933dc-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="933dc-104">Azure Service Fabric помещает hello power в руках, когда нужно решить, как будет toocommunicate вашей службы с пользователями и друг с другом.</span><span class="sxs-lookup"><span data-stu-id="933dc-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="933dc-105">Это руководство посвящено реализации взаимодействия служб с помощью веб-API ASP.NET с саморазмещением Open Web Interface for .NET (OWIN) в API Reliable Services на платформе Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="933dc-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="933dc-106">Мы будем глубокое понимание hello подключаемые связи надежные службы API.</span><span class="sxs-lookup"><span data-stu-id="933dc-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="933dc-107">Мы будем использовать веб-API в tooshow пошаговый пример вы как tooset слушателя пользовательского взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="933dc-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="933dc-108">Введение tooWeb API в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="933dc-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="933dc-109">Веб-API ASP.NET — популярный и мощная платформа для создания HTTP API-интерфейсы поверх hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="933dc-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="933dc-110">Если вы не знакомы с hello framework, см. раздел [Приступая к работе с ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="933dc-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="933dc-111">Веб-API в Service Fabric hello же веб-API ASP.NET вы хорошо знакомую и любимую.</span><span class="sxs-lookup"><span data-stu-id="933dc-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="933dc-112">Hello различие заключается в том, как вы *узла* приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="933dc-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="933dc-113">Этот процесс не предусматривает использование Microsoft IIS.</span><span class="sxs-lookup"><span data-stu-id="933dc-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="933dc-114">toobetter понять разницу hello, давайте разбить на две части:</span><span class="sxs-lookup"><span data-stu-id="933dc-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="933dc-115">Hello веб-API приложения (включая контроллеры и модели)</span><span class="sxs-lookup"><span data-stu-id="933dc-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="933dc-116">узел Hello (hello веб-сервера, обычно IIS)</span><span class="sxs-lookup"><span data-stu-id="933dc-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="933dc-117">Само приложение веб-API не меняется.</span><span class="sxs-lookup"><span data-stu-id="933dc-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="933dc-118">Оно ничем не отличается от веб-API приложения, созданные в предыдущих hello и должен быть перемещения может toosimply через большую часть кода приложения.</span><span class="sxs-lookup"><span data-stu-id="933dc-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="933dc-119">Но если размещения в IIS, используется для размещения приложения hello может быть немного отличается от том, что вы привыкли.</span><span class="sxs-lookup"><span data-stu-id="933dc-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="933dc-120">Прежде чем мы получаем toohello размещение часть, начнем с чего-либо более привычной: hello приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="933dc-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="933dc-121">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="933dc-121">Create hello application</span></span>
<span data-ttu-id="933dc-122">Для начала создайте в Visual Studio 2015 приложение Service Fabric с одной службой без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="933dc-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="933dc-123">Шаблон Visual Studio для службы без отслеживания состояния, с помощью веб-API — доступные tooyou.</span><span class="sxs-lookup"><span data-stu-id="933dc-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="933dc-124">В этом руководстве мы с нуля создадим проект веб-API, который покажет, какие результаты можно получить, выбрав этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="933dc-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="933dc-125">Выберите пустой проект toolearn службы без отслеживания состояния как toobuild проект веб-API с нуля, или начала можно использовать службы без отслеживания состояния hello шаблона веб-API и следуйте.</span><span class="sxs-lookup"><span data-stu-id="933dc-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="933dc-126">Hello первым шагом является toopull в некоторые пакеты NuGet для веб-API.</span><span class="sxs-lookup"><span data-stu-id="933dc-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="933dc-127">пакет Hello, мы хотим toouse — Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="933dc-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="933dc-128">Этот пакет содержит все необходимые пакеты веб-API hello и hello *узла* пакетов.</span><span class="sxs-lookup"><span data-stu-id="933dc-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="933dc-129">Это будет важно в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="933dc-129">This will be important later.</span></span>

<span data-ttu-id="933dc-130">После установки пакетов hello можно начать создавать hello базовая структура проекта веб-API.</span><span class="sxs-lookup"><span data-stu-id="933dc-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="933dc-131">Если используется веб-API, структура проекта hello похожа на.</span><span class="sxs-lookup"><span data-stu-id="933dc-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="933dc-132">Начните с добавления каталога `Controllers` и контроллера простых значений.</span><span class="sxs-lookup"><span data-stu-id="933dc-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="933dc-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="933dc-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="933dc-134">Добавьте класс запуска на корневой tooregister hello проекта hello маршрутизации, форматирования и настройки установки.</span><span class="sxs-lookup"><span data-stu-id="933dc-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="933dc-135">Это также где подключает веб-API toohello *узла*, которой будет пересмотрено попытку позже.</span><span class="sxs-lookup"><span data-stu-id="933dc-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="933dc-136">**Startup.cs.**</span><span class="sxs-lookup"><span data-stu-id="933dc-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="933dc-137">Вот и все части приложения hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-137">That's it for hello application part.</span></span> <span data-ttu-id="933dc-138">На этом этапе мы настроили просто hello основные веб-API макет проекта.</span><span class="sxs-lookup"><span data-stu-id="933dc-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="933dc-139">Таким образом не должен выглядеть сильно отличается от проектов веб-API, которые в прошлом hello вы написали или от hello базового шаблона веб-API.</span><span class="sxs-lookup"><span data-stu-id="933dc-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="933dc-140">Бизнес-логики попадают в контроллерах hello и модели в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="933dc-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="933dc-141">Какие шаги по размещению следует выполнить для реального запуска?</span><span class="sxs-lookup"><span data-stu-id="933dc-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="933dc-142">Размещение службы</span><span class="sxs-lookup"><span data-stu-id="933dc-142">Service hosting</span></span>
<span data-ttu-id="933dc-143">В Service Fabric служба запускается в *хост-процессе службы*— исполняемом файле, который выполняет код службы.</span><span class="sxs-lookup"><span data-stu-id="933dc-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="933dc-144">При написании службы с помощью hello надежные API служб проект службы просто компилирует tooan исполняемый файл, который регистрирует тип службы и выполняет код.</span><span class="sxs-lookup"><span data-stu-id="933dc-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="933dc-145">Так происходит в большинстве случаев при написании службы для Service Fabric на платформе .NET.</span><span class="sxs-lookup"><span data-stu-id="933dc-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="933dc-146">При открытии Program.cs в проекте службы без отслеживания состояния hello, вы увидите:</span><span class="sxs-lookup"><span data-stu-id="933dc-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="933dc-147">Если выглядящий подозрительно hello запись точки tooa консольного приложения, то, так как он является.</span><span class="sxs-lookup"><span data-stu-id="933dc-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="933dc-148">Дополнительные сведения об hello хост-процесса службы и службы регистрации выходят за рамки данной статьи hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="933dc-149">Но это tooknow важные для теперь, когда *код службы выполняется в собственном процессе*.</span><span class="sxs-lookup"><span data-stu-id="933dc-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="933dc-150">Саморазмещение веб-API с использованием хоста OWIN</span><span class="sxs-lookup"><span data-stu-id="933dc-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="933dc-151">Учитывая, что код приложения веб-API размещается в отдельном процессе, как подсоединить его tooa веб-сервер?</span><span class="sxs-lookup"><span data-stu-id="933dc-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="933dc-152">Для этого есть [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="933dc-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="933dc-153">OWIN — это просто контракт между веб-приложениями .NET и веб-серверами.</span><span class="sxs-lookup"><span data-stu-id="933dc-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="933dc-154">В большинстве случаев при использовании ASP.NET (вверх tooMVC 5) hello веб-приложения является тесно связанные tooIIS через System.Web.</span><span class="sxs-lookup"><span data-stu-id="933dc-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="933dc-155">Однако веб-API реализует OWIN, можно создать веб-приложение, которое связано с hello веб-сервера, на котором она размещена.</span><span class="sxs-lookup"><span data-stu-id="933dc-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="933dc-156">Таким образом вы можете использовать *тестовый* веб-сервер OWIN, который можно запускать отдельным процессом.</span><span class="sxs-lookup"><span data-stu-id="933dc-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="933dc-157">Это идеально подходит с hello Service Fabric модели размещения которых мы писали выше.</span><span class="sxs-lookup"><span data-stu-id="933dc-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="933dc-158">В этой статье мы будем использовать Katana как hello OWIN узла для веб-API приложения hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="933dc-159">Katana представляет собой реализацию узла OWIN открытым исходным кодом, построенных на [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) и hello Windows [API HTTP-сервера](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="933dc-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="933dc-160">Дополнительные сведения о Katana, последовательно выберите toohello toolearn [Katana сайта](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="933dc-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="933dc-161">Краткий обзор того, как toouse Katana tooself узла веб-API, в разделе [OWIN используйте tooSelf узла веб-API ASP.NET 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="933dc-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="933dc-162">Установить веб-сервер hello</span><span class="sxs-lookup"><span data-stu-id="933dc-162">Set up hello web server</span></span>
<span data-ttu-id="933dc-163">Hello надежные API служб предоставляет точку входа связи, где можно подключить стеками связи, позволяющие пользователям и клиентам tooconnect toohello службы:</span><span class="sxs-lookup"><span data-stu-id="933dc-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="933dc-164">Hello веб-сервера (и другие стек связи, используемого в будущем, таких как WebSockets hello) следует использовать интерфейс toointegrate hello ICommunicationListener правильно с системой hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="933dc-165">Hello причины этого станет яснее в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="933dc-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="933dc-166">Сначала создайте класс с именем OwinCommunicationListener, который реализует ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="933dc-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="933dc-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="933dc-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="933dc-168">интерфейс ICommunicationListener Hello предоставляет три toomanage методы прослушиватель связи для службы:</span><span class="sxs-lookup"><span data-stu-id="933dc-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="933dc-169">*OpenAsync*</span><span class="sxs-lookup"><span data-stu-id="933dc-169">*OpenAsync*.</span></span> <span data-ttu-id="933dc-170">запуск прослушивания запросов.</span><span class="sxs-lookup"><span data-stu-id="933dc-170">Start listening for requests.</span></span>
* <span data-ttu-id="933dc-171">*CloseAsync*</span><span class="sxs-lookup"><span data-stu-id="933dc-171">*CloseAsync*.</span></span> <span data-ttu-id="933dc-172">остановка прослушивания запросов, завершение всех активных запросов и правильное завершение работы.</span><span class="sxs-lookup"><span data-stu-id="933dc-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="933dc-173">*Abort*</span><span class="sxs-lookup"><span data-stu-id="933dc-173">*Abort*.</span></span> <span data-ttu-id="933dc-174">отмена всех операций и немедленная остановка.</span><span class="sxs-lookup"><span data-stu-id="933dc-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="933dc-175">tooget к работе, добавьте закрытым членам класса, для прослушивателя hello действий потребуется toofunction.</span><span class="sxs-lookup"><span data-stu-id="933dc-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="933dc-176">Они будет инициализирована при помощи конструктора hello и использовать при настройке hello прослушивания URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="933dc-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="933dc-177">Реализация OpenAsync</span><span class="sxs-lookup"><span data-stu-id="933dc-177">Implement OpenAsync</span></span>
<span data-ttu-id="933dc-178">tooset копирование hello веб-сервера необходимы два блока данных:</span><span class="sxs-lookup"><span data-stu-id="933dc-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="933dc-179">*Префикс пути URL-адреса*.</span><span class="sxs-lookup"><span data-stu-id="933dc-179">*A URL path prefix*.</span></span> <span data-ttu-id="933dc-180">Хотя это необязательно, это хорошо подходит для вас tooset этого теперь вверх, чтобы безопасно размещать несколько веб-служб в приложении.</span><span class="sxs-lookup"><span data-stu-id="933dc-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="933dc-181">*Порт*.</span><span class="sxs-lookup"><span data-stu-id="933dc-181">*A port*.</span></span>

<span data-ttu-id="933dc-182">Прежде чем вы получить порт для веб-сервера hello, важно понимать, что Service Fabric предоставляет слой приложений, который служит буфером между приложением и hello базовой операционной системы, на котором работает.</span><span class="sxs-lookup"><span data-stu-id="933dc-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="933dc-183">Таким образом, Service Fabric предоставляет tooconfigure способом *конечные точки* для служб.</span><span class="sxs-lookup"><span data-stu-id="933dc-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="933dc-184">Service Fabric гарантирует, что конечные точки будут доступны для toouse вашей службы.</span><span class="sxs-lookup"><span data-stu-id="933dc-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="933dc-185">Таким образом, не имеют tooconfigure их самостоятельно в hello базовой среды операционной системы.</span><span class="sxs-lookup"><span data-stu-id="933dc-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="933dc-186">Можно легко размещать приложения Service Fabric в разных средах без необходимости toomake tooyour любого изменения приложения.</span><span class="sxs-lookup"><span data-stu-id="933dc-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="933dc-187">(Например, можно разместить hello одного приложения в Azure или в собственном центре обработки данных.)</span><span class="sxs-lookup"><span data-stu-id="933dc-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="933dc-188">Настройте конечную точку HTTP в файле PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="933dc-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="933dc-189">Этот шаг важен, так как выполняется хост-процесса службы hello ограниченными учетными данными (Network Service в Windows).</span><span class="sxs-lookup"><span data-stu-id="933dc-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="933dc-190">Это означает, что служба не будет иметь доступ tooset доступ к конечной точке HTTP сам по себе.</span><span class="sxs-lookup"><span data-stu-id="933dc-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="933dc-191">С помощью конфигурации конечной точки hello, Service Fabric знает tooset копирование hello правильный список управления доступом (ACL) для hello, который будет прослушивать URL-адрес, hello службы.</span><span class="sxs-lookup"><span data-stu-id="933dc-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="933dc-192">Service Fabric также предоставляет стандартный место tooconfigure конечных точек.</span><span class="sxs-lookup"><span data-stu-id="933dc-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="933dc-193">Теперь в OwinCommunicationListener.cs можно начать реализацию OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="933dc-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="933dc-194">Это связано с начала hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="933dc-194">This is where you start hello web server.</span></span> <span data-ttu-id="933dc-195">Во-первых получать сведения о конечных точках hello и создавать hello URL-адрес, который будет прослушивать служба hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="933dc-196">Hello URL-адрес будет различаться в зависимости от того, используется ли прослушиватель hello в службы без отслеживания состояния или службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="933dc-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="933dc-197">Для службы с отслеживанием состояния hello прослушивателю toocreate уникальный адрес для каждой реплики службы с отслеживанием состояния он прослушивает.</span><span class="sxs-lookup"><span data-stu-id="933dc-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="933dc-198">Для службы без сохранения состояния hello адрес может быть гораздо проще.</span><span class="sxs-lookup"><span data-stu-id="933dc-198">For stateless services, hello address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="933dc-199">Обратите внимание, что здесь используется адрес «http://+».</span><span class="sxs-lookup"><span data-stu-id="933dc-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="933dc-200">Это toomake том, что этот hello веб-сервер прослушивает все доступные адреса, включая localhost, полное доменное имя или IP-машины hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="933dc-201">Hello OpenAsync реализация является одной из важнейших причин hello почему hello веб-сервер (или любой стек связи) реализуется как ICommunicationListener, а не только его открытия непосредственно из `RunAsync()` в службе hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="933dc-202">Hello возвращает OpenAsync значение что прослушивает адрес hello, hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="933dc-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="933dc-203">При возвращении этот адрес toohello системы, он регистрирует адрес hello hello службе.</span><span class="sxs-lookup"><span data-stu-id="933dc-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="933dc-204">Service Fabric предоставляет API, который позволяет клиентам и других служб toothen запрашивает этот адрес по имени службы.</span><span class="sxs-lookup"><span data-stu-id="933dc-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="933dc-205">Это важно, потому что адресом службы hello не является статическим.</span><span class="sxs-lookup"><span data-stu-id="933dc-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="933dc-206">Службы будут перемещены в кластере hello в целях балансировки и доступности ресурсов.</span><span class="sxs-lookup"><span data-stu-id="933dc-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="933dc-207">Это механизм hello, которая позволяет клиентам tooresolve Здравствуй прослушивает адрес службы.</span><span class="sxs-lookup"><span data-stu-id="933dc-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="933dc-208">С учетом OpenAsync начинается hello веб-сервера и возвращает адрес hello, который он прослушивает.</span><span class="sxs-lookup"><span data-stu-id="933dc-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="933dc-209">Обратите внимание, прослушивает «http://+», но перед OpenAsync возвращает адрес hello, Здравствуйте, «+» заменяется hello IP-адрес или полное доменное имя hello узла, на котором она расположена в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="933dc-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="933dc-210">Hello адрес, который возвращается этим методом является то, что зарегистрирован в системе hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="933dc-211">Его увидят клиенты и другие службы при запросе адреса службы.</span><span class="sxs-lookup"><span data-stu-id="933dc-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="933dc-212">Для клиентов toocorrectly подключения tooit, они должны фактических IP-адрес или полное доменное имя в адрес hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="933dc-213">Обратите внимание, что это ссылается на класс запуска hello, который был передан в toohello OwinCommunicationListener в конструкторе hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="933dc-214">Этот экземпляр запуска используется hello web server toobootstrap hello приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="933dc-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="933dc-215">Hello `ServiceEventSource.Current.Message()` строке будет отображаться в окне событий диагностики hello позже, при запуске приложения tooconfirm hello hello веб-сервера успешно запущена.</span><span class="sxs-lookup"><span data-stu-id="933dc-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="933dc-216">Реализация CloseAsync и Abort</span><span class="sxs-lookup"><span data-stu-id="933dc-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="933dc-217">Наконец, реализации CloseAsync и Abort toostop hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="933dc-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="933dc-218">Hello веб-сервер может быть остановлена, удалив hello server дескриптор, который был создан во время OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="933dc-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="933dc-219">В этом примере реализация CloseAsync и Abort просто остановить hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="933dc-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="933dc-220">Вы можете отказаться от tooperform более легко скоординированного выключение hello веб-сервера в CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="933dc-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="933dc-221">Например hello завершение работы может ожидать завершилось, прежде чем вернуть hello toobe активных запросов.</span><span class="sxs-lookup"><span data-stu-id="933dc-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="933dc-222">Запустите веб-сервер hello</span><span class="sxs-lookup"><span data-stu-id="933dc-222">Start hello web server</span></span>
<span data-ttu-id="933dc-223">Теперь вы готовы toocreate и возвращать экземпляр OwinCommunicationListener toostart hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="933dc-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="933dc-224">Обратно в hello класс службы (WebService.cs), переопределите hello `CreateServiceInstanceListeners()` метод:</span><span class="sxs-lookup"><span data-stu-id="933dc-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="933dc-225">Это где hello веб-API *приложения* и hello OWIN *узла* наконец соответствуют.</span><span class="sxs-lookup"><span data-stu-id="933dc-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="933dc-226">Получает экземпляр hello Hello узла (OwinCommunicationListener) *приложения* (веб-API) через hello класс запуска.</span><span class="sxs-lookup"><span data-stu-id="933dc-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="933dc-227">Его жизненным циклом управляет Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="933dc-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="933dc-228">Такого же шаблона можно придерживаться при использовании любого стека связи.</span><span class="sxs-lookup"><span data-stu-id="933dc-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="933dc-229">Сборка</span><span class="sxs-lookup"><span data-stu-id="933dc-229">Put it all together</span></span>
<span data-ttu-id="933dc-230">В этом примере не требуется toodo что-либо в hello `RunAsync()` метода, так что переопределение просто может быть удалено.</span><span class="sxs-lookup"><span data-stu-id="933dc-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="933dc-231">Реализация Hello окончательного службы должны быть очень простыми.</span><span class="sxs-lookup"><span data-stu-id="933dc-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="933dc-232">Требуется только toocreate hello связи прослушиватель:</span><span class="sxs-lookup"><span data-stu-id="933dc-232">It only needs toocreate hello communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="933dc-233">Полный Hello `OwinCommunicationListener` класса:</span><span class="sxs-lookup"><span data-stu-id="933dc-233">hello complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="933dc-234">Теперь, когда все составляющие hello поместил в месте, проекта должен выглядеть типичное приложение веб-API с узлом OWIN и надежные API служб точки входа.</span><span class="sxs-lookup"><span data-stu-id="933dc-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="933dc-235">Запуск и подключение через веб-браузер</span><span class="sxs-lookup"><span data-stu-id="933dc-235">Run and connect through a web browser</span></span>
<span data-ttu-id="933dc-236">Если это еще не сделано, [настройте среду разработки](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="933dc-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="933dc-237">Теперь можно построить и развернуть службу.</span><span class="sxs-lookup"><span data-stu-id="933dc-237">You can now build and deploy your service.</span></span> <span data-ttu-id="933dc-238">Нажмите клавишу **F5** в toobuild Visual Studio и развертывать приложение hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="933dc-239">В окне приветствия события диагностики, вы увидите сообщение, указывающее, открыт на http://localhost:8281 веб-сервера hello /.</span><span class="sxs-lookup"><span data-stu-id="933dc-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="933dc-240">Если hello порт уже открыт другим процессом на компьютере, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="933dc-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="933dc-241">Это означает, что не удалось открыть прослушиватель hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="933dc-242">Если это так hello, попробуйте использовать другой порт для hello конфигурации конечной точки в файле ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="933dc-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="933dc-243">После установки службы hello, откройте браузер и перейдите в слишком[http://localhost:8281, значения или api](http://localhost:8281/api/values) tootest его.</span><span class="sxs-lookup"><span data-stu-id="933dc-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="933dc-244">Масштабирование</span><span class="sxs-lookup"><span data-stu-id="933dc-244">Scale it out</span></span>
<span data-ttu-id="933dc-245">Горизонтальное масштабирование без сохранения состояния веб-приложений обычно означает добавление нескольких компьютеров и скорость hello веб-приложений на них вращения.</span><span class="sxs-lookup"><span data-stu-id="933dc-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="933dc-246">Service Fabric orchestration engine это можно сделать для вас при каждом добавлении новых узлов кластера tooa.</span><span class="sxs-lookup"><span data-stu-id="933dc-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="933dc-247">При создании экземпляров службы без сохранения состояния, можно указать номер hello экземпляров требуется toocreate.</span><span class="sxs-lookup"><span data-stu-id="933dc-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="933dc-248">Service Fabric помещает соответствующее количество экземпляров на узлах в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="933dc-249">И он проверяет toocreate не более одного экземпляра на любом узле.</span><span class="sxs-lookup"><span data-stu-id="933dc-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="933dc-250">Можно также указать tooalways Service Fabric создавать экземпляры на каждом узле, указав **-1** по количеству экземпляров hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="933dc-251">Это гарантирует, что при каждом добавлении tooscale узлы из кластера экземпляра без сохранения состояния службы создается на новых узлах hello.</span><span class="sxs-lookup"><span data-stu-id="933dc-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="933dc-252">Это значение является свойством экземпляра службы hello, поэтому оно задается при создании экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="933dc-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="933dc-253">Его можно задать с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="933dc-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="933dc-254">Его также можно задать при определении службы по умолчанию в проекте службы без отслеживания состояния в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="933dc-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="933dc-255">Дополнительные сведения о статье toocreate приложений и экземпляров службы [развернуть приложение](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="933dc-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="933dc-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="933dc-256">Next steps</span></span>
[<span data-ttu-id="933dc-257">Отладка приложения Service Fabric с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="933dc-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

