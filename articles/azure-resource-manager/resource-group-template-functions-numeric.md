---
title: "Числовые функции шаблона Azure Resource Manager | Документация Майкрософт"
description: "Описывает функции, используемые в шаблоне Azure Resource Manager для работы с числами."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: ae0261134b8d4a934048f58d6c679a48a904950b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="5b1e1-103">Числовые функции для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5b1e1-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="5b1e1-104">Диспетчер ресурсов предоставляет следующие функции для работы с целыми числами:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-104">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="5b1e1-105">добавление</span><span class="sxs-lookup"><span data-stu-id="5b1e1-105">add</span></span>](#add)
* [<span data-ttu-id="5b1e1-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="5b1e1-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="5b1e1-107">div</span><span class="sxs-lookup"><span data-stu-id="5b1e1-107">div</span></span>](#div)
* [<span data-ttu-id="5b1e1-108">float</span><span class="sxs-lookup"><span data-stu-id="5b1e1-108">float</span></span>](#float)
* [<span data-ttu-id="5b1e1-109">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-109">int</span></span>](#int)
* [<span data-ttu-id="5b1e1-110">min</span><span class="sxs-lookup"><span data-stu-id="5b1e1-110">min</span></span>](#min)
* [<span data-ttu-id="5b1e1-111">max</span><span class="sxs-lookup"><span data-stu-id="5b1e1-111">max</span></span>](#max)
* [<span data-ttu-id="5b1e1-112">mod (модуль)</span><span class="sxs-lookup"><span data-stu-id="5b1e1-112">mod</span></span>](#mod)
* [<span data-ttu-id="5b1e1-113">mul</span><span class="sxs-lookup"><span data-stu-id="5b1e1-113">mul</span></span>](#mul)
* [<span data-ttu-id="5b1e1-114">sub</span><span class="sxs-lookup"><span data-stu-id="5b1e1-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="5b1e1-115">добавление</span><span class="sxs-lookup"><span data-stu-id="5b1e1-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="5b1e1-116">Возвращает сумму двух указанных целочисленных значений.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-116">Returns the sum of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-117">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-117">Parameters</span></span>

| <span data-ttu-id="5b1e1-118">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-118">Parameter</span></span> | <span data-ttu-id="5b1e1-119">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-119">Required</span></span> | <span data-ttu-id="5b1e1-120">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-120">Type</span></span> | <span data-ttu-id="5b1e1-121">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="5b1e1-122">операнд1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-122">operand1</span></span> |<span data-ttu-id="5b1e1-123">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-123">Yes</span></span> |<span data-ttu-id="5b1e1-124">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-124">int</span></span> |<span data-ttu-id="5b1e1-125">Первое слагаемое.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-125">First number to add.</span></span> |
|<span data-ttu-id="5b1e1-126">операнд2</span><span class="sxs-lookup"><span data-stu-id="5b1e1-126">operand2</span></span> |<span data-ttu-id="5b1e1-127">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-127">Yes</span></span> |<span data-ttu-id="5b1e1-128">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-128">int</span></span> |<span data-ttu-id="5b1e1-129">Второе слагаемое.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-129">Second number to add.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-130">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-130">Return value</span></span>

<span data-ttu-id="5b1e1-131">Целое число, содержащее сумму параметров.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-131">An integer that contains the sum of the parameters.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-132">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-132">Example</span></span>

<span data-ttu-id="5b1e1-133">В следующем примере суммируются два параметра.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-133">The following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to add"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to add"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="5b1e1-134">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-134">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5b1e1-135">Имя</span><span class="sxs-lookup"><span data-stu-id="5b1e1-135">Name</span></span> | <span data-ttu-id="5b1e1-136">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-136">Type</span></span> | <span data-ttu-id="5b1e1-137">Значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5b1e1-138">addResult</span><span class="sxs-lookup"><span data-stu-id="5b1e1-138">addResult</span></span> | <span data-ttu-id="5b1e1-139">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-139">Int</span></span> | <span data-ttu-id="5b1e1-140">8</span><span class="sxs-lookup"><span data-stu-id="5b1e1-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="5b1e1-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="5b1e1-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="5b1e1-142">Возвращает индекс цикла итерации.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-142">Returns the index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="5b1e1-143">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-143">Parameters</span></span>

| <span data-ttu-id="5b1e1-144">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-144">Parameter</span></span> | <span data-ttu-id="5b1e1-145">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-145">Required</span></span> | <span data-ttu-id="5b1e1-146">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-146">Type</span></span> | <span data-ttu-id="5b1e1-147">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-148">loopName</span><span class="sxs-lookup"><span data-stu-id="5b1e1-148">loopName</span></span> | <span data-ttu-id="5b1e1-149">Нет</span><span class="sxs-lookup"><span data-stu-id="5b1e1-149">No</span></span> | <span data-ttu-id="5b1e1-150">string</span><span class="sxs-lookup"><span data-stu-id="5b1e1-150">string</span></span> | <span data-ttu-id="5b1e1-151">Имя цикла для получения итерации.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-151">The name of the loop for getting the iteration.</span></span> |
| <span data-ttu-id="5b1e1-152">offset</span><span class="sxs-lookup"><span data-stu-id="5b1e1-152">offset</span></span> |<span data-ttu-id="5b1e1-153">Нет</span><span class="sxs-lookup"><span data-stu-id="5b1e1-153">No</span></span> |<span data-ttu-id="5b1e1-154">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-154">int</span></span> |<span data-ttu-id="5b1e1-155">Число, добавляемое к отсчитываемому от нуля значению итерации.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-155">The number to add to the zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="5b1e1-156">Примечания</span><span class="sxs-lookup"><span data-stu-id="5b1e1-156">Remarks</span></span>

<span data-ttu-id="5b1e1-157">Эта функция всегда используется с объектом **copy**.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="5b1e1-158">Если значение **offset** не указано, возвращается текущее значение итерации.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-158">If no value is provided for **offset**, the current iteration value is returned.</span></span> <span data-ttu-id="5b1e1-159">Значение итерации начинается с нуля.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-159">The iteration value starts at zero.</span></span>

<span data-ttu-id="5b1e1-160">Свойство **loopName** позволяет указать, на какую итерацию ссылается copyIndex: ресурса или свойства.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-160">The **loopName** property enables you to specify whether copyIndex is referring to a resource iteration or property iteration.</span></span> <span data-ttu-id="5b1e1-161">Если значение **loopName** не указано, используется текущая итерация типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-161">If no value is provided for **loopName**, the current resource type iteration is used.</span></span> <span data-ttu-id="5b1e1-162">Укажите значение **loopName** при выполнении итерации по свойству.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="5b1e1-163">Полное описание использования **copyIndex** см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="5b1e1-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-164">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-164">Example</span></span>

<span data-ttu-id="5b1e1-165">В следующем примере представлен цикл копирования, в котором значение индекса включается в имя.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-165">The following example shows a copy loop and the index value included in the name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="5b1e1-166">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-166">Return value</span></span>

<span data-ttu-id="5b1e1-167">Целое число, представляющее текущей индекс итерации.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-167">An integer representing the current index of the iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="5b1e1-168">div</span><span class="sxs-lookup"><span data-stu-id="5b1e1-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="5b1e1-169">Возвращает целую часть частного от деления двух указанных целочисленных значений.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-169">Returns the integer division of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-170">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-170">Parameters</span></span>

| <span data-ttu-id="5b1e1-171">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-171">Parameter</span></span> | <span data-ttu-id="5b1e1-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-172">Required</span></span> | <span data-ttu-id="5b1e1-173">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-173">Type</span></span> | <span data-ttu-id="5b1e1-174">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-175">операнд1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-175">operand1</span></span> |<span data-ttu-id="5b1e1-176">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-176">Yes</span></span> |<span data-ttu-id="5b1e1-177">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-177">int</span></span> |<span data-ttu-id="5b1e1-178">Делимое.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-178">The number being divided.</span></span> |
| <span data-ttu-id="5b1e1-179">операнд2</span><span class="sxs-lookup"><span data-stu-id="5b1e1-179">operand2</span></span> |<span data-ttu-id="5b1e1-180">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-180">Yes</span></span> |<span data-ttu-id="5b1e1-181">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-181">int</span></span> |<span data-ttu-id="5b1e1-182">Делитель.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-182">The number that is used to divide.</span></span> <span data-ttu-id="5b1e1-183">Не может иметь значение 0.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-184">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-184">Return value</span></span>

<span data-ttu-id="5b1e1-185">Целое число, представляющее деление.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-185">An integer representing the division.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-186">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-186">Example</span></span>

<span data-ttu-id="5b1e1-187">В следующем примере один параметр делится на другой.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-187">The following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="5b1e1-188">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-188">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5b1e1-189">Имя</span><span class="sxs-lookup"><span data-stu-id="5b1e1-189">Name</span></span> | <span data-ttu-id="5b1e1-190">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-190">Type</span></span> | <span data-ttu-id="5b1e1-191">Значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5b1e1-192">divResult</span><span class="sxs-lookup"><span data-stu-id="5b1e1-192">divResult</span></span> | <span data-ttu-id="5b1e1-193">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-193">Int</span></span> | <span data-ttu-id="5b1e1-194">2</span><span class="sxs-lookup"><span data-stu-id="5b1e1-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="5b1e1-195">float;</span><span class="sxs-lookup"><span data-stu-id="5b1e1-195">float</span></span>
`float(arg1)`

<span data-ttu-id="5b1e1-196">Преобразует значение в число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-196">Converts the value to a floating point number.</span></span> <span data-ttu-id="5b1e1-197">Эта функция используется только при передаче пользовательских параметров в приложение, такое как приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-197">You only use this function when passing custom parameters to an application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-198">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-198">Parameters</span></span>

| <span data-ttu-id="5b1e1-199">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-199">Parameter</span></span> | <span data-ttu-id="5b1e1-200">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-200">Required</span></span> | <span data-ttu-id="5b1e1-201">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-201">Type</span></span> | <span data-ttu-id="5b1e1-202">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-203">arg1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-203">arg1</span></span> |<span data-ttu-id="5b1e1-204">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-204">Yes</span></span> |<span data-ttu-id="5b1e1-205">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="5b1e1-205">string or int</span></span> |<span data-ttu-id="5b1e1-206">Значение, которое необходимо преобразовать в число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-206">The value to convert to a floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-207">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-207">Return value</span></span>
<span data-ttu-id="5b1e1-208">Число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-209">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-209">Example</span></span>

<span data-ttu-id="5b1e1-210">В следующем примере показано, как с помощью функции float передать параметры в приложение логики:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-210">The following example shows how to use float to pass parameters to a Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="5b1e1-211">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="5b1e1-212">Преобразует указанное значение в целое число.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-212">Converts the specified value to an integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-213">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-213">Parameters</span></span>

| <span data-ttu-id="5b1e1-214">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-214">Parameter</span></span> | <span data-ttu-id="5b1e1-215">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-215">Required</span></span> | <span data-ttu-id="5b1e1-216">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-216">Type</span></span> | <span data-ttu-id="5b1e1-217">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="5b1e1-218">valueToConvert</span></span> |<span data-ttu-id="5b1e1-219">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-219">Yes</span></span> |<span data-ttu-id="5b1e1-220">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="5b1e1-220">string or int</span></span> |<span data-ttu-id="5b1e1-221">Значение, которое необходимо преобразовать в целое число.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-221">The value to convert to an integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-222">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-222">Return value</span></span>

<span data-ttu-id="5b1e1-223">Целое число преобразованного значения.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-223">An integer of the converted value.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-224">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-224">Example</span></span>

<span data-ttu-id="5b1e1-225">В следующем примере указанное пользователем значение параметра преобразуется в целое число.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-225">The following example converts the user-provided parameter value to integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="5b1e1-226">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-226">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5b1e1-227">Имя</span><span class="sxs-lookup"><span data-stu-id="5b1e1-227">Name</span></span> | <span data-ttu-id="5b1e1-228">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-228">Type</span></span> | <span data-ttu-id="5b1e1-229">Значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5b1e1-230">intResult</span><span class="sxs-lookup"><span data-stu-id="5b1e1-230">intResult</span></span> | <span data-ttu-id="5b1e1-231">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-231">Int</span></span> | <span data-ttu-id="5b1e1-232">4.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="5b1e1-233">Min</span><span class="sxs-lookup"><span data-stu-id="5b1e1-233">min</span></span>
`min (arg1)`

<span data-ttu-id="5b1e1-234">Возвращает минимальное значение из массива целых чисел или разделенный запятыми список целых чисел.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-234">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-235">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-235">Parameters</span></span>

| <span data-ttu-id="5b1e1-236">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-236">Parameter</span></span> | <span data-ttu-id="5b1e1-237">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-237">Required</span></span> | <span data-ttu-id="5b1e1-238">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-238">Type</span></span> | <span data-ttu-id="5b1e1-239">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-240">arg1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-240">arg1</span></span> |<span data-ttu-id="5b1e1-241">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-241">Yes</span></span> |<span data-ttu-id="5b1e1-242">массив целых чисел или разделенный запятыми список целых чисел</span><span class="sxs-lookup"><span data-stu-id="5b1e1-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="5b1e1-243">Коллекция, для которой необходимо получить минимальное значение.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-243">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-244">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-244">Return value</span></span>

<span data-ttu-id="5b1e1-245">Целое число, представляющее минимальное значение из коллекции.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-245">An integer representing minimum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-246">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-246">Example</span></span>

<span data-ttu-id="5b1e1-247">В следующем примере показано, как использовать функцию min с массивом и списком целых чисел:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-247">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="5b1e1-248">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-248">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5b1e1-249">Имя</span><span class="sxs-lookup"><span data-stu-id="5b1e1-249">Name</span></span> | <span data-ttu-id="5b1e1-250">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-250">Type</span></span> | <span data-ttu-id="5b1e1-251">Значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5b1e1-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="5b1e1-252">arrayOutput</span></span> | <span data-ttu-id="5b1e1-253">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-253">Int</span></span> | <span data-ttu-id="5b1e1-254">0</span><span class="sxs-lookup"><span data-stu-id="5b1e1-254">0</span></span> |
| <span data-ttu-id="5b1e1-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="5b1e1-255">intOutput</span></span> | <span data-ttu-id="5b1e1-256">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-256">Int</span></span> | <span data-ttu-id="5b1e1-257">0</span><span class="sxs-lookup"><span data-stu-id="5b1e1-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="5b1e1-258">max</span><span class="sxs-lookup"><span data-stu-id="5b1e1-258">max</span></span>
`max (arg1)`

<span data-ttu-id="5b1e1-259">Возвращает максимальное значение из массива целых чисел или разделенный запятыми список целых чисел.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-259">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-260">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-260">Parameters</span></span>

| <span data-ttu-id="5b1e1-261">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-261">Parameter</span></span> | <span data-ttu-id="5b1e1-262">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-262">Required</span></span> | <span data-ttu-id="5b1e1-263">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-263">Type</span></span> | <span data-ttu-id="5b1e1-264">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-265">arg1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-265">arg1</span></span> |<span data-ttu-id="5b1e1-266">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-266">Yes</span></span> |<span data-ttu-id="5b1e1-267">массив целых чисел или разделенный запятыми список целых чисел</span><span class="sxs-lookup"><span data-stu-id="5b1e1-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="5b1e1-268">Коллекция, для которой необходимо получить максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-268">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-269">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-269">Return value</span></span>

<span data-ttu-id="5b1e1-270">Целое число, представляющее максимальное значение из коллекции.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-270">An integer representing the maximum value from the collection.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-271">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-271">Example</span></span>

<span data-ttu-id="5b1e1-272">В следующем примере показано, как использовать функцию max с массивом и списком целых чисел:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-272">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="5b1e1-273">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-273">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5b1e1-274">Имя</span><span class="sxs-lookup"><span data-stu-id="5b1e1-274">Name</span></span> | <span data-ttu-id="5b1e1-275">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-275">Type</span></span> | <span data-ttu-id="5b1e1-276">Значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5b1e1-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="5b1e1-277">arrayOutput</span></span> | <span data-ttu-id="5b1e1-278">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-278">Int</span></span> | <span data-ttu-id="5b1e1-279">5</span><span class="sxs-lookup"><span data-stu-id="5b1e1-279">5</span></span> |
| <span data-ttu-id="5b1e1-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="5b1e1-280">intOutput</span></span> | <span data-ttu-id="5b1e1-281">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-281">Int</span></span> | <span data-ttu-id="5b1e1-282">5</span><span class="sxs-lookup"><span data-stu-id="5b1e1-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="5b1e1-283">mod (модуль)</span><span class="sxs-lookup"><span data-stu-id="5b1e1-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="5b1e1-284">Возвращает остаток от деления двух указанных целочисленных значений.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-284">Returns the remainder of the integer division using the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-285">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-285">Parameters</span></span>

| <span data-ttu-id="5b1e1-286">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-286">Parameter</span></span> | <span data-ttu-id="5b1e1-287">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-287">Required</span></span> | <span data-ttu-id="5b1e1-288">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-288">Type</span></span> | <span data-ttu-id="5b1e1-289">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-290">операнд1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-290">operand1</span></span> |<span data-ttu-id="5b1e1-291">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-291">Yes</span></span> |<span data-ttu-id="5b1e1-292">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-292">int</span></span> |<span data-ttu-id="5b1e1-293">Делимое.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-293">The number being divided.</span></span> |
| <span data-ttu-id="5b1e1-294">операнд2</span><span class="sxs-lookup"><span data-stu-id="5b1e1-294">operand2</span></span> |<span data-ttu-id="5b1e1-295">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-295">Yes</span></span> |<span data-ttu-id="5b1e1-296">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-296">int</span></span> |<span data-ttu-id="5b1e1-297">Делитель, не может быть равен 0.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-297">The number that is used to divide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-298">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-298">Return value</span></span>
<span data-ttu-id="5b1e1-299">Целое число, представляющее остаток.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-299">An integer representing the remainder.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-300">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-300">Example</span></span>

<span data-ttu-id="5b1e1-301">В следующем примере возвращается остаток от деления одного параметра на другой.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-301">The following example returns the remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used to divide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="5b1e1-302">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-302">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5b1e1-303">Имя</span><span class="sxs-lookup"><span data-stu-id="5b1e1-303">Name</span></span> | <span data-ttu-id="5b1e1-304">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-304">Type</span></span> | <span data-ttu-id="5b1e1-305">Значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5b1e1-306">modResult</span><span class="sxs-lookup"><span data-stu-id="5b1e1-306">modResult</span></span> | <span data-ttu-id="5b1e1-307">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-307">Int</span></span> | <span data-ttu-id="5b1e1-308">1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="5b1e1-309">mul</span><span class="sxs-lookup"><span data-stu-id="5b1e1-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="5b1e1-310">Возвращает произведение двух указанных целочисленных значений.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-310">Returns the multiplication of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-311">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-311">Parameters</span></span>

| <span data-ttu-id="5b1e1-312">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-312">Parameter</span></span> | <span data-ttu-id="5b1e1-313">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-313">Required</span></span> | <span data-ttu-id="5b1e1-314">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-314">Type</span></span> | <span data-ttu-id="5b1e1-315">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-316">операнд1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-316">operand1</span></span> |<span data-ttu-id="5b1e1-317">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-317">Yes</span></span> |<span data-ttu-id="5b1e1-318">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-318">int</span></span> |<span data-ttu-id="5b1e1-319">Первый множитель.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-319">First number to multiply.</span></span> |
| <span data-ttu-id="5b1e1-320">операнд2</span><span class="sxs-lookup"><span data-stu-id="5b1e1-320">operand2</span></span> |<span data-ttu-id="5b1e1-321">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-321">Yes</span></span> |<span data-ttu-id="5b1e1-322">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-322">int</span></span> |<span data-ttu-id="5b1e1-323">Второй множитель.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-323">Second number to multiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-324">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-324">Return value</span></span>

<span data-ttu-id="5b1e1-325">Целое число, представляющее произведение.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-325">An integer representing the multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-326">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-326">Example</span></span>

<span data-ttu-id="5b1e1-327">В следующем примере один параметр умножается на другой.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-327">The following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer to multiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer to multiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="5b1e1-328">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-328">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5b1e1-329">Имя</span><span class="sxs-lookup"><span data-stu-id="5b1e1-329">Name</span></span> | <span data-ttu-id="5b1e1-330">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-330">Type</span></span> | <span data-ttu-id="5b1e1-331">Значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5b1e1-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="5b1e1-332">mulResult</span></span> | <span data-ttu-id="5b1e1-333">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-333">Int</span></span> | <span data-ttu-id="5b1e1-334">15</span><span class="sxs-lookup"><span data-stu-id="5b1e1-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="5b1e1-335">sub</span><span class="sxs-lookup"><span data-stu-id="5b1e1-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="5b1e1-336">Возвращает разность двух указанных целочисленных значений.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-336">Returns the subtraction of the two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="5b1e1-337">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b1e1-337">Parameters</span></span>

| <span data-ttu-id="5b1e1-338">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b1e1-338">Parameter</span></span> | <span data-ttu-id="5b1e1-339">Обязательно</span><span class="sxs-lookup"><span data-stu-id="5b1e1-339">Required</span></span> | <span data-ttu-id="5b1e1-340">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-340">Type</span></span> | <span data-ttu-id="5b1e1-341">Описание</span><span class="sxs-lookup"><span data-stu-id="5b1e1-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5b1e1-342">операнд1</span><span class="sxs-lookup"><span data-stu-id="5b1e1-342">operand1</span></span> |<span data-ttu-id="5b1e1-343">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-343">Yes</span></span> |<span data-ttu-id="5b1e1-344">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-344">int</span></span> |<span data-ttu-id="5b1e1-345">Уменьшаемое.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-345">The number that is subtracted from.</span></span> |
| <span data-ttu-id="5b1e1-346">операнд2</span><span class="sxs-lookup"><span data-stu-id="5b1e1-346">operand2</span></span> |<span data-ttu-id="5b1e1-347">Да</span><span class="sxs-lookup"><span data-stu-id="5b1e1-347">Yes</span></span> |<span data-ttu-id="5b1e1-348">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-348">int</span></span> |<span data-ttu-id="5b1e1-349">Вычитаемое.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-349">The number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5b1e1-350">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-350">Return value</span></span>
<span data-ttu-id="5b1e1-351">Целое число, представляющее разность.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-351">An integer representing the subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="5b1e1-352">Пример</span><span class="sxs-lookup"><span data-stu-id="5b1e1-352">Example</span></span>

<span data-ttu-id="5b1e1-353">В следующем примере один параметр вычитается из другого.</span><span class="sxs-lookup"><span data-stu-id="5b1e1-353">The following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer to subtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="5b1e1-354">Выходные данные из предыдущего примера со значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="5b1e1-354">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5b1e1-355">Имя</span><span class="sxs-lookup"><span data-stu-id="5b1e1-355">Name</span></span> | <span data-ttu-id="5b1e1-356">Тип</span><span class="sxs-lookup"><span data-stu-id="5b1e1-356">Type</span></span> | <span data-ttu-id="5b1e1-357">Значение</span><span class="sxs-lookup"><span data-stu-id="5b1e1-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5b1e1-358">subResult</span><span class="sxs-lookup"><span data-stu-id="5b1e1-358">subResult</span></span> | <span data-ttu-id="5b1e1-359">int</span><span class="sxs-lookup"><span data-stu-id="5b1e1-359">Int</span></span> | <span data-ttu-id="5b1e1-360">4</span><span class="sxs-lookup"><span data-stu-id="5b1e1-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5b1e1-361">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b1e1-361">Next steps</span></span>
* <span data-ttu-id="5b1e1-362">Описание разделов в шаблоне Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5b1e1-362">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5b1e1-363">Инструкции по объединению нескольких шаблонов см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5b1e1-363">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="5b1e1-364">Указания по выполнению заданного количества циклов итерации при создании типа ресурса см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="5b1e1-364">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="5b1e1-365">Указания по развертыванию созданного шаблона см. в статье, посвященной [развертыванию приложения с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5b1e1-365">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

