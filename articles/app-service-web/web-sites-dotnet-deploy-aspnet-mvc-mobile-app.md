---
title: "Развертывание мобильного веб-приложения ASP.NET MVC 5 в службе приложений Azure"
description: "В этом учебнике объясняется, как развернуть веб-приложение в службе приложений Azure с помощью инструментов для мобильных устройств в веб-приложении ASP.NET MVC 5."
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
ms.openlocfilehash: c98e9b485c52a82e5be5c0f6b0b67912d1e890b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="b52db-103">Развертывание мобильного веб-приложения ASP.NET MVC 5 в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b52db-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="b52db-104">Этот учебник поможет вам освоить основы создания адаптированного для мобильных устройств веб-приложения ASP.NET MVC 5, а также его развертывания в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="b52db-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span></span> <span data-ttu-id="b52db-105">Для работы с этим руководством вам потребуется [Visual Studio Express 2013 для Web][Visual Studio Express 2013] или профессиональный выпуск Visual Studio, если она у вас уже есть.</span><span class="sxs-lookup"><span data-stu-id="b52db-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="b52db-106">Конечно, вы можете использовать [Visual Studio 2015] , но снимки экрана будут отличаться, и вам нужно будет использовать шаблоны 4.x ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b52db-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="b52db-107">Что вы создадите</span><span class="sxs-lookup"><span data-stu-id="b52db-107">What You'll Build</span></span>
<span data-ttu-id="b52db-108">В данном руководстве вам предстоит добавить компоненты для мобильных устройств в простое приложение списка конференции, которое доступно в [начальном проекте][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="b52db-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span></span> <span data-ttu-id="b52db-109">На следующем снимке экрана показаны сеансы ASP.NET в готовом приложении, отображаемые в эмуляторе браузера в средствах разработчика F12 Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="b52db-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="b52db-110">При помощи инструментов разработчика F12 в Internet Explorer 11 и [инструмента Fiddler][Fiddler] можно упростить отладку своего приложения.</span><span class="sxs-lookup"><span data-stu-id="b52db-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="b52db-111">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="b52db-111">Skills You'll Learn</span></span>
<span data-ttu-id="b52db-112">В этом учебнике вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="b52db-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="b52db-113">Как использовать Visual Studio 2013 для публикации веб-приложения напрямую в веб-приложение службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="b52db-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span></span>
* <span data-ttu-id="b52db-114">Как шаблоны ASP.NET MVC 5 используют платформу Bootstrap CSS для улучшения отображения на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="b52db-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="b52db-115">Как создать представления для мобильных устройств с учетом особенностей конкретных браузеров мобильных устройств, таких как iPhone и Android.</span><span class="sxs-lookup"><span data-stu-id="b52db-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span></span>
* <span data-ttu-id="b52db-116">Как создавать динамические представления (представления, соответствующие различным браузерам на разных устройствах).</span><span class="sxs-lookup"><span data-stu-id="b52db-116">How to create responsive views (views that respond to different browsers across devices)</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="b52db-117">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="b52db-117">Set up the development environment</span></span>
<span data-ttu-id="b52db-118">Настройте среду разработки, установив пакет SDK Azure для платформы .NET 2.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b52db-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="b52db-119">Чтобы установить пакет Azure SDK для .NET, щелкните приведенную ниже ссылку.</span><span class="sxs-lookup"><span data-stu-id="b52db-119">To install the Azure SDK for .NET, click the link below.</span></span> <span data-ttu-id="b52db-120">Если среда Visual Studio 2013 еще не установлена, ее можно установить по ссылке.</span><span class="sxs-lookup"><span data-stu-id="b52db-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span></span> <span data-ttu-id="b52db-121">Для работы с этим учебником требуется Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="b52db-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="b52db-122">[Пакет SDK Azure для Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="b52db-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="b52db-123">Щелкните в окне установщика веб-платформы **Установить** и продолжайте установку.</span><span class="sxs-lookup"><span data-stu-id="b52db-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span></span>

<span data-ttu-id="b52db-124">Кроме того, понадобится эмулятор браузера для мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="b52db-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="b52db-125">Можно использовать любое из следующих средств:</span><span class="sxs-lookup"><span data-stu-id="b52db-125">Any of the following will work:</span></span>

* <span data-ttu-id="b52db-126">Эмулятор браузера в [инструментах разработчика F12 Internet Explorer 11][EmulatorIE11] (используется в снимках экрана всех браузеров мобильного устройства).</span><span class="sxs-lookup"><span data-stu-id="b52db-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="b52db-127">Он содержит предустановки строк агента пользователя для Windows Phone 8, Windows Phone 7 и Apple iPad.</span><span class="sxs-lookup"><span data-stu-id="b52db-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="b52db-128">Эмулятор браузера в [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="b52db-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="b52db-129">Содержит предустановки для многих устройств Android, а также Apple iPhone, Apple iPad и Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="b52db-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="b52db-130">Также поддерживает эмуляцию событий прикосновения.</span><span class="sxs-lookup"><span data-stu-id="b52db-130">It also emulates touch events.</span></span>
* <span data-ttu-id="b52db-131">[Эмулятор Opera Mobile][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="b52db-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="b52db-132">К этой статье прилагаются следующие проекты Visual Studio с исходным кодом C\#.</span><span class="sxs-lookup"><span data-stu-id="b52db-132">Visual Studio projects with C\# source code are available to accompany this topic:</span></span>

* <span data-ttu-id="b52db-133">[Скачивание начального проекта][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="b52db-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="b52db-134">[Скачивание полного проекта][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="b52db-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="b52db-135"><a name="bkmk_DeployStarterProject"></a>Развертывание начального проекта в веб-приложении Azure</span><span class="sxs-lookup"><span data-stu-id="b52db-135"><a name="bkmk_DeployStarterProject"></a>Deploy the starter project to an Azure web app</span></span>
1. <span data-ttu-id="b52db-136">Скачайте [начальный проект][StarterProject] приложения списка конференции.</span><span class="sxs-lookup"><span data-stu-id="b52db-136">Download the conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="b52db-137">Затем в проводнике Windows щелкните загруженный ZIP-файл правой кнопкой мыши и выберите *Свойства*.</span><span class="sxs-lookup"><span data-stu-id="b52db-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="b52db-138">В диалоговом окне **Свойства** нажмите кнопку **Разблокировать**.</span><span class="sxs-lookup"><span data-stu-id="b52db-138">In the **Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="b52db-139">Разблокировка устраняет предупреждение системы безопасности, выводимое при попытке использовать *ZIP-файл* , загруженный из Интернета.</span><span class="sxs-lookup"><span data-stu-id="b52db-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>
4. <span data-ttu-id="b52db-140">Щелкните ZIP-файл правой кнопкой мыши и выберите **Извлечь все** , чтобы распаковать файл.</span><span class="sxs-lookup"><span data-stu-id="b52db-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span></span> 
5. <span data-ttu-id="b52db-141">В Visual Studio откройте файл *C#\Mvc5Mobile.sln*.</span><span class="sxs-lookup"><span data-stu-id="b52db-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="b52db-142">В обозревателе решений щелкните правой кнопкой мыши проект и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b52db-142">In Solution Explorer, right-click the project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="b52db-143">В окне веб-публикации щелкните **Служба приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b52db-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="b52db-144">Если вы еще не выполнили вход в Azure, щелкните **Добавить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="b52db-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="b52db-145">Следуйте указаниям по входу в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b52db-145">Follow the prompts to log into your Azure account.</span></span>
10. <span data-ttu-id="b52db-146">Теперь, когда вход в систему выполнен, диалоговое окно службы приложений должно отобразиться.</span><span class="sxs-lookup"><span data-stu-id="b52db-146">The App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="b52db-147">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b52db-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="b52db-148">В поле **Имя веб-приложения** задайте уникальный префикс имени приложения.</span><span class="sxs-lookup"><span data-stu-id="b52db-148">In the **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="b52db-149">Полностью определенным именем вашего веб-приложения будет *&lt;префикс>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="b52db-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="b52db-150">Также выберите или укажите имя существующей группы ресурсов в поле **Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="b52db-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="b52db-151">Затем щелкните **Создать** , чтобы создать новый план службы приложений</span><span class="sxs-lookup"><span data-stu-id="b52db-151">Then, click **New** to create a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="b52db-152">Настройте новый план службы приложений и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b52db-152">Configure the new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="b52db-153">В диалоговом окне "Создание службы приложений" нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b52db-153">Back in the Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="b52db-154">После создания ресурсов Azure диалоговое окно веб-публикации будет заполнено параметрами нового приложения.</span><span class="sxs-lookup"><span data-stu-id="b52db-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span></span> <span data-ttu-id="b52db-155">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b52db-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="b52db-156">Когда Visual Studio завершит публикацию начального проекта в веб-приложении Microsoft Azure, откроется классический браузер и отобразится действующее веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="b52db-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span></span>
15. <span data-ttu-id="b52db-157">Запустите эмулятор браузера мобильного устройства, скопируйте в него URL-адрес приложения конференции (*<prefix>*.azurewebsites.net), затем нажмите кнопку справа вверху и выберите **Поиск по тегу**.</span><span class="sxs-lookup"><span data-stu-id="b52db-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="b52db-158">Если вы используете Internet Explorer 11 как браузер по умолчанию, просто введите `F12`, затем нажмите `Ctrl+8` и измените профиль браузера на **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="b52db-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span></span> <span data-ttu-id="b52db-159">На рисунке ниже показано представление *AllTags* в портретной ориентации (выбирается в списке **Поиск по тегу**).</span><span class="sxs-lookup"><span data-stu-id="b52db-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="b52db-160">Выполняя отладку своего приложения MVC 5 с помощью Visual Studio, вы можете повторно опубликовать веб-приложение в Azure, чтобы проверить действующее приложение непосредственно из браузера мобильного устройства или эмулятора браузера.</span><span class="sxs-lookup"><span data-stu-id="b52db-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="b52db-161">Этот экран является очень удобным для чтения на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="b52db-161">The display is very readable on a mobile device.</span></span> <span data-ttu-id="b52db-162">Кроме того, вы уже можете просмотреть некоторые визуальные эффекты, применяемые платформой Bootstrap CSS.</span><span class="sxs-lookup"><span data-stu-id="b52db-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span></span>
<span data-ttu-id="b52db-163">Щелкните ссылку **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="b52db-163">Click the **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="b52db-164">Представление тегов ASP.NET адаптировано под размер экрана. Bootstrap делает это для вас автоматически.</span><span class="sxs-lookup"><span data-stu-id="b52db-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="b52db-165">Однако вы можете изменить это представление, чтобы оно лучше подходило для браузера мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="b52db-165">However, you can improve this view to better suit the mobile browser.</span></span> <span data-ttu-id="b52db-166">Например, столбец **Дата** читать неудобно.</span><span class="sxs-lookup"><span data-stu-id="b52db-166">For example, the **Date** column is difficult to read.</span></span> <span data-ttu-id="b52db-167">Позже из этого руководства вы узнаете, как изменить представление *AllTags*, чтобы адаптировать его для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span></span>

## <span data-ttu-id="b52db-168"><a name="bkmk_bootstrap"></a> Платформа начальной загрузки CSS</span><span class="sxs-lookup"><span data-stu-id="b52db-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="b52db-169">Встроенная поддержка начальной загрузки — это новая функция в шаблонах MVC 5.</span><span class="sxs-lookup"><span data-stu-id="b52db-169">New in the MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="b52db-170">Вы уже видели, как она моментально улучшает различные виды в приложении.</span><span class="sxs-lookup"><span data-stu-id="b52db-170">You have already seen how it immediately improves the different views in your application.</span></span> <span data-ttu-id="b52db-171">Например, панель навигации в верхней части автоматически сворачивается, если ширина браузера меньше.</span><span class="sxs-lookup"><span data-stu-id="b52db-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span></span> <span data-ttu-id="b52db-172">Попробуйте изменить размер окна классического браузера, и вы увидите, как изменится вид и поведение панели навигации.</span><span class="sxs-lookup"><span data-stu-id="b52db-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span></span> <span data-ttu-id="b52db-173">Это элемент динамического веб-дизайна, встроенный в Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="b52db-173">This is the responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="b52db-174">Чтобы увидеть, как бы выглядело веб-приложение без поддержки начальной загрузки, откройте *App\_Start\\BundleConfig.cs* и закомментируйте строки, содержащие *bootstrap.js* и *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="b52db-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="b52db-175">Следующий код показывает последние два оператора метода `RegisterBundles` после изменения:</span><span class="sxs-lookup"><span data-stu-id="b52db-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="b52db-176">Нажмите `Ctrl+F5` , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b52db-176">Press `Ctrl+F5` to run the application.</span></span>

<span data-ttu-id="b52db-177">Обратите внимание, что сворачиваемая панель навигации теперь стала обычным неупорядоченным списком.</span><span class="sxs-lookup"><span data-stu-id="b52db-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="b52db-178">Еще раз щелкните **Browse by tag** (Поиск по тегу), затем щелкните **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="b52db-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="b52db-179">В эмуляторе мобильного устройства вы можете видеть, что теперь его представление не адаптировано под размер экрана и приходится пользоваться прокруткой, чтобы увидеть правую часть таблицы.</span><span class="sxs-lookup"><span data-stu-id="b52db-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="b52db-180">Отмените сделанные изменения и обновите браузер мобильного устройства, чтобы проверить, восстановился ли адаптированный для мобильных устройств вид.</span><span class="sxs-lookup"><span data-stu-id="b52db-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="b52db-181">Вы можете использовать преимущества Bootstrap не только в ASP.NET MVC 5, но и в любом другом веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="b52db-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="b52db-182">Теперь эта функция встроена в шаблон проекта ASP.NET MVC 5, таким образом, ваше веб-приложение MVC 5 сможет по умолчанию использовать преимущества Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="b52db-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="b52db-183">Дополнительные сведения о начальной загрузке см. на сайте [Bootstrap][BootstrapSite].</span><span class="sxs-lookup"><span data-stu-id="b52db-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="b52db-184">В следующем разделе вы узнаете, как обеспечить представления для браузеров мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-184">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <span data-ttu-id="b52db-185"><a name="bkmk_overrideviews"></a> Переопределение представлений, макетов и частичных представлений</span><span class="sxs-lookup"><span data-stu-id="b52db-185"><a name="bkmk_overrideviews"></a> Override the Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="b52db-186">Вы можете переопределить любое представление (включая макеты и частичные представления) для браузеров мобильных устройств вообще, для отдельного браузера мобильных устройств или для любого конкретного браузера.</span><span class="sxs-lookup"><span data-stu-id="b52db-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="b52db-187">Чтобы создать вид для мобильных устройств, можно скопировать файл представления и добавить расширение *.Mobile* к имени файла.</span><span class="sxs-lookup"><span data-stu-id="b52db-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="b52db-188">Например, чтобы создать мобильное представление *Index*, скопируйте *Views\\Home\\Index.cshtml* в *Views\\Home\\Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b52db-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="b52db-189">В этом разделе для мобильных устройств будет создан специальный файл макета.</span><span class="sxs-lookup"><span data-stu-id="b52db-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="b52db-190">Сначала скопируйте *Views\\Shared\\\_Layout.cshtml* в *Views\\Shared\\\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b52db-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="b52db-191">Откройте *\_Layout.Mobile.cshtml* и измените заголовок с **Приложение MVC5** на **Приложение MVC5 (мобильное)**.</span><span class="sxs-lookup"><span data-stu-id="b52db-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="b52db-192">В каждом вызове `Html.ActionLink` панели навигации удалите "Поиск по" в каждой ссылке *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="b52db-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="b52db-193">В следующем коде показан законченный тег `<ul class="nav navbar-nav">` файла макета для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="b52db-194">Скопируйте файл *Views\\Home\\AllTags.cshtml* в *Views\\Home\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b52db-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="b52db-195">Откройте новый файл и измените элемент `<h2>` с "Tags" на "Tags (M)":</span><span class="sxs-lookup"><span data-stu-id="b52db-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="b52db-196">Перейдите на страницу тегов, используя классический браузер и эмулятор браузера для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="b52db-197">Эмулятор браузера мобильного устройства показывает два внесенных изменения (заголовки из *\_Layout.Mobile.cshtml* и *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="b52db-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="b52db-198">При этом изображение для настольного компьютера не изменилось (с заголовками из *\_Layout.cshtml* и *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="b52db-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="b52db-199"><a name="bkmk_browserviews"></a> Создание представлений для браузера</span><span class="sxs-lookup"><span data-stu-id="b52db-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="b52db-200">Кроме представлений для мобильных устройств и настольных компьютеров вы также можете создавать представления для отдельных браузеров.</span><span class="sxs-lookup"><span data-stu-id="b52db-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="b52db-201">Например, можно создать представления, адаптированные специально для браузера устройства iPhone или Android.</span><span class="sxs-lookup"><span data-stu-id="b52db-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span></span> <span data-ttu-id="b52db-202">В этом разделе вы узнаете, как создать макет для браузера iPhone и версию представления *AllTags* для iPhone.</span><span class="sxs-lookup"><span data-stu-id="b52db-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="b52db-203">Откройте файл *Global.asax* и добавьте следующий код в нижнюю часть метода `Application_Start`.</span><span class="sxs-lookup"><span data-stu-id="b52db-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="b52db-204">Этот код определяет новый режим отображения с именем iPhone, который будет использоваться для каждого входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="b52db-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="b52db-205">Если входящий запрос удовлетворяет условию, которое вы задали (то есть, если агент пользователя содержит строку iPhone), ASP.NET MVC выполнит поиск представлений, которые содержат в своем имени суффикс iPhone.</span><span class="sxs-lookup"><span data-stu-id="b52db-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="b52db-206">При добавлении особых режимов отображения для браузеров, например для iPhone и Android, обязательно установите первый аргумент равным `0` (вставьте в начале списка), чтобы особый режим для браузеров имел приоритет над шаблоном для мобильных устройств (*.Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="b52db-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="b52db-207">Если первым в списке будет шаблон для мобильных устройств, именно он будет выбираться вместо того режима отображения, который вы хотите использовать (приоритет получает первое соответствие, а шаблон для мобильных устройств соответствует всем браузерам мобильных устройств).</span><span class="sxs-lookup"><span data-stu-id="b52db-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="b52db-208">В коде щелкните правой кнопкой мыши `DefaultDisplayMode`, выберите **Разрешить**, а затем выберите `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="b52db-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="b52db-209">Это действие добавит ссылку на пространство имен `System.Web.WebPages`, в котором определяются типы `DisplayModeProvider` и `DefaultDisplayMode`.</span><span class="sxs-lookup"><span data-stu-id="b52db-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="b52db-210">Кроме того, вы можете вручную добавить следующую строку в раздел `using` файла.</span><span class="sxs-lookup"><span data-stu-id="b52db-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="b52db-211">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="b52db-211">Save the changes.</span></span> <span data-ttu-id="b52db-212">Скопируйте файл*Views\\Shared\\\_Layout.Mobile.cshtml* в *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b52db-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="b52db-213">Откройте новый файл и измените заголовок с `MVC5 Application (Mobile)` на `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="b52db-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="b52db-214">Скопируйте файл *Views\\Home\\AllTags.Mobile.cshtml* в *Views\\Home\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b52db-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="b52db-215">В новом файле измените значение элемента `<h2>` с "Tags (M)" на "Tags (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="b52db-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="b52db-216">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="b52db-216">Run the application.</span></span> <span data-ttu-id="b52db-217">Запустите эмулятор браузера мобильного устройства. Убедитесь, что для его агента пользователя задано значение "iPhone", и перейдите к представлению *AllTags*.</span><span class="sxs-lookup"><span data-stu-id="b52db-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="b52db-218">Если вы используете эмулятор браузера в средствах разработчика F12 Internet Explorer 11, задайте такие параметры эмуляции:</span><span class="sxs-lookup"><span data-stu-id="b52db-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span></span>

* <span data-ttu-id="b52db-219">профиль браузера — **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="b52db-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="b52db-220">строка агента пользователя — **Custom**</span><span class="sxs-lookup"><span data-stu-id="b52db-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="b52db-221">настраиваемая строка — **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="b52db-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="b52db-222">На следующем снимке экрана показано представление *AllTags* , отображаемое в эмуляторе в средствах разработчика F12 Internet Explorer 11 со специальной строкой агента пользователя (это строка агента пользователя iPhone 5C).</span><span class="sxs-lookup"><span data-stu-id="b52db-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="b52db-223">В браузере мобильного устройства выберите ссылку **Speakers** .</span><span class="sxs-lookup"><span data-stu-id="b52db-223">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="b52db-224">Ввиду отсутствия мобильного представления (*AllSpeakers.Mobile.cshtml*) докладчики по умолчанию (*AllSpeakers.cshtml*) отображаются с использованием представления мобильного макета (*\_Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="b52db-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="b52db-225">Как показано ниже, заголовок **Приложение MVC5 (мобильное)** определяется в *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b52db-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="b52db-226">Вы можете глобально отключить представление по умолчанию (не для мобильных устройств) из отображения в мобильном макете, задав для параметра `RequireConsistentDisplayMode` значение `true` в файле *Views\\\_ViewStart.cshtml* следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b52db-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="b52db-227">Если для `RequireConsistentDisplayMode` задано значение `true`, то мобильный макет (*\_Layout.Mobile.cshtml*) используется только для мобильных представлений (т. е. для файла представления используется форма ***ViewName**.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="b52db-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="b52db-228">Возможно, вы захотите установить для `RequireConsistentDisplayMode` значение `true`, если макет для мобильных устройств не работает с представлениями, не предназначенными для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="b52db-229">На следующем снимке экрана показано, как страница *Speakers* отображается при значении `RequireConsistentDisplayMode`, равном `true` (без строки "(Мобильное)" на панели навигации вверху страницы).</span><span class="sxs-lookup"><span data-stu-id="b52db-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="b52db-230">Вы можете отключить согласованный режим отображения, задав в файле представления для `RequireConsistentDisplayMode` значение `false`.</span><span class="sxs-lookup"><span data-stu-id="b52db-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="b52db-231">Приведенный ниже код разметки в файле *Views\\Home\\AllSpeakers.cshtml* устанавливает для `RequireConsistentDisplayMode` значение `false`.</span><span class="sxs-lookup"><span data-stu-id="b52db-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="b52db-232">В этом разделе мы рассмотрели, как создавать макеты и представления для мобильных устройств, а также как создавать макеты и представления для конкретных устройств, таких как iPhone.</span><span class="sxs-lookup"><span data-stu-id="b52db-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span>
<span data-ttu-id="b52db-233">При этом главное преимущество платформы Bootstrap CSS – это динамический макет, позволяющий применять одну таблицу стилей в браузерах настольных компьютеров, телефонов и планшетных устройств, создавая единый стиль отображения и поведения.</span><span class="sxs-lookup"><span data-stu-id="b52db-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span></span> <span data-ttu-id="b52db-234">В следующем разделе вы узнаете, как воспользоваться платформой Bootstrap для создания представлений, адаптированных для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span></span>

## <span data-ttu-id="b52db-235"><a name="bkmk_Improvespeakerslist"></a> Улучшение списка докладчиков</span><span class="sxs-lookup"><span data-stu-id="b52db-235"><a name="bkmk_Improvespeakerslist"></a> Improve the Speakers List</span></span>
<span data-ttu-id="b52db-236">Как вы только что увидели, представление *Speakers* удобно для чтения, но ссылки слишком малы, и касаться их на мобильном устройстве трудно.</span><span class="sxs-lookup"><span data-stu-id="b52db-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="b52db-237">В этом разделе вы узнаете, как создать представление *AllSpeakers*, адаптированное для мобильных устройств. Оно содержит большие, удобные для касания ссылки, а также поле поиска, позволяющее быстро находить докладчиков.</span><span class="sxs-lookup"><span data-stu-id="b52db-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="b52db-238">Вы можете воспользоваться стилем [группы связанного списка][linked list group] начальной загрузки, чтобы улучшить представление *Speakers*.</span><span class="sxs-lookup"><span data-stu-id="b52db-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span></span> <span data-ttu-id="b52db-239">В *Views\\Home\\AllSpeakers.cshtml* замените содержимое файла Razor кодом, приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="b52db-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span></span>

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

<span data-ttu-id="b52db-240">Атрибут `class="list-group"` в теге `<div>` применяет стиль списка начальной загрузки, а атрибут `class="input-group-item"` применяет стиль элементов списка начальной загрузки к каждой ссылке.</span><span class="sxs-lookup"><span data-stu-id="b52db-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span></span>

<span data-ttu-id="b52db-241">Обновите браузер для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-241">Refresh the mobile browser.</span></span> <span data-ttu-id="b52db-242">Обновленное представление выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b52db-242">The updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="b52db-243">Стиль [группы связанного списка][linked list group] начальной загрузки делает поле каждой ссылки полностью интерактивным, что значительно удобней для пользователя.</span><span class="sxs-lookup"><span data-stu-id="b52db-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="b52db-244">Переключитесь в представление для настольного компьютера, чтобы проверить единый стиль отображения и поведения.</span><span class="sxs-lookup"><span data-stu-id="b52db-244">Switch to the desktop view and observe the consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="b52db-245">Мы улучшили представление браузера для мобильных устройств, но перемещаться по длинному списку докладчиков все еще неудобно.</span><span class="sxs-lookup"><span data-stu-id="b52db-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="b52db-246">Исходные настройки Bootstrap не предусматривают функцию фильтра поиска, но вы можете ее добавить с помощью нескольких строк кода.</span><span class="sxs-lookup"><span data-stu-id="b52db-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="b52db-247">Сначала вы добавите в представление поле поиска, а затем с помощью кода JavaScript подключите функцию фильтра.</span><span class="sxs-lookup"><span data-stu-id="b52db-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span></span> <span data-ttu-id="b52db-248">В *Views\\Home\\AllSpeakers.cshtml* добавьте тег \<form\> сразу после тега \<h2\>, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b52db-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span></span>

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

<span data-ttu-id="b52db-249">Обратите внимание, что к обоим тегам (`<form>` и `<input>`) были применены стили начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="b52db-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span></span> <span data-ttu-id="b52db-250">Элемент `<span>` добавляет глиф начальной загрузки [glyphicon][glyphicon] в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="b52db-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span></span>

<span data-ttu-id="b52db-251">В папку *Scripts* добавьте файл JavaScript с именем *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="b52db-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="b52db-252">Откройте файл и вставьте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="b52db-252">Open the file and paste the following code into it:</span></span>

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
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

<span data-ttu-id="b52db-253">Также включите filter.js в свои зарегистрированные наборы.</span><span class="sxs-lookup"><span data-stu-id="b52db-253">You also need to include filter.js in your registered bundles.</span></span> <span data-ttu-id="b52db-254">Откройте файл *App\_Start\\BundleConfig.cs* и измените первые наборы.</span><span class="sxs-lookup"><span data-stu-id="b52db-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span></span> <span data-ttu-id="b52db-255">Измените первую инструкцию `bundles.Add` (для набора **jquery**), чтобы добавить *Scripts\\filter.js*, следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b52db-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="b52db-256">Набор **jquery** уже отображается в представлении по умолчанию *\_Layout*.</span><span class="sxs-lookup"><span data-stu-id="b52db-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span></span> <span data-ttu-id="b52db-257">Затем вы сможете использовать тот же код JavaScript для применения функции фильтра к другим представлениям списка.</span><span class="sxs-lookup"><span data-stu-id="b52db-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span></span>

<span data-ttu-id="b52db-258">Обновите браузер мобильного устройства и перейдите к представлению *AllSpeakers* .</span><span class="sxs-lookup"><span data-stu-id="b52db-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span></span> <span data-ttu-id="b52db-259">В поле поиска введите «sc».</span><span class="sxs-lookup"><span data-stu-id="b52db-259">In the search box, type "sc".</span></span> <span data-ttu-id="b52db-260">Теперь список докладчиков должен быть отфильтрован по вашей строке поиска.</span><span class="sxs-lookup"><span data-stu-id="b52db-260">The speakers list should now be filtered according to your search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="b52db-261"><a name="bkmk_improvetags"></a> Улучшение списка тегов</span><span class="sxs-lookup"><span data-stu-id="b52db-261"><a name="bkmk_improvetags"></a> Improve the Tags List</span></span>
<span data-ttu-id="b52db-262">Как и представление *Speakers*, представление *Tags* удобно для чтения, но ссылки слишком малы, и касаться их на мобильном устройстве трудно.</span><span class="sxs-lookup"><span data-stu-id="b52db-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="b52db-263">Вы можете исправить представление *Tags* таким же образом, как вы сделали с представлением *Speakers*, внеся описанные выше изменения в код. Но при этом необходимо использовать следующий синтаксис метода `Html.ActionLink` в *Views\\Home\\AllTags.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b52db-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="b52db-264">Вот как выглядит обновленный классический браузер:</span><span class="sxs-lookup"><span data-stu-id="b52db-264">The refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="b52db-265">А вот как выглядит обновленный браузер мобильного устройства:</span><span class="sxs-lookup"><span data-stu-id="b52db-265">And the refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="b52db-266">Возможно, вы обнаружите, что в браузере мобильного устройства по-прежнему отображается исходный формат списка. Что же случилось с вашим привлекательным стилем Bootstrap? Это следствие ранее выполненного действия при создании представлений для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span></span> <span data-ttu-id="b52db-267">Тем не менее, теперь вы используете платформу Bootstrap CSS и создаете динамический веб-дизайн, поэтому перейдите к следующему шагу и удалите эти представления и представления с макетом для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span></span> <span data-ttu-id="b52db-268">После выполнения этих действий обновленный браузер мобильного устройства отобразит стиль Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="b52db-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="b52db-269"><a name="bkmk_improvedates"></a> Улучшение списка дат</span><span class="sxs-lookup"><span data-stu-id="b52db-269"><a name="bkmk_improvedates"></a> Improve the Dates List</span></span>
<span data-ttu-id="b52db-270">Вы можете улучшить представление *Dates* таким же образом, как вы сделали с представлениями *Speakers* и *Tags*, внеся описанные выше изменения в код. Но при этом необходимо использовать следующий синтаксис метода `Html.ActionLink` в *Views\\Home\\AllDates.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b52db-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="b52db-271">Вот как будет выглядеть обновленное представление браузера мобильного устройства:</span><span class="sxs-lookup"><span data-stu-id="b52db-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="b52db-272">Вы также можете улучшить представление *Dates* , упорядочив отображение значений даты и времени по дате.</span><span class="sxs-lookup"><span data-stu-id="b52db-272">You can further improve the *Dates* view by organizing the date-time values by date.</span></span> <span data-ttu-id="b52db-273">Вы можете это сделать с помощью стиля [панелей][panels] начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="b52db-273">This can be done with the Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="b52db-274">Замените содержимое файла *Views\\Home\\Claims.cshtml* следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="b52db-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="b52db-275">Этот код создает отдельный тег `<div class="panel panel-primary">` для каждой отличной даты в списке и, как и ранее, использует [группу связанного списка][linked list group] для соответствующих ссылок.</span><span class="sxs-lookup"><span data-stu-id="b52db-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="b52db-276">Вот как выглядит браузер мобильного устройства при выполнении этого кода:</span><span class="sxs-lookup"><span data-stu-id="b52db-276">Here's what the mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="b52db-277">Переключитесь в классический браузер.</span><span class="sxs-lookup"><span data-stu-id="b52db-277">Switch to the desktop browser.</span></span> <span data-ttu-id="b52db-278">Также обратите внимание на единый стиль отображения.</span><span class="sxs-lookup"><span data-stu-id="b52db-278">Again, note the consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="b52db-279"><a name="bkmk_improvesessionstable"></a> Улучшение представления SessionsTable</span><span class="sxs-lookup"><span data-stu-id="b52db-279"><a name="bkmk_improvesessionstable"></a> Improve the SessionsTable View</span></span>
<span data-ttu-id="b52db-280">В этом разделе вы узнаете, как адаптировать представление *SessionsTable* для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="b52db-281">Для этого необходимо внести более обширные изменения, чем описанные выше.</span><span class="sxs-lookup"><span data-stu-id="b52db-281">This change is more extensive the previous changes.</span></span>

<span data-ttu-id="b52db-282">В браузере мобильного устройства коснитесь кнопки **Тег**, а затем введите `asp` в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="b52db-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="b52db-283">Коснитесь ссылки **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="b52db-283">Tap the **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="b52db-284">Как вы видите, отображение имеет формат таблицы, которая сейчас предназначена для просмотра в классическом браузере.</span><span class="sxs-lookup"><span data-stu-id="b52db-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span></span> <span data-ttu-id="b52db-285">При этом чтение в браузере мобильного устройства немного затруднено.</span><span class="sxs-lookup"><span data-stu-id="b52db-285">However, it's a little bit difficult to read on a mobile browser.</span></span> <span data-ttu-id="b52db-286">Чтобы исправить эту проблему, откройте файл *Views\\Home\\SessionsTable.cshtml* и замените его содержимое следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="b52db-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span></span>

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

<span data-ttu-id="b52db-287">Этот код выполняет 3 действия:</span><span class="sxs-lookup"><span data-stu-id="b52db-287">The code does 3 things:</span></span>

* <span data-ttu-id="b52db-288">использует [настраиваемую группу связанного списка][custom linked list group] начальной загрузки для форматирования данных сеанса по вертикали, чтобы все эти данные можно было читать в браузере мобильного устройства (используя классы, такие как list-group-item-text);</span><span class="sxs-lookup"><span data-stu-id="b52db-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="b52db-289">применяет к макету [систему сетки][grid system], чтобы элементы сеанса отображались в классическом браузере по горизонтали, а в браузере мобильного устройства — по вертикали (используя класс col-md-4);</span><span class="sxs-lookup"><span data-stu-id="b52db-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span></span>
* <span data-ttu-id="b52db-290">использует [динамические служебные программы][responsive utilities], чтобы скрыть теги сеансов при просмотре в браузере мобильного устройства (используя класс hidden-xs).</span><span class="sxs-lookup"><span data-stu-id="b52db-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span></span>

<span data-ttu-id="b52db-291">Вы также можете коснуться ссылки на заголовок, чтобы перейти к соответствующему сеансу.</span><span class="sxs-lookup"><span data-stu-id="b52db-291">You can also tap a title link to go to the respective session.</span></span> <span data-ttu-id="b52db-292">На рисунке ниже приведены изменения кода.</span><span class="sxs-lookup"><span data-stu-id="b52db-292">The image below reflects the code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="b52db-293">Система сетки начальной загрузки, которую вы применили, автоматически упорядочит сеансы в браузере мобильного устройства по вертикали.</span><span class="sxs-lookup"><span data-stu-id="b52db-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span></span> <span data-ttu-id="b52db-294">Кроме того, обратите внимание, что теги не отображаются.</span><span class="sxs-lookup"><span data-stu-id="b52db-294">Also, notice that the tags are not shown.</span></span> <span data-ttu-id="b52db-295">Переключитесь в классический браузер.</span><span class="sxs-lookup"><span data-stu-id="b52db-295">Switch to the desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="b52db-296">Обратите внимание, что в классическом браузере теги отображаются.</span><span class="sxs-lookup"><span data-stu-id="b52db-296">In the desktop browser, notice that the tags are now displayed.</span></span> <span data-ttu-id="b52db-297">Также вы можете видеть, что используемая система сетки Bootstrap, упорядочивает элементы сеанса в два столбца.</span><span class="sxs-lookup"><span data-stu-id="b52db-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span></span> <span data-ttu-id="b52db-298">Если вы увеличите браузер, то увидите, что упорядочение изменится на три столбца.</span><span class="sxs-lookup"><span data-stu-id="b52db-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span></span>

## <span data-ttu-id="b52db-299"><a name="bkmk_improvesessionbycode"></a> Улучшение представления SessionByCode</span><span class="sxs-lookup"><span data-stu-id="b52db-299"><a name="bkmk_improvesessionbycode"></a> Improve the SessionByCode View</span></span>
<span data-ttu-id="b52db-300">Наконец, вы можете исправить представление *SessionByCode* , чтобы адаптировать его для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span></span>

<span data-ttu-id="b52db-301">В браузере мобильного устройства коснитесь кнопки **Тег**, а затем введите `asp` в поле поиска.</span><span class="sxs-lookup"><span data-stu-id="b52db-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="b52db-302">Коснитесь ссылки **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="b52db-302">Tap the **ASP.NET** link.</span></span> <span data-ttu-id="b52db-303">Отобразятся сеансы для тега ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b52db-303">Sessions for the ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="b52db-304">Щелкните ссылку **Building a Single Page Application with ASP.NET and AngularJS** (Создание приложения на одной странице с помощью ASP.NET и AngularJS).</span><span class="sxs-lookup"><span data-stu-id="b52db-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="b52db-305">Представление для классического браузера выглядит замечательно, но вы можете его улучшить, используя некоторые компоненты графического пользовательского интерфейса Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="b52db-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="b52db-306">Откройте файл *Views\\Home\\SessionByCode.cshtml* и замените его содержимое следующей разметкой.</span><span class="sxs-lookup"><span data-stu-id="b52db-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span></span>

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

<span data-ttu-id="b52db-307">Новая разметка использует стиль панелей Bootstrap, чтобы улучшить представление для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span></span> 

<span data-ttu-id="b52db-308">Обновите браузер для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="b52db-308">Refresh the mobile browser.</span></span> <span data-ttu-id="b52db-309">Следующий рисунок отражает только что внесенные в код изменения:</span><span class="sxs-lookup"><span data-stu-id="b52db-309">The following image reflects the code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="b52db-310">Заключение и сводка</span><span class="sxs-lookup"><span data-stu-id="b52db-310">Wrap Up and Review</span></span>
<span data-ttu-id="b52db-311">В этом учебнике вы узнали, как использовать ASP.NET MVC 5 для разработки адаптированных для мобильных устройств веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="b52db-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span></span> <span data-ttu-id="b52db-312">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="b52db-312">These include:</span></span>

* <span data-ttu-id="b52db-313">развертывание приложения ASP.NET MVC 5 в веб-приложении службы приложений;</span><span class="sxs-lookup"><span data-stu-id="b52db-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span></span>
* <span data-ttu-id="b52db-314">использование Bootstrap для создания динамического веб-макета в приложении MVC 5;</span><span class="sxs-lookup"><span data-stu-id="b52db-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="b52db-315">переопределение макетов, представлений и частичных представлений, как глобально, так и для отдельного представления;</span><span class="sxs-lookup"><span data-stu-id="b52db-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="b52db-316">управления макетом и принудительное частичное переопределение с помощью свойства `RequireConsistentDisplayMode`;</span><span class="sxs-lookup"><span data-stu-id="b52db-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="b52db-317">создание представлений для конкретных браузеров, таких как браузер iPhone;</span><span class="sxs-lookup"><span data-stu-id="b52db-317">Create views that target specific browsers, such as the iPhone browser</span></span>
* <span data-ttu-id="b52db-318">применение стиля Bootstrap в коде Razor.</span><span class="sxs-lookup"><span data-stu-id="b52db-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="b52db-319">См. также</span><span class="sxs-lookup"><span data-stu-id="b52db-319">See Also</span></span>
* [<span data-ttu-id="b52db-320">9 основных принципов динамического веб-дизайна</span><span class="sxs-lookup"><span data-stu-id="b52db-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="b52db-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="b52db-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="b52db-322">[Официальный блог о начальной загрузке][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="b52db-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="b52db-323">[Учебник по начальной загрузке Twitter от Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="b52db-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="b52db-324">[Интерактивная площадка начальной загрузки][The Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="b52db-324">[The Bootstrap Playground][The Bootstrap Playground]</span></span>
* <span data-ttu-id="b52db-325">[Рекомендации от W3C по веб-приложениям для мобильных устройств][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="b52db-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="b52db-326">[Проектные рекомендации от W3C по запросам мультимедиа][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="b52db-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b52db-327">Изменения</span><span class="sxs-lookup"><span data-stu-id="b52db-327">What's changed</span></span>
* <span data-ttu-id="b52db-328">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b52db-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

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
[The Bootstrap Playground]: http://www.bootply.com/
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

