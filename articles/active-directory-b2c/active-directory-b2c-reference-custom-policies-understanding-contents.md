---
title: "Azure Active Directory B2C: Основные сведения о настраиваемых политик пакет начального приветствия | Документы Microsoft"
description: "В этой статье описываются пользовательские политики Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="e73dc-103">Основные сведения о настраиваемых политик hello пакета начального hello Azure AD B2C настраиваемой политики</span><span class="sxs-lookup"><span data-stu-id="e73dc-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="e73dc-104">В этом разделе перечислены все ключевые элементы hello hello B2C_1A_base политики, входящий в состав hello **пакет начального** и который используется для создания собственных политик через наследование hello hello *B2C_1A_base_ расширения политики*.</span><span class="sxs-lookup"><span data-stu-id="e73dc-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="e73dc-105">Таким образом он более особенно посвящено hello уже определен утверждения типы, преобразования утверждений, определения содержимого, поставщиками утверждений с их профилями технические и hello поездок основных пользователей.</span><span class="sxs-lookup"><span data-stu-id="e73dc-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e73dc-106">Корпорация Майкрософт не дает каких-либо гарантий, явных или подразумеваемых, относительно toohello сведения, предоставленные здесь и далее.</span><span class="sxs-lookup"><span data-stu-id="e73dc-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="e73dc-107">Изменения могут быть внесены в любое время: до, во время или после выпуска общедоступной версии.</span><span class="sxs-lookup"><span data-stu-id="e73dc-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="e73dc-108">Hello B2C_1A_base_extensions политики и собственные политики можно переопределить эти определения и распространить действие этой политики родительского, предоставляя дополнительные шаблоны, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e73dc-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="e73dc-109">Здравствуйте, ключевые элементы hello *B2C_1A_base политики* : типы утверждений, преобразования утверждений и определения содержимого.</span><span class="sxs-lookup"><span data-stu-id="e73dc-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="e73dc-110">Эти элементы можно подвержены toobe, на которые ссылается собственные политики, а также как hello *B2C_1A_base_extensions политики*.</span><span class="sxs-lookup"><span data-stu-id="e73dc-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="e73dc-111">Схемы утверждений</span><span class="sxs-lookup"><span data-stu-id="e73dc-111">Claims schemas</span></span>

<span data-ttu-id="e73dc-112">Схемы утверждений состоят из трех разделов:</span><span class="sxs-lookup"><span data-stu-id="e73dc-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="e73dc-113">Первый раздел, в котором перечислены hello минимальное утверждения, которые необходимы для hello пользователя поездок toowork должным образом.</span><span class="sxs-lookup"><span data-stu-id="e73dc-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="e73dc-114">Второй раздел, что списки hello утверждениями, необходимыми для параметров строки запроса и другие специальные параметры toobe передан tooother поставщиков утверждений, особенно login.microsoftonline.com для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e73dc-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="e73dc-115">**Не изменяйте эти утверждения**.</span><span class="sxs-lookup"><span data-stu-id="e73dc-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="e73dc-116">В результате и третий раздел, в котором перечислены дополнительные утверждения, которые могут быть собраны от пользователя hello, хранятся в каталоге hello отправляются в токенах во время входа в.</span><span class="sxs-lookup"><span data-stu-id="e73dc-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="e73dc-117">В этом разделе можно добавить новые утверждения типа toobe полученные от пользователя hello и/или отправки в маркере hello.</span><span class="sxs-lookup"><span data-stu-id="e73dc-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e73dc-118">Схема утверждений Hello содержит ограничения на определенных утверждений, например пароли и имена пользователей.</span><span class="sxs-lookup"><span data-stu-id="e73dc-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="e73dc-119">Hello политики доверия Framework (TF) рассматривает Azure AD как любой другой поставщик утверждений и все ограничения modelled в политике premium hello.</span><span class="sxs-lookup"><span data-stu-id="e73dc-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="e73dc-120">Политика может быть измененный tooadd дополнительные ограничения или использовать другого поставщика утверждений для хранения учетных данных, который будет иметь свои собственные ограничения.</span><span class="sxs-lookup"><span data-stu-id="e73dc-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="e73dc-121">Ниже перечислены типы доступных утверждений Hello.</span><span class="sxs-lookup"><span data-stu-id="e73dc-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="e73dc-122">Утверждения, которые требуются для поездок пользователя hello</span><span class="sxs-lookup"><span data-stu-id="e73dc-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="e73dc-123">После утверждения Hello требуются toowork поездок пользователя должным образом.</span><span class="sxs-lookup"><span data-stu-id="e73dc-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="e73dc-124">Тип утверждения</span><span class="sxs-lookup"><span data-stu-id="e73dc-124">Claims type</span></span> | <span data-ttu-id="e73dc-125">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="e73dc-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-126">*UserId*</span></span> | <span data-ttu-id="e73dc-127">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="e73dc-127">Username</span></span> |
| <span data-ttu-id="e73dc-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="e73dc-128">*signInName*</span></span> | <span data-ttu-id="e73dc-129">Имя входа</span><span class="sxs-lookup"><span data-stu-id="e73dc-129">Sign in name</span></span> |
| <span data-ttu-id="e73dc-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-130">*tenantId*</span></span> | <span data-ttu-id="e73dc-131">Идентификатор клиента (ID) hello объекта-пользователя в Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="e73dc-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="e73dc-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-132">*objectId*</span></span> | <span data-ttu-id="e73dc-133">Идентификатор объекта (ID) hello объекта пользователя в Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="e73dc-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="e73dc-134">*password*</span><span class="sxs-lookup"><span data-stu-id="e73dc-134">*password*</span></span> | <span data-ttu-id="e73dc-135">Пароль</span><span class="sxs-lookup"><span data-stu-id="e73dc-135">Password</span></span> |
| <span data-ttu-id="e73dc-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="e73dc-136">*newPassword*</span></span> | |
| <span data-ttu-id="e73dc-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="e73dc-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="e73dc-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="e73dc-138">*passwordPolicies*</span></span> | <span data-ttu-id="e73dc-139">Политики паролей, используемых стойкость пароля Azure AD B2C Premium toodetermine, срока действия и т. д.</span><span class="sxs-lookup"><span data-stu-id="e73dc-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="e73dc-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="e73dc-140">*sub*</span></span> | |
| <span data-ttu-id="e73dc-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="e73dc-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="e73dc-142">*identityProvider*</span></span> | |
| <span data-ttu-id="e73dc-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="e73dc-143">*displayName*</span></span> | |
| <span data-ttu-id="e73dc-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="e73dc-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="e73dc-145">Номер телефона пользователя</span><span class="sxs-lookup"><span data-stu-id="e73dc-145">User's telephone number</span></span> |
| <span data-ttu-id="e73dc-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="e73dc-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="e73dc-147">*email*</span><span class="sxs-lookup"><span data-stu-id="e73dc-147">*email*</span></span> | <span data-ttu-id="e73dc-148">Адрес электронной почты, может быть пользователя используется toocontact hello</span><span class="sxs-lookup"><span data-stu-id="e73dc-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="e73dc-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="e73dc-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="e73dc-150">Адрес электронной почты, hello пользователя можно использовать toosign в</span><span class="sxs-lookup"><span data-stu-id="e73dc-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="e73dc-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="e73dc-151">*otherMails*</span></span> | <span data-ttu-id="e73dc-152">Адреса электронной почты, которые могут быть пользователя используется toocontact hello</span><span class="sxs-lookup"><span data-stu-id="e73dc-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="e73dc-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="e73dc-153">*userPrincipalName*</span></span> | <span data-ttu-id="e73dc-154">Имя пользователя, сохраненного в Azure AD B2C Premium hello</span><span class="sxs-lookup"><span data-stu-id="e73dc-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="e73dc-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="e73dc-155">*upnUserName*</span></span> | <span data-ttu-id="e73dc-156">Имя пользователя для создания имени субъекта-пользователя</span><span class="sxs-lookup"><span data-stu-id="e73dc-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="e73dc-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="e73dc-157">*mailNickName*</span></span> | <span data-ttu-id="e73dc-158">Имя ник почты пользователя, сохраненного в Azure AD B2C Premium hello</span><span class="sxs-lookup"><span data-stu-id="e73dc-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="e73dc-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="e73dc-159">*newUser*</span></span> | |
| <span data-ttu-id="e73dc-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="e73dc-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="e73dc-161">Утверждения с указанием ли атрибуты, собранные от пользователя hello</span><span class="sxs-lookup"><span data-stu-id="e73dc-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="e73dc-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="e73dc-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="e73dc-163">Утверждения с указанием, собираются ли новый номер телефона пользователя hello</span><span class="sxs-lookup"><span data-stu-id="e73dc-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="e73dc-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="e73dc-164">*authenticationSource*</span></span> | <span data-ttu-id="e73dc-165">Указывает, была ли проверка подлинности пользователя hello в социальных поставщика удостоверений, login.microsoftonline.com или локальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="e73dc-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="e73dc-166">Утверждения, необходимые для параметров строки запроса и других особых параметров</span><span class="sxs-lookup"><span data-stu-id="e73dc-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="e73dc-167">Hello следующие утверждения — это обязательный toopass на поставщиков утверждений tooother специальных параметров (включая некоторые параметры строки запроса):</span><span class="sxs-lookup"><span data-stu-id="e73dc-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="e73dc-168">Тип утверждения</span><span class="sxs-lookup"><span data-stu-id="e73dc-168">Claims type</span></span> | <span data-ttu-id="e73dc-169">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="e73dc-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="e73dc-170">*nux*</span></span> | <span data-ttu-id="e73dc-171">Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e73dc-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="e73dc-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="e73dc-172">*nca*</span></span> | <span data-ttu-id="e73dc-173">Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e73dc-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="e73dc-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="e73dc-174">*prompt*</span></span> | <span data-ttu-id="e73dc-175">Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e73dc-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="e73dc-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="e73dc-176">*mkt*</span></span> | <span data-ttu-id="e73dc-177">Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e73dc-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="e73dc-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="e73dc-178">*lc*</span></span> | <span data-ttu-id="e73dc-179">Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e73dc-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="e73dc-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="e73dc-180">*grant_type*</span></span> | <span data-ttu-id="e73dc-181">Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e73dc-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="e73dc-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="e73dc-182">*scope*</span></span> | <span data-ttu-id="e73dc-183">Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e73dc-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="e73dc-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="e73dc-184">*client_id*</span></span> | <span data-ttu-id="e73dc-185">Переданный для локальной учетной записи проверки подлинности toologin.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e73dc-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="e73dc-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="e73dc-186">*objectIdFromSession*</span></span> | <span data-ttu-id="e73dc-187">Параметр, предоставляемые hello по умолчанию сеанса управления поставщика tooindicate, hello объекта с идентификатором были получены из сеанса единого входа</span><span class="sxs-lookup"><span data-stu-id="e73dc-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="e73dc-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="e73dc-188">*isActiveMFASession*</span></span> | <span data-ttu-id="e73dc-189">Параметр с hello многофакторной проверки Подлинности сеанса управления tooindicate при условии, что этот пользователь hello имеет активный сеанс многофакторной проверки Подлинности</span><span class="sxs-lookup"><span data-stu-id="e73dc-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="e73dc-190">Дополнительные (необязательные) утверждения для сбора</span><span class="sxs-lookup"><span data-stu-id="e73dc-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="e73dc-191">Hello следующих утверждений дополнительные утверждения, которые могут быть собраны от пользователей hello, хранятся в каталоге hello и отправляются в маркере hello.</span><span class="sxs-lookup"><span data-stu-id="e73dc-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="e73dc-192">Как описано перед дополнительные утверждения можно добавить список toothis.</span><span class="sxs-lookup"><span data-stu-id="e73dc-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="e73dc-193">Тип утверждения</span><span class="sxs-lookup"><span data-stu-id="e73dc-193">Claims type</span></span> | <span data-ttu-id="e73dc-194">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="e73dc-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="e73dc-195">*givenName*</span></span> | <span data-ttu-id="e73dc-196">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="e73dc-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="e73dc-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="e73dc-197">*surname*</span></span> | <span data-ttu-id="e73dc-198">Фамилия пользователя</span><span class="sxs-lookup"><span data-stu-id="e73dc-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="e73dc-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="e73dc-199">*Extension_picture*</span></span> | <span data-ttu-id="e73dc-200">Фотография пользователя из социальных сетей</span><span class="sxs-lookup"><span data-stu-id="e73dc-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="e73dc-201">Преобразования утверждения</span><span class="sxs-lookup"><span data-stu-id="e73dc-201">Claim transformations</span></span>

<span data-ttu-id="e73dc-202">Ниже перечислены преобразования доступных утверждений Hello.</span><span class="sxs-lookup"><span data-stu-id="e73dc-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="e73dc-203">Преобразования утверждения</span><span class="sxs-lookup"><span data-stu-id="e73dc-203">Claim transformation</span></span> | <span data-ttu-id="e73dc-204">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="e73dc-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="e73dc-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="e73dc-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="e73dc-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="e73dc-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="e73dc-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="e73dc-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="e73dc-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="e73dc-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="e73dc-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="e73dc-211">Определения содержимого</span><span class="sxs-lookup"><span data-stu-id="e73dc-211">Content definitions</span></span>

<span data-ttu-id="e73dc-212">В этом разделе описываются определения hello содержимого, уже объявлен в hello *B2C_1A_base* политики.</span><span class="sxs-lookup"><span data-stu-id="e73dc-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="e73dc-213">Эти определения содержимого будут подвержены toobe ссылка, переопределения и/или расширено по мере необходимости в собственные политики, а также как hello *B2C_1A_base_extensions* политики.</span><span class="sxs-lookup"><span data-stu-id="e73dc-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="e73dc-214">Поставщик утверждений</span><span class="sxs-lookup"><span data-stu-id="e73dc-214">Claims provider</span></span> | <span data-ttu-id="e73dc-215">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="e73dc-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="e73dc-216">*Facebook*</span></span> | |
| <span data-ttu-id="e73dc-217">*Вход с использованием локальной учетной записи*</span><span class="sxs-lookup"><span data-stu-id="e73dc-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="e73dc-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="e73dc-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="e73dc-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="e73dc-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="e73dc-220">*Самоподтверждение*</span><span class="sxs-lookup"><span data-stu-id="e73dc-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="e73dc-221">*Локальная учетная запись*</span><span class="sxs-lookup"><span data-stu-id="e73dc-221">*Local Account*</span></span> | |
| <span data-ttu-id="e73dc-222">*Управление сеансами*</span><span class="sxs-lookup"><span data-stu-id="e73dc-222">*Session Management*</span></span> | |
| <span data-ttu-id="e73dc-223">*Подсистема политик инфраструктуры доверия*</span><span class="sxs-lookup"><span data-stu-id="e73dc-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="e73dc-224">*Технические профили*</span><span class="sxs-lookup"><span data-stu-id="e73dc-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="e73dc-225">*Поставщик токенов*</span><span class="sxs-lookup"><span data-stu-id="e73dc-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="e73dc-226">Технические профили</span><span class="sxs-lookup"><span data-stu-id="e73dc-226">Technical profiles</span></span>

<span data-ttu-id="e73dc-227">В этом разделе описывается технические профили hello уже объявлен каждого поставщика утверждений в hello *B2C_1A_base* политики.</span><span class="sxs-lookup"><span data-stu-id="e73dc-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="e73dc-228">Эти технические профили будут подвержены toobe Дополнительные ссылки, переопределении или расширено по мере необходимости в собственные политики, а также как hello *B2C_1A_base_extensions* политики.</span><span class="sxs-lookup"><span data-stu-id="e73dc-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="e73dc-229">Технические профили для Facebook</span><span class="sxs-lookup"><span data-stu-id="e73dc-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="e73dc-230">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="e73dc-230">Technical profile</span></span> | <span data-ttu-id="e73dc-231">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="e73dc-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="e73dc-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="e73dc-233">Технические профили для входа с использованием локальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="e73dc-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="e73dc-234">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="e73dc-234">Technical profile</span></span> | <span data-ttu-id="e73dc-235">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="e73dc-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="e73dc-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="e73dc-237">Технические профили для PhoneFactor</span><span class="sxs-lookup"><span data-stu-id="e73dc-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="e73dc-238">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="e73dc-238">Technical profile</span></span> | <span data-ttu-id="e73dc-239">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="e73dc-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="e73dc-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="e73dc-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="e73dc-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="e73dc-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="e73dc-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="e73dc-243">Технические профили для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e73dc-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="e73dc-244">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="e73dc-244">Technical profile</span></span> | <span data-ttu-id="e73dc-245">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="e73dc-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="e73dc-246">*AAD-Common*</span></span> | <span data-ttu-id="e73dc-247">Включен технические профиль hello другие профили технические AAD-xxx</span><span class="sxs-lookup"><span data-stu-id="e73dc-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="e73dc-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="e73dc-249">Технический профиль для входа в социальные сети</span><span class="sxs-lookup"><span data-stu-id="e73dc-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="e73dc-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="e73dc-251">Технический профиль для входа в социальные сети</span><span class="sxs-lookup"><span data-stu-id="e73dc-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="e73dc-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="e73dc-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="e73dc-253">Технический профиль для входа в социальные сети</span><span class="sxs-lookup"><span data-stu-id="e73dc-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="e73dc-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="e73dc-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="e73dc-255">Технический профиль для локальных учетных записей</span><span class="sxs-lookup"><span data-stu-id="e73dc-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="e73dc-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="e73dc-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="e73dc-257">Технический профиль для локальных учетных записей</span><span class="sxs-lookup"><span data-stu-id="e73dc-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="e73dc-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="e73dc-259">Технический профиль для обновления записи пользователя с помощью objectId</span><span class="sxs-lookup"><span data-stu-id="e73dc-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="e73dc-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="e73dc-261">Технический профиль для обновления записи пользователя с помощью objectId</span><span class="sxs-lookup"><span data-stu-id="e73dc-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="e73dc-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="e73dc-263">Технический профиль для обновления записи пользователя с помощью objectId</span><span class="sxs-lookup"><span data-stu-id="e73dc-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="e73dc-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="e73dc-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="e73dc-265">Технические профиль является данных используется tooread после аутентификации пользователя</span><span class="sxs-lookup"><span data-stu-id="e73dc-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="e73dc-266">Технические профили для самоподтверждения</span><span class="sxs-lookup"><span data-stu-id="e73dc-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="e73dc-267">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="e73dc-267">Technical profile</span></span> | <span data-ttu-id="e73dc-268">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="e73dc-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="e73dc-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="e73dc-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="e73dc-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="e73dc-271">Технические профили для локальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="e73dc-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="e73dc-272">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="e73dc-272">Technical profile</span></span> | <span data-ttu-id="e73dc-273">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="e73dc-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="e73dc-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="e73dc-275">Технические профили для управления сеансами</span><span class="sxs-lookup"><span data-stu-id="e73dc-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="e73dc-276">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="e73dc-276">Technical profile</span></span> | <span data-ttu-id="e73dc-277">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="e73dc-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="e73dc-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="e73dc-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="e73dc-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="e73dc-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="e73dc-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="e73dc-281">Имя профиля, используемых toodisambiguate AAD сеанса между входами вверх и вход</span><span class="sxs-lookup"><span data-stu-id="e73dc-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="e73dc-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="e73dc-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="e73dc-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="e73dc-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="e73dc-284">Технические профили для технических профилей и подсистемы политик инфраструктуры доверия</span><span class="sxs-lookup"><span data-stu-id="e73dc-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="e73dc-285">В настоящее время нет технических профили задаются для hello **TechnicalProfiles модуль политики Trustframework** поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="e73dc-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="e73dc-286">Технические профили для поставщика токенов</span><span class="sxs-lookup"><span data-stu-id="e73dc-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="e73dc-287">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="e73dc-287">Technical profile</span></span> | <span data-ttu-id="e73dc-288">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="e73dc-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="e73dc-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="e73dc-290">Пути взаимодействия пользователя</span><span class="sxs-lookup"><span data-stu-id="e73dc-290">User journeys</span></span>

<span data-ttu-id="e73dc-291">В этом разделе описывается hello пользователя пути уже объявлен в hello *B2C_1A_base* политики.</span><span class="sxs-lookup"><span data-stu-id="e73dc-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="e73dc-292">Эти пути пользователя, подвержены toobe Дополнительные ссылки, переопределении или расширено по мере необходимости в собственные политики, а также как hello *B2C_1A_base_extensions* политики.</span><span class="sxs-lookup"><span data-stu-id="e73dc-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="e73dc-293">Пути взаимодействия пользователя</span><span class="sxs-lookup"><span data-stu-id="e73dc-293">User journey</span></span> | <span data-ttu-id="e73dc-294">Описание</span><span class="sxs-lookup"><span data-stu-id="e73dc-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="e73dc-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="e73dc-295">*SignUp*</span></span> | |
| <span data-ttu-id="e73dc-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="e73dc-296">*SignIn*</span></span> | |
| <span data-ttu-id="e73dc-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="e73dc-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="e73dc-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="e73dc-298">*EditProfile*</span></span> | |
| <span data-ttu-id="e73dc-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="e73dc-299">*PasswordReset*</span></span> | |
