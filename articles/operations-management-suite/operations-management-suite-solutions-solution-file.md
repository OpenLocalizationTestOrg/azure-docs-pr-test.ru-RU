---
title: "aaaCreating решения для управления в Operations Management Suite (OMS) | Документы Microsoft"
description: "Решения для управления расширить функциональность hello Operations Management Suite (OMS), предоставляя сценариев пакете управления, клиентам можно добавить tootheir рабочей области OMS.  Эта статья содержит сведения по созданию toobe решений управления используется в вашей рабочей среде или сделаны доступными tooyour клиентов."
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
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="8b794-104">Создание файла решения по управлению в Operations Management Suite (OMS) (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="8b794-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="8b794-105">Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="8b794-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="8b794-106">Ни одной схеме, описанной ниже — toochange субъекта.</span><span class="sxs-lookup"><span data-stu-id="8b794-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="8b794-107">Решения по управлению в Operations Management Suite (OMS) реализованы в виде [шаблонов Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8b794-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="8b794-108">Основная задача Hello при изучении способ обучения tooauthor решения для управления как слишком[создания шаблона](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8b794-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="8b794-109">Эта статья содержит уникальные сведения шаблонов, используемых решениями и каким образом ресурсы tooconfigure стандартного решения.</span><span class="sxs-lookup"><span data-stu-id="8b794-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="8b794-110">Средства</span><span class="sxs-lookup"><span data-stu-id="8b794-110">Tools</span></span>

<span data-ttu-id="8b794-111">Можно использовать любой текстовый редактор toowork файлы решений, но рекомендуется использование возможностей hello, представлены в Visual Studio или кода Visual Studio, как описано в следующих статей hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="8b794-112">Создание и развертывание групп ресурсов Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8b794-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="8b794-113">Работа с шаблонами Azure Resource Manager в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8b794-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="8b794-114">structure</span><span class="sxs-lookup"><span data-stu-id="8b794-114">Structure</span></span>
<span data-ttu-id="8b794-115">Базовая структура файла решения управления Hello Здравствуйте, таким же, как [шаблона диспетчера ресурсов](../azure-resource-manager/resource-group-authoring-templates.md#template-format) которой выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="8b794-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="8b794-116">В следующих разделах hello описаны элементы верхнего уровня hello и и их содержимое в решении.</span><span class="sxs-lookup"><span data-stu-id="8b794-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="8b794-117">Параметры</span><span class="sxs-lookup"><span data-stu-id="8b794-117">Parameters</span></span>
<span data-ttu-id="8b794-118">[Параметры](../azure-resource-manager/resource-group-authoring-templates.md#parameters) являются значениями, которые требуют от пользователя hello при установке решения по управлению hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="8b794-119">Существуют стандартные параметры для всех решений. При необходимости можно добавить дополнительные параметры для конкретного решения.</span><span class="sxs-lookup"><span data-stu-id="8b794-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="8b794-120">Как пользователи будут указывать значения параметров при установке решения будет зависеть от определенного параметра hello и установка решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="8b794-121">Если пользователь устанавливает решение управления через hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) или [быстрый запуск Azure шаблоны](operations-management-suite-solutions.md#finding-and-installing-management-solutions) они являются запрашиваемые tooselect [OMS рабочей области и учетной записи автоматизации ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="8b794-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="8b794-122">Это используется toopopulate hello значения каждого из стандартных параметров hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="8b794-123">Hello пользователю не предлагается toodirectly указать значения для стандартных параметров hello, но они запрашиваемые tooprovide значения для всех дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="8b794-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="8b794-124">Когда hello пользователь устанавливает решение [другой метод](operations-management-suite-solutions.md#finding-and-installing-management-solutions), они должны предоставить значение для всех стандартных параметров и все дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="8b794-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="8b794-125">Ниже приведен пример параметра.</span><span class="sxs-lookup"><span data-stu-id="8b794-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="8b794-126">Привет, в следующей таблице описываются атрибуты hello параметра.</span><span class="sxs-lookup"><span data-stu-id="8b794-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="8b794-127">Атрибут</span><span class="sxs-lookup"><span data-stu-id="8b794-127">Attribute</span></span> | <span data-ttu-id="8b794-128">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="8b794-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b794-129">type</span><span class="sxs-lookup"><span data-stu-id="8b794-129">type</span></span> |<span data-ttu-id="8b794-130">Тип данных параметра hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-130">Data type for hello parameter.</span></span> <span data-ttu-id="8b794-131">Hello управления вводом, отображаемый для пользователя hello зависит от типа данных hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="8b794-132">bool — раскрывающийся список</span><span class="sxs-lookup"><span data-stu-id="8b794-132">bool - Drop down box</span></span><br><span data-ttu-id="8b794-133">string — текстовое поле</span><span class="sxs-lookup"><span data-stu-id="8b794-133">string - Text box</span></span><br><span data-ttu-id="8b794-134">int — текстовое поле</span><span class="sxs-lookup"><span data-stu-id="8b794-134">int - Text box</span></span><br><span data-ttu-id="8b794-135">securestring — поле для ввода пароля</span><span class="sxs-lookup"><span data-stu-id="8b794-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="8b794-136">category</span><span class="sxs-lookup"><span data-stu-id="8b794-136">category</span></span> |<span data-ttu-id="8b794-137">Необязательный категорию параметра hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="8b794-138">Параметры в одной категории группируются hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="8b794-139">control</span><span class="sxs-lookup"><span data-stu-id="8b794-139">control</span></span> |<span data-ttu-id="8b794-140">Дополнительная функция для строковых параметров.</span><span class="sxs-lookup"><span data-stu-id="8b794-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="8b794-141">datetime — отображается элемент управления для даты и времени.</span><span class="sxs-lookup"><span data-stu-id="8b794-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="8b794-142">Идентификатор GUID - значение идентификатора Guid формируется автоматически и не отображается параметр hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="8b794-143">Описание</span><span class="sxs-lookup"><span data-stu-id="8b794-143">description</span></span> |<span data-ttu-id="8b794-144">Необязательное описание для параметра hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="8b794-145">Отображаются сведения всплывающей Далее toohello параметр.</span><span class="sxs-lookup"><span data-stu-id="8b794-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="8b794-146">Стандартные параметры</span><span class="sxs-lookup"><span data-stu-id="8b794-146">Standard parameters</span></span>
<span data-ttu-id="8b794-147">Hello следующей таблице перечислены стандартные параметры hello для всех решений управления.</span><span class="sxs-lookup"><span data-stu-id="8b794-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="8b794-148">Эти значения будут заполнены пользователем hello вместо запроса их при установке решения на основе шаблонов hello Azure Marketplace или краткое руководство.</span><span class="sxs-lookup"><span data-stu-id="8b794-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="8b794-149">необходимо указать значения для них Hello пользователя, если hello решение устанавливается с помощью другого метода.</span><span class="sxs-lookup"><span data-stu-id="8b794-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="8b794-150">пользовательский интерфейс Hello в шаблонах Azure Marketplace и примеры использования hello ожидает hello имена параметров в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="8b794-151">Если вы используете разные имена параметров затем hello пользователя будет запрашиваться их и они будут заполнены автоматически.</span><span class="sxs-lookup"><span data-stu-id="8b794-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="8b794-152">Параметр</span><span class="sxs-lookup"><span data-stu-id="8b794-152">Parameter</span></span> | <span data-ttu-id="8b794-153">Тип</span><span class="sxs-lookup"><span data-stu-id="8b794-153">Type</span></span> | <span data-ttu-id="8b794-154">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="8b794-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b794-155">accountName</span><span class="sxs-lookup"><span data-stu-id="8b794-155">accountName</span></span> |<span data-ttu-id="8b794-156">строка</span><span class="sxs-lookup"><span data-stu-id="8b794-156">string</span></span> |<span data-ttu-id="8b794-157">Учетная запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="8b794-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="8b794-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="8b794-158">pricingTier</span></span> |<span data-ttu-id="8b794-159">string</span><span class="sxs-lookup"><span data-stu-id="8b794-159">string</span></span> |<span data-ttu-id="8b794-160">Ценовая категория рабочей области Log Analytics и учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="8b794-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="8b794-161">regionId</span><span class="sxs-lookup"><span data-stu-id="8b794-161">regionId</span></span> |<span data-ttu-id="8b794-162">string</span><span class="sxs-lookup"><span data-stu-id="8b794-162">string</span></span> |<span data-ttu-id="8b794-163">Область hello учетной записи службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="8b794-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="8b794-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="8b794-164">solutionName</span></span> |<span data-ttu-id="8b794-165">string</span><span class="sxs-lookup"><span data-stu-id="8b794-165">string</span></span> |<span data-ttu-id="8b794-166">Имя решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-166">Name of hello solution.</span></span>  <span data-ttu-id="8b794-167">При развертывании решения через примеры использования шаблонов, то следует определить имя_решения как параметр, можно определить строку, вместо необходимости toospecify пользователя hello один.</span><span class="sxs-lookup"><span data-stu-id="8b794-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="8b794-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="8b794-168">workspaceName</span></span> |<span data-ttu-id="8b794-169">строка</span><span class="sxs-lookup"><span data-stu-id="8b794-169">string</span></span> |<span data-ttu-id="8b794-170">Имя рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b794-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="8b794-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="8b794-171">workspaceRegionId</span></span> |<span data-ttu-id="8b794-172">string</span><span class="sxs-lookup"><span data-stu-id="8b794-172">string</span></span> |<span data-ttu-id="8b794-173">Области рабочей области аналитики журналов hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="8b794-174">Ниже приведен структуры hello hello стандартных параметров, которые можно скопировать и вставить в файл решения.</span><span class="sxs-lookup"><span data-stu-id="8b794-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

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
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="8b794-175">Ссылки tooparameter значения в других элементах hello решения с использованием синтаксиса hello **параметры ("имя параметра")**.</span><span class="sxs-lookup"><span data-stu-id="8b794-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="8b794-176">Например, tooaccess Здравствуйте имя рабочей области, можно использовать **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="8b794-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="8b794-177">Переменные</span><span class="sxs-lookup"><span data-stu-id="8b794-177">Variables</span></span>
<span data-ttu-id="8b794-178">[Переменные](../azure-resource-manager/resource-group-authoring-templates.md#variables) — это значения, которые будут использоваться в hello остальной части решения по управлению hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="8b794-179">Эти значения не предоставляется toohello пользователь, устанавливающий hello решения.</span><span class="sxs-lookup"><span data-stu-id="8b794-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="8b794-180">Они являются предполагаемого tooprovide hello автору, с одного места, где ими значения, которые могут использоваться несколько раз на протяжении hello решения.</span><span class="sxs-lookup"><span data-stu-id="8b794-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="8b794-181">Решения определенных tooyour значения должны быть помещены в переменные как противоположность toohard кодировать их в hello **ресурсов** элемента.</span><span class="sxs-lookup"><span data-stu-id="8b794-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="8b794-182">Это повышает удобочитаемость кода hello и предоставляет tooeasily изменения этих значений в более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="8b794-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="8b794-183">Ниже приведен пример элемента **variables** с типичные параметрами, используемыми в решениях.</span><span class="sxs-lookup"><span data-stu-id="8b794-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="8b794-184">Ссылки toovariable значений с помощью решения hello синтаксису hello **переменных ("имя переменной")**.</span><span class="sxs-lookup"><span data-stu-id="8b794-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="8b794-185">Например, tooaccess Здравствуйте имя_решения переменной, следует использовать **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="8b794-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="8b794-186">Кроме того, можно определить сложные переменные как несколько наборов значений.</span><span class="sxs-lookup"><span data-stu-id="8b794-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="8b794-187">Это особенно удобно в решениях по управлению, где для разных типов ресурсов определяется несколько свойств.</span><span class="sxs-lookup"><span data-stu-id="8b794-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="8b794-188">Например вы измените показанный выше toohello следующие переменные решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="8b794-189">В этом случае ссылки toovariable значений с помощью решения hello синтаксису hello **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="8b794-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="8b794-190">Например, tooaccess Здравствуйте переменной имя решения, следует использовать **variables('Solution'). Имя**.</span><span class="sxs-lookup"><span data-stu-id="8b794-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="8b794-191">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="8b794-191">Resources</span></span>
<span data-ttu-id="8b794-192">[Ресурсы](../azure-resource-manager/resource-group-authoring-templates.md#resources) определить hello различных ресурсов, которые будут устанавливать и настраивать решения по управлению.</span><span class="sxs-lookup"><span data-stu-id="8b794-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="8b794-193">Это будет наибольшее hello и самые сложные части шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="8b794-194">Можно получить структуру hello и полное описание элементов ресурсов в [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="8b794-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="8b794-195">В других статьях этой документации описаны различные ресурсы, которые обычно определяются.</span><span class="sxs-lookup"><span data-stu-id="8b794-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="8b794-196">Зависимости</span><span class="sxs-lookup"><span data-stu-id="8b794-196">Dependencies</span></span>
<span data-ttu-id="8b794-197">Hello **dependsOn** указывает элементы [зависимостей](../azure-resource-manager/resource-group-define-dependencies.md) на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="8b794-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="8b794-198">При установке решения hello ресурса не создается, пока все его зависимости были созданы.</span><span class="sxs-lookup"><span data-stu-id="8b794-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="8b794-199">Например, при установке решение может [запустить модуль Runbook](operations-management-suite-solutions-resources-automation.md#runbooks) с помощью [ресурса задания](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="8b794-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="8b794-200">ресурс Hello заданий будет зависеть от hello runbook ресурсов toomake том, что для этого модуля hello создается перед созданием задания hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="8b794-201">Рабочая область OMS и учетная запись службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="8b794-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="8b794-202">Решения управления требуют [рабочей области OMS](../log-analytics/log-analytics-manage-access.md) toocontain представления и [учетной записи автоматизации](../automation/automation-security-overview.md#automation-account-overview) toocontain модулей Runbook и ресурсы, связанные с.</span><span class="sxs-lookup"><span data-stu-id="8b794-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="8b794-203">Они должны быть доступны перед hello ресурсы в hello решения создаются и не должен быть определен в самом решении hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="8b794-204">Hello пользователя будет [укажите рабочую область и учетную запись](operations-management-suite-solutions.md#oms-workspace-and-automation-account) при развертывании решения, но разработчики hello следует после точки hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="8b794-205">Ресурс решения</span><span class="sxs-lookup"><span data-stu-id="8b794-205">Solution resource</span></span>
<span data-ttu-id="8b794-206">Каждое решение требует запись ресурса в hello **ресурсов** элемент, определяющий само решение hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="8b794-207">Это будет иметь тип **Microsoft.OperationsManagement/solutions** и имеют следующие структуры hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="8b794-208">Сюда входят [стандартные параметры](#parameters) и [переменных](#variables) , являются типовыми toodefine свойствами hello решения.</span><span class="sxs-lookup"><span data-stu-id="8b794-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


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




### <a name="dependencies"></a><span data-ttu-id="8b794-209">Зависимости</span><span class="sxs-lookup"><span data-stu-id="8b794-209">Dependencies</span></span>
<span data-ttu-id="8b794-210">Hello решения ресурс должен иметь [зависимостей](../azure-resource-manager/resource-group-define-dependencies.md) на каждый ресурс в решении hello, так как они должны tooexist перед созданием hello решения.</span><span class="sxs-lookup"><span data-stu-id="8b794-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="8b794-211">Это делается путем добавления записи для каждого ресурса в hello **dependsOn** элемента.</span><span class="sxs-lookup"><span data-stu-id="8b794-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="8b794-212">Свойства</span><span class="sxs-lookup"><span data-stu-id="8b794-212">Properties</span></span>
<span data-ttu-id="8b794-213">Библиотека ресурсов Hello имеет свойства hello в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="8b794-214">Сюда входят ресурсы hello ссылки и принадлежащих hello решение, которое определяет управление hello ресурсов после установки решения для hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="8b794-215">Каждый ресурс в решении hello должна быть указана в любом hello **referencedResources** или hello **containedResources** свойство.</span><span class="sxs-lookup"><span data-stu-id="8b794-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="8b794-216">Свойство</span><span class="sxs-lookup"><span data-stu-id="8b794-216">Property</span></span> | <span data-ttu-id="8b794-217">Описание</span><span class="sxs-lookup"><span data-stu-id="8b794-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b794-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="8b794-218">workspaceResourceId</span></span> |<span data-ttu-id="8b794-219">Идентификатор рабочей области аналитики журналов hello в форме hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<имя рабочей области\>*.</span><span class="sxs-lookup"><span data-stu-id="8b794-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="8b794-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="8b794-220">referencedResources</span></span> |<span data-ttu-id="8b794-221">Список ресурсов в решении hello, который не должен быть удален при удалении решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="8b794-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="8b794-222">containedResources</span></span> |<span data-ttu-id="8b794-223">Список ресурсов в решении hello, который должен быть удален при удалении решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="8b794-224">пример Hello выше предназначен для решения с runbook, расписание и представления.</span><span class="sxs-lookup"><span data-stu-id="8b794-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="8b794-225">расписание Hello и runbook *упоминаемого* в hello **свойства** элемента, поэтому они не удаляются при удалении решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="8b794-226">представление Hello *содержится* , он удаляется при удалении решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="8b794-227">План</span><span class="sxs-lookup"><span data-stu-id="8b794-227">Plan</span></span>
<span data-ttu-id="8b794-228">Hello **плана** сущность hello решения ресурса имеет свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="8b794-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="8b794-229">Свойство</span><span class="sxs-lookup"><span data-stu-id="8b794-229">Property</span></span> | <span data-ttu-id="8b794-230">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="8b794-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b794-231">name</span><span class="sxs-lookup"><span data-stu-id="8b794-231">name</span></span> |<span data-ttu-id="8b794-232">Имя решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-232">Name of hello solution.</span></span> |
| <span data-ttu-id="8b794-233">версия</span><span class="sxs-lookup"><span data-stu-id="8b794-233">version</span></span> |<span data-ttu-id="8b794-234">Версия решения hello определяется автором hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="8b794-235">product</span><span class="sxs-lookup"><span data-stu-id="8b794-235">product</span></span> |<span data-ttu-id="8b794-236">Уникальная строка tooidentify hello решения.</span><span class="sxs-lookup"><span data-stu-id="8b794-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="8b794-237">publisher</span><span class="sxs-lookup"><span data-stu-id="8b794-237">publisher</span></span> |<span data-ttu-id="8b794-238">Издатель решения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="8b794-239">Образец</span><span class="sxs-lookup"><span data-stu-id="8b794-239">Sample</span></span>
<span data-ttu-id="8b794-240">Образцы файлов решения с ресурсом решения можно просмотреть в следующих расположения hello.</span><span class="sxs-lookup"><span data-stu-id="8b794-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="8b794-241">Ресурсы службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="8b794-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="8b794-242">Сохраненные поиски и оповещения Log Analytics в решениях OMS (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="8b794-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="8b794-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b794-243">Next steps</span></span>
* <span data-ttu-id="8b794-244">[Добавьте сохраненные поисковые запросы и оповещения](operations-management-suite-solutions-resources-searches-alerts.md) tooyour решение для управления.</span><span class="sxs-lookup"><span data-stu-id="8b794-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="8b794-245">[Добавление представления](operations-management-suite-solutions-resources-views.md) tooyour решение для управления.</span><span class="sxs-lookup"><span data-stu-id="8b794-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="8b794-246">[Добавление модулей Runbook и другие ресурсы автоматизации](operations-management-suite-solutions-resources-automation.md) tooyour решение для управления.</span><span class="sxs-lookup"><span data-stu-id="8b794-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="8b794-247">Узнайте подробности hello [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8b794-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8b794-248">Найдите в коллекции [шаблонов быстрого запуска Azure](https://azure.microsoft.com/documentation/templates) примеры разных шаблонов Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b794-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
