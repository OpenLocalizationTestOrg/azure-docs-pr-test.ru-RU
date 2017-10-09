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
# <a name="createuidefinition-functions"></a>Функции CreateUiDefinition
Этот раздел содержит hello подписи для всех поддерживаемые функции CreateUiDefinition.

toouse функции объявления hello заключить в квадратные скобки. Например:

```json
"[function()]"
```

На строки и другие функции можно ссылаться как на параметры функции, но строки должны быть заключены в одинарные кавычки. Например:

```json
"[fn1(fn2(), 'foobar')]"
```

Там, где это применимо, можно указать свойства hello выходных данных функции с помощью оператора точки hello. Например:

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>Функции для ссылки
Эти функции могут быть выходы используется tooreference свойствами hello или контексте CreateUiDefinition.

### <a name="basics"></a>basics
Возвращает элемент, определенный на шаге основы hello hello выходные значения.

Hello следующий пример возвращает выходные данные hello hello элемента с именем `foo` hello основные сведения о шаге:

```json
"[basics('foo')]"
```

### <a name="steps"></a>steps
Возвращает hello выходных значений элемента, который определен в указанный шаг hello. использовать tooget hello выходных значений элементов на этапе основы hello `basics()` вместо него.

Hello следующий пример возвращает выходные данные hello hello элемента с именем `bar` на шаге hello с именем `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Возвращает расположение hello, выбранного в шаге основы hello или hello текущего контекста.

Hello следующий пример может вернуть `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>Строковые функции
Эти функции могут использоваться только со строками JSON.

### <a name="concat"></a>concat
Объединяет одну или несколько строк.

Например, если hello выходные значения `element1` Если `"bar"`, то этот пример возвращает строку hello `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
Возвращает подстроку hello hello указанную строку. подстрока Hello начинается с указанного индекса hello и hello указана длина.

Hello следующий пример возвращает `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>replace
Возвращает строку, в которой все вхождения hello указанную строку в текущую строку hello заменяются на другую строку.

Hello следующий пример возвращает `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>GUID
Создает глобально уникальную строку (идентификатор GUID).

Hello следующий пример может вернуть `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
Возвращает строку, преобразованную toolowercase.

Hello следующий пример возвращает `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
Возвращает строку, преобразованную toouppercase.

Hello следующий пример возвращает `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>Функции для коллекций
Эти функции могут использоваться с коллекциями, такими как строки, массивы и объекты JSON.

### <a name="contains"></a>contains
Возвращает `true` Если строка содержит подстроку hello, массив содержит hello заданное значение или объект содержит указанный ключ hello.

#### <a name="example-1-string"></a>Пример 1: строка
Hello следующий пример возвращает `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>Пример 2: массив
Предположим, что `element1` возвращает `[1, 2, 3]`. Hello следующий пример возвращает `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>Пример 3: объект
Предположим, что `element1` возвращает:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello следующий пример возвращает `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>длина
Возвращает hello количество символов в строке, hello число значений в массиве или hello число ключей в объект.

#### <a name="example-1-string"></a>Пример 1: строка
Hello следующий пример возвращает `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>Пример 2: массив
Предположим, что `element1` возвращает `[1, 2, 3]`. Hello следующий пример возвращает `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Пример 3: объект
Предположим, что `element1` возвращает:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello следующий пример возвращает `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>empty
Возвращает `true` Если строка hello, массив или объект имеет значение null или пустым.

#### <a name="example-1-string"></a>Пример 1: строка
Hello следующий пример возвращает `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>Пример 2: массив
Предположим, что `element1` возвращает `[1, 2, 3]`. Hello следующий пример возвращает `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Пример 3: объект
Предположим, что `element1` возвращает:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello следующий пример возвращает `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>Пример 4: null и не определено
Предположим, что `element1` имеет значение `null` или не определено. Hello следующий пример возвращает `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>first
Возвращает hello hello в первый знак заданной строкой; Первое значение из указанного массива hello; или hello первый ключ и значение указанного объекта hello.

#### <a name="example-1-string"></a>Пример 1: строка
Hello следующий пример возвращает `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>Пример 2: массив
Предположим, что `element1` возвращает `[1, 2, 3]`. Hello следующий пример возвращает `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Пример 3: объект
Предположим, что `element1` возвращает:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Hello следующий пример возвращает `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>last
Возвращает hello последним символом hello указан строка hello последнее значение указанного массива hello, или hello последний ключ и значение указанного объекта hello.

#### <a name="example-1-string"></a>Пример 1: строка
Hello следующий пример возвращает `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>Пример 2: массив
Предположим, что `element1` возвращает `[1, 2, 3]`. Hello следующий пример возвращает `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Пример 3: объект
Предположим, что `element1` возвращает:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello следующий пример возвращает `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>take
Возвращает указанное количество смежных символов от начала hello строку hello, указанное число последовательных значений от начала массива hello hello или указанное число последовательных ключей и значений от начала hello hello объекта.

#### <a name="example-1-string"></a>Пример 1: строка
Hello следующий пример возвращает `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>Пример 2: массив
Предположим, что `element1` возвращает `[1, 2, 3]`. Hello следующий пример возвращает `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Пример 3: объект
Предположим, что `element1` возвращает:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Hello следующий пример возвращает `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>skip
Пропускает заданное число элементов в коллекции и возвращает hello остальных элементов.

#### <a name="example-1-string"></a>Пример 1: строка
Hello следующий пример возвращает `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>Пример 2: массив
Предположим, что `element1` возвращает `[1, 2, 3]`. Hello следующий пример возвращает `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Пример 3: объект
Предположим, что `element1` возвращает:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Hello следующий пример возвращает `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>Логические функции
Эти функции можно использовать в условных выражениях. Некоторые функции не поддерживают все типы данных JSON.

### <a name="equals"></a>equals (равно)
Возвращает `true` Если оба параметра имеют hello же тип и значение. Эта функция поддерживает все типы данных JSON.

Hello следующий пример возвращает `true`:

```json
"[equals(0, 0)]"
```

Hello следующий пример возвращает `true`:

```json
"[equals('foo', 'foo')]"
```

Hello следующий пример возвращает `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>less
Возвращает `true` Если hello первый параметр является строго меньше значения второго параметра hello. Эта функция поддерживает только параметры типа "число" и "строка".

Hello следующий пример возвращает `true`:

```json
"[less(1, 2)]"
```

Hello следующий пример возвращает `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
Возвращает `true` Если hello первый параметр меньше или равно toohello второго параметра. Эта функция поддерживает только параметры типа "число" и "строка".

Hello следующий пример возвращает `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>greater
Возвращает `true` первый параметр hello строго больше значения второго параметра hello. Эта функция поддерживает только параметры типа "число" и "строка".

Hello следующий пример возвращает `false`:

```json
"[greater(1, 2)]"
```

Hello следующий пример возвращает `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
Возвращает `true` Если hello первого параметра больше или равно toohello второго параметра. Эта функция поддерживает только параметры типа "число" и "строка".

Hello следующий пример возвращает `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>и
Возвращает `true` Если все параметры hello принимают слишком`true`. Эта функция поддерживает два или более параметров только логического типа.

Hello следующий пример возвращает `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Hello следующий пример возвращает `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>или
Возвращает `true` Если хотя бы один из параметров hello оценивает слишком`true`. Эта функция поддерживает два или более параметров только логического типа.

Hello следующий пример возвращает `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Hello следующий пример возвращает `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>not
Возвращает `true` Если hello параметр принимает слишком`false`. Эта функция поддерживает только параметры логического типа.

Hello следующий пример возвращает `true`:

```json
"[not(false)]"
```

Hello следующий пример возвращает `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>coalesce
Возвращает hello значение первого параметра ненулевой hello. Эта функция поддерживает все типы данных JSON.

Предположим, что `element1` и `element2` не определены. Hello следующий пример возвращает `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>Функции преобразования
Эти функции могут принимать значения используется tooconvert между типами данных JSON и кодировки.

### <a name="int"></a>int
Преобразует целое tooan параметр hello. Эта функция поддерживает параметры типа "число" и "строка".

Hello следующий пример возвращает `1`:

```json
"[int('1')]"
```

Hello следующий пример возвращает `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>float;
Преобразует hello параметр tooa с плавающей запятой. Эта функция поддерживает параметры типа "число" и "строка".

Hello следующий пример возвращает `1.0`:

```json
"[float('1.0')]"
```

Hello следующий пример возвращает `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>string
Преобразует строку tooa параметр hello. Эта функция поддерживает параметры всех типов данных JSON.

Hello следующий пример возвращает `"1"`:

```json
"[string(1)]"
```

Hello следующий пример возвращает `"2.9"`:

```json
"[string(2.9)]"
```

Hello следующий пример возвращает `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

Hello следующий пример возвращает `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>bool
Преобразует параметр hello tooa логическое значение. Эта функция поддерживает параметры типа "число", "строка" и "логическое значение". Аналогичные tooBooleans на языке JavaScript, любое значение, кроме `0` или `'false'` возвращает `true`.

Hello следующий пример возвращает `true`:

```json
"[bool(1)]"
```

Hello следующий пример возвращает `false`:

```json
"[bool(0)]"
```

Hello следующий пример возвращает `true`:

```json
"[bool(true)]"
```

Hello следующий пример возвращает `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>parse
Преобразует собственный тип параметра hello tooa. Другими словами, эта функция представляет обратное hello `string()`. Эта функция поддерживает только параметры типа "строка".

Hello следующий пример возвращает `1`:

```json
"[parse('1')]"
```

Hello следующий пример возвращает `true`:

```json
"[parse('true')]"
```

Hello следующий пример возвращает `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

Hello следующий пример возвращает `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Кодирует закодированную строку hello параметр tooa base-64. Эта функция поддерживает только параметры типа "строка".

Hello следующий пример возвращает `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Декодирует hello параметра из строка в кодировке base-64. Эта функция поддерживает только параметры типа "строка".

Hello следующий пример возвращает `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeUriComponent
Кодирует строку в кодировке URL-адрес tooa параметр hello. Эта функция поддерживает только параметры типа "строка".

Hello следующий пример возвращает `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeUriComponent
Декодирует hello параметра из строки в кодировке URL. Эта функция поддерживает только параметры типа "строка".

Hello следующий пример возвращает `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>Математические функции
### <a name="add"></a>добавление
Складывает два числа и возвращает результат hello.

Hello следующий пример возвращает `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>sub
Вычитает второе число hello из первого hello и возвращает результат hello.

Hello следующий пример возвращает `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
Умножает два числа и возвращает результат hello.

Hello следующий пример возвращает `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
Делит первый число hello на второй hello и возвращает результат hello. Hello результат всегда является целочисленным.

Hello следующий пример возвращает `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod (модуль)
Делит первый число hello на второй hello и возвращает остаток hello.

Hello следующий пример возвращает `0`:

```json
"[mod(6, 3)]"
```

Hello следующий пример возвращает `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>Min
Возвращает hello малых hello двух чисел.

Hello следующий пример возвращает `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>max
Hello возвращает большее из двух чисел hello.

Hello следующий пример возвращает `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>range
Формирует последовательность из целого числа в hello указан диапазон.

Hello следующий пример возвращает `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
Возвращает случайное целым числом в пределах hello указанного диапазона. Эта функция не создает криптографически безопасное случайное число.

Hello следующий пример может вернуть `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>floor
Возвращает наибольшее целое число hello меньше или равно toohello указанное число.

Hello следующий пример возвращает `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
Здравствуйте, возвращает наибольшее целое число, больше или равно toohello указанное число.

Hello следующий пример возвращает `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>Функции данных
### <a name="utcnow"></a>utcnow
Возвращает строку в формате ISO 8601 hello текущую дату и время на локальном компьютере hello.

Hello следующий пример может вернуть `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addseconds
Добавляет целому числу секунд toohello указан отметки времени.

Hello следующий пример возвращает `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addminutes
Добавляет целое количество минут toohello указан отметки времени.

Hello следующий пример возвращает `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addhours
Добавляет целое количество часов toohello указан отметки времени.

Hello следующий пример возвращает `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>Дальнейшие действия
* Введение tooAzure диспетчера ресурсов. в разделе [Обзор диспетчера ресурсов Azure](resource-group-overview.md).

