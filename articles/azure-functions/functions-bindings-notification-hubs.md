---
title: "Концентратор уведомлений функции привязки aaaAzure | Документы Microsoft"
description: "Понять, как привязки toouse концентратор уведомлений Azure в функциях Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Выходная привязка центра уведомлений для функций Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как привязки концентратор уведомлений Azure tooconfigure и код в функциях Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Функции могут отправлять push-уведомления всего несколькими строками кода, используя настроенный центр уведомлений Azure. Однако hello концентратор уведомлений Azure должны быть настроены для платформы уведомления службы (PNS) необходимо toouse hello. Дополнительные сведения о настройке концентратор уведомлений Azure и разработка клиентских приложений, которые регистрируют tooreceive уведомления см. в разделе [Приступая к работе с концентраторами уведомлений](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) и выберите целевую платформу на приветствия клиента Вверх.

Hello уведомлений, отправляемых может быть собственный уведомления или шаблон уведомления. Получения собственных уведомлений платформы уведомлений, настроенной в hello `platform` свойство hello привязка для вывода. Шаблон уведомления могут быть tootarget используется несколько платформ.   

## <a name="notification-hub-output-binding-properties"></a>Свойства привязки для вывода центра уведомлений
файл function.json Hello предоставляет hello следующие свойства:

* `name`: Переменной имя, используемое в коде функция для концентратора уведомлений приветственное сообщение.
* `type`: необходимо задать слишком*«концентратора уведомлений»*.
* `tagExpression`: Выражения с тегами разрешить toospecify доставить уведомления tooa набора устройств, имеющих зарегистрированные tooreceive уведомлений, которые соответствуют hello выражение тегов.  Дополнительные сведения см. в статье [Маршрутизация и выражения тегов](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Имя ресурса концентратора уведомлений hello в hello портал Azure.
* `connection`: Строка подключения должна быть **параметр приложения** toohello задать строку подключения *DefaultFullSharedAccessSignature* значения для центра уведомлений.
* `direction`: необходимо задать слишком*«out»*. 
* `platform`: свойство платформы hello указывает платформу уведомления hello целей уведомления. Должен быть hello следующие значения:
  * По умолчанию если выходных данных hello привязки указано свойство платформы hello шаблон уведомления может быть используется tootarget на любой платформе, настроенного на hello концентратор уведомлений Azure. Дополнительные сведения об использовании шаблонов в целом toosend кросс-уведомлений платформы с концентратор уведомлений Azure. в разделе [шаблоны](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns` — служба push-уведомлений Apple. Дополнительные сведения о настройке hello концентратора уведомлений для APNS и получение уведомления hello в клиентском приложении см. в разделе [tooiOS уведомления Принудительная отправка с концентраторами уведомлений Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm` — [Amazon Device Messaging](https://developer.amazon.com/device-messaging). Дополнительные сведения о настройке hello концентратора уведомлений для ADM и получение hello уведомления в приложении Kindle см. в разделе [Приступая к работе с концентраторами уведомлений для Kindle приложений](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm` — [Google Cloud Messaging](https://developers.google.com/cloud-messaging/). Firebase Cloud Messaging, являющийся hello новую версию GCM, также поддерживается. Дополнительные сведения о настройке hello концентратора уведомлений для GCM/FCM и получение hello уведомления в клиентское приложение для Android см. в разделе [tooAndroid уведомления Принудительная отправка с концентраторами уведомлений Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns` — [службы push-уведомлений Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) для различных платформ Windows. Службы WNS поддерживают также Windows Phone 8.1 и более поздние версии. Дополнительные сведения о настройке hello концентратора уведомлений для службы WNS и получение hello уведомления в приложении универсальной платформы Windows (UWP) см. в разделе [Приступая к работе с уведомления концентраторов для универсальной платформы приложений для Windows](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns` — [служба push-уведомлений Майкрософт](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx). Данная платформа поддерживает Windows Phone 8 и более ранние версии платформ Windows Phone. Дополнительные сведения о настройке hello концентратора уведомлений для MPNS и получение hello уведомления в приложения Windows Phone см. в разделе [Отправка push-уведомлений с концентраторами уведомлений Azure на Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

Пример файла function.json:

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a>Настройка строки подключения центра уведомлений
Привязка для вывода toouse концентратор уведомлений, необходимо настроить hello строку подключения для hello концентратора. Это можно сделать на hello *Интеграция* вкладку, выбрав концентратор уведомлений или создать новую. 

Можно также вручную добавить строку подключения для существующий концентратор, добавив строку подключения для hello *DefaultFullSharedAccessSignature* tooyour концентратора уведомлений. Эта строка подключения предоставляет доступ к функции разрешение toosend уведомляющих сообщений. Hello *DefaultFullSharedAccessSignature* значение строки подключения может осуществляться из hello **ключей** кнопку в главной колонке hello ресурса концентратора уведомлений в hello портал Azure. toomanually добавить строку подключения для вашего концентратора hello используйте следующие шаги: 

1. На hello **функции приложения** колонке hello портала Azure щелкните **параметрами приложения функции > Перейти параметры службы tooApp**.
2. В hello **параметры** колонка, щелкните **параметры приложения**.
3. Прокрутите вниз toohello **параметры приложения** раздела и Добавление именованного записи для *DefaultFullSharedAccessSignature* значения для центра уведомлений.
4. Ссылаться на строку имени параметра в hello привязок выходного приложения. Аналогичные слишком**MyHubConnectionString** используется в приведенном выше примере hello.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>Использование собственных уведомлений APNs с триггерами очереди на языке C#
В этом примере показано, как toouse типы, определенные в hello [библиотека концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend собственные уведомления APNS. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>Использование собственных уведомлений GCM с триггерами очереди на языке C#
В этом примере показано, как toouse типы, определенные в hello [библиотека концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend собственные уведомления GCM. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>Использование собственных уведомлений WNS с триггерами очереди на языке C#
В этом примере показано, как toouse типы, определенные в hello [библиотека концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend собственного WNS всплывающих уведомлений. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a>Пример шаблона для триггеров таймера на основе Node.js
В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего свойства `location` и `message`.

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a>Пример шаблона для триггеров таймера на языке F#
В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего свойства `location` и `message`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>Пример шаблона с параметром вывода
Этот пример отправляет уведомление [регистрацию шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) , содержащий `message` заполнителя в шаблоне hello.

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a>Пример шаблона с асинхронной функцией
При использовании асинхронного кода параметры вывода не допускаются. В этом случае использовать `IAsyncCollector` tooreturn создания шаблона уведомления. Hello ниже приведен пример асинхронной приведенного выше кода hello. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>Пример шаблона с использованием JSON
Этот пример отправляет уведомление [регистрацию шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) , содержащий `message` заполнитель в шаблон hello, используя допустимую строку JSON.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Пример шаблона, в котором используются типы из библиотеки центров уведомлений
В этом примере показано, как toouse типы, определенные в hello [библиотека концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

