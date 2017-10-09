---
title: "ресурсы автоматизации aaaAzure решения OMS | Документы Microsoft"
description: "Как правило, решения в OMS включает модули Runbook в автоматизации Azure tooautomate процессов, таких как сбор и обработку данных мониторинга.  В этой статье описывается как tooinclude модулей Runbook и их связанные ресурсы в решении."
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
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="90ab9-104">Добавление решение управления OMS tooan ресурсы службы автоматизации Azure (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="90ab9-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="90ab9-105">Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="90ab9-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="90ab9-106">Ни одной схеме, описанной ниже — toochange субъекта.</span><span class="sxs-lookup"><span data-stu-id="90ab9-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="90ab9-107">[Решения для управления в OMS](operations-management-suite-solutions.md) как правило, включают модули Runbook в автоматизации Azure tooautomate процессов, таких как сбор и обработку данных мониторинга.</span><span class="sxs-lookup"><span data-stu-id="90ab9-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="90ab9-108">В дополнение к этому toorunbooks, учетные записи автоматизации включает средства, такие как переменные и расписаний, которые поддерживают hello модулей Runbook используется в решении hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="90ab9-109">В этой статье описывается как tooinclude модулей Runbook и их связанные ресурсы в решении.</span><span class="sxs-lookup"><span data-stu-id="90ab9-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="90ab9-110">Hello примеры в этой статье с помощью параметров и переменные, которые либо обязательными или общие toomanagement решений и описано в [создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="90ab9-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="90ab9-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90ab9-111">Prerequisites</span></span>
<span data-ttu-id="90ab9-112">В этой статье предполагается, что вы уже знакомы с hello следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="90ab9-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="90ab9-113">Как слишком[создать решение для управления](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="90ab9-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="90ab9-114">Здравствуйте, структура [файл решения](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="90ab9-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="90ab9-115">Как слишком[создании шаблонов диспетчера ресурсов](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="90ab9-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="90ab9-116">Учетная запись службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="90ab9-116">Automation account</span></span>
<span data-ttu-id="90ab9-117">Все ресурсы в службе автоматизации Azure содержатся в [учетной записи службы автоматизации](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="90ab9-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="90ab9-118">Как описано в [OMS рабочей области и учетной записи автоматизации](operations-management-suite-solutions.md#oms-workspace-and-automation-account) не включен в решение по управлению hello hello учетной записи автоматизации, но должна существовать до установки решения hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="90ab9-119">Если эти сведения недоступны, то произойдет сбой установки решения hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="90ab9-120">Hello имя каждого ресурса автоматизации содержит hello собственной учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="90ab9-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="90ab9-121">Для этого в решении hello с hello **accountName** параметра как следующий пример runbook ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="90ab9-122">Модули Runbook</span><span class="sxs-lookup"><span data-stu-id="90ab9-122">Runbooks</span></span>
<span data-ttu-id="90ab9-123">Следует включить все модули Runbook, используемых решении hello в файле решения hello, чтобы они создаются при установке решения hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="90ab9-124">Не может содержать текст hello runbook hello в шаблоне hello, поэтому следует опубликовать hello runbook tooa общедоступное расположение которых может осуществляться любым пользователем, установка решения.</span><span class="sxs-lookup"><span data-stu-id="90ab9-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="90ab9-125">[Azure Automation runbook](../automation/automation-runbook-types.md) ресурсы имеют тип **Microsoft.Automation/automationAccounts/runbooks** и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="90ab9-126">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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


<span data-ttu-id="90ab9-127">в hello в следующей таблице описаны свойства Hello для модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="90ab9-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="90ab9-128">Property</span></span> | <span data-ttu-id="90ab9-129">Описание</span><span class="sxs-lookup"><span data-stu-id="90ab9-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="90ab9-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="90ab9-130">runbookType</span></span> |<span data-ttu-id="90ab9-131">Указывает типы hello hello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="90ab9-132">Script — сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="90ab9-132">Script - PowerShell script</span></span> <br><span data-ttu-id="90ab9-133">PowerShell — рабочий процесс PowerShell</span><span class="sxs-lookup"><span data-stu-id="90ab9-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="90ab9-134">GraphPowerShell — графический модуль сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="90ab9-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="90ab9-135">GraphPowerShellWorkflow — графический модуль Runbook рабочего процесса PowerShell</span><span class="sxs-lookup"><span data-stu-id="90ab9-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="90ab9-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="90ab9-136">logProgress</span></span> |<span data-ttu-id="90ab9-137">Указывает ли [записей хода выполнения](../automation/automation-runbook-output-and-messages.md) должно создаваться для hello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="90ab9-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="90ab9-138">logVerbose</span></span> |<span data-ttu-id="90ab9-139">Указывает, является ли [подробные записи](../automation/automation-runbook-output-and-messages.md) должно создаваться для hello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="90ab9-140">Описание</span><span class="sxs-lookup"><span data-stu-id="90ab9-140">description</span></span> |<span data-ttu-id="90ab9-141">Необязательное описание для hello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="90ab9-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="90ab9-142">publishContentLink</span></span> |<span data-ttu-id="90ab9-143">Указывает содержимое hello hello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="90ab9-144">URI - Uri содержимого toohello hello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="90ab9-145">Это будет PS1-файл для модулей Runbook PowerShell и сценариев, а также файл экспортированного графического модуля Runbook для графического модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="90ab9-146">версия - версии hello runbook для собственных отслеживания.</span><span class="sxs-lookup"><span data-stu-id="90ab9-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="90ab9-147">Задания службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="90ab9-147">Automation jobs</span></span>
<span data-ttu-id="90ab9-148">При запуске модуля Runbook в службе автоматизации Azure создается задание службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="90ab9-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="90ab9-149">Можно добавить runbook автоматизации задания tooyour решения tooautomatically начало ресурса, при установке решения по управлению hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="90ab9-150">Этот метод является типовыми toostart модулей Runbook, которые используются для начальной настройки решения hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="90ab9-151">Создание toostart runbook через регулярные интервалы [расписания](#schedules) и [расписания задания](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="90ab9-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="90ab9-152">Задание ресурсы имеют тип **Microsoft.Automation/automationAccounts/jobs** и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="90ab9-153">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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

<span data-ttu-id="90ab9-154">в hello в следующей таблице описаны свойства Hello для автоматизации заданий.</span><span class="sxs-lookup"><span data-stu-id="90ab9-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="90ab9-155">Свойство</span><span class="sxs-lookup"><span data-stu-id="90ab9-155">Property</span></span> | <span data-ttu-id="90ab9-156">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="90ab9-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="90ab9-157">runbook</span><span class="sxs-lookup"><span data-stu-id="90ab9-157">runbook</span></span> |<span data-ttu-id="90ab9-158">Одно имя сущности с именем hello hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="90ab9-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="90ab9-159">parameters</span><span class="sxs-lookup"><span data-stu-id="90ab9-159">parameters</span></span> |<span data-ttu-id="90ab9-160">Сущность для каждого значения параметра, предусмотренного hello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="90ab9-161">Задание Hello включает имя runbook hello и toobe значения любого параметра, отправляемых toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="90ab9-162">Задание Hello следует [зависят от](operations-management-suite-solutions-solution-file.md#resources) hello runbook, он начинается с момента hello runbook должен быть создан до задания hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="90ab9-163">При наличии нескольких модулей Runbook, которые нужно запустить, порядок их запуска можно определить, создав зависимость между заданием и другими заданиями, которые должны выполняться в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="90ab9-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="90ab9-164">Имя ресурса задания Hello должен содержать идентификатор GUID, который обычно назначается один из параметров.</span><span class="sxs-lookup"><span data-stu-id="90ab9-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="90ab9-165">Дополнительные сведения о параметрах GUID см. в статье [Создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="90ab9-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="90ab9-166">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="90ab9-166">Certificates</span></span>
<span data-ttu-id="90ab9-167">[Azure сертификаты автоматизации](../automation/automation-certificates.md) имеют тип **Microsoft.Automation/automationAccounts/certificates** и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="90ab9-168">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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



<span data-ttu-id="90ab9-169">в hello в следующей таблице описаны Hello свойств ресурсов сертификаты.</span><span class="sxs-lookup"><span data-stu-id="90ab9-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="90ab9-170">Свойство</span><span class="sxs-lookup"><span data-stu-id="90ab9-170">Property</span></span> | <span data-ttu-id="90ab9-171">Описание</span><span class="sxs-lookup"><span data-stu-id="90ab9-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="90ab9-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="90ab9-172">base64Value</span></span> |<span data-ttu-id="90ab9-173">Значение Base 64 для сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="90ab9-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="90ab9-174">thumbprint</span></span> |<span data-ttu-id="90ab9-175">Отпечаток сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="90ab9-176">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="90ab9-176">Credentials</span></span>
<span data-ttu-id="90ab9-177">[Учетные данные Azure Automation](../automation/automation-credentials.md) имеют тип **Microsoft.Automation/automationAccounts/credentials** и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="90ab9-178">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


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

<span data-ttu-id="90ab9-179">в hello в следующей таблице описаны Hello свойства учетных данных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90ab9-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="90ab9-180">Свойство</span><span class="sxs-lookup"><span data-stu-id="90ab9-180">Property</span></span> | <span data-ttu-id="90ab9-181">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="90ab9-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="90ab9-182">userName</span><span class="sxs-lookup"><span data-stu-id="90ab9-182">userName</span></span> |<span data-ttu-id="90ab9-183">Имя пользователя для учетных данных hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-183">User name for hello credential.</span></span> |
| <span data-ttu-id="90ab9-184">пароль</span><span class="sxs-lookup"><span data-stu-id="90ab9-184">password</span></span> |<span data-ttu-id="90ab9-185">Пароль для учетных данных hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="90ab9-186">Расписания</span><span class="sxs-lookup"><span data-stu-id="90ab9-186">Schedules</span></span>
<span data-ttu-id="90ab9-187">[Azure расписания автоматизации](../automation/automation-schedules.md) имеют тип **Microsoft.Automation/automationAccounts/schedules** и имеют следующие структуры hello hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="90ab9-188">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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

<span data-ttu-id="90ab9-189">в hello в следующей таблице описаны свойства Hello планирование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90ab9-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="90ab9-190">Свойство</span><span class="sxs-lookup"><span data-stu-id="90ab9-190">Property</span></span> | <span data-ttu-id="90ab9-191">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="90ab9-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="90ab9-192">Описание</span><span class="sxs-lookup"><span data-stu-id="90ab9-192">description</span></span> |<span data-ttu-id="90ab9-193">Необязательное описание для hello расписания.</span><span class="sxs-lookup"><span data-stu-id="90ab9-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="90ab9-194">startTime</span><span class="sxs-lookup"><span data-stu-id="90ab9-194">startTime</span></span> |<span data-ttu-id="90ab9-195">Указывает hello время начала расписания в виде объекта DateTime.</span><span class="sxs-lookup"><span data-stu-id="90ab9-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="90ab9-196">Можно указать строку, если преобразованное tooa действительное значение DateTime.</span><span class="sxs-lookup"><span data-stu-id="90ab9-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="90ab9-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="90ab9-197">isEnabled</span></span> |<span data-ttu-id="90ab9-198">Указывает, включено ли расписание hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="90ab9-199">interval</span><span class="sxs-lookup"><span data-stu-id="90ab9-199">interval</span></span> |<span data-ttu-id="90ab9-200">Тип интервала для расписания hello Hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="90ab9-201">day</span><span class="sxs-lookup"><span data-stu-id="90ab9-201">day</span></span><br><span data-ttu-id="90ab9-202">hour</span><span class="sxs-lookup"><span data-stu-id="90ab9-202">hour</span></span> |
| <span data-ttu-id="90ab9-203">frequency</span><span class="sxs-lookup"><span data-stu-id="90ab9-203">frequency</span></span> |<span data-ttu-id="90ab9-204">Частоту, расписание hello должен срабатывать в число дней или часов.</span><span class="sxs-lookup"><span data-stu-id="90ab9-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="90ab9-205">Расписания должны иметь время начала со значением больше hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="90ab9-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="90ab9-206">Нельзя задавать это значение с переменной, поскольку невозможно узнать, когда это toobe будет установлен.</span><span class="sxs-lookup"><span data-stu-id="90ab9-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="90ab9-207">Используйте одну из hello, следующие две стратегии при использовании планирование ресурсов в решении.</span><span class="sxs-lookup"><span data-stu-id="90ab9-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="90ab9-208">Используйте параметр для hello время начала расписания hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="90ab9-209">При установке решения hello, предложит tooprovide hello пользователем значение.</span><span class="sxs-lookup"><span data-stu-id="90ab9-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="90ab9-210">Если у вас есть несколько расписаний, для них можно использовать одно значение параметра.</span><span class="sxs-lookup"><span data-stu-id="90ab9-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="90ab9-211">Создание расписания hello, с помощью runbook, который начинается после установки решения hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="90ab9-212">Эта функция удаляет требование hello hello пользователя toospecify время, но не может содержать расписания hello в вашем решении, поэтому он будет удален при удалении решения hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="90ab9-213">Расписания заданий</span><span class="sxs-lookup"><span data-stu-id="90ab9-213">Job schedules</span></span>
<span data-ttu-id="90ab9-214">Ресурсы расписания заданий связывают модуль Runbook с расписанием.</span><span class="sxs-lookup"><span data-stu-id="90ab9-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="90ab9-215">Они имеют тип **Microsoft.Automation/automationAccounts/jobSchedules** и имеют следующие структуры hello hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="90ab9-216">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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


<span data-ttu-id="90ab9-217">свойства Hello для расписания задания описаны в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="90ab9-218">Свойство</span><span class="sxs-lookup"><span data-stu-id="90ab9-218">Property</span></span> | <span data-ttu-id="90ab9-219">Описание</span><span class="sxs-lookup"><span data-stu-id="90ab9-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="90ab9-220">schedule name</span><span class="sxs-lookup"><span data-stu-id="90ab9-220">schedule name</span></span> |<span data-ttu-id="90ab9-221">Один **имя** сущность с именем hello hello расписания.</span><span class="sxs-lookup"><span data-stu-id="90ab9-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="90ab9-222">runbook name</span><span class="sxs-lookup"><span data-stu-id="90ab9-222">runbook name</span></span>  |<span data-ttu-id="90ab9-223">Один **имя** сущность с именем hello hello модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="90ab9-224">Переменные</span><span class="sxs-lookup"><span data-stu-id="90ab9-224">Variables</span></span>
<span data-ttu-id="90ab9-225">[Azure переменные автоматизации](../automation/automation-variables.md) имеют тип **Microsoft.Automation/automationAccounts/variables** и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="90ab9-226">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

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

<span data-ttu-id="90ab9-227">в hello в следующей таблице описаны Hello свойств переменной ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90ab9-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="90ab9-228">Свойство</span><span class="sxs-lookup"><span data-stu-id="90ab9-228">Property</span></span> | <span data-ttu-id="90ab9-229">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="90ab9-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="90ab9-230">Описание</span><span class="sxs-lookup"><span data-stu-id="90ab9-230">description</span></span> | <span data-ttu-id="90ab9-231">Необязательное описание для переменной hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="90ab9-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="90ab9-232">isEncrypted</span></span> | <span data-ttu-id="90ab9-233">Указывает, нужно ли шифровать hello переменной.</span><span class="sxs-lookup"><span data-stu-id="90ab9-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="90ab9-234">type</span><span class="sxs-lookup"><span data-stu-id="90ab9-234">type</span></span> | <span data-ttu-id="90ab9-235">Сейчас это свойство ни на что не влияет.</span><span class="sxs-lookup"><span data-stu-id="90ab9-235">This property currently has no effect.</span></span>  <span data-ttu-id="90ab9-236">Тип данных Hello hello переменной определяется hello начальное значение.</span><span class="sxs-lookup"><span data-stu-id="90ab9-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="90ab9-237">value</span><span class="sxs-lookup"><span data-stu-id="90ab9-237">value</span></span> | <span data-ttu-id="90ab9-238">Значение для переменной hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="90ab9-239">Hello **тип** свойство в настоящее время не оказывает влияния на создание переменной hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="90ab9-240">Тип данных Hello для hello переменной определяется значение hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="90ab9-241">Если задать начальное значение переменной hello hello, его необходимо настроить как hello правильный тип данных.</span><span class="sxs-lookup"><span data-stu-id="90ab9-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="90ab9-242">Hello в следующей таблице приводится hello различных типов данных допустимый и их синтаксис.</span><span class="sxs-lookup"><span data-stu-id="90ab9-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="90ab9-243">Обратите внимание, что значения в JSON ожидаемый tooalways заключаться в кавычки с специальные символы в кавычках hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="90ab9-244">Например, строковое значение может быть задано в кавычки строку hello (с помощью escape-символ hello (\\)) во время может быть задано числовое значение с одним набором квот.</span><span class="sxs-lookup"><span data-stu-id="90ab9-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="90ab9-245">Тип данных</span><span class="sxs-lookup"><span data-stu-id="90ab9-245">Data type</span></span> | <span data-ttu-id="90ab9-246">Описание</span><span class="sxs-lookup"><span data-stu-id="90ab9-246">Description</span></span> | <span data-ttu-id="90ab9-247">Пример</span><span class="sxs-lookup"><span data-stu-id="90ab9-247">Example</span></span> | <span data-ttu-id="90ab9-248">Разрешает слишком</span><span class="sxs-lookup"><span data-stu-id="90ab9-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="90ab9-249">string</span><span class="sxs-lookup"><span data-stu-id="90ab9-249">string</span></span>   | <span data-ttu-id="90ab9-250">Заключает значение в две пары кавычек.</span><span class="sxs-lookup"><span data-stu-id="90ab9-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="90ab9-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="90ab9-251">"\"Hello world\""</span></span> | <span data-ttu-id="90ab9-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="90ab9-252">"Hello world"</span></span> |
| <span data-ttu-id="90ab9-253">numeric</span><span class="sxs-lookup"><span data-stu-id="90ab9-253">numeric</span></span>  | <span data-ttu-id="90ab9-254">Числовое значение с одной парой кавычек.</span><span class="sxs-lookup"><span data-stu-id="90ab9-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="90ab9-255">"64"</span><span class="sxs-lookup"><span data-stu-id="90ab9-255">"64"</span></span> | <span data-ttu-id="90ab9-256">64</span><span class="sxs-lookup"><span data-stu-id="90ab9-256">64</span></span> |
| <span data-ttu-id="90ab9-257">Логическое</span><span class="sxs-lookup"><span data-stu-id="90ab9-257">boolean</span></span>  | <span data-ttu-id="90ab9-258">Значение **true** или **false** в кавычках.</span><span class="sxs-lookup"><span data-stu-id="90ab9-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="90ab9-259">Обратите внимание, что это значение должно быть в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="90ab9-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="90ab9-260">True</span><span class="sxs-lookup"><span data-stu-id="90ab9-260">"true"</span></span> | <span data-ttu-id="90ab9-261">Да</span><span class="sxs-lookup"><span data-stu-id="90ab9-261">true</span></span> |
| <span data-ttu-id="90ab9-262">Datetime</span><span class="sxs-lookup"><span data-stu-id="90ab9-262">datetime</span></span> | <span data-ttu-id="90ab9-263">Сериализованное значение даты.</span><span class="sxs-lookup"><span data-stu-id="90ab9-263">Serialized date value.</span></span><br><span data-ttu-id="90ab9-264">Командлет ConvertTo-Json hello в PowerShell toogenerate можно использовать это значение для определенной даты.</span><span class="sxs-lookup"><span data-stu-id="90ab9-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="90ab9-265">Пример: get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="90ab9-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="90ab9-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="90ab9-266">ConvertTo-Json</span></span> | <span data-ttu-id="90ab9-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="90ab9-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="90ab9-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="90ab9-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="90ab9-269">модули</span><span class="sxs-lookup"><span data-stu-id="90ab9-269">Modules</span></span>
<span data-ttu-id="90ab9-270">Решения управления не обязательно toodefine [глобальных модулей](../automation/automation-integration-modules.md) используемых модулей Runbook, так как они всегда будут доступны в учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="90ab9-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="90ab9-271">Вам нужен tooinclude ресурса для любого модуля, используемые модули Runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="90ab9-272">[Модули интеграции](../automation/automation-integration-modules.md) имеют тип **Microsoft.Automation/automationAccounts/modules** и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="90ab9-273">Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

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


<span data-ttu-id="90ab9-274">в hello в следующей таблице описаны свойства Hello модуля ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90ab9-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="90ab9-275">Свойство</span><span class="sxs-lookup"><span data-stu-id="90ab9-275">Property</span></span> | <span data-ttu-id="90ab9-276">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="90ab9-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="90ab9-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="90ab9-277">contentLink</span></span> |<span data-ttu-id="90ab9-278">Указывает содержимое hello модуля "hello".</span><span class="sxs-lookup"><span data-stu-id="90ab9-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="90ab9-279">URI - содержимое toohello Uri модуля "hello".</span><span class="sxs-lookup"><span data-stu-id="90ab9-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="90ab9-280">Это будет PS1-файл для модулей Runbook PowerShell и сценариев, а также файл экспортированного графического модуля Runbook для графического модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="90ab9-281">версия - версия модуля "hello" для собственных отслеживания.</span><span class="sxs-lookup"><span data-stu-id="90ab9-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="90ab9-282">Hello runbook должны зависеть от tooensure hello модуля ресурсов, которых он создан до hello runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="90ab9-283">Обновление модулей</span><span class="sxs-lookup"><span data-stu-id="90ab9-283">Updating modules</span></span>
<span data-ttu-id="90ab9-284">Если обновить решение управления, включающее runbook, использующий расписание, а hello новая версия решения имеет новый модуль, используемый этого модуля, hello runbook может использовать hello старая версия модуля "hello".</span><span class="sxs-lookup"><span data-stu-id="90ab9-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="90ab9-285">Следует включать следующие модули Runbook в вашем решении hello и создать toorun задания их перед другими модулями Runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="90ab9-286">Это позволит гарантировать, что модули обновляются как обязательный перед hello загрузки модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="90ab9-287">[Обновление ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) проверит все модули hello использовать модули Runbook в вашем решении hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="90ab9-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="90ab9-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) будет повторно зарегистрировать все ресурсы tooensure hello расписание, что модули Runbook hello связаны toothem с модулями последнюю hello используйте.</span><span class="sxs-lookup"><span data-stu-id="90ab9-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="90ab9-289">Образец</span><span class="sxs-lookup"><span data-stu-id="90ab9-289">Sample</span></span>
<span data-ttu-id="90ab9-290">Ниже приведен образец, включают решение, включающее hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="90ab9-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="90ab9-291">Модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="90ab9-291">Runbook.</span></span>  <span data-ttu-id="90ab9-292">Это пример модуля Runbook, хранящийся в общедоступном репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="90ab9-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="90ab9-293">Задание службы автоматизации, начинающийся hello runbook после установки решения hello.</span><span class="sxs-lookup"><span data-stu-id="90ab9-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="90ab9-294">Расписание и задание расписания toostart hello runbook через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="90ab9-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="90ab9-295">Сертификат.</span><span class="sxs-lookup"><span data-stu-id="90ab9-295">Certificate.</span></span>
- <span data-ttu-id="90ab9-296">Учетные данные.</span><span class="sxs-lookup"><span data-stu-id="90ab9-296">Credential.</span></span>
- <span data-ttu-id="90ab9-297">Переменная.</span><span class="sxs-lookup"><span data-stu-id="90ab9-297">Variable.</span></span>
- <span data-ttu-id="90ab9-298">Модуль.</span><span class="sxs-lookup"><span data-stu-id="90ab9-298">Module.</span></span>  <span data-ttu-id="90ab9-299">Это hello [OMSIngestionAPI модуль](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) для записи данных tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="90ab9-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="90ab9-300">Здравствуйте, образец использует [параметры стандартное решение](operations-management-suite-solutions-solution-file.md#parameters) переменные, которые часто используются в решении, что отличие от значений toohardcoding в hello определения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90ab9-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


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
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="90ab9-301">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="90ab9-301">Next steps</span></span>
* <span data-ttu-id="90ab9-302">[Добавление решения tooyour представление](operations-management-suite-solutions-resources-views.md) toovisualize собранных данных.</span><span class="sxs-lookup"><span data-stu-id="90ab9-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
