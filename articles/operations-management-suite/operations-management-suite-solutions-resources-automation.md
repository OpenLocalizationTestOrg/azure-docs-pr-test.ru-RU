---
title: "Ресурсы службы автоматизации Azure в решениях OMS | Документация Майкрософт"
description: "Как правило, решения в OMS содержат модули Runbook службы автоматизации Azure для автоматизации процессов, таких как сбор и обработка данных мониторинга.  В этой статье описывается, как добавлять модули Runbook и связанные с ними ресурсы в решение."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="05b6e-104">Добавление ресурсов службы автоматизации Azure в решение по управлению OMS (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="05b6e-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="05b6e-105">Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="05b6e-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="05b6e-106">Любые схемы, приведенные ниже, могут измениться.</span><span class="sxs-lookup"><span data-stu-id="05b6e-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="05b6e-107">Как правило, [решения для управления в OMS](operations-management-suite-solutions.md) содержат модули Runbook службы автоматизации Azure для автоматизации процессов, таких как сбор и обработка данных мониторинга.</span><span class="sxs-lookup"><span data-stu-id="05b6e-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="05b6e-108">Помимо модулей Runbook учетные записи службы автоматизации содержат ресурсы, такие как переменные и расписания, поддерживающие модули Runbook, используемые в решении.</span><span class="sxs-lookup"><span data-stu-id="05b6e-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="05b6e-109">В этой статье описывается, как добавлять модули Runbook и связанные с ними ресурсы в решение.</span><span class="sxs-lookup"><span data-stu-id="05b6e-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="05b6e-110">В примерах здесь используются обязательные или общие параметры и переменные для решений по управлению, описанные в статье [Создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="05b6e-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="05b6e-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="05b6e-111">Prerequisites</span></span>
<span data-ttu-id="05b6e-112">В этой статье предполагается, что вы уже знакомы со следующими сведениями.</span><span class="sxs-lookup"><span data-stu-id="05b6e-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="05b6e-113">Как [создать решение по управлению](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="05b6e-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="05b6e-114">Структура [файла решения](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="05b6e-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="05b6e-115">Как [создавать шаблоны Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="05b6e-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="05b6e-116">Учетная запись службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="05b6e-116">Automation account</span></span>
<span data-ttu-id="05b6e-117">Все ресурсы в службе автоматизации Azure содержатся в [учетной записи службы автоматизации](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="05b6e-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="05b6e-118">Как описано в разделе [Рабочая область OMS и учетная запись службы автоматизации](operations-management-suite-solutions.md#oms-workspace-and-automation-account), учетная запись службы автоматизации не включена в решение для управления и должна быть создана до установки решения.</span><span class="sxs-lookup"><span data-stu-id="05b6e-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="05b6e-119">Если она недоступна, произойдет сбой установки решения.</span><span class="sxs-lookup"><span data-stu-id="05b6e-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="05b6e-120">Имя учетной записи службы автоматизации указывается в имени каждого ресурса службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="05b6e-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="05b6e-121">Оно указывается в решении с помощью параметра **accountName**, как в следующем примере ресурса модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="05b6e-122">Модули Runbook</span><span class="sxs-lookup"><span data-stu-id="05b6e-122">Runbooks</span></span>
<span data-ttu-id="05b6e-123">В файл решения следует включить все модули Runbook, используемые решением, чтобы они создавались при установке решения.</span><span class="sxs-lookup"><span data-stu-id="05b6e-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="05b6e-124">Однако в шаблон нельзя добавить текст модуля Runbook, поэтому следует опубликовать модуль Runbook в общедоступном месте, где к нему может обратиться любой пользователь, устанавливающий решение.</span><span class="sxs-lookup"><span data-stu-id="05b6e-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="05b6e-125">Тип ресурсов [модуля Runbook службы автоматизации Azure](../automation/automation-runbook-types.md) — **Microsoft.Automation/automationAccounts/runbooks**. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="05b6e-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="05b6e-126">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="05b6e-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="05b6e-127">В следующей таблице описаны свойства модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="05b6e-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="05b6e-128">Property</span></span> | <span data-ttu-id="05b6e-129">Описание</span><span class="sxs-lookup"><span data-stu-id="05b6e-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="05b6e-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="05b6e-130">runbookType</span></span> |<span data-ttu-id="05b6e-131">Указывает тип модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="05b6e-132">Script — сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="05b6e-132">Script - PowerShell script</span></span> <br><span data-ttu-id="05b6e-133">PowerShell — рабочий процесс PowerShell</span><span class="sxs-lookup"><span data-stu-id="05b6e-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="05b6e-134">GraphPowerShell — графический модуль сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="05b6e-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="05b6e-135">GraphPowerShellWorkflow — графический модуль Runbook рабочего процесса PowerShell</span><span class="sxs-lookup"><span data-stu-id="05b6e-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="05b6e-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="05b6e-136">logProgress</span></span> |<span data-ttu-id="05b6e-137">Указывает, нужно ли создавать [записи о ходе выполнения](../automation/automation-runbook-output-and-messages.md) для модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="05b6e-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="05b6e-138">logVerbose</span></span> |<span data-ttu-id="05b6e-139">Указывает, нужно ли создавать [подробные записи](../automation/automation-runbook-output-and-messages.md) для модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="05b6e-140">Описание</span><span class="sxs-lookup"><span data-stu-id="05b6e-140">description</span></span> |<span data-ttu-id="05b6e-141">Необязательное описание модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="05b6e-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="05b6e-142">publishContentLink</span></span> |<span data-ttu-id="05b6e-143">Указывает содержимое модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="05b6e-144">uri — URI содержимого модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="05b6e-145">Это будет PS1-файл для модулей Runbook PowerShell и сценариев, а также файл экспортированного графического модуля Runbook для графического модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="05b6e-146">version — версия модуля Runbook для собственного отслеживания.</span><span class="sxs-lookup"><span data-stu-id="05b6e-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="05b6e-147">Задания службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="05b6e-147">Automation jobs</span></span>
<span data-ttu-id="05b6e-148">При запуске модуля Runbook в службе автоматизации Azure создается задание службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="05b6e-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="05b6e-149">Ресурс задания службы автоматизации можно добавить в решение для автоматического запуска модуля Runbook при установке решения по управлению.</span><span class="sxs-lookup"><span data-stu-id="05b6e-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="05b6e-150">Этот метод обычно используется для запуска модулей Runbook, которые используются для начальной настройки решения.</span><span class="sxs-lookup"><span data-stu-id="05b6e-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="05b6e-151">Для запуска модуля Runbook через регулярные интервалы создайте [расписание](#schedules) и [расписание заданий](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="05b6e-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="05b6e-152">Тип ресурсов задания — **Microsoft.Automation/automationAccounts/jobs**. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="05b6e-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="05b6e-153">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="05b6e-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="05b6e-154">В следующей таблице описаны свойства заданий службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="05b6e-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="05b6e-155">Свойство</span><span class="sxs-lookup"><span data-stu-id="05b6e-155">Property</span></span> | <span data-ttu-id="05b6e-156">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="05b6e-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="05b6e-157">runbook</span><span class="sxs-lookup"><span data-stu-id="05b6e-157">runbook</span></span> |<span data-ttu-id="05b6e-158">Одна сущность name с именем модуля Runbook для запуска.</span><span class="sxs-lookup"><span data-stu-id="05b6e-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="05b6e-159">parameters</span><span class="sxs-lookup"><span data-stu-id="05b6e-159">parameters</span></span> |<span data-ttu-id="05b6e-160">Сущность для каждого значения параметра, необходимого для модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="05b6e-161">Задание включает в себя имя модуля Runbook и все значения параметров, которые нужно отправить в модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="05b6e-162">Задание должно [зависеть от](operations-management-suite-solutions-solution-file.md#resources) модуля Runbook, который оно запускает, так как модуль Runbook нужно создать до задания.</span><span class="sxs-lookup"><span data-stu-id="05b6e-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="05b6e-163">При наличии нескольких модулей Runbook, которые нужно запустить, порядок их запуска можно определить, создав зависимость между заданием и другими заданиями, которые должны выполняться в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="05b6e-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="05b6e-164">Имя ресурса задания должно содержать GUID, который обычно назначается с помощью параметра.</span><span class="sxs-lookup"><span data-stu-id="05b6e-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="05b6e-165">Дополнительные сведения о параметрах GUID см. в статье [Создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="05b6e-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="05b6e-166">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="05b6e-166">Certificates</span></span>
<span data-ttu-id="05b6e-167">Тип [сертификатов службы автоматизации Azure](../automation/automation-certificates.md) — **Microsoft.Automation/automationAccounts/certificates**. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="05b6e-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="05b6e-168">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="05b6e-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="05b6e-169">В следующей таблице описаны свойства ресурсов сертификатов.</span><span class="sxs-lookup"><span data-stu-id="05b6e-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="05b6e-170">Свойство</span><span class="sxs-lookup"><span data-stu-id="05b6e-170">Property</span></span> | <span data-ttu-id="05b6e-171">Описание</span><span class="sxs-lookup"><span data-stu-id="05b6e-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="05b6e-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="05b6e-172">base64Value</span></span> |<span data-ttu-id="05b6e-173">Значение Base 64 для сертификата.</span><span class="sxs-lookup"><span data-stu-id="05b6e-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="05b6e-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="05b6e-174">thumbprint</span></span> |<span data-ttu-id="05b6e-175">Отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="05b6e-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="05b6e-176">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="05b6e-176">Credentials</span></span>
<span data-ttu-id="05b6e-177">Тип [учетных данных службы автоматизации Azure](../automation/automation-credentials.md) — **Microsoft.Automation/automationAccounts/credentials**. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="05b6e-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="05b6e-178">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="05b6e-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="05b6e-179">В следующей таблице описаны свойства ресурсов учетных записей.</span><span class="sxs-lookup"><span data-stu-id="05b6e-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="05b6e-180">Свойство</span><span class="sxs-lookup"><span data-stu-id="05b6e-180">Property</span></span> | <span data-ttu-id="05b6e-181">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="05b6e-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="05b6e-182">userName</span><span class="sxs-lookup"><span data-stu-id="05b6e-182">userName</span></span> |<span data-ttu-id="05b6e-183">Имя пользователя для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="05b6e-183">User name for the credential.</span></span> |
| <span data-ttu-id="05b6e-184">password</span><span class="sxs-lookup"><span data-stu-id="05b6e-184">password</span></span> |<span data-ttu-id="05b6e-185">Пароль для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="05b6e-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="05b6e-186">Расписания</span><span class="sxs-lookup"><span data-stu-id="05b6e-186">Schedules</span></span>
<span data-ttu-id="05b6e-187">Тип [расписаний службы автоматизации Azure](../automation/automation-schedules.md) — **Microsoft.Automation/automationAccounts/schedules**. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="05b6e-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="05b6e-188">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="05b6e-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="05b6e-189">В следующей таблице описаны свойства ресурсов расписания.</span><span class="sxs-lookup"><span data-stu-id="05b6e-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="05b6e-190">Свойство</span><span class="sxs-lookup"><span data-stu-id="05b6e-190">Property</span></span> | <span data-ttu-id="05b6e-191">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="05b6e-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="05b6e-192">Описание</span><span class="sxs-lookup"><span data-stu-id="05b6e-192">description</span></span> |<span data-ttu-id="05b6e-193">Необязательное описание расписания.</span><span class="sxs-lookup"><span data-stu-id="05b6e-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="05b6e-194">startTime</span><span class="sxs-lookup"><span data-stu-id="05b6e-194">startTime</span></span> |<span data-ttu-id="05b6e-195">Указывает время начала расписания в виде объекта DateTime.</span><span class="sxs-lookup"><span data-stu-id="05b6e-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="05b6e-196">Строка указывается, если ее можно преобразовать в допустимое значение даты и времени.</span><span class="sxs-lookup"><span data-stu-id="05b6e-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="05b6e-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="05b6e-197">isEnabled</span></span> |<span data-ttu-id="05b6e-198">Указывает, включено ли расписание.</span><span class="sxs-lookup"><span data-stu-id="05b6e-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="05b6e-199">interval</span><span class="sxs-lookup"><span data-stu-id="05b6e-199">interval</span></span> |<span data-ttu-id="05b6e-200">Тип интервала для расписания.</span><span class="sxs-lookup"><span data-stu-id="05b6e-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="05b6e-201">day</span><span class="sxs-lookup"><span data-stu-id="05b6e-201">day</span></span><br><span data-ttu-id="05b6e-202">hour</span><span class="sxs-lookup"><span data-stu-id="05b6e-202">hour</span></span> |
| <span data-ttu-id="05b6e-203">frequency</span><span class="sxs-lookup"><span data-stu-id="05b6e-203">frequency</span></span> |<span data-ttu-id="05b6e-204">Частота, с которой срабатывает расписание (количество дней или часов).</span><span class="sxs-lookup"><span data-stu-id="05b6e-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="05b6e-205">Значение времени начала для расписаний должно быть больше, чем значение текущего времени.</span><span class="sxs-lookup"><span data-stu-id="05b6e-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="05b6e-206">Это значение невозможно указать в переменной, так как вы не сможете узнать время установки.</span><span class="sxs-lookup"><span data-stu-id="05b6e-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="05b6e-207">При использовании ресурсов расписания в решении следуйте одной из следующих двух стратегий.</span><span class="sxs-lookup"><span data-stu-id="05b6e-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="05b6e-208">Используйте параметр для времени запуска в расписании.</span><span class="sxs-lookup"><span data-stu-id="05b6e-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="05b6e-209">Таким образом, пользователю будет предложено ввести значение при установке решения.</span><span class="sxs-lookup"><span data-stu-id="05b6e-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="05b6e-210">Если у вас есть несколько расписаний, для них можно использовать одно значение параметра.</span><span class="sxs-lookup"><span data-stu-id="05b6e-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="05b6e-211">Создайте расписание с помощью модуля Runbook, который запускается после установки решения.</span><span class="sxs-lookup"><span data-stu-id="05b6e-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="05b6e-212">Таким образом, пользователю не нужно будет указывать время. Однако нельзя добавлять расписание в решение, так как при его удалении расписание тоже будет удалено.</span><span class="sxs-lookup"><span data-stu-id="05b6e-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="05b6e-213">Расписания заданий</span><span class="sxs-lookup"><span data-stu-id="05b6e-213">Job schedules</span></span>
<span data-ttu-id="05b6e-214">Ресурсы расписания заданий связывают модуль Runbook с расписанием.</span><span class="sxs-lookup"><span data-stu-id="05b6e-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="05b6e-215">Их тип — **Microsoft.Automation/automationAccounts/jobSchedules**. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="05b6e-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="05b6e-216">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="05b6e-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="05b6e-217">В следующей таблице описаны свойства расписаний заданий.</span><span class="sxs-lookup"><span data-stu-id="05b6e-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="05b6e-218">Свойство</span><span class="sxs-lookup"><span data-stu-id="05b6e-218">Property</span></span> | <span data-ttu-id="05b6e-219">Описание</span><span class="sxs-lookup"><span data-stu-id="05b6e-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="05b6e-220">schedule name</span><span class="sxs-lookup"><span data-stu-id="05b6e-220">schedule name</span></span> |<span data-ttu-id="05b6e-221">Одна сущность **name** с именем расписания.</span><span class="sxs-lookup"><span data-stu-id="05b6e-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="05b6e-222">runbook name</span><span class="sxs-lookup"><span data-stu-id="05b6e-222">runbook name</span></span>  |<span data-ttu-id="05b6e-223">Одна сущность **name** с именем модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="05b6e-224">Переменные</span><span class="sxs-lookup"><span data-stu-id="05b6e-224">Variables</span></span>
<span data-ttu-id="05b6e-225">Тип [переменных службы автоматизации Azure](../automation/automation-variables.md) — **Microsoft.Automation/automationAccounts/variables**. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="05b6e-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="05b6e-226">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="05b6e-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="05b6e-227">В следующей таблице описаны свойства ресурсов переменной.</span><span class="sxs-lookup"><span data-stu-id="05b6e-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="05b6e-228">Свойство</span><span class="sxs-lookup"><span data-stu-id="05b6e-228">Property</span></span> | <span data-ttu-id="05b6e-229">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="05b6e-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="05b6e-230">Описание</span><span class="sxs-lookup"><span data-stu-id="05b6e-230">description</span></span> | <span data-ttu-id="05b6e-231">Необязательное описание переменной.</span><span class="sxs-lookup"><span data-stu-id="05b6e-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="05b6e-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="05b6e-232">isEncrypted</span></span> | <span data-ttu-id="05b6e-233">Указывает, следует ли шифровать переменную.</span><span class="sxs-lookup"><span data-stu-id="05b6e-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="05b6e-234">type</span><span class="sxs-lookup"><span data-stu-id="05b6e-234">type</span></span> | <span data-ttu-id="05b6e-235">Сейчас это свойство ни на что не влияет.</span><span class="sxs-lookup"><span data-stu-id="05b6e-235">This property currently has no effect.</span></span>  <span data-ttu-id="05b6e-236">Тип данных переменной определяется начальным значением.</span><span class="sxs-lookup"><span data-stu-id="05b6e-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="05b6e-237">value</span><span class="sxs-lookup"><span data-stu-id="05b6e-237">value</span></span> | <span data-ttu-id="05b6e-238">Значение переменной.</span><span class="sxs-lookup"><span data-stu-id="05b6e-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="05b6e-239">Сейчас свойство **type** не влияет на создаваемую переменную.</span><span class="sxs-lookup"><span data-stu-id="05b6e-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="05b6e-240">Тип данных переменной определяется значением.</span><span class="sxs-lookup"><span data-stu-id="05b6e-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="05b6e-241">Если для переменной задается начальное значение, его необходимо настроить в качестве правильного типа данных.</span><span class="sxs-lookup"><span data-stu-id="05b6e-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="05b6e-242">В таблице ниже приведены различные допустимые типы данных и их синтаксис.</span><span class="sxs-lookup"><span data-stu-id="05b6e-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="05b6e-243">Обратите внимание, что значения в JSON всегда должны заключаться в кавычки со всеми специальными знаками.</span><span class="sxs-lookup"><span data-stu-id="05b6e-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="05b6e-244">Например, строковое значение задается с парами кавычек в начале и в конце строки (с escape-символом (\\)), а числовое значение задается с одной парой кавычек.</span><span class="sxs-lookup"><span data-stu-id="05b6e-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="05b6e-245">Тип данных</span><span class="sxs-lookup"><span data-stu-id="05b6e-245">Data type</span></span> | <span data-ttu-id="05b6e-246">Описание</span><span class="sxs-lookup"><span data-stu-id="05b6e-246">Description</span></span> | <span data-ttu-id="05b6e-247">Пример</span><span class="sxs-lookup"><span data-stu-id="05b6e-247">Example</span></span> | <span data-ttu-id="05b6e-248">Результат разрешения</span><span class="sxs-lookup"><span data-stu-id="05b6e-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="05b6e-249">string</span><span class="sxs-lookup"><span data-stu-id="05b6e-249">string</span></span>   | <span data-ttu-id="05b6e-250">Заключает значение в две пары кавычек.</span><span class="sxs-lookup"><span data-stu-id="05b6e-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="05b6e-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="05b6e-251">"\"Hello world\""</span></span> | <span data-ttu-id="05b6e-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="05b6e-252">"Hello world"</span></span> |
| <span data-ttu-id="05b6e-253">numeric</span><span class="sxs-lookup"><span data-stu-id="05b6e-253">numeric</span></span>  | <span data-ttu-id="05b6e-254">Числовое значение с одной парой кавычек.</span><span class="sxs-lookup"><span data-stu-id="05b6e-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="05b6e-255">"64"</span><span class="sxs-lookup"><span data-stu-id="05b6e-255">"64"</span></span> | <span data-ttu-id="05b6e-256">64</span><span class="sxs-lookup"><span data-stu-id="05b6e-256">64</span></span> |
| <span data-ttu-id="05b6e-257">Логическое</span><span class="sxs-lookup"><span data-stu-id="05b6e-257">boolean</span></span>  | <span data-ttu-id="05b6e-258">Значение **true** или **false** в кавычках.</span><span class="sxs-lookup"><span data-stu-id="05b6e-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="05b6e-259">Обратите внимание, что это значение должно быть в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="05b6e-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="05b6e-260">True</span><span class="sxs-lookup"><span data-stu-id="05b6e-260">"true"</span></span> | <span data-ttu-id="05b6e-261">Да</span><span class="sxs-lookup"><span data-stu-id="05b6e-261">true</span></span> |
| <span data-ttu-id="05b6e-262">Datetime</span><span class="sxs-lookup"><span data-stu-id="05b6e-262">datetime</span></span> | <span data-ttu-id="05b6e-263">Сериализованное значение даты.</span><span class="sxs-lookup"><span data-stu-id="05b6e-263">Serialized date value.</span></span><br><span data-ttu-id="05b6e-264">Вы можете создать это значение для определенной даты с помощью командлета ConvertTo-Json в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05b6e-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="05b6e-265">Пример: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="05b6e-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="05b6e-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="05b6e-266">ConvertTo-Json</span></span> | <span data-ttu-id="05b6e-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="05b6e-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="05b6e-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="05b6e-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="05b6e-269">модули</span><span class="sxs-lookup"><span data-stu-id="05b6e-269">Modules</span></span>
<span data-ttu-id="05b6e-270">Решению для управления не нужно определять [глобальные модули](../automation/automation-integration-modules.md), используемые в модулях Runbook, так как они будут доступны постоянно в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="05b6e-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="05b6e-271">Необходимо включить ресурс для любого модуля, используемого в модулях Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="05b6e-272">[Тип модулей интеграции](../automation/automation-integration-modules.md) — **Microsoft.Automation/automationAccounts/modules**. Их структура приведена ниже.</span><span class="sxs-lookup"><span data-stu-id="05b6e-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="05b6e-273">Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров.</span><span class="sxs-lookup"><span data-stu-id="05b6e-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="05b6e-274">В следующей таблице описаны свойства ресурсов модуля.</span><span class="sxs-lookup"><span data-stu-id="05b6e-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="05b6e-275">Свойство</span><span class="sxs-lookup"><span data-stu-id="05b6e-275">Property</span></span> | <span data-ttu-id="05b6e-276">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="05b6e-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="05b6e-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="05b6e-277">contentLink</span></span> |<span data-ttu-id="05b6e-278">Указывает содержимое модуля.</span><span class="sxs-lookup"><span data-stu-id="05b6e-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="05b6e-279">uri — URI содержимого модуля.</span><span class="sxs-lookup"><span data-stu-id="05b6e-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="05b6e-280">Это будет PS1-файл для модулей Runbook PowerShell и сценариев, а также файл экспортированного графического модуля Runbook для графического модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="05b6e-281">version — версия модуля для собственного отслеживания.</span><span class="sxs-lookup"><span data-stu-id="05b6e-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="05b6e-282">Модуль Runbook должен зависеть от ресурса модуля, чтобы этот ресурс создавался до модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="05b6e-283">Обновление модулей</span><span class="sxs-lookup"><span data-stu-id="05b6e-283">Updating modules</span></span>
<span data-ttu-id="05b6e-284">Если при обновлении решения для управления, включающего в себя модуль Runbook, который использует расписание, обновляется и модуль, используемый модулем Runbook, то Runbook может вернуться к старой версии модуля.</span><span class="sxs-lookup"><span data-stu-id="05b6e-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="05b6e-285">В решение следует добавить указанные ниже модули Runbook и создать задание для их выполнения перед выполнением остальных модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="05b6e-286">Таким образом все модули будут обновляться, как указано, перед загрузкой модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="05b6e-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) обеспечивает то, что модули Runbook в решении используют модули последней версии.</span><span class="sxs-lookup"><span data-stu-id="05b6e-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="05b6e-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) повторно зарегистрирует все ресурсы расписания, чтобы обеспечить, что модули Runbook, связанные с ними, используют модули последней версии.</span><span class="sxs-lookup"><span data-stu-id="05b6e-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="05b6e-289">Образец</span><span class="sxs-lookup"><span data-stu-id="05b6e-289">Sample</span></span>
<span data-ttu-id="05b6e-290">Ниже приведен пример решения со приведенными ниже ресурсами.</span><span class="sxs-lookup"><span data-stu-id="05b6e-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="05b6e-291">Модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="05b6e-291">Runbook.</span></span>  <span data-ttu-id="05b6e-292">Это пример модуля Runbook, хранящийся в общедоступном репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="05b6e-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="05b6e-293">Задание службы автоматизации, которое запускает модуль Runbook при установке решения.</span><span class="sxs-lookup"><span data-stu-id="05b6e-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="05b6e-294">Расписание и расписание заданий для запуска модуля Runbook через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="05b6e-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="05b6e-295">Сертификат.</span><span class="sxs-lookup"><span data-stu-id="05b6e-295">Certificate.</span></span>
- <span data-ttu-id="05b6e-296">Учетные данные.</span><span class="sxs-lookup"><span data-stu-id="05b6e-296">Credential.</span></span>
- <span data-ttu-id="05b6e-297">Переменная.</span><span class="sxs-lookup"><span data-stu-id="05b6e-297">Variable.</span></span>
- <span data-ttu-id="05b6e-298">Модуль.</span><span class="sxs-lookup"><span data-stu-id="05b6e-298">Module.</span></span>  <span data-ttu-id="05b6e-299">Это [модуль OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) для записи данных в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="05b6e-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="05b6e-300">В примере используются переменные [стандартных параметров решения](operations-management-suite-solutions-solution-file.md#parameters), что является общепринятой практикой для решений, в отличие от жестко программируемых значений в определениях ресурсов.</span><span class="sxs-lookup"><span data-stu-id="05b6e-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="05b6e-301">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05b6e-301">Next steps</span></span>
* <span data-ttu-id="05b6e-302">[Добавьте представление в решение](operations-management-suite-solutions-resources-views.md) для визуализации собранных данных.</span><span class="sxs-lookup"><span data-stu-id="05b6e-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
