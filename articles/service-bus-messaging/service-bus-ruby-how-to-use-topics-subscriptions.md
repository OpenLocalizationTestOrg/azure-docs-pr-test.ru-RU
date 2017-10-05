---
title: "Использование разделов служебной шины (Ruby) | Документация Майкрософт"
description: "Узнайте, как использовать разделы и подписки служебной шины в Azure. Примеры кода написаны для приложений Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 4a4c9949843b16ae6be2f516de4fd1e3f7415959
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="7268c-104">Как использовать разделы и подписки служебной шины с Ruby</span><span class="sxs-lookup"><span data-stu-id="7268c-104">How to use Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="7268c-105">В этой статье показано, как использовать разделы и подписки служебной шины в приложениях Ruby.</span><span class="sxs-lookup"><span data-stu-id="7268c-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="7268c-106">В этой статье описаны такие сценарии, как **создание разделов и подписок, создание фильтров подписок, отправка сообщений** в раздел, **получение сообщений из подписки** и **удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="7268c-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="7268c-107">Дополнительные сведения о разделах и подписках см. в разделе [Дальнейшие действия](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="7268c-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="7268c-108">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="7268c-108">Create a topic</span></span>
<span data-ttu-id="7268c-109">Объект **Azure::ServiceBusService** позволяет работать с разделами.</span><span class="sxs-lookup"><span data-stu-id="7268c-109">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="7268c-110">Следующий код создает объект **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="7268c-110">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7268c-111">Чтобы создать раздел, используйте метод `create_topic()`.</span><span class="sxs-lookup"><span data-stu-id="7268c-111">To create a topic, use the `create_topic()` method.</span></span> <span data-ttu-id="7268c-112">В следующем примере создается раздел или выводятся возникающие ошибки.</span><span class="sxs-lookup"><span data-stu-id="7268c-112">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="7268c-113">Также можно передать объект **Azure::ServiceBus::Topic** с дополнительными параметрами, которые позволяют переопределить параметры раздела по умолчанию, например срок жизни сообщения или максимальный размер очереди.</span><span class="sxs-lookup"><span data-stu-id="7268c-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="7268c-114">В следующем примере показано, как установить максимальный размер очереди 5 ГБ и срок жизни в 1 минуту.</span><span class="sxs-lookup"><span data-stu-id="7268c-114">The following example shows setting the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="7268c-115">Создание подписок</span><span class="sxs-lookup"><span data-stu-id="7268c-115">Create subscriptions</span></span>
<span data-ttu-id="7268c-116">Подписки разделов также создаются с помощью объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="7268c-116">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7268c-117">Подписки имеют имена и могут использовать дополнительный фильтр, который ограничивает набор сообщений, доставляемых в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="7268c-117">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="7268c-118">Подписки являются постоянными и продолжают существовать либо до их удаления, либо до удаления раздела, с которым они связаны.</span><span class="sxs-lookup"><span data-stu-id="7268c-118">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="7268c-119">Если приложение содержит логику для создания подписки, оно сначала должно проверить, существует ли подписка, используя метод getSubscription.</span><span class="sxs-lookup"><span data-stu-id="7268c-119">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="7268c-120">Создание подписки с фильтром по умолчанию (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="7268c-120">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="7268c-121">Фильтр **MatchAll** является фильтром по умолчанию, используемым, если при создании новой подписки не указан фильтр.</span><span class="sxs-lookup"><span data-stu-id="7268c-121">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="7268c-122">Если используется фильтр **MatchAll**, то все сообщения, опубликованные в разделе, помещаются в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="7268c-122">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="7268c-123">В следующем примере создается подписка с именем "all-messages" и используется фильтр по умолчанию **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="7268c-123">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="7268c-124">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="7268c-124">Create subscriptions with filters</span></span>
<span data-ttu-id="7268c-125">Можно также задавать фильтры, позволяющие определять, какие посылаемые в раздел сообщения должны отображаться в рамках конкретной подписки.</span><span class="sxs-lookup"><span data-stu-id="7268c-125">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="7268c-126">Самый гибкий тип фильтра, который поддерживается подписками, — это **Azure::ServiceBus::SqlFilter**, реализующий подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="7268c-126">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="7268c-127">Фильтры SQL работают со свойствами сообщений, которые опубликованы в разделе.</span><span class="sxs-lookup"><span data-stu-id="7268c-127">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="7268c-128">Дополнительные сведения о выражениях, которые можно использовать с фильтром SQL, см. в описании синтаксиса [SqlFilter](service-bus-messaging-sql-filter.md).</span><span class="sxs-lookup"><span data-stu-id="7268c-128">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="7268c-129">Фильтры можно добавить в подписку с помощью метода `create_rule()` объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="7268c-129">You can add filters to a subscription by using the `create_rule()` method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7268c-130">Этот метод позволяет добавлять новые фильтры в существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="7268c-130">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="7268c-131">Так как ко всем новым подпискам автоматически применяется фильтр по умолчанию, сначала необходимо удалить фильтр по умолчанию, иначе **MatchAll** будет действовать вместо любых других заданных фильтров.</span><span class="sxs-lookup"><span data-stu-id="7268c-131">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="7268c-132">Вы можете удалить правило по умолчанию с помощью метода `delete_rule()` объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="7268c-132">You can remove the default rule by using the `delete_rule()` method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="7268c-133">В приведенном ниже примере создается подписка high-messages с фильтром **Azure::ServiceBus::SqlFilter**, который выбирает только те сообщения, значение настраиваемого свойства `message_number` которых больше 3.</span><span class="sxs-lookup"><span data-stu-id="7268c-133">The following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="7268c-134">Аналогичным образом в следующем примере создается подписка `low-messages` с фильтром **Azure::ServiceBus::SqlFilter**, который выбирает только те сообщения, значение свойства `message_number` которых меньше или равно 3.</span><span class="sxs-lookup"><span data-stu-id="7268c-134">Similarly, the following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal to 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="7268c-135">Если сообщение отправляется в раздел `test-topic`, оно всегда будет доставляться в приемники, подписанные на подписку раздела `all-messages`, и в отдельные приемники, подписанные на подписки разделов `high-messages` и `low-messages` (в зависимости от содержимого сообщения).</span><span class="sxs-lookup"><span data-stu-id="7268c-135">When a message is now sent to `test-topic`, it is always be delivered to receivers subscribed to the `all-messages` topic subscription, and selectively delivered to receivers subscribed to the `high-messages` and `low-messages` topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="7268c-136">Отправка сообщений в раздел</span><span class="sxs-lookup"><span data-stu-id="7268c-136">Send messages to a topic</span></span>
<span data-ttu-id="7268c-137">Чтобы отправить сообщение в раздел служебной шины, приложение должно использовать метод `send_topic_message()` объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="7268c-137">To send a message to a Service Bus topic, your application must use the `send_topic_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7268c-138">Сообщения, отправленные в разделы служебной шины, представляют собой экземпляры объектов **Azure::ServiceBus::BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="7268c-138">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="7268c-139">Объекты **Azure::ServiceBus::BrokeredMessage** содержат набор стандартных свойств (например, `label` и `time_to_live`), словарь, используемый для хранения настраиваемых свойств приложения, и текст из строковых данных.</span><span class="sxs-lookup"><span data-stu-id="7268c-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="7268c-140">Приложение может задавать текст сообщения, передавая строковое значение в метод `send_topic_message()`, и все обязательные стандартные свойства будут заполнены значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7268c-140">An application can set the body of the message by passing a string value to the `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="7268c-141">В следующем примере показано, как отправить пять тестовых сообщений в `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="7268c-141">The following example demonstrates how to send five test messages to `test-topic`.</span></span> <span data-ttu-id="7268c-142">Обратите внимание, что значение настраиваемого свойства `message_number` каждого сообщения зависит от итерации цикла (определяет подписку, которая получит это сообщение).</span><span class="sxs-lookup"><span data-stu-id="7268c-142">Note that the `message_number` custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="7268c-143">Разделы служебной шины поддерживают максимальный размер сообщения 256 КБ для [уровня "Стандартный"](service-bus-premium-messaging.md) и 1 МБ для [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="7268c-143">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="7268c-144">Максимальный размер заголовка, который содержит стандартные и настраиваемые свойства приложения, — 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="7268c-144">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="7268c-145">Ограничения на количество сообщений в разделе нет, но есть максимальный общий размер сообщений, содержащихся в разделе.</span><span class="sxs-lookup"><span data-stu-id="7268c-145">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="7268c-146">Этот размер раздела определяется при создании с верхним пределом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="7268c-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="7268c-147">Получение сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="7268c-147">Receive messages from a subscription</span></span>
<span data-ttu-id="7268c-148">Сообщения извлекаются из подписки с помощью метода `receive_subscription_message()` объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="7268c-148">Messages are received from a subscription using the `receive_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7268c-149">По умолчанию сообщения считываются (просматриваются) и блокируются без удаления из подписки.</span><span class="sxs-lookup"><span data-stu-id="7268c-149">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="7268c-150">Сообщения можно считывать и удалять из подписки, установив для параметра `peek_lock` значение **false**.</span><span class="sxs-lookup"><span data-stu-id="7268c-150">You can read and delete the message from the subscription by setting the `peek_lock` option to **false**.</span></span>

<span data-ttu-id="7268c-151">По умолчанию чтение и удаление выполняются в два этапа, что позволяет поддерживать приложения, не способные обрабатывать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="7268c-151">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="7268c-152">Получив запрос, служебная шина находит следующее сообщение, блокирует его, чтобы предотвратить его получение другими получателями, и возвращает его приложению.</span><span class="sxs-lookup"><span data-stu-id="7268c-152">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="7268c-153">Обработав сообщение (или сохранив его в надежном месте для последующей обработки), приложение вызывает метод `delete_subscription_message()` и указывает сообщение, которое будет удалено как параметр, таким образом завершая второй этап процесса получения.</span><span class="sxs-lookup"><span data-stu-id="7268c-153">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_subscription_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="7268c-154">Метод `delete_subscription_message()` помечает сообщение как использованное и удаляет его из подписки.</span><span class="sxs-lookup"><span data-stu-id="7268c-154">The `delete_subscription_message()` method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="7268c-155">Если параметр `:peek_lock` имеет значение **false**, чтение и удаление сообщения осуществляется очень просто. Этот метод оптимально подходит для сценариев, в которых приложение может пропустить обработку сообщения без последствий в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="7268c-155">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="7268c-156">Чтобы это понять, рассмотрим сценарий, в котором объект-получатель выдает запрос на получение и выходит из строя до его обработки.</span><span class="sxs-lookup"><span data-stu-id="7268c-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="7268c-157">Поскольку служебная шина помечает сообщение как использованное, то когда после своего перезапуска приложение снова начнет обрабатывать сообщения, оно пропустит сообщение, использованное до сбоя.</span><span class="sxs-lookup"><span data-stu-id="7268c-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="7268c-158">В следующем примере показано, как получать и обрабатывать сообщения с помощью метода `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="7268c-158">The following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="7268c-159">В примере сначала поступает и удаляется сообщение из подписки `low-messages` с помощью метода `:peek_lock`, для которого задано значение **false**, затем поступает другое сообщение из подписки `high-messages` и удаляется с помощью метода `delete_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="7268c-159">The example first receives and deletes a message from the `low-messages` subscription by using `:peek_lock` set to **false**, then it receives another message from the `high-messages` and then deletes the message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="7268c-160">Как обрабатывать сбои приложения и нечитаемые сообщения</span><span class="sxs-lookup"><span data-stu-id="7268c-160">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="7268c-161">служебная шина предоставляет функции, помогающие корректно выполнить восстановление после ошибок в приложении или трудностей, возникших при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="7268c-161">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="7268c-162">Если по какой-либо причине приложению-получателю не удается обработать сообщение, оно вызывает метод `unlock_subscription_message()` для объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="7268c-162">If a receiver application is unable to process the message for some reason, then it can call the `unlock_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7268c-163">После этого служебная шина разблокирует сообщение в подписке и снова сделает его доступным для получения тем же или другим приложением.</span><span class="sxs-lookup"><span data-stu-id="7268c-163">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="7268c-164">Кроме того, с сообщением, заблокированным в подписке, связано время ожидания. Если приложение не сможет обработать сообщение в течение времени ожидания (например, при сбое приложения), служебная шина автоматически разблокирует сообщение и сделает его доступным для повторного приема.</span><span class="sxs-lookup"><span data-stu-id="7268c-164">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="7268c-165">Если в приложении происходит сбой после обработки сообщения, но перед вызовом метода `delete_subscription_message()`, сообщение будет повторно доставлено в приложение после его перезапуска.</span><span class="sxs-lookup"><span data-stu-id="7268c-165">In the event that the application crashes after processing the message but before the `delete_subscription_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="7268c-166">Часто этот подход называют *обработать хотя бы один раз*, т. е. каждое сообщение будет обрабатываться по крайней мере один раз, но в некоторых случаях это же сообщение может быть доставлено повторно.</span><span class="sxs-lookup"><span data-stu-id="7268c-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="7268c-167">Если повторная обработка недопустима, разработчики приложения должны добавить дополнительную логику для обработки повторной доставки сообщений.</span><span class="sxs-lookup"><span data-stu-id="7268c-167">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="7268c-168">Часто это реализуется с помощью свойства `message_id` сообщения, которое остается постоянным для различных попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="7268c-168">This logic is often achieved using the `message_id` property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="7268c-169">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="7268c-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="7268c-170">Разделы и подписки хранятся постоянно, и их нужно удалять явным образом на [портале Azure][Azure portal] или с помощью программных средств.</span><span class="sxs-lookup"><span data-stu-id="7268c-170">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="7268c-171">В приведенном ниже примере показано, как удалить раздел с именем `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="7268c-171">The example below demonstrates how to delete the topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="7268c-172">При удалении раздела также удаляются все подписки, зарегистрированные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="7268c-172">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="7268c-173">Подписки также можно удалять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="7268c-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="7268c-174">В следующем примере кода показано, как удалить подписку с именем `high-messages` из раздела `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="7268c-174">The following code demonstrates how to delete the subscription named `high-messages` from the `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="7268c-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7268c-175">Next steps</span></span>
<span data-ttu-id="7268c-176">Вы узнали основные сведения о разделах служебной шины. Для получения дополнительных сведений используйте следующие ссылки.</span><span class="sxs-lookup"><span data-stu-id="7268c-176">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="7268c-177">См. статью [Очереди, разделы и подписки](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="7268c-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="7268c-178">Справочник API для [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="7268c-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="7268c-179">Посетите репозиторий [Azure SDK для Ruby](https://github.com/Azure/azure-sdk-for-ruby) на веб-сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="7268c-179">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
