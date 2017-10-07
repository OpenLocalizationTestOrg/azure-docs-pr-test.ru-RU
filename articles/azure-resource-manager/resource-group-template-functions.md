---
title: "aaaResource функции шаблона диспетчера | Документы Microsoft"
description: "Описывает toouse функции hello в значениях tooretrieve шаблона диспетчера ресурсов Azure, работы со строками и числовые значения и получить сведения о развертывании."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="4f95c-103">Функции шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="4f95c-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="4f95c-104">В этом разделе описываются все функции hello, которые можно использовать в шаблоне диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="4f95c-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="4f95c-105">Функции нужно добавлять в шаблоны, заключая их в скобки `[` и `]` соответственно.</span><span class="sxs-lookup"><span data-stu-id="4f95c-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="4f95c-106">Hello выражение вычисляется во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="4f95c-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="4f95c-107">Во время записи как строковый литерал hello результат вычисления выражения hello может быть другого типа JSON, например массиву, объекта или целое число со знаком.</span><span class="sxs-lookup"><span data-stu-id="4f95c-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="4f95c-108">Как и в языке JavaScript, вызовы функций форматируются так: `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="4f95c-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="4f95c-109">Ссылки на свойства с помощью операторов [index] и точками hello.</span><span class="sxs-lookup"><span data-stu-id="4f95c-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="4f95c-110">Выражение шаблона не может превышать 24 576 знаков.</span><span class="sxs-lookup"><span data-stu-id="4f95c-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="4f95c-111">Функции шаблонов и их параметры зависят от регистра.</span><span class="sxs-lookup"><span data-stu-id="4f95c-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="4f95c-112">Например, диспетчер ресурсов преобразует **variables('var1')** и **VARIABLES('VAR1')** как же hello.</span><span class="sxs-lookup"><span data-stu-id="4f95c-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="4f95c-113">При вычислении, если функция hello явно не изменяет регистр (например toUpper или toLower), функции hello сохраняет регистр hello.</span><span class="sxs-lookup"><span data-stu-id="4f95c-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="4f95c-114">Для некоторых типов ресурсов требования к регистру могут не зависеть от того, как происходит вычисление функций.</span><span class="sxs-lookup"><span data-stu-id="4f95c-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="4f95c-115">Функции массива и объекта</span><span class="sxs-lookup"><span data-stu-id="4f95c-115">Array and object functions</span></span>
<span data-ttu-id="4f95c-116">Resource Manager предоставляет ряд функций для работы с массивами и объектами.</span><span class="sxs-lookup"><span data-stu-id="4f95c-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* <span data-ttu-id="4f95c-117">[array](resource-group-template-functions-array.md#array).</span><span class="sxs-lookup"><span data-stu-id="4f95c-117">[array](resource-group-template-functions-array.md#array)</span></span>
* [<span data-ttu-id="4f95c-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="4f95c-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="4f95c-119">concat</span><span class="sxs-lookup"><span data-stu-id="4f95c-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="4f95c-120">contains</span><span class="sxs-lookup"><span data-stu-id="4f95c-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="4f95c-121">createArray</span><span class="sxs-lookup"><span data-stu-id="4f95c-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="4f95c-122">empty</span><span class="sxs-lookup"><span data-stu-id="4f95c-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="4f95c-123">first</span><span class="sxs-lookup"><span data-stu-id="4f95c-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="4f95c-124">intersection</span><span class="sxs-lookup"><span data-stu-id="4f95c-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="4f95c-125">json</span><span class="sxs-lookup"><span data-stu-id="4f95c-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="4f95c-126">last</span><span class="sxs-lookup"><span data-stu-id="4f95c-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="4f95c-127">длина</span><span class="sxs-lookup"><span data-stu-id="4f95c-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="4f95c-128">min</span><span class="sxs-lookup"><span data-stu-id="4f95c-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="4f95c-129">max</span><span class="sxs-lookup"><span data-stu-id="4f95c-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="4f95c-130">range</span><span class="sxs-lookup"><span data-stu-id="4f95c-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="4f95c-131">skip</span><span class="sxs-lookup"><span data-stu-id="4f95c-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="4f95c-132">take</span><span class="sxs-lookup"><span data-stu-id="4f95c-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="4f95c-133">union</span><span class="sxs-lookup"><span data-stu-id="4f95c-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="4f95c-134">Функции сравнения</span><span class="sxs-lookup"><span data-stu-id="4f95c-134">Comparison functions</span></span>
<span data-ttu-id="4f95c-135">Resource Manager предоставляет ряд функций для выполнения сравнений в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="4f95c-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="4f95c-136">equals</span><span class="sxs-lookup"><span data-stu-id="4f95c-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="4f95c-137">less</span><span class="sxs-lookup"><span data-stu-id="4f95c-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="4f95c-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="4f95c-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="4f95c-139">greater</span><span class="sxs-lookup"><span data-stu-id="4f95c-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="4f95c-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="4f95c-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="4f95c-141">Функции для параметров развертывания</span><span class="sxs-lookup"><span data-stu-id="4f95c-141">Deployment value functions</span></span>
<span data-ttu-id="4f95c-142">Диспетчер ресурсов предоставляет hello следующие функции для получения значения из разделов шаблона hello и значения связанных toohello развертывания:</span><span class="sxs-lookup"><span data-stu-id="4f95c-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="4f95c-143">deployment</span><span class="sxs-lookup"><span data-stu-id="4f95c-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="4f95c-144">parameters</span><span class="sxs-lookup"><span data-stu-id="4f95c-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="4f95c-145">variables</span><span class="sxs-lookup"><span data-stu-id="4f95c-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="4f95c-146">Логические функции</span><span class="sxs-lookup"><span data-stu-id="4f95c-146">Logical functions</span></span>
<span data-ttu-id="4f95c-147">Диспетчер ресурсов предоставляет следующие функции для работы с логических условий hello:</span><span class="sxs-lookup"><span data-stu-id="4f95c-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* <span data-ttu-id="4f95c-148">[and](resource-group-template-functions-logical.md#and) (и);</span><span class="sxs-lookup"><span data-stu-id="4f95c-148">[and](resource-group-template-functions-logical.md#and)</span></span>
* <span data-ttu-id="4f95c-149">[bool](resource-group-template-functions-logical.md#bool);</span><span class="sxs-lookup"><span data-stu-id="4f95c-149">[bool](resource-group-template-functions-logical.md#bool)</span></span>
* <span data-ttu-id="4f95c-150">[if](resource-group-template-functions-logical.md#if) (если);</span><span class="sxs-lookup"><span data-stu-id="4f95c-150">[if](resource-group-template-functions-logical.md#if)</span></span>
* <span data-ttu-id="4f95c-151">[not](resource-group-template-functions-logical.md#not) (не);</span><span class="sxs-lookup"><span data-stu-id="4f95c-151">[not](resource-group-template-functions-logical.md#not)</span></span>
* <span data-ttu-id="4f95c-152">[or](resource-group-template-functions-logical.md#or) (или).</span><span class="sxs-lookup"><span data-stu-id="4f95c-152">[or](resource-group-template-functions-logical.md#or)</span></span>

## <a name="numeric-functions"></a><span data-ttu-id="4f95c-153">Числовые функции</span><span class="sxs-lookup"><span data-stu-id="4f95c-153">Numeric functions</span></span>
<span data-ttu-id="4f95c-154">Диспетчер ресурсов предоставляет следующие функции для работы с целыми числами hello:</span><span class="sxs-lookup"><span data-stu-id="4f95c-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="4f95c-155">добавление</span><span class="sxs-lookup"><span data-stu-id="4f95c-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="4f95c-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="4f95c-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="4f95c-157">div</span><span class="sxs-lookup"><span data-stu-id="4f95c-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="4f95c-158">float</span><span class="sxs-lookup"><span data-stu-id="4f95c-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="4f95c-159">int</span><span class="sxs-lookup"><span data-stu-id="4f95c-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="4f95c-160">min</span><span class="sxs-lookup"><span data-stu-id="4f95c-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="4f95c-161">max</span><span class="sxs-lookup"><span data-stu-id="4f95c-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="4f95c-162">mod (модуль)</span><span class="sxs-lookup"><span data-stu-id="4f95c-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="4f95c-163">mul</span><span class="sxs-lookup"><span data-stu-id="4f95c-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="4f95c-164">sub</span><span class="sxs-lookup"><span data-stu-id="4f95c-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="4f95c-165">Функции для работы с ресурсами</span><span class="sxs-lookup"><span data-stu-id="4f95c-165">Resource functions</span></span>
<span data-ttu-id="4f95c-166">Диспетчер ресурсов предоставляет следующие функции для получения значений ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="4f95c-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="4f95c-167">listKeys и list{Value}</span><span class="sxs-lookup"><span data-stu-id="4f95c-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="4f95c-168">providers</span><span class="sxs-lookup"><span data-stu-id="4f95c-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="4f95c-169">reference</span><span class="sxs-lookup"><span data-stu-id="4f95c-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="4f95c-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="4f95c-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="4f95c-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="4f95c-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="4f95c-172">subscription</span><span class="sxs-lookup"><span data-stu-id="4f95c-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="4f95c-173">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="4f95c-173">String functions</span></span>
<span data-ttu-id="4f95c-174">Диспетчер ресурсов предоставляет следующие функции для работы со строками hello:</span><span class="sxs-lookup"><span data-stu-id="4f95c-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="4f95c-175">base64</span><span class="sxs-lookup"><span data-stu-id="4f95c-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="4f95c-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="4f95c-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="4f95c-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="4f95c-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="4f95c-178">concat</span><span class="sxs-lookup"><span data-stu-id="4f95c-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="4f95c-179">contains</span><span class="sxs-lookup"><span data-stu-id="4f95c-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="4f95c-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="4f95c-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="4f95c-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="4f95c-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="4f95c-182">empty</span><span class="sxs-lookup"><span data-stu-id="4f95c-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="4f95c-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="4f95c-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="4f95c-184">first</span><span class="sxs-lookup"><span data-stu-id="4f95c-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="4f95c-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="4f95c-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="4f95c-186">last</span><span class="sxs-lookup"><span data-stu-id="4f95c-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="4f95c-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="4f95c-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="4f95c-188">длина</span><span class="sxs-lookup"><span data-stu-id="4f95c-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="4f95c-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="4f95c-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="4f95c-190">replace</span><span class="sxs-lookup"><span data-stu-id="4f95c-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="4f95c-191">skip</span><span class="sxs-lookup"><span data-stu-id="4f95c-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="4f95c-192">split</span><span class="sxs-lookup"><span data-stu-id="4f95c-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="4f95c-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="4f95c-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="4f95c-194">string</span><span class="sxs-lookup"><span data-stu-id="4f95c-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="4f95c-195">substring</span><span class="sxs-lookup"><span data-stu-id="4f95c-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="4f95c-196">take</span><span class="sxs-lookup"><span data-stu-id="4f95c-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="4f95c-197">toLower</span><span class="sxs-lookup"><span data-stu-id="4f95c-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="4f95c-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="4f95c-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="4f95c-199">trim</span><span class="sxs-lookup"><span data-stu-id="4f95c-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="4f95c-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="4f95c-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="4f95c-201">uri</span><span class="sxs-lookup"><span data-stu-id="4f95c-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="4f95c-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="4f95c-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="4f95c-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="4f95c-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="4f95c-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f95c-204">Next steps</span></span>
* <span data-ttu-id="4f95c-205">Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны создания диспетчера ресурсов Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="4f95c-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="4f95c-206">toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="4f95c-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="4f95c-207">tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="4f95c-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="4f95c-208">toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона диспетчера ресурсов Azure](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="4f95c-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

