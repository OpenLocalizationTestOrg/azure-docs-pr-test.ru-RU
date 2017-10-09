---
title: "функции - массивы и объекты шаблона диспетчера ресурсов aaaAzure | Документы Microsoft"
description: "Описывает toouse функции hello в шаблоне диспетчера ресурсов Azure для работы с массивы и объекты."
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Функции массивов и объектов для шаблонов Azure Resource Manager 

Resource Manager предоставляет ряд функций для работы с массивами и объектами.

* [array](#array).
* [coalesce](#coalesce)
* [concat](#concat)
* [contains](#contains)
* [createArray](#createarray)
* [empty](#empty)
* [first](#first)
* [intersection](#intersection)
* [json](#json)
* [last](#last)
* [длина](#length)
* [min](#min)
* [max](#max)
* [range](#range)
* [skip](#skip)
* [take](#take)
* [union](#union)

tooget массив строковых значений, разделенных по значению, в разделе [разбиение](resource-group-template-functions-string.md#split).

<a id="array" />

## <a name="array"></a>array
`array(convertToArray)`

Преобразует массив tooan значение hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| convertToArray |Да |целое число, строка, массив или объект |Массив tooan tooconvert значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

Массив.

### <a name="example"></a>Пример

Hello следующем примере показано, как toouse hello функции массива с различными типами.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| intOutput | Массив, | [1] |
| stringOutput | Массив, | ["a"] |
| objectOutput | Массив, | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>coalesce
`coalesce(arg1, arg2, arg3, ...)`

Возвращает первое непустое значение на основе параметров hello. Пустые строки, пустые массивы и пустые объекты не имеют значение null.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |целое число, строка, массив или объект |Hello первый tootest значение со значением NULL. |
| дополнительные аргументы |Нет |целое число, строка, массив или объект |Дополнительные значения tootest со значением NULL. |

### <a name="return-value"></a>Возвращаемое значение

значение Hello hello первый ненулевой параметров, может быть строка, int, массив или объект. Null, если все параметры имеют значение null. 

### <a name="example"></a>Пример

Hello пример hello выходные данные различных вариантах использования coalesce.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| stringOutput | Строка | по умолчанию |
| intOutput | int | 1 |
| objectOutput | Объект | {"first": "default"} |
| arrayOutput | Массив, | [1] |
| emptyOutput | Bool | Да |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

Объединяет несколько массивов и возвращает массив объединенные hello, или объединяет несколько строковых значений и возвращает строку hello объединяются. 

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или строка |Здравствуйте, первый массив или строка для сцепления. |
| дополнительные аргументы |Нет |массив или строка |Дополнительные массивы или строки в последовательном порядке для объединения. |

Эта функция может принимать любое количество аргументов и могут принимать строки или массивы параметров hello.

### <a name="return-value"></a>Возвращаемое значение
Строка или массив объединенных значений.

### <a name="example"></a>Пример

Hello в следующем примере показано, как toocombine двух массивов.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| return | Массив, | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

Привет, в следующем примере показано, как toocombine двух строковые значения и возвращает сцепленную строку.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| concatOutput | Строка | prefix-5yj4yjf5mbg72 |

<a id="contains" />

## <a name="contains"></a>contains
`contains(container, itemToFind)`

Проверяет, содержит ли массив значение, содержит ли объект ключ или содержит ли строка подстроку.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| container |Да |массив, объект или строка |Hello значение, содержащее значение toofind hello. |
| itemToFind |Да |строка или целое число |toofind значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

**Значение true,** Если hello элемент найден; в противном случае — **False**.

### <a name="example"></a>Пример

Hello следующий пример показывает, как toouse содержит с разными типами:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| stringTrue | Bool | Да |
| stringFalse | Bool | Ложь |
| objectTrue | Bool | Да |
| objectFalse | Bool | Ложь |
| arrayTrue | Bool | Да |
| arrayFalse | Bool | Ложь |

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Создает массив из параметров hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |Строка, целое число, массив или объект |Hello первое значение в массиве hello. |
| дополнительные аргументы |Нет |Строка, целое число, массив или объект |Дополнительные значения в массиве hello. |

### <a name="return-value"></a>Возвращаемое значение

Массив.

### <a name="example"></a>Пример

Следующий пример показывает как Hello createArray toouse с различными типами:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
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
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| stringArray | Массив, | ["a", "b", "c"] |
| intArray | Массив, | [1, 2, 3] |
| objectArray | Массив, | [{"one": "a", "two": "b", "three": "c"}] |
| arrayArray | Массив, | [["one", "two", "three"]] |

<a id="empty" />

## <a name="empty"></a>empty

`empty(itemToTest)`

Определяет, являются ли пустыми массив, объект или строка.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| itemToTest |Да |массив, объект или строка |Здравствуйте toocheck значение, если она пуста. |

### <a name="return-value"></a>Возвращаемое значение

Возвращает **True** Если hello значение является пустой; в противном случае — **False**.

### <a name="example"></a>Пример

Следующий пример Hello проверяет array, object и string пустым.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| arrayEmpty | Bool | Да |
| objectEmpty | Bool | Да |
| stringEmpty | Bool | Да |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

Возвращает hello первый элемент массива hello или первым символом строки hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или строка |символ или первый элемент tooretrieve значение hello Hello. |

### <a name="return-value"></a>Возвращаемое значение

Hello тип (строка, int, массива или объекта) hello первый элемент массива, или hello первого символа строки.

### <a name="example"></a>Пример

Hello следующем примере показано, как toouse hello первой функции с массивом и строкой.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| arrayOutput | Строка | one |
| stringOutput | Строка | O |

<a id="intersection" />

## <a name="intersection"></a>пересечению
`intersection(arg1, arg2, arg3, ...)`

Возвращает массив или объект с hello Общие элементы на основе параметров hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или объект |Hello первый toouse значение для поиска Общие элементы. |
| arg2 |Да |массив или объект |Hello второй toouse значение для поиска Общие элементы. |
| дополнительные аргументы |Нет |массив или объект |Toouse дополнительных значений для поиска Общие элементы. |

### <a name="return-value"></a>Возвращаемое значение

Массив или объект с hello Общие элементы.

### <a name="example"></a>Пример

Следующий пример показывает, как массивы toouse пересечение с Hello и объектов:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| objectOutput | Объект | {"one": "a", "three": "c"} |
| arrayOutput | Массив, | ["two", "three"] |


## <a name="json"></a>json
`json(arg1)`

Возвращает объект JSON.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |string |tooJSON tooconvert значение Hello. |


### <a name="return-value"></a>Возвращаемое значение

Hello объекта JSON из hello указанная строка или пустой объект при **null** указано.

### <a name="example"></a>Пример

Следующий пример показывает, как массивы toouse пересечение с Hello и объектов:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| jsonOutput | Объект | {"a": "b"} |
| nullOutput | Логический | Да |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

Возвращает hello последний элемент массива hello или последнего символа строки hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или строка |последний элемент hello tooretrieve Hello значение или символ. |

### <a name="return-value"></a>Возвращаемое значение

Hello тип (строка, int, массива или объекта) hello последнего элемента в массиве, или hello последнего символа строки.

### <a name="example"></a>Пример

Hello следующем примере показано, как toouse hello последнюю функцию с массивом и строкой.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| arrayOutput | Строка | three |
| stringOutput | Строка | e |

<a id="length" />

## <a name="length"></a>длина
`length(arg1)`

Возвращает hello количество элементов в массиве, или символы в строке.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или строка |Здравствуйте toouse массива для получения hello количество элементов или hello toouse строки для получения hello число символов. |

### <a name="return-value"></a>Возвращаемое значение

Целое число. 

### <a name="example"></a>Пример

Следующий пример показывает как Hello toouse длины с массивом и строкой:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13. |

При создании ресурсов, можно использовать эту функцию с массивом toospecify hello количеством итераций. В следующем примере hello, hello параметр **siteNames** относится tooan массив toouse имен при создании hello веб-сайтов.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

Дополнительные сведения об использовании этой функции с массивом см. в статье [Создание нескольких экземпляров ресурсов в Azure Resource Manager](resource-group-create-multiple.md).

<a id="min" />

## <a name="min"></a>Min
`min(arg1)`

Возвращает hello минимальное значение из массива целых чисел или разделителями запятыми списка целых чисел.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив целых чисел или разделенный запятыми список целых чисел |Hello коллекции tooget hello минимальное значение. |

### <a name="return-value"></a>Возвращаемое значение

Целое число, представляющее минимальное значение hello.

### <a name="example"></a>Пример

Следующий пример показывает как Hello min toouse с массивом и список целых чисел:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>max
`max(arg1)`

Возвращает hello максимальное значение из массива целых чисел или разделителями запятыми списка целых чисел.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив целых чисел или разделенный запятыми список целых чисел |Hello коллекции tooget hello максимальное значение. |

### <a name="return-value"></a>Возвращаемое значение

Целое число, представляющее максимальное значение hello.

### <a name="example"></a>Пример

Следующий пример показывает как Hello toouse max с массивом и список целых чисел:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="range" />

## <a name="range"></a>range
`range(startingInteger, numberOfElements)`

Создает массив целых чисел, используя начальное целое число и количество элементов.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| startingInteger |Да |int |Hello первое целое число в массиве hello. |
| numberofElements |Да |int |Количество целочисленных значений в массиве hello Hello. |

### <a name="return-value"></a>Возвращаемое значение

Массив целых чисел.

### <a name="example"></a>Пример

Hello в следующем примере показано, как toouse hello диапазона функции:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| rangeOutput | Массив, | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Возвращает массив со всеми элементами hello после hello указанное число в массиве hello, или возвращает строку, в которой все символы hello после hello указанное число в строку hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| originalValue |Да |массив или строка |Hello массиву или строке toouse для пропуска. |
| numberToSkip |Да |int |количество элементов или символы tooskip Hello. Если это значение меньше или равно 0, все hello элементов или символов в значении hello возвращаются. Если превышает длину hello hello массиву или строке, возвращается пустой массив или строку. |

### <a name="return-value"></a>Возвращаемое значение

Массив или строка.

### <a name="example"></a>Пример

Следующий пример hello пропускает Hello заданное число элементов в массиве hello и hello указанное число символов в строке.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| arrayOutput | Массив, | ["three"] |
| stringOutput | Строка | two three |

<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Здравствуйте, возвращает массив с hello указанное число элементов от начала массива hello, или строка с hello указанное число символов от начала hello строку hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| originalValue |Да |массив или строка |Здравствуйте, массиву или строке tootake hello элементы. |
| numberToTake |Да |int |количество элементов или символы tootake Hello. Если это значение меньше или равно 0, то возвращается пустой массив или строка. Если это больше, чем длина заданного массива или строка hello hello, возвращаются все элементы hello hello массиву или строке. |

### <a name="return-value"></a>Возвращаемое значение

Массив или строка.

### <a name="example"></a>Пример

Следующий пример принимает hello Hello заданное число элементов из массива hello и символов из строки.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| arrayOutput | Массив, | ["one", "two"] |
| stringOutput | Строка | on |

<a id="union" />

## <a name="union"></a>union
`union(arg1, arg2, arg3, ...)`

Возвращает массив или объект со всеми элементами на основе параметров hello. Повторяющиеся значения или ключи включаются только один раз.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или объект |Hello первый toouse значение для объединения элементов. |
| arg2 |Да |массив или объект |Hello второй toouse значение для объединения элементов. |
| дополнительные аргументы |Нет |массив или объект |Дополнительные значения toouse для объединения элементов. |

### <a name="return-value"></a>Возвращаемое значение

Массив или объект.

### <a name="example"></a>Пример

Следующий пример показывает, как массивы toouse объединения с Hello и объектов:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| objectOutput | Объект | {"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"} |
| arrayOutput | Массив, | ["one", "two", "three", "four"] |

## <a name="next-steps"></a>Дальнейшие действия
* Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).
* tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).
* toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).

