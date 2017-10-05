---
title: "Управление учетной записью службы автоматизации Azure | Документация Майкрософт"
description: "В этой статье описывается управление конфигурацией учетной записи службы автоматизации, например обновление, удаление и неправильные настройки сертификатов."
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
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 41efdbcacede74bac038342688362ff480cadc7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="f4fc4-103">Управление учетной записью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="f4fc4-103">Manage Azure Automation account</span></span>
<span data-ttu-id="f4fc4-104">В определенный момент перед истечением срока действия учетной записи службы автоматизации вам потребуется обновить сертификат.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-104">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="f4fc4-105">Если вы считаете, что учетная запись запуска от имени была скомпрометирована, ее можно удалить и создать заново.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-105">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="f4fc4-106">В этом разделе описано, как выполнить эти операции.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-106">This section discusses how to perform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="f4fc4-107">Обновление самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="f4fc4-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="f4fc4-108">Срок действия самозаверяющего сертификата, созданного для учетной записи запуска от имени, составляет один год с момента создания.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-108">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="f4fc4-109">Его можно обновить в любое время до истечения его срока действия.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="f4fc4-110">При обновлении текущее значение сертификата сохраняется, чтобы гарантировать, что все модули runbook, которые поставлены в очередь или активно выполняются и для проверки подлинности которых используется учетная запись запуска от имени, не будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-110">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="f4fc4-111">Сертификат будет существовать до окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-111">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="f4fc4-112">Если вы настроили учетную запись запуска от имени службы автоматизации так, чтобы использовать сертификат, выданный центром сертификации предприятия, и используете этот параметр, то этот сертификат предприятия будет заменен самозаверяющим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-112">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="f4fc4-113">Чтобы обновить сертификат, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f4fc4-113">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="f4fc4-114">На портале Azure откройте учетную запись службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-114">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="f4fc4-115">В колонке **Учетная запись службы автоматизации** в области **свойств учетной записи** выберите **Учетные записи запуска от имени** в разделе **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-115">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Область свойств учетной записи службы автоматизации](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="f4fc4-117">В колонке свойств **Учетные записи запуска от имени** выберите учетную запись запуска от имени или классическую учетную запись запуска от имени, для которой нужно обновить сертификат.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-117">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="f4fc4-118">В колонке **Свойства** выбранной учетной записи щелкните **Обновление сертификата**.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-118">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Обновление сертификата для учетной записи запуска от имени](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="f4fc4-120">Ход обновления сертификата можно отслеживать в разделе **Уведомления** в меню.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-120">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="f4fc4-121">Удаление учетной записи запуска от имени или классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="f4fc4-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="f4fc4-122">В этом разделе описано, как удалить и повторно создать учетную запись запуска от имени или классическую учетную запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-122">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="f4fc4-123">При выполнении этого действия учетная запись службы автоматизации сохраняется.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-123">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="f4fc4-124">После удаления учетной записи запуска от имени или классической учетной записи запуска от имени ее можно создать заново на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-124">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="f4fc4-125">На портале Azure откройте учетную запись службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-125">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="f4fc4-126">В колонке **Учетная запись службы автоматизации** в области свойств учетной записи выберите **Учетные записи запуска от имени**.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-126">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="f4fc4-127">В колонке свойств **Учетные записи запуска от имени** выберите учетную запись запуска от имени или классическую учетную запись запуска от имени, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-127">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="f4fc4-128">Затем в колонке **Свойства** выбранной учетной записи щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-128">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Удаление учетной записи запуска от имени](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="f4fc4-130">Ход удаления учетной записи можно отслеживать в разделе **Уведомления** в меню.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-130">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="f4fc4-131">После удаления учетной записи ее можно повторно создать в колонке свойств **Учетные записи запуска от имени**, выбрав параметр создания **Учетная запись запуска от имени Azure**.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-131">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Повторное создание учетной записи запуска от имени службы автоматизации](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="f4fc4-133">Неправильные настройки</span><span class="sxs-lookup"><span data-stu-id="f4fc4-133">Misconfiguration</span></span>
<span data-ttu-id="f4fc4-134">Во время начальной настройки некоторые из элементов конфигурации, необходимых для правильной работы учетной записи запуска от имени или классической учетной записи запуска от имени, могут быть удалены или неправильно созданы.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-134">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="f4fc4-135">К этим элементам относятся:</span><span class="sxs-lookup"><span data-stu-id="f4fc4-135">The items include:</span></span>

* <span data-ttu-id="f4fc4-136">ресурс сертификата,</span><span class="sxs-lookup"><span data-stu-id="f4fc4-136">Certificate asset</span></span>
* <span data-ttu-id="f4fc4-137">ресурс подключения,</span><span class="sxs-lookup"><span data-stu-id="f4fc4-137">Connection asset</span></span>
* <span data-ttu-id="f4fc4-138">учетная запись запуска от имени (удалена из роли участника),</span><span class="sxs-lookup"><span data-stu-id="f4fc4-138">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="f4fc4-139">субъект-служба или приложение-служба в Azure AD,</span><span class="sxs-lookup"><span data-stu-id="f4fc4-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="f4fc4-140">В случае такой неправильной настройки (или в других примерах) учетная запись службы автоматизации обнаружит эти изменения и отобразит в колонке свойств **Учетные записи запуска от имени** состояние *Не завершено*.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-140">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Сообщение о том, что настройка учетной записи запуска от имени не завершена](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="f4fc4-142">При выборе учетной записи запуска от имени в области **Свойства** учетной записи отобразится следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="f4fc4-142">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Предупреждение о том, что настройка учетной записи запуска от имени не завершена](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="f4fc4-144">.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-144">.</span></span>

<span data-ttu-id="f4fc4-145">Эти проблемы с учетной записью запуска от имени можно быстро устранить, удалив и повторно создав ее.</span><span class="sxs-lookup"><span data-stu-id="f4fc4-145">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4fc4-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4fc4-146">Next steps</span></span>
* <span data-ttu-id="f4fc4-147">Дополнительные сведения о субъектах-службах см. в статье [Объекты приложения и субъекта-службы в Azure Active Directory](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="f4fc4-147">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="f4fc4-148">Дополнительные сведения об управлении доступом на основе ролей в службе автоматизации Azure см. в [этой статье](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="f4fc4-148">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="f4fc4-149">Дополнительные сведения о сертификатах и службах Azure см. в статье [Общие сведения о сертификатах для облачных служб Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="f4fc4-149">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>