---
title: "aaaSign взаимодействия с Azure AD Identity Protection | Документы Microsoft"
description: "Обзор hello взаимодействие с пользователем при защиты идентификации ее смягчения или исправить пользователь или когда многофакторной проверки подлинности необходим для политики."
services: active-directory
keywords: "защита удостоверений Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="b2685-104">Процедуры входа с защитой идентификации Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2685-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="b2685-105">С помощью защиты идентификации Azure Active Directory можно:</span><span class="sxs-lookup"><span data-stu-id="b2685-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="b2685-106">требуется многофакторная проверка подлинности пользователей tooregister</span><span class="sxs-lookup"><span data-stu-id="b2685-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="b2685-107">контролировать рискованные входы в систему и скомпрометированных пользователей.</span><span class="sxs-lookup"><span data-stu-id="b2685-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="b2685-108">ответ Hello hello системы toothese проблем оказывает влияние на пользователя входа в систему, поскольку непосредственно просто войдите в, указав имя пользователя и пароль не будет возможности больше.</span><span class="sxs-lookup"><span data-stu-id="b2685-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="b2685-109">Дополнительные действия, необходимые tooget пользователя безопасно обратно в business.</span><span class="sxs-lookup"><span data-stu-id="b2685-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="b2685-110">В этом разделе описываются возможности входа пользователя в систему во всех возможных случаях.</span><span class="sxs-lookup"><span data-stu-id="b2685-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="b2685-111">**Многофакторная проверка подлинности**</span><span class="sxs-lookup"><span data-stu-id="b2685-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="b2685-112">Регистрация с многофакторной проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="b2685-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="b2685-113">**Вход, представляющий риск**</span><span class="sxs-lookup"><span data-stu-id="b2685-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="b2685-114">Восстановление входа, представлявшего риск</span><span class="sxs-lookup"><span data-stu-id="b2685-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="b2685-115">Блокировка входа, представляющего риск</span><span class="sxs-lookup"><span data-stu-id="b2685-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="b2685-116">Регистрация с многофакторной проверкой подлинности во время входа, представляющего риск</span><span class="sxs-lookup"><span data-stu-id="b2685-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="b2685-117">**Пользователь под угрозой**</span><span class="sxs-lookup"><span data-stu-id="b2685-117">**User at risk**</span></span>

* <span data-ttu-id="b2685-118">Восстановление скомпрометированной учетной записи</span><span class="sxs-lookup"><span data-stu-id="b2685-118">Compromised account recovery</span></span>
* <span data-ttu-id="b2685-119">Скомпрометированная учетная запись заблокирована</span><span class="sxs-lookup"><span data-stu-id="b2685-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="b2685-120">Регистрация с многофакторной проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="b2685-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="b2685-121">Hello оптимального взаимодействия с пользователем для обоих, hello потока восстановления скомпрометированного счета hello рискованным потока, когда hello позволяет самостоятельно восстановить.</span><span class="sxs-lookup"><span data-stu-id="b2685-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="b2685-122">Если пользователи зарегистрированы для многофакторной проверки подлинности, они уже имеют номер телефона, связанный с учетной записью, который можно использовать toopass проблемами безопасности.</span><span class="sxs-lookup"><span data-stu-id="b2685-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="b2685-123">Не вмешивается справки службы поддержки или администратором является необходимые toorecover от компрометации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b2685-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="b2685-124">Таким образом, настоятельно рекомендуется tooget пользователей зарегистрирован для многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b2685-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="b2685-125">Администраторы могут:</span><span class="sxs-lookup"><span data-stu-id="b2685-125">Administrators can:</span></span>

* <span data-ttu-id="b2685-126">Задайте политику, которая требует tooset пользователями своих учетных записей для дополнительной проверки безопасности.</span><span class="sxs-lookup"><span data-stu-id="b2685-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="b2685-127">Разрешить пропуск регистрации многофакторной проверки подлинности для копирования too30 дней, в случае, если они отображаться toogive льготный период до регистрации.</span><span class="sxs-lookup"><span data-stu-id="b2685-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="b2685-128">**Hello регистрации многофакторной проверки подлинности состоит из трех шагов.**</span><span class="sxs-lookup"><span data-stu-id="b2685-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="b2685-129">В hello, сначала hello пользователь получает уведомление о hello требование tooset hello учетной записи для использования многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b2685-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="b2685-130">![Исправление](./media/active-directory-identityprotection-flows/140.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="b2685-131">tooset многофакторную проверку подлинности вверх, вам требуется система hello toolet знать, как именно необходимо связаться с toobe.</span><span class="sxs-lookup"><span data-stu-id="b2685-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="b2685-132">![Исправление](./media/active-directory-identityprotection-flows/141.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="b2685-133">Hello система отправляет tooyou задачей, и необходимо toorespond.</span><span class="sxs-lookup"><span data-stu-id="b2685-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="b2685-134">![Исправление](./media/active-directory-identityprotection-flows/142.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="b2685-135">Восстановление входа, представлявшего риск</span><span class="sxs-lookup"><span data-stu-id="b2685-135">Risky sign-in recovery</span></span>
<span data-ttu-id="b2685-136">Если администратор настроил политику для входа риски, hello затронутые пользователи получают уведомления при попытке toosign в.</span><span class="sxs-lookup"><span data-stu-id="b2685-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="b2685-137">**Hello рискованным процесс входа в состоит из двух шагов:**</span><span class="sxs-lookup"><span data-stu-id="b2685-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="b2685-138">Hello пользователю сообщается, что что-то необычное обнаружено о вход, например вход из нового расположения, устройства или приложения.</span><span class="sxs-lookup"><span data-stu-id="b2685-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="b2685-139">![Исправление](./media/active-directory-identityprotection-flows/120.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="b2685-140">Hello пользователя является обязательным tooprove свою личность по решению проблем безопасности.</span><span class="sxs-lookup"><span data-stu-id="b2685-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="b2685-141">Если пользователь hello зарегистрирован для многофакторной проверки подлинности, они должны tooround-trip номер телефона tootheir код безопасности.</span><span class="sxs-lookup"><span data-stu-id="b2685-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="b2685-142">Поскольку это только что рискованным вход и скомпрометированного счета, hello пользователь не будет иметь toochange hello пароль в этой процедуре.</span><span class="sxs-lookup"><span data-stu-id="b2685-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="b2685-143">![Исправление](./media/active-directory-identityprotection-flows/121.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="b2685-144">Блокировка входа, представляющего риск</span><span class="sxs-lookup"><span data-stu-id="b2685-144">Risky sign-in blocked</span></span>
<span data-ttu-id="b2685-145">Администраторы также могут выбрать пользователи tooblock входа риск политики при входе в зависимости от уровня риска hello tooset.</span><span class="sxs-lookup"><span data-stu-id="b2685-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="b2685-146">tooget разблокирован, пользователям необходимо обратиться к администратору или в службу поддержки или они попробуйте войти с выберите путь или устройства.</span><span class="sxs-lookup"><span data-stu-id="b2685-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="b2685-147">В этом случае не поможет самостоятельное восстановление путем многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b2685-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="b2685-148">![Исправление](./media/active-directory-identityprotection-flows/200.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="b2685-149">Восстановление скомпрометированной учетной записи</span><span class="sxs-lookup"><span data-stu-id="b2685-149">Compromised account recovery</span></span>
<span data-ttu-id="b2685-150">При настройке политики пользователя риск безопасности пользователей, которые соответствуют пользователя hello уровень, указанным в политике hello риска (и поэтому принимается скомпрометирован) должны проходить через поток восстановления компрометации hello пользователя, прежде чем они могут войти.</span><span class="sxs-lookup"><span data-stu-id="b2685-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="b2685-151">**поток восстановления компрометации Hello пользователя состоит из трех шагов:**</span><span class="sxs-lookup"><span data-stu-id="b2685-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="b2685-152">Hello пользователь уведомляется, что их учетной записи безопасности риску из-за подозрительной активности или утечке учетных данных.</span><span class="sxs-lookup"><span data-stu-id="b2685-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="b2685-153">![Исправление](./media/active-directory-identityprotection-flows/101.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="b2685-154">Hello пользователя является обязательным tooprove свою личность по решению проблем безопасности.</span><span class="sxs-lookup"><span data-stu-id="b2685-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="b2685-155">Если hello пользователь зарегистрирован для многофакторной проверки подлинности они могут самостоятельно восстанавливать раскрытия.</span><span class="sxs-lookup"><span data-stu-id="b2685-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="b2685-156">Им необходимо будет tooround-trip номер телефона tootheir код безопасности.</span><span class="sxs-lookup"><span data-stu-id="b2685-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="b2685-157">![Исправление](./media/active-directory-identityprotection-flows/110.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="b2685-158">Наконец, hello пользователя является принудительное toochange свой пароль, так как кто-то другой могли учетная запись доступа к tootheir.</span><span class="sxs-lookup"><span data-stu-id="b2685-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="b2685-159">На снимках экрана ниже показан этот процесс.</span><span class="sxs-lookup"><span data-stu-id="b2685-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="b2685-160">![Исправление](./media/active-directory-identityprotection-flows/111.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="b2685-161">Скомпрометированная учетная запись заблокирована</span><span class="sxs-lookup"><span data-stu-id="b2685-161">Compromised account blocked</span></span>
<span data-ttu-id="b2685-162">tooget пользователя, который был заблокирован пользовательской политики безопасности риск разблокирован, hello пользователя необходимо обратитесь к администратору или справочной службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="b2685-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="b2685-163">В этом случае не поможет самостоятельное восстановление путем многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b2685-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="b2685-164">![Исправление](./media/active-directory-identityprotection-flows/104.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="b2685-165">Сброс пароля</span><span class="sxs-lookup"><span data-stu-id="b2685-165">Reset password</span></span>
<span data-ttu-id="b2685-166">Если для скомпрометированных пользователей заблокирован вход, администратор может создать для них временный пароль.</span><span class="sxs-lookup"><span data-stu-id="b2685-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="b2685-167">Hello пользователи получат toochange свой пароль при следующем входе в систему.</span><span class="sxs-lookup"><span data-stu-id="b2685-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="b2685-168">![Исправление](./media/active-directory-identityprotection-flows/160.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b2685-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="b2685-169">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="b2685-169">See also</span></span>
* [<span data-ttu-id="b2685-170">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2685-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

