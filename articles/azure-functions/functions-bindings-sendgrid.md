---
title: "Привязки SendGrid для Функций Azure"
description: "Справочник по привязкам SendGrid для службы \"Функции Azure\"."
services: functions
documentationcenter: na
author: tdykstra
manager: cfowler
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/29/2017
ms.author: tdykstra
ms.openlocfilehash: aa64bbc764fe96d7c15d62660114222458e5acf4
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/02/2018
---
# <a name="azure-functions-sendgrid-bindings"></a>Привязки SendGrid для Функций Azure

В этой статье объясняется, как отправить электронное сообщение с помощью привязок [SendGrid](https://sendgrid.com/docs/User_Guide/index.html) в службе "Функции Azure". Служба "Функции Azure" поддерживают выходную привязку для SendGrid.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="example"></a>Пример

Языковой пример см. в разделах:

* [C#](#c-example)
* [Скрипт C# (.csx)](#c-script-example)
* [JavaScript](#javascript-example)

### <a name="c-example"></a>Пример C#

В следующем примере показан [функции C#](functions-dotnet-class-library.md) , триггер использует очереди Service Bus и привязка для вывода SendGrid.

```cs
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid(ApiKey = "CustomSendGridKeyAppSettingName")] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string To { get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

Вы можете не задавать свойство атрибута `ApiKey` при наличии ключа API в настройка приложения с именем AzureWebJobsSendGridApiKey.

### <a name="c-script-example"></a>Пример сценария C#

В следующем примере показаны выходная привязка SendGrid в файле *function.json* и [функция сценария C#](functions-reference-csharp.md), которая использует эту привязку.

Данные привязки в файле *function.json*:

```json 
{
    "bindings": [
        {
            "name": "message",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

В разделе [Конфигурация](#configuration) описываются эти свойства.

Ниже приведен код скрипта C#.

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

### <a name="javascript-example"></a>Пример JavaScript

В следующем примере показаны выходная привязка SendGrid в файле *function.json* и [функция JavaScript](functions-reference-node.md), которая использует эту привязку.

Данные привязки в файле *function.json*:

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

В разделе [Конфигурация](#configuration) описываются эти свойства.

Ниже показан код JavaScript.

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: { email: "sender@contoso.com" },        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};
```

## <a name="attributes"></a>Атрибуты

В [библиотеки классов C#](functions-dotnet-class-library.md), используйте [SendGrid](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs) атрибут, который определен в пакет NuGet [Microsoft.Azure.WebJobs.Extensions.SendGrid](http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid).

Дополнительные сведения о настройке свойств атрибутов см. в разделе [Конфигурация](#configuration). Ниже приведен пример атрибута `SendGrid` в сигнатуре метода:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid(ApiKey = "CustomSendGridKeyAppSettingName")] out SendGridMessage message)
{
    ...
}
```

Полный пример см. в разделе [пример на C#](#c-example).

## <a name="configuration"></a>Параметр Configuration

В следующей таблице описываются свойства конфигурации привязки, которые задаются в файле *function.json* и атрибуте `SendGrid`.

|свойство function.json | Свойство атрибута |ОПИСАНИЕ|
|---------|---------|----------------------|
|**type**|| Обязательное. Необходимо задать значение `sendGrid`.|
|**direction**|| Обязательное. Необходимо задать значение `out`.|
|**name**|| Обязательное. Имя переменной, из которой в коде функции можно получить запрос или текст запроса. Это значение равно ```$return``` при наличии только одного возвращаемого значения. |
|**apiKey**|**apiKey**| Имя параметра приложения, в котором содержится ваш ключ API. Если значение не задано, имя параметра приложения по умолчанию AzureWebJobsSendGridApiKey.|
|**to**|**To**| Электронный адрес получателя. |
|**from**|**from**| Электронный адрес отправителя. |
|**subject**|**Тема**| Тема электронного сообщения. |
|**text**|**текст**| Содержимое электронного сообщения. |

[!INCLUDE [app settings to local.settings.json](../../includes/functions-app-settings-local.md)]

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Основные понятия триггеров и привязок в Функциях Azure](functions-triggers-bindings.md)