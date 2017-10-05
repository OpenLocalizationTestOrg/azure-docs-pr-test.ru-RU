---
title: "Логические функции шаблона Azure Resource Manager | Документация Майкрософт"
description: "Описываются функции, используемые в шаблоне Azure Resource Manager для определения логических значений."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: 313601ad99cdc12c4b50f5469959d37a9fa70d35
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="663a2-103">Логические функции для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="663a2-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="663a2-104">Resource Manager предоставляет ряд функций для выполнения сравнений в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="663a2-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* <span data-ttu-id="663a2-105">[and](#and) (и);</span><span class="sxs-lookup"><span data-stu-id="663a2-105">[and](#and)</span></span>
* <span data-ttu-id="663a2-106">[bool](#bool);</span><span class="sxs-lookup"><span data-stu-id="663a2-106">[bool](#bool)</span></span>
* <span data-ttu-id="663a2-107">[if](#if) (если);</span><span class="sxs-lookup"><span data-stu-id="663a2-107">[if](#if)</span></span>
* <span data-ttu-id="663a2-108">[not](#not) (не);</span><span class="sxs-lookup"><span data-stu-id="663a2-108">[not](#not)</span></span>
* <span data-ttu-id="663a2-109">[or](#or) (или).</span><span class="sxs-lookup"><span data-stu-id="663a2-109">[or](#or)</span></span>

## <a name="and"></a><span data-ttu-id="663a2-110">и</span><span class="sxs-lookup"><span data-stu-id="663a2-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="663a2-111">Проверяет, соответствуют ли истине два значения параметров.</span><span class="sxs-lookup"><span data-stu-id="663a2-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="663a2-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="663a2-112">Parameters</span></span>

| <span data-ttu-id="663a2-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="663a2-113">Parameter</span></span> | <span data-ttu-id="663a2-114">Обязательно</span><span class="sxs-lookup"><span data-stu-id="663a2-114">Required</span></span> | <span data-ttu-id="663a2-115">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-115">Type</span></span> | <span data-ttu-id="663a2-116">Описание</span><span class="sxs-lookup"><span data-stu-id="663a2-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="663a2-117">arg1</span><span class="sxs-lookup"><span data-stu-id="663a2-117">arg1</span></span> |<span data-ttu-id="663a2-118">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-118">Yes</span></span> |<span data-ttu-id="663a2-119">Логическое</span><span class="sxs-lookup"><span data-stu-id="663a2-119">boolean</span></span> |<span data-ttu-id="663a2-120">Первое значение, которое необходимо проверить на соответствие истине.</span><span class="sxs-lookup"><span data-stu-id="663a2-120">The first value to check whether is true.</span></span> |
| <span data-ttu-id="663a2-121">arg2</span><span class="sxs-lookup"><span data-stu-id="663a2-121">arg2</span></span> |<span data-ttu-id="663a2-122">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-122">Yes</span></span> |<span data-ttu-id="663a2-123">Логическое</span><span class="sxs-lookup"><span data-stu-id="663a2-123">boolean</span></span> |<span data-ttu-id="663a2-124">Второе значение, которое необходимо проверить на соответствие истине.</span><span class="sxs-lookup"><span data-stu-id="663a2-124">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="663a2-125">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="663a2-125">Return value</span></span>

<span data-ttu-id="663a2-126">Возвращает результат **True** (Истина), если оба значения соответствуют истине. В противном случае — **False** (Ложь).</span><span class="sxs-lookup"><span data-stu-id="663a2-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="663a2-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="663a2-127">Examples</span></span>

<span data-ttu-id="663a2-128">В следующем примере показано, как использовать логические функции.</span><span class="sxs-lookup"><span data-stu-id="663a2-128">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="663a2-129">Выходные данные из предыдущего примера:</span><span class="sxs-lookup"><span data-stu-id="663a2-129">The output from the preceding example is:</span></span>

| <span data-ttu-id="663a2-130">Имя</span><span class="sxs-lookup"><span data-stu-id="663a2-130">Name</span></span> | <span data-ttu-id="663a2-131">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-131">Type</span></span> | <span data-ttu-id="663a2-132">Значение</span><span class="sxs-lookup"><span data-stu-id="663a2-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="663a2-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-133">andExampleOutput</span></span> | <span data-ttu-id="663a2-134">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-134">Bool</span></span> | <span data-ttu-id="663a2-135">Ложь</span><span class="sxs-lookup"><span data-stu-id="663a2-135">False</span></span> |
| <span data-ttu-id="663a2-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-136">orExampleOutput</span></span> | <span data-ttu-id="663a2-137">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-137">Bool</span></span> | <span data-ttu-id="663a2-138">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-138">True</span></span> |
| <span data-ttu-id="663a2-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-139">notExampleOutput</span></span> | <span data-ttu-id="663a2-140">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-140">Bool</span></span> | <span data-ttu-id="663a2-141">Ложь</span><span class="sxs-lookup"><span data-stu-id="663a2-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="663a2-142">bool</span><span class="sxs-lookup"><span data-stu-id="663a2-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="663a2-143">Преобразует параметр в логическое значение.</span><span class="sxs-lookup"><span data-stu-id="663a2-143">Converts the parameter to a boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="663a2-144">Параметры</span><span class="sxs-lookup"><span data-stu-id="663a2-144">Parameters</span></span>

| <span data-ttu-id="663a2-145">Параметр</span><span class="sxs-lookup"><span data-stu-id="663a2-145">Parameter</span></span> | <span data-ttu-id="663a2-146">Обязательно</span><span class="sxs-lookup"><span data-stu-id="663a2-146">Required</span></span> | <span data-ttu-id="663a2-147">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-147">Type</span></span> | <span data-ttu-id="663a2-148">Описание</span><span class="sxs-lookup"><span data-stu-id="663a2-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="663a2-149">arg1</span><span class="sxs-lookup"><span data-stu-id="663a2-149">arg1</span></span> |<span data-ttu-id="663a2-150">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-150">Yes</span></span> |<span data-ttu-id="663a2-151">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="663a2-151">string or int</span></span> |<span data-ttu-id="663a2-152">Значение, которое необходимо преобразовать в логическое.</span><span class="sxs-lookup"><span data-stu-id="663a2-152">The value to convert to a boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="663a2-153">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="663a2-153">Return value</span></span>
<span data-ttu-id="663a2-154">Логическое выражение преобразованного значения.</span><span class="sxs-lookup"><span data-stu-id="663a2-154">A boolean of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="663a2-155">Примеры</span><span class="sxs-lookup"><span data-stu-id="663a2-155">Examples</span></span>

<span data-ttu-id="663a2-156">В следующем примере показано, как использовать функцию bool со строкой или целым числом:</span><span class="sxs-lookup"><span data-stu-id="663a2-156">The following example shows how to use bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="663a2-157">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="663a2-157">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="663a2-158">Имя</span><span class="sxs-lookup"><span data-stu-id="663a2-158">Name</span></span> | <span data-ttu-id="663a2-159">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-159">Type</span></span> | <span data-ttu-id="663a2-160">Значение</span><span class="sxs-lookup"><span data-stu-id="663a2-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="663a2-161">trueString</span><span class="sxs-lookup"><span data-stu-id="663a2-161">trueString</span></span> | <span data-ttu-id="663a2-162">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-162">Bool</span></span> | <span data-ttu-id="663a2-163">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-163">True</span></span> |
| <span data-ttu-id="663a2-164">falseString</span><span class="sxs-lookup"><span data-stu-id="663a2-164">falseString</span></span> | <span data-ttu-id="663a2-165">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-165">Bool</span></span> | <span data-ttu-id="663a2-166">Ложь</span><span class="sxs-lookup"><span data-stu-id="663a2-166">False</span></span> |
| <span data-ttu-id="663a2-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="663a2-167">trueInt</span></span> | <span data-ttu-id="663a2-168">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-168">Bool</span></span> | <span data-ttu-id="663a2-169">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-169">True</span></span> |
| <span data-ttu-id="663a2-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="663a2-170">falseInt</span></span> | <span data-ttu-id="663a2-171">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-171">Bool</span></span> | <span data-ttu-id="663a2-172">Ложь</span><span class="sxs-lookup"><span data-stu-id="663a2-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="663a2-173">if</span><span class="sxs-lookup"><span data-stu-id="663a2-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="663a2-174">Возвращает значение в зависимости от того, выполняется ли условие.</span><span class="sxs-lookup"><span data-stu-id="663a2-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="663a2-175">Параметры</span><span class="sxs-lookup"><span data-stu-id="663a2-175">Parameters</span></span>

| <span data-ttu-id="663a2-176">Параметр</span><span class="sxs-lookup"><span data-stu-id="663a2-176">Parameter</span></span> | <span data-ttu-id="663a2-177">Обязательно</span><span class="sxs-lookup"><span data-stu-id="663a2-177">Required</span></span> | <span data-ttu-id="663a2-178">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-178">Type</span></span> | <span data-ttu-id="663a2-179">Описание</span><span class="sxs-lookup"><span data-stu-id="663a2-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="663a2-180">condition</span><span class="sxs-lookup"><span data-stu-id="663a2-180">condition</span></span> |<span data-ttu-id="663a2-181">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-181">Yes</span></span> |<span data-ttu-id="663a2-182">Логическое</span><span class="sxs-lookup"><span data-stu-id="663a2-182">boolean</span></span> |<span data-ttu-id="663a2-183">Значение, которое необходимо проверить на соответствие истине.</span><span class="sxs-lookup"><span data-stu-id="663a2-183">The value to check whether it is true.</span></span> |
| <span data-ttu-id="663a2-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="663a2-184">trueValue</span></span> |<span data-ttu-id="663a2-185">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-185">Yes</span></span> | <span data-ttu-id="663a2-186">строка, целое число, объект или массив</span><span class="sxs-lookup"><span data-stu-id="663a2-186">string, int, object, or array</span></span> |<span data-ttu-id="663a2-187">Возвращаемое значение, если условие выполняется.</span><span class="sxs-lookup"><span data-stu-id="663a2-187">The value to return when the condition is true.</span></span> |
| <span data-ttu-id="663a2-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="663a2-188">falseValue</span></span> |<span data-ttu-id="663a2-189">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-189">Yes</span></span> | <span data-ttu-id="663a2-190">строка, целое число, объект или массив</span><span class="sxs-lookup"><span data-stu-id="663a2-190">string, int, object, or array</span></span> |<span data-ttu-id="663a2-191">Возвращаемое значение, если условие не выполняется.</span><span class="sxs-lookup"><span data-stu-id="663a2-191">The value to return when the condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="663a2-192">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="663a2-192">Return value</span></span>

<span data-ttu-id="663a2-193">Возвращает второй параметр, если первый параметр имеет значение **True** (Истина). В противном случае возвращает третий параметр.</span><span class="sxs-lookup"><span data-stu-id="663a2-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="663a2-194">Примечания</span><span class="sxs-lookup"><span data-stu-id="663a2-194">Remarks</span></span>

<span data-ttu-id="663a2-195">Эту функцию можно использовать, чтобы условно задавать свойство ресурса.</span><span class="sxs-lookup"><span data-stu-id="663a2-195">You can use this function to conditionally set a resource property.</span></span> <span data-ttu-id="663a2-196">Следующий пример не является полным шаблоном, но в нем показаны соответствующие части для условной настройки группы доступности.</span><span class="sxs-lookup"><span data-stu-id="663a2-196">The following example is not a full template, but it shows the relevant portions for conditionally setting the availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="663a2-197">Примеры</span><span class="sxs-lookup"><span data-stu-id="663a2-197">Examples</span></span>

<span data-ttu-id="663a2-198">Ниже представлен пример использования функции `if`.</span><span class="sxs-lookup"><span data-stu-id="663a2-198">The following example shows how to use the `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="663a2-199">Выходные данные из предыдущего примера:</span><span class="sxs-lookup"><span data-stu-id="663a2-199">The output from the preceding example is:</span></span>

| <span data-ttu-id="663a2-200">Имя</span><span class="sxs-lookup"><span data-stu-id="663a2-200">Name</span></span> | <span data-ttu-id="663a2-201">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-201">Type</span></span> | <span data-ttu-id="663a2-202">Значение</span><span class="sxs-lookup"><span data-stu-id="663a2-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="663a2-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-203">yesOutput</span></span> | <span data-ttu-id="663a2-204">Строка</span><span class="sxs-lookup"><span data-stu-id="663a2-204">String</span></span> | <span data-ttu-id="663a2-205">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-205">yes</span></span> |
| <span data-ttu-id="663a2-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-206">noOutput</span></span> | <span data-ttu-id="663a2-207">Строка</span><span class="sxs-lookup"><span data-stu-id="663a2-207">String</span></span> | <span data-ttu-id="663a2-208">Нет</span><span class="sxs-lookup"><span data-stu-id="663a2-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="663a2-209">not</span><span class="sxs-lookup"><span data-stu-id="663a2-209">not</span></span>
`not(arg1)`

<span data-ttu-id="663a2-210">Преобразует логическое значение в противоположное ему значение.</span><span class="sxs-lookup"><span data-stu-id="663a2-210">Converts boolean value to its opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="663a2-211">Параметры</span><span class="sxs-lookup"><span data-stu-id="663a2-211">Parameters</span></span>

| <span data-ttu-id="663a2-212">Параметр</span><span class="sxs-lookup"><span data-stu-id="663a2-212">Parameter</span></span> | <span data-ttu-id="663a2-213">Обязательно</span><span class="sxs-lookup"><span data-stu-id="663a2-213">Required</span></span> | <span data-ttu-id="663a2-214">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-214">Type</span></span> | <span data-ttu-id="663a2-215">Описание</span><span class="sxs-lookup"><span data-stu-id="663a2-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="663a2-216">arg1</span><span class="sxs-lookup"><span data-stu-id="663a2-216">arg1</span></span> |<span data-ttu-id="663a2-217">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-217">Yes</span></span> |<span data-ttu-id="663a2-218">Логическое</span><span class="sxs-lookup"><span data-stu-id="663a2-218">boolean</span></span> |<span data-ttu-id="663a2-219">Значение, которое необходимо преобразовать.</span><span class="sxs-lookup"><span data-stu-id="663a2-219">The value to convert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="663a2-220">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="663a2-220">Return value</span></span>

<span data-ttu-id="663a2-221">Возвращает значение **True** (Истина), если параметр имеет значение **False** (Ложь).</span><span class="sxs-lookup"><span data-stu-id="663a2-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="663a2-222">Возвращает значение **False** (Ложь), если параметр имеет значение **True** (Истина).</span><span class="sxs-lookup"><span data-stu-id="663a2-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="663a2-223">Примеры</span><span class="sxs-lookup"><span data-stu-id="663a2-223">Examples</span></span>

<span data-ttu-id="663a2-224">В следующем примере показано, как использовать логические функции.</span><span class="sxs-lookup"><span data-stu-id="663a2-224">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="663a2-225">Выходные данные из предыдущего примера:</span><span class="sxs-lookup"><span data-stu-id="663a2-225">The output from the preceding example is:</span></span>

| <span data-ttu-id="663a2-226">Имя</span><span class="sxs-lookup"><span data-stu-id="663a2-226">Name</span></span> | <span data-ttu-id="663a2-227">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-227">Type</span></span> | <span data-ttu-id="663a2-228">Значение</span><span class="sxs-lookup"><span data-stu-id="663a2-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="663a2-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-229">andExampleOutput</span></span> | <span data-ttu-id="663a2-230">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-230">Bool</span></span> | <span data-ttu-id="663a2-231">Ложь</span><span class="sxs-lookup"><span data-stu-id="663a2-231">False</span></span> |
| <span data-ttu-id="663a2-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-232">orExampleOutput</span></span> | <span data-ttu-id="663a2-233">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-233">Bool</span></span> | <span data-ttu-id="663a2-234">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-234">True</span></span> |
| <span data-ttu-id="663a2-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-235">notExampleOutput</span></span> | <span data-ttu-id="663a2-236">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-236">Bool</span></span> | <span data-ttu-id="663a2-237">Ложь</span><span class="sxs-lookup"><span data-stu-id="663a2-237">False</span></span> |

<span data-ttu-id="663a2-238">В следующем примере используется функция **not** (не) с [equals](resource-group-template-functions-comparison.md#equals) (равно).</span><span class="sxs-lookup"><span data-stu-id="663a2-238">The following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="663a2-239">Выходные данные из предыдущего примера:</span><span class="sxs-lookup"><span data-stu-id="663a2-239">The output from the preceding example is:</span></span>

| <span data-ttu-id="663a2-240">Имя</span><span class="sxs-lookup"><span data-stu-id="663a2-240">Name</span></span> | <span data-ttu-id="663a2-241">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-241">Type</span></span> | <span data-ttu-id="663a2-242">Значение</span><span class="sxs-lookup"><span data-stu-id="663a2-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="663a2-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="663a2-243">checkNotEquals</span></span> | <span data-ttu-id="663a2-244">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-244">Bool</span></span> | <span data-ttu-id="663a2-245">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="663a2-246">или</span><span class="sxs-lookup"><span data-stu-id="663a2-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="663a2-247">Проверяет, соответствует ли истине одно из значений параметров.</span><span class="sxs-lookup"><span data-stu-id="663a2-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="663a2-248">Параметры</span><span class="sxs-lookup"><span data-stu-id="663a2-248">Parameters</span></span>

| <span data-ttu-id="663a2-249">Параметр</span><span class="sxs-lookup"><span data-stu-id="663a2-249">Parameter</span></span> | <span data-ttu-id="663a2-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="663a2-250">Required</span></span> | <span data-ttu-id="663a2-251">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-251">Type</span></span> | <span data-ttu-id="663a2-252">Описание</span><span class="sxs-lookup"><span data-stu-id="663a2-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="663a2-253">arg1</span><span class="sxs-lookup"><span data-stu-id="663a2-253">arg1</span></span> |<span data-ttu-id="663a2-254">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-254">Yes</span></span> |<span data-ttu-id="663a2-255">Логическое</span><span class="sxs-lookup"><span data-stu-id="663a2-255">boolean</span></span> |<span data-ttu-id="663a2-256">Первое значение, которое необходимо проверить на соответствие истине.</span><span class="sxs-lookup"><span data-stu-id="663a2-256">The first value to check whether is true.</span></span> |
| <span data-ttu-id="663a2-257">arg2</span><span class="sxs-lookup"><span data-stu-id="663a2-257">arg2</span></span> |<span data-ttu-id="663a2-258">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-258">Yes</span></span> |<span data-ttu-id="663a2-259">Логическое</span><span class="sxs-lookup"><span data-stu-id="663a2-259">boolean</span></span> |<span data-ttu-id="663a2-260">Второе значение, которое необходимо проверить на соответствие истине.</span><span class="sxs-lookup"><span data-stu-id="663a2-260">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="663a2-261">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="663a2-261">Return value</span></span>

<span data-ttu-id="663a2-262">Возвращает результат **True** (Истина), если одно из значений соответствует истине. В противном случае — **False** (Ложь).</span><span class="sxs-lookup"><span data-stu-id="663a2-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="663a2-263">Примеры</span><span class="sxs-lookup"><span data-stu-id="663a2-263">Examples</span></span>

<span data-ttu-id="663a2-264">В следующем примере показано, как использовать логические функции.</span><span class="sxs-lookup"><span data-stu-id="663a2-264">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="663a2-265">Выходные данные из предыдущего примера:</span><span class="sxs-lookup"><span data-stu-id="663a2-265">The output from the preceding example is:</span></span>

| <span data-ttu-id="663a2-266">Имя</span><span class="sxs-lookup"><span data-stu-id="663a2-266">Name</span></span> | <span data-ttu-id="663a2-267">Тип</span><span class="sxs-lookup"><span data-stu-id="663a2-267">Type</span></span> | <span data-ttu-id="663a2-268">Значение</span><span class="sxs-lookup"><span data-stu-id="663a2-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="663a2-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-269">andExampleOutput</span></span> | <span data-ttu-id="663a2-270">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-270">Bool</span></span> | <span data-ttu-id="663a2-271">Ложь</span><span class="sxs-lookup"><span data-stu-id="663a2-271">False</span></span> |
| <span data-ttu-id="663a2-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-272">orExampleOutput</span></span> | <span data-ttu-id="663a2-273">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-273">Bool</span></span> | <span data-ttu-id="663a2-274">Да</span><span class="sxs-lookup"><span data-stu-id="663a2-274">True</span></span> |
| <span data-ttu-id="663a2-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="663a2-275">notExampleOutput</span></span> | <span data-ttu-id="663a2-276">Bool</span><span class="sxs-lookup"><span data-stu-id="663a2-276">Bool</span></span> | <span data-ttu-id="663a2-277">Ложь</span><span class="sxs-lookup"><span data-stu-id="663a2-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="663a2-278">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="663a2-278">Next steps</span></span>
* <span data-ttu-id="663a2-279">Описание разделов в шаблоне Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="663a2-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="663a2-280">Инструкции по объединению нескольких шаблонов см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="663a2-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="663a2-281">Указания по выполнению заданного количества циклов итерации при создании типа ресурса см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="663a2-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="663a2-282">Указания по развертыванию созданного шаблона см. в статье, посвященной [развертыванию приложения с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="663a2-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

