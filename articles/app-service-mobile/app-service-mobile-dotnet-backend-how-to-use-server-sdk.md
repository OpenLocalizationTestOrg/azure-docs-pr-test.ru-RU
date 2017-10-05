---
title: "Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений | Документация Майкрософт"
description: "Узнайте, как работать с пакетом SDK для внутреннего сервера .NET для мобильных приложений службы приложений Azure."
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
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="74bd9-104">Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="74bd9-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="74bd9-105">В этом разделе показано, как использовать пакет SDK для внутреннего сервера .NET в основных сценариях применения мобильных приложений службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="74bd9-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="74bd9-106">Пакет SDK для мобильных приложений Azure помогает работать с мобильными клиентами из своего приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="74bd9-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="74bd9-107">[Пакет SDK сервера .NET для мобильных приложений Azure][2] предлагается в виде открытого исходного кода на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="74bd9-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="74bd9-108">Репозиторий содержит весь исходный код, а также полный набор модульных тестов пакета SDK для сервера и некоторые примеры проектов.</span><span class="sxs-lookup"><span data-stu-id="74bd9-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="74bd9-109">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="74bd9-109">Reference documentation</span></span>
<span data-ttu-id="74bd9-110">Справочную документацию по пакету SDK для сервера см. здесь: [Справочник по .NET для мобильных приложений Azure][1].</span><span class="sxs-lookup"><span data-stu-id="74bd9-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="74bd9-111"><a name="create-app"></a>Практическое руководство. Создание серверной части мобильного приложения .NET</span><span class="sxs-lookup"><span data-stu-id="74bd9-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="74bd9-112">Если вы начинаете новый проект, приложение службы приложений можно создать с помощью [портала Azure] или программы Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74bd9-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="74bd9-113">Вы можете запустить приложение службы приложений локально или опубликовать проект в мобильном приложении облачной службы приложений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="74bd9-114">Если вы добавляете мобильные возможности к имеющемуся проекту, см. раздел [Практическое руководство. Скачивание и инициализация пакета SDK](#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="74bd9-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="74bd9-115">Создание серверной части .NET с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="74bd9-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="74bd9-116">Чтобы создать мобильный внутренний сервер службы приложений, следуйте указаниям из этого [краткого руководства][3] или сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="74bd9-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="74bd9-117">Вернитесь в колонку *Начало работы* и в разделе **Create a table API** (Создание API таблицы) в поле **Backend language** (Язык серверной части) выберите значение **C#**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="74bd9-118">Щелкните **Скачать**, извлеките сжатые файлы проекта на локальный компьютер и откройте решение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74bd9-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="74bd9-119">Создание серверной части .NET с помощью Visual Studio 2013 и Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="74bd9-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="74bd9-120">Чтобы создать проект мобильных приложений Azure в Visual Studio, необходимо установить [пакет Azure SDK для .NET][4] версии 2.9.0 или выше.</span><span class="sxs-lookup"><span data-stu-id="74bd9-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="74bd9-121">После установки пакета SDK создайте приложение ASP.NET, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="74bd9-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="74bd9-122">Откройте диалоговое окно **Новый проект** (последовательно выберите *Файл* > **Создать** > **Проект**).</span><span class="sxs-lookup"><span data-stu-id="74bd9-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="74bd9-123">Разверните раздел **Шаблоны** > **Visual C#** и выберите **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="74bd9-124">Выберите **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="74bd9-125">Введите имя проекта.</span><span class="sxs-lookup"><span data-stu-id="74bd9-125">Fill in the project name.</span></span> <span data-ttu-id="74bd9-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-126">Then click **OK**.</span></span>
5. <span data-ttu-id="74bd9-127">В разделе *ASP.NET 4.5.2 Templates* (Шаблоны ASP.NET 4.5.2) выберите **Мобильное приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="74bd9-128">Установите флажок **Разместить в облаке** , чтобы создать мобильный внутренний сервер в облаке, в котором можно опубликовать этот проект.</span><span class="sxs-lookup"><span data-stu-id="74bd9-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="74bd9-129">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-129">Click **OK**.</span></span>

## <span data-ttu-id="74bd9-130"><a name="install-sdk"></a>Практическое руководство. Скачивание и инициализация пакета SDK</span><span class="sxs-lookup"><span data-stu-id="74bd9-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="74bd9-131">Пакет SDK доступен на сайте [NuGet.org].</span><span class="sxs-lookup"><span data-stu-id="74bd9-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="74bd9-132">Этот пакет включает в себя базовые функции, необходимые для начала работы пакетом SDK.</span><span class="sxs-lookup"><span data-stu-id="74bd9-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="74bd9-133">Для инициализации пакета SDK необходимо выполнить действия с объектом **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="74bd9-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="74bd9-134">Установка пакета SDK</span><span class="sxs-lookup"><span data-stu-id="74bd9-134">Install the SDK</span></span>
<span data-ttu-id="74bd9-135">Чтобы установить пакет SDK, щелкните правой кнопкой мыши проект сервера в Visual Studio, выберите **Управление пакетами NuGet**, найдите пакет [Microsoft.Azure.Mobile.Server], а затем щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="74bd9-136"><a name="server-project-setup"></a> Инициализация серверного проекта</span><span class="sxs-lookup"><span data-stu-id="74bd9-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="74bd9-137">Инициализацию проекта внутреннего сервера .NET можно выполнить аналогично инициализации проектов ASP.NET — включив класс запуска OWIN.</span><span class="sxs-lookup"><span data-stu-id="74bd9-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="74bd9-138">Убедитесь, что указана ссылка на пакет NuGet `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="74bd9-139">Чтобы добавить этот класс в Visual Studio, щелкните правой кнопкой мыши проект сервера и выберите **Добавить** >
**Создать элемент**, а затем — **Интернет** > **Общие** > **Класс Startup OWIN**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="74bd9-140">Будет создан класс с указанным ниже атрибутом.</span><span class="sxs-lookup"><span data-stu-id="74bd9-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="74bd9-141">В методе `Configuration()` класса запуска OWIN используйте объект **HttpConfiguration** , чтобы настроить среду мобильных приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="74bd9-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="74bd9-142">В следующем примере выполняется инициализация серверного проекта без дополнительных функций.</span><span class="sxs-lookup"><span data-stu-id="74bd9-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="74bd9-143">Чтобы включить отдельные функции, перед вызовом **ApplyTo** необходимо вызвать методы расширения для объекта **MobileAppConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="74bd9-144">Например, следующий код добавляет во время инициализации маршруты по умолчанию для всех контроллеров API, имеющих атрибут `[MobileAppController]` :</span><span class="sxs-lookup"><span data-stu-id="74bd9-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="74bd9-145">При быстром запуске сервера на портале Azure выполняется вызов **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="74bd9-146">Это эквивалентно указанной ниже настройке.</span><span class="sxs-lookup"><span data-stu-id="74bd9-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="74bd9-147">Используются следующие методы расширения:</span><span class="sxs-lookup"><span data-stu-id="74bd9-147">The extension methods used are:</span></span>

* <span data-ttu-id="74bd9-148">`AddMobileAppHomeController()` предоставляет домашнюю страницу мобильных приложений Azure по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="74bd9-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="74bd9-149">`MapApiControllers()` предоставляет возможности настраиваемого интерфейса API для контроллеров веб-API с атрибутом `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="74bd9-150">`AddTables()` обеспечивает сопоставление конечных точек `/tables` контроллерами таблиц.</span><span class="sxs-lookup"><span data-stu-id="74bd9-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="74bd9-151">`AddTablesWithEntityFramework()` — это сокращение для сопоставления конечных точек `/tables` с помощью контроллеров на основе Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="74bd9-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="74bd9-152">`AddPushNotifications()` предоставляет простой способ регистрации устройств в концентраторах уведомлений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="74bd9-153">`MapLegacyCrossDomainController()` предоставляет стандартные заголовки CORS для локальной разработки.</span><span class="sxs-lookup"><span data-stu-id="74bd9-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="74bd9-154">Расширения пакета SDK</span><span class="sxs-lookup"><span data-stu-id="74bd9-154">SDK extensions</span></span>
<span data-ttu-id="74bd9-155">Следующие пакеты расширений на основе NuGet предоставляют различные возможности мобильных устройств, которые может использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="74bd9-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="74bd9-156">Вы можете включить расширения во время инициализации с помощью объекта **MobileAppConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="74bd9-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="74bd9-157">[Microsoft.Azure.Mobile.Server.Quickstart] поддерживает базовую настройку мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="74bd9-158">Чтобы добавить его в конфигурацию, во время инициализации необходимо вызвать метод расширения **UseDefaultConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="74bd9-159">Это расширение включает в себя следующие расширения: пакеты Notifications, Authentication, Entity, Tables, Crossdomain и Home.</span><span class="sxs-lookup"><span data-stu-id="74bd9-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="74bd9-160">Этот пакет используется в кратком руководстве по созданию мобильных приложений, доступном на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="74bd9-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="74bd9-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) реализует стандартную *страницу «Это мобильное приложение запущено и работает»* для корневого каталога веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="74bd9-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="74bd9-162">Чтобы добавить его в конфигурацию, вызовите метод расширения **AddMobileAppHomeController** .</span><span class="sxs-lookup"><span data-stu-id="74bd9-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="74bd9-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) содержит классы для работы с данными и настраивает конвейер данных.</span><span class="sxs-lookup"><span data-stu-id="74bd9-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="74bd9-164">Чтобы добавить его в конфигурацию, вызовите метод расширения **AddTables** .</span><span class="sxs-lookup"><span data-stu-id="74bd9-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="74bd9-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) позволяет платформе Entity Framework получать доступ к данным в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="74bd9-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="74bd9-166">Чтобы добавить его в конфигурацию, вызовите метод расширения **AddTablesWithEntityFramework** .</span><span class="sxs-lookup"><span data-stu-id="74bd9-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="74bd9-167">[Microsoft.Azure.Mobile.Server.Authentication] включает функцию проверки подлинности и настраивает ПО промежуточного слоя OWIN, используемое для проверки токенов.</span><span class="sxs-lookup"><span data-stu-id="74bd9-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="74bd9-168">Чтобы добавить его в конфигурацию, вызовите методы расширения **AddAppServiceAuthentication** и **IAppBuilder**.**UseAppServiceAuthentication**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="74bd9-169">[Microsoft.Azure.Mobile.Server.Notifications] включает push-уведомления и определяет их конечную точку регистрации.</span><span class="sxs-lookup"><span data-stu-id="74bd9-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="74bd9-170">Чтобы добавить его в конфигурацию, вызовите метод расширения **AddPushNotifications** .</span><span class="sxs-lookup"><span data-stu-id="74bd9-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="74bd9-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) создает контроллер, который передает устаревшим веб-браузерам данные из вашего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="74bd9-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="74bd9-172">Чтобы добавить его в конфигурацию, вызовите метод расширения **MapLegacyCrossDomainController** .</span><span class="sxs-lookup"><span data-stu-id="74bd9-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="74bd9-173">[Microsoft.Azure.Mobile.Server.Login] предоставляет статический метод AppServiceLoginHandler.CreateToken(), используемый во время пользовательской проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="74bd9-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="74bd9-174"><a name="publish-server-project"></a>Практическое руководство. Публикация серверного проекта</span><span class="sxs-lookup"><span data-stu-id="74bd9-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="74bd9-175">В этом разделе показано, как опубликовать серверный проект .NET из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74bd9-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="74bd9-176">Кроме того, для развертывания серверного проекта вы можете использовать Git или любой из методов, описанных в [документации по развертыванию службы приложений Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="74bd9-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="74bd9-177">В Visual Studio выполните повторную сборку проекта, чтобы восстановить пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="74bd9-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="74bd9-178">В Обозревателе решений щелкните проект правой кнопкой мыши и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="74bd9-179">При первой публикации необходимо определить профиль публикации.</span><span class="sxs-lookup"><span data-stu-id="74bd9-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="74bd9-180">Если профиль уже определен, выделите его и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="74bd9-181">Если появится запрос на выбор цели публикации, щелкните **Служба приложений Microsoft Azure** > **Далее**, а затем (при необходимости) войдите, используя учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="74bd9-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="74bd9-182">Visual Studio загрузит параметры публикации из Azure и безопасно сохранит их.</span><span class="sxs-lookup"><span data-stu-id="74bd9-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="74bd9-183">Выберите свою **подписку**, а затем в раскрывающемся списке **Представление** выберите **Тип ресурса**, разверните **Мобильное приложение** и щелкните серверную часть мобильного приложения. После этого нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="74bd9-184">Проверьте сведения в профиле публикации и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="74bd9-185">При успешной публикации серверной части мобильного приложения отобразится соответствующая целевая страница.</span><span class="sxs-lookup"><span data-stu-id="74bd9-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="74bd9-186"><a name="define-table-controller"></a> Практическое руководство. Определение контроллера таблиц</span><span class="sxs-lookup"><span data-stu-id="74bd9-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="74bd9-187">Определите контроллер таблиц, чтобы предоставить доступ к таблице SQL мобильным клиентам.</span><span class="sxs-lookup"><span data-stu-id="74bd9-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="74bd9-188">Настройка контроллера таблиц состоит из трех шагов.</span><span class="sxs-lookup"><span data-stu-id="74bd9-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="74bd9-189">Создание класса объекта передачи данных.</span><span class="sxs-lookup"><span data-stu-id="74bd9-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="74bd9-190">Настройка ссылки на таблицу в мобильном классе DbContext.</span><span class="sxs-lookup"><span data-stu-id="74bd9-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="74bd9-191">Создание контроллера таблиц.</span><span class="sxs-lookup"><span data-stu-id="74bd9-191">Create a table controller.</span></span>

<span data-ttu-id="74bd9-192">Объект передачи данных — это обычный объект C#, наследуемый от `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="74bd9-193">Например:</span><span class="sxs-lookup"><span data-stu-id="74bd9-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="74bd9-194">Объект передачи данных используется для определения таблиц в Базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="74bd9-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="74bd9-195">Чтобы создать запись в базе данных, добавьте свойство `DbSet<>` в используемый объект DbContext.</span><span class="sxs-lookup"><span data-stu-id="74bd9-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="74bd9-196">В шаблоне проекта по умолчанию для мобильных приложений Azure DbContext называется `Models\MobileServiceContext.cs`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="74bd9-197">Если пакет Azure SDK установлен, можно создать контроллер таблиц шаблонов следующим образом.</span><span class="sxs-lookup"><span data-stu-id="74bd9-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="74bd9-198">Щелкните правой кнопкой мыши папку "Контроллеры" и выберите **Добавить** > **Контроллер...**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="74bd9-199">Выберите параметр **Контроллер таблиц мобильных приложений Azure**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="74bd9-200">В диалоговом окне **Добавление контроллера** :</span><span class="sxs-lookup"><span data-stu-id="74bd9-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="74bd9-201">В раскрывающемся списке **Класс модели** выберите новый объект передачи данных.</span><span class="sxs-lookup"><span data-stu-id="74bd9-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="74bd9-202">В раскрывающемся списке **DbContext** выберите класс мобильных служб DbContext.</span><span class="sxs-lookup"><span data-stu-id="74bd9-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="74bd9-203">Будет автоматически создано имя контроллера.</span><span class="sxs-lookup"><span data-stu-id="74bd9-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="74bd9-204">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-204">Click **Add**.</span></span>

<span data-ttu-id="74bd9-205">Серверный проект быстрого запуска содержит пример для простого класса **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="74bd9-206"><a name="adjust-pagesize"></a>Практическое руководство: изменение размера постраничного представления таблиц</span><span class="sxs-lookup"><span data-stu-id="74bd9-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="74bd9-207">По умолчанию мобильные приложения Azure выдают по 50 записей на запрос.</span><span class="sxs-lookup"><span data-stu-id="74bd9-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="74bd9-208">Разбивка на страницы гарантирует, что клиент не связывает ни поток пользовательского интерфейса, ни сервер надолго, обеспечивая таким образом удобство работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="74bd9-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="74bd9-209">Чтобы изменить размер постраничного представления таблиц, увеличьте допустимый размер запроса на серверной стороне и размер страниц на стороне клиента. Допустимый размер запроса на серверной стороне настраивается с помощью атрибута `EnableQuery`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="74bd9-210">Значение параметра PageSize должно быть больше или равно размеру, запрошенному клиентом.</span><span class="sxs-lookup"><span data-stu-id="74bd9-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="74bd9-211">Сведения об изменении размера страницы для изменения клиента см. в методических указаниях по соответствующему клиенту.</span><span class="sxs-lookup"><span data-stu-id="74bd9-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="74bd9-212">Практическое руководство. Определение настраиваемого контроллера API</span><span class="sxs-lookup"><span data-stu-id="74bd9-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="74bd9-213">Настраиваемый контроллер API обеспечивает большинство базовых функций для серверной части мобильного приложения, предоставляя конечную точку.</span><span class="sxs-lookup"><span data-stu-id="74bd9-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="74bd9-214">Вы можете зарегистрировать контроллер API для мобильных приложений с помощью атрибута [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="74bd9-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="74bd9-215">Атрибут `MobileAppController` регистрирует маршрут, настраивает сериализатор JSON мобильных приложений, а также включает [проверку версии клиента](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="74bd9-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="74bd9-216">В Visual Studio щелкните правой кнопкой мыши папку "Контроллеры", щелкните **Добавить** > **Контроллер**, выберите **Контроллер Web API 2&mdash;пустой**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="74bd9-217">Укажите **имя контроллера**, например `CustomController`, и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="74bd9-218">В файле нового класса контроллера добавьте следующую инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="74bd9-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="74bd9-219">Примените атрибут **[MobileAppController]** к определению класса контроллера API, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="74bd9-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="74bd9-220">Добавьте в файл App_Start/Startup.MobileApp.cs вызов метода расширения **MapApiControllers**, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="74bd9-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="74bd9-221">Кроме того, можно использовать метод расширения `UseDefaultConfiguration()` вместо `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="74bd9-222">Клиенты могут получить доступ к любому контроллеру, к которому не применен атрибут **MobileAppControllerAttribute**. Однако клиенты, использующие любой пакет SDK для клиента мобильного приложения, не смогут правильно использовать этот контроллер.</span><span class="sxs-lookup"><span data-stu-id="74bd9-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="74bd9-223">Практическое руководство: работа с проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="74bd9-223">How to: Work with authentication</span></span>
<span data-ttu-id="74bd9-224">В мобильных приложениях Azure для защиты мобильного внутреннего сервера используется проверка подлинности или авторизация службы приложений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="74bd9-225">В этом разделе показано, как выполнять следующие задачи проверки подлинности в серверном проекте .NET:</span><span class="sxs-lookup"><span data-stu-id="74bd9-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="74bd9-226">Практическое руководство. Добавление аутентификации в серверный проект</span><span class="sxs-lookup"><span data-stu-id="74bd9-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="74bd9-227">Практическое руководство. Использование пользовательской проверки подлинности для приложения</span><span class="sxs-lookup"><span data-stu-id="74bd9-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="74bd9-228">Практическое руководство. Получение сведений о пользователе, прошедшем проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="74bd9-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="74bd9-229">Практическое руководство. Ограничение доступа к данным для авторизованных пользователей</span><span class="sxs-lookup"><span data-stu-id="74bd9-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="74bd9-230"><a name="add-auth"></a>Практическое руководство. Добавление аутентификации в серверный проект</span><span class="sxs-lookup"><span data-stu-id="74bd9-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="74bd9-231">Вы можете добавить проверку подлинности в серверный проект, унаследовав от объекта **MobileAppConfiguration** и настроив ПО промежуточного слоя OWIN.</span><span class="sxs-lookup"><span data-stu-id="74bd9-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="74bd9-232">Когда вы установите пакет [Microsoft.Azure.Mobile.Server.Quickstart] и вызовете метод расширения **UseDefaultConfiguration** , переходите к шагу 3.</span><span class="sxs-lookup"><span data-stu-id="74bd9-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="74bd9-233">В Visual Studio установите пакет [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="74bd9-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="74bd9-234">В файле проекта Startup.cs добавьте следующую строку кода в начало метода **Configuration** :</span><span class="sxs-lookup"><span data-stu-id="74bd9-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="74bd9-235">Этот компонент ПО промежуточного слоя OWIN проверяет маркеры, выданные соответствующим шлюзом службы приложений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="74bd9-236">Добавьте атрибут `[Authorize]` во все контроллеры и методы, в которых нужна проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="74bd9-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="74bd9-237">Сведения о том, как проверять подлинность клиентов в серверных мобильных приложениях, см. в статье [Добавление проверки подлинности в приложение iOS](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="74bd9-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="74bd9-238"><a name="custom-auth"></a>Практическое руководство. Использование пользовательской проверки подлинности для приложения</span><span class="sxs-lookup"><span data-stu-id="74bd9-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="74bd9-239">Если вы не хотите использовать один из поставщиков проверки подлинности и авторизации службы приложений, можно реализовать свою собственную систему входа.</span><span class="sxs-lookup"><span data-stu-id="74bd9-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="74bd9-240">Установите пакет [Microsoft.Azure.Mobile.Server.Login] , чтобы упростить создание маркеров проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="74bd9-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="74bd9-241">Предоставьте свой собственный код для проверки учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="74bd9-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="74bd9-242">Например, можно выполнять проверку с помощью дополненных случайными данными и хэшированных паролей в базе данных.</span><span class="sxs-lookup"><span data-stu-id="74bd9-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="74bd9-243">В следующем примере за эти проверки отвечает метод `isValidAssertion()` (определенный в другом месте).</span><span class="sxs-lookup"><span data-stu-id="74bd9-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="74bd9-244">Пользовательская проверка подлинности осуществляется путем создания ApiController и использования действий `register` и `login`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="74bd9-245">Для сбора данных пользователя клиент должен использовать настраиваемый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="74bd9-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="74bd9-246">Затем эти данные отправляются в API с помощью стандартного вызова HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="74bd9-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="74bd9-247">После проверки утверждения сервером выпускается маркер с помощью метода `AppServiceLoginHandler.CreateToken()` .</span><span class="sxs-lookup"><span data-stu-id="74bd9-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="74bd9-248">В ApiController **нельзя** использовать атрибут `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="74bd9-249">Пример действия `login` :</span><span class="sxs-lookup"><span data-stu-id="74bd9-249">An example `login` action:</span></span>

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

<span data-ttu-id="74bd9-250">В предыдущем примере LoginResult и LoginResultUser — это сериализуемые объекты, содержащие необходимые свойства.</span><span class="sxs-lookup"><span data-stu-id="74bd9-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="74bd9-251">Клиент ожидает возвращения ответов входа в виде объектов JSON в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="74bd9-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="74bd9-252">Метод `AppServiceLoginHandler.CreateToken()` включает в себя параметры *audience* и *issuer*.</span><span class="sxs-lookup"><span data-stu-id="74bd9-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="74bd9-253">Для обоих этих параметров обычно устанавливаются значения, равные URL-адресу корня приложения, с помощью схемы HTTPS.</span><span class="sxs-lookup"><span data-stu-id="74bd9-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="74bd9-254">Точно так же для параметра *secretKey* нужно задать значение ключа подписывания приложения.</span><span class="sxs-lookup"><span data-stu-id="74bd9-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="74bd9-255">Не распространяйте ключ подписывания в клиенте, так как он может быть использован для создания ключей и олицетворения пользователей.</span><span class="sxs-lookup"><span data-stu-id="74bd9-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="74bd9-256">Если приложение размещено в службе приложений, этот ключ подписывания можно получить из переменной среды *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="74bd9-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="74bd9-257">Если это необходимо для отладки в локальной среде, можно получить ключ и сохранить его как параметр приложения, выполнив инструкции из раздела [Локальная отладка с проверкой подлинности](#local-debug) .</span><span class="sxs-lookup"><span data-stu-id="74bd9-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="74bd9-258">Выданный маркер может содержать другие утверждения и иметь другую дату окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="74bd9-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="74bd9-259">Выданный маркер должен содержать по крайней мере утверждение субъекта (**sub**).</span><span class="sxs-lookup"><span data-stu-id="74bd9-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="74bd9-260">Чтобы обеспечить поддержку стандартного клиентского метода `loginAsync()` , можно перегрузить маршрут проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="74bd9-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="74bd9-261">Если клиент вызывает `client.loginAsync('custom');` для входа, ваш маршрут должен быть следующим: `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="74bd9-262">Вы можете задать маршрут для контроллера пользовательской проверки подлинности с помощью `MapHttpRoute()`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="74bd9-263">Подход с использованием `loginAsync()` гарантирует, что маркер проверки подлинности прикрепляется к каждому последующему вызову службы.</span><span class="sxs-lookup"><span data-stu-id="74bd9-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="74bd9-264"><a name="user-info"></a>Практическое руководство. Получение сведений о пользователе, прошедшем проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="74bd9-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="74bd9-265">При проверке подлинности пользователя у службы приложений в коде серверной части .NET вы можете получить присвоенный идентификатор пользователя и другие сведения.</span><span class="sxs-lookup"><span data-stu-id="74bd9-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="74bd9-266">Сведения о пользователе можно использовать для принятия решений об авторизации в серверной части.</span><span class="sxs-lookup"><span data-stu-id="74bd9-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="74bd9-267">Следующий код получает идентификатор пользователя, связанный с запросом.</span><span class="sxs-lookup"><span data-stu-id="74bd9-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="74bd9-268">SID является производным от идентификатора пользователя, предоставленного поставщиком, и является статическим для данного пользователя и поставщика входа в систему.</span><span class="sxs-lookup"><span data-stu-id="74bd9-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="74bd9-269">Идентификатор безопасности (SID) имеет значение NULL для недопустимых маркеров проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="74bd9-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="74bd9-270">Кроме того, служба приложений позволяет запрашивать конкретные утверждения от поставщика входа в систему.</span><span class="sxs-lookup"><span data-stu-id="74bd9-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="74bd9-271">Каждый поставщик удостоверений может предоставлять больше сведений с помощью пакета SDK поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="74bd9-272">Например, можно использовать Graph API Facebook для получения сведений о друзьях.</span><span class="sxs-lookup"><span data-stu-id="74bd9-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="74bd9-273">Вы можете задать утверждения, запрошенные в колонке поставщика на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="74bd9-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="74bd9-274">Некоторые утверждения требуют дополнительной настройки поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="74bd9-275">Следующий код вызывает метод расширения **GetAppServiceIdentityAsync** для получения учетных данных входа, которые включают маркер доступа, необходимый для выполнения запросов к API Graph Facebook:</span><span class="sxs-lookup"><span data-stu-id="74bd9-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="74bd9-276">Чтобы предоставить метод расширения **GetAppServiceIdentityAsync**, необходимо добавить выражение для `System.Security.Principal`.</span><span class="sxs-lookup"><span data-stu-id="74bd9-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="74bd9-277"><a name="authorize"></a>Практическое руководство. Ограничение доступа к данным для авторизованных пользователей</span><span class="sxs-lookup"><span data-stu-id="74bd9-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="74bd9-278">В предыдущем разделе мы показали, как получить идентификатор пользователя, прошедшего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="74bd9-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="74bd9-279">По этому значению можно ограничить доступ к данным и другим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="74bd9-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="74bd9-280">Например, добавив в таблицы столбец userId и отфильтровав результаты запросов по идентификатору пользователя, вы получите простой способ ограничения возвращаемых данных только данными для авторизованных пользователей.</span><span class="sxs-lookup"><span data-stu-id="74bd9-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="74bd9-281">Следующий код возвращает строки данных только в том случае, если SID совпадает со значением в столбце UserId таблицы TodoItem.</span><span class="sxs-lookup"><span data-stu-id="74bd9-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="74bd9-282">Метод `Query()` возвращает `IQueryable`, которым можно управлять с помощью LINQ для обработки фильтрации.</span><span class="sxs-lookup"><span data-stu-id="74bd9-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="74bd9-283">Практическое руководство. Добавление push-уведомлений в серверный проект</span><span class="sxs-lookup"><span data-stu-id="74bd9-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="74bd9-284">Добавьте push-уведомления в проект сервера, расширив объект **MobileAppConfiguration** и создав клиент концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="74bd9-285">В Visual Studio щелкните правой кнопкой мыши серверный проект, выберите пункт **Управление пакетами NuGet**, найдите `Microsoft.Azure.Mobile.Server.Notifications` и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="74bd9-286">Повторите это действие, чтобы установить пакет `Microsoft.Azure.NotificationHubs` , который включает в себя клиентскую библиотеку центров уведомлений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="74bd9-287">Перейдите к папке App_Start, откройте файл Startup.MobileApp.cs и добавьте вызов метода расширения **AddPushNotifications()** на этапе инициализации.</span><span class="sxs-lookup"><span data-stu-id="74bd9-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="74bd9-288">Добавьте следующий код, который создает клиент центров уведомлений:</span><span class="sxs-lookup"><span data-stu-id="74bd9-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="74bd9-289">Теперь вы можете использовать клиент концентраторов уведомлений для отправки push-уведомлений на зарегистрированные устройства.</span><span class="sxs-lookup"><span data-stu-id="74bd9-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="74bd9-290">Дополнительные сведения см. в статье [Добавление push-уведомлений в приложение iOS](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="74bd9-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="74bd9-291">Дополнительные сведения о Центрах уведомлений см. в статье [Концентраторы уведомлений Azure](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74bd9-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="74bd9-292"><a name="tags"></a>Практическое руководство. Включение принудительной отправки push-уведомлений с использованием тегов</span><span class="sxs-lookup"><span data-stu-id="74bd9-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="74bd9-293">Центры уведомлений позволяют отправлять целевые уведомления в определенные регистрации с помощью тегов.</span><span class="sxs-lookup"><span data-stu-id="74bd9-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="74bd9-294">Несколько тегов создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="74bd9-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="74bd9-295">Идентификатор установки идентифицирует определенное устройство.</span><span class="sxs-lookup"><span data-stu-id="74bd9-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="74bd9-296">Идентификатор пользователя идентифицирует определенного пользователя на основе прошедшего проверку подлинности SID.</span><span class="sxs-lookup"><span data-stu-id="74bd9-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="74bd9-297">Доступ к идентификатору установки можно получить из свойства **installationId** в **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="74bd9-298">В примере ниже показано, как использовать идентификатор установки для добавления тега в конкретную установку в центрах уведомлений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="74bd9-299">Все теги, предоставленные клиентом во время регистрации push-уведомлений, игнорируются серверной частью при создании установки.</span><span class="sxs-lookup"><span data-stu-id="74bd9-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="74bd9-300">Чтобы включить клиент для добавления тегов в установку, необходимо создать настраиваемый API, который добавляет теги, с помощью шаблона выше.</span><span class="sxs-lookup"><span data-stu-id="74bd9-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="74bd9-301">В качестве примера см. [добавленные клиентом теги push-уведомлений][5] в полном примере краткого руководства по созданию мобильных приложений службы приложений.</span><span class="sxs-lookup"><span data-stu-id="74bd9-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="74bd9-302"><a name="push-user"></a>Практическое руководство. Отправка push-уведомлений аутентифицированному пользователю</span><span class="sxs-lookup"><span data-stu-id="74bd9-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="74bd9-303">Когда прошедший проверку пользователь регистрируется для работы с push-уведомлениями, в регистрацию автоматически добавляется тег с идентификатором пользователя.</span><span class="sxs-lookup"><span data-stu-id="74bd9-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="74bd9-304">С помощью этого тега можно отправлять push-уведомления на все устройства, зарегистрированные этим пользователем.</span><span class="sxs-lookup"><span data-stu-id="74bd9-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="74bd9-305">Следующий код получает идентификатор SID пользователя, выполняющего запрос, и отправляет шаблонное push-уведомление в каждую регистрацию устройства для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="74bd9-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="74bd9-306">При регистрации для работы с push-уведомлениями на клиенте, прошедшем проверку подлинности, убедитесь, что проверка подлинности завершена, и только после этого начинайте регистрацию.</span><span class="sxs-lookup"><span data-stu-id="74bd9-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="74bd9-307">Дополнительные сведения см. в разделе [Отправка push-уведомлений пользователям][6] в полном примере краткого руководства по мобильным приложениям службы приложений для серверной части .NET.</span><span class="sxs-lookup"><span data-stu-id="74bd9-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="74bd9-308">Практическое руководство. Отладка и устранение неполадок пакета SDK для сервера .NET</span><span class="sxs-lookup"><span data-stu-id="74bd9-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="74bd9-309">Служба приложений Azure предоставляет несколько методов отладки и устранения неполадок в приложениях ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="74bd9-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="74bd9-310">Мониторинг службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="74bd9-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="74bd9-311">Включение ведения журналов диагностики в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="74bd9-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="74bd9-312">Диагностика службы приложений Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74bd9-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="74bd9-313">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="74bd9-313">Logging</span></span>
<span data-ttu-id="74bd9-314">Журналы диагностики службы приложений вы можете вести с помощью стандартной записи трассировки ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="74bd9-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="74bd9-315">Перед записью в журналы необходимо включить диагностику в серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="74bd9-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="74bd9-316">Для включения диагностики и записи в журналы сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="74bd9-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="74bd9-317">Следуйте указаниям в разделе [Включение диагностики](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="74bd9-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="74bd9-318">Добавьте в файл с кодом следующую инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="74bd9-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="74bd9-319">Создайте модуль записи трассировки для записи из серверного приложения .NET в журналы диагностики следующим образом:</span><span class="sxs-lookup"><span data-stu-id="74bd9-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="74bd9-320">Повторно опубликуйте серверный проект и запустите серверную часть мобильного приложения с ведением журнала.</span><span class="sxs-lookup"><span data-stu-id="74bd9-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="74bd9-321">Загрузите и оцените журналы, как описано в разделе [Практическое руководство. Загрузка журналов](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="74bd9-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="74bd9-322"><a name="local-debug"></a>Локальная отладка с проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="74bd9-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="74bd9-323">Вы можете запустить приложение локально, чтобы проверить изменения перед их публикацией в облаке.</span><span class="sxs-lookup"><span data-stu-id="74bd9-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="74bd9-324">Для большинства серверных систем мобильных приложений Azure нажмите клавишу *F5* во время работы в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74bd9-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="74bd9-325">Однако при проверке подлинности следует учитывать некоторые дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="74bd9-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="74bd9-326">Необходимо облачное мобильное приложение, в котором настроены проверка подлинности и авторизация службы приложений, а в клиенте должна быть конечная точка облака, указанная как узел для альтернативного входа.</span><span class="sxs-lookup"><span data-stu-id="74bd9-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="74bd9-327">Конкретные указания можно найти в документации для клиентской платформы.</span><span class="sxs-lookup"><span data-stu-id="74bd9-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="74bd9-328">Убедитесь, что в мобильном внутреннем сервере установлен пакет [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="74bd9-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="74bd9-329">В приложении добавьте следующий код в класс запуска OWIN после применения `MobileAppConfiguration` к объекту `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="74bd9-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="74bd9-330">В приведенном выше примере необходимо настроить параметры приложения *authAudience* и *authIssuer* в файле Web.config, задав для каждого из них значение URL-адреса корня приложения в формате HTTPS.</span><span class="sxs-lookup"><span data-stu-id="74bd9-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="74bd9-331">Точно так же для параметра *authSigningKey* нужно задать значение ключа подписывания приложения.</span><span class="sxs-lookup"><span data-stu-id="74bd9-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="74bd9-332">Чтобы получить ключ подписывания, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="74bd9-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="74bd9-333">Перейдите в свое приложение на [портала Azure]</span><span class="sxs-lookup"><span data-stu-id="74bd9-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="74bd9-334">Щелкните **Инструменты**, **Kudu**, **Перейти**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="74bd9-335">На сайте управления Kudu щелкните **Среда**.</span><span class="sxs-lookup"><span data-stu-id="74bd9-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="74bd9-336">Найдите значение для *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="74bd9-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="74bd9-337">Укажите ключ подписывания для параметра *authSigningKey* в файле конфигурации локального приложения.</span><span class="sxs-lookup"><span data-stu-id="74bd9-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="74bd9-338">Теперь на мобильном внутреннем сервере при работе локально есть все необходимое для проверки маркеров, которые клиент получает от конечной точки облака.</span><span class="sxs-lookup"><span data-stu-id="74bd9-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="74bd9-339">[портала Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="74bd9-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="74bd9-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="74bd9-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="74bd9-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="74bd9-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="74bd9-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="74bd9-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="74bd9-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="74bd9-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="74bd9-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="74bd9-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="74bd9-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="74bd9-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
