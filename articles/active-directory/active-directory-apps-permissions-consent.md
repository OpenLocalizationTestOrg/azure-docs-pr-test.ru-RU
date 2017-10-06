---
title: "Приложения, разрешения и согласие в Azure Active Directory | Документация Майкрософт"
description: "Azure AD Connect интегрирует локальные каталоги с Azure Active Directory. Это позволяет tooprovide общего удостоверения для приложений Office 365, Azure и SaaS интегрированы с Azure AD."
keywords: "Введение tooAzure AD, приложений, что такое Azure AD Connect установки active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="377bc-105">Приложения, разрешения и согласие в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="377bc-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="377bc-106">В Azure Active Directory можно добавить каталог tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="377bc-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="377bc-107">приложения Hello можно по-разному в зависимости от типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="377bc-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="377bc-108">tooview приложения hello классическом портале, выберите каталог и выберите приложения.</span><span class="sxs-lookup"><span data-stu-id="377bc-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="377bc-109">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="377bc-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="377bc-110">Типы приложений</span><span class="sxs-lookup"><span data-stu-id="377bc-110">Types of apps</span></span>

1. <span data-ttu-id="377bc-111">**Приложения с одним клиентом**</span><span class="sxs-lookup"><span data-stu-id="377bc-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="377bc-112">**Приложения одного клиента** -часто называют tooas бизнес (LOB) приложения.</span><span class="sxs-lookup"><span data-stu-id="377bc-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="377bc-113">Это hello случай, когда сотрудник вашей организации разрабатывает собственное приложение и хотите пользователей в hello организации toobe может toosign в приложении toohello.</span><span class="sxs-lookup"><span data-stu-id="377bc-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="377bc-114">**Прокси приложения приложения** — при предоставлении доступа к локальному приложению, с помощью прокси приложения Azure AD, регистрации приложения одного клиента в клиенте (в дополнение toohello прокси приложения-службы).</span><span class="sxs-lookup"><span data-stu-id="377bc-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="377bc-115">Это приложение представляет ваше локальное приложение для всех взаимодействий в облаке (например, для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="377bc-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="377bc-116">Прокси-сервер приложений требует Azure AD Basic или более поздних выпусков.</span><span class="sxs-lookup"><span data-stu-id="377bc-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="377bc-117">**Мультитенантные приложения**</span><span class="sxs-lookup"><span data-stu-id="377bc-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="377bc-118">**Мультитенантные которых другим пользователям можно разрешить** — аналогично слишком «приложения одного клиента, разрабатывает организации».</span><span class="sxs-lookup"><span data-stu-id="377bc-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="377bc-119">Основное различие Hello (помимо hello логику в само приложение hello) —, пользователи из других клиентов можно также согласия tooand входа в приложении toohello.</span><span class="sxs-lookup"><span data-stu-id="377bc-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="377bc-120">**Мультитенантные приложения других разработчиков, на использование которых может дать согласие Contoso.**</span><span class="sxs-lookup"><span data-stu-id="377bc-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="377bc-121">Для краткости их можно назвать приложениями с обеспечением согласия. Это сторона hello отразить «мультитенантные, разрабатывает организации».</span><span class="sxs-lookup"><span data-stu-id="377bc-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="377bc-122">Когда другой организации разрабатывает приложения несколькими клиентами, пользователи вашей организации можно согласия toohello приложения и войдите в tooit.</span><span class="sxs-lookup"><span data-stu-id="377bc-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="377bc-123">**Приложения Майкрософт, получающие данные напрямую из источника** — это приложения, которые представляют службы Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="377bc-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="377bc-124">Согласие определяется hello факт регистрации службе hello.</span><span class="sxs-lookup"><span data-stu-id="377bc-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="377bc-125">Это иногда специальные UX и логику для определенных приложений на основном, которая часто используется при создании политики вокруг приложения toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="377bc-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="377bc-126">**Предварительно интегрированных приложений** -приложения, доступные в коллекции приложений Azure AD, которое можно добавить hello tooyour directory tooprovide одного входа (и в некоторых случаях подготовки) toopopular приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="377bc-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="377bc-127">**Единый вход Azure AD** — "настоящий" единый вход для приложений, которые могут интегрироваться с Azure AD, по поддерживаемому протоколу входа, например SAML 2.0 или OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="377bc-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="377bc-128">Hello мастер поможет вам выполнить его настройка.</span><span class="sxs-lookup"><span data-stu-id="377bc-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="377bc-129">**Пароль единого входа**: Azure AD безопасно хранит hello учетные данные пользователя для приложения hello и hello учетные данные» вводится» в форму входа hello по hello расширение браузера для доступа к приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="377bc-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="377bc-130">Этот метод также известен как хранение пароля.</span><span class="sxs-lookup"><span data-stu-id="377bc-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="377bc-131">Разрешения</span><span class="sxs-lookup"><span data-stu-id="377bc-131">Permissions</span></span>

<span data-ttu-id="377bc-132">При регистрации приложения hello пользователя, выполняющего регистрации приложения hello (то есть разработчик hello) определяет, какое приложение hello разрешения не требуются и какие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="377bc-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="377bc-133">(hello ресурсы являются, сами по себе, определяется как другие приложения.) Например кто-то построение приложения для чтения почты, установил бы их приложению разрешение «Доступ к почтовым ящикам как пользователя, выполнившего вход hello» hello в hello «Office 365 Exchange Online» ресурсов:</span><span class="sxs-lookup"><span data-stu-id="377bc-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="377bc-134">В порядке для одного приложения (клиент hello) toorequest определенные разрешения из другого приложения (hello ресурс) developer Привет ресурсов приложения hello определяет hello разрешения, которые существуют.</span><span class="sxs-lookup"><span data-stu-id="377bc-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="377bc-135">В нашем примере Microsoft hello владельца ресурса приложение «Office 365 Exchange Online» hello определено разрешение с именем «Доступ к почтовым ящикам как пользователя, выполнившего вход hello».</span><span class="sxs-lookup"><span data-stu-id="377bc-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="377bc-136">При определении разрешений, разработчик приложения hello необходимо определить, если быть дано разрешение hello, или если требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="377bc-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="377bc-137">Таким образом, разработчики tooconsent tooallow пользователи на своих собственных tooapps запрашиваются только чувствительности низкого разрешения, однако требуются разрешения конфиденциальных toomore tooconsent "Администраторы".</span><span class="sxs-lookup"><span data-stu-id="377bc-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="377bc-138">Например, Здравствуйте, «Azure Active Directory» ресурсов приложения, определен, поэтому пользователи могут дать согласие tooapps, запрашиваются ограниченные разрешения только для чтения.</span><span class="sxs-lookup"><span data-stu-id="377bc-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="377bc-139">Однако для всех разрешений на чтение и запись требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="377bc-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="377bc-140">Так как собственные клиенты не проходят проверку подлинности, приложение, определенное в качестве собственного клиентского приложения, может запрашивать только делегированные разрешения.</span><span class="sxs-lookup"><span data-stu-id="377bc-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="377bc-141">Это означает, что при получении маркера всегда должен присутствовать реальный пользователь.</span><span class="sxs-lookup"><span data-stu-id="377bc-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="377bc-142">При получении маркера доступа веб-приложения и веб-API (конфиденциальные клиенты) должны всегда проходить проверку подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="377bc-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="377bc-143">То есть они также имеют возможность hello запрашиваются разрешения только для приложений.</span><span class="sxs-lookup"><span data-stu-id="377bc-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="377bc-144">Например, если одна служба внутреннего интерфейса должен tooauthenticate tooanother внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="377bc-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="377bc-145">Для приложений, запрашивающих разрешения только для приложения, всегда требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="377bc-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="377bc-146">Выводы:</span><span class="sxs-lookup"><span data-stu-id="377bc-146">Summarizing:</span></span>



- <span data-ttu-id="377bc-147">Приложение (клиент) состояний hello разрешения, которые необходимы для других приложений (ресурсы).</span><span class="sxs-lookup"><span data-stu-id="377bc-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="377bc-148">Приложение (ресурс) с сообщением о разрешениях, предоставляемых tooother приложений (клиентов).</span><span class="sxs-lookup"><span data-stu-id="377bc-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="377bc-149">Разрешение может быть разрешением только для приложения или делегированным разрешением.</span><span class="sxs-lookup"><span data-stu-id="377bc-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="377bc-150">Делегированное разрешение может быть отмечено как "Разрешает согласие пользователя" или "Требует согласия администратора".</span><span class="sxs-lookup"><span data-stu-id="377bc-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="377bc-151">Приложения могут вести себя как клиент (объявляя необходимые разрешения tooa ресурсов), как ресурс (объявляя разрешения, которые он предоставляет) или обоими способами.</span><span class="sxs-lookup"><span data-stu-id="377bc-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="377bc-152">Управление</span><span class="sxs-lookup"><span data-stu-id="377bc-152">Controls</span></span>

<span data-ttu-id="377bc-153">Hello ниже приведен список hello admin различных элементов управления, доступных для данного поведения.</span><span class="sxs-lookup"><span data-stu-id="377bc-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="377bc-154">Здравствуйте, администратор, элементы управления можно получить в классическом портале hello из настроить hello в каталоге.</span><span class="sxs-lookup"><span data-stu-id="377bc-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="377bc-155">В hello Azure портала в разделе **управления**, **параметры пользователя**.</span><span class="sxs-lookup"><span data-stu-id="377bc-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="377bc-156">Можно управлять, могут ли пользователи согласия tooapps:</span><span class="sxs-lookup"><span data-stu-id="377bc-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="377bc-157">В классическом портале hello, выберите **пользователи могут предоставлять разрешения tooaccess приложений свои данные.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="377bc-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="377bc-158">В hello портал Azure, выберите **пользователи разрешают приложениям tooaccess свои данные**.</span><span class="sxs-lookup"><span data-stu-id="377bc-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="377bc-159">Можно управлять ли пользователи могут зарегистрировать свои собственные бизнес-приложения одного клиента: В классическом портала выберите hello **пользователи могут добавлять интегрированные приложения.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="377bc-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="377bc-160">В hello портал Azure, выберите **пользователи разрешают приложениям tooaccess свои данные**.</span><span class="sxs-lookup"><span data-stu-id="377bc-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="377bc-161">Даже если пользователям разрешено tooregister одного клиента бизнес-приложений, существуют ограничения, toowhat могут быть зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="377bc-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="377bc-162">Например, в отношении разработчиков, которые не являются администраторами каталогов.</span><span class="sxs-lookup"><span data-stu-id="377bc-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="377bc-163">Пользователи не могут превратить приложение с одним клиентом в мультитенантное приложение.</span><span class="sxs-lookup"><span data-stu-id="377bc-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="377bc-164">При регистрации одного клиента бизнес-приложений, пользователи не могут запрашивать приложения tooother разрешения только для приложений.</span><span class="sxs-lookup"><span data-stu-id="377bc-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="377bc-165">При регистрации одного клиента бизнес-приложений, пользователи не могут запрашивать приложения tooother делегированных разрешений, если эти разрешения требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="377bc-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="377bc-166">Пользователи не могут вносить изменения tooapps, они не являются владельцами.</span><span class="sxs-lookup"><span data-stu-id="377bc-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="377bc-167">Вы можете указать, могут ли пользователи самостоятельно добавлять предварительно интегрированные приложения, применяющие единый вход с использованием пароля (хранение паролей). ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="377bc-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="377bc-168">Вы можете определять условия доступа к приложениям (условный доступ).</span><span class="sxs-lookup"><span data-stu-id="377bc-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="377bc-169">Имейте в виду, что применяется toohello клиентского приложения и toohello ресурсов приложения.</span><span class="sxs-lookup"><span data-stu-id="377bc-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="377bc-170">Таким образом Предположим, что задать политику условного доступа, о том, что приложение hello «Office 365 Exchange Online» может осуществляться только из машин, которые соответствуют требованиям.</span><span class="sxs-lookup"><span data-stu-id="377bc-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="377bc-171">Эта политика также включится при попытке toouse клиентского приложения, запрашивающий tooExchange разрешения в оперативный режим.</span><span class="sxs-lookup"><span data-stu-id="377bc-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="377bc-172">У вас есть видимости, в которой приложения были согласие tooand, какие из них используются.</span><span class="sxs-lookup"><span data-stu-id="377bc-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="377bc-173">При согласии пользователя приложение tooan, в клиенте hello создается объект субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="377bc-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="377bc-174">В отчет об аудите hello включено Создание субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="377bc-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="377bc-175">Отчеты действия при входе пользователя позволяют понять, какие приложения hello пользователей вход на.</span><span class="sxs-lookup"><span data-stu-id="377bc-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="377bc-176">Пример</span><span class="sxs-lookup"><span data-stu-id="377bc-176">Example</span></span>

<span data-ttu-id="377bc-177">Например рассмотрим приложение «FabrikamMail для Office 365» hello, которое вы заметили, что на вход пользователей в клиенте.</span><span class="sxs-lookup"><span data-stu-id="377bc-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="377bc-178">FabrikamMail — это приложение для чтения почты для Android, опубликованное компанией Fabrikam, Inc.</span><span class="sxs-lookup"><span data-stu-id="377bc-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="377bc-179">Это попадает hello» мультитенантные других разработка, которого может дать согласие Contoso».</span><span class="sxs-lookup"><span data-stu-id="377bc-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="377bc-180">Если пользователям разрешается tooconsent, они получают hello запрос согласия пользователя при первом входе в:![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="377bc-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="377bc-181">«Доступ к почтовых ящиков» строка hello пользовательского интерфейса согласия для разрешение «Доступ к почтовым ящикам как пользователя, выполнившего вход hello» hello, предоставляемые «Office 365 Exchange Online» (то есть Exchange).</span><span class="sxs-lookup"><span data-stu-id="377bc-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="377bc-182">Вы увидите разрешения hello, произведя поиск hello объекта субъекта-службы для Exchange (hello ресурса), которая была добавлена, если вы зарегистрировались в Office 365.</span><span class="sxs-lookup"><span data-stu-id="377bc-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="377bc-183">Можно представить hello объекта субъекта-службы «экземпляр» приложение hello в клиенте, который используется для записи различных параметров и конфигураций.</span><span class="sxs-lookup"><span data-stu-id="377bc-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="377bc-184">Это можно увидеть с помощью hello `Get-AzureADServicePrincipal` в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="377bc-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="377bc-185">Согласие инициируется в том случае, когда hello пользователь нажимает кнопку «Принять».</span><span class="sxs-lookup"><span data-stu-id="377bc-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="377bc-186">Во-первых в клиенте hello создается объект субъекта-службы для «FabrikamMail для Office 365».</span><span class="sxs-lookup"><span data-stu-id="377bc-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="377bc-187">Hello субъекта-службы выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="377bc-187">hello ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="377bc-188">Соглашаетесь tooan приложение создает Oauth2PermissionGrant связь между hello следующее:</span><span class="sxs-lookup"><span data-stu-id="377bc-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="377bc-189">Hello объекта пользователя</span><span class="sxs-lookup"><span data-stu-id="377bc-189">hello user object</span></span>
- <span data-ttu-id="377bc-190">клиентские приложения Hello ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="377bc-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="377bc-191">приложения Hello ресурсов ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="377bc-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="377bc-192">разрешения в приложение hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="377bc-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="377bc-193">В случае FabrikamMail hello выглядит примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="377bc-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="377bc-194">(**ClientId** — идентификатор основной объект службы FabrikamMail (hello, просто создавались) **PrincipalId** — hello объекта идентификатор пользователя (hello пользователя, согласие), **ResourceId**— служба Exchange идентификатор объекта-участника, область является разрешением hello в Exchange, которое было дано).</span><span class="sxs-lookup"><span data-stu-id="377bc-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="377bc-195">Если пользователям не разрешается tooconsent, он увидит экран, на котором говорится, что разрешение не требуется.</span><span class="sxs-lookup"><span data-stu-id="377bc-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

