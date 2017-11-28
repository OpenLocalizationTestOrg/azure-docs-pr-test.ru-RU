---
title: "Приступая к работе с приложениями API и ASP.NET в службе приложений | Документация Майкрософт"
description: "Узнайте, как создать, развернуть и использовать приложение API ASP.NET в службе приложений Azure с помощью Visual Studio 2015."
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
ms.openlocfilehash: e8fbffde29efcdbb2f67362474061e9f6ee0d59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="68c1e-103">Приступая к работе с приложениями API, ASP.NET и Swagger в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="68c1e-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="68c1e-104">Это первое руководство из серии, посвященной использованию функций службы приложений Azure, которые могут быть полезны при разработке и размещении интерфейсов API RESTful.</span><span class="sxs-lookup"><span data-stu-id="68c1e-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="68c1e-105">В этом руководстве рассматривается обеспечение поддержки метаданных API в формате Swagger.</span><span class="sxs-lookup"><span data-stu-id="68c1e-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="68c1e-106">Вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="68c1e-106">You'll learn:</span></span>

* <span data-ttu-id="68c1e-107">как создавать и развертывать [приложения API](app-service-api-apps-why-best-platform.md) в службе приложений Azure с помощью средств, встроенных в Visual Studio 2015;</span><span class="sxs-lookup"><span data-stu-id="68c1e-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="68c1e-108">как автоматизировать обнаружение API, используя пакет NuGet Swashbuckle, чтобы динамически создавать метаданные API Swagger;</span><span class="sxs-lookup"><span data-stu-id="68c1e-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="68c1e-109">как использовать метаданные API Swagger для автоматического создания кода клиента для приложения API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-109">How to use Swagger API metadata to automatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="68c1e-110">Обзор примеров приложений</span><span class="sxs-lookup"><span data-stu-id="68c1e-110">Sample application overview</span></span>
<span data-ttu-id="68c1e-111">В этом руководстве вы будете работать с простым примером приложения списка дел.</span><span class="sxs-lookup"><span data-stu-id="68c1e-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="68c1e-112">Приложение состоит из внешнего одностраничного интерфейса, веб-API ASP.NET среднего уровня и веб-API ASP.NET уровня данных.</span><span class="sxs-lookup"><span data-stu-id="68c1e-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Схема примера приложения приложений API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="68c1e-114">Ниже приведен снимок экрана внешнего интерфейса [AngularJS](https://angularjs.org/) .</span><span class="sxs-lookup"><span data-stu-id="68c1e-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span></span>

![Список дел в примере приложения приложений API](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="68c1e-116">Это решение Visual Studio включает в себя три проекта:</span><span class="sxs-lookup"><span data-stu-id="68c1e-116">The Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="68c1e-117">**ToDoListAngular** (внешний интерфейс). Одностраничное приложение AngularJS, вызывающее средний уровень.</span><span class="sxs-lookup"><span data-stu-id="68c1e-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span></span>
* <span data-ttu-id="68c1e-118">**ToDoListAPI** (средний уровень). Проект веб-API ASP.NET, вызывающий уровень данных, чтобы выполнять операции CRUD с элементами списка дел.</span><span class="sxs-lookup"><span data-stu-id="68c1e-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="68c1e-119">**ToDoListDataAPI** (уровень данных). Проект веб-API ASP.NET, выполняющий операции CRUD с элементами списка дел.</span><span class="sxs-lookup"><span data-stu-id="68c1e-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="68c1e-120">Трехуровневая архитектура — одна из множества архитектур, которые можно реализовать с помощью приложений API. В этой статье она представлена исключительно в демонстрационных целях.</span><span class="sxs-lookup"><span data-stu-id="68c1e-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="68c1e-121">На каждом уровне используется максимально упрощенный код для демонстрации возможностей приложений API. Например, на уровне данных в качестве механизма сохранения используется память сервера, а не база данных.</span><span class="sxs-lookup"><span data-stu-id="68c1e-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="68c1e-122">По завершении этого руководства вы создадите два проекта веб-API, которые будут работать в облаке в приложениях API службы приложений.</span><span class="sxs-lookup"><span data-stu-id="68c1e-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span></span>

<span data-ttu-id="68c1e-123">В следующем руководстве этой серии вы узнаете, как развернуть внешний интерфейс одностраничного приложения в облаке.</span><span class="sxs-lookup"><span data-stu-id="68c1e-123">The next tutorial in the series deploys the SPA front end to the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68c1e-124">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="68c1e-124">Prerequisites</span></span>
* <span data-ttu-id="68c1e-125">Веб-API ASP.NET. В инструкциях руководства предполагается, что у вас уже есть базовые знания о работе с [веб-API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) ASP.NET в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68c1e-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="68c1e-126">Учетная запись Azure. [Создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="68c1e-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="68c1e-127">Чтобы приступить к работе со службой приложений Azure до регистрации и получения учетной записи Azure, перейдите на страницу [пробного использования службы приложений](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="68c1e-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="68c1e-128">Там можно быстро создать кратковременное приложение начального уровня в службе приложений. Это не потребует **ни кредитной карты**, ни каких-либо обязательств.</span><span class="sxs-lookup"><span data-stu-id="68c1e-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="68c1e-129">Visual Studio 2015 с [Azure SDK для .NET](https://azure.microsoft.com/downloads/archive-net-downloads/). Пакет SDK автоматически устанавливает Visual Studio 2015, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="68c1e-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="68c1e-130">В Visual Studio щелкните "Справка -> О Microsoft Visual Studio" и убедитесь, что у вас установлены средства службы приложений Azure версии 2.9.1 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="68c1e-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Версия средств приложений Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="68c1e-132">В зависимости от того, сколько зависимостей пакета SDK уже имеется на компьютере, установка пакета SDK может занять определенное время, от нескольких минут до получаса или более.</span><span class="sxs-lookup"><span data-stu-id="68c1e-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span></span>
    > 
    > 

## <a name="download-the-sample-application"></a><span data-ttu-id="68c1e-133">Загрузка примера приложения</span><span class="sxs-lookup"><span data-stu-id="68c1e-133">Download the sample application</span></span>
1. <span data-ttu-id="68c1e-134">Скачайте репозиторий [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) .</span><span class="sxs-lookup"><span data-stu-id="68c1e-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="68c1e-135">Для этого нажмите кнопку **Download ZIP** (Скачать ZIP-файл) или клонируйте репозиторий на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="68c1e-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span></span>
2. <span data-ttu-id="68c1e-136">Откройте решение ToDoList в Visual Studio 2015 или 2013.</span><span class="sxs-lookup"><span data-stu-id="68c1e-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="68c1e-137">Вам потребуется подтвердить, что нужно доверять всем решениям.</span><span class="sxs-lookup"><span data-stu-id="68c1e-137">You will need to trust each solution.</span></span>
         <span data-ttu-id="68c1e-138">![Предупреждение системы безопасности](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="68c1e-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="68c1e-139">Создайте решение (CTRL+SHIFT+B), чтобы восстановить пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="68c1e-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span></span>
   
    <span data-ttu-id="68c1e-140">Чтобы увидеть приложение в действии перед развертыванием, можно запустить его локально.</span><span class="sxs-lookup"><span data-stu-id="68c1e-140">If you want to see the application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="68c1e-141">Убедитесь, что ToDoListDataAPI настроен в качестве запускаемого проекта, и запустите решение.</span><span class="sxs-lookup"><span data-stu-id="68c1e-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span></span> <span data-ttu-id="68c1e-142">В браузере может отобразиться ошибка HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="68c1e-142">You should expect to see a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="68c1e-143">Использование метаданных и пользовательского интерфейса API Swagger</span><span class="sxs-lookup"><span data-stu-id="68c1e-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="68c1e-144">Поддержка метаданных API [Swagger 2.0](http://swagger.io/) встроена в службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="68c1e-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="68c1e-145">В каждом приложении API можно указать URL-адрес конечной точки, которая возвращает метаданные для API в формате JSON-файла Swagger.</span><span class="sxs-lookup"><span data-stu-id="68c1e-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span></span> <span data-ttu-id="68c1e-146">Метаданные, возвращенные из этой конечной точки, можно использовать для создания клиентского кода.</span><span class="sxs-lookup"><span data-stu-id="68c1e-146">The metadata returned from that endpoint can be used to generate client code.</span></span>

<span data-ttu-id="68c1e-147">Проект веб-API ASP.NET может динамически создавать метаданные Swagger, используя пакет NuGet [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) .</span><span class="sxs-lookup"><span data-stu-id="68c1e-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="68c1e-148">В скачанных проектах ToDoListDataAPI и ToDoListAPI этот пакет уже установлен.</span><span class="sxs-lookup"><span data-stu-id="68c1e-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="68c1e-149">В этом разделе мы рассмотрим созданные метаданные Swagger 2.0 и попробуем поработать с созданным на их основе пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="68c1e-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span></span>

1. <span data-ttu-id="68c1e-150">Установите проект ToDoListDataAPI (**не** проект ToDoListAPI) в качестве запускаемого проекта.</span><span class="sxs-lookup"><span data-stu-id="68c1e-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span></span>
   
    ![Назначить ToDoDataAPI в качестве запускаемого проекта](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="68c1e-152">Нажмите клавишу F5 или выберите **Отладка > Начать отладку**, чтобы запустить проект в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="68c1e-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span></span>
   
    <span data-ttu-id="68c1e-153">Откроется браузер, в котором отобразится страница с ошибкой HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="68c1e-153">The browser opens and shows the HTTP 403 error page.</span></span>
3. <span data-ttu-id="68c1e-154">В адресной строке браузера добавьте `swagger/docs/v1` в конец строки и нажмите кнопку «Назад».</span><span class="sxs-lookup"><span data-stu-id="68c1e-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span></span> <span data-ttu-id="68c1e-155">(URL-адрес — `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="68c1e-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="68c1e-156">Это URL-адрес по умолчанию, используемый Swashbuckle, чтобы вернуть метаданные JSON Swagger 2.0 для API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span></span>
   
    <span data-ttu-id="68c1e-157">При использовании Internet Explorer появится запрос на скачивание файла *v1.json* .</span><span class="sxs-lookup"><span data-stu-id="68c1e-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span></span>
   
    ![Скачивание метаданных JSON в Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="68c1e-159">При использовании Chrome, Firefox или Microsoft Edge в окне браузера отобразится JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="68c1e-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span></span> <span data-ttu-id="68c1e-160">В каждом браузере JSON обрабатывается по-своему. Вид окна вашего браузера может отличаться от вида окна в примере.</span><span class="sxs-lookup"><span data-stu-id="68c1e-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span></span>
   
    ![Метаданные JSON в Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="68c1e-162">В следующем примере показана первая часть метаданных Swagger для API с определением для метода GET.</span><span class="sxs-lookup"><span data-stu-id="68c1e-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span></span> <span data-ttu-id="68c1e-163">Эти метаданные позволяют использовать пользовательский интерфейс Swagger, которым мы воспользуемся на следующих шагах. Он будет использоваться в следующем разделе этого руководства для автоматического создания кода клиента.</span><span class="sxs-lookup"><span data-stu-id="68c1e-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span></span>
   
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
4. <span data-ttu-id="68c1e-164">Закройте браузер и остановите процесс отладки Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68c1e-164">Close the browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="68c1e-165">В проекте ToDoListDataAPI в **обозревателе решений** откройте файл *App_Start\SwaggerConfig.cs*, а затем найдите строку 174 и раскомментируйте следующий код.</span><span class="sxs-lookup"><span data-stu-id="68c1e-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="68c1e-166">При установке пакета Swashbuckle в проекте создается файл *SwaggerConfig.cs* .</span><span class="sxs-lookup"><span data-stu-id="68c1e-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span></span> <span data-ttu-id="68c1e-167">С его помощью можно настроить Swashbuckle несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="68c1e-167">The file provides a number of ways to configure Swashbuckle.</span></span>
   
    <span data-ttu-id="68c1e-168">Раскомментированный код позволяет применять пользовательский интерфейс Swagger, используемый на следующих шагах.</span><span class="sxs-lookup"><span data-stu-id="68c1e-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span></span> <span data-ttu-id="68c1e-169">При создании проекта веб-API с помощью шаблона проекта приложения API в целях безопасности этот код закомментирован по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="68c1e-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="68c1e-170">Запустите проект снова.</span><span class="sxs-lookup"><span data-stu-id="68c1e-170">Run the project again.</span></span>
7. <span data-ttu-id="68c1e-171">В адресной строке браузера добавьте `swagger` в конец строки и нажмите кнопку «Назад».</span><span class="sxs-lookup"><span data-stu-id="68c1e-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span></span> <span data-ttu-id="68c1e-172">(URL-адрес — `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="68c1e-172">(The URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="68c1e-173">Когда откроется страница пользовательского интерфейса Swagger, щелкните **ToDoList** , чтобы увидеть доступные методы.</span><span class="sxs-lookup"><span data-stu-id="68c1e-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span></span>
   
    ![Пользовательский интерфейс Swagger — доступные методы](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="68c1e-175">Нажмите первую кнопку **Get** в списке.</span><span class="sxs-lookup"><span data-stu-id="68c1e-175">Click the first **Get** button in the list.</span></span>
10. <span data-ttu-id="68c1e-176">В разделе **Параметры** введите звездочку в качестве значения параметра `owner`, а затем нажмите кнопку **Попробуйте в деле**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="68c1e-177">В последующих руководствах при добавлении проверки подлинности средний уровень указывает фактический идентификатор пользователя для уровня данных.</span><span class="sxs-lookup"><span data-stu-id="68c1e-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span></span> <span data-ttu-id="68c1e-178">Теперь при выполнении приложения с выключенной аутентификацией для всех задач в качестве идентификатора владельца будет использоваться звездочка.</span><span class="sxs-lookup"><span data-stu-id="68c1e-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span></span>
    
    ![Пользовательский интерфейс Swagger — кнопка Try it out](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="68c1e-180">Пользовательский интерфейс Swagger вызывает метод Get проекта ToDoList и отображает код ответа и результаты JSON.</span><span class="sxs-lookup"><span data-stu-id="68c1e-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span></span>
    
    ![Пользовательский интерфейс Swagger — результаты нажатия кнопки Try it out](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="68c1e-182">Щелкните **Post**, а затем — поле в разделе **Model Schema** (Схема модели).</span><span class="sxs-lookup"><span data-stu-id="68c1e-182">Click **Post**, and then click the box under **Model Schema**.</span></span>
    
    <span data-ttu-id="68c1e-183">При этом предварительно заполняется поле ввода, в котором можно указать значение параметра для метода POST.</span><span class="sxs-lookup"><span data-stu-id="68c1e-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span></span> <span data-ttu-id="68c1e-184">Если этот способ не сработает в Internet Explorer, используйте другой браузер или вручную введите значение параметра на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="68c1e-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span></span>  
    
    ![Пользовательский интерфейс Swagger — нажатие кнопки Try it out при выборе метода Post](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="68c1e-186">В поле ввода параметров `todo` измените код JSON, чтобы он выглядел, как показано ниже, или введите собственное описание:</span><span class="sxs-lookup"><span data-stu-id="68c1e-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy the dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="68c1e-187">Щелкните **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="68c1e-188">Проект ToDoList API возвращает код ответа HTTP 204, который указывает на успешное завершение.</span><span class="sxs-lookup"><span data-stu-id="68c1e-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="68c1e-189">Нажмите первую кнопку **Get**, а затем в соответствующем разделе страницы нажмите кнопку **Попробуйте в деле**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span></span>
    
    <span data-ttu-id="68c1e-190">Теперь ответ метода GET содержит новый элемент списка дел.</span><span class="sxs-lookup"><span data-stu-id="68c1e-190">The Get method response now includes the new to do item.</span></span>
15. <span data-ttu-id="68c1e-191">Необязательно: также попробуйте методы Put, Delete и Get по идентификатору (ID).</span><span class="sxs-lookup"><span data-stu-id="68c1e-191">Optional: Try also the Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="68c1e-192">Закройте браузер и остановите процесс отладки Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68c1e-192">Close the browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="68c1e-193">Swashbuckle можно использовать с любыми проектами веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="68c1e-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="68c1e-194">Если нужно добавить возможность создания метаданных Swagger в существующий проект, просто установите пакет Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="68c1e-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="68c1e-195">В метаданных Swagger есть уникальный идентификатор для каждой операции API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="68c1e-196">По умолчанию пакет Swashbuckle может создавать дублирующиеся идентификаторы операций Swagger для методов контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="68c1e-197">Это происходит, если перегружены методы HTTP контроллера, например `Get()` и `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="68c1e-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="68c1e-198">Дополнительные сведения о действиях при перегрузке см. в статье [Настройка определений API, создаваемых в Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="68c1e-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="68c1e-199">Если проект веб-API в Visual Studio создается с помощью шаблона приложения API Azure, к файлу *SwaggerConfig.cs* автоматически добавляется код, который создает уникальные идентификаторы операций.</span><span class="sxs-lookup"><span data-stu-id="68c1e-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="68c1e-200"><a id="createapiapp"></a> Создание приложения API в Azure и развертывание кода в нем</span><span class="sxs-lookup"><span data-stu-id="68c1e-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code to it</span></span>
<span data-ttu-id="68c1e-201">В этом разделе вы создадите приложение API в Azure с помощью инструментов Azure, интегрированных в мастер **Публикация веб-сайта** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68c1e-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span></span> <span data-ttu-id="68c1e-202">Затем вы развернете проект ToDoListDataAPI в новом приложении API и вызовете API, запустив пользовательский интерфейс Swagger.</span><span class="sxs-lookup"><span data-stu-id="68c1e-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span></span>

1. <span data-ttu-id="68c1e-203">В **обозревателе решений** щелкните правой кнопкой мыши проект ToDoListDataAPI и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Нажмите кнопку "Опубликовать" в Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="68c1e-205">В мастере **Публикация веб-сайта** на вкладке **Профиль** щелкните **Служба приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Выберите "Служба приложений Azure" в мастере веб-публикации](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="68c1e-207">Войдите в учетную запись Azure, если вы этого еще не сделали, или обновите учетные данные, если срок их действия истек.</span><span class="sxs-lookup"><span data-stu-id="68c1e-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="68c1e-208">В диалоговом окне "Служба приложений" в поле **Подписка** выберите подписку Azure, которую хотите использовать, и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span></span>
   
    ![Нажмите кнопку "Создать" в диалоговом окне службы приложений](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="68c1e-210">Откроется диалоговое окно **Создать службу приложений** со вкладкой **Размещение**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="68c1e-211">Так как вы развертываете проект веб-API, в котором установлен пакет Swashbuckle, программа Visual Studio предлагает создать приложение API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span></span> <span data-ttu-id="68c1e-212">Это можно определить по имени поля **API App Name** (Имя приложения API) и типу приложения (в раскрывающемся списке **Изменить тип** выбран тип **Приложение API**).</span><span class="sxs-lookup"><span data-stu-id="68c1e-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span></span>
   
    ![Тип приложения в диалоговом окне службы приложений](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="68c1e-214">В поле **Имя приложения API** введите имя, которое является уникальным в домене *azurewebsites.net* .</span><span class="sxs-lookup"><span data-stu-id="68c1e-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span></span> <span data-ttu-id="68c1e-215">Можно использовать имя по умолчанию, предоставляемое Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68c1e-215">You can accept the default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="68c1e-216">Если ввести имя, которое уже используется, справа появится красный восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="68c1e-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
   
    <span data-ttu-id="68c1e-217">У приложения API будет такой URL-адрес: `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="68c1e-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="68c1e-218">Возле раскрывающегося списка **Группа ресурсов** нажмите кнопку **Создать** и введите имя ToDoListGroup или любое другое.</span><span class="sxs-lookup"><span data-stu-id="68c1e-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="68c1e-219">Группы ресурсов — это совокупность ресурсов Azure, таких как приложения API, базы данных, виртуальные машины и т. д.</span><span class="sxs-lookup"><span data-stu-id="68c1e-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="68c1e-220">Мы рекомендуем создать новую группу ресурсов, так как это позволит быстро удалить все ресурсы Azure, созданные для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="68c1e-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
   
    <span data-ttu-id="68c1e-221">В этом поле можно выбрать существующую [группу ресурсов](../azure-resource-manager/resource-group-overview.md) или создать отдельную, введя имя, которое отличается от имени любой существующей группы ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="68c1e-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="68c1e-222">Нажмите кнопку **Создать** возле раскрывающегося списка **План службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-222">Click the **New** button next to the **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="68c1e-223">На снимке экрана показаны примеры значений в полях **API App Name** (Имя приложения API), **Подписка** и **Группа ресурсов**. Ваши значения будут другими.</span><span class="sxs-lookup"><span data-stu-id="68c1e-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Диалоговое окно "Создание службы приложений"](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="68c1e-225">Далее мы создадим план службы приложений для новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="68c1e-225">In the following steps you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="68c1e-226">План службы приложений определяет вычислительные ресурсы, на которых будет работать ваше приложение API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-226">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="68c1e-227">Например, если выбрать уровень "Бесплатный", ваше приложение будет работает на общих виртуальных машинах, тогда как при выборе некоторых платных уровней приложение будет работать на выделенных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="68c1e-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="68c1e-228">Дополнительные сведения см. в статье [Подробный обзор планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68c1e-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="68c1e-229">В диалоговом окне **Настроить план служб приложений** в соответствующем поле введите ToDoListPlan или другое имя.</span><span class="sxs-lookup"><span data-stu-id="68c1e-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="68c1e-230">В раскрывающемся списке **Расположение** выберите ближайшее расположение.</span><span class="sxs-lookup"><span data-stu-id="68c1e-230">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="68c1e-231">Этот параметр определяет, в каком центре обработки данных Azure будет выполняться приложение.</span><span class="sxs-lookup"><span data-stu-id="68c1e-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="68c1e-232">Выберите ближайшее расположение, чтобы максимально сократить [задержку](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="68c1e-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="68c1e-233">В раскрывающемся списке **Размер** щелкните **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-233">In the **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="68c1e-234">Эта ценовая категория обеспечит достаточную производительность в рамках заданий этого руководства.</span><span class="sxs-lookup"><span data-stu-id="68c1e-234">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="68c1e-235">В диалоговом окне **Настроить план служб приложений** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-235">In the **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Нажмите кнопку "ОК" в диалоговом окне "Настройка плана службы приложений"](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="68c1e-237">В диалоговом окне **Создать службу приложений** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-237">In the **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Нажмите кнопку "Создать" в диалоговом окне"Создание службы приложений"](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="68c1e-239">Visual Studio создает приложение API и профиль публикации со всеми настройками, необходимыми для приложения API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span></span> <span data-ttu-id="68c1e-240">Затем откроется мастер **Публикация веб-сайта** , который будет использоваться для развертывания проекта.</span><span class="sxs-lookup"><span data-stu-id="68c1e-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span></span>
    
    <span data-ttu-id="68c1e-241">В мастере **Публикация веб-сайта** откроется вкладка **Подключение** (показана ниже).</span><span class="sxs-lookup"><span data-stu-id="68c1e-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="68c1e-242">На вкладке **Подключение** в полях **Сервер** и **Имя сайта** укажите данные приложения API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span></span> <span data-ttu-id="68c1e-243">В полях **Имя пользователя** и **Пароль** указываются учетные данные развертывания, созданные Azure.</span><span class="sxs-lookup"><span data-stu-id="68c1e-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="68c1e-244">После развертывания с помощью Visual Studio в браузере откроется страница с **URL-адресом назначения** (**URL-адрес назначения** необходим только для этого).</span><span class="sxs-lookup"><span data-stu-id="68c1e-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="68c1e-245">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-245">Click **Next**.</span></span>
    
    ![Нажмите кнопку "Далее" на вкладке "Подключение" мастера веб-публикации](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="68c1e-247">Следующая вкладка — **Параметры** (показана ниже).</span><span class="sxs-lookup"><span data-stu-id="68c1e-247">The next tab is the **Settings** tab (shown below).</span></span> <span data-ttu-id="68c1e-248">Здесь можно изменить конфигурацию сборки, чтобы развернуть отладочную сборку для [удаленной отладки](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="68c1e-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="68c1e-249">На этой вкладке также представлен раздел **Параметры публикации файлов**с соответствующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="68c1e-249">The tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="68c1e-250">"Удалить дополнительные файлы в месте назначения";</span><span class="sxs-lookup"><span data-stu-id="68c1e-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="68c1e-251">"Предварительно компилировать при публикации";</span><span class="sxs-lookup"><span data-stu-id="68c1e-251">Precompile during publishing</span></span>
    * <span data-ttu-id="68c1e-252">"Исключить файлы из папки App_Data".</span><span class="sxs-lookup"><span data-stu-id="68c1e-252">Exclude files from the App_Data folder</span></span>
    
    <span data-ttu-id="68c1e-253">В данном руководстве эти параметры не используются.</span><span class="sxs-lookup"><span data-stu-id="68c1e-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="68c1e-254">Подробное описание этих параметров см. в статье [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) (Развертывание веб-проекта с помощью публикации одним щелчком в Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="68c1e-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="68c1e-255">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-255">Click **Next**.</span></span>
    
    ![Нажмите кнопку "Далее" на вкладке "Параметры" мастера веб-публикации](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="68c1e-257">Следующая вкладка — **Предварительный просмотр** (показана ниже). Здесь можно узнать, какие файлы скопируются из проекта в приложение API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span></span> <span data-ttu-id="68c1e-258">Если вы развертываете проект в приложение API, в которое проект уже был развернут, копируются только измененные файлы.</span><span class="sxs-lookup"><span data-stu-id="68c1e-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span></span> <span data-ttu-id="68c1e-259">Чтобы просмотреть список файлов, которые будут скопированы, нажмите кнопку **Начать просмотр** .</span><span class="sxs-lookup"><span data-stu-id="68c1e-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span></span>
15. <span data-ttu-id="68c1e-260">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-260">Click **Publish**.</span></span>
    
    ![Нажмите кнопку "Опубликовать" на вкладке "Предварительный просмотр" мастера веб-публикации](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="68c1e-262">Visual Studio развернет проект ToDoListDataAPI в новое приложение API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span></span> <span data-ttu-id="68c1e-263">В окне **Выходные данные** появятся сведения об успешном развертывании, а в окне браузера откроется страница с URL-адресом созданного приложения API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span></span>
    
    ![Окно вывода с информацией об успешном развертывании](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Страница "Приложение API успешно создано"](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="68c1e-266">В адресной строке браузера добавьте swagger в URL-адрес и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="68c1e-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="68c1e-267">(URL-адрес — `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="68c1e-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="68c1e-268">В браузере отобразится тот же пользовательский интерфейс Swagger, который вы уже видели, но теперь он будет работать в облаке.</span><span class="sxs-lookup"><span data-stu-id="68c1e-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span></span> <span data-ttu-id="68c1e-269">Попробуйте метод Get, и вы увидите, что вы возвращаетесь к элементам используемого по умолчанию списка дел 2.</span><span class="sxs-lookup"><span data-stu-id="68c1e-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span></span> <span data-ttu-id="68c1e-270">Внесенные ранее изменения сохранены в памяти локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="68c1e-270">The changes you made earlier were saved in memory in the local machine.</span></span>
17. <span data-ttu-id="68c1e-271">Откройте [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68c1e-271">Open the [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="68c1e-272">Портал Azure — это веб-интерфейс для управления ресурсами Azure, например приложениями API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="68c1e-273">Щелкните **Больше служб > Службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-273">Click **More Services > App Services**.</span></span>
    
    ![Обзор служб приложений](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="68c1e-275">В колонке **Службы приложений** найдите и выберите свое приложение API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-275">In the **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="68c1e-276">(На портале Azure окна, которые открываются справа, называются *колонками*).</span><span class="sxs-lookup"><span data-stu-id="68c1e-276">(In the Azure portal, windows that open to the right are called *blades*.)</span></span>
    
    ![Колонка "Службы приложений"](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="68c1e-278">Откроются две колонки:</span><span class="sxs-lookup"><span data-stu-id="68c1e-278">Two blades open.</span></span> <span data-ttu-id="68c1e-279">в одной будет общая информация о приложении API, а во второй — длинный список параметров, которые можно просматривать и изменять.</span><span class="sxs-lookup"><span data-stu-id="68c1e-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="68c1e-280">В колонке **Параметры** найдите раздел **API** и щелкните **Определение API**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span></span>
    
    ![Определение API в колонке "Параметры"](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="68c1e-282">В колонке **Определение API** можно указать URL-адрес, возвращающий метаданные Swagger 2.0 в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="68c1e-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="68c1e-283">Когда программа Visual Studio создает приложение API, она задает для URL-адреса определения API значение по умолчанию (для созданных пакетом Swashbuckle метаданных, которые вы уже видели ранее). Значением по умолчанию выступает базовый URL-адрес приложения API и строка `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="68c1e-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL-адрес определения API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="68c1e-285">При выборе приложения API, для которого нужно создать код клиента, Visual Studio извлекает метаданные из этого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="68c1e-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span></span>

## <span data-ttu-id="68c1e-286"><a id="codegen"></a> Создание кода клиента для уровня данных</span><span class="sxs-lookup"><span data-stu-id="68c1e-286"><a id="codegen"></a> Generate client code for the data tier</span></span>
<span data-ttu-id="68c1e-287">Одним из преимуществ интеграции платформы Swagger в приложения API Azure является автоматическое создание кода.</span><span class="sxs-lookup"><span data-stu-id="68c1e-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="68c1e-288">Созданные классы клиента упрощают написание кода, который вызывает приложение API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-288">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="68c1e-289">В проекте ToDoListAPI уже есть клиентский код, но на следующих шагах мы удалим его и создадим повторно, чтобы понять, как создается код.</span><span class="sxs-lookup"><span data-stu-id="68c1e-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span></span>

1. <span data-ttu-id="68c1e-290">В **обозревателе решений**Visual Studio в проекте ToDoListAPI удалите папку *ToDoListDataAPI* .</span><span class="sxs-lookup"><span data-stu-id="68c1e-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="68c1e-291">**Предупреждение. Нужно удалить только папку, а не проект ToDoListDataAPI.**</span><span class="sxs-lookup"><span data-stu-id="68c1e-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span></span>
   
    ![Удаление кода, созданного клиентом](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="68c1e-293">Эта папка появилась в процессе создания кода, который мы будем изучать.</span><span class="sxs-lookup"><span data-stu-id="68c1e-293">This folder was created by using the code generation process that you're about to go through.</span></span>
2. <span data-ttu-id="68c1e-294">Щелкните правой кнопкой мыши проект ToDoListAPI и выберите **Добавить > Клиент REST API**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Добавление клиента REST API в Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="68c1e-296">В диалоговом окне **Добавление клиента REST API** установите переключатель **Swagger URL** (URL-адрес Swagger), а затем нажмите кнопку **Выбрать ресурс Azure**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Select Azure Asset](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="68c1e-298">В диалоговом окне **Служба приложений** разверните группу ресурсов, используемую в этом руководстве, выберите нужное приложение API и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Выбор приложения API для создания кода](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="68c1e-300">Обратите внимание, что при возврате к диалоговому окну **Добавление клиента REST API** в текстовом поле введено значение URL-адреса определения API, которое вы видели на портале ранее.</span><span class="sxs-lookup"><span data-stu-id="68c1e-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span></span>
   
    ![URL-адрес определения API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="68c1e-302">Кроме того, чтобы получить метаданные для создания кода, URL-адрес можно ввести напрямую, а не в диалоговом окне обзора.</span><span class="sxs-lookup"><span data-stu-id="68c1e-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span></span> <span data-ttu-id="68c1e-303">Например, если нужно создать клиентский код до развертывания в Azure, запустите проект веб-API локально, перейдите по URL-адресу JSON-файла Swagger, сохраните файл и установите переключатель **Select an existing Swagger metadata file** (Выбрать существующий файл метаданных Swagger).</span><span class="sxs-lookup"><span data-stu-id="68c1e-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="68c1e-304">В диалоговом окне **Добавление клиента REST API** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-304">In the **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="68c1e-305">Visual Studio создает папку с именем приложения API и классы клиента.</span><span class="sxs-lookup"><span data-stu-id="68c1e-305">Visual Studio creates a folder named after the API app and generates client classes.</span></span>
   
    ![Файлы кода для созданного клиента](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="68c1e-307">В проекте ToDoListAPI откройте файл *Controllers\ToDoListController.cs*. В строке 40 вы увидите код, который вызывает API с помощью созданного клиента.</span><span class="sxs-lookup"><span data-stu-id="68c1e-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span></span>
   
    <span data-ttu-id="68c1e-308">В приведенном ниже фрагменте кода показано, как создать экземпляр объекта клиента и вызвать метод GET.</span><span class="sxs-lookup"><span data-stu-id="68c1e-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span></span>
   
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
   
    <span data-ttu-id="68c1e-309">Параметр конструктора получает URL-адрес конечной точки из параметра приложения `toDoListDataAPIURL`.</span><span class="sxs-lookup"><span data-stu-id="68c1e-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="68c1e-310">В файле Web.config это значение содержит локальный URL-адрес IIS Express проекта API, что дает возможность запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="68c1e-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span></span> <span data-ttu-id="68c1e-311">Если опустить параметр конструктора, в качестве конечной точки по умолчанию будет использоваться URL-адрес, на основе которого создан код.</span><span class="sxs-lookup"><span data-stu-id="68c1e-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span></span>
7. <span data-ttu-id="68c1e-312">Класс клиента будет создан с другим именем в зависимости от имени приложения API. Измените код в файле *Controllers\ToDoListController.cs* так, чтобы имя типа совпадало с именем в проекте.</span><span class="sxs-lookup"><span data-stu-id="68c1e-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span></span> <span data-ttu-id="68c1e-313">Например, если вы назвали приложение API ToDoListDataAPI071316, необходимо изменить код</span><span class="sxs-lookup"><span data-stu-id="68c1e-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="68c1e-314">на такой:</span><span class="sxs-lookup"><span data-stu-id="68c1e-314">to this:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-to-host-the-middle-tier"></a><span data-ttu-id="68c1e-315">Создание приложения API для размещения на среднем уровне</span><span class="sxs-lookup"><span data-stu-id="68c1e-315">Create an API app to host the middle tier</span></span>
<span data-ttu-id="68c1e-316">Ранее вы [создали приложение API уровня данных и развернули в нем код](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="68c1e-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span></span>  <span data-ttu-id="68c1e-317">Теперь выполните ту же процедуру, чтобы создать приложение API среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="68c1e-317">Now you follow the same procedure for the middle tier API app.</span></span>

1. <span data-ttu-id="68c1e-318">В **обозревателе решений** щелкните правой кнопкой мыши проект ToDoListAPI среднего уровня (не ToDoListDataAPI уровня данных) и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Нажмите кнопку "Опубликовать" в Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="68c1e-320">В мастере **Публикация веб-сайта** на вкладке **Профиль** щелкните **Служба приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="68c1e-321">В диалоговом окне **Служба приложений** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-321">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="68c1e-322">В диалоговом окне **Создание службы приложений** на вкладке **Размещение** примите значение по умолчанию в поле **API App Name** (Имя приложения API) или введите имя, которое будет уникальным в домене *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="68c1e-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="68c1e-323">В поле **Подписка** выберите используемую подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="68c1e-323">Choose the Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="68c1e-324">В раскрывающемся списке **Группа ресурсов** выберите созданную ранее группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="68c1e-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="68c1e-325">В раскрывающемся списке **План службы приложений** выберите созданный ранее план.</span><span class="sxs-lookup"><span data-stu-id="68c1e-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span></span> <span data-ttu-id="68c1e-326">Это значение будет использоваться по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="68c1e-326">It will default to that value.</span></span>
8. <span data-ttu-id="68c1e-327">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-327">Click **Create**.</span></span>
   
    <span data-ttu-id="68c1e-328">Visual Studio создаст приложение API и профиль публикации для него. Кроме того, в мастере **Публикация веб-сайта** отобразится шаг **Подключение**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
9. <span data-ttu-id="68c1e-329">На шаге **Подключение** мастера **Публикации веб-сайта** нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="68c1e-330">Visual Studio развернет проект ToDoListAPI в новом приложении API и откроет в браузере URL-адрес приложения API.</span><span class="sxs-lookup"><span data-stu-id="68c1e-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span></span> <span data-ttu-id="68c1e-331">Откроется страница "Приложение успешно создано".</span><span class="sxs-lookup"><span data-stu-id="68c1e-331">The "successfully created" page appears.</span></span>

## <a name="configure-the-middle-tier-to-call-the-data-tier"></a><span data-ttu-id="68c1e-332">Настройка вызова уровня данных на среднем уровне</span><span class="sxs-lookup"><span data-stu-id="68c1e-332">Configure the middle tier to call the data tier</span></span>
<span data-ttu-id="68c1e-333">Если вызвать приложение API среднего уровня сейчас, оно попытается вызвать уровень данных, используя URL-адрес локального узла, который указан в файле Web.config.</span><span class="sxs-lookup"><span data-stu-id="68c1e-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span></span> <span data-ttu-id="68c1e-334">В этом разделе мы укажем URL-адрес для приложения API уровня данных в параметре среды в приложении API среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="68c1e-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span></span> <span data-ttu-id="68c1e-335">Когда код в приложении API среднего уровня получает URL-адрес уровня данных, параметр среды перезаписывает значение в файле Web.config.</span><span class="sxs-lookup"><span data-stu-id="68c1e-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span></span>

1. <span data-ttu-id="68c1e-336">Перейдите на [портал Azure](https://portal.azure.com/)и откройте колонку **Приложение API** для приложения API, созданного для размещения проекта TodoListAPI (приложение среднего уровня).</span><span class="sxs-lookup"><span data-stu-id="68c1e-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="68c1e-337">В колонке **Параметры** приложения API щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-337">In the API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="68c1e-338">Прокрутите колонку **Параметры приложения** вниз до раздела **Параметры приложения** и добавьте следующие ключ и значение.</span><span class="sxs-lookup"><span data-stu-id="68c1e-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span></span> <span data-ttu-id="68c1e-339">Необходимо указать URL-адрес первого приложения API, опубликованного при работе с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="68c1e-339">The value will be the URL of the first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="68c1e-340">**Ключ**</span><span class="sxs-lookup"><span data-stu-id="68c1e-340">**Key**</span></span> | <span data-ttu-id="68c1e-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="68c1e-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="68c1e-342">**Значение**</span><span class="sxs-lookup"><span data-stu-id="68c1e-342">**Value**</span></span> |<span data-ttu-id="68c1e-343">https://{имя приложения API уровня данных}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="68c1e-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="68c1e-344">**Пример**</span><span class="sxs-lookup"><span data-stu-id="68c1e-344">**Example**</span></span> |<span data-ttu-id="68c1e-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="68c1e-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="68c1e-346">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-346">Click **Save**.</span></span>
   
    ![Нажмите кнопку "Сохранить" в колонке "Параметры приложения"](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="68c1e-348">Если код выполняется в среде Azure, это значение теперь будет переопределять URL-адрес локального узла, который находится в файле Web.config.</span><span class="sxs-lookup"><span data-stu-id="68c1e-348">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="68c1e-349">Тест</span><span class="sxs-lookup"><span data-stu-id="68c1e-349">Test</span></span>
1. <span data-ttu-id="68c1e-350">В окне браузера перейдите по URL-адресу нового приложения API среднего уровня, созданного для ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="68c1e-350">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="68c1e-351">Для этого на портале в главной колонке приложения API щелкните этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="68c1e-351">You can get there by clicking the URL in the API app's main blade in the portal.</span></span>
2. <span data-ttu-id="68c1e-352">В адресной строке браузера добавьте swagger в URL-адрес и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="68c1e-352">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="68c1e-353">(URL-адрес — `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="68c1e-353">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="68c1e-354">В браузере появится тот же пользовательский интерфейс Swagger, который мы уже видели в проекте ToDoListDataAPI. В этот раз поле `owner` не является обязательным для операции Get, так как приложение API среднего уровня автоматически отправляет это значение в приложение API уровня данных.</span><span class="sxs-lookup"><span data-stu-id="68c1e-354">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span></span> <span data-ttu-id="68c1e-355">(В руководствах по проверке подлинности приложение среднего уровня будет отправлять для параметра `owner` фактические идентификаторы пользователей. Сейчас вместо значения этого параметра отображается звездочка.)</span><span class="sxs-lookup"><span data-stu-id="68c1e-355">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="68c1e-356">Попробуйте применить метод GET и другие методы, чтобы убедиться, что приложение API среднего уровня успешно вызывает приложение API уровня данных.</span><span class="sxs-lookup"><span data-stu-id="68c1e-356">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span></span>
   
    ![Метод Get пользовательского интерфейса Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="68c1e-358">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="68c1e-358">Troubleshooting</span></span>
<span data-ttu-id="68c1e-359">Если в ходе выполнения инструкций этого руководства возникнут проблемы, можно воспользоваться рекомендациями по устранению неполадок ниже:</span><span class="sxs-lookup"><span data-stu-id="68c1e-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="68c1e-360">Убедитесь, что используется последняя версия пакета [Azure SDK для .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="68c1e-360">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="68c1e-361">Имена двух проектов похожи (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="68c1e-361">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="68c1e-362">Если результаты вашей работы выглядят не так, как описано в инструкциях, убедитесь, что вы открыли правильный проект.</span><span class="sxs-lookup"><span data-stu-id="68c1e-362">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span></span>
* <span data-ttu-id="68c1e-363">Если вы работаете в корпоративной сети и пытаетесь развернуть службу приложений Azure через брандмауэр, убедитесь, что порты 443 и 8172 открыты для веб-развертывания.</span><span class="sxs-lookup"><span data-stu-id="68c1e-363">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="68c1e-364">Если не удается открыть эти порты, можно использовать другие способы развертывания.</span><span class="sxs-lookup"><span data-stu-id="68c1e-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="68c1e-365">Дополнительные сведения см. в статье [Развертывание приложения в службе приложений Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="68c1e-365">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="68c1e-366">Ошибки "Имена маршрутов должны быть уникальными" могут возникнуть, если вы случайно развернули в приложении API неправильный проект, а затем правильный.</span><span class="sxs-lookup"><span data-stu-id="68c1e-366">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span></span> <span data-ttu-id="68c1e-367">Чтобы устранить эту проблему, повторно разверните правильный проект в приложении API. В мастере **Публикация веб-сайта** на вкладке **Параметры** установите флажок **Удалять дополнительные файлы в месте назначения**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-367">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="68c1e-368">Запустив приложение API ASP.NET в службе приложений Azure, можно узнать больше о функциях Visual Studio, которые упрощают устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="68c1e-368">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="68c1e-369">Сведения о ведении журналов, удаленной отладке и другую информацию см. в статье [Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="68c1e-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68c1e-370">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68c1e-370">Next steps</span></span>
<span data-ttu-id="68c1e-371">Вы узнали, как развертывать существующие проекты веб-API в приложениях API, создавать клиентский код для приложений API и использовать эти приложения из клиентов .NET.</span><span class="sxs-lookup"><span data-stu-id="68c1e-371">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="68c1e-372">В следующем руководстве из этой серии показано, как [использовать приложения API в клиентах JavaScript с помощью CORS](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="68c1e-372">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="68c1e-373">Дополнительные сведения о создании клиентского кода см. в репозитории [Azure/AutoRest](https://github.com/azure/autorest) на сайте GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="68c1e-373">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span></span> <span data-ttu-id="68c1e-374">Чтобы получить сведения о проблемах, связанных с созданным клиентом, [опубликуйте вопрос о проблеме в репозитории AutoRest](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="68c1e-374">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="68c1e-375">Если нужно создать проекты приложений API с нуля, используйте шаблон **приложения API Azure** .</span><span class="sxs-lookup"><span data-stu-id="68c1e-375">If you want to create new API app projects from scratch, use the **Azure API App** template.</span></span>

![Шаблон приложения API в Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="68c1e-377">После выбора шаблона ASP.NET 4.5.2 **Пустой**, установки флажка добавления поддержки веб-API и пакета NuGet Swashbuckle результат будет таким же, как и при выборе шаблона проекта **Приложение API Azure**.</span><span class="sxs-lookup"><span data-stu-id="68c1e-377">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span></span> <span data-ttu-id="68c1e-378">Но в этот шаблон добавлен еще код конфигурации Swashbuckle, который не позволяет создавать повторяющиеся идентификаторы операций Swagger.</span><span class="sxs-lookup"><span data-stu-id="68c1e-378">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="68c1e-379">Создав проект приложения API, его можно развернуть в приложении API так же, как показано в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="68c1e-379">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span></span>

