---
title: "aaaConditional доступ для совместной работы пользователей Azure Active Directory B2B | Документы Microsoft"
description: "Совместная работа Azure Active Directory B2B поддерживает многофакторную проверку подлинности (MFA) для корпоративных приложений tooyour избирательный доступ"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="c6729-103">Условный доступ пользователей в службе совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="c6729-104">Многофакторная идентификация для пользователей B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="c6729-105">Благодаря службе совместной работы Azure AD B2B организации могут применять политики многофакторной проверки подлинности (MFA) к пользователям B2B.</span><span class="sxs-lookup"><span data-stu-id="c6729-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="c6729-106">Эти политики могут применяться на уровне отдельных пользователей, hello клиента или приложения hello таким же образом, что они включены штатных сотрудников и членов hello организации.</span><span class="sxs-lookup"><span data-stu-id="c6729-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="c6729-107">Политики многофакторной проверки Подлинности применяются в организации по ресурсам hello.</span><span class="sxs-lookup"><span data-stu-id="c6729-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="c6729-108">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6729-108">Example:</span></span>
1. <span data-ttu-id="c6729-109">Рабочий процесс администратора или сведения в компании A приглашает пользователя из приложения компании B tooan *Foo* в компании а.</span><span class="sxs-lookup"><span data-stu-id="c6729-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="c6729-110">Приложение *Foo* в компании A — настроенное toorequire многофакторной проверки Подлинности при доступе.</span><span class="sxs-lookup"><span data-stu-id="c6729-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="c6729-111">Когда пользователь hello компании B пытается tooaccess приложения *Foo* hello компании клиента, они являются задаваемые toocomplete запрос многофакторной проверки Подлинности.</span><span class="sxs-lookup"><span data-stu-id="c6729-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="c6729-112">Hello пользователя можно настроить их многофакторной проверки Подлинности компании A и выбирает параметр их многофакторной проверки Подлинности.</span><span class="sxs-lookup"><span data-stu-id="c6729-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="c6729-113">Такой режим применим для любой учетной записи (например, Azure AD или MSA, если пользователи из компании Б используют для проверки подлинности социальные сети).</span><span class="sxs-lookup"><span data-stu-id="c6729-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="c6729-114">Компания A должна иметь достаточное количество лицензий Azure AD Premium с поддержкой MFA.</span><span class="sxs-lookup"><span data-stu-id="c6729-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="c6729-115">Hello сотрудником компании B использует лицензии компании A.</span><span class="sxs-lookup"><span data-stu-id="c6729-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="c6729-116">приглашение аренды Hello всегда является ответственность за многофакторной проверки Подлинности для пользователей в организации партнера hello, даже если hello партнерской организации возможности многофакторной проверки Подлинности.</span><span class="sxs-lookup"><span data-stu-id="c6729-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="c6729-117">Настройка MFA для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="c6729-118">toodiscover примеры tooset копирование многофакторной проверки Подлинности для пользователей B2B совместной работы, как в разделе hello следующие видео:</span><span class="sxs-lookup"><span data-stu-id="c6729-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="c6729-119">Прохождение MFA пользователями службы B2B при активации предложения</span><span class="sxs-lookup"><span data-stu-id="c6729-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="c6729-120">См. следующие возможности активации hello toosee анимации hello.</span><span class="sxs-lookup"><span data-stu-id="c6729-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="c6729-121">Сброс настроек MFA для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="c6729-122">В настоящее время Здравствуйте, администратор может потребовать B2B совместной работы пользователей tooproof копирование снова только с помощью hello следующие командлеты PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c6729-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="c6729-123">Подключение tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="c6729-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="c6729-124">Получение сведений о методах проверки для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="c6729-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="c6729-125">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6729-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="c6729-126">Сменить hello метод многофакторной проверки Подлинности для конкретного пользователя toorequire hello B2B совместную работу пользователя tooset дополнительная защита методов еще раз.</span><span class="sxs-lookup"><span data-stu-id="c6729-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="c6729-127">Пример:</span><span class="sxs-lookup"><span data-stu-id="c6729-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="c6729-128">Почему мы выполнять многофакторную проверку Подлинности на аренды ресурса hello?</span><span class="sxs-lookup"><span data-stu-id="c6729-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="c6729-129">В текущем выпуске hello многофакторной проверки Подлинности всегда проводится в аренды ресурса hello, по причинам, предсказуемость.</span><span class="sxs-lookup"><span data-stu-id="c6729-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="c6729-130">Например предположим, что пользователь Contoso (Sally) является приглашенных tooFabrikam и Fabrikam включения многофакторной проверки Подлинности для пользователей B2B.</span><span class="sxs-lookup"><span data-stu-id="c6729-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="c6729-131">Если Contoso включенной политикой многофакторной проверки Подлинности для App1, но не App2, затем Если мы рассмотрим hello многофакторной проверки Подлинности Contoso утверждения в маркере hello, мы может отображаться следующая проблема hello.</span><span class="sxs-lookup"><span data-stu-id="c6729-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="c6729-132">День 1. Пользователь, который использует MFA в компании Contoso, обращается к App1 и не получает дополнительный запрос на многофакторную проверку подлинности в Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="c6729-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="c6729-133">Второй день: hello пользователя к 2 приложения в компании Contoso, поэтому теперь при доступе к компании Fabrikam, их необходимо зарегистрировать существует многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c6729-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="c6729-134">Этот процесс может вызывать путаницу и может привести toodrop в завершений вход.</span><span class="sxs-lookup"><span data-stu-id="c6729-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="c6729-135">Кроме того даже если компании Contoso есть возможность многофакторной проверки Подлинности, не всегда hello вариантов hello Fabrikam будет доверять hello политики многофакторной проверки Подлинности Contoso.</span><span class="sxs-lookup"><span data-stu-id="c6729-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="c6729-136">И наконец, MFA клиента ресурса также поддерживает управляемые учетные записи службы (MSA), идентификаторы из социальных сетей и партнерские организации, в которых не настроена многофакторная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="c6729-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="c6729-137">Таким образом hello многофакторной проверки подлинности для пользователей B2B рекомендуется tooalways должен требовать многофакторную проверку Подлинности в приглашении клиента hello.</span><span class="sxs-lookup"><span data-stu-id="c6729-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="c6729-138">Это требование может привести toodouble многофакторной проверки Подлинности, в некоторых случаях, но при каждом обращении к приглашению клиента hello, hello конечным пользователям получается прогнозируемого: необходимо зарегистрировать Sally многофакторной проверки подлинности клиента приглашению hello.</span><span class="sxs-lookup"><span data-stu-id="c6729-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="c6729-139">Условный доступ на основе устройств, расположения и рисков для пользователей B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="c6729-140">Когда Contoso включает политик условного доступа на основе устройств для корпоративных данных, доступ к ней с устройств, которые не управляются компанией Contoso и не соответствуют политикам устройства hello Contoso.</span><span class="sxs-lookup"><span data-stu-id="c6729-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="c6729-141">Если устройство пользователя hello B2B не находится под управлением Contoso, доступ B2B пользователей из hello партнерские организации будет заблокирован в контекст эти политики применяются.</span><span class="sxs-lookup"><span data-stu-id="c6729-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="c6729-142">Тем не менее Contoso может создать исключения, списков, содержащих определенный партнер пользователей tooexclude их из hello политики условного доступа на основе устройств.</span><span class="sxs-lookup"><span data-stu-id="c6729-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="c6729-143">Условный доступ на основе расположения для пользователей B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="c6729-144">Политики условного доступа на основе расположения может применяться для пользователей B2B Если hello приглашению организации могут toocreate доверенных диапазон IP-адресов, который определяет их партнерских организациях.</span><span class="sxs-lookup"><span data-stu-id="c6729-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="c6729-145">Политики условного доступа на основе рисков для пользователей B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="c6729-146">В настоящее время риск вход политики на основе не может быть применен tooB2B пользователей, поскольку оценку рисков hello выполняется в домашней организации пользователя hello B2B.</span><span class="sxs-lookup"><span data-stu-id="c6729-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6729-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6729-147">Next steps</span></span>

<span data-ttu-id="c6729-148">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="c6729-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c6729-149">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="c6729-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c6729-150">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="c6729-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="c6729-151">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6729-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="c6729-152">элементы Hello hello электронное приглашение B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="c6729-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="c6729-153">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="c6729-154">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="c6729-155">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="c6729-156">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c6729-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="c6729-157">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="c6729-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="c6729-158">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="c6729-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="c6729-159">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6729-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
