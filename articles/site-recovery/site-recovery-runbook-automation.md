---
title: "Добавление модулей Runbook службы автоматизации Azure в планы восстановления в Azure Site Recovery | Документы Майкрософт"
description: "Узнайте, как Azure Site Recovery помогает расширить планы восстановления с помощью службы автоматизации Azure. Узнайте, как выполнять сложные задачи во время восстановления в Azure."
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
ms.openlocfilehash: 064a6782970b950543f93c24800998c1f104c8df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a><span data-ttu-id="5e405-104">Добавление модулей Runbook службы автоматизации Azure в планы восстановления</span><span class="sxs-lookup"><span data-stu-id="5e405-104">Add Azure Automation runbooks to recovery plans</span></span>
<span data-ttu-id="5e405-105">В этой статье описывается, как Azure Site Recovery интегрируется со службой автоматизации Azure для обеспечения расширяемости планов восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation to help you extend your recovery plans.</span></span> <span data-ttu-id="5e405-106">Планы восстановления могут управлять восстановлением виртуальных машин, защищенных с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5e405-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="5e405-107">Планы восстановления подходят как для репликации во вторичное облако, так и для репликации в Azure.</span><span class="sxs-lookup"><span data-stu-id="5e405-107">Recovery plans work both for replication to a secondary cloud, and for replication to Azure.</span></span> <span data-ttu-id="5e405-108">Они также помогают реализовать **точное**, **воспроизводимое** и **автоматическое** восстановление.</span><span class="sxs-lookup"><span data-stu-id="5e405-108">Recovery plans also help make the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="5e405-109">Если выполняется отработка отказа с переносом виртуальных машин в Azure, интеграция со службой автоматизации Azure позволяет расширить планы восстановления</span><span class="sxs-lookup"><span data-stu-id="5e405-109">If you fail over your VMs to Azure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="5e405-110">и предоставляет возможность выполнять Runbook, а это, в свою очередь, позволяет значительно облегчить выполнение задач автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5e405-110">You can use it to execute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="5e405-111">Если вы еще не знакомы со службой автоматизации Azure, зарегистрируйтесь [здесь](https://azure.microsoft.com/services/automation/) и скачайте примеры сценариев [здесь](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="5e405-111">If you are new to Azure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="5e405-112">Дополнительные сведения об Azure Site Recovery и о том, как управлять восстановлением в Azure с помощью [планов восстановления](https://azure.microsoft.com/blog/?p=166264), см. [здесь](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="5e405-112">For more information, and to learn how to orchestrate recovery to Azure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="5e405-113">В этой статье мы описываем, как интегрировать модули Runbook службы автоматизации Azure в планы восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="5e405-114">Мы используем примеры автоматизации простых задач, которые ранее требовалось выполнять вручную,</span><span class="sxs-lookup"><span data-stu-id="5e405-114">We use examples to automate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="5e405-115">и узнаем, как преобразовать многоэтапный процесс восстановления в действие восстановления, запускаемое одним щелчком мыши.</span><span class="sxs-lookup"><span data-stu-id="5e405-115">We also describe how to convert a multi-step recovery to a single-click recovery action.</span></span>

## <a name="customize-the-recovery-plan"></a><span data-ttu-id="5e405-116">Настройка плана восстановления</span><span class="sxs-lookup"><span data-stu-id="5e405-116">Customize the recovery plan</span></span>
1. <span data-ttu-id="5e405-117">Перейдите к колонке ресурсов плана восстановления **Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="5e405-117">Go to the **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="5e405-118">В этом примере в план восстановления добавлено две виртуальные машины для восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-118">For this example, the recovery plan has two VMs added to it, for recovery.</span></span> <span data-ttu-id="5e405-119">Чтобы добавить модуль Runbook, выберите вкладку **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="5e405-119">To begin adding a runbook, click the **Customize** tab.</span></span>

    ![Нажмите кнопку "Настроить"](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="5e405-121">Щелкните правой кнопкой мыши элемент **Группа 1: запуск**, а затем выберите **Добавить завершающее действие**.</span><span class="sxs-lookup"><span data-stu-id="5e405-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Щелкните правой кнопкой мыши элемент "Группа 1: запуск" и добавьте завершающее действие.](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="5e405-123">Нажмите **Выбрать сценарий**.</span><span class="sxs-lookup"><span data-stu-id="5e405-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="5e405-124">В колонке **Действие обновления** присвойте сценарию имя **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="5e405-124">On the **Update action** blade, name the script **Hello World**.</span></span>

    ![Колонка "Действие обновления"](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="5e405-126">Введите имя учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5e405-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="5e405-127">Учетная запись службы автоматизации может находиться в любом географическом регионе Azure,</span><span class="sxs-lookup"><span data-stu-id="5e405-127">The Automation account can be in any Azure region.</span></span> <span data-ttu-id="5e405-128">но должна быть в той же подписке, что и хранилище Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5e405-128">The Automation account must be in the same subscription as the Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="5e405-129">В учетной записи службы автоматизации Azure выберите Runbook.</span><span class="sxs-lookup"><span data-stu-id="5e405-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="5e405-130">Этот модуль Runbook представляет сценарий, который запускается после восстановления первой группы во время выполнения плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-130">This runbook is the script that runs during the execution of the recovery plan, after the recovery of the first group.</span></span>

7. <span data-ttu-id="5e405-131">Нажмите кнопку **ОК**, чтобы сохранить этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="5e405-131">To save the script, click **OK**.</span></span> <span data-ttu-id="5e405-132">Сценарий будет добавлен в группу **Группа 1: последующие действия**.</span><span class="sxs-lookup"><span data-stu-id="5e405-132">The script is added to **Group 1: Post-steps**.</span></span>

    !["Группа 1: запуск", последующие действия](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="5e405-134">Рекомендации по добавлению сценария</span><span class="sxs-lookup"><span data-stu-id="5e405-134">Considerations for adding a script</span></span>

* <span data-ttu-id="5e405-135">Можно щелкнуть сценарий правой кнопкой мыши и выбрать **Удалить шаг** или **Обновить сценарий**.</span><span class="sxs-lookup"><span data-stu-id="5e405-135">For options to **delete a step** or **update the script**, right-click the script.</span></span>
* <span data-ttu-id="5e405-136">Сценарий можно запустить в Azure во время отработки отказа из локальной среды в Azure.</span><span class="sxs-lookup"><span data-stu-id="5e405-136">A script can run on Azure during failover from an on-premises machine to Azure.</span></span> <span data-ttu-id="5e405-137">Кроме того, он может быть запущен в Azure как первичный сценарий перед завершением работы во время восстановления размещения из Azure в локальную среду.</span><span class="sxs-lookup"><span data-stu-id="5e405-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure to an on-premises machine.</span></span>
* <span data-ttu-id="5e405-138">При запуске сценарий внедряет контекст плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="5e405-139">Ниже приведен пример того, как выглядит переменная контекста.</span><span class="sxs-lookup"><span data-stu-id="5e405-139">The following example shows a context variable:</span></span>

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

    <span data-ttu-id="5e405-140">В следующей таблице перечислены имена и описания всех переменных контекста.</span><span class="sxs-lookup"><span data-stu-id="5e405-140">The following table lists the name and description of each variable in the context.</span></span>

    | <span data-ttu-id="5e405-141">**Имя переменной**</span><span class="sxs-lookup"><span data-stu-id="5e405-141">**Variable name**</span></span> | <span data-ttu-id="5e405-142">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5e405-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="5e405-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="5e405-143">RecoveryPlanName</span></span> |<span data-ttu-id="5e405-144">Имя выполняемого плана.</span><span class="sxs-lookup"><span data-stu-id="5e405-144">The name of the plan being run.</span></span> <span data-ttu-id="5e405-145">Эта переменная позволяет выполнять различные действия на основе имени плана восстановления,</span><span class="sxs-lookup"><span data-stu-id="5e405-145">This variable helps you take different actions based on the recovery plan name.</span></span> <span data-ttu-id="5e405-146">повторно используя сценарий.</span><span class="sxs-lookup"><span data-stu-id="5e405-146">You also can reuse the script.</span></span> |
    | <span data-ttu-id="5e405-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="5e405-147">FailoverType</span></span> |<span data-ttu-id="5e405-148">Указывает, является ли выполнение тестовым, запланированным или незапланированным.</span><span class="sxs-lookup"><span data-stu-id="5e405-148">Specifies whether the failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="5e405-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="5e405-149">FailoverDirection</span></span> |<span data-ttu-id="5e405-150">Указывает, производится ли восстановление на первичный или вторичный сайт.</span><span class="sxs-lookup"><span data-stu-id="5e405-150">Specifies whether recovery is to a primary or secondary site.</span></span> |
    | <span data-ttu-id="5e405-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="5e405-151">GroupID</span></span> |<span data-ttu-id="5e405-152">Определяет номер группы в плане восстановления при выполнении плана.</span><span class="sxs-lookup"><span data-stu-id="5e405-152">Identifies the group number in the recovery plan when the plan is running.</span></span> |
    | <span data-ttu-id="5e405-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="5e405-153">VmMap</span></span> |<span data-ttu-id="5e405-154">Массив всех виртуальных машин в группе.</span><span class="sxs-lookup"><span data-stu-id="5e405-154">An array of all VMs in the group.</span></span> |
    | <span data-ttu-id="5e405-155">Ключ VMMap</span><span class="sxs-lookup"><span data-stu-id="5e405-155">VMMap key</span></span> |<span data-ttu-id="5e405-156">Уникальный ключ (GUID) для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5e405-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="5e405-157">Это то же самое, что и VMM ID виртуальной машины, там, где это применимо.</span><span class="sxs-lookup"><span data-stu-id="5e405-157">It's the same as the Azure Virtual Machine Manager (VMM) ID of the VM, where applicable.</span></span> |
    | <span data-ttu-id="5e405-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="5e405-158">SubscriptionId</span></span> |<span data-ttu-id="5e405-159">Идентификатор подписки Azure, в которой создана виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="5e405-159">The Azure subscription ID in which the VM was created.</span></span> |
    | <span data-ttu-id="5e405-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="5e405-160">RoleName</span></span> |<span data-ttu-id="5e405-161">Имя виртуальной машины Azure, для которой выполняется восстановление.</span><span class="sxs-lookup"><span data-stu-id="5e405-161">The name of the Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="5e405-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="5e405-162">CloudServiceName</span></span> |<span data-ttu-id="5e405-163">Имя облачной службы Azure, в которой создана виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="5e405-163">The Azure cloud service name under which the VM was created.</span></span> |
    | <span data-ttu-id="5e405-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5e405-164">ResourceGroupName</span></span>|<span data-ttu-id="5e405-165">Имя группы ресурсов Azure, в которой создана виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="5e405-165">The Azure resource group name under which the VM was created.</span></span> |
    | <span data-ttu-id="5e405-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="5e405-166">RecoveryPointId</span></span>|<span data-ttu-id="5e405-167">Отметка времени восстановления виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5e405-167">The timestamp for when the VM is recovered.</span></span> |

* <span data-ttu-id="5e405-168">Убедитесь, что в учетную запись службы автоматизации добавлены следующие модули.</span><span class="sxs-lookup"><span data-stu-id="5e405-168">Ensure that the Automation account has the following modules:</span></span>
    * <span data-ttu-id="5e405-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="5e405-169">AzureRM.profile</span></span>
    * <span data-ttu-id="5e405-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="5e405-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="5e405-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="5e405-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="5e405-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="5e405-172">AzureRM.Network</span></span>
    * <span data-ttu-id="5e405-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="5e405-173">AzureRM.Compute</span></span>

<span data-ttu-id="5e405-174">Все эти модули должны иметь совместимые версии.</span><span class="sxs-lookup"><span data-stu-id="5e405-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="5e405-175">Чтобы обеспечить это, проще всего брать все модули из последней доступной версии.</span><span class="sxs-lookup"><span data-stu-id="5e405-175">An easy way to ensure that all modules are compatible is to use the latest versions of all the modules.</span></span>

### <a name="access-all-vms-of-the-vmmap-in-a-loop"></a><span data-ttu-id="5e405-176">Доступ ко всем виртуальным машинам VMMap в цикле</span><span class="sxs-lookup"><span data-stu-id="5e405-176">Access all VMs of the VMMap in a loop</span></span>
<span data-ttu-id="5e405-177">Используйте следующий фрагмент кода, чтобы в цикле перебрать все виртуальные машины VMMap.</span><span class="sxs-lookup"><span data-stu-id="5e405-177">Use the following code to loop across all VMs of the Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is to ensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="5e405-178">Когда сценарий используется как предварительное действие для групп загрузки, значения для имени группы ресурсов и имени роли не установлены.</span><span class="sxs-lookup"><span data-stu-id="5e405-178">The resource group name and role name values are empty when the script is a pre-action to a boot group.</span></span> <span data-ttu-id="5e405-179">Эти значения заполняются, только если виртуальная машина из этой группы успешно прошла отработку отказа,</span><span class="sxs-lookup"><span data-stu-id="5e405-179">The values are populated only if the VM of that group succeeds in failover.</span></span> <span data-ttu-id="5e405-180">а сценарий выполняется как последующее действие в группе загрузки.</span><span class="sxs-lookup"><span data-stu-id="5e405-180">The script is a post-action of the boot group.</span></span>

## <a name="use-the-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="5e405-181">Использование одного модуля Runbook службы автоматизации в нескольких планах восстановления</span><span class="sxs-lookup"><span data-stu-id="5e405-181">Use the same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="5e405-182">Один и тот же сценарий можно использовать в нескольких планах восстановления, передавая ему внешние переменные.</span><span class="sxs-lookup"><span data-stu-id="5e405-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="5e405-183">[Переменные службы автоматизации Azure](../automation/automation-variables.md) можно использовать для хранения параметров, которые передаются для выполнения плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-183">You can use [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="5e405-184">Если перед именем переменной вы укажете имя плана восстановления, для каждого плана восстановления будут созданы собственные переменные,</span><span class="sxs-lookup"><span data-stu-id="5e405-184">By adding the recovery plan name as a prefix to the variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="5e405-185">которые можно использовать в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="5e405-185">Then, use the variables as parameters.</span></span> <span data-ttu-id="5e405-186">Эти параметры можно изменять, чтобы управлять работой скрипта, не изменяя его содержимое, однако принцип работы сценария будет изменен.</span><span class="sxs-lookup"><span data-stu-id="5e405-186">You can change a parameter without changing the script, but still change the way the script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="5e405-187">Использование простых строковых переменных в сценарии Runbook</span><span class="sxs-lookup"><span data-stu-id="5e405-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="5e405-188">Рассмотрим сценарий, который принимает входные данные группы безопасности сети (NSG) и применяет их к виртуальным машинам в плане восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-188">In this example, a script takes the input of a Network Security Group (NSG) and applies it to the VMs of a recovery plan.</span></span>

<span data-ttu-id="5e405-189">Чтобы определить для сценария текущий выполняемый план восстановления, используйте контекст плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-189">For the script to detect which recovery plan is running, use the recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="5e405-190">Чтобы применить существующую группу NSG, нужно знать имя NSG и имя группы ресурсов NSG.</span><span class="sxs-lookup"><span data-stu-id="5e405-190">To apply an existing NSG, you must know the NSG name and the NSG resource group name.</span></span> <span data-ttu-id="5e405-191">Используйте эти переменные в качестве входных данных для сценариев плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="5e405-192">Для этого создайте две переменные в ресурсах учетной записи службы автоматизации,</span><span class="sxs-lookup"><span data-stu-id="5e405-192">To do this, create two variables in the Automation account assets.</span></span> <span data-ttu-id="5e405-193">указав в качестве префикса в имени переменной имя плана восстановления, для которого вы создаете параметры.</span><span class="sxs-lookup"><span data-stu-id="5e405-193">Add the name of the recovery plan that you are creating the parameters for as a prefix to the variable name.</span></span>

1. <span data-ttu-id="5e405-194">Создайте переменную для хранения имени NSG.</span><span class="sxs-lookup"><span data-stu-id="5e405-194">Create a variable to store the NSG name.</span></span> <span data-ttu-id="5e405-195">В качестве префикса добавьте перед ней имя плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-195">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Создание переменной для имени NSG](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="5e405-197">Создайте переменную для хранения имени группы ресурсов NSG.</span><span class="sxs-lookup"><span data-stu-id="5e405-197">Create a variable to store the NSG's resource group name.</span></span> <span data-ttu-id="5e405-198">В качестве префикса добавьте перед ней имя плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-198">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![Создание имени группы ресурсов NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="5e405-200">В сценарии извлеките значения этих переменных, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="5e405-200">In the script, use the following reference code to get the variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="5e405-201">Используйте переменные в модуле Runbook, что позволит применить NSG к сетевому интерфейсу виртуальной машины, для которой выполняется отработка отказа.</span><span class="sxs-lookup"><span data-stu-id="5e405-201">Use the variables in the runbook to apply the NSG to the network interface of the failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply the NSG to a network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="5e405-202">Для каждого плана восстановления создайте независимые переменные, чтобы скрипт можно было использовать повторно.</span><span class="sxs-lookup"><span data-stu-id="5e405-202">For each recovery plan, create independent variables so that you can reuse the script.</span></span> <span data-ttu-id="5e405-203">Перед именами переменных добавьте имя плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-203">Add a prefix by using the recovery plan name.</span></span> <span data-ttu-id="5e405-204">Полный сценарий, описанный в этом примере, см. в разделе [Добавление общедоступного IP-адреса и NSG на виртуальные машины во время тестовой отработки отказа плана восстановления Azure Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="5e405-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-to-store-more-information"></a><span data-ttu-id="5e405-205">Использование сложной переменной для хранения дополнительных сведений</span><span class="sxs-lookup"><span data-stu-id="5e405-205">Use a complex variable to store more information</span></span>

<span data-ttu-id="5e405-206">Рассмотрим ситуацию, когда один сценарий должен включать общедоступный IP-адрес на определенных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="5e405-206">Consider a scenario in which you want a single script to turn on a public IP on specific VMs.</span></span> <span data-ttu-id="5e405-207">Этот же подход будет полезен, если нужно применить разные группы безопасности сети для нескольких (но не всех) виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5e405-207">In another scenario, you might want to apply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="5e405-208">Такой сценарий можно многократно использовать для других планов восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="5e405-209">Каждый план восстановления может иметь разное число виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5e405-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="5e405-210">Например, точка восстановления SharePoint имеет два внешних интерфейса,</span><span class="sxs-lookup"><span data-stu-id="5e405-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="5e405-211">а простые бизнес-приложения — только один.</span><span class="sxs-lookup"><span data-stu-id="5e405-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="5e405-212">В такой ситуации мы не можем просто создать отдельные переменные для каждого плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="5e405-213">В следующем примере мы применим другую методику, создав в ресурсах учетной записи службы автоматизации Azure [сложную переменную](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396)</span><span class="sxs-lookup"><span data-stu-id="5e405-213">In the following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets.</span></span> <span data-ttu-id="5e405-214">с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="5e405-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="5e405-215">Для выполнения следующих действий потребуется Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e405-215">You must use Azure PowerShell to complete the following steps:</span></span>

1. <span data-ttu-id="5e405-216">Используя PowerShell, войдите в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="5e405-216">In PowerShell, sign in to your Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="5e405-217">Создайте сложную переменную для хранения параметров, присвоив ей имя плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-217">To store the parameters, create the complex variable by using the name of the recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="5e405-218">В этой сложной переменной параметр **VMDetails** содержит идентификатор защищенной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5e405-218">In this complex variable, **VMDetails** is the VM ID for the protected VM.</span></span> <span data-ttu-id="5e405-219">Этот идентификатор указан в свойствах виртуальной машины на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5e405-219">To get the VM ID, in the Azure portal, view the VM properties.</span></span> <span data-ttu-id="5e405-220">На снимке экрана ниже показано, что мы создали переменную для хранения сведений о двух виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="5e405-220">The following screenshot shows a variable that stores the details of two VMs:</span></span>

    ![Используйте идентификатор виртуальной машины в качестве идентификатора GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="5e405-222">Используйте эту переменную в модуле runbook.</span><span class="sxs-lookup"><span data-stu-id="5e405-222">Use this variable in your runbook.</span></span> <span data-ttu-id="5e405-223">Если указанный GUID виртуальной машины находится в контексте плана восстановления, примените группу NSG к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="5e405-223">If the indicated VM GUID is found in the recovery plan context, apply the NSG on the VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="5e405-224">В модуле Runbook выполните циклический перебор виртуальных машин, входящих в контекст плана восстановления,</span><span class="sxs-lookup"><span data-stu-id="5e405-224">In your runbook, loop through the VMs of the recovery plan context.</span></span> <span data-ttu-id="5e405-225">проверяя наличие этих виртуальных машин в **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="5e405-225">Check whether the VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="5e405-226">Если встречается совпадение, примените группу NSG, используя свойства переменной.</span><span class="sxs-lookup"><span data-stu-id="5e405-226">If it exists, access the properties of the variable to apply the NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If the VM exists in the context, this will not b Null
                $VM = $vmMap.$VMID
                # Access the properties of the variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code to apply the NSG properties to the VM
            }
        }
    ```

<span data-ttu-id="5e405-227">Этот же сценарий можно использовать с разными планами восстановления,</span><span class="sxs-lookup"><span data-stu-id="5e405-227">You can use the same script for different recovery plans.</span></span> <span data-ttu-id="5e405-228">сохраняя в разных переменных значения параметров, применимых для соответствующих планов восстановления.</span><span class="sxs-lookup"><span data-stu-id="5e405-228">Enter different parameters by storing the value that corresponds to a recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="5e405-229">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="5e405-229">Sample scripts</span></span>

<span data-ttu-id="5e405-230">Разверните примеры сценариев в учетной записи службы автоматизации с помощью кнопки **Развертывание в Azure**.</span><span class="sxs-lookup"><span data-stu-id="5e405-230">To deploy sample scripts to your Automation account, click the **Deploy to Azure** button.</span></span>

<span data-ttu-id="5e405-231">[![Развертывание в Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="5e405-231">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="5e405-232">Просмотрите следующее видео, чтобы ознакомиться с другим примером,</span><span class="sxs-lookup"><span data-stu-id="5e405-232">For another example, see the following video.</span></span> <span data-ttu-id="5e405-233">в котором показано, как выполнить восстановление двухуровневого приложения WordPress в Azure.</span><span class="sxs-lookup"><span data-stu-id="5e405-233">It demonstrates how to recover a two-tier WordPress application to Azure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="5e405-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5e405-234">Additional resources</span></span>
* [<span data-ttu-id="5e405-235">Учетная запись запуска от имени службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5e405-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="5e405-236">Обзор службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5e405-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Обзор службы автоматизации Azure")
* [<span data-ttu-id="5e405-237">Примеры сценариев службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="5e405-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Примеры сценариев службы автоматизации Azure")
