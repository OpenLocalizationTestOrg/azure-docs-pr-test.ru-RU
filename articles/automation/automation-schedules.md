---
title: "Расписания в службе автоматизации Azure | Документация Майкрософт"
description: "Расписания службы автоматизации используются для планирования автоматического выполнения модулей Runbook в службе автоматизации Azure. Рассматривается создание расписания, которое позволяет автоматически запускать модуль Runbook однократно или несколько раз в определенное время, а также управление этим расписанием."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 140bea93c4563666e8cfdf356eaf87500c1aca8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Создание расписания для Runbook в службе автоматизации Azure
Чтобы запускать модуль Runbook в определенное время с помощью расписания в службе автоматизации Azure, его необходимо привязать к одному или нескольким расписаниям. На классическом портале Azure вы можете настроить расписание для однократного, ежечасного или ежедневного выполнения модулей Runbook. На портале Azure также можно запланировать выполнение еженедельно, ежемесячно, в конкретные дни недели, месяца или в определенный день месяца.  Один модуль Runbook может быть связан с несколькими расписаниями, и одно расписание может иметь несколько привязанных модулей Runbook.

> [!NOTE]
> В настоящее время расписания не поддерживают конфигурации Azure Automation DSC.
> 
> 

## <a name="windows-powershell-cmdlets"></a>Командлеты Windows PowerShell
Командлеты, представленные в следующей таблице, используются для создания расписаний и управления ими с помощью Windows PowerShell в службе автоматизации Azure. Они входят в состав [модуля Azure PowerShell](/powershell/azure/overview).

| Командлеты | Описание |
|:--- |:--- |
| **Командлеты диспетчера ресурсов Azure** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |Получает расписание. |
| [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) |Создает новое расписание. |
| [Remove-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |Удаляет расписание. |
| [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |Задает свойства для существующего расписания. |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |Получает расписание модулей Runbook. |
| [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |Связывает Runbook с расписанием. |
| [Unregister-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |Отменяет связь Runbook с расписанием. |
| **Командлеты для управления службами Azure** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |Получает расписание. |
| [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |Создает новое расписание. |
| [Remove-AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |Удаляет расписание. |
| [Set-AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |Задает свойства для существующего расписания. |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Получает расписание модулей Runbook. |
| [Register-AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Связывает Runbook с расписанием. |
| [Unregister-AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Отменяет связь Runbook с расписанием. |

## <a name="creating-a-schedule"></a>Создание расписания
Новое расписание для модулей Runbook вы можете создать на портале Azure, на классическом портале Azure или с помощью Windows PowerShell. Также расписание можно создать при связывании Runbook с расписанием с помощью портала Azure или классического портала Azure.

> [!NOTE]
> При запуске нового запланированного задания служба автоматизации Azure будет использовать модули последней версии в вашей учетной записи службы автоматизации.  Чтобы избежать влияния на модули Runbook и автоматизируемые ими процессы, необходимо сначала проверить все модули Runbook, которые имеют связанные расписания, используя учетную запись автоматизации, предназначенную для тестирования.  Это позволит обеспечить правильную работу запланированных модулей Runbook, а если нет, то вы сможете устранить неполадки и применить все необходимые изменения, прежде чем переносить обновленную версию модуля Runbook в рабочую среду.  
>  Учетная запись автоматизации не получит новые версии модулей автоматически, если их не обновить вручную, выбрав параметр [Обновить модули Azure](automation-update-azure-modules.md) в колонке **Модули**. 
>  

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a>Создание нового расписания на портале Azure
1. На портале Azure из учетной записи службы автоматизации щелкните элемент **Ресурсы**, чтобы открыть колонку **Ресурсы**.
2. Щелкните элемент **Расписания**, чтобы открыть колонку **Расписания**.
3. Щелкните **Добавить расписание** в верхней части этой колонки.
4. В колонке **Новое расписание** введите **имя** и при желании **описание** нового расписания.
5. Выберите режим выполнения расписания: **Однократно** или **Повторение**.  Если вы выбрали режим **Однократно**, то укажите **время начала** и нажмите кнопку **Создать**.  Если вы выбрали режим **Повторение**, то укажите **время начала** и частоту повторений для модуля Runbook: каждый **час**, **день**, **неделю** или **месяц**.  Если в этом раскрывающемся списке вы выбрали **неделю** или **месяц**, то в колонке появится элемент **Recurrence option** (Параметры периодичности). Щелкнув его, вы откроете колонку **Recurrence option** (Параметры периодичности). Здесь вы сможете выбрать день недели, если ранее выбрали параметр **неделя**.  Если же выбрать параметр **месяц**, то здесь можно выбрать **дни недели** или конкретные дни месяца из календаря, а также указать, будет ли модуль выполняться в последний день месяца. Завершив настройку, нажмите кнопку **OK**.   

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a>Создание нового расписания на классическом портале Azure
1. На классическом портале Azure щелкните "Служба автоматизации", а затем выберите имя учетной записи службы автоматизации.
2. Выберите вкладку **Средства** .
3. Нажмите кнопку **Добавить параметр**в нижней части окна.
4. Щелкните **Добавить расписание**.
5. Введите **имя** и при желании **описание** нового расписания. Расписание может выполняться **однократно**, **ежечасно**, **ежедневно**, **еженедельно** или **ежемесячно**.
6. Укажите **Время начала** и другие параметры в зависимости от типа выбранного расписания.

### <a name="to-create-a-new-schedule-with-windows-powershell"></a>Создание расписания с помощью Windows PowerShell
В службе автоматизации Azure вы можете использовать командлет [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0), чтобы создать новое расписание для классических модулей Runbook, или командлет [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule), чтобы создать расписание для модулей Runbook на портале Azure. Укажите для расписания время начала и частоту выполнения.

Приведенные ниже примеры команд демонстрируют, как с помощью командлета Azure Resource Manager создать расписание для запуска модуля в 15-й и 30-й день каждого месяца.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

Приведенные ниже примеры команд демонстрируют, как с помощью командлета управления службами Azure создать новое расписание, которое будет запускаться каждый день в 15:30 начиная с 20 января 2015 г.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-to-a-runbook"></a>Связывание расписания с модулем Runbook
Один модуль Runbook может быть связан с несколькими расписаниями, и одно расписание может иметь несколько привязанных модулей Runbook. Если Runbook имеет параметры, для них можно указать значения. Необходимо предоставить значения для всех обязательных параметров, а также значения для необязательных параметров.  Значения будут применяться каждый раз при запуске модуля Runbook с помощью расписания.  Один и тот же модуль Runbook можно привязать к другому расписанию и указать другие значения параметров.

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a>Связывание расписания с модулем Runbook с помощью портала Azure
1. На портале Azure из учетной записи службы автоматизации щелкните элемент **Модули Runbook**, чтобы открыть колонку **Модули Runbook**.
2. Щелкните имя одного модуля Runbook для привязки к расписанию.
3. Если модуль Runbook сейчас не связан с расписанием, вы сможете создать новое расписание или связать модуль с существующим расписанием.  
4. Если модуль Runbook имеет параметры, следует выбрать действие **Изменить параметры запуска (по умолчанию: Azure)**, чтобы открыть колонку **Параметры**, где вы сможете ввести нужные данные.  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a>Связывание расписания с модулем Runbook с помощью классического портала Azure
1. На классическом портале Azure щелкните **Служба автоматизации**, а затем — имя учетной записи службы автоматизации.
2. Выберите вкладку **Модули Runbook** .
3. Щелкните имя одного модуля Runbook для привязки к расписанию.
4. Перейдите на вкладку **Расписание** .
5. Если модуль Runbook в настоящее время не связан с расписанием, будет предоставлена возможность выбрать **ссылку на новое расписание** или **ссылку на существующее расписание**.  Если модуль в настоящее время связан с расписанием, щелкните **Ссылки** в нижней части окна для доступа к этим параметрам.
6. Если модуль Runbook имеет параметры, их необходимо будет заполнить.  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a>Связывание расписания с модулем Runbook с помощью Windows PowerShell
Вы можете использовать командлет [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx), чтобы связать расписание с классическим модулем Runbook, или командлет [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) для модулей Runbook на портале Azure.  С помощью параметра "Параметры" можно указать значения параметров для модуля Runbook. Дополнительные сведения об указании значений параметров см. в разделе [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).

Приведенные ниже примеры команд демонстрируют, как связать расписание с модулем Runbook, используя командлет управления службами Azure с параметрами.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
Приведенные ниже примеры команд демонстрируют, как связать расписание, используя командлет управления службами Azure с параметрами.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>Отключение расписания
Если расписание отключено, модули Runbook, связанные с ним, больше не будут запускаться по такому расписанию. Можно отключить расписание вручную или указать срок действия при создании периодических расписаний. При достижении срока действия расписания будут отключены.

### <a name="to-disable-a-schedule-from-the-azure-portal"></a>Отключение расписания на портале Azure
1. На портале Azure из учетной записи службы автоматизации щелкните элемент **Ресурсы**, чтобы открыть колонку **Ресурсы**.
2. Щелкните элемент **Расписания**, чтобы открыть колонку **Расписания**.
3. Щелкните имя расписания и откройте колонку со сведениями о нем.
4. Задайте значение **Нет** для параметра **Включено**.

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a>Отключение расписание на классическом портале Azure
Отключить расписание на классическом портале Azure можно на странице "Сведения о расписании" для соответствующего расписания.

1. На классическом портале Azure щелкните "Служба автоматизации", а затем — имя учетной записи службы автоматизации.
2. Перейдите на вкладку "Средства".
3. Щелкните имя расписания и откройте страницу со сведениями о нем.
4. Задайте значение **Нет** для параметра **Включено**.

### <a name="to-disable-a-schedule-with-windows-powershell"></a>Отключение расписания с помощью Windows PowerShell
В службе автоматизации Azure вы можете использовать командлет [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx), чтобы изменить свойства существующего расписания для классического модуля Runbook, или командлет [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule), чтобы изменить расписание для модулей Runbook на портале Azure. Чтобы отключить расписание, задайте значение **False** для параметра **IsEnabled**.

Приведенные ниже примеры команд демонстрируют, как отключить расписание для Runbook, используя командлет Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

Приведенные ниже примеры команд демонстрируют, как отключить расписание, используя командлет управления службами Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>Дальнейшие действия
* Сведения о том, как начать работу с модулями Runbook в службе автоматизации Azure, см. в статье [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md). 

