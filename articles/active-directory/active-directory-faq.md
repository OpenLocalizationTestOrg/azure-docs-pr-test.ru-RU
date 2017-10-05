---
title: "Azure Active Directory: вопросы и ответы | Документация Майкрософт"
description: "В этой статье приводятся ответы на часто задаваемые вопросы, связанные с доступом к Azure и Azure Active Directory, управлением паролями и доступом к приложениям."
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
ms.openlocfilehash: 8d4460b3059558de2253c6f6a2d2fc8e7564d6d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="65753-103">Azure Active Directory: вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="65753-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="65753-104">Azure Active Directory — это комплексная служба идентификации (IDaaS), охватывающая все аспекты идентификации, управления доступом и безопасности.</span><span class="sxs-lookup"><span data-stu-id="65753-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="65753-105">Дополнительные сведения см. в статье [Что такое Microsoft Azure Active Directory](active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65753-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="65753-106">Доступ к Azure и Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65753-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="65753-107">**Вопрос. Почему при попытке получить доступ к Azure AD на классическом портале Azure появляется сообщение "Подписки не найдены"?**</span><span class="sxs-lookup"><span data-stu-id="65753-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure classic portal?**</span></span>

<span data-ttu-id="65753-108">**Ответ.** Для доступа к классическому порталу Azure каждому пользователю требуются разрешения в рамках подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="65753-108">**A:** To access the Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="65753-109">Если вы используете платную версию Office 365 или подписку Azure AD, перейдите на страницу [http://aka.ms/accessAAD](http://aka.ms/accessAAD) для одноразовой активации.</span><span class="sxs-lookup"><span data-stu-id="65753-109">If you have a paid Office 365 or Azure AD subscription, go to [http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="65753-110">В противном случае необходимо активировать бесплатную [учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/) или платную подписку.</span><span class="sxs-lookup"><span data-stu-id="65753-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="65753-111">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="65753-111">For more information, see:</span></span>

* [<span data-ttu-id="65753-112">Связь между подписками Azure и службой Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65753-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="65753-113">Управление каталогом для подписки Office 365 в Azure</span><span class="sxs-lookup"><span data-stu-id="65753-113">Manage the directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="65753-114">**Вопрос. Как связаны между собой Azure AD, Office 365 и Azure?**</span><span class="sxs-lookup"><span data-stu-id="65753-114">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="65753-115">**Ответ.** Azure AD предоставляет общие возможности идентификации и доступа для всех веб-служб.</span><span class="sxs-lookup"><span data-stu-id="65753-115">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span></span> <span data-ttu-id="65753-116">При использовании Office 365, Microsoft Azure, Intune или других служб Azure AD уже будет использоваться для включения единого входа и управления доступом для всех этих служб.</span><span class="sxs-lookup"><span data-stu-id="65753-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="65753-117">Все пользователи, которые могут использовать веб-службы, определяются как учетные записи пользователей в одном или нескольких экземплярах Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65753-117">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="65753-118">В этих учетных записях Azure AD можно настроить бесплатные возможности, такие как доступ к облачным приложениям.</span><span class="sxs-lookup"><span data-stu-id="65753-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="65753-119">Платные службы Azure AD (например, Enterprise Mobility + Security) дополняют веб-службы, такие как Office 365 и Microsoft Azure, комплексными решениями по управлению и обеспечению безопасности на уровне предприятия.</span><span class="sxs-lookup"><span data-stu-id="65753-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="65753-120">**Вопрос. Почему я могу войти на портал Azure, но не могу войти на классический портал?**</span><span class="sxs-lookup"><span data-stu-id="65753-120">**Q:  Why can I sign in to the Azure portal but not the Azure classic portal?**</span></span>

<span data-ttu-id="65753-121">**Ответ.** Для входа на портал Azure не требуется действующая подписка, а для входа на классический портал она нужна.</span><span class="sxs-lookup"><span data-stu-id="65753-121">**A:**  The Azure portal does not require a valid subscription, and the classic portal does require a valid subscription.</span></span>  <span data-ttu-id="65753-122">Если у вас нет подписки, вы не сможете войти на классический портал.</span><span class="sxs-lookup"><span data-stu-id="65753-122">If you do not have a subscription, you can't sign in to the classic portal.</span></span>
- - -
<span data-ttu-id="65753-123">**Вопрос. Чем отличаются подписки "Администратор" и "Администратор каталога"?**</span><span class="sxs-lookup"><span data-stu-id="65753-123">**Q:  What are the differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="65753-124">**Ответ.** По умолчанию при регистрации Azure вам назначается роль администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="65753-124">**A:** By default, you are assigned the Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="65753-125">Администратор подписки может использовать учетную запись Майкрософт либо рабочую или учебную учетную запись из каталога, с которым связана подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="65753-125">A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span></span>  <span data-ttu-id="65753-126">Эта роль дает право управлять службами на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="65753-126">This role is authorized to manage services in the Azure portal.</span></span>

<span data-ttu-id="65753-127">Если другим пользователям нужно войти в систему и получить доступ к службам с помощью той же подписки, их можно добавить как соадминистраторов.</span><span class="sxs-lookup"><span data-stu-id="65753-127">If others need to sign in and access services by using the same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="65753-128">Эта роль имеет те же права доступа, что и администратор службы, но не может менять связь подписок с каталогами Azure.</span><span class="sxs-lookup"><span data-stu-id="65753-128">This role has the same access privileges as the service admin, but can’t change the association of subscriptions to Azure directories.</span></span>  <span data-ttu-id="65753-129">Дополнительные сведения об администраторах подписок см. в статьях [Добавление или изменение ролей администратора Azure](../billing-add-change-azure-subscription-administrator.md) и [Связь между подписками Azure и службой Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="65753-129">For additional information on subscription admins, see [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="65753-130">Для управления функциями, связанными с каталогом и идентификацией, в Azure AD имеется другой набор ролей администратора.</span><span class="sxs-lookup"><span data-stu-id="65753-130">Azure AD has a different set of admin roles to manage the directory and identity-related features.</span></span>  <span data-ttu-id="65753-131">Эти администраторы будут иметь доступ к различным возможностям на портале Azure или на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="65753-131">These admins will have access to various features in the Azure portal or the Azure classic portal.</span></span> <span data-ttu-id="65753-132">Роль администраторов определяет их возможности, например создание или изменение пользователей, назначение административных ролей другим пользователям, сброс паролей пользователей, управление лицензиями пользователей или управление доменами.</span><span class="sxs-lookup"><span data-stu-id="65753-132">The admin's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="65753-133">Дополнительные сведения об администраторах каталогов Azure AD и их ролях см. в статье [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="65753-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="65753-134">Кроме того, платные службы Azure AD (например, Enterprise Mobility + Security) дополняют веб-службы, такие как Office 365 и Microsoft Azure, комплексными решениями по управлению и обеспечению безопасности на уровне предприятия.</span><span class="sxs-lookup"><span data-stu-id="65753-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="65753-135">**Вопрос. Существует ли отчет, показывающий, когда истекает срок действия пользовательских лицензий на Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="65753-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="65753-136">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="65753-136">**A:** No.</span></span>  <span data-ttu-id="65753-137">В настоящее время недоступно.</span><span class="sxs-lookup"><span data-stu-id="65753-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="65753-138">Начало работы с Hybrid Azure AD</span><span class="sxs-lookup"><span data-stu-id="65753-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="65753-139">**Вопрос. Каким образом можно выйти из клиента, если я добавлен в качестве участника совместной работы?**</span><span class="sxs-lookup"><span data-stu-id="65753-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="65753-140">**Ответ.** Если вы добавлены в клиент другой организации в качестве участника совместной работы, переключаться между клиентами можно с помощью переключателя в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="65753-140">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span></span>  <span data-ttu-id="65753-141">В настоящее время невозможно покинуть приглашающую организацию, но корпорация Майкрософт работает над добавлением такой возможности.</span><span class="sxs-lookup"><span data-stu-id="65753-141">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="65753-142">Пока эта функция недоступна, вы можете попросить приглашающую организацию удалить вас из их клиента.</span><span class="sxs-lookup"><span data-stu-id="65753-142">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span></span>
- - -
<span data-ttu-id="65753-143">**Вопрос. Как подключить локальный каталог к Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="65753-143">**Q: How can I connect my on-premises directory to Azure AD?**</span></span>

<span data-ttu-id="65753-144">**Ответ.** Вы можете подключить локальный каталог к Azure AD с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="65753-144">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="65753-145">Дополнительные сведения см. в статье [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="65753-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="65753-146">**Вопрос. Как настроить единый вход между локальным каталогом и облачными приложениями?**</span><span class="sxs-lookup"><span data-stu-id="65753-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="65753-147">**Ответ.** Вам нужно настроить только единый вход между локальным каталогом и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65753-147">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="65753-148">Если вы получаете доступ к облачным приложениям через Azure AD, служба автоматически помогает пользователям правильно пройти проверку подлинности с помощью учетных данных своей локальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="65753-148">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="65753-149">Единый вход из локальной сети можно легко реализовать благодаря решениям федерации, таким как службы федерации Active Directory (ADFS), или путем настройки синхронизации хэшей паролей. Вы можете легко развернуть оба варианта с помощью мастера настройки Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="65753-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="65753-150">Дополнительные сведения см. в статье [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="65753-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="65753-151">**Вопрос. Предусмотрен ли в Azure AD портал самообслуживания для пользователей в моей организации?**</span><span class="sxs-lookup"><span data-stu-id="65753-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="65753-152">**Ответ.** Да, в Azure AD есть [панель доступа к Azure AD](http://myapps.microsoft.com) для самообслуживания пользователей и доступа к приложениям.</span><span class="sxs-lookup"><span data-stu-id="65753-152">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="65753-153">Если вы являетесь клиентом Office 365, многие возможности вы найдете на портале Office 365.</span><span class="sxs-lookup"><span data-stu-id="65753-153">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span></span>

<span data-ttu-id="65753-154">Дополнительные сведения см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65753-154">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="65753-155">**Вопрос. Можно ли управлять локальной инфраструктурой с помощью Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="65753-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="65753-156">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="65753-156">**A:** Yes.</span></span> <span data-ttu-id="65753-157">В выпуске Azure AD Premium Edition доступна служба Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="65753-157">The Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="65753-158">Служба Azure AD Connect Health помогает отслеживать локальную инфраструктуру идентификации и службы синхронизации.</span><span class="sxs-lookup"><span data-stu-id="65753-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span></span>  

<span data-ttu-id="65753-159">Дополнительные сведения см. в статье [Мониторинг локальной инфраструктуры идентификации и служб синхронизации в облаке](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="65753-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="65753-160">Управление паролями</span><span class="sxs-lookup"><span data-stu-id="65753-160">Password management</span></span>
<span data-ttu-id="65753-161">**Вопрос. Можно ли использовать компонент обратной записи паролей Azure AD без синхронизации паролей? (Можно ли в этом случае использовать самостоятельный сброс пароля Azure AD с обратной записью паролей и не хранить пароли в облаке?)**</span><span class="sxs-lookup"><span data-stu-id="65753-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span></span>

<span data-ttu-id="65753-162">**Ответ.** Чтобы включить обратную запись, не нужно синхронизировать пароли Active Directory с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65753-162">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span></span> <span data-ttu-id="65753-163">В федеративной среде единый вход Azure AD использует локальный каталог для проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="65753-163">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span></span> <span data-ttu-id="65753-164">В этом сценарии не требуется отслеживание локального пароля в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65753-164">This scenario does not require the on-premises password to be tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="65753-165">**Вопрос. Сколько времени длится обратная запись пароля в локальную среду Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="65753-165">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span></span>

<span data-ttu-id="65753-166">**Ответ.** Обратная запись пароля выполняется в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="65753-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="65753-167">Дополнительные сведения см. в статье [Приступая к работе с компонентами управления паролями](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="65753-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="65753-168">**Вопрос. Можно ли использовать обратную запись паролей, которые управляются администратором?**</span><span class="sxs-lookup"><span data-stu-id="65753-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="65753-169">**Ответ.** Да. Если вы включили обратную запись паролей, операции, которые администратор выполняет с паролем, записываются обратно в локальную среду.</span><span class="sxs-lookup"><span data-stu-id="65753-169">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span></span>  

<span data-ttu-id="65753-170">Ответы на другие вопросы, связанные с паролями, см. в статье [Вопросы и ответы об управлении паролями](active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="65753-170">For more answers to password-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="65753-171">**Вопрос. Что делать, если я не могу вспомнить действующий пароль Office 365 или Azure AD при попытке изменить свой пароль?**</span><span class="sxs-lookup"><span data-stu-id="65753-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span></span>

<span data-ttu-id="65753-172">**Ответ.** В такой ситуации есть два варианта действий.</span><span class="sxs-lookup"><span data-stu-id="65753-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="65753-173">Используйте самостоятельный сброс пароля, если он доступен.</span><span class="sxs-lookup"><span data-stu-id="65753-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="65753-174">Функционирование самостоятельного сброса пароля зависит от настройки этой функции.</span><span class="sxs-lookup"><span data-stu-id="65753-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="65753-175">Дополнительные сведения см. в разделе о [принципах работы портала для сброса паролей](active-directory-passwords-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="65753-175">For more information, see [How does the password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="65753-176">Для пользователей Office 365 администраторы могут сбрасывать пароли, используя шаги, описанные в статье [Для администраторов: сброс паролей пользователей](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="65753-176">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="65753-177">Для учетных записей Azure AD администраторы могут сбрасывать пароли, используя один из вариантов:</span><span class="sxs-lookup"><span data-stu-id="65753-177">For Azure AD accounts, admins can reset passwords by using one of the following:</span></span>

- <span data-ttu-id="65753-178">[сброс учетных записей на портале Azure](active-directory-users-reset-password-azure-portal.md);</span><span class="sxs-lookup"><span data-stu-id="65753-178">[Reset accounts in the Azure portal](active-directory-users-reset-password-azure-portal.md)</span></span>
- <span data-ttu-id="65753-179">[сброс учетных записей на классическом портале](active-directory-create-users-reset-password.md);</span><span class="sxs-lookup"><span data-stu-id="65753-179">[Reset accounts in the classic portal](active-directory-create-users-reset-password.md)</span></span>
- [<span data-ttu-id="65753-180">Использование PowerShell</span><span class="sxs-lookup"><span data-stu-id="65753-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="65753-181">Безопасность</span><span class="sxs-lookup"><span data-stu-id="65753-181">Security</span></span>
<span data-ttu-id="65753-182">**Вопрос. Блокируются ли учетные записи после определенного числа неудачных попыток или используется более сложная стратегия?**</span><span class="sxs-lookup"><span data-stu-id="65753-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="65753-183">Мы используем более сложную стратегию для блокировки учетных записей.</span><span class="sxs-lookup"><span data-stu-id="65753-183">We use a more sophisticated strategy to lock accounts.</span></span>  <span data-ttu-id="65753-184">Она основана на IP-адресе запроса и введенном пароле.</span><span class="sxs-lookup"><span data-stu-id="65753-184">This is based on the IP of the request and the passwords entered.</span></span> <span data-ttu-id="65753-185">Если есть вероятность того, что это атака, длительность блокировки увеличивается.</span><span class="sxs-lookup"><span data-stu-id="65753-185">The duration of the lockout also increases based on the likelihood that it is an attack.</span></span>  

<span data-ttu-id="65753-186">**Вопрос. Определенные (общие) пароли отклоняются с сообщением о том, что этот пароль уже много раз использовался. Относится ли это к паролям, используемым в текущей службе Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="65753-186">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span></span></br>
<span data-ttu-id="65753-187">Это относится к глобально общим паролям, например все варианты слова Password и комбинации цифр 123456.</span><span class="sxs-lookup"><span data-stu-id="65753-187">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="65753-188">**Вопрос. Будет ли блокироваться запрос на вход в клиент B2C из сомнительных источников (ботнеты, конечная точка tor) или для этого требуется клиент выпуска Basic или Premium?**</span><span class="sxs-lookup"><span data-stu-id="65753-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="65753-189">У нас есть шлюз, который отфильтровывает запросы и предоставляет некоторую защиту от ботнетов и применяется для всех клиентов B2C.</span><span class="sxs-lookup"><span data-stu-id="65753-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="65753-190">Доступ к приложениям</span><span class="sxs-lookup"><span data-stu-id="65753-190">Application access</span></span>
<span data-ttu-id="65753-191">**Вопрос. Где можно найти список предварительно интегрированных с Azure AD приложений и их возможностей?**</span><span class="sxs-lookup"><span data-stu-id="65753-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="65753-192">**Ответ.** В Azure AD предварительно интегрировано более 2600 приложений корпорации Майкрософт, поставщиков услуг по предоставлению приложений в аренду (ASP) или партнеров.</span><span class="sxs-lookup"><span data-stu-id="65753-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="65753-193">Все предварительно интегрированные приложения поддерживают единый вход.</span><span class="sxs-lookup"><span data-stu-id="65753-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="65753-194">Единый вход позволяет использовать учетные данные организации для доступа к приложениям.</span><span class="sxs-lookup"><span data-stu-id="65753-194">SSO lets you use your organizational credentials to access your apps.</span></span> <span data-ttu-id="65753-195">Некоторые приложения также поддерживают автоматическую подготовку и отмену подготовки.</span><span class="sxs-lookup"><span data-stu-id="65753-195">Some of the applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="65753-196">Полный список предварительно интегрированных приложений см. в магазине [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="65753-196">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="65753-197">**Вопрос. Что делать, если в магазине Azure AD Marketplace нет нужного мне приложения?**</span><span class="sxs-lookup"><span data-stu-id="65753-197">**Q: What if the application I need is not in the Azure AD marketplace?**</span></span>

<span data-ttu-id="65753-198">**Ответ.** С помощью Azure AD Premium вы можете добавить и настроить любое приложение.</span><span class="sxs-lookup"><span data-stu-id="65753-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="65753-199">В зависимости от возможностей вашего приложения и своих предпочтений вы можете настроить единый вход и автоматическую подготовку.</span><span class="sxs-lookup"><span data-stu-id="65753-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="65753-200">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="65753-200">For more information, see:</span></span>

* [<span data-ttu-id="65753-201">Настройка единого входа для приложений, которых нет в коллекции приложений Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65753-201">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="65753-202">Автоматическая подготовка пользователей и групп из Azure Active Directory в приложениях с использованием SCIM</span><span class="sxs-lookup"><span data-stu-id="65753-202">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="65753-203">**Вопрос. Каким образом пользователи входят в приложения с помощью Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="65753-203">**Q: How do users sign in to applications by using Azure AD?**</span></span>

<span data-ttu-id="65753-204">**Ответ.** Azure AD поддерживает несколько способов просмотра приложений и доступа к ним, например:</span><span class="sxs-lookup"><span data-stu-id="65753-204">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span></span>

* <span data-ttu-id="65753-205">панель доступа Azure AD;</span><span class="sxs-lookup"><span data-stu-id="65753-205">The Azure AD access panel</span></span>
* <span data-ttu-id="65753-206">средство запуска приложений Office 365;</span><span class="sxs-lookup"><span data-stu-id="65753-206">The Office 365 application launcher</span></span>
* <span data-ttu-id="65753-207">прямой вход в федеративные приложения;</span><span class="sxs-lookup"><span data-stu-id="65753-207">Direct sign-in to federated apps</span></span>
* <span data-ttu-id="65753-208">прямые ссылки на федеративные приложения, приложения на основе пароля или существующие приложения;</span><span class="sxs-lookup"><span data-stu-id="65753-208">Deep links to federated, password-based, or existing apps</span></span>

<span data-ttu-id="65753-209">Дополнительные сведения см. в разделе [Развертывание интегрированных приложений Azure AD для пользователей](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="65753-209">For more information, see [Deploying Azure AD integrated applications to users](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="65753-210">**Вопрос. Как Azure AD обеспечивает проверку подлинности и единый вход для приложений?**</span><span class="sxs-lookup"><span data-stu-id="65753-210">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span></span>

<span data-ttu-id="65753-211">**Ответ.** Azure AD поддерживает множество стандартных протоколов для проверки подлинности и авторизации, например SAML 2.0, OpenID Connect, OAuth 2.0 и WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="65753-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="65753-212">В Azure AD также реализованы хранилища паролей и возможности автоматического входа для приложений, которые поддерживают только проверку подлинности на основе форм.</span><span class="sxs-lookup"><span data-stu-id="65753-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="65753-213">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="65753-213">For more information, see:</span></span>

* [<span data-ttu-id="65753-214">Сценарии аутентификации в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65753-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="65753-215">Протоколы проверки подлинности Active Directory</span><span class="sxs-lookup"><span data-stu-id="65753-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="65753-216">Принцип работы единого входа с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65753-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="65753-217">**Вопрос. Можно ли добавить приложения, которые я использую в локальной среде?**</span><span class="sxs-lookup"><span data-stu-id="65753-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="65753-218">**Ответ.** Прокси приложения Azure AD предоставляет надежный и безопасный доступ к локальным веб-приложениям, которые вы выбираете.</span><span class="sxs-lookup"><span data-stu-id="65753-218">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span></span> <span data-ttu-id="65753-219">К этим приложениям можно обращаться так же, как и к приложениям SaaS в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65753-219">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="65753-220">Нет необходимости использовать VPN или изменять инфраструктуру сети.</span><span class="sxs-lookup"><span data-stu-id="65753-220">There is no need for a VPN or to change your network infrastructure.</span></span>  

<span data-ttu-id="65753-221">Дополнительные сведения см. в статье [Как обеспечить безопасный удаленный доступ к локальным приложениям](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="65753-221">For more information, see [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="65753-222">**Вопрос. Как установить обязательное выполнение многофакторной идентификации для пользователей, обращающихся к конкретному приложению?**</span><span class="sxs-lookup"><span data-stu-id="65753-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="65753-223">**Ответ.** С помощью условного доступа Azure AD вы можете назначить уникальную политику доступа для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="65753-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="65753-224">В политике вы можете настроить обязательное выполнение многофакторной идентификации для всех пользователей или только для пользователей, не подключенных к локальной сети.</span><span class="sxs-lookup"><span data-stu-id="65753-224">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span></span>  

<span data-ttu-id="65753-225">Дополнительные сведения см. в статье [Условный доступ в Azure Active Directory](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="65753-225">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="65753-226">**Вопрос. Что такое автоматическая подготовка пользователей для приложений SaaS?**</span><span class="sxs-lookup"><span data-stu-id="65753-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="65753-227">**Ответ.** Служба Azure AD предоставляет возможность автоматизировать процесс создания, обслуживания и удаления удостоверений пользователей во многих популярных облачных приложениях SaaS.</span><span class="sxs-lookup"><span data-stu-id="65753-227">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="65753-228">Дополнительные сведения см. в статье [Автоматическая подготовка пользователей и ее отзыв для приложений SaaS в Azure Active Directory](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="65753-228">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="65753-229">**Вопрос. Можно ли установить безопасное подключение LDAP к Azure AD?** </span><span class="sxs-lookup"><span data-stu-id="65753-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="65753-230">**Ответ.** Нет.</span><span class="sxs-lookup"><span data-stu-id="65753-230">**A:**  No.</span></span> <span data-ttu-id="65753-231">Azure AD не поддерживает использование протокола LDAP.</span><span class="sxs-lookup"><span data-stu-id="65753-231">Azure AD does not support the LDAP protocol.</span></span>
