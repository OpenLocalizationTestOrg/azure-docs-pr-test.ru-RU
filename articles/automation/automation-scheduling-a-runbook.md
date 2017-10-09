---
title: "aaaScheduling runbook в автоматизации Azure | Документы Microsoft"
description: "Описывает способ toocreate расписания в службе автоматизации Azure, чтобы он автоматически запустить runbook на определенный момент времени или по повторяющемуся расписанию."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Создание расписания для Runbook в службе автоматизации Azure
tooschedule runbook в автоматизации Azure toostart в указанное время, свяжите его tooone или более расписаний. Расписание может быть настроенный tooeither запустить один раз или повторяющегося часам или дням расписание для Runbook в hello классический портал Azure и для модулей Runbook в hello портал Azure, можно дополнительно запланировать их для еженедельно, ежемесячно, определенные дни недели hello или дней месяц Hello, или определенный день месяца hello.  Runbook может быть toomultiple связанного расписания и одним расписанием можно связать несколько модулей Runbook tooit.

## <a name="creating-a-schedule"></a>Создание расписания
Можно создать новое расписание для Runbook в hello портал Azure hello классического портала или с помощью Windows PowerShell. Также имеется возможность hello создания нового расписания при связывании расписания tooa runbook с помощью hello классический Azure или портал Azure.

> [!NOTE]
> При связывании расписания с runbook автоматизации хранит текущие версии hello hello модулей в вашей учетной записи и их связи toothat расписания.  Это означает, что если вы модуль с версии 1.0 в вашей учетной записи при создании расписания, а затем обновить модуль hello tooversion 2.0, hello расписания будут toouse 1.0.  В версии обновленных модуля hello toouse заказ необходимо создать новое расписание. 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate новое расписание в hello классический портал Azure
1. В hello классический портал Azure выберите автоматизации и затем выберите имя учетной записи автоматизации hello.
2. Выберите hello **активы** вкладки.
3. Hello нижней части окна hello, нажмите кнопку **добавить параметр**.
4. Щелкните **Добавить расписание**.
5. Введите значение **имя** и при необходимости **описание** для новых schedule.your hello расписание запуска **один раз**, **почасовой**, **Ежедневно**, **еженедельно**, или **ежемесячные**.
6. Укажите **время начала** и другие параметры в зависимости от типа выбранного расписания hello.

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate новое расписание в hello портал Azure
1. Hello портала Azure из учетной записи автоматизации щелкните hello **активы** плитки приветствия tooopen **активы** колонку.
2. Щелкните hello **расписания** плитки приветствия tooopen **расписания** колонку.
3. Нажмите кнопку **Добавить расписание** hello верхней части колонки hello.
4. На hello **новое расписание** колонке введите **имя** и при необходимости **описание** для hello новое расписание.
5. Выбрать hello расписание будет выполняться один раз или по расписанию повторяющегося путем выбора **один раз** или **повторения**.  Если вы выбрали режим **Однократно**, то укажите **время начала** и нажмите кнопку **Создать**.  При выборе **повторения**, укажите **время начала** и частоту hello частоту hello runbook toorepeat - по **час**, **день**, **недели**, или **месяц**.  При выборе **недели** или **месяц** из раскрывающегося списка hello, hello **режим повторения** появится в колонке hello и после выбора, hello **повторения параметр** откроется колонка и hello день недели, можно выбрать, если вы выбрали **недели**.  Если вы выбрали **месяц**, вы можете выбрать **дни недели** или конкретные дни месяца hello в hello календаря и наконец, необходимо toorun ее на hello последний день месяца hello, или нет, а затем нажмите кнопку **ОК** .   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate новое расписание с помощью Windows PowerShell
Можно использовать hello [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) toocreate командлет новое расписание в службе автоматизации Azure для классического Runbook или [New AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) командлета для модулей Runbook в hello Azure портал. Необходимо указать время начала hello hello расписание и частота hello, оно должно выполняться.

Следующие примеры команд Hello Показать, как toocreate новое расписание, которое будет выполняться каждый день в 3:30 запуск на 20 января 2015 г. с помощью командлета управления службами Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

Hello следующие примеры команд показано как toocreate расписание для hello 15 и 30-й день каждого месяца, с помощью командлета диспетчера ресурсов Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a>Связывание расписания tooa runbook
Runbook может быть toomultiple связанного расписания и одним расписанием можно связать несколько модулей Runbook tooit. Если Runbook имеет параметры, для них можно указать значения. Необходимо предоставить значения для всех обязательных параметров, а также значения для необязательных параметров.  Эти значения будут использованы каждый раз при запуске hello runbook, это расписание.  Можно присоединить Привет одному расписанию tooanother runbook и указать различные значения параметров.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink runbook tooa расписание с hello классический портал Azure
1. В hello классический портал Azure, выберите **автоматизации** и нажмите кнопку hello имя учетной записи автоматизации.
2. Выберите hello **Runbooks** вкладки.
3. Щелкните имя hello runbook tooschedule hello.
4. Нажмите кнопку hello **расписание** вкладки.
5. Если hello runbook не связанных в данный момент tooa расписания, то вам будет предоставлена возможность hello слишком**связать tooa новое расписание** или **tooan расписание существующие связи**.  Если hello runbook связанных в данный момент tooa расписание, нажмите кнопку **ссылку** на hello нижней части окна tooaccess hello эти параметры.
6. Если hello runbook имеет параметры, будет приглашение их значения.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink runbook tooa расписание с hello портал Azure
1. Hello портала Azure из учетной записи автоматизации щелкните hello **Runbooks** hello tooopen плитки **модулей Runbook** колонку.
2. Щелкните имя hello runbook tooschedule hello.
3. Если hello runbook не связанных в данный момент tooa расписания, будет быть toocreate параметр hello заданного расписания или ссылку tooan существующего расписания.  
4. Если hello runbook имеет параметры, можно выбрать параметр hello **изменить параметры запуска (по умолчанию: Azure)** и hello **параметры** колонке представлены для ввода сведений hello соответствующим образом.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink runbook tooa расписания с помощью Windows PowerShell
Можно использовать hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink runbook классический tooa расписание или [AzureRmAutomationScheduledRunbook регистра](https://msdn.microsoft.com/library/mt603575.aspx) командлета для модулей Runbook в hello портал Azure.  Можно указать значения для параметров hello runbook с параметром параметры hello. Дополнительные сведения об указании значений параметров см. в разделе [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).

Hello следующем образце команд Показать как toolink с помощью командлета управления службами Azure с параметрами расписания.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

Hello следующем образце команд Показать как toolink runbook tooa расписание, с помощью командлета Azure Resource Manager с параметрами.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Отключение расписания
При отключении расписания, все модули Runbook, связанные tooit больше не будут работать по этому расписанию. Можно отключить расписание вручную или указать срок действия при создании периодических расписаний. По истечении времени истечения срока действия hello hello расписания будут отключены.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable расписания из hello классический портал Azure
Вы можете отключить расписания на классический портал Azure на странице Подробности расписания hello для расписания hello hello.

1. В hello классический портал Azure выберите автоматизации и затем щелкните имя учетной записи автоматизации hello.
2. Перейдите на вкладку активы hello.
3. Щелкните страницу сведений о hello имя tooopen расписания.
4. Изменение **включено** слишком**нет**.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable расписания из hello портал Azure
1. Hello портала Azure из учетной записи автоматизации щелкните hello **активы** плитки приветствия tooopen **активы** колонку.
2. Щелкните hello **расписания** плитки приветствия tooopen **расписания** колонку.
3. Щелкните имя hello стоечный модуль подробности расписания tooopen hello.
4. Изменение **включено** слишком**нет**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable расписания с помощью Windows PowerShell
Можно использовать hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) командлет toochange hello свойства существующего расписания для классического runbook или [AzureRmAutomationSchedule набор](https://msdn.microsoft.com/library/mt603566.aspx) командлета для модулей Runbook в hello Azure портал. toodisable hello план, укажите **false** для hello **IsEnabled** параметра.

Hello следующие примеры команд показывают, как toodisable расписанию с помощью hello командлет управления службами Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

Hello следующем образце команд Показать как toodisable расписание для runbook, с помощью командлета диспетчера ресурсов Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о работе с отчетами, в разделе [активы расписания в службе автоматизации Azure](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* tooget к работе с модулями Runbook в автоматизации Azure в разделе [запуск Runbook в автоматизации Azure](automation-starting-a-runbook.md) 

