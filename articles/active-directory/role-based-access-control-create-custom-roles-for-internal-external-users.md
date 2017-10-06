---
title: "aaaCreate пользовательские роли для управления доступом на основе ролей и назначения toointernal и внешних пользователей в Azure | Документы Microsoft"
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
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="33891-103">Общие сведения об управлении доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="33891-103">Intro on role-based access control</span></span>

<span data-ttu-id="33891-104">Управление доступом на основе ролей функция Azure портала только разрешение hello владельцев подписки tooassign детализированных ролей tooother пользователи могут управлять областей определенного ресурса в своей среде.</span><span class="sxs-lookup"><span data-stu-id="33891-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="33891-105">RBAC позволяет более эффективного управления безопасности для крупных организаций, а также для SMB, работе с внешними участниками, поставщикам или freelancers, которым требуется доступ к ресурсам toospecific в вашей среде, но не обязательно toohello всей инфраструктуры или любой области действия, связанные с выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="33891-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="33891-106">RBAC обеспечивает гибкость hello владельцам одной подписки Azure под управлением учетной записи администратора hello (роль администратора служб на уровне подписки) и имеют несколько пользователей, которые приглашены toowork под hello но без одной подписке любое администратора права для него.</span><span class="sxs-lookup"><span data-stu-id="33891-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="33891-107">Для управления и выставления счетов функция RBAC hello доказывает toobe эффективный параметр времени и управления для использования Azure в различных сценариях.</span><span class="sxs-lookup"><span data-stu-id="33891-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33891-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="33891-108">Prerequisites</span></span>
<span data-ttu-id="33891-109">С помощью RBAC в среде Azure hello требуются:</span><span class="sxs-lookup"><span data-stu-id="33891-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="33891-110">Наличие автономного подписки Azure назначенный пользователь toohello имени владельца (роль подписка)</span><span class="sxs-lookup"><span data-stu-id="33891-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="33891-111">Роль владельца hello объекта hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="33891-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="33891-112">Имеет доступ toohello [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="33891-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="33891-113">Убедитесь, что следующие поставщики ресурсов hello toohave зарегистрирован для подписки пользователя hello: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="33891-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="33891-114">Дополнительные сведения о как tooregister hello поставщиков ресурсов см. в разделе [поставщиков диспетчеров ресурсов, регионы, версии API и схем](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="33891-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="33891-115">Подписки Office 365 или лицензии Azure Active Directory (например: доступ к Active Directory tooAzure) подготовленного портал не качества с помощью RBAC hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="33891-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="33891-116">Как можно использовать RBAC</span><span class="sxs-lookup"><span data-stu-id="33891-116">How can RBAC be used</span></span>
<span data-ttu-id="33891-117">RBAC можно применять в трех различных областях в Azure.</span><span class="sxs-lookup"><span data-stu-id="33891-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="33891-118">Из hello наибольший области toohello значением снизу к ним относится следующее:</span><span class="sxs-lookup"><span data-stu-id="33891-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="33891-119">подписка (самый высокий уровень доступа);</span><span class="sxs-lookup"><span data-stu-id="33891-119">Subscription (highest)</span></span>
* <span data-ttu-id="33891-120">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="33891-120">Resource group</span></span>
* <span data-ttu-id="33891-121">Область ресурсов (hello низкий уровень доступа предложения целевой разрешения tooan области отдельных ресурсов Azure)</span><span class="sxs-lookup"><span data-stu-id="33891-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="33891-122">Назначение ролей RBAC в области видимости hello подписки</span><span class="sxs-lookup"><span data-stu-id="33891-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="33891-123">Существует два распространенных примера использования RBAC (но это еще не все):</span><span class="sxs-lookup"><span data-stu-id="33891-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="33891-124">Внешние пользователи из организаций hello (не является частью пользователя admin hello клиента Azure Active Directory) приглашены toomanage определенные ресурсы или всей подписки hello</span><span class="sxs-lookup"><span data-stu-id="33891-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="33891-125">Работа с пользователями внутри организации hello (они являются частью hello Azure Active Directory клиента пользователя), но входит разными командами или группы, которым требуется детального доступа либо toohello всей подписки или toocertain группы ресурсов или ресурсов областей в hello Среда</span><span class="sxs-lookup"><span data-stu-id="33891-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="33891-126">Предоставление доступа на уровне подписки внешним пользователям Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33891-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="33891-127">RBAC роли могут быть предоставлены только в выпуске **владельцев** подписки hello таким образом hello admin пользователь должен быть подключен с именем пользователя, в которой это предварительно назначенной ролью или создал hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="33891-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="33891-128">Из hello портал Azure по окончании вход как администратор, выберите «Подписки» и выбрать hello требуемого один.</span><span class="sxs-lookup"><span data-stu-id="33891-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="33891-129">![колонке подписки на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) по умолчанию, если администратор hello приобрела hello подписки Azure hello пользователя будет показываться как **администратор учетной записи**, то выполняется роль hello подписки.</span><span class="sxs-lookup"><span data-stu-id="33891-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="33891-130">Дополнительные сведения о роли hello подписки Azure см. в разделе [добавить или изменить роли Администратор Azure, управлять hello подписки или службы](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="33891-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="33891-131">В этом примере hello пользователя «alflanigan@outlook.com» — hello **владельца** из hello «Бесплатной пробной версии» подписки в hello AAD клиента «По умолчанию клиента Azure».</span><span class="sxs-lookup"><span data-stu-id="33891-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="33891-132">Так как этот пользователь является создателем hello hello подписки Azure с hello начальной учетной записи Майкрософт «Outlook» (учетная запись Майкрософт = Outlook Live и т.д.) hello имя домена по умолчанию для всех пользователей, добавленные в этот клиент будет **«@alflaniganuoutlook.onmicrosoft.com»**.</span><span class="sxs-lookup"><span data-stu-id="33891-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="33891-133">Намеренно, синтаксис hello hello нового домена образуется путем объединения имя пользователя и домен hello hello пользователя, создавшего клиент hello и Добавление расширения hello **«. onmicrosoft.com»**.</span><span class="sxs-lookup"><span data-stu-id="33891-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="33891-134">Кроме того пользователи могут войти, используя имени пользовательского домена в клиенте hello после добавления и проверки его для нового клиента hello.</span><span class="sxs-lookup"><span data-stu-id="33891-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="33891-135">Дополнительные сведения о tooverify имени пользовательского домена в клиенте Azure Active Directory. в статье [добавить каталог tooyour имя пользовательского домена](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="33891-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="33891-136">В этом примере каталог hello» по умолчанию клиента Azure» содержит только пользователи с доменным именем hello «@alflanigan.onmicrosoft.com».</span><span class="sxs-lookup"><span data-stu-id="33891-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="33891-137">После выбора hello подписки, необходимо нажать кнопку hello пользователя с правами администратора **управления доступа (IAM)** и затем **добавить новую роль**.</span><span class="sxs-lookup"><span data-stu-id="33891-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Функция "Управление доступом (IAM)" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Параметр "Добавить новую роль" в области "Управление доступом (IAM)" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="33891-140">Hello следующим шагом является tooselect hello роли toobe назначенный и hello пользователя, которому будет назначен роли RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="33891-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="33891-141">В hello **роли** раскрывающегося меню hello admin пользователь видит только hello встроенных RBAC ролей, доступных в Azure.</span><span class="sxs-lookup"><span data-stu-id="33891-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="33891-142">Подробное описание каждой роли и их назначаемых областей см. в статье [Встроенные роли для управления доступом на основе ролей в Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="33891-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="33891-143">Hello пользователя с правами администратора, то требуется адрес электронной почты tooadd hello hello внешнего пользователя.</span><span class="sxs-lookup"><span data-stu-id="33891-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="33891-144">Hello ожидается, что поведение для hello внешнего пользователя toonot отображались в hello существующего клиента.</span><span class="sxs-lookup"><span data-stu-id="33891-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="33891-145">После приглашен hello внешнего пользователя, он будут отображаться в списке **подписки > управления доступа (IAM)** со всех hello текущих пользователей, назначенных в данный момент роли RBAC hello область подписки.</span><span class="sxs-lookup"><span data-stu-id="33891-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![Добавьте роль RBAC toonew разрешения](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Список ролей RBAC на уровне подписки](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="33891-148">пользователь Hello»chessercarlton@gmail.com» было приглашенных toobe **владельца** для подписки «Бесплатной пробной версии» hello.</span><span class="sxs-lookup"><span data-stu-id="33891-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="33891-149">После отправки приглашения hello, hello внешнего пользователя будет отправлено сообщение электронной почты со ссылкой активации.</span><span class="sxs-lookup"><span data-stu-id="33891-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="33891-150">![Приглашение по электронной почте стать участником роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="33891-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="33891-151">Возможности использования внешних toohello организации, hello новый пользователь не имеет существующие атрибуты в каталоге «По умолчанию клиента Azure» hello.</span><span class="sxs-lookup"><span data-stu-id="33891-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="33891-152">Они будут созданы после hello внешний пользователь предоставил согласие toobe записывается в каталог hello, связанный с подпиской hello, которой он назначен роли.</span><span class="sxs-lookup"><span data-stu-id="33891-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![Сообщение с приглашением стать участником роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="33891-154">Hello внешнего пользователя отображаются в hello клиента Azure Active Directory теперь как внешнего пользователя, с его можно просмотреть в hello портал Azure и hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="33891-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![Колонка пользователя Azure Active Directory на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Колонка пользователя Azure Active Directory на классическом портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="33891-157">В hello **пользователей** распознаваться представления в обоих порталов hello внешних пользователей:</span><span class="sxs-lookup"><span data-stu-id="33891-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="33891-158">Тип Hello другой значок в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="33891-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="33891-159">разные источники точки в классическом портале hello Hello</span><span class="sxs-lookup"><span data-stu-id="33891-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="33891-160">Однако предоставление **владельца** или **участника** tooan доступ внешних пользователей в hello **подписки** области, не допускает каталога toohello администратора hello доступа пользователей Если hello **глобального администратора** допускает это.</span><span class="sxs-lookup"><span data-stu-id="33891-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="33891-161">В свойства пользователя hello, hello **тип пользователя** содержит два общих параметра — **член** и **гостевой** можно определить.</span><span class="sxs-lookup"><span data-stu-id="33891-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="33891-162">Элемент — это пользователь, который регистрируется в каталоге hello, пока гостя является каталогом toohello пригласить пользователя из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="33891-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="33891-163">Дополнительные сведения см. в статье [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="33891-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="33891-164">Убедитесь в том, что после ввода учетных данных hello в портале hello, hello внешнего пользователя выбирает hello правильный каталог toosign на.</span><span class="sxs-lookup"><span data-stu-id="33891-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="33891-165">Hello одного пользователя может иметь доступа к каталогам toomultiple выберите один из них, щелкнув имя пользователя hello в верхнем правом углу hello в hello портал Azure и hello в раскрывающемся списке выберите нужный каталог hello.</span><span class="sxs-lookup"><span data-stu-id="33891-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="33891-166">Без значительной гостя в каталоге hello, hello внешнего пользователя можно осуществлять управление всеми ресурсами для hello подписки Azure, но не может получить доступ к каталогу hello.</span><span class="sxs-lookup"><span data-stu-id="33891-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![доступ к порталу Azure active directory ограниченных tooazure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="33891-168">Azure Active Directory и подписка Azure не имеют дочерних и родительских отношений, в отличие от других ресурсов Azure (например, виртуальные машины, виртуальные сети, веб-приложения, хранилище и т. д.), которые связаны с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="33891-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="33891-169">Все hello последний создан, управление и выставлен счет по подписке Azure, пока tooan доступа используется toomanage hello Azure directory подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="33891-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="33891-170">Дополнительные сведения см. в разделе [подписка Azure — это связанные tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="33891-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="33891-171">Из всех hello встроенных RBAC ролей **владельца** и **участника** предоставляют доступ полное управление tooall ресурсов в среде hello, hello различие, который участник не может создать и удалить новый RBAC роли.</span><span class="sxs-lookup"><span data-stu-id="33891-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="33891-172">Hello другие встроенные роли, например **участника виртуальной машины** обеспечивают полное управление доступ только имя hello, независимо от того, hello ресурсы toohello **группы ресурсов** они созданы в.</span><span class="sxs-lookup"><span data-stu-id="33891-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="33891-173">Назначение hello встроенных RBAC роль **участника виртуальной машины** на уровне подписки, означает этой роли hello hello, пользователь:</span><span class="sxs-lookup"><span data-stu-id="33891-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="33891-174">Можно просмотреть все виртуальные машины независимо от их развертывания даты и hello групп ресурсов, они являются частью</span><span class="sxs-lookup"><span data-stu-id="33891-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="33891-175">Имеет полный доступ toohello виртуальных машин управления в подписке hello</span><span class="sxs-lookup"><span data-stu-id="33891-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="33891-176">Не удается просмотреть любые другие типы ресурсов в подписке hello</span><span class="sxs-lookup"><span data-stu-id="33891-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="33891-177">не может изменять параметры выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="33891-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="33891-178">RBAC выполняется Azure портала единственный компонент не предоставляет доступа toohello классического портала.</span><span class="sxs-lookup"><span data-stu-id="33891-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="33891-179">Назначение встроенных RBAC роли tooan внешних пользователей</span><span class="sxs-lookup"><span data-stu-id="33891-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="33891-180">Для разных сценариев в этом тесте hello внешнего пользователя «alflanigan@gmail.com» добавляется в качестве **участника виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="33891-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![Встроенная роль "Участник виртуальных машин"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="33891-182">Hello обычное поведение для данного внешнего пользователя с этой ролью встроенных — toosee и управление ими только виртуальные машины и их смежные диспетчера ресурсов только ресурсы, необходимые во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="33891-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="33891-183">Изначально эти ограниченные роли предоставляют доступ только ресурсы корреспондент tootheir, созданные в hello портал Azure, независимо от некоторых можно будет развернуть hello классическом портале, а также (например: виртуальные машины).</span><span class="sxs-lookup"><span data-stu-id="33891-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![Обзор роли "Участник виртуальных машин" на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="33891-185">Предоставление доступа на уровне подписки для пользователя в hello таким же каталога</span><span class="sxs-lookup"><span data-stu-id="33891-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="33891-186">поток процесса Hello — идентичные tooadding внешнего пользователя, как hello перспективы предоставление hello RBAC ролью "Администратор", а также hello пользователя, которому предоставляется роль toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="33891-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="33891-187">различие Hello является hello пригласить пользователя не будет получать любые по электронной почте приглашения всех областей hello ресурсов в рамках подписки hello, будут доступны на панели мониторинга hello после входа в систему.</span><span class="sxs-lookup"><span data-stu-id="33891-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="33891-188">Назначение ролей RBAC в области группы ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="33891-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="33891-189">Назначение роли RBAC в **группы ресурсов** области имеется идентичные процесс для назначения hello роли на уровне подписки hello, для обоих типов пользователей - либо внешних или внутренних (частью hello один каталог).</span><span class="sxs-lookup"><span data-stu-id="33891-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="33891-190">Hello пользователей, назначенных роли RBAC hello: toosee в своей среде только группы ресурсов hello им была назначена доступ из hello **групп ресурсов** значок в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="33891-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="33891-191">Назначение ролей RBAC в области видимости ресурса hello</span><span class="sxs-lookup"><span data-stu-id="33891-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="33891-192">Назначение роли RBAC в области ресурсов в Azure имеется идентичные процесс для назначения hello роли на уровне подписки hello, или на уровне группы ресурсов hello, следующие hello же рабочего процесса для обоих сценариев.</span><span class="sxs-lookup"><span data-stu-id="33891-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="33891-193">Опять же, hello, назначенных роли RBAC hello пользователям только элементы hello, что они были назначены доступ, либо в hello **все ресурсы** вкладка или непосредственно в их мониторинга.</span><span class="sxs-lookup"><span data-stu-id="33891-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="33891-194">Важный аспект для RBAC и в области группы ресурсов или ресурсов области — для hello пользователей toomake toohello убедитесь, что toosign в правильный каталог.</span><span class="sxs-lookup"><span data-stu-id="33891-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![Вход в каталог на портале Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="33891-196">Назначение ролей RBAC группе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33891-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="33891-197">Все сценарии hello, с помощью RBAC в трех различных областях hello в привилегии hello предложение Azure управление, развертывание и администрирование различные ресурсы как назначенный пользователь без hello потребность в управлении личные подписки.</span><span class="sxs-lookup"><span data-stu-id="33891-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="33891-198">Для подписки, группы ресурсов или ресурсов области назначена роль RBAC hello независимо от того, все ресурсы hello, созданные далее в пользователями hello назначенный оплачиваются под hello одной подписки Azure где hello пользователи имеют доступ к.</span><span class="sxs-lookup"><span data-stu-id="33891-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="33891-199">Таким образом, hello пользователи, имеющие разрешения администратора для всей подписки Azure выставления счетов имеет полный обзор потребление hello, независимо от того, который управляет hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="33891-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="33891-200">Для более крупных организациях могут применяться роли RBAC в hello одинаково для группы Azure Active Directory, учитывая hello перспективы этого пользователя admin hello планирует toogrant hello детального доступа для группы или всей отделами, а не по отдельности для каждого пользователя, таким образом Учитывая его как очень времени и управления эффективный параметр.</span><span class="sxs-lookup"><span data-stu-id="33891-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="33891-201">tooillustrate этот пример, hello **участника** роли был добавлен tooone hello групп в клиенте hello на уровне подписки hello.</span><span class="sxs-lookup"><span data-stu-id="33891-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![Добавление роли RBAC группе AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="33891-203">Подготовка этих групп безопасности и управление ими выполняется только в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="33891-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="33891-204">Создайте пользовательскую поддержку tooopen роли RBAC запросов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="33891-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="33891-205">Hello встроенных RBAC ролей, которые доступны в Azure гарантировать определенные уровни разрешений, исходя из доступных ресурсов hello в среде hello.</span><span class="sxs-lookup"><span data-stu-id="33891-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="33891-206">Однако если эти роли соответствуют требованиям пользователя admin hello, есть еще больше, создав пользовательские роли RBAC доступа toolimit параметр hello.</span><span class="sxs-lookup"><span data-stu-id="33891-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="33891-207">Создание пользовательских ролей RBAC требует tootake одной встроенные роли, измените его, затем импортировать обратно в среду hello.</span><span class="sxs-lookup"><span data-stu-id="33891-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="33891-208">Hello загрузки и передачи роли hello управляются с помощью PowerShell или интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="33891-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="33891-209">Это важные toounderstand hello предварительные условия создания пользовательской роли, которые можно предоставлять детального доступа на уровне подписки hello и также обеспечивают гибкость hello hello пригласить пользователя по открытию запросов на получение поддержки.</span><span class="sxs-lookup"><span data-stu-id="33891-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="33891-210">Для этого примера hello встроенные роли **чтения** разрешающее tooview доступ для пользователей всех ресурсов hello областей, но не tooedit их или создавать новые был настроен tooallow hello пользователя hello можно открыть запросов поддержки.</span><span class="sxs-lookup"><span data-stu-id="33891-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="33891-211">Здравствуйте, первое действие экспорта hello **чтения** запускали toobe потребностей роль завершена в PowerShell с повышенными разрешениями от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="33891-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Снимок экрана PowerShell с ролью RBAC "Читатель"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="33891-213">Затем необходимо tooextract шаблона JSON hello hello роли.</span><span class="sxs-lookup"><span data-stu-id="33891-213">Then you need tooextract hello JSON template of hello role.</span></span>





![Шаблон JSON настраиваемой роли RBAC "Читатель"](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="33891-215">Типичная роль RBAC состоит из трех основных разделов: **Actions**, **NotActions** и **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="33891-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="33891-216">В hello **действия** разделе перечислены все hello разрешенных операций для этой роли.</span><span class="sxs-lookup"><span data-stu-id="33891-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="33891-217">Это важные toounderstand, назначенный каждого действия из поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="33891-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="33891-218">В этом случае для создания поддержки билеты hello **Microsoft.Support** должна быть в списке поставщика ресурсов.</span><span class="sxs-lookup"><span data-stu-id="33891-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="33891-219">возможности toosee toobe все Здравствуйте поставщиков ресурсов доступна и зарегистрирована в вашей подписке, можно использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33891-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="33891-220">Кроме того можно искать hello всех hello доступных PowerShell командлеты toomanage hello поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="33891-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="33891-221">![Снимок экрана PowerShell для управления поставщиком ресурсов](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="33891-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="33891-222">Здравствуйте, все действия для определенной роли RBAC ресурсов, перечисленных в разделе "hello" Поставщики toorestrict **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="33891-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="33891-223">И, наконец является обязательным, этой роли RBAC hello содержит явной подписки hello идентификаторов, где он используется.</span><span class="sxs-lookup"><span data-stu-id="33891-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="33891-224">Hello идентификаторы подписки отображаются в категории hello **AssignableScopes**, в противном случае вы не разрешаются tooimport hello роли в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="33891-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="33891-225">После создания и настройки роли RBAC hello, ему toobe импортированных назад hello среды.</span><span class="sxs-lookup"><span data-stu-id="33891-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="33891-226">В этом примере hello пользовательское имя для этой роли RBAC является «Чтения поддержки билеты уровнем доступа «допускающей hello пользователя tooview все данные в hello подписки, а также запросов поддержки tooopen.</span><span class="sxs-lookup"><span data-stu-id="33891-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="33891-227">Hello только два встроенных ролей RBAC, позволяя действие hello открывающие поддержки запросов, **владельца** и **участника**.</span><span class="sxs-lookup"><span data-stu-id="33891-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="33891-228">Для поддержки запросов может tooopen toobe пользователя он должна быть назначена RBAC только в области hello подписки, так как все запросы на поддержку создается подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="33891-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="33891-229">Новой пользовательской роли назначен пользователь tooan из hello один каталог.</span><span class="sxs-lookup"><span data-stu-id="33891-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![Снимок экрана пользовательской роли RBAC импортирована в hello портал Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Снимок экрана: назначение пользовательских импортированных toouser роли RBAC в hello один каталог](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Снимок экрана с разрешениями импортированной настраиваемой роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="33891-233">пример Hello был дополнительные ограничения hello подробные tooemphasize пользовательской роли RBAC следующим образом:</span><span class="sxs-lookup"><span data-stu-id="33891-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="33891-234">может создавать запросы в службу поддержки;</span><span class="sxs-lookup"><span data-stu-id="33891-234">Can create new support requests</span></span>
* <span data-ttu-id="33891-235">не может создавать области действия ресурсов (например, виртуальная машина);</span><span class="sxs-lookup"><span data-stu-id="33891-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="33891-236">не может создавать группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="33891-236">Can't create new resource groups</span></span>





![Снимок экрана настраиваемой роли RBAC, используемой для создания запросов в службу поддержки](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![Снимок экрана пользовательской роли RBAC не удается toocreate виртуальные машины](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![Снимок экрана пользовательской роли RBAC не удается toocreate нового RGs.](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="33891-240">Создайте пользовательскую поддержку tooopen роли RBAC запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="33891-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="33891-241">Запущен на компьютере Mac, а также без необходимости доступа к tooPowerShell, Azure CLI — toogo способом hello.</span><span class="sxs-lookup"><span data-stu-id="33891-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="33891-242">toocreate действия Hello пользовательской роли являются одинаковыми, с единственным исключением hello, с использованием интерфейса CLI hello роли не могут быть загружены в шаблон JSON, но его можно просмотреть в hello CLI приветствия.</span><span class="sxs-lookup"><span data-stu-id="33891-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="33891-243">В этом примере я выбрали hello встроенные роли **чтения резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="33891-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Снимок экрана интерфейса командной строки с ролью Backup Reader (Читатель резервных копий)](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="33891-245">Изменение роли hello в Visual Studio после копирования hello свойства в шаблоне JSON, hello **Microsoft.Support** поставщика ресурсов был добавлен в hello **действия** разделах, чтобы этот пользователь может открыть запросы на поддержку продолжая toobe чтения для hello резервными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="33891-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="33891-246">Еще раз это идентификатор подписки hello необходимые tooadd которых эта роль будет использоваться в hello **AssignableScopes** раздела.</span><span class="sxs-lookup"><span data-stu-id="33891-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Снимок экрана интерфейса командной строки во время импорта настраиваемой роли RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="33891-248">Новая роль Hello теперь доступен в hello портал Azure и процесса любые имена hello hello же, как в предыдущих примерах hello.</span><span class="sxs-lookup"><span data-stu-id="33891-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![Снимок экрана портала Azure с настраиваемой ролью RBAC, созданной с помощью CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="33891-250">Начиная с hello последней сборки 2017 г., hello оболочки облако Azure общедоступна.</span><span class="sxs-lookup"><span data-stu-id="33891-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="33891-251">Azure облачной оболочки — это дополнение tooIDE и hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="33891-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="33891-252">Эта служба предоставляет браузерную оболочку, проходящую аутентификацию и размещенную в Azure. Ее можно установить на компьютере вместо интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="33891-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
