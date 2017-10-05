---
title: "Настройка учетной записи запуска от имени | Документация Майкрософт"
description: "В этом руководстве приводятся пошаговые инструкции по созданию и тестированию, а также пример проверки подлинности с помощью субъекта безопасности в службе автоматизации Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "имя субъекта-службы, SetSPN, проверка подлинности Azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: TRUE
ms.openlocfilehash: f88c775eba19bb227d0e206d6420c08b57305b92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="ef76e-104">Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="ef76e-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="ef76e-105">В этой статье объясняется, как настроить учетную запись службы автоматизации на портале Azure</span><span class="sxs-lookup"><span data-stu-id="ef76e-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="ef76e-106">с использованием учетной записи запуска от имени, чтобы проверять подлинность ресурсов управления модулями runbook в Azure Resource Manager или в службе управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="ef76e-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="ef76e-107">При создании учетной записи службы автоматизации на портале Azure автоматически создаются две приведенные ниже учетные записи.</span><span class="sxs-lookup"><span data-stu-id="ef76e-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="ef76e-108">Учетная запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="ef76e-108">A Run As account.</span></span> <span data-ttu-id="ef76e-109">Эта учетная запись создает субъект-службу в Azure Active Directory (Azure AD) и сертификат,</span><span class="sxs-lookup"><span data-stu-id="ef76e-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="ef76e-110">а также назначает управление доступом на основе ролей участника, используемое для управления ресурсами Resource Manager с помощью модулей runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="ef76e-111">Классическая учетная запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="ef76e-111">A Classic Run As account.</span></span> <span data-ttu-id="ef76e-112">Эта учетная запись отправляет сертификат управления, используемый для администрирования службы управления службами или классических ресурсов с помощью модулей runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="ef76e-113">Создание учетной записи службы автоматизации упрощает процесс и помогает быстро приступить к созданию и развертыванию модулей runbook для решения конкретных задач автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span></span>

<span data-ttu-id="ef76e-114">Используя учетную запись запуска от имени и классическую учетную запись, вы можете:</span><span class="sxs-lookup"><span data-stu-id="ef76e-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="ef76e-115">внедрить стандартную процедуру проверки подлинности в Azure при администрировании ресурсов Resource Manager и ресурсов службы управления службами с помощью модулей runbook на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="ef76e-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span></span>
* <span data-ttu-id="ef76e-116">автоматизировать использование глобальных модулей runbook, которые можно настроить в службе оповещений Azure.</span><span class="sxs-lookup"><span data-stu-id="ef76e-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="ef76e-117">Для работы [функции интеграции оповещений](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) Azure с глобальными модулями runbook службы автоматизации требуется учетная запись службы автоматизации, в которой настроены учетная запись запуска от имени и классическая учетная запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="ef76e-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="ef76e-118">Вы можете выбрать имеющуюся учетную запись службы автоматизации, в которой уже определены учетная запись запуска от имени и классическая учетная запись запуска от имени, или создать новую.</span><span class="sxs-lookup"><span data-stu-id="ef76e-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span></span>
>  

<span data-ttu-id="ef76e-119">В этой статье описано, как создать учетную запись службы автоматизации на портале Azure, обновить ее с помощью Azure PowerShell, а также как управлять конфигурацией учетной записи и проходить проверку подлинности в модулях runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="ef76e-120">Прежде чем приступать к созданию учетной записи службы автоматизации, следует принять во внимание несколько моментов.</span><span class="sxs-lookup"><span data-stu-id="ef76e-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span></span>

* <span data-ttu-id="ef76e-121">Создание этой учетные записи не повлияет на имеющиеся учетные записи службы автоматизации, созданные в классической модели развертывания или в модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef76e-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="ef76e-122">Этот процесс работает только для учетных записей службы автоматизации, созданных на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ef76e-122">The process works only for Automation accounts that you create in the Azure portal.</span></span> <span data-ttu-id="ef76e-123">При попытке создать учетную запись на классическом портале Azure конфигурация учетной записи запуска от имени не будет реплицирована.</span><span class="sxs-lookup"><span data-stu-id="ef76e-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span></span>
* <span data-ttu-id="ef76e-124">Если вы уже создали модули runbook и ресурсы (например, расписания или переменные) для управления классическими ресурсами и хотите выполнять проверку подлинности в этих модулях runbook с помощью классической учетной записи запуска от имени, выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="ef76e-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span></span>

  * <span data-ttu-id="ef76e-125">Создайте классическую учетную запись запуска от имени, используя инструкции в разделе "Управление учетной записью запуска от имени".</span><span class="sxs-lookup"><span data-stu-id="ef76e-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="ef76e-126">Обновите имеющуюся учетную запись с помощью сценария PowerShell, приведенного в разделе "Обновление учетной записи службы автоматизации с помощью PowerShell".</span><span class="sxs-lookup"><span data-stu-id="ef76e-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="ef76e-127">Чтобы выполнять проверку подлинности с помощью новой учетной записи запуска от имени и классической учетной записи запуска от имени (учетная запись службы автоматизации), измените имеющиеся модули runbook с помощью примера кода, приведенного в разделе с [примерами кода для проверки подлинности](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="ef76e-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="ef76e-128">Учетная запись запуска от имени используется для проверки подлинности в ресурсах Resource Manager с помощью субъекта-службы на основе сертификата,</span><span class="sxs-lookup"><span data-stu-id="ef76e-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span></span> <span data-ttu-id="ef76e-129">а классическая учетная запись запуска от имени — в ресурсах управления службами с помощью сертификата управления.</span><span class="sxs-lookup"><span data-stu-id="ef76e-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-the-azure-portal"></a><span data-ttu-id="ef76e-130">Создание учетной записи службы автоматизации на портале Azure</span><span class="sxs-lookup"><span data-stu-id="ef76e-130">Create an Automation account from the Azure portal</span></span>
<span data-ttu-id="ef76e-131">В этом разделе описано, как создать учетную запись службы автоматизации Azure на портале Azure, в результате чего создаются учетная запись запуска от имени и классическая учетная запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="ef76e-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="ef76e-132">Чтобы создать учетную запись службы автоматизации, пользователь должен быть участником роли "Администраторы служб" или соадминистратором подписки, из которой предоставляется доступ к подписке.</span><span class="sxs-lookup"><span data-stu-id="ef76e-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span></span> <span data-ttu-id="ef76e-133">Кроме того, пользователь также должен быть добавлен в роль "Пользователь" в стандартных подписках Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef76e-133">You must also be added as a user to that subscription's default Active Directory instance.</span></span> <span data-ttu-id="ef76e-134">Учетной записи не нужно назначать привилегированную роль.</span><span class="sxs-lookup"><span data-stu-id="ef76e-134">The account does not need to be assigned a privileged role.</span></span>
>
><span data-ttu-id="ef76e-135">Если пользователь, которого добавляют к роли соадминистратора подписки, не является участником подписки Active Directory, он будет добавлен в Active Directory в качестве гостя.</span><span class="sxs-lookup"><span data-stu-id="ef76e-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span></span> <span data-ttu-id="ef76e-136">В этом случае отобразится соответствующее предупреждение "У вас нет разрешений на создание..."</span><span class="sxs-lookup"><span data-stu-id="ef76e-136">In this instance, you will receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="ef76e-137">в колонке **Добавление учетной записи службы автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-137">warning on the **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="ef76e-138">Пользователей, получивших роль соадминистратора, можно удалить из подписки Active Directory, а затем повторно добавить, чтобы предоставить им права полного доступа к Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef76e-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="ef76e-139">Чтобы проверить это, на портале Azure в области **Azure Active Directory** выберите **Пользователи и группы**, а затем — **Все пользователи**. Выбрав конкретного пользователя, щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span></span> <span data-ttu-id="ef76e-140">Значение атрибута **Тип пользователя** в профиле пользователя не должно соответствовать значению **Гость**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="ef76e-141">Войдите на портал Azure с помощью учетной записи, добавленной в качестве участника роли "Администраторы подписки" и соадминистратора подписки.</span><span class="sxs-lookup"><span data-stu-id="ef76e-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

2. <span data-ttu-id="ef76e-142">Выберите элемент **Учетные записи службы автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="ef76e-143">В колонке **Учетные записи службы автоматизации** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-143">On the **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="ef76e-144">После этого откроется колонка **Добавление учетной записи службы автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-144">The **Add Automation Account** blade opens.</span></span>

 ![Колонка "Добавление учетной записи службы автоматизации"](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="ef76e-146">Если учетная запись не является участником роли "Администраторы подписки" и соадминистратором подписки, в колонке **Добавление учетной записи службы автоматизации** отобразится следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="ef76e-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span></span>
   >
   >![Предупреждение в колонке "Добавление учетной записи службы автоматизации"](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="ef76e-148">В колонке **Добавление учетной записи службы автоматизации** в поле **Имя** введите имя новой учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="ef76e-149">Если у вас имеется несколько подписок, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="ef76e-149">If you have more than one subscription, do the following:</span></span>

    <span data-ttu-id="ef76e-150">А.</span><span class="sxs-lookup"><span data-stu-id="ef76e-150">a.</span></span> <span data-ttu-id="ef76e-151">В разделе **Подписка** укажите одну из них для новой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ef76e-151">Under **Subscription**, specify one for the new account.</span></span>

    <span data-ttu-id="ef76e-152">b.</span><span class="sxs-lookup"><span data-stu-id="ef76e-152">b.</span></span> <span data-ttu-id="ef76e-153">В разделе **Группа ресурсов** щелкните **Создать** или **Использовать существующую**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="ef76e-154">c.</span><span class="sxs-lookup"><span data-stu-id="ef76e-154">c.</span></span> <span data-ttu-id="ef76e-155">В разделе **Расположение** выберите расположение центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="ef76e-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="ef76e-156">В разделе **Создать учетную запись запуска от имени Azure** выберите **Да** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef76e-157">Если вы решили не создавать учетную запись запуска от имени и выбрали значение **Нет**, в колонке **Добавление учетной записи службы автоматизации** появится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="ef76e-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span></span> <span data-ttu-id="ef76e-158">Хотя учетная запись и создается на портале Azure, она не будет содержать соответствующее удостоверение проверки подлинности в службе каталогов классической подписки или подписки Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef76e-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="ef76e-159">Поэтому у этой учетной записи не будет доступа к ресурсам в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="ef76e-159">Consequently, the account has no access to resources in your subscription.</span></span> <span data-ttu-id="ef76e-160">В этом случае модули runbook, ссылающиеся на эту учетную запись, не смогут проходить проверку подлинности и выполнять задачи, используя ресурсы в соответствующих моделях развертывания.</span><span class="sxs-lookup"><span data-stu-id="ef76e-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Предупреждение в колонке "Добавление учетной записи службы автоматизации"](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="ef76e-162">Кроме того, если субъект-служба не создан, роль участника не назначается.</span><span class="sxs-lookup"><span data-stu-id="ef76e-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="ef76e-163">Ход создания учетной записи службы автоматизации в Azure можно отслеживать в разделе **Уведомления** в меню.</span><span class="sxs-lookup"><span data-stu-id="ef76e-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="resources"></a><span data-ttu-id="ef76e-164">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="ef76e-164">Resources</span></span>
<span data-ttu-id="ef76e-165">После создания учетной записи службы автоматизации автоматически создаются несколько ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef76e-165">When the Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="ef76e-166">Ниже представлена таблица, в которой указаны эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ef76e-166">The resources are summarized in the following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="ef76e-167">Ресурсы учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="ef76e-167">Run As account resources</span></span>

| <span data-ttu-id="ef76e-168">Ресурс</span><span class="sxs-lookup"><span data-stu-id="ef76e-168">Resource</span></span> | <span data-ttu-id="ef76e-169">Описание</span><span class="sxs-lookup"><span data-stu-id="ef76e-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef76e-170">Модуль Runbook AzureAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="ef76e-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="ef76e-171">Пример графического модуля runbook, который демонстрирует, как выполнить проверку подлинности с помощью учетной записи запуска от имени, и получает доступ ко всем ресурсам Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef76e-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="ef76e-172">Модуль Runbook AzureAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="ef76e-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="ef76e-173">Пример модуля runbook PowerShell, который демонстрирует, как выполнить проверку подлинности с помощью учетной записи запуска от имени, и получает доступ ко всем ресурсам Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef76e-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="ef76e-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="ef76e-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="ef76e-175">Ресурс сертификатов, автоматически создаваемый во время создания учетной записи службы автоматизации или с помощью приведенного ниже сценария PowerShell для имеющейся учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ef76e-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span></span> <span data-ttu-id="ef76e-176">Этот сертификат позволяет пройти проверку подлинности в Azure, что дает возможность управлять ресурсами Azure Resource Manager с помощью модулей runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="ef76e-177">Срок действия этого сертификата — один год.</span><span class="sxs-lookup"><span data-stu-id="ef76e-177">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="ef76e-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="ef76e-178">AzureRunAsConnection</span></span> | <span data-ttu-id="ef76e-179">Ресурс подключений, автоматически создаваемый во время создания учетной записи службы автоматизации или с помощью сценария PowerShell для имеющейся учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ef76e-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="ef76e-180">Ресурсы классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="ef76e-180">Classic Run As account resources</span></span>

| <span data-ttu-id="ef76e-181">Ресурс</span><span class="sxs-lookup"><span data-stu-id="ef76e-181">Resource</span></span> | <span data-ttu-id="ef76e-182">Описание</span><span class="sxs-lookup"><span data-stu-id="ef76e-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef76e-183">Модуль Runbook AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="ef76e-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="ef76e-184">Пример графического модуля runbook, который получает доступ ко всем виртуальным машинам, созданным с использованием классической модели развертывания, в подписке с помощью классической учетной записи запуска от имени (сертификат), а затем записывает имя и состояние виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ef76e-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="ef76e-185">Модуль Runbook AzureClassicAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="ef76e-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="ef76e-186">Пример модуля runbook PowerShell, который получает доступ ко всем классическим виртуальным машинам в подписке с помощью классической учетной записи запуска от имени (сертификат), а затем записывает имя и состояние виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ef76e-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="ef76e-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="ef76e-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="ef76e-188">Автоматически созданный ресурс сертификатов, используемый для проверки подлинности в Azure, что позволяет управлять классическими ресурсами Azure с помощью модулей runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="ef76e-189">Срок действия этого сертификата — один год.</span><span class="sxs-lookup"><span data-stu-id="ef76e-189">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="ef76e-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="ef76e-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="ef76e-191">Автоматически созданный ресурс подключений, используемый для проверки подлинности в Azure, что позволяет управлять классическими ресурсами Azure с помощью модулей runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="ef76e-192">Тестирование проверки подлинности с помощью учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="ef76e-192">Verify Run As authentication</span></span>
<span data-ttu-id="ef76e-193">Выполним небольшой тест, чтобы убедиться, что вы сможете успешно пройти проверку подлинности с помощью новой учетной записи запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="ef76e-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span></span>

1. <span data-ttu-id="ef76e-194">На портале Azure откройте учетную запись службы автоматизации, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="ef76e-194">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="ef76e-195">Щелкните элемент **Модули Runbook** , чтобы открыть список модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-195">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="ef76e-196">Выберите модуль runbook **AzureAutomationTutorialScript** и нажмите кнопку **Запустить**, чтобы запустить его.</span><span class="sxs-lookup"><span data-stu-id="ef76e-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span></span> <span data-ttu-id="ef76e-197">После этого происходят следующие события:</span><span class="sxs-lookup"><span data-stu-id="ef76e-197">The following events occur:</span></span>
 * <span data-ttu-id="ef76e-198">Создается [задание runbook](automation-runbook-execution.md), открывается колонка **Задание**, а на плитке **Сводка по заданию** отображается состояние задания.</span><span class="sxs-lookup"><span data-stu-id="ef76e-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="ef76e-199">Сначала задание получает состояние **В очереди**, указывающее на то, что задание ожидает, пока рабочая роль runbook в облаке станет доступной.</span><span class="sxs-lookup"><span data-stu-id="ef76e-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="ef76e-200">Как только рабочая роль затребует задание, оно получит состояние **Запущено**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-200">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="ef76e-201">С началом фактического выполнения модуля runbook состояние изменится на **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-201">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="ef76e-202">После выполнения задания runbook состояние должно измениться на **Выполнено**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-202">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="ef76e-203">Чтобы просмотреть подробные результаты задания runbook, щелкните плитку **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-203">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="ef76e-204">После этого откроется колонка **Выходные данные** со сведениями о том, что модуль runbook прошел проверку подлинности и вернул список всех ресурсов, доступных в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef76e-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span></span>

5. <span data-ttu-id="ef76e-205">Закройте колонку **Выходные данные**, чтобы вернуться к колонке **Сводка по заданию**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-205">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="ef76e-206">Закройте колонку **Сводка по заданию** и соответствующую колонку модуля runbook **AzureAutomationTutorialScript**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="ef76e-207">Тестирование проверки подлинности классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="ef76e-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="ef76e-208">Выполним небольшой похожий тест, чтобы убедиться, что вы сможете успешно пройти проверку подлинности с помощью новой классической учетной записи запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="ef76e-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span></span>

1. <span data-ttu-id="ef76e-209">На портале Azure откройте учетную запись службы автоматизации, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="ef76e-209">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="ef76e-210">Щелкните элемент **Модули Runbook** , чтобы открыть список модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-210">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="ef76e-211">Выберите модуль Runbook **AzureClassicAutomationTutorialScript** и нажмите кнопку **Запустить**, чтобы запустить его.</span><span class="sxs-lookup"><span data-stu-id="ef76e-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span></span> <span data-ttu-id="ef76e-212">После этого происходят следующие события:</span><span class="sxs-lookup"><span data-stu-id="ef76e-212">The following events occur:</span></span>

 * <span data-ttu-id="ef76e-213">Создается [задание runbook](automation-runbook-execution.md), открывается колонка **Задание**, а на плитке **Сводка по заданию** отображается состояние задания.</span><span class="sxs-lookup"><span data-stu-id="ef76e-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="ef76e-214">Сначала задание получает состояние **В очереди**, указывающее на то, что задание ожидает, пока рабочая роль runbook в облаке станет доступной.</span><span class="sxs-lookup"><span data-stu-id="ef76e-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="ef76e-215">Как только рабочая роль затребует задание, оно получит состояние **Запущено**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-215">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="ef76e-216">С началом фактического выполнения модуля runbook состояние изменится на **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-216">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="ef76e-217">После выполнения задания runbook состояние должно измениться на **Выполнено**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-217">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Тестирование модуля Runbook субъекта безопасности](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="ef76e-219">Чтобы просмотреть подробные результаты задания runbook, щелкните плитку **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-219">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="ef76e-220">После этого откроется колонка **Выходные данные** со сведениями о том, что модуль runbook прошел проверку подлинности и вернул список всех классических виртуальных машин в подписке.</span><span class="sxs-lookup"><span data-stu-id="ef76e-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span></span>

5. <span data-ttu-id="ef76e-221">Закройте колонку **Выходные данные**, чтобы вернуться к колонке **Сводка по заданию**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-221">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="ef76e-222">Закройте колонку **Сводка по заданию** и соответствующую колонку модуля runbook **AzureAutomationTutorialScript**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="ef76e-223">Управление учетной записью запуска от имени</span><span class="sxs-lookup"><span data-stu-id="ef76e-223">Managing your Run As account</span></span>
<span data-ttu-id="ef76e-224">В определенный момент перед истечением срока действия учетной записи службы автоматизации вам потребуется обновить сертификат.</span><span class="sxs-lookup"><span data-stu-id="ef76e-224">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="ef76e-225">Если вы считаете, что учетная запись запуска от имени была скомпрометирована, ее можно удалить и создать заново.</span><span class="sxs-lookup"><span data-stu-id="ef76e-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="ef76e-226">В этом разделе описано, как выполнить эти операции.</span><span class="sxs-lookup"><span data-stu-id="ef76e-226">This section discusses how to perform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="ef76e-227">Обновление самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="ef76e-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="ef76e-228">Срок действия самозаверяющего сертификата, созданного для учетной записи запуска от имени, составляет один год с момента создания.</span><span class="sxs-lookup"><span data-stu-id="ef76e-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="ef76e-229">Его можно обновить в любое время до истечения его срока действия.</span><span class="sxs-lookup"><span data-stu-id="ef76e-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="ef76e-230">При обновлении текущее значение сертификата сохраняется, чтобы гарантировать, что все модули runbook, которые поставлены в очередь или активно выполняются и для проверки подлинности которых используется учетная запись запуска от имени, не будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="ef76e-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="ef76e-231">Сертификат будет существовать до окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="ef76e-231">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="ef76e-232">Если вы настроили учетную запись запуска от имени службы автоматизации так, чтобы использовать сертификат, выданный центром сертификации предприятия, и используете этот параметр, то этот сертификат предприятия будет заменен самозаверяющим сертификатом.</span><span class="sxs-lookup"><span data-stu-id="ef76e-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="ef76e-233">Чтобы обновить сертификат, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ef76e-233">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="ef76e-234">На портале Azure откройте учетную запись службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-234">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="ef76e-235">В колонке **Учетная запись службы автоматизации** в области **свойств учетной записи** выберите **Учетные записи запуска от имени** в разделе **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Область свойств учетной записи службы автоматизации](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="ef76e-237">В колонке свойств **Учетные записи запуска от имени** выберите учетную запись запуска от имени или классическую учетную запись запуска от имени, для которой нужно обновить сертификат.</span><span class="sxs-lookup"><span data-stu-id="ef76e-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="ef76e-238">В колонке **Свойства** выбранной учетной записи щелкните **Обновление сертификата**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Обновление сертификата для учетной записи запуска от имени](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="ef76e-240">Ход обновления сертификата можно отслеживать в разделе **Уведомления** в меню.</span><span class="sxs-lookup"><span data-stu-id="ef76e-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="ef76e-241">Удаление учетной записи запуска от имени или классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="ef76e-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="ef76e-242">В этом разделе описано, как удалить и повторно создать учетную запись запуска от имени или классическую учетную запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="ef76e-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="ef76e-243">При выполнении этого действия учетная запись службы автоматизации сохраняется.</span><span class="sxs-lookup"><span data-stu-id="ef76e-243">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="ef76e-244">После удаления учетной записи запуска от имени или классической учетной записи запуска от имени ее можно создать заново на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ef76e-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="ef76e-245">На портале Azure откройте учетную запись службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-245">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="ef76e-246">В колонке **Учетная запись службы автоматизации** в области свойств учетной записи выберите **Учетные записи запуска от имени**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="ef76e-247">В колонке свойств **Учетные записи запуска от имени** выберите учетную запись запуска от имени или классическую учетную запись запуска от имени, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="ef76e-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="ef76e-248">Затем в колонке **Свойства** выбранной учетной записи щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Удаление учетной записи запуска от имени](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="ef76e-250">Ход удаления учетной записи можно отслеживать в разделе **Уведомления** в меню.</span><span class="sxs-lookup"><span data-stu-id="ef76e-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="ef76e-251">После удаления учетной записи ее можно повторно создать в колонке свойств **Учетные записи запуска от имени**, выбрав параметр создания **Учетная запись запуска от имени Azure**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Повторное создание учетной записи запуска от имени службы автоматизации](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="ef76e-253">Неправильные настройки</span><span class="sxs-lookup"><span data-stu-id="ef76e-253">Misconfiguration</span></span>
<span data-ttu-id="ef76e-254">Во время начальной настройки некоторые из элементов конфигурации, необходимых для правильной работы учетной записи запуска от имени или классической учетной записи запуска от имени, могут быть удалены или неправильно созданы.</span><span class="sxs-lookup"><span data-stu-id="ef76e-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="ef76e-255">К этим элементам относятся:</span><span class="sxs-lookup"><span data-stu-id="ef76e-255">The items include:</span></span>

* <span data-ttu-id="ef76e-256">ресурс сертификата,</span><span class="sxs-lookup"><span data-stu-id="ef76e-256">Certificate asset</span></span>
* <span data-ttu-id="ef76e-257">ресурс подключения,</span><span class="sxs-lookup"><span data-stu-id="ef76e-257">Connection asset</span></span>
* <span data-ttu-id="ef76e-258">учетная запись запуска от имени (удалена из роли участника),</span><span class="sxs-lookup"><span data-stu-id="ef76e-258">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="ef76e-259">субъект-служба или приложение-служба в Azure AD,</span><span class="sxs-lookup"><span data-stu-id="ef76e-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="ef76e-260">В случае такой неправильной настройки (или в других примерах) учетная запись службы автоматизации обнаружит эти изменения и отобразит в колонке свойств **Учетные записи запуска от имени** состояние *Не завершено*.</span><span class="sxs-lookup"><span data-stu-id="ef76e-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Сообщение о том, что настройка учетной записи запуска от имени не завершена](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="ef76e-262">При выборе учетной записи запуска от имени в области **Свойства** учетной записи отобразится следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="ef76e-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Предупреждение о том, что настройка учетной записи запуска от имени не завершена](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="ef76e-264">.</span><span class="sxs-lookup"><span data-stu-id="ef76e-264">.</span></span>

<span data-ttu-id="ef76e-265">Эти проблемы с учетной записью запуска от имени можно быстро устранить, удалив и повторно создав ее.</span><span class="sxs-lookup"><span data-stu-id="ef76e-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="ef76e-266">Обновление учетной записи службы автоматизации с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef76e-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="ef76e-267">Имеющуюся учетную запись службы автоматизации можно обновлять с помощью PowerShell в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="ef76e-267">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="ef76e-268">Вы создали учетную запись службы автоматизации, но не создали учетную запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="ef76e-268">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="ef76e-269">У вас уже есть учетная запись службы автоматизации для управления ресурсами Resource Manager, и вы хотите обновить ее, чтобы включить учетную запись запуска от имени в процедуру проверки подлинности модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="ef76e-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="ef76e-270">У вас есть учетная запись службы автоматизации для управления классическими ресурсами, и вы хотите обновить ее, чтобы использовать классическую учетную запись запуска от имени, а не создавать учетную запись и переносить в нее модули runbook и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ef76e-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="ef76e-271">Вы хотите создать учетную запись запуска от имени и классическую учетную запись запуска от имени, используя сертификат, выданный центром сертификации предприятия.</span><span class="sxs-lookup"><span data-stu-id="ef76e-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="ef76e-272">Предварительные требования для выполнения этого сценария:</span><span class="sxs-lookup"><span data-stu-id="ef76e-272">The script has the following prerequisites:</span></span>

* <span data-ttu-id="ef76e-273">Этот сценарий можно выполнять только в ОС Windows 10 и Windows Server 2016 с модулями Azure Resource Manager 2.01 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ef76e-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="ef76e-274">Более ранние версии Windows не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="ef76e-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="ef76e-275">Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ef76e-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="ef76e-276">Сведения о выпуске PowerShell 1.0 см. в статье [Приступая к работе с командлетами Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ef76e-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ef76e-277">Учетная запись службы автоматизации, указанная как значение для параметров *-AutomationAccountName* и *-ApplicationDisplayName* в приведенных ниже сценариях PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef76e-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="ef76e-278">Чтобы получить значения для параметров *SubscriptionID*, *ResourceGroup* и *AutomationAccountName*, которые являются обязательными для сценариев, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ef76e-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="ef76e-279">На портале Azure выберите свою учетную запись службы автоматизации в колонке **Учетная запись службы автоматизации** и выберите **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="ef76e-280">В колонке **Все параметры** в разделе **Параметры учетной записи** выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="ef76e-281">Обратите внимание на значения в колонке **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-281">Note the values on the **Properties** blade.</span></span>

![Колонка "Свойства" учетной записи службы автоматизации](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="ef76e-283">Создание сценария PowerShell для учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="ef76e-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="ef76e-284">Этот сценарий PowerShell включает в себя поддержку следующих конфигураций:</span><span class="sxs-lookup"><span data-stu-id="ef76e-284">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="ef76e-285">создание учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="ef76e-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="ef76e-286">создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="ef76e-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="ef76e-287">создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата;</span><span class="sxs-lookup"><span data-stu-id="ef76e-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="ef76e-288">создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата в облаке Azure для государственных организаций.</span><span class="sxs-lookup"><span data-stu-id="ef76e-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="ef76e-289">В зависимости от выбранного варианта конфигурации сценарий создает приведенные ниже элементы.</span><span class="sxs-lookup"><span data-stu-id="ef76e-289">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="ef76e-290">**Для учетной записи запуска от имени:**</span><span class="sxs-lookup"><span data-stu-id="ef76e-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="ef76e-291">Приложение Azure AD, используемое для экспорта самозаверяющего сертификата или открытого ключа корпоративного сертификата, и учетную запись субъекта-службы для этого приложения в Azure AD, а также назначает роль участника в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="ef76e-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="ef76e-292">Вместо этой роли можно использовать роль владельца или любую другую роль.</span><span class="sxs-lookup"><span data-stu-id="ef76e-292">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="ef76e-293">Дополнительные сведения см. в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="ef76e-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="ef76e-294">Ресурс сертификатов службы автоматизации с именем *AzureRunAsCertificate* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="ef76e-295">Этот ресурс содержит закрытый ключ сертификата, используемый в приложении Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef76e-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="ef76e-296">Ресурс подключений службы автоматизации с именем *AzureRunAsConnection* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="ef76e-297">Этот ресурс содержит идентификаторы приложения, клиента и подписки, а также отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="ef76e-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="ef76e-298">**Для классической учетной записи запуска от имени Azure:**</span><span class="sxs-lookup"><span data-stu-id="ef76e-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="ef76e-299">Ресурс сертификатов службы автоматизации с именем *AzureClassicRunAsCertificate* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="ef76e-300">Этот ресурс содержит закрытый ключ сертификата, используемый в сертификате управления.</span><span class="sxs-lookup"><span data-stu-id="ef76e-300">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="ef76e-301">Ресурс подключений службы автоматизации с именем *AzureClassicRunAsConnection* в указанной учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="ef76e-302">Этот ресурс содержит имя подписки, идентификатор подписки и имя ресурса сертификатов.</span><span class="sxs-lookup"><span data-stu-id="ef76e-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="ef76e-303">Если вы выбрали создание классической учетной записи запуска от имени, после выполнения сценария отправьте открытый сертификат (файл в формате CER) в хранилище управления подписки, в которой создана учетная запись службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

<span data-ttu-id="ef76e-304">Чтобы выполнить сценарий и отправить сертификат, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ef76e-304">To execute the script and upload the certificate, do the following:</span></span>

1. <span data-ttu-id="ef76e-305">Сохраните приведенный ниже сценарий на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ef76e-305">Save the following script on your computer.</span></span> <span data-ttu-id="ef76e-306">В этом примере используйте имя файла *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="ef76e-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="ef76e-307">На компьютере откройте меню **Пуск** и запустите с повышенными правами **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ef76e-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="ef76e-308">Из оболочки командной строки PowerShell с повышенными привилегиями перейдите в папку, которая содержит сценарий, созданный на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="ef76e-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span></span>

4. <span data-ttu-id="ef76e-309">Выполните этот сценарий, установив значения параметров в зависимости от требуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ef76e-309">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="ef76e-310">**Создание учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="ef76e-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="ef76e-311">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="ef76e-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="ef76e-312">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата**</span><span class="sxs-lookup"><span data-stu-id="ef76e-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="ef76e-313">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата в облаке Azure для государственных организаций**</span><span class="sxs-lookup"><span data-stu-id="ef76e-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="ef76e-314">После выполнения сценария появится запрос на проверку подлинности в Azure.</span><span class="sxs-lookup"><span data-stu-id="ef76e-314">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="ef76e-315">Войдите в систему, используя учетную запись, которая является участником роли "Администраторы подписки" и соадминистратором подписки.</span><span class="sxs-lookup"><span data-stu-id="ef76e-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="ef76e-316">После выполнения сценария обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="ef76e-316">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="ef76e-317">Если вы создали классическую учетную запись запуска от имени с использованием самозаверяющего открытого сертификата (CER-файл), сценарий создает ее и сохраняет в папке временных файлов на компьютере в профиле пользователя, который выполнял сеанс PowerShell: *%Профиль_пользователя%\AppData\Local\Temp*.</span><span class="sxs-lookup"><span data-stu-id="ef76e-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="ef76e-318">Если вы создали классическую учетную запись запуска от имени с использованием открытого корпоративного сертификата (CER-файл), используйте этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="ef76e-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="ef76e-319">Следуя инструкциям, [отправьте сертификат управления API на классический портал Azure](../azure-api-management-certs.md), а затем используйте [пример кода для проверки подлинности](#sample-code-to-authenticate-with-service-management-resources), чтобы проверить конфигурацию учетных данных с помощью ресурсов управления службами.</span><span class="sxs-lookup"><span data-stu-id="ef76e-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="ef76e-320">Если вы *не* создали классическую учетную запись запуска от имени, выполните проверку подлинности с помощью ресурсов Resource Manager и проверьте конфигурацию учетных данных, используя [этот пример кода](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="ef76e-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-to-authenticate-with-resource-manager-resources"></a><span data-ttu-id="ef76e-321">Пример кода для проверки подлинности с помощью ресурсов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef76e-321">Sample code to authenticate with Resource Manager resources</span></span>
<span data-ttu-id="ef76e-322">Чтобы выполнить проверку подлинности с помощью учетной записи запуска от имени для управления ресурсами Resource Manager, используя модули runbook, используйте обновленный пример кода, приведенный ниже, взятый из примера модуля runbook *AzureAutomationTutorialScript*.</span><span class="sxs-lookup"><span data-stu-id="ef76e-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get the connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in to Azure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context to a specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="ef76e-323">Этот сценарий содержит две дополнительные строки кода, что позволяет ссылаться на контекст подписки и без проблем работать с несколькими подписками.</span><span class="sxs-lookup"><span data-stu-id="ef76e-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="ef76e-324">Ресурс переменных *SubscriptionId* содержит идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="ef76e-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span></span> <span data-ttu-id="ef76e-325">После инструкции командлета `Add-AzureRmAccount` командлет [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) указывается с набором параметров *-SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="ef76e-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with the parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="ef76e-326">Если имя переменной слишком общее, вы можете изменить это имя, включив в него префикс или другое соглашение об именовании, чтобы упростить идентификацию.</span><span class="sxs-lookup"><span data-stu-id="ef76e-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span></span> <span data-ttu-id="ef76e-327">Кроме того, вы также можете использовать набор параметров *-SubscriptionName* вместо *-SubscriptionId* с соответствующим ресурсом переменных.</span><span class="sxs-lookup"><span data-stu-id="ef76e-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="ef76e-328">Командлет `Add-AzureRmAccount`, применяемый для проверки подлинности в модуле runbook, использует набор параметров *ServicePrincipalCertificate*.</span><span class="sxs-lookup"><span data-stu-id="ef76e-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="ef76e-329">Он выполняет проверку подлинности с помощью сертификата субъекта-службы, а не учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="ef76e-329">It authenticates by using the service principal certificate, not the user credentials.</span></span>

## <a name="sample-code-to-authenticate-with-service-management-resources"></a><span data-ttu-id="ef76e-330">Пример кода для проверки подлинности с помощью ресурсов управления службами</span><span class="sxs-lookup"><span data-stu-id="ef76e-330">Sample code to authenticate with Service Management resources</span></span>
<span data-ttu-id="ef76e-331">Чтобы выполнить проверку подлинности с помощью классической учетной записи запуска от имени для управления классическими ресурсами с помощью модулей runbook, используйте обновленный пример кода из примера модуля runbook *AzureClassicAutomationTutorialScript*, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="ef76e-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="ef76e-332">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef76e-332">Next steps</span></span>
* [<span data-ttu-id="ef76e-333">Объекты приложения и субъекта-службы в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef76e-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="ef76e-334">Управление доступом на основе ролей в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="ef76e-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="ef76e-335">Общие сведения о сертификатах для облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="ef76e-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
