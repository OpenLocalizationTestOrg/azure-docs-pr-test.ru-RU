---
title: "Автоматическая пересылка сущностей обмена сообщениями служебной шины Azure | Документация Майкрософт"
description: "Описывается, как привязать очередь или подписку служебной шины к другой очереди или разделу."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 2656b3a276c542ca836b3949e4e493d7c7f48f16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="5a80e-103">Объединение в цепочки сущностей служебной шины с помощью автоматической переадресации</span><span class="sxs-lookup"><span data-stu-id="5a80e-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="5a80e-104">Функция *автоматической переадресации* служебной шины позволяет привязать очередь или подписку к другой очереди или разделу, которые являются частью одного и того же пространства имен.</span><span class="sxs-lookup"><span data-stu-id="5a80e-104">The Service Bus *auto-forwarding* feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span></span> <span data-ttu-id="5a80e-105">Если включена автоматическая переадресация, служебная шина автоматически удаляет сообщения, помещенные в первую очередь или подписку (источник), и помещает их во вторую очередь или раздел (место назначения).</span><span class="sxs-lookup"><span data-stu-id="5a80e-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span></span> <span data-ttu-id="5a80e-106">Обратите внимание, что при этом сохраняется возможность отправить сообщение в конечную сущность напрямую.</span><span class="sxs-lookup"><span data-stu-id="5a80e-106">Note that it is still possible to send a message to the destination entity directly.</span></span> <span data-ttu-id="5a80e-107">Кроме того, подочередь (например, очередь недоставленных сообщений) нельзя привязать к другой очереди или разделу.</span><span class="sxs-lookup"><span data-stu-id="5a80e-107">Also, it is not possible to chain a subqueue, such as a deadletter queue, to another queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="5a80e-108">Использование автоматической переадресации</span><span class="sxs-lookup"><span data-stu-id="5a80e-108">Using auto-forwarding</span></span>
<span data-ttu-id="5a80e-109">Автоматическую переадресацию можно включить, задав свойства [QueueDescription.ForwardTo][QueueDescription.ForwardTo] или [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] объектов источника [QueueDescription][QueueDescription] или [SubscriptionDescription][SubscriptionDescription], как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="5a80e-109">You can enable auto-forwarding by setting the [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on the [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for the source, as in the following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="5a80e-110">Конечная сущность должна существовать на момент создания исходной сущности.</span><span class="sxs-lookup"><span data-stu-id="5a80e-110">The destination entity must exist at the time the source entity is created.</span></span> <span data-ttu-id="5a80e-111">Если конечной сущности не существует, служебная шина возвращает исключение при попытке создать исходную сущность.</span><span class="sxs-lookup"><span data-stu-id="5a80e-111">If the destination entity does not exist, Service Bus returns an exception when asked to create the source entity.</span></span>

<span data-ttu-id="5a80e-112">С помощью автоматической переадресации можно выполнить масштабирование отдельного раздела.</span><span class="sxs-lookup"><span data-stu-id="5a80e-112">You can use auto-forwarding to scale out an individual topic.</span></span> <span data-ttu-id="5a80e-113">Служебная шина ограничивает [количество подписок на определенный раздел](service-bus-quotas.md) до 2000.</span><span class="sxs-lookup"><span data-stu-id="5a80e-113">Service Bus limits the [number of subscriptions on a given topic](service-bus-quotas.md) to 2,000.</span></span> <span data-ttu-id="5a80e-114">Создав разделы второго уровня, можно разместить дополнительные подписки.</span><span class="sxs-lookup"><span data-stu-id="5a80e-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="5a80e-115">Обратите внимание: даже если вы не связаны ограничением служебной шины на количество подписок, добавление разделов второго уровня может повысить общую пропускную способность раздела.</span><span class="sxs-lookup"><span data-stu-id="5a80e-115">Note that even if you are not bound by the Service Bus limitation on the number of subscriptions, adding a second level of topics can improve the overall throughput of your topic.</span></span>

![Сценарий автоматической пересылки][0]

<span data-ttu-id="5a80e-117">С помощью автоматической переадресации также можно разделить отправителей и получателей сообщений.</span><span class="sxs-lookup"><span data-stu-id="5a80e-117">You can also use auto-forwarding to decouple message senders from receivers.</span></span> <span data-ttu-id="5a80e-118">Например, рассмотрим систему ERP, состоящую из трех модулей: обработки заказов, управления запасами и управления отношениями с клиентами.</span><span class="sxs-lookup"><span data-stu-id="5a80e-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="5a80e-119">Каждый из этих модулей создает сообщения, передаваемые в очередь в соответствующем разделе.</span><span class="sxs-lookup"><span data-stu-id="5a80e-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="5a80e-120">Алиса и Роберт — торговые представители, которых интересуют все сообщения, относящиеся к своим клиентам.</span><span class="sxs-lookup"><span data-stu-id="5a80e-120">Alice and Bob are sales representatives that are interested in all messages that relate to their customers.</span></span> <span data-ttu-id="5a80e-121">Для получения этих сообщений Алиса и Боб создают персональные очереди и подписки в каждом из разделов ERP, которые автоматически пересылают все сообщения в их очереди.</span><span class="sxs-lookup"><span data-stu-id="5a80e-121">To receive those messages, Alice and Bob each create a personal queue and a subscription on each of the ERP topics that automatically forward all messages to their queue.</span></span>

![Сценарий автоматической пересылки][1]

<span data-ttu-id="5a80e-123">Если Алиса уйдет в отпуск, то заполнится ее личная очередь, а не очередь раздела ERP.</span><span class="sxs-lookup"><span data-stu-id="5a80e-123">If Alice goes on vacation, her personal queue, rather than the ERP topic, fills up.</span></span> <span data-ttu-id="5a80e-124">В этом сценарии ни один из разделов ERP не достигнет выделенной квоты, так как торговый представитель не получил ни одного сообщения.</span><span class="sxs-lookup"><span data-stu-id="5a80e-124">In this scenario, because a sales representative has not received any messages, none of the ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="5a80e-125">Рекомендации при использовании автоматической пересылки</span><span class="sxs-lookup"><span data-stu-id="5a80e-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="5a80e-126">Если целевая сущность накапливает слишком много сообщений и превышает квоту или целевая сущность отключена, то исходная сущность добавляет сообщения в [очередь недоставленных сообщений](service-bus-dead-letter-queues.md) до тех пор, пока в целевой сущности не появится место (или пока целевая сущность не будет снова включена).</span><span class="sxs-lookup"><span data-stu-id="5a80e-126">If the destination entity accumulates too many messages and exceeds the quota, or the destination entity is disabled, the source entity adds the messages to its [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in the destination (or the entity is re-enabled).</span></span> <span data-ttu-id="5a80e-127">Эти сообщения будут находиться в очереди недоставленных сообщений, поэтому необходимо явным образом получать и обрабатывать их из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="5a80e-127">Those messages will continue to live in the dead-letter queue, so you must explicitly receive and process them from the dead-letter queue.</span></span>

<span data-ttu-id="5a80e-128">При объединении в цепочку отдельных разделов для получения составного раздела с несколькими подписками рекомендуется сократить количество подписок на раздел первого уровня до умеренного и увеличить количество подписок на разделы второго уровня.</span><span class="sxs-lookup"><span data-stu-id="5a80e-128">When chaining together individual topics to obtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on the first-level topic and many subscriptions on the second-level topics.</span></span> <span data-ttu-id="5a80e-129">Например, раздел первого уровня с 20 подписками, каждая из которых объединена в цепочку с разделом второго уровня с 200 подписками, позволяет получить более высокую пропускную способность по сравнению с разделом первого уровня с 200 подписками, каждая из которых объединена в цепочку с разделом второго уровня с 20 подписками.</span><span class="sxs-lookup"><span data-stu-id="5a80e-129">For example, a first-level topic with 20 subscriptions, each of them chained to a second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained to a second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="5a80e-130">Служебная шина тарифицирует каждое перенаправленное сообщение как одну операцию.</span><span class="sxs-lookup"><span data-stu-id="5a80e-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="5a80e-131">Например, отправка сообщения в раздел с 20 подписками, каждая из которых настроена на автоматическую переадресацию сообщений в другую очередь или раздел, тарифицируется как 21 операция, если все подписки первого уровня получили копию сообщения.</span><span class="sxs-lookup"><span data-stu-id="5a80e-131">For example, sending a message to a topic with 20 subscriptions, each of them configured to auto-forward messages to another queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of the message.</span></span>

<span data-ttu-id="5a80e-132">Для создания подписки, привязанной к другой очереди или разделу, создатель подписки должен иметь разрешение на **управление** как исходной, так и целевой сущностями.</span><span class="sxs-lookup"><span data-stu-id="5a80e-132">To create a subscription that is chained to another queue or topic, the creator of the subscription must have **Manage** permissions on both the source and the destination entity.</span></span> <span data-ttu-id="5a80e-133">Для отправки сообщений в исходный раздел требуется только разрешение на **отправку** для исходного раздела.</span><span class="sxs-lookup"><span data-stu-id="5a80e-133">Sending messages to the source topic only requires **Send** permissions on the source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a80e-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a80e-134">Next steps</span></span>

<span data-ttu-id="5a80e-135">Подробные сведения об автоматической пересылке см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="5a80e-135">For detailed information about auto-forwarding, see the following reference topics:</span></span>

* <span data-ttu-id="5a80e-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="5a80e-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="5a80e-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="5a80e-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="5a80e-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="5a80e-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="5a80e-139">Дополнительные сведения об улучшении производительности служебной шины см. в статье</span><span class="sxs-lookup"><span data-stu-id="5a80e-139">To learn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="5a80e-140">Рекомендации по повышению производительности с помощью обмена сообщениями через служебную шину</span><span class="sxs-lookup"><span data-stu-id="5a80e-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="5a80e-141">[Секционированные сущности обмена сообщениями][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="5a80e-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
