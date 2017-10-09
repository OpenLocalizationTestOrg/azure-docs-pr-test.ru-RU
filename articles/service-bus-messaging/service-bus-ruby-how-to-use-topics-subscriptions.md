---
title: "темы Service Bus toouse aaaHow (Ruby) | Документы Microsoft"
description: "Узнайте, как toouse Service Bus разделы и подписки в Azure. Примеры кода написаны для приложений Ruby."
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
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="e7c1a-104">Как toouse Service Bus разделов и подписок с Ruby</span><span class="sxs-lookup"><span data-stu-id="e7c1a-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="e7c1a-105">В этой статье описывается как toouse Service Bus разделов и подписок из приложений Ruby.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="e7c1a-106">Hello сценарии включают **создания разделов и подписок, создание фильтров подписку, отправляя сообщения** разделе tooa **получения сообщений из подписки**, и  **Удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="e7c1a-107">Дополнительные сведения о разделах и подписках см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="e7c1a-108">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="e7c1a-108">Create a topic</span></span>
<span data-ttu-id="e7c1a-109">Hello **Azure::ServiceBusService** позволяет toowork с разделами.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="e7c1a-110">Hello следующий код создает **Azure::ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="e7c1a-111">toocreate разделом, использовать hello `create_topic()` метод.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="e7c1a-112">Следующий пример Hello создает раздел или выводит hello ошибки, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="e7c1a-113">Можно также передать **Azure::ServiceBus::Topic** объекта с дополнительными параметрами, позволяющие toooverride исходные разделе параметры, такие как очереди toolive или максимальный размер сообщения времени.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="e7c1a-114">Hello в следующем примере параметр Максимальное очереди hello размером too5 ГБ и время toolive too1 минуту:</span><span class="sxs-lookup"><span data-stu-id="e7c1a-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="e7c1a-115">Создание подписок</span><span class="sxs-lookup"><span data-stu-id="e7c1a-115">Create subscriptions</span></span>
<span data-ttu-id="e7c1a-116">Подписок раздела также создаются с hello **Azure::ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="e7c1a-117">Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий набор hello сообщения, доставленные toohello в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="e7c1a-118">Подписки являются постоянными и продолжится до либо они tooexist или hello раздел они связаны, будут удалены.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="e7c1a-119">Если приложение содержит логику toocreate подписки, он должен сначала проверяет, существует ли hello подписка уже с помощью метода getSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="e7c1a-120">Создайте подписку с фильтром (MatchAll) по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="e7c1a-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="e7c1a-121">Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="e7c1a-122">Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки hello.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="e7c1a-123">Hello следующем примере создается подписка с именем «все сообщения» и использует hello по умолчанию **MatchAll** фильтра.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="e7c1a-124">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="e7c1a-124">Create subscriptions with filters</span></span>
<span data-ttu-id="e7c1a-125">Также можно определить фильтры, позволяющие toospecify сообщений отправила разделе tooa должно отображаться в конкретной подписки.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="e7c1a-126">Hello самый гибкий тип фильтра, поддерживаемых подписок — hello **Azure::ServiceBus::SqlFilter**, который реализует подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="e7c1a-127">Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="e7c1a-128">Дополнительные сведения о выражениях hello, которые могут использоваться с фильтром SQL просмотрите hello [SqlFilter](service-bus-messaging-sql-filter.md) синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="e7c1a-129">Можно добавить фильтры tooa подписки с помощью hello `create_rule()` метод hello **Azure::ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="e7c1a-130">Этот метод позволяет tooadd новые фильтры tooan существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="e7c1a-131">Так как автоматически применяется фильтр по умолчанию hello tooall новых подписках, сначала необходимо удалить фильтр по умолчанию hello или hello **MatchAll** переопределит все фильтры, можно указать.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="e7c1a-132">Правило по умолчанию hello можно удалить с помощью hello `delete_rule()` метод hello **Azure::ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="e7c1a-133">Hello следующий пример создает подписку с именем «высокой сообщений» **Azure::ServiceBus::SqlFilter** , выбирает только сообщения, которые содержат пользовательского `message_number` свойство больше 3:</span><span class="sxs-lookup"><span data-stu-id="e7c1a-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="e7c1a-134">Аналогичным образом hello следующий пример создает подписку с именем `low-messages` с **Azure::ServiceBus::SqlFilter** , выбирает только сообщения, которые содержат `message_number` свойства меньше или равно too3:</span><span class="sxs-lookup"><span data-stu-id="e7c1a-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

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

<span data-ttu-id="e7c1a-135">Если теперь отправляется сообщение слишком`test-topic`, это всегда быть toohello доставленный tooreceivers подписка `all-messages` подписки раздела и выборочно доставленный tooreceivers подписка toohello `high-messages` и `low-messages` (подписки) раздела зависимости от содержимого сообщения hello).</span><span class="sxs-lookup"><span data-stu-id="e7c1a-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="e7c1a-136">Отправить tooa темы о сообщениях</span><span class="sxs-lookup"><span data-stu-id="e7c1a-136">Send messages tooa topic</span></span>
<span data-ttu-id="e7c1a-137">toosend раздела Service Bus tooa сообщения, приложение должно использовать hello `send_topic_message()` метод hello **Azure::ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="e7c1a-138">Сообщения отправляются разделы шины tooService являются экземплярами hello **Azure::ServiceBus::BrokeredMessage** объектов.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="e7c1a-139">**Azure::ServiceBus::BrokeredMessage** объекты имеют набор стандартных свойств (например, `label` и `time_to_live`), словаря, используемые toohold пользовательские свойства для конкретного приложения и текст строки данных.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="e7c1a-140">Приложение может установить текст hello приветственное сообщение, передав значение строки toohello `send_topic_message()` метод и все обязательные, стандартные свойства заполняются значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="e7c1a-141">Hello следующий пример демонстрирует способ тестирования toosend пяти сообщений слишком`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="e7c1a-142">Обратите внимание, что hello `message_number` изменяется значение настраиваемого свойства каждого сообщения hello итерацию цикла hello (этим определяется, какая подписка получит его):</span><span class="sxs-lookup"><span data-stu-id="e7c1a-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="e7c1a-143">Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="e7c1a-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="e7c1a-144">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="e7c1a-145">Нет ограничений на hello количество сообщений, которые содержатся в разделе, но отсутствует ограничение на общий размер сообщений hello, удерживаемые раздела hello.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="e7c1a-146">Этот размер раздела определяется при создании с верхним пределом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="e7c1a-147">Получение сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="e7c1a-147">Receive messages from a subscription</span></span>
<span data-ttu-id="e7c1a-148">Сообщения принимаются из подписки с помощью hello `receive_subscription_message()` метод hello **Azure::ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="e7c1a-149">По умолчанию сообщения read(peak) и заблокирован, не удаляя ее из подписки hello.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="e7c1a-150">Можно читать и удалять приветственное сообщение из подписки hello, установка hello `peek_lock` параметр слишком**false**.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="e7c1a-151">поведение по умолчанию Hello делает hello чтение и удаление двух шаговой операцией, который также вполне возможно toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="e7c1a-152">Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="e7c1a-153">После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова `delete_subscription_message()` метод и предоставляя toobe сообщение hello удален в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="e7c1a-154">Hello `delete_subscription_message()` метод будет пометить приветственное сообщение как полученное и удалите его из подписки hello.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="e7c1a-155">Если hello `:peek_lock` параметра установлено слишком**false**, чтение и удаление приветственное сообщение становится hello самая простая модель и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello для события Произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="e7c1a-156">toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="e7c1a-157">Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="e7c1a-158">Hello следующем примере показано, как можно получать сообщения и обработанные с помощью `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="e7c1a-159">Hello пример сначала получает и удаляет сообщение из hello `low-messages` подписки с помощью `:peek_lock` значение слишком**false**, а затем получает сообщение от hello `high-messages` и затем удаляет hello сообщения с помощью `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="e7c1a-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="e7c1a-160">Как происходит сбой toohandle приложения и может быть прочитан сообщений</span><span class="sxs-lookup"><span data-stu-id="e7c1a-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="e7c1a-161">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="e7c1a-162">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello `unlock_subscription_message()` метод hello **Azure::ServiceBusService** объекта.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="e7c1a-163">Это приводит hello toounlock Service Bus сообщение в рамках подписки hello и сделать ее доступной toobe получения, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="e7c1a-164">Также существует время ожидания, связанные с сообщением, заблокировать в течение hello подписки, и при сбое приложения hello tooprocess приветственное сообщение, прежде чем hello срок блокировки (например, если приложение hello терпит сбой), разблокируйте Service Bus приветственное сообщение автоматически и сделать ее доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="e7c1a-165">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello `delete_subscription_message()` вызывается метод, то приветственное сообщение будет повторно доставлены toohello приложения после его перезапуска.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="e7c1a-166">Это часто называется *по крайней мере после обработки*; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="e7c1a-167">Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="e7c1a-168">Эта логика часто достигается с помощью hello `message_id` свойство сообщения hello, который остается постоянным протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="e7c1a-169">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="e7c1a-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="e7c1a-170">Разделы и подписки являются постоянными, а должен быть явно удалены, либо через hello [портал Azure] [ Azure portal] или программными средствами.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="e7c1a-171">Приведенный ниже пример Hello показывает, как toodelete hello раздел с именем `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="e7c1a-172">При удалении раздела также удаляются все подписки, которые зарегистрированы в разделе hello.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="e7c1a-173">Подписки также можно удалять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="e7c1a-174">Hello следующем коде показано, как с именем подписки hello toodelete `high-messages` из hello `test-topic` раздела:</span><span class="sxs-lookup"><span data-stu-id="e7c1a-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="e7c1a-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7c1a-175">Next steps</span></span>
<span data-ttu-id="e7c1a-176">Теперь, когда вы узнали основы hello разделов Service Bus, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="e7c1a-177">См. статью [Очереди, разделы и подписки](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="e7c1a-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="e7c1a-178">Справочник API для [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="e7c1a-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="e7c1a-179">Посетите hello [пакет Azure SDK для Ruby](https://github.com/Azure/azure-sdk-for-ruby) репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="e7c1a-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
