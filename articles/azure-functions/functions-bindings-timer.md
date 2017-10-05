---
title: "Триггеры с таймерами | Документация Майкрософт"
description: "Узнайте, как использовать триггеры с таймерами в функциях Azure."
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
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="be62b-104">Триггеры с таймерами в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="be62b-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="be62b-105">В этой статье описывается настройка и программирование триггеров с таймерами в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="be62b-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="be62b-106">Функции Azure поддерживают привязку триггеров к таймерам, благодаря чему вы можете выполнять код функции по определенному расписанию.</span><span class="sxs-lookup"><span data-stu-id="be62b-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="be62b-107">Триггер с таймером поддерживает развертывание с несколькими экземплярами. Один экземпляр функции конкретного таймера выполняется для всех экземпляров.</span><span class="sxs-lookup"><span data-stu-id="be62b-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="be62b-108">Триггер таймера</span><span class="sxs-lookup"><span data-stu-id="be62b-108">Timer trigger</span></span>
<span data-ttu-id="be62b-109">Триггер с таймером для функции использует следующий объект JSON в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="be62b-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="be62b-110">Значение `schedule` представляет собой [выражение CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) с шестью полями:</span><span class="sxs-lookup"><span data-stu-id="be62b-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="be62b-111">Во многих выражениях CRON в сети отсутствует поле `{second}`.</span><span class="sxs-lookup"><span data-stu-id="be62b-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="be62b-112">Поэтому если скопировать текст в одном из таких выражений, понадобится добавить дополнительное поле `{second}`.</span><span class="sxs-lookup"><span data-stu-id="be62b-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="be62b-113">Конкретные примеры см. в разделе [Примеры расписания](#examples) ниже.</span><span class="sxs-lookup"><span data-stu-id="be62b-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="be62b-114">Часовой пояс по умолчанию, используемый с выражениями CRON — время в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="be62b-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="be62b-115">Если нужно использовать другой часовой пояс в выражении CRON, создайте новый параметр приложения с именем `WEBSITE_TIME_ZONE` для приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="be62b-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="be62b-116">В качестве значения задайте имя нужного часового пояса, как показано в статье [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx) (Индексы часовых поясов Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="be62b-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="be62b-117">Например, *восточное поясное время* — UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="be62b-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="be62b-118">Если требуется, чтобы триггер с таймером активировался в 10:00 по восточному поясному времени каждый день, можно использовать следующее выражение CRON, в котором учитывается часовой пояс UTC:</span><span class="sxs-lookup"><span data-stu-id="be62b-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="be62b-119">Кроме того, можно добавить новый параметр приложения с именем `WEBSITE_TIME_ZONE` для приложения-функции и задать **Восточное поясное время** в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="be62b-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="be62b-120">Затем можно использовать следующее выражение CRON для 10:00 по восточному поясному времени:</span><span class="sxs-lookup"><span data-stu-id="be62b-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="be62b-121">Примеры расписания</span><span class="sxs-lookup"><span data-stu-id="be62b-121">Schedule examples</span></span>
<span data-ttu-id="be62b-122">Ниже приведены некоторые примеры выражений CRON, которые можно использовать для свойства `schedule`.</span><span class="sxs-lookup"><span data-stu-id="be62b-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="be62b-123">Активация через каждые пять минут:</span><span class="sxs-lookup"><span data-stu-id="be62b-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="be62b-124">Активация через каждый час:</span><span class="sxs-lookup"><span data-stu-id="be62b-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="be62b-125">Активация через каждые 2 часа.</span><span class="sxs-lookup"><span data-stu-id="be62b-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="be62b-126">Активация каждый час с 9:00 до 17:00:</span><span class="sxs-lookup"><span data-stu-id="be62b-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="be62b-127">Активация в 9:30 каждый день:</span><span class="sxs-lookup"><span data-stu-id="be62b-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="be62b-128">Активация в 9:30 каждый будний день:</span><span class="sxs-lookup"><span data-stu-id="be62b-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="be62b-129">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="be62b-129">Trigger usage</span></span>
<span data-ttu-id="be62b-130">При вызове функции триггера с таймером [объект таймера](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) передается в функцию.</span><span class="sxs-lookup"><span data-stu-id="be62b-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="be62b-131">Далее представлен JSON в качестве примера объекта таймера.</span><span class="sxs-lookup"><span data-stu-id="be62b-131">The following JSON is an example representation of the timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="be62b-132">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="be62b-132">Trigger sample</span></span>
<span data-ttu-id="be62b-133">Предположим, что у вас есть следующий триггер с таймером в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="be62b-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="be62b-134">Ознакомьтесь с примером для конкретного языка, считывающим объект таймера, чтобы определить, опаздывает ли он.</span><span class="sxs-lookup"><span data-stu-id="be62b-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="be62b-135">C#</span><span class="sxs-lookup"><span data-stu-id="be62b-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="be62b-136">F#</span><span class="sxs-lookup"><span data-stu-id="be62b-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="be62b-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="be62b-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="be62b-138">Пример триггера на языке C#</span><span class="sxs-lookup"><span data-stu-id="be62b-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="be62b-139">Пример триггера на языке F#</span><span class="sxs-lookup"><span data-stu-id="be62b-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="be62b-140">Пример триггера для Node.js</span><span class="sxs-lookup"><span data-stu-id="be62b-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="be62b-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be62b-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

