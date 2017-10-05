---
title: "Рекомендации по работе с условным доступом в Azure Active Directory | Документация Майкрософт"
description: "Необходимые сведения о том, что нужно и не нужно делать при настройке политики условного доступа."
services: active-directory
keywords: "условный доступ к приложениям, условный доступ посредством Azure Active Directory, безопасный доступ к ресурсам организации, политики условного доступа"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="b31e6-104">Рекомендации по работе с условным доступом в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b31e6-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="b31e6-105">В этом разделе приводятся необходимые сведения о том, что нужно и не нужно делать при настройке политики условного доступа.</span><span class="sxs-lookup"><span data-stu-id="b31e6-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="b31e6-106">Перед прочтением этого раздела следует ознакомиться с основными понятиями и терминологией, связанной с [условным доступом в Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b31e6-106">Before reading this topic, you should familiarize yourself with the concepts and the terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="b31e6-107">Необходимая информация</span><span class="sxs-lookup"><span data-stu-id="b31e6-107">What you should know</span></span>

### <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="b31e6-108">Что необходимо для работы политики?</span><span class="sxs-lookup"><span data-stu-id="b31e6-108">What’s required to make a policy work?</span></span>

<span data-ttu-id="b31e6-109">При создании политики отсутствуют выбранные пользователи, группы, приложения или элементы управления доступом.</span><span class="sxs-lookup"><span data-stu-id="b31e6-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Облачные приложения](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="b31e6-111">Чтобы привести политику в работоспособное состояние, необходимо выполнить следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="b31e6-111">To make your policy work, you must configure the following:</span></span>


|<span data-ttu-id="b31e6-112">Что</span><span class="sxs-lookup"><span data-stu-id="b31e6-112">What</span></span>           | <span data-ttu-id="b31e6-113">Как</span><span class="sxs-lookup"><span data-stu-id="b31e6-113">How</span></span>                                  | <span data-ttu-id="b31e6-114">Назначение</span><span class="sxs-lookup"><span data-stu-id="b31e6-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="b31e6-115">**Облачные приложения**</span><span class="sxs-lookup"><span data-stu-id="b31e6-115">**Cloud apps**</span></span> |<span data-ttu-id="b31e6-116">Необходимо выбрать одно или несколько приложений.</span><span class="sxs-lookup"><span data-stu-id="b31e6-116">You need to select one or more apps.</span></span>  | <span data-ttu-id="b31e6-117">Политика условного доступа предназначена для точной настройки способа доступа авторизованных пользователей к приложениям.</span><span class="sxs-lookup"><span data-stu-id="b31e6-117">The goal of a conditional access policy is to enable you to fine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="b31e6-118">**Пользователи и группы**</span><span class="sxs-lookup"><span data-stu-id="b31e6-118">**Users and groups**</span></span> | <span data-ttu-id="b31e6-119">Необходимо выбрать по меньшей мере одного пользователя или группу, которая имеет права для доступа к выбранным облачным приложениям.</span><span class="sxs-lookup"><span data-stu-id="b31e6-119">You need to select at least one user or group that is authorized to access the cloud apps you have selected.</span></span> | <span data-ttu-id="b31e6-120">Политика условного доступа, которой не назначены пользователи и группы, не активируется.</span><span class="sxs-lookup"><span data-stu-id="b31e6-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="b31e6-121">**Элементы управления доступом**</span><span class="sxs-lookup"><span data-stu-id="b31e6-121">**Access controls**</span></span> | <span data-ttu-id="b31e6-122">Необходимо выбрать по меньшей мере один элемент контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="b31e6-122">You need to select at least one access control.</span></span> | <span data-ttu-id="b31e6-123">Процессор политики должен знать, что делать в случае выполнения условий.</span><span class="sxs-lookup"><span data-stu-id="b31e6-123">Your policy processor needs to know what to do if your conditions are satisfied.</span></span>|


<span data-ttu-id="b31e6-124">Помимо этих основных требований во многих случаях вы также должны настроить условие.</span><span class="sxs-lookup"><span data-stu-id="b31e6-124">In addition to these basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="b31e6-125">Несмотря на то, что политика будет работать и без настроенного условия, условия являются определяющим фактором для точной настройки доступа к приложениям.</span><span class="sxs-lookup"><span data-stu-id="b31e6-125">While a policy would also work without a configured condition, conditions are the driving factor for fine-tuning access to your apps.</span></span>


![Облачные приложения](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="b31e6-127">Проверка назначений</span><span class="sxs-lookup"><span data-stu-id="b31e6-127">How are assignments evaluated?</span></span>

<span data-ttu-id="b31e6-128">Все назначения выполняются с помощью логического оператора **AND**.</span><span class="sxs-lookup"><span data-stu-id="b31e6-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="b31e6-129">Если вы настроили несколько назначений, для активации политики все назначения должны быть выполнены.</span><span class="sxs-lookup"><span data-stu-id="b31e6-129">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="b31e6-130">Если необходимо настроить условие расположения, которое применяется ко всем подключениям из-за пределов сети вашей организации, это можно сделать двумя способами:</span><span class="sxs-lookup"><span data-stu-id="b31e6-130">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="b31e6-131">включить **все расположения**;</span><span class="sxs-lookup"><span data-stu-id="b31e6-131">Including **All locations**</span></span>
- <span data-ttu-id="b31e6-132">исключить **все надежные IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="b31e6-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="b31e6-133">Что произойдет, если настроить политики на классическом портале Azure и на портале Azure?</span><span class="sxs-lookup"><span data-stu-id="b31e6-133">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="b31e6-134">Azure Active Directory применяет обе политики, и пользователь получает доступ только в том случае, если все требования соблюдены.</span><span class="sxs-lookup"><span data-stu-id="b31e6-134">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="b31e6-135">Что произойдет, если настроить политики на портале Intune Silverlight и на портале Azure?</span><span class="sxs-lookup"><span data-stu-id="b31e6-135">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="b31e6-136">Azure Active Directory применяет обе политики, и пользователь получает доступ только в том случае, если все требования соблюдены.</span><span class="sxs-lookup"><span data-stu-id="b31e6-136">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="b31e6-137">Что произойдет, если настроить несколько политик для одного пользователя?</span><span class="sxs-lookup"><span data-stu-id="b31e6-137">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="b31e6-138">Во время каждого входа в систему Azure Active Directory оценивает все политики и проверяет соблюдение всех требований, прежде чем предоставить пользователю доступ.</span><span class="sxs-lookup"><span data-stu-id="b31e6-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="b31e6-139">Работает ли условный доступ с Exchange Active Sync?</span><span class="sxs-lookup"><span data-stu-id="b31e6-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="b31e6-140">Да. Exchange ActiveSync можно использовать в политике условного доступа.</span><span class="sxs-lookup"><span data-stu-id="b31e6-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="b31e6-141">Чего следует избегать</span><span class="sxs-lookup"><span data-stu-id="b31e6-141">What you should avoid doing</span></span>

<span data-ttu-id="b31e6-142">Платформа условного доступа обеспечивает исключительную гибкость конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b31e6-142">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="b31e6-143">Тем не менее, исключительная гибкость также означает, что во избежание нежелательных результатов необходимо внимательно просмотреть каждую политику конфигурации, прежде чем выпускать ее.</span><span class="sxs-lookup"><span data-stu-id="b31e6-143">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="b31e6-144">В этом контексте следует уделить особое внимание назначениям, которые влияют на полные наборы, такие как **все пользователи / группы / облачные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b31e6-144">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="b31e6-145">В своей среде следует избегать следующих конфигураций:</span><span class="sxs-lookup"><span data-stu-id="b31e6-145">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="b31e6-146">**Для всех пользователей, всех облачных приложений:**</span><span class="sxs-lookup"><span data-stu-id="b31e6-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="b31e6-147">**Блокировка доступа** — эта конфигурация блокирует всю организацию, что явно не является хорошей идеей.</span><span class="sxs-lookup"><span data-stu-id="b31e6-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="b31e6-148">**Требовать соответствующее требованиям устройство** — для пользователей, которые еще не зарегистрировали свои устройства, эта политика полностью блокирует доступ, включая доступ к порталу Intune.</span><span class="sxs-lookup"><span data-stu-id="b31e6-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="b31e6-149">Если вы являетесь администратором без зарегистрированного устройства, то эта политика блокирует ваш доступ к порталу Azure для изменения политики.</span><span class="sxs-lookup"><span data-stu-id="b31e6-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="b31e6-150">**Require domain join** (Требовать присоединения к домену) — эта политика блокировки доступа также имеет возможность блокировать доступ для всех пользователей организации, у которых еще нет присоединенных к домену устройств.</span><span class="sxs-lookup"><span data-stu-id="b31e6-150">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="b31e6-151">**Для всех пользователей, всех облачных приложений, всех платформ устройств:**</span><span class="sxs-lookup"><span data-stu-id="b31e6-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="b31e6-152">**Блокировка доступа** — эта конфигурация блокирует всю организацию, что явно не является хорошей идеей.</span><span class="sxs-lookup"><span data-stu-id="b31e6-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="b31e6-153">Распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="b31e6-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="b31e6-154">Требование Многофакторной идентификации для приложений</span><span class="sxs-lookup"><span data-stu-id="b31e6-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="b31e6-155">Во многих средах для одних приложений требуется более высокий уровень защиты, чем для других.</span><span class="sxs-lookup"><span data-stu-id="b31e6-155">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="b31e6-156">Например, это касается приложений с доступом к конфиденциальным данным.</span><span class="sxs-lookup"><span data-stu-id="b31e6-156">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="b31e6-157">Если нужно добавить еще один уровень защиты для этих приложений, можно настроить политику условного доступа, которая требует Многофакторной идентификации при обращении пользователей к этим приложениям.</span><span class="sxs-lookup"><span data-stu-id="b31e6-157">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="b31e6-158">Требование Многофакторной идентификации для доступа из сетей, которые не являются доверенными</span><span class="sxs-lookup"><span data-stu-id="b31e6-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="b31e6-159">Этот сценарий похож на предыдущий, так как он добавляет требование Многофакторной идентификации.</span><span class="sxs-lookup"><span data-stu-id="b31e6-159">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="b31e6-160">Но главное различие — условие для этого требования.</span><span class="sxs-lookup"><span data-stu-id="b31e6-160">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="b31e6-161">Главным фактором в предыдущем сценарии были приложения с доступом к конфиденциальным данным. В этом сценарии главным фактором являются надежные расположения.</span><span class="sxs-lookup"><span data-stu-id="b31e6-161">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="b31e6-162">Иными словами, вы можете настроить требование Многофакторной идентификации, если пользователь обращается к приложению из сети, которой вы не доверяете.</span><span class="sxs-lookup"><span data-stu-id="b31e6-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="b31e6-163">Только доверенные устройства могут получать доступ к службам Office 365</span><span class="sxs-lookup"><span data-stu-id="b31e6-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="b31e6-164">Если вы используете Intune в своей среде, вы можете немедленно начать использовать интерфейс политики условного доступа в консоли Azure.</span><span class="sxs-lookup"><span data-stu-id="b31e6-164">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="b31e6-165">Многие клиенты Intune используют условный доступ, чтобы только доверенные устройства могли обращаться к службам Office 365.</span><span class="sxs-lookup"><span data-stu-id="b31e6-165">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="b31e6-166">К ним относятся мобильные устройства, зарегистрированные с помощью Intune и отвечающие требованиям политики соответствия, а также компьютеры под управлением Windows, присоединенные к локальному домену.</span><span class="sxs-lookup"><span data-stu-id="b31e6-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="b31e6-167">Основное преимущество заключается в том, что вам не нужно настраивать одну и ту же политику для всех служб Office 365.</span><span class="sxs-lookup"><span data-stu-id="b31e6-167">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="b31e6-168">При создании новой политики настройте облачные приложения, чтобы они включали каждое приложение Office 365, которое необходимо защитить с помощью условного доступа.</span><span class="sxs-lookup"><span data-stu-id="b31e6-168">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b31e6-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b31e6-169">Next steps</span></span>

<span data-ttu-id="b31e6-170">Если вы хотите узнать, как настроить политику условного доступа, см. статью о том, как [начать работу с условным доступом в Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b31e6-170">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
