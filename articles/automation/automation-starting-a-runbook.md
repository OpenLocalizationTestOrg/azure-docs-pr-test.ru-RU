---
title: "aaaStarting runbook в автоматизации Azure | Документы Microsoft"
description: "Обобщает hello различные методы, которые можно использовать toostart runbook в автоматизации Azure и предоставляет сведения об использовании обоих hello портал Azure и Windows PowerShell."
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
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="dcd4b-103">Запуск модуля Runbook в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="dcd4b-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="dcd4b-104">в следующей таблице Hello помогают определить hello метод toostart runbook в автоматизации Azure, наиболее подходящий tooyour определенного сценария.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="dcd4b-105">Эта статья содержит сведения о запуске модуля runbook с hello портал Azure и Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="dcd4b-106">Подробные сведения на hello другие методы предоставляются в другую документацию, можно получить доступ из приведенные ниже ссылки hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="dcd4b-107">**МЕТОД**</span><span class="sxs-lookup"><span data-stu-id="dcd4b-107">**METHOD**</span></span> | <span data-ttu-id="dcd4b-108">**ХАРАКТЕРИСТИКИ**</span><span class="sxs-lookup"><span data-stu-id="dcd4b-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="dcd4b-109">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="dcd4b-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="dcd4b-110">Простейший способ с интерактивным пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="dcd4b-111">Значения параметра простой tooprovide формы.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="dcd4b-112">Легко отслеживать состояние задания.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-112">Easily track job state.</span></span><br> <li><span data-ttu-id="dcd4b-113">Доступ с аутентификацией в Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="dcd4b-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcd4b-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="dcd4b-115">Вызов из командной строки с помощью командлетов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="dcd4b-116">Может быть добавлено в автоматическое решение, состоящее из нескольких шагов.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="dcd4b-117">Запрос проходит проверку подлинности с помощью сертификата или по протоколу OAuth.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="dcd4b-118">Необходимо предоставить значения простых и сложных параметров.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="dcd4b-119">Отслеживание состояния задания.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-119">Track job state.</span></span><br> <li><span data-ttu-id="dcd4b-120">Клиент требуется toosupport командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="dcd4b-121">API-интерфейс в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="dcd4b-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="dcd4b-122">Наиболее гибкий и наиболее сложный метод.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="dcd4b-123">Вызов из любого пользовательского кода, который может выполнять HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="dcd4b-124">Запрос проходит проверку подлинности с помощью сертификата или по протоколу OAuth.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="dcd4b-125">Необходимо предоставить значения простых и сложных параметров.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="dcd4b-126">Отслеживание состояния задания.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-126">Track job state.</span></span> |
| [<span data-ttu-id="dcd4b-127">Объекты Webhook</span><span class="sxs-lookup"><span data-stu-id="dcd4b-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="dcd4b-128">Запуск Runbook из одного HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="dcd4b-129">Проверка подлинности с помощью токена безопасности в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="dcd4b-130">Клиент не может переопределять значения параметров, указанные при создании Webhook.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="dcd4b-131">Runbook можно определить один параметр, который содержит сведения о запросе HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="dcd4b-132">Состояние задания отсутствует возможность tootrack через URL-адрес веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="dcd4b-133">Ответ tooAzure предупреждения</span><span class="sxs-lookup"><span data-stu-id="dcd4b-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="dcd4b-134">Запуск runbook в ответ tooAzure предупреждение.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="dcd4b-135">Настройка веб-перехватчика для runbook и связывать их tooalert.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="dcd4b-136">Проверка подлинности с помощью токена безопасности в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="dcd4b-137">Расписание</span><span class="sxs-lookup"><span data-stu-id="dcd4b-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="dcd4b-138">Автоматический запуск Runbook по ежечасному, ежедневному, еженедельному или ежемесячному расписанию.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="dcd4b-139">Управление расписанием с помощью портала Azure, командлетов PowerShell или API-интерфейса Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="dcd4b-140">Укажите параметр toobe значения, используемые вместе с расписанием.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="dcd4b-141">Из другого модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="dcd4b-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="dcd4b-142">Использование одного модуля Runbook в качестве процесса в другом модуле Runbook.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="dcd4b-143">Подходит для функций, используемых в нескольких модулях Runbook.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="dcd4b-144">Укажите runbook toochild значения параметра и использовать результаты в родительский модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="dcd4b-145">Hello следующем рисунке показан Подробное пошаговое описание жизненного цикла hello модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="dcd4b-146">Он включает в себя различные способы запуска модуля runbook в автоматизации Azure, компонентов, необходимых для Runbook службы автоматизации Azure tooexecute гибридной рабочей ролью Runbook и взаимодействие между разными компонентами.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="dcd4b-147">toolearn о выполнении модулей автоматизации Runbook в центре обработки данных, см. слишком[гибридных рабочих ролей runbook](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="dcd4b-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Архитектура Runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="dcd4b-149">Запуск модуля runbook с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="dcd4b-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="dcd4b-150">В hello портал Azure, выберите **автоматизации** и нажмите кнопку hello имя учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="dcd4b-151">Выберите меню концентратора hello **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="dcd4b-152">На hello **Runbooks** колонке выберите runbook и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="dcd4b-153">Если hello runbook имеет параметры, можно tooprovide запрашиваемые значения с текстовым полем для каждого параметра.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="dcd4b-154">Дополнительные сведения о параметрах см. в разделе [Параметры модуля Runbook](#Runbook-parameters) ниже.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="dcd4b-155">На hello **задания** колонки, можно просмотреть состояние задания runbook hello hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="dcd4b-156">Запуск модуля Runbook с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcd4b-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="dcd4b-157">Можно использовать hello [начала AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart runbook с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="dcd4b-158">Hello следующий пример кода запускает модуль runbook с именем Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="dcd4b-159">Возвращает AzureRmAutomationRunbook начала задания объекта, можно использовать tootrack его состояние после запуска hello runbook.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="dcd4b-160">Затем можно использовать этот объект задания с [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello состояние задания hello и [Get AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget свои выходные данные.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="dcd4b-161">Hello, следующий пример кода запускает модуль runbook с именем Test-Runbook, Ожидание его завершения, а затем отображает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="dcd4b-162">Если hello runbook требуются параметры, то необходимо указать их в виде [hashtable](http://technet.microsoft.com/library/hh847780.aspx) где ключ hello hello хэш-таблицы совпадает с именем hello и значением hello — значением параметра hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="dcd4b-163">Hello следующем примере показано, как toostart runbook с двумя строковыми параметрами с именем FirstName и LastName, целочисленным параметром repeatCount и логическим параметром show.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="dcd4b-164">Дополнительные сведения о параметрах см. в разделе [Параметры Runbook](#Runbook-parameters) ниже.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="dcd4b-165">Параметры модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="dcd4b-165">Runbook parameters</span></span>
<span data-ttu-id="dcd4b-166">При запуске модуля runbook из hello портала Azure или Windows PowerShell hello команда отправляется через веб-службы автоматизации Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="dcd4b-167">Эта служба не поддерживает параметры со сложными типами данных.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="dcd4b-168">Если требуется tooprovide значение для сложного параметра, то следует вызвать его из другого модуля runbook как описано в [дочерние модули Runbook в автоматизации Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="dcd4b-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="dcd4b-169">Hello веб-служба автоматизации Azure предоставляет специальные функции для параметров с помощью определенных типов данных, как описано в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="dcd4b-170">Именованные значения</span><span class="sxs-lookup"><span data-stu-id="dcd4b-170">Named values</span></span>
<span data-ttu-id="dcd4b-171">Если hello параметр имеет тип [object], то можно использовать hello после его список именованных значений toosend формат JSON: *{Name1: «Значение1», имя2: «Значение2», Имя3: значение «3»}*.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="dcd4b-172">Значения должны быть простого типа.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-172">These values must be simple types.</span></span> <span data-ttu-id="dcd4b-173">Hello модуль runbook получит параметр hello как [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) со свойствами, соответствующими tooeach с именем value.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="dcd4b-174">Рассмотрим следующий Тестовый модуль runbook, который принимает параметр с именем пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="dcd4b-175">Hello следующий текст может использоваться для параметра пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="dcd4b-176">Это приводит к hello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="dcd4b-177">Массивы</span><span class="sxs-lookup"><span data-stu-id="dcd4b-177">Arrays</span></span>
<span data-ttu-id="dcd4b-178">Если параметр hello представляет собой массив, например [array] или [string []], то можно использовать hello следующие toosend формат JSON его список значений: *[значение1, значение2, значение3]*.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="dcd4b-179">Значения должны быть простого типа.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-179">These values must be simple types.</span></span>

<span data-ttu-id="dcd4b-180">Рассмотрим следующий Тестовый модуль runbook, который принимает параметр с именем hello *пользователя*.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="dcd4b-181">Hello следующий текст может использоваться для параметра пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="dcd4b-182">Это приводит к hello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="dcd4b-183">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="dcd4b-183">Credentials</span></span>
<span data-ttu-id="dcd4b-184">Если тип данных параметра hello **PSCredential**, то можно указать имя hello объекта автоматизации Azure [актива учетных данных](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="dcd4b-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="dcd4b-185">Hello модуль runbook извлечет hello учетные данные с именем hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="dcd4b-186">Рассмотрим следующий Тестовый модуль runbook, который принимает параметр с именем учетных данных hello.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="dcd4b-187">Hello следующий текст можно использовать для параметра пользователя hello, при наличии актива учетных данных с именем *мои учетные данные*.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="dcd4b-188">Предполагается, что имя пользователя hello в учетных данных hello — *jsmith*, это приведет к hello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="dcd4b-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dcd4b-189">Next steps</span></span>
* <span data-ttu-id="dcd4b-190">Архитектура Hello runbook в текущей статьи предоставляет высокоуровневый обзор модулей Runbook управление ресурсами в Azure и локальными с hello гибридной рабочей ролью Runbook.</span><span class="sxs-lookup"><span data-stu-id="dcd4b-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="dcd4b-191">toolearn о выполнении модулей автоматизации Runbook в центре обработки данных, см. слишком[гибридных рабочих ролей Runbook](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="dcd4b-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="dcd4b-192">toolearn Дополнительные сведения о hello Создание toobe модульной модулей Runbook, использовать другие модули Runbook для конкретной или общие функции, см. слишком[дочерние модули Runbook](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="dcd4b-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

