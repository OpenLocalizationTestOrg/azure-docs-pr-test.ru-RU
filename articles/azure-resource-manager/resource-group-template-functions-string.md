---
title: "Строковые функции шаблона Azure Resource Manager | Документация Майкрософт"
description: "Описывает функции, используемые в шаблоне Azure Resource Manager для работы со строками."
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
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="6730a-103">Строковые функции для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6730a-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="6730a-104">Диспетчер ресурсов предоставляет следующие функции для работы со строками:</span><span class="sxs-lookup"><span data-stu-id="6730a-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="6730a-105">base64</span><span class="sxs-lookup"><span data-stu-id="6730a-105">base64</span></span>](#base64)
* [<span data-ttu-id="6730a-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="6730a-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="6730a-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="6730a-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="6730a-108">concat</span><span class="sxs-lookup"><span data-stu-id="6730a-108">concat</span></span>](#concat)
* [<span data-ttu-id="6730a-109">contains</span><span class="sxs-lookup"><span data-stu-id="6730a-109">contains</span></span>](#contains)
* [<span data-ttu-id="6730a-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="6730a-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="6730a-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="6730a-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="6730a-112">empty</span><span class="sxs-lookup"><span data-stu-id="6730a-112">empty</span></span>](#empty)
* [<span data-ttu-id="6730a-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="6730a-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="6730a-114">first</span><span class="sxs-lookup"><span data-stu-id="6730a-114">first</span></span>](#first)
* [<span data-ttu-id="6730a-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="6730a-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="6730a-116">last</span><span class="sxs-lookup"><span data-stu-id="6730a-116">last</span></span>](#last)
* [<span data-ttu-id="6730a-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="6730a-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="6730a-118">длина</span><span class="sxs-lookup"><span data-stu-id="6730a-118">length</span></span>](#length)
* [<span data-ttu-id="6730a-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="6730a-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="6730a-120">replace</span><span class="sxs-lookup"><span data-stu-id="6730a-120">replace</span></span>](#replace)
* [<span data-ttu-id="6730a-121">skip</span><span class="sxs-lookup"><span data-stu-id="6730a-121">skip</span></span>](#skip)
* [<span data-ttu-id="6730a-122">split</span><span class="sxs-lookup"><span data-stu-id="6730a-122">split</span></span>](#split)
* [<span data-ttu-id="6730a-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="6730a-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="6730a-124">string</span><span class="sxs-lookup"><span data-stu-id="6730a-124">string</span></span>](#string)
* [<span data-ttu-id="6730a-125">substring</span><span class="sxs-lookup"><span data-stu-id="6730a-125">substring</span></span>](#substring)
* [<span data-ttu-id="6730a-126">take</span><span class="sxs-lookup"><span data-stu-id="6730a-126">take</span></span>](#take)
* [<span data-ttu-id="6730a-127">toLower</span><span class="sxs-lookup"><span data-stu-id="6730a-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="6730a-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="6730a-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="6730a-129">trim</span><span class="sxs-lookup"><span data-stu-id="6730a-129">trim</span></span>](#trim)
* [<span data-ttu-id="6730a-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="6730a-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="6730a-131">uri</span><span class="sxs-lookup"><span data-stu-id="6730a-131">uri</span></span>](#uri)
* [<span data-ttu-id="6730a-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="6730a-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="6730a-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="6730a-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="6730a-134">base64</span><span class="sxs-lookup"><span data-stu-id="6730a-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="6730a-135">Возвращает входную строку в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="6730a-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-136">Parameters</span></span>

| <span data-ttu-id="6730a-137">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-137">Parameter</span></span> | <span data-ttu-id="6730a-138">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-138">Required</span></span> | <span data-ttu-id="6730a-139">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-139">Type</span></span> | <span data-ttu-id="6730a-140">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-141">входная_строка</span><span class="sxs-lookup"><span data-stu-id="6730a-141">inputString</span></span> |<span data-ttu-id="6730a-142">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-142">Yes</span></span> |<span data-ttu-id="6730a-143">string</span><span class="sxs-lookup"><span data-stu-id="6730a-143">string</span></span> |<span data-ttu-id="6730a-144">Значение, которое нужно вернуть в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="6730a-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-145">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-145">Return value</span></span>

<span data-ttu-id="6730a-146">Строка, содержащая представление в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="6730a-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-147">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-147">Examples</span></span>

<span data-ttu-id="6730a-148">В следующем примере показано, как использовать функцию base64.</span><span class="sxs-lookup"><span data-stu-id="6730a-148">The following example shows how to use the base64 function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="6730a-149">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-150">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-150">Name</span></span> | <span data-ttu-id="6730a-151">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-151">Type</span></span> | <span data-ttu-id="6730a-152">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="6730a-153">base64Output</span></span> | <span data-ttu-id="6730a-154">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-154">String</span></span> | <span data-ttu-id="6730a-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="6730a-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="6730a-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-156">toStringOutput</span></span> | <span data-ttu-id="6730a-157">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-157">String</span></span> | <span data-ttu-id="6730a-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="6730a-158">one, two, three</span></span> |
| <span data-ttu-id="6730a-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-159">toJsonOutput</span></span> | <span data-ttu-id="6730a-160">Объект</span><span class="sxs-lookup"><span data-stu-id="6730a-160">Object</span></span> | <span data-ttu-id="6730a-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="6730a-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="6730a-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="6730a-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="6730a-163">Преобразует представление в кодировке base64 в объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6730a-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-164">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-164">Parameters</span></span>

| <span data-ttu-id="6730a-165">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-165">Parameter</span></span> | <span data-ttu-id="6730a-166">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-166">Required</span></span> | <span data-ttu-id="6730a-167">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-167">Type</span></span> | <span data-ttu-id="6730a-168">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="6730a-169">base64Value</span></span> |<span data-ttu-id="6730a-170">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-170">Yes</span></span> |<span data-ttu-id="6730a-171">string</span><span class="sxs-lookup"><span data-stu-id="6730a-171">string</span></span> |<span data-ttu-id="6730a-172">Представление в кодировке base64, которое необходимо преобразовать в объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6730a-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-173">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-173">Return value</span></span>

<span data-ttu-id="6730a-174">Объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6730a-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-175">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-175">Examples</span></span>

<span data-ttu-id="6730a-176">В следующем примере функция base64ToJson используется для преобразования значения в кодировке base64:</span><span class="sxs-lookup"><span data-stu-id="6730a-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="6730a-177">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-178">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-178">Name</span></span> | <span data-ttu-id="6730a-179">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-179">Type</span></span> | <span data-ttu-id="6730a-180">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="6730a-181">base64Output</span></span> | <span data-ttu-id="6730a-182">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-182">String</span></span> | <span data-ttu-id="6730a-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="6730a-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="6730a-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-184">toStringOutput</span></span> | <span data-ttu-id="6730a-185">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-185">String</span></span> | <span data-ttu-id="6730a-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="6730a-186">one, two, three</span></span> |
| <span data-ttu-id="6730a-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-187">toJsonOutput</span></span> | <span data-ttu-id="6730a-188">Объект</span><span class="sxs-lookup"><span data-stu-id="6730a-188">Object</span></span> | <span data-ttu-id="6730a-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="6730a-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="6730a-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="6730a-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="6730a-191">Преобразует представление в кодировке base64 в строку.</span><span class="sxs-lookup"><span data-stu-id="6730a-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-192">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-192">Parameters</span></span>

| <span data-ttu-id="6730a-193">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-193">Parameter</span></span> | <span data-ttu-id="6730a-194">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-194">Required</span></span> | <span data-ttu-id="6730a-195">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-195">Type</span></span> | <span data-ttu-id="6730a-196">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="6730a-197">base64Value</span></span> |<span data-ttu-id="6730a-198">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-198">Yes</span></span> |<span data-ttu-id="6730a-199">string</span><span class="sxs-lookup"><span data-stu-id="6730a-199">string</span></span> |<span data-ttu-id="6730a-200">Представление в кодировке base64, которое необходимо преобразовать в строку.</span><span class="sxs-lookup"><span data-stu-id="6730a-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-201">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-201">Return value</span></span>

<span data-ttu-id="6730a-202">Строка преобразованного значения в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="6730a-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-203">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-203">Examples</span></span>

<span data-ttu-id="6730a-204">В следующем примере функция base64ToString используется для преобразования значения в кодировке base64:</span><span class="sxs-lookup"><span data-stu-id="6730a-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="6730a-205">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-206">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-206">Name</span></span> | <span data-ttu-id="6730a-207">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-207">Type</span></span> | <span data-ttu-id="6730a-208">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="6730a-209">base64Output</span></span> | <span data-ttu-id="6730a-210">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-210">String</span></span> | <span data-ttu-id="6730a-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="6730a-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="6730a-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-212">toStringOutput</span></span> | <span data-ttu-id="6730a-213">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-213">String</span></span> | <span data-ttu-id="6730a-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="6730a-214">one, two, three</span></span> |
| <span data-ttu-id="6730a-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-215">toJsonOutput</span></span> | <span data-ttu-id="6730a-216">Объект</span><span class="sxs-lookup"><span data-stu-id="6730a-216">Object</span></span> | <span data-ttu-id="6730a-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="6730a-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="6730a-218">concat</span><span class="sxs-lookup"><span data-stu-id="6730a-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="6730a-219">Объединяет несколько строковых значений и возвращает объединенную строку или объединяет несколько массивов и возвращает объединенный массив.</span><span class="sxs-lookup"><span data-stu-id="6730a-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-220">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-220">Parameters</span></span>

| <span data-ttu-id="6730a-221">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-221">Parameter</span></span> | <span data-ttu-id="6730a-222">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-222">Required</span></span> | <span data-ttu-id="6730a-223">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-223">Type</span></span> | <span data-ttu-id="6730a-224">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-225">arg1</span><span class="sxs-lookup"><span data-stu-id="6730a-225">arg1</span></span> |<span data-ttu-id="6730a-226">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-226">Yes</span></span> |<span data-ttu-id="6730a-227">строка или массив</span><span class="sxs-lookup"><span data-stu-id="6730a-227">string or array</span></span> |<span data-ttu-id="6730a-228">Первое значение для сцепки.</span><span class="sxs-lookup"><span data-stu-id="6730a-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="6730a-229">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="6730a-229">additional arguments</span></span> |<span data-ttu-id="6730a-230">Нет</span><span class="sxs-lookup"><span data-stu-id="6730a-230">No</span></span> |<span data-ttu-id="6730a-231">string</span><span class="sxs-lookup"><span data-stu-id="6730a-231">string</span></span> |<span data-ttu-id="6730a-232">Дополнительные значения в последовательном порядке для сцепки.</span><span class="sxs-lookup"><span data-stu-id="6730a-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-233">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-233">Return value</span></span>
<span data-ttu-id="6730a-234">Строка или массив объединенных значений.</span><span class="sxs-lookup"><span data-stu-id="6730a-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-235">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-235">Examples</span></span>

<span data-ttu-id="6730a-236">В следующем примере показано, как объединить два строковых значения и получить объединенную строку.</span><span class="sxs-lookup"><span data-stu-id="6730a-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="6730a-237">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-238">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-238">Name</span></span> | <span data-ttu-id="6730a-239">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-239">Type</span></span> | <span data-ttu-id="6730a-240">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-241">concatOutput</span></span> | <span data-ttu-id="6730a-242">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-242">String</span></span> | <span data-ttu-id="6730a-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="6730a-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="6730a-244">В следующем примере показано, как объединить два массива.</span><span class="sxs-lookup"><span data-stu-id="6730a-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="6730a-245">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-246">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-246">Name</span></span> | <span data-ttu-id="6730a-247">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-247">Type</span></span> | <span data-ttu-id="6730a-248">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-249">return</span><span class="sxs-lookup"><span data-stu-id="6730a-249">return</span></span> | <span data-ttu-id="6730a-250">Массив,</span><span class="sxs-lookup"><span data-stu-id="6730a-250">Array</span></span> | <span data-ttu-id="6730a-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="6730a-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="6730a-252">contains</span><span class="sxs-lookup"><span data-stu-id="6730a-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="6730a-253">Проверяет, содержит ли массив значение, содержит ли объект ключ или содержит ли строка подстроку.</span><span class="sxs-lookup"><span data-stu-id="6730a-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-254">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-254">Parameters</span></span>

| <span data-ttu-id="6730a-255">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-255">Parameter</span></span> | <span data-ttu-id="6730a-256">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-256">Required</span></span> | <span data-ttu-id="6730a-257">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-257">Type</span></span> | <span data-ttu-id="6730a-258">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-259">container</span><span class="sxs-lookup"><span data-stu-id="6730a-259">container</span></span> |<span data-ttu-id="6730a-260">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-260">Yes</span></span> |<span data-ttu-id="6730a-261">массив, объект или строка</span><span class="sxs-lookup"><span data-stu-id="6730a-261">array, object, or string</span></span> |<span data-ttu-id="6730a-262">Значение, содержащее значение, которое необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="6730a-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="6730a-263">itemToFind</span></span> |<span data-ttu-id="6730a-264">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-264">Yes</span></span> |<span data-ttu-id="6730a-265">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="6730a-265">string or int</span></span> |<span data-ttu-id="6730a-266">Значение, которое необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-267">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-267">Return value</span></span>

<span data-ttu-id="6730a-268">**True**, если элемент найден. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="6730a-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-269">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-269">Examples</span></span>

<span data-ttu-id="6730a-270">В следующем примере показано, как использовать функцию contains с различными типами:</span><span class="sxs-lookup"><span data-stu-id="6730a-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="6730a-271">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-272">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-272">Name</span></span> | <span data-ttu-id="6730a-273">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-273">Type</span></span> | <span data-ttu-id="6730a-274">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-275">stringTrue</span></span> | <span data-ttu-id="6730a-276">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-276">Bool</span></span> | <span data-ttu-id="6730a-277">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-277">True</span></span> |
| <span data-ttu-id="6730a-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="6730a-278">stringFalse</span></span> | <span data-ttu-id="6730a-279">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-279">Bool</span></span> | <span data-ttu-id="6730a-280">Ложь</span><span class="sxs-lookup"><span data-stu-id="6730a-280">False</span></span> |
| <span data-ttu-id="6730a-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-281">objectTrue</span></span> | <span data-ttu-id="6730a-282">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-282">Bool</span></span> | <span data-ttu-id="6730a-283">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-283">True</span></span> |
| <span data-ttu-id="6730a-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="6730a-284">objectFalse</span></span> | <span data-ttu-id="6730a-285">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-285">Bool</span></span> | <span data-ttu-id="6730a-286">Ложь</span><span class="sxs-lookup"><span data-stu-id="6730a-286">False</span></span> |
| <span data-ttu-id="6730a-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-287">arrayTrue</span></span> | <span data-ttu-id="6730a-288">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-288">Bool</span></span> | <span data-ttu-id="6730a-289">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-289">True</span></span> |
| <span data-ttu-id="6730a-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="6730a-290">arrayFalse</span></span> | <span data-ttu-id="6730a-291">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-291">Bool</span></span> | <span data-ttu-id="6730a-292">Ложь</span><span class="sxs-lookup"><span data-stu-id="6730a-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="6730a-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="6730a-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="6730a-294">Преобразует значение в универсальный код ресурса (URI) данных.</span><span class="sxs-lookup"><span data-stu-id="6730a-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-295">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-295">Parameters</span></span>

| <span data-ttu-id="6730a-296">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-296">Parameter</span></span> | <span data-ttu-id="6730a-297">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-297">Required</span></span> | <span data-ttu-id="6730a-298">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-298">Type</span></span> | <span data-ttu-id="6730a-299">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="6730a-300">stringToConvert</span></span> |<span data-ttu-id="6730a-301">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-301">Yes</span></span> |<span data-ttu-id="6730a-302">string</span><span class="sxs-lookup"><span data-stu-id="6730a-302">string</span></span> |<span data-ttu-id="6730a-303">Значение, которое необходимо преобразовать в URI данных.</span><span class="sxs-lookup"><span data-stu-id="6730a-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-304">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-304">Return value</span></span>

<span data-ttu-id="6730a-305">Строка в формате URI данных.</span><span class="sxs-lookup"><span data-stu-id="6730a-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-306">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-306">Examples</span></span>

<span data-ttu-id="6730a-307">В следующем примере значение преобразуется в URI данных, а URI данных преобразуется в строку:</span><span class="sxs-lookup"><span data-stu-id="6730a-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="6730a-308">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-309">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-309">Name</span></span> | <span data-ttu-id="6730a-310">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-310">Type</span></span> | <span data-ttu-id="6730a-311">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-312">dataUriOutput</span></span> | <span data-ttu-id="6730a-313">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-313">String</span></span> | <span data-ttu-id="6730a-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="6730a-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="6730a-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-315">toStringOutput</span></span> | <span data-ttu-id="6730a-316">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-316">String</span></span> | <span data-ttu-id="6730a-317">Привет, мир!</span><span class="sxs-lookup"><span data-stu-id="6730a-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="6730a-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="6730a-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="6730a-319">Преобразует значение в формате URI данных в строку.</span><span class="sxs-lookup"><span data-stu-id="6730a-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-320">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-320">Parameters</span></span>

| <span data-ttu-id="6730a-321">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-321">Parameter</span></span> | <span data-ttu-id="6730a-322">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-322">Required</span></span> | <span data-ttu-id="6730a-323">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-323">Type</span></span> | <span data-ttu-id="6730a-324">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="6730a-325">dataUriToConvert</span></span> |<span data-ttu-id="6730a-326">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-326">Yes</span></span> |<span data-ttu-id="6730a-327">string</span><span class="sxs-lookup"><span data-stu-id="6730a-327">string</span></span> |<span data-ttu-id="6730a-328">Значение URI данных, которое необходимо преобразовать.</span><span class="sxs-lookup"><span data-stu-id="6730a-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-329">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-329">Return value</span></span>

<span data-ttu-id="6730a-330">Строка, содержащая преобразованное значение.</span><span class="sxs-lookup"><span data-stu-id="6730a-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-331">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-331">Examples</span></span>

<span data-ttu-id="6730a-332">В следующем примере значение преобразуется в URI данных, а URI данных преобразуется в строку:</span><span class="sxs-lookup"><span data-stu-id="6730a-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="6730a-333">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-334">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-334">Name</span></span> | <span data-ttu-id="6730a-335">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-335">Type</span></span> | <span data-ttu-id="6730a-336">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-337">dataUriOutput</span></span> | <span data-ttu-id="6730a-338">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-338">String</span></span> | <span data-ttu-id="6730a-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="6730a-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="6730a-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-340">toStringOutput</span></span> | <span data-ttu-id="6730a-341">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-341">String</span></span> | <span data-ttu-id="6730a-342">Привет, мир!</span><span class="sxs-lookup"><span data-stu-id="6730a-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="6730a-343">empty</span><span class="sxs-lookup"><span data-stu-id="6730a-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="6730a-344">Определяет, являются ли пустыми массив, объект или строка.</span><span class="sxs-lookup"><span data-stu-id="6730a-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-345">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-345">Parameters</span></span>

| <span data-ttu-id="6730a-346">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-346">Parameter</span></span> | <span data-ttu-id="6730a-347">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-347">Required</span></span> | <span data-ttu-id="6730a-348">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-348">Type</span></span> | <span data-ttu-id="6730a-349">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="6730a-350">itemToTest</span></span> |<span data-ttu-id="6730a-351">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-351">Yes</span></span> |<span data-ttu-id="6730a-352">массив, объект или строка</span><span class="sxs-lookup"><span data-stu-id="6730a-352">array, object, or string</span></span> |<span data-ttu-id="6730a-353">Значение, которое необходимо проверить на наличие содержимого.</span><span class="sxs-lookup"><span data-stu-id="6730a-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-354">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-354">Return value</span></span>

<span data-ttu-id="6730a-355">Возвращает результат **True**, если значение пустое. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="6730a-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-356">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-356">Examples</span></span>

<span data-ttu-id="6730a-357">В следующем примере проверяется, являются ли пустыми массив, объект и строка.</span><span class="sxs-lookup"><span data-stu-id="6730a-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="6730a-358">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-359">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-359">Name</span></span> | <span data-ttu-id="6730a-360">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-360">Type</span></span> | <span data-ttu-id="6730a-361">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="6730a-362">arrayEmpty</span></span> | <span data-ttu-id="6730a-363">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-363">Bool</span></span> | <span data-ttu-id="6730a-364">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-364">True</span></span> |
| <span data-ttu-id="6730a-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="6730a-365">objectEmpty</span></span> | <span data-ttu-id="6730a-366">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-366">Bool</span></span> | <span data-ttu-id="6730a-367">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-367">True</span></span> |
| <span data-ttu-id="6730a-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="6730a-368">stringEmpty</span></span> | <span data-ttu-id="6730a-369">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-369">Bool</span></span> | <span data-ttu-id="6730a-370">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="6730a-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="6730a-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="6730a-372">Определяет, заканчивается ли строка определенным значением.</span><span class="sxs-lookup"><span data-stu-id="6730a-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="6730a-373">При сравнении регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="6730a-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-374">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-374">Parameters</span></span>

| <span data-ttu-id="6730a-375">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-375">Parameter</span></span> | <span data-ttu-id="6730a-376">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-376">Required</span></span> | <span data-ttu-id="6730a-377">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-377">Type</span></span> | <span data-ttu-id="6730a-378">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="6730a-379">stringToSearch</span></span> |<span data-ttu-id="6730a-380">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-380">Yes</span></span> |<span data-ttu-id="6730a-381">string</span><span class="sxs-lookup"><span data-stu-id="6730a-381">string</span></span> |<span data-ttu-id="6730a-382">Значение, содержащее элемент, который необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="6730a-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="6730a-383">stringToFind</span></span> |<span data-ttu-id="6730a-384">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-384">Yes</span></span> |<span data-ttu-id="6730a-385">string</span><span class="sxs-lookup"><span data-stu-id="6730a-385">string</span></span> |<span data-ttu-id="6730a-386">Значение, которое необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-387">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-387">Return value</span></span>

<span data-ttu-id="6730a-388">**True**, если последний знак или знаки строки соответствуют значению. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="6730a-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-389">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-389">Examples</span></span>

<span data-ttu-id="6730a-390">В следующем примере показано, как использовать функции startsWith и endsWith:</span><span class="sxs-lookup"><span data-stu-id="6730a-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="6730a-391">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-392">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-392">Name</span></span> | <span data-ttu-id="6730a-393">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-393">Type</span></span> | <span data-ttu-id="6730a-394">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-395">startsTrue</span></span> | <span data-ttu-id="6730a-396">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-396">Bool</span></span> | <span data-ttu-id="6730a-397">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-397">True</span></span> |
| <span data-ttu-id="6730a-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-398">startsCapTrue</span></span> | <span data-ttu-id="6730a-399">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-399">Bool</span></span> | <span data-ttu-id="6730a-400">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-400">True</span></span> |
| <span data-ttu-id="6730a-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="6730a-401">startsFalse</span></span> | <span data-ttu-id="6730a-402">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-402">Bool</span></span> | <span data-ttu-id="6730a-403">Ложь</span><span class="sxs-lookup"><span data-stu-id="6730a-403">False</span></span> |
| <span data-ttu-id="6730a-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-404">endsTrue</span></span> | <span data-ttu-id="6730a-405">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-405">Bool</span></span> | <span data-ttu-id="6730a-406">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-406">True</span></span> |
| <span data-ttu-id="6730a-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-407">endsCapTrue</span></span> | <span data-ttu-id="6730a-408">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-408">Bool</span></span> | <span data-ttu-id="6730a-409">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-409">True</span></span> |
| <span data-ttu-id="6730a-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="6730a-410">endsFalse</span></span> | <span data-ttu-id="6730a-411">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-411">Bool</span></span> | <span data-ttu-id="6730a-412">Ложь</span><span class="sxs-lookup"><span data-stu-id="6730a-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="6730a-413">first</span><span class="sxs-lookup"><span data-stu-id="6730a-413">first</span></span>
`first(arg1)`

<span data-ttu-id="6730a-414">Возвращает первый знак строки или первый элемент массива.</span><span class="sxs-lookup"><span data-stu-id="6730a-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-415">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-415">Parameters</span></span>

| <span data-ttu-id="6730a-416">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-416">Parameter</span></span> | <span data-ttu-id="6730a-417">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-417">Required</span></span> | <span data-ttu-id="6730a-418">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-418">Type</span></span> | <span data-ttu-id="6730a-419">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-420">arg1</span><span class="sxs-lookup"><span data-stu-id="6730a-420">arg1</span></span> |<span data-ttu-id="6730a-421">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-421">Yes</span></span> |<span data-ttu-id="6730a-422">массив или строка</span><span class="sxs-lookup"><span data-stu-id="6730a-422">array or string</span></span> |<span data-ttu-id="6730a-423">Значение, из которого необходимо извлечь первый элемент или знак.</span><span class="sxs-lookup"><span data-stu-id="6730a-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-424">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-424">Return value</span></span>

<span data-ttu-id="6730a-425">Строка первого знака или тип (строка, целое число, массив или объект) первого элемента в массиве.</span><span class="sxs-lookup"><span data-stu-id="6730a-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-426">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-426">Examples</span></span>

<span data-ttu-id="6730a-427">В следующем примере показано, как использовать функцию first с массивом и строкой:</span><span class="sxs-lookup"><span data-stu-id="6730a-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="6730a-428">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-429">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-429">Name</span></span> | <span data-ttu-id="6730a-430">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-430">Type</span></span> | <span data-ttu-id="6730a-431">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-432">arrayOutput</span></span> | <span data-ttu-id="6730a-433">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-433">String</span></span> | <span data-ttu-id="6730a-434">one</span><span class="sxs-lookup"><span data-stu-id="6730a-434">one</span></span> |
| <span data-ttu-id="6730a-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-435">stringOutput</span></span> | <span data-ttu-id="6730a-436">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-436">String</span></span> | <span data-ttu-id="6730a-437">O</span><span class="sxs-lookup"><span data-stu-id="6730a-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="6730a-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="6730a-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="6730a-439">Возвращает первую позицию значения в строке.</span><span class="sxs-lookup"><span data-stu-id="6730a-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="6730a-440">При сравнении регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="6730a-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-441">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-441">Parameters</span></span>

| <span data-ttu-id="6730a-442">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-442">Parameter</span></span> | <span data-ttu-id="6730a-443">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-443">Required</span></span> | <span data-ttu-id="6730a-444">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-444">Type</span></span> | <span data-ttu-id="6730a-445">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="6730a-446">stringToSearch</span></span> |<span data-ttu-id="6730a-447">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-447">Yes</span></span> |<span data-ttu-id="6730a-448">string</span><span class="sxs-lookup"><span data-stu-id="6730a-448">string</span></span> |<span data-ttu-id="6730a-449">Значение, содержащее элемент, который необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="6730a-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="6730a-450">stringToFind</span></span> |<span data-ttu-id="6730a-451">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-451">Yes</span></span> |<span data-ttu-id="6730a-452">string</span><span class="sxs-lookup"><span data-stu-id="6730a-452">string</span></span> |<span data-ttu-id="6730a-453">Значение, которое необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-454">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-454">Return value</span></span>

<span data-ttu-id="6730a-455">Целое число, представляющее позицию искомого элемента.</span><span class="sxs-lookup"><span data-stu-id="6730a-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="6730a-456">Значение отсчитывается, начиная с нуля.</span><span class="sxs-lookup"><span data-stu-id="6730a-456">The value is zero-based.</span></span> <span data-ttu-id="6730a-457">Если элемент не найден, то возвращается значение -1.</span><span class="sxs-lookup"><span data-stu-id="6730a-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-458">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-458">Examples</span></span>

<span data-ttu-id="6730a-459">В следующем примере показано, как использовать функции indexOf и lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="6730a-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="6730a-460">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-461">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-461">Name</span></span> | <span data-ttu-id="6730a-462">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-462">Type</span></span> | <span data-ttu-id="6730a-463">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-464">firstT</span><span class="sxs-lookup"><span data-stu-id="6730a-464">firstT</span></span> | <span data-ttu-id="6730a-465">int</span><span class="sxs-lookup"><span data-stu-id="6730a-465">Int</span></span> | <span data-ttu-id="6730a-466">0</span><span class="sxs-lookup"><span data-stu-id="6730a-466">0</span></span> |
| <span data-ttu-id="6730a-467">lastT</span><span class="sxs-lookup"><span data-stu-id="6730a-467">lastT</span></span> | <span data-ttu-id="6730a-468">int</span><span class="sxs-lookup"><span data-stu-id="6730a-468">Int</span></span> | <span data-ttu-id="6730a-469">3</span><span class="sxs-lookup"><span data-stu-id="6730a-469">3</span></span> |
| <span data-ttu-id="6730a-470">firstString</span><span class="sxs-lookup"><span data-stu-id="6730a-470">firstString</span></span> | <span data-ttu-id="6730a-471">int</span><span class="sxs-lookup"><span data-stu-id="6730a-471">Int</span></span> | <span data-ttu-id="6730a-472">2</span><span class="sxs-lookup"><span data-stu-id="6730a-472">2</span></span> |
| <span data-ttu-id="6730a-473">lastString</span><span class="sxs-lookup"><span data-stu-id="6730a-473">lastString</span></span> | <span data-ttu-id="6730a-474">int</span><span class="sxs-lookup"><span data-stu-id="6730a-474">Int</span></span> | <span data-ttu-id="6730a-475">0</span><span class="sxs-lookup"><span data-stu-id="6730a-475">0</span></span> |
| <span data-ttu-id="6730a-476">notFound</span><span class="sxs-lookup"><span data-stu-id="6730a-476">notFound</span></span> | <span data-ttu-id="6730a-477">int</span><span class="sxs-lookup"><span data-stu-id="6730a-477">Int</span></span> | <span data-ttu-id="6730a-478">-1</span><span class="sxs-lookup"><span data-stu-id="6730a-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="6730a-479">last</span><span class="sxs-lookup"><span data-stu-id="6730a-479">last</span></span>
`last (arg1)`

<span data-ttu-id="6730a-480">Возвращает последний знак строки или последний элемент массива.</span><span class="sxs-lookup"><span data-stu-id="6730a-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-481">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-481">Parameters</span></span>

| <span data-ttu-id="6730a-482">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-482">Parameter</span></span> | <span data-ttu-id="6730a-483">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-483">Required</span></span> | <span data-ttu-id="6730a-484">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-484">Type</span></span> | <span data-ttu-id="6730a-485">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-486">arg1</span><span class="sxs-lookup"><span data-stu-id="6730a-486">arg1</span></span> |<span data-ttu-id="6730a-487">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-487">Yes</span></span> |<span data-ttu-id="6730a-488">массив или строка</span><span class="sxs-lookup"><span data-stu-id="6730a-488">array or string</span></span> |<span data-ttu-id="6730a-489">Значение, из которого необходимо извлечь последний элемент или знак.</span><span class="sxs-lookup"><span data-stu-id="6730a-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-490">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-490">Return value</span></span>

<span data-ttu-id="6730a-491">Строка последнего знака или тип (строка, целое число, массив или объект) последнего элемента в массиве.</span><span class="sxs-lookup"><span data-stu-id="6730a-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-492">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-492">Examples</span></span>

<span data-ttu-id="6730a-493">В следующем примере показано, как использовать функцию last с массивом и строкой:</span><span class="sxs-lookup"><span data-stu-id="6730a-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="6730a-494">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-495">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-495">Name</span></span> | <span data-ttu-id="6730a-496">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-496">Type</span></span> | <span data-ttu-id="6730a-497">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-498">arrayOutput</span></span> | <span data-ttu-id="6730a-499">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-499">String</span></span> | <span data-ttu-id="6730a-500">three</span><span class="sxs-lookup"><span data-stu-id="6730a-500">three</span></span> |
| <span data-ttu-id="6730a-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-501">stringOutput</span></span> | <span data-ttu-id="6730a-502">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-502">String</span></span> | <span data-ttu-id="6730a-503">e</span><span class="sxs-lookup"><span data-stu-id="6730a-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="6730a-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="6730a-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="6730a-505">Возвращает последнюю позицию значения в строке.</span><span class="sxs-lookup"><span data-stu-id="6730a-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="6730a-506">При сравнении регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="6730a-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-507">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-507">Parameters</span></span>

| <span data-ttu-id="6730a-508">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-508">Parameter</span></span> | <span data-ttu-id="6730a-509">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-509">Required</span></span> | <span data-ttu-id="6730a-510">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-510">Type</span></span> | <span data-ttu-id="6730a-511">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="6730a-512">stringToSearch</span></span> |<span data-ttu-id="6730a-513">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-513">Yes</span></span> |<span data-ttu-id="6730a-514">string</span><span class="sxs-lookup"><span data-stu-id="6730a-514">string</span></span> |<span data-ttu-id="6730a-515">Значение, содержащее элемент, который необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="6730a-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="6730a-516">stringToFind</span></span> |<span data-ttu-id="6730a-517">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-517">Yes</span></span> |<span data-ttu-id="6730a-518">string</span><span class="sxs-lookup"><span data-stu-id="6730a-518">string</span></span> |<span data-ttu-id="6730a-519">Значение, которое необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-520">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-520">Return value</span></span>

<span data-ttu-id="6730a-521">Целое число, представляющее последнюю позицию искомого элемента.</span><span class="sxs-lookup"><span data-stu-id="6730a-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="6730a-522">Значение отсчитывается, начиная с нуля.</span><span class="sxs-lookup"><span data-stu-id="6730a-522">The value is zero-based.</span></span> <span data-ttu-id="6730a-523">Если элемент не найден, то возвращается значение -1.</span><span class="sxs-lookup"><span data-stu-id="6730a-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-524">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-524">Examples</span></span>

<span data-ttu-id="6730a-525">В следующем примере показано, как использовать функции indexOf и lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="6730a-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="6730a-526">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-527">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-527">Name</span></span> | <span data-ttu-id="6730a-528">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-528">Type</span></span> | <span data-ttu-id="6730a-529">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-530">firstT</span><span class="sxs-lookup"><span data-stu-id="6730a-530">firstT</span></span> | <span data-ttu-id="6730a-531">int</span><span class="sxs-lookup"><span data-stu-id="6730a-531">Int</span></span> | <span data-ttu-id="6730a-532">0</span><span class="sxs-lookup"><span data-stu-id="6730a-532">0</span></span> |
| <span data-ttu-id="6730a-533">lastT</span><span class="sxs-lookup"><span data-stu-id="6730a-533">lastT</span></span> | <span data-ttu-id="6730a-534">int</span><span class="sxs-lookup"><span data-stu-id="6730a-534">Int</span></span> | <span data-ttu-id="6730a-535">3</span><span class="sxs-lookup"><span data-stu-id="6730a-535">3</span></span> |
| <span data-ttu-id="6730a-536">firstString</span><span class="sxs-lookup"><span data-stu-id="6730a-536">firstString</span></span> | <span data-ttu-id="6730a-537">int</span><span class="sxs-lookup"><span data-stu-id="6730a-537">Int</span></span> | <span data-ttu-id="6730a-538">2</span><span class="sxs-lookup"><span data-stu-id="6730a-538">2</span></span> |
| <span data-ttu-id="6730a-539">lastString</span><span class="sxs-lookup"><span data-stu-id="6730a-539">lastString</span></span> | <span data-ttu-id="6730a-540">int</span><span class="sxs-lookup"><span data-stu-id="6730a-540">Int</span></span> | <span data-ttu-id="6730a-541">0</span><span class="sxs-lookup"><span data-stu-id="6730a-541">0</span></span> |
| <span data-ttu-id="6730a-542">notFound</span><span class="sxs-lookup"><span data-stu-id="6730a-542">notFound</span></span> | <span data-ttu-id="6730a-543">int</span><span class="sxs-lookup"><span data-stu-id="6730a-543">Int</span></span> | <span data-ttu-id="6730a-544">-1</span><span class="sxs-lookup"><span data-stu-id="6730a-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="6730a-545">длина</span><span class="sxs-lookup"><span data-stu-id="6730a-545">length</span></span>
`length(string)`

<span data-ttu-id="6730a-546">Возвращает число знаков в строке или элементов в массиве.</span><span class="sxs-lookup"><span data-stu-id="6730a-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-547">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-547">Parameters</span></span>

| <span data-ttu-id="6730a-548">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-548">Parameter</span></span> | <span data-ttu-id="6730a-549">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-549">Required</span></span> | <span data-ttu-id="6730a-550">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-550">Type</span></span> | <span data-ttu-id="6730a-551">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-552">arg1</span><span class="sxs-lookup"><span data-stu-id="6730a-552">arg1</span></span> |<span data-ttu-id="6730a-553">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-553">Yes</span></span> |<span data-ttu-id="6730a-554">массив или строка</span><span class="sxs-lookup"><span data-stu-id="6730a-554">array or string</span></span> |<span data-ttu-id="6730a-555">Массив, который необходимо использовать для получения числа элементов, или строка — для получения числа знаков.</span><span class="sxs-lookup"><span data-stu-id="6730a-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-556">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-556">Return value</span></span>

<span data-ttu-id="6730a-557">Целое число.</span><span class="sxs-lookup"><span data-stu-id="6730a-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="6730a-558">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-558">Examples</span></span>

<span data-ttu-id="6730a-559">В следующем примере показано, как использовать функцию length с массивом и строкой:</span><span class="sxs-lookup"><span data-stu-id="6730a-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="6730a-560">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-561">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-561">Name</span></span> | <span data-ttu-id="6730a-562">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-562">Type</span></span> | <span data-ttu-id="6730a-563">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="6730a-564">arrayLength</span></span> | <span data-ttu-id="6730a-565">int</span><span class="sxs-lookup"><span data-stu-id="6730a-565">Int</span></span> | <span data-ttu-id="6730a-566">3</span><span class="sxs-lookup"><span data-stu-id="6730a-566">3</span></span> |
| <span data-ttu-id="6730a-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="6730a-567">stringLength</span></span> | <span data-ttu-id="6730a-568">int</span><span class="sxs-lookup"><span data-stu-id="6730a-568">Int</span></span> | <span data-ttu-id="6730a-569">13.</span><span class="sxs-lookup"><span data-stu-id="6730a-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="6730a-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="6730a-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="6730a-571">Возвращает выровненную по правому краю строку, добавляя символы в левую часть до достижения общее указанной длины.</span><span class="sxs-lookup"><span data-stu-id="6730a-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-572">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-572">Parameters</span></span>

| <span data-ttu-id="6730a-573">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-573">Parameter</span></span> | <span data-ttu-id="6730a-574">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-574">Required</span></span> | <span data-ttu-id="6730a-575">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-575">Type</span></span> | <span data-ttu-id="6730a-576">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-577">значение_для_заполнения </span><span class="sxs-lookup"><span data-stu-id="6730a-577">valueToPad</span></span> |<span data-ttu-id="6730a-578">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-578">Yes</span></span> |<span data-ttu-id="6730a-579">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="6730a-579">string or int</span></span> |<span data-ttu-id="6730a-580">Значение, выравниваемое по правому краю.</span><span class="sxs-lookup"><span data-stu-id="6730a-580">The value to right-align.</span></span> |
| <span data-ttu-id="6730a-581">общая_длина</span><span class="sxs-lookup"><span data-stu-id="6730a-581">totalLength</span></span> |<span data-ttu-id="6730a-582">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-582">Yes</span></span> |<span data-ttu-id="6730a-583">int</span><span class="sxs-lookup"><span data-stu-id="6730a-583">int</span></span> |<span data-ttu-id="6730a-584">Общее число символов в возвращаемой строке.</span><span class="sxs-lookup"><span data-stu-id="6730a-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="6730a-585">символ_заполнения</span><span class="sxs-lookup"><span data-stu-id="6730a-585">paddingCharacter</span></span> |<span data-ttu-id="6730a-586">Нет</span><span class="sxs-lookup"><span data-stu-id="6730a-586">No</span></span> |<span data-ttu-id="6730a-587">один знак</span><span class="sxs-lookup"><span data-stu-id="6730a-587">single character</span></span> |<span data-ttu-id="6730a-588">Символ, используемый для заполнения левой части до достижения общей длины.</span><span class="sxs-lookup"><span data-stu-id="6730a-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="6730a-589">Значение по умолчанию — пробел.</span><span class="sxs-lookup"><span data-stu-id="6730a-589">The default value is a space.</span></span> |

<span data-ttu-id="6730a-590">Если длина исходной строки превышает число знаков для заполнения, то знаки не добавляются.</span><span class="sxs-lookup"><span data-stu-id="6730a-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="6730a-591">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-591">Return value</span></span>

<span data-ttu-id="6730a-592">Строка, содержащая по крайней мере число указанных знаков.</span><span class="sxs-lookup"><span data-stu-id="6730a-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-593">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-593">Examples</span></span>

<span data-ttu-id="6730a-594">В следующем примере показано, как заполнить указанное пользователем значение параметра, добавляя знак нуля до достижения общего числа знаков.</span><span class="sxs-lookup"><span data-stu-id="6730a-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

<span data-ttu-id="6730a-595">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-596">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-596">Name</span></span> | <span data-ttu-id="6730a-597">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-597">Type</span></span> | <span data-ttu-id="6730a-598">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-599">stringOutput</span></span> | <span data-ttu-id="6730a-600">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-600">String</span></span> | <span data-ttu-id="6730a-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="6730a-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="6730a-602">replace</span><span class="sxs-lookup"><span data-stu-id="6730a-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="6730a-603">Возвращает новую строку, в которой все экземпляры одной строки заменены другой строкой.</span><span class="sxs-lookup"><span data-stu-id="6730a-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-604">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-604">Parameters</span></span>

| <span data-ttu-id="6730a-605">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-605">Parameter</span></span> | <span data-ttu-id="6730a-606">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-606">Required</span></span> | <span data-ttu-id="6730a-607">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-607">Type</span></span> | <span data-ttu-id="6730a-608">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-609">исходная_строка</span><span class="sxs-lookup"><span data-stu-id="6730a-609">originalString</span></span> |<span data-ttu-id="6730a-610">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-610">Yes</span></span> |<span data-ttu-id="6730a-611">string</span><span class="sxs-lookup"><span data-stu-id="6730a-611">string</span></span> |<span data-ttu-id="6730a-612">Значение, в котором все экземпляры одной строки заменены другой строкой.</span><span class="sxs-lookup"><span data-stu-id="6730a-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="6730a-613">oldString</span><span class="sxs-lookup"><span data-stu-id="6730a-613">oldString</span></span> |<span data-ttu-id="6730a-614">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-614">Yes</span></span> |<span data-ttu-id="6730a-615">string</span><span class="sxs-lookup"><span data-stu-id="6730a-615">string</span></span> |<span data-ttu-id="6730a-616">Строка, которая удаляется из исходной строки.</span><span class="sxs-lookup"><span data-stu-id="6730a-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="6730a-617">newString</span><span class="sxs-lookup"><span data-stu-id="6730a-617">newString</span></span> |<span data-ttu-id="6730a-618">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-618">Yes</span></span> |<span data-ttu-id="6730a-619">string</span><span class="sxs-lookup"><span data-stu-id="6730a-619">string</span></span> |<span data-ttu-id="6730a-620">Строка, добавляемая вместо удаляемой строки.</span><span class="sxs-lookup"><span data-stu-id="6730a-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-621">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-621">Return value</span></span>

<span data-ttu-id="6730a-622">Строка с замененными знаками.</span><span class="sxs-lookup"><span data-stu-id="6730a-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-623">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-623">Examples</span></span>

<span data-ttu-id="6730a-624">В приведенном ниже примере показано, как удалить все тире из предоставленной пользователем строки и как заменить часть строки другой строкой.</span><span class="sxs-lookup"><span data-stu-id="6730a-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

<span data-ttu-id="6730a-625">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-626">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-626">Name</span></span> | <span data-ttu-id="6730a-627">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-627">Type</span></span> | <span data-ttu-id="6730a-628">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-629">firstOutput</span></span> | <span data-ttu-id="6730a-630">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-630">String</span></span> | <span data-ttu-id="6730a-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="6730a-631">1231231234</span></span> |
| <span data-ttu-id="6730a-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-632">secodeOutput</span></span> | <span data-ttu-id="6730a-633">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-633">String</span></span> | <span data-ttu-id="6730a-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="6730a-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="6730a-635">skip</span><span class="sxs-lookup"><span data-stu-id="6730a-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="6730a-636">Возвращает строку, содержащую все знаки из исходной строки, начиная с заданной позиции, или массив, содержащий все элементы из исходного массива, начиная с заданной позиции.</span><span class="sxs-lookup"><span data-stu-id="6730a-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-637">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-637">Parameters</span></span>

| <span data-ttu-id="6730a-638">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-638">Parameter</span></span> | <span data-ttu-id="6730a-639">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-639">Required</span></span> | <span data-ttu-id="6730a-640">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-640">Type</span></span> | <span data-ttu-id="6730a-641">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="6730a-642">originalValue</span></span> |<span data-ttu-id="6730a-643">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-643">Yes</span></span> |<span data-ttu-id="6730a-644">массив или строка</span><span class="sxs-lookup"><span data-stu-id="6730a-644">array or string</span></span> |<span data-ttu-id="6730a-645">Массив или строка, используемые для пропуска.</span><span class="sxs-lookup"><span data-stu-id="6730a-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="6730a-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="6730a-646">numberToSkip</span></span> |<span data-ttu-id="6730a-647">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-647">Yes</span></span> |<span data-ttu-id="6730a-648">int</span><span class="sxs-lookup"><span data-stu-id="6730a-648">int</span></span> |<span data-ttu-id="6730a-649">Число элементов или знаков, которые необходимо пропустить.</span><span class="sxs-lookup"><span data-stu-id="6730a-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="6730a-650">Если это значение меньше или равно 0, то возвращаются все элементы или знаки в значении.</span><span class="sxs-lookup"><span data-stu-id="6730a-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="6730a-651">Если это значение превышает длину массива или строки, то возвращается пустой массив или пустая строка.</span><span class="sxs-lookup"><span data-stu-id="6730a-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-652">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-652">Return value</span></span>

<span data-ttu-id="6730a-653">Массив или строка.</span><span class="sxs-lookup"><span data-stu-id="6730a-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-654">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-654">Examples</span></span>

<span data-ttu-id="6730a-655">В следующем примере пропускается заданное число элементов в массиве и заданное число знаков в строке.</span><span class="sxs-lookup"><span data-stu-id="6730a-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="6730a-656">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-657">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-657">Name</span></span> | <span data-ttu-id="6730a-658">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-658">Type</span></span> | <span data-ttu-id="6730a-659">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-660">arrayOutput</span></span> | <span data-ttu-id="6730a-661">Массив,</span><span class="sxs-lookup"><span data-stu-id="6730a-661">Array</span></span> | <span data-ttu-id="6730a-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="6730a-662">["three"]</span></span> |
| <span data-ttu-id="6730a-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-663">stringOutput</span></span> | <span data-ttu-id="6730a-664">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-664">String</span></span> | <span data-ttu-id="6730a-665">two three</span><span class="sxs-lookup"><span data-stu-id="6730a-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="6730a-666">split</span><span class="sxs-lookup"><span data-stu-id="6730a-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="6730a-667">Возвращает массив строк, содержащий подстроки входной строки, разделенные переданными разделителями.</span><span class="sxs-lookup"><span data-stu-id="6730a-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-668">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-668">Parameters</span></span>

| <span data-ttu-id="6730a-669">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-669">Parameter</span></span> | <span data-ttu-id="6730a-670">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-670">Required</span></span> | <span data-ttu-id="6730a-671">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-671">Type</span></span> | <span data-ttu-id="6730a-672">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-673">входная_строка</span><span class="sxs-lookup"><span data-stu-id="6730a-673">inputString</span></span> |<span data-ttu-id="6730a-674">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-674">Yes</span></span> |<span data-ttu-id="6730a-675">string</span><span class="sxs-lookup"><span data-stu-id="6730a-675">string</span></span> |<span data-ttu-id="6730a-676">Строка для разделения.</span><span class="sxs-lookup"><span data-stu-id="6730a-676">The string to split.</span></span> |
| <span data-ttu-id="6730a-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="6730a-677">delimiter</span></span> |<span data-ttu-id="6730a-678">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-678">Yes</span></span> |<span data-ttu-id="6730a-679">строка или массив строк</span><span class="sxs-lookup"><span data-stu-id="6730a-679">string or array of strings</span></span> |<span data-ttu-id="6730a-680">Разделитель для разбиения строки.</span><span class="sxs-lookup"><span data-stu-id="6730a-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-681">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-681">Return value</span></span>

<span data-ttu-id="6730a-682">Массив строк.</span><span class="sxs-lookup"><span data-stu-id="6730a-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-683">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-683">Examples</span></span>

<span data-ttu-id="6730a-684">В следующем примере входная строка разбивается с помощью запятой или точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="6730a-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

<span data-ttu-id="6730a-685">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-686">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-686">Name</span></span> | <span data-ttu-id="6730a-687">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-687">Type</span></span> | <span data-ttu-id="6730a-688">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-689">firstOutput</span></span> | <span data-ttu-id="6730a-690">Массив,</span><span class="sxs-lookup"><span data-stu-id="6730a-690">Array</span></span> | <span data-ttu-id="6730a-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="6730a-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="6730a-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-692">secondOutput</span></span> | <span data-ttu-id="6730a-693">Массив,</span><span class="sxs-lookup"><span data-stu-id="6730a-693">Array</span></span> | <span data-ttu-id="6730a-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="6730a-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="6730a-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="6730a-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="6730a-696">Определяет, начинается ли строка с определенного значения.</span><span class="sxs-lookup"><span data-stu-id="6730a-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="6730a-697">При сравнении регистр не учитывается.</span><span class="sxs-lookup"><span data-stu-id="6730a-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-698">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-698">Parameters</span></span>

| <span data-ttu-id="6730a-699">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-699">Parameter</span></span> | <span data-ttu-id="6730a-700">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-700">Required</span></span> | <span data-ttu-id="6730a-701">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-701">Type</span></span> | <span data-ttu-id="6730a-702">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="6730a-703">stringToSearch</span></span> |<span data-ttu-id="6730a-704">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-704">Yes</span></span> |<span data-ttu-id="6730a-705">string</span><span class="sxs-lookup"><span data-stu-id="6730a-705">string</span></span> |<span data-ttu-id="6730a-706">Значение, содержащее элемент, который необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="6730a-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="6730a-707">stringToFind</span></span> |<span data-ttu-id="6730a-708">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-708">Yes</span></span> |<span data-ttu-id="6730a-709">string</span><span class="sxs-lookup"><span data-stu-id="6730a-709">string</span></span> |<span data-ttu-id="6730a-710">Значение, которое необходимо найти.</span><span class="sxs-lookup"><span data-stu-id="6730a-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-711">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-711">Return value</span></span>

<span data-ttu-id="6730a-712">**True**, если первый знак или знаки строки соответствуют значению. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="6730a-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-713">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-713">Examples</span></span>

<span data-ttu-id="6730a-714">В следующем примере показано, как использовать функции startsWith и endsWith:</span><span class="sxs-lookup"><span data-stu-id="6730a-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="6730a-715">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-716">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-716">Name</span></span> | <span data-ttu-id="6730a-717">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-717">Type</span></span> | <span data-ttu-id="6730a-718">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-719">startsTrue</span></span> | <span data-ttu-id="6730a-720">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-720">Bool</span></span> | <span data-ttu-id="6730a-721">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-721">True</span></span> |
| <span data-ttu-id="6730a-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-722">startsCapTrue</span></span> | <span data-ttu-id="6730a-723">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-723">Bool</span></span> | <span data-ttu-id="6730a-724">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-724">True</span></span> |
| <span data-ttu-id="6730a-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="6730a-725">startsFalse</span></span> | <span data-ttu-id="6730a-726">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-726">Bool</span></span> | <span data-ttu-id="6730a-727">Ложь</span><span class="sxs-lookup"><span data-stu-id="6730a-727">False</span></span> |
| <span data-ttu-id="6730a-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-728">endsTrue</span></span> | <span data-ttu-id="6730a-729">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-729">Bool</span></span> | <span data-ttu-id="6730a-730">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-730">True</span></span> |
| <span data-ttu-id="6730a-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="6730a-731">endsCapTrue</span></span> | <span data-ttu-id="6730a-732">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-732">Bool</span></span> | <span data-ttu-id="6730a-733">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-733">True</span></span> |
| <span data-ttu-id="6730a-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="6730a-734">endsFalse</span></span> | <span data-ttu-id="6730a-735">Bool</span><span class="sxs-lookup"><span data-stu-id="6730a-735">Bool</span></span> | <span data-ttu-id="6730a-736">Ложь</span><span class="sxs-lookup"><span data-stu-id="6730a-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="6730a-737">string</span><span class="sxs-lookup"><span data-stu-id="6730a-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="6730a-738">Преобразует указанное значение в строку.</span><span class="sxs-lookup"><span data-stu-id="6730a-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-739">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-739">Parameters</span></span>

| <span data-ttu-id="6730a-740">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-740">Parameter</span></span> | <span data-ttu-id="6730a-741">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-741">Required</span></span> | <span data-ttu-id="6730a-742">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-742">Type</span></span> | <span data-ttu-id="6730a-743">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="6730a-744">valueToConvert</span></span> |<span data-ttu-id="6730a-745">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-745">Yes</span></span> | <span data-ttu-id="6730a-746">Любой</span><span class="sxs-lookup"><span data-stu-id="6730a-746">Any</span></span> |<span data-ttu-id="6730a-747">Значение, которое необходимо преобразовать в строку.</span><span class="sxs-lookup"><span data-stu-id="6730a-747">The value to convert to string.</span></span> <span data-ttu-id="6730a-748">Можно преобразовать любой тип значения, включая объекты и массивы.</span><span class="sxs-lookup"><span data-stu-id="6730a-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-749">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-749">Return value</span></span>

<span data-ttu-id="6730a-750">Строка преобразованного значения.</span><span class="sxs-lookup"><span data-stu-id="6730a-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-751">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-751">Examples</span></span>

<span data-ttu-id="6730a-752">В следующем примере показано, как преобразовать различные типы значений в строки:</span><span class="sxs-lookup"><span data-stu-id="6730a-752">The following example shows how to convert different types of values to strings:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

<span data-ttu-id="6730a-753">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-754">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-754">Name</span></span> | <span data-ttu-id="6730a-755">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-755">Type</span></span> | <span data-ttu-id="6730a-756">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-757">objectOutput</span></span> | <span data-ttu-id="6730a-758">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-758">String</span></span> | <span data-ttu-id="6730a-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="6730a-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="6730a-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-760">arrayOutput</span></span> | <span data-ttu-id="6730a-761">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-761">String</span></span> | <span data-ttu-id="6730a-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="6730a-762">["a","b","c"]</span></span> |
| <span data-ttu-id="6730a-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-763">intOutput</span></span> | <span data-ttu-id="6730a-764">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-764">String</span></span> | <span data-ttu-id="6730a-765">5</span><span class="sxs-lookup"><span data-stu-id="6730a-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="6730a-766">substring</span><span class="sxs-lookup"><span data-stu-id="6730a-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="6730a-767">Возвращает подстроку, которая начинается с указанной позиции и содержит указанное количество символов.</span><span class="sxs-lookup"><span data-stu-id="6730a-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-768">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-768">Parameters</span></span>

| <span data-ttu-id="6730a-769">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-769">Parameter</span></span> | <span data-ttu-id="6730a-770">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-770">Required</span></span> | <span data-ttu-id="6730a-771">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-771">Type</span></span> | <span data-ttu-id="6730a-772">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="6730a-773">stringToParse</span></span> |<span data-ttu-id="6730a-774">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-774">Yes</span></span> |<span data-ttu-id="6730a-775">string</span><span class="sxs-lookup"><span data-stu-id="6730a-775">string</span></span> |<span data-ttu-id="6730a-776">Исходная строка, из которой извлекается подстрока.</span><span class="sxs-lookup"><span data-stu-id="6730a-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="6730a-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="6730a-777">startIndex</span></span> |<span data-ttu-id="6730a-778">Нет</span><span class="sxs-lookup"><span data-stu-id="6730a-778">No</span></span> |<span data-ttu-id="6730a-779">int</span><span class="sxs-lookup"><span data-stu-id="6730a-779">int</span></span> |<span data-ttu-id="6730a-780">Отсчитываемая от нуля позиция первого знака для подстроки.</span><span class="sxs-lookup"><span data-stu-id="6730a-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="6730a-781">длина</span><span class="sxs-lookup"><span data-stu-id="6730a-781">length</span></span> |<span data-ttu-id="6730a-782">Нет</span><span class="sxs-lookup"><span data-stu-id="6730a-782">No</span></span> |<span data-ttu-id="6730a-783">int</span><span class="sxs-lookup"><span data-stu-id="6730a-783">int</span></span> |<span data-ttu-id="6730a-784">Число символов в подстроке.</span><span class="sxs-lookup"><span data-stu-id="6730a-784">The number of characters for the substring.</span></span> <span data-ttu-id="6730a-785">Этот параметр должен ссылаться на позицию в строке.</span><span class="sxs-lookup"><span data-stu-id="6730a-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-786">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-786">Return value</span></span>

<span data-ttu-id="6730a-787">Подстрока.</span><span class="sxs-lookup"><span data-stu-id="6730a-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="6730a-788">Примечания</span><span class="sxs-lookup"><span data-stu-id="6730a-788">Remarks</span></span>

<span data-ttu-id="6730a-789">Если substring выходит за пределы строки, происходит ошибка выполнения функции.</span><span class="sxs-lookup"><span data-stu-id="6730a-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="6730a-790">Следующий пример завершается ошибкой "Параметры индекса и длины должны относиться к расположению в строке.</span><span class="sxs-lookup"><span data-stu-id="6730a-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="6730a-791">Параметр индекса: 0, параметр длины: 11, параметр длины строкового параметра: 10".</span><span class="sxs-lookup"><span data-stu-id="6730a-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="6730a-792">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-792">Examples</span></span>

<span data-ttu-id="6730a-793">В следующем примере из параметра извлекается подстрока.</span><span class="sxs-lookup"><span data-stu-id="6730a-793">The following example extracts a substring from a parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="6730a-794">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-795">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-795">Name</span></span> | <span data-ttu-id="6730a-796">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-796">Type</span></span> | <span data-ttu-id="6730a-797">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-798">substringOutput</span></span> | <span data-ttu-id="6730a-799">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-799">String</span></span> | <span data-ttu-id="6730a-800">two</span><span class="sxs-lookup"><span data-stu-id="6730a-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="6730a-801">take</span><span class="sxs-lookup"><span data-stu-id="6730a-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="6730a-802">Возвращает строку, содержащую указанное число знаков, считая от начала строки, или массив, содержащий указанное число элементов, считая от начала массива.</span><span class="sxs-lookup"><span data-stu-id="6730a-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-803">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-803">Parameters</span></span>

| <span data-ttu-id="6730a-804">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-804">Parameter</span></span> | <span data-ttu-id="6730a-805">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-805">Required</span></span> | <span data-ttu-id="6730a-806">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-806">Type</span></span> | <span data-ttu-id="6730a-807">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="6730a-808">originalValue</span></span> |<span data-ttu-id="6730a-809">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-809">Yes</span></span> |<span data-ttu-id="6730a-810">массив или строка</span><span class="sxs-lookup"><span data-stu-id="6730a-810">array or string</span></span> |<span data-ttu-id="6730a-811">Массив или строка, из которых берутся элементы.</span><span class="sxs-lookup"><span data-stu-id="6730a-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="6730a-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="6730a-812">numberToTake</span></span> |<span data-ttu-id="6730a-813">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-813">Yes</span></span> |<span data-ttu-id="6730a-814">int</span><span class="sxs-lookup"><span data-stu-id="6730a-814">int</span></span> |<span data-ttu-id="6730a-815">Число элементов или знаков, которые необходимо взять.</span><span class="sxs-lookup"><span data-stu-id="6730a-815">The number of elements or characters to take.</span></span> <span data-ttu-id="6730a-816">Если это значение меньше или равно 0, то возвращается пустой массив или строка.</span><span class="sxs-lookup"><span data-stu-id="6730a-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="6730a-817">Если это значение превышает длину заданного массива или строки, то возвращаются все элементы в массиве или строке.</span><span class="sxs-lookup"><span data-stu-id="6730a-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-818">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-818">Return value</span></span>

<span data-ttu-id="6730a-819">Массив или строка.</span><span class="sxs-lookup"><span data-stu-id="6730a-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-820">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-820">Examples</span></span>

<span data-ttu-id="6730a-821">В следующем примере из массива извлекается заданное число элементов, а из строки — заданное число знаков.</span><span class="sxs-lookup"><span data-stu-id="6730a-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="6730a-822">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-823">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-823">Name</span></span> | <span data-ttu-id="6730a-824">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-824">Type</span></span> | <span data-ttu-id="6730a-825">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-826">arrayOutput</span></span> | <span data-ttu-id="6730a-827">Массив,</span><span class="sxs-lookup"><span data-stu-id="6730a-827">Array</span></span> | <span data-ttu-id="6730a-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="6730a-828">["one", "two"]</span></span> |
| <span data-ttu-id="6730a-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-829">stringOutput</span></span> | <span data-ttu-id="6730a-830">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-830">String</span></span> | <span data-ttu-id="6730a-831">on</span><span class="sxs-lookup"><span data-stu-id="6730a-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="6730a-832">toLower</span><span class="sxs-lookup"><span data-stu-id="6730a-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="6730a-833">Преобразует указанную строку в нижний регистр.</span><span class="sxs-lookup"><span data-stu-id="6730a-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-834">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-834">Parameters</span></span>

| <span data-ttu-id="6730a-835">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-835">Parameter</span></span> | <span data-ttu-id="6730a-836">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-836">Required</span></span> | <span data-ttu-id="6730a-837">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-837">Type</span></span> | <span data-ttu-id="6730a-838">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-839">изменяемая_строка</span><span class="sxs-lookup"><span data-stu-id="6730a-839">stringToChange</span></span> |<span data-ttu-id="6730a-840">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-840">Yes</span></span> |<span data-ttu-id="6730a-841">string</span><span class="sxs-lookup"><span data-stu-id="6730a-841">string</span></span> |<span data-ttu-id="6730a-842">Значение, преобразовываемое в нижний регистр.</span><span class="sxs-lookup"><span data-stu-id="6730a-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-843">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-843">Return value</span></span>

<span data-ttu-id="6730a-844">Возвращает строку, преобразованную в нижний регистр.</span><span class="sxs-lookup"><span data-stu-id="6730a-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-845">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-845">Examples</span></span>

<span data-ttu-id="6730a-846">В следующем примере значение параметра преобразуется в нижний регистр и в верхний регистр.</span><span class="sxs-lookup"><span data-stu-id="6730a-846">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="6730a-847">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-848">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-848">Name</span></span> | <span data-ttu-id="6730a-849">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-849">Type</span></span> | <span data-ttu-id="6730a-850">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-851">toLowerOutput</span></span> | <span data-ttu-id="6730a-852">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-852">String</span></span> | <span data-ttu-id="6730a-853">one two three</span><span class="sxs-lookup"><span data-stu-id="6730a-853">one two three</span></span> |
| <span data-ttu-id="6730a-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-854">toUpperOutput</span></span> | <span data-ttu-id="6730a-855">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-855">String</span></span> | <span data-ttu-id="6730a-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="6730a-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="6730a-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="6730a-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="6730a-858">Преобразует указанную строку в верхний регистр.</span><span class="sxs-lookup"><span data-stu-id="6730a-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-859">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-859">Parameters</span></span>

| <span data-ttu-id="6730a-860">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-860">Parameter</span></span> | <span data-ttu-id="6730a-861">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-861">Required</span></span> | <span data-ttu-id="6730a-862">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-862">Type</span></span> | <span data-ttu-id="6730a-863">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-864">изменяемая_строка</span><span class="sxs-lookup"><span data-stu-id="6730a-864">stringToChange</span></span> |<span data-ttu-id="6730a-865">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-865">Yes</span></span> |<span data-ttu-id="6730a-866">string</span><span class="sxs-lookup"><span data-stu-id="6730a-866">string</span></span> |<span data-ttu-id="6730a-867">Значение, преобразовываемое в верхний регистр.</span><span class="sxs-lookup"><span data-stu-id="6730a-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-868">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-868">Return value</span></span>

<span data-ttu-id="6730a-869">Возвращает строку, преобразованную в верхний регистр.</span><span class="sxs-lookup"><span data-stu-id="6730a-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-870">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-870">Examples</span></span>

<span data-ttu-id="6730a-871">В следующем примере значение параметра преобразуется в нижний регистр и в верхний регистр.</span><span class="sxs-lookup"><span data-stu-id="6730a-871">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="6730a-872">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-873">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-873">Name</span></span> | <span data-ttu-id="6730a-874">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-874">Type</span></span> | <span data-ttu-id="6730a-875">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-876">toLowerOutput</span></span> | <span data-ttu-id="6730a-877">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-877">String</span></span> | <span data-ttu-id="6730a-878">one two three</span><span class="sxs-lookup"><span data-stu-id="6730a-878">one two three</span></span> |
| <span data-ttu-id="6730a-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-879">toUpperOutput</span></span> | <span data-ttu-id="6730a-880">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-880">String</span></span> | <span data-ttu-id="6730a-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="6730a-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="6730a-882">trim</span><span class="sxs-lookup"><span data-stu-id="6730a-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="6730a-883">Удаляет все начальные и конечные знаки пробела из указанной строки.</span><span class="sxs-lookup"><span data-stu-id="6730a-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-884">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-884">Parameters</span></span>

| <span data-ttu-id="6730a-885">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-885">Parameter</span></span> | <span data-ttu-id="6730a-886">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-886">Required</span></span> | <span data-ttu-id="6730a-887">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-887">Type</span></span> | <span data-ttu-id="6730a-888">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="6730a-889">stringToTrim</span></span> |<span data-ttu-id="6730a-890">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-890">Yes</span></span> |<span data-ttu-id="6730a-891">string</span><span class="sxs-lookup"><span data-stu-id="6730a-891">string</span></span> |<span data-ttu-id="6730a-892">Обрезаемое значение.</span><span class="sxs-lookup"><span data-stu-id="6730a-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-893">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-893">Return value</span></span>

<span data-ttu-id="6730a-894">Строка без пробелов в начале и в конце.</span><span class="sxs-lookup"><span data-stu-id="6730a-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-895">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-895">Examples</span></span>

<span data-ttu-id="6730a-896">В следующем примере из параметра удаляются пробелы.</span><span class="sxs-lookup"><span data-stu-id="6730a-896">The following example trims the white-space characters from the parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="6730a-897">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-898">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-898">Name</span></span> | <span data-ttu-id="6730a-899">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-899">Type</span></span> | <span data-ttu-id="6730a-900">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-901">return</span><span class="sxs-lookup"><span data-stu-id="6730a-901">return</span></span> | <span data-ttu-id="6730a-902">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-902">String</span></span> | <span data-ttu-id="6730a-903">one two three</span><span class="sxs-lookup"><span data-stu-id="6730a-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="6730a-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="6730a-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="6730a-905">Создает детерминированную хэш-строку на основании значений, указанных как параметры.</span><span class="sxs-lookup"><span data-stu-id="6730a-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="6730a-906">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-906">Parameters</span></span>

| <span data-ttu-id="6730a-907">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-907">Parameter</span></span> | <span data-ttu-id="6730a-908">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-908">Required</span></span> | <span data-ttu-id="6730a-909">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-909">Type</span></span> | <span data-ttu-id="6730a-910">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-911">baseString</span><span class="sxs-lookup"><span data-stu-id="6730a-911">baseString</span></span> |<span data-ttu-id="6730a-912">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-912">Yes</span></span> |<span data-ttu-id="6730a-913">string</span><span class="sxs-lookup"><span data-stu-id="6730a-913">string</span></span> |<span data-ttu-id="6730a-914">Значение, используемое в хэш-функции для создания уникальной строки.</span><span class="sxs-lookup"><span data-stu-id="6730a-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="6730a-915">Дополнительные параметры (если необходимы)</span><span class="sxs-lookup"><span data-stu-id="6730a-915">additional parameters as needed</span></span> |<span data-ttu-id="6730a-916">Нет</span><span class="sxs-lookup"><span data-stu-id="6730a-916">No</span></span> |<span data-ttu-id="6730a-917">string</span><span class="sxs-lookup"><span data-stu-id="6730a-917">string</span></span> |<span data-ttu-id="6730a-918">Можно добавить столько строк, сколько необходимо для создания значения, которое задает уровень уникальности.</span><span class="sxs-lookup"><span data-stu-id="6730a-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="6730a-919">Примечания</span><span class="sxs-lookup"><span data-stu-id="6730a-919">Remarks</span></span>

<span data-ttu-id="6730a-920">Эта функция полезна в тех случаях, когда необходимо создать уникальное имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="6730a-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="6730a-921">Указываются значения параметров, которые ограничивают область уникальности результата.</span><span class="sxs-lookup"><span data-stu-id="6730a-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="6730a-922">Можно указать, является ли уникальным имя в подписке, группе ресурсов или развертывании.</span><span class="sxs-lookup"><span data-stu-id="6730a-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="6730a-923">Возвращаемое значение — не произвольная строка, а, скорее, результат хэш-функции.</span><span class="sxs-lookup"><span data-stu-id="6730a-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="6730a-924">Возвращаемое значение содержит 13 знаков.</span><span class="sxs-lookup"><span data-stu-id="6730a-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="6730a-925">Оно не является глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="6730a-925">It is not globally unique.</span></span> <span data-ttu-id="6730a-926">Вы можете добавить к значению префикс из своего соглашения об именовании, чтобы создать значимое имя.</span><span class="sxs-lookup"><span data-stu-id="6730a-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="6730a-927">В следующем примере показан формат возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="6730a-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="6730a-928">Фактическое значение зависит от указанных параметров.</span><span class="sxs-lookup"><span data-stu-id="6730a-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="6730a-929">В следующих примерах показывается, как использовать uniqueString при создании уникального значения для часто используемых уровней.</span><span class="sxs-lookup"><span data-stu-id="6730a-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="6730a-930">Уникальное в пределах подписки.</span><span class="sxs-lookup"><span data-stu-id="6730a-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="6730a-931">Уникальное в пределах группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6730a-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="6730a-932">Уникальное в пределах развертывания для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6730a-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="6730a-933">В следующем примере показано, как создать уникальное имя учетной записи хранения на основе вашей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6730a-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="6730a-934">Внутри группы ресурсов имена не будут уникальными, если создавать их таким способом.</span><span class="sxs-lookup"><span data-stu-id="6730a-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="6730a-935">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-935">Return value</span></span>

<span data-ttu-id="6730a-936">Строка, содержащая 13 символов.</span><span class="sxs-lookup"><span data-stu-id="6730a-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-937">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-937">Examples</span></span>

<span data-ttu-id="6730a-938">В следующем примере возвращаются результаты выполнения uniquestring.</span><span class="sxs-lookup"><span data-stu-id="6730a-938">The following example returns results from uniquestring:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a><span data-ttu-id="6730a-939">uri</span><span class="sxs-lookup"><span data-stu-id="6730a-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="6730a-940">Создает абсолютный URI, объединяя строки baseUri и relativeUri.</span><span class="sxs-lookup"><span data-stu-id="6730a-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-941">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-941">Parameters</span></span>

| <span data-ttu-id="6730a-942">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-942">Parameter</span></span> | <span data-ttu-id="6730a-943">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-943">Required</span></span> | <span data-ttu-id="6730a-944">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-944">Type</span></span> | <span data-ttu-id="6730a-945">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="6730a-946">baseUri</span></span> |<span data-ttu-id="6730a-947">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-947">Yes</span></span> |<span data-ttu-id="6730a-948">string</span><span class="sxs-lookup"><span data-stu-id="6730a-948">string</span></span> |<span data-ttu-id="6730a-949">Строка базового универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="6730a-949">The base uri string.</span></span> |
| <span data-ttu-id="6730a-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="6730a-950">relativeUri</span></span> |<span data-ttu-id="6730a-951">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-951">Yes</span></span> |<span data-ttu-id="6730a-952">string</span><span class="sxs-lookup"><span data-stu-id="6730a-952">string</span></span> |<span data-ttu-id="6730a-953">Строка относительного универсального кода ресурса (URI), добавляемая к строке базового универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="6730a-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="6730a-954">Значение параметра **baseUri** может включать в себя определенный файл, однако при построении универсального кода ресурса (URI) используется только базовый путь.</span><span class="sxs-lookup"><span data-stu-id="6730a-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="6730a-955">Например, если передать `http://contoso.com/resources/azuredeploy.json` в качестве параметра baseUri, то базовый универсальный код ресурса (URI) будет иметь значение `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="6730a-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="6730a-956">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-956">Return value</span></span>

<span data-ttu-id="6730a-957">Строка, представляющая абсолютный URI для базового и относительного значений.</span><span class="sxs-lookup"><span data-stu-id="6730a-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-958">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-958">Examples</span></span>

<span data-ttu-id="6730a-959">В следующем примере показано создание ссылки на вложенный шаблон в зависимости от значения параметра родительского шаблона.</span><span class="sxs-lookup"><span data-stu-id="6730a-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="6730a-960">В следующем примере показано, как использовать функции uri, uriComponent и uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="6730a-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="6730a-961">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-962">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-962">Name</span></span> | <span data-ttu-id="6730a-963">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-963">Type</span></span> | <span data-ttu-id="6730a-964">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-965">uriOutput</span></span> | <span data-ttu-id="6730a-966">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-966">String</span></span> | <span data-ttu-id="6730a-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="6730a-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-968">componentOutput</span></span> | <span data-ttu-id="6730a-969">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-969">String</span></span> | <span data-ttu-id="6730a-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="6730a-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-971">toStringOutput</span></span> | <span data-ttu-id="6730a-972">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-972">String</span></span> | <span data-ttu-id="6730a-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="6730a-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="6730a-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="6730a-975">Кодирует URI.</span><span class="sxs-lookup"><span data-stu-id="6730a-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-976">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-976">Parameters</span></span>

| <span data-ttu-id="6730a-977">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-977">Parameter</span></span> | <span data-ttu-id="6730a-978">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-978">Required</span></span> | <span data-ttu-id="6730a-979">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-979">Type</span></span> | <span data-ttu-id="6730a-980">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="6730a-981">stringToEncode</span></span> |<span data-ttu-id="6730a-982">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-982">Yes</span></span> |<span data-ttu-id="6730a-983">string</span><span class="sxs-lookup"><span data-stu-id="6730a-983">string</span></span> |<span data-ttu-id="6730a-984">Значение для кодирования.</span><span class="sxs-lookup"><span data-stu-id="6730a-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-985">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-985">Return value</span></span>

<span data-ttu-id="6730a-986">Строка со значением, закодированным в формате URI.</span><span class="sxs-lookup"><span data-stu-id="6730a-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-987">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-987">Examples</span></span>

<span data-ttu-id="6730a-988">В следующем примере показано, как использовать функции uri, uriComponent и uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="6730a-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="6730a-989">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-990">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-990">Name</span></span> | <span data-ttu-id="6730a-991">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-991">Type</span></span> | <span data-ttu-id="6730a-992">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-993">uriOutput</span></span> | <span data-ttu-id="6730a-994">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-994">String</span></span> | <span data-ttu-id="6730a-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="6730a-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-996">componentOutput</span></span> | <span data-ttu-id="6730a-997">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-997">String</span></span> | <span data-ttu-id="6730a-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="6730a-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-999">toStringOutput</span></span> | <span data-ttu-id="6730a-1000">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-1000">String</span></span> | <span data-ttu-id="6730a-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="6730a-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="6730a-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="6730a-1003">Возвращает строку со значением, закодированным в формате URI.</span><span class="sxs-lookup"><span data-stu-id="6730a-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="6730a-1004">Параметры</span><span class="sxs-lookup"><span data-stu-id="6730a-1004">Parameters</span></span>

| <span data-ttu-id="6730a-1005">Параметр</span><span class="sxs-lookup"><span data-stu-id="6730a-1005">Parameter</span></span> | <span data-ttu-id="6730a-1006">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6730a-1006">Required</span></span> | <span data-ttu-id="6730a-1007">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-1007">Type</span></span> | <span data-ttu-id="6730a-1008">Описание</span><span class="sxs-lookup"><span data-stu-id="6730a-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6730a-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="6730a-1009">uriEncodedString</span></span> |<span data-ttu-id="6730a-1010">Да</span><span class="sxs-lookup"><span data-stu-id="6730a-1010">Yes</span></span> |<span data-ttu-id="6730a-1011">string</span><span class="sxs-lookup"><span data-stu-id="6730a-1011">string</span></span> |<span data-ttu-id="6730a-1012">Значение, закодированное в формате URI, которое необходимо преобразовать в строку.</span><span class="sxs-lookup"><span data-stu-id="6730a-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6730a-1013">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6730a-1013">Return value</span></span>

<span data-ttu-id="6730a-1014">Декодированная строка со значением, закодированным в формате URI.</span><span class="sxs-lookup"><span data-stu-id="6730a-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="6730a-1015">Примеры</span><span class="sxs-lookup"><span data-stu-id="6730a-1015">Examples</span></span>

<span data-ttu-id="6730a-1016">В следующем примере показано, как использовать функции uri, uriComponent и uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="6730a-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="6730a-1017">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6730a-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6730a-1018">Имя</span><span class="sxs-lookup"><span data-stu-id="6730a-1018">Name</span></span> | <span data-ttu-id="6730a-1019">Тип</span><span class="sxs-lookup"><span data-stu-id="6730a-1019">Type</span></span> | <span data-ttu-id="6730a-1020">Значение</span><span class="sxs-lookup"><span data-stu-id="6730a-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6730a-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-1021">uriOutput</span></span> | <span data-ttu-id="6730a-1022">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-1022">String</span></span> | <span data-ttu-id="6730a-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="6730a-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-1024">componentOutput</span></span> | <span data-ttu-id="6730a-1025">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-1025">String</span></span> | <span data-ttu-id="6730a-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="6730a-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="6730a-1027">toStringOutput</span></span> | <span data-ttu-id="6730a-1028">Строка</span><span class="sxs-lookup"><span data-stu-id="6730a-1028">String</span></span> | <span data-ttu-id="6730a-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6730a-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="6730a-1030">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6730a-1030">Next steps</span></span>
* <span data-ttu-id="6730a-1031">Описание разделов в шаблоне Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6730a-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="6730a-1032">Инструкции по объединению нескольких шаблонов см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6730a-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="6730a-1033">Указания по выполнению заданного количества циклов итерации при создании типа ресурса см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6730a-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="6730a-1034">Указания по развертыванию созданного шаблона см. в статье, посвященной [развертыванию приложения с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6730a-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

