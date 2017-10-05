---
title: "Функции шаблона Resource Manager | Документация Майкрософт"
description: "Описывает функции, используемые в шаблоне диспетчера ресурсов Azure для извлечения значений, работы со строками и числовыми значениями и получения сведений о развертывании."
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
ms.openlocfilehash: 1324bed07e991e9d84cb6832afe78bdb2d3348fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="1ef7c-103">Функции шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="1ef7c-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="1ef7c-104">В этом разделе описаны все функции, которые можно использовать в шаблоне Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-104">This topic describes all the functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="1ef7c-105">Функции нужно добавлять в шаблоны, заключая их в скобки `[` и `]` соответственно.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="1ef7c-106">Выражение вычисляется во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-106">The expression is evaluated during deployment.</span></span> <span data-ttu-id="1ef7c-107">Хотя результат вычисления выражения и записывается как строковый литерал, он может иметь другой тип JSON, например массив, объект или целое число.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-107">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="1ef7c-108">Как и в языке JavaScript, вызовы функций форматируются так: `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="1ef7c-109">Обращение к свойствам производится с помощью точки и операторов [index].</span><span class="sxs-lookup"><span data-stu-id="1ef7c-109">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="1ef7c-110">Выражение шаблона не может превышать 24 576 знаков.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="1ef7c-111">Функции шаблонов и их параметры зависят от регистра.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="1ef7c-112">Например, Resource Manager одинаково преобразует **variables('var1')** и **VARIABLES('VAR1')**.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as the same.</span></span> <span data-ttu-id="1ef7c-113">При вычислении функция сохранит регистр, если его изменение не является ее явным предназначением (например, функции toUpper и toLower).</span><span class="sxs-lookup"><span data-stu-id="1ef7c-113">When evaluated, unless the function expressly modifies case (such as toUpper or toLower), the function preserves the case.</span></span> <span data-ttu-id="1ef7c-114">Для некоторых типов ресурсов требования к регистру могут не зависеть от того, как происходит вычисление функций.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

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

## <a name="array-and-object-functions"></a><span data-ttu-id="1ef7c-115">Функции массива и объекта</span><span class="sxs-lookup"><span data-stu-id="1ef7c-115">Array and object functions</span></span>
<span data-ttu-id="1ef7c-116">Resource Manager предоставляет ряд функций для работы с массивами и объектами.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* <span data-ttu-id="1ef7c-117">[array](resource-group-template-functions-array.md#array).</span><span class="sxs-lookup"><span data-stu-id="1ef7c-117">[array](resource-group-template-functions-array.md#array)</span></span>
* [<span data-ttu-id="1ef7c-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="1ef7c-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="1ef7c-119">concat</span><span class="sxs-lookup"><span data-stu-id="1ef7c-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="1ef7c-120">contains</span><span class="sxs-lookup"><span data-stu-id="1ef7c-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="1ef7c-121">createArray</span><span class="sxs-lookup"><span data-stu-id="1ef7c-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="1ef7c-122">empty</span><span class="sxs-lookup"><span data-stu-id="1ef7c-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="1ef7c-123">first</span><span class="sxs-lookup"><span data-stu-id="1ef7c-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="1ef7c-124">intersection</span><span class="sxs-lookup"><span data-stu-id="1ef7c-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="1ef7c-125">json</span><span class="sxs-lookup"><span data-stu-id="1ef7c-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="1ef7c-126">last</span><span class="sxs-lookup"><span data-stu-id="1ef7c-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="1ef7c-127">длина</span><span class="sxs-lookup"><span data-stu-id="1ef7c-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="1ef7c-128">min</span><span class="sxs-lookup"><span data-stu-id="1ef7c-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="1ef7c-129">max</span><span class="sxs-lookup"><span data-stu-id="1ef7c-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="1ef7c-130">range</span><span class="sxs-lookup"><span data-stu-id="1ef7c-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="1ef7c-131">skip</span><span class="sxs-lookup"><span data-stu-id="1ef7c-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="1ef7c-132">take</span><span class="sxs-lookup"><span data-stu-id="1ef7c-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="1ef7c-133">union</span><span class="sxs-lookup"><span data-stu-id="1ef7c-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="1ef7c-134">Функции сравнения</span><span class="sxs-lookup"><span data-stu-id="1ef7c-134">Comparison functions</span></span>
<span data-ttu-id="1ef7c-135">Resource Manager предоставляет ряд функций для выполнения сравнений в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="1ef7c-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="1ef7c-136">equals</span><span class="sxs-lookup"><span data-stu-id="1ef7c-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="1ef7c-137">less</span><span class="sxs-lookup"><span data-stu-id="1ef7c-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="1ef7c-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="1ef7c-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="1ef7c-139">greater</span><span class="sxs-lookup"><span data-stu-id="1ef7c-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="1ef7c-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="1ef7c-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="1ef7c-141">Функции для параметров развертывания</span><span class="sxs-lookup"><span data-stu-id="1ef7c-141">Deployment value functions</span></span>
<span data-ttu-id="1ef7c-142">Диспетчер ресурсов предоставляет следующие функции для получения значений из разделов шаблонов и значений, связанных с развертыванием:</span><span class="sxs-lookup"><span data-stu-id="1ef7c-142">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="1ef7c-143">deployment</span><span class="sxs-lookup"><span data-stu-id="1ef7c-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="1ef7c-144">parameters</span><span class="sxs-lookup"><span data-stu-id="1ef7c-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="1ef7c-145">variables</span><span class="sxs-lookup"><span data-stu-id="1ef7c-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

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

## <a name="logical-functions"></a><span data-ttu-id="1ef7c-146">Логические функции</span><span class="sxs-lookup"><span data-stu-id="1ef7c-146">Logical functions</span></span>
<span data-ttu-id="1ef7c-147">Resource Manager предоставляет для работы с логическими условиями следующие функции:</span><span class="sxs-lookup"><span data-stu-id="1ef7c-147">Resource Manager provides the following functions for working with logical conditions:</span></span>

* <span data-ttu-id="1ef7c-148">[and](resource-group-template-functions-logical.md#and) (и);</span><span class="sxs-lookup"><span data-stu-id="1ef7c-148">[and](resource-group-template-functions-logical.md#and)</span></span>
* <span data-ttu-id="1ef7c-149">[bool](resource-group-template-functions-logical.md#bool);</span><span class="sxs-lookup"><span data-stu-id="1ef7c-149">[bool](resource-group-template-functions-logical.md#bool)</span></span>
* <span data-ttu-id="1ef7c-150">[if](resource-group-template-functions-logical.md#if) (если);</span><span class="sxs-lookup"><span data-stu-id="1ef7c-150">[if](resource-group-template-functions-logical.md#if)</span></span>
* <span data-ttu-id="1ef7c-151">[not](resource-group-template-functions-logical.md#not) (не);</span><span class="sxs-lookup"><span data-stu-id="1ef7c-151">[not](resource-group-template-functions-logical.md#not)</span></span>
* <span data-ttu-id="1ef7c-152">[or](resource-group-template-functions-logical.md#or) (или).</span><span class="sxs-lookup"><span data-stu-id="1ef7c-152">[or](resource-group-template-functions-logical.md#or)</span></span>

## <a name="numeric-functions"></a><span data-ttu-id="1ef7c-153">Числовые функции</span><span class="sxs-lookup"><span data-stu-id="1ef7c-153">Numeric functions</span></span>
<span data-ttu-id="1ef7c-154">Диспетчер ресурсов предоставляет следующие функции для работы с целыми числами:</span><span class="sxs-lookup"><span data-stu-id="1ef7c-154">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="1ef7c-155">добавление</span><span class="sxs-lookup"><span data-stu-id="1ef7c-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="1ef7c-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="1ef7c-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="1ef7c-157">div</span><span class="sxs-lookup"><span data-stu-id="1ef7c-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="1ef7c-158">float</span><span class="sxs-lookup"><span data-stu-id="1ef7c-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="1ef7c-159">int</span><span class="sxs-lookup"><span data-stu-id="1ef7c-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="1ef7c-160">min</span><span class="sxs-lookup"><span data-stu-id="1ef7c-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="1ef7c-161">max</span><span class="sxs-lookup"><span data-stu-id="1ef7c-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="1ef7c-162">mod (модуль)</span><span class="sxs-lookup"><span data-stu-id="1ef7c-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="1ef7c-163">mul</span><span class="sxs-lookup"><span data-stu-id="1ef7c-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="1ef7c-164">sub</span><span class="sxs-lookup"><span data-stu-id="1ef7c-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="1ef7c-165">Функции для работы с ресурсами</span><span class="sxs-lookup"><span data-stu-id="1ef7c-165">Resource functions</span></span>
<span data-ttu-id="1ef7c-166">Диспетчер ресурсов предоставляет следующие функции для получения значений ресурсов:</span><span class="sxs-lookup"><span data-stu-id="1ef7c-166">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="1ef7c-167">listKeys и list{Value}</span><span class="sxs-lookup"><span data-stu-id="1ef7c-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="1ef7c-168">providers</span><span class="sxs-lookup"><span data-stu-id="1ef7c-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="1ef7c-169">reference</span><span class="sxs-lookup"><span data-stu-id="1ef7c-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="1ef7c-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="1ef7c-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="1ef7c-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="1ef7c-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="1ef7c-172">subscription</span><span class="sxs-lookup"><span data-stu-id="1ef7c-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

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

## <a name="string-functions"></a><span data-ttu-id="1ef7c-173">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="1ef7c-173">String functions</span></span>
<span data-ttu-id="1ef7c-174">Диспетчер ресурсов предоставляет следующие функции для работы со строками:</span><span class="sxs-lookup"><span data-stu-id="1ef7c-174">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="1ef7c-175">base64</span><span class="sxs-lookup"><span data-stu-id="1ef7c-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="1ef7c-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="1ef7c-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="1ef7c-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="1ef7c-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="1ef7c-178">concat</span><span class="sxs-lookup"><span data-stu-id="1ef7c-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="1ef7c-179">contains</span><span class="sxs-lookup"><span data-stu-id="1ef7c-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="1ef7c-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="1ef7c-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="1ef7c-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="1ef7c-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="1ef7c-182">empty</span><span class="sxs-lookup"><span data-stu-id="1ef7c-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="1ef7c-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="1ef7c-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="1ef7c-184">first</span><span class="sxs-lookup"><span data-stu-id="1ef7c-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="1ef7c-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="1ef7c-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="1ef7c-186">last</span><span class="sxs-lookup"><span data-stu-id="1ef7c-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="1ef7c-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="1ef7c-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="1ef7c-188">длина</span><span class="sxs-lookup"><span data-stu-id="1ef7c-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="1ef7c-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="1ef7c-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="1ef7c-190">replace</span><span class="sxs-lookup"><span data-stu-id="1ef7c-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="1ef7c-191">skip</span><span class="sxs-lookup"><span data-stu-id="1ef7c-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="1ef7c-192">split</span><span class="sxs-lookup"><span data-stu-id="1ef7c-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="1ef7c-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="1ef7c-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="1ef7c-194">string</span><span class="sxs-lookup"><span data-stu-id="1ef7c-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="1ef7c-195">substring</span><span class="sxs-lookup"><span data-stu-id="1ef7c-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="1ef7c-196">take</span><span class="sxs-lookup"><span data-stu-id="1ef7c-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="1ef7c-197">toLower</span><span class="sxs-lookup"><span data-stu-id="1ef7c-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="1ef7c-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="1ef7c-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="1ef7c-199">trim</span><span class="sxs-lookup"><span data-stu-id="1ef7c-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="1ef7c-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="1ef7c-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="1ef7c-201">uri</span><span class="sxs-lookup"><span data-stu-id="1ef7c-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="1ef7c-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="1ef7c-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="1ef7c-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="1ef7c-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="1ef7c-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ef7c-204">Next steps</span></span>
* <span data-ttu-id="1ef7c-205">Описание разделов в шаблоне Azure Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1ef7c-205">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="1ef7c-206">Инструкции по объединению нескольких шаблонов см. в статье [Использование связанных шаблонов в Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1ef7c-206">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="1ef7c-207">Указания по выполнению заданного количества циклов итерации при создании типа см. в разделе [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1ef7c-207">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="1ef7c-208">Указания по развертыванию созданного шаблона см. в статье [Развертывание приложения с использованием шаблона диспетчера ресурсов Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1ef7c-208">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

