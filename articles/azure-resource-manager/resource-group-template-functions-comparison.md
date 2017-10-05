---
title: "Функции сравнения в шаблонах Azure Resource Manager | Документация Майкрософт"
description: "Описывает функции, используемые в шаблоне Azure Resource Manager для сравнения значений."
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
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="54dfb-103">Функции сравнения для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54dfb-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="54dfb-104">Resource Manager предоставляет ряд функций для выполнения сравнений в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="54dfb-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="54dfb-105">equals</span><span class="sxs-lookup"><span data-stu-id="54dfb-105">equals</span></span>](#equals)
* [<span data-ttu-id="54dfb-106">greater</span><span class="sxs-lookup"><span data-stu-id="54dfb-106">greater</span></span>](#greater)
* [<span data-ttu-id="54dfb-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="54dfb-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="54dfb-108">less</span><span class="sxs-lookup"><span data-stu-id="54dfb-108">less</span></span>](#less)
* [<span data-ttu-id="54dfb-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="54dfb-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="54dfb-110">equals (равно)</span><span class="sxs-lookup"><span data-stu-id="54dfb-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="54dfb-111">Проверяет, являются ли два значения равными.</span><span class="sxs-lookup"><span data-stu-id="54dfb-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="54dfb-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="54dfb-112">Parameters</span></span>

| <span data-ttu-id="54dfb-113">Параметр</span><span class="sxs-lookup"><span data-stu-id="54dfb-113">Parameter</span></span> | <span data-ttu-id="54dfb-114">Обязательно</span><span class="sxs-lookup"><span data-stu-id="54dfb-114">Required</span></span> | <span data-ttu-id="54dfb-115">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-115">Type</span></span> | <span data-ttu-id="54dfb-116">Описание</span><span class="sxs-lookup"><span data-stu-id="54dfb-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54dfb-117">arg1</span><span class="sxs-lookup"><span data-stu-id="54dfb-117">arg1</span></span> |<span data-ttu-id="54dfb-118">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-118">Yes</span></span> |<span data-ttu-id="54dfb-119">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="54dfb-119">int, string, array, or object</span></span> |<span data-ttu-id="54dfb-120">Первое значение, которое необходимо проверить на равенство.</span><span class="sxs-lookup"><span data-stu-id="54dfb-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="54dfb-121">arg2</span><span class="sxs-lookup"><span data-stu-id="54dfb-121">arg2</span></span> |<span data-ttu-id="54dfb-122">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-122">Yes</span></span> |<span data-ttu-id="54dfb-123">целое число, строка, массив или объект</span><span class="sxs-lookup"><span data-stu-id="54dfb-123">int, string, array, or object</span></span> |<span data-ttu-id="54dfb-124">Второе значение, которое необходимо проверить на равенство.</span><span class="sxs-lookup"><span data-stu-id="54dfb-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54dfb-125">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-125">Return value</span></span>

<span data-ttu-id="54dfb-126">Возвращает результат **True**, если значения равны. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="54dfb-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="54dfb-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="54dfb-127">Remarks</span></span>

<span data-ttu-id="54dfb-128">Функция equals часто используется с элементом `condition`, чтобы проверить, развернут ли ресурс.</span><span class="sxs-lookup"><span data-stu-id="54dfb-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="54dfb-129">Пример</span><span class="sxs-lookup"><span data-stu-id="54dfb-129">Example</span></span>

<span data-ttu-id="54dfb-130">Пример шаблона проверяет различные типы значений на равенство.</span><span class="sxs-lookup"><span data-stu-id="54dfb-130">The example template checks different types of values for equality.</span></span> <span data-ttu-id="54dfb-131">Все значения по умолчанию возвращают результат True.</span><span class="sxs-lookup"><span data-stu-id="54dfb-131">All the default values return True.</span></span>

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

<span data-ttu-id="54dfb-132">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="54dfb-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54dfb-133">Имя</span><span class="sxs-lookup"><span data-stu-id="54dfb-133">Name</span></span> | <span data-ttu-id="54dfb-134">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-134">Type</span></span> | <span data-ttu-id="54dfb-135">Значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54dfb-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="54dfb-136">checkInts</span></span> | <span data-ttu-id="54dfb-137">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-137">Bool</span></span> | <span data-ttu-id="54dfb-138">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-138">True</span></span> |
| <span data-ttu-id="54dfb-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="54dfb-139">checkStrings</span></span> | <span data-ttu-id="54dfb-140">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-140">Bool</span></span> | <span data-ttu-id="54dfb-141">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-141">True</span></span> |
| <span data-ttu-id="54dfb-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="54dfb-142">checkArrays</span></span> | <span data-ttu-id="54dfb-143">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-143">Bool</span></span> | <span data-ttu-id="54dfb-144">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-144">True</span></span> |
| <span data-ttu-id="54dfb-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="54dfb-145">checkObjects</span></span> | <span data-ttu-id="54dfb-146">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-146">Bool</span></span> | <span data-ttu-id="54dfb-147">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-147">True</span></span> |


<span data-ttu-id="54dfb-148">В следующем примере используется функция [not](resource-group-template-functions-logical.md#not) (не) с **equals** (равно).</span><span class="sxs-lookup"><span data-stu-id="54dfb-148">The following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="54dfb-149">Выходные данные из предыдущего примера:</span><span class="sxs-lookup"><span data-stu-id="54dfb-149">The output from the preceding example is:</span></span>

| <span data-ttu-id="54dfb-150">Имя</span><span class="sxs-lookup"><span data-stu-id="54dfb-150">Name</span></span> | <span data-ttu-id="54dfb-151">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-151">Type</span></span> | <span data-ttu-id="54dfb-152">Значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54dfb-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="54dfb-153">checkNotEquals</span></span> | <span data-ttu-id="54dfb-154">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-154">Bool</span></span> | <span data-ttu-id="54dfb-155">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="54dfb-156">greater</span><span class="sxs-lookup"><span data-stu-id="54dfb-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="54dfb-157">Проверяет, является ли первое значение большим, чем второе.</span><span class="sxs-lookup"><span data-stu-id="54dfb-157">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="54dfb-158">Параметры</span><span class="sxs-lookup"><span data-stu-id="54dfb-158">Parameters</span></span>

| <span data-ttu-id="54dfb-159">Параметр</span><span class="sxs-lookup"><span data-stu-id="54dfb-159">Parameter</span></span> | <span data-ttu-id="54dfb-160">Обязательно</span><span class="sxs-lookup"><span data-stu-id="54dfb-160">Required</span></span> | <span data-ttu-id="54dfb-161">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-161">Type</span></span> | <span data-ttu-id="54dfb-162">Описание</span><span class="sxs-lookup"><span data-stu-id="54dfb-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54dfb-163">arg1</span><span class="sxs-lookup"><span data-stu-id="54dfb-163">arg1</span></span> |<span data-ttu-id="54dfb-164">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-164">Yes</span></span> |<span data-ttu-id="54dfb-165">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="54dfb-165">int or string</span></span> |<span data-ttu-id="54dfb-166">Первое значение для сравнения (является ли большим).</span><span class="sxs-lookup"><span data-stu-id="54dfb-166">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="54dfb-167">arg2</span><span class="sxs-lookup"><span data-stu-id="54dfb-167">arg2</span></span> |<span data-ttu-id="54dfb-168">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-168">Yes</span></span> |<span data-ttu-id="54dfb-169">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="54dfb-169">int or string</span></span> |<span data-ttu-id="54dfb-170">Второе значение для сравнения (является ли большим).</span><span class="sxs-lookup"><span data-stu-id="54dfb-170">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54dfb-171">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-171">Return value</span></span>

<span data-ttu-id="54dfb-172">Возвращает результат **True**, если первое значение больше второго. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="54dfb-172">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="54dfb-173">Пример</span><span class="sxs-lookup"><span data-stu-id="54dfb-173">Example</span></span>

<span data-ttu-id="54dfb-174">Пример шаблона проверяет, является ли первое значение большим, чем второе.</span><span class="sxs-lookup"><span data-stu-id="54dfb-174">The example template checks whether the one value is greater than the other.</span></span>

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

<span data-ttu-id="54dfb-175">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="54dfb-175">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54dfb-176">Имя</span><span class="sxs-lookup"><span data-stu-id="54dfb-176">Name</span></span> | <span data-ttu-id="54dfb-177">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-177">Type</span></span> | <span data-ttu-id="54dfb-178">Значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54dfb-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="54dfb-179">checkInts</span></span> | <span data-ttu-id="54dfb-180">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-180">Bool</span></span> | <span data-ttu-id="54dfb-181">Ложь</span><span class="sxs-lookup"><span data-stu-id="54dfb-181">False</span></span> |
| <span data-ttu-id="54dfb-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="54dfb-182">checkStrings</span></span> | <span data-ttu-id="54dfb-183">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-183">Bool</span></span> | <span data-ttu-id="54dfb-184">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="54dfb-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="54dfb-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="54dfb-186">Проверяет, является ли первое значение большим, чем второе, или равным ему.</span><span class="sxs-lookup"><span data-stu-id="54dfb-186">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="54dfb-187">Параметры</span><span class="sxs-lookup"><span data-stu-id="54dfb-187">Parameters</span></span>

| <span data-ttu-id="54dfb-188">Параметр</span><span class="sxs-lookup"><span data-stu-id="54dfb-188">Parameter</span></span> | <span data-ttu-id="54dfb-189">Обязательно</span><span class="sxs-lookup"><span data-stu-id="54dfb-189">Required</span></span> | <span data-ttu-id="54dfb-190">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-190">Type</span></span> | <span data-ttu-id="54dfb-191">Описание</span><span class="sxs-lookup"><span data-stu-id="54dfb-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54dfb-192">arg1</span><span class="sxs-lookup"><span data-stu-id="54dfb-192">arg1</span></span> |<span data-ttu-id="54dfb-193">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-193">Yes</span></span> |<span data-ttu-id="54dfb-194">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="54dfb-194">int or string</span></span> |<span data-ttu-id="54dfb-195">Первое значение для сравнения (является ли большим или равным).</span><span class="sxs-lookup"><span data-stu-id="54dfb-195">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="54dfb-196">arg2</span><span class="sxs-lookup"><span data-stu-id="54dfb-196">arg2</span></span> |<span data-ttu-id="54dfb-197">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-197">Yes</span></span> |<span data-ttu-id="54dfb-198">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="54dfb-198">int or string</span></span> |<span data-ttu-id="54dfb-199">Второе значение для сравнения (является ли большим или равным).</span><span class="sxs-lookup"><span data-stu-id="54dfb-199">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54dfb-200">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-200">Return value</span></span>

<span data-ttu-id="54dfb-201">Возвращает результат **True**, если первое значение больше или равно второму. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="54dfb-201">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="54dfb-202">Пример</span><span class="sxs-lookup"><span data-stu-id="54dfb-202">Example</span></span>

<span data-ttu-id="54dfb-203">Пример шаблона проверяет, является ли первое значение большим, чем второе, или равным ему.</span><span class="sxs-lookup"><span data-stu-id="54dfb-203">The example template checks whether the one value is greater than or equal to the other.</span></span>

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

<span data-ttu-id="54dfb-204">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="54dfb-204">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54dfb-205">Имя</span><span class="sxs-lookup"><span data-stu-id="54dfb-205">Name</span></span> | <span data-ttu-id="54dfb-206">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-206">Type</span></span> | <span data-ttu-id="54dfb-207">Значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54dfb-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="54dfb-208">checkInts</span></span> | <span data-ttu-id="54dfb-209">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-209">Bool</span></span> | <span data-ttu-id="54dfb-210">Ложь</span><span class="sxs-lookup"><span data-stu-id="54dfb-210">False</span></span> |
| <span data-ttu-id="54dfb-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="54dfb-211">checkStrings</span></span> | <span data-ttu-id="54dfb-212">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-212">Bool</span></span> | <span data-ttu-id="54dfb-213">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="54dfb-214">less</span><span class="sxs-lookup"><span data-stu-id="54dfb-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="54dfb-215">Проверяет, является ли первое значение меньшим, чем второе.</span><span class="sxs-lookup"><span data-stu-id="54dfb-215">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="54dfb-216">Параметры</span><span class="sxs-lookup"><span data-stu-id="54dfb-216">Parameters</span></span>

| <span data-ttu-id="54dfb-217">Параметр</span><span class="sxs-lookup"><span data-stu-id="54dfb-217">Parameter</span></span> | <span data-ttu-id="54dfb-218">Обязательно</span><span class="sxs-lookup"><span data-stu-id="54dfb-218">Required</span></span> | <span data-ttu-id="54dfb-219">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-219">Type</span></span> | <span data-ttu-id="54dfb-220">Описание</span><span class="sxs-lookup"><span data-stu-id="54dfb-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54dfb-221">arg1</span><span class="sxs-lookup"><span data-stu-id="54dfb-221">arg1</span></span> |<span data-ttu-id="54dfb-222">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-222">Yes</span></span> |<span data-ttu-id="54dfb-223">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="54dfb-223">int or string</span></span> |<span data-ttu-id="54dfb-224">Первое значение для сравнения (является ли меньшим).</span><span class="sxs-lookup"><span data-stu-id="54dfb-224">The first value for the less comparison.</span></span> |
| <span data-ttu-id="54dfb-225">arg2</span><span class="sxs-lookup"><span data-stu-id="54dfb-225">arg2</span></span> |<span data-ttu-id="54dfb-226">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-226">Yes</span></span> |<span data-ttu-id="54dfb-227">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="54dfb-227">int or string</span></span> |<span data-ttu-id="54dfb-228">Второе значение для сравнения (является ли меньшим).</span><span class="sxs-lookup"><span data-stu-id="54dfb-228">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54dfb-229">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-229">Return value</span></span>

<span data-ttu-id="54dfb-230">Возвращает результат **True**, если первое значение меньше второго. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="54dfb-230">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="54dfb-231">Пример</span><span class="sxs-lookup"><span data-stu-id="54dfb-231">Example</span></span>

<span data-ttu-id="54dfb-232">Пример шаблона проверяет, является ли первое значение меньшим, чем второе.</span><span class="sxs-lookup"><span data-stu-id="54dfb-232">The example template checks whether the one value is less than the other.</span></span>

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

<span data-ttu-id="54dfb-233">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="54dfb-233">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54dfb-234">Имя</span><span class="sxs-lookup"><span data-stu-id="54dfb-234">Name</span></span> | <span data-ttu-id="54dfb-235">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-235">Type</span></span> | <span data-ttu-id="54dfb-236">Значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54dfb-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="54dfb-237">checkInts</span></span> | <span data-ttu-id="54dfb-238">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-238">Bool</span></span> | <span data-ttu-id="54dfb-239">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-239">True</span></span> |
| <span data-ttu-id="54dfb-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="54dfb-240">checkStrings</span></span> | <span data-ttu-id="54dfb-241">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-241">Bool</span></span> | <span data-ttu-id="54dfb-242">Ложь</span><span class="sxs-lookup"><span data-stu-id="54dfb-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="54dfb-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="54dfb-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="54dfb-244">Проверяет, является ли первое значение меньшим, чем второе, или равным ему.</span><span class="sxs-lookup"><span data-stu-id="54dfb-244">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="54dfb-245">Параметры</span><span class="sxs-lookup"><span data-stu-id="54dfb-245">Parameters</span></span>

| <span data-ttu-id="54dfb-246">Параметр</span><span class="sxs-lookup"><span data-stu-id="54dfb-246">Parameter</span></span> | <span data-ttu-id="54dfb-247">Обязательно</span><span class="sxs-lookup"><span data-stu-id="54dfb-247">Required</span></span> | <span data-ttu-id="54dfb-248">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-248">Type</span></span> | <span data-ttu-id="54dfb-249">Описание</span><span class="sxs-lookup"><span data-stu-id="54dfb-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54dfb-250">arg1</span><span class="sxs-lookup"><span data-stu-id="54dfb-250">arg1</span></span> |<span data-ttu-id="54dfb-251">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-251">Yes</span></span> |<span data-ttu-id="54dfb-252">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="54dfb-252">int or string</span></span> |<span data-ttu-id="54dfb-253">Первое значение для сравнения (является ли меньшим или равным).</span><span class="sxs-lookup"><span data-stu-id="54dfb-253">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="54dfb-254">arg2</span><span class="sxs-lookup"><span data-stu-id="54dfb-254">arg2</span></span> |<span data-ttu-id="54dfb-255">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-255">Yes</span></span> |<span data-ttu-id="54dfb-256">целое число или строка</span><span class="sxs-lookup"><span data-stu-id="54dfb-256">int or string</span></span> |<span data-ttu-id="54dfb-257">Второе значение для сравнения (является ли меньшим или равным).</span><span class="sxs-lookup"><span data-stu-id="54dfb-257">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="54dfb-258">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-258">Return value</span></span>

<span data-ttu-id="54dfb-259">Возвращает результат **True**, если первое значение меньше или равно второму. В противном случае — **False**.</span><span class="sxs-lookup"><span data-stu-id="54dfb-259">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="54dfb-260">Пример</span><span class="sxs-lookup"><span data-stu-id="54dfb-260">Example</span></span>

<span data-ttu-id="54dfb-261">Пример шаблона проверяет, является ли первое значение меньшим, чем второе, или равным ему.</span><span class="sxs-lookup"><span data-stu-id="54dfb-261">The example template checks whether the one value is less than or equal to the other.</span></span>

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

<span data-ttu-id="54dfb-262">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="54dfb-262">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="54dfb-263">Имя</span><span class="sxs-lookup"><span data-stu-id="54dfb-263">Name</span></span> | <span data-ttu-id="54dfb-264">Тип</span><span class="sxs-lookup"><span data-stu-id="54dfb-264">Type</span></span> | <span data-ttu-id="54dfb-265">Значение</span><span class="sxs-lookup"><span data-stu-id="54dfb-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="54dfb-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="54dfb-266">checkInts</span></span> | <span data-ttu-id="54dfb-267">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-267">Bool</span></span> | <span data-ttu-id="54dfb-268">Да</span><span class="sxs-lookup"><span data-stu-id="54dfb-268">True</span></span> |
| <span data-ttu-id="54dfb-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="54dfb-269">checkStrings</span></span> | <span data-ttu-id="54dfb-270">Bool</span><span class="sxs-lookup"><span data-stu-id="54dfb-270">Bool</span></span> | <span data-ttu-id="54dfb-271">Ложь</span><span class="sxs-lookup"><span data-stu-id="54dfb-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="54dfb-272">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="54dfb-272">Next steps</span></span>
* <span data-ttu-id="54dfb-273">Описание разделов в шаблоне Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="54dfb-273">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="54dfb-274">Инструкции по объединению нескольких шаблонов см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="54dfb-274">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="54dfb-275">Указания по выполнению заданного количества циклов итерации при создании типа ресурса см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="54dfb-275">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="54dfb-276">Указания по развертыванию созданного шаблона см. в статье, посвященной [развертыванию приложения с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="54dfb-276">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

