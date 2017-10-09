---
title: "aaaOverview обмена сообщениями, очереди, разделы и подписки Azure Service Bus | Документы Microsoft"
description: "Общие сведения о сущностях обмена сообщениями в служебной шине."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Очереди, разделы и подписки служебной шины

Служебная шина Microsoft Azure поддерживает набор облачных технологий промежуточного уровня, ориентированных на обработку сообщений. Эти технологии представлены надежными очередями сообщений, а также возможностями публикации и подписки в рамках обмена сообщениями. Эти «через посредника» возможности обмена сообщениями может рассматриваться как несвязанный обмен сообщениями с поддержкой публикации, подписки, временного разъединения и сценариев, с помощью фабрики обмена сообщениями Service Bus hello балансировки нагрузки. Разделенный обмен данными имеет множество преимуществ. Например, клиенты и серверы могут подключаться по необходимости, выполняя свои операции в асинхронном режиме.

сущности обмена сообщениями Hello, формирующие ядро hello hello этой возможности в Service Bus являются очереди, разделы и подписки и правила/действия.

## <a name="queues"></a>Очереди

Очереди обеспечивают *первым пришел, первым ушел* tooone доставки сообщений (FIFO) или несколько конкурирующих клиентов. То есть сообщения, обычно ожидаемый toobe получаются и обрабатываются получателями hello в порядке hello, в котором они были добавлены toohello очереди, и каждое сообщение принимается и обрабатывается с только одним потребителем сообщения. Основное преимущество использования очередей состоит tooachieve «временная развязка» компонентов приложений. Здравствуйте, другими словами, создатели (отправители) и потребители (получатели) не имеют toobe отправке и получении сообщений в hello же времени, так как сообщения долговременно хранятся в очереди hello. Кроме того производитель hello не имеют toowait ответа от получателя hello в порядке toocontinue tooprocess и отправки сообщений.

Связанные поощрение представляет «выравниванию нагрузки, «что позволяет toosend отправителями и получателями и получать сообщения с разной интенсивностью. Во многих приложениях системная нагрузка hello изменяется со временем; время обработки hello, необходимое для каждой единицы работы то, как правило, постоянно. Посредничество отправителями и получателями сообщений с очередью означает, что этот hello использует только приложение toobe подготовленных toobe может toohandle среднюю нагрузку вместо пиковой нагрузки. Глубина Hello hello очереди будет расти или уменьшаться как hello входящая нагрузка меняется. Это напрямую экономит деньги с учета toohello объем нагрузки приложения hello необходимые tooservice инфраструктуры. Повышении нагрузки hello, больше рабочих процессов могут быть добавлены tooread из очереди hello. Каждое сообщение обрабатывается только один hello рабочих процессов. Кроме того, этот основе опросов Балансировка нагрузки позволяет для оптимально использовать рабочие компьютеры hello даже если hello рабочий компьютер отличается по с мощностью tooprocessing учета, как они будут опрашивать сообщения на максимальной скорости. Данный шаблон часто называется «конкурирующий клиент» шаблон hello.

Использование очередей toointermediate между отправителями и получателями сообщений обеспечивает свойственную ей свободную связь между компонентами hello. Так как производители и потребители не знают друг друга, потребитель можно обновить без необходимости влияет на производитель hello.

Создание очереди является многоэтапным процессом. Выполнять операции управления для сущностей (очередей и разделов) через hello обмена сообщениями Service Bus [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) класс, который конструируется при вводе hello базовый адрес hello Service Bus пространство имен и hello учетные данные пользователя. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) предоставляет toocreate методов перечисления и удаления сущностей обмена сообщениями. После создания [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) объекта из hello SAS имя и ключ и пространство имен службы управления, можно использовать hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) метод toocreate hello очереди. Например:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

Затем можно создать объект очереди и фабрику обмена сообщениями с hello URI служебной шины в качестве аргумента. Например:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

Затем можно отправить toohello сообщений в очереди. Например, если имеется список сообщений посредника вызывается `MessageList`, кода hello появится примерно следующее toohello:

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

Затем сообщения из очереди hello следующим образом:

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

В hello [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) получать hello режиме единовременной операцией; то есть, Service Bus, получив запрос hello, он помечает приветственное сообщение как полученное и возвращает его toohello приложения. **ReceiveAndDelete** режим — самая простая модель hello и лучше всего подходит для сценариев, в которых hello приложение может не обрабатывать сообщение hello в случае сбоя. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку Service Bus помечает приветственное сообщение как полученное, когда приложение hello перезапускается и начинает получать сообщения снова, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.

В [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) получать hello режиме операции становится два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения. Service Bus, получив запрос hello, он выполняет поиск следующего сообщения toobe hello потребляет, блокирует его tooprevent других потребителей получать и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова [завершить](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) на полученных приветственное сообщение. Когда Service Bus обнаруживает hello **завершить** вызов, она помечает приветственное сообщение как полученное.

Если приложение hello не может tooprocess сообщение hello для какой-либо причине, оно может вызвать hello [отказаться от](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) метод для получения приветственное сообщение (вместо [завершить](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Это позволяет сообщение hello toounlock служебной шины и сделать ее доступной toobe получили еще раз, либо путем Привет одному клиенту или другим конкурирующих объектом-получателем. Во-вторых существует время ожидания, связанного с блокировкой hello и если происходит сбой приложения hello tooprocess hello сообщение перед hello срок блокировки (например, если приложение hello терпит сбой), то Service Bus разблокирует приветственное сообщение и делает ее доступной toobe получен еще раз (фактически выполняет [прервать](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) операции по умолчанию).

Обратите внимание, что в hello событие, которое приложение hello аварийно завершает работу после обработки сообщения hello, но перед hello **завершить** выдается запрос, приветственное сообщение повторно доставлены toohello приложения после его перезапуска. Такой подход предполагает принцип обработки сообщения *хотя бы один раз*. Однако в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, то требуется дополнительная логика в дубликаты toodetect приложения hello, которые может осуществляться на основе hello **MessageId** свойства сообщения hello, который остается Константа протяжении всех попыток доставки. Такой подход предполагает концепцию обработки *только один раз*.

## <a name="topics-and-subscriptions"></a>Разделы и подписки
В отличие от tooqueues, в котором каждое сообщение обрабатывается одним потребителем *разделы* и *подписки* обеспечивают один ко многим связь, в *публикациииподписки* шаблон. Это удобно при масштабировании toovery большое число получателей, каждого опубликованное сообщение становится доступной tooeach подписки, зарегистрированной разделе hello. Сообщения отправляются в разделе tooa и доставленный tooone или более связанных подписок, в зависимости от правил фильтрации, которые могут быть установлены в соответствии с подписками. Hello подписки могут использовать, они должны tooreceive сообщений hello toorestrict дополнительные фильтры. Сообщения отправляются теме tooa в hello таким же, каким образом они отправляются tooa очереди, но не были получены сообщения из раздела hello напрямую. Зато их можно получить из подписок. Подписка раздела напоминает виртуальную очередь, получающую копии сообщений hello, отправляемых toohello раздела. Сообщения принимаются из подписки идентично toohello способ их получения из очереди.

Для сравнения hello функция очереди по отправке сообщений сопоставляется напрямую tooa раздела, и ее функция приема сообщений — карты tooa подписки. Помимо прочего, это означает, что подписки поддерживают hello же шаблоны, описанные ранее в этом разделе с учета tooqueues: конкурирующий клиент, временное разъединение, выравнивание нагрузки и балансировки нагрузки.

Создание раздела является аналогичные toocreating очереди, как показано в примере hello в предыдущем разделе hello. Создайте URI службы hello, а затем используйте hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) hello пространство имен класса toocreate клиента. Затем можно создать раздел с помощью hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) метод. Например:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

Затем добавьте необходимые подписки:

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

После этого можно создать клиент раздела. Например:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

Отправитель сообщения hello можно отправлять и получать сообщения tooand hello раздела, как показано в предыдущем разделе hello. Например:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Аналогичные tooqueues, сообщения принимаются из подписки с помощью [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) объекта вместо [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) объекта. Создайте клиент подписки hello, передав имя hello hello раздела, имя подписки hello hello и (необязательно) hello режим получения в качестве параметров. Например, с помощью hello **инвентаризации** подписки:

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>Правила и действия
Во многих ситуациях сообщения с определенными характеристиками должны обрабатываться разными способами. tooenable это, можно настроить подписки toofind сообщений, которые нужными свойствами, а затем выполнить некоторые изменения toothose свойства. А подписках Service Bus считать, что все сообщения, отправленные toohello раздела, можно копировать только подмножество этих сообщений toohello виртуальную очередь подписки. Это возможно благодаря использованию фильтров подписок. Такие изменения называются *действиями фильтров*. При создании подписки можно указать критерий фильтра, который обрабатывает свойства приветственное сообщение hello, оба hello системные свойства (например, **метка**) и пользовательских параметров (например, **StoreName**.) hello SQL-критерий фильтра является необязательным в этом случае; без критерия фильтра SQL любое действие фильтра, заданное для подписки выполняется на все сообщения hello для этой подписки.

Используя предыдущий пример hello, toofilter сообщений только из **Store1**, необходимо создать подписку панели мониторинга hello следующим образом:

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

С помощью такого фильтра подписки на месте, только сообщения, имеющие hello `StoreName` значение свойства слишком`Store1` , скопированный toohello виртуальную очередь для hello `Dashboard` подписки.

Дополнительные сведения о возможные значения фильтра документации hello hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) и [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) классы. См. также, hello [обмен сообщениями через посредника: дополнительных фильтров](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) и [фильтры разделов](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) образцов.

## <a name="next-steps"></a>Дальнейшие действия
В разделе hello следующие дополнительные разделы, Дополнительные сведения и примеры использования сообщений Service Bus.

* [Основные сведения об обмене сообщениями через служебную шину](service-bus-messaging-overview.md)
* [Учебное пособие по обмену сообщениями .NET через посредника в служебной шине](service-bus-brokered-tutorial-dotnet.md)
* [Руководство по обмену сообщениями через посредника служебной шины на основе REST](service-bus-brokered-tutorial-rest.md)
* [Пример фильтров разделов](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [Brokered Messaging: Advanced Filters (Обмен сообщениями через брокер: расширенные фильтры)](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

