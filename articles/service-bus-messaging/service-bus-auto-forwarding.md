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
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>Объединение в цепочки сущностей служебной шины с помощью автоматической переадресации

Hello Service Bus *Авто переадресации* дают возможность toochain очереди или подписки tooanother очередь или раздел, который является частью hello того же пространства имен. При включенной Авто переадресации Service Bus автоматически удаляет сообщения, помещенные в первую очередь hello или подписку (источник) и помещает их в hello вторую очередь или раздел (адресат). Обратите внимание, что все еще возможно toosend сущность назначения сообщение toohello напрямую. Кроме того он не возможные toochain подочередь, например очередь недоставленных сообщений, tooanother очереди или раздела.

## <a name="using-auto-forwarding"></a>Использование автоматической переадресации
Вы можете включить Авто переадресации, установка hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] или [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] свойства hello [QueueDescription] [ QueueDescription] или [SubscriptionDescription] [ SubscriptionDescription] объектов hello источника, как и hello Ниже приведен пример.

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

во время hello создания hello исходная сущность должна существовать сущность назначения Hello. Если сущность назначения hello не существует, Service Bus возвращает исключение, если задаваемые toocreate hello исходной сущности.

Можно использовать tooscale Авто переадресацию из раздела. Service Bus ограничения hello [количество подписок в заданном разделе](service-bus-quotas.md) too2 000. Создав разделы второго уровня, можно разместить дополнительные подписки. Обратите внимание, что даже если вы не связаны с hello Service Bus повышает ограничение на количество подписок, добавление разделов второго уровня в hello hello общую пропускную способность раздела.

![Сценарий автоматической пересылки][0]

Также можно использовать отправителей сообщений toodecouple Авто переадресации от получателей. Например, рассмотрим систему ERP, состоящую из трех модулей: обработки заказов, управления запасами и управления отношениями с клиентами. Каждый из этих модулей создает сообщения, передаваемые в очередь в соответствующем разделе. Ольга и Алексей — торговые представители, которых интересуют все сообщения, относящиеся tootheir клиентов. tooreceive те сообщения, Анна и Виктор Создание личные очереди и подписки на каждом из разделов ERP hello, которые автоматически переадресовывают все tootheir сообщений в очереди.

![Сценарий автоматической пересылки][1]

Если Ольга уйдет в отпуск, ее личная очередь, а не раздел ERP hello, заполняется до конца. В этом сценарии, поскольку Торговый представитель не получил никаких сообщений, ни один из разделов ERP hello никогда не достигнет квоты.

## <a name="auto-forwarding-considerations"></a>Рекомендации при использовании автоматической пересылки

Если сущность назначения hello накапливает слишком много сообщений и превышает квоту hello или сущность назначения hello отключена, hello исходной сущности добавляет hello сообщений tooits [очереди недоставленных сообщений](service-bus-dead-letter-queues.md) до места назначения hello (или hello сущности будет снова включен). Эти сообщения по-прежнему toolive в очереди недоставленных сообщений hello, поэтому необходимо явным образом получать и обрабатывать их из очереди недоставленных сообщений hello.

При объединении в цепочку отдельных разделов tooobtain составного раздела с большим числом подписок, рекомендуется наличие умеренное количество подписок на раздел первого уровня hello и нескольких подписок на hello разделов второго уровня. Например, раздел первого уровня с 20 подписками, каждая из которых присоединена tooa раздел второго уровня с 200 подписками, обеспечивает более высокую пропускную способность, чем раздел первого уровня с 200 подписками, каждая их которых присоединена tooa раздел второго уровня с 20 подписками .

Служебная шина тарифицирует каждое перенаправленное сообщение как одну операцию. Например отправка сообщения tooa раздел с 20 подписками, каждый из них настроен tooauto переадресацию сообщений tooanother очередь или раздел, выставляется счет на 21 операцию, если все подписки первого уровня получают копию сообщения hello.

toocreate подписка цепочек tooanother очередь или раздел, создатель hello hello подписки должен иметь **управление** разрешения для источника hello и hello конечной сущности. Отправка сообщений toohello исходный раздел требуются только **отправки** разрешения на исходный раздел hello.

## <a name="next-steps"></a>Дальнейшие действия

Подробные сведения об автоматической пересылки см. следующие справочные разделы hello:

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

toolearn Дополнительные сведения о Service Bus выигрыш в производительности, см. 

* [Рекомендации по повышению производительности с помощью обмена сообщениями через служебную шину](service-bus-performance-improvements.md)
* [Секционированные сущности обмена сообщениями][Partitioned messaging entities].

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
