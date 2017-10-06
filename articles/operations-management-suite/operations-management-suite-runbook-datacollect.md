---
title: "aaaCollecting данных аналитики журналов с runbook в автоматизации Azure | Документы Microsoft"
description: "Пошаговые руководства, проходит через создание модуля runbook в автоматизации Azure toocollect данные в репозиторий OMS hello для анализа службой аналитики журналов."
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
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="6a8fd-103">Сбор данных в Log Analytics с использованием модуля runbook в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="6a8fd-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="6a8fd-104">В Log Analytics можно собрать значительный объем данных из различных источников, включая [источники данных](../log-analytics/log-analytics-data-sources.md) в агентах и [данные, собранные в Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="6a8fd-105">Существуют сценарии, хотя которых требуется toocollect данных, не доступны через эти стандартные источники.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="6a8fd-106">В этих случаях можно использовать hello [HTTP API-Интерфейс сборщика данных](../log-analytics/log-analytics-data-collector-api.md) tooLog toowrite данных аналитики из любого клиента REST API.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="6a8fd-107">Общие tooperform метод runbook в службе автоматизации Azure использует эту коллекцию.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="6a8fd-108">Этого учебника вы научитесь hello процесс создания и планирования runbook в автоматизации Azure toowrite данных tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6a8fd-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6a8fd-109">Prerequisites</span></span>
<span data-ttu-id="6a8fd-110">Данный сценарий требует hello следующих ресурсов, настроенных в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="6a8fd-111">Их можно использовать с бесплатной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-111">Both can be a free account.</span></span>

- <span data-ttu-id="6a8fd-112">[Рабочая область Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="6a8fd-113">[Учетная запись службы автоматизации Azure](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="6a8fd-114">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="6a8fd-114">Overview of scenario</span></span>
<span data-ttu-id="6a8fd-115">В этом руководстве вы создадите модуль runbook, который собирает сведения о заданиях службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="6a8fd-116">Runbook в автоматизации Azure, реализуются с помощью PowerShell, поэтому начнем с создания и тестирования сценария в редактор Azure Automation hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="6a8fd-117">Убедившись, что собираются hello необходимые сведения, будет записывать, tooLog данных аналитики и проверять hello пользовательского типа данных.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="6a8fd-118">Наконец вы создадите расписание toostart hello runbook через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="6a8fd-119">Вы можете настроить службы автоматизации Azure toosend задания сведения tooLog Analytics без этого модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="6a8fd-120">Этот сценарий является главным образом используется toosupport учебника hello и рекомендуется отправлять hello данных tooa тестовой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="6a8fd-121">1. Установка модуля API сборщика данных</span><span class="sxs-lookup"><span data-stu-id="6a8fd-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="6a8fd-122">Каждый [запрос от hello HTTP API-Интерфейс сборщика данных](../log-analytics/log-analytics-data-collector-api.md#create-a-request) должен быть отформатирован должным образом и включать заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="6a8fd-123">Это можно сделать в модуле runbook, но могут снизить hello объем кода, необходимо с помощью модуля, который упрощает этот процесс.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="6a8fd-124">Один модуль, который можно использовать является [OMSIngestionAPI модуль](https://www.powershellgallery.com/packages/OMSIngestionAPI) в коллекции PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="6a8fd-125">toouse [модуль](../automation/automation-integration-modules.md) в модуле runbook, он должен быть установлен в вашей учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="6a8fd-126">Здравствуйте, любого модуля runbook в hello учетную запись можно использовать функции в модуле hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="6a8fd-127">Вы можете установить новый модуль, последовательно выбрав в своей учетной записи службы автоматизации **Ресурсы** > **Модули** > **Добавить модуль**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="6a8fd-128">Hello коллекции PowerShell хотя предоставляет быстрый параметр toodeploy модуля напрямую автоматизации tooyour учетной записи, поэтому этот параметр можно использовать для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![Модуль OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="6a8fd-130">Go слишком[коллекции PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="6a8fd-131">Введите в строке поиска **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="6a8fd-132">Щелкните hello **tooAzure автоматизации развертывания** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="6a8fd-133">Выберите учетную запись автоматизации и нажмите кнопку **ОК** tooinstall hello модуля.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="6a8fd-134">2. Создание переменных службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="6a8fd-134">2. Create Automation variables</span></span>
<span data-ttu-id="6a8fd-135">[Переменные службы автоматизации](..\automation\automation-variables.md) содержат значения, которые могут использоваться всеми модулями runbook в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="6a8fd-136">Они делают модулей Runbook, более гибкую, позволяя toochange эти значения, не изменяя hello фактическое runbook.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="6a8fd-137">Каждый запрос из hello HTTP API-Интерфейс сборщика данных требует hello идентификатор и ключ рабочей области OMS hello и ресурсы переменных являются идеальной toostore эти сведения.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![Переменные](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="6a8fd-139">В hello портал Azure перейдите tooyour учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="6a8fd-140">Выберите **Переменные** в разделе **Общие ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="6a8fd-141">Нажмите кнопку **добавить переменную** и создайте две переменные hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="6a8fd-142">Свойство</span><span class="sxs-lookup"><span data-stu-id="6a8fd-142">Property</span></span> | <span data-ttu-id="6a8fd-143">Значение идентификатора рабочей области</span><span class="sxs-lookup"><span data-stu-id="6a8fd-143">Workspace ID Value</span></span> | <span data-ttu-id="6a8fd-144">Значение ключа рабочей области</span><span class="sxs-lookup"><span data-stu-id="6a8fd-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="6a8fd-145">Имя</span><span class="sxs-lookup"><span data-stu-id="6a8fd-145">Name</span></span> | <span data-ttu-id="6a8fd-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="6a8fd-146">WorkspaceId</span></span> | <span data-ttu-id="6a8fd-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="6a8fd-147">WorkspaceKey</span></span> |
| <span data-ttu-id="6a8fd-148">Тип</span><span class="sxs-lookup"><span data-stu-id="6a8fd-148">Type</span></span> | <span data-ttu-id="6a8fd-149">Строка</span><span class="sxs-lookup"><span data-stu-id="6a8fd-149">String</span></span> | <span data-ttu-id="6a8fd-150">Строка</span><span class="sxs-lookup"><span data-stu-id="6a8fd-150">String</span></span> |
| <span data-ttu-id="6a8fd-151">Значение</span><span class="sxs-lookup"><span data-stu-id="6a8fd-151">Value</span></span> | <span data-ttu-id="6a8fd-152">Вставьте идентификатор рабочей области рабочей области аналитики журналов hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="6a8fd-153">Вставить с помощью hello первичный или вторичный ключ рабочей области аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="6a8fd-154">зашифрованные;</span><span class="sxs-lookup"><span data-stu-id="6a8fd-154">Encrypted</span></span> | <span data-ttu-id="6a8fd-155">Нет</span><span class="sxs-lookup"><span data-stu-id="6a8fd-155">No</span></span> | <span data-ttu-id="6a8fd-156">Да</span><span class="sxs-lookup"><span data-stu-id="6a8fd-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="6a8fd-157">3. Создание модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="6a8fd-157">3. Create runbook</span></span>

<span data-ttu-id="6a8fd-158">Служба автоматизации Azure имеет редактор hello портала, где можно изменить и протестировать модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="6a8fd-159">У вас есть hello параметр toouse hello скрипта редактор toowork с [PowerShell непосредственно](../automation/automation-edit-textual-runbook.md) или [создать графический runbook](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="6a8fd-160">В этом руководстве мы будем работать со скриптом PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Изменение модуля runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="6a8fd-162">Перейдите tooyour учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="6a8fd-163">Щелкните **Модули Runbook** > **Добавить Runbook** > **Создание нового модуля Runbook**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="6a8fd-164">Введите имя runbook hello, **задания для автоматизации сбор**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="6a8fd-165">Выберите тип runbook hello **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="6a8fd-166">Нажмите кнопку **создать** toocreate hello runbook и начала hello редактора.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="6a8fd-167">Скопируйте и вставьте следующий код в hello runbook hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="6a8fd-168">См. объяснение кода hello toohello комментарии в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="6a8fd-169">4. Тестирование модуля runbook</span><span class="sxs-lookup"><span data-stu-id="6a8fd-169">4. Test runbook</span></span>
<span data-ttu-id="6a8fd-170">Служба автоматизации Azure включает в себя среду слишком[тестирования модуля runbook](../automation/automation-testing-runbook.md) перед его публикацией.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="6a8fd-171">Можно проверять hello данными, собранными hello runbook и убедитесь, что она записывает tooLog Analytics должным образом, прежде чем публиковать их tooproduction.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Тестирование модуля runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="6a8fd-173">Нажмите кнопку **Сохранить** toosave hello runbook.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="6a8fd-174">Нажмите кнопку **области тестов** tooopen hello runbook в тестовой среде hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="6a8fd-175">Так как модуль runbook имеет параметры, вы tooenter запрашиваемые значения для них.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="6a8fd-176">Введите имя группы ресурсов hello hello и автоматизации hello учетной записи, ваши данные задания постоянной toocollect от.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="6a8fd-177">Нажмите кнопку **запустить** toohello запустить hello runbook.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="6a8fd-178">Hello runbook будет запущен с состоянием **в очереди** перед его отправкой слишком**под управлением**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="6a8fd-179">Hello runbook отображать подробные выходные данные с заданиями hello, собранные в формате json.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="6a8fd-180">Если в списке нет заданий, затем возникли нет заданий, созданных в учетной записи автоматизации hello в hello последний час.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="6a8fd-181">Попробуйте запустить любой runbook в учетной записи автоматизации hello, а затем снова выполните тест hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="6a8fd-182">Убедитесь, что выходные данные hello не показывает все ошибки в hello отправки команды tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="6a8fd-183">Необходимо иметь следующее сообщение аналогичные toohello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-183">You should have a message similar toohello following.</span></span>

    ![Выходные данные POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="6a8fd-185">5. Проверка записей в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6a8fd-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="6a8fd-186">После завершения hello runbook в тесте, и вы проверили hello выходные данные были успешно получены, можно проверить, что записи hello были созданы с помощью [поиска журналов в службе анализа журналов](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Выходные данные журналов](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="6a8fd-188">В hello портал Azure выберите рабочую область службы анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="6a8fd-189">Щелкните **Поиск по журналам**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="6a8fd-190">Тип hello следующую команду `Type=AutomationJob_CL` и нажмите кнопку поиска hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="6a8fd-191">Обратите внимание, что тип записи hello включает _CL, который не указан в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="6a8fd-192">Этот суффикс является автоматически добавленных toohello журнала типа tooindicate, он является типом пользовательского журнала.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="6a8fd-193">Вы увидите одну или несколько записей, возвращаемых, которое указывает, что hello runbook работает надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="6a8fd-194">6. Публикация hello runbook</span><span class="sxs-lookup"><span data-stu-id="6a8fd-194">6. Publish hello runbook</span></span>
<span data-ttu-id="6a8fd-195">После проверки правильности работы этого модуля hello, вам потребуется toopublish его, чтобы можно было запустить в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="6a8fd-196">Можно продолжить tooedit и тестирования hello runbook без изменения hello опубликованной версии.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Публикация модуля runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="6a8fd-198">Возвращает tooyour учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="6a8fd-199">Щелкните **Модули Runbook** и выберите **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="6a8fd-200">Щелкните **Правка** и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="6a8fd-201">Нажмите кнопку **Да** при задаваемые tooverify требуется toooverwrite hello ранее опубликованной версии.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="6a8fd-202">7. Настройка параметров ведения журнала</span><span class="sxs-lookup"><span data-stu-id="6a8fd-202">7. Set logging options</span></span> 
<span data-ttu-id="6a8fd-203">Для проверки, были может tooview [подробный вывод](../automation/automation-runbook-output-and-messages.md#message-streams) так как значение переменной hello $VerbosePreference в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="6a8fd-204">Для рабочей среды нужны свойства ведения журнала hello tooset для hello runbook, если требуется подробный вывод tooview.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="6a8fd-205">Для runbook hello, используемые в этом учебнике это будет отображаться отправляемых tooLog аналитика данных json hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![Ведение журнала и трассировка](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="6a8fd-207">В модуле runbook hello свойств выберите **ведения журнала и трассировки** под **параметры Runbook**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="6a8fd-208">Изменение параметров hello для **ведение журнала подробных сообщений** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="6a8fd-209">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="6a8fd-210">8. Создание расписания для модуля runbook</span><span class="sxs-lookup"><span data-stu-id="6a8fd-210">8. Schedule runbook</span></span>
<span data-ttu-id="6a8fd-211">Hello наиболее распространенных способа toostart runbook, который собирает данные наблюдения является tooschedule его toorun автоматически.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="6a8fd-212">Это делается путем создания [расписания в службе автоматизации Azure](../automation/automation-schedules.md) , подключив ее tooyour runbook.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Создание расписания для модуля runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="6a8fd-214">В свойствах hello модуль runbook, выберите **расписания** под **ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="6a8fd-215">Нажмите кнопку **Добавить расписание** > **связать runbook расписания tooyour** > **создать новое расписание**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="6a8fd-216">Тип в hello следующие значения для hello расписания и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="6a8fd-217">Свойство</span><span class="sxs-lookup"><span data-stu-id="6a8fd-217">Property</span></span> | <span data-ttu-id="6a8fd-218">Значение</span><span class="sxs-lookup"><span data-stu-id="6a8fd-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="6a8fd-219">Имя</span><span class="sxs-lookup"><span data-stu-id="6a8fd-219">Name</span></span> | <span data-ttu-id="6a8fd-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="6a8fd-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="6a8fd-221">Запуск</span><span class="sxs-lookup"><span data-stu-id="6a8fd-221">Starts</span></span> | <span data-ttu-id="6a8fd-222">Выберите любое время, по крайней мере на 5 минут последние hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="6a8fd-223">Периодичность</span><span class="sxs-lookup"><span data-stu-id="6a8fd-223">Recurrence</span></span> | <span data-ttu-id="6a8fd-224">Повторение</span><span class="sxs-lookup"><span data-stu-id="6a8fd-224">Recurring</span></span> |
| <span data-ttu-id="6a8fd-225">Повторять каждые</span><span class="sxs-lookup"><span data-stu-id="6a8fd-225">Recur every</span></span> | <span data-ttu-id="6a8fd-226">1 час</span><span class="sxs-lookup"><span data-stu-id="6a8fd-226">1 hour</span></span> |
| <span data-ttu-id="6a8fd-227">Срок действия</span><span class="sxs-lookup"><span data-stu-id="6a8fd-227">Set expiration</span></span> | <span data-ttu-id="6a8fd-228">Нет</span><span class="sxs-lookup"><span data-stu-id="6a8fd-228">No</span></span> |

<span data-ttu-id="6a8fd-229">После создания расписания hello, вам потребуется значения параметров tooset hello, которые будут использоваться при каждом запуске hello runbook этого расписания.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="6a8fd-230">Щелкните **Настройка параметров и настроек запуска**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="6a8fd-231">Укажите значения для **ResourceGroupName** и **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="6a8fd-232">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="6a8fd-233">9. Проверка запуска модуля runbook по расписанию</span><span class="sxs-lookup"><span data-stu-id="6a8fd-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="6a8fd-234">При каждом запуске модуля runbook [создается задание](../automation/automation-runbook-execution.md), и все выходные данные записываются в журнал.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="6a8fd-235">На самом деле это сбор и тех же заданий, которые hello runbook hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="6a8fd-236">Вы можете подтвердить этого модуля hello запускается как положено, проверив hello задания для модуля hello после истечения времени запуска hello расписании hello.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![Задания](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="6a8fd-238">В свойствах hello модуль runbook, выберите **заданий** под **ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="6a8fd-239">Вы увидите список заданий для каждого модуля runbook hello времени была начата.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="6a8fd-240">Выберите одну из tooview hello задания сведений о нем.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="6a8fd-241">Щелкните **все журналы** tooview hello вывод hello runbook и журналы.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="6a8fd-242">Прокрутите toofind нижней toohello входа аналогичные toohello образ ниже.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![Подробная информация](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="6a8fd-244">Щелкните эту запись tooview hello подробные данные json, который был отправлен tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6a8fd-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a8fd-245">Next steps</span></span>
- <span data-ttu-id="6a8fd-246">Используйте [конструктор представлений](../log-analytics/log-analytics-view-designer.md) toocreate отображение представления hello собранными toohello анализа журналов хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="6a8fd-247">Модуль runbook в пакет [решение для управления](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span><span class="sxs-lookup"><span data-stu-id="6a8fd-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="6a8fd-248">Дополнительные сведения о [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="6a8fd-249">Дополнительные сведения о [службе автоматизации Azure](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="6a8fd-250">Дополнительные сведения о hello [HTTP API-Интерфейс сборщика данных](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="6a8fd-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
