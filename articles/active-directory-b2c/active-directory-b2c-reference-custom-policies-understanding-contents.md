---
title: "Azure Active Directory B2C. Общие сведения о пользовательских политиках начального пакета | Документация Майкрософт"
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
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="9205d-103">Общие сведения о пользовательских политиках начального пакета Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="9205d-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="9205d-104">В этой статье перечислены все основные элементы политики B2C_1A_base, которые входят в **начальный пакет** и используются для создания собственных политик путем наследования политики *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9205d-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="9205d-105">Таким образом, здесь особое внимание уделяется определенным типам утверждений, преобразованию утверждений, определениям содержимого, поставщикам утверждений с их техническими профилями и основным путям взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="9205d-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9205d-106">Корпорация Майкрософт не дает никаких явных или подразумеваемых гарантий в отношении представленной ниже информации.</span><span class="sxs-lookup"><span data-stu-id="9205d-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="9205d-107">Изменения могут быть внесены в любое время: до, во время или после выпуска общедоступной версии.</span><span class="sxs-lookup"><span data-stu-id="9205d-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="9205d-108">Как ваши собственные политики, так и политика B2C_1A_base_extensions могут переопределить эти определения и расширить эту родительскую политику, добавив при необходимости дополнительные.</span><span class="sxs-lookup"><span data-stu-id="9205d-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="9205d-109">Основные элементы *политики B2C_1A_base* — это типы утверждений, преобразования утверждений и определения содержимого.</span><span class="sxs-lookup"><span data-stu-id="9205d-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="9205d-110">На эти элементы можно ссылаться в собственных политиках, а также в *политике B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9205d-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="9205d-111">Схемы утверждений</span><span class="sxs-lookup"><span data-stu-id="9205d-111">Claims schemas</span></span>

<span data-ttu-id="9205d-112">Схемы утверждений состоят из трех разделов:</span><span class="sxs-lookup"><span data-stu-id="9205d-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="9205d-113">Первый раздел содержит минимальные утверждения, требуемые для правильной работы путей взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="9205d-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="9205d-114">Второй раздел содержит утверждения, необходимые для параметров строки запроса и других особых параметров, которые нужно передавать другим поставщикам утверждений, особенно для проверки подлинности в домене login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="9205d-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="9205d-115">**Не изменяйте эти утверждения**.</span><span class="sxs-lookup"><span data-stu-id="9205d-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="9205d-116">Третий раздел содержит дополнительные необязательные утверждения, которые можно получить от пользователя, сохранить в каталоге и отправить в токенах во время входа.</span><span class="sxs-lookup"><span data-stu-id="9205d-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="9205d-117">В этом разделе можно добавить новые типы утверждений, которые можно получить от пользователя или отправить в токенах.</span><span class="sxs-lookup"><span data-stu-id="9205d-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9205d-118">Схема утверждений содержит ограничения на определенные утверждения, такие как пароли и имена пользователей.</span><span class="sxs-lookup"><span data-stu-id="9205d-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="9205d-119">Политика инфраструктуры доверия рассматривает Azure AD так же, как и любого другого поставщика утверждений, и все его ограничения смоделированы в политике уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="9205d-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="9205d-120">Политику можно изменить, чтобы добавить дополнительные ограничения или использовать другой поставщик утверждений для хранилища учетных данных со своими ограничениями.</span><span class="sxs-lookup"><span data-stu-id="9205d-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="9205d-121">Ниже перечислены доступные типы утверждений.</span><span class="sxs-lookup"><span data-stu-id="9205d-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="9205d-122">Утверждения, необходимые для путей взаимодействия пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="9205d-123">Следующие утверждения необходимы для правильной работы путей взаимодействия пользователя:</span><span class="sxs-lookup"><span data-stu-id="9205d-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="9205d-124">Тип утверждения</span><span class="sxs-lookup"><span data-stu-id="9205d-124">Claims type</span></span> | <span data-ttu-id="9205d-125">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="9205d-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="9205d-126">*UserId*</span></span> | <span data-ttu-id="9205d-127">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-127">Username</span></span> |
| <span data-ttu-id="9205d-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="9205d-128">*signInName*</span></span> | <span data-ttu-id="9205d-129">Имя входа</span><span class="sxs-lookup"><span data-stu-id="9205d-129">Sign in name</span></span> |
| <span data-ttu-id="9205d-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="9205d-130">*tenantId*</span></span> | <span data-ttu-id="9205d-131">Идентификатор клиента объекта-пользователя в Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="9205d-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="9205d-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="9205d-132">*objectId*</span></span> | <span data-ttu-id="9205d-133">Идентификатор объекта-пользователя в Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="9205d-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="9205d-134">*password*</span><span class="sxs-lookup"><span data-stu-id="9205d-134">*password*</span></span> | <span data-ttu-id="9205d-135">Пароль</span><span class="sxs-lookup"><span data-stu-id="9205d-135">Password</span></span> |
| <span data-ttu-id="9205d-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="9205d-136">*newPassword*</span></span> | |
| <span data-ttu-id="9205d-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="9205d-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="9205d-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="9205d-138">*passwordPolicies*</span></span> | <span data-ttu-id="9205d-139">Политики пароля, используемые Azure AD B2C Premium, определяющие надежность пароля, срок действия и т. д.</span><span class="sxs-lookup"><span data-stu-id="9205d-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="9205d-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="9205d-140">*sub*</span></span> | |
| <span data-ttu-id="9205d-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9205d-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="9205d-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="9205d-142">*identityProvider*</span></span> | |
| <span data-ttu-id="9205d-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="9205d-143">*displayName*</span></span> | |
| <span data-ttu-id="9205d-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="9205d-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="9205d-145">Номер телефона пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-145">User's telephone number</span></span> |
| <span data-ttu-id="9205d-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="9205d-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="9205d-147">*email*</span><span class="sxs-lookup"><span data-stu-id="9205d-147">*email*</span></span> | <span data-ttu-id="9205d-148">Адрес электронной почты, который может использоваться для связи с пользователем</span><span class="sxs-lookup"><span data-stu-id="9205d-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="9205d-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="9205d-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="9205d-150">Адрес электронной почты, который пользователь может использовать для входа</span><span class="sxs-lookup"><span data-stu-id="9205d-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="9205d-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="9205d-151">*otherMails*</span></span> | <span data-ttu-id="9205d-152">Адреса электронной почты, которые могут использоваться для связи с пользователем</span><span class="sxs-lookup"><span data-stu-id="9205d-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="9205d-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="9205d-153">*userPrincipalName*</span></span> | <span data-ttu-id="9205d-154">Имя пользователя, сохраненное в Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="9205d-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="9205d-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="9205d-155">*upnUserName*</span></span> | <span data-ttu-id="9205d-156">Имя пользователя для создания имени субъекта-пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="9205d-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="9205d-157">*mailNickName*</span></span> | <span data-ttu-id="9205d-158">Псевдоним пользовательской почты, сохраненный в Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="9205d-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="9205d-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="9205d-159">*newUser*</span></span> | |
| <span data-ttu-id="9205d-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="9205d-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="9205d-161">Утверждение, которое указывает, были ли получены от пользователя атрибуты</span><span class="sxs-lookup"><span data-stu-id="9205d-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="9205d-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="9205d-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="9205d-163">Утверждение, которое указывает, был ли получен от пользователя номер телефона</span><span class="sxs-lookup"><span data-stu-id="9205d-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="9205d-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="9205d-164">*authenticationSource*</span></span> | <span data-ttu-id="9205d-165">Указывает, прошел ли пользователь проверку подлинности в поставщике удостоверений социальных сетей, на сайте login.microsoftonline.com или с использованием локальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="9205d-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="9205d-166">Утверждения, необходимые для параметров строки запроса и других особых параметров</span><span class="sxs-lookup"><span data-stu-id="9205d-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="9205d-167">Следующие утверждения необходимы для передачи особых параметров (в том числе некоторые параметры строки запроса) другим поставщикам утверждений:</span><span class="sxs-lookup"><span data-stu-id="9205d-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="9205d-168">Тип утверждения</span><span class="sxs-lookup"><span data-stu-id="9205d-168">Claims type</span></span> | <span data-ttu-id="9205d-169">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="9205d-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="9205d-170">*nux*</span></span> | <span data-ttu-id="9205d-171">Специальный параметр, который передается для проверки подлинности локальной учетной записи на сайт login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9205d-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9205d-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="9205d-172">*nca*</span></span> | <span data-ttu-id="9205d-173">Специальный параметр, который передается для проверки подлинности локальной учетной записи на сайт login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9205d-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9205d-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="9205d-174">*prompt*</span></span> | <span data-ttu-id="9205d-175">Специальный параметр, который передается для проверки подлинности локальной учетной записи на сайт login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9205d-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9205d-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="9205d-176">*mkt*</span></span> | <span data-ttu-id="9205d-177">Специальный параметр, который передается для проверки подлинности локальной учетной записи на сайт login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9205d-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9205d-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="9205d-178">*lc*</span></span> | <span data-ttu-id="9205d-179">Специальный параметр, который передается для проверки подлинности локальной учетной записи на сайт login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9205d-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9205d-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="9205d-180">*grant_type*</span></span> | <span data-ttu-id="9205d-181">Специальный параметр, который передается для проверки подлинности локальной учетной записи на сайт login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9205d-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9205d-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="9205d-182">*scope*</span></span> | <span data-ttu-id="9205d-183">Специальный параметр, который передается для проверки подлинности локальной учетной записи на сайт login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9205d-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9205d-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="9205d-184">*client_id*</span></span> | <span data-ttu-id="9205d-185">Специальный параметр, который передается для проверки подлинности локальной учетной записи на сайт login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9205d-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="9205d-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="9205d-186">*objectIdFromSession*</span></span> | <span data-ttu-id="9205d-187">Параметр, предоставленный поставщиком управления сеансами по умолчанию, чтобы указать, что идентификатор объекта был получен из сеанса единого входа</span><span class="sxs-lookup"><span data-stu-id="9205d-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="9205d-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="9205d-188">*isActiveMFASession*</span></span> | <span data-ttu-id="9205d-189">Параметр, предоставленный поставщиком управления сеансами MFA по умолчанию, чтобы указать, что у пользователя активен сеанс MFA</span><span class="sxs-lookup"><span data-stu-id="9205d-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="9205d-190">Дополнительные (необязательные) утверждения для сбора</span><span class="sxs-lookup"><span data-stu-id="9205d-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="9205d-191">Далее представлены дополнительные утверждения, которые можно получить от пользователей, сохранить в каталоге и отправить в токене.</span><span class="sxs-lookup"><span data-stu-id="9205d-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="9205d-192">Как упоминалось выше, дополнительные утверждения можно добавить к этому списку.</span><span class="sxs-lookup"><span data-stu-id="9205d-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="9205d-193">Тип утверждения</span><span class="sxs-lookup"><span data-stu-id="9205d-193">Claims type</span></span> | <span data-ttu-id="9205d-194">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="9205d-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="9205d-195">*givenName*</span></span> | <span data-ttu-id="9205d-196">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="9205d-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="9205d-197">*surname*</span></span> | <span data-ttu-id="9205d-198">Фамилия пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="9205d-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="9205d-199">*Extension_picture*</span></span> | <span data-ttu-id="9205d-200">Фотография пользователя из социальных сетей</span><span class="sxs-lookup"><span data-stu-id="9205d-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="9205d-201">Преобразования утверждения</span><span class="sxs-lookup"><span data-stu-id="9205d-201">Claim transformations</span></span>

<span data-ttu-id="9205d-202">Ниже перечислены доступные преобразования утверждений.</span><span class="sxs-lookup"><span data-stu-id="9205d-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="9205d-203">Преобразования утверждения</span><span class="sxs-lookup"><span data-stu-id="9205d-203">Claim transformation</span></span> | <span data-ttu-id="9205d-204">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="9205d-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="9205d-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="9205d-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="9205d-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="9205d-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="9205d-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="9205d-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="9205d-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="9205d-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9205d-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="9205d-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9205d-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="9205d-211">Определения содержимого</span><span class="sxs-lookup"><span data-stu-id="9205d-211">Content definitions</span></span>

<span data-ttu-id="9205d-212">В этом разделе описываются определения содержимого, уже объявленные в политике *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="9205d-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="9205d-213">На эти определения можно ссылаться, их можно переопределять или расширять по мере необходимости в собственных политиках и в политике *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9205d-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="9205d-214">Поставщик утверждений</span><span class="sxs-lookup"><span data-stu-id="9205d-214">Claims provider</span></span> | <span data-ttu-id="9205d-215">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="9205d-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="9205d-216">*Facebook*</span></span> | |
| <span data-ttu-id="9205d-217">*Вход с использованием локальной учетной записи*</span><span class="sxs-lookup"><span data-stu-id="9205d-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="9205d-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="9205d-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="9205d-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="9205d-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="9205d-220">*Самоподтверждение*</span><span class="sxs-lookup"><span data-stu-id="9205d-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="9205d-221">*Локальная учетная запись*</span><span class="sxs-lookup"><span data-stu-id="9205d-221">*Local Account*</span></span> | |
| <span data-ttu-id="9205d-222">*Управление сеансами*</span><span class="sxs-lookup"><span data-stu-id="9205d-222">*Session Management*</span></span> | |
| <span data-ttu-id="9205d-223">*Подсистема политик инфраструктуры доверия*</span><span class="sxs-lookup"><span data-stu-id="9205d-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="9205d-224">*Технические профили*</span><span class="sxs-lookup"><span data-stu-id="9205d-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="9205d-225">*Поставщик токенов*</span><span class="sxs-lookup"><span data-stu-id="9205d-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="9205d-226">Технические профили</span><span class="sxs-lookup"><span data-stu-id="9205d-226">Technical profiles</span></span>

<span data-ttu-id="9205d-227">В этом разделе описаны технические профили, уже объявленные поставщиком утверждений в политике  *B2C_1A_base* .</span><span class="sxs-lookup"><span data-stu-id="9205d-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="9205d-228">На эти технические профили можно ссылаться, их можно переопределять или расширять по мере необходимости в собственных политиках и в политике *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9205d-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="9205d-229">Технические профили для Facebook</span><span class="sxs-lookup"><span data-stu-id="9205d-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="9205d-230">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="9205d-230">Technical profile</span></span> | <span data-ttu-id="9205d-231">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9205d-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="9205d-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="9205d-233">Технические профили для входа с использованием локальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="9205d-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="9205d-234">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="9205d-234">Technical profile</span></span> | <span data-ttu-id="9205d-235">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9205d-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="9205d-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="9205d-237">Технические профили для PhoneFactor</span><span class="sxs-lookup"><span data-stu-id="9205d-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="9205d-238">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="9205d-238">Technical profile</span></span> | <span data-ttu-id="9205d-239">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9205d-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="9205d-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="9205d-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="9205d-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="9205d-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="9205d-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="9205d-243">Технические профили для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9205d-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="9205d-244">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="9205d-244">Technical profile</span></span> | <span data-ttu-id="9205d-245">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9205d-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="9205d-246">*AAD-Common*</span></span> | <span data-ttu-id="9205d-247">Технические профили, включенные другими техническими профилями AAD</span><span class="sxs-lookup"><span data-stu-id="9205d-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="9205d-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9205d-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="9205d-249">Технический профиль для входа в социальные сети</span><span class="sxs-lookup"><span data-stu-id="9205d-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="9205d-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="9205d-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="9205d-251">Технический профиль для входа в социальные сети</span><span class="sxs-lookup"><span data-stu-id="9205d-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="9205d-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="9205d-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="9205d-253">Технический профиль для входа в социальные сети</span><span class="sxs-lookup"><span data-stu-id="9205d-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="9205d-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="9205d-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="9205d-255">Технический профиль для локальных учетных записей</span><span class="sxs-lookup"><span data-stu-id="9205d-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="9205d-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="9205d-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="9205d-257">Технический профиль для локальных учетных записей</span><span class="sxs-lookup"><span data-stu-id="9205d-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="9205d-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="9205d-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="9205d-259">Технический профиль для обновления записи пользователя с помощью objectId</span><span class="sxs-lookup"><span data-stu-id="9205d-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="9205d-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="9205d-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="9205d-261">Технический профиль для обновления записи пользователя с помощью objectId</span><span class="sxs-lookup"><span data-stu-id="9205d-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="9205d-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="9205d-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="9205d-263">Технический профиль для обновления записи пользователя с помощью objectId</span><span class="sxs-lookup"><span data-stu-id="9205d-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="9205d-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="9205d-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="9205d-265">Технический профиль, используемый для считывания данных после проверки подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="9205d-266">Технические профили для самоподтверждения</span><span class="sxs-lookup"><span data-stu-id="9205d-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="9205d-267">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="9205d-267">Technical profile</span></span> | <span data-ttu-id="9205d-268">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9205d-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="9205d-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="9205d-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="9205d-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="9205d-271">Технические профили для локальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="9205d-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="9205d-272">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="9205d-272">Technical profile</span></span> | <span data-ttu-id="9205d-273">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9205d-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="9205d-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="9205d-275">Технические профили для управления сеансами</span><span class="sxs-lookup"><span data-stu-id="9205d-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="9205d-276">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="9205d-276">Technical profile</span></span> | <span data-ttu-id="9205d-277">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9205d-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="9205d-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="9205d-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="9205d-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="9205d-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="9205d-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="9205d-281">Имя профиля, используемое для устранения неоднозначности сеанса AAD между регистрацией и входом</span><span class="sxs-lookup"><span data-stu-id="9205d-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="9205d-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="9205d-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="9205d-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="9205d-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="9205d-284">Технические профили для технических профилей и подсистемы политик инфраструктуры доверия</span><span class="sxs-lookup"><span data-stu-id="9205d-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="9205d-285">Сейчас технические профили для поставщика утверждений **технические профили и подсистема политик инфраструктуры доверия** не определены.</span><span class="sxs-lookup"><span data-stu-id="9205d-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="9205d-286">Технические профили для поставщика токенов</span><span class="sxs-lookup"><span data-stu-id="9205d-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="9205d-287">Технический профиль</span><span class="sxs-lookup"><span data-stu-id="9205d-287">Technical profile</span></span> | <span data-ttu-id="9205d-288">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="9205d-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="9205d-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="9205d-290">Пути взаимодействия пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-290">User journeys</span></span>

<span data-ttu-id="9205d-291">В этом разделе описываются пути взаимодействия пользователя, уже объявленные в политике *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="9205d-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="9205d-292">На эти пути взаимодействия пользователя можно ссылаться, их можно переопределять или расширять по мере необходимости в собственных политиках и в политике *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="9205d-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="9205d-293">Пути взаимодействия пользователя</span><span class="sxs-lookup"><span data-stu-id="9205d-293">User journey</span></span> | <span data-ttu-id="9205d-294">Описание</span><span class="sxs-lookup"><span data-stu-id="9205d-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="9205d-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="9205d-295">*SignUp*</span></span> | |
| <span data-ttu-id="9205d-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="9205d-296">*SignIn*</span></span> | |
| <span data-ttu-id="9205d-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="9205d-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="9205d-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="9205d-298">*EditProfile*</span></span> | |
| <span data-ttu-id="9205d-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="9205d-299">*PasswordReset*</span></span> | |
