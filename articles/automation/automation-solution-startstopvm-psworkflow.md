---
title: "Запуск и остановка виртуальных машин с помощью службы автоматизации Azure: рабочий процесс PowerShell | Документация Майкрософт"
description: "Версия сценария с графическим интерфейсом для службы автоматизации Azure, включая модули Runbook для запуска и остановки классических виртуальных машин."
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
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="26bcb-103">Сценарий для службы автоматизации Azure: запуск и остановка виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="26bcb-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="26bcb-104">В этот сценарий для службы автоматизации Azure входят модули Runbook для запуска и остановки классических виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="26bcb-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="26bcb-105">С этим сценарием вы можете:</span><span class="sxs-lookup"><span data-stu-id="26bcb-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="26bcb-106">использовать модули Runbook без внесения изменений в свою рабочую среду;</span><span class="sxs-lookup"><span data-stu-id="26bcb-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="26bcb-107">реализовать дополнительные функциональные возможности посредством изменения модулей Runbook;</span><span class="sxs-lookup"><span data-stu-id="26bcb-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="26bcb-108">вызывать модули Runbook из другого модуля Runbook в рамках общего решения;</span><span class="sxs-lookup"><span data-stu-id="26bcb-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="26bcb-109">использовать модули Runbook в качестве учебников для ознакомления с основными концепциями создания таких модулей.</span><span class="sxs-lookup"><span data-stu-id="26bcb-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="26bcb-110">Графический</span><span class="sxs-lookup"><span data-stu-id="26bcb-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="26bcb-111">Рабочий процесс PowerShell</span><span class="sxs-lookup"><span data-stu-id="26bcb-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="26bcb-112">В этой статье описывается сценарий применения модулей Runbook для рабочих процессов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26bcb-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="26bcb-113">Также есть статья о [модулях Runbook с графическим интерфейсом](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="26bcb-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="26bcb-114">Получение сценария</span><span class="sxs-lookup"><span data-stu-id="26bcb-114">Getting the scenario</span></span>
<span data-ttu-id="26bcb-115">Этот сценарий состоит из двух модулей Runbook для рабочих процессов PowerShell. Эти модули можно скачать по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="26bcb-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="26bcb-116">Ссылки на графические модули Runbook для сценария с графическим интерфейсом приведены в [соответствующей статье](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="26bcb-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="26bcb-117">Модуль Runbook</span><span class="sxs-lookup"><span data-stu-id="26bcb-117">Runbook</span></span> | <span data-ttu-id="26bcb-118">Ссылка</span><span class="sxs-lookup"><span data-stu-id="26bcb-118">Link</span></span> | <span data-ttu-id="26bcb-119">Тип</span><span class="sxs-lookup"><span data-stu-id="26bcb-119">Type</span></span> | <span data-ttu-id="26bcb-120">Описание</span><span class="sxs-lookup"><span data-stu-id="26bcb-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="26bcb-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="26bcb-121">Start-AzureVMs</span></span> |[<span data-ttu-id="26bcb-122">Запуск классических виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="26bcb-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="26bcb-123">Рабочий процесс PowerShell</span><span class="sxs-lookup"><span data-stu-id="26bcb-123">PowerShell Workflow</span></span> |<span data-ttu-id="26bcb-124">Запуск всех классических виртуальных машин в подписке Azure или всех виртуальных машин с определенным именем службы.</span><span class="sxs-lookup"><span data-stu-id="26bcb-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="26bcb-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="26bcb-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="26bcb-126">Остановка классических виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="26bcb-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="26bcb-127">Рабочий процесс PowerShell</span><span class="sxs-lookup"><span data-stu-id="26bcb-127">PowerShell Workflow</span></span> |<span data-ttu-id="26bcb-128">Остановка всех классических виртуальных машин в учетной записи службы автоматизации или всех виртуальных машин с определенным именем службы.</span><span class="sxs-lookup"><span data-stu-id="26bcb-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="26bcb-129">Установка и настройка сценария</span><span class="sxs-lookup"><span data-stu-id="26bcb-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="26bcb-130">1. Установка модулей Runbook</span><span class="sxs-lookup"><span data-stu-id="26bcb-130">1. Install the runbooks</span></span>
<span data-ttu-id="26bcb-131">Загрузив модули Runbook, импортируйте их, как описано в статье [Импорт модуля Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="26bcb-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="26bcb-132">2. Просмотр описания и требований</span><span class="sxs-lookup"><span data-stu-id="26bcb-132">2. Review the description and requirements</span></span>
<span data-ttu-id="26bcb-133">Модули Runbook содержат справочные комментарии с описанием и сведениями о необходимых ресурсах.</span><span class="sxs-lookup"><span data-stu-id="26bcb-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="26bcb-134">Аналогичную информацию можно получить из этой статьи.</span><span class="sxs-lookup"><span data-stu-id="26bcb-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="26bcb-135">3. Настройка ресурсов</span><span class="sxs-lookup"><span data-stu-id="26bcb-135">3. Configure assets</span></span>
<span data-ttu-id="26bcb-136">Для модулей Runbook нужно создать перечисленные ниже ресурсы, после чего добавить в них соответствующие значения.</span><span class="sxs-lookup"><span data-stu-id="26bcb-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="26bcb-137">Тип ресурса</span><span class="sxs-lookup"><span data-stu-id="26bcb-137">Asset Type</span></span> | <span data-ttu-id="26bcb-138">Имя ресурса</span><span class="sxs-lookup"><span data-stu-id="26bcb-138">Asset Name</span></span> | <span data-ttu-id="26bcb-139">Описание</span><span class="sxs-lookup"><span data-stu-id="26bcb-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="26bcb-140">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="26bcb-140">Credential</span></span> |<span data-ttu-id="26bcb-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="26bcb-141">AzureCredential</span></span> |<span data-ttu-id="26bcb-142">Содержит учетные данные для учетной записи, имеющей полномочия для запуска и остановки виртуальных машин в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="26bcb-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="26bcb-143">Кроме того, вы можете указать другой ресурс учетных данных. Для этого используйте параметр **Credential** действия **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="26bcb-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="26bcb-144">Переменная</span><span class="sxs-lookup"><span data-stu-id="26bcb-144">Variable</span></span> |<span data-ttu-id="26bcb-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="26bcb-145">AzureSubscriptionId</span></span> |<span data-ttu-id="26bcb-146">Содержит идентификатор вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="26bcb-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="26bcb-147">Использование сценария</span><span class="sxs-lookup"><span data-stu-id="26bcb-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="26bcb-148">Параметры</span><span class="sxs-lookup"><span data-stu-id="26bcb-148">Parameters</span></span>
<span data-ttu-id="26bcb-149">Модули Runbooks имеют следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="26bcb-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="26bcb-150">Вам необходимо указать значения всех обязательных параметров. Также по желанию можно указать значения дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="26bcb-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="26bcb-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="26bcb-151">Parameter</span></span> | <span data-ttu-id="26bcb-152">Тип</span><span class="sxs-lookup"><span data-stu-id="26bcb-152">Type</span></span> | <span data-ttu-id="26bcb-153">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26bcb-153">Mandatory</span></span> | <span data-ttu-id="26bcb-154">Описание</span><span class="sxs-lookup"><span data-stu-id="26bcb-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="26bcb-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="26bcb-155">ServiceName</span></span> |<span data-ttu-id="26bcb-156">string</span><span class="sxs-lookup"><span data-stu-id="26bcb-156">string</span></span> |<span data-ttu-id="26bcb-157">Нет</span><span class="sxs-lookup"><span data-stu-id="26bcb-157">No</span></span> |<span data-ttu-id="26bcb-158">Если значение указано, запускаются или останавливаются все виртуальные машины с таким именем службы.</span><span class="sxs-lookup"><span data-stu-id="26bcb-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="26bcb-159">Если значение не указано, запускаются или останавливаются все классические виртуальные машины в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="26bcb-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="26bcb-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="26bcb-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="26bcb-161">string</span><span class="sxs-lookup"><span data-stu-id="26bcb-161">string</span></span> |<span data-ttu-id="26bcb-162">Нет</span><span class="sxs-lookup"><span data-stu-id="26bcb-162">No</span></span> |<span data-ttu-id="26bcb-163">Содержит имя [ресурса переменной](#installing-and-configuring-the-scenario) , в котором указан идентификатор вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="26bcb-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="26bcb-164">Если значение не указано, используется значение *AzureSubscriptionId* .</span><span class="sxs-lookup"><span data-stu-id="26bcb-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="26bcb-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="26bcb-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="26bcb-166">string</span><span class="sxs-lookup"><span data-stu-id="26bcb-166">string</span></span> |<span data-ttu-id="26bcb-167">Нет</span><span class="sxs-lookup"><span data-stu-id="26bcb-167">No</span></span> |<span data-ttu-id="26bcb-168">Содержит имя [ресурса учетных данных](#installing-and-configuring-the-scenario) , в котором указаны учетные данные используемого модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="26bcb-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="26bcb-169">Если не указать это значение, будет использоваться значение *AzureCredential* .</span><span class="sxs-lookup"><span data-stu-id="26bcb-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="26bcb-170">Запуск модулей Runbook</span><span class="sxs-lookup"><span data-stu-id="26bcb-170">Starting the runbooks</span></span>
<span data-ttu-id="26bcb-171">Для запуска модуля Runbook в данном сценарии можно использовать любой из методов, описанных в статье [Запуск модуля Runbook в службе автоматизации Azure](automation-starting-a-runbook.md) .</span><span class="sxs-lookup"><span data-stu-id="26bcb-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="26bcb-172">Приведенные ниже команды выполняются в Windows PowerShell. Они запускают модуль **StartAzureVMs**, который запускает все виртуальные машины с именем службы *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="26bcb-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="26bcb-173">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="26bcb-173">Output</span></span>
<span data-ttu-id="26bcb-174">При выполнении модулей выводятся [сообщения](automation-runbook-output-and-messages.md) для каждой виртуальной машины. Из них можно узнать о результатах инструкций запуска или остановки.</span><span class="sxs-lookup"><span data-stu-id="26bcb-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="26bcb-175">Чтобы определить результат выполнения каждого модуля Runbook, найдите в выходных данных соответствующую строку.</span><span class="sxs-lookup"><span data-stu-id="26bcb-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="26bcb-176">В следующей таблице перечислены возможные варианты выходных данных.</span><span class="sxs-lookup"><span data-stu-id="26bcb-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="26bcb-177">Модуль Runbook</span><span class="sxs-lookup"><span data-stu-id="26bcb-177">Runbook</span></span> | <span data-ttu-id="26bcb-178">Условие</span><span class="sxs-lookup"><span data-stu-id="26bcb-178">Condition</span></span> | <span data-ttu-id="26bcb-179">Сообщение</span><span class="sxs-lookup"><span data-stu-id="26bcb-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="26bcb-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="26bcb-180">Start-AzureVMs</span></span> |<span data-ttu-id="26bcb-181">Виртуальная машина уже запущена</span><span class="sxs-lookup"><span data-stu-id="26bcb-181">Virtual machine is already running</span></span> |<span data-ttu-id="26bcb-182">MyVM is already running</span><span class="sxs-lookup"><span data-stu-id="26bcb-182">MyVM is already running</span></span> |
| <span data-ttu-id="26bcb-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="26bcb-183">Start-AzureVMs</span></span> |<span data-ttu-id="26bcb-184">Запрос на запуск виртуальной машины успешно отправлен</span><span class="sxs-lookup"><span data-stu-id="26bcb-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="26bcb-185">MyVM has been started</span><span class="sxs-lookup"><span data-stu-id="26bcb-185">MyVM has been started</span></span> |
| <span data-ttu-id="26bcb-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="26bcb-186">Start-AzureVMs</span></span> |<span data-ttu-id="26bcb-187">Не удалось отправить запрос на запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="26bcb-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="26bcb-188">MyVM failed to start</span><span class="sxs-lookup"><span data-stu-id="26bcb-188">MyVM failed to start</span></span> |
| <span data-ttu-id="26bcb-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="26bcb-189">Stop-AzureVMs</span></span> |<span data-ttu-id="26bcb-190">Виртуальная машина уже остановлена.</span><span class="sxs-lookup"><span data-stu-id="26bcb-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="26bcb-191">MyVM is already stopped</span><span class="sxs-lookup"><span data-stu-id="26bcb-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="26bcb-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="26bcb-192">Stop-AzureVMs</span></span> |<span data-ttu-id="26bcb-193">Запрос на остановку виртуальной машины успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="26bcb-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="26bcb-194">MyVM остановлена.</span><span class="sxs-lookup"><span data-stu-id="26bcb-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="26bcb-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="26bcb-195">Stop-AzureVMs</span></span> |<span data-ttu-id="26bcb-196">Не удалось отправить запрос на остановку виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="26bcb-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="26bcb-197">Не удалось остановить MyVM.</span><span class="sxs-lookup"><span data-stu-id="26bcb-197">MyVM failed to stop</span></span> |

<span data-ttu-id="26bcb-198">Например, следующий фрагмент кода в модуле Runbook пытается запустить все виртуальные машины с именем службы *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="26bcb-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="26bcb-199">Если какой-либо из запросов на запуск не будет выполнен, вы сможете попытаться устранить ошибку.</span><span class="sxs-lookup"><span data-stu-id="26bcb-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="26bcb-200">Подробный разбор</span><span class="sxs-lookup"><span data-stu-id="26bcb-200">Detailed breakdown</span></span>
<span data-ttu-id="26bcb-201">Ниже приведен подробный разбор модулей Runbook из этого сценария.</span><span class="sxs-lookup"><span data-stu-id="26bcb-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="26bcb-202">Вы можете использовать эти сведения для настройки модулей Runbook или просто для их изучения с целью создания собственных сценариев автоматизации.</span><span class="sxs-lookup"><span data-stu-id="26bcb-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="26bcb-203">Параметры</span><span class="sxs-lookup"><span data-stu-id="26bcb-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="26bcb-204">Рабочий процесс начинается с получения значений для [входных параметров](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="26bcb-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="26bcb-205">Если имена ресурсов не указаны, используются имена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="26bcb-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="26bcb-206">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="26bcb-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="26bcb-207">В этой строке кода объявляется строковый тип выходных данных модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="26bcb-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="26bcb-208">Это действие не обязательно, но рекомендуется не пропускать его на случай, если модуль Runbook будет использоваться как [дочерний](automation-child-runbooks.md). В результате родительский модуль Runbook будет знать тип выходных данных дочернего модуля.</span><span class="sxs-lookup"><span data-stu-id="26bcb-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="26bcb-209">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="26bcb-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="26bcb-210">Следующие строки определяют [учетные данные](automation-credentials.md) и подписку Azure, которые будут использоваться в остальной части Runbook.</span><span class="sxs-lookup"><span data-stu-id="26bcb-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="26bcb-211">Сначала мы используем **Get-AutomationPSCredential** , чтобы получить ресурс с учетными данными для запуска и остановки виртуальных машин в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="26bcb-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="26bcb-212">**Add-AzureAccount** использует этот ресурс для добавления учетных данных.</span><span class="sxs-lookup"><span data-stu-id="26bcb-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="26bcb-213">Выходные данные передаются в фиктивную переменную, чтобы они не включались в выходные данные модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="26bcb-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="26bcb-214">Затем с помощью **Get-AutomationVariable** извлекается ресурс-контейнер переменной с идентификатором подписки, а с помощью **Select-AzureSubscription** выбирается подписка.</span><span class="sxs-lookup"><span data-stu-id="26bcb-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="26bcb-215">Получение виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="26bcb-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="26bcb-216">**Get-AzureVM** используется для получения виртуальных машин, с которыми будет работать модуль.</span><span class="sxs-lookup"><span data-stu-id="26bcb-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="26bcb-217">Если входной переменной **ServiceName** присвоено значение, будут извлечены только виртуальные машины с указанным именем службы.</span><span class="sxs-lookup"><span data-stu-id="26bcb-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="26bcb-218">Если значение **ServiceName** пустое, извлекаются все виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="26bcb-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="26bcb-219">Запуск и остановка виртуальных машин, отправка выходных данных</span><span class="sxs-lookup"><span data-stu-id="26bcb-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="26bcb-220">На следующем этапе выполняется перебор всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="26bcb-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="26bcb-221">Сначала проверяется свойство **PowerState**, чтобы определить состояние виртуальной машины: запущена или остановлена (в зависимости от модуля Runbook).</span><span class="sxs-lookup"><span data-stu-id="26bcb-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="26bcb-222">Если машина уже находится в нужном состоянии, в выходные данные отправляется сообщение и выполнение модуля Runbook завершается.</span><span class="sxs-lookup"><span data-stu-id="26bcb-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="26bcb-223">В противном случае используется команда **Start-AzureVM** или **Stop-AzureVM** для запуска или остановки виртуальной машины. Результат запроса сохраняется в переменной.</span><span class="sxs-lookup"><span data-stu-id="26bcb-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="26bcb-224">Затем в выходные данные отправляется сообщение с указанием результата запроса на запуск или остановку.</span><span class="sxs-lookup"><span data-stu-id="26bcb-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26bcb-225">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26bcb-225">Next steps</span></span>
* <span data-ttu-id="26bcb-226">Дополнительные сведения о работе с дочерними модулями Runbook см. в статье [Дочерние модули Runbook в службе автоматизации Azure](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="26bcb-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="26bcb-227">Чтобы узнать больше о выходных сообщениях во время выполнения Runbook и ведении журнала для устранения неполадок, ознакомьтесь с разделом [Выходные данные и сообщения Runbook в службе автоматизации Azure](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="26bcb-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

