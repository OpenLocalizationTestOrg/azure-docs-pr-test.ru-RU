---
title: "Azure Active Directory B2C: регистрация приложения | Документация Майкрософт"
description: "Как tooregister приложения с Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="a4232-103">Azure Active Directory B2C: регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="a4232-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="a4232-104">Из этого краткого руководства вы узнаете, как зарегистрировать приложение в клиенте Microsoft Azure Active Directory (Azure AD) B2C за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a4232-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="a4232-105">После завершения приложение регистрируется для использования в клиенте hello Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="a4232-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4232-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a4232-106">Prerequisites</span></span>

<span data-ttu-id="a4232-107">toobuild приложения, которое принимает потребителя регистрации и входе в систему, необходимо сначала приложения hello tooregister с клиентом Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a4232-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="a4232-108">Получение вашего собственного клиента с помощью hello действия, описанные в [создание клиента Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a4232-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="a4232-109">Приложения, созданные из колонки hello Azure AD B2C в hello портал Azure, должна управляться из hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="a4232-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="a4232-110">При редактировании hello B2C приложений с помощью PowerShell или другого портала становятся не поддерживается и не работают с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a4232-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="a4232-111">Просмотреть сведения в hello [произошел сбой приложения](#faulted-apps) раздела.</span><span class="sxs-lookup"><span data-stu-id="a4232-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="a4232-112">Параметры tooB2C перехода</span><span class="sxs-lookup"><span data-stu-id="a4232-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="a4232-113">Войдите в toohello [портал Azure](https://portal.azure.com/) как глобальный администратор клиента hello B2C hello.</span><span class="sxs-lookup"><span data-stu-id="a4232-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="a4232-114">Выбор следующего действия в зависимости от типа приложения hello, регистрируемая:</span><span class="sxs-lookup"><span data-stu-id="a4232-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="a4232-115">регистрация веб-приложения;</span><span class="sxs-lookup"><span data-stu-id="a4232-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="a4232-116">регистрация веб-API;</span><span class="sxs-lookup"><span data-stu-id="a4232-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="a4232-117">регистрация мобильного или собственного приложения.</span><span class="sxs-lookup"><span data-stu-id="a4232-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="a4232-118">Регистрация веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a4232-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="a4232-119">Если веб-приложение вызовет веб-API, защищенный Azure AD B2C, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a4232-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="a4232-120">Создать секрет приложения с переходом toohello **ключей** колонки и щелкнув hello **создать ключ** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a4232-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="a4232-121">Запишите hello **ключ приложения** значение.</span><span class="sxs-lookup"><span data-stu-id="a4232-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="a4232-122">Значение hello используется секрет приложения hello в код приложения.</span><span class="sxs-lookup"><span data-stu-id="a4232-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="a4232-123">Щелкните **Доступ через API**, **Добавить** и выберите свой веб-API и области (разрешения).</span><span class="sxs-lookup"><span data-stu-id="a4232-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="a4232-124">**Секрет приложения** — это важные учетные данные безопасности, которые должны быть надежно защищены.</span><span class="sxs-lookup"><span data-stu-id="a4232-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="a4232-125">Переход слишком**дальнейшие действия**</span><span class="sxs-lookup"><span data-stu-id="a4232-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="a4232-126">Регистрация веб-API</span><span class="sxs-lookup"><span data-stu-id="a4232-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="a4232-127">Нажмите кнопку **публикации областей** tooadd более областей при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a4232-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="a4232-128">По умолчанию определяется областью «user_impersonation» hello.</span><span class="sxs-lookup"><span data-stu-id="a4232-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="a4232-129">областью user_impersonation Hello дает tooaccess возможность hello других приложений этот api от имени пользователя, выполнившего вход hello.</span><span class="sxs-lookup"><span data-stu-id="a4232-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="a4232-130">При желании можно удалить областью user_impersonation hello.</span><span class="sxs-lookup"><span data-stu-id="a4232-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="a4232-131">Переход слишком**дальнейшие действия**</span><span class="sxs-lookup"><span data-stu-id="a4232-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="a4232-132">Регистрация мобильного или собственного приложения</span><span class="sxs-lookup"><span data-stu-id="a4232-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="a4232-133">Переход слишком**дальнейшие действия**</span><span class="sxs-lookup"><span data-stu-id="a4232-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="a4232-134">Ограничения</span><span class="sxs-lookup"><span data-stu-id="a4232-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="a4232-135">Выбор URL-адреса ответа для веб-приложения или API</span><span class="sxs-lookup"><span data-stu-id="a4232-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="a4232-136">В настоящее время приложения, которые зарегистрированы в Azure AD B2C являются ограниченными tooa ограниченный набор значений URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="a4232-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="a4232-137">Здравствуйте, URL-адрес для веб-приложений и служб должны начинаться со схемой hello ответ `https`, и всех ответов значений URL-адреса должны совместно использовать одного домена DNS.</span><span class="sxs-lookup"><span data-stu-id="a4232-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="a4232-138">Например, невозможно зарегистрировать веб-приложение с одним из следующих URL-адресов ответа:</span><span class="sxs-lookup"><span data-stu-id="a4232-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="a4232-139">Система регистрации Hello сравнивает hello всей DNS-имя hello существующего ответа URL-адрес toohello DNS-имя URL-адреса hello ответа, который добавляется.</span><span class="sxs-lookup"><span data-stu-id="a4232-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="a4232-140">hello tooadd Hello запрос DNS-имя завершается ошибкой, если выполняется любое из следующих условий hello:</span><span class="sxs-lookup"><span data-stu-id="a4232-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="a4232-141">Hello всей DNS-имя hello новый URL-адрес ответа не соответствует DNS-имя hello hello существующий URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="a4232-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="a4232-142">всего DNS-имя Hello hello новый URL-адреса ответа не поддомен hello существующий URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="a4232-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="a4232-143">Например если hello приложение имеет этот URL-адрес ответа:</span><span class="sxs-lookup"><span data-stu-id="a4232-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="a4232-144">Можно добавить tooit следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a4232-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="a4232-145">В этом случае hello DNS-имя соответствует точно.</span><span class="sxs-lookup"><span data-stu-id="a4232-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="a4232-146">Или же можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="a4232-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="a4232-147">В этом случае ссылка поддомен login.contoso.com tooa DNS. Если вы хотите toohave входа east.contoso.com и west.contoso.com входа как URL-адреса ответа приложения, необходимо добавить эти URL-адреса ответа в указанном порядке:</span><span class="sxs-lookup"><span data-stu-id="a4232-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="a4232-148">Можно добавить hello последние две, поскольку они являются поддомены hello первого URL-адреса ответа, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a4232-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="a4232-149">Выбор URI перенаправления для собственного приложения</span><span class="sxs-lookup"><span data-stu-id="a4232-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="a4232-150">При выборе URI перенаправления для мобильных и собственных приложений нужно учитывать два важных момента:</span><span class="sxs-lookup"><span data-stu-id="a4232-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="a4232-151">**Уникальный**: hello схема URI перенаправления hello должно быть уникальным для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="a4232-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="a4232-152">В нашем примере (com.onmicrosoft.contoso.appname://redirect/path) мы используем com.onmicrosoft.contoso.appname как схему hello.</span><span class="sxs-lookup"><span data-stu-id="a4232-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="a4232-153">Рекомендуется следовать этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="a4232-153">We recommend following this pattern.</span></span> <span data-ttu-id="a4232-154">Если два приложения имеют hello же схемы, hello пользователь видит диалоговое окно «Выбор приложений».</span><span class="sxs-lookup"><span data-stu-id="a4232-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="a4232-155">Если пользователь hello вносит неправильному выбору, вход hello не выполняется.</span><span class="sxs-lookup"><span data-stu-id="a4232-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="a4232-156">**Полнота**. URI перенаправления должен иметь схему и путь.</span><span class="sxs-lookup"><span data-stu-id="a4232-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="a4232-157">Hello путь должен содержать по крайней мере одного знака косой черты после hello домена (например, //contoso/ работает и //contoso завершается с ошибкой).</span><span class="sxs-lookup"><span data-stu-id="a4232-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="a4232-158">Убедитесь, что никакие специальные символы, как символ подчеркивания в hello uri перенаправления.</span><span class="sxs-lookup"><span data-stu-id="a4232-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="a4232-159">Неисправные приложения</span><span class="sxs-lookup"><span data-stu-id="a4232-159">Faulted apps</span></span>

<span data-ttu-id="a4232-160">Не следует вносить изменения в приложения B2C:</span><span class="sxs-lookup"><span data-stu-id="a4232-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="a4232-161">с помощью других порталов для управления приложениями, таких как [классический портал Azure](https://manage.windowsazure.com/) и [портал регистрации приложений](https://apps.dev.microsoft.com/);</span><span class="sxs-lookup"><span data-stu-id="a4232-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="a4232-162">с помощью API Graph или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4232-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="a4232-163">Если изменить приложение hello B2C, как описано выше и повторите tooedit его снова в колонке функции hello Azure AD B2C на hello портал Azure, становится неисправной приложения и приложения больше не может использоваться с Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a4232-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="a4232-164">Приложение hello toodelete и создайте его заново.</span><span class="sxs-lookup"><span data-stu-id="a4232-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="a4232-165">приложение hello toodelete, последовательно выберите toohello [портала регистрации приложения](https://apps.dev.microsoft.com/) и удалить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="a4232-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="a4232-166">Чтобы toobe приложения hello видимым понадобится toobe hello владелец приложения hello (и не только администратор клиента hello).</span><span class="sxs-lookup"><span data-stu-id="a4232-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4232-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4232-167">Next steps</span></span>

<span data-ttu-id="a4232-168">Теперь, когда приложение зарегистрировано в Azure AD B2C, выполните одно из [нашим руководствам краткое](active-directory-b2c-overview.md#get-started) tooget запуска.</span><span class="sxs-lookup"><span data-stu-id="a4232-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4232-169">Azure AD B2C: регистрация и вход в систему в веб-приложении ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a4232-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)