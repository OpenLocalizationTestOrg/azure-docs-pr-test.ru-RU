---
title: "Azure Active Directory B2C: встроенные политики | Документы Майкрософт"
description: "Раздел на hello расширяемая инфраструктура политик из Azure Active Directory B2C и о том, как toocreate различные типы политики"
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
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="05c87-103">Azure Active Directory B2C: встроенные политики</span><span class="sxs-lookup"><span data-stu-id="05c87-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="05c87-104">Hello расширяемая инфраструктура политик из B2C Azure Active Directory (Azure AD) — сильные стороны hello hello службы.</span><span class="sxs-lookup"><span data-stu-id="05c87-104">hello extensible policy framework of Azure Active Directory (Azure AD) B2C is hello core strength of hello service.</span></span> <span data-ttu-id="05c87-105">Политики полностью описывают процесс идентификации пользователей: регистрацию, вход и редактирование профиля.</span><span class="sxs-lookup"><span data-stu-id="05c87-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="05c87-106">Например политику регистрации позволяет toocontrol поведения, настроив следующие параметры hello:</span><span class="sxs-lookup"><span data-stu-id="05c87-106">For instance, a sign-up policy allows you toocontrol behaviors by configuring hello following settings:</span></span>

* <span data-ttu-id="05c87-107">Что потребители могут использовать toosign для использования приложения hello типов (социальных учетные записи таких как Facebook) или локальные учетные записи, такие как адреса электронной почты учетной записи</span><span class="sxs-lookup"><span data-stu-id="05c87-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use toosign up for hello application</span></span>
* <span data-ttu-id="05c87-108">Атрибуты (например, имя, почтовый индекс и размере обуви) toobe, полученные от потребителя hello во время регистрации</span><span class="sxs-lookup"><span data-stu-id="05c87-108">Attributes (for example, first name, postal code, and shoe size) toobe collected from hello consumer during sign-up</span></span>
* <span data-ttu-id="05c87-109">использование Многофакторной идентификации Azure;</span><span class="sxs-lookup"><span data-stu-id="05c87-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="05c87-110">Hello внешний вид и поведение все страницы регистрации</span><span class="sxs-lookup"><span data-stu-id="05c87-110">hello look and feel of all sign-up pages</span></span>
* <span data-ttu-id="05c87-111">Получает сведения (которая объявляется в качестве утверждения в токене), приложение hello после завершения выполнения политики hello</span><span class="sxs-lookup"><span data-stu-id="05c87-111">Information (which manifests as claims in a token) that hello application receives when hello policy run finishes</span></span>

<span data-ttu-id="05c87-112">В своем клиенте вы можете создать несколько политик различных типов и при необходимости использовать их в приложениях.</span><span class="sxs-lookup"><span data-stu-id="05c87-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="05c87-113">Политики могут повторно использоваться в разных приложениях.</span><span class="sxs-lookup"><span data-stu-id="05c87-113">Policies can be reused across applications.</span></span> <span data-ttu-id="05c87-114">Такая гибкость позволяет разработчикам toodefine и изменения функций удостоверений потребителей с минимальными или tootheir без изменения кода.</span><span class="sxs-lookup"><span data-stu-id="05c87-114">This flexibility enables developers toodefine and modify consumer identity experiences with minimal or no changes tootheir code.</span></span>

<span data-ttu-id="05c87-115">Работа с политиками выполняется через простой интерфейс разработчика.</span><span class="sxs-lookup"><span data-stu-id="05c87-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="05c87-116">Приложение запускает политику с помощью стандартных HTTP-запроса проверки подлинности (передача параметра политики в запросе hello) и получает маркер, настроенный как ответ.</span><span class="sxs-lookup"><span data-stu-id="05c87-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in hello request) and receives a customized token as response.</span></span> <span data-ttu-id="05c87-117">Например hello между запросов, которые вызывают политику регистрации и запросов, которые вызывают политику входа отличается только имя политики hello, используемый в параметр строки запроса «p» hello:</span><span class="sxs-lookup"><span data-stu-id="05c87-117">For example, hello only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is hello policy name that's used in hello "p" query string parameter:</span></span>

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

<span data-ttu-id="05c87-118">Дополнительные сведения о политике framework hello. в разделе [этой записи блога о Azure AD B2C на hello Enterprise Mobility и безопасности](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="05c87-118">For more information about hello policy framework, see [this blog post about Azure AD B2C on hello Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="05c87-119">Создание политики регистрации или входа в систему</span><span class="sxs-lookup"><span data-stu-id="05c87-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="05c87-120">Эта политика регулирует процедуры регистрации и входа в систему в рамках одной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="05c87-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="05c87-121">Потребители ведет работу hello верный путь (регистрации или входа) в зависимости от контекста hello.</span><span class="sxs-lookup"><span data-stu-id="05c87-121">Consumers are led down hello right path (sign-up or sign-in) depending on hello context.</span></span> <span data-ttu-id="05c87-122">Он также описывает содержимое hello токенов, которые будут получать приложения hello после успешной регистрацией или входа в систему.  Образец кода для регистрации или входа политики hello содержит [доступные здесь](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="05c87-122">It also describes hello contents of tokens that hello application will receive upon successful sign-ups or sign-ins.  A code sample for hello sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="05c87-123">Мы рекомендуем использовать эту политику вместо политики регистрации и политики входа в систему.</span><span class="sxs-lookup"><span data-stu-id="05c87-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="05c87-124">Создание политики регистрации</span><span class="sxs-lookup"><span data-stu-id="05c87-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="05c87-125">Создание политики входа в систему</span><span class="sxs-lookup"><span data-stu-id="05c87-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="05c87-126">Создание политики изменения профиля</span><span class="sxs-lookup"><span data-stu-id="05c87-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="05c87-127">Создание политики сброса паролей</span><span class="sxs-lookup"><span data-stu-id="05c87-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="05c87-128">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="05c87-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="05c87-129">Как связать политику регистрации или входа с политикой сброса паролей?</span><span class="sxs-lookup"><span data-stu-id="05c87-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="05c87-130">При создании политики регистрации или входа в систему (с локальных учетных записей), вы видите **забыли пароль?** ссылку на первой странице hello опыта hello.</span><span class="sxs-lookup"><span data-stu-id="05c87-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on hello first page of hello experience.</span></span> <span data-ttu-id="05c87-131">При переходе по этой ссылке политика сброса паролей не активируется автоматически.</span><span class="sxs-lookup"><span data-stu-id="05c87-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="05c87-132">Вместо этого Здравствуйте, код ошибки  **`AADB2C90118`**  возвращается tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="05c87-132">Instead, hello error code **`AADB2C90118`** is returned tooyour app.</span></span> <span data-ttu-id="05c87-133">Приложение должно toohandle этот код ошибки путем вызова политику сброса пароля.</span><span class="sxs-lookup"><span data-stu-id="05c87-133">Your app needs toohandle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="05c87-134">Дополнительные сведения см. в разделе [пример, демонстрирующий способ hello связывания политики](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="05c87-134">For more information, see a [sample that demonstrates hello approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="05c87-135">Следует ли использовать политику регистрации или входа либо две политики: политику регистрации и политику входа?</span><span class="sxs-lookup"><span data-stu-id="05c87-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="05c87-136">Мы рекомендуем использовать политику регистрации или входа вместо политики регистрации и политики входа.</span><span class="sxs-lookup"><span data-stu-id="05c87-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="05c87-137">политика регистрации или входа Hello имеет больше возможностей, чем hello вход политики.</span><span class="sxs-lookup"><span data-stu-id="05c87-137">hello sign-up or sign-in policy has more capabilities than hello sign-in policy.</span></span> <span data-ttu-id="05c87-138">Он также позволяет toouse Настройка пользовательского интерфейса страницы и обеспечивает улучшенную поддержку локализации.</span><span class="sxs-lookup"><span data-stu-id="05c87-138">It also enables you toouse page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="05c87-139">Рекомендуется Hello вход политику, если вам не требуется toolocalize политик, только требуются функции работы с минимальными изменениями для продвижения и пароль встроенных сброса.</span><span class="sxs-lookup"><span data-stu-id="05c87-139">hello sign-in policy is recommended if you don't need toolocalize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05c87-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05c87-140">Next steps</span></span>
* [<span data-ttu-id="05c87-141">Настройка токена, сеанса и единого входа</span><span class="sxs-lookup"><span data-stu-id="05c87-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="05c87-142">Azure Active Directory B2C: отключение проверки адреса электронной почты во время регистрации потребителя</span><span class="sxs-lookup"><span data-stu-id="05c87-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

