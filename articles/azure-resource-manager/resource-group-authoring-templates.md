---
title: "Структура и синтаксис шаблона Azure Resource Manager | Документация Майкрософт"
description: "Описывается создание структуры и свойств шаблонов Azure Resource Manager с помощью декларативного синтаксиса JSON."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="c7e10-103">Описание структуры и синтаксиса шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c7e10-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="c7e10-104">В этой статье описана структура шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7e10-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="c7e10-105">Статья содержит информацию о разных разделах шаблона и свойствах, которые доступны в этих разделах.</span><span class="sxs-lookup"><span data-stu-id="c7e10-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="c7e10-106">Шаблон состоит из JSON и выражений, на основе которых можно создавать значения для развертывания.</span><span class="sxs-lookup"><span data-stu-id="c7e10-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="c7e10-107">Пошаговое руководство по созданию шаблона приведено в разделе [Создание первого шаблона Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="c7e10-108">Формат шаблона</span><span class="sxs-lookup"><span data-stu-id="c7e10-108">Template format</span></span>
<span data-ttu-id="c7e10-109">Шаблон с самой простой структурой содержит следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="c7e10-109">In its simplest structure, a template contains the following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="c7e10-110">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c7e10-110">Element name</span></span> | <span data-ttu-id="c7e10-111">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c7e10-111">Required</span></span> | <span data-ttu-id="c7e10-112">Описание</span><span class="sxs-lookup"><span data-stu-id="c7e10-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c7e10-113">$schema</span><span class="sxs-lookup"><span data-stu-id="c7e10-113">$schema</span></span> |<span data-ttu-id="c7e10-114">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-114">Yes</span></span> |<span data-ttu-id="c7e10-115">Расположение файла схемы JSON, который описывает версию языка шаблона.</span><span class="sxs-lookup"><span data-stu-id="c7e10-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="c7e10-116">Используйте URL-адрес из предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="c7e10-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="c7e10-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="c7e10-117">contentVersion</span></span> |<span data-ttu-id="c7e10-118">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-118">Yes</span></span> |<span data-ttu-id="c7e10-119">Версия шаблона (например, 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="c7e10-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="c7e10-120">Для этого элемента можно предоставить любое значение.</span><span class="sxs-lookup"><span data-stu-id="c7e10-120">You can provide any value for this element.</span></span> <span data-ttu-id="c7e10-121">При развертывании ресурсов с помощью шаблона это значение позволяет убедиться в том, что используется нужный шаблон.</span><span class="sxs-lookup"><span data-stu-id="c7e10-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="c7e10-122">parameters</span><span class="sxs-lookup"><span data-stu-id="c7e10-122">parameters</span></span> |<span data-ttu-id="c7e10-123">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-123">No</span></span> |<span data-ttu-id="c7e10-124">Значения, которые предоставляются при выполнении развертывания для настройки развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e10-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="c7e10-125">variables</span><span class="sxs-lookup"><span data-stu-id="c7e10-125">variables</span></span> |<span data-ttu-id="c7e10-126">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-126">No</span></span> |<span data-ttu-id="c7e10-127">Значения, используемые в виде фрагментов JSON в шаблоне для упрощения выражений на языке шаблона.</span><span class="sxs-lookup"><span data-stu-id="c7e10-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="c7e10-128">ресурсов</span><span class="sxs-lookup"><span data-stu-id="c7e10-128">resources</span></span> |<span data-ttu-id="c7e10-129">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-129">Yes</span></span> |<span data-ttu-id="c7e10-130">Типы ресурсов, которые развертываются или обновляются в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e10-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="c7e10-131">outputs</span><span class="sxs-lookup"><span data-stu-id="c7e10-131">outputs</span></span> |<span data-ttu-id="c7e10-132">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-132">No</span></span> |<span data-ttu-id="c7e10-133">Значения, возвращаемые после развертывания.</span><span class="sxs-lookup"><span data-stu-id="c7e10-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="c7e10-134">Каждый элемент содержит свойства, которые можно задать.</span><span class="sxs-lookup"><span data-stu-id="c7e10-134">Each element contains properties you can set.</span></span> <span data-ttu-id="c7e10-135">В следующем примере приведен полный синтаксис шаблона.</span><span class="sxs-lookup"><span data-stu-id="c7e10-135">The following example contains the full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-the parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="c7e10-136">Разделы шаблона мы рассмотрим более подробно далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c7e10-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="c7e10-137">Выражения и функции</span><span class="sxs-lookup"><span data-stu-id="c7e10-137">Expressions and functions</span></span>
<span data-ttu-id="c7e10-138">Базовый синтаксис шаблона — это JSON.</span><span class="sxs-lookup"><span data-stu-id="c7e10-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="c7e10-139">Тем не менее выражения и функции расширяют значения JSON, доступные в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="c7e10-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="c7e10-140">Выражения записываются в строковых литералах JSON, первым и последним знаком которых являются квадратные скобки: `[` и `]` соответственно.</span><span class="sxs-lookup"><span data-stu-id="c7e10-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="c7e10-141">Значение выражения вычисляется при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="c7e10-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="c7e10-142">Хотя результат вычисления выражения и записывается как строковый литерал, он может иметь другой тип JSON, например массив или целое число, в зависимости от фактического выражения.</span><span class="sxs-lookup"><span data-stu-id="c7e10-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="c7e10-143">Чтобы строковый литерал, начинающийся с квадратной скобки (`[`), не интерпретировался как выражение, добавьте дополнительную скобку, чтобы строка начиналась со знака `[[`.</span><span class="sxs-lookup"><span data-stu-id="c7e10-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="c7e10-144">Как правило, выражения используются с функциями для выполнения операций по настройке развертывания.</span><span class="sxs-lookup"><span data-stu-id="c7e10-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="c7e10-145">Как и в языке JavaScript, вызовы функций форматируются так: `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="c7e10-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="c7e10-146">Обращение к свойствам производится с помощью точки и операторов [index].</span><span class="sxs-lookup"><span data-stu-id="c7e10-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="c7e10-147">Вот пример использования нескольких функций во время создания значений.</span><span class="sxs-lookup"><span data-stu-id="c7e10-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="c7e10-148">Полный список функций шаблонов см. в статье [Функции шаблонов диспетчера ресурсов Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="c7e10-149">Параметры</span><span class="sxs-lookup"><span data-stu-id="c7e10-149">Parameters</span></span>
<span data-ttu-id="c7e10-150">В разделе параметров шаблона указываются значения, которые вы можете вводить во время развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e10-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="c7e10-151">Значения этих параметров позволяют настраивать развертывание путем предоставления значений, предназначенных для конкретной среды (например, для среды разработки, тестирования и рабочей среды).</span><span class="sxs-lookup"><span data-stu-id="c7e10-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="c7e10-152">Предоставление параметров в шаблоне не является обязательным требованием, однако без параметров шаблон всегда будет развертывать одни и те же ресурсы с одинаковыми именами, расположениями и свойствами.</span><span class="sxs-lookup"><span data-stu-id="c7e10-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="c7e10-153">Параметры определяются с помощью следующей структуры.</span><span class="sxs-lookup"><span data-stu-id="c7e10-153">You define parameters with the following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="c7e10-154">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c7e10-154">Element name</span></span> | <span data-ttu-id="c7e10-155">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c7e10-155">Required</span></span> | <span data-ttu-id="c7e10-156">Описание</span><span class="sxs-lookup"><span data-stu-id="c7e10-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c7e10-157">имя_параметра</span><span class="sxs-lookup"><span data-stu-id="c7e10-157">parameterName</span></span> |<span data-ttu-id="c7e10-158">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-158">Yes</span></span> |<span data-ttu-id="c7e10-159">Имя параметра.</span><span class="sxs-lookup"><span data-stu-id="c7e10-159">Name of the parameter.</span></span> <span data-ttu-id="c7e10-160">Должно быть допустимым идентификатором JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c7e10-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="c7e10-161">type</span><span class="sxs-lookup"><span data-stu-id="c7e10-161">type</span></span> |<span data-ttu-id="c7e10-162">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-162">Yes</span></span> |<span data-ttu-id="c7e10-163">Тип значения параметра.</span><span class="sxs-lookup"><span data-stu-id="c7e10-163">Type of the parameter value.</span></span> <span data-ttu-id="c7e10-164">Ознакомьтесь со списком допустимых типов после данной таблицы.</span><span class="sxs-lookup"><span data-stu-id="c7e10-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="c7e10-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="c7e10-165">defaultValue</span></span> |<span data-ttu-id="c7e10-166">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-166">No</span></span> |<span data-ttu-id="c7e10-167">Значение параметра, используемое по умолчанию, если пользователь не задал иное значение.</span><span class="sxs-lookup"><span data-stu-id="c7e10-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="c7e10-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="c7e10-168">allowedValues</span></span> |<span data-ttu-id="c7e10-169">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-169">No</span></span> |<span data-ttu-id="c7e10-170">Массив допустимых значений параметра, по которому сверяются правильные значения.</span><span class="sxs-lookup"><span data-stu-id="c7e10-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="c7e10-171">minValue</span><span class="sxs-lookup"><span data-stu-id="c7e10-171">minValue</span></span> |<span data-ttu-id="c7e10-172">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-172">No</span></span> |<span data-ttu-id="c7e10-173">Минимальное значение для параметров типа int. Это включающее значение.</span><span class="sxs-lookup"><span data-stu-id="c7e10-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="c7e10-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="c7e10-174">maxValue</span></span> |<span data-ttu-id="c7e10-175">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-175">No</span></span> |<span data-ttu-id="c7e10-176">Максимальное значение для параметров типа int. Это включающее значение.</span><span class="sxs-lookup"><span data-stu-id="c7e10-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="c7e10-177">minLength</span><span class="sxs-lookup"><span data-stu-id="c7e10-177">minLength</span></span> |<span data-ttu-id="c7e10-178">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-178">No</span></span> |<span data-ttu-id="c7e10-179">Минимальная длина параметров типа string, secureString и array. Это включающее значение.</span><span class="sxs-lookup"><span data-stu-id="c7e10-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="c7e10-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="c7e10-180">maxLength</span></span> |<span data-ttu-id="c7e10-181">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-181">No</span></span> |<span data-ttu-id="c7e10-182">Максимальная длина параметров типа string, secureString и array. Это включающее значение.</span><span class="sxs-lookup"><span data-stu-id="c7e10-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="c7e10-183">Описание</span><span class="sxs-lookup"><span data-stu-id="c7e10-183">description</span></span> |<span data-ttu-id="c7e10-184">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-184">No</span></span> |<span data-ttu-id="c7e10-185">Описание параметра, отображаемого для пользователей на портале.</span><span class="sxs-lookup"><span data-stu-id="c7e10-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="c7e10-186">Допустимые типы и значения:</span><span class="sxs-lookup"><span data-stu-id="c7e10-186">The allowed types and values are:</span></span>

* <span data-ttu-id="c7e10-187">**string**</span><span class="sxs-lookup"><span data-stu-id="c7e10-187">**string**</span></span>
* <span data-ttu-id="c7e10-188">**secureString**;</span><span class="sxs-lookup"><span data-stu-id="c7e10-188">**secureString**</span></span>
* <span data-ttu-id="c7e10-189">**int**</span><span class="sxs-lookup"><span data-stu-id="c7e10-189">**int**</span></span>
* <span data-ttu-id="c7e10-190">**bool**;</span><span class="sxs-lookup"><span data-stu-id="c7e10-190">**bool**</span></span>
* <span data-ttu-id="c7e10-191">**object**;</span><span class="sxs-lookup"><span data-stu-id="c7e10-191">**object**</span></span> 
* <span data-ttu-id="c7e10-192">**secureObject**;</span><span class="sxs-lookup"><span data-stu-id="c7e10-192">**secureObject**</span></span>
* <span data-ttu-id="c7e10-193">**array**.</span><span class="sxs-lookup"><span data-stu-id="c7e10-193">**array**</span></span>

<span data-ttu-id="c7e10-194">Чтобы указать параметр как необязательный, задайте defaultValue (это может быть пустая строка).</span><span class="sxs-lookup"><span data-stu-id="c7e10-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="c7e10-195">Если указать в шаблоне имя параметра, которое совпадает с параметром в команде развертывания шаблона, то возникнет потенциальная неоднозначность заданных значений.</span><span class="sxs-lookup"><span data-stu-id="c7e10-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="c7e10-196">Resource Manager устраняет эту путаницу, добавляя постфикс **FromTemplate** к параметру шаблона.</span><span class="sxs-lookup"><span data-stu-id="c7e10-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="c7e10-197">Предположим, вы добавили в шаблон параметр **ResourceGroupName**, и он конфликтует с параметром **ResourceGroupName** в командлете [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="c7e10-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="c7e10-198">При развертывании вам будет предложено указать значение для параметра **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="c7e10-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="c7e10-199">В общем случае следует избегать этой путаницы, не присваивая параметрам имена параметров, используемых для операций развертывания.</span><span class="sxs-lookup"><span data-stu-id="c7e10-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="c7e10-200">Все пароли, ключи и другие секреты данные должны использовать тип **secureString** .</span><span class="sxs-lookup"><span data-stu-id="c7e10-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="c7e10-201">При передаче конфиденциальных данных в объекте JSON используйте тип **secureObject**.</span><span class="sxs-lookup"><span data-stu-id="c7e10-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="c7e10-202">Параметры шаблона с типами secureString и secureObject невозможно прочитать после развертывания ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="c7e10-203">Например, следующая запись в журнале развертывания содержит значения для строки и объекта, но не содержит значений для secureString и secureObject.</span><span class="sxs-lookup"><span data-stu-id="c7e10-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![показать значения развертывания](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="c7e10-205">В следующем примере показано, как определять параметры.</span><span class="sxs-lookup"><span data-stu-id="c7e10-205">The following example shows how to define parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="c7e10-206">Сведения о том, как вводить значения параметров во время развертывания, см. в статье [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="c7e10-207">Переменные</span><span class="sxs-lookup"><span data-stu-id="c7e10-207">Variables</span></span>
<span data-ttu-id="c7e10-208">В разделе переменных вы создаете значения, которые можно использовать в разных частях шаблона.</span><span class="sxs-lookup"><span data-stu-id="c7e10-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="c7e10-209">Переменные определять не обязательно, однако они часто упрощают шаблон, снижая число сложных выражений.</span><span class="sxs-lookup"><span data-stu-id="c7e10-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="c7e10-210">Переменные определяются с помощью следующей структуры:</span><span class="sxs-lookup"><span data-stu-id="c7e10-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="c7e10-211">В следующем примере показано, как определить переменную, которая состоит из двух значений параметра.</span><span class="sxs-lookup"><span data-stu-id="c7e10-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="c7e10-212">В следующем примере показана переменная, которая является сложным типом JSON, и переменные, построенные на основе других переменных.</span><span class="sxs-lookup"><span data-stu-id="c7e10-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="c7e10-213">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="c7e10-213">Resources</span></span>
<span data-ttu-id="c7e10-214">В разделе resources определяются ресурсы, которые развертываются или обновляются.</span><span class="sxs-lookup"><span data-stu-id="c7e10-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="c7e10-215">Этот раздел может еще больше усложниться, так как вы должны понимать принципы работы развертываемых типов для предоставления правильных значений.</span><span class="sxs-lookup"><span data-stu-id="c7e10-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="c7e10-216">Сведения о конкретных значениях ресурсов (apiVersion, тип и свойства), которые необходимо задать, см. в разделе [Define resources in Azure Resource Manager templates](/azure/templates/) (Определение ресурсов в шаблонах Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="c7e10-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="c7e10-217">Ресурсы определяются с помощью следующей структуры:</span><span class="sxs-lookup"><span data-stu-id="c7e10-217">You define resources with the following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="c7e10-218">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c7e10-218">Element name</span></span> | <span data-ttu-id="c7e10-219">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c7e10-219">Required</span></span> | <span data-ttu-id="c7e10-220">Описание</span><span class="sxs-lookup"><span data-stu-id="c7e10-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c7e10-221">condition</span><span class="sxs-lookup"><span data-stu-id="c7e10-221">condition</span></span> | <span data-ttu-id="c7e10-222">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-222">No</span></span> | <span data-ttu-id="c7e10-223">Логическое значение, указывающее, развернут ли ресурс.</span><span class="sxs-lookup"><span data-stu-id="c7e10-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="c7e10-224">версия_API</span><span class="sxs-lookup"><span data-stu-id="c7e10-224">apiVersion</span></span> |<span data-ttu-id="c7e10-225">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-225">Yes</span></span> |<span data-ttu-id="c7e10-226">Версия REST API, которая будет использована для создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="c7e10-227">type</span><span class="sxs-lookup"><span data-stu-id="c7e10-227">type</span></span> |<span data-ttu-id="c7e10-228">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-228">Yes</span></span> |<span data-ttu-id="c7e10-229">Тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-229">Type of the resource.</span></span> <span data-ttu-id="c7e10-230">Это значение представляет собой сочетание пространства имен поставщика ресурсов и типа ресурса (например, **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="c7e10-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="c7e10-231">name</span><span class="sxs-lookup"><span data-stu-id="c7e10-231">name</span></span> |<span data-ttu-id="c7e10-232">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-232">Yes</span></span> |<span data-ttu-id="c7e10-233">Имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-233">Name of the resource.</span></span> <span data-ttu-id="c7e10-234">Имя должно соответствовать ограничениям компонентов URI, определенным в RFC3986.</span><span class="sxs-lookup"><span data-stu-id="c7e10-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="c7e10-235">Кроме того, службы Azure, которые предоставляют имя ресурса внешним пользователям, проверяют это имя, чтобы убедиться, что это не попытка подделки другого удостоверения.</span><span class="sxs-lookup"><span data-stu-id="c7e10-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="c7e10-236">location</span><span class="sxs-lookup"><span data-stu-id="c7e10-236">location</span></span> |<span data-ttu-id="c7e10-237">Varies</span><span class="sxs-lookup"><span data-stu-id="c7e10-237">Varies</span></span> |<span data-ttu-id="c7e10-238">Поддерживаемые географические расположения указанного ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="c7e10-239">Вы можете выбрать любое из доступных расположений. Но обычно имеет смысл выбрать расположение, которое находится недалеко от пользователей.</span><span class="sxs-lookup"><span data-stu-id="c7e10-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="c7e10-240">Кроме того, целесообразно разместить взаимодействующие ресурсы в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="c7e10-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="c7e10-241">Большинству типов ресурсов нужно расположение, но некоторым типам (например, назначению роли) оно не требуется.</span><span class="sxs-lookup"><span data-stu-id="c7e10-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="c7e10-242">Ознакомьтесь с разделом [Определение расположения ресурса в шаблонах Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="c7e10-243">tags</span><span class="sxs-lookup"><span data-stu-id="c7e10-243">tags</span></span> |<span data-ttu-id="c7e10-244">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-244">No</span></span> |<span data-ttu-id="c7e10-245">Теги, связанные с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="c7e10-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="c7e10-246">Ознакомьтесь с разделом [Присвоение тегов ресурсам в шаблоне Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="c7e10-247">комментарии</span><span class="sxs-lookup"><span data-stu-id="c7e10-247">comments</span></span> |<span data-ttu-id="c7e10-248">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-248">No</span></span> |<span data-ttu-id="c7e10-249">Заметки по ресурсам в шаблоне</span><span class="sxs-lookup"><span data-stu-id="c7e10-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="c7e10-250">копирование</span><span class="sxs-lookup"><span data-stu-id="c7e10-250">copy</span></span> |<span data-ttu-id="c7e10-251">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-251">No</span></span> |<span data-ttu-id="c7e10-252">Количество создаваемых ресурсов (если нужно несколько экземпляров).</span><span class="sxs-lookup"><span data-stu-id="c7e10-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="c7e10-253">Параллельный режим используется по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c7e10-253">The default mode is parallel.</span></span> <span data-ttu-id="c7e10-254">Используйте последовательный режим, если вы не хотите развертывать все ресурсы одновременно.</span><span class="sxs-lookup"><span data-stu-id="c7e10-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="c7e10-255">Дополнительные сведения см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="c7e10-256">Свойство dependsOn</span><span class="sxs-lookup"><span data-stu-id="c7e10-256">dependsOn</span></span> |<span data-ttu-id="c7e10-257">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-257">No</span></span> |<span data-ttu-id="c7e10-258">Ресурсы, которые должны быть развернуты перед развертыванием этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="c7e10-259">Resource Manager оценивает зависимости между ресурсами и развертывает эти ресурсы в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="c7e10-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="c7e10-260">Если ресурсы не зависят друг от друга, они развертываются параллельно.</span><span class="sxs-lookup"><span data-stu-id="c7e10-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="c7e10-261">Значение может представлять собой разделенный запятыми список имен ресурсов или уникальных идентификаторов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e10-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="c7e10-262">Выводится только список ресурсов, развертываемых в этом шаблоне.</span><span class="sxs-lookup"><span data-stu-id="c7e10-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="c7e10-263">Ресурсы, которые не определены в этом шаблоне, уже должны существовать.</span><span class="sxs-lookup"><span data-stu-id="c7e10-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="c7e10-264">Избегайте добавления ненужных зависимостей, так как это может замедлить развертывание и привести к созданию циклических зависимостей.</span><span class="sxs-lookup"><span data-stu-id="c7e10-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="c7e10-265">Рекомендации по настройке зависимостей см. в статье [Определение зависимостей в шаблонах диспетчера ресурсов Azure](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="c7e10-266">properties</span><span class="sxs-lookup"><span data-stu-id="c7e10-266">properties</span></span> |<span data-ttu-id="c7e10-267">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-267">No</span></span> |<span data-ttu-id="c7e10-268">Параметры конфигурации ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="c7e10-269">Значения свойств совпадают со значениями, указываемыми в тексте запроса для операции REST API (метод PUT) для создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="c7e10-270">Кроме того, можно указать массив copy для создания нескольких экземпляров свойства.</span><span class="sxs-lookup"><span data-stu-id="c7e10-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="c7e10-271">Дополнительные сведения см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="c7e10-272">ресурсов</span><span class="sxs-lookup"><span data-stu-id="c7e10-272">resources</span></span> |<span data-ttu-id="c7e10-273">Нет</span><span class="sxs-lookup"><span data-stu-id="c7e10-273">No</span></span> |<span data-ttu-id="c7e10-274">Дочерние ресурсы, которые зависят от определяемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="c7e10-275">Следует указать только те типы ресурсов, которые разрешены в схеме родительского ресурса.</span><span class="sxs-lookup"><span data-stu-id="c7e10-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="c7e10-276">Полное имя типа дочернего ресурса содержит тип родительского ресурса, например **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="c7e10-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="c7e10-277">Зависимость от родительского ресурса не подразумевается.</span><span class="sxs-lookup"><span data-stu-id="c7e10-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="c7e10-278">Ее необходимо определить явным образом.</span><span class="sxs-lookup"><span data-stu-id="c7e10-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="c7e10-279">Раздел ресурсов содержит набор ресурсов для развертывания.</span><span class="sxs-lookup"><span data-stu-id="c7e10-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="c7e10-280">Внутри каждого ресурса можно также определить набор дочерних ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e10-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="c7e10-281">Таким образом раздел ресурсов может иметь примерно следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="c7e10-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="c7e10-282">Дополнительные сведения об определении дочерних ресурсов см. в разделе [Указание имени и типа дочернего ресурса в шаблоне Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="c7e10-283">Элемент **condition** определяет, развернут ли ресурс.</span><span class="sxs-lookup"><span data-stu-id="c7e10-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="c7e10-284">Этот элемент возвращает значение True или False.</span><span class="sxs-lookup"><span data-stu-id="c7e10-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="c7e10-285">Используйте следующую команду, чтобы указать, развернута ли новая учетная запись хранения :</span><span class="sxs-lookup"><span data-stu-id="c7e10-285">For example, to specify whether a new storage account is deployed, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="c7e10-286">Пример использования нового или имеющегося шаблона условий см. [здесь](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="c7e10-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="c7e10-287">Чтобы указать, что использовалось для развертывания виртуальной машины (пароль или ключ SSH), определите две версии виртуальной машины в шаблоне и используйте свойство **condition** для разделения случаев использования.</span><span class="sxs-lookup"><span data-stu-id="c7e10-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="c7e10-288">Передайте параметр, указывающий сценарий для развертывания.</span><span class="sxs-lookup"><span data-stu-id="c7e10-288">Pass a parameter that specifies which scenario to deploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="c7e10-289">Пример использования пароля или ключа SSH для развертывания виртуальной машины см. в [шаблоне имени пользователя или условия SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="c7e10-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="c7e10-290">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="c7e10-290">Outputs</span></span>
<span data-ttu-id="c7e10-291">В разделе выходных данных следует указать значения, которые возвращаются после развертывания.</span><span class="sxs-lookup"><span data-stu-id="c7e10-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="c7e10-292">Например, можно возвращать URI для доступа к развернутому ресурсу.</span><span class="sxs-lookup"><span data-stu-id="c7e10-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="c7e10-293">В следующем примере показана структура определения выходных данных:</span><span class="sxs-lookup"><span data-stu-id="c7e10-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="c7e10-294">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="c7e10-294">Element name</span></span> | <span data-ttu-id="c7e10-295">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c7e10-295">Required</span></span> | <span data-ttu-id="c7e10-296">Описание</span><span class="sxs-lookup"><span data-stu-id="c7e10-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c7e10-297">outputName</span><span class="sxs-lookup"><span data-stu-id="c7e10-297">outputName</span></span> |<span data-ttu-id="c7e10-298">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-298">Yes</span></span> |<span data-ttu-id="c7e10-299">Имя выходного значения.</span><span class="sxs-lookup"><span data-stu-id="c7e10-299">Name of the output value.</span></span> <span data-ttu-id="c7e10-300">Должно быть допустимым идентификатором JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c7e10-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="c7e10-301">type</span><span class="sxs-lookup"><span data-stu-id="c7e10-301">type</span></span> |<span data-ttu-id="c7e10-302">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-302">Yes</span></span> |<span data-ttu-id="c7e10-303">Тип выходного значения.</span><span class="sxs-lookup"><span data-stu-id="c7e10-303">Type of the output value.</span></span> <span data-ttu-id="c7e10-304">Выходные значения поддерживает те же типы, что и входные параметры шаблона.</span><span class="sxs-lookup"><span data-stu-id="c7e10-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="c7e10-305">value</span><span class="sxs-lookup"><span data-stu-id="c7e10-305">value</span></span> |<span data-ttu-id="c7e10-306">Да</span><span class="sxs-lookup"><span data-stu-id="c7e10-306">Yes</span></span> |<span data-ttu-id="c7e10-307">Выражение на языке шаблона, которое вычисляется и возвращается в качестве выходного значения.</span><span class="sxs-lookup"><span data-stu-id="c7e10-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="c7e10-308">В следующем примере показано значение, которое возвращается в разделе выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c7e10-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="c7e10-309">Дополнительные сведения о работе с выходными данными см. в статье [Совместное использование состояния в шаблонах Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="c7e10-310">Ограничения шаблонов</span><span class="sxs-lookup"><span data-stu-id="c7e10-310">Template limits</span></span>

<span data-ttu-id="c7e10-311">Задайте максимальный размер шаблона, равный 1 МБ, а максимальный размер каждого файла параметров — 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="c7e10-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="c7e10-312">Ограничение в 1 МБ применяется к конечному состоянию шаблона после расширения с использованием итеративных определений ресурсов, а также значений переменных и параметров.</span><span class="sxs-lookup"><span data-stu-id="c7e10-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="c7e10-313">Кроме того, ограничение распространяется на:</span><span class="sxs-lookup"><span data-stu-id="c7e10-313">You are also limited to:</span></span>

* <span data-ttu-id="c7e10-314">256 параметров;</span><span class="sxs-lookup"><span data-stu-id="c7e10-314">256 parameters</span></span>
* <span data-ttu-id="c7e10-315">256 переменных;</span><span class="sxs-lookup"><span data-stu-id="c7e10-315">256 variables</span></span>
* <span data-ttu-id="c7e10-316">800 ресурсов (включая число копий);</span><span class="sxs-lookup"><span data-stu-id="c7e10-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="c7e10-317">64 выходных значения;</span><span class="sxs-lookup"><span data-stu-id="c7e10-317">64 output values</span></span>
* <span data-ttu-id="c7e10-318">24 576 знаков в выражении шаблона.</span><span class="sxs-lookup"><span data-stu-id="c7e10-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="c7e10-319">Некоторые ограничения можно превысить, используя вложенные шаблоны.</span><span class="sxs-lookup"><span data-stu-id="c7e10-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="c7e10-320">Дополнительные сведения см. разделе [Использование связанных шаблонов в при развертывании ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="c7e10-321">Чтобы уменьшить число параметров, переменных или выходных данных, можно объединить несколько значений в объект.</span><span class="sxs-lookup"><span data-stu-id="c7e10-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="c7e10-322">См. дополнительные сведения об [использовании объектов как параметров](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7e10-323">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7e10-323">Next steps</span></span>
* <span data-ttu-id="c7e10-324">Полные шаблоны для различных типов решений доступны на странице [Шаблоны быстрого запуска Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="c7e10-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="c7e10-325">Дополнительные сведения о функциях, которые можно использовать в шаблонах, см. в статье [Функции шаблонов Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="c7e10-326">Инструкции по объединению нескольких шаблонов при развертывании см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c7e10-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="c7e10-327">Может потребоваться использовать ресурсы, которые существуют в другой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e10-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="c7e10-328">Это распространенная ситуация при работе с учетными записями хранения или виртуальными сетями, которые совместно используются в нескольких группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c7e10-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="c7e10-329">Дополнительные сведения см. в описании [функции resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="c7e10-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
