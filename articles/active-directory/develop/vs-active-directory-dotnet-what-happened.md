---
title: "внесенные aaaChanges tooa MVC проекта при подключении tooAzure AD | Документы Microsoft"
description: "Описывает, что происходит проекта MVC tooyour при подключении tooAzure AD с помощью Visual Studio подключенных служб"
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="6437f-103">Какая ошибка toomy проекта MVC (Visual Studio Azure Active Directory подключенных служб)?</span><span class="sxs-lookup"><span data-stu-id="6437f-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6437f-104">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="6437f-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="6437f-105">Что произошло?</span><span class="sxs-lookup"><span data-stu-id="6437f-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="6437f-106">Добавлены ссылки</span><span class="sxs-lookup"><span data-stu-id="6437f-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="6437f-107">Ссылки на пакет NuGet</span><span class="sxs-lookup"><span data-stu-id="6437f-107">NuGet package references</span></span>
* <span data-ttu-id="6437f-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="6437f-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="6437f-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="6437f-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="6437f-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="6437f-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="6437f-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="6437f-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="6437f-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="6437f-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="6437f-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="6437f-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="6437f-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="6437f-114">**Owin**</span></span>
* <span data-ttu-id="6437f-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="6437f-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="6437f-116">Ссылки на .NET</span><span class="sxs-lookup"><span data-stu-id="6437f-116">.NET references</span></span>
* <span data-ttu-id="6437f-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="6437f-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="6437f-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="6437f-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="6437f-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="6437f-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="6437f-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="6437f-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="6437f-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="6437f-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="6437f-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="6437f-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="6437f-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="6437f-123">**Owin**</span></span>
* <span data-ttu-id="6437f-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="6437f-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="6437f-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="6437f-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="6437f-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="6437f-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="6437f-127">Добавлен код</span><span class="sxs-lookup"><span data-stu-id="6437f-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="6437f-128">Файлы кода были добавлены tooyour проекта</span><span class="sxs-lookup"><span data-stu-id="6437f-128">Code files were added tooyour project</span></span>
<span data-ttu-id="6437f-129">Класс запуска проверки подлинности, **App_Start/Startup.Auth.cs** был добавлен tooyour проект, содержащий логику запуска для проверки подлинности Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6437f-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="6437f-130">Кроме того, добавлен класс контролера Controllers/AccountController.cs, который содержит методы **SignIn()** и **SignOut()**.</span><span class="sxs-lookup"><span data-stu-id="6437f-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="6437f-131">Наконец, добавлено частичное представление **Views/Shared/_LoginPartial.cshtml**, содержащее ссылку действия для SignIn и SignOut.</span><span class="sxs-lookup"><span data-stu-id="6437f-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="6437f-132">Код запуска был добавлен tooyour проекта</span><span class="sxs-lookup"><span data-stu-id="6437f-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="6437f-133">Если класс запуска уже есть в вашем проекте, hello **конфигурации** метод было обновленные tooinclude вызов слишком**ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="6437f-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="6437f-134">В противном случае класс запуска была добавлена tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="6437f-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="6437f-135">В файл app.config или web.config добавлены значения конфигурации</span><span class="sxs-lookup"><span data-stu-id="6437f-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="6437f-136">были добавлены следующие записи конфигурации Hello.</span><span class="sxs-lookup"><span data-stu-id="6437f-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="6437f-137">Было создано приложение Azure Active Directory (AD)</span><span class="sxs-lookup"><span data-stu-id="6437f-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="6437f-138">Приложения Azure AD был создан в каталоге hello, выбранная в мастере hello.</span><span class="sxs-lookup"><span data-stu-id="6437f-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="6437f-139">Если после проверки *отключить проверку подлинности учетных записей отдельных пользователей*, какие дополнительные изменения были сделаны toomy проекта?</span><span class="sxs-lookup"><span data-stu-id="6437f-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="6437f-140">Удалены ссылки на пакет NuGet. Для файлов созданы резервные копии, а сами файлы удалены.</span><span class="sxs-lookup"><span data-stu-id="6437f-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="6437f-141">В зависимости от состояния hello проекта вы можете иметь toomanually удалите дополнительные материалы или файлы или измените код соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="6437f-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="6437f-142">Ссылки на существующие пакеты NuGet удалены</span><span class="sxs-lookup"><span data-stu-id="6437f-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="6437f-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="6437f-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="6437f-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="6437f-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="6437f-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="6437f-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="6437f-146">Для существующих файлов кода созданы резервные копии, а сами файлы удалены.</span><span class="sxs-lookup"><span data-stu-id="6437f-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="6437f-147">Каждый из следующих файлов был заархивирован и удален из проекта hello.</span><span class="sxs-lookup"><span data-stu-id="6437f-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="6437f-148">Файлы резервных копий расположены в папке «Backup» в корневой каталог проекта hello hello.</span><span class="sxs-lookup"><span data-stu-id="6437f-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="6437f-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="6437f-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="6437f-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="6437f-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="6437f-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="6437f-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="6437f-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="6437f-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="6437f-153">Для существующих файлов кода созданы резервные копии</span><span class="sxs-lookup"><span data-stu-id="6437f-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="6437f-154">Для каждого из следующих файлов создана резервная копия, после чего файлы были заменены.</span><span class="sxs-lookup"><span data-stu-id="6437f-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="6437f-155">Файлы резервных копий расположены в папке «Backup» в корневой каталог проекта hello hello.</span><span class="sxs-lookup"><span data-stu-id="6437f-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="6437f-156">**Startup.cs.**</span><span class="sxs-lookup"><span data-stu-id="6437f-156">**Startup.cs**</span></span>
* <span data-ttu-id="6437f-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="6437f-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="6437f-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="6437f-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="6437f-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="6437f-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="6437f-160">Если после проверки *читать данные каталога*, какие дополнительные изменения были сделаны toomy проекта?</span><span class="sxs-lookup"><span data-stu-id="6437f-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="6437f-161">Добавлены дополнительные ссылки.</span><span class="sxs-lookup"><span data-stu-id="6437f-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="6437f-162">Дополнительные ссылки на пакет NuGet</span><span class="sxs-lookup"><span data-stu-id="6437f-162">Additional NuGet package references</span></span>
* <span data-ttu-id="6437f-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="6437f-163">**EntityFramework**</span></span>
* <span data-ttu-id="6437f-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="6437f-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="6437f-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="6437f-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="6437f-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="6437f-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="6437f-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="6437f-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="6437f-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="6437f-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="6437f-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="6437f-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="6437f-170">Дополнительные ссылки на .NET</span><span class="sxs-lookup"><span data-stu-id="6437f-170">Additional .NET references</span></span>
* <span data-ttu-id="6437f-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="6437f-171">**EntityFramework**</span></span>
* <span data-ttu-id="6437f-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="6437f-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="6437f-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="6437f-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="6437f-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="6437f-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="6437f-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="6437f-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="6437f-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="6437f-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="6437f-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="6437f-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="6437f-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="6437f-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="6437f-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="6437f-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="6437f-180">Дополнительные файлы кода были добавлены tooyour проекта</span><span class="sxs-lookup"><span data-stu-id="6437f-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="6437f-181">Два файла были добавлены toosupport кэширования токенов: **Models\ADALTokenCache.cs** и **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="6437f-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="6437f-182">Доступ к сведениям профиля пользователя с помощью Azure graph API-интерфейсы tooillustrate были добавлены дополнительного контроллера и представления.</span><span class="sxs-lookup"><span data-stu-id="6437f-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="6437f-183">Они содержатся в файлах **Controllers\UserProfileController.cs** и **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="6437f-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="6437f-184">Дополнительный код запуска был добавлен tooyour проекта</span><span class="sxs-lookup"><span data-stu-id="6437f-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="6437f-185">В hello **startup.auth.cs** файл, новый **OpenIdConnectAuthenticationNotifications** объект был добавлен toohello **уведомления** членом hello  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="6437f-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="6437f-186">Это tooenable получение кода OAuth hello и обмен его маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="6437f-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="6437f-187">Были внесены дополнительные изменения tooyour app.config или web.config</span><span class="sxs-lookup"><span data-stu-id="6437f-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="6437f-188">Hello следующие дополнительные настройки записи были добавлены.</span><span class="sxs-lookup"><span data-stu-id="6437f-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="6437f-189">Hello следующих разделов конфигурации и строка подключения были добавлены.</span><span class="sxs-lookup"><span data-stu-id="6437f-189">hello following configuration sections and connection string have been added.</span></span>

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="6437f-190">Обновлено приложение Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6437f-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="6437f-191">Приложение Azure Active Directory была hello обновленные tooinclude *читать данные каталога* разрешений и дополнительный раздел был создан, затем которой использовался как hello *ida: ClientSecret* в hello  **Web.config** файла.</span><span class="sxs-lookup"><span data-stu-id="6437f-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6437f-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6437f-192">Next steps</span></span>
- [<span data-ttu-id="6437f-193">Дополнительная информация о службе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6437f-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

