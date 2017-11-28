---
title: "Планирование запуска модуля Runbook в службе автоматизации Azure | Документация Майкрософт"
description: "Рассматривается создание расписания в службе автоматизации Azure, которое позволяет запускать модуль Runbook однократно или несколько раз в определенное время."
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
ms.openlocfilehash: 52f1d55f141bb1b3948e3b7039cfc131a5e407b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="7c509-103">Создание расписания для Runbook в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="7c509-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="7c509-104">Чтобы запускать модуль Runbook в определенное время с помощью расписания в службе автоматизации Azure, его необходимо привязать к одному или нескольким расписаниям.</span><span class="sxs-lookup"><span data-stu-id="7c509-104">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span></span> <span data-ttu-id="7c509-105">На классическом портале Azure вы можете настроить расписание для однократного, ежечасного или ежедневного выполнения модулей Runbook. На портале Azure, кроме того, можно запланировать выполнение еженедельно, ежемесячно, в конкретные дни недели или месяца, а также в определенный день месяца.</span><span class="sxs-lookup"><span data-stu-id="7c509-105">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can additionally schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span></span>  <span data-ttu-id="7c509-106">Один модуль Runbook может быть связан с несколькими расписаниями, и одно расписание может иметь несколько привязанных модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="7c509-106">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="7c509-107">Создание расписания</span><span class="sxs-lookup"><span data-stu-id="7c509-107">Creating a schedule</span></span>
<span data-ttu-id="7c509-108">Новое расписание для модулей Runbook вы можете создать на портале Azure, на классическом портале Azure или с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c509-108">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="7c509-109">Также расписание можно создать при связывании Runbook с расписанием с помощью портала Azure или классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7c509-109">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="7c509-110">При связывании расписания с модулем Runbook служба автоматизации сохраняет текущие версии модулей в вашей учетной записи и связывает их с данным расписанием.</span><span class="sxs-lookup"><span data-stu-id="7c509-110">When you associate a schedule with a runbook, Automation stores the current versions of the modules in your account and links them to that schedule.</span></span>  <span data-ttu-id="7c509-111">Это означает, что если при создании расписания в вашей учетной записи был модуль версии 1.0, и затем этот модуль был обновлен до версии 2.0, то расписание по-прежнему будет использовать версию 1.0.</span><span class="sxs-lookup"><span data-stu-id="7c509-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update the module to version 2.0, the schedule will continue to use 1.0.</span></span>  <span data-ttu-id="7c509-112">Чтобы использовать обновленную версию модуля, необходимо создать новое расписание.</span><span class="sxs-lookup"><span data-stu-id="7c509-112">In order to use the updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a><span data-ttu-id="7c509-113">Создание нового расписания на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="7c509-113">To create a new schedule in the Azure classic portal</span></span>
1. <span data-ttu-id="7c509-114">На классическом портале Azure щелкните "Служба автоматизации", а затем выберите имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="7c509-114">In the Azure classic portal, select Automation and then then select the name of an automation account.</span></span>
2. <span data-ttu-id="7c509-115">Выберите вкладку **Средства** .</span><span class="sxs-lookup"><span data-stu-id="7c509-115">Select the **Assets** tab.</span></span>
3. <span data-ttu-id="7c509-116">Нажмите кнопку **Добавить параметр**в нижней части окна.</span><span class="sxs-lookup"><span data-stu-id="7c509-116">At the bottom of the window, click **Add Setting**.</span></span>
4. <span data-ttu-id="7c509-117">Щелкните **Добавить расписание**.</span><span class="sxs-lookup"><span data-stu-id="7c509-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="7c509-118">Введите **имя** и при желании **описание** нового расписания. Расписание может выполняться **однократно**, **ежечасно**, **ежедневно**, **еженедельно** или **ежемесячно**.</span><span class="sxs-lookup"><span data-stu-id="7c509-118">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="7c509-119">Укажите **Время начала** и другие параметры в зависимости от типа выбранного расписания.</span><span class="sxs-lookup"><span data-stu-id="7c509-119">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span></span>

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a><span data-ttu-id="7c509-120">Создание нового расписания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="7c509-120">To create a new schedule in the Azure portal</span></span>
1. <span data-ttu-id="7c509-121">На портале Azure из учетной записи службы автоматизации щелкните элемент **Ресурсы**, чтобы открыть колонку **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="7c509-121">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="7c509-122">Щелкните элемент **Расписания**, чтобы открыть колонку **Расписания**.</span><span class="sxs-lookup"><span data-stu-id="7c509-122">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="7c509-123">Щелкните **Добавить расписание** в верхней части этой колонки.</span><span class="sxs-lookup"><span data-stu-id="7c509-123">Click **Add a schedule** at the top of the blade.</span></span>
4. <span data-ttu-id="7c509-124">В колонке **Новое расписание** введите **имя** и при желании **описание** нового расписания.</span><span class="sxs-lookup"><span data-stu-id="7c509-124">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span></span>
5. <span data-ttu-id="7c509-125">Выберите режим выполнения расписания: **Однократно** или **Повторение**.</span><span class="sxs-lookup"><span data-stu-id="7c509-125">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="7c509-126">Если вы выбрали режим **Однократно**, то укажите **время начала** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7c509-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="7c509-127">Если вы выбрали режим **Повторение**, то укажите **время начала** и частоту повторений для модуля Runbook: каждый **час**, **день**, **неделю** или **месяц**.</span><span class="sxs-lookup"><span data-stu-id="7c509-127">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="7c509-128">Если в этом раскрывающемся списке вы выбрали **неделю** или **месяц**, то в колонке появится элемент **Recurrence option** (Параметры периодичности). Щелкнув его, вы откроете колонку **Recurrence option** (Параметры периодичности). Здесь вы сможете выбрать день недели, если ранее выбрали параметр **неделя**.</span><span class="sxs-lookup"><span data-stu-id="7c509-128">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span></span>  <span data-ttu-id="7c509-129">Если же вы выбрали параметр **месяц**, то здесь сможете выбрать **дни недели** или конкретные дни месяца из календаря, а также указать, будет ли модуль выполняться в последний день месяца. Завершив настройку, нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c509-129">If you selected **month**, you can choose by **week days** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span></span>   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="7c509-130">Создание расписания с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c509-130">To create a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="7c509-131">В службе автоматизации Azure вы можете использовать командлет [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx), чтобы создать новое расписание для классических модулей Runbook, или командлет [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx), чтобы создать расписание для модулей Runbook на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7c509-131">You can use the [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="7c509-132">Укажите для расписания время начала и частоту выполнения.</span><span class="sxs-lookup"><span data-stu-id="7c509-132">You must specify the start time for the schedule and the frequency it should run.</span></span>

<span data-ttu-id="7c509-133">Приведенные ниже примеры команд демонстрируют, как с помощью командлета управления службами Azure создать новое расписание, которое будет запускаться каждый день в 15:30 начиная с 20 января 2015 г.</span><span class="sxs-lookup"><span data-stu-id="7c509-133">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="7c509-134">Приведенные ниже примеры команд демонстрируют, как с помощью командлета Azure Resource Manager создать расписание для запуска в 15-й и 30-й день каждого месяца.</span><span class="sxs-lookup"><span data-stu-id="7c509-134">The following sample commands shows how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a><span data-ttu-id="7c509-135">Связывание расписания с модулем Runbook</span><span class="sxs-lookup"><span data-stu-id="7c509-135">Linking a schedule to a runbook</span></span>
<span data-ttu-id="7c509-136">Один модуль Runbook может быть связан с несколькими расписаниями, и одно расписание может иметь несколько привязанных модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="7c509-136">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span> <span data-ttu-id="7c509-137">Если Runbook имеет параметры, для них можно указать значения.</span><span class="sxs-lookup"><span data-stu-id="7c509-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="7c509-138">Необходимо предоставить значения для всех обязательных параметров, а также значения для необязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="7c509-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="7c509-139">Значения будут применяться каждый раз при запуске модуля Runbook с помощью расписания.</span><span class="sxs-lookup"><span data-stu-id="7c509-139">These values will be used each time the runbook is started by this schedule.</span></span>  <span data-ttu-id="7c509-140">Один и тот же модуль Runbook можно привязать к другому расписанию и указать другие значения параметров.</span><span class="sxs-lookup"><span data-stu-id="7c509-140">You can attach the same runbook to another schedule and specify different parameter values.</span></span>

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="7c509-141">Связывание расписания с модулем Runbook с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="7c509-141">To link a schedule to a runbook with the Azure classic portal</span></span>
1. <span data-ttu-id="7c509-142">На классическом портале Azure щелкните **Служба автоматизации** , а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="7c509-142">In the Azure classic portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="7c509-143">Выберите вкладку **Модули Runbook** .</span><span class="sxs-lookup"><span data-stu-id="7c509-143">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="7c509-144">Щелкните имя одного модуля Runbook для привязки к расписанию.</span><span class="sxs-lookup"><span data-stu-id="7c509-144">Click on the name of the runbook to schedule.</span></span>
4. <span data-ttu-id="7c509-145">Перейдите на вкладку **Расписание** .</span><span class="sxs-lookup"><span data-stu-id="7c509-145">Click the **Schedule** tab.</span></span>
5. <span data-ttu-id="7c509-146">Если модуль Runbook в настоящее время не связан с расписанием, будет предоставлена возможность выбрать **ссылку на новое расписание** или **ссылку на существующее расписание**.</span><span class="sxs-lookup"><span data-stu-id="7c509-146">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span></span>  <span data-ttu-id="7c509-147">Если модуль в настоящее время связан с расписанием, щелкните **Ссылки** в нижней части окна для доступа к этим параметрам.</span><span class="sxs-lookup"><span data-stu-id="7c509-147">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span></span>
6. <span data-ttu-id="7c509-148">Если модуль Runbook имеет параметры, их необходимо будет заполнить.</span><span class="sxs-lookup"><span data-stu-id="7c509-148">If the runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a><span data-ttu-id="7c509-149">Связывание расписания с модулем Runbook с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="7c509-149">To link a schedule to a runbook with the Azure portal</span></span>
1. <span data-ttu-id="7c509-150">На портале Azure из учетной записи службы автоматизации щелкните элемент **Модули Runbook**, чтобы открыть колонку **Модули Runbook**.</span><span class="sxs-lookup"><span data-stu-id="7c509-150">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="7c509-151">Щелкните имя одного модуля Runbook для привязки к расписанию.</span><span class="sxs-lookup"><span data-stu-id="7c509-151">Click on the name of the runbook to schedule.</span></span>
3. <span data-ttu-id="7c509-152">Если модуль Runbook сейчас не связан с расписанием, вы сможете создать новое расписание или связать модуль с существующим расписанием.</span><span class="sxs-lookup"><span data-stu-id="7c509-152">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span></span>  
4. <span data-ttu-id="7c509-153">Если модуль Runbook имеет параметры, следует выбрать действие **Изменить параметры запуска (по умолчанию: Azure)**, чтобы открыть колонку **Параметры**, где вы сможете ввести нужные данные.</span><span class="sxs-lookup"><span data-stu-id="7c509-153">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a><span data-ttu-id="7c509-154">Связывание расписания с модулем Runbook с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c509-154">To link a schedule to a runbook with Windows PowerShell</span></span>
<span data-ttu-id="7c509-155">Вы можете использовать командлет [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx), чтобы связать расписание с классическим модулем Runbook, или командлет [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) для модулей Runbook на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7c509-155">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in the Azure portal.</span></span>  <span data-ttu-id="7c509-156">С помощью параметра "Параметры" можно указать значения параметров для модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="7c509-156">You can specify values for the runbook’s parameters with the Parameters parameter.</span></span> <span data-ttu-id="7c509-157">Дополнительные сведения об указании значений параметров см. в разделе [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7c509-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="7c509-158">Приведенные ниже примеры команд демонстрируют, как связать расписание, используя командлет управления службами Azure с параметрами.</span><span class="sxs-lookup"><span data-stu-id="7c509-158">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="7c509-159">Приведенные ниже примеры команд демонстрируют, как связать расписание с модулем Runbook, используя командлет управления службами Azure с параметрами.</span><span class="sxs-lookup"><span data-stu-id="7c509-159">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="7c509-160">Отключение расписания</span><span class="sxs-lookup"><span data-stu-id="7c509-160">Disabling a schedule</span></span>
<span data-ttu-id="7c509-161">Если расписание отключено, модули Runbook, связанные с ним, больше не будут запускаться по такому расписанию.</span><span class="sxs-lookup"><span data-stu-id="7c509-161">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span></span> <span data-ttu-id="7c509-162">Можно отключить расписание вручную или указать срок действия при создании периодических расписаний.</span><span class="sxs-lookup"><span data-stu-id="7c509-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="7c509-163">При достижении срока действия расписания будут отключены.</span><span class="sxs-lookup"><span data-stu-id="7c509-163">When the expiration time is reached, the schedule will be disabled.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a><span data-ttu-id="7c509-164">Отключение расписание на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="7c509-164">To disable a schedule from the Azure classic portal</span></span>
<span data-ttu-id="7c509-165">Отключить расписание на классическом портале Azure можно на странице "Сведения о расписании" для соответствующего расписания.</span><span class="sxs-lookup"><span data-stu-id="7c509-165">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span></span>

1. <span data-ttu-id="7c509-166">На классическом портале Azure щелкните "Служба автоматизации", а затем — имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="7c509-166">In the Azure classic portal, select Automation and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="7c509-167">Перейдите на вкладку "Средства".</span><span class="sxs-lookup"><span data-stu-id="7c509-167">Select the Assets tab.</span></span>
3. <span data-ttu-id="7c509-168">Щелкните имя расписания и откройте страницу со сведениями о нем.</span><span class="sxs-lookup"><span data-stu-id="7c509-168">Click the name of a schedule to open its detail page.</span></span>
4. <span data-ttu-id="7c509-169">Задайте значение **Нет** для параметра **Включено**.</span><span class="sxs-lookup"><span data-stu-id="7c509-169">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-portal"></a><span data-ttu-id="7c509-170">Отключение расписания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="7c509-170">To disable a schedule from the Azure portal</span></span>
1. <span data-ttu-id="7c509-171">На портале Azure из учетной записи службы автоматизации щелкните элемент **Ресурсы**, чтобы открыть колонку **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="7c509-171">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="7c509-172">Щелкните элемент **Расписания**, чтобы открыть колонку **Расписания**.</span><span class="sxs-lookup"><span data-stu-id="7c509-172">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="7c509-173">Щелкните имя расписания и откройте колонку со сведениями о нем.</span><span class="sxs-lookup"><span data-stu-id="7c509-173">Click the name of a schedule to open the details blade.</span></span>
4. <span data-ttu-id="7c509-174">Задайте значение **Нет** для параметра **Включено**.</span><span class="sxs-lookup"><span data-stu-id="7c509-174">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-with-windows-powershell"></a><span data-ttu-id="7c509-175">Отключение расписания с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c509-175">To disable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="7c509-176">В службе автоматизации Azure вы можете использовать командлет [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx), чтобы изменить свойства существующего расписания для классического модуля Runbook, или командлет [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx), чтобы изменить расписание для модулей Runbook на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7c509-176">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="7c509-177">Чтобы отключить расписание, задайте значение **False** для параметра **IsEnabled**.</span><span class="sxs-lookup"><span data-stu-id="7c509-177">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span></span>

<span data-ttu-id="7c509-178">Приведенные ниже примеры команд демонстрируют, как отключить расписание, используя командлет управления службами Azure.</span><span class="sxs-lookup"><span data-stu-id="7c509-178">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="7c509-179">Приведенные ниже примеры команд демонстрируют, как отключить расписание для Runbook, используя командлет Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c509-179">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="7c509-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c509-180">Next steps</span></span>
* <span data-ttu-id="7c509-181">Дополнительные сведения о работе с расписаниями см. в статье [Расписания в службе автоматизации Azure](http://msdn.microsoft.com/library/azure/dn940016.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c509-181">To learn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="7c509-182">Сведения о том, как начать работу с модулями Runbook в службе автоматизации Azure, см. в статье [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7c509-182">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 

