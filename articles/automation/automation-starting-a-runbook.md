---
title: "Запуск модуля Runbook в службе автоматизации Azure | Документация Майкрософт"
description: "Кратко рассматриваются различные методы, которые позволяют запускать модуль Runbook в службе автоматизации Azure с помощью портала Azure и Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="c114b-103">Запуск модуля Runbook в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="c114b-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="c114b-104">Следующая таблица поможет определить метод для запуска модуля Runbook в службе автоматизации Azure, наиболее подходящий для конкретной ситуации.</span><span class="sxs-lookup"><span data-stu-id="c114b-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="c114b-105">Данная статья содержит сведения о запуске модуля Runbook с помощью портала Azure и Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c114b-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="c114b-106">Сведения об остальных методах приведены в другой документации, доступной по ссылкам, которые указаны ниже.</span><span class="sxs-lookup"><span data-stu-id="c114b-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="c114b-107">**МЕТОД**</span><span class="sxs-lookup"><span data-stu-id="c114b-107">**METHOD**</span></span> | <span data-ttu-id="c114b-108">**ХАРАКТЕРИСТИКИ**</span><span class="sxs-lookup"><span data-stu-id="c114b-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="c114b-109">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c114b-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="c114b-110">Простейший способ с интерактивным пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="c114b-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="c114b-111">Форма для предоставления значений простых параметров.</span><span class="sxs-lookup"><span data-stu-id="c114b-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="c114b-112">Легко отслеживать состояние задания.</span><span class="sxs-lookup"><span data-stu-id="c114b-112">Easily track job state.</span></span><br> <li><span data-ttu-id="c114b-113">Доступ с аутентификацией в Azure.</span><span class="sxs-lookup"><span data-stu-id="c114b-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="c114b-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c114b-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="c114b-115">Вызов из командной строки с помощью командлетов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c114b-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="c114b-116">Может быть добавлено в автоматическое решение, состоящее из нескольких шагов.</span><span class="sxs-lookup"><span data-stu-id="c114b-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="c114b-117">Запрос проходит проверку подлинности с помощью сертификата или по протоколу OAuth.</span><span class="sxs-lookup"><span data-stu-id="c114b-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="c114b-118">Необходимо предоставить значения простых и сложных параметров.</span><span class="sxs-lookup"><span data-stu-id="c114b-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="c114b-119">Отслеживание состояния задания.</span><span class="sxs-lookup"><span data-stu-id="c114b-119">Track job state.</span></span><br> <li><span data-ttu-id="c114b-120">Для поддержки командлетов PowerShell необходим клиент.</span><span class="sxs-lookup"><span data-stu-id="c114b-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="c114b-121">API-интерфейс в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="c114b-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="c114b-122">Наиболее гибкий и наиболее сложный метод.</span><span class="sxs-lookup"><span data-stu-id="c114b-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="c114b-123">Вызов из любого пользовательского кода, который может выполнять HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="c114b-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="c114b-124">Запрос проходит проверку подлинности с помощью сертификата или по протоколу OAuth.</span><span class="sxs-lookup"><span data-stu-id="c114b-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="c114b-125">Необходимо предоставить значения простых и сложных параметров.</span><span class="sxs-lookup"><span data-stu-id="c114b-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="c114b-126">Отслеживание состояния задания.</span><span class="sxs-lookup"><span data-stu-id="c114b-126">Track job state.</span></span> |
| [<span data-ttu-id="c114b-127">Объекты Webhook</span><span class="sxs-lookup"><span data-stu-id="c114b-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="c114b-128">Запуск Runbook из одного HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="c114b-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="c114b-129">Проверка подлинности с помощью токена безопасности в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="c114b-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="c114b-130">Клиент не может переопределять значения параметров, указанные при создании Webhook.</span><span class="sxs-lookup"><span data-stu-id="c114b-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="c114b-131">Runbook может определить один параметр, который содержит сведения об HTTP-запросе.</span><span class="sxs-lookup"><span data-stu-id="c114b-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="c114b-132">Отсутствует возможность отслеживать состояния задания через URL-адрес webhook.</span><span class="sxs-lookup"><span data-stu-id="c114b-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="c114b-133">Ответ на оповещение Azure</span><span class="sxs-lookup"><span data-stu-id="c114b-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="c114b-134">Запуск Runbook в ответ на оповещение Azure.</span><span class="sxs-lookup"><span data-stu-id="c114b-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="c114b-135">Настройка веб-перехватчика для Runbook и ссылки на оповещение.</span><span class="sxs-lookup"><span data-stu-id="c114b-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="c114b-136">Проверка подлинности с помощью токена безопасности в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="c114b-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="c114b-137">Расписание</span><span class="sxs-lookup"><span data-stu-id="c114b-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="c114b-138">Автоматический запуск Runbook по ежечасному, ежедневному, еженедельному или ежемесячному расписанию.</span><span class="sxs-lookup"><span data-stu-id="c114b-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="c114b-139">Управление расписанием с помощью портала Azure, командлетов PowerShell или API-интерфейса Azure.</span><span class="sxs-lookup"><span data-stu-id="c114b-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="c114b-140">Предоставление значений параметров, которые будут использованы в расписании.</span><span class="sxs-lookup"><span data-stu-id="c114b-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="c114b-141">Из другого модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="c114b-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="c114b-142">Использование одного модуля Runbook в качестве процесса в другом модуле Runbook.</span><span class="sxs-lookup"><span data-stu-id="c114b-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="c114b-143">Подходит для функций, используемых в нескольких модулях Runbook.</span><span class="sxs-lookup"><span data-stu-id="c114b-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="c114b-144">Предоставление значений параметров для дочернего модуля Runbook и использование выходных данных в родительском модуле Runbook.</span><span class="sxs-lookup"><span data-stu-id="c114b-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="c114b-145">На следующем рисунке показан подробный пошаговый процесс жизненного цикла модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="c114b-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="c114b-146">Он включает различные способы запуска модуля Runbook в службе автоматизации Azure, компоненты, необходимые для выполнения модулей Runbook для службы автоматизации Azure в гибридной рабочей роли, и взаимодействие между различными компонентами.</span><span class="sxs-lookup"><span data-stu-id="c114b-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="c114b-147">Дополнительные сведения о выполнении модулей Runbook службы автоматизации Azure в центре обработки данных см. в статье о [гибридных рабочих ролях Runbook](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="c114b-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Архитектура Runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="c114b-149">Запуск Runbook с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="c114b-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="c114b-150">На портале Azure щелкните **Служба автоматизации** и затем имя учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="c114b-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="c114b-151">В меню концентратора выберите **Модули Runbook**.</span><span class="sxs-lookup"><span data-stu-id="c114b-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="c114b-152">В колонке **Модули Runbook** выберите модуль runbook и щелкните **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="c114b-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="c114b-153">Если модуль Runbook имеет параметры, будет предложено предоставить значения в текстовом поле для каждого параметра.</span><span class="sxs-lookup"><span data-stu-id="c114b-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="c114b-154">Дополнительные сведения о параметрах см. в разделе [Параметры модуля Runbook](#Runbook-parameters) ниже.</span><span class="sxs-lookup"><span data-stu-id="c114b-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="c114b-155">В колонке **Задание** можно просмотреть состояние задания runbook.</span><span class="sxs-lookup"><span data-stu-id="c114b-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="c114b-156">Запуск модуля Runbook с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c114b-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="c114b-157">Чтобы запустить модуль Runbook с помощью Windows PowerShell, воспользуйтесь командлетом [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c114b-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="c114b-158">В следующем примере кода будет запущен модуль Runbook с именем Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="c114b-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="c114b-159">Командлет Start-AzureRmAutomationRunbook возвращает объект задания, который позволяет отслеживать его состояние после запуска.</span><span class="sxs-lookup"><span data-stu-id="c114b-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="c114b-160">Используйте командлет [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619440.aspx), чтобы определить состояние задания, и [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx), чтобы получить его выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c114b-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="c114b-161">В следующем примере кода будет запущен модуль Runbook с именем Test-Runbook и после его завершения выводится результат.</span><span class="sxs-lookup"><span data-stu-id="c114b-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="c114b-162">Если для модуля Runbook требуются параметры, то необходимо указать их в виде [хэш-таблицы](http://technet.microsoft.com/library/hh847780.aspx), где ключ в хэш-таблице совпадает с именем параметра, а значение — это значение параметра.</span><span class="sxs-lookup"><span data-stu-id="c114b-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="c114b-163">В следующем примере показано, как запустить модуль Runbook с двумя строковыми параметрами FirstName и LastName, целочисленным параметром RepeatCount и логическим параметром Show.</span><span class="sxs-lookup"><span data-stu-id="c114b-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="c114b-164">Дополнительные сведения о параметрах см. в разделе [Параметры Runbook](#Runbook-parameters) ниже.</span><span class="sxs-lookup"><span data-stu-id="c114b-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="c114b-165">Параметры модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="c114b-165">Runbook parameters</span></span>
<span data-ttu-id="c114b-166">При запуске модуля Runbook из портала управления Azure или Windows PowerShell инструкция отправляется через веб-службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="c114b-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="c114b-167">Эта служба не поддерживает параметры со сложными типами данных.</span><span class="sxs-lookup"><span data-stu-id="c114b-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="c114b-168">Если необходимо указать значение для сложного параметра, его необходимо вызвать из другого модуля Runbook, как описано в разделе [Дочерние модули Runbook в службе автоматизации Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="c114b-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="c114b-169">Веб-службы автоматизации Azure предоставляют специальные функции для параметров, которые используют определенные типы данных, как описано в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="c114b-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="c114b-170">Именованные значения</span><span class="sxs-lookup"><span data-stu-id="c114b-170">Named values</span></span>
<span data-ttu-id="c114b-171">Если параметр имеет тип данных [object], используйте следующий формат JSON, чтобы передать в параметр список именованных значений: *{имя1:'значение1', имя2:'значение2', имя3:'значение3'}*.</span><span class="sxs-lookup"><span data-stu-id="c114b-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="c114b-172">Значения должны быть простого типа.</span><span class="sxs-lookup"><span data-stu-id="c114b-172">These values must be simple types.</span></span> <span data-ttu-id="c114b-173">Модуль Runbook получает параметр в виде объекта [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) , у которого свойства соответствуют каждому именованному значению.</span><span class="sxs-lookup"><span data-stu-id="c114b-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="c114b-174">Рассмотрим следующий тестовый модуль Runbook, который принимает параметр user.</span><span class="sxs-lookup"><span data-stu-id="c114b-174">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="c114b-175">Для параметра user может быть использован следующий текст.</span><span class="sxs-lookup"><span data-stu-id="c114b-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="c114b-176">Результат должен быть следующим.</span><span class="sxs-lookup"><span data-stu-id="c114b-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="c114b-177">Массивы</span><span class="sxs-lookup"><span data-stu-id="c114b-177">Arrays</span></span>
<span data-ttu-id="c114b-178">Если параметр представляет собой массив ([array] или [string[]]), используйте следующий формат JSON, чтобы отправить его в виде списка значений: *[значение1,значение2,значение3]*.</span><span class="sxs-lookup"><span data-stu-id="c114b-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="c114b-179">Значения должны быть простого типа.</span><span class="sxs-lookup"><span data-stu-id="c114b-179">These values must be simple types.</span></span>

<span data-ttu-id="c114b-180">Рассмотрим следующий тестовый модуль Runbook, который принимает параметр *user*.</span><span class="sxs-lookup"><span data-stu-id="c114b-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="c114b-181">Для параметра user может быть использован следующий текст.</span><span class="sxs-lookup"><span data-stu-id="c114b-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="c114b-182">Результат должен быть следующим.</span><span class="sxs-lookup"><span data-stu-id="c114b-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="c114b-183">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="c114b-183">Credentials</span></span>
<span data-ttu-id="c114b-184">Если параметр относится к типу данных **PSCredential**, можно предоставить имя [учетных данных](automation-credentials.md)в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="c114b-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="c114b-185">Модуль Runbook получит учетную запись с указанным именем.</span><span class="sxs-lookup"><span data-stu-id="c114b-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="c114b-186">Рассмотрим следующий тестовый модуль Runbook, который принимает параметр credential.</span><span class="sxs-lookup"><span data-stu-id="c114b-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="c114b-187">Следующий текст можно использовать для параметра user, если используется учетная запись *My Credential*.</span><span class="sxs-lookup"><span data-stu-id="c114b-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="c114b-188">Если имя пользователя в параметре credential — *jsmith*, будет получен следующий результат.</span><span class="sxs-lookup"><span data-stu-id="c114b-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="c114b-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c114b-189">Next steps</span></span>
* <span data-ttu-id="c114b-190">В текущей статье описана общая архитектура Runbook для управления ресурсами в Azure и локальной среде с помощью гибридной рабочей роли Runbook.</span><span class="sxs-lookup"><span data-stu-id="c114b-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="c114b-191">Дополнительные сведения о выполнении модулей Runbook службы автоматизации Azure в центре обработки данных см. в статье о [гибридных рабочих ролях Runbook](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="c114b-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="c114b-192">Чтобы узнать больше о создании модульных Runbook, используемых другими модулями Runbook для выполнения конкретных или общих функций, ознакомьтесь с [дочерними модулями Runbook](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="c114b-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>

