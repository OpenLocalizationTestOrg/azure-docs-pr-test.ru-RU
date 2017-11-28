---
title: "aaaAzure защиты идентификации Active Directory | Документы Microsoft"
description: "Узнайте, как Azure AD Identity Protection делает возможность hello toolimit злоумышленник tooexploit скомпрометированных удостоверения или устройство и toosecure удостоверения или устройства, который ранее был toobe подозреваемое или известных скомпрометирован."
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
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="b02f7-104">Защита идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b02f7-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="b02f7-105">Azure Active Directory Identity Protection — это функция hello Azure AD Premium P2 выпуск, который позволяет:</span><span class="sxs-lookup"><span data-stu-id="b02f7-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="b02f7-106">обнаруживать потенциальные уязвимости, которые могут повлиять на учетные записи организации;</span><span class="sxs-lookup"><span data-stu-id="b02f7-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="b02f7-107">Настроить подозрительные действия toodetected автоматические ответы, которые представляют удостоверения организации связанных tooyour</span><span class="sxs-lookup"><span data-stu-id="b02f7-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="b02f7-108">Проверка подозрительных инцидентов и принимать соответствующие меры tooresolve их</span><span class="sxs-lookup"><span data-stu-id="b02f7-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="b02f7-109">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="b02f7-109">Getting started</span></span>

<span data-ttu-id="b02f7-110">Корпорация Майкрософт более десяти лет обеспечивает безопасность облачной идентификации.</span><span class="sxs-lookup"><span data-stu-id="b02f7-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="b02f7-111">В Azure Active Directory защиту, в вашей среде, можно использовать hello же защиты систем Microsoft использует toosecure удостоверения.</span><span class="sxs-lookup"><span data-stu-id="b02f7-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="b02f7-112">Большинство Hello занять нарушений безопасности разместить, если злоумышленник получает доступ tooan среды, кража удостоверения пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="b02f7-113">За годы hello злоумышленники стали более эффективно использование нарушений сторонних производителей и с помощью сложных фишинг-атаках.</span><span class="sxs-lookup"><span data-stu-id="b02f7-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="b02f7-114">Как только злоумышленник получит доступ tooeven низкий привилегированных учетных записей пользователей, проходит относительно легко их toogain доступ к ресурсам компании tooimportant через боковое смещение.</span><span class="sxs-lookup"><span data-stu-id="b02f7-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="b02f7-115">Поэтому необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b02f7-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="b02f7-116">защитить все удостоверения независимо от их уровня привилегий;</span><span class="sxs-lookup"><span data-stu-id="b02f7-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="b02f7-117">предотвратить злонамеренное использование скомпрометированных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b02f7-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="b02f7-118">Обнаружение скомпрометированных удостоверений — непростая задача.</span><span class="sxs-lookup"><span data-stu-id="b02f7-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="b02f7-119">Azure Active Directory использует адаптивный алгоритмы обучения и аномалий toodetect эвристики и подозрительные инцидентов, которые указывают на потенциально компрометация удостоверения.</span><span class="sxs-lookup"><span data-stu-id="b02f7-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="b02f7-120">С помощью этих данных, защиту учетных данных создает отчеты и оповещения, позволяющие tooevaluate hello обнаружил проблемы и принимать соответствующие Уменьшение или действия по исправлению.</span><span class="sxs-lookup"><span data-stu-id="b02f7-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="b02f7-121">Защита идентификации Azure Active Directory — это больше, чем просто инструмент для мониторинга и создания отчетности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="b02f7-122">tooprotect удостоверения организации, можно настроить политики на основе риска, автоматически ответить toodetected проблем, когда был достигнут уровень риска указанного.</span><span class="sxs-lookup"><span data-stu-id="b02f7-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="b02f7-123">Эти политики в дополнение к этому tooother условного доступа к элементам управления, предоставляемые Azure Active Directory и EMS, можно автоматически блокировать или инициировать адаптивной исправления действий, включая сброс пароля и принудительного применения многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="b02f7-124">Возможности защиты идентификации</span><span class="sxs-lookup"><span data-stu-id="b02f7-124">Identity Protection capabilities</span></span>

<span data-ttu-id="b02f7-125">**Обнаружение уязвимостей и учетных записей, подверженных риску:**</span><span class="sxs-lookup"><span data-stu-id="b02f7-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="b02f7-126">Предоставление пользовательских рекомендации tooimprove общего уровня безопасности с помощью выделения уязвимостей</span><span class="sxs-lookup"><span data-stu-id="b02f7-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="b02f7-127">расчет уровня риска при входе;</span><span class="sxs-lookup"><span data-stu-id="b02f7-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="b02f7-128">расчет уровня риска для пользователя;</span><span class="sxs-lookup"><span data-stu-id="b02f7-128">Calculating user risk levels</span></span>


<span data-ttu-id="b02f7-129">**Исследование событий риска:**</span><span class="sxs-lookup"><span data-stu-id="b02f7-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="b02f7-130">отправка уведомлений о событиях риска;</span><span class="sxs-lookup"><span data-stu-id="b02f7-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="b02f7-131">исследование событий риска на основе соответствующей и контекстной информации;</span><span class="sxs-lookup"><span data-stu-id="b02f7-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="b02f7-132">Предоставление основных рабочих tootrack исследования</span><span class="sxs-lookup"><span data-stu-id="b02f7-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="b02f7-133">Обеспечивает легкий доступ tooremediation действий, таких как сброс пароля</span><span class="sxs-lookup"><span data-stu-id="b02f7-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="b02f7-134">**Политики условного доступа на основе рисков:**</span><span class="sxs-lookup"><span data-stu-id="b02f7-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="b02f7-135">Политика toomitigate рискованным входа в систему по блокировки входа в систему или необходима проблем многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="b02f7-136">Политика tooblock или безопасные рискованным учетных записей</span><span class="sxs-lookup"><span data-stu-id="b02f7-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="b02f7-137">Tooregister пользователи toorequire политики многофакторной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="b02f7-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="b02f7-138">Роли защиты идентификации</span><span class="sxs-lookup"><span data-stu-id="b02f7-138">Identity Protection roles</span></span>

<span data-ttu-id="b02f7-139">tooload баланс hello действия по управлению вокруг реализации защиту учетных данных, можно назначить несколько ролей.</span><span class="sxs-lookup"><span data-stu-id="b02f7-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="b02f7-140">Служба защиты идентификации Azure AD поддерживает три роли каталога:</span><span class="sxs-lookup"><span data-stu-id="b02f7-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="b02f7-141">Роль</span><span class="sxs-lookup"><span data-stu-id="b02f7-141">Role</span></span>                         | <span data-ttu-id="b02f7-142">Может</span><span class="sxs-lookup"><span data-stu-id="b02f7-142">Can do</span></span>                          | <span data-ttu-id="b02f7-143">Не может</span><span class="sxs-lookup"><span data-stu-id="b02f7-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="b02f7-144">Глобальный администратор</span><span class="sxs-lookup"><span data-stu-id="b02f7-144">Global administrator</span></span>         | <span data-ttu-id="b02f7-145">Полный доступ tooIdentity защиты, встроенной защиты идентификации</span><span class="sxs-lookup"><span data-stu-id="b02f7-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="b02f7-146">администратор безопасности;</span><span class="sxs-lookup"><span data-stu-id="b02f7-146">Security administrator</span></span>       | <span data-ttu-id="b02f7-147">Полный доступ tooIdentity защиты</span><span class="sxs-lookup"><span data-stu-id="b02f7-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="b02f7-148">Встроенная защита идентификации, сброс паролей для пользователя</span><span class="sxs-lookup"><span data-stu-id="b02f7-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="b02f7-149">Читатель безопасности</span><span class="sxs-lookup"><span data-stu-id="b02f7-149">Security reader</span></span>              | <span data-ttu-id="b02f7-150">Доступ только для чтения tooIdentity защиты</span><span class="sxs-lookup"><span data-stu-id="b02f7-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="b02f7-151">Встроенная защита идентификации, исправление пользователей, настройка политик, сброс паролей</span><span class="sxs-lookup"><span data-stu-id="b02f7-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="b02f7-152">См. дополнительные сведения о [назначении ролей администратора в Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b02f7-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="b02f7-153">Обнаружение</span><span class="sxs-lookup"><span data-stu-id="b02f7-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="b02f7-154">Уязвимости</span><span class="sxs-lookup"><span data-stu-id="b02f7-154">Vulnerabilities</span></span>

<span data-ttu-id="b02f7-155">Защита идентификации Azure Active Directory анализирует вашу конфигурацию и обнаруживает уязвимости, которые могут повлиять на безопасность ваших пользовательских удостоверений.</span><span class="sxs-lookup"><span data-stu-id="b02f7-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="b02f7-156">Дополнительные сведения см. в статье [Уязвимости, обнаруживаемые защитой идентификации Azure Active Directory](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="b02f7-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="b02f7-157">События риска</span><span class="sxs-lookup"><span data-stu-id="b02f7-157">Risk events</span></span>

<span data-ttu-id="b02f7-158">Azure Active Directory использует адаптивный машинного обучения алгоритмов и эвристики toodetect подозрительные действия, которые являются удостоверения tooyour связанных пользователей.</span><span class="sxs-lookup"><span data-stu-id="b02f7-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="b02f7-159">Hello система создает запись для каждого обнаруженного подозрительные действия.</span><span class="sxs-lookup"><span data-stu-id="b02f7-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="b02f7-160">Эти записи также известны как события риска.</span><span class="sxs-lookup"><span data-stu-id="b02f7-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="b02f7-161">Дополнительные сведения см. в статье о [событиях риска Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="b02f7-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="b02f7-162">Исследование</span><span class="sxs-lookup"><span data-stu-id="b02f7-162">Investigation</span></span>
<span data-ttu-id="b02f7-163">Радостью через защиту учетных данных обычно начинается с панели мониторинга hello защиту учетных данных.</span><span class="sxs-lookup"><span data-stu-id="b02f7-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="b02f7-164">![Исправление](./media/active-directory-identityprotection/1000.png "Исправление")</span><span class="sxs-lookup"><span data-stu-id="b02f7-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="b02f7-165">панель мониторинга Hello дает доступ к:</span><span class="sxs-lookup"><span data-stu-id="b02f7-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="b02f7-166">отчеты, такие как **Пользователи, находящиеся в группе риска**, **События риска** и **Уязвимости**;</span><span class="sxs-lookup"><span data-stu-id="b02f7-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="b02f7-167">Параметры, такие как конфигурация hello вашей **политики безопасности**, **уведомления** и **регистрации многофакторной проверки подлинности**</span><span class="sxs-lookup"><span data-stu-id="b02f7-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="b02f7-168">Обычно является отправной точкой для исследования, являющийся hello процесс проверки действия hello, журналы и другие важные сведения, связанные tooa риск событие toodecide ли исправление или устранения действий, необходимых, и каким образом было hello удостоверений нарушения безопасности, а также понять, как hello скомпрометированы удостоверение использовалось.</span><span class="sxs-lookup"><span data-stu-id="b02f7-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="b02f7-169">Позволяет связать ваш toohello расследования действия [уведомления](active-directory-identityprotection-notifications.md) Azure Active Directory Protection отправляет по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="b02f7-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="b02f7-170">Hello следующих разделах получить дополнительные сведения и шаги hello, исследование связанных tooan.</span><span class="sxs-lookup"><span data-stu-id="b02f7-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="b02f7-171">Вход, представляющий риск</span><span class="sxs-lookup"><span data-stu-id="b02f7-171">Risky sign-ins</span></span>

<span data-ttu-id="b02f7-172">Azure Active Directory обнаруживает [типы событий риска](active-directory-reporting-risk-events.md#risk-event-types) в режиме реального времени и в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="b02f7-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="b02f7-173">Каждому событию риска, обнаруженной при входе в систему пользователя способствует tooa логическое понятие, вызывается рискованным вход.</span><span class="sxs-lookup"><span data-stu-id="b02f7-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="b02f7-174">Рискованные вход является показателем для попытки входа в систему, может не быть выполнено hello законный владелец учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="b02f7-175">Уровень риска при входе</span><span class="sxs-lookup"><span data-stu-id="b02f7-175">Sign-in risk level</span></span>

<span data-ttu-id="b02f7-176">Уровень риска вход свидетельствует о (высокий, средний или низкий) вероятности hello попытки входа не выполнено hello законный владелец учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="b02f7-177">Устранение событий риска при входе</span><span class="sxs-lookup"><span data-stu-id="b02f7-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="b02f7-178">Устранение рисков — действие toolimit hello способность устройству злоумышленник tooexploit скомпрометированных удостоверения или без восстановления hello удостоверения или tooa безопасном состояние устройства.</span><span class="sxs-lookup"><span data-stu-id="b02f7-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="b02f7-179">Исправление не устраняет предыдущих вход риск события, связанные с hello удостоверения или устройства.</span><span class="sxs-lookup"><span data-stu-id="b02f7-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="b02f7-180">toomitigate рискованным вход автоматически, можно настроить policicies входа риск безопасности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="b02f7-181">С помощью этих политик, рассмотрим уровень риска hello hello пользователя или hello вход tooblock рискованным входа в систему или требовать hello пользователя tooperform многофакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="b02f7-182">Эти действия может не дать злоумышленнику использовать повреждения toocause украденного удостоверения и могут предоставить определенное время toosecure hello удостоверение.</span><span class="sxs-lookup"><span data-stu-id="b02f7-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="b02f7-183">Политика безопасности в отношении риска входа</span><span class="sxs-lookup"><span data-stu-id="b02f7-183">Sign-in risk security policy</span></span>
<span data-ttu-id="b02f7-184">Политика входа риска — политику условного доступа, которая вычисляет hello риск tooa конкретных вход и применяет исправления на основе предопределенных условий и правил.</span><span class="sxs-lookup"><span data-stu-id="b02f7-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="b02f7-185">![Политика риска входа](./media/active-directory-identityprotection/1014.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b02f7-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="b02f7-186">Azure AD Identity Protection помогает управлять hello Предотвращение рискованным входа в систему, позволяя:</span><span class="sxs-lookup"><span data-stu-id="b02f7-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="b02f7-187">Набор hello пользователей и групп hello политика применяется к:</span><span class="sxs-lookup"><span data-stu-id="b02f7-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="b02f7-188">![Политика риска входа](./media/active-directory-identityprotection/1015.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b02f7-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="b02f7-189">Задать hello вход риск пороговых значений (низкий, средний и высокий), запускающее hello политики:</span><span class="sxs-lookup"><span data-stu-id="b02f7-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="b02f7-190">![Политика риска входа](./media/active-directory-identityprotection/1016.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b02f7-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="b02f7-191">Набор hello элементы управления toobe применяются при hello политики:</span><span class="sxs-lookup"><span data-stu-id="b02f7-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="b02f7-192">![Политика риска входа](./media/active-directory-identityprotection/1017.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b02f7-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="b02f7-193">Переключение состояния hello политики:</span><span class="sxs-lookup"><span data-stu-id="b02f7-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="b02f7-194">![Регистрация в MFA](./media/active-directory-identityprotection/403.png "Регистрация в MFA")</span><span class="sxs-lookup"><span data-stu-id="b02f7-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="b02f7-195">Проверка и оценка влияния изменений перед ее активацией hello:</span><span class="sxs-lookup"><span data-stu-id="b02f7-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="b02f7-196">![Политика риска входа](./media/active-directory-identityprotection/1018.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b02f7-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="b02f7-197">Что необходимо tooknow</span><span class="sxs-lookup"><span data-stu-id="b02f7-197">What you need tooknow</span></span>
<span data-ttu-id="b02f7-198">Можно настроить вход риск безопасности политики toorequire многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="b02f7-199">![Политика риска входа](./media/active-directory-identityprotection/1017.png "Политика риска входа")</span><span class="sxs-lookup"><span data-stu-id="b02f7-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="b02f7-200">Однако из соображений безопасности этот параметр действует только для пользователей, уже зарегистрированных для многофакторной идентификации.</span><span class="sxs-lookup"><span data-stu-id="b02f7-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="b02f7-201">Если hello условие toorequire многофакторная проверка подлинности выполняется для пользователя, который еще не зарегистрирован для многофакторной проверки подлинности, пользователь hello заблокирован.</span><span class="sxs-lookup"><span data-stu-id="b02f7-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="b02f7-202">Рекомендуется Если требуется, чтобы toorequire многофакторной проверки подлинности для рискованных входа в систему, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b02f7-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="b02f7-203">Включить hello [политики регистрации многофакторной проверки подлинности](#multi-factor-authentication-registration-policy) для hello влияет на пользователей.</span><span class="sxs-lookup"><span data-stu-id="b02f7-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="b02f7-204">Требовать hello затронутые пользователи toologin в tooperform-рискованным сеанса регистрации многофакторной проверки Подлинности</span><span class="sxs-lookup"><span data-stu-id="b02f7-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="b02f7-205">Если вы выполните эти действия, для рискованных входов будет требоваться многофакторная идентификация.</span><span class="sxs-lookup"><span data-stu-id="b02f7-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="b02f7-206">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="b02f7-206">Best practices</span></span>
<span data-ttu-id="b02f7-207">Выбор **высокой** hello число политика запускается и сводит к минимуму влияние toousers hello уменьшает пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="b02f7-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="b02f7-208">Тем не менее, он исключает **Low** и **Средний** входа в систему с отметкой риску hello политику, которая не может блокировать злоумышленнику использовать скомпрометированных удостоверение с.</span><span class="sxs-lookup"><span data-stu-id="b02f7-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="b02f7-209">Если параметр hello политики,</span><span class="sxs-lookup"><span data-stu-id="b02f7-209">When setting hello policy,</span></span>

* <span data-ttu-id="b02f7-210">исключите пользователей, которые не используют или не могут использовать многофакторную проверку подлинности;</span><span class="sxs-lookup"><span data-stu-id="b02f7-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="b02f7-211">Исключить пользователей в регионах, где Включение политики hello не имеет смысла (например toohelpdesk нет доступа)</span><span class="sxs-lookup"><span data-stu-id="b02f7-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="b02f7-212">Исключить пользователей, которые, скорее всего, toogenerate много ложных срабатываний (разработчикам, аналитикам в области безопасности)</span><span class="sxs-lookup"><span data-stu-id="b02f7-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="b02f7-213">Используйте пороговое значение уровня **Высокий** при начальном развертывании политики, а также если требуется уменьшить количество запросов защиты для конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="b02f7-214">Используйте пороговое значение уровня **Низкий**, если нужно повысить уровень безопасности для организации.</span><span class="sxs-lookup"><span data-stu-id="b02f7-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="b02f7-215">Если вы выберете пороговое значение уровня **Низкий** , при входе для пользователей будет отображаться больше запросов защиты, но уровень безопасности будет выше.</span><span class="sxs-lookup"><span data-stu-id="b02f7-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="b02f7-216">Рекомендуется использовать по умолчанию для большинства организаций tooconfigure правило для Hello **Средний** пороговое значение toostrike баланс между простотой использования и безопасности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="b02f7-217">политика входа риск Hello —.</span><span class="sxs-lookup"><span data-stu-id="b02f7-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="b02f7-218">Примененные tooall браузера трафик и входа в систему с помощью современную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="b02f7-219">С помощью более старые протоколы безопасности, отключив конечную точку WS-Trust hello по hello федеративных Удостоверений, например служб федерации Active Directory не применяются tooapplications.</span><span class="sxs-lookup"><span data-stu-id="b02f7-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="b02f7-220">Hello **событий риска** hello защиты идентификации консоли отображаются все события:</span><span class="sxs-lookup"><span data-stu-id="b02f7-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="b02f7-221">к которым применена эта политика;</span><span class="sxs-lookup"><span data-stu-id="b02f7-221">This policy was applied to</span></span>
* <span data-ttu-id="b02f7-222">Можно просмотреть действия hello и определить, успешно ли действие hello соответствующие</span><span class="sxs-lookup"><span data-stu-id="b02f7-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="b02f7-223">Общие сведения о hello связанных взаимодействие с пользователем, в разделе:</span><span class="sxs-lookup"><span data-stu-id="b02f7-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="b02f7-224">Восстановление входа, представлявшего риск</span><span class="sxs-lookup"><span data-stu-id="b02f7-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="b02f7-225">Блокировка входа, представляющего риск</span><span class="sxs-lookup"><span data-stu-id="b02f7-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* <span data-ttu-id="b02f7-226">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md) (Процедуры входа с защитой идентификации Azure AD)</span><span class="sxs-lookup"><span data-stu-id="b02f7-226">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md)</span></span>  

<span data-ttu-id="b02f7-227">**диалоговое окно конфигурации hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="b02f7-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="b02f7-228">На hello **Azure AD Identity Protection** колонки в hello **Настройка** щелкните **входа политики риск**.</span><span class="sxs-lookup"><span data-stu-id="b02f7-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="b02f7-229">![Политика риска пользователя](./media/active-directory-identityprotection/1014.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="b02f7-230">Пользователи, находящиеся в группе риска</span><span class="sxs-lookup"><span data-stu-id="b02f7-230">Users flagged for risk</span></span>

<span data-ttu-id="b02f7-231">Все активные [риск события](active-directory-identity-protection-risk-events.md) обнаружены службой Azure Active Directory для tooa логическое понятие, именем пользователя риск участие пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="b02f7-232">"Пользователь, находящийся в группе риска" означает, что безопасность учетной записи пользователя, возможно, была нарушена.</span><span class="sxs-lookup"><span data-stu-id="b02f7-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Пользователи, находящиеся в группе риска](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="b02f7-234">Уровень риска для пользователя</span><span class="sxs-lookup"><span data-stu-id="b02f7-234">User risk level</span></span>

<span data-ttu-id="b02f7-235">Уровень риска пользователя является признаком (высокий, средний или низкий) hello вероятность компрометации удостоверение пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b02f7-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="b02f7-236">Она рассчитывается на основе hello события пользователя рисков, связанных с удостоверением пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="b02f7-237">Hello события риска имеет состояние **Active** или **закрыто**.</span><span class="sxs-lookup"><span data-stu-id="b02f7-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="b02f7-238">Риск событий, которые являются только **Active** участие toohello пользователя риск уровня вычислений.</span><span class="sxs-lookup"><span data-stu-id="b02f7-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="b02f7-239">уровень риска Hello пользователя вычисляется с помощью hello следующие входные данные:</span><span class="sxs-lookup"><span data-stu-id="b02f7-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="b02f7-240">Активный риск события, влияющие на пользователя hello</span><span class="sxs-lookup"><span data-stu-id="b02f7-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="b02f7-241">уровень риска этих событий;</span><span class="sxs-lookup"><span data-stu-id="b02f7-241">Risk level of these events</span></span>
* <span data-ttu-id="b02f7-242">факт выполнения или невыполнения действий по исправлению.</span><span class="sxs-lookup"><span data-stu-id="b02f7-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="b02f7-243">![Риски для пользователя](./media/active-directory-identityprotection/1031.png "Риски для пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="b02f7-244">Используйте hello пользователя риск уровни toocreate политики условного доступа, блокирующие рискованным пользователям входить в или применения к ним toosecurely изменить свой пароль.</span><span class="sxs-lookup"><span data-stu-id="b02f7-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="b02f7-245">Закрытие событий риска вручную</span><span class="sxs-lookup"><span data-stu-id="b02f7-245">Closing risk events manually</span></span>

<span data-ttu-id="b02f7-246">В большинстве случаев действия по исправлению займет такие, как события закрытия риска tooautomatically сброса надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="b02f7-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="b02f7-247">Однако это действие не всегда можно выполнить.</span><span class="sxs-lookup"><span data-stu-id="b02f7-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="b02f7-248">Это, например, hello случай, когда:</span><span class="sxs-lookup"><span data-stu-id="b02f7-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="b02f7-249">был удален пользователь с активными событиями риска;</span><span class="sxs-lookup"><span data-stu-id="b02f7-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="b02f7-250">Расследование показывает, что события отчета риска имеет было выполнять законным пользователем hello</span><span class="sxs-lookup"><span data-stu-id="b02f7-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="b02f7-251">Поскольку события рисков, которые **Active** участие вычисления риск toohello пользователя, может иметь toomanually понизить уровень риска, закрыв событий риска вручную.</span><span class="sxs-lookup"><span data-stu-id="b02f7-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="b02f7-252">Ходе hello расследования можно выбрать tootake любой из этих действий статус hello toochange события риска:</span><span class="sxs-lookup"><span data-stu-id="b02f7-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="b02f7-253">![Действия](./media/active-directory-identityprotection/34.png "Действия")</span><span class="sxs-lookup"><span data-stu-id="b02f7-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="b02f7-254">**Разрешить** — Если после изучения события риска, были выполнены соответствующие действия за пределами защиты идентификации, но вы уверены, что следует учитывать риск события hello закрыто, событие hello пометить как разрешено.</span><span class="sxs-lookup"><span data-stu-id="b02f7-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="b02f7-255">Разрешить события будет установлен tooClosed состояние события риска hello и события риска hello больше не будет передавать toouser риска.</span><span class="sxs-lookup"><span data-stu-id="b02f7-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="b02f7-256">**Пометить как ложное срабатывание** — иногда в результате исследования событий риска может обнаружиться, что событие помечено по ошибке.</span><span class="sxs-lookup"><span data-stu-id="b02f7-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="b02f7-257">Можно уменьшить количество hello таких ситуаций, пометив события риска hello как ложное.</span><span class="sxs-lookup"><span data-stu-id="b02f7-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="b02f7-258">Это поможет hello машинного обучения классификации hello tooimprove алгоритмы схожих событий в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="b02f7-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="b02f7-259">состояние Hello ложных событий является слишком**закрыто** и они больше не будет передавать toouser риска.</span><span class="sxs-lookup"><span data-stu-id="b02f7-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="b02f7-260">**Игнорировать** — Если вы не предпримете никаких действий для исправления, но, чтобы hello toobe событий риска, удален из активного списка hello, можно пометить события риска Ignore и состояние события hello будут закрыты.</span><span class="sxs-lookup"><span data-stu-id="b02f7-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="b02f7-261">Игнорируется события не влияют toouser риска.</span><span class="sxs-lookup"><span data-stu-id="b02f7-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="b02f7-262">Эту возможность следует использовать только при чрезвычайных обстоятельствах.</span><span class="sxs-lookup"><span data-stu-id="b02f7-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="b02f7-263">**Повторная активация** -риска события, которые были закрыты вручную (, выбрав **Разрешить**, **ложный положительный результат**, или **Ignore**) могут быть повторно активированы, установка hello состояние события резервное слишком**Active**.</span><span class="sxs-lookup"><span data-stu-id="b02f7-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="b02f7-264">События Возобновленные рисков contribute toohello пользователя риск уровня вычислений.</span><span class="sxs-lookup"><span data-stu-id="b02f7-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="b02f7-265">События рисков, закрытые вследствие исправления (например, безопасного сброса пароля), нельзя повторно активировать.</span><span class="sxs-lookup"><span data-stu-id="b02f7-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="b02f7-266">**диалоговое окно конфигурации hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="b02f7-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="b02f7-267">На hello **Azure AD Identity Protection** колонки в разделе **проанализируйте**, нажмите кнопку **риск события**.</span><span class="sxs-lookup"><span data-stu-id="b02f7-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="b02f7-268">![Сброс пароля вручную](./media/active-directory-identityprotection/1002.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b02f7-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="b02f7-269">В hello **риск события** выберите риска.</span><span class="sxs-lookup"><span data-stu-id="b02f7-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="b02f7-270">![Сброс пароля вручную](./media/active-directory-identityprotection/1003.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b02f7-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="b02f7-271">В колонке риск hello щелкните правой кнопкой мыши пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="b02f7-272">![Сброс пароля вручную](./media/active-directory-identityprotection/1004.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b02f7-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="b02f7-273">Закрытие всех событий риска для пользователя вручную</span><span class="sxs-lookup"><span data-stu-id="b02f7-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="b02f7-274">Вместо закрытие события рисков для пользователя по отдельности, Azure Active Directory Identity Protection также предоставляет tooclose метода все события для пользователя с одним щелчком мыши.</span><span class="sxs-lookup"><span data-stu-id="b02f7-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="b02f7-275">![Действия](./media/active-directory-identityprotection/2222.png "Действия")</span><span class="sxs-lookup"><span data-stu-id="b02f7-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="b02f7-276">При нажатии кнопки **закрыть все события**, закрываются все события и hello влияет пользователь больше не находятся под угрозой.</span><span class="sxs-lookup"><span data-stu-id="b02f7-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="b02f7-277">Исправление событий риска для пользователей</span><span class="sxs-lookup"><span data-stu-id="b02f7-277">Remediating user risk events</span></span>

<span data-ttu-id="b02f7-278">Исправление является toosecure действие удостоверения или устройства, которое ранее подозревается или известные toobe скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="b02f7-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="b02f7-279">Действие исправления восстанавливает hello удостоверения или tooa безопасном состояние устройства и разрешает предыдущих риск события, связанные с hello удостоверения или устройства.</span><span class="sxs-lookup"><span data-stu-id="b02f7-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="b02f7-280">события риск tooremediate пользователя, можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="b02f7-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="b02f7-281">Вручную выполните события риск сброса tooremediate безопасного пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="b02f7-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="b02f7-282">Настройка пользователя риск безопасности политики toomitigate или автоматически устранять событий риска пользователя</span><span class="sxs-lookup"><span data-stu-id="b02f7-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="b02f7-283">Восстановление образа hello зараженных устройств</span><span class="sxs-lookup"><span data-stu-id="b02f7-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="b02f7-284">Безопасный сброс паролей вручную</span><span class="sxs-lookup"><span data-stu-id="b02f7-284">Manual secure password reset</span></span>
<span data-ttu-id="b02f7-285">Сброс безопасного пароля действующие исправления для многих событий риска и при выполнении автоматически закрывает эти события рисков и повторно вычисляет уровень риска hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="b02f7-286">Можно использовать hello защиты идентификации мониторинга tooinitiate сброс пароля для рискованных пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="b02f7-287">Hello диалоговым предоставляет два различных методов tooreset пароль:</span><span class="sxs-lookup"><span data-stu-id="b02f7-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="b02f7-288">**Сброс пароля** — выберите **требуется пароль пользователя tooreset hello** tooallow hello пользователя tooself восстановить, если hello пользователь зарегистрировал многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="b02f7-289">Во время приветствия пользователя в следующем входе в систему hello пользователь получит необходимые toosolve многофакторной проверки подлинности запрос успешно и затем, принудительная toochange hello пароль.</span><span class="sxs-lookup"><span data-stu-id="b02f7-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="b02f7-290">Этот параметр недоступен, если учетная запись пользователя hello еще не зарегистрированных многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="b02f7-291">**Временный пароль** — выберите **создания временного пароля** tooimmediately сделать недействительным существующий пароль hello и создайте новый временный пароль для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b02f7-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="b02f7-292">Отправьте hello новый временный пароль tooan запасной адрес электронной почты для пользователя hello или toohello руководителя пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="b02f7-293">Так как пароль hello является временным, hello пользователя будет запрашиваемые toochange hello пароля при входе.</span><span class="sxs-lookup"><span data-stu-id="b02f7-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="b02f7-294">![Политика](./media/active-directory-identityprotection/1005.png "Политика")</span><span class="sxs-lookup"><span data-stu-id="b02f7-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="b02f7-295">**диалоговое окно конфигурации hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="b02f7-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="b02f7-296">На hello **Azure AD Identity Protection** колонка, щелкните **пользователей с отметкой риск**.</span><span class="sxs-lookup"><span data-stu-id="b02f7-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="b02f7-297">![Сброс пароля вручную](./media/active-directory-identityprotection/1006.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b02f7-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="b02f7-298">Из списка hello пользователей выберите пользователя с событиями, по крайней мере один риск.</span><span class="sxs-lookup"><span data-stu-id="b02f7-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="b02f7-299">![Сброс пароля вручную](./media/active-directory-identityprotection/1007.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b02f7-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="b02f7-300">В колонке hello пользователя, нажмите кнопку **сброс пароля**.</span><span class="sxs-lookup"><span data-stu-id="b02f7-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="b02f7-301">![Сброс пароля вручную](./media/active-directory-identityprotection/1008.png "Сброс пароля вручную")</span><span class="sxs-lookup"><span data-stu-id="b02f7-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="b02f7-302">Политика безопасности в отношении риска для пользователя</span><span class="sxs-lookup"><span data-stu-id="b02f7-302">User risk security policy</span></span>
<span data-ttu-id="b02f7-303">Политика безопасности пользователя риск представляет политику условного доступа, которая вычисляет hello риск уровня tooa конкретного пользователя и применяет исправления и уменьшение действия в зависимости от предопределенных условий и правил.</span><span class="sxs-lookup"><span data-stu-id="b02f7-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="b02f7-304">![Политика риска пользователя](./media/active-directory-identityprotection/1009.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="b02f7-305">Azure AD Identity Protection помогает управлять уменьшение hello и исправления, отмеченные для риска, позволяя пользователей:</span><span class="sxs-lookup"><span data-stu-id="b02f7-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="b02f7-306">Набор hello пользователей и групп hello политика применяется к:</span><span class="sxs-lookup"><span data-stu-id="b02f7-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="b02f7-307">![Политика риска пользователя](./media/active-directory-identityprotection/1010.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="b02f7-308">Задать hello риск уровня порог пользователей (низкий, средний и высокий), запускающее hello политики:</span><span class="sxs-lookup"><span data-stu-id="b02f7-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="b02f7-309">![Политика риска пользователя](./media/active-directory-identityprotection/1011.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="b02f7-310">Набор hello элементы управления toobe применяются при hello политики:</span><span class="sxs-lookup"><span data-stu-id="b02f7-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="b02f7-311">![Политика риска пользователя](./media/active-directory-identityprotection/1012.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="b02f7-312">Переключение состояния hello политики:</span><span class="sxs-lookup"><span data-stu-id="b02f7-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="b02f7-313">![Политика риска пользователя](./media/active-directory-identityprotection/403.png "Регистрация в MFA")</span><span class="sxs-lookup"><span data-stu-id="b02f7-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="b02f7-314">Проверка и оценка влияния изменений перед ее активацией hello:</span><span class="sxs-lookup"><span data-stu-id="b02f7-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="b02f7-315">![Политика риска пользователя](./media/active-directory-identityprotection/1013.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="b02f7-316">Выбор **высокой** hello число политика запускается и сводит к минимуму влияние toousers hello уменьшает пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="b02f7-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="b02f7-317">Тем не менее, он исключает **Low** и **Средний** пользователей, помеченных для риску hello политику, которая может не обеспечить защиту идентификаторов или устройства, были ранее подозревается или известно toobe скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="b02f7-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="b02f7-318">Если параметр hello политики,</span><span class="sxs-lookup"><span data-stu-id="b02f7-318">When setting hello policy,</span></span>

* <span data-ttu-id="b02f7-319">Исключить пользователей, которые, скорее всего, toogenerate много ложных срабатываний (разработчикам, аналитикам в области безопасности)</span><span class="sxs-lookup"><span data-stu-id="b02f7-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="b02f7-320">Исключить пользователей в регионах, где Включение политики hello не имеет смысла (например toohelpdesk нет доступа)</span><span class="sxs-lookup"><span data-stu-id="b02f7-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="b02f7-321">Используйте пороговое значение уровня **Высокий** при начальном развертывании политики, а также если требуется уменьшить количество запросов защиты для конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b02f7-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="b02f7-322">Используйте пороговое значение уровня **Низкий** , если нужно повысить уровень безопасности для организации.</span><span class="sxs-lookup"><span data-stu-id="b02f7-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="b02f7-323">Если вы выберете пороговое значение уровня **Низкий** , при входе для пользователей будет отображаться больше запросов защиты, но уровень безопасности будет выше.</span><span class="sxs-lookup"><span data-stu-id="b02f7-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="b02f7-324">Рекомендуется использовать по умолчанию для большинства организаций tooconfigure правило для Hello **Средний** пороговое значение toostrike баланс между простотой использования и безопасности.</span><span class="sxs-lookup"><span data-stu-id="b02f7-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="b02f7-325">Общие сведения о hello связанных взаимодействие с пользователем, в разделе:</span><span class="sxs-lookup"><span data-stu-id="b02f7-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="b02f7-326">[Восстановление скомпрометированной учетной записи](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="b02f7-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="b02f7-327">[Скомпрометированная учетная запись заблокирована](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="b02f7-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="b02f7-328">**диалоговое окно конфигурации hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="b02f7-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="b02f7-329">На hello **Azure AD Identity Protection** колонки в hello **Настройка** щелкните **риск политика пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b02f7-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="b02f7-330">![Политика риска пользователя](./media/active-directory-identityprotection/1009.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="b02f7-331">Устранение рисков событий для пользователей</span><span class="sxs-lookup"><span data-stu-id="b02f7-331">Mitigating user risk events</span></span>
<span data-ttu-id="b02f7-332">Администратор может настроить риск безопасности политики tooblock пользователей при входе в зависимости от уровня риска hello.</span><span class="sxs-lookup"><span data-stu-id="b02f7-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="b02f7-333">Блокировка входа:</span><span class="sxs-lookup"><span data-stu-id="b02f7-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="b02f7-334">Не удается создать hello новых событий риска пользователя для пользователя затронутых hello</span><span class="sxs-lookup"><span data-stu-id="b02f7-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="b02f7-335">Позволяет администраторам toomanually исправлять hello риск событиях, влияющих на удостоверения пользователя hello и восстановить его в безопасном состоянии tooa</span><span class="sxs-lookup"><span data-stu-id="b02f7-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="b02f7-336">Политика регистрации с многофакторной проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="b02f7-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="b02f7-337">Azure многофакторной проверки подлинности — это метод проверки того пользователя, который требует использования hello не только имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="b02f7-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="b02f7-338">Он предоставляет дополнительный уровень безопасности toouser входа и транзакций.</span><span class="sxs-lookup"><span data-stu-id="b02f7-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="b02f7-339">Мы советуем настроить обязательную Многофакторную идентификацию Azure при входе пользователей, так как она:</span><span class="sxs-lookup"><span data-stu-id="b02f7-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="b02f7-340">обеспечивает строгую аутентификацию с помощью ряда простых параметров проверки;</span><span class="sxs-lookup"><span data-stu-id="b02f7-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="b02f7-341">Играет ключевую роль в подготовке tooprotect вашей организации и ее восстановление взлом учетной записи</span><span class="sxs-lookup"><span data-stu-id="b02f7-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="b02f7-342">![Политика риска пользователя](./media/active-directory-identityprotection/1019.png "Политика риска пользователя")</span><span class="sxs-lookup"><span data-stu-id="b02f7-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="b02f7-343">Дополнительные сведения см. в статье [Что такое Azure Multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b02f7-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="b02f7-344">Azure AD Identity Protection помогает управлять hello откликами регистрации многофакторной проверки подлинности, настроив политику, которая позволяет:</span><span class="sxs-lookup"><span data-stu-id="b02f7-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="b02f7-345">Набор hello пользователей и групп hello политика применяется к:</span><span class="sxs-lookup"><span data-stu-id="b02f7-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="b02f7-346">![Политика MFA](./media/active-directory-identityprotection/1020.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b02f7-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="b02f7-347">Элементы управления toobe набор hello, при использовании триггеров hello политики принудительно::</span><span class="sxs-lookup"><span data-stu-id="b02f7-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="b02f7-348">![Политика MFA](./media/active-directory-identityprotection/1021.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b02f7-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="b02f7-349">Переключение состояния hello политики:</span><span class="sxs-lookup"><span data-stu-id="b02f7-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="b02f7-350">![Политика MFA](./media/active-directory-identityprotection/403.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b02f7-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="b02f7-351">Просмотреть текущее состояние регистрации hello:</span><span class="sxs-lookup"><span data-stu-id="b02f7-351">View hello current registration status:</span></span>

    <span data-ttu-id="b02f7-352">![Политика MFA](./media/active-directory-identityprotection/1022.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b02f7-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="b02f7-353">Общие сведения о hello связанных взаимодействие с пользователем, в разделе:</span><span class="sxs-lookup"><span data-stu-id="b02f7-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="b02f7-354">[Регистрация с многофакторной проверкой подлинности](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="b02f7-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="b02f7-355">[Процедуры входа с защитой идентификации Azure AD](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="b02f7-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="b02f7-356">**диалоговое окно конфигурации hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="b02f7-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="b02f7-357">На hello **Azure AD Identity Protection** колонки в hello **Настройка** щелкните **регистрации многофакторной проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="b02f7-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="b02f7-358">![Политика MFA](./media/active-directory-identityprotection/1019.png "Политика MFA")</span><span class="sxs-lookup"><span data-stu-id="b02f7-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="b02f7-359">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b02f7-359">Next steps</span></span>
* [<span data-ttu-id="b02f7-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview (Канал 9. Azure Active Directory и идентификация. Предварительная версия защиты идентификации)</span><span class="sxs-lookup"><span data-stu-id="b02f7-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="b02f7-361">Включение защиты идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b02f7-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="b02f7-362">Уязвимости, обнаруживаемые защитой идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b02f7-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="b02f7-363">События риска Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b02f7-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="b02f7-364">Уведомления защиты идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b02f7-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="b02f7-365">Тренировочное задание по защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b02f7-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="b02f7-366">Глоссарий по защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b02f7-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* <span data-ttu-id="b02f7-367">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md) (Процедуры входа с защитой идентификации Azure AD)</span><span class="sxs-lookup"><span data-stu-id="b02f7-367">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md)</span></span>

* [<span data-ttu-id="b02f7-368">Azure Active Directory Identity Protection - как toounblock пользователей</span><span class="sxs-lookup"><span data-stu-id="b02f7-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="b02f7-369">Начало работы с защитой идентификации Azure Active Directory и Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b02f7-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
