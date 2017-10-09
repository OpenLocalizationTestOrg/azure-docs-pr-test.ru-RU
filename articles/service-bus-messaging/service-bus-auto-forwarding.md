---
title: "сущности обмена сообщениями Azure Service Bus пересылки aaaAuto | Документы Microsoft"
description: "Как toochain Service Bus очереди или подписки tooanother очереди или раздела."
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
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="c98fc-103">Объединение в цепочки сущностей служебной шины с помощью автоматической переадресации</span><span class="sxs-lookup"><span data-stu-id="c98fc-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="c98fc-104">Hello Service Bus *Авто переадресации* дают возможность toochain очереди или подписки tooanother очередь или раздел, который является частью hello того же пространства имен.</span><span class="sxs-lookup"><span data-stu-id="c98fc-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="c98fc-105">При включенной Авто переадресации Service Bus автоматически удаляет сообщения, помещенные в первую очередь hello или подписку (источник) и помещает их в hello вторую очередь или раздел (адресат).</span><span class="sxs-lookup"><span data-stu-id="c98fc-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="c98fc-106">Обратите внимание, что все еще возможно toosend сущность назначения сообщение toohello напрямую.</span><span class="sxs-lookup"><span data-stu-id="c98fc-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="c98fc-107">Кроме того он не возможные toochain подочередь, например очередь недоставленных сообщений, tooanother очереди или раздела.</span><span class="sxs-lookup"><span data-stu-id="c98fc-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="c98fc-108">Использование автоматической переадресации</span><span class="sxs-lookup"><span data-stu-id="c98fc-108">Using auto-forwarding</span></span>
<span data-ttu-id="c98fc-109">Вы можете включить Авто переадресации, установка hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] или [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] свойства hello [QueueDescription] [ QueueDescription] или [SubscriptionDescription] [ SubscriptionDescription] объектов hello источника, как и hello Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="c98fc-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="c98fc-110">во время hello создания hello исходная сущность должна существовать сущность назначения Hello.</span><span class="sxs-lookup"><span data-stu-id="c98fc-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="c98fc-111">Если сущность назначения hello не существует, Service Bus возвращает исключение, если задаваемые toocreate hello исходной сущности.</span><span class="sxs-lookup"><span data-stu-id="c98fc-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="c98fc-112">Можно использовать tooscale Авто переадресацию из раздела.</span><span class="sxs-lookup"><span data-stu-id="c98fc-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="c98fc-113">Service Bus ограничения hello [количество подписок в заданном разделе](service-bus-quotas.md) too2 000.</span><span class="sxs-lookup"><span data-stu-id="c98fc-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="c98fc-114">Создав разделы второго уровня, можно разместить дополнительные подписки.</span><span class="sxs-lookup"><span data-stu-id="c98fc-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="c98fc-115">Обратите внимание, что даже если вы не связаны с hello Service Bus повышает ограничение на количество подписок, добавление разделов второго уровня в hello hello общую пропускную способность раздела.</span><span class="sxs-lookup"><span data-stu-id="c98fc-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![Сценарий автоматической пересылки][0]

<span data-ttu-id="c98fc-117">Также можно использовать отправителей сообщений toodecouple Авто переадресации от получателей.</span><span class="sxs-lookup"><span data-stu-id="c98fc-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="c98fc-118">Например, рассмотрим систему ERP, состоящую из трех модулей: обработки заказов, управления запасами и управления отношениями с клиентами.</span><span class="sxs-lookup"><span data-stu-id="c98fc-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="c98fc-119">Каждый из этих модулей создает сообщения, передаваемые в очередь в соответствующем разделе.</span><span class="sxs-lookup"><span data-stu-id="c98fc-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="c98fc-120">Ольга и Алексей — торговые представители, которых интересуют все сообщения, относящиеся tootheir клиентов.</span><span class="sxs-lookup"><span data-stu-id="c98fc-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="c98fc-121">tooreceive те сообщения, Анна и Виктор Создание личные очереди и подписки на каждом из разделов ERP hello, которые автоматически переадресовывают все tootheir сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="c98fc-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![Сценарий автоматической пересылки][1]

<span data-ttu-id="c98fc-123">Если Ольга уйдет в отпуск, ее личная очередь, а не раздел ERP hello, заполняется до конца.</span><span class="sxs-lookup"><span data-stu-id="c98fc-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="c98fc-124">В этом сценарии, поскольку Торговый представитель не получил никаких сообщений, ни один из разделов ERP hello никогда не достигнет квоты.</span><span class="sxs-lookup"><span data-stu-id="c98fc-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="c98fc-125">Рекомендации при использовании автоматической пересылки</span><span class="sxs-lookup"><span data-stu-id="c98fc-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="c98fc-126">Если сущность назначения hello накапливает слишком много сообщений и превышает квоту hello или сущность назначения hello отключена, hello исходной сущности добавляет hello сообщений tooits [очереди недоставленных сообщений](service-bus-dead-letter-queues.md) до места назначения hello (или hello сущности будет снова включен).</span><span class="sxs-lookup"><span data-stu-id="c98fc-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="c98fc-127">Эти сообщения по-прежнему toolive в очереди недоставленных сообщений hello, поэтому необходимо явным образом получать и обрабатывать их из очереди недоставленных сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="c98fc-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="c98fc-128">При объединении в цепочку отдельных разделов tooobtain составного раздела с большим числом подписок, рекомендуется наличие умеренное количество подписок на раздел первого уровня hello и нескольких подписок на hello разделов второго уровня.</span><span class="sxs-lookup"><span data-stu-id="c98fc-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="c98fc-129">Например, раздел первого уровня с 20 подписками, каждая из которых присоединена tooa раздел второго уровня с 200 подписками, обеспечивает более высокую пропускную способность, чем раздел первого уровня с 200 подписками, каждая их которых присоединена tooa раздел второго уровня с 20 подписками .</span><span class="sxs-lookup"><span data-stu-id="c98fc-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="c98fc-130">Служебная шина тарифицирует каждое перенаправленное сообщение как одну операцию.</span><span class="sxs-lookup"><span data-stu-id="c98fc-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="c98fc-131">Например отправка сообщения tooa раздел с 20 подписками, каждый из них настроен tooauto переадресацию сообщений tooanother очередь или раздел, выставляется счет на 21 операцию, если все подписки первого уровня получают копию сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="c98fc-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="c98fc-132">toocreate подписка цепочек tooanother очередь или раздел, создатель hello hello подписки должен иметь **управление** разрешения для источника hello и hello конечной сущности.</span><span class="sxs-lookup"><span data-stu-id="c98fc-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="c98fc-133">Отправка сообщений toohello исходный раздел требуются только **отправки** разрешения на исходный раздел hello.</span><span class="sxs-lookup"><span data-stu-id="c98fc-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c98fc-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c98fc-134">Next steps</span></span>

<span data-ttu-id="c98fc-135">Подробные сведения об автоматической пересылки см. следующие справочные разделы hello:</span><span class="sxs-lookup"><span data-stu-id="c98fc-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="c98fc-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="c98fc-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="c98fc-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="c98fc-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="c98fc-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="c98fc-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="c98fc-139">toolearn Дополнительные сведения о Service Bus выигрыш в производительности, см.</span><span class="sxs-lookup"><span data-stu-id="c98fc-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="c98fc-140">Рекомендации по повышению производительности с помощью обмена сообщениями через служебную шину</span><span class="sxs-lookup"><span data-stu-id="c98fc-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="c98fc-141">[Секционированные сущности обмена сообщениями][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="c98fc-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
