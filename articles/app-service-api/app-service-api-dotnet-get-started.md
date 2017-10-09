---
title: "aaaGet к работе с API приложений и ASP.NET в службе приложений | Документы Microsoft"
description: "Узнайте, как toocreate, развертывать и использовать приложения ASP.NET API в службе приложений Azure, с помощью Visual Studio 2015."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="5ed4e-103">Приступая к работе с приложениями API, ASP.NET и Swagger в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="5ed4e-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="5ed4e-104">— Hello сначала ряд учебники, которые показывают, как службы toouse возможности приложения Azure, полезны при разработке и хост-API RESTful.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-104">This is hello first in a series of tutorials that show how toouse features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="5ed4e-105">В этом руководстве рассматривается обеспечение поддержки метаданных API в формате Swagger.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="5ed4e-106">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="5ed4e-106">You'll learn:</span></span>

* <span data-ttu-id="5ed4e-107">Как toocreate и развернуть [приложения API](app-service-api-apps-why-best-platform.md) в службе приложений Azure с помощью средств, встроенных в Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-107">How toocreate and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="5ed4e-108">Как пакет Swashbuckle NuGet tooautomate API обнаружения с помощью hello toodynamically создания Swagger API метаданных.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-108">How tooautomate API discovery by using hello Swashbuckle NuGet package toodynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="5ed4e-109">Как tooautomatically метаданных Swagger API toouse создания кода клиента для приложения API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-109">How toouse Swagger API metadata tooautomatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="5ed4e-110">Обзор примеров приложений</span><span class="sxs-lookup"><span data-stu-id="5ed4e-110">Sample application overview</span></span>
<span data-ttu-id="5ed4e-111">В этом руководстве вы будете работать с простым примером приложения списка дел.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="5ed4e-112">приложение Hello имеет интерфейсную одностраничного приложения (SPA), средний уровень веб-API ASP.NET и веб-API ASP.NET уровня данных.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-112">hello application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Схема примера приложения приложений API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="5ed4e-114">Ниже приведен снимок экрана приветствия [AngularJS](https://angularjs.org/) переднего плана.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-114">Here's a screen shot of hello [AngularJS](https://angularjs.org/) front end.</span></span>

![API образец приложения toodo список приложений](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="5ed4e-116">Hello решения Visual Studio включает в себя три проекта:</span><span class="sxs-lookup"><span data-stu-id="5ed4e-116">hello Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="5ed4e-117">**ToDoListAngular** -hello переднего плана: SPA AngularJS, который вызывает hello среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-117">**ToDoListAngular** - hello front end: an AngularJS SPA that calls hello middle tier.</span></span>
* <span data-ttu-id="5ed4e-118">**ToDoListAPI** -hello среднего уровня: это проект веб-API ASP.NET, который вызывает hello уровень данных операции CRUD tooperform заданий для выполнения.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-118">**ToDoListAPI** - hello middle tier: an ASP.NET Web API project that calls hello data tier tooperform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="5ed4e-119">**ToDoListDataAPI** -уровень данных hello: проект веб-API ASP.NET, выполняющей заданий для выполнения операций CRUD.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-119">**ToDoListDataAPI** - hello data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="5ed4e-120">Трехуровневая архитектура Hello является одним из многих архитектур, которые можно реализовать с помощью API приложения и используется только для демонстрационных целей.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-120">hello three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="5ed4e-121">Hello код на каждом уровне сводится функций API приложений возможных toodemonstrate; Например уровень данных hello использует памяти сервера, а не базы данных как механизма сохраняемости.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-121">hello code in each tier is as simple as possible toodemonstrate API Apps features; for example, hello data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="5ed4e-122">После завершения этого учебника, вы получите два проекта веб-API hello вверх и запуск в облаке hello в приложение API службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-122">On completing this tutorial, you'll have hello two Web API projects up and running in hello cloud in App Service API apps.</span></span>

<span data-ttu-id="5ed4e-123">Далее учебнике Hello серии hello развертывает hello SPA внешнего интерфейса toohello облака.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-123">hello next tutorial in hello series deploys hello SPA front end toohello cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ed4e-124">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ed4e-124">Prerequisites</span></span>
* <span data-ttu-id="5ed4e-125">Веб-API ASP.NET - hello учебника инструкции предполагают, у вас есть базовых знаний о том, как toowork с ASP.NET [веб-API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-125">ASP.NET Web API - hello tutorial instructions assume you have a basic knowledge of how toowork with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="5ed4e-126">Учетная запись Azure. [Создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="5ed4e-127">Tooget к работе со службой приложения Azure, прежде чем выполнить вход для учетной записи Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-127">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="5ed4e-128">Там можно быстро создать кратковременное приложение начального уровня в службе приложений. Это не потребует **ни кредитной карты**, ни каких-либо обязательств.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="5ed4e-129">Visual Studio 2015 с hello [Azure SDK для .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK устанавливает Visual Studio 2015 автоматически, если вы его еще нет.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-129">Visual Studio 2015 with hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - hello SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="5ed4e-130">В Visual Studio щелкните "Справка -> О Microsoft Visual Studio" и убедитесь, что у вас установлены средства службы приложений Azure версии 2.9.1 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Версия средств приложений Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="5ed4e-132">В зависимости от того, сколько зависимостей SDK hello уже имеется на компьютере установка hello SDK может занять много времени, от нескольких минут tooa полчаса или несколько.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-132">Depending on how many of hello SDK dependencies you already have on your machine, installing hello SDK could take a long time, from several minutes tooa half hour or more.</span></span>
    > 
    > 

## <a name="download-hello-sample-application"></a><span data-ttu-id="5ed4e-133">Загрузите пример приложения hello</span><span class="sxs-lookup"><span data-stu-id="5ed4e-133">Download hello sample application</span></span>
1. <span data-ttu-id="5ed4e-134">Загрузите hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) репозитория.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-134">Download hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="5ed4e-135">Можно щелкнуть hello **загрузить ZIP** кнопки или клонирования репозитория hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-135">You can click hello **Download ZIP** button or clone hello repository on your local machine.</span></span>
2. <span data-ttu-id="5ed4e-136">Откройте решение ToDoList hello в Visual Studio 2015 или 2013.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-136">Open hello ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="5ed4e-137">Вам потребуется tootrust каждого решения.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-137">You will need tootrust each solution.</span></span>
         <span data-ttu-id="5ed4e-138">![Предупреждение системы безопасности](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="5ed4e-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="5ed4e-139">Построение решений (CTRL + SHIFT + B) toorestore hello hello-пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-139">Build hello solution (CTRL + SHIFT + B)  toorestore hello NuGet packages.</span></span>
   
    <span data-ttu-id="5ed4e-140">Перед развертыванием следует toosee приложения hello в операции можно выполнять локально.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-140">If you want toosee hello application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="5ed4e-141">Убедитесь, что ToDoListDataAPI запускаемого проекта и решения выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-141">Make sure that ToDoListDataAPI is your startup project and run hello solution.</span></span> <span data-ttu-id="5ed4e-142">Ошибки HTTP 403 toosee следует ожидать в браузере.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-142">You should expect toosee a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="5ed4e-143">Использование метаданных и пользовательского интерфейса API Swagger</span><span class="sxs-lookup"><span data-stu-id="5ed4e-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="5ed4e-144">Поддержка метаданных API [Swagger 2.0](http://swagger.io/) встроена в службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="5ed4e-145">Каждое приложение API можно указать URL-адрес конечной точки, которая возвращает метаданные для hello API в формате Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-145">Each API app can specify a URL endpoint that returns metadata for hello API in Swagger JSON format.</span></span> <span data-ttu-id="5ed4e-146">Hello метаданные, возвращенные этой конечной точки можно использовать toogenerate клиентский код.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-146">hello metadata returned from that endpoint can be used toogenerate client code.</span></span>

<span data-ttu-id="5ed4e-147">Проект веб-API ASP.NET можно создать динамически метаданных Swagger с помощью hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="5ed4e-148">в проектах ToDoListDataAPI и ToDoListAPI hello, которые загружаются Hello пакет Swashbuckle NuGet уже установлена.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-148">hello Swashbuckle NuGet package is already installed in hello ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="5ed4e-149">В этом разделе учебника hello просмотрите созданные hello метаданных Swagger 2.0, и повторите тестирования пользовательского интерфейса, основанный на метаданных Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-149">In this section of hello tutorial, you look at hello generated Swagger 2.0 metadata, and then you try out a test UI that is based on hello Swagger metadata.</span></span>

1. <span data-ttu-id="5ed4e-150">Установите проект ToDoListDataAPI hello (**не** проекта ToDoListAPI hello) hello запускаемым проектом.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-150">Set hello ToDoListDataAPI project (**not** hello ToDoListAPI project) as hello startup project.</span></span>
   
    ![Назначить ToDoDataAPI в качестве запускаемого проекта](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="5ed4e-152">Нажмите клавишу F5 или выберите **Отладка > Начать отладку** toorun hello проекта в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-152">Press F5 or click **Debug > Start Debugging** toorun hello project in debug mode.</span></span>
   
    <span data-ttu-id="5ed4e-153">Hello браузера открывается и отображается страница ошибки HTTP 403 hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-153">hello browser opens and shows hello HTTP 403 error page.</span></span>
3. <span data-ttu-id="5ed4e-154">В адресной строки браузера, добавьте `swagger/docs/v1` toohello конец строки hello и нажмите клавишу Return.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-154">In your browser address bar, add `swagger/docs/v1` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="5ed4e-155">(URL-адрес является hello `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="5ed4e-155">(hello URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="5ed4e-156">Это значение по умолчанию hello URL-адрес, используемый метаданных Swagger 2.0 JSON tooreturn Swashbuckle для hello API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-156">This is hello default URL used by Swashbuckle tooreturn Swagger 2.0 JSON metadata for hello API.</span></span>
   
    <span data-ttu-id="5ed4e-157">При использовании Internet Explorer hello браузер предложит toodownload *v1.json* файла.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-157">If you're using Internet Explorer, hello browser prompts you toodownload a *v1.json* file.</span></span>
   
    ![Скачивание метаданных JSON в Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="5ed4e-159">При использовании Chrome, Firefox или край hello браузер отображает hello JSON в окне браузера hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-159">If you're using Chrome, Firefox, or Edge, hello browser displays hello JSON in hello browser window.</span></span> <span data-ttu-id="5ed4e-160">По-разному обрабатывать JSON в различных браузерах и окна браузера может выглядеть так же, как и пример hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-160">Different browsers handle JSON differently, and your browser window may not look exactly like hello example.</span></span>
   
    ![Метаданные JSON в Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="5ed4e-162">Hello ниже приведен пример hello первый раздел метаданных Swagger hello для hello API, с определением hello для hello метод Get.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-162">hello following sample shows hello first section of hello Swagger metadata for hello API, with hello definition for hello Get method.</span></span> <span data-ttu-id="5ed4e-163">Эти метаданные являются, какие диски hello Swagger пользовательского интерфейса, используйте в hello, выполнив действия, которое используется в следующем разделе учебника tooautomatically hello создания кода клиента.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-163">This metadata is what drives hello Swagger UI that you use in hello following steps, and you use it in a later section of hello tutorial tooautomatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="5ed4e-164">Закройте браузер hello и остановка отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-164">Close hello browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="5ed4e-165">В hello ToDoListDataAPI проектов в **обозревателе решений**откройте hello *App_Start\SwaggerConfig.cs* файла, а затем прокрутите список вниз tooline 174 и раскомментируйте следующий код hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-165">In hello ToDoListDataAPI project in **Solution Explorer**, open hello *App_Start\SwaggerConfig.cs* file, then scroll down tooline 174 and uncomment hello following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="5ed4e-166">Hello *SwaggerConfig.cs* файл создается при установке пакета Swashbuckle hello в проекте.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-166">hello *SwaggerConfig.cs* file is created when you install hello Swashbuckle package in a project.</span></span> <span data-ttu-id="5ed4e-167">файл Hello предоставляет ряд способов tooconfigure Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-167">hello file provides a number of ways tooconfigure Swashbuckle.</span></span>
   
    <span data-ttu-id="5ed4e-168">Hello код Раскомментировать приветствия включает Swagger пользовательского интерфейса, используемого в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-168">hello code you've uncommented enables hello Swagger UI that you use in hello following steps.</span></span> <span data-ttu-id="5ed4e-169">При создании проекта веб-API с помощью шаблона проекта приложения hello API, этот код закомментирована по умолчанию в качестве меры безопасности.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-169">When you create a Web API project by using hello API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="5ed4e-170">Снова запустите проект hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-170">Run hello project again.</span></span>
7. <span data-ttu-id="5ed4e-171">В адресной строки браузера, добавьте `swagger` toohello конец строки hello и нажмите клавишу Return.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-171">In your browser address bar, add `swagger` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="5ed4e-172">(URL-адрес является hello `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5ed4e-172">(hello URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="5ed4e-173">Когда откроется страница приветствия Swagger пользовательского интерфейса, нажмите кнопку **ToDoList** toosee hello доступные методы.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-173">When hello Swagger UI page appears, click **ToDoList** toosee hello methods available.</span></span>
   
    ![Пользовательский интерфейс Swagger — доступные методы](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="5ed4e-175">Сначала щелкните hello **получить** кнопку в списке hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-175">Click hello first **Get** button in hello list.</span></span>
10. <span data-ttu-id="5ed4e-176">В hello **параметры** введите звездочку в качестве значения hello hello `owner` параметр и нажмите кнопку **попробуйте**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-176">In hello **Parameters** section, enter an asterisk as hello value of hello `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="5ed4e-177">При добавлении проверки подлинности на следующих занятиях рассматривается среднего уровня hello предоставит уровень hello действительного пользовательского идентификатора toohello данных.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-177">When you add authentication in later tutorials, hello middle tier will provide hello actual user ID toohello data tier.</span></span> <span data-ttu-id="5ed4e-178">Пока все задачи имеют звездочку как их идентификатор владельца во время выполнения приложения hello не включена проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-178">For now, all tasks will have asterisk as their owner ID while hello application runs without authentication enabled.</span></span>
    
    ![Пользовательский интерфейс Swagger — кнопка Try it out](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="5ed4e-180">Hello Swagger пользовательского интерфейса вызывает метод ToDoList Get hello и отображает код ответа hello и результаты JSON.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-180">hello Swagger UI calls hello ToDoList Get method and displays hello response code and JSON results.</span></span>
    
    ![Пользовательский интерфейс Swagger — результаты нажатия кнопки Try it out](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="5ed4e-182">Нажмите кнопку **Post**и щелкните поле hello **схему модели**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-182">Click **Post**, and then click hello box under **Model Schema**.</span></span>
    
    <span data-ttu-id="5ed4e-183">Щелкнув hello модели схемы prefills hello поле ввода где можно указать значение параметра hello hello метода Post.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-183">Clicking hello model schema prefills hello input box where you can specify hello parameter value for hello Post method.</span></span> <span data-ttu-id="5ed4e-184">(Если это не сработает в Internet Explorer, используйте другой браузер или вручную ввести значение параметра hello в hello следующий шаг).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-184">(If this doesn't work in Internet Explorer, use a different browser or enter hello parameter value manually in hello next step.)</span></span>  
    
    ![Пользовательский интерфейс Swagger — нажатие кнопки Try it out при выборе метода Post](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="5ed4e-186">Изменение hello JSON в hello `todo` входной параметр, чтобы он выглядит как следующий пример hello или замените текст описания:</span><span class="sxs-lookup"><span data-stu-id="5ed4e-186">Change hello JSON in hello `todo` parameter input box so that it looks like hello following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="5ed4e-187">Щелкните **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="5ed4e-188">Hello ToDoList API возвращает код ответа HTTP 204 означает успешное выполнение.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-188">hello ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="5ed4e-189">Сначала щелкните hello **получить** , а затем в этом разделе страницы приветствия нажмите hello **попробуйте** кнопки.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-189">Click hello first **Get** button, and then in that section of hello page click hello **Try it out** button.</span></span>
    
    <span data-ttu-id="5ed4e-190">метод ответа на получение Hello теперь включает новый элемент toodo hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-190">hello Get method response now includes hello new toodo item.</span></span>
15. <span data-ttu-id="5ed4e-191">Необязательно: Hello Put, Delete, попробуйте также и получить идентификатор методами.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-191">Optional: Try also hello Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="5ed4e-192">Закройте браузер hello и остановка отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-192">Close hello browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="5ed4e-193">Swashbuckle можно использовать с любыми проектами веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="5ed4e-194">Если вы хотите tooadd Swagger метаданных поколения tooan существующий проект, просто установите hello Swashbuckle пакета.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-194">If you want tooadd Swagger metadata generation tooan existing project, just install hello Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="5ed4e-195">В метаданных Swagger есть уникальный идентификатор для каждой операции API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="5ed4e-196">По умолчанию пакет Swashbuckle может создавать дублирующиеся идентификаторы операций Swagger для методов контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="5ed4e-197">Это происходит, если перегружены методы HTTP контроллера, например `Get()` и `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="5ed4e-198">Сведения о как overloads toohandle разделе [определения интерфейсов API настройки Swashbuckle создан](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-198">For information about how toohandle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="5ed4e-199">При создании проекта веб-API в Visual Studio с помощью шаблона приложения API Azure hello toohello автоматически добавляется код, который приводит к возникновению ошибки операции уникальные идентификаторы *SwaggerConfig.cs* файла.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-199">If you create a Web API project in Visual Studio by using hello Azure API App template, code that generates unique operation IDs is automatically added toohello *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="5ed4e-200"><a id="createapiapp"></a>Создание приложения API в Azure и развертывание кода tooit</span><span class="sxs-lookup"><span data-stu-id="5ed4e-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code tooit</span></span>
<span data-ttu-id="5ed4e-201">В этом разделе, используйте инструменты Azure, интегрированные в Visual Studio hello **веб-публикация** мастер toocreate новый API приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-201">In this section, you use Azure tools that are integrated into hello Visual Studio **Publish Web** wizard toocreate a new API app in Azure.</span></span> <span data-ttu-id="5ed4e-202">Затем развертывание ToDoListDataAPI проекта toohello новый API приложение hello и вызвать hello API, запустив hello Swagger пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-202">Then you deploy hello ToDoListDataAPI project toohello new API app and call hello API by running hello Swagger UI.</span></span>

1. <span data-ttu-id="5ed4e-203">В **обозревателе решений**, щелкните правой кнопкой мыши проект ToDoListDataAPI hello и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-203">In **Solution Explorer**, right-click hello ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Нажмите кнопку "Опубликовать" в Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="5ed4e-205">В hello **профиль** шага hello **веб-публикация** мастера, нажмите кнопку **службу приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-205">In hello **Profile** step of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Выберите "Служба приложений Azure" в мастере веб-публикации](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="5ed4e-207">Вход tooyour учетная запись Azure, если вы еще не выполнена или обновите учетные данные, если вы истечении срока.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-207">Sign in tooyour Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="5ed4e-208">В диалоговое окно службы приложения hello, выберите hello Azure **подписки** toouse и нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-208">In hello App Service dialog box, choose hello Azure **Subscription** you want toouse, and then click **New**.</span></span>
   
    ![Нажмите кнопку "Создать" в диалоговом окне службы приложений](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="5ed4e-210">Hello **размещения** вкладка hello **Создание приложения службы** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-210">hello **Hosting** tab of hello **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="5ed4e-211">Так как вы развертываете проект веб-API, который содержит Swashbuckle установлена, Visual Studio подразумевает toocreate приложения API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want toocreate an API App.</span></span> <span data-ttu-id="5ed4e-212">Это обозначается hello **имя приложения API** title и по hello фактов, hello **изменение типа** раскрывающегося списка задано слишком**приложения API**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-212">This is indicated by hello **API App Name** title and by hello fact that hello **Change Type** drop-down list is set too**API App**.</span></span>
   
    ![Тип приложения в диалоговом окне службы приложений](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="5ed4e-214">Введите **имя приложения API** является уникальным в hello *azurewebsites.net* домена.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-214">Enter an **API App Name** that is unique in hello *azurewebsites.net* domain.</span></span> <span data-ttu-id="5ed4e-215">Можно принять имя по умолчанию hello, предлагаемых программой Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-215">You can accept hello default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="5ed4e-216">Если ввести имя, которое уже использован другим пользователем, можно увидеть право toohello красный восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-216">If you enter a name that someone else has already used, you see a red exclamation mark toohello right.</span></span>
   
    <span data-ttu-id="5ed4e-217">Hello URL-адрес приложения hello API будет `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-217">hello URL of hello API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="5ed4e-218">В hello **группы ресурсов** раскрывающийся список, щелкните **New**, а затем введите «ToDoListGroup» или другое имя, если вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-218">In hello **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="5ed4e-219">Группы ресурсов — это совокупность ресурсов Azure, таких как приложения API, базы данных, виртуальные машины и т. д.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="5ed4e-220">В этом учебнике это лучший toocreate новую группу ресурсов, так как это позволяет легко toodelete за один шаг, все hello Azure ресурсов, созданных для учебника hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-220">For this tutorial, it's best toocreate a new resource group because that makes it easy toodelete in one step all hello Azure resources that you create for hello tutorial.</span></span>
   
    <span data-ttu-id="5ed4e-221">В этом поле можно выбрать существующую [группу ресурсов](../azure-resource-manager/resource-group-overview.md) или создать отдельную, введя имя, которое отличается от имени любой существующей группы ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="5ed4e-222">Нажмите кнопку hello **New** кнопку Далее toohello **план служб приложений** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-222">Click hello **New** button next toohello **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="5ed4e-223">Hello снимке экрана показаны примеры значений **имя приложения API**, **подписки**, и **группы ресурсов** --значения будут отличаться.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-223">hello screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Диалоговое окно "Создание службы приложений"](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="5ed4e-225">В следующие шаги hello создается план служб приложений для новой группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-225">In hello following steps you create an App Service plan for hello new resource group.</span></span> <span data-ttu-id="5ed4e-226">План служб приложений указывает hello вычислительные ресурсы, которые ваше приложение API запускается.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-226">An App Service plan specifies hello compute resources that your API app runs on.</span></span> <span data-ttu-id="5ed4e-227">Например при выборе hello бесплатный уровень API приложения выполняется на общих виртуальных машин, выполняющегося на выделенных виртуальных машин для некоторых платных уровней.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-227">For example, if you choose hello free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="5ed4e-228">Дополнительные сведения см. в статье [Подробный обзор планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="5ed4e-229">В hello **настроить план служб приложений** диалоговое окно, введите «ToDoListPlan» или другое имя, если вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-229">In hello **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="5ed4e-230">В hello **расположение** раскрывающегося списка выберите ближайший tooyou расположение hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-230">In hello **Location** drop-down list, choose hello location that is closest tooyou.</span></span>
   
    <span data-ttu-id="5ed4e-231">Этот параметр определяет, в каком центре обработки данных Azure будет выполняться приложение.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="5ed4e-232">Выберите расположение закрыть tooyou toominimize [задержки](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-232">Choose a location close tooyou toominimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="5ed4e-233">В hello **размер** раскрывающийся список, щелкните **Free**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-233">In hello **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="5ed4e-234">В этом учебнике hello бесплатной ценовой категории предоставит достаточно производительности.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-234">For this tutorial, hello free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="5ed4e-235">В hello **настроить план служб приложений** диалоговое окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-235">In hello **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Нажмите кнопку "ОК" в диалоговом окне "Настройка плана службы приложений"](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="5ed4e-237">В hello **Создание приложения службы** диалоговое окно, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-237">In hello **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Нажмите кнопку "Создать" в диалоговом окне"Создание службы приложений"](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="5ed4e-239">Visual Studio создает приложение hello API и профиль публикации, которая имеет все hello необходимые параметры для приложения hello API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-239">Visual Studio creates hello API app and a publish profile that has all of hello required settings for hello API app.</span></span> <span data-ttu-id="5ed4e-240">Затем он открывает hello **веб-публикация** мастер, который будет использоваться toodeploy hello проекта.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-240">Then it opens hello **Publish Web** wizard, which you'll use toodeploy hello project.</span></span>
    
    <span data-ttu-id="5ed4e-241">Hello **веб-публикация** откроется мастер на hello **подключения** вкладка (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-241">hello **Publish Web** wizard opens on hello **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="5ed4e-242">На hello **подключения** вкладке hello **сервера** и **имя сайта** параметры приложения API tooyour точки.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-242">On hello **Connection** tab, hello **Server** and **Site name** settings point tooyour API app.</span></span> <span data-ttu-id="5ed4e-243">Hello **имя пользователя** и **пароль** учетные данные развертывания, которые создает Azure.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-243">hello **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="5ed4e-244">После развертывания Visual Studio открывает toohello браузера **URL-адрес назначения** (это hello единственной целью **URL-адрес назначения**).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-244">After deployment, Visual Studio opens a browser toohello **Destination URL** (that's hello only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="5ed4e-245">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-245">Click **Next**.</span></span>
    
    ![Нажмите кнопку "Далее" на вкладке "Подключение" мастера веб-публикации](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="5ed4e-247">Следующая вкладка Hello — hello **параметры** вкладке (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-247">hello next tab is hello **Settings** tab (shown below).</span></span> <span data-ttu-id="5ed4e-248">Здесь можно изменить toodeploy вкладка конфигурации сборки hello отладочного построения [удаленной отладки](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-248">Here you can change hello build configuration tab toodeploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="5ed4e-249">Hello вкладка также предлагает несколько вариантов **параметры публикации файлов**:</span><span class="sxs-lookup"><span data-stu-id="5ed4e-249">hello tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="5ed4e-250">"Удалить дополнительные файлы в месте назначения";</span><span class="sxs-lookup"><span data-stu-id="5ed4e-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="5ed4e-251">"Предварительно компилировать при публикации";</span><span class="sxs-lookup"><span data-stu-id="5ed4e-251">Precompile during publishing</span></span>
    * <span data-ttu-id="5ed4e-252">Исключить файлы из папки App_Data hello</span><span class="sxs-lookup"><span data-stu-id="5ed4e-252">Exclude files from hello App_Data folder</span></span>
    
    <span data-ttu-id="5ed4e-253">В данном руководстве эти параметры не используются.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="5ed4e-254">Подробное описание этих параметров см. в статье [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) (Развертывание веб-проекта с помощью публикации одним щелчком в Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="5ed4e-255">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-255">Click **Next**.</span></span>
    
    ![Нажмите кнопку "Далее" на вкладке "Параметры" мастера веб-публикации](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="5ed4e-257">Далее следует hello **предварительного просмотра** вкладки (показано ниже), предоставляющей возможности toosee, какие файлы будут скопированы из проекта приложения toohello API toobe.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-257">Next is hello **Preview** tab (shown below), which gives you an opportunity toosee what files are going toobe copied from your project toohello API app.</span></span> <span data-ttu-id="5ed4e-258">При развертывании приложения tooan API проекта, уже развернут tooearlier копируются только измененные файлы.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-258">When you're deploying a project tooan API app that you already deployed tooearlier, only changed files are copied.</span></span> <span data-ttu-id="5ed4e-259">Если требуется toosee список какие будут скопированы, можно щелкнуть hello **начать просмотр** кнопки.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-259">If you want toosee a list of what will be copied, you can click hello **Start Preview** button.</span></span>
15. <span data-ttu-id="5ed4e-260">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-260">Click **Publish**.</span></span>
    
    ![Нажмите кнопку "Опубликовать" на вкладке "Предварительный просмотр" мастера веб-публикации](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="5ed4e-262">Visual Studio развертывает hello ToDoListDataAPI проекта toohello нового приложения API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-262">Visual Studio deploys hello ToDoListDataAPI project toohello new API app.</span></span> <span data-ttu-id="5ed4e-263">Hello **вывода** окно входит успешному развертыванию, и в URL-toohello открытое окно браузера приложение hello API появится страница «создан».</span><span class="sxs-lookup"><span data-stu-id="5ed4e-263">hello **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened toohello URL of hello API app.</span></span>
    
    ![Окно вывода с информацией об успешном развертывании](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Страница "Приложение API успешно создано"](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="5ed4e-266">Добавить URL-адрес toohello «swagger» в адресной строке браузера hello и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-266">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="5ed4e-267">(URL-адрес является hello `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5ed4e-267">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="5ed4e-268">Hello браузер отображает hello же Swagger пользовательский Интерфейс, который вы видели ранее, но теперь он работает в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-268">hello browser displays hello same Swagger UI that you saw earlier, but now it's running in hello cloud.</span></span> <span data-ttu-id="5ed4e-269">Опробуйте hello метод Get и вы увидите, что вы будете toohello назад по умолчанию 2 заданий для выполнения.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-269">Try out hello Get method, and you see that you're back toohello default 2 to-do items.</span></span> <span data-ttu-id="5ed4e-270">Hello изменения, сделанные ранее были сохранены в памяти на локальном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-270">hello changes you made earlier were saved in memory in hello local machine.</span></span>
17. <span data-ttu-id="5ed4e-271">Откройте hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-271">Open hello [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="5ed4e-272">Hello портал Azure является веб-интерфейс для управления ресурсами Azure, таких как приложения API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-272">hello Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="5ed4e-273">Щелкните **Больше служб > Службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-273">Click **More Services > App Services**.</span></span>
    
    ![Обзор служб приложений](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="5ed4e-275">В hello **службы приложений** колонки, найдите и выберите новый API приложения.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-275">In hello **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="5ed4e-276">(В hello портал Azure, называются окнах, открывающихся справа toohello *колонок*.)</span><span class="sxs-lookup"><span data-stu-id="5ed4e-276">(In hello Azure portal, windows that open toohello right are called *blades*.)</span></span>
    
    ![Колонка "Службы приложений"](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="5ed4e-278">Откроются две колонки:</span><span class="sxs-lookup"><span data-stu-id="5ed4e-278">Two blades open.</span></span> <span data-ttu-id="5ed4e-279">Обзор API приложение hello имеет один колонки и один длинный список параметров, которые можно просматривать и изменять.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-279">One blade has an overview of hello API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="5ed4e-280">В hello **параметры** колонки, найти hello **API** и нажмите кнопку **определения API**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-280">In hello **Settings** blade, find hello **API** section and click **API Definition**.</span></span>
    
    ![Определение API в колонке "Параметры"](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="5ed4e-282">Hello **определения API** колонке позволяет указать URL-адрес hello, возвращающий метаданные Swagger 2.0 в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-282">hello **API Definition** blade lets you specify hello URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="5ed4e-283">Когда Visual Studio создает приложение hello API, задает значение по умолчанию toohello URL-адрес определения hello API для созданных Swashbuckle метаданные, вы уже видели раньше, приложение hello API базовый URL-адрес плюс `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-283">When Visual Studio creates hello API app, it sets hello API definition URL toohello default value for Swashbuckle-generated metadata that you saw earlier, which is hello API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL-адрес определения API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="5ed4e-285">При выборе кода клиента toogenerate приложения API для него Visual Studio извлекает метаданные hello из этого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-285">When you select an API app toogenerate client code for it, Visual Studio retrieves hello metadata from this URL.</span></span>

## <span data-ttu-id="5ed4e-286"><a id="codegen"></a>Создание клиентского кода для hello уровня данных</span><span class="sxs-lookup"><span data-stu-id="5ed4e-286"><a id="codegen"></a> Generate client code for hello data tier</span></span>
<span data-ttu-id="5ed4e-287">Одним из преимуществ hello интеграцию Swagger в приложения Azure API является автоматическое создание кода.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-287">One of hello advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="5ed4e-288">Созданные классы клиентских стала проще toowrite код, который вызывает приложение API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-288">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="5ed4e-289">Hello ToDoListAPI проект уже содержит hello созданный код клиента, но в hello, выполнив действия будет удалить его и создать его заново, как создание кода toodo hello toosee.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-289">hello ToDoListAPI project already has hello generated client code, but in hello following steps you'll delete it and regenerate it toosee how toodo hello code generation.</span></span>

1. <span data-ttu-id="5ed4e-290">В Visual Studio **обозревателе решений**, в hello ToDoListAPI проектов, удалите hello *ToDoListDataAPI* папки.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-290">In Visual Studio **Solution Explorer**, in hello ToDoListAPI project, delete hello *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="5ed4e-291">**Предупреждение: Удалите только hello папки, не hello ToDoListDataAPI проекта.**</span><span class="sxs-lookup"><span data-stu-id="5ed4e-291">**Caution: Delete only hello folder, not hello ToDoListDataAPI project.**</span></span>
   
    ![Удаление кода, созданного клиентом](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="5ed4e-293">Эта папка была создана с помощью процесса создания кода hello, скоро будет toogo через.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-293">This folder was created by using hello code generation process that you're about toogo through.</span></span>
2. <span data-ttu-id="5ed4e-294">Щелкните правой кнопкой мыши проект ToDoListAPI hello и нажмите кнопку **Добавить > клиента REST API**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-294">Right-click hello ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Добавление клиента REST API в Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="5ed4e-296">В hello **Добавление клиента REST API** диалоговое окно, нажмите кнопку **URL-адрес Swagger**, а затем нажмите кнопку **активов Azure выберите**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-296">In hello **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Select Azure Asset](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="5ed4e-298">В hello **службы приложений** диалоговое окно, разверните группу ресурсов hello, вы используете для этого учебника выберите API приложения и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-298">In hello **App Service** dialog box, expand hello resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Выбор приложения API для создания кода](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="5ed4e-300">Обратите внимание, что при возврате toohello **Добавление клиента REST API** диалоговом hello текстовое поле автоматически вводится определение hello API значение URL-адреса, который рассматривался выше hello портала.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-300">Notice that when you return toohello **Add REST API Client** dialog, hello text box has been filled in with hello API definition URL value that you saw earlier in hello portal.</span></span>
   
    ![URL-адрес определения API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="5ed4e-302">Метаданные tooget альтернативный способ создания кода — это URL-адрес hello tooenter напрямую, а не через диалоговое окно обзора hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-302">An alternative way tooget metadata for code generation is tooenter hello URL directly instead of going through hello browse dialog.</span></span> <span data-ttu-id="5ed4e-303">Или следует toogenerate клиентский код перед развертыванием tooAzure можно запустить проект веб-API hello локально, go toohello URL-адрес, предоставляющий hello Swagger JSON-файл, сохраните файл hello и использовать hello **выберите существующий файл метаданных Swagger**параметр.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-303">Or if you want toogenerate client code before deploying tooAzure, you could run hello Web API project locally, go toohello URL that provides hello Swagger JSON file, save hello file, and use hello **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="5ed4e-304">В hello **Добавление клиента REST API** диалоговое окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-304">In hello **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="5ed4e-305">Visual Studio создает папку с именем приложение hello API и создает клиентские классы.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-305">Visual Studio creates a folder named after hello API app and generates client classes.</span></span>
   
    ![Файлы кода для созданного клиента](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="5ed4e-307">В проекте ToDoListAPI hello откройте *Controllers\ToDoListController.cs* toosee hello код вызывает hello API с помощью клиента создается hello строки 40.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-307">In hello ToDoListAPI project, open *Controllers\ToDoListController.cs* toosee hello code at line 40  that calls hello API by using hello generated client.</span></span>
   
    <span data-ttu-id="5ed4e-308">Hello, следующий фрагмент кода показывает, как hello код создает экземпляр объекта клиента hello и вызовы hello метода Get.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-308">hello following snippet shows how hello code instantiates hello client object and calls hello Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="5ed4e-309">параметр Hello конструктор получает URL-адрес конечной точки hello от hello `toDoListDataAPIURL` параметра приложения.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-309">hello constructor parameter gets hello endpoint URL from  hello `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="5ed4e-310">В файле Web.config hello это значение является toohello набор локальных IIS Express URL-адрес hello API проекта, чтобы можно было запускать приложения hello локально.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-310">In hello Web.config file, that value is set toohello local IIS Express URL of hello API project so that you can run hello application locally.</span></span> <span data-ttu-id="5ed4e-311">При отсутствии параметра конструктора hello конечную точку по умолчанию hello — hello URL-адрес, созданный код hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-311">If you omit hello constructor parameter, hello default endpoint is hello URL that you generated hello code from.</span></span>
7. <span data-ttu-id="5ed4e-312">Будет создан класс вашего клиента с другим именем на основе имени приложения API; Изменение кода hello в *Controllers\ToDoListController.cs* , чтобы hello имя типа соответствует что был создан в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-312">Your client class will be generated with a different name based on your API app name; change hello code in *Controllers\ToDoListController.cs* so that hello type name matches what was generated in your project.</span></span> <span data-ttu-id="5ed4e-313">Например, если вы назвали приложение API ToDoListDataAPI071316, необходимо изменить код</span><span class="sxs-lookup"><span data-stu-id="5ed4e-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="5ed4e-314">toothis:</span><span class="sxs-lookup"><span data-stu-id="5ed4e-314">toothis:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a><span data-ttu-id="5ed4e-315">Создать API приложения toohost hello среднего уровня</span><span class="sxs-lookup"><span data-stu-id="5ed4e-315">Create an API app toohost hello middle tier</span></span>
<span data-ttu-id="5ed4e-316">Ранее вы [приложения hello данных уровня API создания и развертывания кода tooit](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-316">Earlier you [created hello data tier API app and deployed code tooit](#createapiapp).</span></span>  <span data-ttu-id="5ed4e-317">Теперь выполните hello же процедуру для среднего уровня API приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-317">Now you follow hello same procedure for hello middle tier API app.</span></span>

1. <span data-ttu-id="5ed4e-318">В **обозревателе решений**, щелкните правой кнопкой мыши hello среднего уровня ToDoListAPI проекта (не hello уровень данных ToDoListDataAPI) и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-318">In **Solution Explorer**, right-click hello middle tier ToDoListAPI  project (not hello data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Нажмите кнопку "Опубликовать" в Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="5ed4e-320">В hello **профиль** вкладка hello **веб-публикация** мастера, нажмите кнопку **службу приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-320">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="5ed4e-321">В hello **службы приложений** диалоговое окно, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-321">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="5ed4e-322">В hello **размещения** вкладка hello **Создание приложения службы** диалогового окна поле, примите значение по умолчанию hello **имя приложения API** или введите имя, которое является уникальным в hello  *azurewebsites.NET* домена.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-322">In hello **Hosting** tab of hello **Create App Service** dialog box, accept hello default **API App Name** or enter a name that is unique in hello *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="5ed4e-323">Выберите hello Azure **подписки** вы используете.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-323">Choose hello Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="5ed4e-324">В hello **группы ресурсов** раскрывающийся список, выберите hello одну группу ресурсов, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-324">In hello **Resource Group** drop-down, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="5ed4e-325">В hello **план обслуживания приложений** раскрывающийся список, выберите hello одного плана, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-325">In hello **App Service Plan** drop-down, choose hello same plan you created earlier.</span></span> <span data-ttu-id="5ed4e-326">По умолчанию значение toothat.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-326">It will default toothat value.</span></span>
8. <span data-ttu-id="5ed4e-327">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-327">Click **Create**.</span></span>
   
    <span data-ttu-id="5ed4e-328">Visual Studio создает приложение hello API, создает профиль публикации для него и отображает hello **подключения** шага hello **веб-публикация** мастера.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-328">Visual Studio creates hello API app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
9. <span data-ttu-id="5ed4e-329">В hello **подключения** шага hello **веб-публикация** мастера, нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-329">In hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="5ed4e-330">Visual Studio развертывает ToDoListAPI проекта toohello новый API приложение hello и открывает обозреватель toohello URL-адрес приложения hello API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-330">Visual Studio deploys hello ToDoListAPI project toohello new API app and opens a browser toohello URL of hello API app.</span></span> <span data-ttu-id="5ed4e-331">Откроется страница приветствия «успешно создан».</span><span class="sxs-lookup"><span data-stu-id="5ed4e-331">hello "successfully created" page appears.</span></span>

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a><span data-ttu-id="5ed4e-332">Настроить уровень данных hello toocall среднего уровня hello</span><span class="sxs-lookup"><span data-stu-id="5ed4e-332">Configure hello middle tier toocall hello data tier</span></span>
<span data-ttu-id="5ed4e-333">При вызове API приложение hello среднего уровня теперь он предпримет попытку уровень данных hello toocall, с помощью hello localhost URL-адрес, по-прежнему в файле Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-333">If you called hello middle tier API app now, it would try toocall hello data tier using hello localhost URL that is still in hello Web.config file.</span></span> <span data-ttu-id="5ed4e-334">В этом разделе введите URL-адрес hello данных уровня API приложения в параметры среды в API приложение hello среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-334">In this section you enter hello data tier API app URL into an environment setting in hello middle tier API app.</span></span> <span data-ttu-id="5ed4e-335">Если hello кода в приложении API hello среднего уровня получает URL-адрес уровня данных приветствия, параметр среды hello перезаписывает в файл Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-335">When hello code in hello middle tier API app retrieves hello data tier URL setting, hello environment setting will override what's in hello Web.config file.</span></span>

1. <span data-ttu-id="5ed4e-336">Go toohello [портал Azure](https://portal.azure.com/)и перейдите toohello **приложения API** колонке приложение hello API, созданного проекта TodoListAPI (средний уровень) toohost hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-336">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that you created toohost hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="5ed4e-337">В hello приложения API **параметры** колонка, щелкните **параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-337">In hello API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="5ed4e-338">Здравствуйте, приложения API в **параметры приложения** колонки, прокрутите вниз toohello **параметры приложения** статьи и добавьте следующее hello ключ и значение.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-338">In hello API App's **Application Settings** blade, scroll down toohello **App settings** section and add hello following key and value.</span></span> <span data-ttu-id="5ed4e-339">URL-адрес hello hello первый API приложения, опубликованные в этом учебнике будет иметь значение Hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-339">hello value will be hello URL of hello first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="5ed4e-340">**Ключ**</span><span class="sxs-lookup"><span data-stu-id="5ed4e-340">**Key**</span></span> | <span data-ttu-id="5ed4e-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="5ed4e-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="5ed4e-342">**Значение**</span><span class="sxs-lookup"><span data-stu-id="5ed4e-342">**Value**</span></span> |<span data-ttu-id="5ed4e-343">https://{имя приложения API уровня данных}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5ed4e-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="5ed4e-344">**Пример**</span><span class="sxs-lookup"><span data-stu-id="5ed4e-344">**Example**</span></span> |<span data-ttu-id="5ed4e-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="5ed4e-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="5ed4e-346">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-346">Click **Save**.</span></span>
   
    ![Нажмите кнопку "Сохранить" в колонке "Параметры приложения"](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="5ed4e-348">Когда код hello работает в Azure, это значение теперь переопределит hello localhost URL-адрес, в файле Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-348">When hello code runs in Azure, this value will now override hello localhost URL that is in hello Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="5ed4e-349">Тест</span><span class="sxs-lookup"><span data-stu-id="5ed4e-349">Test</span></span>
1. <span data-ttu-id="5ed4e-350">В окне браузера перейдите toohello URL-адрес нового hello среднего уровня приложения API, который вы только что создали ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-350">In a browser window, browse toohello URL of hello new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="5ed4e-351">Существует можно получить, щелкнув URL-адрес hello в главной колонке приложение hello API на портале hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-351">You can get there by clicking hello URL in hello API app's main blade in hello portal.</span></span>
2. <span data-ttu-id="5ed4e-352">Добавить URL-адрес toohello «swagger» в адресной строке браузера hello и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-352">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="5ed4e-353">(URL-адрес является hello `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="5ed4e-353">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="5ed4e-354">Hello браузер отображает hello же Swagger пользовательский Интерфейс, который вы видели ранее для ToDoListDataAPI, но теперь `owner` не поле является обязательным для операции Get hello, так как приложение среднего уровня API hello отправляет этого API приложения уровня данных значение toohello для вас.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-354">hello browser displays hello same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for hello Get operation, because hello middle tier API app is sending that value toohello data tier API app for you.</span></span> <span data-ttu-id="5ed4e-355">(Hello учебники проверки подлинности, средний уровень hello отправляют идентификаторы пользователя для hello `owner` параметр; теперь он жестко запрограммированного звездочку.)</span><span class="sxs-lookup"><span data-stu-id="5ed4e-355">(When you do hello authentication tutorials, hello middle tier will send actual user IDs for hello `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="5ed4e-356">Опробуйте hello метод Get и hello других toovalidate методы, hello приложения среднего уровня API успешно вызывает hello данных уровня приложения API.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-356">Try out hello Get method and hello other methods toovalidate that hello middle tier API app is successfully calling hello data tier API app.</span></span>
   
    ![Метод Get пользовательского интерфейса Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="5ed4e-358">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="5ed4e-358">Troubleshooting</span></span>
<span data-ttu-id="5ed4e-359">Если в ходе выполнения инструкций этого руководства возникнут проблемы, можно воспользоваться рекомендациями по устранению неполадок ниже:</span><span class="sxs-lookup"><span data-stu-id="5ed4e-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="5ed4e-360">Убедитесь, что вы используете последнюю версию hello hello [Azure SDK для .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-360">Make sure that you're using hello latest version of hello [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="5ed4e-361">Два приветствия имен проекта являются аналогичные (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-361">Two of hello project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="5ed4e-362">Если не выглядит как описано в инструкциях hello при работе с проектом, убедитесь, что вы открыли hello нужный проект.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-362">If things don't look as described in hello instructions when you are working with a project, make sure you have opened hello correct project.</span></span>
* <span data-ttu-id="5ed4e-363">Если вы в корпоративной сети и пытаетесь tooAzure toodeploy службы приложений через брандмауэр, убедитесь, что открыты порты 443 и 8172 для веб-развертывания.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-363">If you're on a corporate network and are trying toodeploy tooAzure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="5ed4e-364">Если не удается открыть эти порты, можно использовать другие способы развертывания.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="5ed4e-365">В разделе [развертывание вашего приложения tooAzure службы приложений](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-365">See [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="5ed4e-366">Ошибки «имена маршрутов должны быть уникальными»--можно получить их, если случайно развернуть приложение tooan API неправильный проекта hello и впоследствии развернуты правильно один tooit hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-366">"Route names must be unique" errors -- you could get these if you accidentally deploy hello wrong project tooan API app and then later deploy hello correct one tooit.</span></span> <span data-ttu-id="5ed4e-367">toocorrect, повторного развертывания нужный проект toohello API приложение hello и на hello **параметры** вкладка hello **веб-публикация** мастера щелкните **удалить дополнительные файлы в месте назначения**.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-367">toocorrect this, redeploy hello correct project toohello API app, and on hello **Settings** tab of hello **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="5ed4e-368">После того как вы приложении ASP.NET API, запущенные в службе приложений Azure, вы можете toolearn Дополнительные сведения о функциональных возможностях Visual Studio, которые упрощают устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-368">After you have your ASP.NET API app running in Azure App Service, you may want toolearn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="5ed4e-369">Сведения о ведении журналов, удаленной отладке и другую информацию см. в статье [Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ed4e-370">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ed4e-370">Next steps</span></span>
<span data-ttu-id="5ed4e-371">Вы знаете, как toodeploy существующие веб-API проекты tooAPI приложения, создания кода клиента для приложения API и использовать API приложения от клиентов .NET.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-371">You've seen how toodeploy existing Web API projects tooAPI apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="5ed4e-372">Hello далее в этой серии мы увидели, как слишком[использовать приложения tooconsume API CORS из клиентов JavaScript](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-372">hello next tutorial in this series shows how too[use CORS tooconsume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="5ed4e-373">Дополнительные сведения о создании кода клиента см. в разделе hello [Azure/AutoRest](https://github.com/azure/autorest) репозитория в GitHub.com. Помощь по вопросам, с помощью клиента создается hello откройте [проблему в репозитории hello AutoRest](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="5ed4e-373">For more information about client code generation, see hello [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com. For help with problems using hello generated client, open an [issue in hello AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="5ed4e-374">Новые проекты приложения API toocreate с нуля, используйте hello **приложения API Azure** шаблона.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-374">If you want toocreate new API app projects from scratch, use hello **Azure API App** template.</span></span>

![Шаблон приложения API в Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="5ed4e-376">Hello **приложения API Azure** шаблон проекта — hello эквивалентные toochoosing **пустой** ASP.NET 4.5.2 шаблона, щелкнув поддержки веб-API tooadd флажок hello и установка пакета Swashbuckle NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-376">hello **Azure API App** project template is equivalent toochoosing hello **Empty** ASP.NET 4.5.2 template, clicking hello check box tooadd Web API support, and installing hello Swashbuckle NuGet package.</span></span> <span data-ttu-id="5ed4e-377">Кроме того шаблон hello добавляет некоторые Создание Swashbuckle конфигурации код, предназначенный tooprevent hello повторяющиеся операции Swagger идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-377">In addition, hello template adds some Swashbuckle configuration code designed tooprevent hello creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="5ed4e-378">После создания проекта приложения API, его можно развернуть приложение hello tooan API так же, как показано в данном учебнике.</span><span class="sxs-lookup"><span data-stu-id="5ed4e-378">Once you've created an API App project, you can deploy it tooan API app hello same way you saw in this tutorial.</span></span>

