---
title: "часто задаваемые вопросы (FAQ) Service Bus aaaAzure | Документы Microsoft"
description: "Ответы на некоторые часто задаваемые вопросы о служебной шине Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Часто задаваемые вопросы о служебной шине
В этой статье содержатся ответы на некоторые часто задаваемые вопросы о служебной шине Microsoft Azure. Также можно посетить hello [вопросы и ответы поддержки Azure](http://go.microsoft.com/fwlink/?LinkID=185083) Общие сведения Azure цены и поддержки.

## <a name="general-questions-about-azure-service-bus"></a>Общие вопросы о служебной шине Azure
### <a name="what-is-azure-service-bus"></a>Что такое служебная шина Azure?
[Azure Service Bus](service-bus-messaging-overview.md) — асинхронного обмена сообщениями облачная платформа, позволяющая toosend данных между системами несвязанным. Корпорация Майкрософт предлагает эту функцию как служба, это означает, что нет необходимости toohost любой оборудования в порядке toouse его.

### <a name="what-is-a-service-bus-namespace"></a>Что такое пространство имен служебной шины?
[Пространство имен](service-bus-create-namespace-portal.md) предоставляет контейнер для адресации ресурсов служебной шины в вашем приложении. Создание одного — необходимые toouse Service Bus и будет иметь одно из hello первые шаги в Приступая к работе.

### <a name="what-is-an-azure-service-bus-queue"></a>Что такое очередь служебной шины Azure?
[Очередь служебной шины](service-bus-queues-topics-subscriptions.md) — это сущность, в которой сохраняются сообщения. Очереди являются особенно полезна при наличии нескольких приложений или несколько частей распределенного приложения, которые должны toocommunicate друг с другом. очередь Hello действует как центр распространения tooa, поступают несколько продуктов (сообщения) и затем отправляется из этого расположения.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Что такое разделы и подписки служебной шины Azure?
Раздел можно представить в виде очереди. При использовании нескольких подписок он становится расширенной моделью обмена сообщениями. По сути, это инструмент связи по принципу "один ко многим". Эта модель публикации и подписки (или *pub/sub*) позволяет приложению, отправляющий сообщение tooa раздела с несколькими подписками toohave это сообщение получено несколькими приложениями.

### <a name="what-is-a-partitioned-entity"></a>Что такое секционированная сущность?
Обычная очередь или раздел обрабатываются одним брокером сообщений и сохраняются в одном хранилище сообщений. [Секционированная очередь или раздел](service-bus-partitioning.md) обрабатывается несколькими брокерами сообщений и хранится в нескольких хранилищах сообщений. Это означает, что hello общая пропускная способность секционированной очереди или раздела больше не ограничивается hello производительностью одного брокера сообщений или хранилища обмена сообщениями. Кроме того, при возникновении временного сбоя хранилища сообщений секционированная очередь или раздел останутся доступными.

Имейте в виду, что при использовании секционирования сущностей их упорядоченность не гарантируется. Hello событий, раздел недоступен можно по-прежнему отправлять и получать сообщения от hello других секций.

## <a name="best-practices"></a>Рекомендации
### <a name="what-are-some-azure-service-bus-best-practices"></a>Рекомендации по работе со служебной шиной Azure
* [Рекомендации по повышению производительности с помощью Service Bus] [ Best practices for performance improvements using Service Bus] — в этой статье описывается, как toooptimize производительности при обмене сообщениями.

### <a name="what-should-i-know-before-creating-entities"></a>Что необходимо знать перед созданием сущностей?
следующие свойства очереди и раздела Hello являются неизменяемыми. Учитывайте это при подготовке сущностей, так как эти свойства можно изменить, только создав сущность для замены.

* Размер
* Секционирование
* Сеансы:
* Обнаружение дубликатов
* экспресс-сущность.

## <a name="pricing"></a>Цены
В этом разделе ответы на некоторые часто задаваемые вопросы о структуре ценообразования hello Service Bus.

Hello [Service Bus, цены и выставление счетов](service-bus-pricing-billing.md) объясняются счетчика выставления счетов hello в Service Bus, а также сведения о ценах Service Bus см. в разделе [Service Bus, сведения о ценах](https://azure.microsoft.com/pricing/details/service-bus/).

Также можно посетить hello [вопросы и ответы поддержки Azure](http://go.microsoft.com/fwlink/?LinkID=185083) для общие Azure, сведения о ценах. 

### <a name="how-do-you-charge-for-service-bus"></a>Как выставляется цена на служебную шину?
Подробные сведения о ценах на использование служебной шины см. [здесь][Pricing overview]. В дополнение к этому toohello цены указаны, назначается цена за выходящих hello центра данных, в котором подготавливается ваше приложение сопутствующие передачи данных.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>При каком использовании шины обслуживания является передача toodata тема? А какое не считается?
Любая передача данных в пределах заданного региона Azure выполняется бесплатно, как и любая входящая передача данных. Передача данных вне региона — тема tooegress расходы, которые можно найти [здесь](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>Взимает ли служебная шина плату за использование хранилища?
Нет, служебная шина не взимает плату за использование хранилища. Однако есть Квота ограничивающей hello максимальный объем данных, которые могут сохраняться в очереди или раздела. См. в ответе на следующий ВОПРОС hello.

## <a name="quotas"></a>Квоты

Список Service Bus ограничениях и квотах см. в разделе hello [Обзор квоты Service Bus][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>Есть ли у служебной шины квоты использования?
По умолчанию для любой облачной службы Майкрософт устанавливается квота совокупного месячного использования в рамках всех подписок клиента. Мы понимаем, что вам может потребоваться больше, чем разрешено этими ограничениями. В таком случае вы можете в любое время обратиться в службу поддержки пользователей, чтобы мы изменили эти ограничения на основе ваших потребностей. Для служебной шины квоты статистического использования hello — 5 триллионов сообщений в месяц.

Хотя резервируются hello правой toodisable учетной записи клиента, для которого превышено квоты использования в данном месяце, будет предоставлять уведомления по электронной почте и сделать несколько попыток toocontact клиента до выполнения любого действия. Клиенты, превысившие эти квоты будут несут ответственность за плату, превышающую hello квоты.

Как и в случае с другими службами в Azure, Service Bus применяет набор особых квот tooensure, что имеется справедливого использования ресурсов. Дополнительные сведения о эти квоты можно найти в hello [Обзор квоты Service Bus][Quotas overview].

## <a name="troubleshooting"></a>Устранение неполадок
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>Какие существуют hello исключения, создаваемые интерфейсов API служебной шины Azure и их предложенные действия?
Список возможных исключений служебной шины приведен в разделе [Общие сведения об исключениях][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>Что такое подписанный URL-адрес? На каких языках можно создавать подписи?
Подписанные URL-адреса представляют собой механизм аутентификации на базе алгоритма безопасного хэширования SHA-256 или URI. Сведения о том, как toogenerate собственные подписи в узел, PHP, Java и C\#, в разделе hello [подписей общего доступа] [ Shared Access Signatures] статьи.

## <a name="subscription-and-namespace-management"></a>Управление подпиской и пространством имен
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Как перенести имен tooanother подписки Azure?

Можно переместить пространство имен из tooanother одной подписки Azure, используя либо hello [портал Azure](https://portal.azure.com) или команд PowerShell. В порядке tooexecute hello операции hello пространство имен уже должна быть активной. Hello пользователь, выполняющий hello команды необходимо иметь права администратора на обоих hello источника и целевой подписки.

#### <a name="portal"></a>Microsoft Azure

hello toouse подписки tooanother пространства имен служебной шины Azure toomigrate портала, следуйте приведенным инструкциям hello [здесь](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Hello следующую последовательность команд PowerShell перемещает пространства имен из одной подписки Azure tooanother. tooexecute этой операции hello пространство имен уже должна быть активной, hello пользователя, выполнение команд PowerShell hello должен быть администратором на hello исходная и целевая подписки.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о Service Bus см. следующие разделы hello.

* [Introducing Azure Service Bus Premium Messaging](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/) (Общие сведения об обмене сообщениями через служебную шину Azure уровня "Премиум") (запись блога)
* [Introducing Azure Service Bus Premium Messaging](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging) (Общие сведения об обмене сообщениями через служебную шину Azure уровня "Премиум") (Channel9)
* [Обзор служебной шины](service-bus-messaging-overview.md)
* [Обзор архитектуры служебной шины Azure](service-bus-fundamentals-hybrid-solutions.md)
* [Начало работы с очередями служебной шины](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
