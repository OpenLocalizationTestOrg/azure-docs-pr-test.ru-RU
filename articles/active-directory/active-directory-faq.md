---
title: "вопросы и ответы по Active Directory aaaAzure | Документы Microsoft"
description: "Azure Active Directory часто задаваемые вопросы о ответы на вопросы о доступом tooaccess Azure и Azure Active Directory, управление паролями и приложения."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="629ea-103">Azure Active Directory: вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="629ea-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="629ea-104">Azure Active Directory — это комплексная служба идентификации (IDaaS), охватывающая все аспекты идентификации, управления доступом и безопасности.</span><span class="sxs-lookup"><span data-stu-id="629ea-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="629ea-105">Дополнительные сведения см. в статье [Что такое Microsoft Azure Active Directory](active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="629ea-106">Доступ к Azure и Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="629ea-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="629ea-107">**Вопрос. Почему получить «подписки не найден» при попытке tooaccess Azure AD в hello классический портал Azure?**</span><span class="sxs-lookup"><span data-stu-id="629ea-107">**Q: Why do I get “No subscriptions found” when I try tooaccess Azure AD in hello Azure classic portal?**</span></span>

<span data-ttu-id="629ea-108">**Ответ** tooaccess Здравствуйте классический портал Azure, каждому пользователю разрешений с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="629ea-108">**A:** tooaccess hello Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="629ea-109">Если у вас есть платная подписка Office 365 или Azure AD, перейдите в слишком[http://aka.ms/accessAAD](http://aka.ms/accessAAD) для однократной активации шага.</span><span class="sxs-lookup"><span data-stu-id="629ea-109">If you have a paid Office 365 or Azure AD subscription, go too[http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="629ea-110">В противном случае вам потребуется бесплатной tooactivate [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/) или платной подписки.</span><span class="sxs-lookup"><span data-stu-id="629ea-110">Otherwise, you will need tooactivate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="629ea-111">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="629ea-111">For more information, see:</span></span>

* [<span data-ttu-id="629ea-112">Связь между подписками Azure и службой Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="629ea-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="629ea-113">Управление каталогом hello для подписки Office 365 в Azure</span><span class="sxs-lookup"><span data-stu-id="629ea-113">Manage hello directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="629ea-114">**Вопрос. что такое hello связь между Azure AD, Office 365 и Azure?**</span><span class="sxs-lookup"><span data-stu-id="629ea-114">**Q: What’s hello relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="629ea-115">**Ответ** Azure AD предоставляет основные возможности удостоверениями и доступом tooall веб-службы.</span><span class="sxs-lookup"><span data-stu-id="629ea-115">**A:** Azure AD provides you with common identity and access capabilities tooall web services.</span></span> <span data-ttu-id="629ea-116">При использовании Office 365, Microsoft Azure, Intune, или другим пользователям, вы будете уже использует Azure AD toohelp включить управление единого входа и доступа для этих служб.</span><span class="sxs-lookup"><span data-stu-id="629ea-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD toohelp turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="629ea-117">Всех пользователей, которые настраиваются toouse веб-службы определяются как учетные записи пользователей в один или несколько экземпляров Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629ea-117">All users who are set up toouse web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="629ea-118">В этих учетных записях Azure AD можно настроить бесплатные возможности, такие как доступ к облачным приложениям.</span><span class="sxs-lookup"><span data-stu-id="629ea-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="629ea-119">Платные службы Azure AD (например, Enterprise Mobility + Security) дополняют веб-службы, такие как Office 365 и Microsoft Azure, комплексными решениями по управлению и обеспечению безопасности на уровне предприятия.</span><span class="sxs-lookup"><span data-stu-id="629ea-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="629ea-120">**Вопрос. Почему войдите в портал Azure toohello но не hello классический портал Azure**</span><span class="sxs-lookup"><span data-stu-id="629ea-120">**Q:  Why can I sign in toohello Azure portal but not hello Azure classic portal?**</span></span>

<span data-ttu-id="629ea-121">**Ответ** hello портал Azure не требуется действующая подписка, и классического портала hello допустимую подписку.</span><span class="sxs-lookup"><span data-stu-id="629ea-121">**A:**  hello Azure portal does not require a valid subscription, and hello classic portal does require a valid subscription.</span></span>  <span data-ttu-id="629ea-122">Если у вас подписка, не удается войти в toohello классического портала.</span><span class="sxs-lookup"><span data-stu-id="629ea-122">If you do not have a subscription, you can't sign in toohello classic portal.</span></span>
- - -
<span data-ttu-id="629ea-123">**Вопрос. Каковы различия hello подписки администратор и администратор каталога?**</span><span class="sxs-lookup"><span data-stu-id="629ea-123">**Q:  What are hello differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="629ea-124">**Ответ** по умолчанию, назначенных роли администратора подписки hello при регистрации в Azure.</span><span class="sxs-lookup"><span data-stu-id="629ea-124">**A:** By default, you are assigned hello Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="629ea-125">Администратор подписки можно использовать учетную запись Майкрософт или рабочую или учебную учетную запись из каталога hello, hello подписка Azure связана с.</span><span class="sxs-lookup"><span data-stu-id="629ea-125">A subscription admin can use either a Microsoft account or a work or school account from hello directory that hello Azure subscription is associated with.</span></span>  <span data-ttu-id="629ea-126">Эта роль является авторизованным toomanage служб в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="629ea-126">This role is authorized toomanage services in hello Azure portal.</span></span>

<span data-ttu-id="629ea-127">Если другие пользователи должны toosign в и получать доступ к службам, с помощью Здравствуйте той же подписке, их можно добавить в качестве помощников администраторов.</span><span class="sxs-lookup"><span data-stu-id="629ea-127">If others need toosign in and access services by using hello same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="629ea-128">Эта роль имеет hello же привилегии доступа как Здравствуйте, администратор службы, но нельзя изменить связь hello каталогов tooAzure подписки.</span><span class="sxs-lookup"><span data-stu-id="629ea-128">This role has hello same access privileges as hello service admin, but can’t change hello association of subscriptions tooAzure directories.</span></span>  <span data-ttu-id="629ea-129">Дополнительные сведения о Администраторы подписки см. в разделе [как tooadd или изменение роли администратора Azure](../billing-add-change-azure-subscription-administrator.md) и [подписки Azure связаны с Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-129">For additional information on subscription admins, see [How tooadd or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="629ea-130">Azure AD предоставляет ряд различных toomanage hello администрирования ролей каталога и функции, связанные с идентификаторами.</span><span class="sxs-lookup"><span data-stu-id="629ea-130">Azure AD has a different set of admin roles toomanage hello directory and identity-related features.</span></span>  <span data-ttu-id="629ea-131">Эти администраторы будет иметь доступа к функциям toovarious hello портал Azure или hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="629ea-131">These admins will have access toovarious features in hello Azure portal or hello Azure classic portal.</span></span> <span data-ttu-id="629ea-132">роль администратора Hello определяет их возможности, как создание или изменение пользователей, назначить административные роли tooothers, сброс паролей пользователей, управление лицензиями на пользователей или управления доменами.</span><span class="sxs-lookup"><span data-stu-id="629ea-132">hello admin's role determines what they can do, like create or edit users, assign administrative roles tooothers, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="629ea-133">Дополнительные сведения об администраторах каталогов Azure AD и их ролях см. в статье [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="629ea-134">Кроме того, платные службы Azure AD (например, Enterprise Mobility + Security) дополняют веб-службы, такие как Office 365 и Microsoft Azure, комплексными решениями по управлению и обеспечению безопасности на уровне предприятия.</span><span class="sxs-lookup"><span data-stu-id="629ea-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="629ea-135">**Вопрос. Существует ли отчет, показывающий, когда истекает срок действия пользовательских лицензий на Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="629ea-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="629ea-136">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="629ea-136">**A:** No.</span></span>  <span data-ttu-id="629ea-137">В настоящее время недоступно.</span><span class="sxs-lookup"><span data-stu-id="629ea-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="629ea-138">Начало работы с Hybrid Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ea-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="629ea-139">**Вопрос. Каким образом можно выйти из клиента, если я добавлен в качестве участника совместной работы?**</span><span class="sxs-lookup"><span data-stu-id="629ea-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="629ea-140">**Ответ** при добавлении клиента tooanother организации как участника совместной работы, можно использовать hello» клиента переключателя» в верхнем правом tooswitch hello между клиентами.</span><span class="sxs-lookup"><span data-stu-id="629ea-140">**A:** When you are added tooanother organization's tenant as a collaborator, you can use hello "tenant switcher" in hello upper right tooswitch between tenants.</span></span>  <span data-ttu-id="629ea-141">В настоящее время отсутствует приглашении организации tooleave hello не способом система, и корпорация Майкрософт работает над предлагают эти возможности.</span><span class="sxs-lookup"><span data-stu-id="629ea-141">Currently, there is no way tooleave hello inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="629ea-142">Пока эта функция доступна, вы можете запросить hello приглашении tooremove организации из своего клиента.</span><span class="sxs-lookup"><span data-stu-id="629ea-142">Until this feature is available, you can ask hello inviting organization tooremove you from their tenant.</span></span>
- - -
<span data-ttu-id="629ea-143">**Вопрос. как подключиться мой локальный каталог tooAzure AD**</span><span class="sxs-lookup"><span data-stu-id="629ea-143">**Q: How can I connect my on-premises directory tooAzure AD?**</span></span>

<span data-ttu-id="629ea-144">**Ответ** подключении вашего локального каталога tooAzure AD с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="629ea-144">**A:** You can connect your on-premises directory tooAzure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="629ea-145">Дополнительные сведения см. в статье [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="629ea-146">**Вопрос. Как настроить единый вход между локальным каталогом и облачными приложениями?**</span><span class="sxs-lookup"><span data-stu-id="629ea-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="629ea-147">**Ответ** достаточно tooset копирование единого входа (SSO) между локальным каталогом и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629ea-147">**A:** You only need tooset up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="629ea-148">При условии, что облачных приложений, доступ через Azure AD, hello службы автоматически диски toocorrectly проверки подлинности с учетными данными своих локальных пользователей.</span><span class="sxs-lookup"><span data-stu-id="629ea-148">As long as you access your cloud applications through Azure AD, hello service automatically drives your users toocorrectly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="629ea-149">Единый вход из локальной сети можно легко реализовать благодаря решениям федерации, таким как службы федерации Active Directory (ADFS), или путем настройки синхронизации хэшей паролей. Оба параметра можно легко развернуть с помощью мастера настройки hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="629ea-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using hello Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="629ea-150">Дополнительные сведения см. в статье [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="629ea-151">**Вопрос. Предусмотрен ли в Azure AD портал самообслуживания для пользователей в моей организации?**</span><span class="sxs-lookup"><span data-stu-id="629ea-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="629ea-152">**Ответ** Да, Azure AD предоставляет hello [панели доступа Azure AD](http://myapps.microsoft.com) для пользователя самообслуживания и доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="629ea-152">**A:** Yes, Azure AD provides you with hello [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="629ea-153">Если вы являетесь клиентом Office 365, многие hello можно найти те же возможности на портале Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="629ea-153">If you are an Office 365 customer, you can find many of hello same capabilities in hello Office 365 portal.</span></span>

<span data-ttu-id="629ea-154">Дополнительные сведения см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-154">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="629ea-155">**Вопрос. Можно ли управлять локальной инфраструктурой с помощью Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="629ea-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="629ea-156">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="629ea-156">**A:** Yes.</span></span> <span data-ttu-id="629ea-157">Hello Azure AD Premium edition позволяет Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="629ea-157">hello Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="629ea-158">Azure AD Connect Health помогает отслеживать и лучшего понимания вашей личности в локальной инфраструктуре и hello служб синхронизации.</span><span class="sxs-lookup"><span data-stu-id="629ea-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and hello synchronization services.</span></span>  

<span data-ttu-id="629ea-159">Дополнительные сведения см. в разделе [мониторинга вашей локальной инфраструктуры и синхронизации службы удостоверений в облаке hello](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in hello cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="629ea-160">Управление паролями</span><span class="sxs-lookup"><span data-stu-id="629ea-160">Password management</span></span>
<span data-ttu-id="629ea-161">**Вопрос. Можно ли использовать компонент обратной записи паролей Azure AD без синхронизации паролей? (В этом случае это возможных toouse Azure AD самостоятельного сброса паролей (SSPR) с паролями обратной записи и сохраняет пароль в облаке hello?)**</span><span class="sxs-lookup"><span data-stu-id="629ea-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible toouse Azure AD self-service password reset (SSPR) with password write-back and not store passwords in hello cloud?)**</span></span>

<span data-ttu-id="629ea-162">**Ответ** не требуется toosynchronize вашей Active Directory пароли tooAzure AD tooenable обратной записи.</span><span class="sxs-lookup"><span data-stu-id="629ea-162">**A:** You do not need toosynchronize your Active Directory passwords tooAzure AD tooenable write-back.</span></span> <span data-ttu-id="629ea-163">В федеративной среде Azure AD единого входа (SSO) использует hello локального каталога tooauthenticate hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="629ea-163">In a federated environment, Azure AD single sign-on (SSO) relies on hello on-premises directory tooauthenticate hello user.</span></span> <span data-ttu-id="629ea-164">В этом сценарии требуется пароль toobe hello в локальной среде, отслеживаются в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629ea-164">This scenario does not require hello on-premises password toobe tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="629ea-165">**Вопрос. как времени требуется для toobe пароль, записаны tooActive каталог локально?**</span><span class="sxs-lookup"><span data-stu-id="629ea-165">**Q: How long does it take for a password toobe written back tooActive Directory on-premises?**</span></span>

<span data-ttu-id="629ea-166">**Ответ.** Обратная запись пароля выполняется в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="629ea-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="629ea-167">Дополнительные сведения см. в статье [Приступая к работе с компонентами управления паролями](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="629ea-168">**Вопрос. Можно ли использовать обратную запись паролей, которые управляются администратором?**</span><span class="sxs-lookup"><span data-stu-id="629ea-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="629ea-169">**Ответ** Да, если имеется обратная запись пароля включен hello пароль операции, выполняемые администратором записываются обратно tooyour в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="629ea-169">**A:** Yes, if you have password write-back enabled, hello password operations performed by an admin are written back tooyour on-premises environment.</span></span>  

<span data-ttu-id="629ea-170">Для получения дополнительных см. вопросы, связанные с toopassword, [вопросы и ответы по управлению паролями](active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-170">For more answers toopassword-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="629ea-171">**Вопрос. что делать, если при попытке toochange пароль забыли существующий пароль Office 365 или Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="629ea-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying toochange my password?**</span></span>

<span data-ttu-id="629ea-172">**Ответ.** В такой ситуации есть два варианта действий.</span><span class="sxs-lookup"><span data-stu-id="629ea-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="629ea-173">Используйте самостоятельный сброс пароля, если он доступен.</span><span class="sxs-lookup"><span data-stu-id="629ea-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="629ea-174">Функционирование самостоятельного сброса пароля зависит от настройки этой функции.</span><span class="sxs-lookup"><span data-stu-id="629ea-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="629ea-175">Дополнительные сведения см. в разделе [как приведет hello пароль к изменению рабочего портала](active-directory-passwords-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-175">For more information, see [How does hello password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="629ea-176">Для пользователей Office 365 администратор может сбросить пароль hello с помощью hello действия, описанные в [сброс паролей пользователей](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="629ea-176">For Office 365 users, your admin can reset hello password by using hello steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="629ea-177">Для учетных записей Azure AD администраторы могут сбросить пароль с помощью одного из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="629ea-177">For Azure AD accounts, admins can reset passwords by using one of hello following:</span></span>

- [<span data-ttu-id="629ea-178">Сброс учетных записей в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="629ea-178">Reset accounts in hello Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="629ea-179">Сброс учетных записей в классическом портале hello</span><span class="sxs-lookup"><span data-stu-id="629ea-179">Reset accounts in hello classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="629ea-180">Использование PowerShell</span><span class="sxs-lookup"><span data-stu-id="629ea-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="629ea-181">Безопасность</span><span class="sxs-lookup"><span data-stu-id="629ea-181">Security</span></span>
<span data-ttu-id="629ea-182">**Вопрос. Блокируются ли учетные записи после определенного числа неудачных попыток или используется более сложная стратегия?**</span><span class="sxs-lookup"><span data-stu-id="629ea-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="629ea-183">Мы используем более сложные счетов toolock стратегии.</span><span class="sxs-lookup"><span data-stu-id="629ea-183">We use a more sophisticated strategy toolock accounts.</span></span>  <span data-ttu-id="629ea-184">Следующий пример основан на IP-адресов hello запроса hello и hello пароли, введенные.</span><span class="sxs-lookup"><span data-stu-id="629ea-184">This is based on hello IP of hello request and hello passwords entered.</span></span> <span data-ttu-id="629ea-185">Hello продолжительность блокировки hello увеличивает основании hello вероятность, что это атаки.</span><span class="sxs-lookup"><span data-stu-id="629ea-185">hello duration of hello lockout also increases based on hello likelihood that it is an attack.</span></span>  

<span data-ttu-id="629ea-186">**Вопрос определенных отклонены пароли (Общие) с hello сообщения «используется toomany раз этот пароль был» см. в это toopasswords, используемого в текущем active directory hello?**</span><span class="sxs-lookup"><span data-stu-id="629ea-186">**Q:  Certain (common) passwords get rejected with hello messages ‘this password has been used toomany times’, does this refer toopasswords used in hello current active directory?**</span></span></br>
<span data-ttu-id="629ea-187">Это относится toopasswords, являющиеся общими глобально, например все варианты «Password» и «123456».</span><span class="sxs-lookup"><span data-stu-id="629ea-187">This refers toopasswords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="629ea-188">**Вопрос. Будет ли блокироваться запрос на вход в клиент B2C из сомнительных источников (ботнеты, конечная точка tor) или для этого требуется клиент выпуска Basic или Premium?**</span><span class="sxs-lookup"><span data-stu-id="629ea-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="629ea-189">У нас есть шлюз, который отфильтровывает запросы и предоставляет некоторую защиту от ботнетов и применяется для всех клиентов B2C.</span><span class="sxs-lookup"><span data-stu-id="629ea-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="629ea-190">Доступ к приложениям</span><span class="sxs-lookup"><span data-stu-id="629ea-190">Application access</span></span>
<span data-ttu-id="629ea-191">**Вопрос. Где можно найти список предварительно интегрированных с Azure AD приложений и их возможностей?**</span><span class="sxs-lookup"><span data-stu-id="629ea-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="629ea-192">**Ответ.** В Azure AD предварительно интегрировано более 2600 приложений корпорации Майкрософт, поставщиков услуг по предоставлению приложений в аренду (ASP) или партнеров.</span><span class="sxs-lookup"><span data-stu-id="629ea-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="629ea-193">Все предварительно интегрированные приложения поддерживают единый вход.</span><span class="sxs-lookup"><span data-stu-id="629ea-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="629ea-194">Единый вход позволяет использовать tooaccess вашей организации учетные данные приложения.</span><span class="sxs-lookup"><span data-stu-id="629ea-194">SSO lets you use your organizational credentials tooaccess your apps.</span></span> <span data-ttu-id="629ea-195">Некоторые приложения hello также поддерживают автоматического удаления и обеспечения.</span><span class="sxs-lookup"><span data-stu-id="629ea-195">Some of hello applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="629ea-196">Полный список hello предварительно интегрированных приложений см. в разделе hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="629ea-196">For a complete list of hello pre-integrated applications, see hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="629ea-197">**Вопрос. что если hello приложение необходимое, не находится в marketplace hello Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="629ea-197">**Q: What if hello application I need is not in hello Azure AD marketplace?**</span></span>

<span data-ttu-id="629ea-198">**Ответ.** С помощью Azure AD Premium вы можете добавить и настроить любое приложение.</span><span class="sxs-lookup"><span data-stu-id="629ea-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="629ea-199">В зависимости от возможностей вашего приложения и своих предпочтений вы можете настроить единый вход и автоматическую подготовку.</span><span class="sxs-lookup"><span data-stu-id="629ea-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="629ea-200">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="629ea-200">For more information, see:</span></span>

* [<span data-ttu-id="629ea-201">Настройка одного tooapplications входа, которых нет в коллекции приложений Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="629ea-201">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="629ea-202">С помощью SCIM tooenable автоматическую подготовку пользователей и групп из Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="629ea-202">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="629ea-203">**Вопрос. как пользователям зарегистрироваться в tooapplications с помощью Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="629ea-203">**Q: How do users sign in tooapplications by using Azure AD?**</span></span>

<span data-ttu-id="629ea-204">**Ответ** Azure AD предоставляет несколько способов для tooview пользователей и доступ к приложениям, например:</span><span class="sxs-lookup"><span data-stu-id="629ea-204">**A:** Azure AD provides several ways for users tooview and access their applications, such as:</span></span>

* <span data-ttu-id="629ea-205">панель доступа Hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="629ea-205">hello Azure AD access panel</span></span>
* <span data-ttu-id="629ea-206">Запуск приложений Hello Office 365</span><span class="sxs-lookup"><span data-stu-id="629ea-206">hello Office 365 application launcher</span></span>
* <span data-ttu-id="629ea-207">Прямой toofederated приложений</span><span class="sxs-lookup"><span data-stu-id="629ea-207">Direct sign-in toofederated apps</span></span>
* <span data-ttu-id="629ea-208">Прямые ссылки toofederated, основанный на пароле, или существующих приложений</span><span class="sxs-lookup"><span data-stu-id="629ea-208">Deep links toofederated, password-based, or existing apps</span></span>

<span data-ttu-id="629ea-209">Дополнительные сведения см. в разделе [развертывание Azure AD интегрированных приложений toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="629ea-209">For more information, see [Deploying Azure AD integrated applications toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="629ea-210">**Вопрос. что можно различными способами hello Azure AD обеспечивает проверку подлинности и tooapplications?**</span><span class="sxs-lookup"><span data-stu-id="629ea-210">**Q: What are hello different ways Azure AD enables authentication and single sign-on tooapplications?**</span></span>

<span data-ttu-id="629ea-211">**Ответ.** Azure AD поддерживает множество стандартных протоколов для проверки подлинности и авторизации, например SAML 2.0, OpenID Connect, OAuth 2.0 и WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="629ea-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="629ea-212">В Azure AD также реализованы хранилища паролей и возможности автоматического входа для приложений, которые поддерживают только проверку подлинности на основе форм.</span><span class="sxs-lookup"><span data-stu-id="629ea-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="629ea-213">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="629ea-213">For more information, see:</span></span>

* [<span data-ttu-id="629ea-214">Сценарии аутентификации в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="629ea-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="629ea-215">Протоколы проверки подлинности Active Directory</span><span class="sxs-lookup"><span data-stu-id="629ea-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="629ea-216">Принцип работы единого входа с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="629ea-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="629ea-217">**Вопрос. Можно ли добавить приложения, которые я использую в локальной среде?**</span><span class="sxs-lookup"><span data-stu-id="629ea-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="629ea-218">**Ответ** прокси приложения Azure AD обеспечивает простой и безопасный доступ tooon локальный веб-приложений, для выбора.</span><span class="sxs-lookup"><span data-stu-id="629ea-218">**A:** Azure AD Application Proxy provides you with easy and secure access tooon-premises web applications that you choose.</span></span> <span data-ttu-id="629ea-219">Доступны эти приложения в hello так же, что доступ к программное обеспечение как услуга (SaaS) приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629ea-219">You can access these applications in hello same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="629ea-220">Нет необходимости для VPN-подключения или toochange сетевой инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="629ea-220">There is no need for a VPN or toochange your network infrastructure.</span></span>  

<span data-ttu-id="629ea-221">Дополнительные сведения см. в разделе [как tooprovide безопасный удаленный доступ tooon локальные приложения](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-221">For more information, see [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="629ea-222">**Вопрос. Как установить обязательное выполнение многофакторной идентификации для пользователей, обращающихся к конкретному приложению?**</span><span class="sxs-lookup"><span data-stu-id="629ea-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="629ea-223">**Ответ.** С помощью условного доступа Azure AD вы можете назначить уникальную политику доступа для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="629ea-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="629ea-224">В политике можно требовать многофакторную проверку подлинности всегда или если пользователи не подключенных toohello локальной сети.</span><span class="sxs-lookup"><span data-stu-id="629ea-224">In your policy, you can require multi-factor authentication always, or when users are not connected toohello local network.</span></span>  

<span data-ttu-id="629ea-225">Дополнительные сведения см. в разделе [защита доступа tooOffice 365 и других приложений подключен tooAzure Active Directory](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-225">For more information, see [Securing access tooOffice 365 and other apps connected tooAzure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="629ea-226">**Вопрос. Что такое автоматическая подготовка пользователей для приложений SaaS?**</span><span class="sxs-lookup"><span data-stu-id="629ea-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="629ea-227">**Ответ** Создание hello tooautomate используют Azure AD, обслуживание и удаление удостоверения пользователя из многих популярных облачных приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="629ea-227">**A:** Use Azure AD tooautomate hello creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="629ea-228">Дополнительные сведения см. в разделе [автоматизировать подготовку пользователей и их отзыв tooSaaS приложений с Azure Active Directory](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="629ea-228">For more information, see [Automate user provisioning and deprovisioning tooSaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="629ea-229">**Вопрос. Можно ли установить безопасное подключение LDAP к Azure AD?** </span><span class="sxs-lookup"><span data-stu-id="629ea-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="629ea-230">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="629ea-230">**A:**  No.</span></span> <span data-ttu-id="629ea-231">Azure AD не поддерживает протокол LDAP hello.</span><span class="sxs-lookup"><span data-stu-id="629ea-231">Azure AD does not support hello LDAP protocol.</span></span>
