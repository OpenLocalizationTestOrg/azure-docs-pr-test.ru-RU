---
title: "Глоссарий защиты идентификации Active Directory aaaAzure | Документы Microsoft"
description: "Глоссарий по защите идентификации Azure Active Directory"
services: active-directory
keywords: "защита идентификации Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности, глоссарий"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="21742-104">Глоссарий по защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21742-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="21742-105">Под угрозой (пользователь)</span><span class="sxs-lookup"><span data-stu-id="21742-105">At risk (User)</span></span>
<span data-ttu-id="21742-106">Пользователь с одним или несколькими активными событиями риска.</span><span class="sxs-lookup"><span data-stu-id="21742-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="21742-107">Нетипичное расположение входа</span><span class="sxs-lookup"><span data-stu-id="21742-107">Atypical sign-in location</span></span>
<span data-ttu-id="21742-108">Войдите в систему из географического расположения, не является типичным для конкретного пользователя hello, подобных пользователей или hello клиента.</span><span class="sxs-lookup"><span data-stu-id="21742-108">A sign-in from a geographic location that is not typical for hello specific user, similar users, or hello tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="21742-109">защиту идентификации Azure AD</span><span class="sxs-lookup"><span data-stu-id="21742-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="21742-110">Модуль безопасности Azure Active Directory, который обеспечивает единое представление обо всех событиях, создающих риски, и потенциальных уязвимостях, которые могут влиять на идентификацию организации.</span><span class="sxs-lookup"><span data-stu-id="21742-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="21742-111">Условный доступ</span><span class="sxs-lookup"><span data-stu-id="21742-111">Conditional access</span></span>
<span data-ttu-id="21742-112">Политика защиты доступа к tooresources.</span><span class="sxs-lookup"><span data-stu-id="21742-112">A policy for securing access tooresources.</span></span> <span data-ttu-id="21742-113">Правила условного доступа хранятся в Azure Active Directory hello и вычисляются с помощью Azure AD перед предоставлением доступа toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="21742-113">Conditional access rules are stored in hello Azure Active Directory and are evaluated by Azure AD before granting access toohello resource.</span></span>  <span data-ttu-id="21742-114">Примерами правил являются ограничения доступа на основе расположения пользователя, работоспособности устройства или метода проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="21742-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="21742-115">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="21742-115">Credentials</span></span>
<span data-ttu-id="21742-116">Сведения, включающие идентификатор и подтверждение идентификатора, используемые toogain доступа toolocal и сетевые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="21742-116">Information that includes identification and proof of identification that is used toogain access toolocal and network resources.</span></span> <span data-ttu-id="21742-117">Примерами учетных данных являются имена пользователей и пароли, смарт-карты и сертификаты.</span><span class="sxs-lookup"><span data-stu-id="21742-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="21742-118">Событие</span><span class="sxs-lookup"><span data-stu-id="21742-118">Event</span></span>
<span data-ttu-id="21742-119">Запись действия в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="21742-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="21742-120">Ложноположительное (событие риска)</span><span class="sxs-lookup"><span data-stu-id="21742-120">False-positive (risk event)</span></span>
<span data-ttu-id="21742-121">Состояние события риска, задать вручную пользователем защиту учетных данных, события риска hello было разобрано и был ошибочно помечается как события риска.</span><span class="sxs-lookup"><span data-stu-id="21742-121">A risk event status set manually by an Identity Protection user, indicating that hello risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="21742-122">Удостоверение</span><span class="sxs-lookup"><span data-stu-id="21742-122">Identity</span></span>
<span data-ttu-id="21742-123">Лицо или организация, которые должны быть проверены с помощью средств проверки подлинности на основе определенных условий, таких как пароль или сертификат.</span><span class="sxs-lookup"><span data-stu-id="21742-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="21742-124">Событие риска удостоверения</span><span class="sxs-lookup"><span data-stu-id="21742-124">Identity risk event</span></span>
<span data-ttu-id="21742-125">Событие AAD, которое было отмечено модулем защиты идентификации как аномальное и может указывать, что удостоверение было скомпрометировано.</span><span class="sxs-lookup"><span data-stu-id="21742-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="21742-126">Игнорируется (событие риска)</span><span class="sxs-lookup"><span data-stu-id="21742-126">Ignored (risk event)</span></span>
<span data-ttu-id="21742-127">Состояние события риска, задать вручную пользователем защиту учетных данных, о том, что события риска hello закрыт без учета действие исправления.</span><span class="sxs-lookup"><span data-stu-id="21742-127">A risk event status set manually by an Identity Protection user, indicating that hello risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="21742-128">Невозможно переместиться из нетипичных расположений</span><span class="sxs-lookup"><span data-stu-id="21742-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="21742-129">Запускается при два входа в систему для hello один пользователь обнаружены, где по крайней мере один из них — из необычного вход расположения и где hello время между входами hello короче, чем hello минимальное время, может потребоваться toophysically события риска перемещаться между этими расположения.</span><span class="sxs-lookup"><span data-stu-id="21742-129">A risk event triggered when two sign-ins for hello same user are detected, where at least one of them is from an atypical sign-in location, and where hello time between hello sign-ins is shorter than hello minimum time it would take toophysically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="21742-130">Исследование</span><span class="sxs-lookup"><span data-stu-id="21742-130">Investigation</span></span>
<span data-ttu-id="21742-131">Hello процесс проверки действия hello, журналы и другие важные сведения, связанных с toodecide событий риска tooa ли исправление или устранения действий, необходимых, понять наличие и способ идентификации hello был скомпрометирован, а также понять, каким образом hello была использована скомпрометированных удостоверения.</span><span class="sxs-lookup"><span data-stu-id="21742-131">hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary, understand if and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="21742-132">Утерянные учетные данные</span><span class="sxs-lookup"><span data-stu-id="21742-132">Leaked credentials</span></span>
<span data-ttu-id="21742-133">Hello темной веб-узле нашей исследователями публично опубликовано событие риска, запускается при обнаружении учетных данных текущего пользователя (имя пользователя и пароль).</span><span class="sxs-lookup"><span data-stu-id="21742-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in hello Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="21742-134">Устранение</span><span class="sxs-lookup"><span data-stu-id="21742-134">Mitigation</span></span>
<span data-ttu-id="21742-135">Действие toolimit или исключить возможность hello злоумышленник tooexploit скомпрометированных удостоверения или устройства без восстановления hello удостоверения или tooa безопасном состояние устройства.</span><span class="sxs-lookup"><span data-stu-id="21742-135">An action toolimit or eliminate hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="21742-136">Исправление не устраняет предыдущих риск события, связанные с hello удостоверения или устройства.</span><span class="sxs-lookup"><span data-stu-id="21742-136">A mitigation does not resolve previous risk events associated with hello identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="21742-137">Многофакторная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="21742-137">Multi-factor authentication</span></span>
<span data-ttu-id="21742-138">Метод проверки подлинности, который требует два или несколько методов проверки подлинности, которые могут содержать то, что пользователь hello, такой сертификат; что-то знает hello пользователя, например имена пользователей, пароли или передайте фразы; Физические атрибуты, например для отпечатка; и личных атрибуты, такие как личной цифровой подписи.</span><span class="sxs-lookup"><span data-stu-id="21742-138">An authentication method that requires two or more authentication methods, which may include something hello user has, such a certificate; something hello user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="21742-139">Обнаружение в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="21742-139">Offline detection</span></span>
<span data-ttu-id="21742-140">Hello обнаружение аномалий и оценки риска hello события, например попытки входа после проведения hello, для события, которое уже прошло.</span><span class="sxs-lookup"><span data-stu-id="21742-140">hello detection of anomalies and evaluation of hello risk of an event such as sign-in attempt after hello fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="21742-141">Условие политики</span><span class="sxs-lookup"><span data-stu-id="21742-141">Policy condition</span></span>
<span data-ttu-id="21742-142">Часть политики безопасности, который определяет hello сущности (группы, пользователи, приложения, платформы устройств, состояния устройства, диапазоны IP-адресов, типы клиента) включаются в политику hello или исключить из нее.</span><span class="sxs-lookup"><span data-stu-id="21742-142">A part of a security policy which defines hello entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in hello policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="21742-143">Правило политики</span><span class="sxs-lookup"><span data-stu-id="21742-143">Policy rule</span></span>
<span data-ttu-id="21742-144">часть политики безопасности, который описывает hello обстоятельств, которые активируют политики hello и hello действия, выполняемые при запуске политики hello Hello.</span><span class="sxs-lookup"><span data-stu-id="21742-144">hello part of a security policy which describes hello circumstances that would trigger hello policy, and hello actions taken when hello policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="21742-145">Предотвращение</span><span class="sxs-lookup"><span data-stu-id="21742-145">Prevention</span></span>
<span data-ttu-id="21742-146">Действие tooprevent повреждения toohello организации через о нарушении удостоверения или устройства, вероятно, или знать toobe скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="21742-146">An action tooprevent damage toohello organization through abuse of an identity or device suspected or know toobe compromised.</span></span> <span data-ttu-id="21742-147">Действие Предотвращение не обеспечивает безопасность устройства hello или удостоверение и не обрабатывается предыдущих событий риска.</span><span class="sxs-lookup"><span data-stu-id="21742-147">A prevention action does not secure hello device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="21742-148">Привилегированный (пользователь)</span><span class="sxs-lookup"><span data-stu-id="21742-148">Privileged (user)</span></span>
<span data-ttu-id="21742-149">Пользователь, во время hello события риска, имеющих tooone разрешения администратора постоянных и временных или больше ресурсов в Azure Active Directory, такие как глобальный администратор, администратор выставления счетов, администратор службы, администратора пользователей и паролей Администратор.</span><span class="sxs-lookup"><span data-stu-id="21742-149">A user that at hello time of a risk event, had permanent or temporary admin permissions tooone or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="21742-150">В режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="21742-150">Real-time</span></span>
<span data-ttu-id="21742-151">См. "Обнаружение в режиме реального времени".</span><span class="sxs-lookup"><span data-stu-id="21742-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="21742-152">Обнаружение в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="21742-152">Real-time detection</span></span>
<span data-ttu-id="21742-153">обнаружение аномалий Hello и оценки риска hello события, например попытки входа перед событием hello допускается tooproceed.</span><span class="sxs-lookup"><span data-stu-id="21742-153">hello detection of anomalies and evaluation of hello risk of an event such as sign-in attempt before hello event is allowed tooproceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="21742-154">Исправлено (событие риска)</span><span class="sxs-lookup"><span data-stu-id="21742-154">Remediated (risk event)</span></span>
<span data-ttu-id="21742-155">Состояние события риска, устанавливается автоматически службой защиты идентификации, о том, что события риска hello исправления с помощью hello стандартные действия для этого типа событий риска.</span><span class="sxs-lookup"><span data-stu-id="21742-155">A risk event status set automatically by Identity Protection, indicating that hello risk event was remediated using hello standard remediation action for this type of risk event.</span></span> <span data-ttu-id="21742-156">Например при сбросе пароля пользователя hello множество событий риска, указывающие, что этот пароль предыдущих hello была скомпрометирована исправляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="21742-156">For example, when hello user password is reset, many risk events that indicate that hello previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="21742-157">Исправление</span><span class="sxs-lookup"><span data-stu-id="21742-157">Remediation</span></span>
<span data-ttu-id="21742-158">Действие toosecure удостоверения или устройстве, ранее подозревается или известные toobe под угрозой.</span><span class="sxs-lookup"><span data-stu-id="21742-158">An action toosecure an identity or a device that were previously suspected or known toobe compromised.</span></span> <span data-ttu-id="21742-159">Действие исправления восстанавливает hello удостоверения или tooa безопасном состояние устройства и разрешает предыдущих риск события, связанные с hello удостоверения или устройства.</span><span class="sxs-lookup"><span data-stu-id="21742-159">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="21742-160">Разрешено (событие риска)</span><span class="sxs-lookup"><span data-stu-id="21742-160">Resolved (risk event)</span></span>
<span data-ttu-id="21742-161">Состояние события риска, задать вручную пользователем с правами защиту учетных данных, что пользователь hello выполнены соответствующие исправления действия за пределами защиту учетных данных и события hello риска следует учитывать закрыт.</span><span class="sxs-lookup"><span data-stu-id="21742-161">A risk event status set manually by an Identity Protection user, indicating that hello user took an appropriate remediation action outside Identity Protection, and that hello risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="21742-162">Состояние события риска</span><span class="sxs-lookup"><span data-stu-id="21742-162">Risk event status</span></span>
<span data-ttu-id="21742-163">Свойство события риска, указывающее, является ли событие hello и закрыто, hello причину закрытия.</span><span class="sxs-lookup"><span data-stu-id="21742-163">A property of a risk event, indicating whether hello event is active, and if closed, hello reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="21742-164">Тип события риска</span><span class="sxs-lookup"><span data-stu-id="21742-164">Risk event type</span></span>
<span data-ttu-id="21742-165">Категория для hello риск событие указывает на тип hello аномалий, вызвавшего считается рискованным toobe событий hello.</span><span class="sxs-lookup"><span data-stu-id="21742-165">A category for hello risk event, indicating hello type of anomaly that caused hello event toobe considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="21742-166">Уровень риска (событие риска)</span><span class="sxs-lookup"><span data-stu-id="21742-166">Risk level (risk event)</span></span>
<span data-ttu-id="21742-167">Указывает серьезность hello hello риск событие toohelp защиту учетных данных пользователей (высокий, средний или низкий) расставлять приоритеты hello действия они принимают риск tootheir tooreduce hello организации.</span><span class="sxs-lookup"><span data-stu-id="21742-167">An indication (High, Medium, or Low) of hello severity of hello risk event toohelp Identity Protection users prioritize hello actions they take tooreduce hello risk tootheir organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="21742-168">Уровень риска (вход)</span><span class="sxs-lookup"><span data-stu-id="21742-168">Risk level (sign-in)</span></span>
<span data-ttu-id="21742-169">Указание (высокий, средний или низкий) вероятность hello, определенные при входе, кто-то другой пытается toouse hello учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="21742-169">An indication (High, Medium, or Low) of hello likelihood that for a specific sign-in, someone else is attempting toouse hello user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="21742-170">Уровень риска (компрометация пользователя)</span><span class="sxs-lookup"><span data-stu-id="21742-170">Risk level (user compromise)</span></span>
<span data-ttu-id="21742-171">Указание (высокий, средний или низкий) hello вероятность того, что удостоверение был скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="21742-171">An indication (High, Medium, or Low) of hello likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="21742-172">Уровень риска (уязвимость)</span><span class="sxs-lookup"><span data-stu-id="21742-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="21742-173">Указывает серьезность hello hello уязвимость toohelp защиту учетных данных пользователей (высокий, средний или низкий) расставлять приоритеты hello действия они принимают риск tootheir tooreduce hello организации.</span><span class="sxs-lookup"><span data-stu-id="21742-173">An indication (High, Medium, or Low) of hello severity of hello vulnerability toohelp Identity Protection users prioritize hello actions they take tooreduce hello risk tootheir organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="21742-174">Безопасное (удостоверение)</span><span class="sxs-lookup"><span data-stu-id="21742-174">Secure (identity)</span></span>
<span data-ttu-id="21742-175">Выполните действие исправления, как изменить пароль или повторное создание образа toorestore состояние tooan устойчивости скомпрометированы удостоверение компьютера.</span><span class="sxs-lookup"><span data-stu-id="21742-175">Take remediation action such as a password change or machine reimaging toorestore a potentially compromised identity tooan uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="21742-176">Политика безопасности</span><span class="sxs-lookup"><span data-stu-id="21742-176">Security policy</span></span>
<span data-ttu-id="21742-177">Коллекция правил и условий политики.</span><span class="sxs-lookup"><span data-stu-id="21742-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="21742-178">Политика может быть применен tooentities как пользователи, группы, приложений, устройств, платформ устройств, состояния устройства, диапазоны IP-адресов и Auth2.0 типов клиентов.</span><span class="sxs-lookup"><span data-stu-id="21742-178">A policy can be applied tooentities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="21742-179">Политика включена, вычисляется каждый раз, когда сущности включаются в политику hello выданный маркер для ресурса.</span><span class="sxs-lookup"><span data-stu-id="21742-179">When a policy is enabled, it is evaluated whenever an entity included in hello policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="21742-180">Выполнить вход</span><span class="sxs-lookup"><span data-stu-id="21742-180">Sign in (v)</span></span>
<span data-ttu-id="21742-181">tooauthenticate tooan удостоверений в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="21742-181">tooauthenticate tooan identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="21742-182">Вход</span><span class="sxs-lookup"><span data-stu-id="21742-182">Sign-in (n)</span></span>
<span data-ttu-id="21742-183">Здравствуйте, процесса или действия проверки подлинности удостоверения в Azure Active Directory и hello событие, которое захватывает этой операции.</span><span class="sxs-lookup"><span data-stu-id="21742-183">hello process or action of authenticating an identity in Azure Active Directory, and hello event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="21742-184">Вход с анонимных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="21742-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="21742-185">Событие риска, возникающее после успешного входа в систему с IP-адреса, который был определен как IP-адрес анонимного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="21742-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="21742-186">Вход с инфицированных устройств</span><span class="sxs-lookup"><span data-stu-id="21742-186">Sign-in from infected device</span></span>
<span data-ttu-id="21742-187">Событие риска, создается при входе исходит от IP-адрес, известный toobe используется один или несколько скомпрометированных устройств, которые активно пытаетесь toocommunicate с этим сервером.</span><span class="sxs-lookup"><span data-stu-id="21742-187">A risk event triggered when a sign-in originates from an IP address which is known toobe used by one or more compromised devices, which are actively attempting toocommunicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="21742-188">Вход с IP-адресов с подозрительными действиями</span><span class="sxs-lookup"><span data-stu-id="21742-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="21742-189">Событие риска, возникающее после успешного входа с IP-адреса с большим количеством неудачных попыток входа с использованием нескольких учетных записей пользователей за короткий период времени.</span><span class="sxs-lookup"><span data-stu-id="21742-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="21742-190">Вход из неизвестного расположения</span><span class="sxs-lookup"><span data-stu-id="21742-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="21742-191">Событие риска, возникающее, когда пользователь успешно выполняет вход из нового расположения (IP-адрес, широта и долгота и ASN).</span><span class="sxs-lookup"><span data-stu-id="21742-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="21742-192">Риск входа</span><span class="sxs-lookup"><span data-stu-id="21742-192">Sign-in risk</span></span>
<span data-ttu-id="21742-193">См. "Уровень риска" (вход)</span><span class="sxs-lookup"><span data-stu-id="21742-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="21742-194">Политика риска входа</span><span class="sxs-lookup"><span data-stu-id="21742-194">Sign-in risk policy</span></span>
<span data-ttu-id="21742-195">Политика условного доступа, которая вычисляет hello риск tooa конкретных вход и применяет исправления на основе предопределенных условий и правил.</span><span class="sxs-lookup"><span data-stu-id="21742-195">A conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="21742-196">Риск компрометации пользователя</span><span class="sxs-lookup"><span data-stu-id="21742-196">User compromise risk</span></span>
<span data-ttu-id="21742-197">См. "Уровень риска" (компрометация пользователя)</span><span class="sxs-lookup"><span data-stu-id="21742-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="21742-198">Риск пользователя</span><span class="sxs-lookup"><span data-stu-id="21742-198">User risk</span></span>
<span data-ttu-id="21742-199">См. "Уровень риска" (компрометация пользователя)</span><span class="sxs-lookup"><span data-stu-id="21742-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="21742-200">Политика риска пользователя</span><span class="sxs-lookup"><span data-stu-id="21742-200">User risk policy</span></span>
<span data-ttu-id="21742-201">Политика условного доступа, считает, что вход hello и применяет исправления на основе предопределенных условий и правил.</span><span class="sxs-lookup"><span data-stu-id="21742-201">A conditional access policy that considers hello sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="21742-202">Пользователи, помеченные для события риска</span><span class="sxs-lookup"><span data-stu-id="21742-202">Users flagged for risk</span></span>
<span data-ttu-id="21742-203">Пользователи с активными или исправленными событиями рисков</span><span class="sxs-lookup"><span data-stu-id="21742-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="21742-204">Уязвимость</span><span class="sxs-lookup"><span data-stu-id="21742-204">Vulnerability</span></span>
<span data-ttu-id="21742-205">Конфигурация или условие в Azure Active Directory, что делает подвержены tooexploits directory hello или угроз.</span><span class="sxs-lookup"><span data-stu-id="21742-205">A configuration or condition in Azure Active Directory which makes hello directory susceptible tooexploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="21742-206">См. также</span><span class="sxs-lookup"><span data-stu-id="21742-206">See also</span></span>
* [<span data-ttu-id="21742-207">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="21742-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

