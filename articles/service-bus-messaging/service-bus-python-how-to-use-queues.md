---
title: "Помещает в очередь aaaHow toouse Azure Service Bus с Python | Документы Microsoft"
description: "Узнайте, как очереди toouse Azure служебной шины из Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a>Как очереди toouse Service Bus с Python

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

В этой статье описывается как toouse очереди Service Bus. Hello примеры написаны на Python и использовать hello [пакета Python Azure Service Bus][Python Azure Service Bus package]. Hello сценарии включают **создание очередей, отправки и получения сообщений**, и **удаление очередей**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> tooinstall Python или hello [пакета Python Azure Service Bus][Python Azure Service Bus package], в разделе hello [руководство по установке Python](../python-how-to-install.md).
> 
> 

## <a name="create-a-queue"></a>Создание очереди
Hello **ServiceBusService** позволяет toowork с очередями. Добавьте hello после кода верхней hello любого файла Python, в котором вы хотите tooprogrammatically доступа служебной шины:

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

Hello следующий код создает **ServiceBusService** объекта. Замените `mynamespace`, `sharedaccesskeyname` и `sharedaccesskey` своим пространством имен, именем и значением ключа подписанного URL-адреса (SAS).

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Hello значения для имени ключа SAS hello и значения можно найти в hello [портал Azure] [ Azure portal] сведения о соединении, или в Visual Studio hello **свойства** панели при выборе Здравствуйте пространства имен шины обслуживания в обозревателе серверов (как показано в предыдущем разделе hello).

```python
bus_service.create_queue('taskqueue')
```

Hello `create_queue` метод также поддерживает дополнительные параметры, позволяющие toooverride параметры очереди по умолчанию сообщения времени toolive (TTL) или максимальный размер очереди. Hello следующий пример задает hello максимальный размер too5 ГБ и hello TTL значение too1 минут:

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>Отправка сообщений в очереди tooa
toosend очередью сообщений tooa Service Bus, приложение вызывает hello `send_queue_message` метод hello **ServiceBusService** объекта.

Hello следующем примере показано, как toosend toohello очереди сообщений теста именоваться `taskqueue` с помощью `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello. Этот размер очереди, определяемый в момент ее создания, не должен превышать 5 ГБ. Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Получение сообщений из очереди
Сообщения принимаются из очереди с помощью hello `receive_queue_message` метод hello **ServiceBusService** объекта:

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

Сообщения удаляются из очереди hello, как они при чтении, если параметр hello `peek_lock` задано слишком**False**. Можно читать (Просмотр) и заблокировать приветственное сообщение не удаляется из очереди hello параметром задание hello `peek_lock` слишком**True**.

Здравствуйте поведение чтение и удаление приветственное сообщение, как часть hello операции получения hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

Если hello `peek_lock` параметра установлено слишком**True**, получать hello становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова hello **удалить** метод hello **сообщения** объекта. Hello **удалить** метод будет пометить приветственное сообщение как полученное и удалите его из очереди hello.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Как происходит сбой toohandle приложения и может быть прочитан сообщений
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello **разблокировать** метод hello **сообщение** объекта. Это будет вызвать Service Bus toounlock приветственное сообщение в очередь hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.

Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess hello сообщение перед hello срок блокировки (например, если приложение hello терпит сбой), то служебной шины будет автоматическую разблокировку приветственное сообщение и сделать ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello **удалить** вызывается метод, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения. Это часто называется **по крайней мере после обработки**, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений. Это можно сделать с помощью hello **MessageId** свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы изучили основы hello очередей Service Bus, см. Эти дополнительные toolearn статей.

* [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

