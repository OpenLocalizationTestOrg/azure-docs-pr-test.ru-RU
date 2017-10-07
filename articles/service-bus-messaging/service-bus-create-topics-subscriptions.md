---
title: "aaaCreate приложений, использующих подписки и темы шины обслуживания Azure | Документы Microsoft"
description: "Введение toohello публикация-подписка на возможности, предлагаемые подписки и темы Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Создание приложений, использующих разделы и подписки служебной шины
Служебная шина Azure поддерживает набор облачных технологий промежуточного уровня, ориентированных на обработку сообщений. Эти технологии представлены надежными очередями сообщений, а также возможностями публикации и подписки в рамках обмена сообщениями. Эта статья основана на информации hello из [создание приложений, использующих очереди шины обслуживания](service-bus-create-queues.md) и содержит введение в возможности публикации или подписки toohello, предлагаемые разделы служебной шины.

## <a name="evolving-retail-scenario"></a>Развитие сценария розничной торговли
В этой статье продолжается hello сценарии розничной торговли, используемом в [создание приложений, использующих очереди шины обслуживания](service-bus-create-queues.md). Помните, что данные о продажах из индивидуального терминала точки продажи (POS) должен быть система управления запасами перенаправленное tooan, использующий, toodetermine данных после toobe времени пополнения запасов. Каждый терминал передает данные о продажах, отправляя сообщения toohello **DataCollectionQueue** очереди, где они остаются до поступления в систему управления запасами hello, как показано ниже:

![Служебная шина 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

tooevolve, это новое требование было добавлено toohello системы: hello владелец магазина хочет toomonitor toobe возможности, как работает хранилище hello в режиме реального времени.

tooaddress это требование hello системы должен «нажать» отключение потока данных о продажах hello. Нам по-прежнему каждое сообщение, отправленное по hello POS терминалы toobe отправляемых системой управления запасами toohello как до, но мы хотим другую копию каждого сообщения, мы используем владелец магазина toohello представления панели мониторинга toopresent hello.

В любой такой ситуации, в которой требуется toobe каждого сообщения, используются в нескольких местах, можно использовать служебную шину *разделы*. Разделы содержат публикации и подписки, в котором каждое опубликованное сообщение становится доступной tooone или несколько подписок, зарегистрированных в разделе hello. В отличие от этой схемы, в очереди каждое сообщение доступно только одному потребителю.

Сообщения отправляются теме tooa hello так же, как они отправляются tooa очереди. Тем не менее не были получены сообщения из раздела hello напрямую. они принимаются из подписок. Раздела tooa подписки можно представить как виртуальную очередь, получающую копии сообщений hello, отправляемых toothat раздела. Сообщения принимаются из подписки hello таким же способом, что они поступают из очереди.

Вернемся toohello сценария розничной торговли, hello очереди не будет заменен раздел и добавляется подписки, можно использовать системный компонент управления какие инвентаризации hello. система Hello теперь выглядит следующим образом:

![Служебная шина 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

Hello конфигурация здесь работает одинаково toohello предыдущей схемой использования очередей. То есть сообщения, отправляемые toohello раздела, перенаправленное toohello **инвентаризации** подписки, из которой hello **систему управления запасами** использует их.

В порядке toosupport hello панели мониторинга мы создадим вторую подписку на раздел hello, как показано ниже:

![Служебная шина 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

С этой конфигурацией каждое сообщение из hello POS-терминалы становится доступной tooboth hello **мониторинга** и **инвентаризации** подписки.

## <a name="show-me-hello-code"></a>Покажите мне код hello
статья Hello [создание приложений, использующих очереди шины обслуживания](service-bus-create-queues.md) описывает способ toosign учетную запись Azure и создайте пространство имен службы. Hello простым способом tooreference Service Bus зависимостей — hello tooinstall Service Bus [пакет Nuget](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). Также можно найти hello библиотеки служебной шины в рамках hello Azure SDK. Hello загрузка доступна на hello [странице загрузки пакета Azure SDK](https://azure.microsoft.com/downloads/).

### <a name="create-hello-topic-and-subscriptions"></a>Создать раздел hello и подписки
Операции управления для сущностей обмена сообщениями (очередей и публикации или подписки разделов) выполняются через hello Service Bus [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) класса. Соответствующие учетные данные являются обязательными в порядке toocreate **NamespaceManager** экземпляр для определенного пространства имен. Служебная шина использует модель безопасности на основе [подписанного URL-адреса](service-bus-sas.md) (SAS). Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) класс представляет поставщик маркеров безопасности со встроенными методами-фабрики возвращение некоторые хорошо известные поставщики токенов. Мы будем использовать [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) учетные данные SAS метод toohold hello. Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) экземпляр конструируется с базовым адресом hello пространства имен Service Bus hello и поставщик маркеров hello.

Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) класс предоставляет методы toocreate, перечисления и удаления сущностей обмена сообщениями. Здравствуйте, код, показанный здесь показано, как hello **NamespaceManager** экземпляра — hello создана и используется toocreate **DataCollectionTopic** раздела.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Обратите внимание, что существуют перегрузки hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) метод, с помощью которых tooset свойства раздела hello. Например можно задать hello значение по умолчанию срока жизни (TTL) для сообщений, отправляемых toohello раздела. Добавьте hello **инвентаризации** и **мониторинга** подписки.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>Отправить toohello темы о сообщениях
Для выполнения операций над сущностями служебной шины, например для отправки и получения сообщений, приложение сначала должно создать объект [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory). Аналогичные toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) класса hello **MessagingFactory** из hello базового адреса пространства имен службы hello и поставщик маркеров hello создается экземпляр.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Сообщения, отправленные tooand, полученных от темы Service Bus являются экземплярами hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) класса. Этот класс — это набор стандартных свойств (например, [метка](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) и [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), словаря, используемые toohold свойств приложения и тело произвольных данных приложения. Приложения можно задать текст hello, передав ему любой сериализуемый объект (hello следующем примере передается в **SalesData** объект, представляющий данные о продажах hello из hello POS терминала), который будет использоваться hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello объекта. Также можно предоставить объект [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx).

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

Hello простым способом toosend toohello темы о сообщениях — toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) объекта непосредственно hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) экземпляр:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Получение сообщений из подписки
Аналогичные toousing очередей, tooreceive сообщения из подписки, можно использовать [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) объект, который создается непосредственно в hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) с помощью [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Можно использовать один из hello двух различных режимов приема (**ReceiveAndDelete** и **PeekLock**), как описано в [создание приложений, использующих очереди шины обслуживания](service-bus-create-queues.md).

Обратите внимание, что при создании **MessageReceiver** подписок, hello *entityPath* параметр имеет форму hello `topicPath/subscriptions/subscriptionName`. Таким образом, toocreate **MessageReceiver** для hello **инвентаризации** подписку hello **DataCollectionTopic** разделе *entityPath*необходимо задать слишком`DataCollectionTopic/subscriptions/Inventory`. Hello кода выглядит следующим образом:

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>Фильтры подписки
Таким образом в этом случае все сообщения, отправленные toohello разделе вносятся доступных tooall регистрации подписки. Hello здесь ключевую фразу «доступны.» А подписках Service Bus считать, что все сообщения, отправленные toohello раздела, можно скопировать только подмножество этих сообщений toohello виртуальную очередь подписки. Это возможно благодаря использованию *фильтров* подписок. При создании подписки можно указать критерий фильтра в форме предиката SQL92, работающую на свойства hello приветственное сообщение hello, оба hello системные свойства (например, [метка](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) и приложения hello свойства, такие как **StoreName** в предыдущем примере hello.

Это развивается tooillustrate сценарий hello второй магазин встречается toobe добавлены tooour розничной торговли. Данные о продажах из всех hello POS-терминалы из обоих магазинов по-прежнему иметь систему управления запасами централизованное toohello toobe маршрутизации, но директор магазина, с помощью средства мониторинга hello заинтересован только hello производительности хранилища. Можно использовать фильтрацию tooachieve это подписки. Обратите внимание, что при публикации сообщений hello POS-терминалы они задается hello **StoreName** свойство приложения приветственное сообщение. Получает два хранилища, например **Redmond** и **Seattle**, hello POS терминалы в Редмонде hello хранить свои данные о продажах сообщения с метки **StoreName** равно слишком **Redmond**, тогда как hello Сиэтл хранения POS терминалы используйте **StoreName** равно слишком**Seattle**. Hello директор hello только хранить Redmond хочет toosee данных со своих терминалов. система Hello выглядит следующим образом:

![Служебная шина 4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

tooset копии этой маршрутизации создать hello **мониторинга** подписки следующим образом:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

С этим [фильтр подписки](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), только сообщения, имеющие hello **StoreName** значение свойства слишком**Redmond** будет скопированный toohello виртуальную очередь для hello **Мониторинга** подписки. Гораздо больше toosubscription фильтрации, однако не существует. Приложения могут иметь несколько правил фильтрации для каждой подписки в дополнение toohello возможность toomodify hello свойств сообщения при его прохождении tooa в виртуальную очередь подписки.

## <a name="summary"></a>Сводка
Все очереди toouse причинам hello описано в [создание приложений, использующих очереди шины обслуживания](service-bus-create-queues.md) справедливы tootopics, в частности:

* Временная развязка — производители и потребители имеют toobe через Интернет в hello сообщения одновременно.
* Выравнивание нагрузки — пики нагрузки смягчаются по разделам hello Включение много toobe приложения, подготовленные для среднюю нагрузку вместо пиковой нагрузки.
* Балансировка нагрузки — аналогично tooa очереди, может иметь несколько конкурирующих потребителей, прослушивающих одну подписку, для каждого сообщения, передан один tooonly потребителей hello, тем самым балансировки нагрузки.
* Слабая связь — можно развивать hello обмена сообщениями сети, не затрагивая существующие конечные точки; например добавление подписок или изменение фильтров раздела tooallow tooa для новых потребителей.

## <a name="next-steps"></a>Дальнейшие действия

В разделе [создание приложений, использующих очереди шины обслуживания](service-bus-create-queues.md) сведения о как toouse очереди в сценарии hello POS розничной торговли.

