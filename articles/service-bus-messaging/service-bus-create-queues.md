---
title: "aaaWrite приложений, использующих очереди шины обслуживания Azure | Документы Microsoft"
description: "Как toowrite простое приложение на основе очередей, которое использует Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Создание приложений, использующих очереди служебной шины
В этом разделе описываются очереди Service Bus и показано, как toowrite простое приложение с использованием очереди, которое использует Service Bus.

Рассмотрим сценарий из мира розничной торговли, в котором данные о продажах из отдельных Point-of-Sale (POS) терминалы должны быть направлены tooan система управления запасами, использующий hello данных toodetermine после toobe времени пополнения запасов hello. Это решение использует сообщений Service Bus для взаимодействия hello hello терминалами и системой управления запасами hello, как показано в следующий рисунок hello:

![Очереди служебной шины, рисунок 1](./media/service-bus-create-queues/IC657161.gif)

Каждый терминал передает данные о продажах, отправляя сообщения toohello **DataCollectionQueue**. Эти сообщения остаются в этой очереди до их загрузки в систему управления запасами hello. Данный шаблон часто называется *асинхронный обмен сообщениями*, так как hello POS терминал не toowait ответа от обработки toocontinue системы управления инвентаризации hello.

## <a name="why-queuing"></a>Зачем использовать очередь?
Прежде чем мы рассмотрим hello код, который является обязательным tooset в этом приложении, рассмотрите преимущества использования очереди в этом случае вместо hello POS-терминалы hello поговорим напрямую (синхронно) toohello инвентаризации системы управления.

### <a name="temporal-decoupling"></a>Временное разделение
С hello шаблоном асинхронного обмена сообщениями, производители и потребители имеют toobe через Интернет в hello то же время. Hello инфраструктуры обмена сообщениями надежно хранит сообщения, пока сторона потребителя hello не готов tooreceive их. Это означает, что компоненты hello hello распределенного приложения может быть отключен, либо добровольно; Например, для обслуживания или из-за сбоя компонента tooa, не затрагивая hello всей системы. Кроме того использование приложения hello может иметь toobe через Интернет в определенное время дня hello. Например в данном сценарии розничной торговли, система управления запасами hello может иметь только toocome через Интернет после окончания рабочего дня hello hello.

### <a name="load-leveling"></a>Выравнивание нагрузки
Во многих приложениях системная нагрузка изменяется со временем, в то время как hello обработки время, необходимое для каждой единицы работы, как правило, постоянно. Посредничество сообщения между отправителями и получателями с означает очереди, Здравствуйте, получающее приложение (hello рабочих процессов) имеет только toobe подготовить tooservice среднее загрузить вместо пиковой нагрузки. Hello глубины hello очереди будет расти и контракт как hello входящая нагрузка меняется. Это напрямую экономит деньги с учета toohello объем нагрузки приложения hello необходимые tooservice инфраструктуры.

![Очереди служебной шины, рисунок 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Балансировка нагрузки.
Повышении нагрузки hello, больше рабочих процессов могут быть добавлены tooread из рабочей очереди hello. Каждое сообщение обрабатывается только один hello рабочих процессов. Кроме того, этот основе опросов Балансировка нагрузки позволяет для оптимального использования hello рабочие компьютеры даже если hello рабочий компьютер отличается по с мощностью tooprocessing учета, как они будут опрашивать сообщения на максимальной скорости. Данный шаблон часто называется hello конкурирующих потребителей шаблон.

![Очереди служебной шины, рисунок 3](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>Слабые связи
Использование toointermediate очереди сообщений между отправителями и получателями сообщений обеспечивает свойственную ей свободную связь между компонентами hello. Так как производители и потребители не знают друг друга, потребитель можно обновить без необходимости влияет на производитель hello. Кроме того обмен сообщениями топологии hello могут изменяться без влияния на существующие конечные точки hello. Мы обсудим это подробнее, когда будем говорить о публикациях и подписках.

## <a name="show-me-hello-code"></a>Покажите мне код hello
Здравствуйте, после раздела показано, как toobuild Service Bus toouse этого приложения.

### <a name="sign-up-for-an-azure-account"></a>Регистрация учетной записи Azure
Вам потребуется учетная запись Azure в работе с Service Bus toostart заказа. Если у вас ее нет, вы можете зарегистрироваться для получения бесплатной учетной записи [здесь](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="create-a-namespace"></a>Создание пространства имен
После получения подписки можно [создать пространство имен службы](service-bus-create-namespace-portal.md). Каждое пространство имен выступает в качестве определяющего область действия контейнера для набора сущностей служебной шины. Присвойте пространству имен имя, которое будет уникальным среди всех учетных записей служебной шины. 

### <a name="install-hello-nuget-package"></a>Установка пакета NuGet hello
пространство имен служебной шины toouse hello, приложение должно ссылаться hello сборки служебной шины, в частности на Microsoft.ServiceBus.dll. Можно найти эту сборку как часть hello Microsoft Azure SDK и hello загрузка доступна на hello [странице загрузки пакета Azure SDK](https://azure.microsoft.com/downloads/). Здравствуйте, однако [пакет шины обслуживания NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus) является hello простым способом tooget hello API служебной шины и tooconfigure приложения со всеми hello зависимости шины обслуживания.

### <a name="create-hello-queue"></a>Создать очередь hello
Операции управления для сущностей обмена сообщениями (очередей и публикации или подписки разделов) выполняются через hello Service Bus [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) класса. Служебная шина использует модель безопасности на основе [подписанного URL-адреса](service-bus-sas.md) (SAS). Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) класс представляет поставщик маркеров безопасности со встроенными методами-фабрики возвращение некоторые хорошо известные поставщики токенов. Мы будем использовать [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) учетные данные SAS метод toohold hello. Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) экземпляр конструируется с базовым адресом hello пространства имен Service Bus hello и поставщик маркеров hello.

Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) класс предоставляет методы toocreate, перечисления и удаления сущностей обмена сообщениями. Здравствуйте, код, показанный здесь показано, как hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) экземпляра — hello создана и используется toocreate **DataCollectionQueue** очереди.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Обратите внимание, что существуют перегрузки hello [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) метода, которые включают свойства настройки toobe очереди hello. Например можно задать hello значение по умолчанию срока жизни (TTL) для сообщений, отправляемых toohello очереди.

### <a name="send-messages-toohello-queue"></a>Отправка сообщений в очереди toohello
Для выполнения операций над сущностями служебной шины, например для отправки и получения сообщений, приложение сначала должно создать объект [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory). Аналогичные toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) класса hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) из hello базового адреса пространства имен службы hello и поставщик маркеров hello создается экземпляр.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

Сообщений, отправленных и полученных через служебную шину очереди являются экземплярами hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) класса. Этот класс — это набор стандартных свойств (например, [метка](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) и [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), словаря, используемые toohold свойств приложения и тело произвольных данных приложения. Приложения можно задать текст hello, передав ему любой сериализуемый объект (hello следующем примере передается в **SalesData** объект, представляющий данные о продажах hello из hello POS терминала), который будет использоваться hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello объекта. Также можно предоставить объект [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx).

Здравствуйте, tooa toosend сообщений простым способом, указанной очереди, в нашем вариантов hello **DataCollectionQueue**, является toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) объекта непосредственно из hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) экземпляра.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Получение сообщений из очереди hello
tooreceive сообщения из очереди hello, можно использовать [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) объект, который создается непосредственно в hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) с помощью [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Получатели сообщений могут работать в двух различных режимах: **ReceiveAndDelete** и **PeekLock**. Hello [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) задается при создании получателя сообщения hello, как toohello параметр [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) вызова.

При использовании hello **ReceiveAndDelete** получать hello режиме является единовременной операцией; то есть, Service Bus, получив запрос hello, он помечает приветственное сообщение как полученное и возвращает его toohello приложения. **ReceiveAndDelete** режим — самая простая модель hello и лучше всего подходит для сценариев, в которых hello приложение может не обрабатывать сообщение при возникновении сбоя toooccur. toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки. Поскольку Service Bus помечен приветственное сообщение как полученное, когда перезапусков приложения hello и начинает получать сообщения снова, оно пропустит приветственное сообщение, которое было получено до сбоя hello.

В **PeekLock** получать hello режиме становится двух шаговой операцией, поэтому его невозможно toosupport приложений, которые не удается обработать отсутствующие сообщения. Получив запрос hello, Service Bus найдет Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения. После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова [завершить](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) на полученных приветственное сообщение. Когда Service Bus обнаруживает hello [завершить](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) вызов, она помечает приветственное сообщение как полученное.

Также возможны два других результата. Во-первых, если приложение hello не может tooprocess сообщение hello для какой-либо причине, оно может вызвать [прервать](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) на полученных приветственное сообщение (вместо [завершить](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Это вызывает сообщение hello toounlock служебной шины и сделать ее доступной toobe получили еще раз, либо путем Привет одному клиенту или другим конкурирующим потребителем. Во-вторых есть таймаут, связанный с блокировкой hello и, если приложение hello не может обработать сообщение hello, до времени ожидания блокировки hello истечения срока действия (например, если приложение hello терпит сбой), Service Bus Разблокируйте сообщение hello и сделать ее доступной toobe получен еще раз (фактически выполняет [прервать](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) операции по умолчанию).

Обратите внимание, что если hello приложение аварийно завершает работу после обработки приветственное сообщение, но перед hello [завершить](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) запрос был выпущен, сообщение hello будет повторно доставлены toohello приложения, при перезапуске. Оно часто называется * хотя бы один раз * обработки. Это означает, что каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться. Если сценарий hello не допускает обработку дубликатов, в дубликаты toodetect приложения hello требуется дополнительная логика. Это можно сделать на hello основе [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) свойства сообщения hello. значение этого свойства Hello остается неизменным для попыток доставки. Это называется обработкой *только один раз*.

Hello код, показанный здесь получает и обрабатывает сообщения с помощью hello **PeekLock** режиме, используемом по умолчанию hello, если не [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) явно указано значение.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
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

### <a name="use-hello-queue-client"></a>Использование клиента очереди hello
Здравствуйте ранее в примерах этого раздела создан [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) и [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) объекты непосредственно из hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend и получения сообщений из очереди hello соответственно. Альтернативный подход — toouse [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) объект, который поддерживает как операций отправки и получения в дополнение toomore дополнительные функции, например сеансов.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello очередей, в разделе [создание приложений, использующих подписки и темы Service Bus](service-bus-create-topics-subscriptions.md) toocontinue данного обсуждения с помощью возможности публикации или подписки hello разделов Service Bus и подписки.

