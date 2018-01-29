---
title: "Управление экземплярами в устойчивых функциях (Azure)"
description: "Сведения о том, как управлять экземплярами в расширении устойчивых функций для Функций Azure."
services: functions
author: cgillum
manager: cfowler
editor: 
tags: 
keywords: 
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: cbf7731c0faa82ebd3e662eb6d2a8fb0acd65c97
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="manage-instances-in-durable-functions-azure-functions"></a>Управление экземплярами в устойчивых функциях (Функции Azure)

Экземпляры оркестрации [устойчивых функций](durable-functions-overview.md) можно запускать и завершать, а также отправлять в них запросы и события уведомления. Все операции управления экземпляром осуществляются с помощью [привязки клиента оркестрации](durable-functions-bindings.md). В этой статье подробно описаны все операции по управлению экземплярами.

## <a name="starting-instances"></a>Запуск экземпляров

Метод [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_) из класса [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) запускает новый экземпляр функции оркестратора. Экземпляры этого класса можно получить с помощью привязки `orchestrationClient`. На внутреннем уровне этот метод ставит в очередь управления сообщение, которое инициирует запуск функции с заданным именем и привязкой к триггеру `orchestrationTrigger`.

Параметры для [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_) , как показано ниже:

* **Name.** Имя функции оркестратора, для которой назначается запуск.
* **Input.** Любые данные, сериализуемые в формат JSON, которые нужно передать как входные данные для функции оркестратора.
* **InstanceId.** Уникальный идентификатор экземпляра (необязательно). Если идентификатор экземпляра не указан, ему будет присвоено случайное значение.

Ниже приведен простой пример на C#.

```csharp
[FunctionName("HelloWorldManualStart")]
public static Task Run(
    [ManualTrigger] string input,
    [OrchestrationClient] DurableOrchestrationClient starter,
    TraceWriter log)
{
    string instanceId = starter.StartNewAsync("HelloWorld", input);
    log.Info($"Started orchestration with ID = '{instanceId}'.");
}
```

В языках, отличных от .NET, также можно использовать привязку к выходным данным функции для запуска новых экземпляров. В этом случае можно применить любой объект, сериализуемый в формат JSON, с тремя указанными выше параметрами в качестве полей. Например, рассмотрим следующую функцию Node.js:

```js
module.exports = function (context, input) {
    var id = generateSomeUniqueId();
    context.bindings.starter = [{
        FunctionName: "HelloWorld",
        Input: input,
        InstanceId: id
    }];

    context.done(null);
};
```

> [!NOTE]
> Рекомендуем использовать случайный идентификатор экземпляра. Это помогает более равномерно распределять нагрузку при масштабировании функций оркестратора между несколькими виртуальными машинами. Указывать конкретные идентификаторы экземпляров имеет смысл в том случае, когда они должны поступать из внешнего источника, а также при реализации схемы [одноэлементного оркестратора](durable-functions-singletons.md).

## <a name="querying-instances"></a>Запросы к экземплярам

Метод [GetStatusAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_GetStatusAsync_) из класса [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) подает запрос на сведения о состоянии экземпляра оркестрации. Он принимает параметр `instanceId` и возвращает объект со следующими свойствами:

* **Name.** Имя функции оркестратора.
* **InstanceId.** Идентификатор экземпляра оркестрации (будет совпадать с переданным значением `instanceId`).
* **CreatedTime.** Время создания, то есть время начала выполнения функции оркестратора.
* **LastUpdatedTime.** Время прохождения последней контрольной точки оркестрации.
* **Input.** Входные данные функции в формате JSON.
* **Output.** Выходные данные функции в формате JSON (если выполнение функции успешно завершено). Если выполнение функции оркестратора завершилась сбоем, это свойство содержит сведения об ошибке. Если функция оркестратора была прервана, это свойство содержит сведения о причине завершения (при их наличии).
* **RuntimeStatus.** Состояние выполнения может иметь одно из следующих значений:
    * **Running.** Началось выполнение экземпляра.
    * **Completed.** Выполнение экземпляра завершилось в обычном режиме.
    * **ContinuedAsNew.** Экземпляр выполнил перезапуск с очисткой журнала выполнения. Это переходное состояние.
    * **Failed.** Выполнение экземпляра завершилось ошибкой.
    * **Terminated.** Выполнение экземпляра прервано.
    
Этот метод возвращает `null`, если экземпляр не существует или его выполнение еще не начато.

```csharp
[FunctionName("GetStatus")]
public static async Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    var status = await client.GetStatusAsync(instanceId);
    // do something based on the current status.
}
```

> [!NOTE]
> Экземпляр запроса является в настоящее время поддерживается только для функции orchestrator C#.

## <a name="terminating-instances"></a>Прерывание выполнения экземпляров

Выполнение запущенного экземпляра можно прервать с помощью метода [TerminateAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_) из класса [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html). Он принимает два параметра: `instanceId` и строку `reason`, которая сохраняется в журнале выполнения и в сведениях о состоянии экземпляра. Выполнение экземпляра прекращается по достижении очередной точки ожидания (`await`). Если он уже находится в состоянии ожидания (`await`), выполнение прекращается немедленно.

```csharp
[FunctionName("TerminateInstance")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    string reason = "It was time to be done.";
    return client.TerminateAsync(instanceId, reason);
}
```

> [!NOTE]
> Завершение экземпляра в данный момент поддерживается только для функции orchestrator C#.

## <a name="sending-events-to-instances"></a>Отправка событий в экземпляры

В выполняющиеся экземпляры можно отсылать уведомления о событиях с помощью метода [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_) из класса [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html). Чтобы обрабатывать эти уведомления, экземпляр должен ожидать вызова при помощи функции [WaitForExternalEvent](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_WaitForExternalEvent_). 

Параметры для [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_) , как показано ниже:

* **InstanceId** — уникальный идентификатор экземпляра;
* **EventName** — имя отправляемого события;
* **EventData** — данные полезной нагрузки в формате JSON, отправляемые в экземпляр.

```csharp
#r "Microsoft.Azure.WebJobs.Extensions.DurableTask"

[FunctionName("RaiseEvent")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    int[] eventData = new int[] { 1, 2, 3 };
    return client.RaiseEventAsync(instanceId, "MyEvent", eventData);
}
```

> [!NOTE]
> Создание событий в настоящее время поддерживается только для функции orchestrator C#.

> [!WARNING]
> Если экземпляра оркестрации с указанным *идентификатором* не существует или этот экземпляр не ожидает указанное *имя события*, сообщение о событии игнорируется. Дополнительные сведения об этом поведении см. в [описании проблемы на GitHub](https://github.com/Azure/azure-functions-durable-extension/issues/29).

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> Узнайте, как использовать [HTTP-интерфейсы API для управления экземплярами](durable-functions-http-api.md)
