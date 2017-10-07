---
title: "aaaAzure диспетчер ресурсов шаблона функции - логических | Документы Microsoft"
description: "Описывает toouse функции hello в шаблона Azure Resource Manager toodetermine логические значения."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Логические функции для шаблонов Azure Resource Manager

Resource Manager предоставляет ряд функций для выполнения сравнений в шаблонах.

* [and](#and) (и);
* [bool](#bool);
* [if](#if) (если);
* [not](#not) (не);
* [or](#or) (или).

## <a name="and"></a>и
`and(arg1, arg2)`

Проверяет, соответствуют ли истине два значения параметров.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |Логическое |Здравствуйте ли первый toocheck значение равно true. |
| arg2 |Да |Логическое |Hello ли toocheck второе значение — true. |

### <a name="return-value"></a>Возвращаемое значение

Возвращает результат **True** (Истина), если оба значения соответствуют истине. В противном случае — **False** (Ложь).

### <a name="examples"></a>Примеры

Следующий пример показывает как Hello toouse логические функции.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

представлен результат Hello предшествующий пример hello.

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| andExampleOutput | Bool | Ложь |
| orExampleOutput | Bool | Да |
| notExampleOutput | Bool | Ложь |


## <a name="bool"></a>bool
`bool(arg1)`

Преобразует hello tooa параметр типа boolean.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |строка или целое число |Здравствуйте, tooa tooconvert значение типа boolean. |

### <a name="return-value"></a>Возвращаемое значение
Логическое hello преобразованное значение.

### <a name="examples"></a>Примеры

Следующий пример показывает как Hello bool toouse строкой или целое число со знаком.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

Hello выходных данных из hello предыдущий пример со значениями по умолчанию hello является:

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| trueString | Bool | Да |
| falseString | Bool | Ложь |
| trueInt | Bool | Да |
| falseInt | Bool | Ложь |

## <a name="if"></a>if
`if(condition, trueValue, falseValue)`

Возвращает значение в зависимости от того, выполняется ли условие.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| condition |Да |Логическое |значение toocheck Hello, является ли значение true. |
| trueValue |Да | строка, целое число, объект или массив |tooreturn значение Hello, hello условие истинно. |
| falseValue |Да | строка, целое число, объект или массив |tooreturn значение Hello, hello условие имеет значение false. |

### <a name="return-value"></a>Возвращаемое значение

Возвращает второй параметр, если первый параметр имеет значение **True** (Истина). В противном случае возвращает третий параметр.

### <a name="remarks"></a>Примечания

Этот набор tooconditionally функции можно использовать свойства ресурса. Hello в примере не является полной шаблоном, но он демонстрирует hello соответствующих частей условно настройки группы доступности hello.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>Примеры

Следующий пример показывает как Hello toouse hello `if` функции.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

представлен результат Hello предшествующий пример hello.

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| yesOutput | Строка | Да |
| noOutput | Строка | Нет |


## <a name="not"></a>not
`not(arg1)`

Преобразует логическое значение tooits противоположные значения.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |Логическое |tooconvert значение Hello. |


### <a name="return-value"></a>Возвращаемое значение

Возвращает значение **True** (Истина), если параметр имеет значение **False** (Ложь). Возвращает значение **False** (Ложь), если параметр имеет значение **True** (Истина).

### <a name="examples"></a>Примеры

Следующий пример показывает как Hello toouse логические функции.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

представлен результат Hello предшествующий пример hello.

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| andExampleOutput | Bool | Ложь |
| orExampleOutput | Bool | Да |
| notExampleOutput | Bool | Ложь |

Hello следующий пример использует **не** с [равняется](resource-group-template-functions-comparison.md#equals).

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

представлен результат Hello предшествующий пример hello.

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| checkNotEquals | Bool | Да |


## <a name="or"></a>или
`or(arg1, arg2)`

Проверяет, соответствует ли истине одно из значений параметров.

### <a name="parameters"></a>Параметры

| Параметр | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| arg1 |Да |Логическое |Здравствуйте ли первый toocheck значение равно true. |
| arg2 |Да |Логическое |Hello ли toocheck второе значение — true. |

### <a name="return-value"></a>Возвращаемое значение

Возвращает результат **True** (Истина), если одно из значений соответствует истине. В противном случае — **False** (Ложь).

### <a name="examples"></a>Примеры

Следующий пример показывает как Hello toouse логические функции.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

представлен результат Hello предшествующий пример hello.

| Имя | Тип | Значение |
| ---- | ---- | ----- |
| andExampleOutput | Bool | Ложь |
| orExampleOutput | Bool | Да |
| notExampleOutput | Bool | Ложь |


## <a name="next-steps"></a>Дальнейшие действия
* Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны разработки Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md).
* tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md).
* toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).

