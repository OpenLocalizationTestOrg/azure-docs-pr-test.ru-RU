---
title: "привязки функции Twilio aaaAzure | Документы Microsoft"
description: "Понять, как toouse Twilio привязки с помощью функций Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a>Отправка SMS-сообщений от функций Azure с помощью hello Twilio привязка для вывода
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как tooconfigure и использование Twilio привязки с помощью функций Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Функции Azure поддерживает Twilio выходные данные привязки tooenable текст функции toosend SMS сообщений с помощью нескольких строк кода и [Twilio](https://www.twilio.com/) учетной записи. 

## <a name="functionjson-for-hello-twilio-output-binding"></a>Вывод Twilio Function.JSON для hello привязки
файл function.json Hello предоставляет hello следующие свойства:

* `name`: Переменной имя, используемое в коде функция для Twilio SMS-сообщение hello.
* `type`: необходимо задать слишком*«twilioSms»*.
* `accountSid`: Это значение должно быть установлено toohello имя параметра приложения, содержащий ваш ИД безопасности учетной записи Twilio.
* `authToken`: Это значение должно быть установлено toohello имя параметра приложения, содержащий токен проверки подлинности Twilio.
* `to`: Это значение toohello номер телефона для отправки SMS текста hello.
* `from`: Это значение toohello номер телефона, отправляемый из текста hello SMS.
* `direction`: необходимо задать слишком*«out»*.
* `body`: Это значение может быть используется toohard кода hello SMS-сообщение, если не требуется tooset динамически в hello кода функции. 

Пример файла function.json:

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a>Пример триггера очереди C# с выходной привязкой Twilio
#### <a name="synchronous"></a>Синхронный
Этот код пример синхронной для триггера очереди хранилища Azure использует выполнении toosend параметр клиента tooa текст сообщения, разместившего заказ.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a>Асинхронный
Этот код асинхронного образца для триггера очереди хранилища Azure отправляет клиента tooa текст сообщения, разместившего заказ.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a>Пример триггера очереди Node.js с выходной привязкой Twilio
В этом примере Node.js отправляет клиента tooa текст сообщения, разместившего заказ.

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

