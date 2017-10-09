---
title: "aaaConfigure Azure учетная запись запуска от | Документы Microsoft"
description: "Этот учебник поможет выполнить hello создания, тестирования и пример использования проверки подлинности субъекта безопасности в службе автоматизации Azure."
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
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="d4add-104">Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="d4add-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="d4add-105">В этой статье показано, как tooconfigure автоматизации Azure учетной записи в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d4add-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="d4add-106">toodo таким образом, используйте hello Запуск от имени учетной записи компонента tooauthenticate runbooks управление ресурсами в диспетчер ресурсов Azure и управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="d4add-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="d4add-107">При создании учетной записи автоматизации в hello портал Azure автоматически создавать две учетные записи:</span><span class="sxs-lookup"><span data-stu-id="d4add-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="d4add-108">Учетная запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="d4add-108">A Run As account.</span></span> <span data-ttu-id="d4add-109">Эта учетная запись создает субъект-службу в Azure Active Directory (Azure AD) и сертификат,</span><span class="sxs-lookup"><span data-stu-id="d4add-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="d4add-110">Присваивает hello участника доступом на основе ролей (RBAC), управляющему ресурсы диспетчера ресурсов с помощью Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="d4add-111">Классическая учетная запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="d4add-111">A Classic Run As account.</span></span> <span data-ttu-id="d4add-112">Этой учетной записи отправляет сертификат управления, который будет использоваться toomanage управления службами или классические ресурсы с помощью модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="d4add-113">Требуется создание автоматической учетной записи упрощает процесс hello для вас и помогает быстро начать создание и развертывание toosupport модули Runbook автоматизации.</span><span class="sxs-lookup"><span data-stu-id="d4add-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="d4add-114">Используя учетную запись запуска от имени и классическую учетную запись, вы можете:</span><span class="sxs-lookup"><span data-stu-id="d4add-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="d4add-115">Предоставить tooauthenticate стандартизованного Azure при управлении диспетчера ресурсов или ресурсов для службы управления из модулей Runbook в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d4add-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="d4add-116">Автоматизация hello Использование глобальных Runbook, которые можно настроить в Azure предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d4add-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="d4add-117">Hello [Azure integration функцию](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) с автоматизацией глобального модули Runbook требуется учетная запись автоматизации, для которой настроена учетная запись запуска от имени и классический учетной записи запуска.</span><span class="sxs-lookup"><span data-stu-id="d4add-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="d4add-118">Можно выбрать учетную запись автоматизации, который уже определен учетные записи запуска от имени и классический запуска от имени или toocreate можно выбрать учетную запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="d4add-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="d4add-119">В этой статье показано, как toocreate учетной записи автоматизации из hello портал Azure, обновить учетную запись службы автоматизации с помощью Azure PowerShell, управление конфигурацией учетной записи hello и проходить проверку подлинности в модули Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="d4add-120">Перед началом создания учетной записи автоматизации, он toounderstand смысл и рассмотрите hello ниже:</span><span class="sxs-lookup"><span data-stu-id="d4add-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="d4add-121">Создание учетной записи автоматизации не влияет на учетные записи автоматизации, могут уже созданных в классическом hello или модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4add-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="d4add-122">Hello процесс работает только для учетных записей автоматизации, создаваемые в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d4add-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="d4add-123">Попытка toocreate учетную запись из классического портала Azure hello конфигурации учетной записи запуска от имени для hello не реплицируются.</span><span class="sxs-lookup"><span data-stu-id="d4add-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="d4add-124">Если уже имеется Runbook и ресурсов (например, расписаниями и переменные) в месте toomanage классические ресурсы, и требуется tooauthenticate модулей Runbook с hello новой классический запуска от имени учетной записи, выполните одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="d4add-125">toocreate классический запуска от имени учетной записи, следуйте инструкциям hello в разделе «Управление вашей учетной записи запуска от» hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="d4add-126">tooupdate существующей учетной записи, используйте hello PowerShell сценария в разделе «Обновление учетной записи автоматизации с помощью PowerShell» hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="d4add-127">tooauthenticate с помощью hello новый запуск от имени учетной записи и классический запуска как автоматизации необходимо существующие модули Runbook с hello пример кода, приведенный в разделе hello toomodify [примеры кода проверки подлинности](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="d4add-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="d4add-128">Hello учетная запись запуска от имени — для проверки подлинности с помощью участника службы на основе сертификатов hello ресурсы диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4add-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="d4add-129">для проверки подлинности в службе управления ресурсами с сертификатом управления — Hello классический запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="d4add-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="d4add-130">Создание учетной записи автоматизации из hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d4add-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="d4add-131">В этом разделе создайте учетную запись службы автоматизации Azure из hello портал Azure, который в свою очередь, создает учетную запись запуска от имени и классический учетной записи запуска.</span><span class="sxs-lookup"><span data-stu-id="d4add-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="d4add-132">toocreate учетной записи автоматизации, необходимо быть членом роли администраторов службы hello или соадминистратором подписки hello, который предоставляет доступ toohello подписки.</span><span class="sxs-lookup"><span data-stu-id="d4add-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="d4add-133">Кроме того, вы должны добавить подписку toothat пользователя экземпляром по умолчанию Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d4add-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="d4add-134">Hello не обязательно toobe назначенный привилегированной роли.</span><span class="sxs-lookup"><span data-stu-id="d4add-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="d4add-135">Если вы не является членом экземпляра Active Directory hello подписки до добавления роли toohello соадминистратора подписки hello, вы будете добавлять tooActive каталог как Гость.</span><span class="sxs-lookup"><span data-stu-id="d4add-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="d4add-136">В этом случае вы получите «у вас разрешения toocreate...»</span><span class="sxs-lookup"><span data-stu-id="d4add-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="d4add-137">Предупреждение, hello **Добавление учетной записи автоматизации** колонку.</span><span class="sxs-lookup"><span data-stu-id="d4add-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="d4add-138">Пользователи, добавленные в роль соадминистратора toohello сначала можно удалить из экземпляра Active Directory hello подписки и повторно добавлен toomake их полный пользователя в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d4add-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="d4add-139">tooverify таких ситуаций с hello **Azure Active Directory** область в Azure портал, выбрав hello **пользователей и групп**, выбрав **всех пользователей** и после выбора Hello конкретного пользователя, при выборе **профиль**.</span><span class="sxs-lookup"><span data-stu-id="d4add-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="d4add-140">Здравствуйте, значение hello **тип пользователя** атрибут профиля hello пользователи не должны быть равны **гостевой**.</span><span class="sxs-lookup"><span data-stu-id="d4add-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="d4add-141">Войдите в портал Azure с учетную запись, которая является членом роли администраторов подписки hello и соадминистратором подписки hello toohello.</span><span class="sxs-lookup"><span data-stu-id="d4add-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="d4add-142">Выберите элемент **Учетные записи службы автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="d4add-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="d4add-143">На hello **учетные записи автоматизации** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="d4add-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="d4add-144">Hello **Добавление учетной записи автоматизации** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="d4add-144">hello **Add Automation Account** blade opens.</span></span>

 ![Колонка «Добавить учетную запись автоматизации» Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="d4add-146">Если ваша учетная запись не является членом роли администраторов подписки hello и соадминистратором подписки hello, hello следующие предупреждения отображается на hello **Добавление учетной записи автоматизации** колонки:</span><span class="sxs-lookup"><span data-stu-id="d4add-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![Предупреждение в колонке "Добавление учетной записи службы автоматизации"](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="d4add-148">На hello **Добавление учетной записи автоматизации** колонки в hello **имя** введите имя для учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="d4add-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="d4add-149">Если у вас есть несколько подписок, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d4add-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="d4add-150">а.</span><span class="sxs-lookup"><span data-stu-id="d4add-150">a.</span></span> <span data-ttu-id="d4add-151">В разделе **подписки**, укажите один для новой учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="d4add-152">b.</span><span class="sxs-lookup"><span data-stu-id="d4add-152">b.</span></span> <span data-ttu-id="d4add-153">В разделе **Группа ресурсов** щелкните **Создать** или **Использовать существующую**.</span><span class="sxs-lookup"><span data-stu-id="d4add-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="d4add-154">c.</span><span class="sxs-lookup"><span data-stu-id="d4add-154">c.</span></span> <span data-ttu-id="d4add-155">В разделе **Расположение** выберите расположение центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d4add-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="d4add-156">В разделе **Создать учетную запись запуска от имени Azure** выберите **Да** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d4add-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d4add-157">При выборе не toocreate hello запуска от имени учетной записи, выбрав **нет**, выводится предупреждающее сообщение hello **Добавление учетной записи автоматизации** колонку.</span><span class="sxs-lookup"><span data-stu-id="d4add-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="d4add-158">Несмотря на то, что hello учетная запись создается в hello портал Azure, он не имеет соответствующего удостоверение проверки подлинности в вашей классический или службы каталогов подписки для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4add-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="d4add-159">Таким образом учетная запись hello имеет tooresources нет доступа в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="d4add-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="d4add-160">В этом случае модули runbook, ссылающиеся на эту учетную запись, не смогут проходить проверку подлинности и выполнять задачи, используя ресурсы в соответствующих моделях развертывания.</span><span class="sxs-lookup"><span data-stu-id="d4add-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Предупреждающее сообщение в колонке «Добавить учетную запись автоматизации» hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="d4add-162">Кроме того поскольку hello участника-службы не создается, не назначена роль участника hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="d4add-163">Пока Azure создает учетную запись автоматизации hello, можно отслеживать ход выполнения hello в **уведомления** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="d4add-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="d4add-164">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="d4add-164">Resources</span></span>
<span data-ttu-id="d4add-165">Если hello учетную запись автоматизации успешно создана, некоторые ресурсы создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="d4add-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="d4add-166">ресурсы Hello, приведены в hello, следующие две таблицы:</span><span class="sxs-lookup"><span data-stu-id="d4add-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="d4add-167">Ресурсы учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="d4add-167">Run As account resources</span></span>

| <span data-ttu-id="d4add-168">Ресурс</span><span class="sxs-lookup"><span data-stu-id="d4add-168">Resource</span></span> | <span data-ttu-id="d4add-169">Описание</span><span class="sxs-lookup"><span data-stu-id="d4add-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4add-170">Модуль Runbook AzureAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="d4add-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="d4add-171">Пример графический runbook, показано, как tooauthenticate с помощью hello учетная запись запуска от имени и получает все ресурсы диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="d4add-172">Модуль Runbook AzureAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="d4add-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="d4add-173">Пример runbook PowerShell, который демонстрирует, как tooauthenticate с помощью hello учетная запись запуска от имени и возвращает все ресурсы диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="d4add-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="d4add-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="d4add-175">Hello активов сертификат, который создается автоматически при создании учетной записи автоматизации или использовать hello следующий сценарий PowerShell для существующей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d4add-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="d4add-176">Hello сертификата позволяет tooauthenticate с Azure, чтобы ресурсы диспетчера ресурсов Azure можно управлять из модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="d4add-177">Hello сертификат имеет время существования в один год.</span><span class="sxs-lookup"><span data-stu-id="d4add-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="d4add-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="d4add-178">AzureRunAsConnection</span></span> | <span data-ttu-id="d4add-179">ресурс подключения Hello, который создается автоматически при создании учетной записи автоматизации или использовать сценарий PowerShell hello существующей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d4add-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="d4add-180">Ресурсы классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="d4add-180">Classic Run As account resources</span></span>

| <span data-ttu-id="d4add-181">Ресурс</span><span class="sxs-lookup"><span data-stu-id="d4add-181">Resource</span></span> | <span data-ttu-id="d4add-182">Описание</span><span class="sxs-lookup"><span data-stu-id="d4add-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4add-183">Модуль Runbook AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="d4add-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="d4add-184">Пример графический runbook, возвращает все виртуальные машины hello, которые создаются с помощью hello классической модели развертывания в подписке с помощью hello классический запуска от имени учетной записи (сертификат), а затем записывает имя виртуальной Машины hello и состояние.</span><span class="sxs-lookup"><span data-stu-id="d4add-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="d4add-185">Модуль Runbook AzureClassicAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="d4add-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="d4add-186">Пример runbook PowerShell, который получает все hello классические ВМ в подписке с помощью hello классический запуска от имени учетной записи (сертификат), а затем записывает hello имя виртуальной Машины и состояния.</span><span class="sxs-lookup"><span data-stu-id="d4add-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="d4add-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="d4add-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="d4add-188">активов Hello автоматически создается сертификат, используйте tooauthenticate с Azure, чтобы вы могли управлять Azure классические ресурсы из модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="d4add-189">Hello сертификат имеет время существования в один год.</span><span class="sxs-lookup"><span data-stu-id="d4add-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="d4add-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="d4add-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="d4add-191">средство автоматически созданное подключение Hello использовать tooauthenticate с Azure, чтобы вы могли управлять Azure классические ресурсы из модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="d4add-192">Тестирование проверки подлинности с помощью учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="d4add-192">Verify Run As authentication</span></span>
<span data-ttu-id="d4add-193">Выполните tooconfirm небольшой тест, который может успешно проверить подлинность с помощью hello новую учетную запись запуска.</span><span class="sxs-lookup"><span data-stu-id="d4add-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="d4add-194">Hello портал Azure откройте hello учетной записи автоматизации, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="d4add-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="d4add-195">Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="d4add-196">Выберите hello **AzureAutomationTutorialScript** runbook, а затем нажмите кнопку **запустить** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="d4add-197">происходят следующие события Hello:</span><span class="sxs-lookup"><span data-stu-id="d4add-197">hello following events occur:</span></span>
 * <span data-ttu-id="d4add-198">Объект [задание runbook](automation-runbook-execution.md) создания hello **задания** колонке отображается, и состояние задания hello в hello **Сводка заданий** плитки.</span><span class="sxs-lookup"><span data-stu-id="d4add-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="d4add-199">состояние задания Hello начинается **в очереди**, означает, что он ожидает runbook worker в доступных toobecome облака hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="d4add-200">состояние Hello становится **запуск** когда исполнитель утверждений hello задания.</span><span class="sxs-lookup"><span data-stu-id="d4add-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="d4add-201">состояние Hello становится **под управлением** при запуске hello runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="d4add-202">Задание runbook hello закончит работу, вы увидите состояние **завершено**.</span><span class="sxs-lookup"><span data-stu-id="d4add-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="d4add-203">toosee Здравствуйте подробные результаты hello runbook, щелкните hello **вывода** плитки.</span><span class="sxs-lookup"><span data-stu-id="d4add-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="d4add-204">Hello **вывода** колонке отображается отображение этого модуля hello успешно проверку подлинности и возвращается список всех ресурсов, доступных в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="d4add-205">Закрыть hello **вывода** toohello tooreturn колонке **Сводка заданий** колонку.</span><span class="sxs-lookup"><span data-stu-id="d4add-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="d4add-206">Закрыть hello **Сводка заданий** колонки и соответствующими hello **AzureAutomationTutorialScript** колонки runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="d4add-207">Тестирование проверки подлинности классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="d4add-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="d4add-208">Выполните небольшой аналогичные тестирования tooconfirm, вы можете успешно проверять подлинность с помощью hello новой классический запуска от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d4add-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="d4add-209">Hello портал Azure откройте hello учетной записи автоматизации, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="d4add-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="d4add-210">Нажмите кнопку hello **Runbooks** плитки tooopen hello список модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="d4add-211">Выберите hello **AzureClassicAutomationTutorialScript** runbook, а затем нажмите кнопку **запустить** слишком запустить hello runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="d4add-212">происходят следующие события Hello:</span><span class="sxs-lookup"><span data-stu-id="d4add-212">hello following events occur:</span></span>

 * <span data-ttu-id="d4add-213">Объект [задание runbook](automation-runbook-execution.md) создания hello **задания** колонке отображается, и состояние задания hello в hello **Сводка заданий** плитки.</span><span class="sxs-lookup"><span data-stu-id="d4add-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="d4add-214">состояние задания Hello начинается **в очереди**, означает, что он ожидает runbook worker в доступных toobecome облака hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="d4add-215">состояние Hello становится **запуск** когда исполнитель утверждений hello задания.</span><span class="sxs-lookup"><span data-stu-id="d4add-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="d4add-216">состояние Hello становится **под управлением** при запуске hello runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="d4add-217">Задание runbook hello закончит работу, вы увидите состояние **завершено**.</span><span class="sxs-lookup"><span data-stu-id="d4add-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Тестирование модуля Runbook субъекта безопасности](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="d4add-219">toosee Здравствуйте подробные результаты hello runbook, щелкните hello **вывода** плитки.</span><span class="sxs-lookup"><span data-stu-id="d4add-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="d4add-220">Hello **вывода** колонке отображается отображение этого модуля hello успешно проверку подлинности и возвращается список всех классических ВМ в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="d4add-221">Закрыть hello **вывода** toohello tooreturn колонке **Сводка заданий** колонку.</span><span class="sxs-lookup"><span data-stu-id="d4add-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="d4add-222">Закрыть hello **Сводка заданий** колонки и соответствующими hello **AzureAutomationTutorialScript** колонки runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="d4add-223">Управление учетной записью запуска от имени</span><span class="sxs-lookup"><span data-stu-id="d4add-223">Managing your Run As account</span></span>
<span data-ttu-id="d4add-224">В некоторый момент до истечения срока действия учетной записи автоматизации, потребуется сертификат toorenew hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="d4add-225">Если вы считаете, что был скомпрометирован, hello учетная запись запуска от имени, можно удалить и создать его повторно.</span><span class="sxs-lookup"><span data-stu-id="d4add-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="d4add-226">В этом разделе рассматриваются как tooperform этих операций.</span><span class="sxs-lookup"><span data-stu-id="d4add-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="d4add-227">Обновление самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="d4add-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="d4add-228">Hello самозаверяющий сертификат, созданный для hello учетная запись запуска от имени истекает один год после даты создания hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="d4add-229">Его можно обновить в любое время до истечения его срока действия.</span><span class="sxs-lookup"><span data-stu-id="d4add-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="d4add-230">При обновлении, hello текущего действительного сертификата — зависимых tooensure, что все модули Runbook, помещаются в очередь до или активно работает и что аутентификации hello учетная запись запуска от имени, не подвергаются отрицательно.</span><span class="sxs-lookup"><span data-stu-id="d4add-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="d4add-231">Hello сертификат остается действительным до истечения срока ее.</span><span class="sxs-lookup"><span data-stu-id="d4add-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="d4add-232">Если вы настроили ваш автоматизации Запуск от имени учетной записи toouse сертификат, выданный центром сертификации предприятия и использовать этот параметр, hello корпоративный сертификат будет заменен самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="d4add-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="d4add-233">toorenew hello сертификатов, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d4add-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="d4add-234">Откройте в hello портал Azure, учетная запись автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="d4add-235">На hello **учетной записи автоматизации** колонки в hello **свойства учетной записи** панели в разделе **параметры учетной записи**выберите **учетные записи запуска от**.</span><span class="sxs-lookup"><span data-stu-id="d4add-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Область свойств учетной записи службы автоматизации](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="d4add-237">На hello **учетные записи запуска от** свойства колонке выберите либо hello Запуск от имени учетной записи или hello классический запуска от имени, требуется сертификат toorenew hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="d4add-238">На hello **свойства** колонке hello выбранную учетную запись, нажмите кнопку **продления сертификата**.</span><span class="sxs-lookup"><span data-stu-id="d4add-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Обновление сертификата для учетной записи запуска от имени](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="d4add-240">При продлении сертификата hello, отслеживания хода hello под **уведомления** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="d4add-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="d4add-241">Удаление учетной записи запуска от имени или классической учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="d4add-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="d4add-242">В этом разделе описываются как toodelete и повторного создания учетной записи запуска от имени или классический Запуск от имени.</span><span class="sxs-lookup"><span data-stu-id="d4add-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="d4add-243">После выполнения этого действия сохраняется hello учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="d4add-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="d4add-244">После удаления учетной записи запуска от имени или классический запуска от имени, повторно создать его hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d4add-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="d4add-245">Откройте в hello портал Azure, учетная запись автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="d4add-246">На hello **учетной записи автоматизации** колонке hello учетной записи «свойства» выберите **учетные записи запуска от**.</span><span class="sxs-lookup"><span data-stu-id="d4add-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="d4add-247">На hello **учетные записи запуска от** колонку свойств, выберите либо hello Запуск от имени учетной записи или классический запуска от имени учетной записи, которые должны toodelete.</span><span class="sxs-lookup"><span data-stu-id="d4add-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="d4add-248">Затем на hello **свойства** колонке hello выбранную учетную запись, нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="d4add-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Удаление учетной записи запуска от имени](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="d4add-250">Во время удаления учетной записи hello, отслеживания хода hello под **уведомления** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="d4add-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="d4add-251">После удаления учетной записи hello, его можно повторно создать на hello **учетные записи запуска от** колонку свойств, выбрав hello создать параметр **Azure учетная запись запуска от имени**.</span><span class="sxs-lookup"><span data-stu-id="d4add-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Повторно создать hello автоматизации Запуск от имени учетной записи](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="d4add-253">Неправильные настройки</span><span class="sxs-lookup"><span data-stu-id="d4add-253">Misconfiguration</span></span>
<span data-ttu-id="d4add-254">Некоторые элементы конфигурации, необходимые для hello toofunction учетная запись запуска от имени или классический Запуск от имени правильно может была удалена или создана неправильно во время начальной настройки.</span><span class="sxs-lookup"><span data-stu-id="d4add-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="d4add-255">Hello элементы включают:</span><span class="sxs-lookup"><span data-stu-id="d4add-255">hello items include:</span></span>

* <span data-ttu-id="d4add-256">ресурс сертификата,</span><span class="sxs-lookup"><span data-stu-id="d4add-256">Certificate asset</span></span>
* <span data-ttu-id="d4add-257">ресурс подключения,</span><span class="sxs-lookup"><span data-stu-id="d4add-257">Connection asset</span></span>
* <span data-ttu-id="d4add-258">Учетная запись запуска от имени был удален из роли участника hello</span><span class="sxs-lookup"><span data-stu-id="d4add-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="d4add-259">субъект-служба или приложение-служба в Azure AD,</span><span class="sxs-lookup"><span data-stu-id="d4add-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="d4add-260">В предыдущем hello и другие экземпляры неправильной настройки, приветствия учетной записи автоматизации обнаруживает hello изменяет и отображает состояние *неполный* на hello **учетные записи запуска от** колонку свойств для hello Учетная запись.</span><span class="sxs-lookup"><span data-stu-id="d4add-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Сообщение о том, что настройка учетной записи запуска от имени не завершена](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="d4add-262">При выборе hello запись запуска от имени учетной записи Здравствуйте, **свойства** отображаются hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="d4add-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Предупреждение о том, что настройка учетной записи запуска от имени не завершена](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="d4add-264">.</span><span class="sxs-lookup"><span data-stu-id="d4add-264">.</span></span>

<span data-ttu-id="d4add-265">Позволяет быстро устранить эти проблемы учетная запись запуска от имени, удаления и повторного создания учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="d4add-266">Обновление учетной записи службы автоматизации с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4add-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="d4add-267">Можно использовать существующую учетную запись автоматизации PowerShell tooupdate, если:</span><span class="sxs-lookup"><span data-stu-id="d4add-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="d4add-268">Создание учетной записи автоматизации, но отклонить toocreate hello запуска от имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d4add-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="d4add-269">Ресурсы диспетчера ресурсов автоматизации toomanage учетной записи уже используется, и требуется tooupdate hello tooinclude hello запуска от имени учетной записи для проверки подлинности runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="d4add-270">Учетная запись автоматизации toomanage классические ресурсы уже используется и нужно tooupdate его toouse hello классический запуска от имени учетной записи вместо создания новой учетной записи и переход к tooit Runbook и активов.</span><span class="sxs-lookup"><span data-stu-id="d4add-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="d4add-271">Требуется toocreate запуска от имени, а классические учетной записи запуска с помощью сертификата, выданного вашего центра сертификации предприятия (ЦС).</span><span class="sxs-lookup"><span data-stu-id="d4add-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="d4add-272">сценарий Hello имеет hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="d4add-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="d4add-273">Hello сценарий может выполняться только в Windows 10 и Windows Server 2016 с модулями Azure Resource Manager 2.01 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d4add-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="d4add-274">Более ранние версии Windows не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="d4add-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="d4add-275">Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d4add-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="d4add-276">Сведения о выпуске hello PowerShell 1.0 см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4add-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d4add-277">Учетная запись автоматизации, на которую ссылается как значение hello для hello *— AutomationAccountName* и *- ApplicationDisplayName* параметры в следующем скрипте PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="d4add-278">tooget hello значения для *SubscriptionID*, *ResourceGroup*, и *AutomationAccountName*, которой являются обязательными параметрами для скриптов hello, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d4add-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="d4add-279">В hello портал Azure, выберите учетную запись автоматизации на hello **учетной записи автоматизации** колонки, а затем выберите **все параметры**.</span><span class="sxs-lookup"><span data-stu-id="d4add-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="d4add-280">На hello **все параметры** колонки в разделе **параметры учетной записи**выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="d4add-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="d4add-281">Запишите значения hello на hello **свойства** колонку.</span><span class="sxs-lookup"><span data-stu-id="d4add-281">Note hello values on hello **Properties** blade.</span></span>

![колонку «Свойства» учетной записи автоматизации Hello](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="d4add-283">Создание сценария PowerShell для учетной записи запуска от имени</span><span class="sxs-lookup"><span data-stu-id="d4add-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="d4add-284">Этот сценарий PowerShell поддерживает hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d4add-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="d4add-285">создание учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="d4add-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="d4add-286">создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата;</span><span class="sxs-lookup"><span data-stu-id="d4add-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="d4add-287">создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата;</span><span class="sxs-lookup"><span data-stu-id="d4add-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="d4add-288">Создайте учетную запись запуска от имени и классический учетной записи запуска с помощью самозаверяющего сертификата в облако Azure для государственных hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="d4add-289">В зависимости от hello параметров настройки при выборе hello скрипт создает hello следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="d4add-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="d4add-290">**Для учетной записи запуска от имени:**</span><span class="sxs-lookup"><span data-stu-id="d4add-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="d4add-291">Создает Azure AD приложения toobe экспортируются вместе с любой hello самозаверяющий или enterprise открытый ключ сертификата, создает основной учетной записи службы для приложения hello в Azure AD и назначает hello роль участника для учетной записи hello в существующую подписка.</span><span class="sxs-lookup"><span data-stu-id="d4add-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="d4add-292">Можно изменить этот параметр tooOwner или любая другая роль.</span><span class="sxs-lookup"><span data-stu-id="d4add-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="d4add-293">Дополнительные сведения см. в статье [Управление доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="d4add-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="d4add-294">Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureRunAsCertificate* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="d4add-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="d4add-295">Hello активов сертификат содержит закрытый ключ сертификата hello, используемого приложением hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4add-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="d4add-296">Создает ресурс подключения автоматизации с именем *AzureRunAsConnection* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="d4add-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="d4add-297">ресурс-контейнер подключений Hello содержит идентификатор приложения hello, идентификатора клиента, идентификатор подписки и отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="d4add-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="d4add-298">**Для классической учетной записи запуска от имени Azure:**</span><span class="sxs-lookup"><span data-stu-id="d4add-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="d4add-299">Создает ресурс-контейнер сертификата службы автоматизации с именем *AzureClassicRunAsCertificate* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="d4add-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="d4add-300">Hello активов сертификат содержит закрытый ключ сертификата hello используемый сертификат управления hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="d4add-301">Создает ресурс подключения автоматизации с именем *AzureClassicRunAsConnection* в hello указана учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="d4add-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="d4add-302">ресурс-контейнер подключений Hello содержит имя подписки hello, идентификатор подписки и имя актива сертификатов.</span><span class="sxs-lookup"><span data-stu-id="d4add-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="d4add-303">При выборе любой из параметров для создания классических запуска от имени учетной записи, после выполнения сценария hello передачи hello открытый сертификат управления (CER-файл с расширением) toohello хранения для подписки hello этой учетной записи автоматизации hello был создан в.</span><span class="sxs-lookup"><span data-stu-id="d4add-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="d4add-304">tooexecute Здравствуйте сценарий и передать сертификат hello, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d4add-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="d4add-305">Сохраните следующий сценарий на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-305">Save hello following script on your computer.</span></span> <span data-ttu-id="d4add-306">В этом примере, сохраните его с именем файла hello *New RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="d4add-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="d4add-307">На компьютере откройте меню **Пуск** и запустите с повышенными правами **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d4add-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="d4add-308">Из hello повышенными оболочка командной строки PowerShell, toohello откройте папку, содержащую hello скрипт, созданный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="d4add-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="d4add-309">Выполните сценарий hello, используя значения параметров hello hello конфигурации, требуемую.</span><span class="sxs-lookup"><span data-stu-id="d4add-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="d4add-310">**Создание учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="d4add-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="d4add-311">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени с использованием самозаверяющего сертификата**</span><span class="sxs-lookup"><span data-stu-id="d4add-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="d4add-312">**Создание учетной записи запуска от имени и классической учетной записи запуска от имени Azure с использованием корпоративного сертификата**</span><span class="sxs-lookup"><span data-stu-id="d4add-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="d4add-313">**Создание учетной записи запуска от имени и классический учетной записи запуска с помощью самозаверяющего сертификата в облако Azure для государственных hello**</span><span class="sxs-lookup"><span data-stu-id="d4add-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="d4add-314">После выполнения сценария hello, появится запрос tooauthenticate с Azure.</span><span class="sxs-lookup"><span data-stu-id="d4add-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="d4add-315">Войдите с учетной записью, которая является членом роли администраторов подписки hello и соадминистратором подписки hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="d4add-316">После успешного выполнения сценария hello Обратите внимание hello следующее:</span><span class="sxs-lookup"><span data-stu-id="d4add-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="d4add-317">При создании классического учетной записи запуска с общей самозаверяющего сертификата (CER-файл), hello скрипт создает и сохраняет его toohello в папке временных файлов на компьютере в пользовательском профиле hello *%USERPROFILE%\AppData\Local\Temp*, мы использовали сеанс PowerShell tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="d4add-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="d4add-318">Если вы создали классическую учетную запись запуска от имени с использованием открытого корпоративного сертификата (CER-файл), используйте этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="d4add-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="d4add-319">Следуйте инструкциям hello [передачи toohello сертификата API управления классический портал Azure](../azure-api-management-certs.md)и последующей проверки hello конфигурации учетных данных с ресурсами службы управления с помощью hello [пример кода tooauthenticate с ресурсами службы управления](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="d4add-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="d4add-320">Если вы уже сделали *не* создания классических учетной записи запуска, проверки подлинности в ресурсах диспетчера ресурсов и проверка конфигурации hello учетных данных с помощью hello [пример кода для проверки подлинности с помощью службы управления ресурсы](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="d4add-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="d4add-321">Образец кода tooauthenticate с ресурсами диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4add-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="d4add-322">Можно использовать следующие hello обновлен пример кода, взяты из hello *AzureAutomationTutorialScript* пример runbook, tooauthenticate с помощью hello запуска от имени учетной записи toomanage диспетчера ресурсов ресурсов с помощью модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
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

<span data-ttu-id="d4add-323">toohelp вы tooeasily работы между несколькими подписками, hello скрипт включает два дополнительных строк кода, поддерживающие создание ссылок на контекст подписки.</span><span class="sxs-lookup"><span data-stu-id="d4add-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="d4add-324">Переменная ресурса с именем *SubscriptionId* содержит идентификатор hello hello подписки.</span><span class="sxs-lookup"><span data-stu-id="d4add-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="d4add-325">После hello `Add-AzureRmAccount` инструкции командлет hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) командлет устанавливается с набором параметров hello *- SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="d4add-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="d4add-326">Если имя переменной hello слишком универсален, можно зашифрованного tooinclude префикс или использовать другой именования toomake соглашение о его проще tooidentify.</span><span class="sxs-lookup"><span data-stu-id="d4add-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="d4add-327">Кроме того, можно использовать набор параметров hello *- SubscriptionName* вместо *- SubscriptionId* с соответствующей переменной активов.</span><span class="sxs-lookup"><span data-stu-id="d4add-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="d4add-328">Здравствуйте, командлет, который используется для проверки подлинности в hello runbook `Add-AzureRmAccount`, использует hello *ServicePrincipalCertificate* набор параметров.</span><span class="sxs-lookup"><span data-stu-id="d4add-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="d4add-329">Проверяет подлинность с помощью hello службы субъекта сертификата, не hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="d4add-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="d4add-330">Образец кода tooauthenticate с ресурсами службы управления</span><span class="sxs-lookup"><span data-stu-id="d4add-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="d4add-331">Можно использовать следующий код обновленный образец, который будет взято из hello hello *AzureClassicAutomationTutorialScript* пример runbook, tooauthenticate с помощью hello классический запуска от имени учетной записи toomanage классические ресурсы с вашей модули Runbook.</span><span class="sxs-lookup"><span data-stu-id="d4add-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="d4add-332">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4add-332">Next steps</span></span>
* [<span data-ttu-id="d4add-333">Объекты приложения и субъекта-службы в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4add-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="d4add-334">Управление доступом на основе ролей в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="d4add-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="d4add-335">Общие сведения о сертификатах для облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="d4add-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
