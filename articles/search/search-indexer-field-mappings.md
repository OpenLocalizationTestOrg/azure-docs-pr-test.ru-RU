---
title: "сопоставление aaaField в поиске Azure индексаторы"
description: "Настройка tooaccount сопоставления поля индексатор поиска Azure для различия в поле имена и данные представления"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Сопоставление полей в индексаторах Поиска Azure
При использовании службы поиска Azure индексаторы, иногда можно найти самостоятельно в ситуациях, где входные данные довольно не соответствует схеме hello целевого индекса. В таких случаях можно использовать **поля сопоставления** tootransform данные hello ожидаемая форма.

Примеры ситуаций, в которых могут пригодиться сопоставления полей:

* Источник данных содержит поле `_id`, но поиск Azure не допускает, чтобы имена полей начинались с символа подчеркивания. Сопоставление полей позволяет слишком «переименовать» поле.
* Вы хотите toopopulate нескольких полей в hello индексирования с помощью hello и те же данные источника данных, например, так как tooapply различных анализаторы toothose полей. Сопоставления полей позволяют разветвить поле источника данных.
* Требуется tooBase64 закодировать или декодировать данные. Сопоставления полей поддерживают несколько **функций сопоставления**, включая шифрование и расшифровку в кодировке Base64.   

## <a name="setting-up-field-mappings"></a>Настройка сопоставлений полей
Можно добавить сопоставления полей, создавая новый индексатор, используя hello [Создание индексатора](https://msdn.microsoft.com/library/azure/dn946899.aspx) API. Вы можете управлять сопоставления полей для индексирования с помощью hello индексатора [обновление индексатора](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.

Сопоставление полей состоит из трех частей:

1. Параметр `sourceFieldName`— представляет поле в источнике данных. Это — обязательное свойство.
2. Необязательный параметр `targetFieldName`— представляет поле в индексе поиска. Если этот параметр опущен, hello же имя, что и источник данных hello используется.
3. Необязательный параметр `mappingFunction`— позволяет преобразовывать данные, используя одну из нескольких предопределенных функций. Полный список функций Hello [ниже](#mappingFunctions).

Сопоставления полей добавляются toohello `fieldMappings` массива на определение индексатора hello.

Например, так можно устранить расхождения в именах полей:

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Индексатор может содержать несколько сопоставлений полей. Например, так можно разветвить поле:

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Поиск Azure использует сравнение без учета регистра tooresolve hello поле имена и функций в сопоставления полей. Это удобно, (а не tooget все hello регистр вправо), но это означает, что источник данных или индекс не может иметь поля, которые отличаются только регистром.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Функции сопоставления полей
В настоящее время поддерживаются следующие функции:

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Выполняет *URL-безопасными* кодирование Base64 hello входной строки. Предполагается, что входные данные hello в кодировке UTF-8.

#### <a name="sample-use-case"></a>Примеры вариантов использования
Только URL-безопасными символов могут отображаться в ключ документа поиска Azure (так как пользователь должен был документ hello tooaddress может, например с помощью hello API поиска). Если данные содержат URL-адрес небезопасных символов и toouse его toopopulate поля ключа в индексе поиска, используйте эту функцию.   

#### <a name="example"></a>Пример
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Выполняет декодирование Base64 hello входной строки. Hello входных данных принимается tooa *URL-безопасными* строки в кодировке Base64.

#### <a name="sample-use-case"></a>Примеры вариантов использования
Значения настраиваемых метаданных BLOB-объекта должны быть в кодировке ASCII. Можно использовать Base64 кодирования toorepresent произвольные строки в Юникоде в пользовательские метаданные большого двоичного объекта. Тем не менее поиск toomake смысла, можно использовать эти данные в кодировке hello tooturn функция обратно в строки «стандартными» при заполнении индекса поиска.  

#### <a name="example"></a>Пример
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Разбиений в строковом поле с помощью hello указан разделитель и получает маркер hello на hello указанной позиции результирующей разбиение hello.

Например, если hello входные данные — `Jane Doe`, hello `delimiter` — `" "`(пробел) и hello `position` равно 0, результат hello `Jane`; Если hello `position` -1, результат hello `Doe`. Если позиция hello ссылается tooa маркер, который не существует, будет возвращена ошибка.

#### <a name="sample-use-case"></a>Примеры вариантов использования
Источник данных содержит `PersonName` поле, чтобы tooindex его как два отдельных `FirstName` и `LastName` поля. Можно использовать toosplit этой функции hello, входной символ hello пространство используется в качестве разделителя hello.

#### <a name="parameters"></a>Параметры
* `delimiter`: строка toouse в качестве разделителя hello после разделения входной строки "hello".
* `position`: разбиение Отсчитываемая от нуля позиция hello маркера toopick после hello введите строку в целое число со знаком.    

#### <a name="example"></a>Пример
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Преобразует строку в формате JSON массив строк в массив строк, который можно использовать toopopulate `Collection(Edm.String)` в индекс hello.

Например, если строка ввода hello — `["red", "white", "blue"]`, а затем hello целевое поле типа `Collection(Edm.String)` будет заполняться значениями hello трех `red`, `white` и `blue`. Если входные значения нельзя проанализировать как массивы строк JSON, выдается ошибка.

#### <a name="sample-use-case"></a>Примеры вариантов использования
База данных SQL Azure не имеет встроенный тип данных, естественным образом сопоставляет слишком`Collection(Edm.String)` поля в поиске Azure. toopopulate строка коллекции полей, исходные данные как массив JSON строка форматирования и использовать эту функцию.

#### <a name="example"></a>Пример
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Помогите нам усовершенствовать службу поиска Azure
При наличии запросов компонентов или идеи об улучшениях, пожалуйста направляться toous на нашем [сайт UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
