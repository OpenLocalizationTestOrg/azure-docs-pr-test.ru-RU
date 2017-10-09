---
title: "планы toorecovery aaaAdd автоматизации Azure модули Runbook в Azure Site Recovery | Документы Microsoft"
description: "Узнайте, как Azure Site Recovery помогает расширить планы восстановления с помощью службы автоматизации Azure. Узнайте, как toocomplete комплексных задач во время восстановления tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="503d0-104">Добавить схемы toorecovery модулей Runbook службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="503d0-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="503d0-105">В этой статье описывается как интегрируется Azure Site Recovery с toohelp автоматизации Azure расширить планах восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="503d0-106">Планы восстановления могут управлять восстановлением виртуальных машин, защищенных с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="503d0-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="503d0-107">Планы восстановления работают как для репликации tooa вторичное облако, так и для tooAzure репликации.</span><span class="sxs-lookup"><span data-stu-id="503d0-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="503d0-108">Планы восстановления также помогают сделать hello восстановления **точных**, **repeatable**, и **автоматических**.</span><span class="sxs-lookup"><span data-stu-id="503d0-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="503d0-109">Если переход на виртуальных машинах tooAzure интеграции в службе автоматизации Azure расширяет планах восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="503d0-110">Его можно использовать tooexecute Runbook, которые предоставляют мощные автоматизации задач.</span><span class="sxs-lookup"><span data-stu-id="503d0-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="503d0-111">Если новый tooAzure автоматизации, вы можете [зарегистрироваться](https://azure.microsoft.com/services/automation/) и [загрузить примеры скриптов](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="503d0-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="503d0-112">Дополнительные сведения и toolearn как tooorchestrate tooAzure восстановления с помощью [планы восстановления](https://azure.microsoft.com/blog/?p=166264), в разделе [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="503d0-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="503d0-113">В этой статье мы описываем, как интегрировать модули Runbook службы автоматизации Azure в планы восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="503d0-114">Мы используем простейших задач tooautomate примеры, которые ранее требуется ручное вмешательство.</span><span class="sxs-lookup"><span data-stu-id="503d0-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="503d0-115">Мы также рассматриваются как tooconvert tooa восстановления многоэтапной одним щелчком действия по восстановлению.</span><span class="sxs-lookup"><span data-stu-id="503d0-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="503d0-116">Настройка плана восстановления hello</span><span class="sxs-lookup"><span data-stu-id="503d0-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="503d0-117">Go toohello **Site Recovery** колонки ресурсов для плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="503d0-118">В этом примере hello план восстановления содержит две tooit добавленные виртуальные машины, для восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="503d0-119">Добавление модуля runbook toobegin щелкните hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="503d0-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![При нажатии кнопки настройки hello](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="503d0-121">Щелкните правой кнопкой мыши элемент **Группа 1: запуск**, а затем выберите **Добавить завершающее действие**.</span><span class="sxs-lookup"><span data-stu-id="503d0-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Щелкните правой кнопкой мыши элемент "Группа 1: запуск" и добавьте завершающее действие.](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="503d0-123">Нажмите **Выбрать сценарий**.</span><span class="sxs-lookup"><span data-stu-id="503d0-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="503d0-124">На hello **действие обновления** колонки, сценарий приветствия имен **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="503d0-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![Колонка действие обновления Hello](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="503d0-126">Введите имя учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="503d0-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="503d0-127">Hello учетной записи автоматизации могут находиться в любом регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="503d0-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="503d0-128">Hello учетной записи автоматизации должны находиться в hello той же подписке, хранилище Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="503d0-129">В учетной записи службы автоматизации Azure выберите Runbook.</span><span class="sxs-lookup"><span data-stu-id="503d0-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="503d0-130">Этот runbook — hello сценарий, который выполняется во время выполнения hello hello плана восстановления, после восстановления hello hello первой группы.</span><span class="sxs-lookup"><span data-stu-id="503d0-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="503d0-131">сценарий toosave hello, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="503d0-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="503d0-132">Hello скрипт добавляется слишком**группа 1: после действия**.</span><span class="sxs-lookup"><span data-stu-id="503d0-132">hello script is added too**Group 1: Post-steps**.</span></span>

    !["Группа 1: запуск", последующие действия](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="503d0-134">Рекомендации по добавлению сценария</span><span class="sxs-lookup"><span data-stu-id="503d0-134">Considerations for adding a script</span></span>

* <span data-ttu-id="503d0-135">Для параметров слишком**удалить шаг** или **hello скрипт обновления**, щелкните правой кнопкой мыши сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="503d0-136">Можно запустить сценарий в Azure во время отработки отказа из локальной машины tooAzure.</span><span class="sxs-lookup"><span data-stu-id="503d0-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="503d0-137">Он также может запускать на платформе Azure как сценарий первичный сайт перед завершением работы, при отработке отказа из Azure tooan на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="503d0-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="503d0-138">При запуске сценарий внедряет контекст плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="503d0-139">Следующий пример Hello показана переменная контекста:</span><span class="sxs-lookup"><span data-stu-id="503d0-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="503d0-140">Привет, в следующей таблице перечислены hello имя и описание каждой переменной в контексте hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="503d0-141">**Имя переменной**</span><span class="sxs-lookup"><span data-stu-id="503d0-141">**Variable name**</span></span> | <span data-ttu-id="503d0-142">**Описание**</span><span class="sxs-lookup"><span data-stu-id="503d0-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="503d0-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="503d0-143">RecoveryPlanName</span></span> |<span data-ttu-id="503d0-144">Имя плана hello Hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-144">hello name of hello plan being run.</span></span> <span data-ttu-id="503d0-145">Эта переменная помогает выполнять различные действия на основе имени плана восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="503d0-146">Также можно повторно использовать скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="503d0-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="503d0-147">FailoverType</span></span> |<span data-ttu-id="503d0-148">Указывает, является ли тест hello отработки отказа, плановой или незапланированной.</span><span class="sxs-lookup"><span data-stu-id="503d0-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="503d0-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="503d0-149">FailoverDirection</span></span> |<span data-ttu-id="503d0-150">Указывает, является ли восстановления tooa первичного или вторичного сайта.</span><span class="sxs-lookup"><span data-stu-id="503d0-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="503d0-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="503d0-151">GroupID</span></span> |<span data-ttu-id="503d0-152">Определяет номер группы hello в плане восстановления hello, при выполнении плана hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="503d0-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="503d0-153">VmMap</span></span> |<span data-ttu-id="503d0-154">Массив всех виртуальных машин в группе hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="503d0-155">Ключ VMMap</span><span class="sxs-lookup"><span data-stu-id="503d0-155">VMMap key</span></span> |<span data-ttu-id="503d0-156">Уникальный ключ (GUID) для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="503d0-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="503d0-157">Его hello таким же, как hello Azure Virtual Machine Manager (VMM) идентификатор hello виртуальной Машины, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="503d0-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="503d0-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="503d0-158">SubscriptionId</span></span> |<span data-ttu-id="503d0-159">Идентификатор подписки Azure Hello Здравствуйте виртуальной Машины, в котором был создан.</span><span class="sxs-lookup"><span data-stu-id="503d0-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="503d0-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="503d0-160">RoleName</span></span> |<span data-ttu-id="503d0-161">Имя Hello hello виртуальной Машине Azure, в которой выполняется восстановление.</span><span class="sxs-lookup"><span data-stu-id="503d0-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="503d0-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="503d0-162">CloudServiceName</span></span> |<span data-ttu-id="503d0-163">Hello имя облачной службы Azure Здравствуйте виртуальных Машин, под которой был создан.</span><span class="sxs-lookup"><span data-stu-id="503d0-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="503d0-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="503d0-164">ResourceGroupName</span></span>|<span data-ttu-id="503d0-165">Имя группы ресурсов Azure Hello, под которой hello виртуальной Машины была создана.</span><span class="sxs-lookup"><span data-stu-id="503d0-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="503d0-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="503d0-166">RecoveryPointId</span></span>|<span data-ttu-id="503d0-167">Hello отметка времени при восстановлении hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="503d0-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="503d0-168">Убедитесь, что для этой учетной записи автоматизации hello hello следующие модули:</span><span class="sxs-lookup"><span data-stu-id="503d0-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="503d0-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="503d0-169">AzureRM.profile</span></span>
    * <span data-ttu-id="503d0-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="503d0-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="503d0-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="503d0-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="503d0-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="503d0-172">AzureRM.Network</span></span>
    * <span data-ttu-id="503d0-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="503d0-173">AzureRM.Compute</span></span>

<span data-ttu-id="503d0-174">Все эти модули должны иметь совместимые версии.</span><span class="sxs-lookup"><span data-stu-id="503d0-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="503d0-175">Простой способ tooensure все модули совместимы — toouse hello последние версии всех модулей hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="503d0-176">Доступ к hello VMMap в цикле все виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="503d0-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="503d0-177">Используйте следующие tooloop кода для всех виртуальных машин, hello Microsoft VMMap hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="503d0-178">Hello ресурсов группы и роли значения имени были пустыми, если hello сценария — это группа загрузки tooa перед действием.</span><span class="sxs-lookup"><span data-stu-id="503d0-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="503d0-179">заполняется значениями Hello только в том случае, если переход на другой ресурс успешно hello виртуальной Машины из этой группы.</span><span class="sxs-lookup"><span data-stu-id="503d0-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="503d0-180">сценарий Hello — после действия группы загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="503d0-181">Используйте hello же runbook службы автоматизации в несколько планов восстановления</span><span class="sxs-lookup"><span data-stu-id="503d0-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="503d0-182">Один и тот же сценарий можно использовать в нескольких планах восстановления, передавая ему внешние переменные.</span><span class="sxs-lookup"><span data-stu-id="503d0-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="503d0-183">Можно использовать [переменных службы автоматизации Azure](../automation/automation-variables.md) выполнение плана toostore параметры, которые можно передать для восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="503d0-184">Добавляя имя плана восстановления hello как переменная toohello префикс, можно создать отдельные переменные для каждого плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="503d0-185">Затем с помощью переменных hello в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="503d0-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="503d0-186">Можно изменить параметр без изменения сценария hello, но по-прежнему изменение hello, каким образом hello скрипт работает.</span><span class="sxs-lookup"><span data-stu-id="503d0-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="503d0-187">Использование простых строковых переменных в сценарии Runbook</span><span class="sxs-lookup"><span data-stu-id="503d0-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="503d0-188">В этом примере сценария принимает входные данные hello объекта группы безопасности сети (NSG) и применяет его toohello виртуальные машины плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="503d0-189">Сценарий toodetect hello, используемого плана восстановления выполняется при помощи контекста плана восстановления hello:</span><span class="sxs-lookup"><span data-stu-id="503d0-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="503d0-190">tooapply существующей NSG, необходимо знать имя NSG hello и имя группы ресурсов NSG hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="503d0-191">Используйте эти переменные в качестве входных данных для сценариев плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="503d0-192">toodo это, создайте две переменные hello ресурсы учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="503d0-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="503d0-193">Добавьте имя hello hello плана восстановления, для которого создается как имя переменной toohello префикс параметров hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="503d0-194">Создайте имя переменной toostore hello NSG.</span><span class="sxs-lookup"><span data-stu-id="503d0-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="503d0-195">Добавьте имя переменной toohello префикс с помощью hello имя плана восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Создание переменной для имени NSG](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="503d0-197">Создайте NSG hello переменной toostore имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="503d0-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="503d0-198">Добавьте имя переменной toohello префикс с помощью hello имя плана восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Создание имени группы ресурсов NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="503d0-200">В сценарии hello используйте следующие hello ссылаться на значения переменных hello tooget кода:</span><span class="sxs-lookup"><span data-stu-id="503d0-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="503d0-201">Используйте переменные hello в hello runbook tooapply hello NSG toohello сетевому интерфейсу hello отработка отказа виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="503d0-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="503d0-202">Для каждого плана восстановления создайте независимых переменных, чтобы можно было повторно использовать скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="503d0-203">Добавление префикса с помощью hello имя плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="503d0-204">Полный, конца в конец скрипта для этого сценария см. в разделе [добавить открытый IP-адрес и NSG tooVMs во время тестовой отработки отказа плана восстановления Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="503d0-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="503d0-205">Используйте toostore переменной сложного Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="503d0-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="503d0-206">Рассмотрим ситуацию, в которой будет tooturn один скрипт на общедоступный IP-адрес на конкретных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="503d0-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="503d0-207">В другом сценарии может потребоваться tooapply другой Nsg на разных виртуальных машинах (не на всех виртуальных машинах).</span><span class="sxs-lookup"><span data-stu-id="503d0-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="503d0-208">Такой сценарий можно многократно использовать для других планов восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="503d0-209">Каждый план восстановления может иметь разное число виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="503d0-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="503d0-210">Например, точка восстановления SharePoint имеет два внешних интерфейса,</span><span class="sxs-lookup"><span data-stu-id="503d0-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="503d0-211">а простые бизнес-приложения — только один.</span><span class="sxs-lookup"><span data-stu-id="503d0-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="503d0-212">В такой ситуации мы не можем просто создать отдельные переменные для каждого плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="503d0-213">В следующем примере hello, мы используем новый метод и создать [переменной сложного](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) в ресурсах учетной записи службы автоматизации Azure hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="503d0-214">с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="503d0-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="503d0-215">Необходимо использовать toocomplete hello Azure PowerShell, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="503d0-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="503d0-216">В PowerShell войдите в tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="503d0-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="503d0-217">Параметры toostore hello, создание переменной сложного hello с помощью hello имя плана восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="503d0-218">В этой переменной комплексного **VMDetails** — hello ИД виртуальной Машины, к hello защищенных виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="503d0-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="503d0-219">hello tooget ИД виртуальной Машины в hello портал Azure, просмотреть свойства виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="503d0-220">Hello следующем снимке экрана показана переменная, которая хранит hello сведения о двух других виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="503d0-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Здравствуйте, GUID служит hello ИД виртуальной Машины](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="503d0-222">Используйте эту переменную в модуле runbook.</span><span class="sxs-lookup"><span data-stu-id="503d0-222">Use this variable in your runbook.</span></span> <span data-ttu-id="503d0-223">Если hello указывает, что GUID виртуальной Машины находится в контексте плана восстановления hello, применяются hello NSG на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="503d0-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="503d0-224">В модуле runbook цикла по виртуальным машинам hello контекста плана восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="503d0-225">Проверьте, существует ли hello виртуальной Машины в **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="503d0-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="503d0-226">Если он существует, доступ к свойствам hello hello hello переменной tooapply NSG:</span><span class="sxs-lookup"><span data-stu-id="503d0-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="503d0-227">Hello же скрипт можно использовать для планов восстановления.</span><span class="sxs-lookup"><span data-stu-id="503d0-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="503d0-228">Введите различные параметры, сохраняя значение hello, которое соответствует tooa плана восстановления в различные переменные.</span><span class="sxs-lookup"><span data-stu-id="503d0-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="503d0-229">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="503d0-229">Sample scripts</span></span>

<span data-ttu-id="503d0-230">tooyour скрипты образца toodeploy учетной записи автоматизации, нажмите кнопку hello **развертывание tooAzure** кнопки.</span><span class="sxs-lookup"><span data-stu-id="503d0-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="503d0-231">[![Развертывание tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="503d0-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="503d0-232">Еще один пример см. следующие видео hello.</span><span class="sxs-lookup"><span data-stu-id="503d0-232">For another example, see hello following video.</span></span> <span data-ttu-id="503d0-233">Здесь показано, как toorecover tooAzure двухуровневая WordPress приложения:</span><span class="sxs-lookup"><span data-stu-id="503d0-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="503d0-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="503d0-234">Additional resources</span></span>
* [<span data-ttu-id="503d0-235">Учетная запись запуска от имени службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="503d0-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="503d0-236">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="503d0-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Обзор службы автоматизации Azure")
* [<span data-ttu-id="503d0-237">Примеры сценариев службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="503d0-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Примеры сценариев службы автоматизации Azure")
