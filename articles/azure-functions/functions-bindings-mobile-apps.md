---
title: "Привязки мобильных приложений в Функциях Azure | Документация Майкрософт"
description: "Узнайте, как использовать привязки мобильных приложений Azure в функциях Azure."
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
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="adfab-104">Привязки мобильных приложений в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="adfab-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="adfab-105">Эта статья объясняет, как настроить и запрограммировать привязки [мобильных приложений Azure](../app-service-mobile/app-service-mobile-value-prop.md) в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="adfab-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="adfab-106">Функции Azure поддерживают входные и выходные привязки для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="adfab-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="adfab-107">Входные и выходные привязки мобильных приложений позволяют выполнять [чтение и запись в таблицах данных](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) в вашем мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="adfab-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="adfab-108">Входная привязка мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="adfab-108">Mobile Apps input binding</span></span>
<span data-ttu-id="adfab-109">Входная привязка мобильных приложений загружает запись из конечной точки мобильной таблицы и передает ее в функцию.</span><span class="sxs-lookup"><span data-stu-id="adfab-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="adfab-110">В функциях C# и F# любые изменения, внесенные в запись, автоматически отправляются обратно в таблицу после успешного выхода из функции.</span><span class="sxs-lookup"><span data-stu-id="adfab-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="adfab-111">Входные данные мобильных приложений для функции используют следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="adfab-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="adfab-112">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="adfab-112">Note the following:</span></span>

* <span data-ttu-id="adfab-113">Параметр `id` может быть статическим или определяться по триггеру, который вызывает функцию.</span><span class="sxs-lookup"><span data-stu-id="adfab-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="adfab-114">Например, если вы используете [триггер очереди]() для функции, то `"id": "{queueTrigger}"` использует строковое значение сообщения очереди в качестве идентификатора записи, который нужно получить.</span><span class="sxs-lookup"><span data-stu-id="adfab-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="adfab-115">Параметр `connection` должен содержать имя параметра приложения в приложении-функции, которое, в свою очередь, содержит URL-адрес мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="adfab-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="adfab-116">Функция использует этот URL-адрес для создания необходимых операций REST с мобильным приложением.</span><span class="sxs-lookup"><span data-stu-id="adfab-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="adfab-117">[Создайте параметр приложения в приложении-функции](), содержащем URL-адрес мобильного приложения (который выглядит следующим образом: `http://<appname>.azurewebsites.net`), а затем укажите имя параметра приложения в свойстве `connection` во входной привязке.</span><span class="sxs-lookup"><span data-stu-id="adfab-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="adfab-118">При [внедрении ключа API в серверной части мобильного приложения Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) или [.NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key) необходимо указать `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="adfab-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="adfab-119">Для этого [создайте параметр приложения в приложении-функции](), содержащем ключ API, а затем добавьте свойство `apiKey` в свою входную привязку с именем параметра приложения.</span><span class="sxs-lookup"><span data-stu-id="adfab-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="adfab-120">Этот ключ API не должен использоваться совместно с клиентами мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="adfab-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="adfab-121">Его нужно безопасно распространять среди клиентов на стороне службы, таких как Функции Azure.</span><span class="sxs-lookup"><span data-stu-id="adfab-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="adfab-122">Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="adfab-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="adfab-123">Таким образом обеспечивается защита конфиденциальной информации.</span><span class="sxs-lookup"><span data-stu-id="adfab-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="adfab-124">Использование входной привязки</span><span class="sxs-lookup"><span data-stu-id="adfab-124">Input usage</span></span>
<span data-ttu-id="adfab-125">В этом разделе показано, как использовать входную привязку мобильных приложений в коде функции.</span><span class="sxs-lookup"><span data-stu-id="adfab-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="adfab-126">Когда будет найдена запись с указанной таблицей и идентификатором записи, она передается в именованный параметр [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) (в Node.js она передается в объект `context.bindings.<name>`).</span><span class="sxs-lookup"><span data-stu-id="adfab-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="adfab-127">Если запись не найдена, параметр имеет значение `null`.</span><span class="sxs-lookup"><span data-stu-id="adfab-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="adfab-128">В функциях C# и F# любые изменения, внесенные во входную запись (входной параметр), будут автоматически отправляться обратно в таблицу мобильных приложений после успешного выхода из функции.</span><span class="sxs-lookup"><span data-stu-id="adfab-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="adfab-129">Для доступа к входной записи в функциях Node.js используйте `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="adfab-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="adfab-130">Изменить запись в Node.js невозможно.</span><span class="sxs-lookup"><span data-stu-id="adfab-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="adfab-131">Пример входной привязки</span><span class="sxs-lookup"><span data-stu-id="adfab-131">Input sample</span></span>
<span data-ttu-id="adfab-132">Предположим, что у вас есть следующий файл function.json, извлекающий запись таблицы мобильного приложения с идентификатором сообщения триггера очереди:</span><span class="sxs-lookup"><span data-stu-id="adfab-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

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

<span data-ttu-id="adfab-133">Ознакомьтесь с примером для конкретного языка, использующим входную запись из привязки.</span><span class="sxs-lookup"><span data-stu-id="adfab-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="adfab-134">Примеры C# и F # также изменяют свойство записи `text`.</span><span class="sxs-lookup"><span data-stu-id="adfab-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="adfab-135">C#</span><span class="sxs-lookup"><span data-stu-id="adfab-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="adfab-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="adfab-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="adfab-137">Пример входной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="adfab-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="adfab-138">Пример входной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="adfab-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="adfab-139">Выходная привязка мобильных приложений</span><span class="sxs-lookup"><span data-stu-id="adfab-139">Mobile Apps output binding</span></span>
<span data-ttu-id="adfab-140">Используйте выходную привязку мобильных приложений, чтобы сделать новую запись в конечную точку таблицы мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="adfab-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="adfab-141">Выходные данные мобильных приложений для функции используют следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="adfab-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="adfab-142">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="adfab-142">Note the following:</span></span>

* <span data-ttu-id="adfab-143">Параметр `connection` должен содержать имя параметра приложения в приложении-функции, которое, в свою очередь, содержит URL-адрес мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="adfab-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="adfab-144">Функция использует этот URL-адрес для создания необходимых операций REST с мобильным приложением.</span><span class="sxs-lookup"><span data-stu-id="adfab-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="adfab-145">[Создайте параметр приложения в приложении-функции](), содержащем URL-адрес мобильного приложения (который выглядит следующим образом: `http://<appname>.azurewebsites.net`), а затем укажите имя параметра приложения в свойстве `connection` во входной привязке.</span><span class="sxs-lookup"><span data-stu-id="adfab-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="adfab-146">При [внедрении ключа API в серверной части мобильного приложения Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) или [.NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key) необходимо указать `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="adfab-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="adfab-147">Для этого [создайте параметр приложения в приложении-функции](), содержащем ключ API, а затем добавьте свойство `apiKey` в свою входную привязку с именем параметра приложения.</span><span class="sxs-lookup"><span data-stu-id="adfab-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="adfab-148">Этот ключ API не должен использоваться совместно с клиентами мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="adfab-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="adfab-149">Его нужно безопасно распространять среди клиентов на стороне службы, таких как Функции Azure.</span><span class="sxs-lookup"><span data-stu-id="adfab-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="adfab-150">Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="adfab-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="adfab-151">Таким образом обеспечивается защита конфиденциальной информации.</span><span class="sxs-lookup"><span data-stu-id="adfab-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="adfab-152">Использование выходной привязки</span><span class="sxs-lookup"><span data-stu-id="adfab-152">Output usage</span></span>
<span data-ttu-id="adfab-153">В этом разделе показано, как использовать выходную привязку мобильных приложений в коде функции.</span><span class="sxs-lookup"><span data-stu-id="adfab-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="adfab-154">Для доступа к выходной записи в функциях C# используйте именованный выходной параметр типа `out object`.</span><span class="sxs-lookup"><span data-stu-id="adfab-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="adfab-155">Для доступа к выходной записи в функциях Node.js используйте `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="adfab-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="adfab-156">Пример выходной привязки</span><span class="sxs-lookup"><span data-stu-id="adfab-156">Output sample</span></span>
<span data-ttu-id="adfab-157">Предположим, что у вас есть следующий файл function.json, определяющий триггер очереди и выходные данные мобильных приложений:</span><span class="sxs-lookup"><span data-stu-id="adfab-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="adfab-158">Ознакомьтесь с примером для конкретного языка, который создает запись в таблице конечной точки мобильных приложений с содержимым сообщения очереди.</span><span class="sxs-lookup"><span data-stu-id="adfab-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="adfab-159">C#</span><span class="sxs-lookup"><span data-stu-id="adfab-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="adfab-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="adfab-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="adfab-161">Пример выходной привязки для языка C#</span><span class="sxs-lookup"><span data-stu-id="adfab-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="adfab-162">Пример выходной привязки для Node.js</span><span class="sxs-lookup"><span data-stu-id="adfab-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="adfab-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="adfab-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

