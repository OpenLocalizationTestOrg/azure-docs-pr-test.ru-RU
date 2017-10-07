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
# <a name="azure-resource-manager-template-functions"></a>Функции шаблонов диспетчера ресурсов Azure
В этом разделе описываются все функции hello, которые можно использовать в шаблоне диспетчера ресурсов Azure.

Функции нужно добавлять в шаблоны, заключая их в скобки `[` и `]` соответственно. Hello выражение вычисляется во время развертывания. Во время записи как строковый литерал hello результат вычисления выражения hello может быть другого типа JSON, например массиву, объекта или целое число со знаком. Как и в языке JavaScript, вызовы функций форматируются так: `functionName(arg1,arg2,arg3)`. Ссылки на свойства с помощью операторов [index] и точками hello.

Выражение шаблона не может превышать 24 576 знаков.

Функции шаблонов и их параметры зависят от регистра. Например, диспетчер ресурсов преобразует **variables('var1')** и **VARIABLES('VAR1')** как же hello. При вычислении, если функция hello явно не изменяет регистр (например toUpper или toLower), функции hello сохраняет регистр hello. Для некоторых типов ресурсов требования к регистру могут не зависеть от того, как происходит вычисление функций.

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

## <a name="array-and-object-functions"></a>Функции массива и объекта
Resource Manager предоставляет ряд функций для работы с массивами и объектами.

* [array](resource-group-template-functions-array.md#array).
* [coalesce](resource-group-template-functions-array.md#coalesce)
* [concat](resource-group-template-functions-array.md#concat)
* [contains](resource-group-template-functions-array.md#contains)
* [createArray](resource-group-template-functions-array.md#createarray)
* [empty](resource-group-template-functions-array.md#empty)
* [first](resource-group-template-functions-array.md#first)
* [intersection](resource-group-template-functions-array.md#intersection)
* [json](resource-group-template-functions-array.md#json)
* [last](resource-group-template-functions-array.md#last)
* [длина](resource-group-template-functions-array.md#length)
* [min](resource-group-template-functions-array.md#min)
* [max](resource-group-template-functions-array.md#max)
* [range](resource-group-template-functions-array.md#range)
* [skip](resource-group-template-functions-array.md#skip)
* [take](resource-group-template-functions-array.md#take)
* [union](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a>Функции сравнения
Resource Manager предоставляет ряд функций для выполнения сравнений в шаблонах.

* [equals](resource-group-template-functions-comparison.md#equals)
* [less](resource-group-template-functions-comparison.md#less)
* [lessOrEquals](resource-group-template-functions-comparison.md#lessorequals)
* [greater](resource-group-template-functions-comparison.md#greater)
* [greaterOrEquals](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a>Функции для параметров развертывания
Диспетчер ресурсов предоставляет hello следующие функции для получения значения из разделов шаблона hello и значения связанных toohello развертывания:

* [deployment](resource-group-template-functions-deployment.md#deployment)
* [parameters](resource-group-template-functions-deployment.md#parameters)
* [variables](resource-group-template-functions-deployment.md#variables)

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

## <a name="logical-functions"></a>Логические функции
Диспетчер ресурсов предоставляет следующие функции для работы с логических условий hello:

* [and](resource-group-template-functions-logical.md#and) (и);
* [bool](resource-group-template-functions-logical.md#bool);
* [if](resource-group-template-functions-logical.md#if) (если);
* [not](resource-group-template-functions-logical.md#not) (не);
* [or](resource-group-template-functions-logical.md#or) (или).

## <a name="numeric-functions"></a>Числовые функции
Диспетчер ресурсов предоставляет следующие функции для работы с целыми числами hello:

* [добавление](resource-group-template-functions-numeric.md#add)
* [copyIndex](resource-group-template-functions-numeric.md#copyindex)
* [div](resource-group-template-functions-numeric.md#div)
* [float](resource-group-template-functions-numeric.md#float)
* [int](resource-group-template-functions-numeric.md#int)
* [min](resource-group-template-functions-numeric.md#min)
* [max](resource-group-template-functions-numeric.md#max)
* [mod (модуль)](resource-group-template-functions-numeric.md#mod)
* [mul](resource-group-template-functions-numeric.md#mul)
* [sub](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a>Функции для работы с ресурсами
Диспетчер ресурсов предоставляет следующие функции для получения значений ресурсов hello:

* [listKeys и list{Value}](resource-group-template-functions-resource.md#listkeys)
* [providers](resource-group-template-functions-resource.md#providers)
* [reference](resource-group-template-functions-resource.md#reference)
* [resourceGroup](resource-group-template-functions-resource.md#resourcegroup)
* [resourceId](resource-group-template-functions-resource.md#resourceid)
* [subscription](resource-group-template-functions-resource.md#subscription)

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

## <a name="string-functions"></a>Строковые функции
Диспетчер ресурсов предоставляет следующие функции для работы со строками hello:

* [base64](resource-group-template-functions-string.md#base64)
* [base64ToJson](resource-group-template-functions-string.md#base64tojson)
* [base64ToString](resource-group-template-functions-string.md#base64tostring)
* [concat](resource-group-template-functions-string.md#concat)
* [contains](resource-group-template-functions-string.md#contains)
* [dataUri](resource-group-template-functions-string.md#datauri)
* [dataUriToString](resource-group-template-functions-string.md#datauritostring)
* [empty](resource-group-template-functions-string.md#empty)
* [endsWith](resource-group-template-functions-string.md#endswith)
* [first](resource-group-template-functions-string.md#first)
* [indexOf](resource-group-template-functions-string.md#indexof)
* [last](resource-group-template-functions-string.md#last)
* [lastIndexOf](resource-group-template-functions-string.md#lastindexof)
* [длина](resource-group-template-functions-string.md#length)
* [padLeft](resource-group-template-functions-string.md#padleft)
* [replace](resource-group-template-functions-string.md#replace)
* [skip](resource-group-template-functions-string.md#skip)
* [split](resource-group-template-functions-string.md#split)
* [startsWith](resource-group-template-functions-string.md#startswith)
* [string](resource-group-template-functions-string.md#string)
* [substring](resource-group-template-functions-string.md#substring)
* [take](resource-group-template-functions-string.md#take)
* [toLower](resource-group-template-functions-string.md#tolower)
* [toUpper](resource-group-template-functions-string.md#toupper)
* [trim](resource-group-template-functions-string.md#trim)
* [uniqueString](resource-group-template-functions-string.md#uniquestring)
* [uri](resource-group-template-functions-string.md#uri)
* [uriComponent](resource-group-template-functions-string.md#uricomponent)
* [uriComponentToString](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a>Дальнейшие действия
* Описание разделов hello в шаблоне диспетчера ресурсов Azure см. в разделе [шаблоны создания диспетчера ресурсов Azure](resource-group-authoring-templates.md)
* toomerge несколько шаблонов, см. раздел [с помощью шаблонов, связанных с диспетчером ресурсов Azure](resource-group-linked-templates.md)
* tooiterate указанное число раз при создании типа ресурса в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](resource-group-create-multiple.md)
* toosee toodeploy hello шаблон был создан, в статье [развернуть приложение с помощью шаблона диспетчера ресурсов Azure](resource-group-template-deploy.md)

