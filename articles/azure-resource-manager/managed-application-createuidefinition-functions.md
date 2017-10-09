---
title: "aaaAzure управляемые приложения создайте определения функций пользовательского интерфейса | Документы Microsoft"
description: "Описывает toouse функции hello при создании определения пользовательского интерфейса для управляемого приложения Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="460e9-103">Функции CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="460e9-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="460e9-104">Этот раздел содержит hello подписи для всех поддерживаемые функции CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="460e9-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="460e9-105">toouse функции объявления hello заключить в квадратные скобки.</span><span class="sxs-lookup"><span data-stu-id="460e9-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="460e9-106">Например:</span><span class="sxs-lookup"><span data-stu-id="460e9-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="460e9-107">На строки и другие функции можно ссылаться как на параметры функции, но строки должны быть заключены в одинарные кавычки.</span><span class="sxs-lookup"><span data-stu-id="460e9-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="460e9-108">Например:</span><span class="sxs-lookup"><span data-stu-id="460e9-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="460e9-109">Там, где это применимо, можно указать свойства hello выходных данных функции с помощью оператора точки hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="460e9-110">Например:</span><span class="sxs-lookup"><span data-stu-id="460e9-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="460e9-111">Функции для ссылки</span><span class="sxs-lookup"><span data-stu-id="460e9-111">Referencing functions</span></span>
<span data-ttu-id="460e9-112">Эти функции могут быть выходы используется tooreference свойствами hello или контексте CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="460e9-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="460e9-113">basics</span><span class="sxs-lookup"><span data-stu-id="460e9-113">basics</span></span>
<span data-ttu-id="460e9-114">Возвращает элемент, определенный на шаге основы hello hello выходные значения.</span><span class="sxs-lookup"><span data-stu-id="460e9-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="460e9-115">Hello следующий пример возвращает выходные данные hello hello элемента с именем `foo` hello основные сведения о шаге:</span><span class="sxs-lookup"><span data-stu-id="460e9-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="460e9-116">steps</span><span class="sxs-lookup"><span data-stu-id="460e9-116">steps</span></span>
<span data-ttu-id="460e9-117">Возвращает hello выходных значений элемента, который определен в указанный шаг hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="460e9-118">использовать tooget hello выходных значений элементов на этапе основы hello `basics()` вместо него.</span><span class="sxs-lookup"><span data-stu-id="460e9-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="460e9-119">Hello следующий пример возвращает выходные данные hello hello элемента с именем `bar` на шаге hello с именем `foo`:</span><span class="sxs-lookup"><span data-stu-id="460e9-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="460e9-120">location</span><span class="sxs-lookup"><span data-stu-id="460e9-120">location</span></span>
<span data-ttu-id="460e9-121">Возвращает расположение hello, выбранного в шаге основы hello или hello текущего контекста.</span><span class="sxs-lookup"><span data-stu-id="460e9-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="460e9-122">Hello следующий пример может вернуть `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="460e9-123">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="460e9-123">String functions</span></span>
<span data-ttu-id="460e9-124">Эти функции могут использоваться только со строками JSON.</span><span class="sxs-lookup"><span data-stu-id="460e9-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="460e9-125">concat</span><span class="sxs-lookup"><span data-stu-id="460e9-125">concat</span></span>
<span data-ttu-id="460e9-126">Объединяет одну или несколько строк.</span><span class="sxs-lookup"><span data-stu-id="460e9-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="460e9-127">Например, если hello выходные значения `element1` Если `"bar"`, то этот пример возвращает строку hello `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="460e9-128">substring</span><span class="sxs-lookup"><span data-stu-id="460e9-128">substring</span></span>
<span data-ttu-id="460e9-129">Возвращает подстроку hello hello указанную строку.</span><span class="sxs-lookup"><span data-stu-id="460e9-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="460e9-130">подстрока Hello начинается с указанного индекса hello и hello указана длина.</span><span class="sxs-lookup"><span data-stu-id="460e9-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="460e9-131">Hello следующий пример возвращает `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="460e9-132">replace</span><span class="sxs-lookup"><span data-stu-id="460e9-132">replace</span></span>
<span data-ttu-id="460e9-133">Возвращает строку, в которой все вхождения hello указанную строку в текущую строку hello заменяются на другую строку.</span><span class="sxs-lookup"><span data-stu-id="460e9-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="460e9-134">Hello следующий пример возвращает `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="460e9-135">GUID</span><span class="sxs-lookup"><span data-stu-id="460e9-135">guid</span></span>
<span data-ttu-id="460e9-136">Создает глобально уникальную строку (идентификатор GUID).</span><span class="sxs-lookup"><span data-stu-id="460e9-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="460e9-137">Hello следующий пример может вернуть `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="460e9-138">toLower</span><span class="sxs-lookup"><span data-stu-id="460e9-138">toLower</span></span>
<span data-ttu-id="460e9-139">Возвращает строку, преобразованную toolowercase.</span><span class="sxs-lookup"><span data-stu-id="460e9-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="460e9-140">Hello следующий пример возвращает `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="460e9-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="460e9-141">toUpper</span></span>
<span data-ttu-id="460e9-142">Возвращает строку, преобразованную toouppercase.</span><span class="sxs-lookup"><span data-stu-id="460e9-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="460e9-143">Hello следующий пример возвращает `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="460e9-144">Функции для коллекций</span><span class="sxs-lookup"><span data-stu-id="460e9-144">Collection functions</span></span>
<span data-ttu-id="460e9-145">Эти функции могут использоваться с коллекциями, такими как строки, массивы и объекты JSON.</span><span class="sxs-lookup"><span data-stu-id="460e9-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="460e9-146">contains</span><span class="sxs-lookup"><span data-stu-id="460e9-146">contains</span></span>
<span data-ttu-id="460e9-147">Возвращает `true` Если строка содержит подстроку hello, массив содержит hello заданное значение или объект содержит указанный ключ hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="460e9-148">Пример 1: строка</span><span class="sxs-lookup"><span data-stu-id="460e9-148">Example 1: string</span></span>
<span data-ttu-id="460e9-149">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="460e9-150">Пример 2: массив</span><span class="sxs-lookup"><span data-stu-id="460e9-150">Example 2: array</span></span>
<span data-ttu-id="460e9-151">Предположим, что `element1` возвращает `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="460e9-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="460e9-152">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="460e9-153">Пример 3: объект</span><span class="sxs-lookup"><span data-stu-id="460e9-153">Example 3: object</span></span>
<span data-ttu-id="460e9-154">Предположим, что `element1` возвращает:</span><span class="sxs-lookup"><span data-stu-id="460e9-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="460e9-155">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="460e9-156">длина</span><span class="sxs-lookup"><span data-stu-id="460e9-156">length</span></span>
<span data-ttu-id="460e9-157">Возвращает hello количество символов в строке, hello число значений в массиве или hello число ключей в объект.</span><span class="sxs-lookup"><span data-stu-id="460e9-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="460e9-158">Пример 1: строка</span><span class="sxs-lookup"><span data-stu-id="460e9-158">Example 1: string</span></span>
<span data-ttu-id="460e9-159">Hello следующий пример возвращает `6`:</span><span class="sxs-lookup"><span data-stu-id="460e9-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="460e9-160">Пример 2: массив</span><span class="sxs-lookup"><span data-stu-id="460e9-160">Example 2: array</span></span>
<span data-ttu-id="460e9-161">Предположим, что `element1` возвращает `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="460e9-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="460e9-162">Hello следующий пример возвращает `3`:</span><span class="sxs-lookup"><span data-stu-id="460e9-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="460e9-163">Пример 3: объект</span><span class="sxs-lookup"><span data-stu-id="460e9-163">Example 3: object</span></span>
<span data-ttu-id="460e9-164">Предположим, что `element1` возвращает:</span><span class="sxs-lookup"><span data-stu-id="460e9-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="460e9-165">Hello следующий пример возвращает `2`:</span><span class="sxs-lookup"><span data-stu-id="460e9-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="460e9-166">empty</span><span class="sxs-lookup"><span data-stu-id="460e9-166">empty</span></span>
<span data-ttu-id="460e9-167">Возвращает `true` Если строка hello, массив или объект имеет значение null или пустым.</span><span class="sxs-lookup"><span data-stu-id="460e9-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="460e9-168">Пример 1: строка</span><span class="sxs-lookup"><span data-stu-id="460e9-168">Example 1: string</span></span>
<span data-ttu-id="460e9-169">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="460e9-170">Пример 2: массив</span><span class="sxs-lookup"><span data-stu-id="460e9-170">Example 2: array</span></span>
<span data-ttu-id="460e9-171">Предположим, что `element1` возвращает `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="460e9-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="460e9-172">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="460e9-173">Пример 3: объект</span><span class="sxs-lookup"><span data-stu-id="460e9-173">Example 3: object</span></span>
<span data-ttu-id="460e9-174">Предположим, что `element1` возвращает:</span><span class="sxs-lookup"><span data-stu-id="460e9-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="460e9-175">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="460e9-176">Пример 4: null и не определено</span><span class="sxs-lookup"><span data-stu-id="460e9-176">Example 4: null and undefined</span></span>
<span data-ttu-id="460e9-177">Предположим, что `element1` имеет значение `null` или не определено.</span><span class="sxs-lookup"><span data-stu-id="460e9-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="460e9-178">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="460e9-179">first</span><span class="sxs-lookup"><span data-stu-id="460e9-179">first</span></span>
<span data-ttu-id="460e9-180">Возвращает hello hello в первый знак заданной строкой; Первое значение из указанного массива hello; или hello первый ключ и значение указанного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="460e9-181">Пример 1: строка</span><span class="sxs-lookup"><span data-stu-id="460e9-181">Example 1: string</span></span>
<span data-ttu-id="460e9-182">Hello следующий пример возвращает `"f"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="460e9-183">Пример 2: массив</span><span class="sxs-lookup"><span data-stu-id="460e9-183">Example 2: array</span></span>
<span data-ttu-id="460e9-184">Предположим, что `element1` возвращает `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="460e9-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="460e9-185">Hello следующий пример возвращает `1`:</span><span class="sxs-lookup"><span data-stu-id="460e9-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="460e9-186">Пример 3: объект</span><span class="sxs-lookup"><span data-stu-id="460e9-186">Example 3: object</span></span>
<span data-ttu-id="460e9-187">Предположим, что `element1` возвращает:</span><span class="sxs-lookup"><span data-stu-id="460e9-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="460e9-188">Hello следующий пример возвращает `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="460e9-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="460e9-189">last</span><span class="sxs-lookup"><span data-stu-id="460e9-189">last</span></span>
<span data-ttu-id="460e9-190">Возвращает hello последним символом hello указан строка hello последнее значение указанного массива hello, или hello последний ключ и значение указанного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="460e9-191">Пример 1: строка</span><span class="sxs-lookup"><span data-stu-id="460e9-191">Example 1: string</span></span>
<span data-ttu-id="460e9-192">Hello следующий пример возвращает `"r"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="460e9-193">Пример 2: массив</span><span class="sxs-lookup"><span data-stu-id="460e9-193">Example 2: array</span></span>
<span data-ttu-id="460e9-194">Предположим, что `element1` возвращает `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="460e9-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="460e9-195">Hello следующий пример возвращает `2`:</span><span class="sxs-lookup"><span data-stu-id="460e9-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="460e9-196">Пример 3: объект</span><span class="sxs-lookup"><span data-stu-id="460e9-196">Example 3: object</span></span>
<span data-ttu-id="460e9-197">Предположим, что `element1` возвращает:</span><span class="sxs-lookup"><span data-stu-id="460e9-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="460e9-198">Hello следующий пример возвращает `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="460e9-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="460e9-199">take</span><span class="sxs-lookup"><span data-stu-id="460e9-199">take</span></span>
<span data-ttu-id="460e9-200">Возвращает указанное количество смежных символов от начала hello строку hello, указанное число последовательных значений от начала массива hello hello или указанное число последовательных ключей и значений от начала hello hello объекта.</span><span class="sxs-lookup"><span data-stu-id="460e9-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="460e9-201">Пример 1: строка</span><span class="sxs-lookup"><span data-stu-id="460e9-201">Example 1: string</span></span>
<span data-ttu-id="460e9-202">Hello следующий пример возвращает `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="460e9-203">Пример 2: массив</span><span class="sxs-lookup"><span data-stu-id="460e9-203">Example 2: array</span></span>
<span data-ttu-id="460e9-204">Предположим, что `element1` возвращает `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="460e9-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="460e9-205">Hello следующий пример возвращает `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="460e9-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="460e9-206">Пример 3: объект</span><span class="sxs-lookup"><span data-stu-id="460e9-206">Example 3: object</span></span>
<span data-ttu-id="460e9-207">Предположим, что `element1` возвращает:</span><span class="sxs-lookup"><span data-stu-id="460e9-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="460e9-208">Hello следующий пример возвращает `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="460e9-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="460e9-209">skip</span><span class="sxs-lookup"><span data-stu-id="460e9-209">skip</span></span>
<span data-ttu-id="460e9-210">Пропускает заданное число элементов в коллекции и возвращает hello остальных элементов.</span><span class="sxs-lookup"><span data-stu-id="460e9-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="460e9-211">Пример 1: строка</span><span class="sxs-lookup"><span data-stu-id="460e9-211">Example 1: string</span></span>
<span data-ttu-id="460e9-212">Hello следующий пример возвращает `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="460e9-213">Пример 2: массив</span><span class="sxs-lookup"><span data-stu-id="460e9-213">Example 2: array</span></span>
<span data-ttu-id="460e9-214">Предположим, что `element1` возвращает `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="460e9-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="460e9-215">Hello следующий пример возвращает `[3]`:</span><span class="sxs-lookup"><span data-stu-id="460e9-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="460e9-216">Пример 3: объект</span><span class="sxs-lookup"><span data-stu-id="460e9-216">Example 3: object</span></span>
<span data-ttu-id="460e9-217">Предположим, что `element1` возвращает:</span><span class="sxs-lookup"><span data-stu-id="460e9-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="460e9-218">Hello следующий пример возвращает `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="460e9-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="460e9-219">Логические функции</span><span class="sxs-lookup"><span data-stu-id="460e9-219">Logical functions</span></span>
<span data-ttu-id="460e9-220">Эти функции можно использовать в условных выражениях.</span><span class="sxs-lookup"><span data-stu-id="460e9-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="460e9-221">Некоторые функции не поддерживают все типы данных JSON.</span><span class="sxs-lookup"><span data-stu-id="460e9-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="460e9-222">equals (равно)</span><span class="sxs-lookup"><span data-stu-id="460e9-222">equals</span></span>
<span data-ttu-id="460e9-223">Возвращает `true` Если оба параметра имеют hello же тип и значение.</span><span class="sxs-lookup"><span data-stu-id="460e9-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="460e9-224">Эта функция поддерживает все типы данных JSON.</span><span class="sxs-lookup"><span data-stu-id="460e9-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="460e9-225">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="460e9-226">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="460e9-227">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="460e9-228">less</span><span class="sxs-lookup"><span data-stu-id="460e9-228">less</span></span>
<span data-ttu-id="460e9-229">Возвращает `true` Если hello первый параметр является строго меньше значения второго параметра hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="460e9-230">Эта функция поддерживает только параметры типа "число" и "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="460e9-231">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="460e9-232">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="460e9-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="460e9-233">lessOrEquals</span></span>
<span data-ttu-id="460e9-234">Возвращает `true` Если hello первый параметр меньше или равно toohello второго параметра.</span><span class="sxs-lookup"><span data-stu-id="460e9-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="460e9-235">Эта функция поддерживает только параметры типа "число" и "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="460e9-236">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="460e9-237">greater</span><span class="sxs-lookup"><span data-stu-id="460e9-237">greater</span></span>
<span data-ttu-id="460e9-238">Возвращает `true` первый параметр hello строго больше значения второго параметра hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="460e9-239">Эта функция поддерживает только параметры типа "число" и "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="460e9-240">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="460e9-241">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="460e9-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="460e9-242">greaterOrEquals</span></span>
<span data-ttu-id="460e9-243">Возвращает `true` Если hello первого параметра больше или равно toohello второго параметра.</span><span class="sxs-lookup"><span data-stu-id="460e9-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="460e9-244">Эта функция поддерживает только параметры типа "число" и "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="460e9-245">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="460e9-246">и</span><span class="sxs-lookup"><span data-stu-id="460e9-246">and</span></span>
<span data-ttu-id="460e9-247">Возвращает `true` Если все параметры hello принимают слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="460e9-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="460e9-248">Эта функция поддерживает два или более параметров только логического типа.</span><span class="sxs-lookup"><span data-stu-id="460e9-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="460e9-249">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="460e9-250">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="460e9-251">или</span><span class="sxs-lookup"><span data-stu-id="460e9-251">or</span></span>
<span data-ttu-id="460e9-252">Возвращает `true` Если хотя бы один из параметров hello оценивает слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="460e9-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="460e9-253">Эта функция поддерживает два или более параметров только логического типа.</span><span class="sxs-lookup"><span data-stu-id="460e9-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="460e9-254">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="460e9-255">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="460e9-256">not</span><span class="sxs-lookup"><span data-stu-id="460e9-256">not</span></span>
<span data-ttu-id="460e9-257">Возвращает `true` Если hello параметр принимает слишком`false`.</span><span class="sxs-lookup"><span data-stu-id="460e9-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="460e9-258">Эта функция поддерживает только параметры логического типа.</span><span class="sxs-lookup"><span data-stu-id="460e9-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="460e9-259">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="460e9-260">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="460e9-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="460e9-261">coalesce</span></span>
<span data-ttu-id="460e9-262">Возвращает hello значение первого параметра ненулевой hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="460e9-263">Эта функция поддерживает все типы данных JSON.</span><span class="sxs-lookup"><span data-stu-id="460e9-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="460e9-264">Предположим, что `element1` и `element2` не определены.</span><span class="sxs-lookup"><span data-stu-id="460e9-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="460e9-265">Hello следующий пример возвращает `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="460e9-266">Функции преобразования</span><span class="sxs-lookup"><span data-stu-id="460e9-266">Conversion functions</span></span>
<span data-ttu-id="460e9-267">Эти функции могут принимать значения используется tooconvert между типами данных JSON и кодировки.</span><span class="sxs-lookup"><span data-stu-id="460e9-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="460e9-268">int</span><span class="sxs-lookup"><span data-stu-id="460e9-268">int</span></span>
<span data-ttu-id="460e9-269">Преобразует целое tooan параметр hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="460e9-270">Эта функция поддерживает параметры типа "число" и "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="460e9-271">Hello следующий пример возвращает `1`:</span><span class="sxs-lookup"><span data-stu-id="460e9-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="460e9-272">Hello следующий пример возвращает `2`:</span><span class="sxs-lookup"><span data-stu-id="460e9-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="460e9-273">float;</span><span class="sxs-lookup"><span data-stu-id="460e9-273">float</span></span>
<span data-ttu-id="460e9-274">Преобразует hello параметр tooa с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="460e9-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="460e9-275">Эта функция поддерживает параметры типа "число" и "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="460e9-276">Hello следующий пример возвращает `1.0`:</span><span class="sxs-lookup"><span data-stu-id="460e9-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="460e9-277">Hello следующий пример возвращает `2.9`:</span><span class="sxs-lookup"><span data-stu-id="460e9-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="460e9-278">string</span><span class="sxs-lookup"><span data-stu-id="460e9-278">string</span></span>
<span data-ttu-id="460e9-279">Преобразует строку tooa параметр hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="460e9-280">Эта функция поддерживает параметры всех типов данных JSON.</span><span class="sxs-lookup"><span data-stu-id="460e9-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="460e9-281">Hello следующий пример возвращает `"1"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="460e9-282">Hello следующий пример возвращает `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="460e9-283">Hello следующий пример возвращает `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="460e9-284">Hello следующий пример возвращает `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="460e9-285">bool</span><span class="sxs-lookup"><span data-stu-id="460e9-285">bool</span></span>
<span data-ttu-id="460e9-286">Преобразует параметр hello tooa логическое значение.</span><span class="sxs-lookup"><span data-stu-id="460e9-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="460e9-287">Эта функция поддерживает параметры типа "число", "строка" и "логическое значение".</span><span class="sxs-lookup"><span data-stu-id="460e9-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="460e9-288">Аналогичные tooBooleans на языке JavaScript, любое значение, кроме `0` или `'false'` возвращает `true`.</span><span class="sxs-lookup"><span data-stu-id="460e9-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="460e9-289">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="460e9-290">Hello следующий пример возвращает `false`:</span><span class="sxs-lookup"><span data-stu-id="460e9-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="460e9-291">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="460e9-292">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="460e9-293">parse</span><span class="sxs-lookup"><span data-stu-id="460e9-293">parse</span></span>
<span data-ttu-id="460e9-294">Преобразует собственный тип параметра hello tooa.</span><span class="sxs-lookup"><span data-stu-id="460e9-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="460e9-295">Другими словами, эта функция представляет обратное hello `string()`.</span><span class="sxs-lookup"><span data-stu-id="460e9-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="460e9-296">Эта функция поддерживает только параметры типа "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="460e9-297">Hello следующий пример возвращает `1`:</span><span class="sxs-lookup"><span data-stu-id="460e9-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="460e9-298">Hello следующий пример возвращает `true`:</span><span class="sxs-lookup"><span data-stu-id="460e9-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="460e9-299">Hello следующий пример возвращает `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="460e9-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="460e9-300">Hello следующий пример возвращает `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="460e9-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="460e9-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="460e9-301">encodeBase64</span></span>
<span data-ttu-id="460e9-302">Кодирует закодированную строку hello параметр tooa base-64.</span><span class="sxs-lookup"><span data-stu-id="460e9-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="460e9-303">Эта функция поддерживает только параметры типа "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="460e9-304">Hello следующий пример возвращает `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="460e9-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="460e9-305">decodeBase64</span></span>
<span data-ttu-id="460e9-306">Декодирует hello параметра из строка в кодировке base-64.</span><span class="sxs-lookup"><span data-stu-id="460e9-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="460e9-307">Эта функция поддерживает только параметры типа "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="460e9-308">Hello следующий пример возвращает `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="460e9-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="460e9-309">encodeUriComponent</span></span>
<span data-ttu-id="460e9-310">Кодирует строку в кодировке URL-адрес tooa параметр hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="460e9-311">Эта функция поддерживает только параметры типа "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="460e9-312">Hello следующий пример возвращает `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="460e9-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="460e9-313">decodeUriComponent</span></span>
<span data-ttu-id="460e9-314">Декодирует hello параметра из строки в кодировке URL.</span><span class="sxs-lookup"><span data-stu-id="460e9-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="460e9-315">Эта функция поддерживает только параметры типа "строка".</span><span class="sxs-lookup"><span data-stu-id="460e9-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="460e9-316">Hello следующий пример возвращает `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="460e9-317">Математические функции</span><span class="sxs-lookup"><span data-stu-id="460e9-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="460e9-318">добавление</span><span class="sxs-lookup"><span data-stu-id="460e9-318">add</span></span>
<span data-ttu-id="460e9-319">Складывает два числа и возвращает результат hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="460e9-320">Hello следующий пример возвращает `3`:</span><span class="sxs-lookup"><span data-stu-id="460e9-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="460e9-321">sub</span><span class="sxs-lookup"><span data-stu-id="460e9-321">sub</span></span>
<span data-ttu-id="460e9-322">Вычитает второе число hello из первого hello и возвращает результат hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="460e9-323">Hello следующий пример возвращает `1`:</span><span class="sxs-lookup"><span data-stu-id="460e9-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="460e9-324">mul</span><span class="sxs-lookup"><span data-stu-id="460e9-324">mul</span></span>
<span data-ttu-id="460e9-325">Умножает два числа и возвращает результат hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="460e9-326">Hello следующий пример возвращает `6`:</span><span class="sxs-lookup"><span data-stu-id="460e9-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="460e9-327">div</span><span class="sxs-lookup"><span data-stu-id="460e9-327">div</span></span>
<span data-ttu-id="460e9-328">Делит первый число hello на второй hello и возвращает результат hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="460e9-329">Hello результат всегда является целочисленным.</span><span class="sxs-lookup"><span data-stu-id="460e9-329">hello result is always an integer.</span></span>

<span data-ttu-id="460e9-330">Hello следующий пример возвращает `2`:</span><span class="sxs-lookup"><span data-stu-id="460e9-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="460e9-331">mod (модуль)</span><span class="sxs-lookup"><span data-stu-id="460e9-331">mod</span></span>
<span data-ttu-id="460e9-332">Делит первый число hello на второй hello и возвращает остаток hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="460e9-333">Hello следующий пример возвращает `0`:</span><span class="sxs-lookup"><span data-stu-id="460e9-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="460e9-334">Hello следующий пример возвращает `2`:</span><span class="sxs-lookup"><span data-stu-id="460e9-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="460e9-335">Min</span><span class="sxs-lookup"><span data-stu-id="460e9-335">min</span></span>
<span data-ttu-id="460e9-336">Возвращает hello малых hello двух чисел.</span><span class="sxs-lookup"><span data-stu-id="460e9-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="460e9-337">Hello следующий пример возвращает `1`:</span><span class="sxs-lookup"><span data-stu-id="460e9-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="460e9-338">max</span><span class="sxs-lookup"><span data-stu-id="460e9-338">max</span></span>
<span data-ttu-id="460e9-339">Hello возвращает большее из двух чисел hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="460e9-340">Hello следующий пример возвращает `2`:</span><span class="sxs-lookup"><span data-stu-id="460e9-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="460e9-341">range</span><span class="sxs-lookup"><span data-stu-id="460e9-341">range</span></span>
<span data-ttu-id="460e9-342">Формирует последовательность из целого числа в hello указан диапазон.</span><span class="sxs-lookup"><span data-stu-id="460e9-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="460e9-343">Hello следующий пример возвращает `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="460e9-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="460e9-344">rand</span><span class="sxs-lookup"><span data-stu-id="460e9-344">rand</span></span>
<span data-ttu-id="460e9-345">Возвращает случайное целым числом в пределах hello указанного диапазона.</span><span class="sxs-lookup"><span data-stu-id="460e9-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="460e9-346">Эта функция не создает криптографически безопасное случайное число.</span><span class="sxs-lookup"><span data-stu-id="460e9-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="460e9-347">Hello следующий пример может вернуть `42`:</span><span class="sxs-lookup"><span data-stu-id="460e9-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="460e9-348">floor</span><span class="sxs-lookup"><span data-stu-id="460e9-348">floor</span></span>
<span data-ttu-id="460e9-349">Возвращает наибольшее целое число hello меньше или равно toohello указанное число.</span><span class="sxs-lookup"><span data-stu-id="460e9-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="460e9-350">Hello следующий пример возвращает `3`:</span><span class="sxs-lookup"><span data-stu-id="460e9-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="460e9-351">ceil</span><span class="sxs-lookup"><span data-stu-id="460e9-351">ceil</span></span>
<span data-ttu-id="460e9-352">Здравствуйте, возвращает наибольшее целое число, больше или равно toohello указанное число.</span><span class="sxs-lookup"><span data-stu-id="460e9-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="460e9-353">Hello следующий пример возвращает `4`:</span><span class="sxs-lookup"><span data-stu-id="460e9-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="460e9-354">Функции данных</span><span class="sxs-lookup"><span data-stu-id="460e9-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="460e9-355">utcnow</span><span class="sxs-lookup"><span data-stu-id="460e9-355">utcNow</span></span>
<span data-ttu-id="460e9-356">Возвращает строку в формате ISO 8601 hello текущую дату и время на локальном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="460e9-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="460e9-357">Hello следующий пример может вернуть `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="460e9-358">addseconds</span><span class="sxs-lookup"><span data-stu-id="460e9-358">addSeconds</span></span>
<span data-ttu-id="460e9-359">Добавляет целому числу секунд toohello указан отметки времени.</span><span class="sxs-lookup"><span data-stu-id="460e9-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="460e9-360">Hello следующий пример возвращает `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="460e9-361">addminutes</span><span class="sxs-lookup"><span data-stu-id="460e9-361">addMinutes</span></span>
<span data-ttu-id="460e9-362">Добавляет целое количество минут toohello указан отметки времени.</span><span class="sxs-lookup"><span data-stu-id="460e9-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="460e9-363">Hello следующий пример возвращает `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="460e9-364">addhours</span><span class="sxs-lookup"><span data-stu-id="460e9-364">addHours</span></span>
<span data-ttu-id="460e9-365">Добавляет целое количество часов toohello указан отметки времени.</span><span class="sxs-lookup"><span data-stu-id="460e9-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="460e9-366">Hello следующий пример возвращает `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="460e9-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="460e9-367">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="460e9-367">Next steps</span></span>
* <span data-ttu-id="460e9-368">Введение tooAzure диспетчера ресурсов. в разделе [Обзор диспетчера ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="460e9-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

