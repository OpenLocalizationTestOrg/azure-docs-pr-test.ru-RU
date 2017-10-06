---
title: "триггер таймера функции aaaAzure | Документы Microsoft"
description: "Понять, как триггеры toouse таймера в функциях Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="1c208-104">Триггеры с таймерами в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="1c208-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="1c208-105">В этой статье объясняется, как триггеры таймера tooconfigure и код в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="1c208-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="1c208-106">Функции Azure поддерживают привязку триггеров к таймерам, благодаря чему вы можете выполнять код функции по определенному расписанию.</span><span class="sxs-lookup"><span data-stu-id="1c208-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="1c208-107">триггер таймера Hello поддерживает масштабирование нескольких экземпляров. Один экземпляр функции конкретного таймера выполняется для всех экземпляров.</span><span class="sxs-lookup"><span data-stu-id="1c208-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="1c208-108">Триггер таймера</span><span class="sxs-lookup"><span data-stu-id="1c208-108">Timer trigger</span></span>
<span data-ttu-id="1c208-109">Hello таймера триггер tooa функция использует следующий объект JSON в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="1c208-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="1c208-110">Здравствуйте, значение `schedule` — [выражение CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) , включающего следующих шести полей:</span><span class="sxs-lookup"><span data-stu-id="1c208-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="1c208-111">Многие выражения cron hello, можно найти в документации по опустить hello `{second}` поля.</span><span class="sxs-lookup"><span data-stu-id="1c208-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="1c208-112">При копировании из одной из них требуется tooadjust для дополнительных hello `{second}` поля.</span><span class="sxs-lookup"><span data-stu-id="1c208-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="1c208-113">Конкретные примеры см. в разделе [Примеры расписания](#examples) ниже.</span><span class="sxs-lookup"><span data-stu-id="1c208-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="1c208-114">При использовании выражения CRON hello часовой пояс по умолчанию Hello — по Гринвичу (UTC).</span><span class="sxs-lookup"><span data-stu-id="1c208-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="1c208-115">toohave на основе CRON-выражение в другом часовом поясе, создайте новый параметр приложения для приложения с именем функции `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="1c208-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="1c208-116">Набор значение hello toohello имя hello требуемого часового пояса, как показано в hello [индекс часовой пояс Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c208-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="1c208-117">Например, *восточное поясное время* — UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="1c208-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="1c208-118">toohave таймера запускать срабатывают в 10:00 центральноевропейское время каждый день, используйте hello, следующее выражение CRON, учетные записи для часового пояса UTC.</span><span class="sxs-lookup"><span data-stu-id="1c208-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="1c208-119">Кроме того, можно добавить новый параметр приложения для приложения с именем функции `WEBSITE_TIME_ZONE` и задайте значение hello слишком**Восточное время**.</span><span class="sxs-lookup"><span data-stu-id="1c208-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="1c208-120">Далее можно использовать следующее выражение CRON hello для 10:00 по стандартному восточному времени:</span><span class="sxs-lookup"><span data-stu-id="1c208-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="1c208-121">Примеры расписания</span><span class="sxs-lookup"><span data-stu-id="1c208-121">Schedule examples</span></span>
<span data-ttu-id="1c208-122">Ниже приведены некоторые образцы выражений CRON, можно использовать для hello `schedule` свойство.</span><span class="sxs-lookup"><span data-stu-id="1c208-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="1c208-123">tootrigger каждые пять минут:</span><span class="sxs-lookup"><span data-stu-id="1c208-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="1c208-124">tootrigger один раз в начале hello каждый час:</span><span class="sxs-lookup"><span data-stu-id="1c208-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="1c208-125">tootrigger каждые 2 часа:</span><span class="sxs-lookup"><span data-stu-id="1c208-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="1c208-126">tootrigger один раз в час из too5 9: 00 PM:</span><span class="sxs-lookup"><span data-stu-id="1c208-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="1c208-127">tootrigger в 9:30:00 каждый день:</span><span class="sxs-lookup"><span data-stu-id="1c208-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="1c208-128">tootrigger в 9:30:00 каждый день недели:</span><span class="sxs-lookup"><span data-stu-id="1c208-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="1c208-129">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="1c208-129">Trigger usage</span></span>
<span data-ttu-id="1c208-130">При вызове функции триггер таймера hello [объект таймера](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) передается в функцию hello.</span><span class="sxs-lookup"><span data-stu-id="1c208-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="1c208-131">Hello следующий JSON является представлением пример hello объекта таймера.</span><span class="sxs-lookup"><span data-stu-id="1c208-131">hello following JSON is an example representation of hello timer object.</span></span> 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="1c208-132">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="1c208-132">Trigger sample</span></span>
<span data-ttu-id="1c208-133">Предположим, что имеется следующий триггер таймера в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="1c208-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="1c208-134">См. пример hello зависящие от языка, который считывает таймера hello объекта toosee ли выполняется позднее.</span><span class="sxs-lookup"><span data-stu-id="1c208-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="1c208-135">C#</span><span class="sxs-lookup"><span data-stu-id="1c208-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="1c208-136">F#</span><span class="sxs-lookup"><span data-stu-id="1c208-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="1c208-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="1c208-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="1c208-138">Пример триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="1c208-138">Trigger sample in C#</span></span> #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="1c208-139">Пример триггера на языке F#</span><span class="sxs-lookup"><span data-stu-id="1c208-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="1c208-140">Пример триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="1c208-140">Trigger sample in Node.js</span></span>
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="1c208-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c208-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

