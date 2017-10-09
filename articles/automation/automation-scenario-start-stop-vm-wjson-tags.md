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
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Сценария автоматизации Azure: с помощью формата JSON теги toocreate расписание для включения и выключения виртуальной Машины Azure
Часто возникает необходимость запуска tooschedule hello и завершение работы виртуальных машин toohelp снизить затраты на подписку или поддержки коммерческих и технических требований.

Hello следующий сценарий позволяет tooset автоматического запуска и завершения работы виртуальных машин с помощью тега "Расписание" на уровне группы ресурсов или уровне виртуальной машины в Azure. Это расписание можно настроить из tooSaturday воскресенье с временем запуска и время завершения работы.

Для реализации этой возможности используются некоторые готовые функции. В частности, описаны такие возможности:

* [Наборы масштабирования виртуальных машин](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) с параметрами автоматического масштабирования, позволяющие tooscale in или out.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) службу, которая имеет встроенные возможности hello планирования операций запуска и завершения работы.

Однако эти параметры поддерживают только конкретных сценариев и не может быть применен tooinfrastructure как услуга (IaaS) виртуальных машин.

Hello тег расписания применяются tooa группы ресурсов, открывается также примененных tooall виртуальных машин в этой группе ресурсов. Если расписание также непосредственно примененных tooa виртуальной Машины, последнего расписания hello приоритет в hello следующий порядок:

1. Группа ресурсов примененных tooa расписания
2. Расписание применяется tooa группы ресурсов и виртуальной машины в группе ресурсов hello
3. Расписание применения tooa виртуальной машины

Этот сценарий по существу принимает строку в указанном формате JSON и добавляет его как значение hello для тега "Расписание". Затем runbook список всех групп ресурсов и виртуальных машин и определяет hello расписания для каждой виртуальной Машины на основе сценариев hello, перечисленных выше. Затем просматривает hello виртуальных машин, которые имеют расписания, связанные и оценивает, какое действие должно выполняться. Например он определяет, какие виртуальные машины должны toobe остановлена, завершение работы или игнорируются.

Эти модули Runbook для проверки подлинности с помощью hello [учетная запись запуска от имени Azure](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Скачать Runbook hello для сценария hello
Этот сценарий состоит из четырех Runbook рабочего процесса PowerShell, которые можно загрузить из hello [коллекции TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) или hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) репозитория для этого проекта.

| Модуль Runbook | Описание |
| --- | --- |
| Test-ResourceSchedule |Проверяет каждое расписание виртуальной машины и выполняет завершения работы или запуска, в зависимости от расписания hello. |
| Add-ResourceSchedule |Добавляет hello расписание тег tooa виртуальной Машины или группы ресурсов. |
| Update-ResourceSchedule |Изменяет существующий тег расписание hello, заменив его новым. |
| Remove-ResourceSchedule |Удаляет расписание тег hello из виртуальной Машины или группы ресурсов. |

## <a name="install-and-configure-this-scenario"></a>Установка и настройка сценария
### <a name="install-and-publish-hello-runbooks"></a>Установка и публикации Runbook hello
После загрузки hello модулей Runbook, можно импортировать их с помощью процедуры hello в [Создание или импорт модуля runbook в автоматизации Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Опубликуйте каждый модуль Runbook после импорта в учетную запись автоматизации.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Добавить расписание toohello ResourceSchedule теста runbook
Выполните эти шаги tooenable hello расписание hello ResourceSchedule тестирования runbook. Это hello runbook, который проверяет, какие виртуальные машины должна быть запущена, выключена, или влево, как есть.

1. Из hello портал Azure, откройте учетную запись автоматизации и нажмите кнопку hello **Runbooks** плитки.
2. На hello **теста ResourceSchedule** колонка, щелкните hello **расписания** плитки.
3. На hello **расписания** колонка, щелкните **Добавить расписание**.
4. На hello **расписания** колонке выберите **связать runbook расписания tooyour**. а затем — **Создать новое расписание**.
5. На hello **новое расписание** колонки, введите имя hello этого расписания, например: *HourlyExecution*.
6. Для расписания hello **запустить**, задайте увеличение час tooan времени начала hello.
7. Выберите **Повторение** и для интервала **Повторять кажд.** выберите значение **1 час**.
8. Убедитесь, что **срок действия набора** задано слишком**нет**, а затем нажмите кнопку **создать** toosave новое расписание.
9. На hello **Runbook расписания** параметры колонке выберите **параметры и настройки запуска**. В hello теста ResourceSchedule **параметры** колонки, введите имя подписки hello в hello **Имя_подписки** поля.  Это единственный параметр hello, требуемое для hello runbook.  Закончив, нажмите кнопку **ОК**.

После завершения Hello согласно расписанию runbook должен выглядеть hello следующее:

![Настроенный модуль Runbook Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Формат hello строки JSON
Это решение по сути принимает строку в указанном формате JSON и добавляет его как значение hello для тега "Расписание". Затем runbook список всех групп ресурсов и виртуальных машин и определяет hello расписания для каждой виртуальной машины.

Hello runbook обрабатывает в цикле hello виртуальных машин, имеющих расписания, связанные и проверяет, какие действия необходимы. Hello ниже приведен пример форматирования hello решения:

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

Вот подробные сведения об этой структуре:

1. Формат Hello этой структуры JSON — оптимизированный toowork обойти ограничение до 256 символов hello значения одного тега в Azure.
2. *TzId* представляет hello часового пояса hello виртуальной машины. Этот идентификатор можно получить с помощью класса TimeZoneInfo .NET hello в сеансе PowerShell--**[System.TimeZoneInfo]:: GetSystemTimeZones()**.

   ![GetSystemTimeZones в PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Дни недели, представлены с числовым значением нуль toosix. нулевое значение Hello равняется воскресенье.
   * Hello время начала представляется с hello **S** атрибут и его значение находится в 24-часовом формате.
   * Hello времени завершения или завершения работы представляется с hello **E** атрибут и его значение находится в 24-часовом формате.

     Если hello **S** и **E** атрибуты каждого иметь значение нуль (0), hello виртуальной машины остается в текущем состоянии во время hello оценки.
3. Если требуется tooskip оценки для определенного дня недели hello не добавить раздел в тот же день недели hello. В hello вычисляется следующий пример, только понедельник и hello остальные дни недели hello игнорируются:

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Добавление тегов для групп ресурсов или виртуальных машин
tooshut работу виртуальных машин необходимо tootag hello виртуальных машин или hello групп ресурсов, в которых они расположены. Виртуальные машины, у которых нет тега Schedule, не проверяются. По этой причине их запуск или завершение их работы не выполняется.

Существуют два способа tootag ресурсов группы или виртуальные машины с данным решением. Его можно сделать непосредственно с портала hello. Или можно использовать hello ResourceSchedule добавить, ResourceSchedule обновление и удаление ResourceSchedule модулей Runbook.

### <a name="tag-through-hello-portal"></a>Тег через портал hello
Выполните эти шаги tootag виртуальной машины или группы ресурсов на портале hello.

1. Сведение строку hello JSON и убедитесь, что не все пробелы.  Строка JSON должна выглядеть следующим образом.

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Выберите hello **тега** значок для виртуальной Машины или ресурсов группы tooapply этого расписания.

   ![Параметр тега виртуальной машины](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. Теги определяются следующей парой "ключ — значение". Тип **расписания** в hello **ключ** поле, а затем вставьте строку JSON hello в hello **значение** поле. Щелкните **Сохранить**. Ваш новый тег должен появиться в списке hello тегов для ресурса.

   ![Тег Schedule виртуальной машины](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>Добавление тега из PowerShell
Все импортированные модули Runbook содержат справочные сведения в начале hello hello скрипт, который описывает, каким образом tooexecute hello Runbook непосредственно из PowerShell. Модули Runbook ScheduleResource Установка и обновление ScheduleResource hello можно вызвать из PowerShell. Это делается путем передачи обязательные параметры, позволяющие тег расписание hello toocreate или обновление виртуальной Машины или группа ресурсов за пределами портала hello.

toocreate, добавление и удаление тегов с помощью PowerShell, необходимо сначала слишком[настройки среды PowerShell для Azure](/powershell/azure/overview). После завершения установки hello, можно продолжить hello следующие шаги.

### <a name="create-a-schedule-tag-with-powershell"></a>Создание тега Schedule с помощью PowerShell
1. Откройте сеанс PowerShell. Затем используйте следующий пример tooauthenticate, используя учетную запись запуска от имени и toospecify подписки hello:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Определите хэш-таблицу расписания. Ниже приведен пример ее структуры.

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Определите параметры hello, необходимых для hello runbook. В следующем примере hello мы ожидаем виртуальной Машины:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Если добавление тегов в группе ресурсов, удалите hello *VMName* параметр из хэша hello $params таблицы следующим образом:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Выполните hello добавить ResourceSchedule runbook с hello после тега расписание hello toocreate параметры:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. tooupdate тег виртуальной машины или группы ресурсов, выполните hello **ResourceSchedule обновление** runbook с hello следующие параметры:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>Удаление тега Schedule с помощью PowerShell
1. Откройте сеанс PowerShell и выполните следующие tooauthenticate, используя учетную запись запуска от имени и tooselect hello и укажите подписку.

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Определите параметры hello, необходимых для hello runbook. В следующем примере hello мы ожидаем виртуальной Машины:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    При удалении тег из группы ресурсов, удалите hello *VMName* параметр из хэша hello $params таблицы следующим образом:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Выполнение расписания hello Remove ResourceSchedule runbook tooremove hello тег:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate тег виртуальной машины или группы ресурсов, выполнить hello Remove ResourceSchedule runbook с hello следующие параметры:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> Рекомендуется заранее отслеживать эти модули Runbook (и hello состояния виртуальных машин) tooverify, виртуальных машин выполняется завершение работы и работы соответствующим образом.
>

Подробности hello tooview hello ResourceSchedule тестирования модуля Runbook задания в hello портал Azure, выберите hello **заданий** плитки приветствия runbook. Hello задания сводки Вывод hello входных параметров и вывода hello потока, кроме toogeneral сведения о задании hello и любые исключения, если они имели место.

Hello **Сводка заданий** включает в себя сообщения из hello потоков вывода, предупреждения и ошибки. Выберите hello **вывода** плитки tooview подробные результаты из выполнения runbook hello.

![Выходные данные Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Дальнейшие действия
* tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый рабочий процесс runbook PowerShell](automation-first-runbook-textual.md).
* в разделе toolearn Дополнительные сведения о типах runbook и их преимущества и ограничения, [типов runbook службы автоматизации Azure](automation-runbook-types.md).
* Дополнительные сведения о функции поддержки сценариев PowerShell см. в публикации блога [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/) (Поддержка собственных сценариев PowerShell в службе автоматизации Azure).
* toolearn Дополнительные сведения о ведение журнала runbook и выходные данные, в разделе [Runbook выходные данные и сообщения в службе автоматизации Azure](automation-runbook-output-and-messages.md).
* Дополнительные сведения об учетной записи запуска от имени Azure и как tooauthenticate модули Runbook с помощью, см. статью toolearn [проверки подлинности модулей Runbook с помощью учетной записи запуска от имени Azure](automation-sec-configure-azure-runas-account.md).
