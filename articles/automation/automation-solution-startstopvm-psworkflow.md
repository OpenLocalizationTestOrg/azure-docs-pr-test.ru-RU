---
title: "aaaStarting и остановки виртуальных машин с автоматизацией Azure — рабочий процесс PowerShell | Документы Microsoft"
description: "Сценарий автоматизации Azure, включая модули Runbook toostart и остановить классических виртуальных машин графической версии."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="01f26-103">Сценарий для службы автоматизации Azure: запуск и остановка виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="01f26-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="01f26-104">Этот сценарий автоматизации Azure включает модули Runbook toostart и остановить классических виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="01f26-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="01f26-105">Этот сценарий можно использовать для следующих hello:</span><span class="sxs-lookup"><span data-stu-id="01f26-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="01f26-106">Модули Runbook hello без каких-либо используйте в собственной среде.</span><span class="sxs-lookup"><span data-stu-id="01f26-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="01f26-107">Измените функциональность tooperform пользовательские модули Runbook hello.</span><span class="sxs-lookup"><span data-stu-id="01f26-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="01f26-108">Вызывает hello модулей Runbook из другого модуля runbook как часть общего решения.</span><span class="sxs-lookup"><span data-stu-id="01f26-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="01f26-109">Используйте модули Runbook hello как разработка основные понятия runbook toolearn учебники.</span><span class="sxs-lookup"><span data-stu-id="01f26-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="01f26-110">Графический</span><span class="sxs-lookup"><span data-stu-id="01f26-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="01f26-111">Рабочий процесс PowerShell</span><span class="sxs-lookup"><span data-stu-id="01f26-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="01f26-112">Это hello версии runbook рабочего процесса PowerShell этого сценария.</span><span class="sxs-lookup"><span data-stu-id="01f26-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="01f26-113">Также есть статья о [модулях Runbook с графическим интерфейсом](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="01f26-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="01f26-114">Начало сценария hello</span><span class="sxs-lookup"><span data-stu-id="01f26-114">Getting hello scenario</span></span>
<span data-ttu-id="01f26-115">Этот сценарий состоит из двух Runbook рабочего процесса PowerShell, которые можно загрузить из hello ссылкам.</span><span class="sxs-lookup"><span data-stu-id="01f26-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="01f26-116">В разделе hello [графической версии](automation-solution-startstopvm-graphical.md) этого сценария для графических модулей Runbook toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="01f26-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="01f26-117">Модуль Runbook</span><span class="sxs-lookup"><span data-stu-id="01f26-117">Runbook</span></span> | <span data-ttu-id="01f26-118">Ссылка</span><span class="sxs-lookup"><span data-stu-id="01f26-118">Link</span></span> | <span data-ttu-id="01f26-119">Тип</span><span class="sxs-lookup"><span data-stu-id="01f26-119">Type</span></span> | <span data-ttu-id="01f26-120">Описание</span><span class="sxs-lookup"><span data-stu-id="01f26-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01f26-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="01f26-121">Start-AzureVMs</span></span> |[<span data-ttu-id="01f26-122">Запуск классических виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="01f26-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="01f26-123">Рабочий процесс PowerShell</span><span class="sxs-lookup"><span data-stu-id="01f26-123">PowerShell Workflow</span></span> |<span data-ttu-id="01f26-124">Запуск всех классических виртуальных машин в подписке Azure или всех виртуальных машин с определенным именем службы.</span><span class="sxs-lookup"><span data-stu-id="01f26-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="01f26-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="01f26-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="01f26-126">Остановка классических виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="01f26-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="01f26-127">Рабочий процесс PowerShell</span><span class="sxs-lookup"><span data-stu-id="01f26-127">PowerShell Workflow</span></span> |<span data-ttu-id="01f26-128">Остановка всех классических виртуальных машин в учетной записи службы автоматизации или всех виртуальных машин с определенным именем службы.</span><span class="sxs-lookup"><span data-stu-id="01f26-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="01f26-129">Установка и настройка сценария hello</span><span class="sxs-lookup"><span data-stu-id="01f26-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="01f26-130">1. Установка модулей Runbook hello</span><span class="sxs-lookup"><span data-stu-id="01f26-130">1. Install hello runbooks</span></span>
<span data-ttu-id="01f26-131">После загрузки модулей Runbook hello, их можно импортировать с помощью процедуры hello в [импорт модуля Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="01f26-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="01f26-132">2. Просмотрите описание hello и требования</span><span class="sxs-lookup"><span data-stu-id="01f26-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="01f26-133">модули Runbook Hello включать текст комментария справки, который включает в себя описание и необходимые активы.</span><span class="sxs-lookup"><span data-stu-id="01f26-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="01f26-134">Можно также получить hello же сведения из этой статьи.</span><span class="sxs-lookup"><span data-stu-id="01f26-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="01f26-135">3. Настройка ресурсов</span><span class="sxs-lookup"><span data-stu-id="01f26-135">3. Configure assets</span></span>
<span data-ttu-id="01f26-136">Hello Runbook требуют hello следующие ресурсы, которые необходимо создать и заполнить с соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="01f26-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="01f26-137">Тип ресурса</span><span class="sxs-lookup"><span data-stu-id="01f26-137">Asset Type</span></span> | <span data-ttu-id="01f26-138">Имя ресурса</span><span class="sxs-lookup"><span data-stu-id="01f26-138">Asset Name</span></span> | <span data-ttu-id="01f26-139">Описание</span><span class="sxs-lookup"><span data-stu-id="01f26-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01f26-140">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="01f26-140">Credential</span></span> |<span data-ttu-id="01f26-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="01f26-141">AzureCredential</span></span> |<span data-ttu-id="01f26-142">Содержит учетные данные учетной записи, которая имеет полномочия toostart и остановки виртуальных машин в hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="01f26-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="01f26-143">Кроме того, можно указать другой ресурс учетных данных в hello **учетные данные** параметр hello **Add-AzureAccount** действия.</span><span class="sxs-lookup"><span data-stu-id="01f26-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="01f26-144">Переменная</span><span class="sxs-lookup"><span data-stu-id="01f26-144">Variable</span></span> |<span data-ttu-id="01f26-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="01f26-145">AzureSubscriptionId</span></span> |<span data-ttu-id="01f26-146">Содержит идентификатор подписки hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="01f26-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="01f26-147">С помощью сценария hello</span><span class="sxs-lookup"><span data-stu-id="01f26-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="01f26-148">Параметры</span><span class="sxs-lookup"><span data-stu-id="01f26-148">Parameters</span></span>
<span data-ttu-id="01f26-149">Каждый Hello Runbook имеют hello следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="01f26-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="01f26-150">Вам потребуется указать значения всех обязательных параметров и, при необходимости, указать значения дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="01f26-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="01f26-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="01f26-151">Parameter</span></span> | <span data-ttu-id="01f26-152">Тип</span><span class="sxs-lookup"><span data-stu-id="01f26-152">Type</span></span> | <span data-ttu-id="01f26-153">Обязательно</span><span class="sxs-lookup"><span data-stu-id="01f26-153">Mandatory</span></span> | <span data-ttu-id="01f26-154">Описание</span><span class="sxs-lookup"><span data-stu-id="01f26-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="01f26-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="01f26-155">ServiceName</span></span> |<span data-ttu-id="01f26-156">string</span><span class="sxs-lookup"><span data-stu-id="01f26-156">string</span></span> |<span data-ttu-id="01f26-157">Нет</span><span class="sxs-lookup"><span data-stu-id="01f26-157">No</span></span> |<span data-ttu-id="01f26-158">Если значение указано, запускаются или останавливаются все виртуальные машины с таким именем службы.</span><span class="sxs-lookup"><span data-stu-id="01f26-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="01f26-159">Если значение не указано, затем классических виртуальных машин в hello подписки Azure запуска или остановки.</span><span class="sxs-lookup"><span data-stu-id="01f26-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="01f26-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="01f26-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="01f26-161">string</span><span class="sxs-lookup"><span data-stu-id="01f26-161">string</span></span> |<span data-ttu-id="01f26-162">Нет</span><span class="sxs-lookup"><span data-stu-id="01f26-162">No</span></span> |<span data-ttu-id="01f26-163">Содержит имя hello hello [переменной активов](#installing-and-configuring-the-scenario) , содержащее идентификатор подписки hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="01f26-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="01f26-164">Если значение не указано, используется значение *AzureSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="01f26-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="01f26-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="01f26-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="01f26-166">string</span><span class="sxs-lookup"><span data-stu-id="01f26-166">string</span></span> |<span data-ttu-id="01f26-167">Нет</span><span class="sxs-lookup"><span data-stu-id="01f26-167">No</span></span> |<span data-ttu-id="01f26-168">Содержит имя hello hello [актива учетных данных](#installing-and-configuring-the-scenario) , содержащий hello учетные данные для hello runbook toouse.</span><span class="sxs-lookup"><span data-stu-id="01f26-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="01f26-169">Если не указать это значение, будет использоваться значение *AzureCredential* .</span><span class="sxs-lookup"><span data-stu-id="01f26-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="01f26-170">Запуск модулей Runbook hello</span><span class="sxs-lookup"><span data-stu-id="01f26-170">Starting hello runbooks</span></span>
<span data-ttu-id="01f26-171">Можно использовать любой из методов hello в [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md) toostart либо Runbook hello в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="01f26-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="01f26-172">Следующие примеры команд Hello использует Windows PowerShell toorun **StartAzureVMs** toostart все виртуальные машины с именем службы hello *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="01f26-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="01f26-173">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="01f26-173">Output</span></span>
<span data-ttu-id="01f26-174">модули Runbook Hello будет [выводить сообщение](automation-runbook-output-and-messages.md) для каждой виртуальной машины, указывающее, ли hello Пуск или инструкция stop успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="01f26-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="01f26-175">Можно найти конкретную строку в результате hello toodetermine hello выходные данные для каждого модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="01f26-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="01f26-176">в hello в следующей таблице перечислены строки возможного выхода Hello.</span><span class="sxs-lookup"><span data-stu-id="01f26-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="01f26-177">Модуль Runbook</span><span class="sxs-lookup"><span data-stu-id="01f26-177">Runbook</span></span> | <span data-ttu-id="01f26-178">Условие</span><span class="sxs-lookup"><span data-stu-id="01f26-178">Condition</span></span> | <span data-ttu-id="01f26-179">Сообщение</span><span class="sxs-lookup"><span data-stu-id="01f26-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="01f26-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="01f26-180">Start-AzureVMs</span></span> |<span data-ttu-id="01f26-181">Виртуальная машина уже запущена</span><span class="sxs-lookup"><span data-stu-id="01f26-181">Virtual machine is already running</span></span> |<span data-ttu-id="01f26-182">MyVM is already running</span><span class="sxs-lookup"><span data-stu-id="01f26-182">MyVM is already running</span></span> |
| <span data-ttu-id="01f26-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="01f26-183">Start-AzureVMs</span></span> |<span data-ttu-id="01f26-184">Запрос на запуск виртуальной машины успешно отправлен</span><span class="sxs-lookup"><span data-stu-id="01f26-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="01f26-185">MyVM has been started</span><span class="sxs-lookup"><span data-stu-id="01f26-185">MyVM has been started</span></span> |
| <span data-ttu-id="01f26-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="01f26-186">Start-AzureVMs</span></span> |<span data-ttu-id="01f26-187">Не удалось выполнить запрос запуска виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="01f26-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="01f26-188">Не удалось выполнить MyVM toostart</span><span class="sxs-lookup"><span data-stu-id="01f26-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="01f26-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="01f26-189">Stop-AzureVMs</span></span> |<span data-ttu-id="01f26-190">Виртуальная машина уже остановлена.</span><span class="sxs-lookup"><span data-stu-id="01f26-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="01f26-191">MyVM is already stopped</span><span class="sxs-lookup"><span data-stu-id="01f26-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="01f26-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="01f26-192">Stop-AzureVMs</span></span> |<span data-ttu-id="01f26-193">Запрос на остановку виртуальной машины успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="01f26-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="01f26-194">MyVM остановлена.</span><span class="sxs-lookup"><span data-stu-id="01f26-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="01f26-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="01f26-195">Stop-AzureVMs</span></span> |<span data-ttu-id="01f26-196">Не удалось отправить запрос на остановку виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="01f26-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="01f26-197">Не удалось выполнить MyVM toostop</span><span class="sxs-lookup"><span data-stu-id="01f26-197">MyVM failed toostop</span></span> |

<span data-ttu-id="01f26-198">Например, следующий фрагмент кода из модуля hello пытается toostart все виртуальные машины с именем службы hello *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="01f26-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="01f26-199">Если любой из hello запускается сбоев запросов, можно предпринять действия при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="01f26-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="01f26-200">Подробный разбор</span><span class="sxs-lookup"><span data-stu-id="01f26-200">Detailed breakdown</span></span>
<span data-ttu-id="01f26-201">Ниже приведен подробный разбор Runbook hello в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="01f26-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="01f26-202">Эти сведения можно использовать tooeither Настройка модулей Runbook hello или просто toolearn из них для создания собственных сценариев автоматизации.</span><span class="sxs-lookup"><span data-stu-id="01f26-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="01f26-203">Параметры</span><span class="sxs-lookup"><span data-stu-id="01f26-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="01f26-204">Hello рабочий процесс запускается путем получения значения hello для hello [входных параметров](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="01f26-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="01f26-205">Если имена ресурсов hello не указаны, используются имена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="01f26-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="01f26-206">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="01f26-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="01f26-207">Эта строка объявляет, что представляет собой строку hello выходные данные модуля runbook hello.</span><span class="sxs-lookup"><span data-stu-id="01f26-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="01f26-208">Это не является обязательным, но рекомендуется для при использовании hello runbook как [дочернего модуля runbook](automation-child-runbooks.md) , чтобы родительский модуль runbook знали вывода hello введите tooexpect.</span><span class="sxs-lookup"><span data-stu-id="01f26-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="01f26-209">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="01f26-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="01f26-210">следующие строки Hello задать hello [учетные данные](automation-credentials.md) и подписку Azure, которая будет использоваться для оставшихся hello hello runbook.</span><span class="sxs-lookup"><span data-stu-id="01f26-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="01f26-211">Сперва мы используем **Get-AutomationPSCredential** tooget hello актива, который содержит учетные данные hello с доступом toostart и остановки виртуальных машин в hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="01f26-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="01f26-212">**-AzureAccount** затем использует этот учетных данных ОС tooset hello.</span><span class="sxs-lookup"><span data-stu-id="01f26-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="01f26-213">выходные данные Hello назначается фиктивный tooa, чтобы он не включен в выходные данные runbook hello.</span><span class="sxs-lookup"><span data-stu-id="01f26-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="01f26-214">Hello переменной активов с Идентификатором затем извлекается с подпиской hello **Get-AutomationVariable** и hello подписки с **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="01f26-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="01f26-215">Получение виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="01f26-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="01f26-216">**Get-AzureVM** — используется tooretrieve hello виртуальных машин hello runbook будут работать с.</span><span class="sxs-lookup"><span data-stu-id="01f26-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="01f26-217">Если значение указано в hello **ServiceName** входных данных извлекаются переменной, а затем только hello виртуальных машин с таким именем службы.</span><span class="sxs-lookup"><span data-stu-id="01f26-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="01f26-218">Если значение **ServiceName** пустое, извлекаются все виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="01f26-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="01f26-219">Запуск и остановка виртуальных машин, отправка выходных данных</span><span class="sxs-lookup"><span data-stu-id="01f26-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="01f26-220">следующие строки Hello пошаговое выполнение каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="01f26-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="01f26-221">Здравствуйте, сначала **PowerState** hello виртуальной машины — checked toosee, если он уже работает или остановлена в зависимости от hello runbook.</span><span class="sxs-lookup"><span data-stu-id="01f26-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="01f26-222">Если он уже находится в состоянии целевой hello, сообщение отправляется toooutput и заканчивается runbook hello.</span><span class="sxs-lookup"><span data-stu-id="01f26-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="01f26-223">В противном случае нажмите **Start-AzureVM** или **Stop-AzureVM** используется tooattempt toostart или остановки hello виртуальная машина с результатом hello hello запрос хранимых tooa переменной.</span><span class="sxs-lookup"><span data-stu-id="01f26-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="01f26-224">Затем сообщение отправляется указание toooutput ли toostart запрос hello или stop был успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="01f26-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01f26-225">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01f26-225">Next steps</span></span>
* <span data-ttu-id="01f26-226">toolearn Дополнительные сведения о работе с дочерними модулями Runbook в разделе [дочерние модули Runbook в автоматизации Azure](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="01f26-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="01f26-227">Дополнительные сведения о toolearn выходных сообщений во время выполнения runbook и toohelp ведение журнала устранения неполадок см. в разделе [Runbook выходные данные и сообщения в службе автоматизации Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="01f26-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

