---
title: "Привязки SendGrid для Функций Azure | Документация Майкрософт"
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
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="ee11e-103">Привязки SendGrid для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="ee11e-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="ee11e-104">В этой статье объясняется, как настроить и использовать привязки SendGrid в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="ee11e-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="ee11e-105">С помощью SendGrid можно использовать Функции Azure для программной отправки настраиваемой электронной почты.</span><span class="sxs-lookup"><span data-stu-id="ee11e-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="ee11e-106">Эта статья содержит справочные сведения для разработчиков Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="ee11e-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="ee11e-107">Если вы новичок в функциях Azure, начните со следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="ee11e-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="ee11e-108">[Создание первой функции Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="ee11e-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="ee11e-109">Справочники разработчика по [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) или [Node](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="ee11e-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="ee11e-110">Файл function.json для привязок SendGrid</span><span class="sxs-lookup"><span data-stu-id="ee11e-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="ee11e-111">Функции Azure предоставляют привязку для вывода для SendGrid.</span><span class="sxs-lookup"><span data-stu-id="ee11e-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="ee11e-112">Привязка для вывода SendGrid дает возможность программно создавать и отправлять электронные сообщения.</span><span class="sxs-lookup"><span data-stu-id="ee11e-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="ee11e-113">Привязка SendGrid поддерживает перечисленные ниже свойства.</span><span class="sxs-lookup"><span data-stu-id="ee11e-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="ee11e-114">`name` (обязательное) — имя переменной, из которой в коде функции можно получить запрос или текст запроса.</span><span class="sxs-lookup"><span data-stu-id="ee11e-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="ee11e-115">Это значение равно ```$return``` при наличии только одного возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="ee11e-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="ee11e-116">`type` (обязательное) — для этого свойства нужно задать значение SendGrid.</span><span class="sxs-lookup"><span data-stu-id="ee11e-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="ee11e-117">`direction` (обязательное) — для этого свойства нужно задать значение out.</span><span class="sxs-lookup"><span data-stu-id="ee11e-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="ee11e-118">`apiKey` (обязательное) — для этого свойства нужно задать имя ключа API, сохраненное в параметрах приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="ee11e-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="ee11e-119">`to` — электронный адрес получателя.</span><span class="sxs-lookup"><span data-stu-id="ee11e-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="ee11e-120">`from` — электронный адрес отправителя.</span><span class="sxs-lookup"><span data-stu-id="ee11e-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="ee11e-121">`subject` — тема электронного сообщения.</span><span class="sxs-lookup"><span data-stu-id="ee11e-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="ee11e-122">`text` — содержимое электронного сообщения.</span><span class="sxs-lookup"><span data-stu-id="ee11e-122">`text` : the email content.</span></span>

<span data-ttu-id="ee11e-123">Ниже приведен пример файла **function.json**.</span><span class="sxs-lookup"><span data-stu-id="ee11e-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="ee11e-124">Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="ee11e-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="ee11e-125">Это обеспечивает защиту конфиденциальной информации.</span><span class="sxs-lookup"><span data-stu-id="ee11e-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="ee11e-126">Пример привязки для вывода SendGrid на C#</span><span class="sxs-lookup"><span data-stu-id="ee11e-126">C# example of the SendGrid output binding</span></span>

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

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="ee11e-127">Пример привязки для вывода SendGrid на Node</span><span class="sxs-lookup"><span data-stu-id="ee11e-127">Node example of the SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ee11e-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee11e-128">Next steps</span></span>
<span data-ttu-id="ee11e-129">Сведения о других привязках и триггерах для Функций Azure доступны в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="ee11e-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="ee11e-130">Справочник разработчика по триггерам и привязкам в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="ee11e-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="ee11e-131">[Рекомендации по Функциям Azure](functions-best-practices.md). Некоторые рекомендации по созданию функций Azure.</span><span class="sxs-lookup"><span data-stu-id="ee11e-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="ee11e-132">[Руководство для разработчиков по Функциям Azure](functions-reference.md). Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="ee11e-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
