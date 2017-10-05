---
title: "Создание учетной записи запуска от имени службы автоматизации Azure | Документация Майкрософт"
description: "В этой статье объясняется, как обновлять учетную запись службы автоматизации и создавать учетные записи запуска от имени с помощью PowerShell или портала."
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
ms.openlocfilehash: eaf6eb49bbfe4572827fcc101d1f552b48ab91e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="a24aa-103">Обновление проверки подлинности учетных записей службы автоматизации с использованием учетных записей запуска от имени</span><span class="sxs-lookup"><span data-stu-id="a24aa-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="a24aa-104">Существующую учетную запись службы автоматизации можно обновлять с помощью портала или PowerShell в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="a24aa-104">You can update your existing Automation account from the portal or use PowerShell if:</span></span>

* <span data-ttu-id="a24aa-105">Вы создали учетную запись службы автоматизации, но не создали учетную запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="a24aa-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="a24aa-106">У вас уже есть учетная запись службы автоматизации для управления ресурсами Resource Manager, и вы хотите обновить ее, чтобы включить учетную запись запуска от имени в процедуру проверки подлинности модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="a24aa-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="a24aa-107">У вас есть учетная запись службы автоматизации для управления классическими ресурсами, и вы хотите обновить ее, чтобы использовать классическую учетную запись запуска от имени, а не создавать учетную запись и переносить в нее модули runbook и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a24aa-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="a24aa-108">Вы хотите создать учетную запись запуска от имени и классическую учетную запись запуска от имени, используя сертификат, выданный центром сертификации предприятия.</span><span class="sxs-lookup"><span data-stu-id="a24aa-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a24aa-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a24aa-109">Prerequisites</span></span>

* <span data-ttu-id="a24aa-110">Этот скрипт можно выполнять только в ОС Windows 10 и Windows Server 2016 с модулями Azure Resource Manager 3.0.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a24aa-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="a24aa-111">Более ранние версии Windows не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a24aa-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="a24aa-112">Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a24aa-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="a24aa-113">Сведения о выпуске PowerShell 1.0 см. в статье [Приступая к работе с командлетами Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a24aa-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="a24aa-114">Учетная запись службы автоматизации, указанная как значение для параметров *-AutomationAccountName* и *-ApplicationDisplayName* в приведенных ниже сценариях PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a24aa-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="a24aa-115">Чтобы получить значения для параметров *SubscriptionID*, *ResourceGroup* и *AutomationAccountName*, которые являются обязательными для скрипта, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a24aa-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span></span>

1. <span data-ttu-id="a24aa-116">На портале Azure выберите свою учетную запись службы автоматизации в колонке **Учетная запись службы автоматизации** и выберите **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="a24aa-117">В колонке **Все параметры** в разделе **Параметры учетной записи** выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="a24aa-118">Обратите внимание на значения в колонке **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-118">Note the values on the **Properties** blade.</span></span><br><br> <span data-ttu-id="a24aa-119">![Колонка "Свойства" учетной записи службы автоматизации](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="a24aa-119">![The Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-to-update-your-automation-account"></a><span data-ttu-id="a24aa-120">Необходимые разрешения для обновления учетной записи службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="a24aa-120">Required permissions to update your Automation account</span></span>
<span data-ttu-id="a24aa-121">Чтобы обновить учетную запись службы автоматизации, вам потребуются следующие привилегии и разрешения, необходимые для работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="a24aa-121">To update an Automation account, you must have the following specific privileges and permissions required to complete this topic.</span></span>   
 
* <span data-ttu-id="a24aa-122">Необходимо добавить учетную запись AD к роли с разрешениями, аналогичными роли участника для ресурсов Microsoft.Automation, как описано в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="a24aa-122">Your AD user account needs to be added to a role with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="a24aa-123">Пользователи без прав администратора в клиенте Azure AD могут [регистрировать приложения AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions), если для параметра регистрации установлено значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the App registrations setting is set to **Yes**.</span></span>  <span data-ttu-id="a24aa-124">Если для этого параметра задано значение **Нет**, пользователю потребуются права глобального администратора в Azure AD, чтобы выполнить это действие.</span><span class="sxs-lookup"><span data-stu-id="a24aa-124">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="a24aa-125">Если пользователь, которому назначают роль глобального администратора или соадминистратора подписки, не является участником экземпляра подписки Active Directory, он будет добавлен в Active Directory в качестве гостя.</span><span class="sxs-lookup"><span data-stu-id="a24aa-125">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span></span> <span data-ttu-id="a24aa-126">В этом случае отобразится соответствующее предупреждение "У вас нет разрешений на создание…"</span><span class="sxs-lookup"><span data-stu-id="a24aa-126">In this situation, you receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="a24aa-127">в колонке **Добавление учетной записи службы автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-127">warning on the **Add Automation Account** blade.</span></span> <span data-ttu-id="a24aa-128">Пользователей, которым назначена роль соадминистратора или глобального администратора, можно удалить из экземпляра подписки Active Directory, а затем повторно добавить, чтобы предоставить им права полного доступа к Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a24aa-128">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="a24aa-129">Чтобы проверить это, на портале Azure в области **Azure Active Directory** выберите **Пользователи и группы** и **Все пользователи**. Выбрав нужного пользователя, щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-129">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span></span> <span data-ttu-id="a24aa-130">Значение атрибута **Тип пользователя** в профиле пользователя не должно соответствовать значению **Гость**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-130">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-the-portal"></a><span data-ttu-id="a24aa-131">Создание учетной записи запуска от имени на портале</span><span class="sxs-lookup"><span data-stu-id="a24aa-131">Create Run As account from the portal</span></span>
<span data-ttu-id="a24aa-132">В этом разделе указаны действия, с помощью которых на портале Azure можно обновить учетную запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="a24aa-132">In this section, perform the following steps to update your Azure Automation account from  the Azure portal.</span></span>  <span data-ttu-id="a24aa-133">Учетная запись запуска от имени и классическая учетная запись запуска от имени создаются отдельно. Если управлять ресурсами на классическом портале Azure не требуется, можно просто создать учетную запись запуска от имени Azure.</span><span class="sxs-lookup"><span data-stu-id="a24aa-133">You create the Run As and Classic Run As accounts individually, and if you don't need to manage resources in the classic Azure portal, you can just create the Azure Run As account.</span></span>  

<span data-ttu-id="a24aa-134">В результате этого процесса создаются следующие элементы учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-134">The process creates the following items in your Automation account.</span></span>

<span data-ttu-id="a24aa-135">**Для учетной записи запуска от имени:**</span><span class="sxs-lookup"><span data-stu-id="a24aa-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="a24aa-136">Создается приложение Azure AD с самозаверяющим сертификатом, учетная запись субъекта-службы для этого приложения в Azure AD, а также назначается роль участника для учетной записи в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="a24aa-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="a24aa-137">Вместо этой роли можно использовать роль владельца или любую другую роль.</span><span class="sxs-lookup"><span data-stu-id="a24aa-137">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="a24aa-138">Дополнительные сведения см. в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a24aa-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="a24aa-139">Ресурс сертификатов службы автоматизации с именем *AzureRunAsCertificate* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="a24aa-140">Этот ресурс содержит закрытый ключ сертификата, используемый в приложении Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a24aa-140">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="a24aa-141">Ресурс подключений службы автоматизации с именем *AzureRunAsConnection* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-141">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="a24aa-142">Этот ресурс содержит идентификаторы приложения, клиента и подписки, а также отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="a24aa-142">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="a24aa-143">**Для классической учетной записи запуска от имени Azure:**</span><span class="sxs-lookup"><span data-stu-id="a24aa-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="a24aa-144">Ресурс сертификатов службы автоматизации с именем *AzureClassicRunAsCertificate* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="a24aa-145">Этот ресурс содержит закрытый ключ сертификата, используемый в сертификате управления.</span><span class="sxs-lookup"><span data-stu-id="a24aa-145">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="a24aa-146">Ресурс подключений службы автоматизации с именем *AzureClassicRunAsConnection* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="a24aa-147">Этот ресурс содержит имя подписки, идентификатор подписки и имя ресурса сертификатов.</span><span class="sxs-lookup"><span data-stu-id="a24aa-147">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="a24aa-148">Войдите на портал Azure с помощью учетной записи, которая является участником роли "Администраторы подписки" и соадминистратором подписки.</span><span class="sxs-lookup"><span data-stu-id="a24aa-148">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span></span>
2. <span data-ttu-id="a24aa-149">В разделе **Параметры учетной записи** колонки учетной записи службы автоматизации выберите **Учетные записи запуска от имени**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-149">From the Automation account blade, select **Run As Accounts** under the section **Account Settings**.</span></span>  
3. <span data-ttu-id="a24aa-150">В зависимости от того, какую учетную запись необходимо создать, выберите **Учетная запись запуска от имени Azure** или **Классическая учетная запись запуска от имени Azure**.</span><span class="sxs-lookup"><span data-stu-id="a24aa-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="a24aa-151">После выбора отобразится колонка **Добавить учетную запись запуска от имени Azure** или **Добавить классическую учетную запись запуска от имени Azure**. Просмотрев общие сведения, нажмите кнопку **Создать**, чтобы продолжить создание учетной записи запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="a24aa-151">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span></span>  
4. <span data-ttu-id="a24aa-152">Пока Azure создает учетную запись запуска от имени, можно отслеживать ход выполнения в меню раздела **Уведомления**, где на баннере отображается уведомление о создании учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a24aa-152">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu and a banner is displayed stating the account is being created.</span></span>  <span data-ttu-id="a24aa-153">Процесс создания может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a24aa-153">This process can take a few minutes to complete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="a24aa-154">Создание учетной записи запуска от имени с использованием скрипта PowerShell</span><span class="sxs-lookup"><span data-stu-id="a24aa-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="a24aa-155">Этот сценарий PowerShell включает в себя поддержку следующих конфигураций:</span><span class="sxs-lookup"><span data-stu-id="a24aa-155">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="a24aa-156">создание учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="a24aa-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="a24aa-157">создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="a24aa-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="a24aa-158">создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата;</span><span class="sxs-lookup"><span data-stu-id="a24aa-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="a24aa-159">создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата в облаке Azure для государственных организаций.</span><span class="sxs-lookup"><span data-stu-id="a24aa-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="a24aa-160">В зависимости от выбранного варианта конфигурации сценарий создает приведенные ниже элементы.</span><span class="sxs-lookup"><span data-stu-id="a24aa-160">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="a24aa-161">**Для учетной записи запуска от имени:**</span><span class="sxs-lookup"><span data-stu-id="a24aa-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="a24aa-162">Приложение Azure AD, используемое для экспорта самозаверяющего сертификата или открытого ключа корпоративного сертификата, и учетную запись субъекта-службы для этого приложения в Azure AD, а также назначает роль участника в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="a24aa-162">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="a24aa-163">Вместо этой роли можно использовать роль владельца или любую другую роль.</span><span class="sxs-lookup"><span data-stu-id="a24aa-163">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="a24aa-164">Дополнительные сведения см. в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a24aa-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="a24aa-165">Ресурс сертификатов службы автоматизации с именем *AzureRunAsCertificate* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="a24aa-166">Этот ресурс содержит закрытый ключ сертификата, используемый в приложении Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a24aa-166">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="a24aa-167">Ресурс подключений службы автоматизации с именем *AzureRunAsConnection* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-167">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="a24aa-168">Этот ресурс содержит идентификаторы приложения, клиента и подписки, а также отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="a24aa-168">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="a24aa-169">**Для классической учетной записи запуска от имени Azure:**</span><span class="sxs-lookup"><span data-stu-id="a24aa-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="a24aa-170">Ресурс сертификатов службы автоматизации с именем *AzureClassicRunAsCertificate* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="a24aa-171">Этот ресурс содержит закрытый ключ сертификата, используемый в сертификате управления.</span><span class="sxs-lookup"><span data-stu-id="a24aa-171">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="a24aa-172">Ресурс подключений службы автоматизации с именем *AzureClassicRunAsConnection* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="a24aa-173">Этот ресурс содержит имя подписки, идентификатор подписки и имя ресурса сертификатов.</span><span class="sxs-lookup"><span data-stu-id="a24aa-173">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="a24aa-174">Если вы выбрали создание классической учетной записи запуска от имени, после выполнения сценария отправьте открытый сертификат (файл в формате CER) в хранилище управления подписки, в которой создана учетная запись службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-174">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="a24aa-175">Сохраните приведенный ниже сценарий на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a24aa-175">Save the following script on your computer.</span></span> <span data-ttu-id="a24aa-176">В этом примере используйте имя файла *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="a24aa-176">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
            Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                     "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="a24aa-177">На компьютере запустите с повышенными правами **Windows PowerShell** с **начального** экрана.</span><span class="sxs-lookup"><span data-stu-id="a24aa-177">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="a24aa-178">Из оболочки командной строки с повышенными привилегиями перейдите в папку, которая содержит сценарий, созданный на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="a24aa-178">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="a24aa-179">Выполните этот сценарий, установив значения параметров в зависимости от требуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a24aa-179">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="a24aa-180">**Создание учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="a24aa-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="a24aa-181">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="a24aa-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="a24aa-182">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата**</span><span class="sxs-lookup"><span data-stu-id="a24aa-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="a24aa-183">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата в облаке Azure для государственных организаций**</span><span class="sxs-lookup"><span data-stu-id="a24aa-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="a24aa-184">После выполнения сценария появится запрос на проверку подлинности в Azure.</span><span class="sxs-lookup"><span data-stu-id="a24aa-184">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="a24aa-185">Войдите в систему, используя учетную запись, которая является участником роли "Администраторы подписки" и соадминистратором подписки.</span><span class="sxs-lookup"><span data-stu-id="a24aa-185">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="a24aa-186">После выполнения сценария обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="a24aa-186">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="a24aa-187">Если вы создали классическую учетную запись запуска от имени с использованием самозаверяющего открытого сертификата (CER-файл), сценарий создает ее и сохраняет в папке временных файлов на компьютере в профиле пользователя, который выполнял сеанс PowerShell: *%Профиль_пользователя%\AppData\Local\Temp*.</span><span class="sxs-lookup"><span data-stu-id="a24aa-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="a24aa-188">Если вы создали классическую учетную запись запуска от имени с использованием открытого корпоративного сертификата (CER-файл), используйте этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="a24aa-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="a24aa-189">Следуя инструкциям, [отправьте сертификат управления API на классический портал Azure](../azure-api-management-certs.md), а затем используйте [пример кода для проверки подлинности](automation-verify-runas-authentication.md#classic-run-as-authentication), чтобы проверить конфигурацию учетных данных с помощью классических ресурсов развертывания Azure.</span><span class="sxs-lookup"><span data-stu-id="a24aa-189">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="a24aa-190">Если вы *не* создали классическую учетную запись запуска от имени, выполните проверку подлинности с помощью ресурсов Resource Manager и проверьте конфигурацию учетных данных, используя [этот пример кода](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="a24aa-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a24aa-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a24aa-191">Next steps</span></span>
* <span data-ttu-id="a24aa-192">Дополнительные сведения о субъектах-службах см. в статье [Объекты приложения и субъекта-службы в Azure Active Directory](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a24aa-192">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="a24aa-193">Дополнительные сведения о сертификатах и службах Azure см. в статье [Общие сведения о сертификатах для облачных служб Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a24aa-193">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>