---
title: "Приложения, разрешения и согласие в Azure Active Directory | Документация Майкрософт"
description: "Azure AD Connect интегрирует локальные каталоги с Azure Active Directory. Таким образом вы сможете предоставить пользователям возможность получать доступ с использованием одного удостоверения для Office 365, Azure и SaaS, интегрированных с Azure AD."
keywords: "введение в Azure AD, приложения, что такое Azure AD Connect, установка Аctive Directory"
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
ms.openlocfilehash: 6f6baf5e1538fb280a899065c64ca5688473c04a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="ae12d-105">Приложения, разрешения и согласие в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae12d-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="ae12d-106">В Azure Active Directory можно добавлять приложения в каталог.</span><span class="sxs-lookup"><span data-stu-id="ae12d-106">Within Azure Active Directory, you can add applications to your directory.</span></span>  <span data-ttu-id="ae12d-107">Приложения разделяются по типам задач.</span><span class="sxs-lookup"><span data-stu-id="ae12d-107">The applications can vary depending on the type of application.</span></span>  <span data-ttu-id="ae12d-108">Чтобы просмотреть приложения на классическом портале, выберите каталог и приложения.</span><span class="sxs-lookup"><span data-stu-id="ae12d-108">To view applications in the classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="ae12d-109">Для управления службой Azure AD мы рекомендуем использовать [Центр администрирования Azure AD](https://aad.portal.azure.com) на портале Azure, а не классический портал Azure, который упоминается в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ae12d-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="ae12d-110">Типы приложений</span><span class="sxs-lookup"><span data-stu-id="ae12d-110">Types of apps</span></span>

1. <span data-ttu-id="ae12d-111">**Приложения с одним клиентом**</span><span class="sxs-lookup"><span data-stu-id="ae12d-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="ae12d-112">**Приложения с одним клиентом** часто называются бизнес-приложениями.</span><span class="sxs-lookup"><span data-stu-id="ae12d-112">**Single-tenant apps** - Often referred to as line-of-business (LOB) apps.</span></span> <span data-ttu-id="ae12d-113">В этом случае сотрудник вашей организации разрабатывает свои приложения и хотел бы предоставить корпоративным пользователям возможность входа в это приложение.</span><span class="sxs-lookup"><span data-stu-id="ae12d-113">This is the case where someone within your organization develops their own app, and would like users in the organization to be able to sign in to the app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="ae12d-114">**Приложения прокси-сервера приложений.** После размещения локального приложения на прокси-сервере приложений Azure AD в вашем клиенте регистрируется приложение с одним клиентом (помимо службы прокси-сервера приложений).</span><span class="sxs-lookup"><span data-stu-id="ae12d-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition to the App Proxy service).</span></span> <span data-ttu-id="ae12d-115">Это приложение представляет ваше локальное приложение для всех взаимодействий в облаке (например, для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="ae12d-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="ae12d-116">Прокси-сервер приложений требует Azure AD Basic или более поздних выпусков.</span><span class="sxs-lookup"><span data-stu-id="ae12d-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="ae12d-117">**Мультитенантные приложения**</span><span class="sxs-lookup"><span data-stu-id="ae12d-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="ae12d-118">**Мультитенантные приложения, на использование которых можно дать согласие,** похожи на приложения с одним клиентом, разрабатываемые в организации.</span><span class="sxs-lookup"><span data-stu-id="ae12d-118">**Multi-tenant apps which others can consent to** - similar to “single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="ae12d-119">Основное различие (помимо логики приложения) заключается в том, что пользователи из других клиентов также могут дать согласие на их использование и войти в них.</span><span class="sxs-lookup"><span data-stu-id="ae12d-119">The main difference (besides the logic in the app itself) is that users from other tenants can also consent to and sign in to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="ae12d-120">**Мультитенантные приложения других разработчиков, на использование которых может дать согласие Contoso.**</span><span class="sxs-lookup"><span data-stu-id="ae12d-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="ae12d-121">Для краткости их можно назвать приложениями с обеспечением согласия. Эти приложения по сути противоположны мультитенантным приложениям, разрабатываемым в организации.</span><span class="sxs-lookup"><span data-stu-id="ae12d-121">(Or “consented apps”, for short.) This is the flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="ae12d-122">Если другая организация разрабатывает мультитенантное приложение, пользователи вашей организации могут предоставить согласие на его использование и войти в него.</span><span class="sxs-lookup"><span data-stu-id="ae12d-122">When another organization develops a multi-tenant app, users of your organization can consent to the app and sign in to it.</span></span>
    - <span data-ttu-id="ae12d-123">**Приложения Майкрософт, получающие данные напрямую из источника** — это приложения, которые представляют службы Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ae12d-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="ae12d-124">Согласие определяется тем, что вам необходимо пройти регистрацию для использования службы.</span><span class="sxs-lookup"><span data-stu-id="ae12d-124">Consent is driven by the fact that you sign up for the service.</span></span> <span data-ttu-id="ae12d-125">Иногда в определенных приложениях, получающих данные напрямую из источника, реализованы специальный интерфейс и логика, которые часто используются при создании политики доступа к приложению.</span><span class="sxs-lookup"><span data-stu-id="ae12d-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="ae12d-126">**Предварительно интегрированные приложения** — это приложения в коллекции приложений Azure AD, которые можно добавить в каталог для предоставления возможности единого входа (и в некоторых случаях подготовки) в популярных приложениях SaaS.</span><span class="sxs-lookup"><span data-stu-id="ae12d-126">**Pre-integrated apps** - Apps available in the Azure AD App Gallery, which you can add to your directory to provide single sign-on (and in some cases, provisioning) to popular SaaS apps.</span></span>
    - <span data-ttu-id="ae12d-127">**Единый вход Azure AD** — "настоящий" единый вход для приложений, которые могут интегрироваться с Azure AD, по поддерживаемому протоколу входа, например SAML 2.0 или OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="ae12d-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="ae12d-128">Мастер поможет настроить его.</span><span class="sxs-lookup"><span data-stu-id="ae12d-128">The wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="ae12d-129">**Единый вход с использованием пароля.** Azure AD безопасно хранит учетные данные пользователя для приложения, а расширение браузера для доступа к приложениям Azure AD позволяет вставить их в форму единого входа.</span><span class="sxs-lookup"><span data-stu-id="ae12d-129">**Password single sign-on**: Azure AD securely stores the user’s credentials for the app, and the credentials are “injected” into the sign-in form by the Azure AD App Access browser extension.</span></span> <span data-ttu-id="ae12d-130">Этот метод также известен как хранение пароля.</span><span class="sxs-lookup"><span data-stu-id="ae12d-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="ae12d-131">Разрешения</span><span class="sxs-lookup"><span data-stu-id="ae12d-131">Permissions</span></span>

<span data-ttu-id="ae12d-132">При регистрации приложения пользователь (разработчик) определяет разрешения и ресурсы, к которым приложению нужен доступ.</span><span class="sxs-lookup"><span data-stu-id="ae12d-132">When an app is registered, the user performing the app registration (that is, the developer) defines which permissions the app needs access to, and which resources.</span></span> <span data-ttu-id="ae12d-133">В качестве ресурсов выступают другие приложения. Например, разработчик приложения для чтения почты может заявить, что его приложению требуется разрешение на доступ к почтовым ящикам для пользователя, выполнившего вход, в ресурсе Office 365 Exchange Online:</span><span class="sxs-lookup"><span data-stu-id="ae12d-133">(The resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires the “Access mailboxes as the signed-in user” permission in the “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="ae12d-134">Чтобы одно приложение (клиент) могло запросить определенные разрешения у другого приложения (ресурс), разработчик приложения-ресурса определяет существующие разрешения.</span><span class="sxs-lookup"><span data-stu-id="ae12d-134">In order for one app (the client) to request a certain permission from another app (the resource), the developer of the resource app defines the permissions that exist.</span></span> <span data-ttu-id="ae12d-135">В нашем примере корпорация Майкрософт, владелец приложения-ресурса Office 365 Exchange Online, определила разрешение с именем "Доступ к почтовым ящикам для пользователя, выполнившего вход".</span><span class="sxs-lookup"><span data-stu-id="ae12d-135">In our example, Microsoft, the owner of the “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as the signed-in user”.</span></span>

<span data-ttu-id="ae12d-136">При определении разрешений разработчику приложений необходимо указать, можно ли дать согласие на использование разрешения или же требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="ae12d-136">When defining permissions, the app developer must define if the permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="ae12d-137">Таким образом разработчики могут разрешить пользователям самостоятельно давать согласие на использование приложений, запрашивающих разрешения низкого уровня. При этом согласие на использование приложений с разрешениями высокого уровня может дать только администратор.</span><span class="sxs-lookup"><span data-stu-id="ae12d-137">This allows developers to allow users to consent on their own to apps requesting only low-sensitivity permissions, but require admins to consent to more sensitive permissions.</span></span> <span data-ttu-id="ae12d-138">Например, в приложении-ресурсе Azure Active Directory определено, что пользователи могут дать согласие на использование приложений, запрашивающих ограниченные разрешения только для чтения.</span><span class="sxs-lookup"><span data-stu-id="ae12d-138">For example, the “Azure Active Directory” resource app, has been defined, so users can consent to apps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="ae12d-139">Однако для всех разрешений на чтение и запись требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="ae12d-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="ae12d-140">Так как собственные клиенты не проходят проверку подлинности, приложение, определенное в качестве собственного клиентского приложения, может запрашивать только делегированные разрешения.</span><span class="sxs-lookup"><span data-stu-id="ae12d-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="ae12d-141">Это означает, что при получении маркера всегда должен присутствовать реальный пользователь.</span><span class="sxs-lookup"><span data-stu-id="ae12d-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="ae12d-142">При получении маркера доступа веб-приложения и веб-API (конфиденциальные клиенты) должны всегда проходить проверку подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae12d-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="ae12d-143">То есть у них также есть возможность запрашивать разрешения только для приложения.</span><span class="sxs-lookup"><span data-stu-id="ae12d-143">Meaning they also have the possibility of requesting app-only permissions.</span></span> <span data-ttu-id="ae12d-144">Например, если одной серверной службе требуется пройти проверку подлинности в другой серверной службе.</span><span class="sxs-lookup"><span data-stu-id="ae12d-144">For example, if one back-end service needs to authenticate to another back-end service.</span></span> <span data-ttu-id="ae12d-145">Для приложений, запрашивающих разрешения только для приложения, всегда требуется согласие администратора.</span><span class="sxs-lookup"><span data-stu-id="ae12d-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="ae12d-146">Выводы:</span><span class="sxs-lookup"><span data-stu-id="ae12d-146">Summarizing:</span></span>



- <span data-ttu-id="ae12d-147">Приложение (клиент) сообщает о разрешениях, необходимых для других приложений (ресурсы).</span><span class="sxs-lookup"><span data-stu-id="ae12d-147">An app (client) states the permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="ae12d-148">Приложение (ресурс) сообщает, какие разрешения предоставляются другим приложениям (клиенты).</span><span class="sxs-lookup"><span data-stu-id="ae12d-148">An app (resource) states what permissions are exposed to other apps (clients).</span></span>
- <span data-ttu-id="ae12d-149">Разрешение может быть разрешением только для приложения или делегированным разрешением.</span><span class="sxs-lookup"><span data-stu-id="ae12d-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="ae12d-150">Делегированное разрешение может быть отмечено как "Разрешает согласие пользователя" или "Требует согласия администратора".</span><span class="sxs-lookup"><span data-stu-id="ae12d-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="ae12d-151">Приложение может выступать в качестве клиента (объявляя о том, что ему нужны разрешения на ресурс), ресурса (объявляя о предоставляемых разрешениях) или выполнять обе роли.</span><span class="sxs-lookup"><span data-stu-id="ae12d-151">An app can behave as a client (by declaring that it needs permissions to a resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="ae12d-152">Управление</span><span class="sxs-lookup"><span data-stu-id="ae12d-152">Controls</span></span>

<span data-ttu-id="ae12d-153">Ниже приведен список элементов управления администратора для всех указанных выше ситуаций.</span><span class="sxs-lookup"><span data-stu-id="ae12d-153">The following is a list of the different admin controls available for all this behavior.</span></span> <span data-ttu-id="ae12d-154">К элементам управления администратора можно получить доступ на классическом портале, щелкнув "Настроить" в каталоге.</span><span class="sxs-lookup"><span data-stu-id="ae12d-154">The admin controls can be accessed in the classic portal from configure under the directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="ae12d-155">На портале Azure — в разделе **Управление** и **Настройки пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ae12d-155">In the Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="ae12d-156">Вы можете указать, могут ли пользователи дать согласие на использование приложений:</span><span class="sxs-lookup"><span data-stu-id="ae12d-156">You can control whether users can consent to apps:</span></span>

<span data-ttu-id="ae12d-157">На классическом портале выберите **Users may give applications permissions to access their data** (Пользователи могут предоставлять приложениям разрешение на доступ к данным).
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="ae12d-157">In the classic portal, select **Users may give applications permissions to access their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="ae12d-158">На портале Azure выберите **Users can allow apps to access their data** (Пользователи могут предоставлять приложениям разрешение на доступ к данным).</span><span class="sxs-lookup"><span data-stu-id="ae12d-158">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="ae12d-159">Вы можете управлять возможностью пользователей регистрировать собственные бизнес-приложения с одним клиентом. На классическом портале выберите **Пользователи могут добавлять интегрированные приложения.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="ae12d-159">You can control whether users can register their own single-tenant LOB apps: In the classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="ae12d-160">На портале Azure выберите **Users can allow apps to access their data** (Пользователи могут предоставлять приложениям разрешение на доступ к данным).</span><span class="sxs-lookup"><span data-stu-id="ae12d-160">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="ae12d-161">Даже если разрешить пользователям регистрировать бизнес-приложения с одним клиентом, существуют определенные ограничения относительно того, что можно зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="ae12d-161">Even if you do allow users to register single-tenant LOB apps, there are limits to what can be registered.</span></span>  
><span data-ttu-id="ae12d-162">Например, в отношении разработчиков, которые не являются администраторами каталогов.</span><span class="sxs-lookup"><span data-stu-id="ae12d-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="ae12d-163">Пользователи не могут превратить приложение с одним клиентом в мультитенантное приложение.</span><span class="sxs-lookup"><span data-stu-id="ae12d-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="ae12d-164">При регистрации бизнес-приложений с одним клиентом пользователи не могут запрашивать разрешения только для приложений для других приложений.</span><span class="sxs-lookup"><span data-stu-id="ae12d-164">When registering single-tenant LOB apps, users cannot request app-only permissions to other apps.</span></span>
>- <span data-ttu-id="ae12d-165">При регистрации бизнес-приложений с одним клиентом пользователи не могут запрашивать делегированные разрешения для других приложений, если эти разрешения требуют согласия администратора.</span><span class="sxs-lookup"><span data-stu-id="ae12d-165">When registering single-tenant LOB apps, users cannot request delegated permissions to other apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="ae12d-166">Пользователи не могут вносить изменения в приложения, которые им не принадлежат.</span><span class="sxs-lookup"><span data-stu-id="ae12d-166">Users cannot make changes to apps that they are not owners of.</span></span>



- <span data-ttu-id="ae12d-167">Вы можете указать, могут ли пользователи самостоятельно добавлять предварительно интегрированные приложения, применяющие единый вход с использованием пароля (хранение паролей). ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="ae12d-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="ae12d-168">Вы можете определять условия доступа к приложениям (условный доступ).</span><span class="sxs-lookup"><span data-stu-id="ae12d-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="ae12d-169">Имейте в виду, что это касается как приложений-клиентов, так и приложений-ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ae12d-169">Be aware this applies both to the client app and to the resource app.</span></span> <span data-ttu-id="ae12d-170">Предположим, что вы установили политику условного доступа, в соответствии с которой к приложению Office 365 Exchange Online можно получить доступ только с совместимых компьютеров.</span><span class="sxs-lookup"><span data-stu-id="ae12d-170">So, say you set a conditional access policy that says that the “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="ae12d-171">Эта политика также активируется при попытке использовать клиентское приложение, запрашивающее разрешения для Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="ae12d-171">This policy will also kick in when a user attempts to use a client app which requests permissions to Exchange Online.</span></span>



- <span data-ttu-id="ae12d-172">Вы видите приложения, на использование которых предоставлено согласие, а также используемые приложения.</span><span class="sxs-lookup"><span data-stu-id="ae12d-172">You have visibility into which apps have been consented to and which ones are being used.</span></span>

1.  <span data-ttu-id="ae12d-173">Когда пользователь предоставляет согласие для приложения, в клиенте создается объект ServicePrincipal.</span><span class="sxs-lookup"><span data-stu-id="ae12d-173">When a user consents to an app, a ServicePrincipal object is created in the tenant.</span></span> <span data-ttu-id="ae12d-174">Это событие включается в отчет по аудиту.</span><span class="sxs-lookup"><span data-stu-id="ae12d-174">ServicePrincipal creation is included in the audit report.</span></span>
2.  <span data-ttu-id="ae12d-175">В соответствии со сведениями отчетов по действиям входа можно определить приложение, в которое входит пользователь.</span><span class="sxs-lookup"><span data-stu-id="ae12d-175">User sign-in activity reports tell you which app the user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="ae12d-176">Пример</span><span class="sxs-lookup"><span data-stu-id="ae12d-176">Example</span></span>

<span data-ttu-id="ae12d-177">Например, рассмотрим приложение FabrikamMail для Office 365. Вы обнаружили, что пользователи в клиенте входят в него.</span><span class="sxs-lookup"><span data-stu-id="ae12d-177">As an example, let’s take the “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="ae12d-178">FabrikamMail — это приложение для чтения почты для Android, опубликованное компанией Fabrikam, Inc.</span><span class="sxs-lookup"><span data-stu-id="ae12d-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="ae12d-179">Оно попадает в группу "Мультитенантные приложения других разработчиков, на использование которых может дать согласие Contoso".</span><span class="sxs-lookup"><span data-stu-id="ae12d-179">This falls into the “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="ae12d-180">Если пользователям разрешено давать согласие, при первом входе для них отобразится запрос на согласие: ![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="ae12d-180">If users are allowed to consent, they get a consent prompt the first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="ae12d-181">"Доступ к почтовым ящикам" — это строка согласия пользователя для разрешения "Доступ к почтовым ящикам для пользователя, выполнившего вход", предоставляемого приложением Office 365 Exchange Online (то есть Exchange).</span><span class="sxs-lookup"><span data-stu-id="ae12d-181">“Access your mailboxes” is the user-facing consent string for the “Access mailboxes as the signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="ae12d-182">Разрешения можно увидеть, посмотрев объект ServicePrincipal для Exchange (ресурс), добавленный при регистрации в Office 365.</span><span class="sxs-lookup"><span data-stu-id="ae12d-182">You can see the permissions by looking up the ServicePrincipal object for Exchange (the resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="ae12d-183">Объект ServicePrincipal можно рассматривать как экземпляр приложения в клиенте, используемый для записи различных параметров и конфигураций.</span><span class="sxs-lookup"><span data-stu-id="ae12d-183">You can think of the ServicePrincipal object of an “instance” of the app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="ae12d-184">Его можно увидеть, используя `Get-AzureADServicePrincipal` в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae12d-184">You can see this by using the `Get-AzureADServicePrincipal` in PowerShell.</span></span>

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
                                  AdminConsentDescription : Allows the app to have the same access to mailboxes as the signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as the signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows the app full access to your mailboxes on your behalf.
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

<span data-ttu-id="ae12d-185">Согласие предоставляется, когда пользователь нажимает кнопку "Принять".</span><span class="sxs-lookup"><span data-stu-id="ae12d-185">Consent is initiated when the user clicks “Accept”.</span></span> <span data-ttu-id="ae12d-186">Сначала в клиенте создается объект ServicePrincipal для приложения FabrikamMail для Office 365.</span><span class="sxs-lookup"><span data-stu-id="ae12d-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in the tenant.</span></span> <span data-ttu-id="ae12d-187">ServicePrincipal выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ae12d-187">The ServicePrincipal looks something like this:</span></span>

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

<span data-ttu-id="ae12d-188">При предоставлении согласия на использование приложения создается связь Oauth2PermissionGrant между следующими компонентами:</span><span class="sxs-lookup"><span data-stu-id="ae12d-188">Consenting to an app creates an Oauth2PermissionGrant link between the following:</span></span>
  
- <span data-ttu-id="ae12d-189">объект пользователя;</span><span class="sxs-lookup"><span data-stu-id="ae12d-189">the user object</span></span>
- <span data-ttu-id="ae12d-190">ServicePrincipalName (SPN) приложений-клиентов;</span><span class="sxs-lookup"><span data-stu-id="ae12d-190">the client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="ae12d-191">ServicePrincipalName (SPN) приложений-ресурсов;</span><span class="sxs-lookup"><span data-stu-id="ae12d-191">the resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="ae12d-192">разрешения в приложении-ресурсе.</span><span class="sxs-lookup"><span data-stu-id="ae12d-192">permissions in the resource app.</span></span>  

<span data-ttu-id="ae12d-193">В случае с FabrikamMail это выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="ae12d-193">In the case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="ae12d-194">**ClientId** — это созданный идентификатор объекта ServicePrincipal приложения FabrikamMail, **PrincipalId** — идентификатор объекта пользователя, давшего согласие, **ResourceId** — идентификатор объекта ServicePrincipal приложения Exchange, а Scope — это разрешение в Exchange, на использование которого предоставлено согласие.</span><span class="sxs-lookup"><span data-stu-id="ae12d-194">(**ClientId** is FabrikamMail’s service principal object ID (the one that just got created), **PrincipalId** is the user object ID (of the user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is the permission in Exchange that was consented to).</span></span>

<span data-ttu-id="ae12d-195">Если пользователям запрещено давать согласие, они увидят экран с сообщением о том, что требуется разрешение.</span><span class="sxs-lookup"><span data-stu-id="ae12d-195">If users are not allowed to consent, they will see a screen that says that permission is required.</span></span>

