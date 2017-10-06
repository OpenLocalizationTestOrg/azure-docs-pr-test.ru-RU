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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="d2119-103">Как toouse Service Bus разделов и подписок с Python</span><span class="sxs-lookup"><span data-stu-id="d2119-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="d2119-104">В этой статье описывается как toouse Service Bus разделы и подписки.</span><span class="sxs-lookup"><span data-stu-id="d2119-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="d2119-105">Hello примеры написаны на Python и использовать hello [пакета SDK для Python Azure][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="d2119-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="d2119-106">Hello сценарии включают **создания разделов и подписок**, **создание фильтров подписок**, **отправки темы о сообщениях tooa**, **получения сообщения из подписки**, и **удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="d2119-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="d2119-107">Дополнительные сведения о разделах и подписках см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="d2119-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="d2119-108">Если требуется tooinstall Python или hello [пакета Azure Python][Azure Python package], разделе hello [руководство по установке Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="d2119-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="d2119-109">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="d2119-109">Create a topic</span></span>
<span data-ttu-id="d2119-110">Hello **ServiceBusService** позволяет toowork с разделами.</span><span class="sxs-lookup"><span data-stu-id="d2119-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="d2119-111">Добавьте следующее hello верхней hello любого файла Python, в котором вы хотите tooprogrammatically доступа служебной шины:</span><span class="sxs-lookup"><span data-stu-id="d2119-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="d2119-112">Hello следующий код создает **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="d2119-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="d2119-113">Замените `mynamespace`, `sharedaccesskeyname` и `sharedaccesskey` своим пространством имен, именем и значением ключа подписанного URL-адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="d2119-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="d2119-114">Можно получить hello значения для имени ключа SAS hello и значению hello [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d2119-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="d2119-115">Hello `create_topic` метод также поддерживает дополнительные параметры, позволяющие toooverride исходные разделе параметры, такие как размер раздела toolive или максимального времени сообщения.</span><span class="sxs-lookup"><span data-stu-id="d2119-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="d2119-116">Hello следующий пример задает размер too5 hello максимальное число разделов ГБ и значение времени toolive (TTL) — 1 минута.</span><span class="sxs-lookup"><span data-stu-id="d2119-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="d2119-117">Создание подписок</span><span class="sxs-lookup"><span data-stu-id="d2119-117">Create subscriptions</span></span>
<span data-ttu-id="d2119-118">Tootopics подписки также создаются с hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="d2119-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="d2119-119">Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий набор hello сообщения, доставленные toohello в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="d2119-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="d2119-120">Подписки являются постоянными и продолжится до либо они tooexist или hello toowhich разделе они подписаны, удаляются.</span><span class="sxs-lookup"><span data-stu-id="d2119-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="d2119-121">Создайте подписку с фильтром (MatchAll) по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="d2119-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="d2119-122">Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки.</span><span class="sxs-lookup"><span data-stu-id="d2119-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="d2119-123">Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки hello.</span><span class="sxs-lookup"><span data-stu-id="d2119-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="d2119-124">Hello следующий пример создает подписку с именем `AllMessages` и использует hello по умолчанию **MatchAll** фильтра.</span><span class="sxs-lookup"><span data-stu-id="d2119-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="d2119-125">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="d2119-125">Create subscriptions with filters</span></span>
<span data-ttu-id="d2119-126">Также можно определить фильтры, позволяющие toospecify сообщений отправила разделе tooa должно отображаться в рамках подписки определенный раздел.</span><span class="sxs-lookup"><span data-stu-id="d2119-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="d2119-127">Hello самый гибкий тип фильтра, поддерживаемых подписок — **SqlFilter**, который реализует подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="d2119-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="d2119-128">Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello.</span><span class="sxs-lookup"><span data-stu-id="d2119-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="d2119-129">Дополнительные сведения о выражениях hello, которые могут использоваться с фильтром SQL см. в разделе hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="d2119-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="d2119-130">Можно добавить фильтры tooa подписки с помощью hello **создания\_правило** метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="d2119-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="d2119-131">Этот метод позволяет tooadd новые фильтры tooan существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="d2119-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d2119-132">Так как автоматически применяется фильтр по умолчанию hello tooall новых подписок, необходимо сначала удалить фильтр по умолчанию hello или hello **MatchAll** переопределит все фильтры, можно указать.</span><span class="sxs-lookup"><span data-stu-id="d2119-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="d2119-133">Правило по умолчанию hello можно удалить с помощью hello `delete_rule` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="d2119-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="d2119-134">Hello следующий пример создает подписку с именем `HighMessages` с **SqlFilter** , выбирает только сообщения, которые содержат пользовательского `messagenumber` свойство больше 3:</span><span class="sxs-lookup"><span data-stu-id="d2119-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="d2119-135">Аналогичным образом hello следующий пример создает подписку с именем `LowMessages` с **SqlFilter** , выбирает только сообщения, которые содержат `messagenumber` свойства меньше или равно too3:</span><span class="sxs-lookup"><span data-stu-id="d2119-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="d2119-136">Теперь, когда сообщение отправляется слишком`mytopic` всегда доставляется подписана tooreceivers toohello **AllMessages** подписки раздела и выборочно доставленный tooreceivers подписка toohello **HighMessages**  и **LowMessages** подписок раздела (в зависимости от содержимого сообщения hello).</span><span class="sxs-lookup"><span data-stu-id="d2119-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="d2119-137">Отправить tooa темы о сообщениях</span><span class="sxs-lookup"><span data-stu-id="d2119-137">Send messages tooa topic</span></span>
<span data-ttu-id="d2119-138">toosend раздела Service Bus tooa сообщения, приложение должно использовать hello `send_topic_message` метод hello **ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="d2119-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="d2119-139">Hello следующий пример демонстрирует способ тестирования toosend пяти сообщений слишком`mytopic`.</span><span class="sxs-lookup"><span data-stu-id="d2119-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="d2119-140">Обратите внимание, что hello `messagenumber` зависит от значения свойства каждого сообщения hello итерацию цикла hello (этим определяется, какие подписки получают его):</span><span class="sxs-lookup"><span data-stu-id="d2119-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="d2119-141">Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="d2119-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="d2119-142">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="d2119-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="d2119-143">Нет ограничений на hello количество сообщений, которые содержатся в разделе, но отсутствует ограничение на общий размер сообщений hello, удерживаемые раздела hello.</span><span class="sxs-lookup"><span data-stu-id="d2119-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="d2119-144">Этот размер раздела определяется при создании с верхним пределом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="d2119-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="d2119-145">Дополнительные сведения о квотах см. в статье [Квоты на служебную шину][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="d2119-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="d2119-146">Получение сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="d2119-146">Receive messages from a subscription</span></span>
<span data-ttu-id="d2119-147">Сообщения принимаются из подписки с помощью hello `receive_subscription_message` метод hello **ServiceBusService** объекта:</span><span class="sxs-lookup"><span data-stu-id="d2119-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="d2119-148">Сообщения удаляются из подписки hello, как они при чтении, если параметр hello `peek_lock` задано слишком**False**.</span><span class="sxs-lookup"><span data-stu-id="d2119-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="d2119-149">Можно читать (Просмотр) и заблокировать приветственное сообщение не удаляется из очереди hello параметром задание hello `peek_lock` слишком**True**.</span><span class="sxs-lookup"><span data-stu-id="d2119-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="d2119-150">Здравствуйте поведение чтение и удаление приветственное сообщение, как часть hello операции получения hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="d2119-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="d2119-151">toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="d2119-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="d2119-152">Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="d2119-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="d2119-153">Если hello `peek_lock` параметра установлено слишком**True**, получать hello становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="d2119-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="d2119-154">Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d2119-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="d2119-155">После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова `delete` метод hello **сообщение** объекта.</span><span class="sxs-lookup"><span data-stu-id="d2119-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="d2119-156">Hello `delete` метод помечает приветственное сообщение как полученное и удаляет его из подписки hello.</span><span class="sxs-lookup"><span data-stu-id="d2119-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="d2119-157">Как происходит сбой toohandle приложения и может быть прочитан сообщений</span><span class="sxs-lookup"><span data-stu-id="d2119-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="d2119-158">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="d2119-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="d2119-159">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlock` метод hello **сообщение** объекта.</span><span class="sxs-lookup"><span data-stu-id="d2119-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="d2119-160">Это сообщение hello toounlock Service Bus в рамках подписки hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="d2119-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="d2119-161">Также существует время ожидания, связанные с сообщением, заблокировать в течение hello подписки, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), а затем Service Bus разблокирует сообщение hello автоматически и делает ее доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="d2119-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="d2119-162">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `delete` вызывается метод, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d2119-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="d2119-163">Это часто называется *по крайней мере после обработки*, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="d2119-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="d2119-164">Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="d2119-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="d2119-165">Это можно сделать с помощью hello **MessageId** свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="d2119-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="d2119-166">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="d2119-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="d2119-167">Разделы и подписки являются постоянными, а должен быть явно удалены, либо через hello [портал Azure] [ Azure portal] или программными средствами.</span><span class="sxs-lookup"><span data-stu-id="d2119-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="d2119-168">Hello следующем примере показано, как toodelete hello раздел с именем `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="d2119-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="d2119-169">При удалении раздела также удаляются все подписки, которые зарегистрированы в разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d2119-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="d2119-170">Подписки также можно удалять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="d2119-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="d2119-171">Hello следующий код показывает, как toodelete подписки именоваться `HighMessages` из hello `mytopic` раздела:</span><span class="sxs-lookup"><span data-stu-id="d2119-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="d2119-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2119-172">Next steps</span></span>
<span data-ttu-id="d2119-173">Теперь, когда вы узнали основы hello разделов Service Bus, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="d2119-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="d2119-174">Дополнительные сведения см. в статье [Очереди, разделы и подписки служебной шины][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="d2119-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="d2119-175">Справочник по [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="d2119-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
