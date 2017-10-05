---
title: "Условный доступ пользователей в службе совместной работы Azure Active Directory B2B | Документация Майкрософт"
description: "Служба совместной работы Azure Active Directory B2B поддерживает Многофакторную идентификацию (MFA), которая позволяет предоставлять выборочный доступ к корпоративным приложениям."
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
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="e1342-103">Условный доступ пользователей в службе совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="e1342-104">Многофакторная идентификация для пользователей B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="e1342-105">Благодаря службе совместной работы Azure AD B2B организации могут применять политики многофакторной проверки подлинности (MFA) к пользователям B2B.</span><span class="sxs-lookup"><span data-stu-id="e1342-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="e1342-106">Эти политики можно применять на уровне клиента, приложения или отдельных пользователей точно так же, как для штатных сотрудников и членов организации.</span><span class="sxs-lookup"><span data-stu-id="e1342-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="e1342-107">Политики MFA применяются на уровне организации ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e1342-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="e1342-108">Пример:</span><span class="sxs-lookup"><span data-stu-id="e1342-108">Example:</span></span>
1. <span data-ttu-id="e1342-109">Администратор или информационный работник компании А приглашает пользователя из компании Б использовать приложение *Foo*, принадлежащее компании A.</span><span class="sxs-lookup"><span data-stu-id="e1342-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="e1342-110">При доступе в приложение *Foo*, принадлежащее компании A, настроено обязательное прохождение MFA.</span><span class="sxs-lookup"><span data-stu-id="e1342-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="e1342-111">Когда пользователь из компании Б пытается получить доступ к приложению *Foo*, размещенному в клиенте компании А, ему предлагается пройти многофакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="e1342-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="e1342-112">Пользователь может согласовать с компанией А параметры прохождения MFA и выбрать приемлемый вариант.</span><span class="sxs-lookup"><span data-stu-id="e1342-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="e1342-113">Такой режим применим для любой учетной записи (например, Azure AD или MSA, если пользователи из компании Б используют для проверки подлинности социальные сети).</span><span class="sxs-lookup"><span data-stu-id="e1342-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="e1342-114">Компания A должна иметь достаточное количество лицензий Azure AD Premium с поддержкой MFA.</span><span class="sxs-lookup"><span data-stu-id="e1342-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="e1342-115">Пользователь из компании Б использует такую лицензию компании А.</span><span class="sxs-lookup"><span data-stu-id="e1342-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="e1342-116">Таким образом, за настройку MFA для пользователей из партнерской организации всегда отвечает приглашающий клиент, даже если партнерская организация поддерживает использование MFA.</span><span class="sxs-lookup"><span data-stu-id="e1342-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="e1342-117">Настройка MFA для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="e1342-118">Чтобы узнать, как можно с легкостью настроить MFA для пользователей службы совместной работы B2B, просмотрите следующий видеоролик:</span><span class="sxs-lookup"><span data-stu-id="e1342-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="e1342-119">Прохождение MFA пользователями службы B2B при активации предложения</span><span class="sxs-lookup"><span data-stu-id="e1342-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="e1342-120">В следующем видеоролике показано, как выглядит процедура активации:</span><span class="sxs-lookup"><span data-stu-id="e1342-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="e1342-121">Сброс настроек MFA для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="e1342-122">Сейчас администратор может потребовать от пользователей службы совместной работы B2B пройти повторную проверку только с помощью приведенных ниже командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1342-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="e1342-123">Подключение к Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1342-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="e1342-124">Получение сведений о методах проверки для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="e1342-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="e1342-125">Пример:</span><span class="sxs-lookup"><span data-stu-id="e1342-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="e1342-126">Сброс метода многофакторной проверки подлинности для определенного пользователя, после которого пользователь службы совместной работы B2B должен заново задать методы проверки.</span><span class="sxs-lookup"><span data-stu-id="e1342-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="e1342-127">Пример:</span><span class="sxs-lookup"><span data-stu-id="e1342-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="e1342-128">Зачем выполнять MFA на уровне клиента ресурса?</span><span class="sxs-lookup"><span data-stu-id="e1342-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="e1342-129">В текущем выпуске MFA всегда применяется на уровне клиента ресурса, чтобы обеспечить предсказуемое поведение.</span><span class="sxs-lookup"><span data-stu-id="e1342-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="e1342-130">Предположим, что пользователь компании Contoso (Светлана) приглашен в компанию Fabrikam, в которой включена MFA для пользователей B2B.</span><span class="sxs-lookup"><span data-stu-id="e1342-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="e1342-131">Если Contoso использует политику MFA для приложения App1, но не использует для приложения App2, то при использовании такого утверждения MFA Contoso в маркере возникает следующая проблема:</span><span class="sxs-lookup"><span data-stu-id="e1342-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="e1342-132">День 1. Пользователь, который использует MFA в компании Contoso, обращается к App1 и не получает дополнительный запрос на многофакторную проверку подлинности в Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="e1342-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="e1342-133">День 2. Пользователь получил доступ к App 2 компании Contoso и теперь при обращении к Fabrikam должен пройти регистрацию для многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e1342-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="e1342-134">Такой процесс может запутать пользователей и привести к тому, что не все они завершат регистрацию в системе.</span><span class="sxs-lookup"><span data-stu-id="e1342-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="e1342-135">Кроме того, даже если в Contoso предусмотрена функция выполнения MFA, нет гарантии того, что Fabrikam будет доверять политике MFA в Contoso.</span><span class="sxs-lookup"><span data-stu-id="e1342-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="e1342-136">И наконец, MFA клиента ресурса также поддерживает управляемые учетные записи службы (MSA), идентификаторы из социальных сетей и партнерские организации, в которых не настроена многофакторная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="e1342-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="e1342-137">Поэтому мы советуем всегда применять MFA в приглашающем клиенте для пользователей B2B.</span><span class="sxs-lookup"><span data-stu-id="e1342-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="e1342-138">В некоторых случаях это приводит к двойной проверке, но взаимодействие с пользователем при обращении к приглашающему клиенту всегда будет предсказуемым: Светлана должна зарегистрироваться для прохождения MFA в приглашающем клиенте.</span><span class="sxs-lookup"><span data-stu-id="e1342-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="e1342-139">Условный доступ на основе устройств, расположения и рисков для пользователей B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="e1342-140">Если компания Contoso применяет условный доступ на основе устройства к корпоративным данным, блокируется доступ с устройств, которые не управляются компанией Contoso или не соответствуют политикам устройств этой компании.</span><span class="sxs-lookup"><span data-stu-id="e1342-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="e1342-141">Если компания Contoso не управляет устройствами пользователей B2B, то доступ пользователей из организаций-партнеров будет заблокирован во всех контекстах, в которых применяются такие политики.</span><span class="sxs-lookup"><span data-stu-id="e1342-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="e1342-142">Но Contoso может создать списки исключений, включающие пользователей конкретного партнера, чтобы для них не действовали политики условного доступа на основе устройств.</span><span class="sxs-lookup"><span data-stu-id="e1342-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="e1342-143">Условный доступ на основе расположения для пользователей B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="e1342-144">Политики условного доступа на основе расположения есть смысл применять к пользователям B2B в тех случаях, когда приглашающая организация способна создать диапазон надежных IP-адресов, определяющий партнерские организации.</span><span class="sxs-lookup"><span data-stu-id="e1342-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="e1342-145">Политики условного доступа на основе рисков для пользователей B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="e1342-146">Сейчас политики выполнения входа на основе рисков не применяются к пользователям B2B, так как оценка рисков выполняется в домашней организации этих пользователей.</span><span class="sxs-lookup"><span data-stu-id="e1342-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1342-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1342-147">Next steps</span></span>

<span data-ttu-id="e1342-148">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="e1342-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e1342-149">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="e1342-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e1342-150">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="e1342-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="e1342-151">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1342-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="e1342-152">Элементы сообщения с приглашением в службу совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="e1342-153">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="e1342-154">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="e1342-155">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="e1342-156">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="e1342-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="e1342-157">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="e1342-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="e1342-158">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="e1342-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="e1342-159">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1342-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
