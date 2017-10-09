---
title: "привязки функции мобильные приложения aaaAzure | Документы Microsoft"
description: "Понять, как привязки toouse мобильных приложений Azure в функциях Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="b5862-104">Привязки мобильных приложений в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="b5862-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b5862-105">В этой статье объясняется, как tooconfigure и код [мобильных приложений Azure](../app-service-mobile/app-service-mobile-value-prop.md) привязок в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="b5862-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="b5862-106">Функции Azure поддерживают входные и выходные привязки для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="b5862-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="b5862-107">Hello мобильные приложения входной и выходной привязки позволяют [чтения и записи таблицы toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) в мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="b5862-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="b5862-108">Входная привязка мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="b5862-108">Mobile Apps input binding</span></span>
<span data-ttu-id="b5862-109">Привязка ввода мобильные приложения Hello загружает записи из таблицы мобильных конечной точки и передает его в функции.</span><span class="sxs-lookup"><span data-stu-id="b5862-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="b5862-110">В C# и F # функции любые изменения, внесенные toohello записи автоматически отправляются назад toohello таблицы, при выходе из функции hello, успешно.</span><span class="sxs-lookup"><span data-stu-id="b5862-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="b5862-111">Мобильные приложения Hello ввода функция tooa использует следующий объект JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="b5862-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="b5862-112">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="b5862-112">Note hello following:</span></span>

* <span data-ttu-id="b5862-113">`id`может быть статическим, или он может быть основан на hello триггер, который вызывает функции hello.</span><span class="sxs-lookup"><span data-stu-id="b5862-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="b5862-114">Например, если вы используете [очереди триггера]() функции, затем `"id": "{queueTrigger}"` использует hello строковое значение сообщения hello очереди как hello записей tooretrieve идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b5862-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="b5862-115">`connection`должен содержать hello имя параметра приложения в приложении функции, который в свою очередь содержит URL-адрес hello мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b5862-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="b5862-116">функции Hello использует этот операции URL-адрес tooconstruct hello необходимые REST от мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b5862-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="b5862-117">Вы [создаются Настройка приложения в приложении функции]() , содержащий URL-адрес мобильного приложения (который выглядит как `http://<appname>.azurewebsites.net`), затем укажите имя параметра приложения hello hello в hello `connection` свойство в вашей входной привязки.</span><span class="sxs-lookup"><span data-stu-id="b5862-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="b5862-118">Требуется toospecify `apiKey` Если вы [реализовать ключ API в серверной части мобильных приложений Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), или [реализовать ключ API в серверной части мобильных приложений .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="b5862-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="b5862-119">toodo это, вы [создаются Настройка приложения в приложении функции]() , содержащий ключ hello API, затем добавьте hello `apiKey` свойство в вашей входной привязки с именем hello объекта параметра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b5862-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="b5862-120">Этот ключ API не должен использоваться совместно с клиентами мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b5862-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="b5862-121">Он должен иметь распределенных безопасно tooservice стороне клиентов, подобно функциям Azure.</span><span class="sxs-lookup"><span data-stu-id="b5862-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="b5862-122">Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="b5862-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="b5862-123">Таким образом обеспечивается защита конфиденциальной информации.</span><span class="sxs-lookup"><span data-stu-id="b5862-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="b5862-124">Использование входной привязки</span><span class="sxs-lookup"><span data-stu-id="b5862-124">Input usage</span></span>
<span data-ttu-id="b5862-125">В этом разделе показано, как toouse входные привязки в коде функция мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="b5862-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="b5862-126">Если запись hello с hello найти идентификатор таблицы и записи, передаваемый в hello с именем [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) параметра (или в Node.js, он передается hello `context.bindings.<name>` объекта).</span><span class="sxs-lookup"><span data-stu-id="b5862-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="b5862-127">При записи hello не найден, параметр hello является `null`.</span><span class="sxs-lookup"><span data-stu-id="b5862-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="b5862-128">В функции C# и F # любые изменения, внесенные toohello ввода записи (входной параметр) автоматически отправляются назад toohello таблицы мобильные приложения при выходе из функции hello, успешно.</span><span class="sxs-lookup"><span data-stu-id="b5862-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="b5862-129">В функции Node.js с помощью `context.bindings.<name>` tooaccess hello входной записи.</span><span class="sxs-lookup"><span data-stu-id="b5862-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="b5862-130">Изменить запись в Node.js невозможно.</span><span class="sxs-lookup"><span data-stu-id="b5862-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="b5862-131">Пример входной привязки</span><span class="sxs-lookup"><span data-stu-id="b5862-131">Input sample</span></span>
<span data-ttu-id="b5862-132">Предположим, что имеется следующая function.json hello получает записи таблицы мобильное приложение с идентификатором hello триггер очереди приветственное сообщение:</span><span class="sxs-lookup"><span data-stu-id="b5862-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="b5862-133">См. пример hello зависящие от языка, который использует hello входной записи из привязки hello.</span><span class="sxs-lookup"><span data-stu-id="b5862-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="b5862-134">Примеры C# и F # Hello также изменить запись hello `text` свойство.</span><span class="sxs-lookup"><span data-stu-id="b5862-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="b5862-135">C#</span><span class="sxs-lookup"><span data-stu-id="b5862-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="b5862-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="b5862-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="b5862-137">Пример входной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="b5862-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="b5862-138">Пример входной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="b5862-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="b5862-139">Выходная привязка мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="b5862-139">Mobile Apps output binding</span></span>
<span data-ttu-id="b5862-140">Мобильные приложения hello использование вывода toowrite привязки новую конечную точку таблицы записей tooa мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="b5862-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="b5862-141">выходные данные функции применяется следующий объект JSON в hello hello мобильные приложения Hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="b5862-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="b5862-142">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="b5862-142">Note hello following:</span></span>

* <span data-ttu-id="b5862-143">`connection`должен содержать hello имя параметра приложения в приложении функции, который в свою очередь содержит URL-адрес hello мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b5862-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="b5862-144">функции Hello использует этот операции URL-адрес tooconstruct hello необходимые REST от мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b5862-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="b5862-145">Вы [создаются Настройка приложения в приложении функции]() , содержащий URL-адрес мобильного приложения (который выглядит как `http://<appname>.azurewebsites.net`), затем укажите имя параметра приложения hello hello в hello `connection` свойство в вашей входной привязки.</span><span class="sxs-lookup"><span data-stu-id="b5862-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="b5862-146">Требуется toospecify `apiKey` Если вы [реализовать ключ API в серверной части мобильных приложений Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), или [реализовать ключ API в серверной части мобильных приложений .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="b5862-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="b5862-147">toodo это, вы [создаются Настройка приложения в приложении функции]() , содержащий ключ hello API, затем добавьте hello `apiKey` свойство в вашей входной привязки с именем hello объекта параметра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b5862-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="b5862-148">Этот ключ API не должен использоваться совместно с клиентами мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b5862-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="b5862-149">Он должен иметь распределенных безопасно tooservice стороне клиентов, подобно функциям Azure.</span><span class="sxs-lookup"><span data-stu-id="b5862-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="b5862-150">Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="b5862-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="b5862-151">Таким образом обеспечивается защита конфиденциальной информации.</span><span class="sxs-lookup"><span data-stu-id="b5862-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="b5862-152">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="b5862-152">Output usage</span></span>
<span data-ttu-id="b5862-153">В этом разделе показано, как toouse вывода привязки в коде функция мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="b5862-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="b5862-154">В C# функции, используйте именованный выходной параметр типа `out object` tooaccess hello выходные данные записи.</span><span class="sxs-lookup"><span data-stu-id="b5862-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="b5862-155">В функции Node.js с помощью `context.bindings.<name>` tooaccess hello выходные данные записи.</span><span class="sxs-lookup"><span data-stu-id="b5862-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="b5862-156">Пример выходной привязки</span><span class="sxs-lookup"><span data-stu-id="b5862-156">Output sample</span></span>
<span data-ttu-id="b5862-157">Предположим, что имеется следующая function.json, который определяет триггер очередь и вывода мобильные приложения hello:</span><span class="sxs-lookup"><span data-stu-id="b5862-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="b5862-158">См. Образец hello конкретного языка, создает запись в конечной таблице hello мобильные приложения с содержимым hello приветственное сообщение очереди.</span><span class="sxs-lookup"><span data-stu-id="b5862-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="b5862-159">C#</span><span class="sxs-lookup"><span data-stu-id="b5862-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b5862-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="b5862-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="b5862-161">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="b5862-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="b5862-162">Пример выходной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="b5862-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b5862-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5862-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

