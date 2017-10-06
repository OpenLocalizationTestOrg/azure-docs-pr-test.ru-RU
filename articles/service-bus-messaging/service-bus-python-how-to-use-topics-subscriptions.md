---
title: "разделы шины обслуживания Azure toouse aaaHow с Python | Документы Microsoft"
description: "Узнайте, как toouse Azure Service Bus разделов и подписок из Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>Как toouse Service Bus разделов и подписок с Python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

В этой статье описывается как toouse Service Bus разделы и подписки. Hello примеры написаны на Python и использовать hello [пакета SDK для Python Azure][Azure Python package]. Hello сценарии включают **создания разделов и подписок**, **создание фильтров подписок**, **отправки темы о сообщениях tooa**, **получения сообщения из подписки**, и **удаление разделов и подписок**. Дополнительные сведения о разделах и подписках см. в разделе hello [дальнейшие действия](#next-steps) раздела.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Если требуется tooinstall Python или hello [пакета Azure Python][Azure Python package], разделе hello [руководство по установке Python](../python-how-to-install.md).

## <a name="create-a-topic"></a>Создание раздела
Hello **ServiceBusService** позволяет toowork с разделами. Добавьте следующее hello верхней hello любого файла Python, в котором вы хотите tooprogrammatically доступа служебной шины:

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

Hello следующий код создает **ServiceBusService** объекта. Замените `mynamespace`, `sharedaccesskeyname` и `sharedaccesskey` своим пространством имен, именем и значением ключа подписанного URL-адреса (SAS).

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Можно получить hello значения для имени ключа SAS hello и значению hello [портал Azure][Azure portal].

```python
bus_service.create_topic('mytopic')
```

Hello `create_topic` метод также поддерживает дополнительные параметры, позволяющие toooverride исходные разделе параметры, такие как размер раздела toolive или максимального времени сообщения. Hello следующий пример задает размер too5 hello максимальное число разделов ГБ и значение времени toolive (TTL) — 1 минута.

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>Создание подписок
Tootopics подписки также создаются с hello **ServiceBusService** объекта. Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий набор hello сообщения, доставленные toohello в виртуальную очередь подписки.

> [!NOTE]
> Подписки являются постоянными и продолжится до либо они tooexist или hello toowhich разделе они подписаны, удаляются.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Создайте подписку с фильтром (MatchAll) по умолчанию hello
Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки. Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки hello. Hello следующий пример создает подписку с именем `AllMessages` и использует hello по умолчанию **MatchAll** фильтра.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>Создание подписок с фильтрами
Также можно определить фильтры, позволяющие toospecify сообщений отправила разделе tooa должно отображаться в рамках подписки определенный раздел.

Hello самый гибкий тип фильтра, поддерживаемых подписок — **SqlFilter**, который реализует подмножество SQL92. Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello. Дополнительные сведения о выражениях hello, которые могут использоваться с фильтром SQL см. в разделе hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] синтаксиса.

Можно добавить фильтры tooa подписки с помощью hello **создания\_правило** метод hello **ServiceBusService** объекта. Этот метод позволяет tooadd новые фильтры tooan существующую подписку.

> [!NOTE]
> Так как автоматически применяется фильтр по умолчанию hello tooall новых подписок, необходимо сначала удалить фильтр по умолчанию hello или hello **MatchAll** переопределит все фильтры, можно указать. Правило по умолчанию hello можно удалить с помощью hello `delete_rule` метод hello **ServiceBusService** объекта.
> 
> 

Hello следующий пример создает подписку с именем `HighMessages` с **SqlFilter** , выбирает только сообщения, которые содержат пользовательского `messagenumber` свойство больше 3:

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

Аналогичным образом hello следующий пример создает подписку с именем `LowMessages` с **SqlFilter** , выбирает только сообщения, которые содержат `messagenumber` свойства меньше или равно too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

Теперь, когда сообщение отправляется слишком`mytopic` всегда доставляется подписана tooreceivers toohello **AllMessages** подписки раздела и выборочно доставленный tooreceivers подписка toohello **HighMessages**  и **LowMessages** подписок раздела (в зависимости от содержимого сообщения hello).

## <a name="send-messages-tooa-topic"></a>Отправить tooa темы о сообщениях
toosend раздела Service Bus tooa сообщения, приложение должно использовать hello `send_topic_message` метод hello **ServiceBusService** объекта.

Hello следующий пример демонстрирует способ тестирования toosend пяти сообщений слишком`mytopic`. Обратите внимание, что hello `messagenumber` зависит от значения свойства каждого сообщения hello итерацию цикла hello (этим определяется, какие подписки получают его):

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на hello количество сообщений, которые содержатся в разделе, но отсутствует ограничение на общий размер сообщений hello, удерживаемые раздела hello. Этот размер раздела определяется при создании с верхним пределом 5 ГБ. Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Получение сообщений из подписки
Сообщения принимаются из подписки с помощью hello `receive_subscription_message` метод hello **ServiceBusService** объекта:

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

Сообщения удаляются из подписки hello, как они при чтении, если параметр hello `peek_lock` задано слишком**False**. Можно читать (Просмотр) и заблокировать приветственное сообщение не удаляется из очереди hello параметром задание hello `peek_lock` слишком**True**.

Здравствуйте поведение чтение и удаление приветственное сообщение, как часть hello операции получения hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

Если hello `peek_lock` параметра установлено слишком**True**, получать hello становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова `delete` метод hello **сообщение** объекта. Hello `delete` метод помечает приветственное сообщение как полученное и удаляет его из подписки hello.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Как происходит сбой toohandle приложения и может быть прочитан сообщений
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlock` метод hello **сообщение** объекта. Это сообщение hello toounlock Service Bus в рамках подписки hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.

Также существует время ожидания, связанные с сообщением, заблокировать в течение hello подписки, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), а затем Service Bus разблокирует сообщение hello автоматически и делает ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `delete` вызывается метод, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения. Это часто называется *по крайней мере после обработки*, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений. Это можно сделать с помощью hello **MessageId** свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.

## <a name="delete-topics-and-subscriptions"></a>Удаление разделов и подписок
Разделы и подписки являются постоянными, а должен быть явно удалены, либо через hello [портал Azure] [ Azure portal] или программными средствами. Hello следующем примере показано, как toodelete hello раздел с именем `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

При удалении раздела также удаляются все подписки, которые зарегистрированы в разделе hello. Подписки также можно удалять по отдельности. Hello следующий код показывает, как toodelete подписки именоваться `HighMessages` из hello `mytopic` раздела:

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello разделов Service Bus, выполните следующие дополнительные toolearn ссылки.

* Дополнительные сведения см. в статье [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions].
* Справочник по [SqlFilter.SqlExpression][SqlFilter.SqlExpression].

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
