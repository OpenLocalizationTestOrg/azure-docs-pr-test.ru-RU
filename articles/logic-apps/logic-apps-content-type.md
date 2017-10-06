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
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="ee1cb-103">Обработка типов содержимого в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="ee1cb-103">Handle content types in logic apps</span></span>

<span data-ttu-id="ee1cb-104">Через приложение логики могут проходить различные типы содержимого, включая JSON, XML, неструктурированные файлы и двоичные данные.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="ee1cb-105">Хотя hello Engine логику приложения поддерживает все типы содержимого, некоторые изначально воспринимает hello Engine логику приложения.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="ee1cb-106">а другие могут потребовать преобразования или приведения.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="ee1cb-107">Эта статья описывает, как hello engine обрабатывает разные типы содержимого и как toocorrectly обрабатывать такие типы, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="ee1cb-108">Заголовок Content-Type</span><span class="sxs-lookup"><span data-stu-id="ee1cb-108">Content-Type Header</span></span>

<span data-ttu-id="ee1cb-109">toostart по сути, давайте взглянем на hello двух `Content-Types` , не требуют преобразования или приведения, который можно использовать в приложении логику: `application/json` и `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="ee1cb-110">Приложение/JSON</span><span class="sxs-lookup"><span data-stu-id="ee1cb-110">Application/JSON</span></span>

<span data-ttu-id="ee1cb-111">Hello потоков работ зависит от hello `Content-Type` заголовок HTTP вызывает соответствующую обработку toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="ee1cb-112">Любой запрос с типом содержимого hello `application/json` хранится и обрабатывается как объект JSON.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="ee1cb-113">Кроме того, содержимое JSON может быть проанализировано по умолчанию без преобразования.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="ee1cb-114">Например, можно проанализировать запрос, который имеет заголовок content-type hello `application/json ` в рабочем процессе с помощью выражения, подобного `@body('myAction')['foo'][0]` tooget hello значение `bar` в этом случае:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="ee1cb-115">Дополнительное преобразование не требуется.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-115">No additional casting is needed.</span></span> <span data-ttu-id="ee1cb-116">При работе с данными, JSON, но не имеет заголовка, указанного вручную можно его с помощью hello tooJSON `@json()` функции, например: `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="ee1cb-117">Схема и генератор схем</span><span class="sxs-lookup"><span data-stu-id="ee1cb-117">Schema and schema generator</span></span>

<span data-ttu-id="ee1cb-118">Hello запрос триггер позволяет tooenter схему JSON для полезных данных hello предполагается, что tooreceive.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="ee1cb-119">Эта схема позволяет конструктор hello создания токенов, поэтому вы можете использовать hello содержимое запроса hello.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="ee1cb-120">При отсутствии готовности схемы выберите **использовать образец полезных данных toogenerate схему**, поэтому на основе образца полезных данных можно создать схему JSON.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Схема](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="ee1cb-122">Действие Parse JSON</span><span class="sxs-lookup"><span data-stu-id="ee1cb-122">'Parse JSON' action</span></span>

<span data-ttu-id="ee1cb-123">Hello `Parse JSON` действие позволяет проанализировать содержимое JSON в понятное маркеры для использования логики приложения.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="ee1cb-124">Аналогичный запрос toohello срабатывание триггера, это действие позволяет введите или создайте схему JSON для содержимого, что нужно tooparse hello.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="ee1cb-125">Этот инструмент упрощает использование данных из служебной шины, Azure Cosmos DB и т. д.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Parse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="ee1cb-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="ee1cb-127">Text/plain</span></span>

<span data-ttu-id="ee1cb-128">Аналогичные слишком`application/json`, HTTP-сообщения, полученные с hello `Content-Type` заголовок `text/plain` хранятся в необработанном виде.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="ee1cb-129">Кроме того, если эти сообщения включены в последующие действия без какого-либо приведения, запрос будет передан с заголовком `Content-Type`: `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="ee1cb-130">Например, при работе с неструктурированным файлом вы можете получить содержимое HTTP в виде `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="ee1cb-131">При отправке запроса hello в следующее действие hello, тексте hello другой запрос (`@body('flatfile')`), будет иметь запрос hello `text/plain` Заголовок Content-Type.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="ee1cb-132">При работе с данными, обычный текст, но не имеет заголовка, указанного вручную можно привести hello tootext данных, с помощью hello `@string()` функции, например: `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="ee1cb-133">Application/xml, Application/octet-stream и функции преобразователя</span><span class="sxs-lookup"><span data-stu-id="ee1cb-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="ee1cb-134">Hello Engine логику приложения всегда сохраняет hello `Content-Type` , полученного на hello HTTP-запроса или ответа.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="ee1cb-135">Таким образом, если обработчик hello Получает содержимое с hello `Content-Type` из `application/octet-stream`, а вы включаете содержимого в последующие действия без приведения, hello исходящего запроса наличие `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="ee1cb-136">Таким образом, hello обработчик гарантии, что данные не потеряны во время перемещения посредством hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="ee1cb-137">Однако hello состояния действия (входы и выходы) хранится в объект JSON, поскольку hello состояние прохождения hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="ee1cb-138">Поэтому toopreserve, некоторые типы данных, механизм hello преобразует hello строка содержимого tooa двоичный в кодировке base64 с соответствующие метаданные, и сохраняет `$content` и `$content-type`, которой будут автоматически преобразованы.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="ee1cb-139">`@json()`-слишком приводит данных`application/json`</span><span class="sxs-lookup"><span data-stu-id="ee1cb-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="ee1cb-140">`@xml()`-слишком приводит данных`application/xml`</span><span class="sxs-lookup"><span data-stu-id="ee1cb-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="ee1cb-141">`@binary()`-слишком приводит данных`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="ee1cb-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="ee1cb-142">`@string()`-слишком приводит данных`text/plain`</span><span class="sxs-lookup"><span data-stu-id="ee1cb-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="ee1cb-143">`@base64()`— Преобразует строку base64 содержимого tooa</span><span class="sxs-lookup"><span data-stu-id="ee1cb-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="ee1cb-144">`@base64toString()`-слишком преобразует строку в кодировке base64`text/plain`</span><span class="sxs-lookup"><span data-stu-id="ee1cb-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="ee1cb-145">`@base64toBinary()`-слишком преобразует строку в кодировке base64`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="ee1cb-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="ee1cb-146">`@encodeDataUri()` кодирует строку как массив байтов dataUri.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="ee1cb-147">`@decodeDataUri()` декодирует dataUri в массив байтов.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="ee1cb-148">Например, при получении HTTP-запроса с `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="ee1cb-149">Вы можете привести данные, а затем использовать их, например, в `@xml(triggerBody())` либо в какой-то функции, например в `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="ee1cb-150">Другие типы содержимого</span><span class="sxs-lookup"><span data-stu-id="ee1cb-150">Other content types</span></span>

<span data-ttu-id="ee1cb-151">Поддерживаются другие типы содержимого и работы с приложениями логики, но может потребоваться вручную извлечение текста сообщения hello при декодировании hello `$content`.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="ee1cb-152">Предположим, что вы инициируете `application/x-www-url-formencoded` запроса where `$content` полезных данных hello кодируется как строка base64 toopreserve все данные:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="ee1cb-153">Так как запрос hello не обычный текст или JSON, hello запроса хранятся в действие hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

В настоящее время собственную функцию для данных формы, не существует, поэтому можно продолжать использовать эти данные в рабочем процессе, вручную, обратившись к hello данные с помощью функции как `@string(body('formdataAction'))`. При желании hello исходящего запроса tooalso имеют hello `application/x-www-url-formencoded` заголовок content-type, можно добавить текст hello запроса toohello действие без приведения типов как `@body('formdataAction')`. Тем не менее, этот метод работает, только если текст hello является единственным параметром hello в hello `body` ввода. <span data-ttu-id="ee1cb-157">Если при попытке toouse `@body('formdataAction')` в `application/json` запрос, возникнет ошибка времени выполнения, так как текст в кодировке hello отправляется.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

