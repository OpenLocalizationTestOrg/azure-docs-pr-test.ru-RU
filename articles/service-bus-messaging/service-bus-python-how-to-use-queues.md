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
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="944f0-103">Как очереди toouse Service Bus с Python</span><span class="sxs-lookup"><span data-stu-id="944f0-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="944f0-104">В этой статье описывается как toouse очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="944f0-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="944f0-105">Hello примеры написаны на Python и использовать hello [пакета Python Azure Service Bus][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="944f0-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="944f0-106">Hello сценарии включают **создание очередей, отправки и получения сообщений**, и **удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="944f0-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="944f0-107">tooinstall Python или hello [пакета Python Azure Service Bus][Python Azure Service Bus package], в разделе hello [руководство по установке Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="944f0-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="944f0-108">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="944f0-108">Create a queue</span></span>
<span data-ttu-id="944f0-109">Hello **ServiceBusService** позволяет toowork с очередями.</span><span class="sxs-lookup"><span data-stu-id="944f0-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="944f0-110">Добавьте hello после кода верхней hello любого файла Python, в котором вы хотите tooprogrammatically доступа служебной шины:</span><span class="sxs-lookup"><span data-stu-id="944f0-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="944f0-111">Hello следующий код создает **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="944f0-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="944f0-112">Замените `mynamespace`, `sharedaccesskeyname` и `sharedaccesskey` своим пространством имен, именем и значением ключа подписанного URL-адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="944f0-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="944f0-113">Hello значения для имени ключа SAS hello и значения можно найти в hello [портал Azure] [ Azure portal] сведения о соединении, или в Visual Studio hello **свойства** панели при выборе Здравствуйте пространства имен шины обслуживания в обозревателе серверов (как показано в предыдущем разделе hello).</span><span class="sxs-lookup"><span data-stu-id="944f0-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="944f0-114">Hello `create_queue` метод также поддерживает дополнительные параметры, позволяющие toooverride параметры очереди по умолчанию сообщения времени toolive (TTL) или максимальный размер очереди.</span><span class="sxs-lookup"><span data-stu-id="944f0-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="944f0-115">Hello следующий пример задает hello максимальный размер too5 ГБ и hello TTL значение too1 минут:</span><span class="sxs-lookup"><span data-stu-id="944f0-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="944f0-116">Отправка сообщений в очереди tooa</span><span class="sxs-lookup"><span data-stu-id="944f0-116">Send messages tooa queue</span></span>
<span data-ttu-id="944f0-117">toosend очередью сообщений tooa Service Bus, приложение вызывает hello `send_queue_message` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="944f0-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="944f0-118">Hello следующем примере показано, как toosend toohello очереди сообщений теста именоваться `taskqueue` с помощью `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="944f0-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="944f0-119">Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="944f0-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="944f0-120">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="944f0-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="944f0-121">Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="944f0-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="944f0-122">Этот размер очереди, определяемый в момент ее создания, не должен превышать 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="944f0-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="944f0-123">Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="944f0-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="944f0-124">Получение сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="944f0-124">Receive messages from a queue</span></span>
<span data-ttu-id="944f0-125">Сообщения принимаются из очереди с помощью hello `receive_queue_message` метод hello **ServiceBusService** объекта:</span><span class="sxs-lookup"><span data-stu-id="944f0-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="944f0-126">Сообщения удаляются из очереди hello, как они при чтении, если параметр hello `peek_lock` задано слишком**False**.</span><span class="sxs-lookup"><span data-stu-id="944f0-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="944f0-127">Можно читать (Просмотр) и заблокировать приветственное сообщение не удаляется из очереди hello параметром задание hello `peek_lock` слишком**True**.</span><span class="sxs-lookup"><span data-stu-id="944f0-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="944f0-128">Здравствуйте поведение чтение и удаление приветственное сообщение, как часть hello операции получения hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="944f0-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="944f0-129">toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="944f0-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="944f0-130">Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="944f0-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="944f0-131">Если hello `peek_lock` параметра установлено слишком**True**, получать hello становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="944f0-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="944f0-132">Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="944f0-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="944f0-133">После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова hello **удалить** метод hello **сообщения** объекта.</span><span class="sxs-lookup"><span data-stu-id="944f0-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="944f0-134">Hello **удалить** метод будет пометить приветственное сообщение как полученное и удалите его из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="944f0-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="944f0-135">Как происходит сбой toohandle приложения и может быть прочитан сообщений</span><span class="sxs-lookup"><span data-stu-id="944f0-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="944f0-136">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="944f0-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="944f0-137">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello **разблокировать** метод hello **сообщение** объекта.</span><span class="sxs-lookup"><span data-stu-id="944f0-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="944f0-138">Это будет вызвать Service Bus toounlock приветственное сообщение в очередь hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="944f0-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="944f0-139">Также существует время ожидания, связанные с сообщением, заблокировать в течение hello очереди, и при сбое приложения hello tooprocess hello сообщение перед hello срок блокировки (например, если приложение hello терпит сбой), то служебной шины будет автоматическую разблокировку приветственное сообщение и сделать ее доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="944f0-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="944f0-140">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello **удалить** вызывается метод, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="944f0-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="944f0-141">Это часто называется **по крайней мере после обработки**, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="944f0-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="944f0-142">Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="944f0-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="944f0-143">Это можно сделать с помощью hello **MessageId** свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="944f0-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="944f0-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="944f0-144">Next steps</span></span>
<span data-ttu-id="944f0-145">Теперь, когда вы изучили основы hello очередей Service Bus, см. Эти дополнительные toolearn статей.</span><span class="sxs-lookup"><span data-stu-id="944f0-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="944f0-146">[Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="944f0-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

