---
title: "Обработка типов содержимого в Azure Logic Apps | Документация Майкрософт"
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
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="a9d6f-103">Обработка типов содержимого в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="a9d6f-103">Handle content types in logic apps</span></span>

<span data-ttu-id="a9d6f-104">Через приложение логики могут проходить различные типы содержимого, включая JSON, XML, неструктурированные файлы и двоичные данные.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="a9d6f-105">Обработчик приложений логики поддерживает все типы содержимого, однако некоторые типы он распознает изначально,</span><span class="sxs-lookup"><span data-stu-id="a9d6f-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="a9d6f-106">а другие могут потребовать преобразования или приведения.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="a9d6f-107">В этой статье описывается, как обработчик работает с различными типами содержимого и как при необходимости добиться их корректной обработки.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="a9d6f-108">Заголовок Content-Type</span><span class="sxs-lookup"><span data-stu-id="a9d6f-108">Content-Type Header</span></span>

<span data-ttu-id="a9d6f-109">Для начала рассмотрим два типа `Content-Types`, не требующих преобразования или приведения для использования в приложении логики: `application/json` и `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="a9d6f-110">Приложение/JSON</span><span class="sxs-lookup"><span data-stu-id="a9d6f-110">Application/JSON</span></span>

<span data-ttu-id="a9d6f-111">Обработчик рабочего процесса определяет способ обработки по заголовку `Content-Type` в HTTP-вызовах.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="a9d6f-112">Любой запрос с типом содержимого `application/json` храниться и обрабатывается как объект JSON.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="a9d6f-113">Кроме того, содержимое JSON может быть проанализировано по умолчанию без преобразования.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="a9d6f-114">Например, в рабочем процессе можно проанализировать запрос, который имеет заголовок типа содержимого `application/json `, с помощью выражения `@body('myAction')['foo'][0]` для получения значения `bar` (в данном случае):</span><span class="sxs-lookup"><span data-stu-id="a9d6f-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="a9d6f-115">Дополнительное преобразование не требуется.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-115">No additional casting is needed.</span></span> <span data-ttu-id="a9d6f-116">Если вы работаете с данными формата JSON и у вас не указан заголовок, их можно привести в формат JSON вручную с помощью функции `@json()`, например `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="a9d6f-117">Схема и генератор схем</span><span class="sxs-lookup"><span data-stu-id="a9d6f-117">Schema and schema generator</span></span>

<span data-ttu-id="a9d6f-118">Триггер запроса позволяет добавить схему JSON для полезных данных, которые ожидается получить.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="a9d6f-119">Это схема позволяет конструктору генерировать токены, чтобы упростить использование содержимого запроса.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="a9d6f-120">Если у вас нет схемы, выберите **Использовать полезную нагрузку из примера для создания схемы**, чтобы создать схему JSON из примера полезных данных.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![SCHEMA (Схема)](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="a9d6f-122">Действие Parse JSON</span><span class="sxs-lookup"><span data-stu-id="a9d6f-122">'Parse JSON' action</span></span>

<span data-ttu-id="a9d6f-123">Действие `Parse JSON` позволяет проанализировать содержимое JSON, преобразив его в понятные токены для приложения логики.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="a9d6f-124">Как и триггер запроса, это действие позволяет добавить или создать схему JSON для содержимого, которое необходимо проанализировать.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="a9d6f-125">Этот инструмент упрощает использование данных из служебной шины, Azure Cosmos DB и т. д.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Parse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="a9d6f-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="a9d6f-127">Text/plain</span></span>

<span data-ttu-id="a9d6f-128">Как и в случае с `application/json`, HTTP-сообщения, полученные с заголовком `Content-Type` типа `text/plain`, хранятся в необработанном виде.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="a9d6f-129">Кроме того, если эти сообщения включены в последующие действия без какого-либо приведения, запрос будет передан с заголовком `Content-Type`: `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="a9d6f-130">Например, при работе с неструктурированным файлом вы можете получить содержимое HTTP в виде `text/plain`:</span><span class="sxs-lookup"><span data-stu-id="a9d6f-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="a9d6f-131">Если в следующем действии запрос отправляется как тело другого запроса (`@body('flatfile')`), запрос получает заголовок Content-Type типа `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="a9d6f-132">Если вы работаете с данными в формате простого текста и у вас не указан заголовок, их можно привести в формат текста вручную с помощью функции `@string()`, например `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="a9d6f-133">Application/xml, Application/octet-stream и функции преобразователя</span><span class="sxs-lookup"><span data-stu-id="a9d6f-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="a9d6f-134">Обработчик приложений логики всегда сохраняет `Content-Type`, полученный в HTTP-запросе или ответе.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="a9d6f-135">Поэтому, если обработчик получает содержимое с заголовком `Content-Type` типа `application/octet-stream` и вы добавляете это содержимое в последующее действие без приведения, исходящий запрос будет иметь заголовок `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="a9d6f-136">Таким образом обработчик может гарантировать, что при прохождении через рабочий процесс данные не будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="a9d6f-137">При этом состояние действия (входные и выходные данные) хранится в объекте JSON, так как оно проходит через рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="a9d6f-138">Поэтому для сохранения некоторых типов данных обработчик преобразует содержимое в двоичную строку в кодировке Base64 с соответствующими метаданными, сохраняя и `$content`, и `$content-type`, преобразование которых выполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="a9d6f-139">`@json()`: приводит данные в `application/json`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="a9d6f-140">`@xml()`: приводит данные в `application/xml`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="a9d6f-141">`@binary()`: приводит данные в `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="a9d6f-142">`@string()`: приводит данные в `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="a9d6f-143">`@base64()` приводит содержимое в строку Base64.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="a9d6f-144">`@base64toString()` приводит строку в кодировке Base64 в `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="a9d6f-145">`@base64toBinary()` приводит строку в кодировке Base64 в `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="a9d6f-146">`@encodeDataUri()` кодирует строку как массив байтов dataUri.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="a9d6f-147">`@decodeDataUri()` декодирует dataUri в массив байтов.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="a9d6f-148">Например, при получении HTTP-запроса с `Content-Type`: `application/xml`:</span><span class="sxs-lookup"><span data-stu-id="a9d6f-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="a9d6f-149">Вы можете привести данные, а затем использовать их, например, в `@xml(triggerBody())` либо в какой-то функции, например в `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="a9d6f-150">Другие типы содержимого</span><span class="sxs-lookup"><span data-stu-id="a9d6f-150">Other content types</span></span>

<span data-ttu-id="a9d6f-151">Другие типы содержимого поддерживаются и работают с приложениями логики, но для этого может потребоваться извлечение тела запроса вручную путем декодирования `$content`.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="a9d6f-152">Например, предположим вы инициируете запрос `application/x-www-url-formencoded`, где `$content` — это полезная нагрузка, закодированная в виде строки Base64 для сохранения всех данных:</span><span class="sxs-lookup"><span data-stu-id="a9d6f-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="a9d6f-153">Так как запрос не имеет формат простого текста или JSON, он сохраняется в действии в следующем виде:</span><span class="sxs-lookup"><span data-stu-id="a9d6f-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

В настоящее время встроенной функции для формирования данных нет, поэтому эти данные можно использовать в рабочем процессе, обращаясь к ним вручную с помощью функции вида `@string(body('formdataAction'))`. Если исходящий запрос должен также иметь заголовок content-type типа `application/x-www-url-formencoded`, вы можете добавить запрос в тело действия без приведения (например, `@body('formdataAction')`). Однако этот метод работает, только если тело запроса является единственным параметром входных данных `body`. <span data-ttu-id="a9d6f-157">Если вы попытаетесь использовать `@body('formdataAction')` в запросе `application/json`, вы получите ошибку выполнения, так как тело запроса будет отправлено в закодированном виде.</span><span class="sxs-lookup"><span data-stu-id="a9d6f-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

