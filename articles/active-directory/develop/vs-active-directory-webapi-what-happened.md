---
title: "внесенные aaaChanges tooa WebApi проекта при подключении tooAzure AD | Документы Microsoft"
description: "Описывает, что происходит tooyour WebApi проекта при подключении tooAzure AD с помощью Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="40670-103">В каком проекте WebApi ошибка toomy (Visual Studio Azure Active Directory подключенных служб)</span><span class="sxs-lookup"><span data-stu-id="40670-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40670-104">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="40670-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="40670-105">Что произошло?</span><span class="sxs-lookup"><span data-stu-id="40670-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="40670-106">Добавлены ссылки</span><span class="sxs-lookup"><span data-stu-id="40670-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="40670-107">Ссылки на пакет NuGet</span><span class="sxs-lookup"><span data-stu-id="40670-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="40670-108">Ссылки на .NET</span><span class="sxs-lookup"><span data-stu-id="40670-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="40670-109">Изменения в коде</span><span class="sxs-lookup"><span data-stu-id="40670-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="40670-110">Файлы кода были добавлены tooyour проекта</span><span class="sxs-lookup"><span data-stu-id="40670-110">Code files were added tooyour project</span></span>
<span data-ttu-id="40670-111">Класс запуска проверки подлинности, **App_Start/Startup.Auth.cs** был добавлен tooyour проект, содержащий логику запуска для проверки подлинности Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40670-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="40670-112">Код запуска был добавлен tooyour проекта</span><span class="sxs-lookup"><span data-stu-id="40670-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="40670-113">Если класс запуска уже есть в вашем проекте, hello **конфигурации** метод было обновленные tooinclude вызов слишком`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="40670-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="40670-114">В противном случае класс запуска была добавлена tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="40670-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="40670-115">Один из файлов app.config или web.config имеет новое значение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40670-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="40670-116">были добавлены следующие записи конфигурации Hello.</span><span class="sxs-lookup"><span data-stu-id="40670-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="40670-117">Создано приложение Azure AD</span><span class="sxs-lookup"><span data-stu-id="40670-117">An Azure AD App was created</span></span>
<span data-ttu-id="40670-118">Приложения Azure AD был создан в каталоге hello, выбранная в мастере hello.</span><span class="sxs-lookup"><span data-stu-id="40670-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="40670-119">Дополнительная информация о службе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40670-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="40670-120">Если после проверки *отключить проверку подлинности учетных записей отдельных пользователей*, какие дополнительные изменения были сделаны toomy проекта?</span><span class="sxs-lookup"><span data-stu-id="40670-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="40670-121">Удалены ссылки на пакет NuGet. Для файлов созданы резервные копии, а сами файлы удалены.</span><span class="sxs-lookup"><span data-stu-id="40670-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="40670-122">В зависимости от состояния hello проекта вы можете иметь toomanually удалите дополнительные материалы или файлы или измените код соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="40670-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="40670-123">Ссылки на существующие пакеты NuGet удалены</span><span class="sxs-lookup"><span data-stu-id="40670-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="40670-124">Для существующих файлов кода созданы резервные копии, а сами файлы удалены.</span><span class="sxs-lookup"><span data-stu-id="40670-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="40670-125">Каждый из следующих файлов был заархивирован и удален из проекта hello.</span><span class="sxs-lookup"><span data-stu-id="40670-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="40670-126">Файлы резервных копий расположены в папке «Backup» в корневой каталог проекта hello hello.</span><span class="sxs-lookup"><span data-stu-id="40670-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="40670-127">Для существующих файлов кода созданы резервные копии</span><span class="sxs-lookup"><span data-stu-id="40670-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="40670-128">Для каждого из следующих файлов создана резервная копия, после чего файлы были заменены.</span><span class="sxs-lookup"><span data-stu-id="40670-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="40670-129">Файлы резервных копий расположены в папке «Backup» в корневой каталог проекта hello hello.</span><span class="sxs-lookup"><span data-stu-id="40670-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="40670-130">Если после проверки *читать данные каталога*, какие дополнительные изменения были сделаны toomy проекта?</span><span class="sxs-lookup"><span data-stu-id="40670-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="40670-131">Были внесены дополнительные изменения tooyour app.config или web.config</span><span class="sxs-lookup"><span data-stu-id="40670-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="40670-132">Hello следующие дополнительные настройки записи были добавлены.</span><span class="sxs-lookup"><span data-stu-id="40670-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="40670-133">Обновлено приложение Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40670-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="40670-134">Приложение Azure Active Directory была hello обновленные tooinclude *читать данные каталога* разрешение и дополнительный раздел был создан, затем которой использовался как hello *ida: пароль* в hello `web.config` файла.</span><span class="sxs-lookup"><span data-stu-id="40670-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40670-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40670-135">Next steps</span></span>
- [<span data-ttu-id="40670-136">Дополнительная информация о службе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40670-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

