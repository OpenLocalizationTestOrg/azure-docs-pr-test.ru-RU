---
title: "Учетная запись службы автоматизации Azure aaaManage | Документы Microsoft"
description: "В этой статье описывается, как toomanage hello конфигурации учетной записи автоматизации, такие как обновление сертификата, удаления и неправильной настройки."
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
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="a6d9c-103">Управление учетной записью службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="a6d9c-103">Manage Azure Automation account</span></span>
<span data-ttu-id="a6d9c-104">В некоторый момент до истечения срока действия учетной записи автоматизации, потребуется сертификат toorenew hello.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="a6d9c-105">Если вы считаете, что был скомпрометирован, hello учетная запись запуска от имени, можно удалить и создать его повторно.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="a6d9c-106">В этом разделе рассматриваются как tooperform этих операций.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="a6d9c-107">Обновление самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="a6d9c-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="a6d9c-108">Hello самозаверяющий сертификат, созданный для hello учетная запись запуска от имени истекает один год после даты создания hello.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="a6d9c-109">Его можно обновить в любое время до истечения его срока действия.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="a6d9c-110">При обновлении, hello текущего действительного сертификата — зависимых tooensure, что все модули Runbook, помещаются в очередь до или активно работает и что аутентификации hello учетная запись запуска от имени, не подвергаются отрицательно.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="a6d9c-111">Hello сертификат остается действительным до истечения срока ее.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="a6d9c-112">Если вы настроили ваш автоматизации Запуск от имени учетной записи toouse сертификат, выданный центром сертификации предприятия и использовать этот параметр, hello корпоративный сертификат будет заменен самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="a6d9c-113">toorenew hello сертификатов, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a6d9c-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="a6d9c-114">Откройте в hello портал Azure, учетная запись автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="a6d9c-115">На hello **учетной записи автоматизации** колонки в hello **свойства учетной записи** панели в разделе **параметры учетной записи**выберите **учетные записи запуска от**.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Область свойств учетной записи службы автоматизации](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="a6d9c-117">На hello **учетные записи запуска от** свойства колонке выберите либо hello Запуск от имени учетной записи или hello классический запуска от имени, требуется сертификат toorenew hello.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="a6d9c-118">На hello **свойства** колонке hello выбранную учетную запись, нажмите кнопку **продления сертификата**.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Обновление сертификата для учетной записи запуска от имени](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="a6d9c-120">При продлении сертификата hello, отслеживания хода hello под **уведомления** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="a6d9c-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="a6d9c-121">Удаление учетной записи запуска от имени или классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="a6d9c-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="a6d9c-122">В этом разделе описываются как toodelete и повторного создания учетной записи запуска от имени или классический Запуск от имени.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="a6d9c-123">После выполнения этого действия сохраняется hello учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="a6d9c-124">После удаления учетной записи запуска от имени или классический запуска от имени, повторно создать его hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="a6d9c-125">Откройте в hello портал Azure, учетная запись автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="a6d9c-126">На hello **учетной записи автоматизации** колонке hello учетной записи «свойства» выберите **учетные записи запуска от**.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="a6d9c-127">На hello **учетные записи запуска от** колонку свойств, выберите либо hello Запуск от имени учетной записи или классический запуска от имени учетной записи, которые должны toodelete.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="a6d9c-128">Затем на hello **свойства** колонке hello выбранную учетную запись, нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Удаление учетной записи запуска от имени](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="a6d9c-130">Во время удаления учетной записи hello, отслеживания хода hello под **уведомления** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="a6d9c-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="a6d9c-131">После удаления учетной записи hello, его можно повторно создать на hello **учетные записи запуска от** колонку свойств, выбрав hello создать параметр **Azure учетная запись запуска от имени**.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Повторно создать hello автоматизации Запуск от имени учетной записи](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="a6d9c-133">Неправильные настройки</span><span class="sxs-lookup"><span data-stu-id="a6d9c-133">Misconfiguration</span></span>
<span data-ttu-id="a6d9c-134">Некоторые элементы конфигурации, необходимые для hello toofunction учетная запись запуска от имени или классический Запуск от имени правильно может была удалена или создана неправильно во время начальной настройки.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="a6d9c-135">Hello элементы включают:</span><span class="sxs-lookup"><span data-stu-id="a6d9c-135">hello items include:</span></span>

* <span data-ttu-id="a6d9c-136">ресурс сертификата,</span><span class="sxs-lookup"><span data-stu-id="a6d9c-136">Certificate asset</span></span>
* <span data-ttu-id="a6d9c-137">ресурс подключения,</span><span class="sxs-lookup"><span data-stu-id="a6d9c-137">Connection asset</span></span>
* <span data-ttu-id="a6d9c-138">Учетная запись запуска от имени был удален из роли участника hello</span><span class="sxs-lookup"><span data-stu-id="a6d9c-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="a6d9c-139">субъект-служба или приложение-служба в Azure AD,</span><span class="sxs-lookup"><span data-stu-id="a6d9c-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="a6d9c-140">В предыдущем hello и другие экземпляры неправильной настройки, приветствия учетной записи автоматизации обнаруживает hello изменяет и отображает состояние *неполный* на hello **учетные записи запуска от** колонку свойств для hello Учетная запись.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Сообщение о том, что настройка учетной записи запуска от имени не завершена](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="a6d9c-142">При выборе hello запись запуска от имени учетной записи Здравствуйте, **свойства** отображаются hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="a6d9c-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Предупреждение о том, что настройка учетной записи запуска от имени не завершена](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="a6d9c-144">.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-144">.</span></span>

<span data-ttu-id="a6d9c-145">Позволяет быстро устранить эти проблемы учетная запись запуска от имени, удаления и повторного создания учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="a6d9c-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6d9c-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6d9c-146">Next steps</span></span>
* <span data-ttu-id="a6d9c-147">Дополнительные сведения о субъектах ссылаться слишком[участника-службы и объекты приложений](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a6d9c-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="a6d9c-148">Дополнительные сведения об элементе управления доступом на основе ролей в службе автоматизации Azure дополнительную информацию слишком[управления доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a6d9c-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="a6d9c-149">Дополнительные сведения о сертификатах и служб Azure см. в разделе слишком[Общие сведения о сертификатах для облачных служб Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a6d9c-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
