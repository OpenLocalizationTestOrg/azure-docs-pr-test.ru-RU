---
title: "Создание решений для управления в Operations Management Suite (OMS) | Документация Майкрософт"
description: "Решения для управления расширяют функции консоли Operations Management Suite (OMS), предоставляя упакованные сценарии управления, которые клиенты могут добавить в свое рабочее пространство OMS.  В этой статье описано, как создавать решения для управления, которые можно использовать в своей среде или предоставлять другим пользователям."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee3462c13101d18921dc488b08c79e1e4e02ff3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="4d26f-104">Создание файла решения по управлению в Operations Management Suite (OMS) (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="4d26f-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="4d26f-105">Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="4d26f-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="4d26f-106">Любые схемы, приведенные ниже, могут измениться.</span><span class="sxs-lookup"><span data-stu-id="4d26f-106">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="4d26f-107">Решения по управлению в Operations Management Suite (OMS) реализованы в виде [шаблонов Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="4d26f-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="4d26f-108">Поэтому создание решения для управления — это, по сути, [создание шаблона](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4d26f-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="4d26f-109">В этой статье подробно описываются шаблоны, используемые для решений, а также способы настойки ресурсов для типичного решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="4d26f-110">Средства</span><span class="sxs-lookup"><span data-stu-id="4d26f-110">Tools</span></span>

<span data-ttu-id="4d26f-111">Для работы с файлами решения можно использовать любой текстовый редактор, но мы рекомендуем использовать компоненты, предоставляемые в Visual Studio или Visual Studio Code, как описано в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="4d26f-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span></span>

- [<span data-ttu-id="4d26f-112">Создание и развертывание групп ресурсов Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d26f-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="4d26f-113">Работа с шаблонами Azure Resource Manager в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4d26f-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="4d26f-114">structure</span><span class="sxs-lookup"><span data-stu-id="4d26f-114">Structure</span></span>
<span data-ttu-id="4d26f-115">Базовая структура файла решения для управления аналогична структуре [шаблона Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#template-format) и выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="4d26f-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="4d26f-116">В следующих разделах описаны элементы верхнего уровня и их содержимое в решении.</span><span class="sxs-lookup"><span data-stu-id="4d26f-116">Each of the sections below describes the top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="4d26f-117">Параметры</span><span class="sxs-lookup"><span data-stu-id="4d26f-117">Parameters</span></span>
<span data-ttu-id="4d26f-118">[Параметры](../azure-resource-manager/resource-group-authoring-templates.md#parameters) — это значения, которые пользователь указывает при установке решения для управления.</span><span class="sxs-lookup"><span data-stu-id="4d26f-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span></span>  <span data-ttu-id="4d26f-119">Существуют стандартные параметры для всех решений. При необходимости можно добавить дополнительные параметры для конкретного решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="4d26f-120">Каким образом пользователи будут указывать значения параметров при установке решения, будет зависеть от конкретного параметра и способа установки решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span></span>

<span data-ttu-id="4d26f-121">Если пользователь устанавливает решение для управления с помощью [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) или [шаблонов быстрого запуска Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions), ему будет предложено выбрать [рабочую область OMS и учетную запись службы автоматизации](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="4d26f-121">When a user installs your management solution through the [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted to select an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="4d26f-122">Их используют для заполнения значений для каждого из стандартных параметров.</span><span class="sxs-lookup"><span data-stu-id="4d26f-122">These are used to populate the values of each of the standard parameters.</span></span>  <span data-ttu-id="4d26f-123">Здесь пользователю совсем не обязательно указывать значения для всех стандартных параметров, а только для дополнительных.</span><span class="sxs-lookup"><span data-stu-id="4d26f-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span></span>

<span data-ttu-id="4d26f-124">При установке решения [другим способом](operations-management-suite-solutions.md#finding-and-installing-management-solutions) пользователю нужно указать значения для всех стандартных и дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="4d26f-124">When the user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="4d26f-125">Ниже приведен пример параметра.</span><span class="sxs-lookup"><span data-stu-id="4d26f-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="4d26f-126">В следующей таблице описываются атрибуты параметра.</span><span class="sxs-lookup"><span data-stu-id="4d26f-126">The following table describes the attributes of a parameter.</span></span>

| <span data-ttu-id="4d26f-127">Атрибут</span><span class="sxs-lookup"><span data-stu-id="4d26f-127">Attribute</span></span> | <span data-ttu-id="4d26f-128">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="4d26f-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4d26f-129">type</span><span class="sxs-lookup"><span data-stu-id="4d26f-129">type</span></span> |<span data-ttu-id="4d26f-130">Тип данных для параметра.</span><span class="sxs-lookup"><span data-stu-id="4d26f-130">Data type for the parameter.</span></span> <span data-ttu-id="4d26f-131">Элемент управления вводом, отображаемый для пользователя, зависит от типа данных.</span><span class="sxs-lookup"><span data-stu-id="4d26f-131">The input control displayed for the user depends on the data type.</span></span><br><br><span data-ttu-id="4d26f-132">bool — раскрывающийся список</span><span class="sxs-lookup"><span data-stu-id="4d26f-132">bool - Drop down box</span></span><br><span data-ttu-id="4d26f-133">string — текстовое поле</span><span class="sxs-lookup"><span data-stu-id="4d26f-133">string - Text box</span></span><br><span data-ttu-id="4d26f-134">int — текстовое поле</span><span class="sxs-lookup"><span data-stu-id="4d26f-134">int - Text box</span></span><br><span data-ttu-id="4d26f-135">securestring — поле для ввода пароля</span><span class="sxs-lookup"><span data-stu-id="4d26f-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="4d26f-136">category</span><span class="sxs-lookup"><span data-stu-id="4d26f-136">category</span></span> |<span data-ttu-id="4d26f-137">Необязательная категория для параметра.</span><span class="sxs-lookup"><span data-stu-id="4d26f-137">Optional category for the parameter.</span></span>  <span data-ttu-id="4d26f-138">Параметры одной категории группируются.</span><span class="sxs-lookup"><span data-stu-id="4d26f-138">Parameters in the same category are grouped together.</span></span> |
| <span data-ttu-id="4d26f-139">control</span><span class="sxs-lookup"><span data-stu-id="4d26f-139">control</span></span> |<span data-ttu-id="4d26f-140">Дополнительная функция для строковых параметров.</span><span class="sxs-lookup"><span data-stu-id="4d26f-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="4d26f-141">datetime — отображается элемент управления для даты и времени.</span><span class="sxs-lookup"><span data-stu-id="4d26f-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="4d26f-142">guid — значение GUID создается автоматически и параметр не отображается.</span><span class="sxs-lookup"><span data-stu-id="4d26f-142">guid - Guid value is automatically generated, and the parameter is not displayed.</span></span> |
| <span data-ttu-id="4d26f-143">Описание</span><span class="sxs-lookup"><span data-stu-id="4d26f-143">description</span></span> |<span data-ttu-id="4d26f-144">Необязательное описание параметра.</span><span class="sxs-lookup"><span data-stu-id="4d26f-144">Optional description for the parameter.</span></span>  <span data-ttu-id="4d26f-145">Отображается в информационном всплывающем предупреждении возле параметра.</span><span class="sxs-lookup"><span data-stu-id="4d26f-145">Displayed in an information balloon next to the parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="4d26f-146">Стандартные параметры</span><span class="sxs-lookup"><span data-stu-id="4d26f-146">Standard parameters</span></span>
<span data-ttu-id="4d26f-147">В следующей таблице перечислены стандартные параметры для всех решений для управления.</span><span class="sxs-lookup"><span data-stu-id="4d26f-147">The following table lists the standard parameters for all management solutions.</span></span>  <span data-ttu-id="4d26f-148">Эти значения заполняются автоматически, а не предлагаются для заполнения пользователем при установке решения из Azure Marketplace или с помощью шаблонов быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="4d26f-148">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="4d26f-149">Пользователь должен указать значения для стандартных параметров, если решение устанавливается другим способом.</span><span class="sxs-lookup"><span data-stu-id="4d26f-149">The user must provide values for them if the solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="4d26f-150">Пользовательский интерфейс в Azure Marketplace и шаблонах быстрого запуска ожидает ввода имен параметров, указанных в таблице.</span><span class="sxs-lookup"><span data-stu-id="4d26f-150">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span></span>  <span data-ttu-id="4d26f-151">При использовании других имен параметров пользователю будет предложено указать их, они не будут указаны автоматически.</span><span class="sxs-lookup"><span data-stu-id="4d26f-151">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="4d26f-152">Параметр</span><span class="sxs-lookup"><span data-stu-id="4d26f-152">Parameter</span></span> | <span data-ttu-id="4d26f-153">Тип</span><span class="sxs-lookup"><span data-stu-id="4d26f-153">Type</span></span> | <span data-ttu-id="4d26f-154">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="4d26f-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4d26f-155">accountName</span><span class="sxs-lookup"><span data-stu-id="4d26f-155">accountName</span></span> |<span data-ttu-id="4d26f-156">строка</span><span class="sxs-lookup"><span data-stu-id="4d26f-156">string</span></span> |<span data-ttu-id="4d26f-157">Учетная запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="4d26f-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="4d26f-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="4d26f-158">pricingTier</span></span> |<span data-ttu-id="4d26f-159">string</span><span class="sxs-lookup"><span data-stu-id="4d26f-159">string</span></span> |<span data-ttu-id="4d26f-160">Ценовая категория рабочей области Log Analytics и учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="4d26f-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="4d26f-161">regionId</span><span class="sxs-lookup"><span data-stu-id="4d26f-161">regionId</span></span> |<span data-ttu-id="4d26f-162">строка</span><span class="sxs-lookup"><span data-stu-id="4d26f-162">string</span></span> |<span data-ttu-id="4d26f-163">Регион службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="4d26f-163">Region of the Azure Automation account.</span></span> |
| <span data-ttu-id="4d26f-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="4d26f-164">solutionName</span></span> |<span data-ttu-id="4d26f-165">строка</span><span class="sxs-lookup"><span data-stu-id="4d26f-165">string</span></span> |<span data-ttu-id="4d26f-166">Имя решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-166">Name of the solution.</span></span>  <span data-ttu-id="4d26f-167">При развертывании решения с использованием шаблонов быстрого запуска следует указать solutionName как параметр, чтобы можно было определить строку и не требовалось, чтобы ее указывал пользователь.</span><span class="sxs-lookup"><span data-stu-id="4d26f-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span></span> |
| <span data-ttu-id="4d26f-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="4d26f-168">workspaceName</span></span> |<span data-ttu-id="4d26f-169">строка</span><span class="sxs-lookup"><span data-stu-id="4d26f-169">string</span></span> |<span data-ttu-id="4d26f-170">Имя рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4d26f-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="4d26f-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="4d26f-171">workspaceRegionId</span></span> |<span data-ttu-id="4d26f-172">строка</span><span class="sxs-lookup"><span data-stu-id="4d26f-172">string</span></span> |<span data-ttu-id="4d26f-173">Регион рабочего пространства Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4d26f-173">Region of the Log Analytics workspace.</span></span> |


<span data-ttu-id="4d26f-174">Ниже приведена структура стандартных параметров, которую можно скопировать и вставить в файл решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-174">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="4d26f-175">Ссылки на значения параметров в других элементах решения создаются с помощью синтаксиса **parameters('имя_параметра')**.</span><span class="sxs-lookup"><span data-stu-id="4d26f-175">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="4d26f-176">Например, для доступа к имени рабочей области можно использовать **parameters('имя_рабочей_области')**.</span><span class="sxs-lookup"><span data-stu-id="4d26f-176">For example, to access the workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="4d26f-177">Переменные</span><span class="sxs-lookup"><span data-stu-id="4d26f-177">Variables</span></span>
<span data-ttu-id="4d26f-178">[Переменные](../azure-resource-manager/resource-group-authoring-templates.md#variables) представляют собой значения, которые будут использоваться в остальной части решения по управлению.</span><span class="sxs-lookup"><span data-stu-id="4d26f-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span></span>  <span data-ttu-id="4d26f-179">Эти значения невидимы для пользователя, который устанавливает решение.</span><span class="sxs-lookup"><span data-stu-id="4d26f-179">These values are not exposed to the user installing the solution.</span></span>  <span data-ttu-id="4d26f-180">Их задача — обеспечить пользователя единым расположением для управления значениями, которые в решении могут использоваться многократно.</span><span class="sxs-lookup"><span data-stu-id="4d26f-180">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span></span> <span data-ttu-id="4d26f-181">Все значения для решения следует поместить в переменные, а не прямо указывать их в элементе **resources** в коде.</span><span class="sxs-lookup"><span data-stu-id="4d26f-181">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span></span>  <span data-ttu-id="4d26f-182">Таким образом код становится более удобным для чтения. Кроме того, в этом случае значения можно легко изменить в более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="4d26f-182">This makes the code more readable and allows you to easily change these values in later versions.</span></span>

<span data-ttu-id="4d26f-183">Ниже приведен пример элемента **variables** с типичные параметрами, используемыми в решениях.</span><span class="sxs-lookup"><span data-stu-id="4d26f-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="4d26f-184">Обращаться к значениям переменных в рамках решения можно с помощью синтаксиса **variables('имя_переменной')**.</span><span class="sxs-lookup"><span data-stu-id="4d26f-184">You refer to variable values through the solution with the syntax **variables('variable name')**.</span></span>  <span data-ttu-id="4d26f-185">Например, для доступа к переменной SolutionName можно использовать синтаксис **variables('имя_решения')**.</span><span class="sxs-lookup"><span data-stu-id="4d26f-185">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="4d26f-186">Кроме того, можно определить сложные переменные как несколько наборов значений.</span><span class="sxs-lookup"><span data-stu-id="4d26f-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="4d26f-187">Это особенно удобно в решениях по управлению, где для разных типов ресурсов определяется несколько свойств.</span><span class="sxs-lookup"><span data-stu-id="4d26f-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="4d26f-188">Например, можно изменить структуру переменных решения выше, чтобы они выглядели следующим образом.</span><span class="sxs-lookup"><span data-stu-id="4d26f-188">For example, you could restructure the solution variables shown above to the following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="4d26f-189">В этом случае обращаться к значениям переменных в рамках решения можно с помощью синтаксиса **variables('имя_переменной').property**.</span><span class="sxs-lookup"><span data-stu-id="4d26f-189">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="4d26f-190">Например, для доступа к переменной SolutionName можно использовать синтаксис **variables('решение').Name**.</span><span class="sxs-lookup"><span data-stu-id="4d26f-190">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="4d26f-191">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="4d26f-191">Resources</span></span>
<span data-ttu-id="4d26f-192">Элемент [Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) определяет различные ресурсы, которые будет устанавливать и настраивать решение по управлению.</span><span class="sxs-lookup"><span data-stu-id="4d26f-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="4d26f-193">Это самая крупная и сложная часть шаблона.</span><span class="sxs-lookup"><span data-stu-id="4d26f-193">This will be the largest and most complex portion of the template.</span></span>  <span data-ttu-id="4d26f-194">Структуру и полное описание элементов ресурсов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="4d26f-194">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="4d26f-195">В других статьях этой документации описаны различные ресурсы, которые обычно определяются.</span><span class="sxs-lookup"><span data-stu-id="4d26f-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="4d26f-196">Зависимости</span><span class="sxs-lookup"><span data-stu-id="4d26f-196">Dependencies</span></span>
<span data-ttu-id="4d26f-197">Элемент **dependsOn** указывает [зависимость](../azure-resource-manager/resource-group-define-dependencies.md) от другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4d26f-197">The **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="4d26f-198">При установке решения ресурс не создается, пока не будут созданы все его зависимости.</span><span class="sxs-lookup"><span data-stu-id="4d26f-198">When the solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="4d26f-199">Например, при установке решение может [запустить модуль Runbook](operations-management-suite-solutions-resources-automation.md#runbooks) с помощью [ресурса задания](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="4d26f-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="4d26f-200">Ресурс задания будет зависеть от ресурса модуля Runbook. Таким образом обеспечивается создание модуля Runbook до задания.</span><span class="sxs-lookup"><span data-stu-id="4d26f-200">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="4d26f-201">Рабочая область OMS и учетная запись службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="4d26f-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="4d26f-202">Решения для управления требуют [рабочую область OMS](../log-analytics/log-analytics-manage-access.md) для хранения представлений и [учетную запись службы автоматизации](../automation/automation-security-overview.md#automation-account-overview) для хранения модулей Runbook и связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4d26f-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span>  <span data-ttu-id="4d26f-203">К ним нужно предоставить доступ перед созданием ресурсов решения. Их не нужно определять в самом решении.</span><span class="sxs-lookup"><span data-stu-id="4d26f-203">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span></span>  <span data-ttu-id="4d26f-204">Пользователь указывает [рабочую область и учетную запись](operations-management-suite-solutions.md#oms-workspace-and-automation-account) при развертывании решения. Однако разработчик решения должен учитывать следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="4d26f-204">The user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="4d26f-205">Ресурс решения</span><span class="sxs-lookup"><span data-stu-id="4d26f-205">Solution resource</span></span>
<span data-ttu-id="4d26f-206">Для каждого решения требуется запись ресурса в элементе **resources**, который определяет само решение.</span><span class="sxs-lookup"><span data-stu-id="4d26f-206">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span></span>  <span data-ttu-id="4d26f-207">Ресурс представлен типом **Microsoft.OperationsManagement/solutions** и имеет следующую структуру.</span><span class="sxs-lookup"><span data-stu-id="4d26f-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span></span> <span data-ttu-id="4d26f-208">К ним относятся [стандартные параметры](#parameters) и [переменные](#variables), которые, как правило, используются для определения свойств решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="4d26f-209">Зависимости</span><span class="sxs-lookup"><span data-stu-id="4d26f-209">Dependencies</span></span>
<span data-ttu-id="4d26f-210">Ресурс решения должен содержать [зависимость](../azure-resource-manager/resource-group-define-dependencies.md) от всех ресурсов решения, так как их нужно создать до решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-210">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span></span>  <span data-ttu-id="4d26f-211">Это можно сделать, добавив запись для каждого ресурса в элемент **dependsOn**.</span><span class="sxs-lookup"><span data-stu-id="4d26f-211">You do this by adding an entry for each resource in the **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="4d26f-212">Свойства</span><span class="sxs-lookup"><span data-stu-id="4d26f-212">Properties</span></span>
<span data-ttu-id="4d26f-213">У ресурса решения есть свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4d26f-213">The solution resource has the properties in the following table.</span></span>  <span data-ttu-id="4d26f-214">Сюда входят ресурсы, на которые решение ссылается и которые оно содержит. Это и определяет, как будет осуществляться управление ресурсом после установки решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-214">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span></span>  <span data-ttu-id="4d26f-215">Каждый ресурс в решении должен быть указан в одном из свойств: **referencedResources** или **containedResources**.</span><span class="sxs-lookup"><span data-stu-id="4d26f-215">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span></span>

| <span data-ttu-id="4d26f-216">Свойство</span><span class="sxs-lookup"><span data-stu-id="4d26f-216">Property</span></span> | <span data-ttu-id="4d26f-217">Описание</span><span class="sxs-lookup"><span data-stu-id="4d26f-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4d26f-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="4d26f-218">workspaceResourceId</span></span> |<span data-ttu-id="4d26f-219">Идентификатор рабочей области Log Analytics в формате *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<имя_рабочей_области\>*.</span><span class="sxs-lookup"><span data-stu-id="4d26f-219">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="4d26f-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="4d26f-220">referencedResources</span></span> |<span data-ttu-id="4d26f-221">Список ресурсов решения, которые не будут удалены при удалении решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-221">List of resources in the solution that should not be removed when the solution is removed.</span></span> |
| <span data-ttu-id="4d26f-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="4d26f-222">containedResources</span></span> |<span data-ttu-id="4d26f-223">Список ресурсов решения, которые будут удалены при удалении решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-223">List of resources in the solution that should be removed when the solution is removed.</span></span> |

<span data-ttu-id="4d26f-224">Приведенный выше пример предназначен для решения с модулем Runbook, расписанием и представлением.</span><span class="sxs-lookup"><span data-stu-id="4d26f-224">The example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="4d26f-225">На расписание и модуль Runbook *ссылается* элемент **properties**, поэтому они не будут удалены вместе с решением.</span><span class="sxs-lookup"><span data-stu-id="4d26f-225">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span></span>  <span data-ttu-id="4d26f-226">Представление *содержится* в решении, поэтому будет удалено при удалении решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-226">The view is *contained* so it is removed when the solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="4d26f-227">План</span><span class="sxs-lookup"><span data-stu-id="4d26f-227">Plan</span></span>
<span data-ttu-id="4d26f-228">Свойства сущности **plan** ресурса решения приведены в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4d26f-228">The **plan** entity of the solution resource has the properties in the following table.</span></span>

| <span data-ttu-id="4d26f-229">Свойство</span><span class="sxs-lookup"><span data-stu-id="4d26f-229">Property</span></span> | <span data-ttu-id="4d26f-230">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="4d26f-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4d26f-231">name</span><span class="sxs-lookup"><span data-stu-id="4d26f-231">name</span></span> |<span data-ttu-id="4d26f-232">Имя решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-232">Name of the solution.</span></span> |
| <span data-ttu-id="4d26f-233">версия</span><span class="sxs-lookup"><span data-stu-id="4d26f-233">version</span></span> |<span data-ttu-id="4d26f-234">Версия решения, указанная разработчиком.</span><span class="sxs-lookup"><span data-stu-id="4d26f-234">Version of the solution as determined by the author.</span></span> |
| <span data-ttu-id="4d26f-235">product</span><span class="sxs-lookup"><span data-stu-id="4d26f-235">product</span></span> |<span data-ttu-id="4d26f-236">Уникальная строка для определения решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-236">Unique string to identify the solution.</span></span> |
| <span data-ttu-id="4d26f-237">publisher</span><span class="sxs-lookup"><span data-stu-id="4d26f-237">publisher</span></span> |<span data-ttu-id="4d26f-238">Издатель решения.</span><span class="sxs-lookup"><span data-stu-id="4d26f-238">Publisher of the solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="4d26f-239">Образец</span><span class="sxs-lookup"><span data-stu-id="4d26f-239">Sample</span></span>
<span data-ttu-id="4d26f-240">Примеры файлов решения с ресурсом решения см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="4d26f-240">You can view samples of solution files with a solution resource at the following locations.</span></span>

- <span data-ttu-id="4d26f-241">[Automation resources](operations-management-suite-solutions-resources-automation.md#sample) (Ресурсы службы автоматизации)</span><span class="sxs-lookup"><span data-stu-id="4d26f-241">[Automation resources](operations-management-suite-solutions-resources-automation.md#sample)</span></span>
- [<span data-ttu-id="4d26f-242">Сохраненные поиски и оповещения Log Analytics в решениях OMS (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="4d26f-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="4d26f-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d26f-243">Next steps</span></span>
* <span data-ttu-id="4d26f-244">[Добавьте сохраненные поиски и оповещения](operations-management-suite-solutions-resources-searches-alerts.md) в решение для управления.</span><span class="sxs-lookup"><span data-stu-id="4d26f-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="4d26f-245">[Добавьте представления](operations-management-suite-solutions-resources-views.md) в решение для управления.</span><span class="sxs-lookup"><span data-stu-id="4d26f-245">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="4d26f-246">[Добавьте модули Runbook и другие ресурсы службы автоматизации](operations-management-suite-solutions-resources-automation.md) в решение по управлению.</span><span class="sxs-lookup"><span data-stu-id="4d26f-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>
* <span data-ttu-id="4d26f-247">Узнайте больше о [создании шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4d26f-247">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="4d26f-248">Найдите в коллекции [шаблонов быстрого запуска Azure](https://azure.microsoft.com/documentation/templates) примеры разных шаблонов Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d26f-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
