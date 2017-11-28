---
title: "Помещает в очередь aaaHow toouse Azure Service Bus с помощью Java | Документы Microsoft"
description: "Узнайте, как очереди toouse Service Bus в Azure. Примеры кода написаны на Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="d81ea-104">Как очереди toouse Service Bus с помощью Java</span><span class="sxs-lookup"><span data-stu-id="d81ea-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="d81ea-105">В этой статье описывается как toouse очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d81ea-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="d81ea-106">Hello примеры написаны на Java и использовать hello [пакет Azure SDK для Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="d81ea-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="d81ea-107">Hello сценарии включают **создание очередей**, **отправки и получения сообщений**, и **удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="d81ea-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="d81ea-108">Настройка вашего приложения toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="d81ea-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="d81ea-109">Убедитесь, что вы установили hello [пакет Azure SDK для Java] [ Azure SDK for Java] перед построением в этом примере.</span><span class="sxs-lookup"><span data-stu-id="d81ea-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="d81ea-110">Если вы используете Eclipse, вы можете установить hello [средств Azure для Eclipse] [ Azure Toolkit for Eclipse] , включающего hello Azure SDK для Java.</span><span class="sxs-lookup"><span data-stu-id="d81ea-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="d81ea-111">Затем можно добавить hello **библиотеки Microsoft Azure для Java** tooyour проекта:</span><span class="sxs-lookup"><span data-stu-id="d81ea-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="d81ea-112">Добавьте следующее hello `import` вверху файла Java hello toohello инструкции:</span><span class="sxs-lookup"><span data-stu-id="d81ea-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="d81ea-113">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="d81ea-113">Create a queue</span></span>
<span data-ttu-id="d81ea-114">Операции управления для очередей служебной шины можно выполнять с помощью класса **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="d81ea-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="d81ea-115">Объект **ServiceBusContract** объект создан с соответствующей конфигурации, инкапсулирующий маркер SAS toomanage разрешения и hello **ServiceBusContract** класс является единственной точкой hello связи с Azure.</span><span class="sxs-lookup"><span data-stu-id="d81ea-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="d81ea-116">Hello **ServiceBusService** класс предоставляет методы toocreate, перечисления и удаления очередей.</span><span class="sxs-lookup"><span data-stu-id="d81ea-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="d81ea-117">Здравствуйте в следующем примере показано, как **ServiceBusService** объект можно использовать toocreate очереди с именем `TestQueue`, с пространством имен с именем `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="d81ea-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="d81ea-118">Существуют методы на `QueueInfo` , которые позволяют toobe очереди hello настраиваемых свойств (например: tooset hello по умолчанию срок жизни (TTL) значение toobe применения toomessages отправлено toohello очереди).</span><span class="sxs-lookup"><span data-stu-id="d81ea-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="d81ea-119">Hello следующем примере показано как toocreate очереди с именем `TestQueue` с максимальным размером 5 ГБ:</span><span class="sxs-lookup"><span data-stu-id="d81ea-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="d81ea-120">Обратите внимание, что можно использовать hello `listQueues` метод **ServiceBusContract** объектов toocheck, если очередь с указанным именем уже существует в пространстве имен службы.</span><span class="sxs-lookup"><span data-stu-id="d81ea-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="d81ea-121">Отправка сообщений в очереди tooa</span><span class="sxs-lookup"><span data-stu-id="d81ea-121">Send messages tooa queue</span></span>
<span data-ttu-id="d81ea-122">toosend очередью сообщений tooa Service Bus, приложение получает **ServiceBusContract** объекта.</span><span class="sxs-lookup"><span data-stu-id="d81ea-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="d81ea-123">Здравствуйте, как следующий код показывает toosend сообщение hello `TestQueue` очереди, созданной ранее в hello `HowToSample` пространство имен:</span><span class="sxs-lookup"><span data-stu-id="d81ea-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="d81ea-124">Сообщений, отправленных и полученных через служебную шину очереди являются экземплярами hello [BrokeredMessage] [ BrokeredMessage] класса.</span><span class="sxs-lookup"><span data-stu-id="d81ea-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="d81ea-125">[BrokeredMessage] [ BrokeredMessage] объекты имеют набор стандартных свойств (такие как [метка](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) и [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), словари, используемые toohold пользовательские Свойства приложения и текст из произвольных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="d81ea-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="d81ea-126">Приложение может установить текст hello приветственное сообщение, передав в конструктор hello hello любой сериализуемый объект [BrokeredMessage][BrokeredMessage], после чего следует использовать соответствующий сериализатор hello tooserialize hello объекта.</span><span class="sxs-lookup"><span data-stu-id="d81ea-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="d81ea-127">Вы также можете указать объект **java.IO.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="d81ea-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="d81ea-128">Hello следующий пример демонстрирует способ тестирования toosend пяти сообщений toothe `TestQueue` **MessageSender** были получены в предыдущем фрагменте кода hello:</span><span class="sxs-lookup"><span data-stu-id="d81ea-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="d81ea-129">Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="d81ea-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="d81ea-130">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="d81ea-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="d81ea-131">Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="d81ea-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="d81ea-132">Этот размер очереди, определяемый в момент ее создания, не должен превышать 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="d81ea-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="d81ea-133">Получение сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="d81ea-133">Receive messages from a queue</span></span>
<span data-ttu-id="d81ea-134">Hello основной способ tooreceive сообщений из очереди — toouse **ServiceBusContract** объекта.</span><span class="sxs-lookup"><span data-stu-id="d81ea-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="d81ea-135">Полученные сообщения могут работать в двух различных режимах: **ReceiveAndDelete** и **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="d81ea-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="d81ea-136">При использовании hello **ReceiveAndDelete** режиме получение является единовременной операцией — то есть, когда Service Bus получает запросы на чтение для сообщения в очереди, он помечает приветственное сообщение как полученное и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d81ea-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="d81ea-137">**ReceiveAndDelete** режиме (режим по умолчанию hello) — самая простая модель hello и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="d81ea-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="d81ea-138">toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="d81ea-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="d81ea-139">Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="d81ea-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="d81ea-140">В **PeekLock** режиме получать становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="d81ea-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="d81ea-141">Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d81ea-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="d81ea-142">После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова **удалить** на полученных приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="d81ea-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="d81ea-143">Когда Service Bus обнаруживает hello **удалить** вызов, он пометить приветственное сообщение как полученное и удалите его из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="d81ea-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="d81ea-144">Hello следующем примере показано, как можно получать сообщения и обработанные с помощью **PeekLock** режиме (не hello по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="d81ea-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="d81ea-145">Hello приведенном ниже примере не бесконечный цикл и обрабатывает сообщения по мере их поступления в нашем `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="d81ea-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="d81ea-146">Как происходит сбой toohandle приложения и может быть прочитан сообщений</span><span class="sxs-lookup"><span data-stu-id="d81ea-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="d81ea-147">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="d81ea-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="d81ea-148">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello **unlockMessage** метод для получения приветственное сообщение (вместо hello **deleteMessage** метода).</span><span class="sxs-lookup"><span data-stu-id="d81ea-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="d81ea-149">Это приводит hello toounlock Service Bus сообщений в очереди hello и сделать ее доступной toobe получения, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="d81ea-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="d81ea-150">Кроме того, есть таймаут, связанный с сообщения, заблокированного в очереди, и если происходит сбой приложения hello tooprocess hello сообщения до истечения времени ожидания блокировки (например, если приложение hello терпит сбой), а затем Service Bus автоматически разблокирует сообщение hello и делает доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="d81ea-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="d81ea-151">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello **deleteMessage** выдается запрос, то приветственное сообщение будет повторно доставлены toohello приложения после его перезапуска.</span><span class="sxs-lookup"><span data-stu-id="d81ea-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="d81ea-152">Это часто называется *по крайней мере после обработки*; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="d81ea-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="d81ea-153">Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="d81ea-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="d81ea-154">Это можно сделать с помощью hello **getMessageId** метод приветственное сообщение, остается постоянным на протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="d81ea-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d81ea-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d81ea-155">Next Steps</span></span>
<span data-ttu-id="d81ea-156">Теперь, когда вы узнали основы hello очереди шины обслуживания, в разделе [очереди, разделы и подписки] [ Queues, topics, and subscriptions] для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="d81ea-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="d81ea-157">Дополнительные сведения см. в разделе hello [центра разработчиков Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="d81ea-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
