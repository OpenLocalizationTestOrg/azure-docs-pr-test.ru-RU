---
title: "Сбор данных для Log Analytics с использованием модуля runbook в службе автоматизации Azure | Документация Майкрософт"
description: "Пошаговое руководство по созданию модуля runbook в службе автоматизации Azure для сбора данных в репозитории OMS и анализа с помощью Log Analytics."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="803b3-103">Сбор данных в Log Analytics с использованием модуля runbook в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="803b3-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="803b3-104">В Log Analytics можно собрать значительный объем данных из различных источников, включая [источники данных](../log-analytics/log-analytics-data-sources.md) в агентах и [данные, собранные в Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="803b3-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="803b3-105">Но иногда требуется собирать данные, недоступные в этих стандартных источниках.</span><span class="sxs-lookup"><span data-stu-id="803b3-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="803b3-106">В таких случаях вы можете использовать [API сборщика данных HTTP](../log-analytics/log-analytics-data-collector-api.md), чтобы записать данные в Log Analytics из любого клиента REST API.</span><span class="sxs-lookup"><span data-stu-id="803b3-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="803b3-107">Чаще всего такие данные собираются с помощью модулей runbook в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="803b3-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="803b3-108">В этом руководстве описан пошаговый процесс создания модуля runbook и расписания для него в службе автоматизации Azure, позволяющий записывать данные в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="803b3-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="803b3-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="803b3-109">Prerequisites</span></span>
<span data-ttu-id="803b3-110">Для выполнения этого сценария нужно настроить в подписке Azure указанные ниже ресурсы.</span><span class="sxs-lookup"><span data-stu-id="803b3-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="803b3-111">Их можно использовать с бесплатной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="803b3-111">Both can be a free account.</span></span>

- <span data-ttu-id="803b3-112">[Рабочая область Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="803b3-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="803b3-113">[Учетная запись службы автоматизации Azure](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="803b3-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="803b3-114">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="803b3-114">Overview of scenario</span></span>
<span data-ttu-id="803b3-115">В этом руководстве вы создадите модуль runbook, который собирает сведения о заданиях службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="803b3-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="803b3-116">Модули runbook в службе автоматизации Azure реализуются с помощью PowerShell, поэтому начнем с написания и тестирования скрипта в редакторе службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="803b3-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="803b3-117">Убедившись, что вы собрали необходимые сведения, запишите эти данные в Log Analytics и проверьте тип пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="803b3-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="803b3-118">В завершение создайте расписание для запуска модуля runbook через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="803b3-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="803b3-119">Службу автоматизации Azure можно настроить таким образом, чтобы сведения о задании отправлялись в Log Analytics без этого модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="803b3-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="803b3-120">Этот сценарий в основном используется для работы с руководством. Рекомендуем отправлять данные в тестовую рабочую область.</span><span class="sxs-lookup"><span data-stu-id="803b3-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="803b3-121">1. Установка модуля API сборщика данных</span><span class="sxs-lookup"><span data-stu-id="803b3-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="803b3-122">Каждый [запрос от API сборщика данных HTTP](../log-analytics/log-analytics-data-collector-api.md#create-a-request) должен быть правильно отформатирован и содержать заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="803b3-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="803b3-123">Это можно сделать в модуле runbook, но вы можете уменьшить объем требуемого кода с помощью модуля, упрощающего процесс.</span><span class="sxs-lookup"><span data-stu-id="803b3-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="803b3-124">Один из модулей, которые можно использовать, — это [модуль OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI) в коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="803b3-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="803b3-125">Чтобы использовать [модуль](../automation/automation-integration-modules.md) в runbook, установите его в своей учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="803b3-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="803b3-126">После этого любой модуль runbook в той же учетной записи сможет использовать функции из модуля.</span><span class="sxs-lookup"><span data-stu-id="803b3-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="803b3-127">Вы можете установить новый модуль, последовательно выбрав в своей учетной записи службы автоматизации **Ресурсы** > **Модули** > **Добавить модуль**.</span><span class="sxs-lookup"><span data-stu-id="803b3-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="803b3-128">Кроме того, коллекция PowerShell позволяет быстро развернуть модуль непосредственно в учетной записи службы автоматизации. Воспользуемся этой возможностью для работы с нашим руководством.</span><span class="sxs-lookup"><span data-stu-id="803b3-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![Модуль OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="803b3-130">Перейдите к [коллекции PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="803b3-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="803b3-131">Введите в строке поиска **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="803b3-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="803b3-132">Нажмите кнопку **Deploy to Azure Automation** (Развертывание в службе автоматизации Azure).</span><span class="sxs-lookup"><span data-stu-id="803b3-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="803b3-133">Выберите учетную запись службы автоматизации и нажмите кнопку **ОК**, чтобы установить модуль.</span><span class="sxs-lookup"><span data-stu-id="803b3-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="803b3-134">2) Создание переменных службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="803b3-134">2. Create Automation variables</span></span>
<span data-ttu-id="803b3-135">[Переменные службы автоматизации](..\automation\automation-variables.md) содержат значения, которые могут использоваться всеми модулями runbook в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="803b3-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="803b3-136">Вы можете изменить эти значения, не изменяя сам модуль runbook, чтобы повысить его гибкость.</span><span class="sxs-lookup"><span data-stu-id="803b3-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="803b3-137">Для каждого запроса API сборщика данных HTTP требуется идентификатор и ключ рабочей области OMS, а ресурсы переменных отлично подходят для хранения таких данных.</span><span class="sxs-lookup"><span data-stu-id="803b3-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Переменные](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="803b3-139">На портале Azure перейдите к учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="803b3-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="803b3-140">Выберите **Переменные** в разделе **Общие ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="803b3-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="803b3-141">Щелкните **Добавить переменную** и создайте две переменные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="803b3-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="803b3-142">Свойство</span><span class="sxs-lookup"><span data-stu-id="803b3-142">Property</span></span> | <span data-ttu-id="803b3-143">Значение идентификатора рабочей области</span><span class="sxs-lookup"><span data-stu-id="803b3-143">Workspace ID Value</span></span> | <span data-ttu-id="803b3-144">Значение ключа рабочей области</span><span class="sxs-lookup"><span data-stu-id="803b3-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="803b3-145">Имя</span><span class="sxs-lookup"><span data-stu-id="803b3-145">Name</span></span> | <span data-ttu-id="803b3-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="803b3-146">WorkspaceId</span></span> | <span data-ttu-id="803b3-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="803b3-147">WorkspaceKey</span></span> |
| <span data-ttu-id="803b3-148">Тип</span><span class="sxs-lookup"><span data-stu-id="803b3-148">Type</span></span> | <span data-ttu-id="803b3-149">Строка</span><span class="sxs-lookup"><span data-stu-id="803b3-149">String</span></span> | <span data-ttu-id="803b3-150">Строка</span><span class="sxs-lookup"><span data-stu-id="803b3-150">String</span></span> |
| <span data-ttu-id="803b3-151">Значение</span><span class="sxs-lookup"><span data-stu-id="803b3-151">Value</span></span> | <span data-ttu-id="803b3-152">Вставьте идентификатор рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="803b3-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="803b3-153">Вставьте первичный или вторичный ключ рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="803b3-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="803b3-154">зашифрованные;</span><span class="sxs-lookup"><span data-stu-id="803b3-154">Encrypted</span></span> | <span data-ttu-id="803b3-155">Нет</span><span class="sxs-lookup"><span data-stu-id="803b3-155">No</span></span> | <span data-ttu-id="803b3-156">Да</span><span class="sxs-lookup"><span data-stu-id="803b3-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="803b3-157">3. Создание модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="803b3-157">3. Create runbook</span></span>

<span data-ttu-id="803b3-158">На портале для службы автоматизации Azure предусмотрен редактор, с помощью которого можно изменять и тестировать модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="803b3-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="803b3-159">Вы можете использовать редактор скриптов для [работы непосредственно с PowerShell](../automation/automation-edit-textual-runbook.md) или [создать графический модуль runbook](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="803b3-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="803b3-160">В этом руководстве мы будем работать со скриптом PowerShell.</span><span class="sxs-lookup"><span data-stu-id="803b3-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Изменение модуля runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="803b3-162">Перейдите к учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="803b3-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="803b3-163">Щелкните **Модули Runbook** > **Добавить Runbook** > **Создание нового модуля Runbook**.</span><span class="sxs-lookup"><span data-stu-id="803b3-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="803b3-164">В качестве имени модуля runbook введите **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="803b3-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="803b3-165">Для типа runbook выберите значение **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="803b3-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="803b3-166">Щелкните **Создать**, чтобы создать модуль runbook и запустить текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="803b3-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="803b3-167">Скопируйте приведенный ниже код и вставьте его в модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="803b3-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="803b3-168">См. комментарии в скрипте для объяснения кода.</span><span class="sxs-lookup"><span data-stu-id="803b3-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="803b3-169">4. Тестирование модуля runbook</span><span class="sxs-lookup"><span data-stu-id="803b3-169">4. Test runbook</span></span>
<span data-ttu-id="803b3-170">Служба автоматизации Azure содержит среду для [тестирования модуля runbook](../automation/automation-testing-runbook.md) перед публикацией.</span><span class="sxs-lookup"><span data-stu-id="803b3-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="803b3-171">Можно проверить данные, собранные модулем runbook, и убедиться, что он надлежащим образом записывает их в Log Analytics перед публикацией в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="803b3-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Тестирование модуля runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="803b3-173">Нажмите кнопку **Сохранить**, чтобы сохранить модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="803b3-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="803b3-174">Щелкните **Область тестирования**, чтобы открыть runbook в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="803b3-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="803b3-175">Когда в модуле runbook станут доступны параметры, для них будет предложено ввести значения.</span><span class="sxs-lookup"><span data-stu-id="803b3-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="803b3-176">Введите имя группы ресурсов и учетной записи службы автоматизации, из которых вы будете собирать сведения о задании.</span><span class="sxs-lookup"><span data-stu-id="803b3-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="803b3-177">Щелкните **Пуск**, чтобы запустить модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="803b3-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="803b3-178">Модуль runbook запустится с состоянием **В очереди**, а затем перейдет в состояние **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="803b3-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="803b3-179">Для модуля runbook должны отображаться подробные выходные данные с собранными заданиями в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="803b3-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="803b3-180">Если в списке нет заданий, возможно, за последний час в учетной записи службы автоматизации задания не создавались.</span><span class="sxs-lookup"><span data-stu-id="803b3-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="803b3-181">Попробуйте запустить любой модуль runbook в учетной записи службы автоматизации и выполнить тестирование еще раз.</span><span class="sxs-lookup"><span data-stu-id="803b3-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="803b3-182">Убедитесь, что в выходных данных не отображаются сообщения об ошибках команды POST для Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="803b3-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="803b3-183">Должно появиться примерно такое сообщение:</span><span class="sxs-lookup"><span data-stu-id="803b3-183">You should have a message similar to the following.</span></span>

    ![Выходные данные POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="803b3-185">5. Проверка записей в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="803b3-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="803b3-186">Когда тестирование runbook будет завершено и вы убедитесь, что выходные данные получены успешно, можно проверить, созданы ли записи, с помощью [поиска по журналам в Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="803b3-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Выходные данные журналов](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="803b3-188">На портале Azure выберите рабочую область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="803b3-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="803b3-189">Щелкните **Поиск по журналам**.</span><span class="sxs-lookup"><span data-stu-id="803b3-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="803b3-190">Введите команду `Type=AutomationJob_CL` и нажмите кнопку поиска.</span><span class="sxs-lookup"><span data-stu-id="803b3-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="803b3-191">Обратите внимание, что тип записи включает суффикс _CL, не указанный в скрипте.</span><span class="sxs-lookup"><span data-stu-id="803b3-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="803b3-192">Этот суффикс автоматически добавляется в тип журнала, чтобы указать, что журнал пользовательский.</span><span class="sxs-lookup"><span data-stu-id="803b3-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="803b3-193">Должна отобразиться одна или несколько возвращенных записей. Это указывает на то, что модуль runbook работает правильно.</span><span class="sxs-lookup"><span data-stu-id="803b3-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="803b3-194">6. Публикация модуля runbook</span><span class="sxs-lookup"><span data-stu-id="803b3-194">6. Publish the runbook</span></span>
<span data-ttu-id="803b3-195">Убедившись, что модуль runbook работает правильно, необходимо опубликовать его, чтобы запустить в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="803b3-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="803b3-196">Вы можете и дальше изменять и тестировать модуль runbook без изменения опубликованной версии.</span><span class="sxs-lookup"><span data-stu-id="803b3-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Публикация модуля runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="803b3-198">Вернитесь к учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="803b3-198">Return to your automation account.</span></span>
2. <span data-ttu-id="803b3-199">Щелкните **Модули Runbook** и выберите **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="803b3-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="803b3-200">Щелкните **Правка** и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="803b3-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="803b3-201">Нажмите **Да** при запросе на подтверждение перезаписи для ранее опубликованной версии.</span><span class="sxs-lookup"><span data-stu-id="803b3-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="803b3-202">7. Настройка параметров ведения журнала</span><span class="sxs-lookup"><span data-stu-id="803b3-202">7. Set logging options</span></span> 
<span data-ttu-id="803b3-203">Для тестирования можно было просмотреть [подробные выходные данные](../automation/automation-runbook-output-and-messages.md#message-streams), так как в скрипте была задана переменная $VerbosePreference.</span><span class="sxs-lookup"><span data-stu-id="803b3-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="803b3-204">Если вы хотите просмотреть подробные выходные данные в рабочей среде, задайте для модуля runbook свойства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="803b3-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="803b3-205">Для модуля runbook, используемого в этом руководстве, отобразятся данные JSON, отправляемые в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="803b3-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Ведение журнала и трассировка](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="803b3-207">В окне свойств для модуля runbook выберите **Ведение журнала и трассировка** в разделе **Параметры Runbook**.</span><span class="sxs-lookup"><span data-stu-id="803b3-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="803b3-208">Задайте для параметра **Подробные записи в журнале** значение **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="803b3-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="803b3-209">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="803b3-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="803b3-210">8. Создание расписания для модуля runbook</span><span class="sxs-lookup"><span data-stu-id="803b3-210">8. Schedule runbook</span></span>
<span data-ttu-id="803b3-211">Наиболее распространенным способом запуска модуля runbook, который собирает данные мониторинга, является автоматический запуск по расписанию.</span><span class="sxs-lookup"><span data-stu-id="803b3-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="803b3-212">Для этого создайте [расписание в службе автоматизации Azure](../automation/automation-schedules.md) и подключите его к модулю runbook.</span><span class="sxs-lookup"><span data-stu-id="803b3-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Создание расписания для модуля runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="803b3-214">В окне свойств модуля runbook выберите **Расписания** в разделе **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="803b3-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="803b3-215">Последовательно выберите **Добавить расписание** > **Связать расписание с модулем Runbook** > **Создать новое расписание**.</span><span class="sxs-lookup"><span data-stu-id="803b3-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="803b3-216">Введите указанные ниже значения для расписания и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="803b3-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="803b3-217">Свойство</span><span class="sxs-lookup"><span data-stu-id="803b3-217">Property</span></span> | <span data-ttu-id="803b3-218">Значение</span><span class="sxs-lookup"><span data-stu-id="803b3-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="803b3-219">Имя</span><span class="sxs-lookup"><span data-stu-id="803b3-219">Name</span></span> | <span data-ttu-id="803b3-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="803b3-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="803b3-221">Запуск</span><span class="sxs-lookup"><span data-stu-id="803b3-221">Starts</span></span> | <span data-ttu-id="803b3-222">Выберите любое время как минимум на 5 минут позже текущего.</span><span class="sxs-lookup"><span data-stu-id="803b3-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="803b3-223">Периодичность</span><span class="sxs-lookup"><span data-stu-id="803b3-223">Recurrence</span></span> | <span data-ttu-id="803b3-224">Повторение</span><span class="sxs-lookup"><span data-stu-id="803b3-224">Recurring</span></span> |
| <span data-ttu-id="803b3-225">Повторять каждые</span><span class="sxs-lookup"><span data-stu-id="803b3-225">Recur every</span></span> | <span data-ttu-id="803b3-226">1 час</span><span class="sxs-lookup"><span data-stu-id="803b3-226">1 hour</span></span> |
| <span data-ttu-id="803b3-227">Срок действия</span><span class="sxs-lookup"><span data-stu-id="803b3-227">Set expiration</span></span> | <span data-ttu-id="803b3-228">Нет</span><span class="sxs-lookup"><span data-stu-id="803b3-228">No</span></span> |

<span data-ttu-id="803b3-229">Создав расписание, задайте значения параметров, которые будут использоваться при каждом запуске модуля runbook по этому расписанию.</span><span class="sxs-lookup"><span data-stu-id="803b3-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="803b3-230">Щелкните **Настройка параметров и настроек запуска**.</span><span class="sxs-lookup"><span data-stu-id="803b3-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="803b3-231">Укажите значения для **ResourceGroupName** и **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="803b3-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="803b3-232">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="803b3-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="803b3-233">9. Проверка запуска модуля runbook по расписанию</span><span class="sxs-lookup"><span data-stu-id="803b3-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="803b3-234">При каждом запуске модуля runbook [создается задание](../automation/automation-runbook-execution.md), и все выходные данные записываются в журнал.</span><span class="sxs-lookup"><span data-stu-id="803b3-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="803b3-235">Фактически это те же задания, которые собирает модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="803b3-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="803b3-236">Вы можете убедиться, что модуль runbook запускается правильно, проверив задания для него после момента запуска по расписанию.</span><span class="sxs-lookup"><span data-stu-id="803b3-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![Задания](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="803b3-238">В окне свойств модуля runbook выберите **Задания** в разделе **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="803b3-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="803b3-239">Для каждого запуска модуля runbook должен отображаться список заданий.</span><span class="sxs-lookup"><span data-stu-id="803b3-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="803b3-240">Щелкните одно из заданий, чтобы просмотреть сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="803b3-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="803b3-241">Щелкните **Все журналы**, чтобы просмотреть журналы и выходные данные модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="803b3-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="803b3-242">Прокрутите вниз, чтобы найти запись, как на изображении ниже.</span><span class="sxs-lookup"><span data-stu-id="803b3-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Подробная информация](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="803b3-244">Щелкните эту запись для просмотра подробных данных JSON, отправленных в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="803b3-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="803b3-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="803b3-245">Next steps</span></span>
- <span data-ttu-id="803b3-246">При помощи [конструктора представлений](../log-analytics/log-analytics-view-designer.md) создайте представление с данными, собранными в репозитории Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="803b3-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="803b3-247">Поместите модуль runbook в пакет [решения по управлению](operations-management-suite-solutions-creating.md), чтобы можно было распространять его среди заказчиков.</span><span class="sxs-lookup"><span data-stu-id="803b3-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="803b3-248">Дополнительные сведения о [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="803b3-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="803b3-249">Дополнительные сведения о [службе автоматизации Azure](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="803b3-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="803b3-250">Дополнительные сведения об [API сборщика данных HTTP](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="803b3-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>