---
title: "aaaCreate Azure Automation учетные записи запуска от | Документы Microsoft"
description: "В этой статье описывается как tooupdate автоматической учетной записи или создайте учетные записи запуска от имени с помощью PowerShell или с портала hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="9edd6-103">Обновление проверки подлинности учетных записей службы автоматизации с использованием учетных записей запуска от имени</span><span class="sxs-lookup"><span data-stu-id="9edd6-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="9edd6-104">Вы можете обновить существующую учетную запись автоматизации с портала hello или используйте PowerShell, если:</span><span class="sxs-lookup"><span data-stu-id="9edd6-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="9edd6-105">Создание учетной записи автоматизации, но отклонить toocreate hello запуска от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9edd6-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="9edd6-106">Ресурсы диспетчера ресурсов автоматизации toomanage учетной записи уже используется, и требуется tooupdate hello tooinclude hello запуска от имени учетной записи для проверки подлинности runbook.</span><span class="sxs-lookup"><span data-stu-id="9edd6-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="9edd6-107">Учетная запись автоматизации toomanage классические ресурсы уже используется и нужно tooupdate его toouse hello классический запуска от имени учетной записи вместо создания новой учетной записи и переход к tooit Runbook и активов.</span><span class="sxs-lookup"><span data-stu-id="9edd6-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="9edd6-108">Требуется toocreate запуска от имени, а классические учетной записи запуска с помощью сертификата, выданного вашего центра сертификации предприятия (ЦС).</span><span class="sxs-lookup"><span data-stu-id="9edd6-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9edd6-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9edd6-109">Prerequisites</span></span>

* <span data-ttu-id="9edd6-110">Hello сценарий может быть запущена только в Windows 10 и Windows Server 2016 с модулями Azure Resource Manager 3.0.0 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="9edd6-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="9edd6-111">Более ранние версии Windows не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9edd6-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="9edd6-112">Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="9edd6-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="9edd6-113">Сведения о выпуске hello PowerShell 1.0 см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="9edd6-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="9edd6-114">Учетная запись автоматизации, на которую ссылается как значение hello для hello *— AutomationAccountName* и *- ApplicationDisplayName* параметры в следующем скрипте PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="9edd6-115">tooget hello значения для *SubscriptionID*, *ResourceGroup*, и *AutomationAccountName*, которой являются обязательными параметрами для скрипта hello, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="9edd6-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="9edd6-116">В hello портал Azure, выберите учетную запись автоматизации на hello **учетной записи автоматизации** колонки, а затем выберите **все параметры**.</span><span class="sxs-lookup"><span data-stu-id="9edd6-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="9edd6-117">На hello **все параметры** колонки в разделе **параметры учетной записи**выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="9edd6-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="9edd6-118">Запишите значения hello на hello **свойства** колонку.</span><span class="sxs-lookup"><span data-stu-id="9edd6-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="9edd6-119">![колонку «Свойства» учетной записи автоматизации Hello](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="9edd6-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="9edd6-120">Необходимые разрешения tooupdate ваша учетная запись автоматизации</span><span class="sxs-lookup"><span data-stu-id="9edd6-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="9edd6-121">tooupdate учетной записи автоматизации, должны иметь hello следующие специальные права и разрешения, необходимые toocomplete в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="9edd6-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="9edd6-122">Учетная запись пользователя AD должен toobe добавлены tooa роль с роль участника toohello эквивалентные разрешения Microsoft.Automation ресурсов, как описано в статье [управления доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="9edd6-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="9edd6-123">Пользователи без прав администратора в клиенте Azure AD могут [регистрировать приложения AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) при регистрации приложения hello параметра установлено слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="9edd6-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="9edd6-124">Если параметр регистрации приложения hello задано слишком**нет**, hello пользователь, выполняющий это действие должно быть глобальным администратором в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9edd6-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="9edd6-125">Если вы не является членом экземпляра Active Directory hello подписки до добавления toohello глобальный администратор или соадминистратор роли hello подписки, tooActive Directory добавляются как Гость.</span><span class="sxs-lookup"><span data-stu-id="9edd6-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="9edd6-126">В этом случае вы получите «у вас разрешения toocreate...»</span><span class="sxs-lookup"><span data-stu-id="9edd6-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="9edd6-127">Предупреждение, hello **Добавление учетной записи автоматизации** колонку.</span><span class="sxs-lookup"><span data-stu-id="9edd6-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="9edd6-128">Пользователи, добавленные toohello глобальный администратор или соадминистратор роль сначала можно удалить из экземпляра Active Directory hello подписки и повторно добавлен toomake их полный пользователя в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9edd6-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="9edd6-129">tooverify этой ситуации из hello **Azure Active Directory** панели hello Azure portal, **пользователей и групп**выберите **всех пользователей** и после выбора hello конкретного пользователя, **профиль**.</span><span class="sxs-lookup"><span data-stu-id="9edd6-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="9edd6-130">Здравствуйте, значение hello **тип пользователя** атрибут профиля hello пользователи не должны быть равны **гостевой**.</span><span class="sxs-lookup"><span data-stu-id="9edd6-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="9edd6-131">Создание учетной записи запуска от имени с портала hello</span><span class="sxs-lookup"><span data-stu-id="9edd6-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="9edd6-132">В этом разделе выполняйте следующие действия tooupdate hello учетной записи службы автоматизации Azure hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9edd6-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="9edd6-133">Создается hello учетные записи запуска от имени и классический запуска от имени по отдельности, и toomanage ресурсы в классический портал Azure hello не нужны, можно просто создать hello Azure Запуск от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9edd6-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="9edd6-134">процесс Hello создает hello следующих элементов в учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="9edd6-135">**Для учетной записи запуска от имени:**</span><span class="sxs-lookup"><span data-stu-id="9edd6-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="9edd6-136">Создание приложения Azure AD с помощью самозаверяющего сертификата, создает учетную запись участника службы для приложения hello в Azure AD и назначает hello роль участника для учетной записи hello в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="9edd6-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="9edd6-137">Можно изменить этот параметр tooOwner или любая другая роль.</span><span class="sxs-lookup"><span data-stu-id="9edd6-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="9edd6-138">Дополнительные сведения см. в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="9edd6-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="9edd6-139">Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureRunAsCertificate* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="9edd6-140">Hello активов сертификат содержит закрытый ключ сертификата hello, используемого приложением hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9edd6-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="9edd6-141">Создает ресурс подключения автоматизации с именем *AzureRunAsConnection* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="9edd6-142">ресурс-контейнер подключений Hello содержит идентификатор приложения hello, идентификатора клиента, идентификатор подписки и отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="9edd6-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="9edd6-143">**Для классической учетной записи запуска от имени Azure:**</span><span class="sxs-lookup"><span data-stu-id="9edd6-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="9edd6-144">Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureClassicRunAsCertificate* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="9edd6-145">Hello активов сертификат содержит закрытый ключ сертификата hello используемый сертификат управления hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="9edd6-146">Создает ресурс подключения автоматизации с именем *AzureClassicRunAsConnection* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="9edd6-147">ресурс-контейнер подключений Hello содержит имя подписки hello, идентификатор подписки и имя актива сертификатов.</span><span class="sxs-lookup"><span data-stu-id="9edd6-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="9edd6-148">Войдите в систему toohello портал Azure с учетную запись, которая является членом роли администраторов подписки hello и соадминистратором подписки hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="9edd6-149">В колонке учетной записи автоматизации hello, выберите **учетные записи запуска от** в разделе "hello" **параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="9edd6-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="9edd6-150">В зависимости от того, какую учетную запись необходимо создать, выберите **Учетная запись запуска от имени Azure** или **Классическая учетная запись запуска от имени Azure**.</span><span class="sxs-lookup"><span data-stu-id="9edd6-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="9edd6-151">После выбора либо hello **добавьте запуска от имени Azure** или **добавьте Azure классические учетная запись запуска от** колонке отображается и просмотрев hello Общие сведения, нажмите кнопку **создать** tooproceed с Создание учетной записи запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="9edd6-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="9edd6-152">Пока Azure создает hello запуска от имени учетной записи, можно отслеживать ход выполнения hello в **уведомления** из hello меню и заголовок отобразится создается учетная запись hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="9edd6-153">Этот процесс может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9edd6-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="9edd6-154">Создание учетной записи запуска от имени с использованием скрипта PowerShell</span><span class="sxs-lookup"><span data-stu-id="9edd6-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="9edd6-155">Этот сценарий PowerShell поддерживает hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="9edd6-156">создание учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="9edd6-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="9edd6-157">создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="9edd6-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="9edd6-158">создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата;</span><span class="sxs-lookup"><span data-stu-id="9edd6-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="9edd6-159">Создайте учетную запись запуска от имени и классический учетной записи запуска с помощью самозаверяющего сертификата в облако Azure для государственных hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="9edd6-160">В зависимости от hello параметров настройки при выборе hello скрипт создает hello следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="9edd6-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="9edd6-161">**Для учетной записи запуска от имени:**</span><span class="sxs-lookup"><span data-stu-id="9edd6-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="9edd6-162">Создает Azure AD приложения toobe экспортируются вместе с любой hello самозаверяющий или enterprise открытый ключ сертификата, создает основной учетной записи службы для приложения hello в Azure AD и назначает hello роль участника для учетной записи hello в существующую подписка.</span><span class="sxs-lookup"><span data-stu-id="9edd6-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="9edd6-163">Можно изменить этот параметр tooOwner или любая другая роль.</span><span class="sxs-lookup"><span data-stu-id="9edd6-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="9edd6-164">Дополнительные сведения см. в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="9edd6-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="9edd6-165">Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureRunAsCertificate* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="9edd6-166">Hello активов сертификат содержит закрытый ключ сертификата hello, используемого приложением hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9edd6-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="9edd6-167">Создает ресурс подключения автоматизации с именем *AzureRunAsConnection* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="9edd6-168">ресурс-контейнер подключений Hello содержит идентификатор приложения hello, идентификатора клиента, идентификатор подписки и отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="9edd6-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="9edd6-169">**Для классической учетной записи запуска от имени Azure:**</span><span class="sxs-lookup"><span data-stu-id="9edd6-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="9edd6-170">Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureClassicRunAsCertificate* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="9edd6-171">Hello активов сертификат содержит закрытый ключ сертификата hello используемый сертификат управления hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="9edd6-172">Создает ресурс подключения автоматизации с именем *AzureClassicRunAsConnection* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="9edd6-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="9edd6-173">ресурс-контейнер подключений Hello содержит имя подписки hello, идентификатор подписки и имя актива сертификатов.</span><span class="sxs-lookup"><span data-stu-id="9edd6-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="9edd6-174">При выборе любой из параметров для создания классических запуска от имени учетной записи, после выполнения сценария hello передачи hello открытый сертификат управления (CER-файл с расширением) toohello хранения для подписки hello этой учетной записи автоматизации hello был создан в.</span><span class="sxs-lookup"><span data-stu-id="9edd6-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="9edd6-175">Сохраните следующий сценарий на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-175">Save hello following script on your computer.</span></span> <span data-ttu-id="9edd6-176">В этом примере, сохраните его с именем файла hello *New RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="9edd6-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
        Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                       [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
            -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
            -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
            Sleep -s 10
            New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
            $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
            $Retries++;
        }
            return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
           $CertificateName = $AutomationAccountName+$CertifcateAssetName
           $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
           $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
           $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
           CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                     "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload hello .cer format of #CERT#"

              if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
              $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
              $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
              $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
              $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
              $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
              $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
              $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
              $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
              CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="9edd6-177">На компьютере, запустите **Windows PowerShell** из hello **запустить** экрана с повышенными правами пользователя.</span><span class="sxs-lookup"><span data-stu-id="9edd6-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="9edd6-178">Из hello повышенными оболочка командной строки, toohello откройте папку, содержащую hello скрипт, созданный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="9edd6-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="9edd6-179">Выполните сценарий hello, используя значения параметров hello hello конфигурации, требуемую.</span><span class="sxs-lookup"><span data-stu-id="9edd6-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="9edd6-180">**Создание учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="9edd6-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="9edd6-181">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="9edd6-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="9edd6-182">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата**</span><span class="sxs-lookup"><span data-stu-id="9edd6-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="9edd6-183">**Создание учетной записи запуска от имени и классический учетной записи запуска с помощью самозаверяющего сертификата в облако Azure для государственных hello**</span><span class="sxs-lookup"><span data-stu-id="9edd6-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="9edd6-184">После выполнения сценария hello, появится запрос tooauthenticate с Azure.</span><span class="sxs-lookup"><span data-stu-id="9edd6-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="9edd6-185">Войдите с учетной записью, которая является членом роли администраторов подписки hello и соадминистратором подписки hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="9edd6-186">После успешного выполнения сценария hello Обратите внимание hello следующее:</span><span class="sxs-lookup"><span data-stu-id="9edd6-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="9edd6-187">При создании классического учетной записи запуска с общей самозаверяющего сертификата (CER-файл), hello скрипт создает и сохраняет его toohello в папке временных файлов на компьютере в пользовательском профиле hello *%USERPROFILE%\AppData\Local\Temp*, мы использовали сеанс PowerShell tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="9edd6-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="9edd6-188">Если вы создали классическую учетную запись запуска от имени с использованием открытого корпоративного сертификата (CER-файл), используйте этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="9edd6-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="9edd6-189">Следуйте инструкциям hello [передачи toohello сертификата API управления классический портал Azure](../azure-api-management-certs.md)и последующей проверки hello конфигурации учетных данных с ресурсами классическое развертывание с помощью hello [пример кода tooauthenticate с Azure классические ресурсы развертывания](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="9edd6-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="9edd6-190">Если вы уже сделали *не* создания классических учетной записи запуска, проверки подлинности в ресурсах диспетчера ресурсов и проверка конфигурации hello учетных данных с помощью hello [пример кода для проверки подлинности с помощью службы управления ресурсы](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="9edd6-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9edd6-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9edd6-191">Next steps</span></span>
* <span data-ttu-id="9edd6-192">Дополнительные сведения о субъектах ссылаться слишком[участника-службы и объекты приложений](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="9edd6-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="9edd6-193">Дополнительные сведения о сертификатах и служб Azure см. в разделе слишком[Общие сведения о сертификатах для облачных служб Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="9edd6-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
