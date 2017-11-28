---
title: "Массивы и объекты в функциях шаблона Azure Resource Manager | Документация Майкрософт"
description: "Описывает функции, используемые в шаблоне Azure Resource Manager для работы с массивами и объектами."
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: 0bd9ec41761c9ce575f3bcf4d1f8e8578b83e01c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="45be3-103">Функции массивов и объектов для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45be3-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="45be3-104">Resource Manager предоставляет ряд функций для работы с массивами и объектами.</span><span class="sxs-lookup"><span data-stu-id="45be3-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* <span data-ttu-id="45be3-105">[array](#array).</span><span class="sxs-lookup"><span data-stu-id="45be3-105">[array](#array)</span></span>
* [<span data-ttu-id="45be3-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="45be3-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="45be3-107">concat</span><span class="sxs-lookup"><span data-stu-id="45be3-107">concat</span></span>](#concat)
* [<span data-ttu-id="45be3-108">contains</span><span class="sxs-lookup"><span data-stu-id="45be3-108">contains</span></span>](#contains)
* [<span data-ttu-id="45be3-109">createArray</span><span class="sxs-lookup"><span data-stu-id="45be3-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="45be3-110">empty</span><span class="sxs-lookup"><span data-stu-id="45be3-110">empty</span></span>](#empty)
* [<span data-ttu-id="45be3-111">first</span><span class="sxs-lookup"><span data-stu-id="45be3-111">first</span></span>](#first)
* [<span data-ttu-id="45be3-112">intersection</span><span class="sxs-lookup"><span data-stu-id="45be3-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="45be3-113">json</span><span class="sxs-lookup"><span data-stu-id="45be3-113">json</span></span>](#json)
* [<span data-ttu-id="45be3-114">last</span><span class="sxs-lookup"><span data-stu-id="45be3-114">last</span></span>](#last)
* [<span data-ttu-id="45be3-115">длина</span><span class="sxs-lookup"><span data-stu-id="45be3-115">length</span></span>](#length)
* [<span data-ttu-id="45be3-116">min</span><span class="sxs-lookup"><span data-stu-id="45be3-116">min</span></span>](#min)
* [<span data-ttu-id="45be3-117">max</span><span class="sxs-lookup"><span data-stu-id="45be3-117">max</span></span>](#max)
* [<span data-ttu-id="45be3-118">range</span><span class="sxs-lookup"><span data-stu-id="45be3-118">range</span></span>](#range)
* [<span data-ttu-id="45be3-119">skip</span><span class="sxs-lookup"><span data-stu-id="45be3-119">skip</span></span>](#skip)
* [<span data-ttu-id="45be3-120">take</span><span class="sxs-lookup"><span data-stu-id="45be3-120">take</span></span>](#take)
* [<span data-ttu-id="45be3-121">union</span><span class="sxs-lookup"><span data-stu-id="45be3-121">union</span></span>](#union)

<span data-ttu-id="45be3-122">Чтобы получить массив строковых значений, разделенных определенным значением, используйте [split](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="45be3-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="45be3-123">array</span><span class="sxs-lookup"><span data-stu-id="45be3-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="45be3-124">Преобразует значение в массив.</span><span class="sxs-lookup"><span data-stu-id="45be3-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-125">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-125">Parameters</span></span>

| <span data-ttu-id="45be3-126">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-126">Parameter</span></span> | <span data-ttu-id="45be3-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-127">Required</span></span> | <span data-ttu-id="45be3-128">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-128">Type</span></span> | <span data-ttu-id="45be3-129">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="45be3-130">convertToArray</span></span> |<span data-ttu-id="45be3-131">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-131">Yes</span></span> |<span data-ttu-id="45be3-132">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-132">int, string, array, or object</span></span> |<span data-ttu-id="45be3-133">Значение, которое необходимо преобразовать в массив.</span><span class="sxs-lookup"><span data-stu-id="45be3-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-134">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-134">Return value</span></span>

<span data-ttu-id="45be3-135">Массив.</span><span class="sxs-lookup"><span data-stu-id="45be3-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-136">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-136">Example</span></span>

<span data-ttu-id="45be3-137">В следующем примере показано, как использовать функцию array с различными типами:</span><span class="sxs-lookup"><span data-stu-id="45be3-137">The following example shows how to use the array function with different types.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

<span data-ttu-id="45be3-138">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-139">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-139">Name</span></span> | <span data-ttu-id="45be3-140">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-140">Type</span></span> | <span data-ttu-id="45be3-141">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-142">intOutput</span></span> | <span data-ttu-id="45be3-143">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-143">Array</span></span> | <span data-ttu-id="45be3-144">[1]</span><span class="sxs-lookup"><span data-stu-id="45be3-144">[1]</span></span> |
| <span data-ttu-id="45be3-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-145">stringOutput</span></span> | <span data-ttu-id="45be3-146">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-146">Array</span></span> | <span data-ttu-id="45be3-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="45be3-147">["a"]</span></span> |
| <span data-ttu-id="45be3-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-148">objectOutput</span></span> | <span data-ttu-id="45be3-149">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-149">Array</span></span> | <span data-ttu-id="45be3-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="45be3-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="45be3-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="45be3-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="45be3-152">Возвращает из параметров первое значение, отличное от null.</span><span class="sxs-lookup"><span data-stu-id="45be3-152">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="45be3-153">Пустые строки, пустые массивы и пустые объекты не имеют значение null.</span><span class="sxs-lookup"><span data-stu-id="45be3-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-154">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-154">Parameters</span></span>

| <span data-ttu-id="45be3-155">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-155">Parameter</span></span> | <span data-ttu-id="45be3-156">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-156">Required</span></span> | <span data-ttu-id="45be3-157">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-157">Type</span></span> | <span data-ttu-id="45be3-158">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-159">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-159">arg1</span></span> |<span data-ttu-id="45be3-160">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-160">Yes</span></span> |<span data-ttu-id="45be3-161">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-161">int, string, array, or object</span></span> |<span data-ttu-id="45be3-162">Первое значение, которое проверяется на соответствие значению null.</span><span class="sxs-lookup"><span data-stu-id="45be3-162">The first value to test for null.</span></span> |
| <span data-ttu-id="45be3-163">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="45be3-163">additional args</span></span> |<span data-ttu-id="45be3-164">Нет</span><span class="sxs-lookup"><span data-stu-id="45be3-164">No</span></span> |<span data-ttu-id="45be3-165">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-165">int, string, array, or object</span></span> |<span data-ttu-id="45be3-166">Дополнительные значения, которые проверяются на соответствие значению null.</span><span class="sxs-lookup"><span data-stu-id="45be3-166">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-167">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-167">Return value</span></span>

<span data-ttu-id="45be3-168">Значение первых параметров, отличных от null, которое может быть строкой, целым числом, массивом или объектом.</span><span class="sxs-lookup"><span data-stu-id="45be3-168">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="45be3-169">Null, если все параметры имеют значение null.</span><span class="sxs-lookup"><span data-stu-id="45be3-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="45be3-170">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-170">Example</span></span>

<span data-ttu-id="45be3-171">В следующем примере показаны выходные данные для разных случаев использования coalesce.</span><span class="sxs-lookup"><span data-stu-id="45be3-171">The following example shows the output from different uses of coalesce.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

<span data-ttu-id="45be3-172">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-172">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-173">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-173">Name</span></span> | <span data-ttu-id="45be3-174">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-174">Type</span></span> | <span data-ttu-id="45be3-175">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-176">stringOutput</span></span> | <span data-ttu-id="45be3-177">Строка</span><span class="sxs-lookup"><span data-stu-id="45be3-177">String</span></span> | <span data-ttu-id="45be3-178">по умолчанию</span><span class="sxs-lookup"><span data-stu-id="45be3-178">default</span></span> |
| <span data-ttu-id="45be3-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-179">intOutput</span></span> | <span data-ttu-id="45be3-180">int</span><span class="sxs-lookup"><span data-stu-id="45be3-180">Int</span></span> | <span data-ttu-id="45be3-181">1</span><span class="sxs-lookup"><span data-stu-id="45be3-181">1</span></span> |
| <span data-ttu-id="45be3-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-182">objectOutput</span></span> | <span data-ttu-id="45be3-183">Объект</span><span class="sxs-lookup"><span data-stu-id="45be3-183">Object</span></span> | <span data-ttu-id="45be3-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="45be3-184">{"first": "default"}</span></span> |
| <span data-ttu-id="45be3-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-185">arrayOutput</span></span> | <span data-ttu-id="45be3-186">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-186">Array</span></span> | <span data-ttu-id="45be3-187">[1]</span><span class="sxs-lookup"><span data-stu-id="45be3-187">[1]</span></span> |
| <span data-ttu-id="45be3-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-188">emptyOutput</span></span> | <span data-ttu-id="45be3-189">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-189">Bool</span></span> | <span data-ttu-id="45be3-190">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="45be3-191">concat</span><span class="sxs-lookup"><span data-stu-id="45be3-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="45be3-192">Объединяет несколько массивов и возвращает объединенный массив или объединяет несколько строковых значений и возвращает объединенную строку.</span><span class="sxs-lookup"><span data-stu-id="45be3-192">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="45be3-193">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-193">Parameters</span></span>

| <span data-ttu-id="45be3-194">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-194">Parameter</span></span> | <span data-ttu-id="45be3-195">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-195">Required</span></span> | <span data-ttu-id="45be3-196">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-196">Type</span></span> | <span data-ttu-id="45be3-197">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-198">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-198">arg1</span></span> |<span data-ttu-id="45be3-199">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-199">Yes</span></span> |<span data-ttu-id="45be3-200">массив или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-200">array or string</span></span> |<span data-ttu-id="45be3-201">Первый массив или строка для объединения.</span><span class="sxs-lookup"><span data-stu-id="45be3-201">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="45be3-202">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="45be3-202">additional arguments</span></span> |<span data-ttu-id="45be3-203">Нет</span><span class="sxs-lookup"><span data-stu-id="45be3-203">No</span></span> |<span data-ttu-id="45be3-204">массив или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-204">array or string</span></span> |<span data-ttu-id="45be3-205">Дополнительные массивы или строки в последовательном порядке для объединения.</span><span class="sxs-lookup"><span data-stu-id="45be3-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="45be3-206">Эта функция может принимать любое количество аргументов, а также строки или массивы параметров.</span><span class="sxs-lookup"><span data-stu-id="45be3-206">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="45be3-207">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-207">Return value</span></span>
<span data-ttu-id="45be3-208">Строка или массив объединенных значений.</span><span class="sxs-lookup"><span data-stu-id="45be3-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-209">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-209">Example</span></span>

<span data-ttu-id="45be3-210">В следующем примере показано, как объединить два массива.</span><span class="sxs-lookup"><span data-stu-id="45be3-210">The following example shows how to combine two arrays.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="45be3-211">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-211">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-212">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-212">Name</span></span> | <span data-ttu-id="45be3-213">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-213">Type</span></span> | <span data-ttu-id="45be3-214">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-215">return</span><span class="sxs-lookup"><span data-stu-id="45be3-215">return</span></span> | <span data-ttu-id="45be3-216">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-216">Array</span></span> | <span data-ttu-id="45be3-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="45be3-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="45be3-218">В следующем примере показано, как объединить два строковых значения и получить объединенную строку.</span><span class="sxs-lookup"><span data-stu-id="45be3-218">The following example shows how to combine two string values and return a concatenated string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="45be3-219">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-219">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-220">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-220">Name</span></span> | <span data-ttu-id="45be3-221">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-221">Type</span></span> | <span data-ttu-id="45be3-222">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-223">concatOutput</span></span> | <span data-ttu-id="45be3-224">Строка</span><span class="sxs-lookup"><span data-stu-id="45be3-224">String</span></span> | <span data-ttu-id="45be3-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="45be3-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="45be3-226">contains</span><span class="sxs-lookup"><span data-stu-id="45be3-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="45be3-227">Проверяет, содержит ли массив значение, содержит ли объект ключ или содержит ли строка подстроку.</span><span class="sxs-lookup"><span data-stu-id="45be3-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-228">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-228">Parameters</span></span>

| <span data-ttu-id="45be3-229">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-229">Parameter</span></span> | <span data-ttu-id="45be3-230">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-230">Required</span></span> | <span data-ttu-id="45be3-231">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-231">Type</span></span> | <span data-ttu-id="45be3-232">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-233">container</span><span class="sxs-lookup"><span data-stu-id="45be3-233">container</span></span> |<span data-ttu-id="45be3-234">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-234">Yes</span></span> |<span data-ttu-id="45be3-235">массив, объект или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-235">array, object, or string</span></span> |<span data-ttu-id="45be3-236">Значение, содержащее значение, которое необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="45be3-236">The value that contains the value to find.</span></span> |
| <span data-ttu-id="45be3-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="45be3-237">itemToFind</span></span> |<span data-ttu-id="45be3-238">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-238">Yes</span></span> |<span data-ttu-id="45be3-239">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="45be3-239">string or int</span></span> |<span data-ttu-id="45be3-240">Значение, которое необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="45be3-240">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-241">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-241">Return value</span></span>

<span data-ttu-id="45be3-242">**True**, если элемент найден. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="45be3-242">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-243">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-243">Example</span></span>

<span data-ttu-id="45be3-244">В следующем примере показано, как использовать функцию contains с различными типами:</span><span class="sxs-lookup"><span data-stu-id="45be3-244">The following example shows how to use contains with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

<span data-ttu-id="45be3-245">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-246">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-246">Name</span></span> | <span data-ttu-id="45be3-247">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-247">Type</span></span> | <span data-ttu-id="45be3-248">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="45be3-249">stringTrue</span></span> | <span data-ttu-id="45be3-250">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-250">Bool</span></span> | <span data-ttu-id="45be3-251">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-251">True</span></span> |
| <span data-ttu-id="45be3-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="45be3-252">stringFalse</span></span> | <span data-ttu-id="45be3-253">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-253">Bool</span></span> | <span data-ttu-id="45be3-254">Ложь</span><span class="sxs-lookup"><span data-stu-id="45be3-254">False</span></span> |
| <span data-ttu-id="45be3-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="45be3-255">objectTrue</span></span> | <span data-ttu-id="45be3-256">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-256">Bool</span></span> | <span data-ttu-id="45be3-257">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-257">True</span></span> |
| <span data-ttu-id="45be3-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="45be3-258">objectFalse</span></span> | <span data-ttu-id="45be3-259">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-259">Bool</span></span> | <span data-ttu-id="45be3-260">Ложь</span><span class="sxs-lookup"><span data-stu-id="45be3-260">False</span></span> |
| <span data-ttu-id="45be3-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="45be3-261">arrayTrue</span></span> | <span data-ttu-id="45be3-262">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-262">Bool</span></span> | <span data-ttu-id="45be3-263">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-263">True</span></span> |
| <span data-ttu-id="45be3-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="45be3-264">arrayFalse</span></span> | <span data-ttu-id="45be3-265">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-265">Bool</span></span> | <span data-ttu-id="45be3-266">Ложь</span><span class="sxs-lookup"><span data-stu-id="45be3-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="45be3-267">createarray</span><span class="sxs-lookup"><span data-stu-id="45be3-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="45be3-268">Создает массив из параметров.</span><span class="sxs-lookup"><span data-stu-id="45be3-268">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-269">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-269">Parameters</span></span>

| <span data-ttu-id="45be3-270">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-270">Parameter</span></span> | <span data-ttu-id="45be3-271">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-271">Required</span></span> | <span data-ttu-id="45be3-272">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-272">Type</span></span> | <span data-ttu-id="45be3-273">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-274">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-274">arg1</span></span> |<span data-ttu-id="45be3-275">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-275">Yes</span></span> |<span data-ttu-id="45be3-276">Строка, целое число, массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="45be3-277">Первое значение в массиве.</span><span class="sxs-lookup"><span data-stu-id="45be3-277">The first value in the array.</span></span> |
| <span data-ttu-id="45be3-278">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="45be3-278">additional arguments</span></span> |<span data-ttu-id="45be3-279">Нет</span><span class="sxs-lookup"><span data-stu-id="45be3-279">No</span></span> |<span data-ttu-id="45be3-280">Строка, целое число, массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="45be3-281">Дополнительные значения в массиве.</span><span class="sxs-lookup"><span data-stu-id="45be3-281">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-282">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-282">Return value</span></span>

<span data-ttu-id="45be3-283">Массив.</span><span class="sxs-lookup"><span data-stu-id="45be3-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-284">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-284">Example</span></span>

<span data-ttu-id="45be3-285">В следующем примере показано, как использовать функцию createArray с различными типами:</span><span class="sxs-lookup"><span data-stu-id="45be3-285">The following example shows how to use createArray with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

<span data-ttu-id="45be3-286">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-286">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-287">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-287">Name</span></span> | <span data-ttu-id="45be3-288">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-288">Type</span></span> | <span data-ttu-id="45be3-289">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="45be3-290">stringArray</span></span> | <span data-ttu-id="45be3-291">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-291">Array</span></span> | <span data-ttu-id="45be3-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="45be3-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="45be3-293">intArray</span><span class="sxs-lookup"><span data-stu-id="45be3-293">intArray</span></span> | <span data-ttu-id="45be3-294">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-294">Array</span></span> | <span data-ttu-id="45be3-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="45be3-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="45be3-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="45be3-296">objectArray</span></span> | <span data-ttu-id="45be3-297">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-297">Array</span></span> | <span data-ttu-id="45be3-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="45be3-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="45be3-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="45be3-299">arrayArray</span></span> | <span data-ttu-id="45be3-300">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-300">Array</span></span> | <span data-ttu-id="45be3-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="45be3-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="45be3-302">empty</span><span class="sxs-lookup"><span data-stu-id="45be3-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="45be3-303">Определяет, являются ли пустыми массив, объект или строка.</span><span class="sxs-lookup"><span data-stu-id="45be3-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-304">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-304">Parameters</span></span>

| <span data-ttu-id="45be3-305">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-305">Parameter</span></span> | <span data-ttu-id="45be3-306">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-306">Required</span></span> | <span data-ttu-id="45be3-307">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-307">Type</span></span> | <span data-ttu-id="45be3-308">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="45be3-309">itemToTest</span></span> |<span data-ttu-id="45be3-310">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-310">Yes</span></span> |<span data-ttu-id="45be3-311">массив, объект или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-311">array, object, or string</span></span> |<span data-ttu-id="45be3-312">Значение, которое необходимо проверить на наличие содержимого.</span><span class="sxs-lookup"><span data-stu-id="45be3-312">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-313">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-313">Return value</span></span>

<span data-ttu-id="45be3-314">Возвращает результат **True**, если значение пустое. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="45be3-314">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-315">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-315">Example</span></span>

<span data-ttu-id="45be3-316">В следующем примере проверяется, являются ли пустыми массив, объект и строка.</span><span class="sxs-lookup"><span data-stu-id="45be3-316">The following example checks whether an array, object, and string are empty.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="45be3-317">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-317">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-318">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-318">Name</span></span> | <span data-ttu-id="45be3-319">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-319">Type</span></span> | <span data-ttu-id="45be3-320">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="45be3-321">arrayEmpty</span></span> | <span data-ttu-id="45be3-322">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-322">Bool</span></span> | <span data-ttu-id="45be3-323">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-323">True</span></span> |
| <span data-ttu-id="45be3-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="45be3-324">objectEmpty</span></span> | <span data-ttu-id="45be3-325">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-325">Bool</span></span> | <span data-ttu-id="45be3-326">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-326">True</span></span> |
| <span data-ttu-id="45be3-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="45be3-327">stringEmpty</span></span> | <span data-ttu-id="45be3-328">Bool</span><span class="sxs-lookup"><span data-stu-id="45be3-328">Bool</span></span> | <span data-ttu-id="45be3-329">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="45be3-330">first</span><span class="sxs-lookup"><span data-stu-id="45be3-330">first</span></span>
`first(arg1)`

<span data-ttu-id="45be3-331">Возвращает первый элемент массива или первый знак строки.</span><span class="sxs-lookup"><span data-stu-id="45be3-331">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-332">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-332">Parameters</span></span>

| <span data-ttu-id="45be3-333">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-333">Parameter</span></span> | <span data-ttu-id="45be3-334">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-334">Required</span></span> | <span data-ttu-id="45be3-335">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-335">Type</span></span> | <span data-ttu-id="45be3-336">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-337">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-337">arg1</span></span> |<span data-ttu-id="45be3-338">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-338">Yes</span></span> |<span data-ttu-id="45be3-339">массив или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-339">array or string</span></span> |<span data-ttu-id="45be3-340">Значение, из которого необходимо извлечь первый элемент или знак.</span><span class="sxs-lookup"><span data-stu-id="45be3-340">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-341">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-341">Return value</span></span>

<span data-ttu-id="45be3-342">Тип (строка, целое число, массив или объект) первого элемента в массиве или строка первого знака.</span><span class="sxs-lookup"><span data-stu-id="45be3-342">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-343">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-343">Example</span></span>

<span data-ttu-id="45be3-344">В следующем примере показано, как использовать функцию first с массивом и строкой:</span><span class="sxs-lookup"><span data-stu-id="45be3-344">The following example shows how to use the first function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="45be3-345">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-345">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-346">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-346">Name</span></span> | <span data-ttu-id="45be3-347">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-347">Type</span></span> | <span data-ttu-id="45be3-348">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-349">arrayOutput</span></span> | <span data-ttu-id="45be3-350">Строка</span><span class="sxs-lookup"><span data-stu-id="45be3-350">String</span></span> | <span data-ttu-id="45be3-351">one</span><span class="sxs-lookup"><span data-stu-id="45be3-351">one</span></span> |
| <span data-ttu-id="45be3-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-352">stringOutput</span></span> | <span data-ttu-id="45be3-353">Строка</span><span class="sxs-lookup"><span data-stu-id="45be3-353">String</span></span> | <span data-ttu-id="45be3-354">O</span><span class="sxs-lookup"><span data-stu-id="45be3-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="45be3-355">пересечению</span><span class="sxs-lookup"><span data-stu-id="45be3-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="45be3-356">Возвращает из параметров один массив или объект с общими элементами.</span><span class="sxs-lookup"><span data-stu-id="45be3-356">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-357">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-357">Parameters</span></span>

| <span data-ttu-id="45be3-358">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-358">Parameter</span></span> | <span data-ttu-id="45be3-359">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-359">Required</span></span> | <span data-ttu-id="45be3-360">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-360">Type</span></span> | <span data-ttu-id="45be3-361">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-362">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-362">arg1</span></span> |<span data-ttu-id="45be3-363">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-363">Yes</span></span> |<span data-ttu-id="45be3-364">массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-364">array or object</span></span> |<span data-ttu-id="45be3-365">Первое значение для поиска общих элементов.</span><span class="sxs-lookup"><span data-stu-id="45be3-365">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="45be3-366">arg2</span><span class="sxs-lookup"><span data-stu-id="45be3-366">arg2</span></span> |<span data-ttu-id="45be3-367">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-367">Yes</span></span> |<span data-ttu-id="45be3-368">массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-368">array or object</span></span> |<span data-ttu-id="45be3-369">Второе значение для поиска общих элементов.</span><span class="sxs-lookup"><span data-stu-id="45be3-369">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="45be3-370">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="45be3-370">additional arguments</span></span> |<span data-ttu-id="45be3-371">Нет</span><span class="sxs-lookup"><span data-stu-id="45be3-371">No</span></span> |<span data-ttu-id="45be3-372">массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-372">array or object</span></span> |<span data-ttu-id="45be3-373">Дополнительные значения для поиска общих элементов.</span><span class="sxs-lookup"><span data-stu-id="45be3-373">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-374">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-374">Return value</span></span>

<span data-ttu-id="45be3-375">Массив или объект с общими элементами.</span><span class="sxs-lookup"><span data-stu-id="45be3-375">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-376">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-376">Example</span></span>

<span data-ttu-id="45be3-377">В следующем примере показано, как использовать функцию intersection с массивами и объектами:</span><span class="sxs-lookup"><span data-stu-id="45be3-377">The following example shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="45be3-378">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-378">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-379">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-379">Name</span></span> | <span data-ttu-id="45be3-380">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-380">Type</span></span> | <span data-ttu-id="45be3-381">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-382">objectOutput</span></span> | <span data-ttu-id="45be3-383">Объект</span><span class="sxs-lookup"><span data-stu-id="45be3-383">Object</span></span> | <span data-ttu-id="45be3-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="45be3-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="45be3-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-385">arrayOutput</span></span> | <span data-ttu-id="45be3-386">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-386">Array</span></span> | <span data-ttu-id="45be3-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="45be3-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="45be3-388">json</span><span class="sxs-lookup"><span data-stu-id="45be3-388">json</span></span>
`json(arg1)`

<span data-ttu-id="45be3-389">Возвращает объект JSON.</span><span class="sxs-lookup"><span data-stu-id="45be3-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-390">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-390">Parameters</span></span>

| <span data-ttu-id="45be3-391">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-391">Parameter</span></span> | <span data-ttu-id="45be3-392">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-392">Required</span></span> | <span data-ttu-id="45be3-393">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-393">Type</span></span> | <span data-ttu-id="45be3-394">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-395">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-395">arg1</span></span> |<span data-ttu-id="45be3-396">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-396">Yes</span></span> |<span data-ttu-id="45be3-397">string</span><span class="sxs-lookup"><span data-stu-id="45be3-397">string</span></span> |<span data-ttu-id="45be3-398">Значение, которое необходимо преобразовать в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="45be3-398">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="45be3-399">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-399">Return value</span></span>

<span data-ttu-id="45be3-400">Объект JSON из указанной строки или пустой объект, если указано значение **null**.</span><span class="sxs-lookup"><span data-stu-id="45be3-400">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-401">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-401">Example</span></span>

<span data-ttu-id="45be3-402">В следующем примере показано, как использовать функцию intersection с массивами и объектами:</span><span class="sxs-lookup"><span data-stu-id="45be3-402">The following example shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

<span data-ttu-id="45be3-403">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-403">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-404">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-404">Name</span></span> | <span data-ttu-id="45be3-405">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-405">Type</span></span> | <span data-ttu-id="45be3-406">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-407">jsonOutput</span></span> | <span data-ttu-id="45be3-408">Объект</span><span class="sxs-lookup"><span data-stu-id="45be3-408">Object</span></span> | <span data-ttu-id="45be3-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="45be3-409">{"a": "b"}</span></span> |
| <span data-ttu-id="45be3-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-410">nullOutput</span></span> | <span data-ttu-id="45be3-411">Логический</span><span class="sxs-lookup"><span data-stu-id="45be3-411">Boolean</span></span> | <span data-ttu-id="45be3-412">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="45be3-413">last</span><span class="sxs-lookup"><span data-stu-id="45be3-413">last</span></span>
`last (arg1)`

<span data-ttu-id="45be3-414">Возвращает последний элемент массива или последний знак строки.</span><span class="sxs-lookup"><span data-stu-id="45be3-414">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-415">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-415">Parameters</span></span>

| <span data-ttu-id="45be3-416">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-416">Parameter</span></span> | <span data-ttu-id="45be3-417">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-417">Required</span></span> | <span data-ttu-id="45be3-418">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-418">Type</span></span> | <span data-ttu-id="45be3-419">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-420">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-420">arg1</span></span> |<span data-ttu-id="45be3-421">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-421">Yes</span></span> |<span data-ttu-id="45be3-422">массив или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-422">array or string</span></span> |<span data-ttu-id="45be3-423">Значение, из которого необходимо извлечь последний элемент или знак.</span><span class="sxs-lookup"><span data-stu-id="45be3-423">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-424">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-424">Return value</span></span>

<span data-ttu-id="45be3-425">Тип (строка, целое число, массив или объект) последнего элемента в массиве или последнего символа в строке.</span><span class="sxs-lookup"><span data-stu-id="45be3-425">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-426">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-426">Example</span></span>

<span data-ttu-id="45be3-427">В следующем примере показано, как использовать функцию last с массивом и строкой:</span><span class="sxs-lookup"><span data-stu-id="45be3-427">The following example shows how to use the last function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="45be3-428">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-429">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-429">Name</span></span> | <span data-ttu-id="45be3-430">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-430">Type</span></span> | <span data-ttu-id="45be3-431">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-432">arrayOutput</span></span> | <span data-ttu-id="45be3-433">Строка</span><span class="sxs-lookup"><span data-stu-id="45be3-433">String</span></span> | <span data-ttu-id="45be3-434">three</span><span class="sxs-lookup"><span data-stu-id="45be3-434">three</span></span> |
| <span data-ttu-id="45be3-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-435">stringOutput</span></span> | <span data-ttu-id="45be3-436">Строка</span><span class="sxs-lookup"><span data-stu-id="45be3-436">String</span></span> | <span data-ttu-id="45be3-437">e</span><span class="sxs-lookup"><span data-stu-id="45be3-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="45be3-438">длина</span><span class="sxs-lookup"><span data-stu-id="45be3-438">length</span></span>
`length(arg1)`

<span data-ttu-id="45be3-439">Возвращает число элементов в массиве или знаков в строке.</span><span class="sxs-lookup"><span data-stu-id="45be3-439">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-440">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-440">Parameters</span></span>

| <span data-ttu-id="45be3-441">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-441">Parameter</span></span> | <span data-ttu-id="45be3-442">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-442">Required</span></span> | <span data-ttu-id="45be3-443">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-443">Type</span></span> | <span data-ttu-id="45be3-444">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-445">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-445">arg1</span></span> |<span data-ttu-id="45be3-446">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-446">Yes</span></span> |<span data-ttu-id="45be3-447">массив или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-447">array or string</span></span> |<span data-ttu-id="45be3-448">Массив, который необходимо использовать для получения числа элементов, или строка — для получения числа знаков.</span><span class="sxs-lookup"><span data-stu-id="45be3-448">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-449">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-449">Return value</span></span>

<span data-ttu-id="45be3-450">Целое число.</span><span class="sxs-lookup"><span data-stu-id="45be3-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="45be3-451">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-451">Example</span></span>

<span data-ttu-id="45be3-452">В следующем примере показано, как использовать функцию length с массивом и строкой:</span><span class="sxs-lookup"><span data-stu-id="45be3-452">The following example shows how to use length with an array and string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

<span data-ttu-id="45be3-453">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-453">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-454">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-454">Name</span></span> | <span data-ttu-id="45be3-455">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-455">Type</span></span> | <span data-ttu-id="45be3-456">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="45be3-457">arrayLength</span></span> | <span data-ttu-id="45be3-458">int</span><span class="sxs-lookup"><span data-stu-id="45be3-458">Int</span></span> | <span data-ttu-id="45be3-459">3</span><span class="sxs-lookup"><span data-stu-id="45be3-459">3</span></span> |
| <span data-ttu-id="45be3-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="45be3-460">stringLength</span></span> | <span data-ttu-id="45be3-461">int</span><span class="sxs-lookup"><span data-stu-id="45be3-461">Int</span></span> | <span data-ttu-id="45be3-462">13.</span><span class="sxs-lookup"><span data-stu-id="45be3-462">13</span></span> |

<span data-ttu-id="45be3-463">Эту функцию можно использовать с массивом для указания числа итераций при создании ресурсов.</span><span class="sxs-lookup"><span data-stu-id="45be3-463">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="45be3-464">В следующем примере параметр **siteNames** ссылается на массив имен для использования при создании веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="45be3-464">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="45be3-465">Дополнительные сведения об использовании этой функции с массивом см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="45be3-466">Min</span><span class="sxs-lookup"><span data-stu-id="45be3-466">min</span></span>
`min(arg1)`

<span data-ttu-id="45be3-467">Возвращает минимальное значение из массива целых чисел или разделенный запятыми список целых чисел.</span><span class="sxs-lookup"><span data-stu-id="45be3-467">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-468">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-468">Parameters</span></span>

| <span data-ttu-id="45be3-469">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-469">Parameter</span></span> | <span data-ttu-id="45be3-470">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-470">Required</span></span> | <span data-ttu-id="45be3-471">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-471">Type</span></span> | <span data-ttu-id="45be3-472">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-473">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-473">arg1</span></span> |<span data-ttu-id="45be3-474">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-474">Yes</span></span> |<span data-ttu-id="45be3-475">массив целых чисел или разделенный запятыми список целых чисел</span><span class="sxs-lookup"><span data-stu-id="45be3-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="45be3-476">Коллекция, для которой необходимо получить минимальное значение.</span><span class="sxs-lookup"><span data-stu-id="45be3-476">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-477">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-477">Return value</span></span>

<span data-ttu-id="45be3-478">Целое число, представляющее минимальное значение.</span><span class="sxs-lookup"><span data-stu-id="45be3-478">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-479">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-479">Example</span></span>

<span data-ttu-id="45be3-480">В следующем примере показано, как использовать функцию min с массивом и списком целых чисел:</span><span class="sxs-lookup"><span data-stu-id="45be3-480">The following example shows how to use min with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="45be3-481">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-481">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-482">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-482">Name</span></span> | <span data-ttu-id="45be3-483">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-483">Type</span></span> | <span data-ttu-id="45be3-484">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-485">arrayOutput</span></span> | <span data-ttu-id="45be3-486">int</span><span class="sxs-lookup"><span data-stu-id="45be3-486">Int</span></span> | <span data-ttu-id="45be3-487">0</span><span class="sxs-lookup"><span data-stu-id="45be3-487">0</span></span> |
| <span data-ttu-id="45be3-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-488">intOutput</span></span> | <span data-ttu-id="45be3-489">int</span><span class="sxs-lookup"><span data-stu-id="45be3-489">Int</span></span> | <span data-ttu-id="45be3-490">0</span><span class="sxs-lookup"><span data-stu-id="45be3-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="45be3-491">max</span><span class="sxs-lookup"><span data-stu-id="45be3-491">max</span></span>
`max(arg1)`

<span data-ttu-id="45be3-492">Возвращает максимальное значение из массива целых чисел или разделенный запятыми список целых чисел.</span><span class="sxs-lookup"><span data-stu-id="45be3-492">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-493">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-493">Parameters</span></span>

| <span data-ttu-id="45be3-494">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-494">Parameter</span></span> | <span data-ttu-id="45be3-495">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-495">Required</span></span> | <span data-ttu-id="45be3-496">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-496">Type</span></span> | <span data-ttu-id="45be3-497">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-498">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-498">arg1</span></span> |<span data-ttu-id="45be3-499">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-499">Yes</span></span> |<span data-ttu-id="45be3-500">массив целых чисел или разделенный запятыми список целых чисел</span><span class="sxs-lookup"><span data-stu-id="45be3-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="45be3-501">Коллекция, для которой необходимо получить максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="45be3-501">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-502">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-502">Return value</span></span>

<span data-ttu-id="45be3-503">Целое число, представляющее максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="45be3-503">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-504">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-504">Example</span></span>

<span data-ttu-id="45be3-505">В следующем примере показано, как использовать функцию max с массивом и списком целых чисел:</span><span class="sxs-lookup"><span data-stu-id="45be3-505">The following example shows how to use max with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="45be3-506">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-506">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-507">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-507">Name</span></span> | <span data-ttu-id="45be3-508">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-508">Type</span></span> | <span data-ttu-id="45be3-509">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-510">arrayOutput</span></span> | <span data-ttu-id="45be3-511">int</span><span class="sxs-lookup"><span data-stu-id="45be3-511">Int</span></span> | <span data-ttu-id="45be3-512">5</span><span class="sxs-lookup"><span data-stu-id="45be3-512">5</span></span> |
| <span data-ttu-id="45be3-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-513">intOutput</span></span> | <span data-ttu-id="45be3-514">int</span><span class="sxs-lookup"><span data-stu-id="45be3-514">Int</span></span> | <span data-ttu-id="45be3-515">5</span><span class="sxs-lookup"><span data-stu-id="45be3-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="45be3-516">range</span><span class="sxs-lookup"><span data-stu-id="45be3-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="45be3-517">Создает массив целых чисел, используя начальное целое число и количество элементов.</span><span class="sxs-lookup"><span data-stu-id="45be3-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-518">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-518">Parameters</span></span>

| <span data-ttu-id="45be3-519">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-519">Parameter</span></span> | <span data-ttu-id="45be3-520">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-520">Required</span></span> | <span data-ttu-id="45be3-521">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-521">Type</span></span> | <span data-ttu-id="45be3-522">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="45be3-523">startingInteger</span></span> |<span data-ttu-id="45be3-524">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-524">Yes</span></span> |<span data-ttu-id="45be3-525">int</span><span class="sxs-lookup"><span data-stu-id="45be3-525">int</span></span> |<span data-ttu-id="45be3-526">Первое целое число в массиве.</span><span class="sxs-lookup"><span data-stu-id="45be3-526">The first integer in the array.</span></span> |
| <span data-ttu-id="45be3-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="45be3-527">numberofElements</span></span> |<span data-ttu-id="45be3-528">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-528">Yes</span></span> |<span data-ttu-id="45be3-529">int</span><span class="sxs-lookup"><span data-stu-id="45be3-529">int</span></span> |<span data-ttu-id="45be3-530">Количество целых чисел в массиве.</span><span class="sxs-lookup"><span data-stu-id="45be3-530">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-531">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-531">Return value</span></span>

<span data-ttu-id="45be3-532">Массив целых чисел.</span><span class="sxs-lookup"><span data-stu-id="45be3-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-533">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-533">Example</span></span>

<span data-ttu-id="45be3-534">В следующем примере показано, как использовать функцию range:</span><span class="sxs-lookup"><span data-stu-id="45be3-534">The following example shows how to use the range function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

<span data-ttu-id="45be3-535">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-535">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-536">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-536">Name</span></span> | <span data-ttu-id="45be3-537">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-537">Type</span></span> | <span data-ttu-id="45be3-538">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-539">rangeOutput</span></span> | <span data-ttu-id="45be3-540">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-540">Array</span></span> | <span data-ttu-id="45be3-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="45be3-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="45be3-542">skip</span><span class="sxs-lookup"><span data-stu-id="45be3-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="45be3-543">Возвращает массив, содержащий все элементы из исходного массива, начиная с заданной позиции в массиве, или строку, содержащую все знаки из исходной строки, начиная с заданной позиции в строке.</span><span class="sxs-lookup"><span data-stu-id="45be3-543">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-544">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-544">Parameters</span></span>

| <span data-ttu-id="45be3-545">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-545">Parameter</span></span> | <span data-ttu-id="45be3-546">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-546">Required</span></span> | <span data-ttu-id="45be3-547">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-547">Type</span></span> | <span data-ttu-id="45be3-548">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="45be3-549">originalValue</span></span> |<span data-ttu-id="45be3-550">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-550">Yes</span></span> |<span data-ttu-id="45be3-551">массив или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-551">array or string</span></span> |<span data-ttu-id="45be3-552">Массив или строка, используемые для пропуска.</span><span class="sxs-lookup"><span data-stu-id="45be3-552">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="45be3-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="45be3-553">numberToSkip</span></span> |<span data-ttu-id="45be3-554">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-554">Yes</span></span> |<span data-ttu-id="45be3-555">int</span><span class="sxs-lookup"><span data-stu-id="45be3-555">int</span></span> |<span data-ttu-id="45be3-556">Число элементов или знаков, которые необходимо пропустить.</span><span class="sxs-lookup"><span data-stu-id="45be3-556">The number of elements or characters to skip.</span></span> <span data-ttu-id="45be3-557">Если это значение меньше или равно 0, то возвращаются все элементы или знаки в значении.</span><span class="sxs-lookup"><span data-stu-id="45be3-557">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="45be3-558">Если это значение превышает длину массива или строки, то возвращается пустой массив или пустая строка.</span><span class="sxs-lookup"><span data-stu-id="45be3-558">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-559">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-559">Return value</span></span>

<span data-ttu-id="45be3-560">Массив или строка.</span><span class="sxs-lookup"><span data-stu-id="45be3-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-561">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-561">Example</span></span>

<span data-ttu-id="45be3-562">В следующем примере пропускается заданное число элементов в массиве и заданное число знаков в строке.</span><span class="sxs-lookup"><span data-stu-id="45be3-562">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

<span data-ttu-id="45be3-563">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-564">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-564">Name</span></span> | <span data-ttu-id="45be3-565">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-565">Type</span></span> | <span data-ttu-id="45be3-566">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-567">arrayOutput</span></span> | <span data-ttu-id="45be3-568">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-568">Array</span></span> | <span data-ttu-id="45be3-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="45be3-569">["three"]</span></span> |
| <span data-ttu-id="45be3-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-570">stringOutput</span></span> | <span data-ttu-id="45be3-571">Строка</span><span class="sxs-lookup"><span data-stu-id="45be3-571">String</span></span> | <span data-ttu-id="45be3-572">two three</span><span class="sxs-lookup"><span data-stu-id="45be3-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="45be3-573">take</span><span class="sxs-lookup"><span data-stu-id="45be3-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="45be3-574">Возвращает массив, содержащий указанное число элементов, считая от начала массива, или строку, содержащую указанное число знаков, считая от начала строки.</span><span class="sxs-lookup"><span data-stu-id="45be3-574">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-575">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-575">Parameters</span></span>

| <span data-ttu-id="45be3-576">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-576">Parameter</span></span> | <span data-ttu-id="45be3-577">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-577">Required</span></span> | <span data-ttu-id="45be3-578">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-578">Type</span></span> | <span data-ttu-id="45be3-579">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="45be3-580">originalValue</span></span> |<span data-ttu-id="45be3-581">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-581">Yes</span></span> |<span data-ttu-id="45be3-582">массив или строка</span><span class="sxs-lookup"><span data-stu-id="45be3-582">array or string</span></span> |<span data-ttu-id="45be3-583">Массив или строка, из которых берутся элементы.</span><span class="sxs-lookup"><span data-stu-id="45be3-583">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="45be3-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="45be3-584">numberToTake</span></span> |<span data-ttu-id="45be3-585">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-585">Yes</span></span> |<span data-ttu-id="45be3-586">int</span><span class="sxs-lookup"><span data-stu-id="45be3-586">int</span></span> |<span data-ttu-id="45be3-587">Число элементов или знаков, которые необходимо взять.</span><span class="sxs-lookup"><span data-stu-id="45be3-587">The number of elements or characters to take.</span></span> <span data-ttu-id="45be3-588">Если это значение меньше или равно 0, то возвращается пустой массив или строка.</span><span class="sxs-lookup"><span data-stu-id="45be3-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="45be3-589">Если это значение превышает длину заданного массива или строки, то возвращаются все элементы в массиве или строке.</span><span class="sxs-lookup"><span data-stu-id="45be3-589">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-590">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-590">Return value</span></span>

<span data-ttu-id="45be3-591">Массив или строка.</span><span class="sxs-lookup"><span data-stu-id="45be3-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-592">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-592">Example</span></span>

<span data-ttu-id="45be3-593">В следующем примере из массива извлекается заданное число элементов, а из строки — заданное число знаков.</span><span class="sxs-lookup"><span data-stu-id="45be3-593">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

<span data-ttu-id="45be3-594">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-594">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-595">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-595">Name</span></span> | <span data-ttu-id="45be3-596">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-596">Type</span></span> | <span data-ttu-id="45be3-597">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-598">arrayOutput</span></span> | <span data-ttu-id="45be3-599">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-599">Array</span></span> | <span data-ttu-id="45be3-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="45be3-600">["one", "two"]</span></span> |
| <span data-ttu-id="45be3-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-601">stringOutput</span></span> | <span data-ttu-id="45be3-602">Строка</span><span class="sxs-lookup"><span data-stu-id="45be3-602">String</span></span> | <span data-ttu-id="45be3-603">on</span><span class="sxs-lookup"><span data-stu-id="45be3-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="45be3-604">union</span><span class="sxs-lookup"><span data-stu-id="45be3-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="45be3-605">Возвращает из параметров один массив или объект со всеми элементами.</span><span class="sxs-lookup"><span data-stu-id="45be3-605">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="45be3-606">Повторяющиеся значения или ключи включаются только один раз.</span><span class="sxs-lookup"><span data-stu-id="45be3-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="45be3-607">Параметры</span><span class="sxs-lookup"><span data-stu-id="45be3-607">Parameters</span></span>

| <span data-ttu-id="45be3-608">Параметр</span><span class="sxs-lookup"><span data-stu-id="45be3-608">Parameter</span></span> | <span data-ttu-id="45be3-609">Обязательно</span><span class="sxs-lookup"><span data-stu-id="45be3-609">Required</span></span> | <span data-ttu-id="45be3-610">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-610">Type</span></span> | <span data-ttu-id="45be3-611">Описание</span><span class="sxs-lookup"><span data-stu-id="45be3-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="45be3-612">arg1</span><span class="sxs-lookup"><span data-stu-id="45be3-612">arg1</span></span> |<span data-ttu-id="45be3-613">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-613">Yes</span></span> |<span data-ttu-id="45be3-614">массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-614">array or object</span></span> |<span data-ttu-id="45be3-615">Первое значение для объединения элементов.</span><span class="sxs-lookup"><span data-stu-id="45be3-615">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="45be3-616">arg2</span><span class="sxs-lookup"><span data-stu-id="45be3-616">arg2</span></span> |<span data-ttu-id="45be3-617">Да</span><span class="sxs-lookup"><span data-stu-id="45be3-617">Yes</span></span> |<span data-ttu-id="45be3-618">массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-618">array or object</span></span> |<span data-ttu-id="45be3-619">Второе значение для объединения элементов.</span><span class="sxs-lookup"><span data-stu-id="45be3-619">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="45be3-620">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="45be3-620">additional arguments</span></span> |<span data-ttu-id="45be3-621">Нет</span><span class="sxs-lookup"><span data-stu-id="45be3-621">No</span></span> |<span data-ttu-id="45be3-622">массив или объект</span><span class="sxs-lookup"><span data-stu-id="45be3-622">array or object</span></span> |<span data-ttu-id="45be3-623">Дополнительные значения для объединения элементов.</span><span class="sxs-lookup"><span data-stu-id="45be3-623">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="45be3-624">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="45be3-624">Return value</span></span>

<span data-ttu-id="45be3-625">Массив или объект.</span><span class="sxs-lookup"><span data-stu-id="45be3-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="45be3-626">Пример</span><span class="sxs-lookup"><span data-stu-id="45be3-626">Example</span></span>

<span data-ttu-id="45be3-627">В следующем примере показано, как использовать функцию union с массивами и объектами:</span><span class="sxs-lookup"><span data-stu-id="45be3-627">The following example shows how to use union with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="45be3-628">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="45be3-628">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="45be3-629">Имя</span><span class="sxs-lookup"><span data-stu-id="45be3-629">Name</span></span> | <span data-ttu-id="45be3-630">Тип</span><span class="sxs-lookup"><span data-stu-id="45be3-630">Type</span></span> | <span data-ttu-id="45be3-631">Значение</span><span class="sxs-lookup"><span data-stu-id="45be3-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="45be3-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-632">objectOutput</span></span> | <span data-ttu-id="45be3-633">Объект</span><span class="sxs-lookup"><span data-stu-id="45be3-633">Object</span></span> | <span data-ttu-id="45be3-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="45be3-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="45be3-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="45be3-635">arrayOutput</span></span> | <span data-ttu-id="45be3-636">Массив,</span><span class="sxs-lookup"><span data-stu-id="45be3-636">Array</span></span> | <span data-ttu-id="45be3-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="45be3-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45be3-638">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45be3-638">Next steps</span></span>
* <span data-ttu-id="45be3-639">Описание разделов в шаблоне Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-639">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="45be3-640">Инструкции по объединению нескольких шаблонов см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-640">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="45be3-641">Указания по выполнению заданного количества циклов итерации при создании типа ресурса см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-641">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="45be3-642">Указания по развертыванию созданного шаблона см. в статье, посвященной [развертыванию приложения с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="45be3-642">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

