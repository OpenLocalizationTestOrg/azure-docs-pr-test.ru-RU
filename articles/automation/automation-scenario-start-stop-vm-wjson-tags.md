---
title: "Использование тегов в формате JSON для планирования состояния виртуальной машины Azure | Документация Майкрософт"
description: "В этой статье демонстрируется использование строк JSON в тегах для автоматизации планирования запуска и завершения работы виртуальной машины."
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
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="b891e-103">Сценарий службы автоматизации Azure: создание расписания запуска и завершения работы виртуальной машины Azure с помощью тегов в формате JSON</span><span class="sxs-lookup"><span data-stu-id="b891e-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="b891e-104">Часто клиентам необходимо планировать запуск и завершение работы виртуальных машин, чтобы уменьшить затраты на подписку или соблюсти деловые и технические требования.</span><span class="sxs-lookup"><span data-stu-id="b891e-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="b891e-105">Приведенный ниже сценарий позволяет настроить автоматические запуск и завершение работы виртуальных машин, используя тег Schedule на уровне группы ресурсов или виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="b891e-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="b891e-106">Это расписание можно настроить с воскресенья по субботу с указанием времени запуска и времени завершения работы.</span><span class="sxs-lookup"><span data-stu-id="b891e-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="b891e-107">Для реализации этой возможности используются некоторые готовые функции.</span><span class="sxs-lookup"><span data-stu-id="b891e-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="b891e-108">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="b891e-108">These include:</span></span>

* <span data-ttu-id="b891e-109">[наборы масштабирования виртуальных машин](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) с параметрами автомасштабирования, которые позволяют увеличивать или уменьшать масштаб;</span><span class="sxs-lookup"><span data-stu-id="b891e-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="b891e-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) со встроенными возможностями планирования операций запуска и завершения работы.</span><span class="sxs-lookup"><span data-stu-id="b891e-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="b891e-111">Эти функции подходят только для определенных сценариев и не могут использоваться для виртуальных машин IaaS.</span><span class="sxs-lookup"><span data-stu-id="b891e-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="b891e-112">Если тег Schedule применяется к группе ресурсов, то он также будет применен ко всем виртуальным машинам в ней.</span><span class="sxs-lookup"><span data-stu-id="b891e-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="b891e-113">Если же непосредственно к виртуальной машине применяется другое расписание, то приоритетность расписаний устанавливается в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="b891e-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="b891e-114">расписание, примененное к группе ресурсов;</span><span class="sxs-lookup"><span data-stu-id="b891e-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="b891e-115">расписание, примененное к группе ресурсов и виртуальной машине в этой группе ресурсов;</span><span class="sxs-lookup"><span data-stu-id="b891e-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="b891e-116">расписание, примененное к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="b891e-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="b891e-117">Этот сценарий фактически принимает строку JSON в указанном формате и добавляет ее в качестве значения для тега Schedule.</span><span class="sxs-lookup"><span data-stu-id="b891e-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="b891e-118">Затем модуль Runbook получает список всех групп ресурсов и виртуальных машин и определяет расписание для каждой виртуальной машины на основе указанных выше сценариев.</span><span class="sxs-lookup"><span data-stu-id="b891e-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="b891e-119">После этого он перебирает виртуальные машины по заданным расписаниям и оценивает действие, которое должно быть выполнено:</span><span class="sxs-lookup"><span data-stu-id="b891e-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="b891e-120">остановка, завершение работы либо пропуск действия.</span><span class="sxs-lookup"><span data-stu-id="b891e-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="b891e-121">Эти модули Runbook выполняют аутентификацию с помощью [учетной записи запуска от имени Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="b891e-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="b891e-122">Скачивание модулей Runbook для сценария</span><span class="sxs-lookup"><span data-stu-id="b891e-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="b891e-123">Сценарий состоит из четырех модулей Runbook рабочего процесса PowerShell, которые можно скачать из [коллекции TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) или репозитория [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="b891e-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="b891e-124">Модуль Runbook</span><span class="sxs-lookup"><span data-stu-id="b891e-124">Runbook</span></span> | <span data-ttu-id="b891e-125">Описание</span><span class="sxs-lookup"><span data-stu-id="b891e-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b891e-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="b891e-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="b891e-127">Проверяет расписание каждой виртуальной машины и выполняет завершение работы или запуск в зависимости от расписания</span><span class="sxs-lookup"><span data-stu-id="b891e-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="b891e-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="b891e-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="b891e-129">Добавляет тег Schedule для виртуальной машины или группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b891e-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="b891e-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="b891e-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="b891e-131">Изменяет имеющийся тег Schedule, заменяя его новым</span><span class="sxs-lookup"><span data-stu-id="b891e-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="b891e-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="b891e-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="b891e-133">Удаляет тег Schedule виртуальной машины или группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b891e-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="b891e-134">Установка и настройка сценария</span><span class="sxs-lookup"><span data-stu-id="b891e-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="b891e-135">Установка и публикация модулей Runbook</span><span class="sxs-lookup"><span data-stu-id="b891e-135">Install and publish the runbooks</span></span>
<span data-ttu-id="b891e-136">Скачав модули Runbook, импортируйте их, как описано в статье [Создание или импорт модуля Runbook в службе автоматизации Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="b891e-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="b891e-137">Опубликуйте каждый модуль Runbook после импорта в учетную запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b891e-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="b891e-138">Добавление расписания в модуль Runbook Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="b891e-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="b891e-139">Выполните следующие действия, чтобы включить расписание в модуль Runbook Test-ResourceSchedule.</span><span class="sxs-lookup"><span data-stu-id="b891e-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="b891e-140">Это модуль Runbook, который проверяет, какую виртуальную машину следует запустить, отключить или оставить как есть.</span><span class="sxs-lookup"><span data-stu-id="b891e-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="b891e-141">На портале Azure откройте свою учетную запись службы автоматизации и щелкните элемент **Модули Runbook** .</span><span class="sxs-lookup"><span data-stu-id="b891e-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="b891e-142">В колонке **Test-ResourceSchedule** щелкните элемент **Расписания**.</span><span class="sxs-lookup"><span data-stu-id="b891e-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="b891e-143">В колонке **Расписания** щелкните **Добавить расписание**.</span><span class="sxs-lookup"><span data-stu-id="b891e-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="b891e-144">В колонке **Расписания** выберите **Связать расписание с модулем Runbook**,</span><span class="sxs-lookup"><span data-stu-id="b891e-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="b891e-145">а затем — **Создать новое расписание**.</span><span class="sxs-lookup"><span data-stu-id="b891e-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="b891e-146">В колонке **Новое расписание** введите имя расписания, например *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="b891e-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="b891e-147">В поле **Запуск**расписания задайте время запуска, округленное до часов.</span><span class="sxs-lookup"><span data-stu-id="b891e-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="b891e-148">Выберите **Повторение** и для интервала **Повторять кажд.** выберите значение **1 час**.</span><span class="sxs-lookup"><span data-stu-id="b891e-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="b891e-149">Для параметра **Задать срок действия** задайте значение **Нет** и нажмите кнопку **Создать**, чтобы сохранить новое расписание.</span><span class="sxs-lookup"><span data-stu-id="b891e-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="b891e-150">В колонке параметров **Включить модуль Runbook в расписание** выберите **Параметры и настройки запуска**.</span><span class="sxs-lookup"><span data-stu-id="b891e-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="b891e-151">В колонке **Параметры** модуля Test-ResourceSchedule в поле **SubscriptionName** введите имя подписки.</span><span class="sxs-lookup"><span data-stu-id="b891e-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="b891e-152">Это единственный параметр, необходимый для модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="b891e-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="b891e-153">Закончив, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b891e-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="b891e-154">После этого расписание Runbook должно выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b891e-154">The runbook schedule should look like the following when it's completed:</span></span>

![Настроенный модуль Runbook Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="b891e-156">Форматирование строки JSON</span><span class="sxs-lookup"><span data-stu-id="b891e-156">Format the JSON string</span></span>
<span data-ttu-id="b891e-157">Это решение фактически принимает строку JSON в указанном формате и добавляет ее в качестве значения для тега Schedule.</span><span class="sxs-lookup"><span data-stu-id="b891e-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="b891e-158">Затем модуль Runbook получает список всех групп ресурсов и виртуальных машин и определяет расписания для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b891e-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="b891e-159">Он перебирает эти виртуальные машины по заданным расписаниям и проверяет, какое действие следует выполнить.</span><span class="sxs-lookup"><span data-stu-id="b891e-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="b891e-160">Ниже приведен пример соответствующего форматирования.</span><span class="sxs-lookup"><span data-stu-id="b891e-160">The following is an example of how the solutions should be formatted:</span></span>

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

<span data-ttu-id="b891e-161">Вот подробные сведения об этой структуре:</span><span class="sxs-lookup"><span data-stu-id="b891e-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="b891e-162">Формат этой структуры JSON оптимизирован для обхода ограничения в 256 знаков на значение тега в Azure.</span><span class="sxs-lookup"><span data-stu-id="b891e-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="b891e-163">*TzId* представляет часовой пояс виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b891e-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="b891e-164">Этот идентификатор можно получить с помощью класса TimeZoneInfo .NET в сеансе PowerShell:**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="b891e-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones в PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="b891e-166">Дни недели представлены числом от нуля до шести.</span><span class="sxs-lookup"><span data-stu-id="b891e-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="b891e-167">Значение 0 соответствует воскресенью.</span><span class="sxs-lookup"><span data-stu-id="b891e-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="b891e-168">Время запуска представлено атрибутом **S** и его значением в 24-часовом формате.</span><span class="sxs-lookup"><span data-stu-id="b891e-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="b891e-169">Время окончания или завершения работы представлено атрибутом **E** и его значением в 24-часовом формате.</span><span class="sxs-lookup"><span data-stu-id="b891e-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="b891e-170">Если атрибуты **S** и **E** имеют значение 0 (ноль), то во время проверки виртуальная машина останется в своем текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="b891e-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="b891e-171">Если вы хотите пропустить проверку в определенный день недели, то не добавляйте раздел этого дня недели.</span><span class="sxs-lookup"><span data-stu-id="b891e-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="b891e-172">В следующем примере проверка выполняется только в понедельник, а в остальные дни недели она пропускается.</span><span class="sxs-lookup"><span data-stu-id="b891e-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="b891e-173">Добавление тегов для групп ресурсов или виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b891e-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="b891e-174">Для завершения работы виртуальных машин необходимо отметить тегом их или группы ресурсов, в которых они находятся.</span><span class="sxs-lookup"><span data-stu-id="b891e-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="b891e-175">Виртуальные машины, у которых нет тега Schedule, не проверяются.</span><span class="sxs-lookup"><span data-stu-id="b891e-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="b891e-176">По этой причине их запуск или завершение их работы не выполняется.</span><span class="sxs-lookup"><span data-stu-id="b891e-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="b891e-177">Существует два способа маркировки виртуальных машин или групп ресурсов при использовании этого решения.</span><span class="sxs-lookup"><span data-stu-id="b891e-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="b891e-178">Это можно сделать непосредственно на портале</span><span class="sxs-lookup"><span data-stu-id="b891e-178">You can do it directly from the portal.</span></span> <span data-ttu-id="b891e-179">или с помощью модулей Runbook Add-ResourceSchedule, Update-ResourceSchedule и Remove-ResourceSchedule.</span><span class="sxs-lookup"><span data-stu-id="b891e-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="b891e-180">Добавление тегов с помощью портала</span><span class="sxs-lookup"><span data-stu-id="b891e-180">Tag through the portal</span></span>
<span data-ttu-id="b891e-181">Выполните следующие действия, чтобы добавить тег для виртуальной машины или группы ресурсов на портале.</span><span class="sxs-lookup"><span data-stu-id="b891e-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="b891e-182">Преобразуйте строку JSON в плоскую структуру и убедитесь, что в ней нет пробелов.</span><span class="sxs-lookup"><span data-stu-id="b891e-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="b891e-183">Строка JSON должна выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b891e-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="b891e-184">Щелкните значок **Тег** для виртуальной машины или группы ресурсов, чтобы применить это расписание.</span><span class="sxs-lookup"><span data-stu-id="b891e-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![Параметр тега виртуальной машины](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="b891e-186">Теги определяются следующей парой "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="b891e-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="b891e-187">Введите **Schedule** в поле **Ключ** и вставьте строку JSON в поле **Значение**.</span><span class="sxs-lookup"><span data-stu-id="b891e-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="b891e-188">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b891e-188">Click **Save**.</span></span> <span data-ttu-id="b891e-189">Новый тег должен появиться в списке тегов для ресурса.</span><span class="sxs-lookup"><span data-stu-id="b891e-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![Тег Schedule виртуальной машины](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="b891e-191">Добавление тега из PowerShell</span><span class="sxs-lookup"><span data-stu-id="b891e-191">Tag from PowerShell</span></span>
<span data-ttu-id="b891e-192">Все импортированные модули Runbook содержат справочные сведения в начале скрипта, в которых описывается выполнение Runbook непосредственно из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b891e-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="b891e-193">Модули Runbook Add-ScheduleResource и Update-ScheduleResource можно вызывать из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b891e-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="b891e-194">Для этого нужно передать необходимые параметры, позволяющие создать или обновить тег Schedule для виртуальной машины или группы ресурсов за пределами портала.</span><span class="sxs-lookup"><span data-stu-id="b891e-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="b891e-195">Чтобы создавать, добавлять и удалять теги с помощью PowerShell, необходимо сначала настроить [среду PowerShell для Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b891e-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="b891e-196">После завершения настройки можно перейти к следующим действиям.</span><span class="sxs-lookup"><span data-stu-id="b891e-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="b891e-197">Создание тега Schedule с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b891e-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="b891e-198">Откройте сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b891e-198">Open a PowerShell session.</span></span> <span data-ttu-id="b891e-199">Затем выполните следующую команду, чтобы пройти аутентификацию с помощью учетной записи запуска от имени и указать подписку.</span><span class="sxs-lookup"><span data-stu-id="b891e-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="b891e-200">Определите хэш-таблицу расписания.</span><span class="sxs-lookup"><span data-stu-id="b891e-200">Define a schedule hash table.</span></span> <span data-ttu-id="b891e-201">Ниже приведен пример ее структуры.</span><span class="sxs-lookup"><span data-stu-id="b891e-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="b891e-202">Определите параметры, необходимые для Runbook.</span><span class="sxs-lookup"><span data-stu-id="b891e-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="b891e-203">В следующем примере в качестве цели используется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="b891e-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="b891e-204">Если вы отмечаете тегами группу ресурсов, удалите параметр *VMName* из хэш-таблицы $params следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b891e-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="b891e-205">Выполните модуль Runbook Add-ResourceSchedule со следующими параметрами, чтобы создать тег Schedule.</span><span class="sxs-lookup"><span data-stu-id="b891e-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="b891e-206">Чтобы обновить тег группы ресурсов или виртуальной машины, выполните модуль Runbook **Update-ResourceSchedule** со следующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="b891e-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="b891e-207">Удаление тега Schedule с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b891e-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="b891e-208">Откройте сеанс PowerShell и выполните следующую команду, чтобы пройти аутентификацию с помощью учетной записи запуска от имени, а также выбрать и указать подписку.</span><span class="sxs-lookup"><span data-stu-id="b891e-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="b891e-209">Определите параметры, необходимые для Runbook.</span><span class="sxs-lookup"><span data-stu-id="b891e-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="b891e-210">В следующем примере в качестве цели используется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="b891e-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="b891e-211">Если вы удаляете тег группы ресурсов, удалите параметр *VMName* из хэш-таблицы $params следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b891e-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="b891e-212">Выполните модуль Runbook Remove-ResourceSchedule, чтобы удалить тег Schedule.</span><span class="sxs-lookup"><span data-stu-id="b891e-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="b891e-213">Чтобы обновить тег группы ресурсов или виртуальной машины, выполните модуль Runbook Remove-ResourceSchedule со следующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="b891e-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="b891e-214">Рекомендуется применять упреждающий мониторинг этих модулей Runbook (и состояния виртуальной машины), чтобы проверять, соответствующим ли образом выполняется запуск и завершение работы виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b891e-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="b891e-215">Сведения о задании Runbook Test-ResourceSchedule можно просмотреть на портале Azure, выбрав элемент **Задания** этого модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="b891e-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="b891e-216">Помимо общей информации о задании, сводка задания будет содержать входные параметры и поток вывода, а также все возникшие исключения.</span><span class="sxs-lookup"><span data-stu-id="b891e-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="b891e-217">**Сводка по заданию** содержит сообщения из потоков вывода, предупреждений и ошибок.</span><span class="sxs-lookup"><span data-stu-id="b891e-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="b891e-218">Выберите элемент **Вывод** , чтобы просмотреть подробные сведения о результатах выполнения модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="b891e-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Выходные данные Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="b891e-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b891e-220">Next steps</span></span>
* <span data-ttu-id="b891e-221">Чтобы приступить к работе с модулями Runbook рабочих процессов PowerShell, обратитесь к статье [Первый Runbook рабочего процесса PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="b891e-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="b891e-222">Дополнительные сведения о типах модулей Runbook, их преимуществах и ограничениях см. в статье [Типы модулей Runbook в службе автоматизации Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="b891e-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="b891e-223">Дополнительные сведения о функции поддержки сценариев PowerShell см. в публикации блога [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Поддержка собственных сценариев PowerShell в службе автоматизации Azure).</span><span class="sxs-lookup"><span data-stu-id="b891e-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="b891e-224">Чтобы узнать больше о ведении журнала и выходных данных Runbook, ознакомьтесь со статьей [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="b891e-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="b891e-225">Дополнительные сведения об учетной записи запуска от имени Azure и о том, как с ее помощью выполнить аутентификацию модулей Runbook, см. в статье [Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="b891e-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
