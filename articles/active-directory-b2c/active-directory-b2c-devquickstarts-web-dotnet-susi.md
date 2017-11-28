---
title: "Azure Active Directory B2C | Документация Майкрософт"
description: "Сведения по созданию веб-приложений, позволяющих пользователям выполнять вход, изменять профиль, регистрироваться и сбрасывать пароль с помощью Azure Active Directory B2C."
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
ms.openlocfilehash: 3144ced01b524abb035dc1c6f0cdf764bec46804
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="633e5-103">Создание веб-приложения ASP.NET с возможностями регистрации, входа, редактирования профиля и сброса пароля Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="633e5-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="633e5-104">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="633e5-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="633e5-105">Добавление функций управления удостоверениями Azure AD B2C в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="633e5-105">Add Azure AD B2C identity features to your web app</span></span>
> * <span data-ttu-id="633e5-106">Регистрация веб-приложения в каталоге Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="633e5-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="633e5-107">Создание политики регистрации, входа, изменения профиля и сброса пароля пользователя для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="633e5-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="633e5-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="633e5-108">Prerequisites</span></span>

- <span data-ttu-id="633e5-109">Подключите клиент B2C к учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="633e5-109">You must connect your B2C Tenant to an Azure account.</span></span> <span data-ttu-id="633e5-110">Вы можете создать бесплатную учетную запись Azure [здесь](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="633e5-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="633e5-111">Вам требуется [Microsoft Visual Studio](https://www.visualstudio.com/) или аналогичная программа для просмотра и изменения примера кода.</span><span class="sxs-lookup"><span data-stu-id="633e5-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program to view and modify the sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="633e5-112">Создание каталога Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="633e5-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="633e5-113">Перед использованием Azure AD B2C необходимо создать каталог или клиент.</span><span class="sxs-lookup"><span data-stu-id="633e5-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="633e5-114">Каталог — это контейнер для всех пользователей, приложений, групп и т. д.</span><span class="sxs-lookup"><span data-stu-id="633e5-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="633e5-115">Прежде чем продолжать работу с руководством, создайте каталог B2C, если вы его еще не создали.</span><span class="sxs-lookup"><span data-stu-id="633e5-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="633e5-116">Необходимо подключить клиент B2C к подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="633e5-116">You need to connect the B2C Tenant to your Azure subscription.</span></span> <span data-ttu-id="633e5-117">Выбрав **Создать**, выберите параметр **Связывание существующего B2C-клиента Azure AD с вашей подпиской Azure**, а затем в раскрывающемся списке **Клиент B2C Azure AD** выберите клиент, которого требуется связать.</span><span class="sxs-lookup"><span data-stu-id="633e5-117">After selecting **Create**, select the **Link an existing Azure AD B2C Tenant to my Azure subscription** option, and then in the **Azure AD B2C Tenant** drop down, select the tenant you want to associate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="633e5-118">Создание и регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="633e5-118">Create and register an application</span></span>

<span data-ttu-id="633e5-119">Затем необходимо создать и зарегистрировать приложение в каталоге B2C.</span><span class="sxs-lookup"><span data-stu-id="633e5-119">Next, you need to create and register the app in your B2C directory.</span></span> <span data-ttu-id="633e5-120">Так вы получаете информацию, необходимую Azure AD B2C для безопасного взаимодействия с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="633e5-120">This provides information that Azure AD B2C needs to securely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="633e5-121">По окончании у вас будет API и собственное приложение в параметрах приложения.</span><span class="sxs-lookup"><span data-stu-id="633e5-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="633e5-122">Создание политик в клиенте B2C</span><span class="sxs-lookup"><span data-stu-id="633e5-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="633e5-123">В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="633e5-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="633e5-124">Этот пример кода включает три способа идентификации: **регистрацию и вход в систему**, **изменение профиля**, а также **сброс пароля**.</span><span class="sxs-lookup"><span data-stu-id="633e5-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="633e5-125">Вам нужно создать по одной политике каждого типа, как описано в [справочной статье о политиках](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="633e5-125">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="633e5-126">Для каждой политики выберите атрибут или утверждение отображаемого имени, а также скопируйте имя политики для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="633e5-126">For each policy, be sure to select the Display name attribute or claim, and to copy down the name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="633e5-127">Добавление поставщиков удостоверений</span><span class="sxs-lookup"><span data-stu-id="633e5-127">Add your identity providers</span></span>

<span data-ttu-id="633e5-128">В разделе параметров щелкните **Поставщики удостоверений** и выберите вход с помощью имени пользователя или электронной почты.</span><span class="sxs-lookup"><span data-stu-id="633e5-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="633e5-129">Создание политики регистрации и входа в систему</span><span class="sxs-lookup"><span data-stu-id="633e5-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="633e5-130">Создание политики изменения профиля</span><span class="sxs-lookup"><span data-stu-id="633e5-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="633e5-131">Создание политики сброса паролей</span><span class="sxs-lookup"><span data-stu-id="633e5-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="633e5-132">После создания политик можно приступать к сборке приложения.</span><span class="sxs-lookup"><span data-stu-id="633e5-132">After you create your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="633e5-133">Скачивание примера кода</span><span class="sxs-lookup"><span data-stu-id="633e5-133">Download the sample code</span></span>

<span data-ttu-id="633e5-134">Код примеров для этого руководства размещен на портале [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="633e5-134">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="633e5-135">Вы можете клонировать пример, выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="633e5-135">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="633e5-136">Скачав пример кода, откройте SLN-файл Visual Studio, чтобы начать работу.</span><span class="sxs-lookup"><span data-stu-id="633e5-136">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="633e5-137">Теперь решение содержит два проекта: `TaskWebApp` и `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="633e5-137">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="633e5-138">`TaskWebApp` — это веб-приложение MVC, с которым взаимодействует пользователь.</span><span class="sxs-lookup"><span data-stu-id="633e5-138">`TaskWebApp` is the MVC web application that the user interacts with.</span></span> <span data-ttu-id="633e5-139">`TaskService` — веб-API серверной части приложения, в котором хранится список дел для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="633e5-139">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="633e5-140">В этой статье рассматривается только приложение `TaskWebApp`.</span><span class="sxs-lookup"><span data-stu-id="633e5-140">This article will only discuss the `TaskWebApp` application.</span></span> <span data-ttu-id="633e5-141">Сведения о создании `TaskService` с помощью Azure AD B2C см. в [этом руководстве по веб-приложениям .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="633e5-141">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-to-use-your-tenant-and-policies"></a><span data-ttu-id="633e5-142">Обновление кода для использования клиента и политик</span><span class="sxs-lookup"><span data-stu-id="633e5-142">Update code to use your tenant and policies</span></span>

<span data-ttu-id="633e5-143">В нашем примере настроено использование политик и идентификатора демонстрационного клиента.</span><span class="sxs-lookup"><span data-stu-id="633e5-143">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="633e5-144">Чтобы подключить его к своему клиенту, необходимо открыть файл `web.config` в проекте `TaskWebApp` и заменить следующие значения:</span><span class="sxs-lookup"><span data-stu-id="633e5-144">To connect it to your own tenant, you need to open `web.config` in the `TaskWebApp` project and replace the following values:</span></span>

* <span data-ttu-id="633e5-145">`ida:Tenant` именем своего клиента;</span><span class="sxs-lookup"><span data-stu-id="633e5-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="633e5-146">`ida:ClientId` идентификатором клиента для веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="633e5-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="633e5-147">`ida:ClientSecret` секретным ключом веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="633e5-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="633e5-148">`ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;</span><span class="sxs-lookup"><span data-stu-id="633e5-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="633e5-149">`ida:EditProfilePolicyId` именем политики "Изменение профиля";</span><span class="sxs-lookup"><span data-stu-id="633e5-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="633e5-150">`ida:ResetPasswordPolicyId` именем политики "Сброс профиля".</span><span class="sxs-lookup"><span data-stu-id="633e5-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-the-app"></a><span data-ttu-id="633e5-151">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="633e5-151">Launch the app</span></span>
<span data-ttu-id="633e5-152">Из среды Visual Studio запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="633e5-152">From within Visual Studio, launch the app.</span></span> <span data-ttu-id="633e5-153">Перейдите на вкладку To-Do List (Список задач) и обратите внимание на URL-адрес: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.</span><span class="sxs-lookup"><span data-stu-id="633e5-153">Navigate to the To-Do List tab, and note the URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="633e5-154">Зарегистрируйтесь в приложении с использованием адреса электронной почты или имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="633e5-154">Sign up for the app by using your email address or user name.</span></span> <span data-ttu-id="633e5-155">Выйдите из системы, а затем войдите и измените профиль или сбросьте пароль.</span><span class="sxs-lookup"><span data-stu-id="633e5-155">Sign out, then sign in again and edit the profile or reset the password.</span></span> <span data-ttu-id="633e5-156">Выйдите и зарегистрируйтесь от имени другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="633e5-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="633e5-157">Добавление поставщиков удостоверений социальных сетей</span><span class="sxs-lookup"><span data-stu-id="633e5-157">Add social IDPs</span></span>

<span data-ttu-id="633e5-158">Сейчас приложение поддерживает регистрацию и вход пользователя с помощью **локальных учетных записей**, которые хранятся в каталоге B2C и используют имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="633e5-158">Currently, the app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="633e5-159">С помощью Azure AD B2C можно добавить поддержку для других **поставщиков удостоверений** (IDP), не изменяя код.</span><span class="sxs-lookup"><span data-stu-id="633e5-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="633e5-160">Чтобы добавить в приложение поставщиков удостоверений социальных сетей, следуйте подробным инструкциям, приведенным в указанных ниже статьях.</span><span class="sxs-lookup"><span data-stu-id="633e5-160">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="633e5-161">Для каждого поставщика удостоверений, поддержку которого нужно добавить, необходимо зарегистрировать приложение в соответствующей системе и получить идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="633e5-161">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="633e5-162">Настройка Facebook как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="633e5-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="633e5-163">Настройка Google как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="633e5-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="633e5-164">Настройка Amazon как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="633e5-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="633e5-165">Настройка LinkedIn как поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="633e5-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="633e5-166">Добавив поставщики удостоверений в каталог B2C, внесите соответствующие изменения в три политики, как описано в [справочной статье о политиках](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="633e5-166">After you add the identity providers to your B2C directory, edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="633e5-167">Сохраните политики и перезапустите приложение.</span><span class="sxs-lookup"><span data-stu-id="633e5-167">After you save your policies, run the app again.</span></span>  <span data-ttu-id="633e5-168">Добавленные поставщики удостоверений должны отобразиться в виде вариантов при входе и регистрации.</span><span class="sxs-lookup"><span data-stu-id="633e5-168">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="633e5-169">Вы можете свободно экспериментировать с политиками,</span><span class="sxs-lookup"><span data-stu-id="633e5-169">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="633e5-170">например: добавлять или удалять поставщиков удостоверений, управлять утверждениями приложений или изменять атрибуты регистрации, а также наблюдать эффект в примере приложения.</span><span class="sxs-lookup"><span data-stu-id="633e5-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="633e5-171">Эксперименты помогают увидеть связь между политиками, запросами на проверку подлинности и библиотекой OWIN.</span><span class="sxs-lookup"><span data-stu-id="633e5-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="633e5-172">Пошаговое руководство по примеру кода</span><span class="sxs-lookup"><span data-stu-id="633e5-172">Sample code walkthrough</span></span>
<span data-ttu-id="633e5-173">В следующих разделах показано, как настроить пример кода приложения.</span><span class="sxs-lookup"><span data-stu-id="633e5-173">The following sections show you how the sample application code is configured.</span></span> <span data-ttu-id="633e5-174">Вы можете использовать это руководство при разработке приложения в будущем.</span><span class="sxs-lookup"><span data-stu-id="633e5-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="633e5-175">Добавление поддержки проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="633e5-175">Add authentication support</span></span>

<span data-ttu-id="633e5-176">Теперь можно настроить приложение для использования Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="633e5-176">You can now configure your app to use Azure AD B2C.</span></span> <span data-ttu-id="633e5-177">Приложение взаимодействует с Azure AD B2C, отправляя запросы проверки подлинности по протоколу OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="633e5-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="633e5-178">В запросах задана политика, регулирующая взаимодействие пользователя с приложением.</span><span class="sxs-lookup"><span data-stu-id="633e5-178">The requests dictate the user experience your app wants to execute by specifying the policy.</span></span> <span data-ttu-id="633e5-179">Вы можете использовать библиотеку OWIN от Майкрософт. С ее помощью можно отправлять запросы, выполнять политики, управлять сеансом пользователя и решать другие задачи.</span><span class="sxs-lookup"><span data-stu-id="633e5-179">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="633e5-180">Установка OWIN</span><span class="sxs-lookup"><span data-stu-id="633e5-180">Install OWIN</span></span>

<span data-ttu-id="633e5-181">Сначала добавьте пакеты NuGet ПО промежуточного слоя OWIN в проект с помощью консоли диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="633e5-181">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="633e5-182">Добавление класса запуска OWIN</span><span class="sxs-lookup"><span data-stu-id="633e5-182">Add an OWIN startup class</span></span>

<span data-ttu-id="633e5-183">Добавьте класс запуска OWIN в API с именем `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="633e5-183">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="633e5-184">Щелкните проект правой кнопкой мыши и выберите **Добавить** и **Новый элемент**, после чего найдите OWIN.</span><span class="sxs-lookup"><span data-stu-id="633e5-184">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="633e5-185">При запуске вашего приложения промежуточный слой OWIN вызовет метод `Configuration(…)` .</span><span class="sxs-lookup"><span data-stu-id="633e5-185">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="633e5-186">В нашем примере мы изменили объявление класса на `public partial class Startup` и реализовали другую часть класса в `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="633e5-186">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="633e5-187">Внутри метода `Configuration` мы добавили вызов `ConfigureAuth`, определенный в `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="633e5-187">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="633e5-188">После внесения изменений `Startup.cs` выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="633e5-188">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-the-authentication-middleware"></a><span data-ttu-id="633e5-189">Настройка ПО промежуточного слоя для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="633e5-189">Configure the authentication middleware</span></span>

<span data-ttu-id="633e5-190">Откройте файл `App_Start\Startup.Auth.cs` и реализуйте метод `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="633e5-190">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="633e5-191">Параметры, указанные в разделе `OpenIdConnectAuthenticationOptions`, будут служить координатами приложения для взаимодействия с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="633e5-191">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span></span> <span data-ttu-id="633e5-192">Если не задать определенные параметры, будут использоваться значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="633e5-192">If you do not specify certain parameters, it will use the default value.</span></span> <span data-ttu-id="633e5-193">Например, в примере не был указан параметр `ResponseType`, поэтому для каждого исходящего запроса к Azure AD B2C будет использоваться значение по умолчанию `code id_token`.</span><span class="sxs-lookup"><span data-stu-id="633e5-193">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span></span>

<span data-ttu-id="633e5-194">Также будет необходимо настроить проверку подлинности для файлов Cookie —</span><span class="sxs-lookup"><span data-stu-id="633e5-194">You also need to set up cookie authentication.</span></span> <span data-ttu-id="633e5-195">промежуточный слой OpenID Connect использует файлы cookie для поддержки сеанса пользователя и выполнения других задач.</span><span class="sxs-lookup"><span data-stu-id="633e5-195">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure the OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate the metadata address using the tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify the callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify the claims to validate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement the "Notification" methods...
}
```

<span data-ttu-id="633e5-196">В приведенном выше разделе `OpenIdConnectAuthenticationOptions` мы определили набор функций обратного вызова для специальных уведомлений, получаемых с помощью ПО промежуточного слоя OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="633e5-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span></span> <span data-ttu-id="633e5-197">Эти поведения определяются с помощью объекта `OpenIdConnectAuthenticationNotifications` и хранятся в переменной `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="633e5-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span></span> <span data-ttu-id="633e5-198">В этом примере мы определяем три различных обратных вызова в зависимости от события.</span><span class="sxs-lookup"><span data-stu-id="633e5-198">In our sample, we define three different callbacks depending on the event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="633e5-199">Использование различных политик</span><span class="sxs-lookup"><span data-stu-id="633e5-199">Using different policies</span></span>

<span data-ttu-id="633e5-200">При каждом запросе к Azure AD B2C инициируется уведомление `RedirectToIdentityProvider`.</span><span class="sxs-lookup"><span data-stu-id="633e5-200">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span></span> <span data-ttu-id="633e5-201">Если требуется использовать другую политику, в функции обратного вызова `OnRedirectToIdentityProvider` нужно проверять исходящий вызов.</span><span class="sxs-lookup"><span data-stu-id="633e5-201">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span></span> <span data-ttu-id="633e5-202">Чтобы сбросить пароль или изменить профиль, необходимо использовать соответствующую политику, например политику сброса паролей, вместо политики регистрации или входа, заданной по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="633e5-202">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="633e5-203">В этом примере, если пользователь хочет сбросить пароль или изменить профиль, мы добавляем политику, которую рекомендуется использовать в контексте OWIN.</span><span class="sxs-lookup"><span data-stu-id="633e5-203">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span></span> <span data-ttu-id="633e5-204">Для этого необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="633e5-204">That can be done by doing the following:</span></span>

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="633e5-205">Вы можете реализовать функцию обратного вызова `OnRedirectToIdentityProvider`, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="633e5-205">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span></span>

```CSharp
/*
*  On each call to Azure AD B2C, check if a policy (e.g. the profile edit or password reset policy) has been specified in the OWIN context.
*  If so, use that policy when making the call. Also, don't request a code (since it won't be needed).
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

### <a name="handling-authorization-codes"></a><span data-ttu-id="633e5-206">Обработка кодов авторизации</span><span class="sxs-lookup"><span data-stu-id="633e5-206">Handling authorization codes</span></span>

<span data-ttu-id="633e5-207">При получении кода авторизации инициируется уведомление `AuthorizationCodeReceived`.</span><span class="sxs-lookup"><span data-stu-id="633e5-207">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="633e5-208">ПО промежуточного слоя OpenID Connect не поддерживает обмен кодов на маркеры доступа.</span><span class="sxs-lookup"><span data-stu-id="633e5-208">The OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="633e5-209">Вы можете вручную выполнить обмен кода на маркер в функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="633e5-209">You can manually exchange the code for the token in a callback function.</span></span> <span data-ttu-id="633e5-210">Дополнительные сведения см. в [этой документации](active-directory-b2c-devquickstarts-web-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="633e5-210">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="633e5-211">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="633e5-211">Handling errors</span></span>

<span data-ttu-id="633e5-212">При сбое проверки подлинности инициируется уведомление `AuthenticationFailed`.</span><span class="sxs-lookup"><span data-stu-id="633e5-212">The `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="633e5-213">С помощью метода обратного вызова можно обрабатывать ошибки по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="633e5-213">In its callback method, you can handle the errors as you wish.</span></span> <span data-ttu-id="633e5-214">Тем не менее необходимо добавить проверку кода ошибки `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="633e5-214">You should however add a check for the error code `AADB2C90118`.</span></span> <span data-ttu-id="633e5-215">Во время выполнения политики регистрации и входа пользователь может щелкнуть ссылку **Забыли пароль?**.</span><span class="sxs-lookup"><span data-stu-id="633e5-215">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to select a **Forgot your password?** link.</span></span> <span data-ttu-id="633e5-216">В этом случае Azure AD B2C отправляет код ошибки, указывающий, что приложение должно выполнить запрос с помощью политики сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="633e5-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using the password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by the authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle the error code that Azure AD B2C throws when trying to reset a password from the login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If the user clicked the reset password link, redirect to the reset password route
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

### <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="633e5-217">Отправка запросов на проверку подлинности в Azure AD</span><span class="sxs-lookup"><span data-stu-id="633e5-217">Send authentication requests to Azure AD</span></span>

<span data-ttu-id="633e5-218">Теперь приложение настроено на взаимодействие с Azure AD B2C с использованием протокола проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="633e5-218">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="633e5-219">OWIN берет на себя создание сообщений аутентификации, проверку маркеров из Azure AD B2C и поддержку сеанса пользователя.</span><span class="sxs-lookup"><span data-stu-id="633e5-219">OWIN manages the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="633e5-220">Осталось инициировать все потоки пользователей.</span><span class="sxs-lookup"><span data-stu-id="633e5-220">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="633e5-221">Когда пользователь выбирает **Регистрация или Вход**, **Изменить профиль** или **Сброс пароля** в веб-приложении, в `Controllers\AccountController.cs` вызывается соответствующее действие:</span><span class="sxs-lookup"><span data-stu-id="633e5-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign up or sign in
*/
public void SignUpSignIn()
{
    // Use the default policy to process the sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting to edit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let the middleware know you are trying to use the edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set the page to redirect to after editing the profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting to reset a password
*/
public void ResetPassword()
{
    // Let the middleware know you are trying to use the reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set the page to redirect to after changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="633e5-222">Для выхода пользователя из приложения также можно использовать OWIN.</span><span class="sxs-lookup"><span data-stu-id="633e5-222">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="633e5-223">В `Controllers\AccountController.cs` у нас есть следующее:</span><span class="sxs-lookup"><span data-stu-id="633e5-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign out
*/
public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="633e5-224">Помимо явного вызова политики, можно использовать тег `[Authorize]` в контроллерах, что приведет к выполнению политики, если пользователь не выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="633e5-224">In addition to explicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if the user is not signed in.</span></span> <span data-ttu-id="633e5-225">Откройте файл `Controllers\HomeController.cs` и добавьте тег `[Authorize]` в контроллер утверждений.</span><span class="sxs-lookup"><span data-stu-id="633e5-225">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="633e5-226">OWIN выберет последнюю настроенную политику при вызове тега `[Authorize]`.</span><span class="sxs-lookup"><span data-stu-id="633e5-226">OWIN selects the last policy configured when the `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="633e5-227">Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="633e5-227">Display user information</span></span>

<span data-ttu-id="633e5-228">При проверке подлинности пользователей с помощью OpenID Connect служба Azure AD B2C возвращает в приложение маркер идентификатора, который содержит **утверждения**.</span><span class="sxs-lookup"><span data-stu-id="633e5-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="633e5-229">о пользователе.</span><span class="sxs-lookup"><span data-stu-id="633e5-229">These are assertions about the user.</span></span> <span data-ttu-id="633e5-230">Эти утверждения можно использовать для персонализации приложения.</span><span class="sxs-lookup"><span data-stu-id="633e5-230">You can use claims to personalize your app.</span></span>

<span data-ttu-id="633e5-231">Откройте файл `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="633e5-231">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="633e5-232">Для доступа к утверждениям о пользователе в своих контроллерах можно использовать объект субъекта безопасности `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="633e5-232">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

<span data-ttu-id="633e5-233">Вы можете открыть любое утверждение, которое ваше приложение получает таким же образом.</span><span class="sxs-lookup"><span data-stu-id="633e5-233">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="633e5-234">Список всех получаемых приложением утверждений можно найти на странице **Утверждения** .</span><span class="sxs-lookup"><span data-stu-id="633e5-234">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>
