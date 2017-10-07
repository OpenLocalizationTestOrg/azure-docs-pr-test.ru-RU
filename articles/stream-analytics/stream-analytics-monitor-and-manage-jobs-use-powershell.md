---
title: "aaaMonitor и управление заданиями Stream Analytics с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как командлеты Azure PowerShell и toomonitor toouse заданий Stream Analytics и управление ими."
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
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="04bd1-104">Отслеживание заданий Stream Analytics и управление ими с помощью командлетов Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="04bd1-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="04bd1-105">Узнайте, как toomonitor и управление ресурсами Stream Analytics с помощью командлетов Azure PowerShell и сценариев powershell, выполнять основные задачи Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="04bd1-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="04bd1-106">Необходимые условия для запуска командлетов Azure PowerShell службы Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04bd1-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="04bd1-107">Создайте группу ресурсов Azure в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="04bd1-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="04bd1-108">Hello ниже приведен пример сценария Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04bd1-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="04bd1-109">Дополнительную информацию об Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04bd1-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="04bd1-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="04bd1-111">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="04bd1-112">Отслеживание заданий Stream Analytics, созданных программным путем, по умолчанию отключено.</span><span class="sxs-lookup"><span data-stu-id="04bd1-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="04bd1-113">Вы можете вручную включить наблюдение в hello портал Azure, перейдя на страницу toohello задания монитора и щелкнув кнопку Enable hello, или это можно сделать программным образом, выполнив следующие шаги hello, расположенный в [Azure Stream Analytics — поток монитора Аналитика программным путем задания](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="04bd1-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="04bd1-114">Командлеты Azure PowerShell для службы Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04bd1-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="04bd1-115">Hello следующие командлеты Azure PowerShell можно использовать toomonitor и управление заданиями Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="04bd1-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="04bd1-116">Обратите внимание, что Azure PowerShell имеет различные версии.</span><span class="sxs-lookup"><span data-stu-id="04bd1-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="04bd1-117">**В примерах hello, первая команда перечисленных hello предназначен для Azure PowerShell 0.9.8 вторая команда hello является для Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="04bd1-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="04bd1-118">команды Hello Azure PowerShell 1.0 всегда будет содержать «AzureRM» в команде hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="04bd1-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="04bd1-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="04bd1-120">Перечисляет все задания Stream Analytics, определенные в hello подписки Azure или группа ресурсов или получает задание сведений о конкретном задании в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="04bd1-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="04bd1-121">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-121">**Example 1**</span></span>

<span data-ttu-id="04bd1-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="04bd1-123">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="04bd1-124">Эта команда PowerShell возвращает сведения обо всех заданиях Stream Analytics hello в hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="04bd1-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="04bd1-125">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="04bd1-125">**Example 2**</span></span>

<span data-ttu-id="04bd1-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="04bd1-127">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="04bd1-128">Эта команда PowerShell возвращает сведения обо всех заданиях hello Stream Analytics в группе ресурсов hello StreamAnalytics по умолчанию-Центральная часть США.</span><span class="sxs-lookup"><span data-stu-id="04bd1-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="04bd1-129">**Пример 3**</span><span class="sxs-lookup"><span data-stu-id="04bd1-129">**Example 3**</span></span>

<span data-ttu-id="04bd1-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="04bd1-131">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="04bd1-132">Эта команда PowerShell возвращает сведения о задании Stream Analytics hello StreamingJob в группе ресурсов hello StreamAnalytics по умолчанию-Центральная часть США.</span><span class="sxs-lookup"><span data-stu-id="04bd1-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="04bd1-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="04bd1-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="04bd1-134">Перечисляет все hello входных данных, которые определены в указанное задание Stream Analytics, или возвращает сведения об определенных входных данных.</span><span class="sxs-lookup"><span data-stu-id="04bd1-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="04bd1-135">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-135">**Example 1**</span></span>

<span data-ttu-id="04bd1-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="04bd1-137">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="04bd1-138">Эта команда PowerShell возвращает сведения о всех входных данных hello, определенные в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="04bd1-139">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="04bd1-139">**Example 2**</span></span>

<span data-ttu-id="04bd1-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="04bd1-141">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="04bd1-142">Эта команда PowerShell возвращает сведения о hello входных данных с именем EntryStream, определенные в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="04bd1-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="04bd1-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="04bd1-144">Перечисляет все hello выходных данных, которые определены в указанное задание Stream Analytics, или возвращает сведения о конкретных выходных данных.</span><span class="sxs-lookup"><span data-stu-id="04bd1-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="04bd1-145">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-145">**Example 1**</span></span>

<span data-ttu-id="04bd1-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="04bd1-147">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="04bd1-148">Эта команда PowerShell возвращает сведения о определены в задании hello StreamingJob hello выходов.</span><span class="sxs-lookup"><span data-stu-id="04bd1-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="04bd1-149">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="04bd1-149">**Example 2**</span></span>

<span data-ttu-id="04bd1-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="04bd1-151">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="04bd1-152">Эта команда PowerShell возвращает сведения о hello выходных данных с именем выходные данные, определенные в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="04bd1-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="04bd1-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="04bd1-154">Получает сведения о квоте hello единицы в указанном регионе потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="04bd1-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="04bd1-155">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-155">**Example 1**</span></span>

<span data-ttu-id="04bd1-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="04bd1-157">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="04bd1-158">Эту команду PowerShell возвращает сведения о квоте hello и использования единиц потоковой передачи в регионе hello центральной части США.</span><span class="sxs-lookup"><span data-stu-id="04bd1-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="04bd1-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="04bd1-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="04bd1-160">Возвращает сведения о конкретном преобразовании, определенном в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="04bd1-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="04bd1-161">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-161">**Example 1**</span></span>

<span data-ttu-id="04bd1-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="04bd1-163">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="04bd1-164">Эта команда PowerShell возвращает сведения о преобразовании «hello», называется StreamingJob в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="04bd1-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="04bd1-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="04bd1-166">Создает новые или обновляет существующие входные данные в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="04bd1-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="04bd1-167">Hello Привет вводимых данных может быть указано имя в hello JSON-файл или в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="04bd1-168">Если указаны оба имени hello hello в командной строке необходимо hello то же, что один hello в файле hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="04bd1-169">Если указать входной, уже существует и не указывайте hello — параметр Force, командлет hello запрашивает ли tooreplace hello существующий вход.</span><span class="sxs-lookup"><span data-stu-id="04bd1-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="04bd1-170">Если нужно задать hello — параметр Force и существующий ввода имени, hello входные данные будут заменены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="04bd1-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="04bd1-171">Подробные сведения о структуре файла JSON hello и содержимое, см. в разделе toohello [создать входные данные (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] раздел hello [API REST управления Stream Analytics Справочная библиотека][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="04bd1-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="04bd1-172">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-172">**Example 1**</span></span>

<span data-ttu-id="04bd1-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="04bd1-174">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="04bd1-175">Эта команда PowerShell создает новые входные данные из файла hello Input.json.</span><span class="sxs-lookup"><span data-stu-id="04bd1-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="04bd1-176">Если существующий вход с именем hello, указанной в файле ввода определения hello уже определено, hello командлет запросит ли tooreplace его.</span><span class="sxs-lookup"><span data-stu-id="04bd1-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="04bd1-177">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="04bd1-177">**Example 2**</span></span>

<span data-ttu-id="04bd1-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="04bd1-179">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="04bd1-180">Эта команда PowerShell создает новые входные данные в задании hello вызывается EntryStream.</span><span class="sxs-lookup"><span data-stu-id="04bd1-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="04bd1-181">Если существующий вход с таким именем уже определено, hello командлет запросит ли tooreplace его.</span><span class="sxs-lookup"><span data-stu-id="04bd1-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="04bd1-182">**Пример 3**</span><span class="sxs-lookup"><span data-stu-id="04bd1-182">**Example 3**</span></span>

<span data-ttu-id="04bd1-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="04bd1-184">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="04bd1-185">Эта команда PowerShell заменяет определение hello hello существующий источник входных данных называется EntryStream с определением hello из файла hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="04bd1-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="04bd1-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="04bd1-187">Создает новое задание Stream Analytics в Microsoft Azure или обновляет определение hello существующего указанного задания.</span><span class="sxs-lookup"><span data-stu-id="04bd1-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="04bd1-188">Имя задания hello Hello указываются в hello JSON-файл или в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="04bd1-189">Если указаны оба имени hello hello в командной строке необходимо hello то же, что один hello в файле hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="04bd1-190">Если указать имя задания, которое уже существует и не указывайте hello — параметр Force, командлет hello запрашивает ли tooreplace hello существующего задания.</span><span class="sxs-lookup"><span data-stu-id="04bd1-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="04bd1-191">Если нужно задать hello — параметр Force и задания имени существующего определения задания hello будут заменены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="04bd1-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="04bd1-192">Подробные сведения о структуре файла JSON hello и содержимое, см. в разделе toohello [создать задание Stream Analytics] [ msdn-rest-api-create-stream-analytics-job] раздел hello [Справочник API REST управления Stream Analytics Библиотека][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="04bd1-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="04bd1-193">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-193">**Example 1**</span></span>

<span data-ttu-id="04bd1-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="04bd1-195">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="04bd1-196">Эта команда PowerShell создает новое задание из определения hello в JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="04bd1-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="04bd1-197">Если существующее задание с именем hello, указанной в файле определения задания hello уже определено, hello командлет запросит ли tooreplace его.</span><span class="sxs-lookup"><span data-stu-id="04bd1-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="04bd1-198">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="04bd1-198">**Example 2**</span></span>

<span data-ttu-id="04bd1-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="04bd1-200">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="04bd1-201">Эта команда PowerShell заменяет hello определения задания для StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="04bd1-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="04bd1-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="04bd1-203">Создает новые или обновляет существующие выходные данные в задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="04bd1-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="04bd1-204">можно указать имя Hello hello выходных данных, в hello JSON-файл или в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="04bd1-205">Если указаны оба имени hello hello в командной строке необходимо hello то же, что один hello в файле hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="04bd1-206">Если указано ключевое слово output, который уже существует и не указывайте hello — параметр Force, командлет hello запрашивает ли tooreplace hello существующего выхода.</span><span class="sxs-lookup"><span data-stu-id="04bd1-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="04bd1-207">При указании hello — параметр Force и укажите имя существующего выходного, hello выходные данные будут заменены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="04bd1-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="04bd1-208">Подробные сведения о структуре файла JSON hello и содержимое, см. в разделе toohello [создание выходных данных (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] раздел hello [API REST управления Stream Analytics Справочная библиотека][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="04bd1-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="04bd1-209">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-209">**Example 1**</span></span>

<span data-ttu-id="04bd1-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="04bd1-211">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="04bd1-212">Эта команда PowerShell создает новые выходные данные с именем «выход» в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="04bd1-213">Если существующий выходных данных с таким именем уже определено, hello командлет запросит ли tooreplace его.</span><span class="sxs-lookup"><span data-stu-id="04bd1-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="04bd1-214">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="04bd1-214">**Example 2**</span></span>

<span data-ttu-id="04bd1-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="04bd1-216">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="04bd1-217">Эта команда PowerShell заменяет определение «выход» в задании hello StreamingJob hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="04bd1-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="04bd1-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="04bd1-219">Создает новое преобразование в задании Stream Analytics или обновляет существующий преобразования hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="04bd1-220">можно указать имя Hello преобразования «hello», в hello JSON-файл или в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="04bd1-221">Если указаны оба имени hello hello в командной строке необходимо hello то же, что один hello в файле hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="04bd1-222">Если указано преобразование, которое уже существует и не указывайте hello — параметр Force, командлет hello запрашивает ли tooreplace hello существующего преобразования.</span><span class="sxs-lookup"><span data-stu-id="04bd1-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="04bd1-223">При указании hello — параметр Force и укажите имя существующей преобразование, преобразование «hello» будут заменены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="04bd1-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="04bd1-224">Подробные сведения о структуре файла JSON hello и содержимое, см. в разделе toohello [Создание преобразования (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] раздел hello [управления Stream Analytics Справочная библиотека API REST][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="04bd1-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="04bd1-225">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-225">**Example 1**</span></span>

<span data-ttu-id="04bd1-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="04bd1-227">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="04bd1-228">Эта команда PowerShell создает новое преобразование называется StreamingJobTransform в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="04bd1-229">Если преобразование существующих с таким именем уже определено, hello командлет запросит ли tooreplace его.</span><span class="sxs-lookup"><span data-stu-id="04bd1-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="04bd1-230">**Пример 2**</span><span class="sxs-lookup"><span data-stu-id="04bd1-230">**Example 2**</span></span>

<span data-ttu-id="04bd1-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="04bd1-232">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="04bd1-233">Эта команда PowerShell заменяет определение StreamingJobTransform hello в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="04bd1-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="04bd1-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="04bd1-235">Асинхронно удаляет указанные входные данные из задания Stream Analytics в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="04bd1-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="04bd1-236">При указании hello — параметр Force, hello ввода будет удален без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="04bd1-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="04bd1-237">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-237">**Example 1**</span></span>

<span data-ttu-id="04bd1-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="04bd1-239">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="04bd1-240">Эту команду PowerShell, удаляет hello ввода EventStream в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="04bd1-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="04bd1-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="04bd1-242">Асинхронно удаляет указанное задание Stream Analytics в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="04bd1-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="04bd1-243">При указании hello — параметр Force hello задание будет удален без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="04bd1-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="04bd1-244">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-244">**Example 1**</span></span>

<span data-ttu-id="04bd1-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="04bd1-246">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="04bd1-247">Эта команда PowerShell удаляет задание hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="04bd1-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="04bd1-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="04bd1-249">Асинхронно удаляет указанные выходные данные из задания Stream Analytics в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="04bd1-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="04bd1-250">При указании hello — параметр Force hello выходные данные будут удалены без подтверждения.</span><span class="sxs-lookup"><span data-stu-id="04bd1-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="04bd1-251">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-251">**Example 1**</span></span>

<span data-ttu-id="04bd1-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="04bd1-253">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="04bd1-254">Выходные данные этого PowerShell команда удаляет hello выходные данные в задании hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="04bd1-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="04bd1-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="04bd1-256">Асинхронно развертывает и запускает задание Stream Analytics в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="04bd1-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="04bd1-257">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-257">**Example 1**</span></span>

<span data-ttu-id="04bd1-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="04bd1-259">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="04bd1-260">Эта команда PowerShell запускает hello задание StreamingJob с временем начала пользовательский вывод tooDecember 12, 2012 г., 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="04bd1-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="04bd1-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="04bd1-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="04bd1-262">Асинхронно останавливает задание Stream Analytics в Microsoft Azure и освобождает используемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="04bd1-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="04bd1-263">Hello определение задания и метаданные останутся доступными в подписке через портал Azure hello и API управления, hello задания можно изменить и перезапустить.</span><span class="sxs-lookup"><span data-stu-id="04bd1-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="04bd1-264">Вы не будете платить за задание в состоянии остановки hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="04bd1-265">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-265">**Example 1**</span></span>

<span data-ttu-id="04bd1-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="04bd1-267">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="04bd1-268">Эта команда PowerShell останавливает задание hello StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="04bd1-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="04bd1-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="04bd1-270">Проверяет возможность hello tooa tooconnect Stream Analytics указано входных данных.</span><span class="sxs-lookup"><span data-stu-id="04bd1-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="04bd1-271">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-271">**Example 1**</span></span>

<span data-ttu-id="04bd1-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="04bd1-273">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="04bd1-274">Это PowerShell команды тесты hello состояние соединения hello ввода EntryStream в StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="04bd1-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="04bd1-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="04bd1-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="04bd1-276">Возможность hello тесты tooa tooconnect Stream Analytics указаны выходные данные.</span><span class="sxs-lookup"><span data-stu-id="04bd1-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="04bd1-277">**Пример 1**</span><span class="sxs-lookup"><span data-stu-id="04bd1-277">**Example 1**</span></span>

<span data-ttu-id="04bd1-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="04bd1-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="04bd1-279">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="04bd1-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="04bd1-280">Выходные данные в StreamingJob вывода этого PowerShell команды тесты hello состояние соединения hello.</span><span class="sxs-lookup"><span data-stu-id="04bd1-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="04bd1-281">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="04bd1-281">Get support</span></span>
<span data-ttu-id="04bd1-282">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="04bd1-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="04bd1-283">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04bd1-283">Next steps</span></span>
* [<span data-ttu-id="04bd1-284">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04bd1-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="04bd1-285">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04bd1-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="04bd1-286">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04bd1-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="04bd1-287">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04bd1-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="04bd1-288">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="04bd1-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

