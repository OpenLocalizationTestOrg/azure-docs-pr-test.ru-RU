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
# <a name="azure-functions-timer-trigger"></a>Триггеры с таймерами в функциях Azure

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

В этой статье объясняется, как триггеры таймера tooconfigure и код в функциях Azure. Функции Azure поддерживают привязку триггеров к таймерам, благодаря чему вы можете выполнять код функции по определенному расписанию. 

триггер таймера Hello поддерживает масштабирование нескольких экземпляров. Один экземпляр функции конкретного таймера выполняется для всех экземпляров.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>Триггер таймера
Hello таймера триггер tooa функция использует следующий объект JSON в hello hello `bindings` массив function.json:

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

Здравствуйте, значение `schedule` — [выражение CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) , включающего следующих шести полей: 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>Многие выражения cron hello, можно найти в документации по опустить hello `{second}` поля. При копировании из одной из них требуется tooadjust для дополнительных hello `{second}` поля. Конкретные примеры см. в разделе [Примеры расписания](#examples) ниже.

При использовании выражения CRON hello часовой пояс по умолчанию Hello — по Гринвичу (UTC). toohave на основе CRON-выражение в другом часовом поясе, создайте новый параметр приложения для приложения с именем функции `WEBSITE_TIME_ZONE`. Набор значение hello toohello имя hello требуемого часового пояса, как показано в hello [индекс часовой пояс Microsoft](https://msdn.microsoft.com/library/ms912391.aspx). 

Например, *восточное поясное время* — UTC-05:00. toohave таймера запускать срабатывают в 10:00 центральноевропейское время каждый день, используйте hello, следующее выражение CRON, учетные записи для часового пояса UTC.

```json
"schedule": "0 0 15 * * *",
``` 

Кроме того, можно добавить новый параметр приложения для приложения с именем функции `WEBSITE_TIME_ZONE` и задайте значение hello слишком**Восточное время**.  Далее можно использовать следующее выражение CRON hello для 10:00 по стандартному восточному времени: 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>Примеры расписания
Ниже приведены некоторые образцы выражений CRON, можно использовать для hello `schedule` свойство. 

tootrigger каждые пять минут:

```json
"schedule": "0 */5 * * * *"
```

tootrigger один раз в начале hello каждый час:

```json
"schedule": "0 0 * * * *",
```

tootrigger каждые 2 часа:

```json
"schedule": "0 0 */2 * * *",
```

tootrigger один раз в час из too5 9: 00 PM:

```json
"schedule": "0 0 9-17 * * *",
```

tootrigger в 9:30:00 каждый день:

```json
"schedule": "0 30 9 * * *",
```

tootrigger в 9:30:00 каждый день недели:

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>Использование триггера
При вызове функции триггер таймера hello [объект таймера](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) передается в функцию hello. Hello следующий JSON является представлением пример hello объекта таймера. 

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

## <a name="trigger-sample"></a>Пример триггера
Предположим, что имеется следующий триггер таймера в hello hello `bindings` массив function.json:

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

См. пример hello зависящие от языка, который считывает таймера hello объекта toosee ли выполняется позднее.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Пример триггера на языке C# #
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

### <a name="trigger-sample-in-f"></a>Пример триггера на языке F# #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Пример триггера для Node.js
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

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

