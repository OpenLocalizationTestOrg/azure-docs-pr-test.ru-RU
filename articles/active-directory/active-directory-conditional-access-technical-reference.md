---
title: "aaaAzure Технический справочник по Active Directory условного доступа | Документы Microsoft"
description: "С помощью элемента управления условного доступа Azure Active Directory проверяет hello определенных условий, выбранное при проверке подлинности пользователя hello и перед предоставлением доступа toohello приложения. Если эти условия выполнены, hello пользователя с проверкой подлинности и доступа toohello приложение, которому разрешен."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="5dfa6-104">Техническая информация об условном доступе в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="5dfa6-105">Службы, включаемые с условным доступом</span><span class="sxs-lookup"><span data-stu-id="5dfa6-105">Services enabled with conditional access</span></span>

<span data-ttu-id="5dfa6-106">Правила условного доступа поддерживаются в самых разных типах приложений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="5dfa6-107">В этот список входят:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-107">This list includes:</span></span>


* <span data-ttu-id="5dfa6-108">Приложений, зарегистрированных с hello прокси приложения Azure</span><span class="sxs-lookup"><span data-stu-id="5dfa6-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="5dfa6-109">Удаленное приложение Azure</span><span class="sxs-lookup"><span data-stu-id="5dfa6-109">Azure Remote App</span></span>
* <span data-ttu-id="5dfa6-110">Линейка многопользовательских и бизнес-приложений, зарегистрированных в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5dfa6-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="5dfa6-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="5dfa6-111">Dynamics CRM</span></span>
* <span data-ttu-id="5dfa6-112">Федеративным приложениям из коллекции приложений Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="5dfa6-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="5dfa6-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="5dfa6-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="5dfa6-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="5dfa6-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="5dfa6-115">Microsoft Office 365 SharePoint Online (включая OneDrive для бизнеса)</span><span class="sxs-lookup"><span data-stu-id="5dfa6-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="5dfa6-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="5dfa6-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="5dfa6-117">Пароль приложения с единым ВХОДОМ из галереи приложения hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5dfa6-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="5dfa6-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="5dfa6-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="5dfa6-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5dfa6-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="5dfa6-120">Включить правила доступа</span><span class="sxs-lookup"><span data-stu-id="5dfa6-120">Enable access rules</span></span>
<span data-ttu-id="5dfa6-121">Каждое правило можно включать или отключать для каждого приложения отдельно.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="5dfa6-122">Если правила являются **ON** они будут включены и принудительно применяется для пользователей, обращающихся к приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="5dfa6-123">Во время **OFF** не будет использоваться и будет воздействия пользователей hello входа.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="5dfa6-124">Применение правил toospecific пользователей</span><span class="sxs-lookup"><span data-stu-id="5dfa6-124">Applying rules toospecific users</span></span>
<span data-ttu-id="5dfa6-125">Правила может быть применен toospecific групп пользователей, основанных на группе безопасности, задав **применить к**.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="5dfa6-126">**Применить к** можно задать слишком**всех пользователей** или **группы**.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="5dfa6-127">Если задано слишком**всех пользователей** hello и правила применяются tooany пользователя с приложением toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="5dfa6-128">Hello **группы** позволяет обеспечению безопасности и выборе toobe группы распространения правила будут применяться только для этих групп.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="5dfa6-129">При развертывании правила, чаще всего toofirst применить ограниченный набор пользователей, которые являются членами групп апробации.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="5dfa6-130">После завершения hello правило может быть применено слишком**всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="5dfa6-131">Это приведет к toobe применяется для всех пользователей в организации hello правило hello.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="5dfa6-132">Выберите группы также может быть исключен из политики с помощью hello **за исключением** параметр.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="5dfa6-133">Все члены этих групп будет исключены, даже если они входят в какую-либо включенную группу.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="5dfa6-134">Сети "на работе"</span><span class="sxs-lookup"><span data-stu-id="5dfa6-134">“At work” networks</span></span>
<span data-ttu-id="5dfa6-135">Правила условного доступа, используемые в сети «на работе», зависят от доверенных диапазоны IP-адресов, которые были настроены в Azure AD или использования hello «внутри корпоративной сети» утверждение от AD FS.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="5dfa6-136">В эти правила входит следующее:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-136">These rules include:</span></span>

* <span data-ttu-id="5dfa6-137">Требовать многофакторную проверку подлинности, если пользователь находится не на работе.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="5dfa6-138">Блокировать доступ, если пользователь находится не на работе.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-138">Block access when not at work</span></span>

<span data-ttu-id="5dfa6-139">Как указать сети "на работе"</span><span class="sxs-lookup"><span data-stu-id="5dfa6-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="5dfa6-140">Настройка надежных IP-адресов в hello [страницы конфигурации многофакторной проверки подлинности](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="5dfa6-141">Политики условного доступа будет использоваться диапазоны hello настроен на каждой проверки подлинности запроса и токен tooevaluate правил выдачи.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="5dfa6-142">Настроить использование hello внутри корпоративной сети утверждения, этот параметр может использоваться с федеративной каталоги, с помощью AD FS.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="5dfa6-143">toolearn Дополнительные сведения о hello внутри корпоративной сети утверждения, в разделе [Tusted IP-адреса](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="5dfa6-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="5dfa6-144">Правила, учитывающие уровень конфиденциальности приложений</span><span class="sxs-lookup"><span data-stu-id="5dfa6-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="5dfa6-145">Правила настраиваются для конкретных приложений, позволяя hello важных служб toobe защищенным без ущерба для доступа к службам tooother.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="5dfa6-146">Правила условного доступа можно настроить на hello **Настройка** вкладку приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="5dfa6-147">Далее указаны правила, предлагаемые в настоящее время:</span><span class="sxs-lookup"><span data-stu-id="5dfa6-147">Rules currently offered:</span></span>

* <span data-ttu-id="5dfa6-148">**Требовать многофакторную проверку подлинности**</span><span class="sxs-lookup"><span data-stu-id="5dfa6-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="5dfa6-149">Все пользователи, что она применяется toowill быть обязательным tooauthenticate через многофакторной проверки подлинности по крайней мере один раз.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="5dfa6-150">**Требовать многофакторную проверку подлинности, если пользователь находится не на работе.**</span><span class="sxs-lookup"><span data-stu-id="5dfa6-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="5dfa6-151">Если применяется эта политика, все пользователи будут использоваться необходимые toohave выполнена многофакторная проверка подлинности по крайней мере один раз их доступа к службе hello из удаленного расположения, не являющимися рабочими.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="5dfa6-152">При передаче из расположения tooremote работы, они будут tooperform требуется многофакторная проверка подлинности при доступе к службе hello.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="5dfa6-153">**Блокировать доступ, если пользователь находится не на работе.**</span><span class="sxs-lookup"><span data-stu-id="5dfa6-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="5dfa6-154">При перемещении из удаленного расположения tooa работы, они будут заблокированы, если hello «Блокировать доступ, если не на работе» политика применяется toothem.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="5dfa6-155">Оказавшись на рабочем месте, они вновь получат права на доступ.</span><span class="sxs-lookup"><span data-stu-id="5dfa6-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="5dfa6-156">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="5dfa6-156">Related topics</span></span>
* [<span data-ttu-id="5dfa6-157">Защита доступа tooOffice 365 и других приложений подключен tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5dfa6-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="5dfa6-158">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5dfa6-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

