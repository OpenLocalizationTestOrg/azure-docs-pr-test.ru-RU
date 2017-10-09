---
title: "функции - массивы и объекты шаблона диспетчера ресурсов aaaAzure | Документы Microsoft"
description: "Описывает toouse функции hello в шаблоне диспетчера ресурсов Azure для работы с массивы и объекты."
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
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="dd4b6-103">Функции массивов и объектов для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dd4b6-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="dd4b6-104">Resource Manager предоставляет ряд функций для работы с массивами и объектами.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* <span data-ttu-id="dd4b6-105">[array](#array).</span><span class="sxs-lookup"><span data-stu-id="dd4b6-105">[array](#array)</span></span>
* [<span data-ttu-id="dd4b6-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="dd4b6-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="dd4b6-107">concat</span><span class="sxs-lookup"><span data-stu-id="dd4b6-107">concat</span></span>](#concat)
* [<span data-ttu-id="dd4b6-108">contains</span><span class="sxs-lookup"><span data-stu-id="dd4b6-108">contains</span></span>](#contains)
* [<span data-ttu-id="dd4b6-109">createArray</span><span class="sxs-lookup"><span data-stu-id="dd4b6-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="dd4b6-110">empty</span><span class="sxs-lookup"><span data-stu-id="dd4b6-110">empty</span></span>](#empty)
* [<span data-ttu-id="dd4b6-111">first</span><span class="sxs-lookup"><span data-stu-id="dd4b6-111">first</span></span>](#first)
* [<span data-ttu-id="dd4b6-112">intersection</span><span class="sxs-lookup"><span data-stu-id="dd4b6-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="dd4b6-113">json</span><span class="sxs-lookup"><span data-stu-id="dd4b6-113">json</span></span>](#json)
* [<span data-ttu-id="dd4b6-114">last</span><span class="sxs-lookup"><span data-stu-id="dd4b6-114">last</span></span>](#last)
* [<span data-ttu-id="dd4b6-115">длина</span><span class="sxs-lookup"><span data-stu-id="dd4b6-115">length</span></span>](#length)
* [<span data-ttu-id="dd4b6-116">min</span><span class="sxs-lookup"><span data-stu-id="dd4b6-116">min</span></span>](#min)
* [<span data-ttu-id="dd4b6-117">max</span><span class="sxs-lookup"><span data-stu-id="dd4b6-117">max</span></span>](#max)
* [<span data-ttu-id="dd4b6-118">range</span><span class="sxs-lookup"><span data-stu-id="dd4b6-118">range</span></span>](#range)
* [<span data-ttu-id="dd4b6-119">skip</span><span class="sxs-lookup"><span data-stu-id="dd4b6-119">skip</span></span>](#skip)
* [<span data-ttu-id="dd4b6-120">take</span><span class="sxs-lookup"><span data-stu-id="dd4b6-120">take</span></span>](#take)
* [<span data-ttu-id="dd4b6-121">union</span><span class="sxs-lookup"><span data-stu-id="dd4b6-121">union</span></span>](#union)

<span data-ttu-id="dd4b6-122">tooget массив строковых значений, разделенных по значению, в разделе [разбиение](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="dd4b6-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="dd4b6-123">array</span><span class="sxs-lookup"><span data-stu-id="dd4b6-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="dd4b6-124">Преобразует массив tooan значение hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-125">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-125">Parameters</span></span>

| <span data-ttu-id="dd4b6-126">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-126">Parameter</span></span> | <span data-ttu-id="dd4b6-127">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-127">Required</span></span> | <span data-ttu-id="dd4b6-128">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-128">Type</span></span> | <span data-ttu-id="dd4b6-129">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="dd4b6-130">convertToArray</span></span> |<span data-ttu-id="dd4b6-131">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-131">Yes</span></span> |<span data-ttu-id="dd4b6-132">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-132">int, string, array, or object</span></span> |<span data-ttu-id="dd4b6-133">Массив tooan tooconvert значение Hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-134">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-134">Return value</span></span>

<span data-ttu-id="dd4b6-135">Массив.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-136">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-136">Example</span></span>

<span data-ttu-id="dd4b6-137">Hello следующем примере показано, как toouse hello функции массива с различными типами.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-137">hello following example shows how toouse hello array function with different types.</span></span>

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

<span data-ttu-id="dd4b6-138">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-139">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-139">Name</span></span> | <span data-ttu-id="dd4b6-140">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-140">Type</span></span> | <span data-ttu-id="dd4b6-141">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-142">intOutput</span></span> | <span data-ttu-id="dd4b6-143">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-143">Array</span></span> | <span data-ttu-id="dd4b6-144">[1]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-144">[1]</span></span> |
| <span data-ttu-id="dd4b6-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-145">stringOutput</span></span> | <span data-ttu-id="dd4b6-146">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-146">Array</span></span> | <span data-ttu-id="dd4b6-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-147">["a"]</span></span> |
| <span data-ttu-id="dd4b6-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-148">objectOutput</span></span> | <span data-ttu-id="dd4b6-149">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-149">Array</span></span> | <span data-ttu-id="dd4b6-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="dd4b6-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="dd4b6-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="dd4b6-152">Возвращает первое непустое значение на основе параметров hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="dd4b6-153">Пустые строки, пустые массивы и пустые объекты не имеют значение null.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-154">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-154">Parameters</span></span>

| <span data-ttu-id="dd4b6-155">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-155">Parameter</span></span> | <span data-ttu-id="dd4b6-156">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-156">Required</span></span> | <span data-ttu-id="dd4b6-157">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-157">Type</span></span> | <span data-ttu-id="dd4b6-158">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-159">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-159">arg1</span></span> |<span data-ttu-id="dd4b6-160">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-160">Yes</span></span> |<span data-ttu-id="dd4b6-161">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-161">int, string, array, or object</span></span> |<span data-ttu-id="dd4b6-162">Hello первый tootest значение со значением NULL.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="dd4b6-163">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="dd4b6-163">additional args</span></span> |<span data-ttu-id="dd4b6-164">Нет</span><span class="sxs-lookup"><span data-stu-id="dd4b6-164">No</span></span> |<span data-ttu-id="dd4b6-165">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-165">int, string, array, or object</span></span> |<span data-ttu-id="dd4b6-166">Дополнительные значения tootest со значением NULL.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-167">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-167">Return value</span></span>

<span data-ttu-id="dd4b6-168">значение Hello hello первый ненулевой параметров, может быть строка, int, массив или объект.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="dd4b6-169">Null, если все параметры имеют значение null.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="dd4b6-170">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-170">Example</span></span>

<span data-ttu-id="dd4b6-171">Hello пример hello выходные данные различных вариантах использования coalesce.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-171">hello following example shows hello output from different uses of coalesce.</span></span>

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

<span data-ttu-id="dd4b6-172">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-173">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-173">Name</span></span> | <span data-ttu-id="dd4b6-174">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-174">Type</span></span> | <span data-ttu-id="dd4b6-175">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-176">stringOutput</span></span> | <span data-ttu-id="dd4b6-177">Строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-177">String</span></span> | <span data-ttu-id="dd4b6-178">по умолчанию</span><span class="sxs-lookup"><span data-stu-id="dd4b6-178">default</span></span> |
| <span data-ttu-id="dd4b6-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-179">intOutput</span></span> | <span data-ttu-id="dd4b6-180">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-180">Int</span></span> | <span data-ttu-id="dd4b6-181">1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-181">1</span></span> |
| <span data-ttu-id="dd4b6-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-182">objectOutput</span></span> | <span data-ttu-id="dd4b6-183">Объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-183">Object</span></span> | <span data-ttu-id="dd4b6-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="dd4b6-184">{"first": "default"}</span></span> |
| <span data-ttu-id="dd4b6-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-185">arrayOutput</span></span> | <span data-ttu-id="dd4b6-186">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-186">Array</span></span> | <span data-ttu-id="dd4b6-187">[1]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-187">[1]</span></span> |
| <span data-ttu-id="dd4b6-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-188">emptyOutput</span></span> | <span data-ttu-id="dd4b6-189">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-189">Bool</span></span> | <span data-ttu-id="dd4b6-190">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="dd4b6-191">concat</span><span class="sxs-lookup"><span data-stu-id="dd4b6-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="dd4b6-192">Объединяет несколько массивов и возвращает массив объединенные hello, или объединяет несколько строковых значений и возвращает строку hello объединяются.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="dd4b6-193">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-193">Parameters</span></span>

| <span data-ttu-id="dd4b6-194">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-194">Parameter</span></span> | <span data-ttu-id="dd4b6-195">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-195">Required</span></span> | <span data-ttu-id="dd4b6-196">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-196">Type</span></span> | <span data-ttu-id="dd4b6-197">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-198">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-198">arg1</span></span> |<span data-ttu-id="dd4b6-199">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-199">Yes</span></span> |<span data-ttu-id="dd4b6-200">массив или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-200">array or string</span></span> |<span data-ttu-id="dd4b6-201">Здравствуйте, первый массив или строка для сцепления.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="dd4b6-202">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="dd4b6-202">additional arguments</span></span> |<span data-ttu-id="dd4b6-203">Нет</span><span class="sxs-lookup"><span data-stu-id="dd4b6-203">No</span></span> |<span data-ttu-id="dd4b6-204">массив или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-204">array or string</span></span> |<span data-ttu-id="dd4b6-205">Дополнительные массивы или строки в последовательном порядке для объединения.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="dd4b6-206">Эта функция может принимать любое количество аргументов и могут принимать строки или массивы параметров hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="dd4b6-207">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-207">Return value</span></span>
<span data-ttu-id="dd4b6-208">Строка или массив объединенных значений.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-209">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-209">Example</span></span>

<span data-ttu-id="dd4b6-210">Hello в следующем примере показано, как toocombine двух массивов.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-210">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="dd4b6-211">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-212">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-212">Name</span></span> | <span data-ttu-id="dd4b6-213">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-213">Type</span></span> | <span data-ttu-id="dd4b6-214">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-215">return</span><span class="sxs-lookup"><span data-stu-id="dd4b6-215">return</span></span> | <span data-ttu-id="dd4b6-216">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-216">Array</span></span> | <span data-ttu-id="dd4b6-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="dd4b6-218">Привет, в следующем примере показано, как toocombine двух строковые значения и возвращает сцепленную строку.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="dd4b6-219">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-220">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-220">Name</span></span> | <span data-ttu-id="dd4b6-221">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-221">Type</span></span> | <span data-ttu-id="dd4b6-222">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-223">concatOutput</span></span> | <span data-ttu-id="dd4b6-224">Строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-224">String</span></span> | <span data-ttu-id="dd4b6-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="dd4b6-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="dd4b6-226">contains</span><span class="sxs-lookup"><span data-stu-id="dd4b6-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="dd4b6-227">Проверяет, содержит ли массив значение, содержит ли объект ключ или содержит ли строка подстроку.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-228">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-228">Parameters</span></span>

| <span data-ttu-id="dd4b6-229">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-229">Parameter</span></span> | <span data-ttu-id="dd4b6-230">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-230">Required</span></span> | <span data-ttu-id="dd4b6-231">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-231">Type</span></span> | <span data-ttu-id="dd4b6-232">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-233">container</span><span class="sxs-lookup"><span data-stu-id="dd4b6-233">container</span></span> |<span data-ttu-id="dd4b6-234">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-234">Yes</span></span> |<span data-ttu-id="dd4b6-235">массив, объект или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-235">array, object, or string</span></span> |<span data-ttu-id="dd4b6-236">Hello значение, содержащее значение toofind hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="dd4b6-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="dd4b6-237">itemToFind</span></span> |<span data-ttu-id="dd4b6-238">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-238">Yes</span></span> |<span data-ttu-id="dd4b6-239">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="dd4b6-239">string or int</span></span> |<span data-ttu-id="dd4b6-240">toofind значение Hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-241">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-241">Return value</span></span>

<span data-ttu-id="dd4b6-242">**Значение true,** Если hello элемент найден; в противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-243">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-243">Example</span></span>

<span data-ttu-id="dd4b6-244">Hello следующий пример показывает, как toouse содержит с разными типами:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-244">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="dd4b6-245">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-246">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-246">Name</span></span> | <span data-ttu-id="dd4b6-247">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-247">Type</span></span> | <span data-ttu-id="dd4b6-248">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="dd4b6-249">stringTrue</span></span> | <span data-ttu-id="dd4b6-250">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-250">Bool</span></span> | <span data-ttu-id="dd4b6-251">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-251">True</span></span> |
| <span data-ttu-id="dd4b6-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="dd4b6-252">stringFalse</span></span> | <span data-ttu-id="dd4b6-253">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-253">Bool</span></span> | <span data-ttu-id="dd4b6-254">Ложь</span><span class="sxs-lookup"><span data-stu-id="dd4b6-254">False</span></span> |
| <span data-ttu-id="dd4b6-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="dd4b6-255">objectTrue</span></span> | <span data-ttu-id="dd4b6-256">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-256">Bool</span></span> | <span data-ttu-id="dd4b6-257">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-257">True</span></span> |
| <span data-ttu-id="dd4b6-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="dd4b6-258">objectFalse</span></span> | <span data-ttu-id="dd4b6-259">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-259">Bool</span></span> | <span data-ttu-id="dd4b6-260">Ложь</span><span class="sxs-lookup"><span data-stu-id="dd4b6-260">False</span></span> |
| <span data-ttu-id="dd4b6-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="dd4b6-261">arrayTrue</span></span> | <span data-ttu-id="dd4b6-262">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-262">Bool</span></span> | <span data-ttu-id="dd4b6-263">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-263">True</span></span> |
| <span data-ttu-id="dd4b6-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="dd4b6-264">arrayFalse</span></span> | <span data-ttu-id="dd4b6-265">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-265">Bool</span></span> | <span data-ttu-id="dd4b6-266">Ложь</span><span class="sxs-lookup"><span data-stu-id="dd4b6-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="dd4b6-267">createarray</span><span class="sxs-lookup"><span data-stu-id="dd4b6-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="dd4b6-268">Создает массив из параметров hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-269">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-269">Parameters</span></span>

| <span data-ttu-id="dd4b6-270">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-270">Parameter</span></span> | <span data-ttu-id="dd4b6-271">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-271">Required</span></span> | <span data-ttu-id="dd4b6-272">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-272">Type</span></span> | <span data-ttu-id="dd4b6-273">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-274">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-274">arg1</span></span> |<span data-ttu-id="dd4b6-275">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-275">Yes</span></span> |<span data-ttu-id="dd4b6-276">Строка, целое число, массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="dd4b6-277">Hello первое значение в массиве hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="dd4b6-278">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="dd4b6-278">additional arguments</span></span> |<span data-ttu-id="dd4b6-279">Нет</span><span class="sxs-lookup"><span data-stu-id="dd4b6-279">No</span></span> |<span data-ttu-id="dd4b6-280">Строка, целое число, массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="dd4b6-281">Дополнительные значения в массиве hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-282">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-282">Return value</span></span>

<span data-ttu-id="dd4b6-283">Массив.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-284">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-284">Example</span></span>

<span data-ttu-id="dd4b6-285">Следующий пример показывает как Hello createArray toouse с различными типами:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-285">hello following example shows how toouse createArray with different types:</span></span>

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

<span data-ttu-id="dd4b6-286">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-287">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-287">Name</span></span> | <span data-ttu-id="dd4b6-288">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-288">Type</span></span> | <span data-ttu-id="dd4b6-289">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="dd4b6-290">stringArray</span></span> | <span data-ttu-id="dd4b6-291">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-291">Array</span></span> | <span data-ttu-id="dd4b6-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="dd4b6-293">intArray</span><span class="sxs-lookup"><span data-stu-id="dd4b6-293">intArray</span></span> | <span data-ttu-id="dd4b6-294">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-294">Array</span></span> | <span data-ttu-id="dd4b6-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="dd4b6-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="dd4b6-296">objectArray</span></span> | <span data-ttu-id="dd4b6-297">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-297">Array</span></span> | <span data-ttu-id="dd4b6-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="dd4b6-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="dd4b6-299">arrayArray</span></span> | <span data-ttu-id="dd4b6-300">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-300">Array</span></span> | <span data-ttu-id="dd4b6-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="dd4b6-302">empty</span><span class="sxs-lookup"><span data-stu-id="dd4b6-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="dd4b6-303">Определяет, являются ли пустыми массив, объект или строка.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-304">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-304">Parameters</span></span>

| <span data-ttu-id="dd4b6-305">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-305">Parameter</span></span> | <span data-ttu-id="dd4b6-306">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-306">Required</span></span> | <span data-ttu-id="dd4b6-307">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-307">Type</span></span> | <span data-ttu-id="dd4b6-308">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="dd4b6-309">itemToTest</span></span> |<span data-ttu-id="dd4b6-310">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-310">Yes</span></span> |<span data-ttu-id="dd4b6-311">массив, объект или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-311">array, object, or string</span></span> |<span data-ttu-id="dd4b6-312">Здравствуйте toocheck значение, если она пуста.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-313">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-313">Return value</span></span>

<span data-ttu-id="dd4b6-314">Возвращает **True** Если hello значение является пустой; в противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-315">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-315">Example</span></span>

<span data-ttu-id="dd4b6-316">Следующий пример Hello проверяет array, object и string пустым.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-316">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="dd4b6-317">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-318">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-318">Name</span></span> | <span data-ttu-id="dd4b6-319">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-319">Type</span></span> | <span data-ttu-id="dd4b6-320">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="dd4b6-321">arrayEmpty</span></span> | <span data-ttu-id="dd4b6-322">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-322">Bool</span></span> | <span data-ttu-id="dd4b6-323">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-323">True</span></span> |
| <span data-ttu-id="dd4b6-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="dd4b6-324">objectEmpty</span></span> | <span data-ttu-id="dd4b6-325">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-325">Bool</span></span> | <span data-ttu-id="dd4b6-326">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-326">True</span></span> |
| <span data-ttu-id="dd4b6-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="dd4b6-327">stringEmpty</span></span> | <span data-ttu-id="dd4b6-328">Bool</span><span class="sxs-lookup"><span data-stu-id="dd4b6-328">Bool</span></span> | <span data-ttu-id="dd4b6-329">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="dd4b6-330">first</span><span class="sxs-lookup"><span data-stu-id="dd4b6-330">first</span></span>
`first(arg1)`

<span data-ttu-id="dd4b6-331">Возвращает hello первый элемент массива hello или первым символом строки hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-332">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-332">Parameters</span></span>

| <span data-ttu-id="dd4b6-333">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-333">Parameter</span></span> | <span data-ttu-id="dd4b6-334">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-334">Required</span></span> | <span data-ttu-id="dd4b6-335">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-335">Type</span></span> | <span data-ttu-id="dd4b6-336">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-337">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-337">arg1</span></span> |<span data-ttu-id="dd4b6-338">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-338">Yes</span></span> |<span data-ttu-id="dd4b6-339">массив или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-339">array or string</span></span> |<span data-ttu-id="dd4b6-340">символ или первый элемент tooretrieve значение hello Hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-341">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-341">Return value</span></span>

<span data-ttu-id="dd4b6-342">Hello тип (строка, int, массива или объекта) hello первый элемент массива, или hello первого символа строки.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-343">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-343">Example</span></span>

<span data-ttu-id="dd4b6-344">Hello следующем примере показано, как toouse hello первой функции с массивом и строкой.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-344">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="dd4b6-345">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-346">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-346">Name</span></span> | <span data-ttu-id="dd4b6-347">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-347">Type</span></span> | <span data-ttu-id="dd4b6-348">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-349">arrayOutput</span></span> | <span data-ttu-id="dd4b6-350">Строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-350">String</span></span> | <span data-ttu-id="dd4b6-351">one</span><span class="sxs-lookup"><span data-stu-id="dd4b6-351">one</span></span> |
| <span data-ttu-id="dd4b6-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-352">stringOutput</span></span> | <span data-ttu-id="dd4b6-353">Строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-353">String</span></span> | <span data-ttu-id="dd4b6-354">O</span><span class="sxs-lookup"><span data-stu-id="dd4b6-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="dd4b6-355">пересечению</span><span class="sxs-lookup"><span data-stu-id="dd4b6-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="dd4b6-356">Возвращает массив или объект с hello Общие элементы на основе параметров hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-357">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-357">Parameters</span></span>

| <span data-ttu-id="dd4b6-358">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-358">Parameter</span></span> | <span data-ttu-id="dd4b6-359">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-359">Required</span></span> | <span data-ttu-id="dd4b6-360">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-360">Type</span></span> | <span data-ttu-id="dd4b6-361">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-362">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-362">arg1</span></span> |<span data-ttu-id="dd4b6-363">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-363">Yes</span></span> |<span data-ttu-id="dd4b6-364">массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-364">array or object</span></span> |<span data-ttu-id="dd4b6-365">Hello первый toouse значение для поиска Общие элементы.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="dd4b6-366">arg2</span><span class="sxs-lookup"><span data-stu-id="dd4b6-366">arg2</span></span> |<span data-ttu-id="dd4b6-367">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-367">Yes</span></span> |<span data-ttu-id="dd4b6-368">массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-368">array or object</span></span> |<span data-ttu-id="dd4b6-369">Hello второй toouse значение для поиска Общие элементы.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="dd4b6-370">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="dd4b6-370">additional arguments</span></span> |<span data-ttu-id="dd4b6-371">Нет</span><span class="sxs-lookup"><span data-stu-id="dd4b6-371">No</span></span> |<span data-ttu-id="dd4b6-372">массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-372">array or object</span></span> |<span data-ttu-id="dd4b6-373">Toouse дополнительных значений для поиска Общие элементы.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-374">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-374">Return value</span></span>

<span data-ttu-id="dd4b6-375">Массив или объект с hello Общие элементы.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-376">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-376">Example</span></span>

<span data-ttu-id="dd4b6-377">Следующий пример показывает, как массивы toouse пересечение с Hello и объектов:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="dd4b6-378">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-379">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-379">Name</span></span> | <span data-ttu-id="dd4b6-380">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-380">Type</span></span> | <span data-ttu-id="dd4b6-381">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-382">objectOutput</span></span> | <span data-ttu-id="dd4b6-383">Объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-383">Object</span></span> | <span data-ttu-id="dd4b6-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="dd4b6-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="dd4b6-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-385">arrayOutput</span></span> | <span data-ttu-id="dd4b6-386">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-386">Array</span></span> | <span data-ttu-id="dd4b6-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="dd4b6-388">json</span><span class="sxs-lookup"><span data-stu-id="dd4b6-388">json</span></span>
`json(arg1)`

<span data-ttu-id="dd4b6-389">Возвращает объект JSON.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-390">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-390">Parameters</span></span>

| <span data-ttu-id="dd4b6-391">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-391">Parameter</span></span> | <span data-ttu-id="dd4b6-392">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-392">Required</span></span> | <span data-ttu-id="dd4b6-393">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-393">Type</span></span> | <span data-ttu-id="dd4b6-394">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-395">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-395">arg1</span></span> |<span data-ttu-id="dd4b6-396">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-396">Yes</span></span> |<span data-ttu-id="dd4b6-397">string</span><span class="sxs-lookup"><span data-stu-id="dd4b6-397">string</span></span> |<span data-ttu-id="dd4b6-398">tooJSON tooconvert значение Hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="dd4b6-399">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-399">Return value</span></span>

<span data-ttu-id="dd4b6-400">Hello объекта JSON из hello указанная строка или пустой объект при **null** указано.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-401">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-401">Example</span></span>

<span data-ttu-id="dd4b6-402">Следующий пример показывает, как массивы toouse пересечение с Hello и объектов:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="dd4b6-403">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-404">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-404">Name</span></span> | <span data-ttu-id="dd4b6-405">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-405">Type</span></span> | <span data-ttu-id="dd4b6-406">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-407">jsonOutput</span></span> | <span data-ttu-id="dd4b6-408">Объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-408">Object</span></span> | <span data-ttu-id="dd4b6-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="dd4b6-409">{"a": "b"}</span></span> |
| <span data-ttu-id="dd4b6-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-410">nullOutput</span></span> | <span data-ttu-id="dd4b6-411">Логический</span><span class="sxs-lookup"><span data-stu-id="dd4b6-411">Boolean</span></span> | <span data-ttu-id="dd4b6-412">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="dd4b6-413">last</span><span class="sxs-lookup"><span data-stu-id="dd4b6-413">last</span></span>
`last (arg1)`

<span data-ttu-id="dd4b6-414">Возвращает hello последний элемент массива hello или последнего символа строки hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-415">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-415">Parameters</span></span>

| <span data-ttu-id="dd4b6-416">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-416">Parameter</span></span> | <span data-ttu-id="dd4b6-417">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-417">Required</span></span> | <span data-ttu-id="dd4b6-418">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-418">Type</span></span> | <span data-ttu-id="dd4b6-419">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-420">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-420">arg1</span></span> |<span data-ttu-id="dd4b6-421">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-421">Yes</span></span> |<span data-ttu-id="dd4b6-422">массив или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-422">array or string</span></span> |<span data-ttu-id="dd4b6-423">последний элемент hello tooretrieve Hello значение или символ.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-424">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-424">Return value</span></span>

<span data-ttu-id="dd4b6-425">Hello тип (строка, int, массива или объекта) hello последнего элемента в массиве, или hello последнего символа строки.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-426">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-426">Example</span></span>

<span data-ttu-id="dd4b6-427">Hello следующем примере показано, как toouse hello последнюю функцию с массивом и строкой.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-427">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="dd4b6-428">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-429">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-429">Name</span></span> | <span data-ttu-id="dd4b6-430">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-430">Type</span></span> | <span data-ttu-id="dd4b6-431">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-432">arrayOutput</span></span> | <span data-ttu-id="dd4b6-433">Строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-433">String</span></span> | <span data-ttu-id="dd4b6-434">three</span><span class="sxs-lookup"><span data-stu-id="dd4b6-434">three</span></span> |
| <span data-ttu-id="dd4b6-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-435">stringOutput</span></span> | <span data-ttu-id="dd4b6-436">Строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-436">String</span></span> | <span data-ttu-id="dd4b6-437">e</span><span class="sxs-lookup"><span data-stu-id="dd4b6-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="dd4b6-438">длина</span><span class="sxs-lookup"><span data-stu-id="dd4b6-438">length</span></span>
`length(arg1)`

<span data-ttu-id="dd4b6-439">Возвращает hello количество элементов в массиве, или символы в строке.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-440">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-440">Parameters</span></span>

| <span data-ttu-id="dd4b6-441">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-441">Parameter</span></span> | <span data-ttu-id="dd4b6-442">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-442">Required</span></span> | <span data-ttu-id="dd4b6-443">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-443">Type</span></span> | <span data-ttu-id="dd4b6-444">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-445">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-445">arg1</span></span> |<span data-ttu-id="dd4b6-446">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-446">Yes</span></span> |<span data-ttu-id="dd4b6-447">массив или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-447">array or string</span></span> |<span data-ttu-id="dd4b6-448">Здравствуйте toouse массива для получения hello количество элементов или hello toouse строки для получения hello число символов.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-449">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-449">Return value</span></span>

<span data-ttu-id="dd4b6-450">Целое число.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="dd4b6-451">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-451">Example</span></span>

<span data-ttu-id="dd4b6-452">Следующий пример показывает как Hello toouse длины с массивом и строкой:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-452">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="dd4b6-453">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-454">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-454">Name</span></span> | <span data-ttu-id="dd4b6-455">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-455">Type</span></span> | <span data-ttu-id="dd4b6-456">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="dd4b6-457">arrayLength</span></span> | <span data-ttu-id="dd4b6-458">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-458">Int</span></span> | <span data-ttu-id="dd4b6-459">3</span><span class="sxs-lookup"><span data-stu-id="dd4b6-459">3</span></span> |
| <span data-ttu-id="dd4b6-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="dd4b6-460">stringLength</span></span> | <span data-ttu-id="dd4b6-461">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-461">Int</span></span> | <span data-ttu-id="dd4b6-462">13.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-462">13</span></span> |

<span data-ttu-id="dd4b6-463">При создании ресурсов, можно использовать эту функцию с массивом toospecify hello количеством итераций.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="dd4b6-464">В следующем примере hello, hello параметр **siteNames** относится tooan массив toouse имен при создании hello веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="dd4b6-465">Дополнительные сведения об использовании этой функции с массивом см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="dd4b6-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="dd4b6-466">Min</span><span class="sxs-lookup"><span data-stu-id="dd4b6-466">min</span></span>
`min(arg1)`

<span data-ttu-id="dd4b6-467">Возвращает hello минимальное значение из массива целых чисел или разделителями запятыми списка целых чисел.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-468">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-468">Parameters</span></span>

| <span data-ttu-id="dd4b6-469">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-469">Parameter</span></span> | <span data-ttu-id="dd4b6-470">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-470">Required</span></span> | <span data-ttu-id="dd4b6-471">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-471">Type</span></span> | <span data-ttu-id="dd4b6-472">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-473">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-473">arg1</span></span> |<span data-ttu-id="dd4b6-474">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-474">Yes</span></span> |<span data-ttu-id="dd4b6-475">массив целых чисел или разделенный запятыми список целых чисел</span><span class="sxs-lookup"><span data-stu-id="dd4b6-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="dd4b6-476">Hello коллекции tooget hello минимальное значение.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-477">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-477">Return value</span></span>

<span data-ttu-id="dd4b6-478">Целое число, представляющее минимальное значение hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-479">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-479">Example</span></span>

<span data-ttu-id="dd4b6-480">Следующий пример показывает как Hello min toouse с массивом и список целых чисел:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="dd4b6-481">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-482">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-482">Name</span></span> | <span data-ttu-id="dd4b6-483">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-483">Type</span></span> | <span data-ttu-id="dd4b6-484">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-485">arrayOutput</span></span> | <span data-ttu-id="dd4b6-486">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-486">Int</span></span> | <span data-ttu-id="dd4b6-487">0</span><span class="sxs-lookup"><span data-stu-id="dd4b6-487">0</span></span> |
| <span data-ttu-id="dd4b6-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-488">intOutput</span></span> | <span data-ttu-id="dd4b6-489">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-489">Int</span></span> | <span data-ttu-id="dd4b6-490">0</span><span class="sxs-lookup"><span data-stu-id="dd4b6-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="dd4b6-491">max</span><span class="sxs-lookup"><span data-stu-id="dd4b6-491">max</span></span>
`max(arg1)`

<span data-ttu-id="dd4b6-492">Возвращает hello максимальное значение из массива целых чисел или разделителями запятыми списка целых чисел.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-493">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-493">Parameters</span></span>

| <span data-ttu-id="dd4b6-494">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-494">Parameter</span></span> | <span data-ttu-id="dd4b6-495">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-495">Required</span></span> | <span data-ttu-id="dd4b6-496">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-496">Type</span></span> | <span data-ttu-id="dd4b6-497">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-498">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-498">arg1</span></span> |<span data-ttu-id="dd4b6-499">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-499">Yes</span></span> |<span data-ttu-id="dd4b6-500">массив целых чисел или разделенный запятыми список целых чисел</span><span class="sxs-lookup"><span data-stu-id="dd4b6-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="dd4b6-501">Hello коллекции tooget hello максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-502">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-502">Return value</span></span>

<span data-ttu-id="dd4b6-503">Целое число, представляющее максимальное значение hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-504">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-504">Example</span></span>

<span data-ttu-id="dd4b6-505">Следующий пример показывает как Hello toouse max с массивом и список целых чисел:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="dd4b6-506">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-507">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-507">Name</span></span> | <span data-ttu-id="dd4b6-508">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-508">Type</span></span> | <span data-ttu-id="dd4b6-509">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-510">arrayOutput</span></span> | <span data-ttu-id="dd4b6-511">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-511">Int</span></span> | <span data-ttu-id="dd4b6-512">5</span><span class="sxs-lookup"><span data-stu-id="dd4b6-512">5</span></span> |
| <span data-ttu-id="dd4b6-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-513">intOutput</span></span> | <span data-ttu-id="dd4b6-514">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-514">Int</span></span> | <span data-ttu-id="dd4b6-515">5</span><span class="sxs-lookup"><span data-stu-id="dd4b6-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="dd4b6-516">range</span><span class="sxs-lookup"><span data-stu-id="dd4b6-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="dd4b6-517">Создает массив целых чисел, используя начальное целое число и количество элементов.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-518">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-518">Parameters</span></span>

| <span data-ttu-id="dd4b6-519">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-519">Parameter</span></span> | <span data-ttu-id="dd4b6-520">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-520">Required</span></span> | <span data-ttu-id="dd4b6-521">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-521">Type</span></span> | <span data-ttu-id="dd4b6-522">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="dd4b6-523">startingInteger</span></span> |<span data-ttu-id="dd4b6-524">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-524">Yes</span></span> |<span data-ttu-id="dd4b6-525">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-525">int</span></span> |<span data-ttu-id="dd4b6-526">Hello первое целое число в массиве hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="dd4b6-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="dd4b6-527">numberofElements</span></span> |<span data-ttu-id="dd4b6-528">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-528">Yes</span></span> |<span data-ttu-id="dd4b6-529">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-529">int</span></span> |<span data-ttu-id="dd4b6-530">Количество целочисленных значений в массиве hello Hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-531">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-531">Return value</span></span>

<span data-ttu-id="dd4b6-532">Массив целых чисел.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-533">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-533">Example</span></span>

<span data-ttu-id="dd4b6-534">Hello в следующем примере показано, как toouse hello диапазона функции:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-534">hello following example shows how toouse hello range function:</span></span>

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

<span data-ttu-id="dd4b6-535">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-536">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-536">Name</span></span> | <span data-ttu-id="dd4b6-537">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-537">Type</span></span> | <span data-ttu-id="dd4b6-538">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-539">rangeOutput</span></span> | <span data-ttu-id="dd4b6-540">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-540">Array</span></span> | <span data-ttu-id="dd4b6-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="dd4b6-542">skip</span><span class="sxs-lookup"><span data-stu-id="dd4b6-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="dd4b6-543">Возвращает массив со всеми элементами hello после hello указанное число в массиве hello, или возвращает строку, в которой все символы hello после hello указанное число в строку hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-544">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-544">Parameters</span></span>

| <span data-ttu-id="dd4b6-545">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-545">Parameter</span></span> | <span data-ttu-id="dd4b6-546">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-546">Required</span></span> | <span data-ttu-id="dd4b6-547">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-547">Type</span></span> | <span data-ttu-id="dd4b6-548">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="dd4b6-549">originalValue</span></span> |<span data-ttu-id="dd4b6-550">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-550">Yes</span></span> |<span data-ttu-id="dd4b6-551">массив или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-551">array or string</span></span> |<span data-ttu-id="dd4b6-552">Hello массиву или строке toouse для пропуска.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="dd4b6-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="dd4b6-553">numberToSkip</span></span> |<span data-ttu-id="dd4b6-554">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-554">Yes</span></span> |<span data-ttu-id="dd4b6-555">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-555">int</span></span> |<span data-ttu-id="dd4b6-556">количество элементов или символы tooskip Hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="dd4b6-557">Если это значение меньше или равно 0, все hello элементов или символов в значении hello возвращаются.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="dd4b6-558">Если превышает длину hello hello массиву или строке, возвращается пустой массив или строку.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-559">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-559">Return value</span></span>

<span data-ttu-id="dd4b6-560">Массив или строка.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-561">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-561">Example</span></span>

<span data-ttu-id="dd4b6-562">Следующий пример hello пропускает Hello заданное число элементов в массиве hello и hello указанное число символов в строке.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="dd4b6-563">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-564">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-564">Name</span></span> | <span data-ttu-id="dd4b6-565">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-565">Type</span></span> | <span data-ttu-id="dd4b6-566">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-567">arrayOutput</span></span> | <span data-ttu-id="dd4b6-568">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-568">Array</span></span> | <span data-ttu-id="dd4b6-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-569">["three"]</span></span> |
| <span data-ttu-id="dd4b6-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-570">stringOutput</span></span> | <span data-ttu-id="dd4b6-571">Строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-571">String</span></span> | <span data-ttu-id="dd4b6-572">two three</span><span class="sxs-lookup"><span data-stu-id="dd4b6-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="dd4b6-573">take</span><span class="sxs-lookup"><span data-stu-id="dd4b6-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="dd4b6-574">Здравствуйте, возвращает массив с hello указанное число элементов от начала массива hello, или строка с hello указанное число символов от начала hello строку hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-575">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-575">Parameters</span></span>

| <span data-ttu-id="dd4b6-576">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-576">Parameter</span></span> | <span data-ttu-id="dd4b6-577">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-577">Required</span></span> | <span data-ttu-id="dd4b6-578">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-578">Type</span></span> | <span data-ttu-id="dd4b6-579">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="dd4b6-580">originalValue</span></span> |<span data-ttu-id="dd4b6-581">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-581">Yes</span></span> |<span data-ttu-id="dd4b6-582">массив или строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-582">array or string</span></span> |<span data-ttu-id="dd4b6-583">Здравствуйте, массиву или строке tootake hello элементы.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="dd4b6-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="dd4b6-584">numberToTake</span></span> |<span data-ttu-id="dd4b6-585">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-585">Yes</span></span> |<span data-ttu-id="dd4b6-586">int</span><span class="sxs-lookup"><span data-stu-id="dd4b6-586">int</span></span> |<span data-ttu-id="dd4b6-587">количество элементов или символы tootake Hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="dd4b6-588">Если это значение меньше или равно 0, то возвращается пустой массив или строка.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="dd4b6-589">Если это больше, чем длина заданного массива или строка hello hello, возвращаются все элементы hello hello массиву или строке.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-590">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-590">Return value</span></span>

<span data-ttu-id="dd4b6-591">Массив или строка.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-592">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-592">Example</span></span>

<span data-ttu-id="dd4b6-593">Следующий пример принимает hello Hello заданное число элементов из массива hello и символов из строки.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="dd4b6-594">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-595">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-595">Name</span></span> | <span data-ttu-id="dd4b6-596">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-596">Type</span></span> | <span data-ttu-id="dd4b6-597">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-598">arrayOutput</span></span> | <span data-ttu-id="dd4b6-599">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-599">Array</span></span> | <span data-ttu-id="dd4b6-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-600">["one", "two"]</span></span> |
| <span data-ttu-id="dd4b6-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-601">stringOutput</span></span> | <span data-ttu-id="dd4b6-602">Строка</span><span class="sxs-lookup"><span data-stu-id="dd4b6-602">String</span></span> | <span data-ttu-id="dd4b6-603">on</span><span class="sxs-lookup"><span data-stu-id="dd4b6-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="dd4b6-604">union</span><span class="sxs-lookup"><span data-stu-id="dd4b6-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="dd4b6-605">Возвращает массив или объект со всеми элементами на основе параметров hello.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="dd4b6-606">Повторяющиеся значения или ключи включаются только один раз.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="dd4b6-607">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd4b6-607">Parameters</span></span>

| <span data-ttu-id="dd4b6-608">Параметр</span><span class="sxs-lookup"><span data-stu-id="dd4b6-608">Parameter</span></span> | <span data-ttu-id="dd4b6-609">Обязательно</span><span class="sxs-lookup"><span data-stu-id="dd4b6-609">Required</span></span> | <span data-ttu-id="dd4b6-610">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-610">Type</span></span> | <span data-ttu-id="dd4b6-611">Описание</span><span class="sxs-lookup"><span data-stu-id="dd4b6-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="dd4b6-612">arg1</span><span class="sxs-lookup"><span data-stu-id="dd4b6-612">arg1</span></span> |<span data-ttu-id="dd4b6-613">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-613">Yes</span></span> |<span data-ttu-id="dd4b6-614">массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-614">array or object</span></span> |<span data-ttu-id="dd4b6-615">Hello первый toouse значение для объединения элементов.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="dd4b6-616">arg2</span><span class="sxs-lookup"><span data-stu-id="dd4b6-616">arg2</span></span> |<span data-ttu-id="dd4b6-617">Да</span><span class="sxs-lookup"><span data-stu-id="dd4b6-617">Yes</span></span> |<span data-ttu-id="dd4b6-618">массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-618">array or object</span></span> |<span data-ttu-id="dd4b6-619">Hello второй toouse значение для объединения элементов.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="dd4b6-620">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="dd4b6-620">additional arguments</span></span> |<span data-ttu-id="dd4b6-621">Нет</span><span class="sxs-lookup"><span data-stu-id="dd4b6-621">No</span></span> |<span data-ttu-id="dd4b6-622">массив или объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-622">array or object</span></span> |<span data-ttu-id="dd4b6-623">Дополнительные значения toouse для объединения элементов.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="dd4b6-624">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-624">Return value</span></span>

<span data-ttu-id="dd4b6-625">Массив или объект.</span><span class="sxs-lookup"><span data-stu-id="dd4b6-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="dd4b6-626">Пример</span><span class="sxs-lookup"><span data-stu-id="dd4b6-626">Example</span></span>

<span data-ttu-id="dd4b6-627">Следующий пример показывает, как массивы toouse объединения с Hello и объектов:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-627">hello following example shows how toouse union with arrays and objects:</span></span>

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

<span data-ttu-id="dd4b6-628">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="dd4b6-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="dd4b6-629">Имя</span><span class="sxs-lookup"><span data-stu-id="dd4b6-629">Name</span></span> | <span data-ttu-id="dd4b6-630">Тип</span><span class="sxs-lookup"><span data-stu-id="dd4b6-630">Type</span></span> | <span data-ttu-id="dd4b6-631">Значение</span><span class="sxs-lookup"><span data-stu-id="dd4b6-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="dd4b6-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-632">objectOutput</span></span> | <span data-ttu-id="dd4b6-633">Объект</span><span class="sxs-lookup"><span data-stu-id="dd4b6-633">Object</span></span> | <span data-ttu-id="dd4b6-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="dd4b6-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="dd4b6-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="dd4b6-635">arrayOutput</span></span> | <span data-ttu-id="dd4b6-636">Массив,</span><span class="sxs-lookup"><span data-stu-id="dd4b6-636">Array</span></span> | <span data-ttu-id="dd4b6-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="dd4b6-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dd4b6-638">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd4b6-638">Next steps</span></span>
* <span data-ttu-id="dd4b6-639">Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dd4b6-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="dd4b6-640">toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dd4b6-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="dd4b6-641">tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="dd4b6-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="dd4b6-642">toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="dd4b6-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

