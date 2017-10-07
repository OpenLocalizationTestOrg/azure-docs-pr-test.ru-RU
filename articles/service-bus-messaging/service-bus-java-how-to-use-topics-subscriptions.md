---
title: "разделы шины обслуживания Azure toouse aaaHow с Java | Документы Microsoft"
description: "Использование разделов и подписок служебной шины в Azure."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>Как toouse Service Bus разделов и подписок с помощью Java

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

В этом руководстве описаны как toouse Service Bus разделы и подписки. Hello примеры написаны на Java и использовать hello [пакет Azure SDK для Java][Azure SDK for Java]. Hello сценарии включают **создания разделов и подписок**, **создание фильтров подписок**, **отправки темы о сообщениях tooa**, **получения сообщения из подписки**, и **удаление разделов и подписок**.

## <a name="what-are-service-bus-topics-and-subscriptions"></a>Что такое разделы и подписки служебной шины?
Разделы и подписки служебной шины поддерживают модель обмена сообщениями " *публикация и подписка* ". При использовании разделов и подписок компоненты распределенного приложения не взаимодействуют между собой напрямую, а обмениваются сообщениями через раздел, который выступает в качестве посредника.

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

В отличие от очередей служебной шины, где каждое сообщение обрабатывается одним потребителем, разделы и подписки предоставляют вид связи одного со многими с помощью шаблона публикации/подписки. Можно зарегистрировать несколько подписок tooa раздела. Когда сообщение отправляется раздел tooa, он становятся доступны tooeach подписки toohandle или процесс независимо друг от друга.

Tooa подписка раздела напоминает виртуальную очередь, которая получает копии отправленных toohello раздел сообщений hello. При необходимости можно зарегистрировать правила фильтрации для раздела по подпискам, позволяющий toofilter или ограничить какие tooa темы о сообщениях, полученных какие подписок раздела.

Подписки и темы Service Bus позволяют tooscale tooprocess очень большое количество сообщений очень большом количестве пользователей и приложений.

## <a name="create-a-service-namespace"></a>Создание пространства имен службы
toobegin с помощью подписки и темы Service Bus в Azure, необходимо сначала создать пространство имен, которое предоставляет контейнером для адресации ресурсов служебной шины в приложении.

toocreate пространство имен:

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Настройка вашего приложения toouse Service Bus
Убедитесь, что вы установили hello [пакет Azure SDK для Java] [ Azure SDK for Java] перед построением в этом примере. Если вы используете Eclipse, вы можете установить hello [средств Azure для Eclipse] [ Azure Toolkit for Eclipse] , включающего hello Azure SDK для Java. Затем можно добавить hello **библиотеки Microsoft Azure для Java** tooyour проекта:

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

Добавьте следующее hello `import` вверху файла Java hello toohello инструкции:

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

Добавьте hello библиотек Azure для Java tooyour путь сборки и включите его в сборку развертывания проекта.

## <a name="create-a-topic"></a>Создание раздела
Операции управления для разделов служебной шины можно выполнять с помощью класса **ServiceBusContract**. Объект **ServiceBusContract** объект создан с соответствующей конфигурации, инкапсулирующий маркер SAS toomanage разрешения и hello **ServiceBusContract** класс является единственной точкой hello связи с Azure.

Hello **ServiceBusService** класс предоставляет методы toocreate, перечислять и удалять разделы. Следующий пример показывает как Hello **ServiceBusService** объект можно использовать toocreate раздел с именем `TestTopic`, с именем пространства имен `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Существуют методы на **TopicInfo** , позволяющие свойства раздела hello задаваемый (например: tooset hello по умолчанию срок жизни (TTL) значение toobe применения toomessages отправлено toohello раздела). Hello следующем примере показано как toocreate раздел с именем `TestTopic` с максимальным размером 5 ГБ:

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

Обратите внимание, что можно использовать hello **listTopics** метод **ServiceBusContract** объектов toocheck, если раздел с указанным именем уже существует в пространстве имен службы.

## <a name="create-subscriptions"></a>Создание подписок
Tootopics подписки также создаются с hello **ServiceBusService** класса. Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий hello набор сообщений, передаваемых toohello в виртуальную очередь подписки.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Создайте подписку с фильтром (MatchAll) по умолчанию hello
Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки. Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки. Hello следующем примере создается подписка с именем «AllMessages» и использует hello по умолчанию **MatchAll** фильтра.

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>Создание подписок с фильтрами
Также можно создать фильтры, позволяющие tooscope сообщений отправила разделе tooa должно отображаться в рамках подписки определенный раздел.

Hello самый гибкий тип фильтра, поддерживаемых подписок — [SqlFilter][SqlFilter], который реализует подмножество SQL92. Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello. Дополнительные сведения о выражениях hello, которые могут использоваться с фильтром SQL просмотрите hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] синтаксиса.

Hello следующий пример создает подписку с именем `HighMessages` с [SqlFilter] [ SqlFilter] объект, который выбирает только сообщения, которые содержат пользовательского **MessageNumber** свойство больше 3:

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

Аналогичным образом hello следующий пример создает подписку с именем `LowMessages` с [SqlFilter] [ SqlFilter] объект, который выбирает только сообщения, которые содержат **MessageNumber** Свойство меньше или равно too3:

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

Когда теперь отправляется сообщение слишком`TestTopic`, его будет всегда доставляться toohello tooreceivers подписка `AllMessages` подписки и выборочно доставленный tooreceivers подписка toohello `HighMessages` и `LowMessages` (подписки зависимости содержимое сообщения).

## <a name="send-messages-tooa-topic"></a>Отправить tooa темы о сообщениях
приложение получает toosend раздела Service Bus сообщение tooa **ServiceBusContract** объекта. Hello следующий код демонстрирует, как toosend сообщение hello `TestTopic` раздел создан ранее в рамках hello `HowToSample` пространство имен:

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

Сообщения, отправляемые разделы шины tooService, экземпляры [BrokeredMessage] [ BrokeredMessage] класса. [BrokeredMessage][BrokeredMessage]* объекты имеют ряд стандартных методов (например, **setLabel** и **TimeToLive**), словари, используемые toohold пользовательские Свойства приложения и текст из произвольных данных приложения. Приложение может установить hello текст сообщения, передав в конструктор hello любой сериализуемый объект [BrokeredMessage][BrokeredMessage]и соответствующие hello **DataContractSerializer**  затем будет использоваться tooserialize hello объекта. Кроме того, может быть предоставлен объект **java.io.InputStream**.

Hello следующий пример демонстрирует способ тестирования toosend пяти сообщений toothe `TestTopic` **MessageSender** были получены в приведенном выше фрагменте кода hello.
Обратите внимание, каким образом hello **MessageNumber** зависит от значения свойства каждого сообщения hello итерацию цикла hello (Это определяет, какие подписки получают его):

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md). Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ. Нет ограничений на hello количество сообщений, которые содержатся в разделе, но имеется ограничение на общий размер сообщений hello, удерживаемые раздела hello. Этот размер раздела определяется при создании с верхним пределом 5 ГБ.

## <a name="how-tooreceive-messages-from-a-subscription"></a>Способ tooreceive сообщений из подписки
tooreceive сообщения из подписки, используют **ServiceBusContract** объекта. Полученные сообщения могут работать в двух различных режимах: **ReceiveAndDelete** и **PeekLock**.

При использовании hello **ReceiveAndDelete** режиме получение является единовременной операцией - то есть, Service Bus, получив запрос чтения для сообщения, он помечает приветственное сообщение как полученное и возвращает его toothe приложения. **ReceiveAndDelete** режим — самая простая модель hello и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Так как сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

В **PeekLock** режиме получать становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова **удалить** на полученных приветственное сообщение. Когда Service Bus обнаруживает hello **удалить** вызов, он пометить приветственное сообщение как полученное и удалите его из раздела hello.

Hello приведенном ниже примере показано, как можно получать сообщения и обработанные с помощью **PeekLock** режиме (не hello по умолчанию). Hello пример выполняет цикл и обрабатывает сообщения в подписки «HighMessages» hello и затем завершается, если больше нет сообщений (Кроме того, могут быть заданы toowait для новых сообщений).

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
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
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
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
Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения. Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello **unlockMessage** метод для получения приветственное сообщение (вместо hello **deleteMessage** метода). Это сообщение hello toounlock Service Bus в пределах раздела hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.

Кроме того, есть таймаут, связанный с сообщения, заблокированного раздела и при сбое приложения hello tooprocess приветственное сообщение, прежде чем срок блокировки (например, если приложение hello терпит сбой), то служебной шины будет автоматическую разблокировку сообщения hello и сделать ее доступной toobe получили еще раз.

В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello **deleteMessage** выдается запрос, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения. Это часто называется **по крайней мере после обработки**, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений. Это можно сделать с помощью hello **getMessageId** метод сообщения hello, который остается постоянным протяжении всех попыток доставки.

## <a name="delete-topics-and-subscriptions"></a>Удаление разделов и подписок
Здравствуйте основной способ toodelete разделы и подписки — toouse **ServiceBusContract** объекта. Удаление раздела приведет к удалению всех подписок, зарегистрированных в разделе hello. Подписки также можно удалять по отдельности.

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello очереди шины обслуживания, в разделе [очереди Service Bus, разделы и подписки] [ Service Bus queues, topics, and subscriptions] для получения дополнительной информации.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
