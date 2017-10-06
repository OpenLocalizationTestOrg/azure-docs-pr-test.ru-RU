---
title: "aaaBest и рекомендации для условного доступа в Azure Active Directory | Документы Microsoft"
description: "Необходимые сведения о том, что нужно и не нужно делать при настройке политики условного доступа."
services: active-directory
keywords: "tooapps условного доступа, условного доступа с Azure AD, защита доступа к ресурсам toocompany, политики условного доступа"
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
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="48627-104">Рекомендации по работе с условным доступом в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48627-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="48627-105">В этом разделе приводятся необходимые сведения о том, что нужно и не нужно делать при настройке политики условного доступа.</span><span class="sxs-lookup"><span data-stu-id="48627-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="48627-106">Перед прочтением этого раздела следует ознакомиться с основными понятиями hello и терминология hello появлялся [условный доступ в Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="48627-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="48627-107">Необходимая информация</span><span class="sxs-lookup"><span data-stu-id="48627-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="48627-108">Что необходимо toomake рабочих политики?</span><span class="sxs-lookup"><span data-stu-id="48627-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="48627-109">При создании политики отсутствуют выбранные пользователи, группы, приложения или элементы управления доступом.</span><span class="sxs-lookup"><span data-stu-id="48627-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Облачные приложения](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="48627-111">toomake политикой работы, необходимо настроить hello следующее:</span><span class="sxs-lookup"><span data-stu-id="48627-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="48627-112">Что</span><span class="sxs-lookup"><span data-stu-id="48627-112">What</span></span>           | <span data-ttu-id="48627-113">Как</span><span class="sxs-lookup"><span data-stu-id="48627-113">How</span></span>                                  | <span data-ttu-id="48627-114">Назначение</span><span class="sxs-lookup"><span data-stu-id="48627-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="48627-115">**Облачные приложения**</span><span class="sxs-lookup"><span data-stu-id="48627-115">**Cloud apps**</span></span> |<span data-ttu-id="48627-116">Tooselect требуется одно или несколько приложений.</span><span class="sxs-lookup"><span data-stu-id="48627-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="48627-117">Цель Hello политику условного доступа — tooenable вы toofine Настройка как авторизованные пользователи имеют доступ к приложениям.</span><span class="sxs-lookup"><span data-stu-id="48627-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="48627-118">**Пользователи и группы**</span><span class="sxs-lookup"><span data-stu-id="48627-118">**Users and groups**</span></span> | <span data-ttu-id="48627-119">Требуется tooselect по крайней мере один пользователь или группа, авторизованных tooaccess hello облачные приложения вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="48627-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="48627-120">Политика условного доступа, которой не назначены пользователи и группы, не активируется.</span><span class="sxs-lookup"><span data-stu-id="48627-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="48627-121">**Элементы управления доступом**</span><span class="sxs-lookup"><span data-stu-id="48627-121">**Access controls**</span></span> | <span data-ttu-id="48627-122">Требуется по крайней мере один tooselect контроль доступа.</span><span class="sxs-lookup"><span data-stu-id="48627-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="48627-123">Процессор политики должен tooknow какие toodo, если соблюдены условия.</span><span class="sxs-lookup"><span data-stu-id="48627-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="48627-124">В дополнение toothese базовые требования, во многих случаях нужно также настроить условие.</span><span class="sxs-lookup"><span data-stu-id="48627-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="48627-125">Политики также будет работать без настроенное условие, условия — hello определяющим фактором для точной настройки доступа tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="48627-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![Облачные приложения](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="48627-127">Проверка назначений</span><span class="sxs-lookup"><span data-stu-id="48627-127">How are assignments evaluated?</span></span>

<span data-ttu-id="48627-128">Все назначения выполняются с помощью логического оператора **AND**.</span><span class="sxs-lookup"><span data-stu-id="48627-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="48627-129">При наличии более одного настройки назначения tootrigger политики, должны быть выполнены все назначения.</span><span class="sxs-lookup"><span data-stu-id="48627-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="48627-130">Если вам требуется tooconfigure расположение условие, которое применяет tooall подключения за пределами сети организации, это достигается путем:</span><span class="sxs-lookup"><span data-stu-id="48627-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="48627-131">включить **все расположения**;</span><span class="sxs-lookup"><span data-stu-id="48627-131">Including **All locations**</span></span>
- <span data-ttu-id="48627-132">исключить **все надежные IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="48627-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="48627-133">Что произойдет, если у вас есть политики в hello классический портал Azure и Azure настроен портал?</span><span class="sxs-lookup"><span data-stu-id="48627-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="48627-134">Обе политики с Azure Active Directory и hello пользователь получает доступ только в том случае, если выполняются все требования.</span><span class="sxs-lookup"><span data-stu-id="48627-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="48627-135">Что произойдет, если у вас есть политики в hello портал Intune Silverlight и hello портала Azure?</span><span class="sxs-lookup"><span data-stu-id="48627-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="48627-136">Обе политики с Azure Active Directory и hello пользователь получает доступ только в том случае, если выполняются все требования.</span><span class="sxs-lookup"><span data-stu-id="48627-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="48627-137">Что произойдет, если у меня есть несколько политик для одного пользователя настроен hello?</span><span class="sxs-lookup"><span data-stu-id="48627-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="48627-138">При каждом входе в систему Azure Active Directory оценивает все политики и гарантирует, что соблюдены все требования перед пользователя toohello предоставленный доступ.</span><span class="sxs-lookup"><span data-stu-id="48627-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="48627-139">Работает ли условный доступ с Exchange Active Sync?</span><span class="sxs-lookup"><span data-stu-id="48627-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="48627-140">Да. Exchange ActiveSync можно использовать в политике условного доступа.</span><span class="sxs-lookup"><span data-stu-id="48627-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="48627-141">Чего следует избегать</span><span class="sxs-lookup"><span data-stu-id="48627-141">What you should avoid doing</span></span>

<span data-ttu-id="48627-142">Hello условным доступом framework предоставляет гибкость значительные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="48627-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="48627-143">Однако гибкость также означает, что необходимо внимательно просмотреть каждый tooreleasing предыдущей конфигурации политики она tooavoid нежелательные результаты.</span><span class="sxs-lookup"><span data-stu-id="48627-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="48627-144">В этом контексте следует уделять особое внимание tooassignments, такие как влияния на полные наборы **все пользователи / группы / облачные приложения**.</span><span class="sxs-lookup"><span data-stu-id="48627-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="48627-145">В вашей среде следует избегать hello конфигурации:</span><span class="sxs-lookup"><span data-stu-id="48627-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="48627-146">**Для всех пользователей, всех облачных приложений:**</span><span class="sxs-lookup"><span data-stu-id="48627-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="48627-147">**Блокировка доступа** — эта конфигурация блокирует всю организацию, что явно не является хорошей идеей.</span><span class="sxs-lookup"><span data-stu-id="48627-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="48627-148">**Требовать соответствующее требованиям устройство** — для пользователей, не зарегистрировавшие свои устройства, но эта политика блокирует все доступ, включая доступ toohello портала.</span><span class="sxs-lookup"><span data-stu-id="48627-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="48627-149">Если вы являетесь администратором без зарегистрированного устройства, эта политика блокирует возвращались в hello Azure портала toochange hello политики.</span><span class="sxs-lookup"><span data-stu-id="48627-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="48627-150">**Требует присоединения к домену** — этот блок политики доступа имеет также hello потенциальных tooblock доступ для всех пользователей в вашей организации при отсутствии устройств, присоединенных к домену еще.</span><span class="sxs-lookup"><span data-stu-id="48627-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="48627-151">**Для всех пользователей, всех облачных приложений, всех платформ устройств:**</span><span class="sxs-lookup"><span data-stu-id="48627-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="48627-152">**Блокировка доступа** — эта конфигурация блокирует всю организацию, что явно не является хорошей идеей.</span><span class="sxs-lookup"><span data-stu-id="48627-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="48627-153">Распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="48627-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="48627-154">Требование Многофакторной идентификации для приложений</span><span class="sxs-lookup"><span data-stu-id="48627-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="48627-155">Во многих средах имеется приложения, требующие более высокий уровень защиты, чем hello другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="48627-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="48627-156">Это, например, hello вариант для приложений, имеющих доступ к данным toosensitive.</span><span class="sxs-lookup"><span data-stu-id="48627-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="48627-157">Если вы хотите tooadd еще один уровень защиты toothese приложения, можно настроить политику условного доступа, которая требует многофакторной проверки подлинности, когда пользователи получают доступ к этим приложениям.</span><span class="sxs-lookup"><span data-stu-id="48627-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="48627-158">Требование Многофакторной идентификации для доступа из сетей, которые не являются доверенными</span><span class="sxs-lookup"><span data-stu-id="48627-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="48627-159">Этот сценарий является аналогичные toohello предыдущего сценария, так как он добавляет требование многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="48627-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="48627-160">Тем не менее hello основное различие — hello условие для соответствия этому требованию.</span><span class="sxs-lookup"><span data-stu-id="48627-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="48627-161">При фокус hello hello предыдущего сценария в приложениях с toosensitve доступа к данным, hello этот сценарий посвящен надежных расположений.</span><span class="sxs-lookup"><span data-stu-id="48627-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="48627-162">Иными словами, вы можете настроить требование Многофакторной идентификации, если пользователь обращается к приложению из сети, которой вы не доверяете.</span><span class="sxs-lookup"><span data-stu-id="48627-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="48627-163">Только доверенные устройства могут получать доступ к службам Office 365</span><span class="sxs-lookup"><span data-stu-id="48627-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="48627-164">Если вы используете Intune в вашей среде, можно немедленно начать с помощью интерфейса политики hello условным доступом в консоли Azure hello.</span><span class="sxs-lookup"><span data-stu-id="48627-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="48627-165">Многие клиенты Intune используют только доверенные устройства могут получить доступ к службам Office 365 tooensure условного доступа.</span><span class="sxs-lookup"><span data-stu-id="48627-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="48627-166">Это означает, что мобильных устройств, зарегистрированных в Intune и соответствие требованиям политики, а, соединенных tooan локальному домену компьютеров под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="48627-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="48627-167">Основное улучшение состоит в том, вы не tooset hello одну политику для всех служб Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="48627-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="48627-168">При создании новой политики, настройте hello облачных приложений tooinclude каждого приложения hello Office 365, с которыми нужно tooprotect с с помощью условного доступа.</span><span class="sxs-lookup"><span data-stu-id="48627-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48627-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48627-169">Next steps</span></span>

<span data-ttu-id="48627-170">Если необходимо, чтобы tooknow tooconfigure политику условного доступа. в статье [приступить к работе с помощью условного доступа в Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="48627-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
