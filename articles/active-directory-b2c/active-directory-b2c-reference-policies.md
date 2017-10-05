---
title: "Azure Active Directory B2C: встроенные политики | Документы Майкрософт"
description: "В разделе описывается инфраструктура расширяемых политик Azure Active Directory B2C и создание различных типов политик."
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: daad3af089afdf76b930053728bb11a5cf4c2a92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="0b50a-103">Azure Active Directory B2C: встроенные политики</span><span class="sxs-lookup"><span data-stu-id="0b50a-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="0b50a-104">Инфраструктура расширяемых политик Azure Active Directory (Azure AD) B2C — это основное преимущество службы.</span><span class="sxs-lookup"><span data-stu-id="0b50a-104">The extensible policy framework of Azure Active Directory (Azure AD) B2C is the core strength of the service.</span></span> <span data-ttu-id="0b50a-105">Политики полностью описывают процесс идентификации пользователей: регистрацию, вход и редактирование профиля.</span><span class="sxs-lookup"><span data-stu-id="0b50a-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="0b50a-106">К примеру, политика регистрации позволяет управлять поведением с помощью таких параметров:</span><span class="sxs-lookup"><span data-stu-id="0b50a-106">For instance, a sign-up policy allows you to control behaviors by configuring the following settings:</span></span>

* <span data-ttu-id="0b50a-107">типы учетных записей (учетные записи в социальных сетях, например Facebook, или локальные учетные записи, например адреса электронной почты), которые пользователи могут применять для регистрации в приложении;</span><span class="sxs-lookup"><span data-stu-id="0b50a-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use to sign up for the application</span></span>
* <span data-ttu-id="0b50a-108">атрибуты (например, имя, почтовый индекс и размер обуви), которые нужно получить от пользователя во время регистрации;</span><span class="sxs-lookup"><span data-stu-id="0b50a-108">Attributes (for example, first name, postal code, and shoe size) to be collected from the consumer during sign-up</span></span>
* <span data-ttu-id="0b50a-109">использование Многофакторной идентификации Azure;</span><span class="sxs-lookup"><span data-stu-id="0b50a-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="0b50a-110">внешний вид и удобство использования всех страниц регистрации;</span><span class="sxs-lookup"><span data-stu-id="0b50a-110">The look and feel of all sign-up pages</span></span>
* <span data-ttu-id="0b50a-111">сведения (объявляемые в качестве утверждений в токене), которые получает приложение после завершения выполнения политики.</span><span class="sxs-lookup"><span data-stu-id="0b50a-111">Information (which manifests as claims in a token) that the application receives when the policy run finishes</span></span>

<span data-ttu-id="0b50a-112">В своем клиенте вы можете создать несколько политик различных типов и при необходимости использовать их в приложениях.</span><span class="sxs-lookup"><span data-stu-id="0b50a-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="0b50a-113">Политики могут повторно использоваться в разных приложениях.</span><span class="sxs-lookup"><span data-stu-id="0b50a-113">Policies can be reused across applications.</span></span> <span data-ttu-id="0b50a-114">Такая гибкость позволяет разработчикам определять и изменять процесс идентификации пользователя, внося лишь незначительные изменения в код или совсем не изменяя его.</span><span class="sxs-lookup"><span data-stu-id="0b50a-114">This flexibility enables developers to define and modify consumer identity experiences with minimal or no changes to their code.</span></span>

<span data-ttu-id="0b50a-115">Работа с политиками выполняется через простой интерфейс разработчика.</span><span class="sxs-lookup"><span data-stu-id="0b50a-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="0b50a-116">Приложение запускает политику с помощью стандартного HTTP-запроса на проверку подлинности (передавая в запросе параметр политики) и в ответ получает настроенный токен.</span><span class="sxs-lookup"><span data-stu-id="0b50a-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in the request) and receives a customized token as response.</span></span> <span data-ttu-id="0b50a-117">Например, единственное различие между запросами, которые вызывают политику регистрации и политику входа, заключается в имени политики, которое используется в качестве строкового параметра "p" в запросе.</span><span class="sxs-lookup"><span data-stu-id="0b50a-117">For example, the only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is the policy name that's used in the "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="0b50a-118">Дополнительные сведения об инфраструктуре политики см. в [этой записи, посвященной Azure AD B2C, в блоге по Enterprise Mobility and Security](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b50a-118">For more information about the policy framework, see [this blog post about Azure AD B2C on the Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="0b50a-119">Создание политики регистрации или входа в систему</span><span class="sxs-lookup"><span data-stu-id="0b50a-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="0b50a-120">Эта политика регулирует процедуры регистрации и входа в систему в рамках одной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b50a-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="0b50a-121">Потребители проводятся через соответствующую процедуру (регистрации или входа в систему) в зависимости от контекста.</span><span class="sxs-lookup"><span data-stu-id="0b50a-121">Consumers are led down the right path (sign-up or sign-in) depending on the context.</span></span> <span data-ttu-id="0b50a-122">В ней также описывается содержимое токенов, которые приложение будет получать при успешной регистрации или входе в систему.  Пример кода для политики регистрации или входа в систему см. [здесь](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="0b50a-122">It also describes the contents of tokens that the application will receive upon successful sign-ups or sign-ins.  A code sample for the sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="0b50a-123">Мы рекомендуем использовать эту политику вместо политики регистрации и политики входа в систему.</span><span class="sxs-lookup"><span data-stu-id="0b50a-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="0b50a-124">Создание политики регистрации</span><span class="sxs-lookup"><span data-stu-id="0b50a-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="0b50a-125">Создание политики входа в систему</span><span class="sxs-lookup"><span data-stu-id="0b50a-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="0b50a-126">Создание политики изменения профиля</span><span class="sxs-lookup"><span data-stu-id="0b50a-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="0b50a-127">Создание политики сброса паролей</span><span class="sxs-lookup"><span data-stu-id="0b50a-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="0b50a-128">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="0b50a-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="0b50a-129">Как связать политику регистрации или входа с политикой сброса паролей?</span><span class="sxs-lookup"><span data-stu-id="0b50a-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="0b50a-130">При создании политики регистрации или входа (с помощью локальных учетных записей) на первой странице отображается ссылка **Забыли пароль?**.</span><span class="sxs-lookup"><span data-stu-id="0b50a-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on the first page of the experience.</span></span> <span data-ttu-id="0b50a-131">При переходе по этой ссылке политика сброса паролей не активируется автоматически.</span><span class="sxs-lookup"><span data-stu-id="0b50a-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="0b50a-132">Вместо этого в приложение возвращается код ошибки **`AADB2C90118`**.</span><span class="sxs-lookup"><span data-stu-id="0b50a-132">Instead, the error code **`AADB2C90118`** is returned to your app.</span></span> <span data-ttu-id="0b50a-133">Приложение должно обработать этот код, вызвав определенную политику сброса паролей.</span><span class="sxs-lookup"><span data-stu-id="0b50a-133">Your app needs to handle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="0b50a-134">Дополнительные сведения см. в [примере, демонстрирующем подход к связыванию политик](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="0b50a-134">For more information, see a [sample that demonstrates the approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="0b50a-135">Следует ли использовать политику регистрации или входа либо две политики: политику регистрации и политику входа?</span><span class="sxs-lookup"><span data-stu-id="0b50a-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="0b50a-136">Мы рекомендуем использовать политику регистрации или входа вместо политики регистрации и политики входа.</span><span class="sxs-lookup"><span data-stu-id="0b50a-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="0b50a-137">Политика регистрации или входа обеспечивает больше возможностей, чем политика входа.</span><span class="sxs-lookup"><span data-stu-id="0b50a-137">The sign-up or sign-in policy has more capabilities than the sign-in policy.</span></span> <span data-ttu-id="0b50a-138">Она также позволяет настраивать пользовательский интерфейс страницы и лучше поддерживает локализацию.</span><span class="sxs-lookup"><span data-stu-id="0b50a-138">It also enables you to use page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="0b50a-139">Политика входа рекомендуется, если вам не нужно локализовать политики либо если вам требуются ограниченные возможности для настройки фирменного оформления и встроенные возможности сброса паролей.</span><span class="sxs-lookup"><span data-stu-id="0b50a-139">The sign-in policy is recommended if you don't need to localize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b50a-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b50a-140">Next steps</span></span>
* [<span data-ttu-id="0b50a-141">Настройка токена, сеанса и единого входа</span><span class="sxs-lookup"><span data-stu-id="0b50a-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="0b50a-142">Azure Active Directory B2C: отключение проверки адреса электронной почты во время регистрации потребителя</span><span class="sxs-lookup"><span data-stu-id="0b50a-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

