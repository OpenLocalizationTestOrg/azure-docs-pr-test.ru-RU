---
title: "aaaAzure Service Bus Premium и Standard обмена сообщениями Обзор цен уровней | Документы Microsoft"
description: "Уровни обмена сообщениями через служебную шину \"Премиум\" и \"Стандартный\""
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>Уровни обмена сообщениями через служебную шину Premium и Standard

Обмен сообщениями через служебную шину включает такие сущности, как очереди и темы, а также объединяет возможности корпоративного обмена сообщениями с расширенной семантикой публикаций и подписок в масштабе облака. Обмен сообщениями Service Bus используется как магистрали hello связи для многих сложных облачных решений.

Hello *Premium* уровень обмена сообщениями Service Bus рассматриваются общие запросы от клиентов вокруг масштабируемость, производительность и доступность критически важных приложений. Несмотря на то, что наборы функций hello практически идентичны, этих двух уровней обмен сообщениями Service Bus, разработанной tooserve различных вариантов использования.

Некоторые различия высокого уровня, выделяются в hello в следующей таблице.

| Premium | Стандартная |
| --- | --- |
| Высокая пропускная способность |Переменная пропускная способность |
| Прогнозируемая производительность |Переменная задержка |
| Фиксированные цены |Переменная оплата по мере использования |
| Рабочая нагрузка tooscale возможность вверх и вниз |Недоступно |
| Сообщение размером до too1 МБ |Увеличение размера сообщения too256 КБ |

**Отправка сообщений Premium Service Bus** обеспечивает изоляцию ресурсов на уровне hello ЦП и памяти, чтобы каждой рабочей нагрузки клиентов работающий в изоляции. Контейнер ресурса называется *единицей обмена сообщениями*. Для каждого премиального пространства имен выделяется хотя бы одна единица обмена сообщениями. Для каждого пространства имен служебной шины Premium можно приобрести одну, две или четыре единицы обмена сообщениями. Одной рабочей нагрузки или сущности может охватывать несколько блоков обмена сообщениями и по желанию, можно изменить hello число единиц обмена сообщениями, хотя плата за 24 часа или ежедневной частоты выставления счетов. Hello результатом является прогнозируемым и повторяющиеся производительности для вашего решения на основе Service Bus.

Оно отличается не только более предсказуемой производительностью и высокой доступностью, но и более высокой скоростью работы. Отправка сообщений Premium Service Bus лежит hello подсистемы хранилища, представленные в [концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/). Передача сообщений Premium максимальной производительности намного быстрее, чем с помощью стандартного уровня hello.

## <a name="premium-messaging-technical-differences"></a>Технические отличия обмена сообщениями уровня Premium

Hello следующих разделах рассматривается ряд различий между Premium и стандартного уровней обмена сообщениями.

### <a name="partitioned-queues-and-topics"></a>Секционированные очереди и разделы

Секционированные очереди и разделы поддерживаются на уровне обмена сообщениями "Премиум". На самом деле эти сущности всегда секционируются (это нельзя отключить). Однако Premium секционированные очереди и разделы hello не работают так же, как hello уровней Standard и Basic обмена сообщениями Service Bus. "Премиум" обмена сообщениями не использует SQL в качестве хранилища данных и больше не имеет hello конкуренции возможных ресурса, связанный с общей платформы. В результате секционирование не необходимые tooimprove производительности. Кроме того количество разделов hello было изменено с 16 секциями в сообщения Standard too2 секций в Premium. Наличие двух секций обеспечивает доступность и является номером больше подходит для среды выполнения "премиум" hello. 

С Premium обмена сообщениями, при указании размера hello сущности с [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), что размер разбивается равномерно по секциям hello 2, в отличие от [стандарт секционированных сущностей](service-bus-partitioning.md#standard) в какой hello общий размер равен 16 раз hello указанный размер. 

Дополнительные сведения о секционировании см. в статье [Секционированные очереди и разделы](service-bus-partitioning.md).

### <a name="express-entities"></a>Экспресс-сущности

Так как обмен сообщениями уровня "Премиум" работает в полностью изолированной среде, экспресс-сущности не поддерживаются в пространстве имен этого уровня. Дополнительные сведения о явных функции hello см. в разделе hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) свойство.

При наличии кода, запущенного под стандартной tooport обмена сообщениями и хотите его toohello уровня Premium, убедитесь, что hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) задано слишком**false** (значение по умолчанию hello).

## <a name="get-started-with-premium-messaging"></a>Приступая к работе с обменом сообщениями уровня "Премиум"

Приступая к работе с отправка сообщений Premium несложно, и процесс hello аналогичные toothat обмена сообщениями Standard. Для начала [создайте пространство имен](service-bus-create-namespace-portal.md). В разделе **Ценовая категория** выберите **Премиум**.

![create-premium-namespace][create-premium-namespace]

Вы можете также создать [пространство имен уровня "Премиум", используя шаблоны Azure Resource Manager](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).


## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о Service Bus обмена сообщениями, см. следующие разделы hello.

* [Introducing Azure Service Bus Premium Messaging (blog post)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/) (Общие сведения об обмене сообщениями через служебную шину Azure уровня "Премиум" (запись в блоге))
* [Introducing Azure Service Bus Premium Messaging (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging) (Общие сведения об обмене сообщениями через служебную шину Azure уровня "Премиум" (Channel9))
* [Обмен сообщениями через служебную шину: гибкая доставка данных в облаке](service-bus-messaging-overview.md)
* [Как toouse очереди шины обслуживания](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
