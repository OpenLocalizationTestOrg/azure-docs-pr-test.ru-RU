---
title: "aaaOverview операции обработки в Azure Service Bus | Документы Microsoft"
description: "Общие сведения об атомарных транзакциях служебной шины Azure"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a>Обзор обработки транзакций в служебной шине
В этой статье рассматриваются возможности транзакций hello Azure Service Bus. Большая часть hello-обсуждений показана hello [атомарные транзакции с примером служебной шины](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions). В этой статье приведен обзор ограниченного tooan обработка транзакций и hello *отправки по* функции в Service Bus, образец hello атомарной транзакции большими во время области.

## <a name="transactions-in-service-bus"></a>Транзакции в служебной шине
[Транзакция](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) объединяет две или более операций в *область выполнения*. По своей природе такая транзакция необходимо убедиться, что все операции, принадлежащий tooa группы операций завершится успехом или сбоем совместно. В этом отношении транзакции воздействуют как одно целое, который часто ссылка tooas *атомарность*. 

Служебная шина является брокером для транзакционных сообщений и гарантирует целостность всех внутренних операций в соответствии с хранилищами сообщений. Все передачи сообщения внутри Service Bus, такие как перемещение сообщений tooa [очереди недоставленных сообщений](service-bus-dead-letter-queues.md) или [автоматическая переадресация](service-bus-auto-forwarding.md) сообщений между сущностями являются транзакционными. Таким образом, когда служебная шина принимает сообщение, оно уже сохранено и помечено порядковым номером. После этого для любой передачу сообщений в Service Bus являются операциями согласованных между сущностями, и ни один приведет tooloss (источник завершается успешно и целевой завершается с ошибкой) или tooduplication (сбой источника и цели успешного) сообщения hello.

Service Bus поддерживает операции группирования от одной сущности обмена сообщениями (очередь, раздел, подписка) в пределах области hello транзакции. Например можно отправить несколько сообщений очереди tooone из в области транзакции и сообщений hello будет только зафиксированных toohello очереди журнала при успешном выполнении транзакции hello.

## <a name="operations-within-a-transaction-scope"></a>Операции в области транзакций
Ниже приведены Hello операций, которые могут выполняться в области транзакции.

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync 

Получение операций не включаются, так как предполагается, что приложение hello получает сообщения с помощью hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) режиме внутри некоторых цикл получения или с [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) обратного вызова, и только затем открывается транзакции области видимости для обработки сообщения hello.

Hello метода обработки сообщения hello (полное, отложить прерывания недоставленных сообщений), то возникает внутри области hello и в зависимости от, hello общий результат транзакции hello.

## <a name="transfers-and-send-via"></a>Передачи и функция "отправить через"
tooenable транзакций передача в эксплуатацию данных из очереди tooa процессора, а затем tooanother очереди, Service Bus поддерживает *передачи*. В операции передачи отправитель сначала отправляет tooa сообщение «очередь передачи» и очередь передачи hello немедленно перемещает toohello сообщение hello предназначен конечной очереди, используя же надежной передачи реализацию, которая использует возможность автоматическую пересылку hello hello в. приветственное сообщение никогда не будет зафиксирована toohello передачи очереди журнала таким образом, что он станет видимым для потребителей очередь передачи hello.

Hello power этой возможности транзакций становится очевидным, когда очередь передачи hello сам является источником hello входящих сообщений hello отправителя. Другими словами, Service Bus можно перенести очередь назначения toohello сообщение hello «via» hello очереди передачи, при выполнении полной (или отложить, или недоставленных писем) операция на входящее сообщение hello в одной атомарной операции. 

### <a name="see-it-in-code"></a>Пример кода
tooset копирование подобная передача создать отправителя сообщения, предназначенного для очереди назначения hello через очередь передачи hello. Также имеется получатель, который извлекает сообщения из той же очереди. Например:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

Простой транзакции затем использует эти элементы, как следующий пример hello:

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a>Дальнейшие действия

См. следующие дополнительные сведения об очередях Service Bus hello.

* [Объединение в цепочки сущностей служебной шины с помощью автоматической переадресации](service-bus-auto-forwarding.md)
* [Пример автоматической пересылки](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [Пример выполнения атомарных транзакций с помощью служебной шины](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [Сравнение службы очередей Azure и службы очередей служебной шины](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [Как toouse очереди шины обслуживания](service-bus-dotnet-get-started-with-queues.md)

