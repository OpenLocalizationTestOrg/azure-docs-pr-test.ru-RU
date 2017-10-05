---
title: "Создание настраиваемых ролей управления доступом на основе ролей и их назначение внутренним и внешним пользователям в Azure | Документация Майкрософт"
description: "Назначение настраиваемых ролей RBAC, созданных с помощью PowerShell и интерфейса командной строки, внутренним и внешним пользователям."
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="ea358-103">Общие сведения об управлении доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="ea358-103">Intro on role-based access control</span></span>

<span data-ttu-id="ea358-104">Управление доступом на основе ролей (RBAC) — это единственная функция на портале Azure, с помощью которой владельцы подписки могут назначать роли другим пользователям, что позволяет им управлять определенными областями действия ресурсов в среде.</span><span class="sxs-lookup"><span data-stu-id="ea358-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="ea358-105">RBAC предоставляет расширенные возможности управления безопасностью для больших организаций, а также малых и средних предприятий, работающих с внешними сотрудниками, поставщиками или фрилансерами, которым требуется доступ к определенным ресурсам в среде, а не к целой инфраструктуре или любым областям, связанным с выставлением счетов.</span><span class="sxs-lookup"><span data-stu-id="ea358-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="ea358-106">Кроме того, RBAC обеспечивает гибкость владения подпиской Azure, управляемой с использованием учетной записи администратора (роль администратора службы на уровне подписки), и позволяет нескольким пользователям работать в рамках одной подписки, но без прав администратора.</span><span class="sxs-lookup"><span data-stu-id="ea358-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="ea358-107">Что касается управления и выставления счетов, функция RBAC гарантирует эффективное использование времени, а также предоставляет полезные возможности управления средой Azure в разных сценариях.</span><span class="sxs-lookup"><span data-stu-id="ea358-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea358-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea358-108">Prerequisites</span></span>
<span data-ttu-id="ea358-109">Чтобы реализовать возможности RBAC в среде Azure, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ea358-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="ea358-110">автономная подписка Azure, назначенная пользователю как владельцу (роль подписки);</span><span class="sxs-lookup"><span data-stu-id="ea358-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="ea358-111">роль владельца подписки Azure;</span><span class="sxs-lookup"><span data-stu-id="ea358-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="ea358-112">доступ к [порталу Azure](https://portal.azure.com);</span><span class="sxs-lookup"><span data-stu-id="ea358-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="ea358-113">поставщики ресурсов **Microsoft.Authorization**, зарегистрированные в подписке пользователя.</span><span class="sxs-lookup"><span data-stu-id="ea358-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="ea358-114">Дополнительные сведения о регистрации поставщиков ресурсов см. в статье [Поставщики диспетчера ресурсов, регионы, версии API и схемы](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="ea358-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ea358-115">Подписки Office 365 или лицензии Azure Active Directory (например, доступ к Azure Active Directory), подготовленные на портале O365, не поддерживают RBAC.</span><span class="sxs-lookup"><span data-stu-id="ea358-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="ea358-116">Как можно использовать RBAC</span><span class="sxs-lookup"><span data-stu-id="ea358-116">How can RBAC be used</span></span>
<span data-ttu-id="ea358-117">RBAC можно применять в трех различных областях в Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="ea358-118">Вот они (от самой высокой области действия до самой низкой):</span><span class="sxs-lookup"><span data-stu-id="ea358-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="ea358-119">подписка (самый высокий уровень доступа);</span><span class="sxs-lookup"><span data-stu-id="ea358-119">Subscription (highest)</span></span>
* <span data-ttu-id="ea358-120">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="ea358-120">Resource group</span></span>
* <span data-ttu-id="ea358-121">область действия ресурса (самый низкий уровень доступа с разрешениями на доступ к отдельной области действия ресурса Azure).</span><span class="sxs-lookup"><span data-stu-id="ea358-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="ea358-122">Назначение ролей RBAC в области действия подписки</span><span class="sxs-lookup"><span data-stu-id="ea358-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="ea358-123">Существует два распространенных примера использования RBAC (но это еще не все):</span><span class="sxs-lookup"><span data-stu-id="ea358-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="ea358-124">При работе с внешними пользователями организации, которые не являются частью клиента Azure Active Directory администратора и которым предоставляется доступ на управление определенными ресурсами или целой подпиской.</span><span class="sxs-lookup"><span data-stu-id="ea358-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="ea358-125">При работе с пользователями в организации, которые являются частью клиента Azure Active Directory пользователя, но входят в разные команды или группы и им требуется доступ к целой подписке или определенным группам ресурсов (областям действия ресурсов) в среде.</span><span class="sxs-lookup"><span data-stu-id="ea358-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="ea358-126">Предоставление доступа на уровне подписки внешним пользователям Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea358-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="ea358-127">Роли RBAC можно назначать только **владельцам** подписки, поэтому администратор должен войти в систему, используя имя пользователя, которому заранее назначена эта роль, или имя пользователя, используемое при создании подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="ea358-128">Войдите на портал Azure как администратор. Выберите "Подписки", а затем выберите необходимую подписку.</span><span class="sxs-lookup"><span data-stu-id="ea358-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="ea358-129">![Колонка подписки на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) По умолчанию администратору, который приобрел подписку Azure, назначается роль **администратора учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="ea358-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="ea358-130">Сведения о ролях подписки Azure см. в статье [Добавление или изменение ролей администратора Azure, управляющих подписками и службами](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="ea358-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="ea358-131">В этом примере пользователь alflanigan@outlook.com является **владельцем** бесплатной пробной версии подписки в клиенте AAD (каталог Default tenant Azure (Клиент Azure по умолчанию)).</span><span class="sxs-lookup"><span data-stu-id="ea358-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="ea358-132">Так как этот пользователь создал подписку Azure, используя начальную учетную запись Microsoft Outlook, после добавления других пользователей в этот клиент к их учетной записи будет добавляться следующее доменное имя (по умолчанию):  **@alflaniganuoutlook.onmicrosoft.com** .</span><span class="sxs-lookup"><span data-stu-id="ea358-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="ea358-133">Новое доменное имя состоит из имени пользователя и доменного имени пользователя, создавшего клиент, а также расширения **.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="ea358-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="ea358-134">Кроме того, пользователи могут войти в систему, используя имя личного домена в клиенте. Для этого сначала необходимо добавить это имя в новый клиент, а затем проверить.</span><span class="sxs-lookup"><span data-stu-id="ea358-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="ea358-135">Дополнительные сведения о проверке имени личного домена в клиенте Azure Active Directory см. в [этой статье](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="ea358-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="ea358-136">В этом примере в каталоге Default tenant Azure (Клиент Azure по умолчанию) содержатся только пользователи с доменным именем @alflanigan.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="ea358-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="ea358-137">После выбора подписки администратор должен щелкнуть **Управление доступом (IAM)** и выбрать **Добавить новую роль**.</span><span class="sxs-lookup"><span data-stu-id="ea358-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Функция "Управление доступом (IAM)" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Параметр "Добавить новую роль" в области "Управление доступом (IAM)" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="ea358-140">Далее необходимо выбрать роль RBAC и пользователя, которому ее нужно назначить.</span><span class="sxs-lookup"><span data-stu-id="ea358-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="ea358-141">В раскрывающемся меню **Роль** для администратора отображаются только встроенные роли RBAC, доступные в Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="ea358-142">Подробное описание каждой роли и их назначаемых областей см. в статье [Встроенные роли для управления доступом на основе ролей в Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ea358-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="ea358-143">Затем необходимо добавить адрес электронной почты внешнего пользователя.</span><span class="sxs-lookup"><span data-stu-id="ea358-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="ea358-144">Этот внешний пользователь не должен отображаться в имеющемся клиенте.</span><span class="sxs-lookup"><span data-stu-id="ea358-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="ea358-145">Приглашенные пользователи, а также все текущие пользователи с ролью RBAC в области действия подписки отображаются в области **"Подписки > Управление доступом (IAM)"**.</span><span class="sxs-lookup"><span data-stu-id="ea358-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![Добавить разрешения в новую роль RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Список ролей RBAC на уровне подписки](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="ea358-148">Пользователя chessercarlton@gmail.com пригласили стать **владельцем** бесплатной пробной версии подписки.</span><span class="sxs-lookup"><span data-stu-id="ea358-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="ea358-149">После отправки приглашения внешний пользователь получит письмо со ссылкой активации.</span><span class="sxs-lookup"><span data-stu-id="ea358-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="ea358-150">![Приглашение по электронной почте стать участником роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="ea358-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="ea358-151">Новые внешние пользователи организации не имеют атрибутов в каталоге Default tenant Azure (Клиент Azure по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="ea358-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="ea358-152">Все атрибуты создаются после предоставления этому пользователю разрешений на запись в каталоге, который связан с подпиской с назначенной ролью.</span><span class="sxs-lookup"><span data-stu-id="ea358-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![Сообщение с приглашением стать участником роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="ea358-154">В дальнейшем этот пользователь отображается в клиенте Azure Active Directory как внешний. Это можно посмотреть на портале Azure и на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![Колонка пользователя Azure Active Directory на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Колонка пользователя Azure Active Directory на классическом портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="ea358-157">В представлении **Пользователи** на обоих порталах внешних пользователей можно распознать по следующему:</span><span class="sxs-lookup"><span data-stu-id="ea358-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="ea358-158">разные типы значков на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="ea358-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="ea358-159">разные источники на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="ea358-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="ea358-160">Тем не менее внешний пользователь с ролью **Владелец** или **Участник** в области действия **подписки** не имеет доступа к каталогу администратора, если это разрешение ему не предоставит **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="ea358-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="ea358-161">В свойствах пользователя можно определить параметр **Тип пользователя**, который имеет два значения: **Участник** и **Гость**.</span><span class="sxs-lookup"><span data-stu-id="ea358-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="ea358-162">Участник — это зарегистрированный в каталоге пользователь, а гость — это пользователь, приглашенный в каталог из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="ea358-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="ea358-163">Дополнительные сведения см. в статье [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="ea358-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="ea358-164">Убедитесь, что после ввода учетных данных на портале внешний пользователь входит в нужный каталог.</span><span class="sxs-lookup"><span data-stu-id="ea358-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="ea358-165">Тот же пользователь может иметь доступ к нескольким каталогам и может войти в любой из них, щелкнув имя пользователя в верхнем правом углу на портале Azure и выбрав в раскрывающемся списке нужный каталог.</span><span class="sxs-lookup"><span data-stu-id="ea358-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="ea358-166">Будучи гостем, внешний пользователь может управлять всеми ресурсами в подписке Azure, но не имеет доступа к каталогу.</span><span class="sxs-lookup"><span data-stu-id="ea358-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![Доступ к каталогу Azure Active Directory на портале Azure ограничен](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="ea358-168">Azure Active Directory и подписка Azure не имеют дочерних и родительских отношений, в отличие от других ресурсов Azure (например, виртуальные машины, виртуальные сети, веб-приложения, хранилище и т. д.), которые связаны с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="ea358-169">Создание этих ресурсов, выставление счетов за использование и управление ими выполняется в рамках подписки Azure, а сама подписка используется для управления доступом к каталогу Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="ea358-170">Дополнительные сведения см. в статье [Связь между подписками Azure и службой Azure Active Directory](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="ea358-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="ea358-171">Из всех встроенных ролей RBAC только роли **Владелец** и **Участник** предлагают возможности полного доступа к управлению всеми ресурсами в среде. Разница между ними заключается в том, что участник не может создавать и удалять роли RBAC.</span><span class="sxs-lookup"><span data-stu-id="ea358-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="ea358-172">Другие встроенные роли, например **Участник виртуальных машин**, обеспечивают доступ к управлению только теми ресурсами, которые указаны в названиях этих ролей, вне зависимости от **группы ресурсов**, используемой при их создании.</span><span class="sxs-lookup"><span data-stu-id="ea358-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="ea358-173">К пользователю с ролью **Участник виртуальных машин**, назначенной на уровне подписки, применяются следующие разрешения и ограничения:</span><span class="sxs-lookup"><span data-stu-id="ea358-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="ea358-174">просматривать все виртуальные машины независимо от даты их развертывания и группы ресурсов, к которой они принадлежат;</span><span class="sxs-lookup"><span data-stu-id="ea358-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="ea358-175">полный доступ к управлению виртуальными машинами в подписке;</span><span class="sxs-lookup"><span data-stu-id="ea358-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="ea358-176">не может просматривать другие типы ресурсов в подписке;</span><span class="sxs-lookup"><span data-stu-id="ea358-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="ea358-177">не может изменять параметры выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="ea358-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="ea358-178">Функция RBAC доступна только на портале Azure. Она не предоставляет доступ к классическому порталу.</span><span class="sxs-lookup"><span data-stu-id="ea358-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="ea358-179">Назначение встроенной роли RBAC внешним пользователям</span><span class="sxs-lookup"><span data-stu-id="ea358-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="ea358-180">Для оценки разных сценариев внешнему пользователю alflanigan@gmail.com назначили роль **Участник виртуальных машин**.</span><span class="sxs-lookup"><span data-stu-id="ea358-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![Встроенная роль "Участник виртуальных машин"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="ea358-182">Внешний пользователь с этой встроенной ролью может просматривать только виртуальные машины и ресурсы Resource Manager, необходимые во время развертывания, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="ea358-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="ea358-183">Эти роли с ограниченными правами обеспечивают доступ только к соответствующим ресурсам, созданным на портале Azure, хотя развертывание некоторых из них, например виртуальных машин, могло также выполняться на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="ea358-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![Обзор роли "Участник виртуальных машин" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="ea358-185">Предоставление доступа на уровне подписки пользователям в том же каталоге</span><span class="sxs-lookup"><span data-stu-id="ea358-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="ea358-186">Этот процесс аналогичен добавлению внешнего пользователя и в отношении администратора, предоставляющего роль RBAC, и пользователя, которому эта роль назначается.</span><span class="sxs-lookup"><span data-stu-id="ea358-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="ea358-187">Отличие заключается в том, что приглашенный пользователь не получит приглашение по электронной почте, так как после входа все области действия ресурсов в подписке будут доступны на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ea358-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="ea358-188">Назначение ролей RBAC в области действия группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="ea358-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="ea358-189">Процесс назначения роли RBAC внешним и внутренним пользователям (в том же каталоге) в области действия **группы ресурсов** и на уровне подписки аналогичен.</span><span class="sxs-lookup"><span data-stu-id="ea358-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="ea358-190">Пользователи с ролью RBAC могут просматривать в среде только группу ресурсов, к которой им предоставлен доступ, щелкнув значок **Группы ресурсов** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="ea358-191">Назначение ролей RBAC в области действия ресурсов</span><span class="sxs-lookup"><span data-stu-id="ea358-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="ea358-192">Процесс назначения роли RBAC в области действия ресурсов, на уровне подписки и на уровне группы ресурсов аналогичен. В обоих сценариях используется тот же рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="ea358-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="ea358-193">Опять же, пользователи с ролью RBAC могут просматривать только те элементы, к которым им предоставлен доступ. Эти ресурсы отображаются на вкладке **Все ресурсы** или непосредственно на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ea358-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="ea358-194">Важный аспект, который следует учитывать при назначении роли RBAC на уровне группы ресурсов или на уровне ресурсов, — это то, что пользователи должны войти в нужный каталог.</span><span class="sxs-lookup"><span data-stu-id="ea358-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![Вход в каталог на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="ea358-196">Назначение ролей RBAC группе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea358-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="ea358-197">Все сценарии с использованием ролей RBAC на трех различных уровнях в Azure обеспечивают права на развертывание, администрирование различных ресурсов и управление ими, не управляя личной подпиской.</span><span class="sxs-lookup"><span data-stu-id="ea358-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="ea358-198">Независимо от того, назначена ли роль RBAC на уровне подписки, группы ресурсов или ресурса, все созданные пользователями ресурсы оплачиваются в рамках подписки Azure, к которой они имеют доступ.</span><span class="sxs-lookup"><span data-stu-id="ea358-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="ea358-199">Таким образом, пользователи с правами администратора выставления счетов всей подписки Azure имеют полное представление о потреблении ресурсов, независимо от того, кто ими управляет.</span><span class="sxs-lookup"><span data-stu-id="ea358-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="ea358-200">В более крупных организациях роли RBAC можно таким же образом применять к группам Azure Active Directory, учитывая то, что администраторы хотят предоставлять доступ командам или целым отделам, а не отдельно каждому пользователю. Это позволяет эффективно использовать время, а также предоставляет полезные возможности управления.</span><span class="sxs-lookup"><span data-stu-id="ea358-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="ea358-201">Чтобы проиллюстрировать этот момент, мы назначили одной из групп в клиенте роль **Участник** на уровне подписки.</span><span class="sxs-lookup"><span data-stu-id="ea358-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![Добавление роли RBAC группе AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="ea358-203">Подготовка этих групп безопасности и управление ими выполняется только в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea358-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="ea358-204">Создание настраиваемой роли RBAC с разрешением на открытие запросов в службу поддержки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea358-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="ea358-205">Встроенные роли RBAC, доступные в Azure, предоставляют определенные уровни разрешений, исходя из доступных ресурсов в среде.</span><span class="sxs-lookup"><span data-stu-id="ea358-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="ea358-206">Но если эти роли не соответствуют требованиям администратора, доступ можно ограничить еще больше, создав настраиваемые роли RBAC.</span><span class="sxs-lookup"><span data-stu-id="ea358-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="ea358-207">Создание настраиваемых ролей RBAC подразумевает изменение одной из встроенных ролей RBAC и ее возвращение в среду.</span><span class="sxs-lookup"><span data-stu-id="ea358-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="ea358-208">Скачивание и отправка роли осуществляется с помощью PowerShell или интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="ea358-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="ea358-209">При создании настраиваемой роли, которая предоставляет доступ на уровне подписки, а также позволяет приглашенным пользователям открывать запросы в службу поддержки, важно учитывать предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="ea358-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="ea358-210">В этом примере мы настроили встроенную роль **Читатель**, которая позволяет пользователям просматривать все области действия ресурсов, но не создавать или изменять их, и добавили в нее разрешение на открытие запросов в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="ea358-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="ea358-211">Первое действие при экспорте роли **Читатель** выполняется в среде PowerShell, запущенной с повышенным уровнем разрешений (от имени администратора).</span><span class="sxs-lookup"><span data-stu-id="ea358-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Снимок экрана PowerShell с ролью RBAC "Читатель"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="ea358-213">Затем необходимо извлечь шаблон JSON роли.</span><span class="sxs-lookup"><span data-stu-id="ea358-213">Then you need to extract the JSON template of the role.</span></span>





![Шаблон JSON настраиваемой роли RBAC "Читатель"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="ea358-215">Типичная роль RBAC состоит из трех основных разделов: **Actions**, **NotActions** и **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="ea358-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="ea358-216">В разделе **Actions** перечислены все разрешенные операции этой роли.</span><span class="sxs-lookup"><span data-stu-id="ea358-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="ea358-217">Важно понимать, что каждое действие назначается из поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ea358-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="ea358-218">В этом случае для создания запросов в службу поддержки в списке должен находиться поставщик ресурсов **Microsoft.Support**.</span><span class="sxs-lookup"><span data-stu-id="ea358-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="ea358-219">Чтобы просмотреть все доступные и зарегистрированные в подписке поставщики ресурсов, можно использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea358-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="ea358-220">Кроме того, вы также можете проверить все доступные командлеты PowerShell для управления поставщиками ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ea358-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="ea358-221">![Снимок экрана PowerShell для управления поставщиком ресурсов](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="ea358-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="ea358-222">Чтобы ограничить все действия конкретной роли RBAC, поставщики ресурсов перечислены в разделе **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="ea358-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="ea358-223">И наконец, роль RBAC обязательно должна содержать явные идентификаторы подписки, в которой она назначена.</span><span class="sxs-lookup"><span data-stu-id="ea358-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="ea358-224">Идентификаторы подписки перечислены в разделе **AssignableScopes**. Если они не указаны, вы не сможете импортировать роль в подписку.</span><span class="sxs-lookup"><span data-stu-id="ea358-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="ea358-225">После создания и настройки роли RBAC их необходимо импортировать обратно в среду.</span><span class="sxs-lookup"><span data-stu-id="ea358-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="ea358-226">В этом примере мы присвоили этой настраиваемой роли RBAC имя Reader support tickets access level. Пользователи с этой ролью могут просматривать все ресурсы в подписке, а также открывать запросы в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="ea358-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="ea358-227">Только две встроенные роли RBAC позволяют открывать запросы в службу поддержки: **Владелец** и **Участник**.</span><span class="sxs-lookup"><span data-stu-id="ea358-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="ea358-228">Чтобы разрешить пользователю открывать запросы в службу поддержки, ему необходимо назначить роль RBAC только на уровне подписки, так как все эти запросы создаются на основе подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="ea358-229">Мы назначили эту новую настраиваемую роль пользователю в том же каталоге.</span><span class="sxs-lookup"><span data-stu-id="ea358-229">This new custom role has been assigned to an user from the same directory.</span></span>





![Снимок экрана настраиваемой роли RBAC, импортированной на портал Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Снимок экрана назначения импортированной настраиваемой роли RBAC пользователю в том же каталоге](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Снимок экрана с разрешениями импортированной настраиваемой роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="ea358-233">Примеры разрешений и ограничений настраиваемой роли RBAC (дополнительные сведения об ограничениях см. ниже):</span><span class="sxs-lookup"><span data-stu-id="ea358-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="ea358-234">может создавать запросы в службу поддержки;</span><span class="sxs-lookup"><span data-stu-id="ea358-234">Can create new support requests</span></span>
* <span data-ttu-id="ea358-235">не может создавать области действия ресурсов (например, виртуальная машина);</span><span class="sxs-lookup"><span data-stu-id="ea358-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="ea358-236">не может создавать группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ea358-236">Can't create new resource groups</span></span>





![Снимок экрана настраиваемой роли RBAC, используемой для создания запросов в службу поддержки](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![Снимок экрана настраиваемой роли RBAC, которая не имеет разрешений на создание виртуальных машин](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![Снимок экрана настраиваемой роли RBAC, которая не имеет разрешений на создание групп ресурсов](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="ea358-240">Создание настраиваемой роли RBAC с разрешением на открытие запросов в службу поддержки с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ea358-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="ea358-241">На компьютерах Mac, на которых нет доступа к PowerShell, создать настраиваемую роль можно с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ea358-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="ea358-242">Процесс создания аналогичен. Единственное отличие заключается в том, что при использовании интерфейса командной строки вы не сможете скачать шаблон JSON, но его можно просмотреть.</span><span class="sxs-lookup"><span data-stu-id="ea358-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="ea358-243">В этом примере мы используем встроенную роль **Backup Reader** (Читатель резервных копий).</span><span class="sxs-lookup"><span data-stu-id="ea358-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Снимок экрана интерфейса командной строки с ролью Backup Reader (Читатель резервных копий)](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="ea358-245">Чтобы добавить разрешение на открытие запросов в службу поддержки, необходимо скопировать свойства в шаблоне JSON и изменить роль в Visual Studio, а затем добавить поставщик ресурсов **Microsoft.Support** в разделы **Actions**. При этом пользователю по-прежнему будет назначена роль читателя в резервных хранилищах.</span><span class="sxs-lookup"><span data-stu-id="ea358-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="ea358-246">Кроме того, необходимо добавить идентификатор подписки, в которой эта роль будет назначена, в разделе **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="ea358-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Снимок экрана интерфейса командной строки во время импорта настраиваемой роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="ea358-248">Новая роль теперь доступна на портале Azure. Процесс назначения такой же, как и в предыдущих примерах.</span><span class="sxs-lookup"><span data-stu-id="ea358-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![Снимок экрана портала Azure с настраиваемой ролью RBAC, созданной с помощью CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="ea358-250">По данным конференции Build 2017 служба Azure Cloud Shell теперь общедоступна.</span><span class="sxs-lookup"><span data-stu-id="ea358-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="ea358-251">Azure Cloud Shell — это дополнение к IDE и порталу Azure.</span><span class="sxs-lookup"><span data-stu-id="ea358-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="ea358-252">Эта служба предоставляет браузерную оболочку, проходящую аутентификацию и размещенную в Azure. Ее можно установить на компьютере вместо интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="ea358-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
