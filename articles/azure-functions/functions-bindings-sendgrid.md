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
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="92bba-103">Привязки SendGrid для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="92bba-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="92bba-104">В этой статье объясняется, как tooconfigure и работать с привязками SendGrid в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="92bba-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="92bba-105">С помощью SendGrid можно использовать функции Azure toosend настроить электронную программными средствами.</span><span class="sxs-lookup"><span data-stu-id="92bba-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="92bba-106">Эта статья содержит справочные сведения для разработчиков Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="92bba-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="92bba-107">Если вы новые функции tooAzure, начните с hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="92bba-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="92bba-108">[Создание первой функции Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="92bba-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="92bba-109">Справочники разработчика по [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) или [Node](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="92bba-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="92bba-110">Файл function.json для привязок SendGrid</span><span class="sxs-lookup"><span data-stu-id="92bba-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="92bba-111">Функции Azure предоставляют привязку для вывода для SendGrid.</span><span class="sxs-lookup"><span data-stu-id="92bba-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="92bba-112">Hello SendGrid вывода привязка позволяет toocreate и отправить сообщение электронной почты программными средствами.</span><span class="sxs-lookup"><span data-stu-id="92bba-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="92bba-113">Hello SendGrid привязка поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="92bba-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="92bba-114">`name`— Обязательный - hello переменной имя, используемое в коде функция для запроса hello или текст запроса.</span><span class="sxs-lookup"><span data-stu-id="92bba-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="92bba-115">Это значение равно ```$return``` при наличии только одного возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="92bba-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="92bba-116">`type`— Обязательный - должен быть задан слишком «sendGrid.»</span><span class="sxs-lookup"><span data-stu-id="92bba-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="92bba-117">`direction`— Обязательный - должно быть задано слишком «out».</span><span class="sxs-lookup"><span data-stu-id="92bba-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="92bba-118">`apiKey`— Обязательный - должно быть именем toohello набор ваш ключ API, хранящихся в параметрах приложения hello функции приложения.</span><span class="sxs-lookup"><span data-stu-id="92bba-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="92bba-119">`to`: hello адрес электронной почты получателя.</span><span class="sxs-lookup"><span data-stu-id="92bba-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="92bba-120">`from`: hello адрес электронной почты отправителя.</span><span class="sxs-lookup"><span data-stu-id="92bba-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="92bba-121">`subject`: hello субъекта hello электронной почты.</span><span class="sxs-lookup"><span data-stu-id="92bba-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="92bba-122">`text`: hello содержимое электронной почты.</span><span class="sxs-lookup"><span data-stu-id="92bba-122">`text` : hello email content.</span></span>

<span data-ttu-id="92bba-123">Ниже приведен пример файла **function.json**.</span><span class="sxs-lookup"><span data-stu-id="92bba-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="92bba-124">Функции Azure хранят сведения о подключении и ключи API в качестве параметров приложения, чтобы они не возвращались в репозиторий системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="92bba-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="92bba-125">Это обеспечивает защиту конфиденциальной информации.</span><span class="sxs-lookup"><span data-stu-id="92bba-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="92bba-126">Привязка для вывода C# пример hello SendGrid</span><span class="sxs-lookup"><span data-stu-id="92bba-126">C# example of hello SendGrid output binding</span></span>

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="92bba-127">Пример узла hello SendGrid вывода привязки</span><span class="sxs-lookup"><span data-stu-id="92bba-127">Node example of hello SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="92bba-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="92bba-128">Next steps</span></span>
<span data-ttu-id="92bba-129">Сведения о других привязках и триггерах для Функций Azure доступны в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="92bba-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="92bba-130">Справочник разработчика по триггерам и привязкам в Функциях Azure</span><span class="sxs-lookup"><span data-stu-id="92bba-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="92bba-131">[Советы и рекомендации для функций Azure](functions-best-practices.md) приведены некоторые советы и рекомендации toouse при создании функций Azure.</span><span class="sxs-lookup"><span data-stu-id="92bba-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="92bba-132">[Руководство для разработчиков по Функциям Azure](functions-reference.md). Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="92bba-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
