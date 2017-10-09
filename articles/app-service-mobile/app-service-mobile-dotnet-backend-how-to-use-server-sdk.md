---
title: "toowork aaaHow с сервера базы данных hello .NET SDK для мобильных приложений | Документы Microsoft"
description: "Узнайте, как toowork с hello внутреннего сервера .NET SDK для мобильных приложений службы приложения Azure."
keywords: "служба приложений, служба приложений azure, мобильное приложение, мобильная служба, масштабировать, масштабируемый, разработка приложений, разработка приложений azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="04349-104">Работать с сервера базы данных hello .NET SDK для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="04349-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="04349-105">В этом разделе показано, как toouse hello внутреннему серверу .NET SDK в основные сценарии мобильные приложения службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="04349-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="04349-106">пакет SDK Azure Mobile приложения Hello предназначенный для работы с мобильными клиентами из приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="04349-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="04349-107">Hello [сервер .NET SDK для мобильных приложений Azure] [ 2] является открытым исходным кодом на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="04349-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="04349-108">репозиторий Hello содержит все исходного кода, включая набор модульных тестов hello всего сервера SDK и некоторые образцы проектов.</span><span class="sxs-lookup"><span data-stu-id="04349-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="04349-109">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="04349-109">Reference documentation</span></span>
<span data-ttu-id="04349-110">Hello справочную документацию по SDK сервера hello находится здесь: [Справочник по Azure мобильных приложений .NET][1].</span><span class="sxs-lookup"><span data-stu-id="04349-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="04349-111"><a name="create-app"></a>Практическое руководство. Создание серверной части мобильного приложения .NET</span><span class="sxs-lookup"><span data-stu-id="04349-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="04349-112">При запуске нового проекта, можно создать приложение службы приложений с помощью либо hello [портал Azure] или Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04349-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="04349-113">Можно выполнить локально hello приложения служб приложений или опубликовать hello проекта tooyour облачного приложения-службы мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="04349-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="04349-114">При добавлении существующего проекта tooan возможности мобильных устройств в разделе hello [загрузки и инициализации hello SDK](#install-sdk) раздела.</span><span class="sxs-lookup"><span data-stu-id="04349-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="04349-115">Создание серверной части .NET с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="04349-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="04349-116">toocreate мобильного внутреннего сервера приложения службы, либо выполните hello [учебника] [ 3] или выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="04349-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="04349-117">В hello *приступить к работе* колонки в разделе **создать таблицу API**, выберите **C#** как вашей **языка серверной**.</span><span class="sxs-lookup"><span data-stu-id="04349-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="04349-118">Нажмите кнопку **загрузки**извлечения локального компьютера проекта сжатые файлы tooyour и откройте решение hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04349-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="04349-119">Создание серверной части .NET с помощью Visual Studio 2013 и Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="04349-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="04349-120">Установка hello [Azure SDK для .NET] [ 4] (версии 2.9.0 или более поздней версии) toocreate проект мобильных приложений Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04349-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="04349-121">После установки пакета SDK для hello создайте приложения ASP.NET, используя hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="04349-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="04349-122">Откройте hello **новый проект** диалоговое окно (из *файл* > **New** > **проект...** ).</span><span class="sxs-lookup"><span data-stu-id="04349-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="04349-123">Разверните раздел **Шаблоны** > **Visual C#** и выберите **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="04349-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="04349-124">Выберите **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="04349-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="04349-125">Введите имя проекта hello.</span><span class="sxs-lookup"><span data-stu-id="04349-125">Fill in hello project name.</span></span> <span data-ttu-id="04349-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="04349-126">Then click **OK**.</span></span>
5. <span data-ttu-id="04349-127">В разделе *ASP.NET 4.5.2 Templates* (Шаблоны ASP.NET 4.5.2) выберите **Мобильное приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="04349-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="04349-128">Проверьте **узлов в облаке hello** toocreate мобильной серверной части в hello облако toowhich, можно опубликовать этот проект.</span><span class="sxs-lookup"><span data-stu-id="04349-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="04349-129">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="04349-129">Click **OK**.</span></span>

## <span data-ttu-id="04349-130"><a name="install-sdk"></a>Как: загрузка и инициализация hello SDK</span><span class="sxs-lookup"><span data-stu-id="04349-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="04349-131">Hello пакет SDK доступен на [NuGet.org]. Этот пакет содержит базовые функциональные возможности, необходимые tooget hello, работы с использованием пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="04349-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="04349-132">tooinitialize Здравствуйте SDK, необходимо tooperform действий над hello **HttpConfiguration** объекта.</span><span class="sxs-lookup"><span data-stu-id="04349-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="04349-133">Установка пакета SDK для hello</span><span class="sxs-lookup"><span data-stu-id="04349-133">Install hello SDK</span></span>
<span data-ttu-id="04349-134">hello tooinstall SDK, щелкните правой кнопкой мыши проект сервера hello в Visual Studio выберите **управление пакетами NuGet**, поиск hello [Microsoft.Azure.Mobile.Server] пакета, а затем нажмите кнопку  **Установить**.</span><span class="sxs-lookup"><span data-stu-id="04349-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="04349-135"><a name="server-project-setup"></a>Инициализировать проект сервера hello</span><span class="sxs-lookup"><span data-stu-id="04349-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="04349-136">Сервер серверного проекта .NET — инициализированный аналогичные проекты tooother ASP.NET, включая класс запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="04349-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="04349-137">Убедитесь, что ссылка на пакет NuGet hello `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="04349-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="04349-138">tooadd этого класса в Visual Studio, щелкните правой кнопкой мыши проект сервера и выберите **добавить** >
**новый элемент**, затем **Web**  >  ** Общие** > **запуска OWIN класса**.</span><span class="sxs-lookup"><span data-stu-id="04349-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="04349-139">Класс создается hello следующий атрибут:</span><span class="sxs-lookup"><span data-stu-id="04349-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="04349-140">В hello `Configuration()` метод класса запуска OWIN, используйте **HttpConfiguration** объекта tooconfigure hello мобильных приложений Azure среды.</span><span class="sxs-lookup"><span data-stu-id="04349-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="04349-141">Следующий пример Hello инициализирует проект сервера hello без добавленных функций:</span><span class="sxs-lookup"><span data-stu-id="04349-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="04349-142">tooenable отдельные компоненты, необходимо вызывать методы расширения для hello **MobileAppConfiguration** объект перед вызовом **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="04349-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="04349-143">Например, hello, следующий код добавляет по умолчанию hello направляет tooall API контроллерами, имеющими атрибут hello `[MobileAppController]` во время инициализации:</span><span class="sxs-lookup"><span data-stu-id="04349-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="04349-144">Быстрый запуск сервера Hello из hello Azure портала вызовы **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="04349-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="04349-145">Это эквивалент toohello после завершения программы установки:</span><span class="sxs-lookup"><span data-stu-id="04349-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="04349-146">методы расширения Hello, используемые являются:</span><span class="sxs-lookup"><span data-stu-id="04349-146">hello extension methods used are:</span></span>

* <span data-ttu-id="04349-147">`AddMobileAppHomeController()`предоставляет Домашняя страница мобильных приложений Azure по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="04349-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="04349-148">`MapApiControllers()`предоставляет возможности пользовательского интерфейса API для контроллеров WebAPI декорированных hello `[MobileAppController]` атрибута.</span><span class="sxs-lookup"><span data-stu-id="04349-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="04349-149">`AddTables()`содержит сопоставления hello `/tables` tootable контроллеров конечных точек.</span><span class="sxs-lookup"><span data-stu-id="04349-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="04349-150">`AddTablesWithEntityFramework()`является собирательным для сопоставления hello `/tables` конечные точки, использующие Entity Framework на основе контроллеров.</span><span class="sxs-lookup"><span data-stu-id="04349-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="04349-151">`AddPushNotifications()` предоставляет простой способ регистрации устройств в концентраторах уведомлений.</span><span class="sxs-lookup"><span data-stu-id="04349-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="04349-152">`MapLegacyCrossDomainController()` предоставляет стандартные заголовки CORS для локальной разработки.</span><span class="sxs-lookup"><span data-stu-id="04349-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="04349-153">Расширения пакета SDK</span><span class="sxs-lookup"><span data-stu-id="04349-153">SDK extensions</span></span>
<span data-ttu-id="04349-154">следующие пакеты NuGet основе расширений Hello предоставляют различные возможности мобильных устройств, используемых приложением.</span><span class="sxs-lookup"><span data-stu-id="04349-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="04349-155">Включить расширения во время инициализации с помощью hello **MobileAppConfiguration** объекта.</span><span class="sxs-lookup"><span data-stu-id="04349-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="04349-156">[Microsoft.Azure.Mobile.Server.Quickstart] поддерживает hello базовая настройка мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="04349-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="04349-157">Добавлены toohello конфигурации путем вызова hello **UseDefaultConfiguration** метод расширения во время инициализации.</span><span class="sxs-lookup"><span data-stu-id="04349-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="04349-158">Это расширение включает в себя следующие расширения: пакеты Notifications, Authentication, Entity, Tables, Crossdomain и Home.</span><span class="sxs-lookup"><span data-stu-id="04349-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="04349-159">Этот пакет используется hello на портал Azure hello быстрый запуск приложений мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="04349-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="04349-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) реализует по умолчанию hello *— это мобильное приложение работает страница* для hello корневого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="04349-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="04349-161">Добавление конфигурации toohello путем вызова **AddMobileAppHomeController** метода расширения.</span><span class="sxs-lookup"><span data-stu-id="04349-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="04349-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) содержит классы для работы с конвейером данных hello данных и наборы вверх.</span><span class="sxs-lookup"><span data-stu-id="04349-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="04349-163">Добавьте конфигурации toohello, вызывающему Привет **AddTables** метода расширения.</span><span class="sxs-lookup"><span data-stu-id="04349-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="04349-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) данные tooaccess Entity Framework hello hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="04349-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="04349-165">Добавьте конфигурации toohello, вызывающему Привет **AddTablesWithEntityFramework** метода расширения.</span><span class="sxs-lookup"><span data-stu-id="04349-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="04349-166">[Microsoft.Azure.Mobile.Server.Authentication] включает проверку подлинности и наборы вверх hello по промежуточного слоя OWIN, как использовать toovalidate токены.</span><span class="sxs-lookup"><span data-stu-id="04349-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="04349-167">Добавьте конфигурации toohello, вызывающему Привет **AddAppServiceAuthentication** и **IAppBuilder**. **UseAppServiceAuthentication** методы расширения.</span><span class="sxs-lookup"><span data-stu-id="04349-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="04349-168">[Microsoft.Azure.Mobile.Server.Notifications] включает push-уведомления и определяет их конечную точку регистрации.</span><span class="sxs-lookup"><span data-stu-id="04349-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="04349-169">Добавьте конфигурации toohello, вызывающему Привет **AddPushNotifications** метода расширения.</span><span class="sxs-lookup"><span data-stu-id="04349-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="04349-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) будет создан контроллер, выполняющий toolegacy данных веб-браузеров из мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="04349-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="04349-171">Добавление конфигурации toohello путем вызова **MapLegacyCrossDomainController** метода расширения.</span><span class="sxs-lookup"><span data-stu-id="04349-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="04349-172">[Microsoft.Azure.Mobile.Server.Login] предоставляет метод AppServiceLoginHandler.CreateToken() hello, который представляет собой статический метод, используемый при выполнении сценариев нестандартной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="04349-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="04349-173"><a name="publish-server-project"></a>Как: публикации проекта сервера hello</span><span class="sxs-lookup"><span data-stu-id="04349-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="04349-174">В этом разделе показано, как toopublish серверной части .NET из проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04349-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="04349-175">Можно также развернуть проект базы данных с использованием Git или любой из hello других методов, описанных в hello [документации по развертыванию службы приложений Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="04349-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="04349-176">В Visual Studio перестройте пакетов NuGet toorestore hello проекта.</span><span class="sxs-lookup"><span data-stu-id="04349-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="04349-177">В обозревателе решений щелкните правой кнопкой мыши проект hello, нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="04349-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="04349-178">Hello публикации, при первом запуске необходимо toodefine профиль публикации.</span><span class="sxs-lookup"><span data-stu-id="04349-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="04349-179">Если профиль уже определен, выделите его и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="04349-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="04349-180">При получении запроса tooselect место назначения публикации, нажмите кнопку **службу приложений Microsoft Azure** > **Далее**, а затем (при необходимости) войти, используя свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="04349-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="04349-181">Visual Studio загрузит параметры публикации из Azure и безопасно сохранит их.</span><span class="sxs-lookup"><span data-stu-id="04349-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="04349-182">Выберите свою **подписку**, а затем в раскрывающемся списке **Представление** выберите **Тип ресурса**, разверните **Мобильное приложение** и щелкните серверную часть мобильного приложения. После этого нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="04349-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="04349-183">Проверьте hello сведения профиля публикации и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="04349-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="04349-184">При успешной публикации серверной части мобильного приложения отобразится соответствующая целевая страница.</span><span class="sxs-lookup"><span data-stu-id="04349-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="04349-185"><a name="define-table-controller"></a> Практическое руководство. Определение контроллера таблиц</span><span class="sxs-lookup"><span data-stu-id="04349-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="04349-186">Определите tooexpose контроллер таблиц клиенты toomobile таблицы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="04349-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="04349-187">Настройка контроллера таблиц состоит из трех шагов.</span><span class="sxs-lookup"><span data-stu-id="04349-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="04349-188">Создание класса объекта передачи данных.</span><span class="sxs-lookup"><span data-stu-id="04349-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="04349-189">Настройте ссылку на таблицу в hello класс Mobile DbContext.</span><span class="sxs-lookup"><span data-stu-id="04349-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="04349-190">Создание контроллера таблиц.</span><span class="sxs-lookup"><span data-stu-id="04349-190">Create a table controller.</span></span>

<span data-ttu-id="04349-191">Объект передачи данных — это обычный объект C#, наследуемый от `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="04349-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="04349-192">Например:</span><span class="sxs-lookup"><span data-stu-id="04349-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="04349-193">Hello DTO — используется toodefine hello таблицы в базе данных SQL hello.</span><span class="sxs-lookup"><span data-stu-id="04349-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="04349-194">toocreate hello входа базы данных, добавьте `DbSet<>` свойства hello DbContext, вы используете.</span><span class="sxs-lookup"><span data-stu-id="04349-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="04349-195">В шаблоне проекта по умолчанию hello для мобильных приложений Azure, hello DbContext называется `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="04349-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="04349-196">Если установлен пакет SDK Azure приветствия, вы теперь можно создать контроллер шаблон таблицы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04349-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="04349-197">Щелкните правой кнопкой мыши папку Controllers hello и выберите **добавить** > **контроллера...** .</span><span class="sxs-lookup"><span data-stu-id="04349-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="04349-198">Выберите hello **контроллер таблицы Azure мобильных приложений** параметр, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="04349-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="04349-199">В hello **добавить контроллер** диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="04349-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="04349-200">В hello **класс модели** раскрывающийся список, выберите ваш новый DTO.</span><span class="sxs-lookup"><span data-stu-id="04349-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="04349-201">В hello **DbContext** раскрывающийся список, класс DbContext службы Mobile выберите hello.</span><span class="sxs-lookup"><span data-stu-id="04349-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="04349-202">имя контроллера Hello создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="04349-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="04349-203">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="04349-203">Click **Add**.</span></span>

<span data-ttu-id="04349-204">проект сервера Hello краткое руководство содержит пример для простой **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="04349-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="04349-205"><a name="adjust-pagesize"></a>Как: размер подкачки hello таблицы</span><span class="sxs-lookup"><span data-stu-id="04349-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="04349-206">По умолчанию мобильные приложения Azure выдают по 50 записей на запрос.</span><span class="sxs-lookup"><span data-stu-id="04349-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="04349-207">Разбиение на страницы гарантирует, что этот клиент hello не связывать их пользовательского интерфейса потока ни hello сервер слишком долго, обеспечивая эффективное взаимодействие с пользователем.</span><span class="sxs-lookup"><span data-stu-id="04349-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="04349-208">размер разбиение по страницам таблицы toochange hello, размер запроса стороны сервера hello увеличение «разрешено» и hello страницы на стороне клиента размер hello серверной «допустимый размер запроса» настраивается с помощью hello `EnableQuery` атрибута:</span><span class="sxs-lookup"><span data-stu-id="04349-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="04349-209">Убедитесь, что hello PageSize hello же или больше, чем размер hello, необходимая для клиента hello.</span><span class="sxs-lookup"><span data-stu-id="04349-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="04349-210">Дополнительную информацию по изменению размера страницы приветствия клиента см. в документации HOWTO toohello конкретного клиента.</span><span class="sxs-lookup"><span data-stu-id="04349-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="04349-211">Практическое руководство. Определение настраиваемого контроллера API</span><span class="sxs-lookup"><span data-stu-id="04349-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="04349-212">Hello пользовательского API устройства предоставляет hello основные функциональные возможности tooyour мобильного внутреннего сервера приложения путем предоставления конечной точки.</span><span class="sxs-lookup"><span data-stu-id="04349-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="04349-213">Можно зарегистрировать контроллер API зависящие от мобильных устройств, с помощью атрибута [MobileAppController] hello.</span><span class="sxs-lookup"><span data-stu-id="04349-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="04349-214">Hello `MobileAppController` атрибут регистрирует маршрут hello, настраивает сериализатор JSON мобильного приложения hello и включает [проверке версии](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="04349-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="04349-215">В Visual Studio, щелкните правой кнопкой мыши hello контроллеров папка, а затем нажмите **добавить** > **контроллера**выберите **Web API 2 контроллера&mdash;пустой** и Нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="04349-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="04349-216">Укажите **имя контроллера**, например `CustomController`, и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="04349-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="04349-217">В hello новый файл класса контроллера, добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="04349-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="04349-218">Применить hello **[MobileAppController]** определения класса контроллера toohello API, как следующий пример hello атрибута:</span><span class="sxs-lookup"><span data-stu-id="04349-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="04349-219">Добавьте в файл App_Start/Startup.MobileApp.cs toohello вызов **MapApiControllers** методом расширения, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="04349-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="04349-220">Можно также использовать hello `UseDefaultConfiguration()` расширения вместо метода `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="04349-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="04349-221">Клиенты могут получить доступ к любому контроллеру, к которому не применен атрибут **MobileAppControllerAttribute**. Однако клиенты, использующие любой пакет SDK для клиента мобильного приложения, не смогут правильно использовать этот контроллер.</span><span class="sxs-lookup"><span data-stu-id="04349-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="04349-222">Практическое руководство: работа с проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="04349-222">How to: Work with authentication</span></span>
<span data-ttu-id="04349-223">Мобильные приложения Azure использует проверку подлинности службы для приложения / toosecure авторизации серверной части мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="04349-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="04349-224">В этом разделе показано, как hello tooperform следующие задачи, связанные с проверки подлинности в проекте .NET внутреннего сервера:</span><span class="sxs-lookup"><span data-stu-id="04349-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="04349-225">Способ: добавить проект сервера tooa проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="04349-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="04349-226">Практическое руководство. Использование пользовательской проверки подлинности для приложения</span><span class="sxs-lookup"><span data-stu-id="04349-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="04349-227">Практическое руководство. Получение сведений о пользователе, прошедшем проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="04349-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="04349-228">Практическое руководство. Ограничение доступа к данным для авторизованных пользователей</span><span class="sxs-lookup"><span data-stu-id="04349-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="04349-229"><a name="add-auth"></a>Способ: добавить проект сервера tooa проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="04349-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="04349-230">Проект сервера tooyour проверки подлинности можно расширить за счет hello **MobileAppConfiguration** объекта и настройки по промежуточного слоя OWIN.</span><span class="sxs-lookup"><span data-stu-id="04349-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="04349-231">При установке hello [Microsoft.Azure.Mobile.Server.Quickstart] пакета и вызова hello **UseDefaultConfiguration** метод расширения, можно пропустить toostep 3.</span><span class="sxs-lookup"><span data-stu-id="04349-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="04349-232">В Visual Studio, установите hello [Microsoft.Azure.Mobile.Server.Authentication] пакета.</span><span class="sxs-lookup"><span data-stu-id="04349-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="04349-233">Добавьте в файл проекта файла Startup.cs hello hello, следующей строкой кода в начале hello hello **конфигурации** метод:</span><span class="sxs-lookup"><span data-stu-id="04349-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="04349-234">Этот компонент по промежуточного слоя OWIN проверки токенов, выданных hello связанного приложения службы шлюза.</span><span class="sxs-lookup"><span data-stu-id="04349-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="04349-235">Добавить hello `[Authorize]` атрибута tooany контроллеру или методу, который требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="04349-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="04349-236">toolearn о том, как клиенты tooauthenticate tooyour внутренней мобильные приложения, см. [приложение tooyour authentication добавить](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="04349-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="04349-237"><a name="custom-auth"></a>Практическое руководство. Использование пользовательской проверки подлинности для приложения</span><span class="sxs-lookup"><span data-stu-id="04349-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="04349-238">Если toouse одного из поставщиков проверки подлинности и авторизации службы приложения hello не готовы, можно реализовать собственную систему для имени входа.</span><span class="sxs-lookup"><span data-stu-id="04349-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="04349-239">Установка hello [Microsoft.Azure.Mobile.Server.Login] пакета tooassist с создания токенов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="04349-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="04349-240">Предоставьте свой собственный код для проверки учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="04349-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="04349-241">Например, можно выполнять проверку с помощью дополненных случайными данными и хэшированных паролей в базе данных.</span><span class="sxs-lookup"><span data-stu-id="04349-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="04349-242">В следующем примере hello, hello `isValidAssertion()` метод (определенный в другом месте) отвечает за эти проверки.</span><span class="sxs-lookup"><span data-stu-id="04349-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="04349-243">Нестандартная проверка подлинности Hello предоставляется путем создания ApiController и предоставление доступа к `register` и `login` действия.</span><span class="sxs-lookup"><span data-stu-id="04349-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="04349-244">Hello клиенту следует использовать пользовательские данные пользовательского интерфейса toocollect hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="04349-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="04349-245">Hello сведения можно затем вызвать отправленной toohello API с помощью стандартных HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="04349-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="04349-246">После hello server проверяет утверждения hello, выдает маркер с помощью hello `AppServiceLoginHandler.CreateToken()` метод.</span><span class="sxs-lookup"><span data-stu-id="04349-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="04349-247">Hello ApiController **не должны** использовать hello `[MobileAppController]` атрибута.</span><span class="sxs-lookup"><span data-stu-id="04349-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="04349-248">Пример действия `login` :</span><span class="sxs-lookup"><span data-stu-id="04349-248">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="04349-249">В предыдущих пример hello LoginResult и LoginResultUser являются сериализуемые объекты, содержащие необходимые свойства.</span><span class="sxs-lookup"><span data-stu-id="04349-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="04349-250">Hello клиент ожидает ответы toobe входа, возвращаются в виде объектов JSON hello формы:</span><span class="sxs-lookup"><span data-stu-id="04349-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="04349-251">Hello `AppServiceLoginHandler.CreateToken()` метод включает *аудитории* и *издателя* параметра.</span><span class="sxs-lookup"><span data-stu-id="04349-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="04349-252">Оба этих параметра задаются toohello URL-адрес корневой каталог приложения с помощью hello схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="04349-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="04349-253">Аналогично следует задать *secretKey* toobe hello значение приложении подписывающий ключ.</span><span class="sxs-lookup"><span data-stu-id="04349-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="04349-254">Не распространяйте hello ключ в клиенте подписи, как можно использовать toomint ключи и олицетворять пользователей.</span><span class="sxs-lookup"><span data-stu-id="04349-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="04349-255">Вы можете получить ключ во время размещенных в службе приложений с помощью ссылки на hello подписи hello *веб-САЙТ\_AUTH\_ПОДПИСЫВАНИЕ\_ключ* переменной среды.</span><span class="sxs-lookup"><span data-stu-id="04349-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="04349-256">При необходимости в локальном контексте, отладки, следуйте инструкциям hello hello [локальной отладки с использованием проверки подлинности](#local-debug) статьи tooretrieve hello ключ и сохранить ее в качестве параметра приложения.</span><span class="sxs-lookup"><span data-stu-id="04349-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="04349-257">Hello выданный маркер может также включать другие утверждения и дату окончания действия.</span><span class="sxs-lookup"><span data-stu-id="04349-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="04349-258">Как минимум, hello выданный маркер должен включать тему (**sub**) утверждения.</span><span class="sxs-lookup"><span data-stu-id="04349-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="04349-259">Может поддерживать стандартную клиентскую hello `loginAsync()` метод путем перегрузки hello способа проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="04349-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="04349-260">Если клиент hello вызывает `client.loginAsync('custom');` toolog в маршрута должно быть `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="04349-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="04349-261">Можно задать hello маршрут для hello контроллер нестандартной проверки подлинности с помощью `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="04349-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="04349-262">С помощью hello `loginAsync()` подход гарантирует присоединен этот маркер проверки подлинности hello tooevery последующий вызов toohello службы.</span><span class="sxs-lookup"><span data-stu-id="04349-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="04349-263"><a name="user-info"></a>Практическое руководство. Получение сведений о пользователе, прошедшем проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="04349-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="04349-264">При проверке подлинности пользователя службой приложений можно получить доступ к hello назначенный идентификатор пользователя и другие сведения в свой код серверной части .NET.</span><span class="sxs-lookup"><span data-stu-id="04349-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="04349-265">сведения о пользователе Hello можно использовать для принятия решения об авторизации в серверном hello.</span><span class="sxs-lookup"><span data-stu-id="04349-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="04349-266">Hello следующий код получает идентификатор пользователя hello, связанный с запросом:</span><span class="sxs-lookup"><span data-stu-id="04349-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="04349-267">Hello SID является производным от ИД пользователя поставщика hello и статический объект для указанного пользователя и поставщик входа в систему.</span><span class="sxs-lookup"><span data-stu-id="04349-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="04349-268">Hello SID имеет значение null для маркеров недействительная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="04349-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="04349-269">Кроме того, служба приложений позволяет запрашивать конкретные утверждения от поставщика входа в систему.</span><span class="sxs-lookup"><span data-stu-id="04349-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="04349-270">Каждый поставщик удостоверений может предоставлять больше сведений с помощью пакета SDK поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="04349-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="04349-271">Например можно использовать hello Facebook Graph API сведения друзей.</span><span class="sxs-lookup"><span data-stu-id="04349-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="04349-272">Можно указать утверждения, которые запрашиваются в колонке поставщика hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="04349-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="04349-273">Некоторые утверждения требуют дополнительной настройки с помощью поставщика удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="04349-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="04349-274">Hello следующий код вызывает hello **GetAppServiceIdentityAsync** расширение метода tooget hello учетные данные входа, включая hello запросов маркера необходимые toomake доступ к hello Facebook Graph API:</span><span class="sxs-lookup"><span data-stu-id="04349-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="04349-275">Добавить с помощью инструкции для `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** метода расширения.</span><span class="sxs-lookup"><span data-stu-id="04349-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="04349-276"><a name="authorize"></a>Практическое руководство. Ограничение доступа к данным для авторизованных пользователей</span><span class="sxs-lookup"><span data-stu-id="04349-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="04349-277">В предыдущем разделе hello мы показали, как tooretrieve hello идентификатор пользователя, прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="04349-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="04349-278">Вы можете ограничить доступ toodata и другие ресурсы, на основе этого значения.</span><span class="sxs-lookup"><span data-stu-id="04349-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="04349-279">Например добавление столбца userId tootables и фильтрация результатов запроса hello по Идентификатору пользователя hello — toolimit удобное средство, возвращаются только пользователи tooauthorized данных.</span><span class="sxs-lookup"><span data-stu-id="04349-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="04349-280">Hello следующий код возвращает строки данных только в том случае, если hello SID соответствует значению в столбце таблицы TodoItem hello UserId hello:</span><span class="sxs-lookup"><span data-stu-id="04349-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="04349-281">Hello `Query()` возвращает метод `IQueryable` , можно управлять с помощью фильтрации toohandle LINQ.</span><span class="sxs-lookup"><span data-stu-id="04349-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="04349-282">Способ: добавить проект сервера tooa уведомлений push</span><span class="sxs-lookup"><span data-stu-id="04349-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="04349-283">Добавление push уведомления tooyour server проекта, расширяя hello **MobileAppConfiguration** объекта и создание концентраторов уведомлений клиента.</span><span class="sxs-lookup"><span data-stu-id="04349-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="04349-284">В Visual Studio, щелкните правой кнопкой мыши проект сервера hello и нажмите кнопку **управление пакетами NuGet**, поиск `Microsoft.Azure.Mobile.Server.Notifications`, нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="04349-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="04349-285">Повторите этот шаг tooinstall hello `Microsoft.Azure.NotificationHubs` пакет, который включает клиентскую библиотеку hello концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="04349-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="04349-286">В App_Start/Startup.MobileApp.cs и добавьте toohello вызов **AddPushNotifications()** метод расширения во время инициализации:</span><span class="sxs-lookup"><span data-stu-id="04349-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="04349-287">Добавьте следующий код, который создает клиент, концентраторы уведомлений hello:</span><span class="sxs-lookup"><span data-stu-id="04349-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="04349-288">Теперь можно использовать hello концентраторы уведомлений клиента toosend принудительной уведомления tooregistered устройств.</span><span class="sxs-lookup"><span data-stu-id="04349-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="04349-289">Дополнительные сведения см. в разделе [уведомления tooyour добавить push приложения](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="04349-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="04349-290">toolearn Дополнительные сведения о концентраторах уведомлений см [Обзор концентраторов уведомлений](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04349-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="04349-291"><a name="tags"></a>Практическое руководство. Включение принудительной отправки push-уведомлений с использованием тегов</span><span class="sxs-lookup"><span data-stu-id="04349-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="04349-292">Концентраторы уведомлений позволяет отправлять уведомления о целевых toospecific регистрации с помощью тегов.</span><span class="sxs-lookup"><span data-stu-id="04349-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="04349-293">Несколько тегов создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="04349-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="04349-294">Hello код установки идентифицирует определенное устройство.</span><span class="sxs-lookup"><span data-stu-id="04349-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="04349-295">Hello идентификатор пользователя на основе проверки подлинности hello ИД безопасности определяет конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="04349-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="04349-296">Здравствуйте, установки, код может осуществляться из hello **installationId** свойство hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="04349-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="04349-297">Hello в примере показано использование tooadd идентификатор установки конкретного экземпляра tooa тег в концентраторах уведомлений:</span><span class="sxs-lookup"><span data-stu-id="04349-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="04349-298">При создании hello установки серверной hello игнорируются все теги, полученных от клиента hello во время регистрации push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="04349-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="04349-299">tooenable tooadd клиента теги toohello установки, необходимо создать пользовательский API, который добавляет теги с помощью hello предшествующий шаблон.</span><span class="sxs-lookup"><span data-stu-id="04349-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="04349-300">В разделе [теги уведомления клиента добавлены принудительной] [ 5] в hello мобильные приложения службы приложений завершенного примеров использования в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="04349-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="04349-301"><a name="push-user"></a>Как: tooan уведомления принудительной отправки, проверку подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="04349-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="04349-302">Когда прошедший проверку пользователь регистрируется для push-уведомлений, тег ИД пользователя автоматически добавляется toohello регистрации.</span><span class="sxs-lookup"><span data-stu-id="04349-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="04349-303">Используя этот тег, вы можете отправлять push уведомления tooall устройств, зарегистрированных этим пользователем.</span><span class="sxs-lookup"><span data-stu-id="04349-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="04349-304">Hello следующий код возвращает hello идентификатор SID пользователя, выполняющего запрос и отправляет шаблон регистрации push-уведомлений tooevery устройства пользователем:</span><span class="sxs-lookup"><span data-stu-id="04349-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="04349-305">При регистрации для работы с push-уведомлениями на клиенте, прошедшем проверку подлинности, убедитесь, что проверка подлинности завершена, и только после этого начинайте регистрацию.</span><span class="sxs-lookup"><span data-stu-id="04349-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="04349-306">Дополнительные сведения см. в разделе [Push toousers] [ 6] в hello мобильные приложения службы приложений завершенного примеров для серверного приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="04349-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="04349-307">Как: отладки и устранения неполадок hello Server .NET SDK</span><span class="sxs-lookup"><span data-stu-id="04349-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="04349-308">Служба приложений Azure предоставляет несколько методов отладки и устранения неполадок в приложениях ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="04349-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="04349-309">Мониторинг службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="04349-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="04349-310">Включение ведения журналов диагностики в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="04349-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="04349-311">Диагностика службы приложений Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04349-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="04349-312">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="04349-312">Logging</span></span>
<span data-ttu-id="04349-313">Журналы диагностики службы tooApp можно создавать с помощью hello Стандартная ASP.NET трассировки записи.</span><span class="sxs-lookup"><span data-stu-id="04349-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="04349-314">Перед написанием toohello журналы диагностики необходимо включить в серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="04349-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="04349-315">журналы toohello по tooenable диагностики и записи:</span><span class="sxs-lookup"><span data-stu-id="04349-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="04349-316">Следуйте указаниям hello [как диагностики tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="04349-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="04349-317">Добавьте следующее hello с помощью оператора в файл кода:</span><span class="sxs-lookup"><span data-stu-id="04349-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="04349-318">Создайте toowrite записи трассировки из hello .NET серверной toohello журналы диагностики, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04349-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="04349-319">Повторная публикация проекта сервера и доступа hello мобильное приложение серверной tooexecute hello путь кода, включив ведение hello.</span><span class="sxs-lookup"><span data-stu-id="04349-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="04349-320">Загрузите и оцените hello журналы, как описано в [как: загрузка журналов](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="04349-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="04349-321"><a name="local-debug"></a>Локальная отладка с проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="04349-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="04349-322">Приложение можно запустить локально tootest изменения перед их публикацией toohello облака.</span><span class="sxs-lookup"><span data-stu-id="04349-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="04349-323">Для большинства серверных систем мобильных приложений Azure нажмите клавишу *F5* во время работы в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04349-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="04349-324">Однако при проверке подлинности следует учитывать некоторые дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="04349-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="04349-325">Необходимо иметь облачного мобильное приложение с приложение службы проверки подлинности и авторизации настроены и клиент должен иметь конечную точку облака hello указан как hello альтернативных имен узлов.</span><span class="sxs-lookup"><span data-stu-id="04349-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="04349-326">Hello документации для вашей платформы клиента для hello определенные шаги.</span><span class="sxs-lookup"><span data-stu-id="04349-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="04349-327">Убедитесь, что в мобильном внутреннем сервере установлен пакет [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="04349-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="04349-328">В классе запуска приложения OWIN, добавьте следующее hello после `MobileAppConfiguration` был применен tooyour `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="04349-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="04349-329">В предыдущих пример hello, следует настроить hello *authAudience* и *authIssuer* файла параметров приложения в файл Web.config tooeach быть URL-адрес корневой каталог приложения с помощью hello HTTPS схема.</span><span class="sxs-lookup"><span data-stu-id="04349-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="04349-330">Аналогично следует задать *authSigningKey* toobe hello значение приложении подписывающий ключ.</span><span class="sxs-lookup"><span data-stu-id="04349-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="04349-331">ключ подписывания hello tooobtain:</span><span class="sxs-lookup"><span data-stu-id="04349-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="04349-332">Перейдите tooyour приложения в hello [портал Azure]</span><span class="sxs-lookup"><span data-stu-id="04349-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="04349-333">Щелкните **Инструменты**, **Kudu**, **Перейти**.</span><span class="sxs-lookup"><span data-stu-id="04349-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="04349-334">В узле управления Kudu hello, щелкните **среды**.</span><span class="sxs-lookup"><span data-stu-id="04349-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="04349-335">Найти значение hello *веб-САЙТ\_AUTH\_ПОДПИСЫВАНИЕ\_ключ*.</span><span class="sxs-lookup"><span data-stu-id="04349-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="04349-336">Ключ для hello подписи hello используйте *authSigningKey* параметр в файле config локального приложения.  Серверной части мобильных устройств теперь является токены мощной toovalidate при выполнении локально, какие hello клиент получает маркер hello из конечной точки облачного hello.</span><span class="sxs-lookup"><span data-stu-id="04349-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[портал Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
