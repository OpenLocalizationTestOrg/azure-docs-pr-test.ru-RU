---
title: "Отслеживание заданий Stream Analytics и управление ими с помощью PowerShell | Документация Майкрософт"
description: "Сведения об использовании Azure PowerShell и командлетов для отслеживания заданий Stream Analytics и управления ими."
keywords: "azure powershell, командлеты azure powershell, команда powershell, сценарии powershell"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e3449ee90cc83c5e823e5948a2a2e7e633c454f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="938ec-104">Отслеживание заданий Stream Analytics и управление ими с помощью командлетов Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="938ec-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="938ec-105">Узнайте, как отслеживать ресурсы Stream Analytics и управлять ими с помощью командлетов Azure PowerShell и сценариев PowerShell, выполняющих базовые задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="938ec-105">Learn how to monitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="938ec-106">Необходимые условия для запуска командлетов Azure PowerShell службы Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="938ec-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="938ec-107">Создайте группу ресурсов Azure в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="938ec-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="938ec-108">Ниже приведен пример сценария Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="938ec-108">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="938ec-109">Дополнительную информацию об Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="938ec-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="938ec-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="938ec-111">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-111">Azure PowerShell 1.0:</span></span>  

         # Log in to your Azure account
        Login-AzureRmAccount

        # Select the Azure subscription you want to use to create the resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="938ec-112">Отслеживание заданий Stream Analytics, созданных программным путем, по умолчанию отключено.</span><span class="sxs-lookup"><span data-stu-id="938ec-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="938ec-113">Вы можете вручную включить отслеживание на портале Azure. Для этого перейдите на страницу "Отслеживание" задания и нажмите кнопку "Включить". Это также можно сделать программным путем, выполнив действия, приведенные в статье [Azure Stream Analytics. Отслеживание заданий Stream Analytics программным путем](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="938ec-113">You can manually enable monitoring in the Azure Portal by navigating to the job’s Monitor page and clicking the Enable button or you can do this programmatically by following the steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="938ec-114">Командлеты Azure PowerShell для службы Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="938ec-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="938ec-115">Следующие командлеты Azure PowerShell можно использовать для отслеживания заданий Azure Stream Analytics и управления ими.</span><span class="sxs-lookup"><span data-stu-id="938ec-115">The following Azure PowerShell cmdlets can be used to monitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="938ec-116">Обратите внимание, что Azure PowerShell имеет различные версии.</span><span class="sxs-lookup"><span data-stu-id="938ec-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="938ec-117">**В приведенных примерах первая команда приведена для Azure PowerShell 0.9.8, вторая — для Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="938ec-117">**In the examples listed the first command is for Azure PowerShell 0.9.8, the second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="938ec-118">В названиях команд Azure PowerShell 1.0 всегда содержится "AzureRM".</span><span class="sxs-lookup"><span data-stu-id="938ec-118">The Azure PowerShell 1.0 commands will always have "AzureRM" in the command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="938ec-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="938ec-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="938ec-120">Выводит список всех заданий Stream Analytics, определенных в подписке Azure или указанной группе ресурсов, или показывает сведения о конкретном задании в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="938ec-120">Lists all Stream Analytics jobs defined in the Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="938ec-121">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-121">**Example 1**</span></span>

<span data-ttu-id="938ec-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="938ec-123">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="938ec-124">Эта команда PowerShell возвращает сведения обо всех заданиях Stream Analytics в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="938ec-124">This PowerShell command returns information about all the Stream Analytics jobs in the Azure subscription.</span></span>

<span data-ttu-id="938ec-125">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="938ec-125">**Example 2**</span></span>

<span data-ttu-id="938ec-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="938ec-127">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="938ec-128">Эта команда PowerShell возвращает сведения о всех заданиях Stream Analytics в группе ресурсов StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="938ec-128">This PowerShell command returns information about all the Stream Analytics jobs in the resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="938ec-129">**Пример 3**</span><span class="sxs-lookup"><span data-stu-id="938ec-129">**Example 3**</span></span>

<span data-ttu-id="938ec-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="938ec-131">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="938ec-132">Эта команда PowerShell возвращает сведения о задании Stream Analytics StreamingJob в группе ресурсов StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="938ec-132">This PowerShell command returns information about the Stream Analytics job StreamingJob in the resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="938ec-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="938ec-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="938ec-134">Выводит список всех входных данных, определенных в указанном задании Stream Analytics, или показывает сведения о конкретных данных.</span><span class="sxs-lookup"><span data-stu-id="938ec-134">Lists all of the inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="938ec-135">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-135">**Example 1**</span></span>

<span data-ttu-id="938ec-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="938ec-137">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="938ec-138">Эта команда PowerShell возвращает сведения о всех входных данных, определенных в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-138">This PowerShell command returns information about all the inputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="938ec-139">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="938ec-139">**Example 2**</span></span>

<span data-ttu-id="938ec-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="938ec-141">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="938ec-142">Эта команда PowerShell возвращает сведения о входных данных EntryStream, определенных в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-142">This PowerShell command returns information about the input named EntryStream defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="938ec-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="938ec-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="938ec-144">Выводит список всех выходных данных, определенных в указанном задании Stream Analytics, или показывает сведения о конкретных данных.</span><span class="sxs-lookup"><span data-stu-id="938ec-144">Lists all of the outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="938ec-145">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-145">**Example 1**</span></span>

<span data-ttu-id="938ec-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="938ec-147">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="938ec-148">Эта команда PowerShell возвращает сведения о выходных данных, определенных в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-148">This PowerShell command returns information about the outputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="938ec-149">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="938ec-149">**Example 2**</span></span>

<span data-ttu-id="938ec-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="938ec-151">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="938ec-152">Эта команда PowerShell возвращает сведения о выходных данных Output, определенных в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-152">This PowerShell command returns information about the output named Output defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="938ec-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="938ec-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="938ec-154">Возвращает сведения о квоте единиц потоковой передачи в указанном регионе.</span><span class="sxs-lookup"><span data-stu-id="938ec-154">Gets information about the quota of streaming units in a specified region.</span></span>

<span data-ttu-id="938ec-155">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-155">**Example 1**</span></span>

<span data-ttu-id="938ec-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="938ec-157">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="938ec-158">Эта команда PowerShell возвращает сведения о квоте и использовании единиц потоковой передачи в центральном регионе США.</span><span class="sxs-lookup"><span data-stu-id="938ec-158">This PowerShell command returns information about the quota and usage of streaming units in the Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="938ec-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="938ec-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="938ec-160">Возвращает сведения о конкретном преобразовании, определенном в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="938ec-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="938ec-161">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-161">**Example 1**</span></span>

<span data-ttu-id="938ec-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="938ec-163">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="938ec-164">Эта команда PowerShell возвращает сведения о преобразовании StreamingJob в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-164">This PowerShell command returns information about the transformation called StreamingJob in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="938ec-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="938ec-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="938ec-166">Создает новые или обновляет существующие входные данные в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="938ec-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="938ec-167">Имя входных данных можно указать в JSON-файле или в командной строке.</span><span class="sxs-lookup"><span data-stu-id="938ec-167">The name of the input can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="938ec-168">Если указаны оба, имя в командной строке должно совпадать с именем в файле.</span><span class="sxs-lookup"><span data-stu-id="938ec-168">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="938ec-169">Если указаны существующие входные данные и не задан параметр –Force, командлет предложит заменить существующие входные данные.</span><span class="sxs-lookup"><span data-stu-id="938ec-169">If you specify an input that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing input.</span></span>

<span data-ttu-id="938ec-170">Если указать параметр –Force и существующее имя входных данных, входные данные будут заменены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="938ec-170">If you specify the –Force parameter and specify an existing input name, the input will be replaced without confirmation.</span></span>

<span data-ttu-id="938ec-171">Подробные сведения о структуре и содержимом JSON-файла см. в разделе о [создании входных данных][msdn-rest-api-create-stream-analytics-input] [справочника по интерфейсу REST API управления Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="938ec-171">For detailed information on the JSON file structure and contents, refer to the [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="938ec-172">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-172">**Example 1**</span></span>

<span data-ttu-id="938ec-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="938ec-174">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="938ec-175">Эта команда PowerShell создает новые входные данные из файла Input.json.</span><span class="sxs-lookup"><span data-stu-id="938ec-175">This PowerShell command creates a new input from the file Input.json.</span></span> <span data-ttu-id="938ec-176">Если существующие входные данные с именем, указанным во входном файле определения, уже определены, командлет предложит их заменить.</span><span class="sxs-lookup"><span data-stu-id="938ec-176">If an existing input with the name specified in the input definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="938ec-177">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="938ec-177">**Example 2**</span></span>

<span data-ttu-id="938ec-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="938ec-179">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="938ec-180">Эта команда PowerShell создает новые входные данные в задании EntryStream.</span><span class="sxs-lookup"><span data-stu-id="938ec-180">This PowerShell command creates a new input in the job called EntryStream.</span></span> <span data-ttu-id="938ec-181">Если существующие входные данные с таким именем уже определены, командлет предложит их заменить.</span><span class="sxs-lookup"><span data-stu-id="938ec-181">If an existing input with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="938ec-182">**Пример 3**</span><span class="sxs-lookup"><span data-stu-id="938ec-182">**Example 3**</span></span>

<span data-ttu-id="938ec-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="938ec-184">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="938ec-185">Эта команда PowerShell заменяет определение существующего источника входных данных EntryStream на определение из файла.</span><span class="sxs-lookup"><span data-stu-id="938ec-185">This PowerShell command replaces the definition of the existing input source called EntryStream with the definition from the file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="938ec-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="938ec-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="938ec-187">Создает задание Stream Analytics в Microsoft Azure или обновляет определение существующего задания.</span><span class="sxs-lookup"><span data-stu-id="938ec-187">Creates a new Stream Analytics job in Microsoft Azure, or updates the definition of an existing specified job.</span></span>

<span data-ttu-id="938ec-188">Имя задания можно указать в JSON-файле или в командной строке.</span><span class="sxs-lookup"><span data-stu-id="938ec-188">The name of the job can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="938ec-189">Если указаны оба, имя в командной строке должно совпадать с именем в файле.</span><span class="sxs-lookup"><span data-stu-id="938ec-189">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="938ec-190">Если указано существующее имя задания и не указан параметр –Force, командлет предложит заменить существующее задание.</span><span class="sxs-lookup"><span data-stu-id="938ec-190">If you specify a job name that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing job.</span></span>

<span data-ttu-id="938ec-191">Если указать параметр –Force и существующее имя задания, определение задания будет заменено без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="938ec-191">If you specify the –Force parameter and specify an existing job name, the job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="938ec-192">Подробные сведения о структуре и содержимом JSON-файла см. в разделе о [создании задания Stream Analytics][msdn-rest-api-create-stream-analytics-job] [справочника по интерфейсу REST API управления Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="938ec-192">For detailed information on the JSON file structure and contents, refer to the [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="938ec-193">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-193">**Example 1**</span></span>

<span data-ttu-id="938ec-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="938ec-195">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="938ec-196">Эта команда PowerShell создает новое задание из определения в JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="938ec-196">This PowerShell command creates a new job from the definition in JobDefinition.json.</span></span> <span data-ttu-id="938ec-197">Если существующее задание с именем, указанным в файле определения задания, уже определено, командлет предложит его заменить.</span><span class="sxs-lookup"><span data-stu-id="938ec-197">If an existing job with the name specified in the job definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="938ec-198">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="938ec-198">**Example 2**</span></span>

<span data-ttu-id="938ec-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="938ec-200">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="938ec-201">Эта команда PowerShell заменяет определение задания StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-201">This PowerShell command replaces the job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="938ec-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="938ec-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="938ec-203">Создает новые или обновляет существующие выходные данные в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="938ec-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="938ec-204">Имя выходных данных можно указать в JSON-файле или в командной строке.</span><span class="sxs-lookup"><span data-stu-id="938ec-204">The name of the output can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="938ec-205">Если указаны оба, имя в командной строке должно совпадать с именем в файле.</span><span class="sxs-lookup"><span data-stu-id="938ec-205">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="938ec-206">Если указаны существующие выходные данные и не задан параметр –Force, командлет предложит заменить существующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="938ec-206">If you specify an output that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing output.</span></span>

<span data-ttu-id="938ec-207">Если указать параметр –Force и существующее имя выходных данных, выходные данные будут заменены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="938ec-207">If you specify the –Force parameter and specify an existing output name, the output will be replaced without confirmation.</span></span>

<span data-ttu-id="938ec-208">Подробные сведения о структуре и содержимом JSON-файла см. в разделе о [создании выходных данных][msdn-rest-api-create-stream-analytics-output] [справочника по интерфейсу REST API управления Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="938ec-208">For detailed information on the JSON file structure and contents, refer to the [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="938ec-209">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-209">**Example 1**</span></span>

<span data-ttu-id="938ec-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="938ec-211">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="938ec-212">Эта команда PowerShell создает новые выходные данные output в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-212">This PowerShell command creates a new output called "output" in the job StreamingJob.</span></span> <span data-ttu-id="938ec-213">Если существующие выходные данные с таким именем уже определены, командлет предложит их заменить.</span><span class="sxs-lookup"><span data-stu-id="938ec-213">If an existing output with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="938ec-214">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="938ec-214">**Example 2**</span></span>

<span data-ttu-id="938ec-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="938ec-216">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="938ec-217">Эта команда PowerShell заменяет определение для output в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-217">This PowerShell command replaces the definition for "output" in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="938ec-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="938ec-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="938ec-219">Создает новое или обновляет существующее преобразование в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="938ec-219">Creates a new transformation within a Stream Analytics job, or updates the existing transformation.</span></span>

<span data-ttu-id="938ec-220">Имя преобразования можно указано в JSON-файле или в командной строке.</span><span class="sxs-lookup"><span data-stu-id="938ec-220">The name of the transformation can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="938ec-221">Если указаны оба, имя в командной строке должно совпадать с именем в файле.</span><span class="sxs-lookup"><span data-stu-id="938ec-221">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="938ec-222">Если указано существующее преобразование и не задан параметр –Force, командлет предложит заменить существующее преобразование.</span><span class="sxs-lookup"><span data-stu-id="938ec-222">If you specify a transformation that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing transformation.</span></span>

<span data-ttu-id="938ec-223">Если указать параметр –Force и существующее имя преобразования, преобразование будет заменено без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="938ec-223">If you specify the –Force parameter and specify an existing transformation name, the transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="938ec-224">Подробные сведения о структуре и содержимом JSON-файла см. в разделе о [создании преобразования][msdn-rest-api-create-stream-analytics-transformation] [справочника по интерфейсу REST API управления Stream Analytics][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="938ec-224">For detailed information on the JSON file structure and contents, refer to the [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="938ec-225">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-225">**Example 1**</span></span>

<span data-ttu-id="938ec-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="938ec-227">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="938ec-228">Эта команда PowerShell создает новое преобразование StreamingJobTransform в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-228">This PowerShell command creates a new transformation called StreamingJobTransform in the job StreamingJob.</span></span> <span data-ttu-id="938ec-229">Если существующее преобразование с таким именем уже определено, командлет предложит его заменить.</span><span class="sxs-lookup"><span data-stu-id="938ec-229">If an existing transformation is already defined with this name, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="938ec-230">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="938ec-230">**Example 2**</span></span>

<span data-ttu-id="938ec-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="938ec-232">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="938ec-233">Эта команда PowerShell заменяет определение StreamingJobTransform в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-233">This PowerShell command replaces the definition of StreamingJobTransform in the job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="938ec-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="938ec-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="938ec-235">Асинхронно удаляет указанные входные данные из задания Stream Analytics в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="938ec-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="938ec-236">Если указать параметр –Force, входные данные будут удалены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="938ec-236">If you specify the –Force parameter, the input will be deleted without confirmation.</span></span>

<span data-ttu-id="938ec-237">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-237">**Example 1**</span></span>

<span data-ttu-id="938ec-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="938ec-239">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="938ec-240">Эта команда PowerShell удаляет входные данные EventStream в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-240">This PowerShell command removes the input EventStream in the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="938ec-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="938ec-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="938ec-242">Асинхронно удаляет указанное задание Stream Analytics в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="938ec-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="938ec-243">Если указать параметр –Force, задание будет удалено без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="938ec-243">If you specify the –Force parameter, the job will be deleted without confirmation.</span></span>

<span data-ttu-id="938ec-244">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-244">**Example 1**</span></span>

<span data-ttu-id="938ec-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="938ec-246">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="938ec-247">Эта команда PowerShell удаляет задание StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-247">This PowerShell command removes the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="938ec-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="938ec-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="938ec-249">Асинхронно удаляет указанные выходные данные из задания Stream Analytics в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="938ec-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="938ec-250">Если указать параметр –Force, выходные данные будут удалены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="938ec-250">If you specify the –Force parameter, the output will be deleted without confirmation.</span></span>

<span data-ttu-id="938ec-251">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-251">**Example 1**</span></span>

<span data-ttu-id="938ec-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="938ec-253">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="938ec-254">Эта команда PowerShell удаляет выходные данные Output в задании StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-254">This PowerShell command removes the output Output in the job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="938ec-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="938ec-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="938ec-256">Асинхронно развертывает и запускает задание Stream Analytics в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="938ec-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="938ec-257">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-257">**Example 1**</span></span>

<span data-ttu-id="938ec-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="938ec-259">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="938ec-260">Это команда PowerShell запускает задание StreamingJob с пользовательским временем запуска выходных данных «12 декабря 2012 г., 12:12:12 UTC».</span><span class="sxs-lookup"><span data-stu-id="938ec-260">This PowerShell command starts the job StreamingJob with a custom output start time set to December 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="938ec-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="938ec-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="938ec-262">Асинхронно останавливает задание Stream Analytics в Microsoft Azure и освобождает используемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="938ec-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="938ec-263">Определение задания и метаданные остаются доступны в подписке через портал Azure и интерфейсы API управления, поэтому задание всегда можно изменить и перезапустить.</span><span class="sxs-lookup"><span data-stu-id="938ec-263">The job definition and metadata will remain available within your subscription through both the Azure portal and management APIs, such that the job can be edited and restarted.</span></span> <span data-ttu-id="938ec-264">Вы не платите за задание в состоянии "Остановлено".</span><span class="sxs-lookup"><span data-stu-id="938ec-264">You will not be charged for a job in the stopped state.</span></span>

<span data-ttu-id="938ec-265">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-265">**Example 1**</span></span>

<span data-ttu-id="938ec-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="938ec-267">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="938ec-268">Эта команда PowerShell останавливает задание StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-268">This PowerShell command stops the job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="938ec-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="938ec-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="938ec-270">Проверяет возможность подключения Stream Analytics к указанным входным данным.</span><span class="sxs-lookup"><span data-stu-id="938ec-270">Tests the ability of Stream Analytics to connect to a specified input.</span></span>

<span data-ttu-id="938ec-271">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-271">**Example 1**</span></span>

<span data-ttu-id="938ec-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="938ec-273">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="938ec-274">Эта команда PowerShell проверяет состояние подключения входных данных EntryStream в StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-274">This PowerShell command tests the connection status of the input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="938ec-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="938ec-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="938ec-276">Проверяет возможность подключения Stream Analytics к указанным выходным данным.</span><span class="sxs-lookup"><span data-stu-id="938ec-276">Tests the ability of Stream Analytics to connect to a specified output.</span></span>

<span data-ttu-id="938ec-277">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="938ec-277">**Example 1**</span></span>

<span data-ttu-id="938ec-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="938ec-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="938ec-279">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="938ec-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="938ec-280">Эта команда PowerShell проверяет состояние подключения выходных данных Output в StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="938ec-280">This PowerShell command tests the connection status of the output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="938ec-281">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="938ec-281">Get support</span></span>
<span data-ttu-id="938ec-282">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="938ec-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="938ec-283">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="938ec-283">Next steps</span></span>
* [<span data-ttu-id="938ec-284">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="938ec-284">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="938ec-285">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="938ec-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="938ec-286">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="938ec-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="938ec-287">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="938ec-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="938ec-288">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="938ec-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

