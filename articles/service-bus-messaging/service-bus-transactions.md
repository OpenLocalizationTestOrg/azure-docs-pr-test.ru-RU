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
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="a2c7f-103">Обзор обработки транзакций в служебной шине</span><span class="sxs-lookup"><span data-stu-id="a2c7f-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="a2c7f-104">В этой статье рассматриваются возможности транзакций hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="a2c7f-105">Большая часть hello-обсуждений показана hello [атомарные транзакции с примером служебной шины](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="a2c7f-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="a2c7f-106">В этой статье приведен обзор ограниченного tooan обработка транзакций и hello *отправки по* функции в Service Bus, образец hello атомарной транзакции большими во время области.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="a2c7f-107">Транзакции в служебной шине</span><span class="sxs-lookup"><span data-stu-id="a2c7f-107">Transactions in Service Bus</span></span>
<span data-ttu-id="a2c7f-108">[Транзакция](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) объединяет две или более операций в *область выполнения*.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="a2c7f-109">По своей природе такая транзакция необходимо убедиться, что все операции, принадлежащий tooa группы операций завершится успехом или сбоем совместно.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="a2c7f-110">В этом отношении транзакции воздействуют как одно целое, который часто ссылка tooas *атомарность*.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="a2c7f-111">Служебная шина является брокером для транзакционных сообщений и гарантирует целостность всех внутренних операций в соответствии с хранилищами сообщений.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="a2c7f-112">Все передачи сообщения внутри Service Bus, такие как перемещение сообщений tooa [очереди недоставленных сообщений](service-bus-dead-letter-queues.md) или [автоматическая переадресация](service-bus-auto-forwarding.md) сообщений между сущностями являются транзакционными.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="a2c7f-113">Таким образом, когда служебная шина принимает сообщение, оно уже сохранено и помечено порядковым номером.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="a2c7f-114">После этого для любой передачу сообщений в Service Bus являются операциями согласованных между сущностями, и ни один приведет tooloss (источник завершается успешно и целевой завершается с ошибкой) или tooduplication (сбой источника и цели успешного) сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="a2c7f-115">Service Bus поддерживает операции группирования от одной сущности обмена сообщениями (очередь, раздел, подписка) в пределах области hello транзакции.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="a2c7f-116">Например можно отправить несколько сообщений очереди tooone из в области транзакции и сообщений hello будет только зафиксированных toohello очереди журнала при успешном выполнении транзакции hello.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="a2c7f-117">Операции в области транзакций</span><span class="sxs-lookup"><span data-stu-id="a2c7f-117">Operations within a transaction scope</span></span>
<span data-ttu-id="a2c7f-118">Ниже приведены Hello операций, которые могут выполняться в области транзакции.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="a2c7f-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="a2c7f-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="a2c7f-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="a2c7f-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="a2c7f-121">Получение операций не включаются, так как предполагается, что приложение hello получает сообщения с помощью hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) режиме внутри некоторых цикл получения или с [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) обратного вызова, и только затем открывается транзакции области видимости для обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="a2c7f-122">Hello метода обработки сообщения hello (полное, отложить прерывания недоставленных сообщений), то возникает внутри области hello и в зависимости от, hello общий результат транзакции hello.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="a2c7f-123">Передачи и функция "отправить через"</span><span class="sxs-lookup"><span data-stu-id="a2c7f-123">Transfers and "send via"</span></span>
<span data-ttu-id="a2c7f-124">tooenable транзакций передача в эксплуатацию данных из очереди tooa процессора, а затем tooanother очереди, Service Bus поддерживает *передачи*.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="a2c7f-125">В операции передачи отправитель сначала отправляет tooa сообщение «очередь передачи» и очередь передачи hello немедленно перемещает toohello сообщение hello предназначен конечной очереди, используя же надежной передачи реализацию, которая использует возможность автоматическую пересылку hello hello в.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="a2c7f-126">приветственное сообщение никогда не будет зафиксирована toohello передачи очереди журнала таким образом, что он станет видимым для потребителей очередь передачи hello.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="a2c7f-127">Hello power этой возможности транзакций становится очевидным, когда очередь передачи hello сам является источником hello входящих сообщений hello отправителя.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="a2c7f-128">Другими словами, Service Bus можно перенести очередь назначения toohello сообщение hello «via» hello очереди передачи, при выполнении полной (или отложить, или недоставленных писем) операция на входящее сообщение hello в одной атомарной операции.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="a2c7f-129">Пример кода</span><span class="sxs-lookup"><span data-stu-id="a2c7f-129">See it in code</span></span>
<span data-ttu-id="a2c7f-130">tooset копирование подобная передача создать отправителя сообщения, предназначенного для очереди назначения hello через очередь передачи hello.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="a2c7f-131">Также имеется получатель, который извлекает сообщения из той же очереди.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="a2c7f-132">Например:</span><span class="sxs-lookup"><span data-stu-id="a2c7f-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="a2c7f-133">Простой транзакции затем использует эти элементы, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="a2c7f-133">A simple transaction then uses these elements, as in hello following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a2c7f-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2c7f-134">Next steps</span></span>

<span data-ttu-id="a2c7f-135">См. следующие дополнительные сведения об очередях Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="a2c7f-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="a2c7f-136">Объединение в цепочки сущностей служебной шины с помощью автоматической переадресации</span><span class="sxs-lookup"><span data-stu-id="a2c7f-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="a2c7f-137">Пример автоматической пересылки</span><span class="sxs-lookup"><span data-stu-id="a2c7f-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="a2c7f-138">Пример выполнения атомарных транзакций с помощью служебной шины</span><span class="sxs-lookup"><span data-stu-id="a2c7f-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="a2c7f-139">Сравнение службы очередей Azure и службы очередей служебной шины</span><span class="sxs-lookup"><span data-stu-id="a2c7f-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="a2c7f-140">Как toouse очереди шины обслуживания</span><span class="sxs-lookup"><span data-stu-id="a2c7f-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

