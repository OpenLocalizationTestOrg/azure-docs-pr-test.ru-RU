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
# <a name="how-toouse-service-bus-queues-with-java"></a>Как очереди toouse Service Bus с помощью Java
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

В этой статье описывается как toouse очереди Service Bus. Hello примеры написаны на Java и использовать hello [пакет Azure SDK для Java][Azure SDK for Java]. Hello сценарии включают **создание очередей**, **отправки и получения сообщений**, и **удаление очередей**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Настройка вашего приложения toouse Service Bus
Убедитесь, что вы установили hello [пакет Azure SDK для Java] [ Azure SDK for Java] перед построением в этом примере. Если вы используете Eclipse, вы можете установить hello [средств Azure для Eclipse] [ Azure Toolkit for Eclipse] , включающего hello Azure SDK для Java. Затем можно добавить hello **библиотеки Microsoft Azure для Java** tooyour проекта:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Добавьте следующее hello `import` вверху файла Java hello toohello инструкции:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Создание очереди
Операции управления для очередей служебной шины можно выполнять с помощью класса **ServiceBusContract**. Объект **ServiceBusContract** объект создан с соответствующей конфигурации, инкапсулирующий маркер SAS toomanage разрешения и hello **ServiceBusContract** класс является единственной точкой hello связи с Azure.

Hello **ServiceBusService** класс предоставляет методы toocreate, перечисления и удаления очередей. Здравствуйте в следующем примере показано, как **ServiceBusService** объект можно использовать toocreate очереди с именем `TestQueue`, с пространством имен с именем `HowToSample`:

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

Существуют методы на `QueueInfo` , которые позволяют toobe очереди hello настраиваемых свойств (например: tooset hello по умолчанию срок жизни (TTL) значение toobe применения toomessages отправлено toohello очереди). Hello следующем примере показано как toocreate очереди с именем `TestQueue` с максимальным размером 5 ГБ:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Обратите внимание, что можно использовать hello `listQueues` метод **ServiceBusContract** объектов toocheck, если очередь с указанным именем уже существует в пространстве имен службы.

## <a name="send-messages-tooa-queue"></a>Отправка сообщений в очереди tooa
toosend очередью сообщений tooa Service Bus, приложение получает **ServiceBusContract** объекта. Здравствуйте, как следующий код показывает toosend сообщение hello `TestQueue` очереди, созданной ранее в hello `HowToSample` пространство имен:

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

Сообщений, отправленных и полученных через служебную шину очереди являются экземплярами hello [BrokeredMessage] [ BrokeredMessage] класса. [BrokeredMessage] [ BrokeredMessage] объекты имеют набор стандартных свойств (такие как [метка](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) и [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), словари, используемые toohold пользовательские Свойства приложения и текст из произвольных данных приложения. Приложение может установить текст hello приветственное сообщение, передав в конструктор hello hello любой сериализуемый объект [BrokeredMessage][BrokeredMessage], после чего следует использовать соответствующий сериализатор hello tooserialize hello объекта. Вы также можете указать объект **java.IO.InputStream**.

Hello следующий пример демонстрирует способ тестирования toosend пяти сообщений toothe `TestQueue` **MessageSender** были получены в предыдущем фрагменте кода hello:

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

Очереди шины обслуживания поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на число hello сообщения помещаются в очередь, но отсутствует ограничение на общий размер сообщений hello, хранящиеся в очереди hello. Этот размер очереди, определяемый в момент ее создания, не должен превышать 5 ГБ.

## <a name="receive-messages-from-a-queue"></a>Получение сообщений из очереди
Hello основной способ tooreceive сообщений из очереди — toouse **ServiceBusContract** объекта. Полученные сообщения могут работать в двух различных режимах: **ReceiveAndDelete** и **PeekLock**.

При использовании hello **ReceiveAndDelete** режиме получение является единовременной операцией — то есть, когда Service Bus получает запросы на чтение для сообщения в очереди, он помечает приветственное сообщение как полученное и возвращает его toohello приложения. **ReceiveAndDelete** режиме (режим по умолчанию hello) — самая простая модель hello и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.
Поскольку приветственное сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

В **PeekLock** режиме получать становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова **удалить** на полученных приветственное сообщение. Когда Service Bus обнаруживает hello **удалить** вызов, он пометить приветственное сообщение как полученное и удалите его из очереди hello.

Hello следующем примере показано, как можно получать сообщения и обработанные с помощью **PeekLock** режиме (не hello по умолчанию). Hello приведенном ниже примере не бесконечный цикл и обрабатывает сообщения по мере их поступления в нашем `TestQueue`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Как происходит сбой toohandle приложения и может быть прочитан сообщений
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello **unlockMessage** метод для получения приветственное сообщение (вместо hello **deleteMessage** метода). Это приводит hello toounlock Service Bus сообщений в очереди hello и сделать ее доступной toobe получения, либо путем hello же потреблять приложение или другое приложение потребителя.

Кроме того, есть таймаут, связанный с сообщения, заблокированного в очереди, и если происходит сбой приложения hello tooprocess hello сообщения до истечения времени ожидания блокировки (например, если приложение hello терпит сбой), а затем Service Bus автоматически разблокирует сообщение hello и делает доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello **deleteMessage** выдается запрос, то приветственное сообщение будет повторно доставлены toohello приложения после его перезапуска. Это часто называется *по крайней мере после обработки*; то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений. Это можно сделать с помощью hello **getMessageId** метод приветственное сообщение, остается постоянным на протяжении всех попыток доставки.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello очереди шины обслуживания, в разделе [очереди, разделы и подписки] [ Queues, topics, and subscriptions] для получения дополнительной информации.

Дополнительные сведения см. в разделе hello [центра разработчиков Java](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
