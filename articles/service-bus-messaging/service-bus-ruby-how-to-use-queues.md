---
title: "Использование очередей служебной шины Azure с Ruby | Документация Майкрософт"
description: "Узнайте, как использовать очереди служебной шины в Azure. Примеры кода написаны на Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 357a7277dd42b6973cf35a9f642b8eec36a745e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-ruby"></a><span data-ttu-id="622fc-104">Как использовать очереди служебной шины с Ruby</span><span class="sxs-lookup"><span data-stu-id="622fc-104">How to use Service Bus queues with Ruby</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="622fc-105">В этом руководстве показано, как использовать очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="622fc-105">This guide describes how to use Service Bus queues.</span></span> <span data-ttu-id="622fc-106">Примеры написаны с помощью Ruby и используют пакет Azure.</span><span class="sxs-lookup"><span data-stu-id="622fc-106">The samples are written in Ruby and use the Azure gem.</span></span> <span data-ttu-id="622fc-107">Здесь описаны такие сценарии, как **создание очередей, отправка и получение сообщений**, а также **удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="622fc-107">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="622fc-108">Дополнительные сведения об очередях служебной шины см. в разделе [Дальнейшие действия](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="622fc-108">For more information about Service Bus queues, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="622fc-109">Как создать очередь</span><span class="sxs-lookup"><span data-stu-id="622fc-109">How to create a queue</span></span>
<span data-ttu-id="622fc-110">Объект **Azure::ServiceBusService** позволяет работать с очередями.</span><span class="sxs-lookup"><span data-stu-id="622fc-110">The **Azure::ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="622fc-111">Чтобы создать очередь, используйте метод `create_queue()`.</span><span class="sxs-lookup"><span data-stu-id="622fc-111">To create a queue, use the `create_queue()` method.</span></span> <span data-ttu-id="622fc-112">В следующем примере создается очередь или выводится ошибка, если она возникла.</span><span class="sxs-lookup"><span data-stu-id="622fc-112">The following example creates a queue or prints out any errors.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

<span data-ttu-id="622fc-113">Можно также передать объект **Azure::ServiceBus::Queue** с дополнительными параметрами, которые позволяют переопределить параметры очереди по умолчанию, например, срок жизни сообщения или максимальный размер очереди.</span><span class="sxs-lookup"><span data-stu-id="622fc-113">You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you to override the default queue settings, such as message time to live or maximum queue size.</span></span> <span data-ttu-id="622fc-114">В следующем примере показано, как установить максимальный размер очереди в 5 ГБ и срок жизни в 1 минуту.</span><span class="sxs-lookup"><span data-stu-id="622fc-114">The following example shows how to set the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-to-send-messages-to-a-queue"></a><span data-ttu-id="622fc-115">Как отправлять сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="622fc-115">How to send messages to a queue</span></span>
<span data-ttu-id="622fc-116">Чтобы отправить сообщение в очередь служебной шины, приложение вызывает метод `send_queue_message()` для объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="622fc-116">To send a message to a Service Bus queue, your application calls the `send_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="622fc-117">Сообщения, отправленные из очередей служебной шины (и полученные из них) представляют собой объекты **Azure::ServiceBus::BrokeredMessage**. У них есть набор стандартных свойств (например, `label` и `time_to_live`), словарь, используемый для хранения настраиваемых свойств приложения, и текст произвольных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="622fc-117">Messages sent to (and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="622fc-118">Приложение может задать текст сообщения, передав строковое значение как сообщение, а все необходимые стандартные свойства заполняются значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="622fc-118">An application can set the body of the message by passing a string value as the message and any required standard properties are populated with default values.</span></span>

<span data-ttu-id="622fc-119">В следующем примере показано, как отправить тестовое сообщение в очередь с именем `test-queue` с помощью метода `send_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="622fc-119">The following example demonstrates how to send a test message to the queue named `test-queue` using `send_queue_message()`:</span></span>

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

<span data-ttu-id="622fc-120">Очереди служебной шины поддерживают максимальный размер сообщения 256 КБ для [уровня "Стандартный"](service-bus-premium-messaging.md) и 1 МБ для [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="622fc-120">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="622fc-121">Максимальный размер заголовка, который содержит стандартные и настраиваемые свойства приложения, — 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="622fc-121">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="622fc-122">Ограничения на количество сообщений в очереди нет, но есть максимальный общий размер сообщений, содержащихся в очереди.</span><span class="sxs-lookup"><span data-stu-id="622fc-122">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="622fc-123">Этот размер очереди, определяемый в момент ее создания, не должен превышать 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="622fc-123">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-queue"></a><span data-ttu-id="622fc-124">Как получать сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="622fc-124">How to receive messages from a queue</span></span>
<span data-ttu-id="622fc-125">Сообщения извлекаются из очереди с помощью метода `receive_queue_message()` для объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="622fc-125">Messages are received from a queue using the `receive_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="622fc-126">По умолчанию сообщения считываются и блокируются без удаления из очереди.</span><span class="sxs-lookup"><span data-stu-id="622fc-126">By default, messages are read and locked without being deleted from the queue.</span></span> <span data-ttu-id="622fc-127">Но вы можете удалить сообщения из очереди после их чтения, установив для параметра `:peek_lock` значение **false**.</span><span class="sxs-lookup"><span data-stu-id="622fc-127">However, you can delete messages from the queue as they are read by setting the `:peek_lock` option to **false**.</span></span>

<span data-ttu-id="622fc-128">По умолчанию чтение и удаление выполняются в два этапа, что позволяет поддерживать приложения, не способные обрабатывать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="622fc-128">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="622fc-129">Получив запрос, служебная шина находит следующее сообщение, блокирует его, чтобы предотвратить его получение другими получателями, и возвращает его приложению.</span><span class="sxs-lookup"><span data-stu-id="622fc-129">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="622fc-130">Обработав сообщение (или сохранив его в надежном месте для последующей обработки), приложение вызывает метод `delete_queue_message()` и указывает сообщение, которое будет удалено как параметр, таким образом завершая второй этап процесса получения.</span><span class="sxs-lookup"><span data-stu-id="622fc-130">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_queue_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="622fc-131">Метод `delete_queue_message()` помечает сообщение как использованное и удаляет его из очереди.</span><span class="sxs-lookup"><span data-stu-id="622fc-131">The `delete_queue_message()` method will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="622fc-132">Если параметр `:peek_lock` имеет значение **false**, чтение и удаление сообщения осуществляется очень просто. Этот метод оптимально подходит для сценариев, в которых приложение может пропустить обработку сообщения без последствий в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="622fc-132">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="622fc-133">Чтобы это понять, рассмотрим сценарий, в котором объект-получатель выдает запрос на получение и выходит из строя до его обработки.</span><span class="sxs-lookup"><span data-stu-id="622fc-133">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="622fc-134">Так как служебная шина помечает сообщение как использованное, перезапущенное приложение, начав снова использовать сообщения, пропустит сообщение, использованное до аварийного завершения работы.</span><span class="sxs-lookup"><span data-stu-id="622fc-134">Because Service Bus has marked the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="622fc-135">В следующем примере показано, как получать и обрабатывать сообщения с помощью метода `receive_queue_message()`.</span><span class="sxs-lookup"><span data-stu-id="622fc-135">The following example demonstrates how to receive and process messages using `receive_queue_message()`.</span></span> <span data-ttu-id="622fc-136">Сначала приложение получает и удаляет сообщение в примере с помощью параметра `:peek_lock`, для которого задано значение **false**, а затем получает другое сообщение и удаляет его с помощью метода `delete_queue_message()`.</span><span class="sxs-lookup"><span data-stu-id="622fc-136">The example first receives and deletes a message by using `:peek_lock` set to **false**, then it receives another message and then deletes the message using `delete_queue_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="622fc-137">Как обрабатывать сбои приложения и нечитаемые сообщения</span><span class="sxs-lookup"><span data-stu-id="622fc-137">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="622fc-138">служебная шина предоставляет функции, помогающие корректно выполнить восстановление после ошибок в приложении или трудностей, возникших при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="622fc-138">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="622fc-139">Если по какой-либо причине приложению-получателю не удается обработать сообщение, оно вызывает метод `unlock_queue_message()` для объекта **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="622fc-139">If a receiver application is unable to process the message for some reason, then it can call the `unlock_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="622fc-140">Этот вызов позволяет служебной шине разблокировать сообщение в очереди и сделать его доступным для приема тем же или другим приложением-пользователем.</span><span class="sxs-lookup"><span data-stu-id="622fc-140">This call causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="622fc-141">Кроме того, с сообщением, блокированным в очереди, связано время ожидания. Если приложение не сможет обработать сообщение в течение времени ожидания (например, при сбое приложения), служебная шина автоматически разблокирует сообщение и снова сделает его доступным для получения.</span><span class="sxs-lookup"><span data-stu-id="622fc-141">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="622fc-142">Если в приложении происходит сбой после обработки сообщения, но перед вызовом метода `delete_queue_message()`, сообщение будет повторно доставлено в приложение после его перезапуска.</span><span class="sxs-lookup"><span data-stu-id="622fc-142">In the event that the application crashes after processing the message but before the `delete_queue_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="622fc-143">Часто такой процесс называют *обработать хотя бы один раз*, т. е. каждое сообщение будет обрабатываться по крайней мере один раз, но в некоторых случаях это же сообщение может быть доставлено повторно.</span><span class="sxs-lookup"><span data-stu-id="622fc-143">This process is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="622fc-144">Если повторная обработка недопустима, разработчики приложения должны добавить дополнительную логику для обработки повторной доставки сообщений.</span><span class="sxs-lookup"><span data-stu-id="622fc-144">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="622fc-145">Как правило, это достигается с помощью свойства `message_id` сообщения, которое остается постоянным для различных попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="622fc-145">This is often achieved using the `message_id` property of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="622fc-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="622fc-146">Next steps</span></span>
<span data-ttu-id="622fc-147">Вы узнали основные сведения об очередях служебной шины. Для получения дополнительных сведений используйте следующие ссылки.</span><span class="sxs-lookup"><span data-stu-id="622fc-147">Now that you've learned the basics of Service Bus queues, follow these links to learn more.</span></span>

* <span data-ttu-id="622fc-148">Обзор [очередей, разделов и подписок](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="622fc-148">Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="622fc-149">Посетите репозиторий [Azure SDK для Ruby](https://github.com/Azure/azure-sdk-for-ruby) на веб-сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="622fc-149">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

<span data-ttu-id="622fc-150">Сравнение очередей служебной шины Azure, описанных в этой статье, и очередей служебной шины Azure, описанных в статье [Использование хранилища очередей из Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md), см. в статье [Очереди Azure и очереди служебной шины: сходства и различия](service-bus-azure-and-service-bus-queues-compared-contrasted.md).</span><span class="sxs-lookup"><span data-stu-id="622fc-150">For a comparison between the Azure Service Bus queues discussed in this article and Azure Queues discussed in the [How to use Queue storage from Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>

