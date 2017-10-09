---
title: "функции шаблонов диспетчера ресурсов aaaAzure - сравнения | Документы Microsoft"
description: "Описывает toouse функции hello значения toocompare шаблона диспетчера ресурсов Azure."
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="70b50-103">Функции сравнения для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="70b50-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="70b50-104">Resource Manager предоставляет ряд функций для выполнения сравнений в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="70b50-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="70b50-105">equals</span><span class="sxs-lookup"><span data-stu-id="70b50-105">equals</span></span>](#equals)
* [<span data-ttu-id="70b50-106">greater</span><span class="sxs-lookup"><span data-stu-id="70b50-106">greater</span></span>](#greater)
* [<span data-ttu-id="70b50-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="70b50-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="70b50-108">less</span><span class="sxs-lookup"><span data-stu-id="70b50-108">less</span></span>](#less)
* [<span data-ttu-id="70b50-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="70b50-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="70b50-110">equals (равно)</span><span class="sxs-lookup"><span data-stu-id="70b50-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="70b50-111">Проверяет, являются ли два значения равными.</span><span class="sxs-lookup"><span data-stu-id="70b50-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="70b50-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="70b50-112">Parameters</span></span>

| <span data-ttu-id="70b50-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="70b50-113">Parameter</span></span> | <span data-ttu-id="70b50-114">Обязательно</span><span class="sxs-lookup"><span data-stu-id="70b50-114">Required</span></span> | <span data-ttu-id="70b50-115">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-115">Type</span></span> | <span data-ttu-id="70b50-116">Описание</span><span class="sxs-lookup"><span data-stu-id="70b50-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70b50-117">arg1</span><span class="sxs-lookup"><span data-stu-id="70b50-117">arg1</span></span> |<span data-ttu-id="70b50-118">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-118">Yes</span></span> |<span data-ttu-id="70b50-119">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="70b50-119">int, string, array, or object</span></span> |<span data-ttu-id="70b50-120">Hello первый toocheck значения на равенство.</span><span class="sxs-lookup"><span data-stu-id="70b50-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="70b50-121">arg2</span><span class="sxs-lookup"><span data-stu-id="70b50-121">arg2</span></span> |<span data-ttu-id="70b50-122">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-122">Yes</span></span> |<span data-ttu-id="70b50-123">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="70b50-123">int, string, array, or object</span></span> |<span data-ttu-id="70b50-124">Hello второй toocheck значения на равенство.</span><span class="sxs-lookup"><span data-stu-id="70b50-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70b50-125">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="70b50-125">Return value</span></span>

<span data-ttu-id="70b50-126">Возвращает **True** Если hello значения равны; в противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="70b50-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="70b50-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="70b50-127">Remarks</span></span>

<span data-ttu-id="70b50-128">Hello равно функция часто используется с hello `condition` tootest элемент развернут ли ресурс.</span><span class="sxs-lookup"><span data-stu-id="70b50-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="70b50-129">Пример</span><span class="sxs-lookup"><span data-stu-id="70b50-129">Example</span></span>

<span data-ttu-id="70b50-130">Пример шаблона Hello проверяет различных типов значений на равенство.</span><span class="sxs-lookup"><span data-stu-id="70b50-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="70b50-131">Все значения по умолчанию hello возвращают значение True.</span><span class="sxs-lookup"><span data-stu-id="70b50-131">All hello default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="70b50-132">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="70b50-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70b50-133">Имя</span><span class="sxs-lookup"><span data-stu-id="70b50-133">Name</span></span> | <span data-ttu-id="70b50-134">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-134">Type</span></span> | <span data-ttu-id="70b50-135">Значение</span><span class="sxs-lookup"><span data-stu-id="70b50-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70b50-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="70b50-136">checkInts</span></span> | <span data-ttu-id="70b50-137">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-137">Bool</span></span> | <span data-ttu-id="70b50-138">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-138">True</span></span> |
| <span data-ttu-id="70b50-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70b50-139">checkStrings</span></span> | <span data-ttu-id="70b50-140">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-140">Bool</span></span> | <span data-ttu-id="70b50-141">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-141">True</span></span> |
| <span data-ttu-id="70b50-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="70b50-142">checkArrays</span></span> | <span data-ttu-id="70b50-143">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-143">Bool</span></span> | <span data-ttu-id="70b50-144">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-144">True</span></span> |
| <span data-ttu-id="70b50-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="70b50-145">checkObjects</span></span> | <span data-ttu-id="70b50-146">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-146">Bool</span></span> | <span data-ttu-id="70b50-147">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-147">True</span></span> |


<span data-ttu-id="70b50-148">Hello следующий пример использует [не](resource-group-template-functions-logical.md#not) с **равняется**.</span><span class="sxs-lookup"><span data-stu-id="70b50-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="70b50-149">представлен результат Hello предшествующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="70b50-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="70b50-150">Имя</span><span class="sxs-lookup"><span data-stu-id="70b50-150">Name</span></span> | <span data-ttu-id="70b50-151">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-151">Type</span></span> | <span data-ttu-id="70b50-152">Значение</span><span class="sxs-lookup"><span data-stu-id="70b50-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70b50-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="70b50-153">checkNotEquals</span></span> | <span data-ttu-id="70b50-154">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-154">Bool</span></span> | <span data-ttu-id="70b50-155">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="70b50-156">greater</span><span class="sxs-lookup"><span data-stu-id="70b50-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="70b50-157">Проверяет, является ли первое значение hello больше, чем значение второго hello.</span><span class="sxs-lookup"><span data-stu-id="70b50-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="70b50-158">Параметры</span><span class="sxs-lookup"><span data-stu-id="70b50-158">Parameters</span></span>

| <span data-ttu-id="70b50-159">Параметр</span><span class="sxs-lookup"><span data-stu-id="70b50-159">Parameter</span></span> | <span data-ttu-id="70b50-160">Обязательно</span><span class="sxs-lookup"><span data-stu-id="70b50-160">Required</span></span> | <span data-ttu-id="70b50-161">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-161">Type</span></span> | <span data-ttu-id="70b50-162">Описание</span><span class="sxs-lookup"><span data-stu-id="70b50-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70b50-163">arg1</span><span class="sxs-lookup"><span data-stu-id="70b50-163">arg1</span></span> |<span data-ttu-id="70b50-164">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-164">Yes</span></span> |<span data-ttu-id="70b50-165">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="70b50-165">int or string</span></span> |<span data-ttu-id="70b50-166">Hello первое значение больше сравнения hello.</span><span class="sxs-lookup"><span data-stu-id="70b50-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="70b50-167">arg2</span><span class="sxs-lookup"><span data-stu-id="70b50-167">arg2</span></span> |<span data-ttu-id="70b50-168">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-168">Yes</span></span> |<span data-ttu-id="70b50-169">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="70b50-169">int or string</span></span> |<span data-ttu-id="70b50-170">Hello второе значение для сравнения больше hello.</span><span class="sxs-lookup"><span data-stu-id="70b50-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70b50-171">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="70b50-171">Return value</span></span>

<span data-ttu-id="70b50-172">Возвращает **True** Если hello первое значение больше, чем второе значение hello; в противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="70b50-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="70b50-173">Пример</span><span class="sxs-lookup"><span data-stu-id="70b50-173">Example</span></span>

<span data-ttu-id="70b50-174">Пример шаблона Hello проверяет, больше ли одно значение hello hello других.</span><span class="sxs-lookup"><span data-stu-id="70b50-174">hello example template checks whether hello one value is greater than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="70b50-175">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="70b50-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70b50-176">Имя</span><span class="sxs-lookup"><span data-stu-id="70b50-176">Name</span></span> | <span data-ttu-id="70b50-177">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-177">Type</span></span> | <span data-ttu-id="70b50-178">Значение</span><span class="sxs-lookup"><span data-stu-id="70b50-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70b50-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="70b50-179">checkInts</span></span> | <span data-ttu-id="70b50-180">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-180">Bool</span></span> | <span data-ttu-id="70b50-181">Ложь</span><span class="sxs-lookup"><span data-stu-id="70b50-181">False</span></span> |
| <span data-ttu-id="70b50-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70b50-182">checkStrings</span></span> | <span data-ttu-id="70b50-183">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-183">Bool</span></span> | <span data-ttu-id="70b50-184">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="70b50-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="70b50-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="70b50-186">Проверяет, является ли первое значение hello второе значение больше или равно toohello.</span><span class="sxs-lookup"><span data-stu-id="70b50-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="70b50-187">Параметры</span><span class="sxs-lookup"><span data-stu-id="70b50-187">Parameters</span></span>

| <span data-ttu-id="70b50-188">Параметр</span><span class="sxs-lookup"><span data-stu-id="70b50-188">Parameter</span></span> | <span data-ttu-id="70b50-189">Обязательно</span><span class="sxs-lookup"><span data-stu-id="70b50-189">Required</span></span> | <span data-ttu-id="70b50-190">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-190">Type</span></span> | <span data-ttu-id="70b50-191">Описание</span><span class="sxs-lookup"><span data-stu-id="70b50-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70b50-192">arg1</span><span class="sxs-lookup"><span data-stu-id="70b50-192">arg1</span></span> |<span data-ttu-id="70b50-193">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-193">Yes</span></span> |<span data-ttu-id="70b50-194">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="70b50-194">int or string</span></span> |<span data-ttu-id="70b50-195">Hello первое значение больше или равно сравнения hello.</span><span class="sxs-lookup"><span data-stu-id="70b50-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="70b50-196">arg2</span><span class="sxs-lookup"><span data-stu-id="70b50-196">arg2</span></span> |<span data-ttu-id="70b50-197">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-197">Yes</span></span> |<span data-ttu-id="70b50-198">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="70b50-198">int or string</span></span> |<span data-ttu-id="70b50-199">Hello второе значение для сравнения hello больше или равно.</span><span class="sxs-lookup"><span data-stu-id="70b50-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70b50-200">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="70b50-200">Return value</span></span>

<span data-ttu-id="70b50-201">Возвращает **True** Если hello первое значение больше или равно toohello второй; в противном случае **False**.</span><span class="sxs-lookup"><span data-stu-id="70b50-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="70b50-202">Пример</span><span class="sxs-lookup"><span data-stu-id="70b50-202">Example</span></span>

<span data-ttu-id="70b50-203">Пример шаблона Hello проверяет ли hello одно значение больше или равно toohello других.</span><span class="sxs-lookup"><span data-stu-id="70b50-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="70b50-204">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="70b50-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70b50-205">Имя</span><span class="sxs-lookup"><span data-stu-id="70b50-205">Name</span></span> | <span data-ttu-id="70b50-206">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-206">Type</span></span> | <span data-ttu-id="70b50-207">Значение</span><span class="sxs-lookup"><span data-stu-id="70b50-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70b50-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="70b50-208">checkInts</span></span> | <span data-ttu-id="70b50-209">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-209">Bool</span></span> | <span data-ttu-id="70b50-210">Ложь</span><span class="sxs-lookup"><span data-stu-id="70b50-210">False</span></span> |
| <span data-ttu-id="70b50-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70b50-211">checkStrings</span></span> | <span data-ttu-id="70b50-212">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-212">Bool</span></span> | <span data-ttu-id="70b50-213">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="70b50-214">less</span><span class="sxs-lookup"><span data-stu-id="70b50-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="70b50-215">Проверяет ли hello первое значение меньше hello второе значение.</span><span class="sxs-lookup"><span data-stu-id="70b50-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="70b50-216">Параметры</span><span class="sxs-lookup"><span data-stu-id="70b50-216">Parameters</span></span>

| <span data-ttu-id="70b50-217">Параметр</span><span class="sxs-lookup"><span data-stu-id="70b50-217">Parameter</span></span> | <span data-ttu-id="70b50-218">Обязательно</span><span class="sxs-lookup"><span data-stu-id="70b50-218">Required</span></span> | <span data-ttu-id="70b50-219">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-219">Type</span></span> | <span data-ttu-id="70b50-220">Описание</span><span class="sxs-lookup"><span data-stu-id="70b50-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70b50-221">arg1</span><span class="sxs-lookup"><span data-stu-id="70b50-221">arg1</span></span> |<span data-ttu-id="70b50-222">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-222">Yes</span></span> |<span data-ttu-id="70b50-223">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="70b50-223">int or string</span></span> |<span data-ttu-id="70b50-224">Hello первое значение hello меньше сравнения.</span><span class="sxs-lookup"><span data-stu-id="70b50-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="70b50-225">arg2</span><span class="sxs-lookup"><span data-stu-id="70b50-225">arg2</span></span> |<span data-ttu-id="70b50-226">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-226">Yes</span></span> |<span data-ttu-id="70b50-227">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="70b50-227">int or string</span></span> |<span data-ttu-id="70b50-228">Hello второе значение hello меньше сравнения.</span><span class="sxs-lookup"><span data-stu-id="70b50-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70b50-229">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="70b50-229">Return value</span></span>

<span data-ttu-id="70b50-230">Возвращает **True** Если hello первое значение меньше, чем hello второй значение; в противном случае **False**.</span><span class="sxs-lookup"><span data-stu-id="70b50-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="70b50-231">Пример</span><span class="sxs-lookup"><span data-stu-id="70b50-231">Example</span></span>

<span data-ttu-id="70b50-232">Пример шаблона Hello проверяет, является ли одно значение hello меньше, чем другие hello.</span><span class="sxs-lookup"><span data-stu-id="70b50-232">hello example template checks whether hello one value is less than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="70b50-233">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="70b50-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70b50-234">Имя</span><span class="sxs-lookup"><span data-stu-id="70b50-234">Name</span></span> | <span data-ttu-id="70b50-235">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-235">Type</span></span> | <span data-ttu-id="70b50-236">Значение</span><span class="sxs-lookup"><span data-stu-id="70b50-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70b50-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="70b50-237">checkInts</span></span> | <span data-ttu-id="70b50-238">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-238">Bool</span></span> | <span data-ttu-id="70b50-239">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-239">True</span></span> |
| <span data-ttu-id="70b50-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70b50-240">checkStrings</span></span> | <span data-ttu-id="70b50-241">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-241">Bool</span></span> | <span data-ttu-id="70b50-242">Ложь</span><span class="sxs-lookup"><span data-stu-id="70b50-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="70b50-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="70b50-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="70b50-244">Проверяет, является ли первое значение hello меньше или равно toohello второе значение.</span><span class="sxs-lookup"><span data-stu-id="70b50-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="70b50-245">Параметры</span><span class="sxs-lookup"><span data-stu-id="70b50-245">Parameters</span></span>

| <span data-ttu-id="70b50-246">Параметр</span><span class="sxs-lookup"><span data-stu-id="70b50-246">Parameter</span></span> | <span data-ttu-id="70b50-247">Обязательно</span><span class="sxs-lookup"><span data-stu-id="70b50-247">Required</span></span> | <span data-ttu-id="70b50-248">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-248">Type</span></span> | <span data-ttu-id="70b50-249">Описание</span><span class="sxs-lookup"><span data-stu-id="70b50-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="70b50-250">arg1</span><span class="sxs-lookup"><span data-stu-id="70b50-250">arg1</span></span> |<span data-ttu-id="70b50-251">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-251">Yes</span></span> |<span data-ttu-id="70b50-252">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="70b50-252">int or string</span></span> |<span data-ttu-id="70b50-253">Первое значение Hello hello меньше или равно сравнение.</span><span class="sxs-lookup"><span data-stu-id="70b50-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="70b50-254">arg2</span><span class="sxs-lookup"><span data-stu-id="70b50-254">arg2</span></span> |<span data-ttu-id="70b50-255">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-255">Yes</span></span> |<span data-ttu-id="70b50-256">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="70b50-256">int or string</span></span> |<span data-ttu-id="70b50-257">Здравствуйте, второе значение для hello меньше или равно сравнения.</span><span class="sxs-lookup"><span data-stu-id="70b50-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="70b50-258">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="70b50-258">Return value</span></span>

<span data-ttu-id="70b50-259">Возвращает **True** Если hello первое значение меньше или равно toohello второе значение; в противном случае **False**.</span><span class="sxs-lookup"><span data-stu-id="70b50-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="70b50-260">Пример</span><span class="sxs-lookup"><span data-stu-id="70b50-260">Example</span></span>

<span data-ttu-id="70b50-261">Hello пример шаблона проверяет, является ли одно значение hello меньше или равно toohello других.</span><span class="sxs-lookup"><span data-stu-id="70b50-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="70b50-262">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="70b50-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="70b50-263">Имя</span><span class="sxs-lookup"><span data-stu-id="70b50-263">Name</span></span> | <span data-ttu-id="70b50-264">Тип</span><span class="sxs-lookup"><span data-stu-id="70b50-264">Type</span></span> | <span data-ttu-id="70b50-265">Значение</span><span class="sxs-lookup"><span data-stu-id="70b50-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="70b50-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="70b50-266">checkInts</span></span> | <span data-ttu-id="70b50-267">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-267">Bool</span></span> | <span data-ttu-id="70b50-268">Да</span><span class="sxs-lookup"><span data-stu-id="70b50-268">True</span></span> |
| <span data-ttu-id="70b50-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="70b50-269">checkStrings</span></span> | <span data-ttu-id="70b50-270">Bool</span><span class="sxs-lookup"><span data-stu-id="70b50-270">Bool</span></span> | <span data-ttu-id="70b50-271">Ложь</span><span class="sxs-lookup"><span data-stu-id="70b50-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="70b50-272">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70b50-272">Next steps</span></span>
* <span data-ttu-id="70b50-273">Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="70b50-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="70b50-274">toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="70b50-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="70b50-275">tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="70b50-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="70b50-276">toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="70b50-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

