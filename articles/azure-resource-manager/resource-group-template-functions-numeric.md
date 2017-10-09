---
title: "aaaAzure диспетчер ресурсов шаблона функции - числовых | Документы Microsoft"
description: "Описывает toouse функции hello в toowork шаблона диспетчера ресурсов Azure с номерами."
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="f0a0e-103">Числовые функции для шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f0a0e-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="f0a0e-104">Диспетчер ресурсов предоставляет следующие функции для работы с целыми числами hello:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="f0a0e-105">добавление</span><span class="sxs-lookup"><span data-stu-id="f0a0e-105">add</span></span>](#add)
* [<span data-ttu-id="f0a0e-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="f0a0e-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="f0a0e-107">div</span><span class="sxs-lookup"><span data-stu-id="f0a0e-107">div</span></span>](#div)
* [<span data-ttu-id="f0a0e-108">float</span><span class="sxs-lookup"><span data-stu-id="f0a0e-108">float</span></span>](#float)
* [<span data-ttu-id="f0a0e-109">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-109">int</span></span>](#int)
* [<span data-ttu-id="f0a0e-110">min</span><span class="sxs-lookup"><span data-stu-id="f0a0e-110">min</span></span>](#min)
* [<span data-ttu-id="f0a0e-111">max</span><span class="sxs-lookup"><span data-stu-id="f0a0e-111">max</span></span>](#max)
* [<span data-ttu-id="f0a0e-112">mod (модуль)</span><span class="sxs-lookup"><span data-stu-id="f0a0e-112">mod</span></span>](#mod)
* [<span data-ttu-id="f0a0e-113">mul</span><span class="sxs-lookup"><span data-stu-id="f0a0e-113">mul</span></span>](#mul)
* [<span data-ttu-id="f0a0e-114">sub</span><span class="sxs-lookup"><span data-stu-id="f0a0e-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="f0a0e-115">добавление</span><span class="sxs-lookup"><span data-stu-id="f0a0e-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="f0a0e-116">Возвращает hello сумму hello двух указанных целых чисел.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-117">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-117">Parameters</span></span>

| <span data-ttu-id="f0a0e-118">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-118">Parameter</span></span> | <span data-ttu-id="f0a0e-119">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-119">Required</span></span> | <span data-ttu-id="f0a0e-120">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-120">Type</span></span> | <span data-ttu-id="f0a0e-121">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="f0a0e-122">операнд1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-122">operand1</span></span> |<span data-ttu-id="f0a0e-123">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-123">Yes</span></span> |<span data-ttu-id="f0a0e-124">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-124">int</span></span> |<span data-ttu-id="f0a0e-125">Первый номер tooadd.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-125">First number tooadd.</span></span> |
|<span data-ttu-id="f0a0e-126">операнд2</span><span class="sxs-lookup"><span data-stu-id="f0a0e-126">operand2</span></span> |<span data-ttu-id="f0a0e-127">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-127">Yes</span></span> |<span data-ttu-id="f0a0e-128">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-128">int</span></span> |<span data-ttu-id="f0a0e-129">Во-вторых, номер tooadd.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-130">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-130">Return value</span></span>

<span data-ttu-id="f0a0e-131">Целое число, содержащее sum hello hello параметров.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-132">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-132">Example</span></span>

<span data-ttu-id="f0a0e-133">Следующий пример Hello добавляются два параметра.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
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

<span data-ttu-id="f0a0e-134">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f0a0e-135">Имя</span><span class="sxs-lookup"><span data-stu-id="f0a0e-135">Name</span></span> | <span data-ttu-id="f0a0e-136">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-136">Type</span></span> | <span data-ttu-id="f0a0e-137">Значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f0a0e-138">addResult</span><span class="sxs-lookup"><span data-stu-id="f0a0e-138">addResult</span></span> | <span data-ttu-id="f0a0e-139">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-139">Int</span></span> | <span data-ttu-id="f0a0e-140">8</span><span class="sxs-lookup"><span data-stu-id="f0a0e-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="f0a0e-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="f0a0e-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="f0a0e-142">Возвращает hello индекса итерации цикла.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="f0a0e-143">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-143">Parameters</span></span>

| <span data-ttu-id="f0a0e-144">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-144">Parameter</span></span> | <span data-ttu-id="f0a0e-145">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-145">Required</span></span> | <span data-ttu-id="f0a0e-146">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-146">Type</span></span> | <span data-ttu-id="f0a0e-147">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-148">loopName</span><span class="sxs-lookup"><span data-stu-id="f0a0e-148">loopName</span></span> | <span data-ttu-id="f0a0e-149">Нет</span><span class="sxs-lookup"><span data-stu-id="f0a0e-149">No</span></span> | <span data-ttu-id="f0a0e-150">string</span><span class="sxs-lookup"><span data-stu-id="f0a0e-150">string</span></span> | <span data-ttu-id="f0a0e-151">Имя Hello цикла hello Начало итерации hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="f0a0e-152">offset</span><span class="sxs-lookup"><span data-stu-id="f0a0e-152">offset</span></span> |<span data-ttu-id="f0a0e-153">Нет</span><span class="sxs-lookup"><span data-stu-id="f0a0e-153">No</span></span> |<span data-ttu-id="f0a0e-154">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-154">int</span></span> |<span data-ttu-id="f0a0e-155">Hello номеров tooadd toohello отсчитываемый от нуля значение итерации.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="f0a0e-156">Примечания</span><span class="sxs-lookup"><span data-stu-id="f0a0e-156">Remarks</span></span>

<span data-ttu-id="f0a0e-157">Эта функция всегда используется с объектом **copy**.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="f0a0e-158">Если значение не указано для **смещение**, возвращается значение текущей итерации hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="f0a0e-159">значение итерации Hello начинается с нуля.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="f0a0e-160">Hello **loopName** свойства можно toospecify ли ссылается copyIndex tooa ресурсов итерации или свойства итерации.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="f0a0e-161">Если значение не указано для **loopName**, используется hello текущей итерации типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="f0a0e-162">Укажите значение **loopName** при выполнении итерации по свойству.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="f0a0e-163">Полное описание использования **copyIndex** см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0e-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-164">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-164">Example</span></span>

<span data-ttu-id="f0a0e-165">Hello пример копирования цикла hello индекса значения и включен в имя hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

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

### <a name="return-value"></a><span data-ttu-id="f0a0e-166">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-166">Return value</span></span>

<span data-ttu-id="f0a0e-167">Целое число, представляющее текущий индекс hello hello итерации.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="f0a0e-168">div</span><span class="sxs-lookup"><span data-stu-id="f0a0e-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="f0a0e-169">Возвращает hello целочисленное деление двух указанных целых чисел hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-170">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-170">Parameters</span></span>

| <span data-ttu-id="f0a0e-171">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-171">Parameter</span></span> | <span data-ttu-id="f0a0e-172">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-172">Required</span></span> | <span data-ttu-id="f0a0e-173">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-173">Type</span></span> | <span data-ttu-id="f0a0e-174">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-175">операнд1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-175">operand1</span></span> |<span data-ttu-id="f0a0e-176">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-176">Yes</span></span> |<span data-ttu-id="f0a0e-177">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-177">int</span></span> |<span data-ttu-id="f0a0e-178">Номер Hello как разделение.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-178">hello number being divided.</span></span> |
| <span data-ttu-id="f0a0e-179">операнд2</span><span class="sxs-lookup"><span data-stu-id="f0a0e-179">operand2</span></span> |<span data-ttu-id="f0a0e-180">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-180">Yes</span></span> |<span data-ttu-id="f0a0e-181">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-181">int</span></span> |<span data-ttu-id="f0a0e-182">число Hello, используемые toodivide.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-182">hello number that is used toodivide.</span></span> <span data-ttu-id="f0a0e-183">Не может иметь значение 0.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-184">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-184">Return value</span></span>

<span data-ttu-id="f0a0e-185">Целочисленное представляющих hello деление.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-186">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-186">Example</span></span>

<span data-ttu-id="f0a0e-187">Следующий пример Hello делит один параметр с другим параметром.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-187">hello following example divides one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="f0a0e-188">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f0a0e-189">Имя</span><span class="sxs-lookup"><span data-stu-id="f0a0e-189">Name</span></span> | <span data-ttu-id="f0a0e-190">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-190">Type</span></span> | <span data-ttu-id="f0a0e-191">Значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f0a0e-192">divResult</span><span class="sxs-lookup"><span data-stu-id="f0a0e-192">divResult</span></span> | <span data-ttu-id="f0a0e-193">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-193">Int</span></span> | <span data-ttu-id="f0a0e-194">2</span><span class="sxs-lookup"><span data-stu-id="f0a0e-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="f0a0e-195">float;</span><span class="sxs-lookup"><span data-stu-id="f0a0e-195">float</span></span>
`float(arg1)`

<span data-ttu-id="f0a0e-196">Преобразует число с плавающей запятой tooa значение hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="f0a0e-197">Только эта функция выполняется при передаче пользовательских параметров tooan приложения, например приложения логики.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-198">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-198">Parameters</span></span>

| <span data-ttu-id="f0a0e-199">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-199">Parameter</span></span> | <span data-ttu-id="f0a0e-200">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-200">Required</span></span> | <span data-ttu-id="f0a0e-201">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-201">Type</span></span> | <span data-ttu-id="f0a0e-202">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-203">arg1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-203">arg1</span></span> |<span data-ttu-id="f0a0e-204">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-204">Yes</span></span> |<span data-ttu-id="f0a0e-205">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="f0a0e-205">string or int</span></span> |<span data-ttu-id="f0a0e-206">Здравствуйте, tooa tooconvert значение с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-207">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-207">Return value</span></span>
<span data-ttu-id="f0a0e-208">Число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-209">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-209">Example</span></span>

<span data-ttu-id="f0a0e-210">Hello в следующем примере показано, как toouse float tooa toopass параметры приложения логики:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

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

## <a name="int"></a><span data-ttu-id="f0a0e-211">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="f0a0e-212">Преобразует целое tooan hello указанное значение.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-213">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-213">Parameters</span></span>

| <span data-ttu-id="f0a0e-214">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-214">Parameter</span></span> | <span data-ttu-id="f0a0e-215">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-215">Required</span></span> | <span data-ttu-id="f0a0e-216">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-216">Type</span></span> | <span data-ttu-id="f0a0e-217">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="f0a0e-218">valueToConvert</span></span> |<span data-ttu-id="f0a0e-219">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-219">Yes</span></span> |<span data-ttu-id="f0a0e-220">строка или целое число</span><span class="sxs-lookup"><span data-stu-id="f0a0e-220">string or int</span></span> |<span data-ttu-id="f0a0e-221">Hello значение tooconvert tooan целое число со знаком.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-222">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-222">Return value</span></span>

<span data-ttu-id="f0a0e-223">Целое hello преобразованное значение.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-224">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-224">Example</span></span>

<span data-ttu-id="f0a0e-225">Hello следующий пример преобразует значение toointeger hello пользовательских параметров.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

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

<span data-ttu-id="f0a0e-226">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f0a0e-227">Имя</span><span class="sxs-lookup"><span data-stu-id="f0a0e-227">Name</span></span> | <span data-ttu-id="f0a0e-228">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-228">Type</span></span> | <span data-ttu-id="f0a0e-229">Значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f0a0e-230">intResult</span><span class="sxs-lookup"><span data-stu-id="f0a0e-230">intResult</span></span> | <span data-ttu-id="f0a0e-231">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-231">Int</span></span> | <span data-ttu-id="f0a0e-232">4.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="f0a0e-233">Min</span><span class="sxs-lookup"><span data-stu-id="f0a0e-233">min</span></span>
`min (arg1)`

<span data-ttu-id="f0a0e-234">Возвращает hello минимальное значение из массива целых чисел или разделителями запятыми списка целых чисел.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-235">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-235">Parameters</span></span>

| <span data-ttu-id="f0a0e-236">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-236">Parameter</span></span> | <span data-ttu-id="f0a0e-237">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-237">Required</span></span> | <span data-ttu-id="f0a0e-238">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-238">Type</span></span> | <span data-ttu-id="f0a0e-239">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-240">arg1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-240">arg1</span></span> |<span data-ttu-id="f0a0e-241">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-241">Yes</span></span> |<span data-ttu-id="f0a0e-242">массив целых чисел или разделенный запятыми список целых чисел</span><span class="sxs-lookup"><span data-stu-id="f0a0e-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="f0a0e-243">Hello коллекции tooget hello минимальное значение.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-244">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-244">Return value</span></span>

<span data-ttu-id="f0a0e-245">Целое число, представляющее минимальное значение из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-246">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-246">Example</span></span>

<span data-ttu-id="f0a0e-247">Следующий пример показывает как Hello min toouse с массивом и список целых чисел:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="f0a0e-248">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f0a0e-249">Имя</span><span class="sxs-lookup"><span data-stu-id="f0a0e-249">Name</span></span> | <span data-ttu-id="f0a0e-250">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-250">Type</span></span> | <span data-ttu-id="f0a0e-251">Значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f0a0e-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="f0a0e-252">arrayOutput</span></span> | <span data-ttu-id="f0a0e-253">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-253">Int</span></span> | <span data-ttu-id="f0a0e-254">0</span><span class="sxs-lookup"><span data-stu-id="f0a0e-254">0</span></span> |
| <span data-ttu-id="f0a0e-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="f0a0e-255">intOutput</span></span> | <span data-ttu-id="f0a0e-256">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-256">Int</span></span> | <span data-ttu-id="f0a0e-257">0</span><span class="sxs-lookup"><span data-stu-id="f0a0e-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="f0a0e-258">max</span><span class="sxs-lookup"><span data-stu-id="f0a0e-258">max</span></span>
`max (arg1)`

<span data-ttu-id="f0a0e-259">Возвращает hello максимальное значение из массива целых чисел или разделителями запятыми списка целых чисел.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-260">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-260">Parameters</span></span>

| <span data-ttu-id="f0a0e-261">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-261">Parameter</span></span> | <span data-ttu-id="f0a0e-262">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-262">Required</span></span> | <span data-ttu-id="f0a0e-263">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-263">Type</span></span> | <span data-ttu-id="f0a0e-264">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-265">arg1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-265">arg1</span></span> |<span data-ttu-id="f0a0e-266">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-266">Yes</span></span> |<span data-ttu-id="f0a0e-267">массив целых чисел или разделенный запятыми список целых чисел</span><span class="sxs-lookup"><span data-stu-id="f0a0e-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="f0a0e-268">Hello коллекции tooget hello максимальное значение.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-269">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-269">Return value</span></span>

<span data-ttu-id="f0a0e-270">Целое число, представляющее максимальное значение hello из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-271">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-271">Example</span></span>

<span data-ttu-id="f0a0e-272">Следующий пример показывает как Hello toouse max с массивом и список целых чисел:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="f0a0e-273">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f0a0e-274">Имя</span><span class="sxs-lookup"><span data-stu-id="f0a0e-274">Name</span></span> | <span data-ttu-id="f0a0e-275">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-275">Type</span></span> | <span data-ttu-id="f0a0e-276">Значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f0a0e-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="f0a0e-277">arrayOutput</span></span> | <span data-ttu-id="f0a0e-278">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-278">Int</span></span> | <span data-ttu-id="f0a0e-279">5</span><span class="sxs-lookup"><span data-stu-id="f0a0e-279">5</span></span> |
| <span data-ttu-id="f0a0e-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="f0a0e-280">intOutput</span></span> | <span data-ttu-id="f0a0e-281">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-281">Int</span></span> | <span data-ttu-id="f0a0e-282">5</span><span class="sxs-lookup"><span data-stu-id="f0a0e-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="f0a0e-283">mod (модуль)</span><span class="sxs-lookup"><span data-stu-id="f0a0e-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="f0a0e-284">Возвращает остаток hello hello целочисленное деление использованием hello указанных значений.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-285">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-285">Parameters</span></span>

| <span data-ttu-id="f0a0e-286">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-286">Parameter</span></span> | <span data-ttu-id="f0a0e-287">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-287">Required</span></span> | <span data-ttu-id="f0a0e-288">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-288">Type</span></span> | <span data-ttu-id="f0a0e-289">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-290">операнд1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-290">operand1</span></span> |<span data-ttu-id="f0a0e-291">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-291">Yes</span></span> |<span data-ttu-id="f0a0e-292">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-292">int</span></span> |<span data-ttu-id="f0a0e-293">Номер Hello как разделение.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-293">hello number being divided.</span></span> |
| <span data-ttu-id="f0a0e-294">операнд2</span><span class="sxs-lookup"><span data-stu-id="f0a0e-294">operand2</span></span> |<span data-ttu-id="f0a0e-295">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-295">Yes</span></span> |<span data-ttu-id="f0a0e-296">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-296">int</span></span> |<span data-ttu-id="f0a0e-297">число Hello, которое используется toodivide не может быть 0.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-298">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-298">Return value</span></span>
<span data-ttu-id="f0a0e-299">Целое число со знаком представляющих hello остаток.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-300">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-300">Example</span></span>

<span data-ttu-id="f0a0e-301">Hello следующий пример возвращает hello остаток от деления одного параметра с другим параметром.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

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
                "description": "Integer used toodivide"
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

<span data-ttu-id="f0a0e-302">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f0a0e-303">Имя</span><span class="sxs-lookup"><span data-stu-id="f0a0e-303">Name</span></span> | <span data-ttu-id="f0a0e-304">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-304">Type</span></span> | <span data-ttu-id="f0a0e-305">Значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f0a0e-306">modResult</span><span class="sxs-lookup"><span data-stu-id="f0a0e-306">modResult</span></span> | <span data-ttu-id="f0a0e-307">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-307">Int</span></span> | <span data-ttu-id="f0a0e-308">1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="f0a0e-309">mul</span><span class="sxs-lookup"><span data-stu-id="f0a0e-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="f0a0e-310">Возвращает hello умножение двух указанных целых чисел hello.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-311">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-311">Parameters</span></span>

| <span data-ttu-id="f0a0e-312">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-312">Parameter</span></span> | <span data-ttu-id="f0a0e-313">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-313">Required</span></span> | <span data-ttu-id="f0a0e-314">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-314">Type</span></span> | <span data-ttu-id="f0a0e-315">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-316">операнд1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-316">operand1</span></span> |<span data-ttu-id="f0a0e-317">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-317">Yes</span></span> |<span data-ttu-id="f0a0e-318">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-318">int</span></span> |<span data-ttu-id="f0a0e-319">Первый номер toomultiply.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-319">First number toomultiply.</span></span> |
| <span data-ttu-id="f0a0e-320">операнд2</span><span class="sxs-lookup"><span data-stu-id="f0a0e-320">operand2</span></span> |<span data-ttu-id="f0a0e-321">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-321">Yes</span></span> |<span data-ttu-id="f0a0e-322">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-322">int</span></span> |<span data-ttu-id="f0a0e-323">Во-вторых, номер toomultiply.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-324">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-324">Return value</span></span>

<span data-ttu-id="f0a0e-325">Представляющих hello умножение.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-326">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-326">Example</span></span>

<span data-ttu-id="f0a0e-327">Следующий пример Hello умножает один параметр с другим параметром.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
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

<span data-ttu-id="f0a0e-328">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f0a0e-329">Имя</span><span class="sxs-lookup"><span data-stu-id="f0a0e-329">Name</span></span> | <span data-ttu-id="f0a0e-330">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-330">Type</span></span> | <span data-ttu-id="f0a0e-331">Значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f0a0e-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="f0a0e-332">mulResult</span></span> | <span data-ttu-id="f0a0e-333">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-333">Int</span></span> | <span data-ttu-id="f0a0e-334">15</span><span class="sxs-lookup"><span data-stu-id="f0a0e-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="f0a0e-335">sub</span><span class="sxs-lookup"><span data-stu-id="f0a0e-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="f0a0e-336">Возвращает hello вычитания hello двух указанных целых чисел.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="f0a0e-337">Параметры</span><span class="sxs-lookup"><span data-stu-id="f0a0e-337">Parameters</span></span>

| <span data-ttu-id="f0a0e-338">Параметр</span><span class="sxs-lookup"><span data-stu-id="f0a0e-338">Parameter</span></span> | <span data-ttu-id="f0a0e-339">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f0a0e-339">Required</span></span> | <span data-ttu-id="f0a0e-340">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-340">Type</span></span> | <span data-ttu-id="f0a0e-341">Описание</span><span class="sxs-lookup"><span data-stu-id="f0a0e-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f0a0e-342">операнд1</span><span class="sxs-lookup"><span data-stu-id="f0a0e-342">operand1</span></span> |<span data-ttu-id="f0a0e-343">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-343">Yes</span></span> |<span data-ttu-id="f0a0e-344">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-344">int</span></span> |<span data-ttu-id="f0a0e-345">число Hello, которое вычитается из.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="f0a0e-346">операнд2</span><span class="sxs-lookup"><span data-stu-id="f0a0e-346">operand2</span></span> |<span data-ttu-id="f0a0e-347">Да</span><span class="sxs-lookup"><span data-stu-id="f0a0e-347">Yes</span></span> |<span data-ttu-id="f0a0e-348">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-348">int</span></span> |<span data-ttu-id="f0a0e-349">число Hello, которое вычитается.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f0a0e-350">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-350">Return value</span></span>
<span data-ttu-id="f0a0e-351">Целое число со знаком представляющих hello вычитания.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="f0a0e-352">Пример</span><span class="sxs-lookup"><span data-stu-id="f0a0e-352">Example</span></span>

<span data-ttu-id="f0a0e-353">Следующий пример Hello вычитает один параметр из другого параметра.</span><span class="sxs-lookup"><span data-stu-id="f0a0e-353">hello following example subtracts one parameter from another parameter.</span></span>

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
                "description": "Integer toosubtract"
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

<span data-ttu-id="f0a0e-354">Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:</span><span class="sxs-lookup"><span data-stu-id="f0a0e-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="f0a0e-355">Имя</span><span class="sxs-lookup"><span data-stu-id="f0a0e-355">Name</span></span> | <span data-ttu-id="f0a0e-356">Тип</span><span class="sxs-lookup"><span data-stu-id="f0a0e-356">Type</span></span> | <span data-ttu-id="f0a0e-357">Значение</span><span class="sxs-lookup"><span data-stu-id="f0a0e-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f0a0e-358">subResult</span><span class="sxs-lookup"><span data-stu-id="f0a0e-358">subResult</span></span> | <span data-ttu-id="f0a0e-359">int</span><span class="sxs-lookup"><span data-stu-id="f0a0e-359">Int</span></span> | <span data-ttu-id="f0a0e-360">4</span><span class="sxs-lookup"><span data-stu-id="f0a0e-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0a0e-361">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0a0e-361">Next steps</span></span>
* <span data-ttu-id="f0a0e-362">Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0e-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f0a0e-363">toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0e-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="f0a0e-364">tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0e-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="f0a0e-365">toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0e-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

