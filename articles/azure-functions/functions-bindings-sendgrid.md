---
title: "привязки функции SendGrid aaaAzure | Документы Microsoft"
description: "Справочник по привязкам SendGrid для Функций Azure."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Привязки SendGrid для Функций Azure

В этой статье объясняется, как tooconfigure и работать с привязками SendGrid в функциях Azure. С помощью SendGrid можно использовать функции Azure toosend настроить электронную программными средствами.

Эта статья содержит справочные сведения для разработчиков Функций Azure. Если вы новые функции tooAzure, начните с hello следующие ресурсы:

[Создание первой функции Azure](functions-create-first-azure-function.md). 
Справочники разработчика по [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) или [Node](functions-reference-node.md).

## <a name="functionjson-for-sendgrid-bindings"></a>Файл function.json для привязок SendGrid

Функции Azure предоставляют привязку для вывода для SendGrid. Hello SendGrid вывода привязка позволяет toocreate и отправить сообщение электронной почты программными средствами. 

Hello SendGrid привязка поддерживает hello следующие свойства:

- `name`— Обязательный - hello переменной имя, используемое в коде функция для запроса hello или текст запроса. Это значение равно ```$return``` при наличии только одного возвращаемого значения. 
- `type`— Обязательный - должен быть задан слишком «sendGrid.»
- `direction`— Обязательный - должно быть задано слишком «out».
- `apiKey`— Обязательный - должно быть именем toohello набор ваш ключ API, хранящихся в параметрах приложения hello функции приложения.
- `to`: hello адрес электронной почты получателя.
- `from`: hello адрес электронной почты отправителя.
- `subject`: hello субъекта hello электронной почты.
- `text`: hello содержимое электронной почты.

Ниже приведен пример файла **function.json**.

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

> [!NOTE]
> Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями. Это обеспечивает защиту конфиденциальной информации.
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a>Привязка для вывода C# пример hello SendGrid

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
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

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Пример узла hello SendGrid вывода привязки

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других привязках и триггерах для Функций Azure доступны в следующих разделах: 
- [Справочник разработчика по триггерам и привязкам в Функциях Azure](functions-triggers-bindings.md)

- [Советы и рекомендации для функций Azure](functions-best-practices.md) приведены некоторые советы и рекомендации toouse при создании функций Azure.

- [Руководство для разработчиков по Функциям Azure](functions-reference.md). Справочник программиста по созданию функций, а также определению триггеров и привязок.
