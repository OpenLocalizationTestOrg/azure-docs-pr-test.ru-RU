---
title: "ASP.NET MVC 5 aaaDeploy мобильного веб-приложения в службе приложений Azure"
description: "Учебник, в котором объясняется, как toodeploy tooAzure приложения web службы приложений с помощью мобильных функции в ASP.NET MVC 5 веб-приложения."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="e3d48-103">Развертывание мобильного веб-приложения ASP.NET MVC 5 в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e3d48-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="e3d48-104">В этом учебнике объясняется hello основы как toobuild ASP.NET MVC 5 веб-приложения, мобильные и развернуть ее tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="e3d48-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="e3d48-105">В этом учебнике требуется [Visual Studio Express 2013 для Web] [ Visual Studio Express 2013] или профессиональных выпусков Visual Studio, если у вас уже есть, hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="e3d48-106">Можно использовать [Visual Studio 2015] снимков экрана приветствия будут отличаться, но необходимо использовать hello ASP.NET 4.x шаблоны.</span><span class="sxs-lookup"><span data-stu-id="e3d48-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="e3d48-107">Что вы создадите</span><span class="sxs-lookup"><span data-stu-id="e3d48-107">What You'll Build</span></span>
<span data-ttu-id="e3d48-108">В этом учебнике вы добавите мобильные функции toohello простое конференции листинг приложение, которое предоставляется в hello [начальный проект][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="e3d48-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="e3d48-109">Hello следующем снимке экрана показано hello сеансов ASP.NET в приложении hello завершена, как видно в эмуляторе hello браузера в Internet Explorer 11 F12 средств разработчика.</span><span class="sxs-lookup"><span data-stu-id="e3d48-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="e3d48-110">Можно использовать средства разработчика Internet Explorer 11 F12 hello и hello [инструмента Fiddler] [ Fiddler] toohelp отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="e3d48-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="e3d48-111">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="e3d48-111">Skills You'll Learn</span></span>
<span data-ttu-id="e3d48-112">В этом учебнике вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="e3d48-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="e3d48-113">Как toopublish toouse Visual Studio 2013 веб-приложения непосредственно tooa веб-приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d48-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="e3d48-114">Использование CSS Bootstrap framework hello шаблоны hello ASP.NET MVC 5 для улучшения отображения на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="e3d48-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="e3d48-115">Как toocreate mobile конкретного представления tootarget конкретных браузеры для мобильных устройств, таких как hello iPhone и Android</span><span class="sxs-lookup"><span data-stu-id="e3d48-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="e3d48-116">Как отвечать на запросы представления toocreate (представления, реагирующие на устройствах toodifferent браузеры)</span><span class="sxs-lookup"><span data-stu-id="e3d48-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="e3d48-117">Настройка среды разработки hello</span><span class="sxs-lookup"><span data-stu-id="e3d48-117">Set up hello development environment</span></span>
<span data-ttu-id="e3d48-118">Настройка среды разработки, установив hello Azure SDK для .NET 2.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e3d48-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="e3d48-119">tooinstall hello Azure SDK для .NET, щелкните ссылку hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="e3d48-120">Если у вас нет Visual Studio 2013, пока установлен, то оно будет установлено по каналу hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="e3d48-121">Для работы с этим учебником требуется Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="e3d48-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="e3d48-122">[Пакет SDK Azure для Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="e3d48-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="e3d48-123">В окне приветствия установщика веб-платформы нажмите кнопку **установить** и продолжите установку hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="e3d48-124">Кроме того, понадобится эмулятор браузера для мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="e3d48-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="e3d48-125">Любой из следующих hello будет работать:</span><span class="sxs-lookup"><span data-stu-id="e3d48-125">Any of hello following will work:</span></span>

* <span data-ttu-id="e3d48-126">Эмулятор браузера в [инструментах разработчика F12 Internet Explorer 11][EmulatorIE11] (используется в снимках экрана всех браузеров мобильного устройства).</span><span class="sxs-lookup"><span data-stu-id="e3d48-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="e3d48-127">Он содержит предустановки строк агента пользователя для Windows Phone 8, Windows Phone 7 и Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="e3d48-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="e3d48-128">Эмулятор браузера в [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="e3d48-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="e3d48-129">Содержит предустановки для многих устройств Android, а также Apple iPhone, Apple iPad и Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="e3d48-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="e3d48-130">Также поддерживает эмуляцию событий прикосновения.</span><span class="sxs-lookup"><span data-stu-id="e3d48-130">It also emulates touch events.</span></span>
* <span data-ttu-id="e3d48-131">[Эмулятор Opera Mobile][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="e3d48-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="e3d48-132">Проекты Visual Studio с C\# исходный код, являются доступными tooaccompany в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="e3d48-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="e3d48-133">[Скачивание начального проекта][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="e3d48-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="e3d48-134">[Скачивание полного проекта][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="e3d48-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="e3d48-135"><a name="bkmk_DeployStarterProject"></a>Развертывание hello начального проекта tooan веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="e3d48-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="e3d48-136">Загрузить приложение hello листинг конференции [начальный проект][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="e3d48-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="e3d48-137">Затем в проводнике Windows щелкните правой кнопкой мыши hello загружен ZIP-файл и выберите *свойства*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="e3d48-138">В hello **свойства** диалогового окна выберите hello **Unblock** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e3d48-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="e3d48-139">(Разблокировке предотвращает предупреждение системы безопасности, которая возникает при попытке toouse *.zip* файл, загруженный с веб-узла hello.)</span><span class="sxs-lookup"><span data-stu-id="e3d48-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="e3d48-140">Щелкните правой кнопкой мыши hello ZIP-файл и выберите **извлечь все** распаковать файл hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="e3d48-141">В Visual Studio откройте hello *C#\Mvc5Mobile.sln* файла.</span><span class="sxs-lookup"><span data-stu-id="e3d48-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="e3d48-142">В обозревателе решений щелкните правой кнопкой мыши проект hello и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="e3d48-143">В окне веб-публикации щелкните **Служба приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="e3d48-144">Если вы еще не выполнили вход в Azure, щелкните **Добавить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="e3d48-145">Выполните запросы toolog hello в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d48-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="e3d48-146">диалоговое окно службы приложения Hello появляются вы как вход.</span><span class="sxs-lookup"><span data-stu-id="e3d48-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="e3d48-147">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="e3d48-148">В hello **имя веб-приложения** укажите префикс имени уникальный приложения.</span><span class="sxs-lookup"><span data-stu-id="e3d48-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="e3d48-149">Полностью определенным именем вашего веб-приложения будет *&lt;префикс>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="e3d48-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="e3d48-150">Также выберите или укажите имя существующей группы ресурсов в поле **Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="e3d48-151">Нажмите кнопку **New** toocreate новый план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="e3d48-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="e3d48-152">Настройте новый план служб приложений hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="e3d48-153">Вернувшись в диалоговое окно создания службы приложения hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="e3d48-154">После того как hello ресурсы Azure, диалоговое окно приветствия веб-публикация будет заполняться hello параметры для нового приложения.</span><span class="sxs-lookup"><span data-stu-id="e3d48-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="e3d48-155">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="e3d48-156">После завершения публикации hello начального проекта toohello веб-приложение Azure Visual Studio браузер для настольных компьютеров hello открывает toodisplay hello динамической веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e3d48-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="e3d48-157">Запустите симулятор мобильных браузеров, скопируйте URL-адрес hello приложения hello конференции (*<prefix>*. azurewebsites.net) в эмуляторе hello, нажмите кнопку сверху справа и выберите **Обзор тегом**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="e3d48-158">Если вы используете Internet Explorer 11 в качестве браузера по умолчанию hello, необходимо просто tootype `F12`, затем `Ctrl+8`и измените профиль браузера hello слишком**Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="e3d48-159">На рисунке ниже показана hello *AllTags* представления в книжной ориентации (в выборе **Обзор тегом**).</span><span class="sxs-lookup"><span data-stu-id="e3d48-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="e3d48-160">При отладке приложения MVC 5 в среде Visual Studio можно опубликовать вашей tooAzure web app снова tooverify hello динамической веб-приложения непосредственно из браузера мобильных или эмулятор браузера.</span><span class="sxs-lookup"><span data-stu-id="e3d48-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="e3d48-161">экран приветствия удобочитаемым на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="e3d48-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="e3d48-162">Уже также можно увидеть некоторые визуальные эффекты hello применены платформой hello CSS начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="e3d48-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="e3d48-163">Нажмите кнопку hello **ASP.NET** ссылку.</span><span class="sxs-lookup"><span data-stu-id="e3d48-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="e3d48-164">Hello представление тега ASP.NET — они масштаба toohello экран, который начальной загрузки может сделать для вас автоматически.</span><span class="sxs-lookup"><span data-stu-id="e3d48-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="e3d48-165">Тем не менее можно улучшить это представление toobetter масть hello мобильных браузеров.</span><span class="sxs-lookup"><span data-stu-id="e3d48-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="e3d48-166">Например, hello **даты** столбца трудно читать.</span><span class="sxs-lookup"><span data-stu-id="e3d48-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="e3d48-167">Далее в учебнике hello изменим hello *AllTags* просмотра toomake его мобильной.</span><span class="sxs-lookup"><span data-stu-id="e3d48-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="e3d48-168"><a name="bkmk_bootstrap"></a> Платформа начальной загрузки CSS</span><span class="sxs-lookup"><span data-stu-id="e3d48-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="e3d48-169">Новое в hello MVC 5 шаблона является встроенной поддержки начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="e3d48-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="e3d48-170">Вы уже видели как усовершенствует немедленно hello различных представлений в приложении.</span><span class="sxs-lookup"><span data-stu-id="e3d48-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="e3d48-171">Например hello панели навигации в верхней hello автоматически сворачиваемого когда меньше ширины обозревателя hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="e3d48-172">В браузер для настольных компьютеров hello попробуйте изменить размер окна браузера hello и см. Изменение внешнего вида панели навигации hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="e3d48-173">Это отвечать на запросы веб-дизайн hello, который встроен в начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="e3d48-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="e3d48-174">toosee о том, как будет выглядеть hello веб-приложения без начальной загрузки, откройте *приложения\_запустить\\BundleConfig.cs* и закомментируйте hello строки, содержащие *bootstrap.js* и *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="e3d48-175">Hello код отображает hello последних двух инструкций hello `RegisterBundles` метод после изменения hello:</span><span class="sxs-lookup"><span data-stu-id="e3d48-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="e3d48-176">Нажмите клавишу `Ctrl+F5` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="e3d48-177">Обратите внимание, что эту панель навигации сворачиваемого hello теперь является просто обычный неупорядоченный список.</span><span class="sxs-lookup"><span data-stu-id="e3d48-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="e3d48-178">Еще раз щелкните **Browse by tag** (Поиск по тегу), затем щелкните **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="e3d48-179">В представлении мобильном эмуляторе hello вы увидите теперь, когда он больше не соответствует масштаба toohello экрана и необходимо прокрутки сбоку в порядке toosee hello правой части таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="e3d48-180">Отменить изменения и обновить tooverify мобильных браузеров hello, экрана приветствия мобильные восстановлена.</span><span class="sxs-lookup"><span data-stu-id="e3d48-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="e3d48-181">Начальной загрузки не определенного tooASP.NET MVC 5, и воспользоваться преимуществами этих функций в любой веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e3d48-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="e3d48-182">Теперь эта функция встроена в шаблон проекта ASP.NET MVC 5, таким образом, ваше веб-приложение MVC 5 сможет по умолчанию использовать преимущества Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="e3d48-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="e3d48-183">Дополнительные сведения о начальной загрузки go toothe [начальной загрузки] [ BootstrapSite] сайта.</span><span class="sxs-lookup"><span data-stu-id="e3d48-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="e3d48-184">В следующем разделе hello будет отображен как tooprovide браузера mobile определенным представлениям.</span><span class="sxs-lookup"><span data-stu-id="e3d48-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="e3d48-185"><a name="bkmk_overrideviews"></a>Переопределить hello, макеты и частичные представления</span><span class="sxs-lookup"><span data-stu-id="e3d48-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="e3d48-186">Вы можете переопределить любое представление (включая макеты и частичные представления) для браузеров мобильных устройств вообще, для отдельного браузера мобильных устройств или для любого конкретного браузера.</span><span class="sxs-lookup"><span data-stu-id="e3d48-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="e3d48-187">Просмотр конкретного mobile tooprovide, можно скопировать файл представления и добавление *. Mobile* toohello имя файла.</span><span class="sxs-lookup"><span data-stu-id="e3d48-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="e3d48-188">Например, toocreate мобильного телефона *индекс* представления, можно скопировать *представления\\Главная\\Index.cshtml* для *представления\\Главная\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="e3d48-189">В этом разделе для мобильных устройств будет создан специальный файл макета.</span><span class="sxs-lookup"><span data-stu-id="e3d48-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="e3d48-190">toostart копирования *представления\\Shared\\\_Layout.cshtml* для *представления\\Shared\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="e3d48-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="e3d48-191">Откройте  *\_Layout.Mobile.cshtml* и измените заголовок hello из **приложения MVC5** слишком**MVC5 приложения (мобильный)**.</span><span class="sxs-lookup"><span data-stu-id="e3d48-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="e3d48-192">В каждом `Html.ActionLink` вызова для hello панели навигации, удалите «Просмотр по» в каждой связи *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="e3d48-193">Hello код отображает hello завершения `<ul class="nav navbar-nav">` тег hello мобильных макета файла.</span><span class="sxs-lookup"><span data-stu-id="e3d48-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="e3d48-194">Копировать hello *представления\\Главная\\AllTags.cshtml* файл *представления\\Главная\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="e3d48-195">Откройте новый файл hello и измените `<h2>` элемент из «Теги» слишком "теги (M)»:</span><span class="sxs-lookup"><span data-stu-id="e3d48-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="e3d48-196">Обзор toohello теги страницы с использованием браузер для настольных компьютеров и мобильных браузеров эмулятора.</span><span class="sxs-lookup"><span data-stu-id="e3d48-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="e3d48-197">эмулятор мобильных браузеров Hello показывает hello два изменения, внесенные (hello заголовка из  *\_Layout.Mobile.cshtml* и заголовок hello от *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="e3d48-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="e3d48-198">Напротив, не изменилась hello рабочего стола (с заголовками из  *\_Layout.cshtml* и *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="e3d48-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="e3d48-199"><a name="bkmk_browserviews"></a> Создание представлений для браузера</span><span class="sxs-lookup"><span data-stu-id="e3d48-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="e3d48-200">Кроме того при представления отдельных toomobile или рабочего стола, можно создать представления для отдельного браузера.</span><span class="sxs-lookup"><span data-stu-id="e3d48-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="e3d48-201">Например можно создать представления, которые специально предназначены для hello iPhone или браузера Android hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="e3d48-202">В этом разделе вы создадите макет для браузера iPhone hello и версию iPhone hello *AllTags* представления.</span><span class="sxs-lookup"><span data-stu-id="e3d48-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="e3d48-203">Откройте hello *Global.asax* и добавьте следующий код toohello внизу hello `Application_Start` метод.</span><span class="sxs-lookup"><span data-stu-id="e3d48-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="e3d48-204">Этот код определяет новый режим отображения с именем iPhone, который будет использоваться для каждого входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="e3d48-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="e3d48-205">Если hello входящий запрос соответствует условию, заданных (то есть, если агент пользователя hello содержит строку hello «iPhone»), ASP.NET MVC будет искать представления, имя которого содержит суффикс «iPhone».</span><span class="sxs-lookup"><span data-stu-id="e3d48-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d48-206">При добавлении мобильных обозревателем режимы отображения, такие как для iPhone и Android, будет убедиться, что первый аргумент hello tooset слишком`0` toomake (вставки в начале hello hello списка), убедиться, что, режим обозревателем hello имеет приоритет над мобильными шаблона hello (*. Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="e3d48-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="e3d48-207">Если hello мобильных шаблон находится в начале hello списка hello, она будет выбрана по вашей режим отображения предполагаемой (hello первого совпадения wins и соответствует hello мобильных шаблон все браузеры для мобильных устройств).</span><span class="sxs-lookup"><span data-stu-id="e3d48-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="e3d48-208">Щелкните правой кнопкой мыши в коде hello `DefaultDisplayMode`, выберите **Разрешить**и нажмите кнопку `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="e3d48-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="e3d48-209">Это добавляет toothe ссылки `System.Web.WebPages` пространство имен, что, если `DisplayModeProvider` и `DefaultDisplayMode` определенных типов.</span><span class="sxs-lookup"><span data-stu-id="e3d48-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="e3d48-210">Кроме того, можно просто вручную добавить следующие строки toothe hello `using` раздел файла hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="e3d48-211">Сохраните изменения hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-211">Save hello changes.</span></span> <span data-ttu-id="e3d48-212">Скопируйте файл*Views\\Shared\\\_Layout.Mobile.cshtml* в *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="e3d48-213">Откройте новый файл hello и измените заголовок hello от `MVC5 Application (Mobile)` для `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="e3d48-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="e3d48-214">Копировать hello *представления\\Главная\\AllTags.Mobile.cshtml* файл *представления\\Главная\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="e3d48-215">В новом файле hello, измените hello `<h2>` из «теги (M)» слишком» тегами элемента (iPhone)».</span><span class="sxs-lookup"><span data-stu-id="e3d48-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="e3d48-216">Запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-216">Run hello application.</span></span> <span data-ttu-id="e3d48-217">Запуск эмулятора мобильных браузеров, убедитесь, что его агент пользователя установлено слишком «iPhone» и найдите toohello *AllTags* представления.</span><span class="sxs-lookup"><span data-stu-id="e3d48-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="e3d48-218">При использовании эмулятора hello в средствах разработчика Internet Explorer 11 F12 настройте эмуляции toohello ниже:</span><span class="sxs-lookup"><span data-stu-id="e3d48-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="e3d48-219">профиль браузера — **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="e3d48-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="e3d48-220">строка агента пользователя — **Custom**</span><span class="sxs-lookup"><span data-stu-id="e3d48-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="e3d48-221">настраиваемая строка — **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="e3d48-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="e3d48-222">Hello следующем снимке экрана показано hello *AllTags* представление в эмуляторе в средствах разработчика Internet Explorer 11 F12 с hello специальную строку агента пользователя (это строки агента пользователя iPhone 5 C).</span><span class="sxs-lookup"><span data-stu-id="e3d48-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="e3d48-223">В браузере мобильного hello выберите hello **динамики** ссылку.</span><span class="sxs-lookup"><span data-stu-id="e3d48-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="e3d48-224">Так как не представлением для мобильных устройств (*AllSpeakers.Mobile.cshtml*), просматривать динамики по умолчанию hello (*AllSpeakers.cshtml*) отображается с помощью мобильных режиме hello ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="e3d48-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="e3d48-225">Как показано ниже, заголовок hello **MVC5 приложения (мобильный)** определяется в  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="e3d48-226">Глобально, представление по умолчанию (не для мобильных устройств) к просмотру в макете мобильных устройств можно отключить, установив `RequireConsistentDisplayMode` для `true` в hello *представления\\\_ViewStart.cshtml* файла следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e3d48-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="e3d48-227">Когда `RequireConsistentDisplayMode` задано слишком`true`, hello мобильных макета (*\_Layout.Mobile.cshtml*) используется только для мобильных представлений (т. е. Если файл представления имеет форму hello  ***ViewName** . Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="e3d48-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="e3d48-228">Может потребоваться tooset `RequireConsistentDisplayMode` слишком`true` Если мобильных макет плохо работает с вашим представлениям не для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="e3d48-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="e3d48-229">Hello снимке экрана ниже показано как hello *динамики* при отображении страницы `RequireConsistentDisplayMode` задано слишком`true` (без строку hello «(мобильный)» в hello навигации панели hello верхней).</span><span class="sxs-lookup"><span data-stu-id="e3d48-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="e3d48-230">Согласованный режим отображения в определенных режимах можно отключить, установив `RequireConsistentDisplayMode` слишком`false` в файл представления hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="e3d48-231">Приведенный ниже код в hello *представления\\Главная\\AllSpeakers.cshtml* файл задает `RequireConsistentDisplayMode` слишком`false`:</span><span class="sxs-lookup"><span data-stu-id="e3d48-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="e3d48-232">В этом разделе мы видели как toocreate мобильных макеты, представлений и hello как toocreate макеты и представлений для конкретных устройств, таких как iPhone.</span><span class="sxs-lookup"><span data-stu-id="e3d48-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="e3d48-233">Однако главным преимуществом hello hello CSS начальной загрузки framework является динамический макет, что означает, что одной таблицы стилей могут применяться за пределами рабочего стола, телефон и планшет браузеры toocreate согласованного внешнего вида и поведения.</span><span class="sxs-lookup"><span data-stu-id="e3d48-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="e3d48-234">В следующем разделе hello вы увидите, как tooleverage начальной загрузки toocreate мобильной представления.</span><span class="sxs-lookup"><span data-stu-id="e3d48-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="e3d48-235"><a name="bkmk_Improvespeakerslist"></a>Улучшения hello динамики списка</span><span class="sxs-lookup"><span data-stu-id="e3d48-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="e3d48-236">Как вы только что увидели hello *динамики* представление доступен для чтения, но ссылки hello невелики и являются трудно tootap на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="e3d48-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="e3d48-237">В этом разделе мы сделаем hello *AllSpeakers* представление мобильные, отображаются большой, чтобы коснитесь ссылки и содержит поле поиска tooquickly найти динамики.</span><span class="sxs-lookup"><span data-stu-id="e3d48-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="e3d48-238">Можно использовать hello начальной загрузки [связанного списка группы] [ linked list group] стили для улучшения hello *динамики* представления.</span><span class="sxs-lookup"><span data-stu-id="e3d48-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="e3d48-239">В *представления\\Главная\\AllSpeakers.cshtml*, замените содержимое файла Razor hello hello приведенный ниже код hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="e3d48-240">Hello `class="list-group"` атрибута в hello `<div>` тег применяет начальной загрузки список стилей и hello `class="input-group-item"` атрибут применяется, связи tooeach стиля элемента списка начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="e3d48-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="e3d48-241">Обновите hello мобильных браузеров.</span><span class="sxs-lookup"><span data-stu-id="e3d48-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="e3d48-242">Hello обновить представление выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e3d48-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="e3d48-243">Hello начальной загрузки [связанного списка группы] [ linked list group] стили делает hello всей поле каждой связи интерактивными, являющийся гораздо более широкие пользователя.</span><span class="sxs-lookup"><span data-stu-id="e3d48-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="e3d48-244">Переключитесь в представление рабочего стола toothe и понаблюдайте за hello согласованный внешний вид.</span><span class="sxs-lookup"><span data-stu-id="e3d48-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="e3d48-245">Несмотря на то, что представление мобильных браузеров hello была улучшена, и громоздкими hello длинный список динамики.</span><span class="sxs-lookup"><span data-stu-id="e3d48-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="e3d48-246">Исходные настройки Bootstrap не предусматривают функцию фильтра поиска, но вы можете ее добавить с помощью нескольких строк кода.</span><span class="sxs-lookup"><span data-stu-id="e3d48-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="e3d48-247">Сначала будет добавлено представление toohello поле поиска, затем подключить hello код JavaScript для функции фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="e3d48-248">В *представления\\Главная\\AllSpeakers.cshtml*, добавьте \<формы\> тег сразу после hello \<h2\> тег, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="e3d48-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="e3d48-249">Обратите внимание, что hello `<form>` и `<input>` теги оба имеют toothem начальной загрузки стили, примененные hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="e3d48-250">Hello `<span>` элемент добавляет начальной загрузкой [glyphicon] [ glyphicon] toothe поле поиска.</span><span class="sxs-lookup"><span data-stu-id="e3d48-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="e3d48-251">В hello *сценариев* папки, добавьте файл JavaScript с именем *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="e3d48-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="e3d48-252">Откройте файл hello и вставьте следующий код в него hello:</span><span class="sxs-lookup"><span data-stu-id="e3d48-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="e3d48-253">Необходимо также tooinclude filter.js в ваш зарегистрированных пакетов.</span><span class="sxs-lookup"><span data-stu-id="e3d48-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="e3d48-254">Откройте *приложения\_запустить\\BundleConfig.cs* и измените первый пакеты hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="e3d48-255">Изменить первый `bundles.Add` инструкции (для hello **jquery** пакета) tooinclude *сценариев\\filter.js*, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="e3d48-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="e3d48-256">Hello **jquery** пакета уже отображается по умолчанию hello  *\_макета* представления.</span><span class="sxs-lookup"><span data-stu-id="e3d48-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="e3d48-257">Более поздней версии, могут использовать hello же JavaScript code tooapply представлений списка tooother функции фильтра.</span><span class="sxs-lookup"><span data-stu-id="e3d48-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="e3d48-258">Обновите hello мобильный браузер и перейдите toohello *AllSpeakers* представления.</span><span class="sxs-lookup"><span data-stu-id="e3d48-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="e3d48-259">В поле поиска введите «sc».</span><span class="sxs-lookup"><span data-stu-id="e3d48-259">In the search box, type "sc".</span></span> <span data-ttu-id="e3d48-260">Hello динамики список теперь должны быть отфильтрованы согласно tooyour строку поиска.</span><span class="sxs-lookup"><span data-stu-id="e3d48-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="e3d48-261"><a name="bkmk_improvetags"></a>Улучшения hello списка тегов</span><span class="sxs-lookup"><span data-stu-id="e3d48-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="e3d48-262">Как hello *динамики* просмотреть, hello *теги* представление доступен для чтения, но hello ссылки — это небольшой и сложной tootap на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="e3d48-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="e3d48-263">Вы можете исправить hello *теги* представление hello таким же способом устранения hello *динамики* просмотра, если использовать описанные ранее, но с hello следующих изменений кода hello `Html.ActionLink` синтаксис методов в  *Представления\\Главная\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e3d48-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="e3d48-264">Hello обновить браузер для настольных компьютеров выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e3d48-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="e3d48-265">И hello обновляется мобильных браузеров выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e3d48-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="e3d48-266">Если вы заметили, что hello исходного списка форматирования осталась в Здравствуйте мобильных браузеров и определить, какая ошибка tooyour стили начальной загрузки работы с низким приоритетом является, это является артефактом предыдущих действий toocreate мобильных конкретного представления.</span><span class="sxs-lookup"><span data-stu-id="e3d48-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="e3d48-267">Однако теперь, когда вы используете toocreate framework hello CSS начальной загрузки конструктора быстродействующих веб-приложений, перейдите head и удалите эти мобильные особых представлений и представления структуры для конкретной mobile hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="e3d48-268">Это сделано, hello обновить мобильных браузеров будут отображены начальной загрузки стили hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="e3d48-269"><a name="bkmk_improvedates"></a>Улучшения hello списка дат</span><span class="sxs-lookup"><span data-stu-id="e3d48-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="e3d48-270">Можно улучшить hello *даты* просмотреть, как повысить hello *динамики* и *теги* представления при использовании описанных выше, но с hello после изменения кода hello `Html.ActionLink` синтаксис методов в *представления\\Главная\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e3d48-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="e3d48-271">Вот как будет выглядеть обновленное представление браузера мобильного устройства:</span><span class="sxs-lookup"><span data-stu-id="e3d48-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="e3d48-272">Можно улучшить hello *даты* представление, организуя hello значений даты и времени по дате.</span><span class="sxs-lookup"><span data-stu-id="e3d48-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="e3d48-273">Это можно сделать с помощью hello начальной загрузки [панелей] [ panels] Задание стиля.</span><span class="sxs-lookup"><span data-stu-id="e3d48-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="e3d48-274">Замените содержимое hello hello *представления\\Главная\\AllDates.cshtml* файла следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="e3d48-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="e3d48-275">Этот код создает отдельную `<div class="panel panel-primary">` тег для каждой даты distinct в списке hello и использует hello [связанного списка группы] [ linked list group] для соответствующего связывает как раньше.</span><span class="sxs-lookup"><span data-stu-id="e3d48-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="e3d48-276">Вот какие hello мобильных браузеров выглядит как при выполнении этого кода:</span><span class="sxs-lookup"><span data-stu-id="e3d48-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="e3d48-277">Коммутатор toohello браузер для настольных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="e3d48-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="e3d48-278">Обратите внимание, согласованного вида hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="e3d48-279"><a name="bkmk_improvesessionstable"></a>Улучшить представление SessionsTable hello</span><span class="sxs-lookup"><span data-stu-id="e3d48-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="e3d48-280">В этом разделе мы сделаем hello *SessionsTable* просмотреть дополнительные мобильные.</span><span class="sxs-lookup"><span data-stu-id="e3d48-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="e3d48-281">Это изменение является более существенные изменения предыдущих hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="e3d48-282">В браузере мобильного hello, коснитесь hello **тега** , а затем введите `asp` в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="e3d48-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="e3d48-283">Коснитесь hello **ASP.NET** ссылку.</span><span class="sxs-lookup"><span data-stu-id="e3d48-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="e3d48-284">Как видите, экрана приветствия форматируется как таблицы, которая является в настоящее время спроектированный toobe просмотре в браузере рабочего стола hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="e3d48-285">Однако это немного сложным tooread на мобильный браузер.</span><span class="sxs-lookup"><span data-stu-id="e3d48-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="e3d48-286">toofix, откройте *представления\\Главная\\SessionsTable.cshtml* и затем замените содержимое файла hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="e3d48-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="e3d48-287">Код Hello выполняет три вещи:</span><span class="sxs-lookup"><span data-stu-id="e3d48-287">hello code does 3 things:</span></span>

* <span data-ttu-id="e3d48-288">использует hello начальной загрузки [группы пользовательских связанного списка] [ custom linked list group] tooformat Здравствуйте, сведения о сеансе по вертикали, чтобы эта информация доступна для чтения на мобильный браузер (с помощью классов такие как Список группа элемент текст)</span><span class="sxs-lookup"><span data-stu-id="e3d48-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="e3d48-289">применяет hello [сетки системы] [ grid system] toothe макета, поэтому сеанса hello элементы потока в браузер для настольных компьютеров hello по горизонтали и по вертикали в мобильных браузеров hello (с помощью класса hello col-md-4)</span><span class="sxs-lookup"><span data-stu-id="e3d48-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="e3d48-290">использует hello [отвечать на запросы программы] [ responsive utilities] скрытие hello сеанса теги при просмотре в мобильных браузеров hello (с помощью класса скрытые xs hello)</span><span class="sxs-lookup"><span data-stu-id="e3d48-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="e3d48-291">Вы также можете нажать заголовок ссылки toogo toohello соответствующих сеанса.</span><span class="sxs-lookup"><span data-stu-id="e3d48-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="e3d48-292">ниже рисунке Hello отражает изменения кода hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="e3d48-293">системы начальной загрузки сетки Hello примененное автоматически упорядочивает сеансы по вертикали в браузере мобильного hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="e3d48-294">Кроме того Обратите внимание, что теги hello не отображаются.</span><span class="sxs-lookup"><span data-stu-id="e3d48-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="e3d48-295">Коммутатор toohello браузер для настольных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="e3d48-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="e3d48-296">Обратите внимание hello теги отображаются в браузер для настольных компьютеров hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="e3d48-297">Кроме того вы увидите, что hello сетки начальной загрузки системы, примененные упорядочивает элементы сеанса hello в двух столбцах.</span><span class="sxs-lookup"><span data-stu-id="e3d48-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="e3d48-298">Если увеличить браузер изменится, упорядочение hello toothree столбцов.</span><span class="sxs-lookup"><span data-stu-id="e3d48-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="e3d48-299"><a name="bkmk_improvesessionbycode"></a>Улучшить представление SessionByCode hello</span><span class="sxs-lookup"><span data-stu-id="e3d48-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="e3d48-300">Наконец, можно исправить hello *SessionByCode* просмотра toomake его мобильной.</span><span class="sxs-lookup"><span data-stu-id="e3d48-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="e3d48-301">В браузере мобильного hello, коснитесь hello **тега** , а затем введите `asp` в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="e3d48-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="e3d48-302">Коснитесь hello **ASP.NET** ссылку.</span><span class="sxs-lookup"><span data-stu-id="e3d48-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="e3d48-303">Отображаются сеансы для тега ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="e3d48-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="e3d48-304">Выберите hello **построение одностраничного приложения с помощью ASP.NET и AngularJS** ссылку.</span><span class="sxs-lookup"><span data-stu-id="e3d48-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="e3d48-305">Представление рабочего стола по умолчанию Hello нормально, но можно улучшить вид hello легко с помощью некоторые компоненты начальной загрузки графического интерфейса пользователя.</span><span class="sxs-lookup"><span data-stu-id="e3d48-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="e3d48-306">Откройте *представления\\Главная\\SessionByCode.cshtml* и замените содержимое hello hello следующая разметка:</span><span class="sxs-lookup"><span data-stu-id="e3d48-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="e3d48-307">Разметка нового Hello использует начальной загрузки панелей стиля tooimprove hello мобильного представления.</span><span class="sxs-lookup"><span data-stu-id="e3d48-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="e3d48-308">Обновите hello мобильных браузеров.</span><span class="sxs-lookup"><span data-stu-id="e3d48-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="e3d48-309">Hello рисунке отражает только что внесенные изменения кода hello:</span><span class="sxs-lookup"><span data-stu-id="e3d48-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="e3d48-310">Заключение и сводка</span><span class="sxs-lookup"><span data-stu-id="e3d48-310">Wrap Up and Review</span></span>
<span data-ttu-id="e3d48-311">Этого учебника было показано, как toouse ASP.NET MVC 5 toodevelop мобильные веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="e3d48-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="e3d48-312">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="e3d48-312">These include:</span></span>

* <span data-ttu-id="e3d48-313">Развертывание tooan приложения ASP.NET MVC 5 веб-приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="e3d48-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="e3d48-314">Используйте начальной загрузки toocreate отвечать на запросы веб-документа в приложении MVC 5</span><span class="sxs-lookup"><span data-stu-id="e3d48-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="e3d48-315">переопределение макетов, представлений и частичных представлений, как глобально, так и для отдельного представления;</span><span class="sxs-lookup"><span data-stu-id="e3d48-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="e3d48-316">управления макетом и принудительное частичное переопределение с помощью свойства `RequireConsistentDisplayMode`;</span><span class="sxs-lookup"><span data-stu-id="e3d48-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="e3d48-317">Создание представлений, предназначенных для определенных обозревателей, например iPhone браузер hello</span><span class="sxs-lookup"><span data-stu-id="e3d48-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="e3d48-318">применение стиля Bootstrap в коде Razor.</span><span class="sxs-lookup"><span data-stu-id="e3d48-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="e3d48-319">См. также</span><span class="sxs-lookup"><span data-stu-id="e3d48-319">See Also</span></span>
* [<span data-ttu-id="e3d48-320">9 основных принципов динамического веб-дизайна</span><span class="sxs-lookup"><span data-stu-id="e3d48-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="e3d48-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="e3d48-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="e3d48-322">[Официальный блог о начальной загрузке][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="e3d48-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="e3d48-323">[Учебник по начальной загрузке Twitter от Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="e3d48-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="e3d48-324">[Hello площадки начальной загрузки][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="e3d48-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="e3d48-325">[Рекомендации от W3C по веб-приложениям для мобильных устройств][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="e3d48-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="e3d48-326">[Проектные рекомендации от W3C по запросам мультимедиа][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="e3d48-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e3d48-327">Изменения</span><span class="sxs-lookup"><span data-stu-id="e3d48-327">What's changed</span></span>
* <span data-ttu-id="e3d48-328">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e3d48-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

