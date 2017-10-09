---
title: "aaaAzure Active Directory B2C | Документы Microsoft"
description: "Как toobuild веб-приложения с регистрации-повышение или входе в систему профиля, изменение и сбросить с помощью Azure Active Directory B2C пароль."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="4da7c-103">Создание веб-приложения ASP.NET с возможностями регистрации, входа, редактирования профиля и сброса пароля Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="4da7c-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="4da7c-104">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="4da7c-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4da7c-105">Добавление Azure AD B2C идентификаторов компонентов tooyour веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4da7c-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="4da7c-106">Регистрация веб-приложения в каталоге Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="4da7c-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="4da7c-107">Создание политики регистрации, входа, изменения профиля и сброса пароля пользователя для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4da7c-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4da7c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4da7c-108">Prerequisites</span></span>

- <span data-ttu-id="4da7c-109">Вашего клиента B2C tooan учетная запись Azure, необходимо подключиться.</span><span class="sxs-lookup"><span data-stu-id="4da7c-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="4da7c-110">Вы можете создать бесплатную учетную запись Azure [здесь](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="4da7c-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="4da7c-111">Требуется [Microsoft Visual Studio](https://www.visualstudio.com/) или аналогичные программы tooview и измените пример кода hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="4da7c-112">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="4da7c-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="4da7c-113">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="4da7c-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="4da7c-114">Каталог — это контейнер для всех пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="4da7c-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="4da7c-115">Прежде чем продолжать работу с руководством, создайте каталог B2C, если вы его еще не создали.</span><span class="sxs-lookup"><span data-stu-id="4da7c-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="4da7c-116">Необходимо tooconnect hello клиента B2C tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4da7c-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="4da7c-117">После выбора **создать**выберите hello **toomy клиента связь существующего Azure AD B2C подписки Azure** параметр и затем в hello **клиента Azure AD B2C** раскрывающийся список, выберите Вы хотите tooassociate клиента Hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="4da7c-118">Создание и регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="4da7c-118">Create and register an application</span></span>

<span data-ttu-id="4da7c-119">Далее требуется toocreate и зарегистрировать приложение hello в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="4da7c-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="4da7c-120">Предоставляет сведения, что Azure AD B2C должна toosecurely взаимодействовать с приложением.</span><span class="sxs-lookup"><span data-stu-id="4da7c-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="4da7c-121">По окончании у вас будет API и собственное приложение в параметрах приложения.</span><span class="sxs-lookup"><span data-stu-id="4da7c-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="4da7c-122">Создание политик в клиенте B2C</span><span class="sxs-lookup"><span data-stu-id="4da7c-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="4da7c-123">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4da7c-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4da7c-124">Этот пример кода включает три способа идентификации: **регистрацию и вход в систему**, **изменение профиля**, а также **сброс пароля**.</span><span class="sxs-lookup"><span data-stu-id="4da7c-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="4da7c-125">Требуется одна политика toocreate каждого типа, как описано в hello [статье политики](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4da7c-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4da7c-126">Для каждой политики быть убедиться, что tooselect hello отображаемое имя атрибута или утверждения и toocopy вниз hello имя политики для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="4da7c-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="4da7c-127">Добавление поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="4da7c-127">Add your identity providers</span></span>

<span data-ttu-id="4da7c-128">В разделе параметров щелкните **Поставщики удостоверений** и выберите вход с помощью имени пользователя или электронной почты.</span><span class="sxs-lookup"><span data-stu-id="4da7c-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="4da7c-129">Создание политики регистрации и входа в систему</span><span class="sxs-lookup"><span data-stu-id="4da7c-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="4da7c-130">Создание политики изменения профиля</span><span class="sxs-lookup"><span data-stu-id="4da7c-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="4da7c-131">Создание политики сброса паролей</span><span class="sxs-lookup"><span data-stu-id="4da7c-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="4da7c-132">После создания политики вы готовы toobuild приложения.</span><span class="sxs-lookup"><span data-stu-id="4da7c-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="4da7c-133">Загрузить пример кода hello</span><span class="sxs-lookup"><span data-stu-id="4da7c-133">Download hello sample code</span></span>

<span data-ttu-id="4da7c-134">Hello кода для этого учебника, сохраняется на [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="4da7c-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="4da7c-135">Образец hello можно клонировать, выполнив:</span><span class="sxs-lookup"><span data-stu-id="4da7c-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="4da7c-136">После загрузки кода образца hello запущен tooget файл .sln Visual Studio откройте hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="4da7c-137">Hello файл решения содержит два проекта: `TaskWebApp` и `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="4da7c-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="4da7c-138">`TaskWebApp`— hello веб-приложение MVC, hello пользователь взаимодействует с.</span><span class="sxs-lookup"><span data-stu-id="4da7c-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="4da7c-139">`TaskService`— приложение hello фоновая веб-API, который хранит список дел каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4da7c-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="4da7c-140">В этой статье рассматривается hello `TaskWebApp` приложения.</span><span class="sxs-lookup"><span data-stu-id="4da7c-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="4da7c-141">toolearn как toobuild `TaskService` с помощью Azure AD B2C, в разделе [наш учебник по api .NET web](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4da7c-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="4da7c-142">Обновить toouse код клиента и политики</span><span class="sxs-lookup"><span data-stu-id="4da7c-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="4da7c-143">Выборка — настроенное toouse hello политик и клиент идентификатор нашей демонстрационному клиенту.</span><span class="sxs-lookup"><span data-stu-id="4da7c-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="4da7c-144">tooconnect его tooyour собственного клиента, необходимо tooopen `web.config` в hello `TaskWebApp` проекта а hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="4da7c-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="4da7c-145">`ida:Tenant` именем своего клиента;</span><span class="sxs-lookup"><span data-stu-id="4da7c-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="4da7c-146">`ida:ClientId` идентификатором клиента для веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="4da7c-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="4da7c-147">`ida:ClientSecret` секретным ключом веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="4da7c-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="4da7c-148">`ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;</span><span class="sxs-lookup"><span data-stu-id="4da7c-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="4da7c-149">`ida:EditProfilePolicyId` именем политики "Изменение профиля";</span><span class="sxs-lookup"><span data-stu-id="4da7c-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="4da7c-150">`ida:ResetPasswordPolicyId` именем политики "Сброс профиля".</span><span class="sxs-lookup"><span data-stu-id="4da7c-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="4da7c-151">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="4da7c-151">Launch hello app</span></span>
<span data-ttu-id="4da7c-152">Из среды Visual Studio, запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="4da7c-153">Перемещение вкладку toohello список дел и hello примечание, URL-адрес: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="4da7c-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="4da7c-154">Зарегистрируйтесь для приложения hello вашей электронной почты адрес или имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="4da7c-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="4da7c-155">Выйдите из системы, затем войти в систему и изменить профиль hello или сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="4da7c-156">Выйдите и зарегистрируйтесь от имени другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4da7c-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="4da7c-157">Добавление поставщиков удостоверений социальных сетей</span><span class="sxs-lookup"><span data-stu-id="4da7c-157">Add social IDPs</span></span>

<span data-ttu-id="4da7c-158">В настоящее время приложение hello поддерживает только пользователь, регистрации и входе в систему с помощью **локальные учетные записи**; учетные записи хранятся в каталоге B2C использовать имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="4da7c-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="4da7c-159">С помощью Azure AD B2C можно добавить поддержку для других **поставщиков удостоверений** (IDP), не изменяя код.</span><span class="sxs-lookup"><span data-stu-id="4da7c-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="4da7c-160">tooadd социальных IDPs tooyour приложение, начните с выполнения следующего hello подробные инструкции в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="4da7c-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="4da7c-161">Для каждого поставщика Удостоверений требуется toosupport, нужно tooregister приложения в этой системе и получение идентификатора клиента.</span><span class="sxs-lookup"><span data-stu-id="4da7c-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="4da7c-162">Настройка Facebook как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="4da7c-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="4da7c-163">Настройка Google как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="4da7c-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="4da7c-164">Настройка Amazon как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="4da7c-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="4da7c-165">Настройка LinkedIn как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="4da7c-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="4da7c-166">После добавления tooyour Поставщики удостоверений hello каталоге B2C, редактирования каждого вашей tooinclude три политики hello новый IDPs, как описано в hello [статье политики](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4da7c-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4da7c-167">После сохранения политик, снова запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="4da7c-168">Вы увидите hello, добавления новых IDPs входа и регистрации в качестве параметров каждой своими впечатлениями удостоверения.</span><span class="sxs-lookup"><span data-stu-id="4da7c-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="4da7c-169">Можно поэкспериментировать с политиками и наблюдать за тем hello влияет на примере приложения.</span><span class="sxs-lookup"><span data-stu-id="4da7c-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="4da7c-170">например: добавлять или удалять поставщиков удостоверений, управлять утверждениями приложений или изменять атрибуты регистрации, а также наблюдать эффект в примере приложения.</span><span class="sxs-lookup"><span data-stu-id="4da7c-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="4da7c-171">Эксперименты помогают увидеть связь между политиками, запросами на проверку подлинности и библиотекой OWIN.</span><span class="sxs-lookup"><span data-stu-id="4da7c-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="4da7c-172">Пошаговое руководство по примеру кода</span><span class="sxs-lookup"><span data-stu-id="4da7c-172">Sample code walkthrough</span></span>
<span data-ttu-id="4da7c-173">Hello в следующих разделах показано, как настроить код приложения образец hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="4da7c-174">Вы можете использовать это руководство при разработке приложения в будущем.</span><span class="sxs-lookup"><span data-stu-id="4da7c-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="4da7c-175">Добавление поддержки проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4da7c-175">Add authentication support</span></span>

<span data-ttu-id="4da7c-176">Теперь можно настроить toouse вашего приложения Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="4da7c-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="4da7c-177">Приложение взаимодействует с Azure AD B2C, отправляя запросы проверки подлинности по протоколу OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4da7c-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="4da7c-178">Hello запросов определяют взаимодействие с пользователем hello приложение хочет tooexecute, указав hello политику.</span><span class="sxs-lookup"><span data-stu-id="4da7c-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="4da7c-179">Можно использовать эти запросы toosend библиотеки OWIN корпорации Майкрософт, выполнение политик, управление пользовательских сеансов и многое другое.</span><span class="sxs-lookup"><span data-stu-id="4da7c-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="4da7c-180">Установка OWIN</span><span class="sxs-lookup"><span data-stu-id="4da7c-180">Install OWIN</span></span>

<span data-ttu-id="4da7c-181">toobegin, добавить toohello hello OWIN по промежуточного слоя NuGet пакетов проекта с помощью консоли диспетчера пакетов Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="4da7c-182">Добавление класса запуска OWIN</span><span class="sxs-lookup"><span data-stu-id="4da7c-182">Add an OWIN startup class</span></span>

<span data-ttu-id="4da7c-183">Добавление toohello класс запуска OWIN API с именем `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="4da7c-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="4da7c-184">Правой кнопкой мыши проект hello, выберите **добавить** и **новый элемент**и выполните поиск OWIN.</span><span class="sxs-lookup"><span data-stu-id="4da7c-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="4da7c-185">по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(…)` метод при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="4da7c-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="4da7c-186">В нашем примере мы изменили объявление класса hello слишком`public partial class Startup` и реализации hello hello класса в другой части `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="4da7c-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="4da7c-187">Внутри hello `Configuration` метод, мы добавили вызов слишком`ConfigureAuth`, которая определена в `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="4da7c-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="4da7c-188">После изменения hello `Startup.cs` выглядит как hello следующее:</span><span class="sxs-lookup"><span data-stu-id="4da7c-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="4da7c-189">Настройки по промежуточного слоя проверки подлинности hello</span><span class="sxs-lookup"><span data-stu-id="4da7c-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="4da7c-190">Привет открыть файл `App_Start\Startup.Auth.cs` и реализовать hello `ConfigureAuth(...)` метод.</span><span class="sxs-lookup"><span data-stu-id="4da7c-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="4da7c-191">Здравствуйте, параметры, указываемые в `OpenIdConnectAuthenticationOptions` служат в качестве координат для toocommunicate вашего приложения с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="4da7c-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="4da7c-192">Если вы не указываете определенные параметры, он будет использовать значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="4da7c-193">Например, мы не указать hello `ResponseType` в образце hello, поэтому значение по умолчанию hello `code id_token` используются для каждого исходящего запроса tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="4da7c-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="4da7c-194">Необходимо также tooset копирование файла cookie проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4da7c-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="4da7c-195">Hello OpenID Connect по промежуточного слоя использует файлы cookie toomaintain пользовательских сеансов, среди прочего.</span><span class="sxs-lookup"><span data-stu-id="4da7c-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="4da7c-196">В `OpenIdConnectAuthenticationOptions` выше, мы определяем набор функций обратного вызова для конкретных уведомлений, полученных по промежуточного слоя, OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="4da7c-197">Эти варианты поведения определяются с помощью `OpenIdConnectAuthenticationNotifications` объекта и сохраняются в hello `Notifications` переменной.</span><span class="sxs-lookup"><span data-stu-id="4da7c-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="4da7c-198">В нашем примере мы определяем три различных обратных вызовов в зависимости от события hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="4da7c-199">Использование различных политик</span><span class="sxs-lookup"><span data-stu-id="4da7c-199">Using different policies</span></span>

<span data-ttu-id="4da7c-200">Hello `RedirectToIdentityProvider` уведомление будет запускаться при каждом запросе tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="4da7c-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="4da7c-201">В функции обратного вызова hello `OnRedirectToIdentityProvider`, мы проверяем в исходящий вызов, если мы хотим toouse hello другой политике.</span><span class="sxs-lookup"><span data-stu-id="4da7c-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="4da7c-202">В порядке toodo пароль сбросить или изменить профиль необходимо toouse hello соответствующая политика такие как политики вместо «Регистрации или входа в систему» политики по умолчанию hello сброса паролей hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="4da7c-203">В нашем примере когда пользователь хочет tooreset hello пароль или измените профиль hello мы Добавление политики hello желательно toouse контекст OWIN hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="4da7c-204">Что можно сделать, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="4da7c-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="4da7c-205">Можно применить функцию обратного вызова hello `OnRedirectToIdentityProvider` , выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="4da7c-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="4da7c-206">Обработка кодов авторизации</span><span class="sxs-lookup"><span data-stu-id="4da7c-206">Handling authorization codes</span></span>

<span data-ttu-id="4da7c-207">Hello `AuthorizationCodeReceived` уведомление срабатывает при получении кода авторизации.</span><span class="sxs-lookup"><span data-stu-id="4da7c-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="4da7c-208">по промежуточного слоя, OpenID Connect Hello не поддерживает обмен коды для маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="4da7c-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="4da7c-209">Можно вручную обмен кода hello hello маркера в функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="4da7c-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="4da7c-210">Дополнительные сведения см. в hello [документации](active-directory-b2c-devquickstarts-web-api-dotnet.md) объясняется, каким образом.</span><span class="sxs-lookup"><span data-stu-id="4da7c-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="4da7c-211">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="4da7c-211">Handling errors</span></span>

<span data-ttu-id="4da7c-212">Hello `AuthenticationFailed` уведомление срабатывает при сбое проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4da7c-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="4da7c-213">В методе обратного вызова можно обрабатывать ошибки hello по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="4da7c-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="4da7c-214">Тем не менее, следует добавить проверку для кода ошибки hello `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="4da7c-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="4da7c-215">Во время выполнения hello hello политики «Регистрации или входа в систему», hello пользователь имеет возможность tooselect hello **забыли пароль?** ссылку.</span><span class="sxs-lookup"><span data-stu-id="4da7c-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="4da7c-216">В этом случае Azure AD B2C отправляет приложения код этой ошибке, указывающее, что приложения необходимо выполнить запрос, вместо этого использовать политики сброса паролей hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="4da7c-217">Отправить tooAzure запросы проверки подлинности AD</span><span class="sxs-lookup"><span data-stu-id="4da7c-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="4da7c-218">Приложение теперь будет правильно настроен toocommunicate с Azure AD B2C с помощью протокола проверки подлинности OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="4da7c-219">OWIN управляет данными hello отправляемого сообщения проверки подлинности, проверка токены из Azure AD B2C и поддержания сеанса пользователя.</span><span class="sxs-lookup"><span data-stu-id="4da7c-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="4da7c-220">Все, что остается приведена tooinitiate каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4da7c-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="4da7c-221">Когда пользователь выбирает **входа вверх или входа**, **редактирование профиля**, или **сброс пароля** в веб-приложения hello, при вызове hello связанные действия в `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="4da7c-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="4da7c-222">Также можно использовать toosign OWIN выход hello пользователя из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="4da7c-223">В `Controllers\AccountController.cs` у нас есть следующее:</span><span class="sxs-lookup"><span data-stu-id="4da7c-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="4da7c-224">В дополнение tooexplicitly вызов политику, можно использовать `[Authorize]` тег в контроллерах, который выполняет политику, если hello пользователь не выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="4da7c-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="4da7c-225">Откройте `Controllers\HomeController.cs` и добавить hello `[Authorize]` toohello тег утверждений контроллера.</span><span class="sxs-lookup"><span data-stu-id="4da7c-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="4da7c-226">OWIN выбирает hello последние политики hello `[Authorize]` попаданий тег.</span><span class="sxs-lookup"><span data-stu-id="4da7c-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="4da7c-227">Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="4da7c-227">Display user information</span></span>

<span data-ttu-id="4da7c-228">Если для проверки подлинности пользователей с помощью OpenID Connect, Azure AD B2C возвращает идентификатор маркера toohello приложение, которое содержит **утверждений**.</span><span class="sxs-lookup"><span data-stu-id="4da7c-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="4da7c-229">Это утверждения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="4da7c-229">These are assertions about hello user.</span></span> <span data-ttu-id="4da7c-230">Toopersonalize утверждения можно использовать приложение.</span><span class="sxs-lookup"><span data-stu-id="4da7c-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="4da7c-231">Откройте hello `Controllers\HomeController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="4da7c-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="4da7c-232">Утверждения пользователей можно использовать в контроллерах через hello `ClaimsPrincipal.Current` объект субъекта безопасности.</span><span class="sxs-lookup"><span data-stu-id="4da7c-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="4da7c-233">Можно открыть любые претензии, что приложение получает в hello таким же способом.</span><span class="sxs-lookup"><span data-stu-id="4da7c-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="4da7c-234">Список всех утверждений hello, приложение hello Получает доступные на hello **утверждений** страницы.</span><span class="sxs-lookup"><span data-stu-id="4da7c-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
