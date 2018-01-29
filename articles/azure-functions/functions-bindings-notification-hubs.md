---
title: "Привязки Центров уведомлений для службы \"Функции Azure\""
description: "Узнайте, как использовать привязки центра уведомлений Azure в функциях Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/21/2017
ms.author: glenga
ms.openlocfilehash: cbc22721bbe06fdc5a8a9026b113071e1616bcb8
ms.sourcegitcommit: 2e540e6acb953b1294d364f70aee73deaf047441
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2018
---
# <a name="notification-hubs-output-binding-for-azure-functions"></a>Выходная привязка Центра уведомлений для службы "Функции Azure"

Эта статья объясняет, как отправлять push-уведомления с помощью привязок [Центров уведомлений](../notification-hubs/notification-hubs-push-notification-overview.md) Azure в службе "Функции Azure". Служба "Функции Azure" поддерживает выходные привязки для Центров уведомлений.

Центры уведомлений нужно настроить для служб уведомлений платформы (PNS), которые необходимо использовать. Сведения о том, как получать push-уведомления в клиентское приложение из Центров уведомлений, см. в статье [Начало работы с Центрами уведомлений для приложений универсальной платформы Windows](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md). Вы также можете выбрать целевую клиентскую платформу из раскрывающегося списка в верхней части страницы.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="example---template"></a>Пример шаблона

Можно отправлять собственные или [шаблонные](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) уведомления. Собственные уведомления нацелены на определенную клиентскую платформу, указанную в свойстве `platform` привязки для вывода. Шаблонное уведомление можно использовать для нескольких платформ.   

Языковой пример см. в разделах:

* [Пример шаблона сценария C# — параметр вывода](#c-script-template-example---out-parameter)
* [Пример шаблона сценария C# — асинхронный](#c-script-template-example---asynchronous)
* [Пример шаблона сценария C# — JSON](#c-script-template-example---json)
* [Пример шаблона сценария C# — типы библиотек](#c-script-template-example---library-types)
* [F#](#f-template-example)
* [JavaScript](#javascript-template-example)

### <a name="c-script-template-example---out-parameter"></a>Пример шаблона сценария C# — параметр вывода

В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего заполнитель `message`.

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

### <a name="c-script-template-example---asynchronous"></a>Пример шаблона сценария C# — асинхронный

При использовании асинхронного кода параметры вывода не допускаются. В этом случае для возвращения шаблонного уведомления следует использовать `IAsyncCollector`. Ниже приведен пример асинхронного кода, описанного выше. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

### <a name="c-script-template-example---json"></a>Пример шаблона сценария C# — JSON

В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего заполнитель `message` и использующего допустимую строку JSON.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

### <a name="c-script-template-example---library-types"></a>Пример шаблона сценария C# — типы библиотек

В этом примере показано, как использовать типы, определенные в [библиотеке центров уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

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

### <a name="f-template-example"></a>Пример шаблона F#

В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего свойства `location` и `message`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

### <a name="javascript-template-example"></a>Пример шаблона JavaScript

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

## <a name="example---apns-native"></a>Пример — собственный APNS

В этом примере сценария C# показано, как отправлять собственные уведомления APNS. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="example---gcm-native"></a>Пример — собственный GCM

В этом примере сценария C# показано, как отправлять собственные уведомления GCM. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="example---wns-native"></a>Пример — собственный WNS

В этом примере сценария C# показано, как использовать типы, определенные в [библиотеке центров уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/), для отправки всплывающего уведомления WNS. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
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
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="attributes"></a>Атрибуты

В [библиотеки классов C#](functions-dotnet-class-library.md), используйте [концентратора уведомлений](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) атрибут, который определен в пакет NuGet [Microsoft.Azure.WebJobs.Extensions.NotificationHubs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs).

Параметры конструктора атрибута и его свойства описаны в разделе [конфигурации](#configuration).

## <a name="configuration"></a>Параметр Configuration

В следующей таблице описываются свойства конфигурации привязки, которые задаются в файле *function.json* и атрибуте `NotificationHub`:

|свойство function.json | Свойство атрибута |ОПИСАНИЕ|
|---------|---------|----------------------|
|**type** |Недоступно| Для этого свойства следует задать значение notificationHub. |
|**direction** |Недоступно| Для этого свойства необходимо задать значение out. | 
|**name** |Недоступно| Имя переменной, используемой в коде функции для сообщения Центра уведомлений. |
|**tagExpression** |**TagExpression** | Выражения тегов позволяют указать, что уведомления должны отправляться на устройства, зарегистрированные для получения уведомлений, соответствующих выражению тега.  Дополнительные сведения см. в статье [Маршрутизация и выражения тегов](../notification-hubs/notification-hubs-tags-segment-push-message.md). |
|**hubName** | **HubName** | Имя ресурса Центра уведомлений на портале Azure. |
|**подключение** | **ConnectionStringSetting** | Имя параметра приложения, содержащего строку подключения Центров уведомлений.  Для нее необходимо задать значение *DefaultFullSharedAccessSignature* для Центра уведомлений. Ознакомьтесь с разделом [Настройка строки подключения](#connection-string-setup) далее в этой статье.|
|**platform** | **Платформа** | Свойство platform указывает целевую клиентскую платформу для ваших уведомлений. По умолчанию, если свойство платформы отсутствует в выходной привязке, шаблонные уведомления могут использоваться для любой платформы, настроенной в концентраторе уведомлений Azure. Дополнительные общие сведения об использовании шаблонов для отправки кроссплатформенных уведомлений с помощью центра уведомлений Azure см. в разделе [Шаблоны](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md). Если свойство **platform** задано, оно должно иметь одно из следующих значений: <ul><li><code>apns</code>&mdash; — Cлужба push-уведомлений Apple. Дополнительные сведения о настройке Центра уведомлений для APNs и получении уведомлений в клиентском приложении см. в статье [Отправка push-уведомлений с помощью Центра уведомлений Azure в iOS](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md).</li><li><code>adm</code>&mdash; — [Amazon Device Messaging](https://developer.amazon.com/device-messaging). Дополнительные сведения о настройке Центра уведомлений для ADM и получении уведомлений в приложении Kindle см. в статье [Приступая к работе с Центрами уведомлений для приложений Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md).</li><li><code>gcm</code>&mdash; — [Google Cloud Messaging](https://developers.google.com/cloud-messaging/). Также поддерживается новая версия GCM, Firebase Cloud Messaging. Дополнительные сведения см. в статье [Отправка push-уведомлений в приложения Android с помощью Центра уведомлений Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md).</li><li><code>wns</code>&mdash; — [службы Microsoft SQL Server Notification Services](https://msdn.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) для различных платформ Windows. Службы WNS поддерживают также Windows Phone 8.1 и более поздние версии. Дополнительные сведения см. в статье [Начало работы с Центрами уведомлений для приложений универсальной платформы Windows](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</li><li><code>mpns</code>&mdash; — [служба push-уведомлений (Майкрософт)](https://msdn.microsoft.com/library/windows/apps/ff402558.aspx). Данная платформа поддерживает Windows Phone 8 и более ранние версии платформ Windows Phone. Дополнительные сведения см. в статье [Отправка push-уведомлений в приложения Windows Phone с помощью Центров уведомлений Azure](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md).</li></ul> |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

### <a name="functionjson-file-example"></a>Пример файла function.json

Ниже приведен пример привязки Центров уведомлений в файле *function.json*.

```json
{
  "bindings": [
    {
      "type": "notificationHub",
      "direction": "out",
      "name": "notification",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm"
    }
  ],
  "disabled": false
}
```

### <a name="connection-string-setup"></a>Настройка строки подключения

Для использования привязки для вывода Центра уведомлений необходимо настроить отдельную строку подключения. На портале Azure вы можете выбрать имеющийся Центр уведомлений или создать новый на вкладке *Интегрировать*. Кроме того, строку подключения можно настроить вручную. 

Настройка строки подключения к имеющемуся Центру уведомлений

1. Перейдите к Центру уведомлений на [портале Azure](https://portal.azure.com). Выберите **Политики доступа**, а затем нажмите кнопку копирования рядом с политикой **DefaultFullSharedAccessSignature**. Это позволит скопировать строку подключения политики *DefaultFullSharedAccessSignature* к вашему Центру уведомлений. Эта строка подключения позволяет функции отправлять сообщения центру уведомлений.
    ![Копирование строки подключения к Центру уведомлений](./media/functions-bindings-notification-hubs/get-notification-hub-connection.png)
1. Перейдите к приложению-функции на портале Azure. Выберите **Параметры приложения**, добавьте ключ, например **MyHubConnectionString**, вставьте скопированную строку подключения политики *DefaultFullSharedAccessSignature* к Центру уведомлений как значение, а затем нажмите кнопку **Сохранить**.

Имя параметра приложения такое же, как и параметра подключения выходной привязки в файле *function.json* или атрибуте .NET. Ознакомьтесь с [разделом конфигурации](#configuration) в этой статье.

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Основные понятия триггеров и привязок в Функциях Azure](functions-triggers-bindings.md)

