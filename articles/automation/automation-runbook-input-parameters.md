---
title: "aaaRunbook входных параметров | Документы Microsoft"
description: "Входные параметры Runbook повысить гибкость hello модулей Runbook, позволяя toopass данных tooa runbook при его запуске. В этой статье описаны различные сценарии использования входных параметров в модулях Runbook."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="1ad97-104">Входные параметры Runbook</span><span class="sxs-lookup"><span data-stu-id="1ad97-104">Runbook input parameters</span></span>
<span data-ttu-id="1ad97-105">Входные параметры Runbook повысить гибкость hello модулей Runbook, позволяя tooit toopass данных при его запуске.</span><span class="sxs-lookup"><span data-stu-id="1ad97-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="1ad97-106">Параметры Hello позволяют toobe действия runbook hello, предназначенные для конкретных сценариях и средах.</span><span class="sxs-lookup"><span data-stu-id="1ad97-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="1ad97-107">В этой статье подробно описаны различные сценарии использования входных параметров в модулях Runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="1ad97-108">Настройка входных параметров</span><span class="sxs-lookup"><span data-stu-id="1ad97-108">Configure input parameters</span></span>
<span data-ttu-id="1ad97-109">Входные параметры настраиваются в модулях Runbook PowerShell рабочих процессов PowerShell и в графических модулях Runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="1ad97-110">Runbook может использовать несколько параметров с разными типами данных или вообще не использовать параметры.</span><span class="sxs-lookup"><span data-stu-id="1ad97-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="1ad97-111">Входные параметры могут быть обязательными или необязательными. Необязательным параметрам можно назначать значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1ad97-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="1ad97-112">Можно назначить значения toohello входных параметров для модуля runbook при запуске через один из доступных методов hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="1ad97-113">Это может быть запуск runbook из hello портал или веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1ad97-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="1ad97-114">Модуль можно также запустить как дочерний модуль Runbook, который вызывается с помощью встроенного вызова в другом Runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="1ad97-115">Настройка входных параметров в модулях Runbook PowerShell и рабочих процессов PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ad97-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="1ad97-116">PowerShell и [модулях Runbook рабочего процесса PowerShell](automation-first-runbook-textual.md) в службе автоматизации Azure поддерживают входных параметров, определенных с помощью hello следующие атрибуты.</span><span class="sxs-lookup"><span data-stu-id="1ad97-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="1ad97-117">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="1ad97-117">**Property**</span></span> | <span data-ttu-id="1ad97-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="1ad97-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="1ad97-119">Тип</span><span class="sxs-lookup"><span data-stu-id="1ad97-119">Type</span></span> |<span data-ttu-id="1ad97-120">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="1ad97-120">Required.</span></span> <span data-ttu-id="1ad97-121">Hello предполагаемый тип данных для значения параметра hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="1ad97-122">Допускаются любые типы .NET.</span><span class="sxs-lookup"><span data-stu-id="1ad97-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="1ad97-123">Имя</span><span class="sxs-lookup"><span data-stu-id="1ad97-123">Name</span></span> |<span data-ttu-id="1ad97-124">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="1ad97-124">Required.</span></span> <span data-ttu-id="1ad97-125">Имя параметра hello Hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-125">hello name of hello parameter.</span></span> <span data-ttu-id="1ad97-126">Это должно быть уникальным в пределах hello runbook и может содержать только буквы, цифры или символы подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="1ad97-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="1ad97-127">Оно должно начинаться с буквы.</span><span class="sxs-lookup"><span data-stu-id="1ad97-127">It must start with a letter.</span></span> |
| <span data-ttu-id="1ad97-128">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1ad97-128">Mandatory</span></span> |<span data-ttu-id="1ad97-129">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-129">Optional.</span></span> <span data-ttu-id="1ad97-130">Указывает, должно быть указано значение для параметра hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="1ad97-131">Если это значение слишком**$true**, то при запуске hello runbook должно быть указано значение.</span><span class="sxs-lookup"><span data-stu-id="1ad97-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="1ad97-132">Если это значение слишком**$false**, а затем значение является необязательным.</span><span class="sxs-lookup"><span data-stu-id="1ad97-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="1ad97-133">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1ad97-133">Default value</span></span> |<span data-ttu-id="1ad97-134">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-134">Optional.</span></span>  <span data-ttu-id="1ad97-135">Задает значение, которое будет использоваться для параметра hello, если значение не передается при запуске hello runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="1ad97-136">Значение по умолчанию можно задать для любого параметра и автоматически внесет hello параметр необязательным независимо от hello обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="1ad97-137">Наряду с перечисленными здесь входными параметрами Windows PowerShell поддерживает дополнительные атрибуты входных параметров, например проверки, псевдонимы наборы параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="1ad97-138">Тем не менее службы автоматизации Azure в настоящее время поддерживает только hello входные параметры, приведенные выше.</span><span class="sxs-lookup"><span data-stu-id="1ad97-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="1ad97-139">Определение параметров в модулях Runbook рабочего процесса PowerShell имеет hello, следуя общую форму, где несколько параметров разделяются запятыми.</span><span class="sxs-lookup"><span data-stu-id="1ad97-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="1ad97-140">При определении параметров, если не указать hello **обязательные** атрибута, то по умолчанию hello параметр считается необязательным.</span><span class="sxs-lookup"><span data-stu-id="1ad97-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="1ad97-141">Кроме того, если задано значение по умолчанию для параметра в модулях Runbook рабочего процесса PowerShell, они рассматриваются в PowerShell как необязательный параметр, независимо от того, hello **обязательные** значение атрибута.</span><span class="sxs-lookup"><span data-stu-id="1ad97-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="1ad97-142">Например настроим hello входные параметры для runbook рабочего процесса PowerShell, который выводит сведения о виртуальных машин одной виртуальной Машины или всех виртуальных машин в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1ad97-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="1ad97-143">Этот runbook имеет два параметра, как показано на следующий снимок экрана приветствия: hello имя виртуальной машины и имя группы ресурсов hello hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![Рабочий процесс PowerShell службы автоматизации](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="1ad97-145">В этом определении параметра hello параметры **$VMName** и **$resourceGroupName** параметров простого строкового типа.</span><span class="sxs-lookup"><span data-stu-id="1ad97-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="1ad97-146">Однако модули Runbook PowerShell и рабочих процессов PowerShell поддерживают все простые и сложные типы, например **object** или **PSCredential**, для входных параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="1ad97-147">Если runbook имеет входной параметр типа объекта, затем с помощью PowerShell хэш-таблицы (имя, значение) пар toopass в значении.</span><span class="sxs-lookup"><span data-stu-id="1ad97-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="1ad97-148">Например, если имеется следующий параметр в модуле runbook hello:</span><span class="sxs-lookup"><span data-stu-id="1ad97-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="1ad97-149">Затем можно передать следующую параметром toohello значение hello:</span><span class="sxs-lookup"><span data-stu-id="1ad97-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="1ad97-150">Настройка входных параметров в графических модулях Runbook</span><span class="sxs-lookup"><span data-stu-id="1ad97-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="1ad97-151">слишком[настроить графический runbook](automation-first-runbook-graphical.md) с входными параметрами, создадим графический модуль runbook, который выводит сведения о виртуальных машинах, либо одной виртуальной Машины или всех виртуальных машин в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1ad97-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="1ad97-152">Настройка модуля состоит из двух основных операций, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="1ad97-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="1ad97-153">[**Проверки подлинности модулей Runbook в учетной записи запуска от имени Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate с Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad97-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="1ad97-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello свойства виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1ad97-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="1ad97-155">Можно использовать hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) действия toooutput приветствия имен виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1ad97-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="1ad97-156">Здравствуйте, действие **Get AzureRmVm** принимает два параметра hello **имя виртуальной машины** и hello **имя группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="1ad97-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="1ad97-157">Поскольку эти параметры могут потребовать различных значений каждый раз при запуске hello runbook, можно добавить runbook tooyour входных параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="1ad97-158">Ниже приведены hello действия tooadd входных параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="1ad97-159">Выберите hello графический runbook из hello **Runbooks** колонку и нажмите кнопку [ **изменить** ](automation-graphical-authoring-intro.md) его.</span><span class="sxs-lookup"><span data-stu-id="1ad97-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="1ad97-160">Из редактора hello runbook, нажмите кнопку **ввод и вывод** tooopen hello **ввод и вывод** колонку.</span><span class="sxs-lookup"><span data-stu-id="1ad97-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![Графический модуль Runbook службы автоматизации](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="1ad97-162">Hello **ввод и вывод** колонке отображается список входных параметров, которые определены для hello runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="1ad97-163">В этой колонке можно добавить новый входной параметр или изменить конфигурацию hello существующего входного параметра.</span><span class="sxs-lookup"><span data-stu-id="1ad97-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="1ad97-164">Щелкните tooadd новый параметр для hello runbook **добавить входные данные** tooopen hello **входной параметр модуля Runbook** колонку.</span><span class="sxs-lookup"><span data-stu-id="1ad97-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="1ad97-165">Нет можно настроить следующие параметры hello:</span><span class="sxs-lookup"><span data-stu-id="1ad97-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="1ad97-166">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="1ad97-166">**Property**</span></span> | <span data-ttu-id="1ad97-167">**Описание**</span><span class="sxs-lookup"><span data-stu-id="1ad97-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1ad97-168">Имя</span><span class="sxs-lookup"><span data-stu-id="1ad97-168">Name</span></span> |<span data-ttu-id="1ad97-169">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="1ad97-169">Required.</span></span>  <span data-ttu-id="1ad97-170">Имя параметра hello Hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-170">hello name of hello parameter.</span></span> <span data-ttu-id="1ad97-171">Это должно быть уникальным в пределах hello runbook и может содержать только буквы, цифры или символы подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="1ad97-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="1ad97-172">Оно должно начинаться с буквы.</span><span class="sxs-lookup"><span data-stu-id="1ad97-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="1ad97-173">Описание</span><span class="sxs-lookup"><span data-stu-id="1ad97-173">Description</span></span> |<span data-ttu-id="1ad97-174">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-174">Optional.</span></span> <span data-ttu-id="1ad97-175">Описание цели hello входного параметра.</span><span class="sxs-lookup"><span data-stu-id="1ad97-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="1ad97-176">Тип</span><span class="sxs-lookup"><span data-stu-id="1ad97-176">Type</span></span> |<span data-ttu-id="1ad97-177">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-177">Optional.</span></span> <span data-ttu-id="1ad97-178">Тип данных Hello, которая ожидается для значения параметра hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="1ad97-179">Поддерживаются параметры **строкового**, **логического**, **объектного** типа, а также типа **Int32**, **Int64**, **DateTime** и типа **десятичного** числа.</span><span class="sxs-lookup"><span data-stu-id="1ad97-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="1ad97-180">Если тип данных не выбран, то по умолчанию слишком**строка**.</span><span class="sxs-lookup"><span data-stu-id="1ad97-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="1ad97-181">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1ad97-181">Mandatory</span></span> |<span data-ttu-id="1ad97-182">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-182">Optional.</span></span> <span data-ttu-id="1ad97-183">Указывает, должно быть указано значение для параметра hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="1ad97-184">При выборе **Да**, то при запуске hello runbook должно быть указано значение.</span><span class="sxs-lookup"><span data-stu-id="1ad97-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="1ad97-185">При выборе **не**, а затем значение не является обязательным при запуске модуля hello и может быть установлено значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1ad97-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="1ad97-186">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="1ad97-186">Default Value</span></span> |<span data-ttu-id="1ad97-187">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-187">Optional.</span></span> <span data-ttu-id="1ad97-188">Задает значение, которое будет использоваться для параметра hello, если значение не передается при запуске hello runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="1ad97-189">Для необязательного параметра можно задать значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1ad97-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="1ad97-190">Выберите значение по умолчанию tooset **настраиваемый**.</span><span class="sxs-lookup"><span data-stu-id="1ad97-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="1ad97-191">Это значение используется в том случае, если не задано другое значение, при запуске hello runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="1ad97-192">Выберите **нет** Если вы не хотите tooprovide любое значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1ad97-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![Добавление новых входных данных](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="1ad97-194">Создайте два параметра с hello следующие свойства, которые будут использоваться hello **Get AzureRmVm** действия:</span><span class="sxs-lookup"><span data-stu-id="1ad97-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="1ad97-195">**Параметр 1:**</span><span class="sxs-lookup"><span data-stu-id="1ad97-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="1ad97-196">Имя — VMName.</span><span class="sxs-lookup"><span data-stu-id="1ad97-196">Name - VMName</span></span>
     * <span data-ttu-id="1ad97-197">Тип: строчный.</span><span class="sxs-lookup"><span data-stu-id="1ad97-197">Type - String</span></span>
     * <span data-ttu-id="1ad97-198">Необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-198">Mandatory - No</span></span>
   * <span data-ttu-id="1ad97-199">**Параметр 2:**</span><span class="sxs-lookup"><span data-stu-id="1ad97-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="1ad97-200">Имя — resourceGroupName.</span><span class="sxs-lookup"><span data-stu-id="1ad97-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="1ad97-201">Тип: строчный.</span><span class="sxs-lookup"><span data-stu-id="1ad97-201">Type - String</span></span>
     * <span data-ttu-id="1ad97-202">Необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-202">Mandatory - No</span></span>
     * <span data-ttu-id="1ad97-203">Настраиваемое значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1ad97-203">Default value - Custom</span></span>
     * <span data-ttu-id="1ad97-204">Значение по умолчанию — \<имя группы ресурсов hello, содержащем виртуальные машины hello ></span><span class="sxs-lookup"><span data-stu-id="1ad97-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="1ad97-205">После добавления параметров приветствия щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1ad97-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="1ad97-206">Теперь их можно просмотреть в hello **ввода и вывода колонке**.</span><span class="sxs-lookup"><span data-stu-id="1ad97-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="1ad97-207">Нажмите кнопку **ОК** еще раз, а затем — **Сохранить** и **Опубликовать**, чтобы сохранить параметры и опубликовать модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="1ad97-208">Назначить значения параметров tooinput в модулях Runbook</span><span class="sxs-lookup"><span data-stu-id="1ad97-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="1ad97-209">Можно передавать значения параметров tooinput в Runbook в hello следующие сценарии.</span><span class="sxs-lookup"><span data-stu-id="1ad97-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="1ad97-210">Запуск Runbook и назначение параметров</span><span class="sxs-lookup"><span data-stu-id="1ad97-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="1ad97-211">Runbook можно запустить различными способами: через портал Azure, веб-перехватчика, с помощью командлетов PowerShell, с помощью API-интерфейса REST hello или hello SDK hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="1ad97-212">Ниже рассмотрены различные методы запуска модуля Runbook и назначения параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="1ad97-213">Запуск опубликованном модуле runbook с помощью портала Azure hello и назначение параметров</span><span class="sxs-lookup"><span data-stu-id="1ad97-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="1ad97-214">Когда вы [запустить hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **запустить Runbook** открывает колонку и вы можете настроить значения для параметров hello, которые вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="1ad97-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Запустить с помощью портала hello](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="1ad97-216">Hello метку под hello поля ввода вы увидите hello атрибуты, которые были установлены для параметра hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="1ad97-217">Атрибуты являются обязательными или необязательными и содержат тип и значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1ad97-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="1ad97-218">Hello справки всплывающей Далее toohello имени параметра вы увидите все hello ключевые сведения, необходимые toomake решения о входных значениях параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="1ad97-219">Эти сведения указывают, является параметр обязательным или нет.</span><span class="sxs-lookup"><span data-stu-id="1ad97-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="1ad97-220">Она также включает hello тип и значение по умолчанию (если таковые имеются) и другие полезные примечания.</span><span class="sxs-lookup"><span data-stu-id="1ad97-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![Всплывающая справка](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="1ad97-222">Параметры строкового типа поддерживают **пустые** строковые значения.</span><span class="sxs-lookup"><span data-stu-id="1ad97-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="1ad97-223">Ввод **[EmptyString]** в входной параметр hello поле будет передать параметр toohello пустая строка.</span><span class="sxs-lookup"><span data-stu-id="1ad97-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="1ad97-224">Параметры строкового типа не поддерживают передачу значений **NULL** .</span><span class="sxs-lookup"><span data-stu-id="1ad97-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="1ad97-225">Если не передать любое значение toohello строковый параметр, затем PowerShell интерпретирует его как допускающий значения null.</span><span class="sxs-lookup"><span data-stu-id="1ad97-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="1ad97-226">Запуск опубликованного модуля Runbook с помощью командлетов PowerShell и назначение параметров</span><span class="sxs-lookup"><span data-stu-id="1ad97-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="1ad97-227">**Командлеты Azure Resource Manager**. Модуль Runbook службы автоматизации, созданный в группе ресурсов, можно запустить с помощью командлета [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ad97-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="1ad97-228">**Пример**</span><span class="sxs-lookup"><span data-stu-id="1ad97-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="1ad97-229">**Командлеты для управления службами Azure.** Модуль Runbook службы автоматизации, созданный в группе ресурсов по умолчанию, можно запустить с помощью командлета [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ad97-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="1ad97-230">**Пример**</span><span class="sxs-lookup"><span data-stu-id="1ad97-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="1ad97-231">При запуске модуля runbook с помощью командлетов PowerShell, параметр по умолчанию, **MicrosoftApplicationManagementStartedBy** создана с использованием hello **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1ad97-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="1ad97-232">Этот параметр можно просмотреть в hello **сведения о задании** колонку.</span><span class="sxs-lookup"><span data-stu-id="1ad97-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="1ad97-233">Запуск Runbook с использованием пакета SDK и назначение параметров</span><span class="sxs-lookup"><span data-stu-id="1ad97-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="1ad97-234">**Метод Azure диспетчера ресурсов:** runbook можно запустить с помощью hello SDK от языка программирования.</span><span class="sxs-lookup"><span data-stu-id="1ad97-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="1ad97-235">Ниже приведен фрагмент кода C# для запуска модуля Runbook в вашей учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="1ad97-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="1ad97-236">Вы можете просмотреть все код hello в нашем [репозитории GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="1ad97-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="1ad97-237">**Метод Azure управления службами:** runbook можно запустить с помощью hello SDK от языка программирования.</span><span class="sxs-lookup"><span data-stu-id="1ad97-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="1ad97-238">Ниже приведен фрагмент кода C# для запуска модуля Runbook в вашей учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="1ad97-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="1ad97-239">Вы можете просмотреть все код hello в нашем [репозитории GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="1ad97-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="1ad97-240">toostart этот метод создания hello toostore словарь параметров runbook **VMName** и **resourceGroupName**и их значения.</span><span class="sxs-lookup"><span data-stu-id="1ad97-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="1ad97-241">Затем запустите hello runbook.</span><span class="sxs-lookup"><span data-stu-id="1ad97-241">Then start hello runbook.</span></span> <span data-ttu-id="1ad97-242">Ниже приведен hello фрагмент кода C# для вызова метода hello, определенный выше.</span><span class="sxs-lookup"><span data-stu-id="1ad97-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="1ad97-243">Запустить модуль runbook с помощью API-интерфейса REST hello и назначение параметров</span><span class="sxs-lookup"><span data-stu-id="1ad97-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="1ad97-244">Задание runbook может быть создан и работы с hello Azure Automation REST API с помощью hello **ПОМЕСТИТЬ** метод с hello следующий URI запроса.</span><span class="sxs-lookup"><span data-stu-id="1ad97-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="1ad97-245">В URI запроса hello замените hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="1ad97-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="1ad97-246">**subscription-id** — идентификатором своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad97-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="1ad97-247">**Имя облачной службы:** имя hello hello облачной службы toowhich hello запроса должно быть отправлено.</span><span class="sxs-lookup"><span data-stu-id="1ad97-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="1ad97-248">**Automation-account-name:** hello вашей учетной записи автоматизации, размещенному в hello имя облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1ad97-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="1ad97-249">**Идентификатор задания:** hello GUID для задания hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="1ad97-250">Идентификаторы GUID в PowerShell могут быть созданы с помощью hello **[GUID]::NewGuid(). ToString()** команды.</span><span class="sxs-lookup"><span data-stu-id="1ad97-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="1ad97-251">В порядке toopass параметры toohello runbook задания используйте текст запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="1ad97-252">Он принимает следующие два свойства, представленные в формате JSON hello:</span><span class="sxs-lookup"><span data-stu-id="1ad97-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="1ad97-253">**Runbook Name** — обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-253">**Runbook name:** Required.</span></span> <span data-ttu-id="1ad97-254">Hello имя hello runbook toostart задания hello.</span><span class="sxs-lookup"><span data-stu-id="1ad97-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="1ad97-255">**Runbook Parameters** — необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1ad97-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="1ad97-256">Словарь список параметров hello в (имя, значение) формате, где имя должно быть строкового типа, а значение может быть любым допустимым значением JSON.</span><span class="sxs-lookup"><span data-stu-id="1ad97-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="1ad97-257">Если требуется toostart hello **Get AzureVMTextual** runbook, который был создан ранее с **VMName** и **resourceGroupName** как параметры, используйте следующий формат JSON hello для hello текст запроса.</span><span class="sxs-lookup"><span data-stu-id="1ad97-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="1ad97-258">Код состояния HTTP 201 возвращается в том случае, если задание hello успешно создан.</span><span class="sxs-lookup"><span data-stu-id="1ad97-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="1ad97-259">Дополнительные сведения о hello текст ответа и заголовки ответов см. в статье toohello о том, как слишком[создать задание runbook с помощью API-интерфейса REST hello.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="1ad97-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="1ad97-260">Тестирование Runbook и назначение параметров</span><span class="sxs-lookup"><span data-stu-id="1ad97-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="1ad97-261">При вы [теста hello черновик runbook](automation-testing-runbook.md) с помощью параметра тестирования hello hello **тестирования** открывает колонку и вы можете настроить значения для параметров hello, которые вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="1ad97-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Тестирование и назначение параметров](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="1ad97-263">Связать runbook tooa расписание и параметры назначить</span><span class="sxs-lookup"><span data-stu-id="1ad97-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="1ad97-264">Вы можете [связать расписание](automation-schedules.md) tooyour runbook, так что runbook hello запускается в определенное время.</span><span class="sxs-lookup"><span data-stu-id="1ad97-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="1ad97-265">При создании расписания hello и hello runbook будет использовать эти значения при запуске по расписанию hello, назначьте входных параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="1ad97-266">Не удается сохранить расписание hello, пока не будут предоставлены значения всех обязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![Создание расписания и назначение параметров](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="1ad97-268">Создание объекта Webhook для модуля Runbook и назначение параметров</span><span class="sxs-lookup"><span data-stu-id="1ad97-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="1ad97-269">Для модуля Runbook можно создать объект [Webhook](automation-webhooks.md) и настроить входные параметры.</span><span class="sxs-lookup"><span data-stu-id="1ad97-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="1ad97-270">Не удается сохранить веб-перехватчика hello, пока не будут предоставлены значения всех обязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="1ad97-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Создание Webhook и назначение параметров](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="1ad97-272">При выполнении модуля runbook с помощью веб-перехватчика hello предопределенные входной параметр  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  отправляется вместе с hello входные параметры, которые были определены.</span><span class="sxs-lookup"><span data-stu-id="1ad97-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="1ad97-273">Можно щелкнуть tooexpand hello **WebhookData** параметр для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="1ad97-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![Параметр WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="1ad97-275">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ad97-275">Next steps</span></span>
* <span data-ttu-id="1ad97-276">Дополнительные сведения о входных и выходных данных Runbook см. в записи блога [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/) (Служба автоматизации Azure. Входные и выходные данные Runbook. Вложенные модули Runbook).</span><span class="sxs-lookup"><span data-stu-id="1ad97-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="1ad97-277">Дополнительные сведения о различных способов toostart runbook см. в разделе [запуск runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1ad97-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="1ad97-278">tooedit текстовое runbook, см. слишком[редактирование текстовое runbooks](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1ad97-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="1ad97-279">слишком ссылаться tooedit графический runbook[графический разработки в Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="1ad97-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

