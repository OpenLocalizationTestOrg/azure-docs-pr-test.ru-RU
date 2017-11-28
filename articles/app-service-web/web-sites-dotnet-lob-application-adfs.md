---
title: "Создание бизнес-приложения Azure с аутентификацией AD FS | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как создать бизнес-приложение в службе приложений Azure, которая выполняет проверку подлинности с помощью службы маркеров безопасности. В этом руководстве рассматриваются службы федерации Acive Directory в качестве локальной службы STS."
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
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="c42b1-104">Создание бизнес-приложения Azure с проверкой подлинности AD FS</span><span class="sxs-lookup"><span data-stu-id="c42b1-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="c42b1-105">Из этой статьи вы узнаете, как создать бизнес-приложение ASP.NET MVC в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) с использованием локальных [служб федерации Active Directory](http://technet.microsoft.com/library/hh831502.aspx) в качестве поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c42b1-105">This article shows you how to create an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as the identity provider.</span></span> <span data-ttu-id="c42b1-106">Этот сценарий можно использовать, когда необходимо создать бизнес-приложения в службе приложений Azure, но организация требует сохранять все данные каталога локально.</span><span class="sxs-lookup"><span data-stu-id="c42b1-106">This scenario can work when you want to create line-of-business applications in Azure App Service but your organization requires directory data to be stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="c42b1-107">Обзор вариантов корпоративной аутентификации и авторизации для службы приложений Azure см. в статье [Проверка подлинности в приложении Azure с помощью локального каталога Active Directory](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="c42b1-107">For an overview of the different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="c42b1-108">Что будет строиться</span><span class="sxs-lookup"><span data-stu-id="c42b1-108">What you will build</span></span>
<span data-ttu-id="c42b1-109">Вы создадите простое приложение ASP.NET в веб-приложениях службы приложений Azure со следующими возможностями:</span><span class="sxs-lookup"><span data-stu-id="c42b1-109">You will build a basic ASP.NET application in Azure App Service Web Apps with the following features:</span></span>

* <span data-ttu-id="c42b1-110">проверка подлинности пользователей в AD FS</span><span class="sxs-lookup"><span data-stu-id="c42b1-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="c42b1-111">использование команды `[Authorize]` для авторизации различных действий пользователей;</span><span class="sxs-lookup"><span data-stu-id="c42b1-111">Uses `[Authorize]` to authorize users for different actions</span></span>
* <span data-ttu-id="c42b1-112">статическая настройка для отладки в Visual Studio и публикации в веб-приложениях службы приложений (после настройки отладка и публикация в любое время).</span><span class="sxs-lookup"><span data-stu-id="c42b1-112">Static configuration for both debugging in Visual Studio and publishing to App Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="c42b1-113">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="c42b1-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="c42b1-114">Чтобы выполнить инструкции этого учебника, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="c42b1-114">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="c42b1-115">локальное развертывание AD FS; полное пошаговое руководство по лаборатории тестирования, которая используется здесь, см. в записи блога [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/) (Лаборатория тестирования: автономная служба маркеров безопасности c AD FS на виртуальной машине Azure (только для тестирования));</span><span class="sxs-lookup"><span data-stu-id="c42b1-115">An on-premises AD FS deployment (for an end-to-end walkthrough of the test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="c42b1-116">разрешения для создания отношений доверия с проверяющей стороной в оснастке управления AD FS</span><span class="sxs-lookup"><span data-stu-id="c42b1-116">Permissions to create relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="c42b1-117">Visual Studio 2013 с обновлением 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c42b1-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="c42b1-118">[Пакет SDK Azure, начиная с версии 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) .</span><span class="sxs-lookup"><span data-stu-id="c42b1-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="c42b1-119">Использование примера приложения в качестве шаблона бизнес-приложения</span><span class="sxs-lookup"><span data-stu-id="c42b1-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="c42b1-120">Пример приложения в этом учебнике, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), создала рабочая группа Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c42b1-120">The sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by the Azure Active Directory team.</span></span> <span data-ttu-id="c42b1-121">Так как службы AD FS поддерживают WS-Federation, их можно использовать как шаблон для быстрого создания бизнес-приложений.</span><span class="sxs-lookup"><span data-stu-id="c42b1-121">Since AD FS supports WS-Federation, you can use it as a template to create line-of-business applications with ease.</span></span> <span data-ttu-id="c42b1-122">Они имеют следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="c42b1-122">It has the following features:</span></span>

* <span data-ttu-id="c42b1-123">использование [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) для аутентификации с помощью локального развертывания служб федерации Active Directory;</span><span class="sxs-lookup"><span data-stu-id="c42b1-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) to authenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="c42b1-124">функции входа и выхода</span><span class="sxs-lookup"><span data-stu-id="c42b1-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="c42b1-125">Использование [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (вместо Windows Identity Foundation, то есть WIF). Этот интерфейс определяет будущее ASP.NET. Настроить его для аутентификации и авторизации гораздо проще, чем WIF.</span><span class="sxs-lookup"><span data-stu-id="c42b1-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is the future of ASP.NET and much simpler to set up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a><span data-ttu-id="c42b1-126">настройка простого приложения</span><span class="sxs-lookup"><span data-stu-id="c42b1-126">Set up the sample application</span></span>
1. <span data-ttu-id="c42b1-127">Создайте клон или скачайте пример решения [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="c42b1-127">Clone or download the sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) to your local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c42b1-128">Следуйте указаниям в файле [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) , чтобы настроить приложение с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c42b1-128">The instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how to set up the application with Azure Active Directory.</span></span> <span data-ttu-id="c42b1-129">Но так как в этом руководстве показано, как настраивать приложение при помощи AD FS, вам нужно выполнить действия, которые описаны здесь.</span><span class="sxs-lookup"><span data-stu-id="c42b1-129">But in this tutorial, you set it up with AD FS, so follow the steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="c42b1-130">Откройте решение, а затем откройте файл Controllers\AccountController.cs в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-130">Open the solution, and then open Controllers\AccountController.cs in the **Solution Explorer**.</span></span>
   
   <span data-ttu-id="c42b1-131">Вы увидите, что код просто выдает запрос проверки подлинности для проверки подлинности пользователя с помощью WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c42b1-131">You will see that the code simply issues an authentication challenge to authenticate the user using WS-Federation.</span></span> <span data-ttu-id="c42b1-132">Вся проверка подлинности настраивается в App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="c42b1-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="c42b1-133">Откройте App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="c42b1-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="c42b1-134">В методе `ConfigureAuth` найдите строку:</span><span class="sxs-lookup"><span data-stu-id="c42b1-134">In the `ConfigureAuth` method, note the line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="c42b1-135">В среде OWIN этот фрагмент действительно является абсолютным минимумом, который необходим для настройки проверки подлинности с помощью WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c42b1-135">In the OWIN world, this snippet is really the bare minimum you need to configure WS-Federation authentication.</span></span> <span data-ttu-id="c42b1-136">Это гораздо более простой и элегантный способ, чем WIF, когда Web.config вставляется с помощью XML по всей программе.</span><span class="sxs-lookup"><span data-stu-id="c42b1-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over the place.</span></span> <span data-ttu-id="c42b1-137">Единственное, что нам потребуется, это идентификатор проверяющей стороны(RP) и URL-адрес файла метаданных службы AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-137">The only information you need is the relying party's (RP) identifier and the URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="c42b1-138">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="c42b1-138">Here's an example:</span></span>
   
   * <span data-ttu-id="c42b1-139">Идентификатор RP: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="c42b1-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="c42b1-140">Адрес метаданных: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="c42b1-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="c42b1-141">В App_Start\Startup.Auth.cs замените такие статические определения строк:</span><span class="sxs-lookup"><span data-stu-id="c42b1-141">In App_Start\Startup.Auth.cs, change the following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="c42b1-142">Теперь сделайте соответствующие изменения в файле Web.config.</span><span class="sxs-lookup"><span data-stu-id="c42b1-142">Now, make the corresponding changes in Web.config.</span></span> <span data-ttu-id="c42b1-143">Откройте файл Web.config и измените такие параметры приложения:</span><span class="sxs-lookup"><span data-stu-id="c42b1-143">Open the Web.config and modify the following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="c42b1-144">Заполните значения ключа на базе данных вашей среды.</span><span class="sxs-lookup"><span data-stu-id="c42b1-144">Fill in the key values based on your respective environment.</span></span>
6. <span data-ttu-id="c42b1-145">Постройте приложение, чтобы убедиться в отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="c42b1-145">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="c42b1-146">Вот и все.</span><span class="sxs-lookup"><span data-stu-id="c42b1-146">That's it.</span></span> <span data-ttu-id="c42b1-147">Теперь учебное приложение готово к работе с AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-147">Now the sample application is ready to work with AD FS.</span></span> <span data-ttu-id="c42b1-148">Позднее вам все-таки потребуется настроить отношения доверия проверяющей стороны с этим приложением в AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-148">You still need to configure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a><span data-ttu-id="c42b1-149">Развертывание примера приложения в веб-приложениях службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c42b1-149">Deploy the sample application to Azure App Service Web Apps</span></span>
<span data-ttu-id="c42b1-150">Здесь вы научитесь публиковать приложение в веб-приложениях службы приложений, сохраняя при этом среду отладки.</span><span class="sxs-lookup"><span data-stu-id="c42b1-150">Here, you publish the application to a web app in App Service Web Apps while preserving the debug environment.</span></span> <span data-ttu-id="c42b1-151">Обратите внимание, что публикация приложения будет выполняться до установления отношений доверия проверяющей стороны с AD FS, поэтому проверка подлинности еще не работает.</span><span class="sxs-lookup"><span data-stu-id="c42b1-151">Note that you're going to publish the application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="c42b1-152">Однако если вы опубликуете приложение сейчас, вы получите URL-адрес веб-приложения, который позднее также будет использоваться для настройки отношения доверия с проверяющей стороной.</span><span class="sxs-lookup"><span data-stu-id="c42b1-152">However, if you do it now you can have the web app URL that you can use to configure the RP trust later.</span></span>

1. <span data-ttu-id="c42b1-153">Щелкните правой кнопкой мыши свой проект и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-153">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="c42b1-154">Щелкните **Служба приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-154">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="c42b1-155">Если вы еще не вошли в Azure, нажмите кнопку **Вход** и укажите данные учетной записи Майкрософт для своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c42b1-155">If you haven't signed in to Azure, click **Sign In** and use the Microsoft account for your Azure subscription to sign in.</span></span>
4. <span data-ttu-id="c42b1-156">После входа щелкните **Создать** , чтобы создать веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="c42b1-156">Once signed in, click **New** to create a web app.</span></span>
5. <span data-ttu-id="c42b1-157">Заполните все обязательные поля.</span><span class="sxs-lookup"><span data-stu-id="c42b1-157">Fill in all required fields.</span></span> <span data-ttu-id="c42b1-158">Подключение к локальным данным выполняется позднее, поэтому вам не нужно создавать базу данных для этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c42b1-158">You are going to connect to on-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="c42b1-159">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-159">Click **Create**.</span></span> <span data-ttu-id="c42b1-160">После создания веб-приложения открывается диалоговое окно публикации в Интернете.</span><span class="sxs-lookup"><span data-stu-id="c42b1-160">Once the web app is created, the Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="c42b1-161">В поле **Конечный URL-адрес** замените **http** на **https**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-161">In **Destination URL**, change **http** to **https**.</span></span> <span data-ttu-id="c42b1-162">Скопируйте весь URL-адрес в текстовый редактор для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="c42b1-162">Copy the entire URL to a text editor for later use.</span></span> <span data-ttu-id="c42b1-163">Затем щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-163">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="c42b1-164">В Visual Studio откройте в своем проекте файл **Web.Release.config** .</span><span class="sxs-lookup"><span data-stu-id="c42b1-164">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="c42b1-165">Вставьте следующий XML-код в тег `<configuration>` и замените значение ключа URL-адресом публикуемого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c42b1-165">Insert the following XML into the `<configuration>` tag, and replace the key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="c42b1-166">После завершения операции вы получите два идентификатора RP, настроенных в проекте: один для среды отладки в Visual Studio, а второй для опубликованного веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="c42b1-166">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for the published web app in Azure.</span></span> <span data-ttu-id="c42b1-167">Доверие с проверяющей стороной (RP) будет необходимо настроить для каждой из двух сред в AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-167">You will set up an RP trust for each of the two environments in AD FS.</span></span> <span data-ttu-id="c42b1-168">Во время отладки параметры приложения в файле Web.config используются, чтобы ваша конфигурация **отладки** работала с AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-168">During debugging, the app settings in Web.config are used to make your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="c42b1-169">При его публикации (по умолчанию публикуется конфигурация **Выпуск** ) отправляется измененный файл Web.config, в котором содержатся изменения параметров приложения в файле Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="c42b1-169">When it's published (by default, the **Release** configuration is published), a transformed Web.config is uploaded that incorporates the app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="c42b1-170">Если требуется подключить опубликованное веб-приложение в Azure к отладчику (т.е. когда нужно отправить символы отладки кода в опубликованное веб-приложение), можно создать клон конфигурации отладки для отладки в Azure. Этот клон должен иметь собственный настраиваемый файл преобразования Web.config (например, Web.AzureDebug.config), в котором используются параметры приложения из файла Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="c42b1-170">If you want to attach the published web app in Azure to the debugger (i.e. you must upload debug symbols of your code in the published web app), you can create a clone of the Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses the app settings from Web.Release.config.</span></span> <span data-ttu-id="c42b1-171">Это дает возможность поддерживать статическую конфигурацию в различных средах.</span><span class="sxs-lookup"><span data-stu-id="c42b1-171">This allows you to maintain a static configuration across the different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="c42b1-172">Настройка доверия с проверяющей стороной в оснастке управления AD FS</span><span class="sxs-lookup"><span data-stu-id="c42b1-172">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="c42b1-173">Теперь необходимо настроить отношение доверия с проверяющей стороной в оснастке управления AD FS, чтобы в вашем примере приложения действительно выполнялась проверка подлинности с помощью AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-173">Now you need to configure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="c42b1-174">Для этого необходимо настроить два различных отношения доверия с проверяющей стороной: одно для среды отладки и одно для опубликованного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c42b1-174">You will need to set up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="c42b1-175">Не забудьте выполнить указанные ниже действия для обеих сред.</span><span class="sxs-lookup"><span data-stu-id="c42b1-175">Make sure that you repeat the following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="c42b1-176">На сервере AD FS выполните вход с использование учетных данных, имеющих права управления для AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-176">On your AD FS server, log in with credentials that have management rights to AD FS.</span></span>
2. <span data-ttu-id="c42b1-177">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-177">Open AD FS Management.</span></span> <span data-ttu-id="c42b1-178">Щелкните правой кнопкой мыши **AD FS\Trusted Relationships\Relying Party Trusts** и выберите **Добавить отношение доверия проверяющей стороны**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-178">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="c42b1-179">На странице **Выбрать источник данных** выберите **Ввод данных о проверяющей стороне вручную**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-179">In the **Select Data Source** page, select **Enter data about the relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="c42b1-180">На странице **Указание отображаемого имени** введите отображаемое имя для приложения и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-180">In the **Specify Display Name** page, type a display name for the application and click **Next**.</span></span>
5. <span data-ttu-id="c42b1-181">На странице **Выбор протокола** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-181">In the **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="c42b1-182">На странице **Настройка сертификата** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-182">In the **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c42b1-183">Так как уже должен использоваться протокол HTTPS, зашифрованные токены необязательны.</span><span class="sxs-lookup"><span data-stu-id="c42b1-183">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="c42b1-184">Если действительно необходимо шифровать токены из AD FS на этой странице, нужно добавить логику расшифровки токенов в код.</span><span class="sxs-lookup"><span data-stu-id="c42b1-184">If you really want to encrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="c42b1-185">Дополнительную информацию см. в статье [Ручная настройка промежуточного слоя OWIN WS-Federation и прием зашифрованных маркеров](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="c42b1-185">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="c42b1-186">Прежде чем переходить к следующему шагу, потребуется часть информации и проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c42b1-186">Before you move onto the next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="c42b1-187">В свойствах проекта обратите внимание на **URL-адрес SSL** приложения.</span><span class="sxs-lookup"><span data-stu-id="c42b1-187">In the project properties, note the **SSL URL** of the application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="c42b1-188">Перейдите снова в оснастку управления AD FS. На странице **Настройка URL-адреса** в **мастера добавления отношения доверия с проверяющей стороной** выберите **Включить поддержку пассивного протокола WS-Federation** и введите URL-адрес SSL проекта Visual Studio, который вы записали на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="c42b1-188">Back in AD FS Management, in the **Configure URL** page of the **Add Relying Party Trust Wizard**, select **Enable support for the WS-Federation Passive protocol** and type in the SSL URL of your Visual Studio project that you noted in the previous step.</span></span> <span data-ttu-id="c42b1-189">Затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-189">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="c42b1-190">URL-адрес указывает, куда отправлять клиента после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c42b1-190">URL specifies where to send the client after authentication succeeds.</span></span> <span data-ttu-id="c42b1-191">Для среды отладки это должен быть <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="c42b1-191">For the debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="c42b1-192">Для опубликованного веб-приложения это должен быть URL-адрес веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c42b1-192">For the published web app, it should be the web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="c42b1-193">На странице **Настройка идентификаторов** убедитесь, что URL-адрес SSL проекта уже есть в списке, и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-193">In the **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="c42b1-194">Щелкайте **Далее** на всех страницах мастера до конца, выбирая значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c42b1-194">Click **Next** all the way to the end of the wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c42b1-195">В App_Start\Startup.Auth.cs проекта Visual Studio этот идентификатор сопоставляется со значением <code>WsFederationAuthenticationOptions.Wtrealm</code> во время федеративной аутентификации.</span><span class="sxs-lookup"><span data-stu-id="c42b1-195">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against the value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="c42b1-196">По умолчанию URL-адрес приложения из предыдущего шага добавляется как идентификатор RP.</span><span class="sxs-lookup"><span data-stu-id="c42b1-196">By default, the application's URL from the previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="c42b1-197">Настройка приложения RP для проекта в AD FS завершена.</span><span class="sxs-lookup"><span data-stu-id="c42b1-197">You have now finished configuring the RP application for your project in AD FS.</span></span> <span data-ttu-id="c42b1-198">Далее необходимо настроить это приложение, чтобы оно отправляло утверждения, необходимые вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="c42b1-198">Next, you configure this application to send the claims needed by your application.</span></span> <span data-ttu-id="c42b1-199">При окончании работы мастера по умолчанию открывается диалоговое окно **Изменение правил для утверждений** и можно сразу приступить к настройке.</span><span class="sxs-lookup"><span data-stu-id="c42b1-199">The **Edit Claim Rules** dialog is opened by default for you at the end of the wizard so you can start immediately.</span></span> <span data-ttu-id="c42b1-200">Как минимум, настроим следующие утверждения (со схемами в круглых скобках):</span><span class="sxs-lookup"><span data-stu-id="c42b1-200">Let's configure at least the following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="c42b1-201">Имя (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) — используется ASP.NET для расконсервации `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="c42b1-201">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET to hydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="c42b1-202">Имя участника-пользователя (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) — используется для уникальной идентификации пользователей в организации.</span><span class="sxs-lookup"><span data-stu-id="c42b1-202">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used to uniquely identify users in the organization.</span></span>
    * <span data-ttu-id="c42b1-203">Членства в группах в качестве ролей (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) — могут использоваться с декорированием `[Authorize(Roles="role1, role2,...")]` для авторизации контроллеров или действий.</span><span class="sxs-lookup"><span data-stu-id="c42b1-203">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration to authorize controllers/actions.</span></span> <span data-ttu-id="c42b1-204">Фактически этот подход может не обеспечивать максимальную производительность для авторизации роли.</span><span class="sxs-lookup"><span data-stu-id="c42b1-204">In reality, this approach may not be the most performant for role authorization.</span></span> <span data-ttu-id="c42b1-205">Если службой AD пользуются участники сотен групп безопасности, они генерируют сотни утверждений роли в токене SAML.</span><span class="sxs-lookup"><span data-stu-id="c42b1-205">If your AD users belong to hundreds of security groups, they become hundreds of role claims in the SAML token.</span></span> <span data-ttu-id="c42b1-206">В качестве альтернативного подхода можно отправить одной утверждение роли, условно зависящее от членства пользователя в определенной группе.</span><span class="sxs-lookup"><span data-stu-id="c42b1-206">An alternative approach is to send a single role claim conditionally depending on the user's membership in a particular group.</span></span> <span data-ttu-id="c42b1-207">Однако в нашем учебнике мы будем придерживаться простого подхода.</span><span class="sxs-lookup"><span data-stu-id="c42b1-207">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="c42b1-208">ИД имени (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) — используется для проверки защиты от подделки.</span><span class="sxs-lookup"><span data-stu-id="c42b1-208">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="c42b1-209">Дополнительную информацию о настройке проверки защиты от подделки см. в разделе **Добавление функциональности бизнес-приложения к примеру приложения** статьи [Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="c42b1-209">For more information on how to make it work with anti-forgery validation, see the **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c42b1-210">Типы утверждений, которые необходимо настроить для приложения определяются его потребностями.</span><span class="sxs-lookup"><span data-stu-id="c42b1-210">The claim types you need to configure for your application is determined by your application's needs.</span></span> <span data-ttu-id="c42b1-211">Список утверждений, поддерживаемых приложениями Azure Active Directory (т. е. отношениями доверия RP), см. в разделе [Справочник по токенам в Azure AD](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="c42b1-211">For the list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="c42b1-212">В диалоговом окне «Изменение правил для утверждений» щелкните **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-212">In the Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="c42b1-213">Задайте имя, имя участника-пользователя и утверждения роли, ориентируясь на этот снимок экрана, и щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-213">Configure the name, UPN, and role claims as shown in the screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="c42b1-214">Теперь необходимо создать временное утверждение идентификатора имени, используя шаги, описанные в записи блога [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)(Идентификаторы имен в утверждениях SAML).</span><span class="sxs-lookup"><span data-stu-id="c42b1-214">Next, you create a transient name ID claim using the steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="c42b1-215">Щелкните **Добавить правило** еще раз.</span><span class="sxs-lookup"><span data-stu-id="c42b1-215">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="c42b1-216">Выберите **Отправка утверждений с помощью настраиваемого правила** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-216">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="c42b1-217">Вставьте следующий код правила в поле **Настраиваемое правило**, присвойте правилу имя **Per Session Identifier** (В соответствии с идентификатором сеанса) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-217">Paste the following rule language into the **Custom rule** box, name the rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="c42b1-218">Настраиваемое правило должно выглядеть, как на этом снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="c42b1-218">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="c42b1-219">Щелкните **Добавить правило** еще раз.</span><span class="sxs-lookup"><span data-stu-id="c42b1-219">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="c42b1-220">Выберите **Преобразование входящего утверждения** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-220">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="c42b1-221">Настройте правило, как показано на этом снимке экрана (используя тип утверждения, созданный в настраиваемом правиле), и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-221">Configure the rule as shown in the screenshot (using the claim type you created in the custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="c42b1-222">Подробную информацию о поэтапном создании временного утверждения идентификатора имени см. в записи блога [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx) (Идентификаторы имен в утверждениях SAML).</span><span class="sxs-lookup"><span data-stu-id="c42b1-222">For detailed information on the steps for the transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="c42b1-223">Щелкните **Применить** в диалоговом окне **Изменить правила утверждений**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-223">Click **Apply** in the **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="c42b1-224">Все должно выглядеть, как на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="c42b1-224">It should now look like the following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="c42b1-225">Не забудьте, что эти шаги необходимо повторить для среды отладки и опубликованного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c42b1-225">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="c42b1-226">Тестирование федеративной проверки подлинности для приложения</span><span class="sxs-lookup"><span data-stu-id="c42b1-226">Test federated authentication for your application</span></span>
<span data-ttu-id="c42b1-227">Все готово для тестирования логики проверки подлинности приложения в AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-227">You are ready to test your application's authentication logic against AD FS.</span></span> <span data-ttu-id="c42b1-228">В моей лабораторной среде AD FS я использую тестового пользователя, который входит в состав тестовой группы в Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="c42b1-228">In my AD FS lab environment, I have a test user that belongs to a test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="c42b1-229">Для аутентификации в отладчике достаточно просто ввести `F5`.</span><span class="sxs-lookup"><span data-stu-id="c42b1-229">To test authentication in the debugger, all you need to do now is type `F5`.</span></span> <span data-ttu-id="c42b1-230">Чтобы протестировать аутентификацию в опубликованном веб-приложении, перейдите по URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="c42b1-230">If you want to test authentication in the published web app, navigate to the URL.</span></span>

<span data-ttu-id="c42b1-231">После загрузки веб-приложения щелкните **Вход**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-231">After the web application loads, click **Sign In**.</span></span> <span data-ttu-id="c42b1-232">Теперь должно появиться диалоговое окно входа или страница входа, обслуживаемые AD FS в зависимости от метода проверки подлинности который выбирается AD FS.</span><span class="sxs-lookup"><span data-stu-id="c42b1-232">You should now get either a login dialog or the login page served by AD FS, depending on the authentication method chosen by AD FS.</span></span> <span data-ttu-id="c42b1-233">Вот что получается в Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="c42b1-233">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="c42b1-234">После входа с правами пользователя в домен AD развертывания AD FS должна опять отобразиться домашняя страница с сообщением **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="c42b1-234">Once you log in with a user in the AD domain of the AD FS deployment, you should now see the homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="c42b1-235">("Добро пожаловать, &lt;имя_пользователя&gt;!") в углу.</span><span class="sxs-lookup"><span data-stu-id="c42b1-235">in the corner.</span></span> <span data-ttu-id="c42b1-236">Вот что у меня получается.</span><span class="sxs-lookup"><span data-stu-id="c42b1-236">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="c42b1-237">Итак, что нам удалось успешно сделать:</span><span class="sxs-lookup"><span data-stu-id="c42b1-237">So far, you've succeeded in the following ways:</span></span>

* <span data-ttu-id="c42b1-238">приложение успешно получило доступ к AD FS, и в базе данных AD FS был найден совпадающий идентификатор RP</span><span class="sxs-lookup"><span data-stu-id="c42b1-238">Your application has successfully reached AD FS and a matching RP identifier is found in the AD FS database</span></span>
* <span data-ttu-id="c42b1-239">AD FS успешно выполняют проверку подлинности пользователя AD и перенаправляют вас обратно на домашнюю страницу приложения</span><span class="sxs-lookup"><span data-stu-id="c42b1-239">AD FS has successfully authenticated an AD user and redirect you back to the application's homepage</span></span>
* <span data-ttu-id="c42b1-240">Если AD FS успешно отправляет утверждение имени (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) приложению, это подтверждается тем, что имя пользователя отображается в углу.</span><span class="sxs-lookup"><span data-stu-id="c42b1-240">AD FS as successfully sent the name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) to your application, as indicated by the fact that the user name is displayed in the corner.</span></span> 

<span data-ttu-id="c42b1-241">Если утверждение имени отсутствует, вы увидите **Здравствуйте, !**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-241">If the name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="c42b1-242">В файле Views\Shared\_LoginPartial.cshtml можно увидеть, что для отображения имени пользователя здесь используется свойство `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="c42b1-242">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` to display the user name.</span></span> <span data-ttu-id="c42b1-243">Как уже отмечалось ранее, ASP.NET заполняет это свойство утверждением имени пользователя, прошедшего проверку подлинности, если оно доступно в токене SAML.</span><span class="sxs-lookup"><span data-stu-id="c42b1-243">As mentioned previously, if the name claim of the authenticated user is available in the SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="c42b1-244">Чтобы просмотреть все утверждения, отправленные AD FS, вставьте точку останова в Controllers\HomeController.cs в методе действия индекса.</span><span class="sxs-lookup"><span data-stu-id="c42b1-244">To see all the claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in the Index action method.</span></span> <span data-ttu-id="c42b1-245">После аутентификации пользователя проверьте коллекцию `System.Security.Claims.Current.Claims` .</span><span class="sxs-lookup"><span data-stu-id="c42b1-245">After the user is authenticated, inspect the `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="c42b1-246">Авторизация пользователей для определенных контроллеров и действий</span><span class="sxs-lookup"><span data-stu-id="c42b1-246">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="c42b1-247">Вы включили членство в группах в качестве утверждений ролей в вашей конфигурации отношения доверия с проверяющей стороной. Теперь вы можете использовать его непосредственно в оформлении `[Authorize(Roles="...")]` для контроллеров и действий.</span><span class="sxs-lookup"><span data-stu-id="c42b1-247">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in the `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="c42b1-248">В бизнес-приложении с шаблоном создать- прочитать-обновить-удалить (CRUD) можно выполнять авторизацию определенных ролей для доступа к каждому действию.</span><span class="sxs-lookup"><span data-stu-id="c42b1-248">In a line-of-business application with the Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles to access each action.</span></span> <span data-ttu-id="c42b1-249">На сегодня просто попробуем, как работает эта функция на примере существующего контроллера Home.</span><span class="sxs-lookup"><span data-stu-id="c42b1-249">For now, you will just try out this feature on the existing Home controller.</span></span>

1. <span data-ttu-id="c42b1-250">Откройте Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="c42b1-250">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="c42b1-251">Оформите методы действия `About` и `Contact` при помощи кода наподобие того, который показан ниже. При этом используйте членство в группе безопасности пользователя, прошедшего проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="c42b1-251">Decorate the `About` and `Contact` action methods similar to the following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="c42b1-252">Так как я добавил **тестового пользователя** в группу **Test Group** в своей лабораторной среде AD FS, я буду использовать эту тестовую группу для проверки авторизации на `About`.</span><span class="sxs-lookup"><span data-stu-id="c42b1-252">Since I added **Test User** to **Test Group** in my AD FS lab environment, I'll use Test Group to test authorization on `About`.</span></span> <span data-ttu-id="c42b1-253">Для `Contact` я проведу тестирование отрицательного случая группы **Domain Admins**, к которой не принадлежит **тестовый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-253">For `Contact`, I'll test the negative case of **Domain Admins**, to which **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="c42b1-254">Запустите отладчик, нажав клавишу `F5` , и войдите в систему, а затем нажмите кнопку **О программе**.</span><span class="sxs-lookup"><span data-stu-id="c42b1-254">Start the debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="c42b1-255">Должна отобразиться страница `~/About/Index` , если прошедший аутентификацию пользователь авторизован для этого действия.</span><span class="sxs-lookup"><span data-stu-id="c42b1-255">You should now be viewing the `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="c42b1-256">Далее щелкните **Контакт**, что в моем случае не должно авторизовать **тестового пользователя** для этого действия.</span><span class="sxs-lookup"><span data-stu-id="c42b1-256">Now click **Contact**, which in my case should not authorize **Test User** for the action.</span></span> <span data-ttu-id="c42b1-257">Тем не менее, браузер перенаправляется к AD FS, в результате чего, в конечном счете, показывается это сообщение:</span><span class="sxs-lookup"><span data-stu-id="c42b1-257">However, the browser is redirected to AD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="c42b1-258">При анализе этой ошибки в средстве просмотра событий на сервере AD FS можно увидеть такое сообщение об исключении:</span><span class="sxs-lookup"><span data-stu-id="c42b1-258">If you investigate this error in Event Viewer on the AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="c42b1-259">Это происходит потому, что по умолчанию MVC возвращает сообщение об ошибке "401 — Не авторизовано", когда роли пользователя не авторизованы.</span><span class="sxs-lookup"><span data-stu-id="c42b1-259">The reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="c42b1-260">В результате активируется запрос на повторную проверку подлинности к поставщику удостоверений(AD FS).</span><span class="sxs-lookup"><span data-stu-id="c42b1-260">This triggers a reauthentication request to your identity provider (AD FS).</span></span> <span data-ttu-id="c42b1-261">Так как пользователь уж прошел проверку подлинности, AD FS возвращается на ту же страницу, которая издает другую ошибку 401, создавая цикл перенаправления.</span><span class="sxs-lookup"><span data-stu-id="c42b1-261">Since the user is already authenticated, AD FS returns to the same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="c42b1-262">Можно переопределить метод `HandleUnauthorizedRequest` в AuthorizeAttribute с помощью простой логики, чтобы отображать более содержательную информацию вместо продолжения цикла перенаправления.</span><span class="sxs-lookup"><span data-stu-id="c42b1-262">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic to show something that makes sense instead of continuing the redirect loop.</span></span>
5. <span data-ttu-id="c42b1-263">Создайте файл в проекте AuthorizeAttribute.cs и вставьте в него приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="c42b1-263">Create a file in the project called AuthorizeAttribute.cs, and paste the following code into it.</span></span>
   
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
   
    <span data-ttu-id="c42b1-264">Код переопределения отправляет сообщение об ошибке "HTTP 403 — запрещено" вместо "401 — не авторизовано", когда аутентификация выполнена, а авторизация не выполнена.</span><span class="sxs-lookup"><span data-stu-id="c42b1-264">The override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="c42b1-265">Запустите отладчик снова, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="c42b1-265">Run the debugger again with `F5`.</span></span> <span data-ttu-id="c42b1-266">Щелкнув **Контакт** , теперь можно увидеть более информативное (хотя и непривлекательное) сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="c42b1-266">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="c42b1-267">Опубликуйте приложение в веб-приложениях службы приложений еще раз и протестируйте поведение развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="c42b1-267">Publish the application to Azure App Service Web Apps again, and test the behavior of the live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a><span data-ttu-id="c42b1-268">Подключение к локальным данным</span><span class="sxs-lookup"><span data-stu-id="c42b1-268">Connect to on-premises data</span></span>
<span data-ttu-id="c42b1-269">Одна из причин реализации бизнес-приложения с AD FS вместо Azure Active Directory заключается в проблемах обеспечения соответствия, когда организации требуется сохранять данные локально.</span><span class="sxs-lookup"><span data-stu-id="c42b1-269">A reason that you would want to implement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="c42b1-270">Это может также означать, что у веб-приложения в Azure должен быть доступ к локальной базе данных, так как вам запрещено использовать [Базу данных SQL](/services/sql-database/) в качестве уровня данных для своих веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c42b1-270">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed to use [SQL Database](/services/sql-database/) as the data tier for your web apps.</span></span>

<span data-ttu-id="c42b1-271">Веб-приложения службы приложений Azure поддерживают доступ к локальным базам данных двумя способами: с помощью [гибридных подключений](../biztalk-services/integration-hybrid-connection-overview.md) и [виртуальных сетей](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="c42b1-271">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="c42b1-272">Дополнительную информацию см. в статье [Использование интеграции VNET и гибридных подключений с веб-приложениями службы приложений Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="c42b1-272">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="c42b1-273">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c42b1-273">Further resources</span></span>
* [<span data-ttu-id="c42b1-274">Проверка подлинности в приложении Azure с помощью локального каталога Active Directory</span><span class="sxs-lookup"><span data-stu-id="c42b1-274">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="c42b1-275">Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c42b1-275">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="c42b1-276">Использование локальной аутентификации в организации (AD FS) с использованием ASP.NET в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c42b1-276">Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="c42b1-277">Миграция веб-проекта VS2013 из WIF в Katana</span><span class="sxs-lookup"><span data-stu-id="c42b1-277">Migrate a VS2013 Web Project From WIF to Katana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="c42b1-278">Обзор служб федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="c42b1-278">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="c42b1-279">Спецификация WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="c42b1-279">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

