---
title: "aaaAzure диспетчер ресурсов шаблона функции - логических | Документы Microsoft"
description: "Описывает toouse функции hello в шаблона Azure Resource Manager toodetermine логические значения."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="8cccd-103">Логические функции для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8cccd-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="8cccd-104">Resource Manager предоставляет ряд функций для выполнения сравнений в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="8cccd-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* <span data-ttu-id="8cccd-105">[and](#and) (и);</span><span class="sxs-lookup"><span data-stu-id="8cccd-105">[and](#and)</span></span>
* <span data-ttu-id="8cccd-106">[bool](#bool);</span><span class="sxs-lookup"><span data-stu-id="8cccd-106">[bool](#bool)</span></span>
* <span data-ttu-id="8cccd-107">[if](#if) (если);</span><span class="sxs-lookup"><span data-stu-id="8cccd-107">[if](#if)</span></span>
* <span data-ttu-id="8cccd-108">[not](#not) (не);</span><span class="sxs-lookup"><span data-stu-id="8cccd-108">[not](#not)</span></span>
* <span data-ttu-id="8cccd-109">[or](#or) (или).</span><span class="sxs-lookup"><span data-stu-id="8cccd-109">[or](#or)</span></span>

## <a name="and"></a><span data-ttu-id="8cccd-110">и</span><span class="sxs-lookup"><span data-stu-id="8cccd-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="8cccd-111">Проверяет, соответствуют ли истине два значения параметров.</span><span class="sxs-lookup"><span data-stu-id="8cccd-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="8cccd-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="8cccd-112">Parameters</span></span>

| <span data-ttu-id="8cccd-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="8cccd-113">Parameter</span></span> | <span data-ttu-id="8cccd-114">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8cccd-114">Required</span></span> | <span data-ttu-id="8cccd-115">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-115">Type</span></span> | <span data-ttu-id="8cccd-116">Описание</span><span class="sxs-lookup"><span data-stu-id="8cccd-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8cccd-117">arg1</span><span class="sxs-lookup"><span data-stu-id="8cccd-117">arg1</span></span> |<span data-ttu-id="8cccd-118">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-118">Yes</span></span> |<span data-ttu-id="8cccd-119">Логическое</span><span class="sxs-lookup"><span data-stu-id="8cccd-119">boolean</span></span> |<span data-ttu-id="8cccd-120">Здравствуйте ли первый toocheck значение равно true.</span><span class="sxs-lookup"><span data-stu-id="8cccd-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="8cccd-121">arg2</span><span class="sxs-lookup"><span data-stu-id="8cccd-121">arg2</span></span> |<span data-ttu-id="8cccd-122">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-122">Yes</span></span> |<span data-ttu-id="8cccd-123">Логическое</span><span class="sxs-lookup"><span data-stu-id="8cccd-123">boolean</span></span> |<span data-ttu-id="8cccd-124">Hello ли toocheck второе значение — true.</span><span class="sxs-lookup"><span data-stu-id="8cccd-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="8cccd-125">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-125">Return value</span></span>

<span data-ttu-id="8cccd-126">Возвращает результат **True** (Истина), если оба значения соответствуют истине. В противном случае — **False** (Ложь).</span><span class="sxs-lookup"><span data-stu-id="8cccd-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="8cccd-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="8cccd-127">Examples</span></span>

<span data-ttu-id="8cccd-128">Следующий пример показывает как Hello toouse логические функции.</span><span class="sxs-lookup"><span data-stu-id="8cccd-128">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="8cccd-129">представлен результат Hello предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="8cccd-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="8cccd-130">Имя</span><span class="sxs-lookup"><span data-stu-id="8cccd-130">Name</span></span> | <span data-ttu-id="8cccd-131">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-131">Type</span></span> | <span data-ttu-id="8cccd-132">Значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="8cccd-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-133">andExampleOutput</span></span> | <span data-ttu-id="8cccd-134">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-134">Bool</span></span> | <span data-ttu-id="8cccd-135">Ложь</span><span class="sxs-lookup"><span data-stu-id="8cccd-135">False</span></span> |
| <span data-ttu-id="8cccd-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-136">orExampleOutput</span></span> | <span data-ttu-id="8cccd-137">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-137">Bool</span></span> | <span data-ttu-id="8cccd-138">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-138">True</span></span> |
| <span data-ttu-id="8cccd-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-139">notExampleOutput</span></span> | <span data-ttu-id="8cccd-140">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-140">Bool</span></span> | <span data-ttu-id="8cccd-141">Ложь</span><span class="sxs-lookup"><span data-stu-id="8cccd-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="8cccd-142">bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="8cccd-143">Преобразует hello tooa параметр типа boolean.</span><span class="sxs-lookup"><span data-stu-id="8cccd-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="8cccd-144">Параметры</span><span class="sxs-lookup"><span data-stu-id="8cccd-144">Parameters</span></span>

| <span data-ttu-id="8cccd-145">Параметр</span><span class="sxs-lookup"><span data-stu-id="8cccd-145">Parameter</span></span> | <span data-ttu-id="8cccd-146">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8cccd-146">Required</span></span> | <span data-ttu-id="8cccd-147">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-147">Type</span></span> | <span data-ttu-id="8cccd-148">Описание</span><span class="sxs-lookup"><span data-stu-id="8cccd-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8cccd-149">arg1</span><span class="sxs-lookup"><span data-stu-id="8cccd-149">arg1</span></span> |<span data-ttu-id="8cccd-150">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-150">Yes</span></span> |<span data-ttu-id="8cccd-151">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="8cccd-151">string or int</span></span> |<span data-ttu-id="8cccd-152">Здравствуйте, tooa tooconvert значение типа boolean.</span><span class="sxs-lookup"><span data-stu-id="8cccd-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="8cccd-153">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-153">Return value</span></span>
<span data-ttu-id="8cccd-154">Логическое hello преобразованное значение.</span><span class="sxs-lookup"><span data-stu-id="8cccd-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="8cccd-155">Примеры</span><span class="sxs-lookup"><span data-stu-id="8cccd-155">Examples</span></span>

<span data-ttu-id="8cccd-156">Следующий пример показывает как Hello bool toouse строкой или целое число со знаком.</span><span class="sxs-lookup"><span data-stu-id="8cccd-156">hello following example shows how toouse bool with a string or integer.</span></span>

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

<span data-ttu-id="8cccd-157">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="8cccd-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="8cccd-158">Имя</span><span class="sxs-lookup"><span data-stu-id="8cccd-158">Name</span></span> | <span data-ttu-id="8cccd-159">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-159">Type</span></span> | <span data-ttu-id="8cccd-160">Значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="8cccd-161">trueString</span><span class="sxs-lookup"><span data-stu-id="8cccd-161">trueString</span></span> | <span data-ttu-id="8cccd-162">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-162">Bool</span></span> | <span data-ttu-id="8cccd-163">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-163">True</span></span> |
| <span data-ttu-id="8cccd-164">falseString</span><span class="sxs-lookup"><span data-stu-id="8cccd-164">falseString</span></span> | <span data-ttu-id="8cccd-165">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-165">Bool</span></span> | <span data-ttu-id="8cccd-166">Ложь</span><span class="sxs-lookup"><span data-stu-id="8cccd-166">False</span></span> |
| <span data-ttu-id="8cccd-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="8cccd-167">trueInt</span></span> | <span data-ttu-id="8cccd-168">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-168">Bool</span></span> | <span data-ttu-id="8cccd-169">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-169">True</span></span> |
| <span data-ttu-id="8cccd-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="8cccd-170">falseInt</span></span> | <span data-ttu-id="8cccd-171">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-171">Bool</span></span> | <span data-ttu-id="8cccd-172">Ложь</span><span class="sxs-lookup"><span data-stu-id="8cccd-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="8cccd-173">if</span><span class="sxs-lookup"><span data-stu-id="8cccd-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="8cccd-174">Возвращает значение в зависимости от того, выполняется ли условие.</span><span class="sxs-lookup"><span data-stu-id="8cccd-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="8cccd-175">Параметры</span><span class="sxs-lookup"><span data-stu-id="8cccd-175">Parameters</span></span>

| <span data-ttu-id="8cccd-176">Параметр</span><span class="sxs-lookup"><span data-stu-id="8cccd-176">Parameter</span></span> | <span data-ttu-id="8cccd-177">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8cccd-177">Required</span></span> | <span data-ttu-id="8cccd-178">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-178">Type</span></span> | <span data-ttu-id="8cccd-179">Описание</span><span class="sxs-lookup"><span data-stu-id="8cccd-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8cccd-180">condition</span><span class="sxs-lookup"><span data-stu-id="8cccd-180">condition</span></span> |<span data-ttu-id="8cccd-181">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-181">Yes</span></span> |<span data-ttu-id="8cccd-182">Логическое</span><span class="sxs-lookup"><span data-stu-id="8cccd-182">boolean</span></span> |<span data-ttu-id="8cccd-183">значение toocheck Hello, является ли значение true.</span><span class="sxs-lookup"><span data-stu-id="8cccd-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="8cccd-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="8cccd-184">trueValue</span></span> |<span data-ttu-id="8cccd-185">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-185">Yes</span></span> | <span data-ttu-id="8cccd-186">строка, целое число, объект или массив</span><span class="sxs-lookup"><span data-stu-id="8cccd-186">string, int, object, or array</span></span> |<span data-ttu-id="8cccd-187">tooreturn значение Hello, hello условие истинно.</span><span class="sxs-lookup"><span data-stu-id="8cccd-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="8cccd-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="8cccd-188">falseValue</span></span> |<span data-ttu-id="8cccd-189">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-189">Yes</span></span> | <span data-ttu-id="8cccd-190">строка, целое число, объект или массив</span><span class="sxs-lookup"><span data-stu-id="8cccd-190">string, int, object, or array</span></span> |<span data-ttu-id="8cccd-191">tooreturn значение Hello, hello условие имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="8cccd-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="8cccd-192">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-192">Return value</span></span>

<span data-ttu-id="8cccd-193">Возвращает второй параметр, если первый параметр имеет значение **True** (Истина). В противном случае возвращает третий параметр.</span><span class="sxs-lookup"><span data-stu-id="8cccd-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="8cccd-194">Примечания</span><span class="sxs-lookup"><span data-stu-id="8cccd-194">Remarks</span></span>

<span data-ttu-id="8cccd-195">Этот набор tooconditionally функции можно использовать свойства ресурса.</span><span class="sxs-lookup"><span data-stu-id="8cccd-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="8cccd-196">Hello в примере не является полной шаблоном, но он демонстрирует hello соответствующих частей условно настройки группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="8cccd-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

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

### <a name="examples"></a><span data-ttu-id="8cccd-197">Примеры</span><span class="sxs-lookup"><span data-stu-id="8cccd-197">Examples</span></span>

<span data-ttu-id="8cccd-198">Следующий пример показывает как Hello toouse hello `if` функции.</span><span class="sxs-lookup"><span data-stu-id="8cccd-198">hello following example shows how toouse hello `if` function.</span></span>

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

<span data-ttu-id="8cccd-199">представлен результат Hello предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="8cccd-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="8cccd-200">Имя</span><span class="sxs-lookup"><span data-stu-id="8cccd-200">Name</span></span> | <span data-ttu-id="8cccd-201">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-201">Type</span></span> | <span data-ttu-id="8cccd-202">Значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="8cccd-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-203">yesOutput</span></span> | <span data-ttu-id="8cccd-204">Строка</span><span class="sxs-lookup"><span data-stu-id="8cccd-204">String</span></span> | <span data-ttu-id="8cccd-205">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-205">yes</span></span> |
| <span data-ttu-id="8cccd-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-206">noOutput</span></span> | <span data-ttu-id="8cccd-207">Строка</span><span class="sxs-lookup"><span data-stu-id="8cccd-207">String</span></span> | <span data-ttu-id="8cccd-208">Нет</span><span class="sxs-lookup"><span data-stu-id="8cccd-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="8cccd-209">not</span><span class="sxs-lookup"><span data-stu-id="8cccd-209">not</span></span>
`not(arg1)`

<span data-ttu-id="8cccd-210">Преобразует логическое значение tooits противоположные значения.</span><span class="sxs-lookup"><span data-stu-id="8cccd-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="8cccd-211">Параметры</span><span class="sxs-lookup"><span data-stu-id="8cccd-211">Parameters</span></span>

| <span data-ttu-id="8cccd-212">Параметр</span><span class="sxs-lookup"><span data-stu-id="8cccd-212">Parameter</span></span> | <span data-ttu-id="8cccd-213">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8cccd-213">Required</span></span> | <span data-ttu-id="8cccd-214">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-214">Type</span></span> | <span data-ttu-id="8cccd-215">Описание</span><span class="sxs-lookup"><span data-stu-id="8cccd-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8cccd-216">arg1</span><span class="sxs-lookup"><span data-stu-id="8cccd-216">arg1</span></span> |<span data-ttu-id="8cccd-217">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-217">Yes</span></span> |<span data-ttu-id="8cccd-218">Логическое</span><span class="sxs-lookup"><span data-stu-id="8cccd-218">boolean</span></span> |<span data-ttu-id="8cccd-219">tooconvert значение Hello.</span><span class="sxs-lookup"><span data-stu-id="8cccd-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="8cccd-220">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-220">Return value</span></span>

<span data-ttu-id="8cccd-221">Возвращает значение **True** (Истина), если параметр имеет значение **False** (Ложь).</span><span class="sxs-lookup"><span data-stu-id="8cccd-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="8cccd-222">Возвращает значение **False** (Ложь), если параметр имеет значение **True** (Истина).</span><span class="sxs-lookup"><span data-stu-id="8cccd-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="8cccd-223">Примеры</span><span class="sxs-lookup"><span data-stu-id="8cccd-223">Examples</span></span>

<span data-ttu-id="8cccd-224">Следующий пример показывает как Hello toouse логические функции.</span><span class="sxs-lookup"><span data-stu-id="8cccd-224">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="8cccd-225">представлен результат Hello предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="8cccd-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="8cccd-226">Имя</span><span class="sxs-lookup"><span data-stu-id="8cccd-226">Name</span></span> | <span data-ttu-id="8cccd-227">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-227">Type</span></span> | <span data-ttu-id="8cccd-228">Значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="8cccd-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-229">andExampleOutput</span></span> | <span data-ttu-id="8cccd-230">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-230">Bool</span></span> | <span data-ttu-id="8cccd-231">Ложь</span><span class="sxs-lookup"><span data-stu-id="8cccd-231">False</span></span> |
| <span data-ttu-id="8cccd-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-232">orExampleOutput</span></span> | <span data-ttu-id="8cccd-233">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-233">Bool</span></span> | <span data-ttu-id="8cccd-234">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-234">True</span></span> |
| <span data-ttu-id="8cccd-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-235">notExampleOutput</span></span> | <span data-ttu-id="8cccd-236">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-236">Bool</span></span> | <span data-ttu-id="8cccd-237">Ложь</span><span class="sxs-lookup"><span data-stu-id="8cccd-237">False</span></span> |

<span data-ttu-id="8cccd-238">Hello следующий пример использует **не** с [равняется](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="8cccd-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="8cccd-239">представлен результат Hello предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="8cccd-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="8cccd-240">Имя</span><span class="sxs-lookup"><span data-stu-id="8cccd-240">Name</span></span> | <span data-ttu-id="8cccd-241">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-241">Type</span></span> | <span data-ttu-id="8cccd-242">Значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="8cccd-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="8cccd-243">checkNotEquals</span></span> | <span data-ttu-id="8cccd-244">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-244">Bool</span></span> | <span data-ttu-id="8cccd-245">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="8cccd-246">или</span><span class="sxs-lookup"><span data-stu-id="8cccd-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="8cccd-247">Проверяет, соответствует ли истине одно из значений параметров.</span><span class="sxs-lookup"><span data-stu-id="8cccd-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="8cccd-248">Параметры</span><span class="sxs-lookup"><span data-stu-id="8cccd-248">Parameters</span></span>

| <span data-ttu-id="8cccd-249">Параметр</span><span class="sxs-lookup"><span data-stu-id="8cccd-249">Parameter</span></span> | <span data-ttu-id="8cccd-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8cccd-250">Required</span></span> | <span data-ttu-id="8cccd-251">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-251">Type</span></span> | <span data-ttu-id="8cccd-252">Описание</span><span class="sxs-lookup"><span data-stu-id="8cccd-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8cccd-253">arg1</span><span class="sxs-lookup"><span data-stu-id="8cccd-253">arg1</span></span> |<span data-ttu-id="8cccd-254">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-254">Yes</span></span> |<span data-ttu-id="8cccd-255">Логическое</span><span class="sxs-lookup"><span data-stu-id="8cccd-255">boolean</span></span> |<span data-ttu-id="8cccd-256">Здравствуйте ли первый toocheck значение равно true.</span><span class="sxs-lookup"><span data-stu-id="8cccd-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="8cccd-257">arg2</span><span class="sxs-lookup"><span data-stu-id="8cccd-257">arg2</span></span> |<span data-ttu-id="8cccd-258">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-258">Yes</span></span> |<span data-ttu-id="8cccd-259">Логическое</span><span class="sxs-lookup"><span data-stu-id="8cccd-259">boolean</span></span> |<span data-ttu-id="8cccd-260">Hello ли toocheck второе значение — true.</span><span class="sxs-lookup"><span data-stu-id="8cccd-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="8cccd-261">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-261">Return value</span></span>

<span data-ttu-id="8cccd-262">Возвращает результат **True** (Истина), если одно из значений соответствует истине. В противном случае — **False** (Ложь).</span><span class="sxs-lookup"><span data-stu-id="8cccd-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="8cccd-263">Примеры</span><span class="sxs-lookup"><span data-stu-id="8cccd-263">Examples</span></span>

<span data-ttu-id="8cccd-264">Следующий пример показывает как Hello toouse логические функции.</span><span class="sxs-lookup"><span data-stu-id="8cccd-264">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="8cccd-265">представлен результат Hello предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="8cccd-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="8cccd-266">Имя</span><span class="sxs-lookup"><span data-stu-id="8cccd-266">Name</span></span> | <span data-ttu-id="8cccd-267">Тип</span><span class="sxs-lookup"><span data-stu-id="8cccd-267">Type</span></span> | <span data-ttu-id="8cccd-268">Значение</span><span class="sxs-lookup"><span data-stu-id="8cccd-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="8cccd-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-269">andExampleOutput</span></span> | <span data-ttu-id="8cccd-270">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-270">Bool</span></span> | <span data-ttu-id="8cccd-271">Ложь</span><span class="sxs-lookup"><span data-stu-id="8cccd-271">False</span></span> |
| <span data-ttu-id="8cccd-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-272">orExampleOutput</span></span> | <span data-ttu-id="8cccd-273">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-273">Bool</span></span> | <span data-ttu-id="8cccd-274">Да</span><span class="sxs-lookup"><span data-stu-id="8cccd-274">True</span></span> |
| <span data-ttu-id="8cccd-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="8cccd-275">notExampleOutput</span></span> | <span data-ttu-id="8cccd-276">Bool</span><span class="sxs-lookup"><span data-stu-id="8cccd-276">Bool</span></span> | <span data-ttu-id="8cccd-277">Ложь</span><span class="sxs-lookup"><span data-stu-id="8cccd-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8cccd-278">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8cccd-278">Next steps</span></span>
* <span data-ttu-id="8cccd-279">Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8cccd-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8cccd-280">toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8cccd-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="8cccd-281">tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8cccd-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="8cccd-282">toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8cccd-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

