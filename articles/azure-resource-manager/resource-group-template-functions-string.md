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
# <a name="string-functions-for-azure-resource-manager-templates"></a>Строковые функции для шаблонов Azure Resource Manager

Диспетчер ресурсов предоставляет следующие функции для работы со строками hello:

* [base64](#base64)
* [base64ToJson](#base64tojson)
* [base64ToString](#base64tostring)
* [concat](#concat)
* [contains](#contains)
* [dataUri](#datauri)
* [dataUriToString](#datauritostring)
* [empty](#empty)
* [endsWith](#endswith)
* [first](#first)
* [indexOf](#indexof)
* [last](#last)
* [lastIndexOf](#lastindexof)
* [длина](#length)
* [padLeft](#padleft)
* [replace](#replace)
* [skip](#skip)
* [split](#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [string](#string)
* [substring](#substring)
* [take](#take)
* [toLower](#tolower)
* [toUpper](#toupper)
* [trim](#trim)
* [uniqueString](#uniquestring)
* [uri](#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a>base64
`base64(inputString)`

Возвращает hello представление base64 hello входной строки.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| входная_строка |Да |string |Hello tooreturn значение как представление base64. |

### <a name="return-value"></a>Возвращаемое значение

Строка, содержащая представление base64 hello.

### <a name="examples"></a>Примеры

Hello в следующем примере показано, как toouse hello функция base64.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| base64Output | Строка | b25lLCB0d28sIHRocmVl |
| toStringOutput | Строка | one, two, three |
| toJsonOutput | Объект | {"one": "a", "two": "b"} |

<a id="base64tojson" />

## <a name="base64tojson"></a>base64ToJson
`base64tojson`

Преобразует объект base64 tooa представление JSON.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| base64Value |Да |string |Hello base64 представление tooconvert tooa объект JSON. |

### <a name="return-value"></a>Возвращаемое значение

Объект JSON.

### <a name="examples"></a>Примеры

Hello следующий пример использует hello base64ToJson функция tooconvert значение base64.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| base64Output | Строка | b25lLCB0d28sIHRocmVl |
| toStringOutput | Строка | one, two, three |
| toJsonOutput | Объект | {"one": "a", "two": "b"} |

<a id="base64tostring" />

## <a name="base64tostring"></a>base64ToString
`base64ToString(base64Value)`

Преобразует строку tooa представление base64.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| base64Value |Да |string |Hello представление tooconvert tooa в кодировке Base64. |

### <a name="return-value"></a>Возвращаемое значение

Строка hello преобразованное значение base64.

### <a name="examples"></a>Примеры

Hello следующий пример использует hello base64ToString функция tooconvert значение base64.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| base64Output | Строка | b25lLCB0d28sIHRocmVl |
| toStringOutput | Строка | one, two, three |
| toJsonOutput | Объект | {"one": "a", "two": "b"} |



<a id="concat" />

## <a name="concat"></a>concat
`concat (arg1, arg2, arg3, ...)`

Объединяет несколько строковых значений и возвращает строку hello объединения или объединяет несколько массивов и возвращает массив hello объединяются.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |строка или массив |Hello первое значение для объединения. |
| дополнительные аргументы |Нет |string |Дополнительные значения в последовательном порядке для сцепки. |

### <a name="return-value"></a>Возвращаемое значение
Строка или массив объединенных значений.

### <a name="examples"></a>Примеры

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

<a id="contains" />

## <a name="contains"></a>contains
`contains (container, itemToFind)`

Проверяет, содержит ли массив значение, содержит ли объект ключ или содержит ли строка подстроку.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| container |Да |массив, объект или строка |Hello значение, содержащее значение toofind hello. |
| itemToFind |Да |строка или целое число |toofind значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

**Значение true,** Если hello элемент найден; в противном случае — **False**.

### <a name="examples"></a>Примеры

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

<a id="datauri" />

## <a name="datauri"></a>dataUri
`dataUri(stringToConvert)`

Преобразует значение tooa URI.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| stringToConvert |Да |string |Hello tooconvert tooa значение URI. |

### <a name="return-value"></a>Возвращаемое значение

Строка в формате URI данных.

### <a name="examples"></a>Примеры

Здравствуйте, следующий пример преобразует значение tooa URI и преобразует данные строки tooa URI:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| dataUriOutput | Строка | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | Строка | Привет, мир! |

<a id="datauritostring" />

## <a name="datauritostring"></a>dataUriToString
`dataUriToString(dataUriToConvert)`

Преобразует URI данных в формате строки tooa значения.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| dataUriToConvert |Да |string |данные Hello tooconvert значение URI. |

### <a name="return-value"></a>Возвращаемое значение

Строка, содержащая hello преобразованное значение.

### <a name="examples"></a>Примеры

Здравствуйте, следующий пример преобразует значение tooa URI и преобразует данные строки tooa URI:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| dataUriOutput | Строка | data:text/plain;charset=utf8;base64,SGVsbG8= |
| toStringOutput | Строка | Привет, мир! |

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

### <a name="examples"></a>Примеры

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

<a id="endswith" />

## <a name="endswith"></a>endsWith
`endsWith(stringToSearch, stringToFind)`

Определяет, заканчивается ли строка определенным значением. Hello выполняется без учета регистра.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| stringToSearch |Да |string |Hello значение, содержащее элемент toofind hello. |
| stringToFind |Да |string |toofind значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

**Значение true,** Если hello последний символ или символы строки hello соответствует значению hello; в противном случае **False**.

### <a name="examples"></a>Примеры

Hello в следующем примере показано, как toouse hello функции startsWith и endsWith.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| startsTrue | Bool | Да |
| startsCapTrue | Bool | Да |
| startsFalse | Bool | Ложь |
| endsTrue | Bool | Да |
| endsCapTrue | Bool | Да |
| endsFalse | Bool | Ложь |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

Возвращает hello первого символа строки hello, или первый элемент массива hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или строка |символ или первый элемент tooretrieve значение hello Hello. |

### <a name="return-value"></a>Возвращаемое значение

Строка hello первого символа или тип hello (строка, int, массива или объекта) hello первый элемент массива.

### <a name="examples"></a>Примеры

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

<a id="indexof" />

## <a name="indexof"></a>indexOf
`indexOf(stringToSearch, stringToFind)`

Возвращает hello первую позицию значения в строке. Hello выполняется без учета регистра.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| stringToSearch |Да |string |Hello значение, содержащее элемент toofind hello. |
| stringToFind |Да |string |toofind значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

Целое число, представляющее позицию элемента toofind hello hello. Hello значение начинается с нуля. Если hello элемент не найден, возвращается значение -1.

### <a name="examples"></a>Примеры

Hello в следующем примере показано, как toouse hello функции indexOf и lastIndexOf:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

Возвращает последнего знака строки hello или hello последним элементом массива hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или строка |последний элемент hello tooretrieve Hello значение или символ. |

### <a name="return-value"></a>Возвращаемое значение

Строка hello последний символ или тип hello (строка, int, массива или объекта) hello последнего элемента в массиве.

### <a name="examples"></a>Примеры

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

<a id="lastindexof" />

## <a name="lastindexof"></a>lastIndexOf
`lastIndexOf(stringToSearch, stringToFind)`

Возвращает hello последней позиции значение в строку. Hello выполняется без учета регистра.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| stringToSearch |Да |string |Hello значение, содержащее элемент toofind hello. |
| stringToFind |Да |string |toofind значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

Целое число, представляющее hello последней позиции элемента toofind hello. Hello значение начинается с нуля. Если hello элемент не найден, возвращается значение -1.

### <a name="examples"></a>Примеры

Hello в следующем примере показано, как toouse hello функции indexOf и lastIndexOf:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| firstT | int | 0 |
| lastT | int | 3 |
| firstString | int | 2 |
| lastString | int | 0 |
| notFound | int | -1 |

<a id="length" />

## <a name="length"></a>длина
`length(string)`

Возвращает hello число знаков в строке или элементов в массиве.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |массив или строка |Здравствуйте toouse массива для получения hello количество элементов или hello toouse строки для получения hello число символов. |

### <a name="return-value"></a>Возвращаемое значение

Целое число. 

### <a name="examples"></a>Примеры

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

<a id="padleft" />

## <a name="padleft"></a>padLeft
`padLeft(valueToPad, totalLength, paddingCharacter)`

Возвращает строку, по правому краю путем добавления слева символов toohello до достижения hello общее указанной длины.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| значение_для_заполнения  |Да |строка или целое число |Здравствуйте, значение tooright-align. |
| общая_длина |Да |int |Общее число символов в hello Hello возвращена строка. |
| символ_заполнения |Нет |один знак |Здравствуйте, toouse символ для заполнения влево до достижения hello общей длины. значение по умолчанию Hello — пробел. |

Если исходная строка hello длиннее, чем число hello toopad символов, символов не добавляются.

### <a name="return-value"></a>Возвращаемое значение

Строка с по крайней мере hello число заданных символов.

### <a name="examples"></a>Примеры

Hello в следующем примере показано, как toopad hello значение параметра, предоставленные пользователем, добавив hello символ нуля до достижения hello общее число символов. 

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| stringOutput | Строка | 0000000123 |

<a id="replace" />

## <a name="replace"></a>replace
`replace(originalString, oldString, newString)`

Возвращает новую строку, в которой все экземпляры одной строки заменены другой строкой.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| исходная_строка |Да |string |значение Hello, которое имеет все вхождения одной строки заменяется на другую строку. |
| oldString |Да |string |toobe строка Hello удаляется из исходной строки hello. |
| newString |Да |string |tooadd строка Hello вместо hello удалена строка. |

### <a name="return-value"></a>Возвращаемое значение

Строка с hello заменить символы.

### <a name="examples"></a>Примеры

Hello в следующем примере показано, как tooremove все дефисы из предоставленных пользователем строку hello и как часть tooreplace hello строка с другой строкой.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| firstOutput | Строка | 1231231234 |
| secodeOutput | Строка | 123-123-xxxx |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Возвращает строку, в которой все символы hello после hello указанное число символов или массив со всеми элементами hello после hello заданное число элементов.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| originalValue |Да |массив или строка |Hello массиву или строке toouse для пропуска. |
| numberToSkip |Да |int |количество элементов или символы tooskip Hello. Если это значение меньше или равно 0, все hello элементов или символов в значении hello возвращаются. Если превышает длину hello hello массиву или строке, возвращается пустой массив или строку. |

### <a name="return-value"></a>Возвращаемое значение

Массив или строка.

### <a name="examples"></a>Примеры

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

<a id="split" />

## <a name="split"></a>split
`split(inputString, delimiter)`

Возвращает массив строк, содержащий подстроки hello hello входной строки, разделенные hello указан разделители.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| входная_строка |Да |string |toosplit строка Hello. |
| delimiter |Да |строка или массив строк |Hello toouse разделитель для разбиения строки hello. |

### <a name="return-value"></a>Возвращаемое значение

Массив строк.

### <a name="examples"></a>Примеры

Hello следующий пример Разделяет входную строку hello запятую и с запятой или точкой с запятой.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| firstOutput | Массив, | ["one", "two", "three"] |
| secondOutput | Массив, | ["one", "two", "three"] |

<a id="startswith" />

## <a name="startswith"></a>startsWith
`startsWith(stringToSearch, stringToFind)`

Определяет, начинается ли строка с определенного значения. Hello выполняется без учета регистра.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| stringToSearch |Да |string |Hello значение, содержащее элемент toofind hello. |
| stringToFind |Да |string |toofind значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

**Значение true,** Если hello первый символ или символы строки hello соответствует значению hello; в противном случае **False**.

### <a name="examples"></a>Примеры

Hello в следующем примере показано, как toouse hello функции startsWith и endsWith.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| startsTrue | Bool | Да |
| startsCapTrue | Bool | Да |
| startsFalse | Bool | Ложь |
| endsTrue | Bool | Да |
| endsCapTrue | Bool | Да |
| endsFalse | Bool | Ложь |

<a id="string" />

## <a name="string"></a>string
`string(valueToConvert)`

Hello Преобразует указанную строку tooa значение.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| valueToConvert |Да | Любой |toostring tooconvert значение Hello. Можно преобразовать любой тип значения, включая объекты и массивы. |

### <a name="return-value"></a>Возвращаемое значение

Строка hello преобразованное значение.

### <a name="examples"></a>Примеры

Hello в следующем примере показано, как tooconvert различных типов значений toostrings:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| objectOutput | Строка | {"valueA":10,"valueB":"Example Text"} |
| arrayOutput | Строка | ["a","b","c"] |
| intOutput | Строка | 5 |

<a id="substring" />

## <a name="substring"></a>substring
`substring(stringToParse, startIndex, length)`

Возвращает подстроку, начинается с указанного hello позиции знака и содержит hello указанное число символов.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| stringToParse |Да |string |Исходная строка Hello, из какой hello извлекается подстрока. |
| startIndex |Нет |int |Hello отсчитываемый от нуля позиция первого знака поиск подстроки hello. |
| длина |Нет |int |число символов в подстроке hello Hello. Должен указывать расположение tooa в строку hello. |

### <a name="return-value"></a>Возвращаемое значение

подстрока Hello.

### <a name="remarks"></a>Примечания

функции Hello завершается сбоем, когда hello подстрока выходит за пределы hello конца строки hello. Следующий пример Hello завершается hello ошибка «hello параметры индекса и длины должны ссылаться tooa расположение в строку hello. Здравствуйте, параметр индекса: "0" hello, длина параметра: "11" hello, длина параметра строку hello: "10".».

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a>Примеры

Следующий пример Hello извлекает подстроку из параметра.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| substringOutput | Строка | two |


<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Возвращает строку с hello указанное число символов от начала hello hello строку или массив с hello заданное число элементов от начала массива hello hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| originalValue |Да |массив или строка |Здравствуйте, массиву или строке tootake hello элементы. |
| numberToTake |Да |int |количество элементов или символы tootake Hello. Если это значение меньше или равно 0, то возвращается пустой массив или строка. Если это больше, чем длина заданного массива или строка hello hello, возвращаются все элементы hello hello массиву или строке. |

### <a name="return-value"></a>Возвращаемое значение

Массив или строка.

### <a name="examples"></a>Примеры

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

<a id="tolower" />

## <a name="tolower"></a>toLower
`toLower(stringToChange)`

Преобразует hello указан вариант toolower строки.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| изменяемая_строка |Да |string |case toolower tooconvert значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

преобразовать строку Hello toolower регистр.

### <a name="examples"></a>Примеры

Следующий пример Hello преобразует запрос toolower значение параметра и tooupper случай.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| toLowerOutput | Строка | one two three |
| toUpperOutput | Строка | ONE TWO THREE |

<a id="toupper" />

## <a name="toupper"></a>toUpper
`toUpper(stringToChange)`

Преобразует hello указан вариант tooupper строки.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| изменяемая_строка |Да |string |case tooupper tooconvert значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

преобразовать строку Hello tooupper регистр.

### <a name="examples"></a>Примеры

Следующий пример Hello преобразует запрос toolower значение параметра и tooupper случай.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| toLowerOutput | Строка | one two three |
| toUpperOutput | Строка | ONE TWO THREE |

<a id="trim" />

## <a name="trim"></a>trim
`trim (stringToTrim)`

Удаляет все начальные и конечные пробелы из hello указанную строку.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| stringToTrim |Да |string |tootrim значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

Строка Hello без начальные и конечные пробелы.

### <a name="examples"></a>Примеры

Hello следующий пример удаляет символы-разделители hello из параметра hello.

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| return | Строка | one two three |

<a id="uniquestring" />

## <a name="uniquestring"></a>uniqueString
`uniqueString (baseString, ...)`

Создает на основе hello значений, переданных как параметры детерминированным хэш-строку. 

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| baseString |Да |string |Hello в использовано значение toocreate функции хэширования Привет уникальная строка. |
| Дополнительные параметры (если необходимы) |Нет |string |В качестве необходимых toocreate hello значение, указывающее уровень hello уникальности можно добавить любое количество строк. |

### <a name="remarks"></a>Примечания

Эта функция полезна в тех случаях, когда требуется toocreate уникальное имя для ресурса. Можно задать значения параметров, ограничить область hello уникальности hello результат. Можно указать, является ли имя hello уникальный вниз toosubscription, группы ресурсов или развертывания. 

Hello возвращаемое значение не является произвольной строки, но вместо hello результат хэш-функции. Hello вернул значение 13 символов. Оно не является глобально уникальным. Вы можете значение hello toocombine с префиксом из вашего именования toocreate соглашение понятное имя. Hello примере показан формат hello hello вернул значение. Фактическое значение Hello зависит от hello с указанными параметрами.

    tcvhiyu5h2o5o

Привет, следующие примеры показывают, как toocreate uniqueString toouse уникальный значение для часто используемых уровнях.

Уникальный toosubscription области

```json
"[uniqueString(subscription().subscriptionId)]"
```

Уникальный tooresource с областью группы

```json
"[uniqueString(resourceGroup().id)]"
```

Уникальный toodeployment с областью для группы ресурсов

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

Hello в следующем примере показано, как toocreate уникальное имя для учетной записи хранения на основе группы ресурсов. Внутри группы ресурсов hello, hello имя не является уникальным, если создан hello таким же образом.

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a>Возвращаемое значение

Строка, содержащая 13 символов.

### <a name="examples"></a>Примеры

Следующий пример Hello возвращает результаты из uniquestring:

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

## <a name="uri"></a>uri
`uri (baseUri, relativeUri)`

Создает абсолютный URI, объединяя hello baseUri и relativeUri строку hello.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| baseUri |Да |string |Строка Hello базовый uri. |
| relativeUri |Да |string |Hello относительный uri строка tooadd toohello базовый uri строка. |

Здравствуйте, значение для hello **baseUri** параметр, можно добавить определенный файл, но только базовый путь hello используется при построении hello URI. Например, если передать `http://contoso.com/resources/azuredeploy.json` в результате параметр baseUri hello в базовый URI `http://contoso.com/resources/`.

### <a name="return-value"></a>Возвращаемое значение

Строка, представляющая hello абсолютный универсальный код Ресурса для значений базового и относительного hello.

### <a name="examples"></a>Примеры

Привет, следующий пример показывает как tooconstruct вложенного шаблона tooa ссылку на основе hello значение hello родительского шаблона.

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

Следующий пример показывает как Hello toouse uri, uriComponent и uriComponentToString:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| uriOutput | Строка | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | Строка | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | Строка | http://contoso.com/resources/nested/azuredeploy.json |

<a id="uricomponent" />

## <a name="uricomponent"></a>uriComponent
`uricomponent(stringToEncode)`

Кодирует URI.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| stringToEncode |Да |string |tooencode значение Hello. |

### <a name="return-value"></a>Возвращаемое значение

Значение в кодировке строку hello URI.

### <a name="examples"></a>Примеры

Следующий пример показывает как Hello toouse uri, uriComponent и uriComponentToString:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| uriOutput | Строка | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | Строка | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | Строка | http://contoso.com/resources/nested/azuredeploy.json |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a>uriComponentToString
`uriComponentToString(uriEncodedString)`

Возвращает строку со значением, закодированным в формате URI.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| uriEncodedString |Да |string |значение tooconvert tooa строка в кодировке Hello URI. |

### <a name="return-value"></a>Возвращаемое значение

Декодированная строка со значением, закодированным в формате URI.

### <a name="examples"></a>Примеры

Следующий пример показывает как Hello toouse uri, uriComponent и uriComponentToString:

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

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| uriOutput | Строка | http://contoso.com/resources/nested/azuredeploy.json |
| componentOutput | Строка | http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json |
| toStringOutput | Строка | http://contoso.com/resources/nested/azuredeploy.json |


## <a name="next-steps"></a>Дальнейшие действия
* Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).
* tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).
* toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).

