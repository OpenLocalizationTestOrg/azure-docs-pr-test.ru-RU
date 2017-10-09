---
title: "очереди недоставленных сообщений шины aaaService | Документы Microsoft"
description: "Обзор очередей недоставленных сообщений служебной шины Azure"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Обзор очередей недоставленных сообщений служебной шины

Очереди служебной шины и подписки на разделы формируют дополнительную вложенную очередь, которая называется *очередью недоставленных сообщений* (DLQ). очереди недоставленных сообщений Hello не обязательно явно создан toobe и не может быть удален или иным образом управляемый независимо от hello основной сущности.

В этой статье рассматриваются очереди недоставленных сообщений в Azure Service Bus. Большая часть hello-обсуждений показана hello [очередей недоставленных сообщений образец](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) на GitHub.
 
## <a name="hello-dead-letter-queue"></a>очереди недоставленных сообщений Hello

Hello очереди недоставленных сообщений hello предназначен toohold сообщений, которые не может быть доставлено получателю tooany или сообщений, которые не удалось обработать. Сообщения можно удалить из hello очередь DLQ и проверен. Приложение может с помощью оператора устранить проблемы и повторно отправить сообщение hello, журнала hello факт, что произошла ошибка и действие по исправлению. 

С точки зрения API и протокола hello очередь DLQ является практически аналогично tooany другую очередь, за исключением того, что сообщения может быть отправлена только через жестов недоставленных сообщений hello hello родительской сущности. Кроме того, в ней не отслеживается время жизни, поэтому удалить сообщение из очереди DLQ невозможно. очереди недоставленных сообщений Hello полностью поддерживает доставки блокировки для просмотра и транзакционных операций.

Обратите внимание, что нет автоматическую очистку hello очередь DLQ. Сообщения остаются в hello очередь DLQ, пока не будет явным образом получать их из очередь DLQ hello и вызова [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) на hello недоставленных сообщений.

## <a name="moving-messages-toohello-dlq"></a>Перемещение сообщений в очередь DLQ toohello

Существует несколько действий в Service Bus, вызывающие tooget сообщения помещаются toohello очередь DLQ из в сам обработчик сообщений hello. Приложение может также явно перемещать сообщения toohello очередь DLQ. 

Брокером hello перемещения сообщения hello, два свойства добавляются toohello сообщение hello broker вызывает его внутренней версии hello [недоставленных сообщений](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) метод приветственное сообщение: `DeadLetterReason` и `DeadLetterErrorDescription`.

Приложения могут определять свои собственные коды для hello `DeadLetterReason` свойство, но hello системы наборов hello следующие значения.

| Условие | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Всегда |HeaderSizeExceeded |была превышена квота размера Hello для этого потока. |
| !TopicDescription.<br />EnableFilteringMessagesBeforePublishing and SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |exception.GetType().Name |exception.Message |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |приветственное сообщение истек и был мертвой очередь. |
| SubscriptionDescription.RequiresSession |Идентификатор сеанса имеет значение null. |Сущность, поддерживающая сеансы, не допускает использование сообщений, идентификатор сеанса которых имеет значение null. |
| !очередь недоставленных сообщений |MaxTransferHopCountExceeded |Null |
| Явное перемещение приложением в очередь недоставленных сообщений |Задается приложением |Задается приложением |

## <a name="exceeding-maxdeliverycount"></a>Превышено значение MaxDeliveryCount
Очереди и подписки имеют [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) и [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) свойство соответственно; hello значение по умолчанию — 10. Каждый раз, когда сообщение было доставлено при блокировке. ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)), но была либо явно прервана или блокировки hello истек, сообщение hello [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) — увеличивается на единицу. Когда [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) превышает [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), сообщение hello является перемещенный toohello очередь DLQ, указав hello `MaxDeliveryCountExceeded` код ошибки.

Такое поведение не может быть отключена, но можно задать [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa слишком большое значение.

## <a name="exceeding-timetolive"></a>Превышение значения TimeToLive
Здравствуйте, когда [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) или [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) задано слишком**true** (по умолчанию hello — **false**), все сообщения, срок действия которых истекает, перемещенный toohello очередь DLQ, указав hello `TTLExpiredException` код ошибки.

Обратите внимание, что сообщения с истекшим сроком очищаются только таким образом переместить toohello очередь DLQ при наличии по крайней мере один active приемника извлечение hello основной очереди или подписки. Это поведение предусмотрено проектом.

## <a name="errors-while-processing-subscription-rules"></a>Ошибки при обработке правил подписки
Здравствуйте, когда [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) включено для подписки, ошибках, возникающих во время правила фильтра подписки SQL записываются в очередь DLQ hello а также неправильная сообщение hello.

## <a name="application-level-dead-lettering"></a>Недоставленные сообщения на уровне приложения
В дополнение toohello системных блокирование компоненты приложения могут использовать неприемлемо сообщений hello очередь DLQ tooexplicitly отказа в доступе. Это могут быть сообщения, которые не может обрабатываться неправильно из-за сортировки tooany неполадка с системой, сообщения, не прошедшие проверку подлинности при использовании некоторых схема безопасности на уровне сообщений или сообщений, которые содержат полезные данные неправильного формата.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>Недоставка сообщений в сценариях ForwardTo или SendVia

Сообщения будет отправлен toohello передачи очередь недоставленных сообщений в группе hello следующие условия:

- Сообщение проходит более 3 очередей или разделов, которые [связаны друг с другом](service-bus-auto-forwarding.md).
- Hello конечной очереди или раздела отключено или удалено.
- Hello конечную очередь или раздел превышает hello максимальный размер сущности.

tooretrieve этих очередь недоставленных сообщений, можно создать получателя с помощью hello [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) вспомогательный метод.

## <a name="example"></a>Пример
Следующий фрагмент кода Hello создает получателя сообщения. В hello цикл для hello основной очереди получения, hello код извлекает сообщение hello с [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), требующее tooinstantly broker hello возвращаемого сообщения доступны или tooreturn без результата. Если код hello получает сообщение, немедленно будут прерваны, увеличит hello `DeliveryCount`. Когда система hello перемещает сообщение hello toohello очередь DLQ, hello основной очереди является пустым и hello завершает работу цикла, как [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) возвращает **null**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия
См. следующие дополнительные сведения об очередях Service Bus hello.

* [Начало работы с очередями служебной шины](service-bus-dotnet-get-started-with-queues.md)
* [Сравнение службы очередей Azure и службы очередей служебной шины](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

