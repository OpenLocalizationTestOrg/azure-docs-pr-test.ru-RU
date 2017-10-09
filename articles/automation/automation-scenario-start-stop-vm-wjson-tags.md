---
title: "aaaUse состояние виртуальной Машины Azure формата JSON теги tooschedule | Документы Microsoft"
description: "В этой статье показано, каким образом строки toouse JSON на теги tooautomate hello планирование включения и выключения виртуальной Машины."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="21860-103">Сценария автоматизации Azure: с помощью формата JSON теги toocreate расписание для включения и выключения виртуальной Машины Azure</span><span class="sxs-lookup"><span data-stu-id="21860-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="21860-104">Часто возникает необходимость запуска tooschedule hello и завершение работы виртуальных машин toohelp снизить затраты на подписку или поддержки коммерческих и технических требований.</span><span class="sxs-lookup"><span data-stu-id="21860-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="21860-105">Hello следующий сценарий позволяет tooset автоматического запуска и завершения работы виртуальных машин с помощью тега "Расписание" на уровне группы ресурсов или уровне виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="21860-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="21860-106">Это расписание можно настроить из tooSaturday воскресенье с временем запуска и время завершения работы.</span><span class="sxs-lookup"><span data-stu-id="21860-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="21860-107">Для реализации этой возможности используются некоторые готовые функции.</span><span class="sxs-lookup"><span data-stu-id="21860-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="21860-108">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="21860-108">These include:</span></span>

* <span data-ttu-id="21860-109">[Наборы масштабирования виртуальных машин](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) с параметрами автоматического масштабирования, позволяющие tooscale in или out.</span><span class="sxs-lookup"><span data-stu-id="21860-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="21860-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) службу, которая имеет встроенные возможности hello планирования операций запуска и завершения работы.</span><span class="sxs-lookup"><span data-stu-id="21860-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="21860-111">Однако эти параметры поддерживают только конкретных сценариев и не может быть применен tooinfrastructure как услуга (IaaS) виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="21860-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="21860-112">Hello тег расписания применяются tooa группы ресурсов, открывается также примененных tooall виртуальных машин в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="21860-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="21860-113">Если расписание также непосредственно примененных tooa виртуальной Машины, последнего расписания hello приоритет в hello следующий порядок:</span><span class="sxs-lookup"><span data-stu-id="21860-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="21860-114">Группа ресурсов примененных tooa расписания</span><span class="sxs-lookup"><span data-stu-id="21860-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="21860-115">Расписание применяется tooa группы ресурсов и виртуальной машины в группе ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="21860-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="21860-116">Расписание применения tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="21860-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="21860-117">Этот сценарий по существу принимает строку в указанном формате JSON и добавляет его как значение hello для тега "Расписание".</span><span class="sxs-lookup"><span data-stu-id="21860-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="21860-118">Затем runbook список всех групп ресурсов и виртуальных машин и определяет hello расписания для каждой виртуальной Машины на основе сценариев hello, перечисленных выше.</span><span class="sxs-lookup"><span data-stu-id="21860-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="21860-119">Затем просматривает hello виртуальных машин, которые имеют расписания, связанные и оценивает, какое действие должно выполняться.</span><span class="sxs-lookup"><span data-stu-id="21860-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="21860-120">Например он определяет, какие виртуальные машины должны toobe остановлена, завершение работы или игнорируются.</span><span class="sxs-lookup"><span data-stu-id="21860-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="21860-121">Эти модули Runbook для проверки подлинности с помощью hello [учетная запись запуска от имени Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="21860-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="21860-122">Скачать Runbook hello для сценария hello</span><span class="sxs-lookup"><span data-stu-id="21860-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="21860-123">Этот сценарий состоит из четырех Runbook рабочего процесса PowerShell, которые можно загрузить из hello [коллекции TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) или hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) репозитория для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="21860-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="21860-124">Модуль Runbook</span><span class="sxs-lookup"><span data-stu-id="21860-124">Runbook</span></span> | <span data-ttu-id="21860-125">Описание</span><span class="sxs-lookup"><span data-stu-id="21860-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21860-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="21860-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="21860-127">Проверяет каждое расписание виртуальной машины и выполняет завершения работы или запуска, в зависимости от расписания hello.</span><span class="sxs-lookup"><span data-stu-id="21860-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="21860-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="21860-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="21860-129">Добавляет hello расписание тег tooa виртуальной Машины или группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="21860-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="21860-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="21860-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="21860-131">Изменяет существующий тег расписание hello, заменив его новым.</span><span class="sxs-lookup"><span data-stu-id="21860-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="21860-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="21860-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="21860-133">Удаляет расписание тег hello из виртуальной Машины или группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="21860-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="21860-134">Установка и настройка сценария</span><span class="sxs-lookup"><span data-stu-id="21860-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="21860-135">Установка и публикации Runbook hello</span><span class="sxs-lookup"><span data-stu-id="21860-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="21860-136">После загрузки hello модулей Runbook, можно импортировать их с помощью процедуры hello в [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="21860-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="21860-137">Опубликуйте каждый модуль Runbook после импорта в учетную запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="21860-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="21860-138">Добавить расписание toohello ResourceSchedule теста runbook</span><span class="sxs-lookup"><span data-stu-id="21860-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="21860-139">Выполните эти шаги tooenable hello расписание hello ResourceSchedule тестирования runbook.</span><span class="sxs-lookup"><span data-stu-id="21860-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="21860-140">Это hello runbook, который проверяет, какие виртуальные машины должна быть запущена, выключена, или влево, как есть.</span><span class="sxs-lookup"><span data-stu-id="21860-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="21860-141">Из hello портал Azure, откройте учетную запись автоматизации и нажмите кнопку hello **Runbooks** плитки.</span><span class="sxs-lookup"><span data-stu-id="21860-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="21860-142">На hello **теста ResourceSchedule** колонка, щелкните hello **расписания** плитки.</span><span class="sxs-lookup"><span data-stu-id="21860-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="21860-143">На hello **расписания** колонка, щелкните **Добавить расписание**.</span><span class="sxs-lookup"><span data-stu-id="21860-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="21860-144">На hello **расписания** колонке выберите **связать runbook расписания tooyour**.</span><span class="sxs-lookup"><span data-stu-id="21860-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="21860-145">а затем — **Создать новое расписание**.</span><span class="sxs-lookup"><span data-stu-id="21860-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="21860-146">На hello **новое расписание** колонки, введите имя hello этого расписания, например: *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="21860-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="21860-147">Для расписания hello **запустить**, задайте увеличение час tooan времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="21860-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="21860-148">Выберите **Повторение** и для интервала **Повторять кажд.** выберите значение **1 час**.</span><span class="sxs-lookup"><span data-stu-id="21860-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="21860-149">Убедитесь, что **срок действия набора** задано слишком**нет**, а затем нажмите кнопку **создать** toosave новое расписание.</span><span class="sxs-lookup"><span data-stu-id="21860-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="21860-150">На hello **Runbook расписания** параметры колонке выберите **параметры и настройки запуска**.</span><span class="sxs-lookup"><span data-stu-id="21860-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="21860-151">В hello теста ResourceSchedule **параметры** колонки, введите имя подписки hello в hello **Имя_подписки** поля.</span><span class="sxs-lookup"><span data-stu-id="21860-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="21860-152">Это единственный параметр hello, требуемое для hello runbook.</span><span class="sxs-lookup"><span data-stu-id="21860-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="21860-153">Закончив, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21860-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="21860-154">После завершения Hello согласно расписанию runbook должен выглядеть hello следующее:</span><span class="sxs-lookup"><span data-stu-id="21860-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Настроенный модуль Runbook Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="21860-156">Формат hello строки JSON</span><span class="sxs-lookup"><span data-stu-id="21860-156">Format hello JSON string</span></span>
<span data-ttu-id="21860-157">Это решение по сути принимает строку в указанном формате JSON и добавляет его как значение hello для тега "Расписание".</span><span class="sxs-lookup"><span data-stu-id="21860-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="21860-158">Затем runbook список всех групп ресурсов и виртуальных машин и определяет hello расписания для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="21860-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="21860-159">Hello runbook обрабатывает в цикле hello виртуальных машин, имеющих расписания, связанные и проверяет, какие действия необходимы.</span><span class="sxs-lookup"><span data-stu-id="21860-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="21860-160">Hello ниже приведен пример форматирования hello решения:</span><span class="sxs-lookup"><span data-stu-id="21860-160">hello following is an example of how hello solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="21860-161">Вот подробные сведения об этой структуре:</span><span class="sxs-lookup"><span data-stu-id="21860-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="21860-162">Формат Hello этой структуры JSON — оптимизированный toowork обойти ограничение до 256 символов hello значения одного тега в Azure.</span><span class="sxs-lookup"><span data-stu-id="21860-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="21860-163">*TzId* представляет hello часового пояса hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="21860-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="21860-164">Этот идентификатор можно получить с помощью класса TimeZoneInfo .NET hello в сеансе PowerShell--**[System.TimeZoneInfo]:: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="21860-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones в PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="21860-166">Дни недели, представлены с числовым значением нуль toosix.</span><span class="sxs-lookup"><span data-stu-id="21860-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="21860-167">нулевое значение Hello равняется воскресенье.</span><span class="sxs-lookup"><span data-stu-id="21860-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="21860-168">Hello время начала представляется с hello **S** атрибут и его значение находится в 24-часовом формате.</span><span class="sxs-lookup"><span data-stu-id="21860-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="21860-169">Hello времени завершения или завершения работы представляется с hello **E** атрибут и его значение находится в 24-часовом формате.</span><span class="sxs-lookup"><span data-stu-id="21860-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="21860-170">Если hello **S** и **E** атрибуты каждого иметь значение нуль (0), hello виртуальной машины остается в текущем состоянии во время hello оценки.</span><span class="sxs-lookup"><span data-stu-id="21860-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="21860-171">Если требуется tooskip оценки для определенного дня недели hello не добавить раздел в тот же день недели hello.</span><span class="sxs-lookup"><span data-stu-id="21860-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="21860-172">В hello вычисляется следующий пример, только понедельник и hello остальные дни недели hello игнорируются:</span><span class="sxs-lookup"><span data-stu-id="21860-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="21860-173">Добавление тегов для групп ресурсов или виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="21860-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="21860-174">tooshut работу виртуальных машин необходимо tootag hello виртуальных машин или hello групп ресурсов, в которых они расположены.</span><span class="sxs-lookup"><span data-stu-id="21860-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="21860-175">Виртуальные машины, у которых нет тега Schedule, не проверяются.</span><span class="sxs-lookup"><span data-stu-id="21860-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="21860-176">По этой причине их запуск или завершение их работы не выполняется.</span><span class="sxs-lookup"><span data-stu-id="21860-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="21860-177">Существуют два способа tootag ресурсов группы или виртуальные машины с данным решением.</span><span class="sxs-lookup"><span data-stu-id="21860-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="21860-178">Его можно сделать непосредственно с портала hello.</span><span class="sxs-lookup"><span data-stu-id="21860-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="21860-179">Или можно использовать hello ResourceSchedule добавить, ResourceSchedule обновление и удаление ResourceSchedule модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="21860-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="21860-180">Тег через портал hello</span><span class="sxs-lookup"><span data-stu-id="21860-180">Tag through hello portal</span></span>
<span data-ttu-id="21860-181">Выполните эти шаги tootag виртуальной машины или группы ресурсов на портале hello.</span><span class="sxs-lookup"><span data-stu-id="21860-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="21860-182">Сведение строку hello JSON и убедитесь, что не все пробелы.</span><span class="sxs-lookup"><span data-stu-id="21860-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="21860-183">Строка JSON должна выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="21860-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="21860-184">Выберите hello **тега** значок для виртуальной Машины или ресурсов группы tooapply этого расписания.</span><span class="sxs-lookup"><span data-stu-id="21860-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![Параметр тега виртуальной машины](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="21860-186">Теги определяются следующей парой "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="21860-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="21860-187">Тип **расписания** в hello **ключ** поле, а затем вставьте строку JSON hello в hello **значение** поле.</span><span class="sxs-lookup"><span data-stu-id="21860-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="21860-188">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="21860-188">Click **Save**.</span></span> <span data-ttu-id="21860-189">Ваш новый тег должен появиться в списке hello тегов для ресурса.</span><span class="sxs-lookup"><span data-stu-id="21860-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![Тег Schedule виртуальной машины](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="21860-191">Добавление тега из PowerShell</span><span class="sxs-lookup"><span data-stu-id="21860-191">Tag from PowerShell</span></span>
<span data-ttu-id="21860-192">Все импортированные модули Runbook содержат справочные сведения в начале hello hello скрипт, который описывает, каким образом tooexecute hello Runbook непосредственно из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21860-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="21860-193">Модули Runbook ScheduleResource Установка и обновление ScheduleResource hello можно вызвать из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21860-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="21860-194">Это делается путем передачи обязательные параметры, позволяющие тег расписание hello toocreate или обновление виртуальной Машины или группа ресурсов за пределами портала hello.</span><span class="sxs-lookup"><span data-stu-id="21860-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="21860-195">toocreate, добавление и удаление тегов с помощью PowerShell, необходимо сначала слишком[настройки среды PowerShell для Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="21860-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="21860-196">После завершения установки hello, можно продолжить hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="21860-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="21860-197">Создание тега Schedule с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="21860-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="21860-198">Откройте сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21860-198">Open a PowerShell session.</span></span> <span data-ttu-id="21860-199">Затем используйте следующий пример tooauthenticate, используя учетную запись запуска от имени и toospecify подписки hello:</span><span class="sxs-lookup"><span data-stu-id="21860-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="21860-200">Определите хэш-таблицу расписания.</span><span class="sxs-lookup"><span data-stu-id="21860-200">Define a schedule hash table.</span></span> <span data-ttu-id="21860-201">Ниже приведен пример ее структуры.</span><span class="sxs-lookup"><span data-stu-id="21860-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="21860-202">Определите параметры hello, необходимых для hello runbook.</span><span class="sxs-lookup"><span data-stu-id="21860-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="21860-203">В следующем примере hello мы ожидаем виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="21860-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="21860-204">Если добавление тегов в группе ресурсов, удалите hello *VMName* параметр из хэша hello $params таблицы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="21860-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="21860-205">Выполните hello добавить ResourceSchedule runbook с hello после тега расписание hello toocreate параметры:</span><span class="sxs-lookup"><span data-stu-id="21860-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="21860-206">tooupdate тег виртуальной машины или группы ресурсов, выполните hello **ResourceSchedule обновление** runbook с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="21860-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="21860-207">Удаление тега Schedule с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="21860-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="21860-208">Откройте сеанс PowerShell и выполните следующие tooauthenticate, используя учетную запись запуска от имени и tooselect hello и укажите подписку.</span><span class="sxs-lookup"><span data-stu-id="21860-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="21860-209">Определите параметры hello, необходимых для hello runbook.</span><span class="sxs-lookup"><span data-stu-id="21860-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="21860-210">В следующем примере hello мы ожидаем виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="21860-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="21860-211">При удалении тег из группы ресурсов, удалите hello *VMName* параметр из хэша hello $params таблицы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="21860-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="21860-212">Выполнение расписания hello Remove ResourceSchedule runbook tooremove hello тег:</span><span class="sxs-lookup"><span data-stu-id="21860-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="21860-213">tooupdate тег виртуальной машины или группы ресурсов, выполнить hello Remove ResourceSchedule runbook с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="21860-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="21860-214">Рекомендуется заранее отслеживать эти модули Runbook (и hello состояния виртуальных машин) tooverify, виртуальных машин выполняется завершение работы и работы соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="21860-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="21860-215">Подробности hello tooview hello ResourceSchedule тестирования модуля Runbook задания в hello портал Azure, выберите hello **заданий** плитки приветствия runbook.</span><span class="sxs-lookup"><span data-stu-id="21860-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="21860-216">Hello задания сводки Вывод hello входных параметров и вывода hello потока, кроме toogeneral сведения о задании hello и любые исключения, если они имели место.</span><span class="sxs-lookup"><span data-stu-id="21860-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="21860-217">Hello **Сводка заданий** включает в себя сообщения из hello потоков вывода, предупреждения и ошибки.</span><span class="sxs-lookup"><span data-stu-id="21860-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="21860-218">Выберите hello **вывода** плитки tooview подробные результаты из выполнения runbook hello.</span><span class="sxs-lookup"><span data-stu-id="21860-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Выходные данные Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="21860-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21860-220">Next steps</span></span>
* <span data-ttu-id="21860-221">tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый рабочий процесс runbook PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="21860-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="21860-222">в разделе toolearn Дополнительные сведения о типах runbook и их преимущества и ограничения, [типов runbook службы автоматизации Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="21860-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="21860-223">Дополнительные сведения о функции поддержки сценариев PowerShell см. в публикации блога [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Поддержка собственных сценариев PowerShell в службе автоматизации Azure).</span><span class="sxs-lookup"><span data-stu-id="21860-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="21860-224">toolearn Дополнительные сведения о ведение журнала runbook и выходные данные, в разделе [Runbook выходные данные и сообщения в службе автоматизации Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="21860-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="21860-225">Дополнительные сведения об учетной записи запуска от имени Azure и как tooauthenticate модули Runbook с помощью, см. статью toolearn [проверки подлинности модулей Runbook с помощью учетной записи запуска от имени Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="21860-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
