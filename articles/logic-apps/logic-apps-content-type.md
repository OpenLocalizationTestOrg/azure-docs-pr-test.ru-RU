---
title: "типы содержимого aaaHandle - приложения логики Azure | Документы Microsoft"
description: "Принципы работы Azure Logic Apps с типами содержимого в среде разработки и в среде выполнения"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a>Обработка типов содержимого в приложениях логики

Через приложение логики могут проходить различные типы содержимого, включая JSON, XML, неструктурированные файлы и двоичные данные. Хотя hello Engine логику приложения поддерживает все типы содержимого, некоторые изначально воспринимает hello Engine логику приложения. а другие могут потребовать преобразования или приведения. Эта статья описывает, как hello engine обрабатывает разные типы содержимого и как toocorrectly обрабатывать такие типы, при необходимости.

## <a name="content-type-header"></a>Заголовок Content-Type

toostart по сути, давайте взглянем на hello двух `Content-Types` , не требуют преобразования или приведения, который можно использовать в приложении логику: `application/json` и `text/plain`.

## <a name="applicationjson"></a>Приложение/JSON

Hello потоков работ зависит от hello `Content-Type` заголовок HTTP вызывает соответствующую обработку toodetermine hello. Любой запрос с типом содержимого hello `application/json` хранится и обрабатывается как объект JSON. Кроме того, содержимое JSON может быть проанализировано по умолчанию без преобразования. 

Например, можно проанализировать запрос, который имеет заголовок content-type hello `application/json ` в рабочем процессе с помощью выражения, подобного `@body('myAction')['foo'][0]` tooget hello значение `bar` в этом случае:

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

Дополнительное преобразование не требуется. При работе с данными, JSON, но не имеет заголовка, указанного вручную можно его с помощью hello tooJSON `@json()` функции, например: `@json(triggerBody())['foo']`.

### <a name="schema-and-schema-generator"></a>Схема и генератор схем

Hello запрос триггер позволяет tooenter схему JSON для полезных данных hello предполагается, что tooreceive. Эта схема позволяет конструктор hello создания токенов, поэтому вы можете использовать hello содержимое запроса hello. При отсутствии готовности схемы выберите **использовать образец полезных данных toogenerate схему**, поэтому на основе образца полезных данных можно создать схему JSON.

![Схема](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>Действие Parse JSON

Hello `Parse JSON` действие позволяет проанализировать содержимое JSON в понятное маркеры для использования логики приложения. Аналогичный запрос toohello срабатывание триггера, это действие позволяет введите или создайте схему JSON для содержимого, что нужно tooparse hello. Этот инструмент упрощает использование данных из служебной шины, Azure Cosmos DB и т. д.

![Parse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>Text/plain

Аналогичные слишком`application/json`, HTTP-сообщения, полученные с hello `Content-Type` заголовок `text/plain` хранятся в необработанном виде. Кроме того, если эти сообщения включены в последующие действия без какого-либо приведения, запрос будет передан с заголовком `Content-Type`: `text/plain`. Например, при работе с неструктурированным файлом вы можете получить содержимое HTTP в виде `text/plain`:

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

При отправке запроса hello в следующее действие hello, тексте hello другой запрос (`@body('flatfile')`), будет иметь запрос hello `text/plain` Заголовок Content-Type. При работе с данными, обычный текст, но не имеет заголовка, указанного вручную можно привести hello tootext данных, с помощью hello `@string()` функции, например: `@string(triggerBody())`.

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Application/xml, Application/octet-stream и функции преобразователя

Hello Engine логику приложения всегда сохраняет hello `Content-Type` , полученного на hello HTTP-запроса или ответа. Таким образом, если обработчик hello Получает содержимое с hello `Content-Type` из `application/octet-stream`, а вы включаете содержимого в последующие действия без приведения, hello исходящего запроса наличие `Content-Type`: `application/octet-stream`. Таким образом, hello обработчик гарантии, что данные не потеряны во время перемещения посредством hello рабочего процесса. Однако hello состояния действия (входы и выходы) хранится в объект JSON, поскольку hello состояние прохождения hello рабочего процесса. Поэтому toopreserve, некоторые типы данных, механизм hello преобразует hello строка содержимого tooa двоичный в кодировке base64 с соответствующие метаданные, и сохраняет `$content` и `$content-type`, которой будут автоматически преобразованы. 

* `@json()`-слишком приводит данных`application/json`
* `@xml()`-слишком приводит данных`application/xml`
* `@binary()`-слишком приводит данных`application/octet-stream`
* `@string()`-слишком приводит данных`text/plain`
* `@base64()`— Преобразует строку base64 содержимого tooa
* `@base64toString()`-слишком преобразует строку в кодировке base64`text/plain`
* `@base64toBinary()`-слишком преобразует строку в кодировке base64`application/octet-stream`
* `@encodeDataUri()` кодирует строку как массив байтов dataUri.
* `@decodeDataUri()` декодирует dataUri в массив байтов.

Например, при получении HTTP-запроса с `Content-Type`: `application/xml`:

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

Вы можете привести данные, а затем использовать их, например, в `@xml(triggerBody())` либо в какой-то функции, например в `@xpath(xml(triggerBody()), '/CustomerName')`.

## <a name="other-content-types"></a>Другие типы содержимого

Поддерживаются другие типы содержимого и работы с приложениями логики, но может потребоваться вручную извлечение текста сообщения hello при декодировании hello `$content`. Предположим, что вы инициируете `application/x-www-url-formencoded` запроса where `$content` полезных данных hello кодируется как строка base64 toopreserve все данные:

```
CustomerName=Frank&Address=123+Avenue
```

Так как запрос hello не обычный текст или JSON, hello запроса хранятся в действие hello следующим образом:

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

В настоящее время собственную функцию для данных формы, не существует, поэтому можно продолжать использовать эти данные в рабочем процессе, вручную, обратившись к hello данные с помощью функции как `@string(body('formdataAction'))`. При желании hello исходящего запроса tooalso имеют hello `application/x-www-url-formencoded` заголовок content-type, можно добавить текст hello запроса toohello действие без приведения типов как `@body('formdataAction')`. Тем не менее, этот метод работает, только если текст hello является единственным параметром hello в hello `body` ввода. Если при попытке toouse `@body('formdataAction')` в `application/json` запрос, возникнет ошибка времени выполнения, так как текст в кодировке hello отправляется.

