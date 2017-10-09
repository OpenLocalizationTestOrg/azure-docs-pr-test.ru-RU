---
title: "бизнес приложения Azure с проверкой подлинности AD FS aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate бизнес приложения в службе приложений Azure, который выполняет проверку подлинности с локальным STS. Этот учебник предназначен для AD FS как hello локальной службы маркеров безопасности."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="17ace-104">Создание бизнес-приложения Azure с проверкой подлинности AD FS</span><span class="sxs-lookup"><span data-stu-id="17ace-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="17ace-105">В этой статье показано, как toocreate ASP.NET MVC для бизнес-приложений в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) с помощью локальной [служб федерации Active Directory](http://technet.microsoft.com/library/hh831502.aspx) как поставщик удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="17ace-106">Этот сценарий можно использовать, когда необходимо toocreate бизнес-приложений в службе приложений Azure, но ваша организация требует toobe каталог данных, хранящихся на месте.</span><span class="sxs-lookup"><span data-stu-id="17ace-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="17ace-107">Обзор hello enterprise для разных параметров проверки подлинности и авторизации для службы приложений Azure см. в разделе [аутентификация с помощью локальной Active Directory в приложении Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="17ace-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="17ace-108">Что будет строиться</span><span class="sxs-lookup"><span data-stu-id="17ace-108">What you will build</span></span>
<span data-ttu-id="17ace-109">Простое приложение ASP.NET в веб-приложениях службы приложений Azure создаст с hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="17ace-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="17ace-110">проверка подлинности пользователей в AD FS</span><span class="sxs-lookup"><span data-stu-id="17ace-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="17ace-111">Использует `[Authorize]` tooauthorize пользователей для различных действий</span><span class="sxs-lookup"><span data-stu-id="17ace-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="17ace-112">Статическая конфигурация для отладки в Visual Studio и публикации веб-приложений служб tooApp (один раз настройки, отладки и публикации в любое время)</span><span class="sxs-lookup"><span data-stu-id="17ace-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="17ace-113">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="17ace-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="17ace-114">Требуется hello следующие toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="17ace-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="17ace-115">Локальному развертывания AD FS (конца в конец Пошаговое руководство по лаборатории тестирования hello, используемые в этом учебнике см. в разделе [лаборатории тестирования: автономный STS с AD FS на виртуальной Машине Azure (для тестирования)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="17ace-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="17ace-116">Доверие проверяющей стороны toocreate разрешения в управления AD FS</span><span class="sxs-lookup"><span data-stu-id="17ace-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="17ace-117">Visual Studio 2013 с обновлением 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="17ace-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="17ace-118">[Пакет SDK Azure, начиная с версии 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) .</span><span class="sxs-lookup"><span data-stu-id="17ace-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="17ace-119">Использование примера приложения в качестве шаблона бизнес-приложения</span><span class="sxs-lookup"><span data-stu-id="17ace-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="17ace-120">Здравствуйте, образец приложения в этом учебнике [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), созданных team hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="17ace-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="17ace-121">Так как службы федерации Active Directory поддерживает WS-Federation, можно использовать как шаблон toocreate бизнес-приложения с легкостью.</span><span class="sxs-lookup"><span data-stu-id="17ace-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="17ace-122">Он имеет hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="17ace-122">It has hello following features:</span></span>

* <span data-ttu-id="17ace-123">Использует [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate с локальное развертывание AD FS</span><span class="sxs-lookup"><span data-stu-id="17ace-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="17ace-124">функции входа и выхода</span><span class="sxs-lookup"><span data-stu-id="17ace-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="17ace-125">Использует [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (вместо Windows Identity Foundation), который является hello будущих ASP.NET и гораздо проще tooset для использования проверки подлинности и авторизации, чем WIF</span><span class="sxs-lookup"><span data-stu-id="17ace-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="17ace-126">Настройка образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="17ace-126">Set up hello sample application</span></span>
1. <span data-ttu-id="17ace-127">Клонировать или загрузить решение образца hello в [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="17ace-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="17ace-128">Здравствуйте, инструкции по [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) показывается, как tooset приложения hello в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="17ace-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="17ace-129">Однако в этом учебнике, он настраивается с AD FS, поэтому вместо этого выполните здесь шаги hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="17ace-130">Откройте решение hello, а затем Controllers\AccountController.cs в hello **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="17ace-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="17ace-131">Вы увидите, что код hello просто направляет пользователя hello tooauthenticate запрос проверки подлинности, с помощью WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="17ace-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="17ace-132">Вся проверка подлинности настраивается в App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="17ace-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="17ace-133">Откройте App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="17ace-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="17ace-134">В hello `ConfigureAuth` метод, строка hello Примечание:</span><span class="sxs-lookup"><span data-stu-id="17ace-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="17ace-135">В OWIN Здравствуй, мир этот фрагмент действительно является hello минимальные необходимые проверки подлинности WS-Federation tooconfigure исходного состояния системы.</span><span class="sxs-lookup"><span data-stu-id="17ace-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="17ace-136">Это гораздо проще и более элегантный, чем WIF, где введенный Web.config в XML по всему месте hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="17ace-137">Здравствуйте только сведения, необходимые hello проверяющей стороны (RP) идентификатор и hello URL-адрес файла метаданных службы AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="17ace-138">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="17ace-138">Here's an example:</span></span>
   
   * <span data-ttu-id="17ace-139">Идентификатор RP: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="17ace-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="17ace-140">Адрес метаданных: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="17ace-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="17ace-141">В App_Start\Startup.Auth.cs измените следующие определения статическую строку hello:</span><span class="sxs-lookup"><span data-stu-id="17ace-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="17ace-142">Сделан hello соответствующих изменений в файле Web.config. Откройте hello Web.config и добавьте следующие параметры приложения hello:</span><span class="sxs-lookup"><span data-stu-id="17ace-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="17ace-143">Заполните значения ключа hello в зависимости от соответствующих среде.</span><span class="sxs-lookup"><span data-stu-id="17ace-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="17ace-144">Построение toomake приложения hello, проверьте, нет ли ошибок.</span><span class="sxs-lookup"><span data-stu-id="17ace-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="17ace-145">Вот и все.</span><span class="sxs-lookup"><span data-stu-id="17ace-145">That's it.</span></span> <span data-ttu-id="17ace-146">Теперь пример приложения hello — Готово toowork с AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="17ace-147">Необходимо по-прежнему tooconfigure доверия проверяющей Стороны с помощью этого приложения в AD FS более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="17ace-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="17ace-148">Развертывание tooAzure приложения hello образец приложения службы веб-приложений</span><span class="sxs-lookup"><span data-stu-id="17ace-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="17ace-149">Здесь опубликовать hello приложения tooa веб-приложения в веб-приложениях службы приложений при сохранении среды отладки hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="17ace-150">Обратите внимание, что ты toopublish приложения hello раньше, чем он RP доверия AD FS, чтобы проверка подлинности по-прежнему не работает еще.</span><span class="sxs-lookup"><span data-stu-id="17ace-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="17ace-151">Однако если сделать это теперь вы можете получить hello web URL-адрес приложения, которые можно использовать позже tooconfigure hello RP доверия.</span><span class="sxs-lookup"><span data-stu-id="17ace-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="17ace-152">Щелкните правой кнопкой мыши свой проект и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="17ace-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="17ace-153">Щелкните **Служба приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="17ace-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="17ace-154">Если вы еще не выполнили вход tooAzure, нажмите кнопку **входа** и использовать учетную запись Microsoft hello toosign вашей подписки Azure в.</span><span class="sxs-lookup"><span data-stu-id="17ace-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="17ace-155">После входа щелкните **New** toocreate веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="17ace-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="17ace-156">Заполните все обязательные поля.</span><span class="sxs-lookup"><span data-stu-id="17ace-156">Fill in all required fields.</span></span> <span data-ttu-id="17ace-157">Вы собираетесь tooconnect tooon локальных данных более поздней версии, поэтому нельзя создавать базы данных для этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="17ace-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="17ace-158">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="17ace-158">Click **Create**.</span></span> <span data-ttu-id="17ace-159">После создания веб-приложения hello открыто диалоговое окно приветствия публикации веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="17ace-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="17ace-160">В **URL-адрес назначения**, изменить **http** слишком**https**.</span><span class="sxs-lookup"><span data-stu-id="17ace-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="17ace-161">Скопируйте hello весь URL-адрес tooa текстовый редактор для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="17ace-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="17ace-162">Затем щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="17ace-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="17ace-163">В Visual Studio откройте в своем проекте файл **Web.Release.config** .</span><span class="sxs-lookup"><span data-stu-id="17ace-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="17ace-164">Вставьте следующий XML-код в hello hello `<configuration>` тег и замените значение ключа hello URL-адрес веб-приложения вашей публикации.</span><span class="sxs-lookup"><span data-stu-id="17ace-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="17ace-165">Когда закончите, у вас есть два идентификатора RP настроены в проекте, один для вашей среды отладки в Visual Studio и один для hello опубликованных веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="17ace-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="17ace-166">Вы настроите доверие проверяющей Стороны для каждого из двух сред hello в AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="17ace-167">Во время отладки, параметры приложения hello в файле Web.config, используемые toomake вашей **отладки** конфигурации работают с AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="17ace-168">При публикации (по умолчанию hello **выпуска** публикуется конфигурации), преобразованный Web.config загружается с учетом изменений параметра приложения hello в Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="17ace-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="17ace-169">Если требуется tooattach hello опубликованных веб-приложения в отладчик Azure toohello (т. е. его необходимо загрузить символы отладки кода в hello опубликованных веб-приложения), можно создать клон hello конфигурация для отладки Azure отладки, но с помощью пользовательских файле Web.config преобразовать) Например, Web.AzureDebug.config), используются параметры приложения hello с Web.Release.config. Это позволяет toomaintain статической конфигурации hello различных средах.</span><span class="sxs-lookup"><span data-stu-id="17ace-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="17ace-170">Настройка доверия с проверяющей стороной в оснастке управления AD FS</span><span class="sxs-lookup"><span data-stu-id="17ace-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="17ace-171">Теперь вам требуется tooconfigure доверия проверяющей Стороны в управления AD FS, прежде чем использовать приложение-образец и фактически проверку подлинности с AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="17ace-172">Необходимо будет tooset копирование два отдельных RP доверия: для вашей среды отладки и для опубликованных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="17ace-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="17ace-173">Убедитесь, что повторить hello следующие шаги для обеих сред.</span><span class="sxs-lookup"><span data-stu-id="17ace-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="17ace-174">Войдите в систему учетные данные, имеющие права управления tooAD FS на сервере AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="17ace-175">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-175">Open AD FS Management.</span></span> <span data-ttu-id="17ace-176">Щелкните правой кнопкой мыши **AD FS\Trusted Relationships\Relying Party Trusts** и выберите **Добавить отношение доверия проверяющей стороны**.</span><span class="sxs-lookup"><span data-stu-id="17ace-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="17ace-177">В hello **Выбор источника данных** выберите **вручную вводить данные о проверяющей стороне hello**.</span><span class="sxs-lookup"><span data-stu-id="17ace-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="17ace-178">В hello **укажите отображаемое имя** введите отображаемое имя для приложения hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ace-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="17ace-179">В hello **выберите протокол** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ace-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="17ace-180">В hello **Настройка сертификата** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ace-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="17ace-181">Так как уже должен использоваться протокол HTTPS, зашифрованные токены необязательны.</span><span class="sxs-lookup"><span data-stu-id="17ace-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="17ace-182">Если действительно tooencrypt токенов AD FS на этой странице, необходимо также добавить расшифровки логика в коде.</span><span class="sxs-lookup"><span data-stu-id="17ace-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="17ace-183">Дополнительную информацию см. в статье [Ручная настройка промежуточного слоя OWIN WS-Federation и прием зашифрованных маркеров](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="17ace-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="17ace-184">Прежде чем выполняется переход к следующему шагу hello, необходим один фрагмент данных из проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17ace-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="17ace-185">В свойствах проекта hello, обратите внимание, hello **URL-адрес SSL** приложения hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="17ace-186">В управление AD FS в hello **настроить URL-адрес** страница hello **проверяющей стороной мастер добавления отношений доверия**выберите **включить поддержку пассивного протокола WS-Federation hello** и Введите в hello URL-адрес SSL проекта Visual Studio, записанное в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="17ace-187">Затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ace-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="17ace-188">URL-адрес указывает, где toosend hello клиента после проверки подлинности завершается успешно.</span><span class="sxs-lookup"><span data-stu-id="17ace-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="17ace-189">Для среды отладки hello, он должен быть <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="17ace-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="17ace-190">Для опубликованных веб-приложения hello следует hello URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="17ace-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="17ace-191">В hello **настроить идентификаторы** , убедитесь, что URL-адрес SSL проекта уже присутствует в списке и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ace-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="17ace-192">Нажмите кнопку **Далее** все hello способом toohello конец hello мастере с использованием параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="17ace-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="17ace-193">В App_Start\Startup.Auth.cs проекта Visual Studio этот идентификатор противопоставляется значение hello <code>WsFederationAuthenticationOptions.Wtrealm</code> во время федеративной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="17ace-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="17ace-194">По умолчанию URL-адрес приложения hello из предыдущего шага hello добавляется в качестве идентификатора RP.</span><span class="sxs-lookup"><span data-stu-id="17ace-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="17ace-195">Настройка hello приложение STS для проекта в AD FS теперь завершена.</span><span class="sxs-lookup"><span data-stu-id="17ace-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="17ace-196">Далее следует настроить этот toosend приложения hello утверждения, необходимые для приложения.</span><span class="sxs-lookup"><span data-stu-id="17ace-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="17ace-197">Hello **изменение правил для утверждений** открытии диалогового окна по умолчанию для вас в конце hello приветствия мастера, можно запустить немедленно.</span><span class="sxs-lookup"><span data-stu-id="17ace-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="17ace-198">Настроим Здравствуйте, по крайней мере следующие утверждения (со схемами в круглых скобках):</span><span class="sxs-lookup"><span data-stu-id="17ace-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="17ace-199">Имя (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name -), используемые ASP.NET toohydrate `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="17ace-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="17ace-200">Имя участника (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - используется toouniquely пользователя определите пользователей в организации hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="17ace-201">Членство в группах как роли (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - может использоваться с `[Authorize(Roles="role1, role2,...")]` tooauthorize Декорирование контроллеров и действий.</span><span class="sxs-lookup"><span data-stu-id="17ace-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="17ace-202">На самом деле этот подход может не быть hello большинство высокопроизводительных для авторизации ролей.</span><span class="sxs-lookup"><span data-stu-id="17ace-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="17ace-203">Если ваши пользователи AD относятся toohundreds групп безопасности, они становятся сотни утверждений ролей в маркере SAML hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="17ace-204">Альтернативный подход — toosend одной роли условно утверждения в зависимости от членства пользователя hello в определенной группе.</span><span class="sxs-lookup"><span data-stu-id="17ace-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="17ace-205">Однако в нашем учебнике мы будем придерживаться простого подхода.</span><span class="sxs-lookup"><span data-stu-id="17ace-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="17ace-206">ИД имени (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) — используется для проверки защиты от подделки.</span><span class="sxs-lookup"><span data-stu-id="17ace-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="17ace-207">Дополнительные сведения об использовании toomake ее защиты от подделки проверки см. в разделе hello **добавить функции бизнес-** раздел [Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="17ace-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="17ace-208">Hello типы утверждений вы должны tooconfigure для приложения зависит от потребностей вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="17ace-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="17ace-209">Hello список утверждений поддерживается в приложениях Azure Active Directory (т. е. отношения доверия проверяющей Стороны) например, см. [типы поддерживаемых токенов и утверждений](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="17ace-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="17ace-210">В диалоговом окне приветствия изменение правил для утверждений, щелкните **добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="17ace-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="17ace-211">Настройка утверждений hello имя участника-пользователя и роли, как показано на снимке экрана приветствия и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="17ace-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="17ace-212">Создайте временный имя, идентификатор утверждений, используя hello шаги демонстрируются в [имя идентификаторы в утверждения SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="17ace-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="17ace-213">Щелкните **Добавить правило** еще раз.</span><span class="sxs-lookup"><span data-stu-id="17ace-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="17ace-214">Выберите **Отправка утверждений с помощью настраиваемого правила** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ace-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="17ace-215">Вставить hello следующие правила языка в hello **настраиваемого правила** поле, имя правила hello **на идентификатор сеанса** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="17ace-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="17ace-216">Настраиваемое правило должно выглядеть, как на этом снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="17ace-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="17ace-217">Щелкните **Добавить правило** еще раз.</span><span class="sxs-lookup"><span data-stu-id="17ace-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="17ace-218">Выберите **Преобразование входящего утверждения** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="17ace-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="17ace-219">Настройте правила hello, как показано на снимке экрана приветствия (с использованием типа утверждения hello, созданный в настраиваемое правило hello) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="17ace-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="17ace-220">Подробные сведения о hello действия для временного идентификатора имени утверждения hello. в разделе [имя идентификаторы в утверждения SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="17ace-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="17ace-221">Нажмите кнопку **применить** в hello **изменение правил для утверждений** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="17ace-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="17ace-222">Он должен выглядеть так hello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="17ace-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="17ace-223">Не забудьте, что эти шаги необходимо повторить для среды отладки и опубликованного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="17ace-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="17ace-224">Тестирование федеративной проверки подлинности для приложения</span><span class="sxs-lookup"><span data-stu-id="17ace-224">Test federated authentication for your application</span></span>
<span data-ttu-id="17ace-225">Вам будут готовы tootest логику приложения проверки подлинности для AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="17ace-226">В моей лабораторной среды AD FS у меня есть тестового пользователя, к которому относится tooa тестовую группу в Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="17ace-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="17ace-227">tootest проверки подлинности в отладчике hello, все, что нужно toodo теперь является типом `F5`.</span><span class="sxs-lookup"><span data-stu-id="17ace-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="17ace-228">Если требуется проверка подлинности tootest в опубликованных веб-приложения hello перейдите toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="17ace-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="17ace-229">После загрузки веб-приложения hello, нажмите кнопку **входа**.</span><span class="sxs-lookup"><span data-stu-id="17ace-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="17ace-230">Теперь вы должны получить либо имя входа диалогового окна или hello страницу входа от службы федерации Active Directory, в зависимости от метода проверки подлинности hello, выбранного с помощью AD FS.</span><span class="sxs-lookup"><span data-stu-id="17ace-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="17ace-231">Вот что получается в Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="17ace-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="17ace-232">После входа под учетной записью пользователя в домене hello AD развертывания hello AD FS должно отобразиться Домашняя страница приветствия с **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="17ace-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="17ace-233">в углу hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-233">in hello corner.</span></span> <span data-ttu-id="17ace-234">Вот что у меня получается.</span><span class="sxs-lookup"><span data-stu-id="17ace-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="17ace-235">Таким образом была успешной hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="17ace-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="17ace-236">Приложение успешно достигнут AD FS, а также соответствующий идентификатор проверяющей Стороны находится в hello базы данных AD FS</span><span class="sxs-lookup"><span data-stu-id="17ace-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="17ace-237">AD FS успешно прошел проверку подлинности пользователя AD и перенаправления обратно домашней страницы приложения toohello</span><span class="sxs-lookup"><span data-stu-id="17ace-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="17ace-238">Службы федерации Active Directory как имя успешно отправленных hello утверждения приложения tooyour (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name), обозначенный фактов hello hello пользователя имя будет отображаться в углу hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="17ace-239">Если отсутствует утверждение "имя" hello, вы бы увидеть **Hello,!**.</span><span class="sxs-lookup"><span data-stu-id="17ace-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="17ace-240">Если взглянуть на одну\_LoginPartial.cshtml, обнаружится, что он использует `User.Identity.Name` имя пользователя toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="17ace-241">Как упоминалось ранее, если имя hello утверждения из hello проверку подлинности пользователей, не доступных в маркере SAML hello, ASP.NET hydrates это свойство вместе с ним.</span><span class="sxs-lookup"><span data-stu-id="17ace-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="17ace-242">toosee, все hello утверждения, отправляемые службой AD FS, установить точку останова в Controllers\HomeController.cs, при hello индекс метода действия.</span><span class="sxs-lookup"><span data-stu-id="17ace-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="17ace-243">После проверки подлинности пользователя hello проверять hello `System.Security.Claims.Current.Claims` коллекции.</span><span class="sxs-lookup"><span data-stu-id="17ace-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="17ace-244">Авторизация пользователей для определенных контроллеров и действий</span><span class="sxs-lookup"><span data-stu-id="17ace-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="17ace-245">С момента включения членства в группах как утверждения роли в конфигурации доверия проверяющей Стороны, теперь можно использовать их непосредственно в hello `[Authorize(Roles="...")]` декорирования для контроллеров и действий.</span><span class="sxs-lookup"><span data-stu-id="17ace-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="17ace-246">В бизнес приложения с шаблоном hello Создание-чтение-обновления и удаления (CRUD) вы можете разрешить tooaccess конкретных ролей каждого действия.</span><span class="sxs-lookup"><span data-stu-id="17ace-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="17ace-247">На данном этапе будет просто опробовать эту возможность на существующий контроллер Home hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="17ace-248">Откройте Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="17ace-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="17ace-249">Украшение hello `About` и `Contact` действие методов аналогичные toohello после кода, с помощью членства в группах безопасности с проверкой подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="17ace-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="17ace-250">Поскольку я добавил **тестового пользователя** слишком**тестовую группу** в моей лабораторной среды AD FS, я буду использовать тестовую группу tootest авторизации на `About`.</span><span class="sxs-lookup"><span data-stu-id="17ace-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="17ace-251">Для `Contact`, я протестируем hello отрицательное регистр **"Администраторы домена"**, toowhich **проверки пользователя** не принадлежит.</span><span class="sxs-lookup"><span data-stu-id="17ace-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="17ace-252">Запустите отладчик hello, введя `F5` входа, а затем выберите **о**.</span><span class="sxs-lookup"><span data-stu-id="17ace-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="17ace-253">Вы теперь должен Просмотр hello `~/About/Index` страница успешно, если ваш прошедший проверку пользователь авторизован для этого действия.</span><span class="sxs-lookup"><span data-stu-id="17ace-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="17ace-254">Сейчас, нажмите кнопку **контакт**, которой в моем случае не следует авторизовать **тестового пользователя** для hello действия.</span><span class="sxs-lookup"><span data-stu-id="17ace-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="17ace-255">Тем не менее перенаправленный tooAD федерации Active Directory, в конечном итоге показывает это сообщение используется hello браузера:</span><span class="sxs-lookup"><span data-stu-id="17ace-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="17ace-256">Если эта ошибка в средстве просмотра событий на сервер AD FS hello изучать, вы увидите это сообщение исключения:</span><span class="sxs-lookup"><span data-stu-id="17ace-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="17ace-257">Hello причина этой ошибки заключается в том, что по умолчанию MVC возвращает подлинности 401 при роли пользователя нет прав.</span><span class="sxs-lookup"><span data-stu-id="17ace-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="17ace-258">При этом запускается повторная проверка подлинности запроса tooyour поставщика удостоверений (AD FS).</span><span class="sxs-lookup"><span data-stu-id="17ace-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="17ace-259">Поскольку hello пользователь уже прошел проверку, службы федерации Active Directory возвращает toohello одной странице, которое затем создает другой 401, создания цикла обработки перенаправления.</span><span class="sxs-lookup"><span data-stu-id="17ace-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="17ace-260">Будут переопределены AuthorizeAttribute `HandleUnauthorizedRequest` метод с простой логики tooshow то, что имеет смысл вместо продолжение цикла перенаправления hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="17ace-261">Создайте файл в проект hello с именем AuthorizeAttribute.cs и hello вставьте следующий код в него.</span><span class="sxs-lookup"><span data-stu-id="17ace-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="17ace-262">Hello переопределить код отправляет HTTP 403 (запрещено) вместо HTTP 401 (не санкционировано) в случаях, прошедшего проверку подлинности, но несанкционированного.</span><span class="sxs-lookup"><span data-stu-id="17ace-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="17ace-263">Запуск отладчика hello с `F5`.</span><span class="sxs-lookup"><span data-stu-id="17ace-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="17ace-264">Щелкнув **Контакт** , теперь можно увидеть более информативное (хотя и непривлекательное) сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="17ace-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="17ace-265">Повторной публикации приложения hello tooAzure приложения службы веб-приложений и тестирования поведения hello динамической приложения hello.</span><span class="sxs-lookup"><span data-stu-id="17ace-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="17ace-266">Подключение tooon локальные данные</span><span class="sxs-lookup"><span data-stu-id="17ace-266">Connect tooon-premises data</span></span>
<span data-ttu-id="17ace-267">Что нужно tooimplement бизнес-приложения с AD FS вместо Azure Active Directory обусловлено проблемы соответствия с сохранением организации данных во внешней среде.</span><span class="sxs-lookup"><span data-stu-id="17ace-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="17ace-268">Это также может означать, что веб-приложения в Azure необходимо получить доступ к локальным базам данных, поскольку toouse не допускаются [базы данных SQL](/services/sql-database/) как hello уровня данных для развертывания веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="17ace-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="17ace-269">Веб-приложения службы приложений Azure поддерживают доступ к локальным базам данных двумя способами: с помощью [гибридных подключений](../biztalk-services/integration-hybrid-connection-overview.md) и [виртуальных сетей](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="17ace-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="17ace-270">Дополнительную информацию см. в статье [Использование интеграции VNET и гибридных подключений с веб-приложениями службы приложений Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="17ace-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="17ace-271">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="17ace-271">Further resources</span></span>
* [<span data-ttu-id="17ace-272">Проверка подлинности в приложении Azure с помощью локального каталога Active Directory</span><span class="sxs-lookup"><span data-stu-id="17ace-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="17ace-273">Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17ace-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="17ace-274">Использовать hello в локальной организации параметр проверки подлинности (ADFS) с ASP.NET в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="17ace-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="17ace-275">Перенос tooKatana VS2013 Web проекта из WIF</span><span class="sxs-lookup"><span data-stu-id="17ace-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="17ace-276">Обзор служб федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="17ace-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="17ace-277">Спецификация WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="17ace-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

