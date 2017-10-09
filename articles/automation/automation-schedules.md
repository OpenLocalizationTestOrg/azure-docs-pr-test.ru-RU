---
title: "aaaSchedules в службе автоматизации Azure | Документы Microsoft"
description: "Расписания автоматизации, используемые tooschedule Runbook в автоматизации Azure toostart автоматически. Описывает способ toocreate управления графиком в, чтобы он автоматически запустить runbook на определенный момент времени или по повторяющемуся расписанию."
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
ms.openlocfilehash: 888a5d15fd3442a2b8ab18dd8b0eb4ab9ad0c0d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Создание расписания для Runbook в службе автоматизации Azure
tooschedule runbook в автоматизации Azure toostart в указанное время, свяжите его tooone или более расписаний. Расписание может быть настроенный tooeither запустить один раз или каждый час повторения или ежедневное расписание для Runbook в hello классический портал Azure и для модулей Runbook в hello портал Azure можно также запланировать их для еженедельно, ежемесячно, определенные дни недели hello или дней hello месяц или определенный день месяца hello.  Runbook может быть toomultiple связанного расписания и одним расписанием можно связать несколько модулей Runbook tooit.

> [!NOTE]
> В настоящее время расписания не поддерживают конфигурации Azure Automation DSC.
> 
> 

## <a name="windows-powershell-cmdlets"></a>Командлеты Windows PowerShell
командлеты Hello в следующей таблице hello, используемые toocreate расписаний и управление ими с помощью Windows PowerShell в службе автоматизации Azure. Они поставляются как часть hello [модуля Azure PowerShell](/powershell/azure/overview).

| Командлеты | Описание |
|:--- |:--- |
| **Командлеты диспетчера ресурсов Azure** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |Получает расписание. |
| [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) |Создает новое расписание. |
| [Remove-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |Удаляет расписание. |
| [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |Задает свойства hello для существующего расписания. |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |Получает расписание модулей Runbook. |
| [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |Связывает Runbook с расписанием. |
| [Unregister-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |Отменяет связь Runbook с расписанием. |
| **Командлеты для управления службами Azure** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |Получает расписание. |
| [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |Создает новое расписание. |
| [Remove-AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |Удаляет расписание. |
| [Set-AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |Задает свойства hello для существующего расписания. |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Получает расписание модулей Runbook. |
| [Register-AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Связывает Runbook с расписанием. |
| [Unregister-AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Отменяет связь Runbook с расписанием. |

## <a name="creating-a-schedule"></a>Создание расписания
Можно создать новое расписание для Runbook в hello портал Azure hello классического портала или с помощью Windows PowerShell. Также имеется возможность hello создания нового расписания при связывании расписания tooa runbook с помощью hello классический Azure или портал Azure.

> [!NOTE]
> Службы автоматизации Azure будет использовать последнюю модули hello в вашей учетной записи автоматизации при запуске нового запланированного задания.  модули Runbook и hello, влияющие на tooavoid процессов они автоматизации, сначала следует проверить все модули Runbook, связанные расписания с помощью учетной записи автоматизации, предназначенный для тестирования.  Это позволит убедиться в запланированных модулей Runbook продолжить toowork правильно, а если нет, можно дополнительно Устранение неполадок и применить все изменения требуется до миграции tooproduction hello обновить версии runbook.  
>  Ваша учетная запись автоматизации не предоставляется автоматически всех новых версий модулей, если вы обновили их вручную, выбрав hello [модули Azure обновления](automation-update-azure-modules.md) параметр из hello **модули** колонку. 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate новое расписание в hello портал Azure
1. Hello портала Azure из учетной записи автоматизации щелкните hello **активы** плитки приветствия tooopen **активы** колонку.
2. Щелкните hello **расписания** плитки приветствия tooopen **расписания** колонку.
3. Нажмите кнопку **Добавить расписание** hello верхней части колонки hello.
4. На hello **новое расписание** колонке введите **имя** и при необходимости **описание** для hello новое расписание.
5. Выбрать hello расписание будет выполняться один раз или по расписанию повторяющегося путем выбора **один раз** или **повторения**.  Если вы выбрали режим **Однократно**, то укажите **время начала** и нажмите кнопку **Создать**.  При выборе **повторения**, укажите **время начала** и частоту hello частоту hello runbook toorepeat - по **час**, **день**, **недели**, или **месяц**.  При выборе **недели** или **месяц** из раскрывающегося списка hello, hello **режим повторения** появится в колонке hello и после выбора, hello **повторения параметр** откроется колонка и hello день недели, можно выбрать, если вы выбрали **недели**.  Если вы выбрали **месяц**, вы можете выбрать **дни недели** или конкретные дни месяца hello в hello календаря и наконец, необходимо toorun ее на hello последний день месяца hello, или нет, а затем нажмите кнопку **ОК** .   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate новое расписание в hello классический портал Azure
1. В hello классический портал Azure выберите автоматизации, а затем выберите имя учетной записи автоматизации hello.
2. Выберите hello **активы** вкладки.
3. Hello нижней части окна hello, нажмите кнопку **добавить параметр**.
4. Щелкните **Добавить расписание**.
5. Введите значение **имя** и при необходимости **описание** для новых schedule.your hello расписание запуска **один раз**, **почасовой**, **Ежедневно**, **еженедельно**, или **ежемесячные**.
6. Укажите **время начала** и другие параметры в зависимости от типа выбранного расписания hello.

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate новое расписание с помощью Windows PowerShell
Можно использовать hello [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) toocreate командлет новое расписание в службе автоматизации Azure для классического Runbook или [New AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) командлета для модулей Runbook в hello Azure портал. Необходимо указать время начала hello hello расписание и частота hello, оно должно выполняться.

Hello следующем образце команд Показать как toocreate расписание для hello 15 и 30-й день каждого месяца, с помощью командлета диспетчера ресурсов Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

Следующие примеры команд Hello Показать, как toocreate новое расписание, которое будет выполняться каждый день в 3:30 запуск на 20 января 2015 г. с помощью командлета управления службами Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a>Связывание расписания tooa runbook
Runbook может быть toomultiple связанного расписания и одним расписанием можно связать несколько модулей Runbook tooit. Если Runbook имеет параметры, для них можно указать значения. Необходимо предоставить значения для всех обязательных параметров, а также значения для необязательных параметров.  Эти значения будут использованы каждый раз при запуске hello runbook, это расписание.  Можно присоединить Привет одному расписанию tooanother runbook и указать различные значения параметров.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink runbook tooa расписание с hello портал Azure
1. Hello портала Azure из учетной записи автоматизации щелкните hello **Runbooks** hello tooopen плитки **модулей Runbook** колонку.
2. Щелкните имя hello runbook tooschedule hello.
3. Если hello runbook не связанных в данный момент tooa расписания, будет быть toocreate параметр hello заданного расписания или ссылку tooan существующего расписания.  
4. Если hello runbook имеет параметры, можно выбрать параметр hello **изменить параметры запуска (по умолчанию: Azure)** и hello **параметры** колонке представлены для ввода сведений hello соответствующим образом.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink runbook tooa расписание с hello классический портал Azure
1. В hello классический портал Azure, выберите **автоматизации** и щелкните имя учетной записи автоматизации hello.
2. Выберите hello **Runbooks** вкладки.
3. Щелкните имя hello runbook tooschedule hello.
4. Нажмите кнопку hello **расписание** вкладки.
5. Если hello runbook не связанных в данный момент tooa расписания, то вам будет предоставлена возможность hello слишком**связать tooa новое расписание** или **tooan расписание существующие связи**.  Если hello runbook связанных в данный момент tooa расписание, нажмите кнопку **ссылку** на hello нижней части окна tooaccess hello эти параметры.
6. Если hello runbook имеет параметры, будет приглашение их значения.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink runbook tooa расписания с помощью Windows PowerShell
Можно использовать hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink runbook классический tooa расписание или [AzureRmAutomationScheduledRunbook регистра](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) командлета для модулей Runbook в hello портал Azure.  Можно указать значения для параметров hello runbook с параметром параметры hello. Дополнительные сведения об указании значений параметров см. в разделе [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).

Hello следующем образце команд Показать как toolink runbook tooa расписание, с помощью командлета Azure Resource Manager с параметрами.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
Hello следующем образце команд Показать как toolink с помощью командлета управления службами Azure с параметрами расписания.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>Отключение расписания
При отключении расписания, все модули Runbook, связанные tooit больше не будут работать по этому расписанию. Можно отключить расписание вручную или указать срок действия при создании периодических расписаний. По истечении времени истечения срока действия hello hello расписания будут отключены.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable расписания из hello портал Azure
1. Hello портала Azure из учетной записи автоматизации щелкните hello **активы** плитки приветствия tooopen **активы** колонку.
2. Щелкните hello **расписания** плитки приветствия tooopen **расписания** колонку.
3. Щелкните имя hello стоечный модуль подробности расписания tooopen hello.
4. Изменение **включено** слишком**нет**.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable расписания из hello классический портал Azure
Вы можете отключить расписания на классический портал Azure на странице Подробности расписания hello для расписания hello hello.

1. В hello классический портал Azure выберите автоматизации и нажмите кнопку hello имя учетной записи автоматизации.
2. Перейдите на вкладку активы hello.
3. Щелкните страницу сведений о hello имя tooopen расписания.
4. Изменение **включено** слишком**нет**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable расписания с помощью Windows PowerShell
Можно использовать hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) командлет toochange hello свойства существующего расписания для классического runbook или [AzureRmAutomationSchedule набор](/powershell/module/azurerm.automation/set-azurermautomationschedule) командлета для модулей Runbook в hello Azure портал. toodisable hello план, укажите **false** для hello **IsEnabled** параметра.

Hello следующем образце команд Показать как toodisable расписание для runbook, с помощью командлета диспетчера ресурсов Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

Hello следующие примеры команд показывают, как toodisable расписанию с помощью hello командлет управления службами Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>Дальнейшие действия
* tooget к работе с модулями Runbook в автоматизации Azure в разделе [запуск Runbook в автоматизации Azure](automation-starting-a-runbook.md) 

