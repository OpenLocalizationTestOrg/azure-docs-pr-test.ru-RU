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
# <a name="azure-functions-mobile-apps-bindings"></a>Привязки мобильных приложений в функциях Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как tooconfigure и код [мобильных приложений Azure](../app-service-mobile/app-service-mobile-value-prop.md) привязок в функциях Azure. Функции Azure поддерживают входные и выходные привязки для мобильных приложений.

Hello мобильные приложения входной и выходной привязки позволяют [чтения и записи таблицы toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) в мобильном приложении.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Входная привязка мобильных приложений
Привязка ввода мобильные приложения Hello загружает записи из таблицы мобильных конечной точки и передает его в функции. В C# и F # функции любые изменения, внесенные toohello записи автоматически отправляются назад toohello таблицы, при выходе из функции hello, успешно.

Мобильные приложения Hello ввода функция tooa использует следующий объект JSON в hello hello `bindings` массив function.json:

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

Обратите внимание hello следующие:

* `id`может быть статическим, или он может быть основан на hello триггер, который вызывает функции hello. Например, если вы используете [очереди триггера]() функции, затем `"id": "{queueTrigger}"` использует hello строковое значение сообщения hello очереди как hello записей tooretrieve идентификатор.
* `connection`должен содержать hello имя параметра приложения в приложении функции, который в свою очередь содержит URL-адрес hello мобильного приложения. функции Hello использует этот операции URL-адрес tooconstruct hello необходимые REST от мобильного приложения. Вы [создаются Настройка приложения в приложении функции]() , содержащий URL-адрес мобильного приложения (который выглядит как `http://<appname>.azurewebsites.net`), затем укажите имя параметра приложения hello hello в hello `connection` свойство в вашей входной привязки. 
* Требуется toospecify `apiKey` Если вы [реализовать ключ API в серверной части мобильных приложений Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), или [реализовать ключ API в серверной части мобильных приложений .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo это, вы [создаются Настройка приложения в приложении функции]() , содержащий ключ hello API, затем добавьте hello `apiKey` свойство в вашей входной привязки с именем hello объекта параметра приложения hello. 
  
  > [!IMPORTANT]
  > Этот ключ API не должен использоваться совместно с клиентами мобильного приложения. Он должен иметь распределенных безопасно tooservice стороне клиентов, подобно функциям Azure. 
  > 
  > [!NOTE]
  > Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями. Таким образом обеспечивается защита конфиденциальной информации.
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>Использование входной привязки
В этом разделе показано, как toouse входные привязки в коде функция мобильных приложений. 

Если запись hello с hello найти идентификатор таблицы и записи, передаваемый в hello с именем [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) параметра (или в Node.js, он передается hello `context.bindings.<name>` объекта). При записи hello не найден, параметр hello является `null`. 

В функции C# и F # любые изменения, внесенные toohello ввода записи (входной параметр) автоматически отправляются назад toohello таблицы мобильные приложения при выходе из функции hello, успешно. В функции Node.js с помощью `context.bindings.<name>` tooaccess hello входной записи. Изменить запись в Node.js невозможно.

<a name="inputsample"></a>

## <a name="input-sample"></a>Пример входной привязки
Предположим, что имеется следующая function.json hello получает записи таблицы мобильное приложение с идентификатором hello триггер очереди приветственное сообщение:

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

См. пример hello зависящие от языка, который использует hello входной записи из привязки hello. Примеры C# и F # Hello также изменить запись hello `text` свойство.

* [C#](#inputcsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Пример входной привязки для языка C# #

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

### <a name="input-sample-in-nodejs"></a>Пример входной привязки для Node.js

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Выходная привязка мобильных приложений
Мобильные приложения hello использование вывода toowrite привязки новую конечную точку таблицы записей tooa мобильные приложения.  

выходные данные функции применяется следующий объект JSON в hello hello мобильные приложения Hello `bindings` массив function.json:

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

Обратите внимание hello следующие:

* `connection`должен содержать hello имя параметра приложения в приложении функции, который в свою очередь содержит URL-адрес hello мобильного приложения. функции Hello использует этот операции URL-адрес tooconstruct hello необходимые REST от мобильного приложения. Вы [создаются Настройка приложения в приложении функции]() , содержащий URL-адрес мобильного приложения (который выглядит как `http://<appname>.azurewebsites.net`), затем укажите имя параметра приложения hello hello в hello `connection` свойство в вашей входной привязки. 
* Требуется toospecify `apiKey` Если вы [реализовать ключ API в серверной части мобильных приложений Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), или [реализовать ключ API в серверной части мобильных приложений .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo это, вы [создаются Настройка приложения в приложении функции]() , содержащий ключ hello API, затем добавьте hello `apiKey` свойство в вашей входной привязки с именем hello объекта параметра приложения hello. 
  
  > [!IMPORTANT]
  > Этот ключ API не должен использоваться совместно с клиентами мобильного приложения. Он должен иметь распределенных безопасно tooservice стороне клиентов, подобно функциям Azure. 
  > 
  > [!NOTE]
  > Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями. Таким образом обеспечивается защита конфиденциальной информации.
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>Использование выходной привязки
В этом разделе показано, как toouse вывода привязки в коде функция мобильных приложений. 

В C# функции, используйте именованный выходной параметр типа `out object` tooaccess hello выходные данные записи. В функции Node.js с помощью `context.bindings.<name>` tooaccess hello выходные данные записи.

<a name="outputsample"></a>

## <a name="output-sample"></a>Пример выходной привязки
Предположим, что имеется следующая function.json, который определяет триггер очередь и вывода мобильные приложения hello:

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

См. Образец hello конкретного языка, создает запись в конечной таблице hello мобильные приложения с содержимым hello приветственное сообщение очереди.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Пример выходной привязки для языка C# #

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

### <a name="output-sample-in-nodejs"></a>Пример выходной привязки для Node.js

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

