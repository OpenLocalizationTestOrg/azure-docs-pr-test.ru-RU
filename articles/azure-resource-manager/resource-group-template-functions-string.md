---
title: "функции шаблонов диспетчера ресурсов aaaAzure - строка | Документы Microsoft"
description: "Описывает toouse функции hello в toowork шаблона диспетчера ресурсов Azure со строками."
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="61dc5-103">Строковые функции для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61dc5-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="61dc5-104">Диспетчер ресурсов предоставляет следующие функции для работы со строками hello:</span><span class="sxs-lookup"><span data-stu-id="61dc5-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="61dc5-105">base64</span><span class="sxs-lookup"><span data-stu-id="61dc5-105">base64</span></span>](#base64)
* [<span data-ttu-id="61dc5-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="61dc5-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="61dc5-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="61dc5-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="61dc5-108">concat</span><span class="sxs-lookup"><span data-stu-id="61dc5-108">concat</span></span>](#concat)
* [<span data-ttu-id="61dc5-109">contains</span><span class="sxs-lookup"><span data-stu-id="61dc5-109">contains</span></span>](#contains)
* [<span data-ttu-id="61dc5-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="61dc5-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="61dc5-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="61dc5-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="61dc5-112">empty</span><span class="sxs-lookup"><span data-stu-id="61dc5-112">empty</span></span>](#empty)
* [<span data-ttu-id="61dc5-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="61dc5-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="61dc5-114">first</span><span class="sxs-lookup"><span data-stu-id="61dc5-114">first</span></span>](#first)
* [<span data-ttu-id="61dc5-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="61dc5-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="61dc5-116">last</span><span class="sxs-lookup"><span data-stu-id="61dc5-116">last</span></span>](#last)
* [<span data-ttu-id="61dc5-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="61dc5-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="61dc5-118">длина</span><span class="sxs-lookup"><span data-stu-id="61dc5-118">length</span></span>](#length)
* [<span data-ttu-id="61dc5-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="61dc5-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="61dc5-120">replace</span><span class="sxs-lookup"><span data-stu-id="61dc5-120">replace</span></span>](#replace)
* [<span data-ttu-id="61dc5-121">skip</span><span class="sxs-lookup"><span data-stu-id="61dc5-121">skip</span></span>](#skip)
* [<span data-ttu-id="61dc5-122">split</span><span class="sxs-lookup"><span data-stu-id="61dc5-122">split</span></span>](#split)
* [<span data-ttu-id="61dc5-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="61dc5-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="61dc5-124">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-124">string</span></span>](#string)
* [<span data-ttu-id="61dc5-125">substring</span><span class="sxs-lookup"><span data-stu-id="61dc5-125">substring</span></span>](#substring)
* [<span data-ttu-id="61dc5-126">take</span><span class="sxs-lookup"><span data-stu-id="61dc5-126">take</span></span>](#take)
* [<span data-ttu-id="61dc5-127">toLower</span><span class="sxs-lookup"><span data-stu-id="61dc5-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="61dc5-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="61dc5-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="61dc5-129">trim</span><span class="sxs-lookup"><span data-stu-id="61dc5-129">trim</span></span>](#trim)
* [<span data-ttu-id="61dc5-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="61dc5-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="61dc5-131">uri</span><span class="sxs-lookup"><span data-stu-id="61dc5-131">uri</span></span>](#uri)
* [<span data-ttu-id="61dc5-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="61dc5-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="61dc5-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="61dc5-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="61dc5-134">base64</span><span class="sxs-lookup"><span data-stu-id="61dc5-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="61dc5-135">Возвращает hello представление base64 hello входной строки.</span><span class="sxs-lookup"><span data-stu-id="61dc5-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-136">Parameters</span></span>

| <span data-ttu-id="61dc5-137">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-137">Parameter</span></span> | <span data-ttu-id="61dc5-138">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-138">Required</span></span> | <span data-ttu-id="61dc5-139">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-139">Type</span></span> | <span data-ttu-id="61dc5-140">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-141">входная_строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-141">inputString</span></span> |<span data-ttu-id="61dc5-142">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-142">Yes</span></span> |<span data-ttu-id="61dc5-143">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-143">string</span></span> |<span data-ttu-id="61dc5-144">Hello tooreturn значение как представление base64.</span><span class="sxs-lookup"><span data-stu-id="61dc5-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-145">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-145">Return value</span></span>

<span data-ttu-id="61dc5-146">Строка, содержащая представление base64 hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-147">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-147">Examples</span></span>

<span data-ttu-id="61dc5-148">Hello в следующем примере показано, как toouse hello функция base64.</span><span class="sxs-lookup"><span data-stu-id="61dc5-148">hello following example shows how toouse hello base64 function.</span></span>

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

<span data-ttu-id="61dc5-149">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-150">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-150">Name</span></span> | <span data-ttu-id="61dc5-151">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-151">Type</span></span> | <span data-ttu-id="61dc5-152">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="61dc5-153">base64Output</span></span> | <span data-ttu-id="61dc5-154">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-154">String</span></span> | <span data-ttu-id="61dc5-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="61dc5-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="61dc5-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-156">toStringOutput</span></span> | <span data-ttu-id="61dc5-157">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-157">String</span></span> | <span data-ttu-id="61dc5-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="61dc5-158">one, two, three</span></span> |
| <span data-ttu-id="61dc5-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-159">toJsonOutput</span></span> | <span data-ttu-id="61dc5-160">Объект</span><span class="sxs-lookup"><span data-stu-id="61dc5-160">Object</span></span> | <span data-ttu-id="61dc5-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="61dc5-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="61dc5-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="61dc5-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="61dc5-163">Преобразует объект base64 tooa представление JSON.</span><span class="sxs-lookup"><span data-stu-id="61dc5-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-164">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-164">Parameters</span></span>

| <span data-ttu-id="61dc5-165">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-165">Parameter</span></span> | <span data-ttu-id="61dc5-166">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-166">Required</span></span> | <span data-ttu-id="61dc5-167">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-167">Type</span></span> | <span data-ttu-id="61dc5-168">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="61dc5-169">base64Value</span></span> |<span data-ttu-id="61dc5-170">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-170">Yes</span></span> |<span data-ttu-id="61dc5-171">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-171">string</span></span> |<span data-ttu-id="61dc5-172">Hello base64 представление tooconvert tooa объект JSON.</span><span class="sxs-lookup"><span data-stu-id="61dc5-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-173">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-173">Return value</span></span>

<span data-ttu-id="61dc5-174">Объект JSON.</span><span class="sxs-lookup"><span data-stu-id="61dc5-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-175">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-175">Examples</span></span>

<span data-ttu-id="61dc5-176">Hello следующий пример использует hello base64ToJson функция tooconvert значение base64.</span><span class="sxs-lookup"><span data-stu-id="61dc5-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="61dc5-177">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-178">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-178">Name</span></span> | <span data-ttu-id="61dc5-179">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-179">Type</span></span> | <span data-ttu-id="61dc5-180">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="61dc5-181">base64Output</span></span> | <span data-ttu-id="61dc5-182">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-182">String</span></span> | <span data-ttu-id="61dc5-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="61dc5-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="61dc5-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-184">toStringOutput</span></span> | <span data-ttu-id="61dc5-185">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-185">String</span></span> | <span data-ttu-id="61dc5-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="61dc5-186">one, two, three</span></span> |
| <span data-ttu-id="61dc5-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-187">toJsonOutput</span></span> | <span data-ttu-id="61dc5-188">Объект</span><span class="sxs-lookup"><span data-stu-id="61dc5-188">Object</span></span> | <span data-ttu-id="61dc5-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="61dc5-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="61dc5-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="61dc5-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="61dc5-191">Преобразует строку tooa представление base64.</span><span class="sxs-lookup"><span data-stu-id="61dc5-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-192">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-192">Parameters</span></span>

| <span data-ttu-id="61dc5-193">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-193">Parameter</span></span> | <span data-ttu-id="61dc5-194">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-194">Required</span></span> | <span data-ttu-id="61dc5-195">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-195">Type</span></span> | <span data-ttu-id="61dc5-196">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="61dc5-197">base64Value</span></span> |<span data-ttu-id="61dc5-198">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-198">Yes</span></span> |<span data-ttu-id="61dc5-199">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-199">string</span></span> |<span data-ttu-id="61dc5-200">Hello представление tooconvert tooa в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="61dc5-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-201">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-201">Return value</span></span>

<span data-ttu-id="61dc5-202">Строка hello преобразованное значение base64.</span><span class="sxs-lookup"><span data-stu-id="61dc5-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-203">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-203">Examples</span></span>

<span data-ttu-id="61dc5-204">Hello следующий пример использует hello base64ToString функция tooconvert значение base64.</span><span class="sxs-lookup"><span data-stu-id="61dc5-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="61dc5-205">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-206">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-206">Name</span></span> | <span data-ttu-id="61dc5-207">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-207">Type</span></span> | <span data-ttu-id="61dc5-208">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="61dc5-209">base64Output</span></span> | <span data-ttu-id="61dc5-210">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-210">String</span></span> | <span data-ttu-id="61dc5-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="61dc5-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="61dc5-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-212">toStringOutput</span></span> | <span data-ttu-id="61dc5-213">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-213">String</span></span> | <span data-ttu-id="61dc5-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="61dc5-214">one, two, three</span></span> |
| <span data-ttu-id="61dc5-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-215">toJsonOutput</span></span> | <span data-ttu-id="61dc5-216">Объект</span><span class="sxs-lookup"><span data-stu-id="61dc5-216">Object</span></span> | <span data-ttu-id="61dc5-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="61dc5-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="61dc5-218">concat</span><span class="sxs-lookup"><span data-stu-id="61dc5-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="61dc5-219">Объединяет несколько строковых значений и возвращает строку hello объединения или объединяет несколько массивов и возвращает массив hello объединяются.</span><span class="sxs-lookup"><span data-stu-id="61dc5-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-220">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-220">Parameters</span></span>

| <span data-ttu-id="61dc5-221">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-221">Parameter</span></span> | <span data-ttu-id="61dc5-222">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-222">Required</span></span> | <span data-ttu-id="61dc5-223">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-223">Type</span></span> | <span data-ttu-id="61dc5-224">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-225">arg1</span><span class="sxs-lookup"><span data-stu-id="61dc5-225">arg1</span></span> |<span data-ttu-id="61dc5-226">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-226">Yes</span></span> |<span data-ttu-id="61dc5-227">строка или массив</span><span class="sxs-lookup"><span data-stu-id="61dc5-227">string or array</span></span> |<span data-ttu-id="61dc5-228">Hello первое значение для объединения.</span><span class="sxs-lookup"><span data-stu-id="61dc5-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="61dc5-229">дополнительные аргументы</span><span class="sxs-lookup"><span data-stu-id="61dc5-229">additional arguments</span></span> |<span data-ttu-id="61dc5-230">Нет</span><span class="sxs-lookup"><span data-stu-id="61dc5-230">No</span></span> |<span data-ttu-id="61dc5-231">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-231">string</span></span> |<span data-ttu-id="61dc5-232">Дополнительные значения в последовательном порядке для сцепки.</span><span class="sxs-lookup"><span data-stu-id="61dc5-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-233">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-233">Return value</span></span>
<span data-ttu-id="61dc5-234">Строка или массив объединенных значений.</span><span class="sxs-lookup"><span data-stu-id="61dc5-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-235">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-235">Examples</span></span>

<span data-ttu-id="61dc5-236">Привет, в следующем примере показано, как toocombine двух строковые значения и возвращает сцепленную строку.</span><span class="sxs-lookup"><span data-stu-id="61dc5-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="61dc5-237">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-238">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-238">Name</span></span> | <span data-ttu-id="61dc5-239">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-239">Type</span></span> | <span data-ttu-id="61dc5-240">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-241">concatOutput</span></span> | <span data-ttu-id="61dc5-242">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-242">String</span></span> | <span data-ttu-id="61dc5-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="61dc5-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="61dc5-244">Hello в следующем примере показано, как toocombine двух массивов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="61dc5-245">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-246">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-246">Name</span></span> | <span data-ttu-id="61dc5-247">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-247">Type</span></span> | <span data-ttu-id="61dc5-248">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-249">return</span><span class="sxs-lookup"><span data-stu-id="61dc5-249">return</span></span> | <span data-ttu-id="61dc5-250">Массив,</span><span class="sxs-lookup"><span data-stu-id="61dc5-250">Array</span></span> | <span data-ttu-id="61dc5-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="61dc5-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="61dc5-252">contains</span><span class="sxs-lookup"><span data-stu-id="61dc5-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="61dc5-253">Проверяет, содержит ли массив значение, содержит ли объект ключ или содержит ли строка подстроку.</span><span class="sxs-lookup"><span data-stu-id="61dc5-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-254">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-254">Parameters</span></span>

| <span data-ttu-id="61dc5-255">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-255">Parameter</span></span> | <span data-ttu-id="61dc5-256">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-256">Required</span></span> | <span data-ttu-id="61dc5-257">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-257">Type</span></span> | <span data-ttu-id="61dc5-258">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-259">container</span><span class="sxs-lookup"><span data-stu-id="61dc5-259">container</span></span> |<span data-ttu-id="61dc5-260">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-260">Yes</span></span> |<span data-ttu-id="61dc5-261">массив, объект или строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-261">array, object, or string</span></span> |<span data-ttu-id="61dc5-262">Hello значение, содержащее значение toofind hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="61dc5-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="61dc5-263">itemToFind</span></span> |<span data-ttu-id="61dc5-264">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-264">Yes</span></span> |<span data-ttu-id="61dc5-265">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="61dc5-265">string or int</span></span> |<span data-ttu-id="61dc5-266">toofind значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-267">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-267">Return value</span></span>

<span data-ttu-id="61dc5-268">**Значение true,** Если hello элемент найден; в противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="61dc5-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-269">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-269">Examples</span></span>

<span data-ttu-id="61dc5-270">Hello следующий пример показывает, как toouse содержит с разными типами:</span><span class="sxs-lookup"><span data-stu-id="61dc5-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="61dc5-271">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-272">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-272">Name</span></span> | <span data-ttu-id="61dc5-273">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-273">Type</span></span> | <span data-ttu-id="61dc5-274">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-275">stringTrue</span></span> | <span data-ttu-id="61dc5-276">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-276">Bool</span></span> | <span data-ttu-id="61dc5-277">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-277">True</span></span> |
| <span data-ttu-id="61dc5-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="61dc5-278">stringFalse</span></span> | <span data-ttu-id="61dc5-279">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-279">Bool</span></span> | <span data-ttu-id="61dc5-280">Ложь</span><span class="sxs-lookup"><span data-stu-id="61dc5-280">False</span></span> |
| <span data-ttu-id="61dc5-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-281">objectTrue</span></span> | <span data-ttu-id="61dc5-282">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-282">Bool</span></span> | <span data-ttu-id="61dc5-283">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-283">True</span></span> |
| <span data-ttu-id="61dc5-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="61dc5-284">objectFalse</span></span> | <span data-ttu-id="61dc5-285">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-285">Bool</span></span> | <span data-ttu-id="61dc5-286">Ложь</span><span class="sxs-lookup"><span data-stu-id="61dc5-286">False</span></span> |
| <span data-ttu-id="61dc5-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-287">arrayTrue</span></span> | <span data-ttu-id="61dc5-288">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-288">Bool</span></span> | <span data-ttu-id="61dc5-289">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-289">True</span></span> |
| <span data-ttu-id="61dc5-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="61dc5-290">arrayFalse</span></span> | <span data-ttu-id="61dc5-291">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-291">Bool</span></span> | <span data-ttu-id="61dc5-292">Ложь</span><span class="sxs-lookup"><span data-stu-id="61dc5-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="61dc5-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="61dc5-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="61dc5-294">Преобразует значение tooa URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-295">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-295">Parameters</span></span>

| <span data-ttu-id="61dc5-296">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-296">Parameter</span></span> | <span data-ttu-id="61dc5-297">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-297">Required</span></span> | <span data-ttu-id="61dc5-298">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-298">Type</span></span> | <span data-ttu-id="61dc5-299">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="61dc5-300">stringToConvert</span></span> |<span data-ttu-id="61dc5-301">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-301">Yes</span></span> |<span data-ttu-id="61dc5-302">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-302">string</span></span> |<span data-ttu-id="61dc5-303">Hello tooconvert tooa значение URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-304">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-304">Return value</span></span>

<span data-ttu-id="61dc5-305">Строка в формате URI данных.</span><span class="sxs-lookup"><span data-stu-id="61dc5-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-306">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-306">Examples</span></span>

<span data-ttu-id="61dc5-307">Здравствуйте, следующий пример преобразует значение tooa URI и преобразует данные строки tooa URI:</span><span class="sxs-lookup"><span data-stu-id="61dc5-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="61dc5-308">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-309">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-309">Name</span></span> | <span data-ttu-id="61dc5-310">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-310">Type</span></span> | <span data-ttu-id="61dc5-311">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-312">dataUriOutput</span></span> | <span data-ttu-id="61dc5-313">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-313">String</span></span> | <span data-ttu-id="61dc5-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="61dc5-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="61dc5-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-315">toStringOutput</span></span> | <span data-ttu-id="61dc5-316">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-316">String</span></span> | <span data-ttu-id="61dc5-317">Привет, мир!</span><span class="sxs-lookup"><span data-stu-id="61dc5-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="61dc5-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="61dc5-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="61dc5-319">Преобразует URI данных в формате строки tooa значения.</span><span class="sxs-lookup"><span data-stu-id="61dc5-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-320">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-320">Parameters</span></span>

| <span data-ttu-id="61dc5-321">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-321">Parameter</span></span> | <span data-ttu-id="61dc5-322">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-322">Required</span></span> | <span data-ttu-id="61dc5-323">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-323">Type</span></span> | <span data-ttu-id="61dc5-324">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="61dc5-325">dataUriToConvert</span></span> |<span data-ttu-id="61dc5-326">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-326">Yes</span></span> |<span data-ttu-id="61dc5-327">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-327">string</span></span> |<span data-ttu-id="61dc5-328">данные Hello tooconvert значение URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-329">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-329">Return value</span></span>

<span data-ttu-id="61dc5-330">Строка, содержащая hello преобразованное значение.</span><span class="sxs-lookup"><span data-stu-id="61dc5-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-331">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-331">Examples</span></span>

<span data-ttu-id="61dc5-332">Здравствуйте, следующий пример преобразует значение tooa URI и преобразует данные строки tooa URI:</span><span class="sxs-lookup"><span data-stu-id="61dc5-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="61dc5-333">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-334">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-334">Name</span></span> | <span data-ttu-id="61dc5-335">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-335">Type</span></span> | <span data-ttu-id="61dc5-336">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-337">dataUriOutput</span></span> | <span data-ttu-id="61dc5-338">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-338">String</span></span> | <span data-ttu-id="61dc5-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="61dc5-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="61dc5-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-340">toStringOutput</span></span> | <span data-ttu-id="61dc5-341">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-341">String</span></span> | <span data-ttu-id="61dc5-342">Привет, мир!</span><span class="sxs-lookup"><span data-stu-id="61dc5-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="61dc5-343">empty</span><span class="sxs-lookup"><span data-stu-id="61dc5-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="61dc5-344">Определяет, являются ли пустыми массив, объект или строка.</span><span class="sxs-lookup"><span data-stu-id="61dc5-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-345">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-345">Parameters</span></span>

| <span data-ttu-id="61dc5-346">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-346">Parameter</span></span> | <span data-ttu-id="61dc5-347">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-347">Required</span></span> | <span data-ttu-id="61dc5-348">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-348">Type</span></span> | <span data-ttu-id="61dc5-349">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="61dc5-350">itemToTest</span></span> |<span data-ttu-id="61dc5-351">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-351">Yes</span></span> |<span data-ttu-id="61dc5-352">массив, объект или строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-352">array, object, or string</span></span> |<span data-ttu-id="61dc5-353">Здравствуйте toocheck значение, если она пуста.</span><span class="sxs-lookup"><span data-stu-id="61dc5-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-354">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-354">Return value</span></span>

<span data-ttu-id="61dc5-355">Возвращает **True** Если hello значение является пустой; в противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="61dc5-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-356">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-356">Examples</span></span>

<span data-ttu-id="61dc5-357">Следующий пример Hello проверяет array, object и string пустым.</span><span class="sxs-lookup"><span data-stu-id="61dc5-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="61dc5-358">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-359">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-359">Name</span></span> | <span data-ttu-id="61dc5-360">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-360">Type</span></span> | <span data-ttu-id="61dc5-361">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="61dc5-362">arrayEmpty</span></span> | <span data-ttu-id="61dc5-363">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-363">Bool</span></span> | <span data-ttu-id="61dc5-364">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-364">True</span></span> |
| <span data-ttu-id="61dc5-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="61dc5-365">objectEmpty</span></span> | <span data-ttu-id="61dc5-366">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-366">Bool</span></span> | <span data-ttu-id="61dc5-367">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-367">True</span></span> |
| <span data-ttu-id="61dc5-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="61dc5-368">stringEmpty</span></span> | <span data-ttu-id="61dc5-369">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-369">Bool</span></span> | <span data-ttu-id="61dc5-370">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="61dc5-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="61dc5-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="61dc5-372">Определяет, заканчивается ли строка определенным значением.</span><span class="sxs-lookup"><span data-stu-id="61dc5-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="61dc5-373">Hello выполняется без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="61dc5-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-374">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-374">Parameters</span></span>

| <span data-ttu-id="61dc5-375">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-375">Parameter</span></span> | <span data-ttu-id="61dc5-376">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-376">Required</span></span> | <span data-ttu-id="61dc5-377">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-377">Type</span></span> | <span data-ttu-id="61dc5-378">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="61dc5-379">stringToSearch</span></span> |<span data-ttu-id="61dc5-380">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-380">Yes</span></span> |<span data-ttu-id="61dc5-381">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-381">string</span></span> |<span data-ttu-id="61dc5-382">Hello значение, содержащее элемент toofind hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="61dc5-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="61dc5-383">stringToFind</span></span> |<span data-ttu-id="61dc5-384">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-384">Yes</span></span> |<span data-ttu-id="61dc5-385">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-385">string</span></span> |<span data-ttu-id="61dc5-386">toofind значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-387">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-387">Return value</span></span>

<span data-ttu-id="61dc5-388">**Значение true,** Если hello последний символ или символы строки hello соответствует значению hello; в противном случае **False**.</span><span class="sxs-lookup"><span data-stu-id="61dc5-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-389">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-389">Examples</span></span>

<span data-ttu-id="61dc5-390">Hello в следующем примере показано, как toouse hello функции startsWith и endsWith.</span><span class="sxs-lookup"><span data-stu-id="61dc5-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="61dc5-391">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-392">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-392">Name</span></span> | <span data-ttu-id="61dc5-393">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-393">Type</span></span> | <span data-ttu-id="61dc5-394">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-395">startsTrue</span></span> | <span data-ttu-id="61dc5-396">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-396">Bool</span></span> | <span data-ttu-id="61dc5-397">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-397">True</span></span> |
| <span data-ttu-id="61dc5-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-398">startsCapTrue</span></span> | <span data-ttu-id="61dc5-399">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-399">Bool</span></span> | <span data-ttu-id="61dc5-400">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-400">True</span></span> |
| <span data-ttu-id="61dc5-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="61dc5-401">startsFalse</span></span> | <span data-ttu-id="61dc5-402">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-402">Bool</span></span> | <span data-ttu-id="61dc5-403">Ложь</span><span class="sxs-lookup"><span data-stu-id="61dc5-403">False</span></span> |
| <span data-ttu-id="61dc5-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-404">endsTrue</span></span> | <span data-ttu-id="61dc5-405">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-405">Bool</span></span> | <span data-ttu-id="61dc5-406">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-406">True</span></span> |
| <span data-ttu-id="61dc5-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-407">endsCapTrue</span></span> | <span data-ttu-id="61dc5-408">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-408">Bool</span></span> | <span data-ttu-id="61dc5-409">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-409">True</span></span> |
| <span data-ttu-id="61dc5-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="61dc5-410">endsFalse</span></span> | <span data-ttu-id="61dc5-411">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-411">Bool</span></span> | <span data-ttu-id="61dc5-412">Ложь</span><span class="sxs-lookup"><span data-stu-id="61dc5-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="61dc5-413">first</span><span class="sxs-lookup"><span data-stu-id="61dc5-413">first</span></span>
`first(arg1)`

<span data-ttu-id="61dc5-414">Возвращает hello первого символа строки hello, или первый элемент массива hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-415">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-415">Parameters</span></span>

| <span data-ttu-id="61dc5-416">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-416">Parameter</span></span> | <span data-ttu-id="61dc5-417">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-417">Required</span></span> | <span data-ttu-id="61dc5-418">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-418">Type</span></span> | <span data-ttu-id="61dc5-419">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-420">arg1</span><span class="sxs-lookup"><span data-stu-id="61dc5-420">arg1</span></span> |<span data-ttu-id="61dc5-421">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-421">Yes</span></span> |<span data-ttu-id="61dc5-422">массив или строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-422">array or string</span></span> |<span data-ttu-id="61dc5-423">символ или первый элемент tooretrieve значение hello Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-424">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-424">Return value</span></span>

<span data-ttu-id="61dc5-425">Строка hello первого символа или тип hello (строка, int, массива или объекта) hello первый элемент массива.</span><span class="sxs-lookup"><span data-stu-id="61dc5-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-426">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-426">Examples</span></span>

<span data-ttu-id="61dc5-427">Hello следующем примере показано, как toouse hello первой функции с массивом и строкой.</span><span class="sxs-lookup"><span data-stu-id="61dc5-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="61dc5-428">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-429">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-429">Name</span></span> | <span data-ttu-id="61dc5-430">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-430">Type</span></span> | <span data-ttu-id="61dc5-431">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-432">arrayOutput</span></span> | <span data-ttu-id="61dc5-433">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-433">String</span></span> | <span data-ttu-id="61dc5-434">one</span><span class="sxs-lookup"><span data-stu-id="61dc5-434">one</span></span> |
| <span data-ttu-id="61dc5-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-435">stringOutput</span></span> | <span data-ttu-id="61dc5-436">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-436">String</span></span> | <span data-ttu-id="61dc5-437">O</span><span class="sxs-lookup"><span data-stu-id="61dc5-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="61dc5-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="61dc5-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="61dc5-439">Возвращает hello первую позицию значения в строке.</span><span class="sxs-lookup"><span data-stu-id="61dc5-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="61dc5-440">Hello выполняется без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="61dc5-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-441">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-441">Parameters</span></span>

| <span data-ttu-id="61dc5-442">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-442">Parameter</span></span> | <span data-ttu-id="61dc5-443">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-443">Required</span></span> | <span data-ttu-id="61dc5-444">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-444">Type</span></span> | <span data-ttu-id="61dc5-445">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="61dc5-446">stringToSearch</span></span> |<span data-ttu-id="61dc5-447">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-447">Yes</span></span> |<span data-ttu-id="61dc5-448">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-448">string</span></span> |<span data-ttu-id="61dc5-449">Hello значение, содержащее элемент toofind hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="61dc5-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="61dc5-450">stringToFind</span></span> |<span data-ttu-id="61dc5-451">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-451">Yes</span></span> |<span data-ttu-id="61dc5-452">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-452">string</span></span> |<span data-ttu-id="61dc5-453">toofind значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-454">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-454">Return value</span></span>

<span data-ttu-id="61dc5-455">Целое число, представляющее позицию элемента toofind hello hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="61dc5-456">Hello значение начинается с нуля.</span><span class="sxs-lookup"><span data-stu-id="61dc5-456">hello value is zero-based.</span></span> <span data-ttu-id="61dc5-457">Если hello элемент не найден, возвращается значение -1.</span><span class="sxs-lookup"><span data-stu-id="61dc5-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-458">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-458">Examples</span></span>

<span data-ttu-id="61dc5-459">Hello в следующем примере показано, как toouse hello функции indexOf и lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="61dc5-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="61dc5-460">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-461">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-461">Name</span></span> | <span data-ttu-id="61dc5-462">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-462">Type</span></span> | <span data-ttu-id="61dc5-463">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-464">firstT</span><span class="sxs-lookup"><span data-stu-id="61dc5-464">firstT</span></span> | <span data-ttu-id="61dc5-465">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-465">Int</span></span> | <span data-ttu-id="61dc5-466">0</span><span class="sxs-lookup"><span data-stu-id="61dc5-466">0</span></span> |
| <span data-ttu-id="61dc5-467">lastT</span><span class="sxs-lookup"><span data-stu-id="61dc5-467">lastT</span></span> | <span data-ttu-id="61dc5-468">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-468">Int</span></span> | <span data-ttu-id="61dc5-469">3</span><span class="sxs-lookup"><span data-stu-id="61dc5-469">3</span></span> |
| <span data-ttu-id="61dc5-470">firstString</span><span class="sxs-lookup"><span data-stu-id="61dc5-470">firstString</span></span> | <span data-ttu-id="61dc5-471">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-471">Int</span></span> | <span data-ttu-id="61dc5-472">2</span><span class="sxs-lookup"><span data-stu-id="61dc5-472">2</span></span> |
| <span data-ttu-id="61dc5-473">lastString</span><span class="sxs-lookup"><span data-stu-id="61dc5-473">lastString</span></span> | <span data-ttu-id="61dc5-474">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-474">Int</span></span> | <span data-ttu-id="61dc5-475">0</span><span class="sxs-lookup"><span data-stu-id="61dc5-475">0</span></span> |
| <span data-ttu-id="61dc5-476">notFound</span><span class="sxs-lookup"><span data-stu-id="61dc5-476">notFound</span></span> | <span data-ttu-id="61dc5-477">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-477">Int</span></span> | <span data-ttu-id="61dc5-478">-1</span><span class="sxs-lookup"><span data-stu-id="61dc5-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="61dc5-479">last</span><span class="sxs-lookup"><span data-stu-id="61dc5-479">last</span></span>
`last (arg1)`

<span data-ttu-id="61dc5-480">Возвращает последнего знака строки hello или hello последним элементом массива hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-481">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-481">Parameters</span></span>

| <span data-ttu-id="61dc5-482">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-482">Parameter</span></span> | <span data-ttu-id="61dc5-483">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-483">Required</span></span> | <span data-ttu-id="61dc5-484">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-484">Type</span></span> | <span data-ttu-id="61dc5-485">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-486">arg1</span><span class="sxs-lookup"><span data-stu-id="61dc5-486">arg1</span></span> |<span data-ttu-id="61dc5-487">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-487">Yes</span></span> |<span data-ttu-id="61dc5-488">массив или строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-488">array or string</span></span> |<span data-ttu-id="61dc5-489">последний элемент hello tooretrieve Hello значение или символ.</span><span class="sxs-lookup"><span data-stu-id="61dc5-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-490">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-490">Return value</span></span>

<span data-ttu-id="61dc5-491">Строка hello последний символ или тип hello (строка, int, массива или объекта) hello последнего элемента в массиве.</span><span class="sxs-lookup"><span data-stu-id="61dc5-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-492">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-492">Examples</span></span>

<span data-ttu-id="61dc5-493">Hello следующем примере показано, как toouse hello последнюю функцию с массивом и строкой.</span><span class="sxs-lookup"><span data-stu-id="61dc5-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="61dc5-494">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-495">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-495">Name</span></span> | <span data-ttu-id="61dc5-496">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-496">Type</span></span> | <span data-ttu-id="61dc5-497">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-498">arrayOutput</span></span> | <span data-ttu-id="61dc5-499">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-499">String</span></span> | <span data-ttu-id="61dc5-500">three</span><span class="sxs-lookup"><span data-stu-id="61dc5-500">three</span></span> |
| <span data-ttu-id="61dc5-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-501">stringOutput</span></span> | <span data-ttu-id="61dc5-502">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-502">String</span></span> | <span data-ttu-id="61dc5-503">e</span><span class="sxs-lookup"><span data-stu-id="61dc5-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="61dc5-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="61dc5-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="61dc5-505">Возвращает hello последней позиции значение в строку.</span><span class="sxs-lookup"><span data-stu-id="61dc5-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="61dc5-506">Hello выполняется без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="61dc5-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-507">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-507">Parameters</span></span>

| <span data-ttu-id="61dc5-508">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-508">Parameter</span></span> | <span data-ttu-id="61dc5-509">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-509">Required</span></span> | <span data-ttu-id="61dc5-510">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-510">Type</span></span> | <span data-ttu-id="61dc5-511">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="61dc5-512">stringToSearch</span></span> |<span data-ttu-id="61dc5-513">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-513">Yes</span></span> |<span data-ttu-id="61dc5-514">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-514">string</span></span> |<span data-ttu-id="61dc5-515">Hello значение, содержащее элемент toofind hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="61dc5-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="61dc5-516">stringToFind</span></span> |<span data-ttu-id="61dc5-517">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-517">Yes</span></span> |<span data-ttu-id="61dc5-518">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-518">string</span></span> |<span data-ttu-id="61dc5-519">toofind значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-520">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-520">Return value</span></span>

<span data-ttu-id="61dc5-521">Целое число, представляющее hello последней позиции элемента toofind hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="61dc5-522">Hello значение начинается с нуля.</span><span class="sxs-lookup"><span data-stu-id="61dc5-522">hello value is zero-based.</span></span> <span data-ttu-id="61dc5-523">Если hello элемент не найден, возвращается значение -1.</span><span class="sxs-lookup"><span data-stu-id="61dc5-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-524">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-524">Examples</span></span>

<span data-ttu-id="61dc5-525">Hello в следующем примере показано, как toouse hello функции indexOf и lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="61dc5-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="61dc5-526">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-527">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-527">Name</span></span> | <span data-ttu-id="61dc5-528">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-528">Type</span></span> | <span data-ttu-id="61dc5-529">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-530">firstT</span><span class="sxs-lookup"><span data-stu-id="61dc5-530">firstT</span></span> | <span data-ttu-id="61dc5-531">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-531">Int</span></span> | <span data-ttu-id="61dc5-532">0</span><span class="sxs-lookup"><span data-stu-id="61dc5-532">0</span></span> |
| <span data-ttu-id="61dc5-533">lastT</span><span class="sxs-lookup"><span data-stu-id="61dc5-533">lastT</span></span> | <span data-ttu-id="61dc5-534">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-534">Int</span></span> | <span data-ttu-id="61dc5-535">3</span><span class="sxs-lookup"><span data-stu-id="61dc5-535">3</span></span> |
| <span data-ttu-id="61dc5-536">firstString</span><span class="sxs-lookup"><span data-stu-id="61dc5-536">firstString</span></span> | <span data-ttu-id="61dc5-537">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-537">Int</span></span> | <span data-ttu-id="61dc5-538">2</span><span class="sxs-lookup"><span data-stu-id="61dc5-538">2</span></span> |
| <span data-ttu-id="61dc5-539">lastString</span><span class="sxs-lookup"><span data-stu-id="61dc5-539">lastString</span></span> | <span data-ttu-id="61dc5-540">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-540">Int</span></span> | <span data-ttu-id="61dc5-541">0</span><span class="sxs-lookup"><span data-stu-id="61dc5-541">0</span></span> |
| <span data-ttu-id="61dc5-542">notFound</span><span class="sxs-lookup"><span data-stu-id="61dc5-542">notFound</span></span> | <span data-ttu-id="61dc5-543">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-543">Int</span></span> | <span data-ttu-id="61dc5-544">-1</span><span class="sxs-lookup"><span data-stu-id="61dc5-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="61dc5-545">длина</span><span class="sxs-lookup"><span data-stu-id="61dc5-545">length</span></span>
`length(string)`

<span data-ttu-id="61dc5-546">Возвращает hello число знаков в строке или элементов в массиве.</span><span class="sxs-lookup"><span data-stu-id="61dc5-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-547">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-547">Parameters</span></span>

| <span data-ttu-id="61dc5-548">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-548">Parameter</span></span> | <span data-ttu-id="61dc5-549">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-549">Required</span></span> | <span data-ttu-id="61dc5-550">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-550">Type</span></span> | <span data-ttu-id="61dc5-551">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-552">arg1</span><span class="sxs-lookup"><span data-stu-id="61dc5-552">arg1</span></span> |<span data-ttu-id="61dc5-553">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-553">Yes</span></span> |<span data-ttu-id="61dc5-554">массив или строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-554">array or string</span></span> |<span data-ttu-id="61dc5-555">Здравствуйте toouse массива для получения hello количество элементов или hello toouse строки для получения hello число символов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-556">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-556">Return value</span></span>

<span data-ttu-id="61dc5-557">Целое число.</span><span class="sxs-lookup"><span data-stu-id="61dc5-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="61dc5-558">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-558">Examples</span></span>

<span data-ttu-id="61dc5-559">Следующий пример показывает как Hello toouse длины с массивом и строкой:</span><span class="sxs-lookup"><span data-stu-id="61dc5-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="61dc5-560">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-561">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-561">Name</span></span> | <span data-ttu-id="61dc5-562">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-562">Type</span></span> | <span data-ttu-id="61dc5-563">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="61dc5-564">arrayLength</span></span> | <span data-ttu-id="61dc5-565">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-565">Int</span></span> | <span data-ttu-id="61dc5-566">3</span><span class="sxs-lookup"><span data-stu-id="61dc5-566">3</span></span> |
| <span data-ttu-id="61dc5-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="61dc5-567">stringLength</span></span> | <span data-ttu-id="61dc5-568">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-568">Int</span></span> | <span data-ttu-id="61dc5-569">13.</span><span class="sxs-lookup"><span data-stu-id="61dc5-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="61dc5-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="61dc5-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="61dc5-571">Возвращает строку, по правому краю путем добавления слева символов toohello до достижения hello общее указанной длины.</span><span class="sxs-lookup"><span data-stu-id="61dc5-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-572">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-572">Parameters</span></span>

| <span data-ttu-id="61dc5-573">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-573">Parameter</span></span> | <span data-ttu-id="61dc5-574">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-574">Required</span></span> | <span data-ttu-id="61dc5-575">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-575">Type</span></span> | <span data-ttu-id="61dc5-576">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-577">значение_для_заполнения </span><span class="sxs-lookup"><span data-stu-id="61dc5-577">valueToPad</span></span> |<span data-ttu-id="61dc5-578">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-578">Yes</span></span> |<span data-ttu-id="61dc5-579">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="61dc5-579">string or int</span></span> |<span data-ttu-id="61dc5-580">Здравствуйте, значение tooright-align.</span><span class="sxs-lookup"><span data-stu-id="61dc5-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="61dc5-581">общая_длина</span><span class="sxs-lookup"><span data-stu-id="61dc5-581">totalLength</span></span> |<span data-ttu-id="61dc5-582">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-582">Yes</span></span> |<span data-ttu-id="61dc5-583">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-583">int</span></span> |<span data-ttu-id="61dc5-584">Общее число символов в hello Hello возвращена строка.</span><span class="sxs-lookup"><span data-stu-id="61dc5-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="61dc5-585">символ_заполнения</span><span class="sxs-lookup"><span data-stu-id="61dc5-585">paddingCharacter</span></span> |<span data-ttu-id="61dc5-586">Нет</span><span class="sxs-lookup"><span data-stu-id="61dc5-586">No</span></span> |<span data-ttu-id="61dc5-587">один знак</span><span class="sxs-lookup"><span data-stu-id="61dc5-587">single character</span></span> |<span data-ttu-id="61dc5-588">Здравствуйте, toouse символ для заполнения влево до достижения hello общей длины.</span><span class="sxs-lookup"><span data-stu-id="61dc5-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="61dc5-589">значение по умолчанию Hello — пробел.</span><span class="sxs-lookup"><span data-stu-id="61dc5-589">hello default value is a space.</span></span> |

<span data-ttu-id="61dc5-590">Если исходная строка hello длиннее, чем число hello toopad символов, символов не добавляются.</span><span class="sxs-lookup"><span data-stu-id="61dc5-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="61dc5-591">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-591">Return value</span></span>

<span data-ttu-id="61dc5-592">Строка с по крайней мере hello число заданных символов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-593">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-593">Examples</span></span>

<span data-ttu-id="61dc5-594">Hello в следующем примере показано, как toopad hello значение параметра, предоставленные пользователем, добавив hello символ нуля до достижения hello общее число символов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

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

<span data-ttu-id="61dc5-595">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-596">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-596">Name</span></span> | <span data-ttu-id="61dc5-597">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-597">Type</span></span> | <span data-ttu-id="61dc5-598">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-599">stringOutput</span></span> | <span data-ttu-id="61dc5-600">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-600">String</span></span> | <span data-ttu-id="61dc5-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="61dc5-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="61dc5-602">replace</span><span class="sxs-lookup"><span data-stu-id="61dc5-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="61dc5-603">Возвращает новую строку, в которой все экземпляры одной строки заменены другой строкой.</span><span class="sxs-lookup"><span data-stu-id="61dc5-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-604">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-604">Parameters</span></span>

| <span data-ttu-id="61dc5-605">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-605">Parameter</span></span> | <span data-ttu-id="61dc5-606">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-606">Required</span></span> | <span data-ttu-id="61dc5-607">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-607">Type</span></span> | <span data-ttu-id="61dc5-608">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-609">исходная_строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-609">originalString</span></span> |<span data-ttu-id="61dc5-610">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-610">Yes</span></span> |<span data-ttu-id="61dc5-611">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-611">string</span></span> |<span data-ttu-id="61dc5-612">значение Hello, которое имеет все вхождения одной строки заменяется на другую строку.</span><span class="sxs-lookup"><span data-stu-id="61dc5-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="61dc5-613">oldString</span><span class="sxs-lookup"><span data-stu-id="61dc5-613">oldString</span></span> |<span data-ttu-id="61dc5-614">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-614">Yes</span></span> |<span data-ttu-id="61dc5-615">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-615">string</span></span> |<span data-ttu-id="61dc5-616">toobe строка Hello удаляется из исходной строки hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="61dc5-617">newString</span><span class="sxs-lookup"><span data-stu-id="61dc5-617">newString</span></span> |<span data-ttu-id="61dc5-618">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-618">Yes</span></span> |<span data-ttu-id="61dc5-619">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-619">string</span></span> |<span data-ttu-id="61dc5-620">tooadd строка Hello вместо hello удалена строка.</span><span class="sxs-lookup"><span data-stu-id="61dc5-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-621">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-621">Return value</span></span>

<span data-ttu-id="61dc5-622">Строка с hello заменить символы.</span><span class="sxs-lookup"><span data-stu-id="61dc5-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-623">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-623">Examples</span></span>

<span data-ttu-id="61dc5-624">Hello в следующем примере показано, как tooremove все дефисы из предоставленных пользователем строку hello и как часть tooreplace hello строка с другой строкой.</span><span class="sxs-lookup"><span data-stu-id="61dc5-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

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

<span data-ttu-id="61dc5-625">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-626">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-626">Name</span></span> | <span data-ttu-id="61dc5-627">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-627">Type</span></span> | <span data-ttu-id="61dc5-628">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-629">firstOutput</span></span> | <span data-ttu-id="61dc5-630">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-630">String</span></span> | <span data-ttu-id="61dc5-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="61dc5-631">1231231234</span></span> |
| <span data-ttu-id="61dc5-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-632">secodeOutput</span></span> | <span data-ttu-id="61dc5-633">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-633">String</span></span> | <span data-ttu-id="61dc5-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="61dc5-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="61dc5-635">skip</span><span class="sxs-lookup"><span data-stu-id="61dc5-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="61dc5-636">Возвращает строку, в которой все символы hello после hello указанное число символов или массив со всеми элементами hello после hello заданное число элементов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-637">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-637">Parameters</span></span>

| <span data-ttu-id="61dc5-638">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-638">Parameter</span></span> | <span data-ttu-id="61dc5-639">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-639">Required</span></span> | <span data-ttu-id="61dc5-640">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-640">Type</span></span> | <span data-ttu-id="61dc5-641">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="61dc5-642">originalValue</span></span> |<span data-ttu-id="61dc5-643">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-643">Yes</span></span> |<span data-ttu-id="61dc5-644">массив или строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-644">array or string</span></span> |<span data-ttu-id="61dc5-645">Hello массиву или строке toouse для пропуска.</span><span class="sxs-lookup"><span data-stu-id="61dc5-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="61dc5-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="61dc5-646">numberToSkip</span></span> |<span data-ttu-id="61dc5-647">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-647">Yes</span></span> |<span data-ttu-id="61dc5-648">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-648">int</span></span> |<span data-ttu-id="61dc5-649">количество элементов или символы tooskip Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="61dc5-650">Если это значение меньше или равно 0, все hello элементов или символов в значении hello возвращаются.</span><span class="sxs-lookup"><span data-stu-id="61dc5-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="61dc5-651">Если превышает длину hello hello массиву или строке, возвращается пустой массив или строку.</span><span class="sxs-lookup"><span data-stu-id="61dc5-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-652">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-652">Return value</span></span>

<span data-ttu-id="61dc5-653">Массив или строка.</span><span class="sxs-lookup"><span data-stu-id="61dc5-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-654">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-654">Examples</span></span>

<span data-ttu-id="61dc5-655">Следующий пример hello пропускает Hello заданное число элементов в массиве hello и hello указанное число символов в строке.</span><span class="sxs-lookup"><span data-stu-id="61dc5-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="61dc5-656">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-657">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-657">Name</span></span> | <span data-ttu-id="61dc5-658">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-658">Type</span></span> | <span data-ttu-id="61dc5-659">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-660">arrayOutput</span></span> | <span data-ttu-id="61dc5-661">Массив,</span><span class="sxs-lookup"><span data-stu-id="61dc5-661">Array</span></span> | <span data-ttu-id="61dc5-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="61dc5-662">["three"]</span></span> |
| <span data-ttu-id="61dc5-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-663">stringOutput</span></span> | <span data-ttu-id="61dc5-664">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-664">String</span></span> | <span data-ttu-id="61dc5-665">two three</span><span class="sxs-lookup"><span data-stu-id="61dc5-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="61dc5-666">split</span><span class="sxs-lookup"><span data-stu-id="61dc5-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="61dc5-667">Возвращает массив строк, содержащий подстроки hello hello входной строки, разделенные hello указан разделители.</span><span class="sxs-lookup"><span data-stu-id="61dc5-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-668">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-668">Parameters</span></span>

| <span data-ttu-id="61dc5-669">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-669">Parameter</span></span> | <span data-ttu-id="61dc5-670">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-670">Required</span></span> | <span data-ttu-id="61dc5-671">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-671">Type</span></span> | <span data-ttu-id="61dc5-672">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-673">входная_строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-673">inputString</span></span> |<span data-ttu-id="61dc5-674">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-674">Yes</span></span> |<span data-ttu-id="61dc5-675">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-675">string</span></span> |<span data-ttu-id="61dc5-676">toosplit строка Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-676">hello string toosplit.</span></span> |
| <span data-ttu-id="61dc5-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="61dc5-677">delimiter</span></span> |<span data-ttu-id="61dc5-678">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-678">Yes</span></span> |<span data-ttu-id="61dc5-679">строка или массив строк</span><span class="sxs-lookup"><span data-stu-id="61dc5-679">string or array of strings</span></span> |<span data-ttu-id="61dc5-680">Hello toouse разделитель для разбиения строки hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-681">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-681">Return value</span></span>

<span data-ttu-id="61dc5-682">Массив строк.</span><span class="sxs-lookup"><span data-stu-id="61dc5-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-683">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-683">Examples</span></span>

<span data-ttu-id="61dc5-684">Hello следующий пример Разделяет входную строку hello запятую и с запятой или точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="61dc5-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="61dc5-685">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-686">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-686">Name</span></span> | <span data-ttu-id="61dc5-687">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-687">Type</span></span> | <span data-ttu-id="61dc5-688">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-689">firstOutput</span></span> | <span data-ttu-id="61dc5-690">Массив,</span><span class="sxs-lookup"><span data-stu-id="61dc5-690">Array</span></span> | <span data-ttu-id="61dc5-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="61dc5-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="61dc5-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-692">secondOutput</span></span> | <span data-ttu-id="61dc5-693">Массив,</span><span class="sxs-lookup"><span data-stu-id="61dc5-693">Array</span></span> | <span data-ttu-id="61dc5-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="61dc5-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="61dc5-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="61dc5-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="61dc5-696">Определяет, начинается ли строка с определенного значения.</span><span class="sxs-lookup"><span data-stu-id="61dc5-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="61dc5-697">Hello выполняется без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="61dc5-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-698">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-698">Parameters</span></span>

| <span data-ttu-id="61dc5-699">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-699">Parameter</span></span> | <span data-ttu-id="61dc5-700">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-700">Required</span></span> | <span data-ttu-id="61dc5-701">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-701">Type</span></span> | <span data-ttu-id="61dc5-702">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="61dc5-703">stringToSearch</span></span> |<span data-ttu-id="61dc5-704">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-704">Yes</span></span> |<span data-ttu-id="61dc5-705">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-705">string</span></span> |<span data-ttu-id="61dc5-706">Hello значение, содержащее элемент toofind hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="61dc5-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="61dc5-707">stringToFind</span></span> |<span data-ttu-id="61dc5-708">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-708">Yes</span></span> |<span data-ttu-id="61dc5-709">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-709">string</span></span> |<span data-ttu-id="61dc5-710">toofind значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-711">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-711">Return value</span></span>

<span data-ttu-id="61dc5-712">**Значение true,** Если hello первый символ или символы строки hello соответствует значению hello; в противном случае **False**.</span><span class="sxs-lookup"><span data-stu-id="61dc5-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-713">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-713">Examples</span></span>

<span data-ttu-id="61dc5-714">Hello в следующем примере показано, как toouse hello функции startsWith и endsWith.</span><span class="sxs-lookup"><span data-stu-id="61dc5-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="61dc5-715">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-716">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-716">Name</span></span> | <span data-ttu-id="61dc5-717">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-717">Type</span></span> | <span data-ttu-id="61dc5-718">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-719">startsTrue</span></span> | <span data-ttu-id="61dc5-720">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-720">Bool</span></span> | <span data-ttu-id="61dc5-721">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-721">True</span></span> |
| <span data-ttu-id="61dc5-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-722">startsCapTrue</span></span> | <span data-ttu-id="61dc5-723">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-723">Bool</span></span> | <span data-ttu-id="61dc5-724">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-724">True</span></span> |
| <span data-ttu-id="61dc5-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="61dc5-725">startsFalse</span></span> | <span data-ttu-id="61dc5-726">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-726">Bool</span></span> | <span data-ttu-id="61dc5-727">Ложь</span><span class="sxs-lookup"><span data-stu-id="61dc5-727">False</span></span> |
| <span data-ttu-id="61dc5-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-728">endsTrue</span></span> | <span data-ttu-id="61dc5-729">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-729">Bool</span></span> | <span data-ttu-id="61dc5-730">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-730">True</span></span> |
| <span data-ttu-id="61dc5-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="61dc5-731">endsCapTrue</span></span> | <span data-ttu-id="61dc5-732">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-732">Bool</span></span> | <span data-ttu-id="61dc5-733">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-733">True</span></span> |
| <span data-ttu-id="61dc5-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="61dc5-734">endsFalse</span></span> | <span data-ttu-id="61dc5-735">Bool</span><span class="sxs-lookup"><span data-stu-id="61dc5-735">Bool</span></span> | <span data-ttu-id="61dc5-736">Ложь</span><span class="sxs-lookup"><span data-stu-id="61dc5-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="61dc5-737">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="61dc5-738">Hello Преобразует указанную строку tooa значение.</span><span class="sxs-lookup"><span data-stu-id="61dc5-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-739">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-739">Parameters</span></span>

| <span data-ttu-id="61dc5-740">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-740">Parameter</span></span> | <span data-ttu-id="61dc5-741">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-741">Required</span></span> | <span data-ttu-id="61dc5-742">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-742">Type</span></span> | <span data-ttu-id="61dc5-743">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="61dc5-744">valueToConvert</span></span> |<span data-ttu-id="61dc5-745">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-745">Yes</span></span> | <span data-ttu-id="61dc5-746">Любой</span><span class="sxs-lookup"><span data-stu-id="61dc5-746">Any</span></span> |<span data-ttu-id="61dc5-747">toostring tooconvert значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="61dc5-748">Можно преобразовать любой тип значения, включая объекты и массивы.</span><span class="sxs-lookup"><span data-stu-id="61dc5-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-749">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-749">Return value</span></span>

<span data-ttu-id="61dc5-750">Строка hello преобразованное значение.</span><span class="sxs-lookup"><span data-stu-id="61dc5-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-751">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-751">Examples</span></span>

<span data-ttu-id="61dc5-752">Hello в следующем примере показано, как tooconvert различных типов значений toostrings:</span><span class="sxs-lookup"><span data-stu-id="61dc5-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

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

<span data-ttu-id="61dc5-753">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-754">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-754">Name</span></span> | <span data-ttu-id="61dc5-755">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-755">Type</span></span> | <span data-ttu-id="61dc5-756">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-757">objectOutput</span></span> | <span data-ttu-id="61dc5-758">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-758">String</span></span> | <span data-ttu-id="61dc5-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="61dc5-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="61dc5-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-760">arrayOutput</span></span> | <span data-ttu-id="61dc5-761">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-761">String</span></span> | <span data-ttu-id="61dc5-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="61dc5-762">["a","b","c"]</span></span> |
| <span data-ttu-id="61dc5-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-763">intOutput</span></span> | <span data-ttu-id="61dc5-764">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-764">String</span></span> | <span data-ttu-id="61dc5-765">5</span><span class="sxs-lookup"><span data-stu-id="61dc5-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="61dc5-766">substring</span><span class="sxs-lookup"><span data-stu-id="61dc5-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="61dc5-767">Возвращает подстроку, начинается с указанного hello позиции знака и содержит hello указанное число символов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-768">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-768">Parameters</span></span>

| <span data-ttu-id="61dc5-769">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-769">Parameter</span></span> | <span data-ttu-id="61dc5-770">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-770">Required</span></span> | <span data-ttu-id="61dc5-771">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-771">Type</span></span> | <span data-ttu-id="61dc5-772">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="61dc5-773">stringToParse</span></span> |<span data-ttu-id="61dc5-774">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-774">Yes</span></span> |<span data-ttu-id="61dc5-775">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-775">string</span></span> |<span data-ttu-id="61dc5-776">Исходная строка Hello, из какой hello извлекается подстрока.</span><span class="sxs-lookup"><span data-stu-id="61dc5-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="61dc5-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="61dc5-777">startIndex</span></span> |<span data-ttu-id="61dc5-778">Нет</span><span class="sxs-lookup"><span data-stu-id="61dc5-778">No</span></span> |<span data-ttu-id="61dc5-779">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-779">int</span></span> |<span data-ttu-id="61dc5-780">Hello отсчитываемый от нуля позиция первого знака поиск подстроки hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="61dc5-781">длина</span><span class="sxs-lookup"><span data-stu-id="61dc5-781">length</span></span> |<span data-ttu-id="61dc5-782">Нет</span><span class="sxs-lookup"><span data-stu-id="61dc5-782">No</span></span> |<span data-ttu-id="61dc5-783">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-783">int</span></span> |<span data-ttu-id="61dc5-784">число символов в подстроке hello Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="61dc5-785">Должен указывать расположение tooa в строку hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-786">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-786">Return value</span></span>

<span data-ttu-id="61dc5-787">подстрока Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="61dc5-788">Примечания</span><span class="sxs-lookup"><span data-stu-id="61dc5-788">Remarks</span></span>

<span data-ttu-id="61dc5-789">функции Hello завершается сбоем, когда hello подстрока выходит за пределы hello конца строки hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="61dc5-790">Следующий пример Hello завершается hello ошибка «hello параметры индекса и длины должны ссылаться tooa расположение в строку hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="61dc5-791">Здравствуйте, параметр индекса: "0" hello, длина параметра: "11" hello, длина параметра строку hello: "10".».</span><span class="sxs-lookup"><span data-stu-id="61dc5-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="61dc5-792">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-792">Examples</span></span>

<span data-ttu-id="61dc5-793">Следующий пример Hello извлекает подстроку из параметра.</span><span class="sxs-lookup"><span data-stu-id="61dc5-793">hello following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="61dc5-794">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-795">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-795">Name</span></span> | <span data-ttu-id="61dc5-796">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-796">Type</span></span> | <span data-ttu-id="61dc5-797">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-798">substringOutput</span></span> | <span data-ttu-id="61dc5-799">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-799">String</span></span> | <span data-ttu-id="61dc5-800">two</span><span class="sxs-lookup"><span data-stu-id="61dc5-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="61dc5-801">take</span><span class="sxs-lookup"><span data-stu-id="61dc5-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="61dc5-802">Возвращает строку с hello указанное число символов от начала hello hello строку или массив с hello заданное число элементов от начала массива hello hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-803">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-803">Parameters</span></span>

| <span data-ttu-id="61dc5-804">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-804">Parameter</span></span> | <span data-ttu-id="61dc5-805">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-805">Required</span></span> | <span data-ttu-id="61dc5-806">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-806">Type</span></span> | <span data-ttu-id="61dc5-807">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="61dc5-808">originalValue</span></span> |<span data-ttu-id="61dc5-809">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-809">Yes</span></span> |<span data-ttu-id="61dc5-810">массив или строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-810">array or string</span></span> |<span data-ttu-id="61dc5-811">Здравствуйте, массиву или строке tootake hello элементы.</span><span class="sxs-lookup"><span data-stu-id="61dc5-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="61dc5-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="61dc5-812">numberToTake</span></span> |<span data-ttu-id="61dc5-813">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-813">Yes</span></span> |<span data-ttu-id="61dc5-814">int</span><span class="sxs-lookup"><span data-stu-id="61dc5-814">int</span></span> |<span data-ttu-id="61dc5-815">количество элементов или символы tootake Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="61dc5-816">Если это значение меньше или равно 0, то возвращается пустой массив или строка.</span><span class="sxs-lookup"><span data-stu-id="61dc5-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="61dc5-817">Если это больше, чем длина заданного массива или строка hello hello, возвращаются все элементы hello hello массиву или строке.</span><span class="sxs-lookup"><span data-stu-id="61dc5-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-818">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-818">Return value</span></span>

<span data-ttu-id="61dc5-819">Массив или строка.</span><span class="sxs-lookup"><span data-stu-id="61dc5-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-820">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-820">Examples</span></span>

<span data-ttu-id="61dc5-821">Следующий пример принимает hello Hello заданное число элементов из массива hello и символов из строки.</span><span class="sxs-lookup"><span data-stu-id="61dc5-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="61dc5-822">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-823">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-823">Name</span></span> | <span data-ttu-id="61dc5-824">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-824">Type</span></span> | <span data-ttu-id="61dc5-825">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-826">arrayOutput</span></span> | <span data-ttu-id="61dc5-827">Массив,</span><span class="sxs-lookup"><span data-stu-id="61dc5-827">Array</span></span> | <span data-ttu-id="61dc5-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="61dc5-828">["one", "two"]</span></span> |
| <span data-ttu-id="61dc5-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-829">stringOutput</span></span> | <span data-ttu-id="61dc5-830">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-830">String</span></span> | <span data-ttu-id="61dc5-831">on</span><span class="sxs-lookup"><span data-stu-id="61dc5-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="61dc5-832">toLower</span><span class="sxs-lookup"><span data-stu-id="61dc5-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="61dc5-833">Преобразует hello указан вариант toolower строки.</span><span class="sxs-lookup"><span data-stu-id="61dc5-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-834">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-834">Parameters</span></span>

| <span data-ttu-id="61dc5-835">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-835">Parameter</span></span> | <span data-ttu-id="61dc5-836">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-836">Required</span></span> | <span data-ttu-id="61dc5-837">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-837">Type</span></span> | <span data-ttu-id="61dc5-838">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-839">изменяемая_строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-839">stringToChange</span></span> |<span data-ttu-id="61dc5-840">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-840">Yes</span></span> |<span data-ttu-id="61dc5-841">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-841">string</span></span> |<span data-ttu-id="61dc5-842">case toolower tooconvert значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-843">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-843">Return value</span></span>

<span data-ttu-id="61dc5-844">преобразовать строку Hello toolower регистр.</span><span class="sxs-lookup"><span data-stu-id="61dc5-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-845">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-845">Examples</span></span>

<span data-ttu-id="61dc5-846">Следующий пример Hello преобразует запрос toolower значение параметра и tooupper случай.</span><span class="sxs-lookup"><span data-stu-id="61dc5-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="61dc5-847">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-848">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-848">Name</span></span> | <span data-ttu-id="61dc5-849">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-849">Type</span></span> | <span data-ttu-id="61dc5-850">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-851">toLowerOutput</span></span> | <span data-ttu-id="61dc5-852">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-852">String</span></span> | <span data-ttu-id="61dc5-853">one two three</span><span class="sxs-lookup"><span data-stu-id="61dc5-853">one two three</span></span> |
| <span data-ttu-id="61dc5-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-854">toUpperOutput</span></span> | <span data-ttu-id="61dc5-855">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-855">String</span></span> | <span data-ttu-id="61dc5-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="61dc5-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="61dc5-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="61dc5-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="61dc5-858">Преобразует hello указан вариант tooupper строки.</span><span class="sxs-lookup"><span data-stu-id="61dc5-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-859">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-859">Parameters</span></span>

| <span data-ttu-id="61dc5-860">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-860">Parameter</span></span> | <span data-ttu-id="61dc5-861">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-861">Required</span></span> | <span data-ttu-id="61dc5-862">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-862">Type</span></span> | <span data-ttu-id="61dc5-863">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-864">изменяемая_строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-864">stringToChange</span></span> |<span data-ttu-id="61dc5-865">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-865">Yes</span></span> |<span data-ttu-id="61dc5-866">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-866">string</span></span> |<span data-ttu-id="61dc5-867">case tooupper tooconvert значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-868">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-868">Return value</span></span>

<span data-ttu-id="61dc5-869">преобразовать строку Hello tooupper регистр.</span><span class="sxs-lookup"><span data-stu-id="61dc5-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-870">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-870">Examples</span></span>

<span data-ttu-id="61dc5-871">Следующий пример Hello преобразует запрос toolower значение параметра и tooupper случай.</span><span class="sxs-lookup"><span data-stu-id="61dc5-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="61dc5-872">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-873">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-873">Name</span></span> | <span data-ttu-id="61dc5-874">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-874">Type</span></span> | <span data-ttu-id="61dc5-875">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-876">toLowerOutput</span></span> | <span data-ttu-id="61dc5-877">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-877">String</span></span> | <span data-ttu-id="61dc5-878">one two three</span><span class="sxs-lookup"><span data-stu-id="61dc5-878">one two three</span></span> |
| <span data-ttu-id="61dc5-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-879">toUpperOutput</span></span> | <span data-ttu-id="61dc5-880">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-880">String</span></span> | <span data-ttu-id="61dc5-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="61dc5-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="61dc5-882">trim</span><span class="sxs-lookup"><span data-stu-id="61dc5-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="61dc5-883">Удаляет все начальные и конечные пробелы из hello указанную строку.</span><span class="sxs-lookup"><span data-stu-id="61dc5-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-884">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-884">Parameters</span></span>

| <span data-ttu-id="61dc5-885">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-885">Parameter</span></span> | <span data-ttu-id="61dc5-886">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-886">Required</span></span> | <span data-ttu-id="61dc5-887">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-887">Type</span></span> | <span data-ttu-id="61dc5-888">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="61dc5-889">stringToTrim</span></span> |<span data-ttu-id="61dc5-890">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-890">Yes</span></span> |<span data-ttu-id="61dc5-891">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-891">string</span></span> |<span data-ttu-id="61dc5-892">tootrim значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-893">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-893">Return value</span></span>

<span data-ttu-id="61dc5-894">Строка Hello без начальные и конечные пробелы.</span><span class="sxs-lookup"><span data-stu-id="61dc5-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-895">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-895">Examples</span></span>

<span data-ttu-id="61dc5-896">Hello следующий пример удаляет символы-разделители hello из параметра hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-896">hello following example trims hello white-space characters from hello parameter.</span></span>

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

<span data-ttu-id="61dc5-897">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-898">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-898">Name</span></span> | <span data-ttu-id="61dc5-899">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-899">Type</span></span> | <span data-ttu-id="61dc5-900">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-901">return</span><span class="sxs-lookup"><span data-stu-id="61dc5-901">return</span></span> | <span data-ttu-id="61dc5-902">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-902">String</span></span> | <span data-ttu-id="61dc5-903">one two three</span><span class="sxs-lookup"><span data-stu-id="61dc5-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="61dc5-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="61dc5-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="61dc5-905">Создает на основе hello значений, переданных как параметры детерминированным хэш-строку.</span><span class="sxs-lookup"><span data-stu-id="61dc5-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="61dc5-906">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-906">Parameters</span></span>

| <span data-ttu-id="61dc5-907">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-907">Parameter</span></span> | <span data-ttu-id="61dc5-908">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-908">Required</span></span> | <span data-ttu-id="61dc5-909">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-909">Type</span></span> | <span data-ttu-id="61dc5-910">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-911">baseString</span><span class="sxs-lookup"><span data-stu-id="61dc5-911">baseString</span></span> |<span data-ttu-id="61dc5-912">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-912">Yes</span></span> |<span data-ttu-id="61dc5-913">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-913">string</span></span> |<span data-ttu-id="61dc5-914">Hello в использовано значение toocreate функции хэширования Привет уникальная строка.</span><span class="sxs-lookup"><span data-stu-id="61dc5-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="61dc5-915">Дополнительные параметры (если необходимы)</span><span class="sxs-lookup"><span data-stu-id="61dc5-915">additional parameters as needed</span></span> |<span data-ttu-id="61dc5-916">Нет</span><span class="sxs-lookup"><span data-stu-id="61dc5-916">No</span></span> |<span data-ttu-id="61dc5-917">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-917">string</span></span> |<span data-ttu-id="61dc5-918">В качестве необходимых toocreate hello значение, указывающее уровень hello уникальности можно добавить любое количество строк.</span><span class="sxs-lookup"><span data-stu-id="61dc5-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="61dc5-919">Примечания</span><span class="sxs-lookup"><span data-stu-id="61dc5-919">Remarks</span></span>

<span data-ttu-id="61dc5-920">Эта функция полезна в тех случаях, когда требуется toocreate уникальное имя для ресурса.</span><span class="sxs-lookup"><span data-stu-id="61dc5-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="61dc5-921">Можно задать значения параметров, ограничить область hello уникальности hello результат.</span><span class="sxs-lookup"><span data-stu-id="61dc5-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="61dc5-922">Можно указать, является ли имя hello уникальный вниз toosubscription, группы ресурсов или развертывания.</span><span class="sxs-lookup"><span data-stu-id="61dc5-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="61dc5-923">Hello возвращаемое значение не является произвольной строки, но вместо hello результат хэш-функции.</span><span class="sxs-lookup"><span data-stu-id="61dc5-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="61dc5-924">Hello вернул значение 13 символов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="61dc5-925">Оно не является глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="61dc5-925">It is not globally unique.</span></span> <span data-ttu-id="61dc5-926">Вы можете значение hello toocombine с префиксом из вашего именования toocreate соглашение понятное имя.</span><span class="sxs-lookup"><span data-stu-id="61dc5-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="61dc5-927">Hello примере показан формат hello hello вернул значение.</span><span class="sxs-lookup"><span data-stu-id="61dc5-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="61dc5-928">Фактическое значение Hello зависит от hello с указанными параметрами.</span><span class="sxs-lookup"><span data-stu-id="61dc5-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="61dc5-929">Привет, следующие примеры показывают, как toocreate uniqueString toouse уникальный значение для часто используемых уровнях.</span><span class="sxs-lookup"><span data-stu-id="61dc5-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="61dc5-930">Уникальный toosubscription области</span><span class="sxs-lookup"><span data-stu-id="61dc5-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="61dc5-931">Уникальный tooresource с областью группы</span><span class="sxs-lookup"><span data-stu-id="61dc5-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="61dc5-932">Уникальный toodeployment с областью для группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="61dc5-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="61dc5-933">Hello в следующем примере показано, как toocreate уникальное имя для учетной записи хранения на основе группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="61dc5-934">Внутри группы ресурсов hello, hello имя не является уникальным, если создан hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="61dc5-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="61dc5-935">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-935">Return value</span></span>

<span data-ttu-id="61dc5-936">Строка, содержащая 13 символов.</span><span class="sxs-lookup"><span data-stu-id="61dc5-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-937">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-937">Examples</span></span>

<span data-ttu-id="61dc5-938">Следующий пример Hello возвращает результаты из uniquestring:</span><span class="sxs-lookup"><span data-stu-id="61dc5-938">hello following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="61dc5-939">uri</span><span class="sxs-lookup"><span data-stu-id="61dc5-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="61dc5-940">Создает абсолютный URI, объединяя hello baseUri и relativeUri строку hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-941">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-941">Parameters</span></span>

| <span data-ttu-id="61dc5-942">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-942">Parameter</span></span> | <span data-ttu-id="61dc5-943">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-943">Required</span></span> | <span data-ttu-id="61dc5-944">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-944">Type</span></span> | <span data-ttu-id="61dc5-945">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="61dc5-946">baseUri</span></span> |<span data-ttu-id="61dc5-947">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-947">Yes</span></span> |<span data-ttu-id="61dc5-948">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-948">string</span></span> |<span data-ttu-id="61dc5-949">Строка Hello базовый uri.</span><span class="sxs-lookup"><span data-stu-id="61dc5-949">hello base uri string.</span></span> |
| <span data-ttu-id="61dc5-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="61dc5-950">relativeUri</span></span> |<span data-ttu-id="61dc5-951">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-951">Yes</span></span> |<span data-ttu-id="61dc5-952">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-952">string</span></span> |<span data-ttu-id="61dc5-953">Hello относительный uri строка tooadd toohello базовый uri строка.</span><span class="sxs-lookup"><span data-stu-id="61dc5-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="61dc5-954">Здравствуйте, значение для hello **baseUri** параметр, можно добавить определенный файл, но только базовый путь hello используется при построении hello URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="61dc5-955">Например, если передать `http://contoso.com/resources/azuredeploy.json` в результате параметр baseUri hello в базовый URI `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="61dc5-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="61dc5-956">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-956">Return value</span></span>

<span data-ttu-id="61dc5-957">Строка, представляющая hello абсолютный универсальный код Ресурса для значений базового и относительного hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-958">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-958">Examples</span></span>

<span data-ttu-id="61dc5-959">Привет, следующий пример показывает как tooconstruct вложенного шаблона tooa ссылку на основе hello значение hello родительского шаблона.</span><span class="sxs-lookup"><span data-stu-id="61dc5-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="61dc5-960">Следующий пример показывает как Hello toouse uri, uriComponent и uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="61dc5-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="61dc5-961">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-962">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-962">Name</span></span> | <span data-ttu-id="61dc5-963">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-963">Type</span></span> | <span data-ttu-id="61dc5-964">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-965">uriOutput</span></span> | <span data-ttu-id="61dc5-966">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-966">String</span></span> | <span data-ttu-id="61dc5-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="61dc5-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-968">componentOutput</span></span> | <span data-ttu-id="61dc5-969">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-969">String</span></span> | <span data-ttu-id="61dc5-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="61dc5-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-971">toStringOutput</span></span> | <span data-ttu-id="61dc5-972">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-972">String</span></span> | <span data-ttu-id="61dc5-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="61dc5-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="61dc5-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="61dc5-975">Кодирует URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-976">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-976">Parameters</span></span>

| <span data-ttu-id="61dc5-977">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-977">Parameter</span></span> | <span data-ttu-id="61dc5-978">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-978">Required</span></span> | <span data-ttu-id="61dc5-979">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-979">Type</span></span> | <span data-ttu-id="61dc5-980">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="61dc5-981">stringToEncode</span></span> |<span data-ttu-id="61dc5-982">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-982">Yes</span></span> |<span data-ttu-id="61dc5-983">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-983">string</span></span> |<span data-ttu-id="61dc5-984">tooencode значение Hello.</span><span class="sxs-lookup"><span data-stu-id="61dc5-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-985">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-985">Return value</span></span>

<span data-ttu-id="61dc5-986">Значение в кодировке строку hello URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-987">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-987">Examples</span></span>

<span data-ttu-id="61dc5-988">Следующий пример показывает как Hello toouse uri, uriComponent и uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="61dc5-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="61dc5-989">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-990">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-990">Name</span></span> | <span data-ttu-id="61dc5-991">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-991">Type</span></span> | <span data-ttu-id="61dc5-992">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-993">uriOutput</span></span> | <span data-ttu-id="61dc5-994">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-994">String</span></span> | <span data-ttu-id="61dc5-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="61dc5-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-996">componentOutput</span></span> | <span data-ttu-id="61dc5-997">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-997">String</span></span> | <span data-ttu-id="61dc5-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="61dc5-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-999">toStringOutput</span></span> | <span data-ttu-id="61dc5-1000">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-1000">String</span></span> | <span data-ttu-id="61dc5-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="61dc5-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="61dc5-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="61dc5-1003">Возвращает строку со значением, закодированным в формате URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="61dc5-1004">Параметры</span><span class="sxs-lookup"><span data-stu-id="61dc5-1004">Parameters</span></span>

| <span data-ttu-id="61dc5-1005">Параметр</span><span class="sxs-lookup"><span data-stu-id="61dc5-1005">Parameter</span></span> | <span data-ttu-id="61dc5-1006">Обязательно</span><span class="sxs-lookup"><span data-stu-id="61dc5-1006">Required</span></span> | <span data-ttu-id="61dc5-1007">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-1007">Type</span></span> | <span data-ttu-id="61dc5-1008">Описание</span><span class="sxs-lookup"><span data-stu-id="61dc5-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="61dc5-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="61dc5-1009">uriEncodedString</span></span> |<span data-ttu-id="61dc5-1010">Да</span><span class="sxs-lookup"><span data-stu-id="61dc5-1010">Yes</span></span> |<span data-ttu-id="61dc5-1011">string</span><span class="sxs-lookup"><span data-stu-id="61dc5-1011">string</span></span> |<span data-ttu-id="61dc5-1012">значение tooconvert tooa строка в кодировке Hello URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="61dc5-1013">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-1013">Return value</span></span>

<span data-ttu-id="61dc5-1014">Декодированная строка со значением, закодированным в формате URI.</span><span class="sxs-lookup"><span data-stu-id="61dc5-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="61dc5-1015">Примеры</span><span class="sxs-lookup"><span data-stu-id="61dc5-1015">Examples</span></span>

<span data-ttu-id="61dc5-1016">Следующий пример показывает как Hello toouse uri, uriComponent и uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="61dc5-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="61dc5-1017">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="61dc5-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="61dc5-1018">Имя</span><span class="sxs-lookup"><span data-stu-id="61dc5-1018">Name</span></span> | <span data-ttu-id="61dc5-1019">Тип</span><span class="sxs-lookup"><span data-stu-id="61dc5-1019">Type</span></span> | <span data-ttu-id="61dc5-1020">Значение</span><span class="sxs-lookup"><span data-stu-id="61dc5-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="61dc5-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-1021">uriOutput</span></span> | <span data-ttu-id="61dc5-1022">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-1022">String</span></span> | <span data-ttu-id="61dc5-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="61dc5-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-1024">componentOutput</span></span> | <span data-ttu-id="61dc5-1025">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-1025">String</span></span> | <span data-ttu-id="61dc5-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="61dc5-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="61dc5-1027">toStringOutput</span></span> | <span data-ttu-id="61dc5-1028">Строка</span><span class="sxs-lookup"><span data-stu-id="61dc5-1028">String</span></span> | <span data-ttu-id="61dc5-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="61dc5-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="61dc5-1030">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61dc5-1030">Next steps</span></span>
* <span data-ttu-id="61dc5-1031">Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="61dc5-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="61dc5-1032">toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="61dc5-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="61dc5-1033">tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="61dc5-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="61dc5-1034">toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="61dc5-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

