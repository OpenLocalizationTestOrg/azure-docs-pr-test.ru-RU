---
title: "Защита идентификации Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как защита идентификации Azure AD позволяет помешать злоумышленникам воспользоваться скомпрометированными удостоверениями и устройствами, а также защитить удостоверение или устройство, которое ранее предположительно или фактически скомпрометировано."
services: active-directory
keywords: "защита удостоверений Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="b4bc1-104">Защита идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4bc1-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="b4bc1-105">Защита идентификации Azure Active Directory — это функция выпуска Azure AD Premium P2, которая позволяет выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="b4bc1-106">обнаруживать потенциальные уязвимости, которые могут повлиять на учетные записи организации;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="b4bc1-107">настраивать автоматические ответы при обнаружении подозрительных действий, связанных с учетными записями организации;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="b4bc1-108">анализировать подозрительные инциденты и выполнять соответствующие действия для их устранения.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="b4bc1-109">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="b4bc1-109">Getting started</span></span>

<span data-ttu-id="b4bc1-110">Корпорация Майкрософт более десяти лет обеспечивает безопасность облачной идентификации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="b4bc1-111">Благодаря функции защиты идентификации Azure Active Directory вы можете использовать в своей среде такие же системы защиты, как и те, что использует корпорация Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="b4bc1-112">Подавляющее большинство нарушений безопасности — это случаи, когда злоумышленники получают доступ к среде за счет кражи удостоверения пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="b4bc1-113">С годами злоумышленники стали еще эффективнее использовать бреши в сторонних системах, а фишинговые атаки стали еще изощреннее.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="b4bc1-114">Как только злоумышленник получит доступ к учетной записи пользователя с привилегиями даже низкого уровня, ему не составит особого труда получить доступ и к важным ресурсам компании.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="b4bc1-115">Поэтому необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="b4bc1-116">защитить все удостоверения независимо от их уровня привилегий;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="b4bc1-117">предотвратить злонамеренное использование скомпрометированных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="b4bc1-118">Обнаружение скомпрометированных удостоверений — непростая задача.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="b4bc1-119">Azure Active Directory использует адаптивные алгоритмы машинного обучения и эвристические методы, чтобы обнаруживать аномалии и подозрительные инциденты, которые могут указывать на компрометацию удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="b4bc1-120">На основе этих данных служба защиты идентификации создает отчеты и оповещения, с помощью которых можно оценить обнаруженные проблемы и предпринять действия по исправлению и устранению рисков.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="b4bc1-121">Защита идентификации Azure Active Directory — это больше, чем просто инструмент для мониторинга и создания отчетности.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="b4bc1-122">Для защиты удостоверений организации можно настроить политики на основе рисков, которые автоматически реагируют на обнаруженные проблемы в случае достижения указанного уровня риска.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="b4bc1-123">Эти политики, помимо других элементов управления условным доступом Azure Active Directory и EMS, позволяют обеспечить автоматическую блокировку или инициировать адаптивные действия по исправлению, в том числе сброс пароля и принудительную многофакторную идентификацию.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="b4bc1-124">Возможности защиты идентификации</span><span class="sxs-lookup"><span data-stu-id="b4bc1-124">Identity Protection capabilities</span></span>

<span data-ttu-id="b4bc1-125">**Обнаружение уязвимостей и учетных записей, подверженных риску:**</span><span class="sxs-lookup"><span data-stu-id="b4bc1-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="b4bc1-126">предоставление пользовательских рекомендаций для повышения общего уровня безопасности путем информирования об уязвимостях.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="b4bc1-127">расчет уровня риска при входе;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="b4bc1-128">расчет уровня риска для пользователя;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-128">Calculating user risk levels</span></span>


<span data-ttu-id="b4bc1-129">**Исследование событий риска:**</span><span class="sxs-lookup"><span data-stu-id="b4bc1-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="b4bc1-130">отправка уведомлений о событиях риска;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="b4bc1-131">исследование событий риска на основе соответствующей и контекстной информации;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="b4bc1-132">базовые рабочие процессы для отслеживания исследований;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="b4bc1-133">легкий доступ к действиям по исправлению, таким как сброс пароля.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="b4bc1-134">**Политики условного доступа на основе рисков:**</span><span class="sxs-lookup"><span data-stu-id="b4bc1-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="b4bc1-135">политика уменьшения рисков при сомнительных входах путем блокировки входа или запроса многофакторной проверки подлинности;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="b4bc1-136">политика блокировки или защиты учетных записей с возможным риском;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="b4bc1-137">политика обязательной регистрации пользователей для многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="b4bc1-138">Роли защиты идентификации</span><span class="sxs-lookup"><span data-stu-id="b4bc1-138">Identity Protection roles</span></span>

<span data-ttu-id="b4bc1-139">Для балансировки нагрузки действий по управлению, связанных с реализацией защиты идентификации, можно назначить несколько ролей.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="b4bc1-140">Служба защиты идентификации Azure AD поддерживает три роли каталога:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="b4bc1-141">Роль</span><span class="sxs-lookup"><span data-stu-id="b4bc1-141">Role</span></span>                         | <span data-ttu-id="b4bc1-142">Может</span><span class="sxs-lookup"><span data-stu-id="b4bc1-142">Can do</span></span>                          | <span data-ttu-id="b4bc1-143">Не может</span><span class="sxs-lookup"><span data-stu-id="b4bc1-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="b4bc1-144">Глобальный администратор</span><span class="sxs-lookup"><span data-stu-id="b4bc1-144">Global administrator</span></span>         | <span data-ttu-id="b4bc1-145">Полный доступ к защите идентификации, встроенная защита идентификации</span><span class="sxs-lookup"><span data-stu-id="b4bc1-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="b4bc1-146">администратор безопасности;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-146">Security administrator</span></span>       | <span data-ttu-id="b4bc1-147">Полный доступ к защите идентификации</span><span class="sxs-lookup"><span data-stu-id="b4bc1-147">Full access to Identity Protection</span></span> | <span data-ttu-id="b4bc1-148">Встроенная защита идентификации, сброс паролей для пользователя</span><span class="sxs-lookup"><span data-stu-id="b4bc1-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="b4bc1-149">Читатель безопасности</span><span class="sxs-lookup"><span data-stu-id="b4bc1-149">Security reader</span></span>              | <span data-ttu-id="b4bc1-150">Доступ только для чтения к защите идентификации</span><span class="sxs-lookup"><span data-stu-id="b4bc1-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="b4bc1-151">Встроенная защита идентификации, исправление пользователей, настройка политик, сброс паролей</span><span class="sxs-lookup"><span data-stu-id="b4bc1-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="b4bc1-152">См. дополнительные сведения о [назначении ролей администратора в Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b4bc1-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="b4bc1-153">Обнаружение</span><span class="sxs-lookup"><span data-stu-id="b4bc1-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="b4bc1-154">Уязвимости</span><span class="sxs-lookup"><span data-stu-id="b4bc1-154">Vulnerabilities</span></span>

<span data-ttu-id="b4bc1-155">Защита идентификации Azure Active Directory анализирует вашу конфигурацию и обнаруживает уязвимости, которые могут повлиять на безопасность ваших пользовательских удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="b4bc1-156">Дополнительные сведения см. в статье [Уязвимости, обнаруживаемые защитой идентификации Azure Active Directory](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="b4bc1-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="b4bc1-157">События риска</span><span class="sxs-lookup"><span data-stu-id="b4bc1-157">Risk events</span></span>

<span data-ttu-id="b4bc1-158">Azure Active Directory использует адаптивные алгоритмы машинного обучения и эвристические методы, чтобы обнаруживать подозрительные действия, связанные с пользовательскими удостоверениями.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="b4bc1-159">Система создает запись для каждого обнаруженного подозрительного действия.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="b4bc1-160">Эти записи также известны как события риска.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="b4bc1-161">Дополнительные сведения см. в статье о [событиях риска Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="b4bc1-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="b4bc1-162">Исследование</span><span class="sxs-lookup"><span data-stu-id="b4bc1-162">Investigation</span></span>
<span data-ttu-id="b4bc1-163">Обычно исследование защиты идентификации начинают с панели мониторинга соответствующей службы.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="b4bc1-164">![Исправление](./media/active-directory-identityprotection/1000.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="b4bc1-165">Панель мониторинга позволяет использовать:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="b4bc1-166">отчеты, такие как **Пользователи, находящиеся в группе риска**, **События риска** и **Уязвимости**;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="b4bc1-167">параметры, такие как **Политики безопасности**, **Уведомления** и **Регистрация в многофакторной проверке подлинности**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="b4bc1-168">Обычно с этого и начинается исследование, которое представляет собой проверку действий, журналов и других сведений, относящихся к событию риска, и позволяет принять решение о том, нужно ли исправлять или устранять риски. Оно также помогает понять, как было скомпрометировано удостоверение и как оно после этого использовалось.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="b4bc1-169">Действия по исследованию можно привязать к [уведомлениям](active-directory-identityprotection-notifications.md) , которые отправляет служба защиты идентификации Azure Active Directory по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="b4bc1-170">Следующие разделы содержат дополнительные сведения и шаги, связанные с исследованием.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="b4bc1-171">Вход, представляющий риск</span><span class="sxs-lookup"><span data-stu-id="b4bc1-171">Risky sign-ins</span></span>

<span data-ttu-id="b4bc1-172">Azure Active Directory обнаруживает [типы событий риска](active-directory-reporting-risk-events.md#risk-event-types) в режиме реального времени и в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="b4bc1-173">Все события риска, обнаруженные при входе пользователя в систему, формируют логическое понятие, которое называется "Вход, представляющий риск".</span><span class="sxs-lookup"><span data-stu-id="b4bc1-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="b4bc1-174">Вход, представляющий риск, означает, что в систему пытался войти пользователь, который не является законным владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="b4bc1-175">Уровень риска при входе</span><span class="sxs-lookup"><span data-stu-id="b4bc1-175">Sign-in risk level</span></span>

<span data-ttu-id="b4bc1-176">Уровень риска при входе ("Высокий", "Средний" или "Низкий") указывает насколько вероятно то, что попытка входа выполнена пользователем, который не является законным владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="b4bc1-177">Устранение событий риска при входе</span><span class="sxs-lookup"><span data-stu-id="b4bc1-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="b4bc1-178">Устранение рисков — это действие, позволяющее ограничить возможность использования злоумышленником скомпрометированного удостоверения или устройства без восстановления их безопасного состояния.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="b4bc1-179">Устранение рисков не разрешает предыдущие события риска при входе, связанные с удостоверением или устройством.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="b4bc1-180">Для автоматического устранения проблем с входом, представляющим риск, можно настроить политики безопасности в отношении риска.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="b4bc1-181">С помощью политик можно настроить уровень риска или условия входа, при которых будет блокироваться вход, если он представляет риск, или обязательную многофакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="b4bc1-182">Эти действия могут помешать злоумышленникам использовать украденное удостоверение в преступных целях и позволят выиграть время для защиты удостоверения.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="b4bc1-183">Политика безопасности в отношении риска входа</span><span class="sxs-lookup"><span data-stu-id="b4bc1-183">Sign-in risk security policy</span></span>
<span data-ttu-id="b4bc1-184">Политика риска входа — это политика условного доступа, согласно которой вычисляется уровень риска конкретной попытки входа, а на основе ее предопределенных условий и правил предпринимаются действия для устранения рисков.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="b4bc1-185">![Политика риска входа](./media/active-directory-identityprotection/1014.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="b4bc1-186">Защита идентификации Azure AD облегчает управление устранением рисков при попытке входа и позволяет:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="b4bc1-187">задать пользователей и группы, к которым следует применять политику;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="b4bc1-188">![Политика риска входа](./media/active-directory-identityprotection/1015.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="b4bc1-189">задать пороговое значение уровня риска входа (низкий, средний или высокий уровень), при достижении которого активируется политика;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="b4bc1-190">![Политика риска входа](./media/active-directory-identityprotection/1016.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="b4bc1-191">задать элементы управления, которые будут применяться при активации политики;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="b4bc1-192">![Политика риска входа](./media/active-directory-identityprotection/1017.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="b4bc1-193">переключить состояние политики;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="b4bc1-194">![Регистрация в MFA](./media/active-directory-identityprotection/403.png "Регистрация в MFA")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="b4bc1-195">проверить и оценить влияние изменений до их активации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="b4bc1-196">![Политика риска входа](./media/active-directory-identityprotection/1018.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="b4bc1-197">Это важно знать</span><span class="sxs-lookup"><span data-stu-id="b4bc1-197">What you need to know</span></span>
<span data-ttu-id="b4bc1-198">Вы можете настроить политику риска при входе так, чтобы требовалась многофакторная идентификация.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="b4bc1-199">![Политика риска входа](./media/active-directory-identityprotection/1017.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="b4bc1-200">Однако из соображений безопасности этот параметр действует только для пользователей, уже зарегистрированных для многофакторной идентификации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="b4bc1-201">Если пользователь, еще не зарегистрированный для многофакторной идентификации, соответствует условию, при котором она требуется, этот пользователь блокируется.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="b4bc1-202">Если вы хотите, чтобы во время рискованных входов требовалась многофакторная идентификация, мы рекомендуем сделать так:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="b4bc1-203">Включить [политику регистрации для многофакторной идентификации](#multi-factor-authentication-registration-policy) для нужных пользователей.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="b4bc1-204">Требовать у этих пользователей входить в безопасные сеансы, чтобы регистрироваться для многофакторной идентификации уже в них.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="b4bc1-205">Если вы выполните эти действия, для рискованных входов будет требоваться многофакторная идентификация.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="b4bc1-206">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="b4bc1-206">Best practices</span></span>
<span data-ttu-id="b4bc1-207">Если выбрать пороговое значение уровня **Высокий** , уменьшится количество случаев активации политики и степень влияния на пользователей.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="b4bc1-208">Тем не менее это исключит из политики пользователей, помеченных для событий риска с уровнем **Низкий** и **Средний**. Есть вероятность, что в таком случае злоумышленникам ничего не будет мешать использовать скомпрометированные удостоверения.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="b4bc1-209">При настройке политики:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-209">When setting the policy,</span></span>

* <span data-ttu-id="b4bc1-210">исключите пользователей, которые не используют или не могут использовать многофакторную проверку подлинности;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="b4bc1-211">исключите пользователей, для языкового стандарта которых нецелесообразно включать политику (например, при его использовании недоступна техническая поддержка);</span><span class="sxs-lookup"><span data-stu-id="b4bc1-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="b4bc1-212">исключите пользователей, из-за которых, скорее всего, создается большое количество ложных срабатываний (разработчиков, аналитиков системы безопасности);</span><span class="sxs-lookup"><span data-stu-id="b4bc1-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="b4bc1-213">Используйте пороговое значение уровня **Высокий** при начальном развертывании политики, а также если требуется уменьшить количество запросов защиты для конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="b4bc1-214">Используйте пороговое значение уровня **Низкий**, если нужно повысить уровень безопасности для организации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="b4bc1-215">Если вы выберете пороговое значение уровня **Низкий** , при входе для пользователей будет отображаться больше запросов защиты, но уровень безопасности будет выше.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="b4bc1-216">Большинству организаций мы рекомендуем настроить для правил пороговое значение уровня **Средний** , чтобы обеспечить оптимальное соотношение удобства использования и безопасности.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="b4bc1-217">Политика риска входа:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="b4bc1-218">применяется ко всему трафику в браузере и при каждом входе с использованием современных способов проверки подлинности;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="b4bc1-219">не применяется к приложениям, которые используют протоколы безопасности старых версий, отключая конечную точку WS-Trust в федеративном IdP, таком как ADFS.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="b4bc1-220">В консоли защиты данных на странице **События риска** содержится список всех событий:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="b4bc1-221">к которым применена эта политика;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-221">This policy was applied to</span></span>
* <span data-ttu-id="b4bc1-222">что позволяет просмотреть действие и определить, выполнено ли оно соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="b4bc1-223">Общие сведения о соответствующем взаимодействии с пользователями см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="b4bc1-224">Восстановление входа, представлявшего риск</span><span class="sxs-lookup"><span data-stu-id="b4bc1-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="b4bc1-225">Блокировка входа, представляющего риск</span><span class="sxs-lookup"><span data-stu-id="b4bc1-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* <span data-ttu-id="b4bc1-226">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md) (Процедуры входа с защитой идентификации Azure AD)</span><span class="sxs-lookup"><span data-stu-id="b4bc1-226">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md)</span></span>  

<span data-ttu-id="b4bc1-227">**Вот как можно открыть диалоговое окно настройки**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="b4bc1-228">В колонке **Azure AD Identity Protection** в разделе **Настройка** щелкните **Политика риска для входа в систему**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="b4bc1-229">![Политика риска пользователя](./media/active-directory-identityprotection/1014.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="b4bc1-230">Пользователи, помеченные для события риска</span><span class="sxs-lookup"><span data-stu-id="b4bc1-230">Users flagged for risk</span></span>

<span data-ttu-id="b4bc1-231">Все активные [события риска](active-directory-identity-protection-risk-events.md), обнаруженные Azure Active Directory для отдельных пользователей, формируют логическое понятие, которое называется "Пользователи, находящиеся в группе риска".</span><span class="sxs-lookup"><span data-stu-id="b4bc1-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="b4bc1-232">"Пользователь, находящийся в группе риска" означает, что безопасность учетной записи пользователя, возможно, была нарушена.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Пользователи, помеченные для события риска](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="b4bc1-234">Уровень риска для пользователя</span><span class="sxs-lookup"><span data-stu-id="b4bc1-234">User risk level</span></span>

<span data-ttu-id="b4bc1-235">Уровень риска для пользователя ("Высокий", "Средний" или "Низкий") означает степень вероятности, что его удостоверение скомпрометировано.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="b4bc1-236">Он рассчитывается на основе событий риска для пользователя, связанных с его удостоверением.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="b4bc1-237">У события риска может быть состояние **Активно** или **Закрыто**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="b4bc1-238">При расчете уровня риска для пользователя учитываются только события с состоянием **Активно**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="b4bc1-239">При расчете риска для пользователя также используются следующие входные данные:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="b4bc1-240">активные события риска, влияющие на пользователя;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="b4bc1-241">уровень риска этих событий;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-241">Risk level of these events</span></span>
* <span data-ttu-id="b4bc1-242">факт выполнения или невыполнения действий по исправлению.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="b4bc1-243">![Риски для пользователя](./media/active-directory-identityprotection/1031.png "Риски для пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="b4bc1-244">Уровни риска для пользователя можно использовать, чтобы создать политики условного доступа для блокировки входа пользователей, представляющих риск, или принудительного изменения пароля.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="b4bc1-245">Закрытие событий риска вручную</span><span class="sxs-lookup"><span data-stu-id="b4bc1-245">Closing risk events manually</span></span>

<span data-ttu-id="b4bc1-246">В большинстве случаев, чтобы события риска закрывались автоматически, вы будете использовать такое действие по исправлению, как безопасный сброс пароля.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="b4bc1-247">Однако это действие не всегда можно выполнить.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="b4bc1-248">Например, это происходит, если:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="b4bc1-249">был удален пользователь с активными событиями риска;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="b4bc1-250">исследование показывает, что выявленные события риска произошли в результате действий полномочного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="b4bc1-251">Так как при расчете риска для пользователя учитываются события с состоянием **Активно** , может потребоваться уменьшить уровень риска, вручную закрыв эти события.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="b4bc1-252">В ходе исследования вы можете использовать любое из этих действий, чтобы изменить состояние события риска.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="b4bc1-253">![Действия](./media/active-directory-identityprotection/34.png "Действия")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="b4bc1-254">**Разрешить** — если после исследования события риска вы выполнили соответствующее действие по исправлению вне службы защиты идентификации и считаете, что событие следует закрыть, пометьте его как разрешенное.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="b4bc1-255">Разрешенным событиям риска будет присвоено состояние "Закрыто", и они больше не будут учитываться при расчете риска для пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="b4bc1-256">**Пометить как ложное срабатывание** — иногда в результате исследования событий риска может обнаружиться, что событие помечено по ошибке.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="b4bc1-257">Количество таких вхождений можно уменьшить, пометив события риска как "Ложное срабатывание".</span><span class="sxs-lookup"><span data-stu-id="b4bc1-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="b4bc1-258">Это позволит усовершенствовать классификацию таких событий при использовании алгоритмов машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="b4bc1-259">Состояние событий с ложным срабатыванием изменяется на **Закрыто** , и они больше не учитываются при расчете риска для пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="b4bc1-260">**Пропустить** — если вы не предпринимали действий по исправлению, но хотите удалить события риска из списка активных, можно пометить их, щелкнув "Пропустить", чтобы изменить состояние на "Закрыто".</span><span class="sxs-lookup"><span data-stu-id="b4bc1-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="b4bc1-261">Пропущенные события не влияют на риск для пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="b4bc1-262">Эту возможность следует использовать только при чрезвычайных обстоятельствах.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="b4bc1-263">**Повторно активировать** — события риска, закрытые вручную (если вы щелкнули **Разрешить**, **Ложное срабатывание** или **Пропустить**), можно активировать снова, установив для них состояние **Активно**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="b4bc1-264">Повторно активированные события рисков учитываются при расчете уровня риска для пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="b4bc1-265">События рисков, закрытые вследствие исправления (например, безопасного сброса пароля), нельзя повторно активировать.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="b4bc1-266">**Вот как можно открыть диалоговое окно настройки**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="b4bc1-267">В колонке **Azure AD Identity Protection** в разделе **Исследовать** щелкните **События риска**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="b4bc1-268">![Сброс пароля вручную](./media/active-directory-identityprotection/1002.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="b4bc1-269">В списке **Risk events** (События риска) выберите риск.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="b4bc1-270">![Сброс пароля вручную](./media/active-directory-identityprotection/1003.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="b4bc1-271">В колонке риска щелкните правой кнопкой мыши пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="b4bc1-272">![Сброс пароля вручную](./media/active-directory-identityprotection/1004.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="b4bc1-273">Закрытие всех событий риска для пользователя вручную</span><span class="sxs-lookup"><span data-stu-id="b4bc1-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="b4bc1-274">Вместо закрытия событий риска для пользователя по отдельности защита идентификации Azure Active Directory предоставляет метод, позволяющий закрыть все события для пользователя одним щелчком.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="b4bc1-275">![Действия](./media/active-directory-identityprotection/2222.png "Действия")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="b4bc1-276">При нажатии кнопки **Dismiss all events**(Закрыть все события) закрываются все события и соответствующий пользователь больше не находится под угрозой.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="b4bc1-277">Исправление событий риска для пользователей</span><span class="sxs-lookup"><span data-stu-id="b4bc1-277">Remediating user risk events</span></span>

<span data-ttu-id="b4bc1-278">Исправление — это действие для защиты удостоверения или устройства, которое ранее предположительно или фактически скомпрометировано.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="b4bc1-279">Действие исправления восстанавливает безопасное состояние удостоверения или устройства и разрешает предыдущие события риска, связанные с таким удостоверением или устройством.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="b4bc1-280">Чтобы устранить события риска для пользователя, можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="b4bc1-281">безопасно сбросить пароль, чтобы устранить событие вручную;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="b4bc1-282">настроить политику безопасности в отношении риска для пользователей, чтобы автоматически устранять события или уменьшать их риск;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="b4bc1-283">переустановить систему инфицированного устройства из образа.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="b4bc1-284">Безопасный сброс паролей вручную</span><span class="sxs-lookup"><span data-stu-id="b4bc1-284">Manual secure password reset</span></span>
<span data-ttu-id="b4bc1-285">Безопасный сброс паролей —это эффективный способ исправления многих событий риска. При таком сбросе события автоматически закрываются и происходит перерасчет уровня риска для пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="b4bc1-286">Чтобы инициировать сброс пароля для пользователя с риском, можно использовать панель мониторинга службы защиты идентификации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="b4bc1-287">Соответствующее диалоговое окно предлагает два метода для сброса пароля:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="b4bc1-288">**Сброс пароля**. Установите флажок **Require user to reset their password** (Требовать от пользователя сброс пароля), чтобы разрешить самостоятельное восстановление, если пользователь зарегистрировался для многофакторной идентификации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="b4bc1-289">При следующем входе пользователю будет необходимо пройти многофакторную проверку подлинности по запросу и только потом произойдет принудительное изменения пароля.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="b4bc1-290">Этот параметр будет недоступен, если учетная запись пользователя еще не зарегистрирована для многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="b4bc1-291">**Временный пароль**. Выберите **Создать временный пароль**, чтобы сразу же аннулировать существующий пароль пользователя и создать для него новый временный пароль.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="b4bc1-292">Отправьте новый временный пароль по альтернативному адресу электронной почты пользователя или руководителя пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="b4bc1-293">Так как пароль временный, после входа пользователю будет предложено изменить его.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="b4bc1-294">![Политика](./media/active-directory-identityprotection/1005.png "Политика")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="b4bc1-295">**Вот как можно открыть диалоговое окно настройки**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="b4bc1-296">В колонке **Azure AD Identity Protection** щелкните **Пользователи, находящиеся в группе риска**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="b4bc1-297">![Сброс пароля вручную](./media/active-directory-identityprotection/1006.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="b4bc1-298">В списке пользователей выберите пользователя по крайней мере с одним событием риска.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="b4bc1-299">![Сброс пароля вручную](./media/active-directory-identityprotection/1007.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="b4bc1-300">В колонке пользователя щелкните **Сбросить пароль**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="b4bc1-301">![Сброс пароля вручную](./media/active-directory-identityprotection/1008.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="b4bc1-302">Политика безопасности в отношении риска для пользователя</span><span class="sxs-lookup"><span data-stu-id="b4bc1-302">User risk security policy</span></span>
<span data-ttu-id="b4bc1-303">Политика безопасности в отношении риска для пользователя — это политика условного доступа, согласно которой вычисляется уровень риска для конкретного пользователя, а на основе ее предопределенных условий и правил предпринимаются действия по исправлению и устранению.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="b4bc1-304">![Политика риска пользователя](./media/active-directory-identityprotection/1009.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="b4bc1-305">Служба защиты идентификации Azure AD облегчает управление исправлением и устранением рисков для пользователей, помеченных для событий риска, и позволяет:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="b4bc1-306">задать пользователей и группы, к которым следует применять политику;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="b4bc1-307">![Политика риска пользователя](./media/active-directory-identityprotection/1010.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="b4bc1-308">задать пороговое значение уровня риска для пользователей (низкий, средний или высокий уровень), при достижении которого активируется политика;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="b4bc1-309">![Политика риска пользователя](./media/active-directory-identityprotection/1011.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="b4bc1-310">задать элементы управления, которые будут применяться при активации политики;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="b4bc1-311">![Политика риска пользователя](./media/active-directory-identityprotection/1012.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="b4bc1-312">переключить состояние политики;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="b4bc1-313">![Политика риска пользователя](./media/active-directory-identityprotection/403.png "Регистрация в MFA")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="b4bc1-314">проверить и оценить влияние изменений до их активации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="b4bc1-315">![Политика риска пользователя](./media/active-directory-identityprotection/1013.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="b4bc1-316">Если выбрать пороговое значение уровня **Высокий** , уменьшится количество случаев активации политики и степень влияния на пользователей.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="b4bc1-317">Однако это исключит из политики пользователей, находящихся в группе риска, с уровнем **Низкий** и **Средний**, оставив незащищенными удостоверения и устройства, которые были ранее предположительно или фактически скомпрометированы.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="b4bc1-318">При настройке политики:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-318">When setting the policy,</span></span>

* <span data-ttu-id="b4bc1-319">исключите пользователей, из-за которых, скорее всего, создается большое количество ложных срабатываний (разработчиков, аналитиков системы безопасности);</span><span class="sxs-lookup"><span data-stu-id="b4bc1-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="b4bc1-320">исключите пользователей, для языкового стандарта которых нецелесообразно включать политику (например, при его использовании недоступна техническая поддержка);</span><span class="sxs-lookup"><span data-stu-id="b4bc1-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="b4bc1-321">Используйте пороговое значение уровня **Высокий** при начальном развертывании политики, а также если требуется уменьшить количество запросов защиты для конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="b4bc1-322">Используйте пороговое значение уровня **Низкий** , если нужно повысить уровень безопасности для организации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="b4bc1-323">Если вы выберете пороговое значение уровня **Низкий** , при входе для пользователей будет отображаться больше запросов защиты, но уровень безопасности будет выше.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="b4bc1-324">Большинству организаций мы рекомендуем настроить для правил пороговое значение уровня **Средний** , чтобы обеспечить оптимальное соотношение удобства использования и безопасности.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="b4bc1-325">Общие сведения о соответствующем взаимодействии с пользователями см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="b4bc1-326">[Восстановление скомпрометированной учетной записи](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="b4bc1-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="b4bc1-327">[Скомпрометированная учетная запись заблокирована](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="b4bc1-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="b4bc1-328">**Вот как можно открыть диалоговое окно настройки**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="b4bc1-329">В колонке **Azure AD Identity Protection** в разделе **Настройка** щелкните **Политика риска пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="b4bc1-330">![Политика риска пользователя](./media/active-directory-identityprotection/1009.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="b4bc1-331">Устранение рисков событий для пользователей</span><span class="sxs-lookup"><span data-stu-id="b4bc1-331">Mitigating user risk events</span></span>
<span data-ttu-id="b4bc1-332">При наличии прав администратора в политике безопасности в отношении риска пользователей можно установить блокировку входа на основе уровня риска.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="b4bc1-333">Блокировка входа:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="b4bc1-334">предотвращает создание новых событий риска для каждого затронутого пользователя;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="b4bc1-335">позволяет администраторам вручную устранить события риска, которые распространяются на удостоверение пользователя, и восстанавливать безопасное состояние.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="b4bc1-336">Политика регистрации с многофакторной проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="b4bc1-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="b4bc1-337">Многофакторная идентификация Azure — это метод проверки идентичности пользователя, при котором используются дополнительные средства, а не только имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="b4bc1-338">Это второй уровень безопасности, который применяется для входа пользователя в систему и выполнения транзакций.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="b4bc1-339">Мы советуем настроить обязательную Многофакторную идентификацию Azure при входе пользователей, так как она:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="b4bc1-340">обеспечивает строгую аутентификацию с помощью ряда простых параметров проверки;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="b4bc1-341">играет ключевую роль при подготовке защиты от компрометации, а также восстановления скомпрометированных учетных записей в организации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="b4bc1-342">![Политика риска пользователя](./media/active-directory-identityprotection/1019.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="b4bc1-343">Дополнительные сведения см. в статье [Что такое Azure Multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b4bc1-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="b4bc1-344">Защита идентификации Azure AD облегчает управление развертыванием регистрации с многофакторной проверкой подлинности за счет настройки политики, которая позволяет:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="b4bc1-345">задать пользователей и группы, к которым следует применять политику;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="b4bc1-346">![Политика MFA](./media/active-directory-identityprotection/1020.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="b4bc1-347">задать элементы управления, которые будут применяться при активации политики;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="b4bc1-348">![Политика MFA](./media/active-directory-identityprotection/1021.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="b4bc1-349">переключить состояние политики;</span><span class="sxs-lookup"><span data-stu-id="b4bc1-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="b4bc1-350">![Политика MFA](./media/active-directory-identityprotection/403.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="b4bc1-351">просматривать текущее состояние регистрации.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-351">View the current registration status:</span></span>

    <span data-ttu-id="b4bc1-352">![Политика MFA](./media/active-directory-identityprotection/1022.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="b4bc1-353">Общие сведения о соответствующем взаимодействии с пользователями см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="b4bc1-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="b4bc1-354">[Регистрация с многофакторной проверкой подлинности](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="b4bc1-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="b4bc1-355">[Процедуры входа с защитой идентификации Azure AD](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="b4bc1-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="b4bc1-356">**Вот как можно открыть диалоговое окно настройки**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="b4bc1-357">В колонке **Azure AD Identity Protection** в разделе **Настройка** щелкните **Регистрация в многофакторной проверке подлинности**.</span><span class="sxs-lookup"><span data-stu-id="b4bc1-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="b4bc1-358">![Политика MFA](./media/active-directory-identityprotection/1019.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b4bc1-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4bc1-359">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4bc1-359">Next steps</span></span>
* [<span data-ttu-id="b4bc1-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview (Канал 9. Azure Active Directory и идентификация. Предварительная версия защиты идентификации)</span><span class="sxs-lookup"><span data-stu-id="b4bc1-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="b4bc1-361">Включение защиты идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4bc1-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="b4bc1-362">Уязвимости, обнаруживаемые защитой идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4bc1-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="b4bc1-363">События риска Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4bc1-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="b4bc1-364">Уведомления защиты идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4bc1-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="b4bc1-365">Тренировочное задание по защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4bc1-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="b4bc1-366">Глоссарий по защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4bc1-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* <span data-ttu-id="b4bc1-367">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md) (Процедуры входа с защитой идентификации Azure AD)</span><span class="sxs-lookup"><span data-stu-id="b4bc1-367">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md)</span></span>

* [<span data-ttu-id="b4bc1-368">Защита идентификации Azure Active Directory. Разблокирование пользователей</span><span class="sxs-lookup"><span data-stu-id="b4bc1-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="b4bc1-369">Начало работы с защитой идентификации Azure Active Directory и Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b4bc1-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
