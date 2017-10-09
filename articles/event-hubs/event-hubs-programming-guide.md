---
title: "руководство по aaaProgramming для концентраторов событий Azure | Документы Microsoft"
description: "Написание кода для концентраторов событий Azure с помощью hello Azure .NET SDK."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Руководство по программированию концентраторов событий

В этой статье рассматриваются некоторые распространенные сценарии, в создании кода с помощью концентраторов событий Azure и hello Azure .NET SDK. Предполагается, что вы уже имеете представление о концентраторах событий. Концептуальный обзор концентраторов событий в разделе hello [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Издатели событий

Вы отправляете концентратора событий tooan события, с помощью HTTP POST или через подключение AMQP 1.0. Здравствуйте, выбор какой toouse и когда зависит от hello конкретного сценария. Подключения AMQP 1.0 измеряются как подключения через посредника по служебной шине. Они больше всего подходят для сценариев с большими объемами сообщений и менее строгими требованиями к задержке, так как такие подключения обеспечивают постоянный канал обмена сообщениями.

Создание и управление с помощью hello концентраторов событий [NamespaceManager][] класса. Создает hello .NET управляемом API-интерфейсы, основной hello для публикации данных tooEvent концентраторы — hello [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) и [EventData][] классы. [EventHubClient][] предоставляет канал связи AMQP hello, по которому события отправляются toohello концентратора событий. Hello [EventData][] класс представляет событие и, концентратора событий tooan используется toopublish сообщений. Этот класс содержит текст hello, некоторые метаданные и данные заголовка о событии hello. Другие свойства добавляются toohello [EventData][] объекта при его прохождении через концентратор событий.

## <a name="get-started"></a>Начало работы

Hello классы .NET, которые поддерживают концентраторы событий приведены в hello сборку Microsoft.ServiceBus.dll. Здравствуйте, наиболее простым способом tooreference hello API служебной шины и tooconfigure приложения со всеми hello зависимости шины обслуживания — toodownload hello [пакет шины обслуживания NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus). Кроме того, можно использовать hello [консоль диспетчера пакетов](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) в Visual Studio. toodo таким образом, выполните следующую команду в hello hello [консоль диспетчера пакетов](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) окна:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Создание концентратора событий
Можно использовать hello [NamespaceManager][] класса toocreate концентраторов событий. Например:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

В большинстве случаев рекомендуется использовать hello [CreateEventHubIfNotExists][] tooavoid методы создания исключений при перезапуске службы hello. Например:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Все операции создания концентраторов событий, включая [CreateEventHubIfNotExists][], требуют **управление** разрешения на пространстве имен hello. Если вы хотите toolimit hello разрешения приложений издателя или потребителя, можно избежать вызовов операций создания в рабочем коде при использовании учетных данных с ограниченными разрешениями.

Hello [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) класс содержит сведения о концентраторе событий, включая правила авторизации hello, период хранения сообщений hello, идентификаторы секций, состояние и путь. Можно использовать этот класс tooupdate hello метаданных в концентраторе событий.

## <a name="create-an-event-hubs-client"></a>Создание клиента концентратора событий
Hello основным классом для взаимодействия с концентраторами событий является [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Этот класс предоставляет возможности отправителя и получателя. Можно создать экземпляр этого класса с помощью hello [создать](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) метода, как показано в следующий пример hello.

```csharp
var client = EventHubClient.Create(description.Path);
```

Этот метод использует сведения о соединении Service Bus hello в файле App.config hello в hello `appSettings` раздела. Пример hello `appSettings` XML использовать сведения о соединении toostore hello Service Bus см. в разделе документации hello hello [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) метод.

Другой вариант — toocreate hello клиента из строки подключения. Этот вариант удобен при использовании рабочих ролей Azure, так как можно сохранить строку hello в hello свойства конфигурации для рабочего процесса hello. Например:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

Строка соединения Hello будет в том же формате, как оно отображается в hello файл App.config для предыдущих методов hello hello:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Наконец, это также возможно toocreate [EventHubClient][] объекта из [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) экземпляра, как показано в следующий пример hello.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

Это что дополнительные важные toonote [EventHubClient][] объекты, созданные из экземпляра фабрики обмена сообщениями, повторно использует hello же базовое соединение TCP. Таким образом эти объекты имеют ограничение на пропускную способность на стороне клиента. Hello [создать](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) метод повторно использует одну фабрику обмена сообщениями. Если требуется достаточно высокая пропускная способность от одного отправителя, то можно создать несколько фабрик обмена сообщениями и один объект [EventHubClient][] из каждой фабрики обмена сообщениями.

## <a name="send-events-tooan-event-hub"></a>Отправить концентратора событий tooan события
Отправить концентратора событий tooan событий путем создания [EventData][] экземпляра и отправкой через hello [отправки](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) метод. Этот метод принимает один [EventData][] параметр экземпляра и синхронно отправляет его tooan концентратора событий.

## <a name="event-serialization"></a>Сериализация событий
Hello [EventData][] класс имеет [четыре перегруженных конструкторов](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) , предпринять ряд параметров, таких как объект и сериализатор, массив байтов или поток. Это также hello возможных tooinstantiate [EventData][] класса, а затем задать поток текста hello. При использовании JSON с помощью [EventData][], можно использовать **Encoding.UTF8.GetBytes()** массива байтов hello tooretrieve строка в кодировке JSON.

## <a name="partition-key"></a>Ключ секции
Hello [EventData][] класс имеет [PartitionKey][] свойство, позволяющее hello отправителя toospecify значение хэшируются tooproduce назначения раздела. Использование ключа раздела гарантирует все Здравствуйте события, с таким же ключом отправляются hello toohello же секции в концентратор событий hello. Общие ключи секции включают идентификаторы сеансов пользователей и уникальные идентификаторы отправителей. Hello [PartitionKey][] свойство является необязательным и может быть указано при использовании hello [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) или [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) методы. Если не указано значение для [PartitionKey][], отправленные события, распределенные toopartitions, используя модель циклический перебор.

### <a name="availability-considerations"></a>Вопросы доступности

Использование ключа раздела является необязательным, и следует тщательно проанализировать ли toouse один. Однако если порядок событий важен, в большинстве случаев следует применять ключ раздела. При использовании ключа раздела, этот раздел требует доступности на одном узле, при этом время от времени могут возникать сбои, например, при перезагрузке узлов и установке исправлений на них. Таким образом Если задан идентификатор секции и этой секции становится недоступен по какой-либо причине, попытка tooaccess hello данные этой секции завершится ошибкой. Если высокий уровень доступности является наиболее важным, не задавать ключ секционирования; в этом случае события будут отправлены toopartitions, с помощью модели циклического hello было описано выше. В этом сценарии вы выполняете явный выбор между доступностью (идентификатор секции не) и согласованности (идентификатор секции tooa события закрепление).

Вам также следует решить, как справиться с задержками в обработке событий. В некоторых случаях он может быть лучше toodrop данных и повторите чем tootry и справиться с обработке, которая потенциально может привести к задержкам дальнейшей последующей обработки. Например биржевые сводки удобно лучше toowait для завершения самые последние данные, но в чата или сценарий VOIP вместо пришлось бы hello данных быстро, даже если он еще не завершен.

Учитывая эти вопросы доступности в этих сценариях можно выбрать один из hello следующие стратегии обработки ошибок:

- прекращение (прекратите чтение из концентраторов событий, пока не будут исправлены все ошибки);
- удаление (удалите ненужные сообщения);
- Повтор ("Повторить" hello, как можно увидеть помещаются сообщения)
- [Недоставленных сообщений](../service-bus-messaging/service-bus-dead-letter-queues.md) (используется только сообщений hello буква в очередь или другой toodead концентратора событий не удалось обработать)

Дополнительные сведения и обсуждение hello компромисс между доступностью и согласованности см. в разделе [доступности и согласованности в концентраторы событий](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Пакетные операции отправки событий
Пакетная отправка событий позволяет значительно повысить пропускную способность. Hello [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) принимает **IEnumerable** параметр типа [EventData][] и отправляет hello весь пакет как атомарную операцию toohello концентратора событий.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Обратите внимание, что один пакет не должно превышать ограничение в 256 КБ hello событие. Кроме того, каждое сообщение в пакете hello использует hello же идентификатор издателя. Он не несет ответственность за hello tooensure отправителя hello, hello пакета превышать hello максимальный размер события. Если же размер больше, генерируется ошибка **Send** клиента.

## <a name="send-asynchronously-and-send-at-scale"></a>Асинхронная отправка и отправка в нужном масштабе
Можно также отправлять события концентратора событий tooan асинхронно. Асинхронная Отправка способствует увеличению hello скорость, с которой клиент может toosend события. Оба hello [отправки](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) и [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) методы доступны в асинхронных версий, которые возвращают [задачи](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) объекта. Хотя этот способ может увеличить пропускную способность, он также может привести к hello клиента toocontinue toosend события даже в том случае, когда он регулируется hello службы концентраторов событий и может привести к hello возникать ошибки или потери сообщений в противном случае правильно реализован. Кроме того, можно использовать hello [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) свойство повторных попыток hello toocontrol клиента клиента.

## <a name="create-a-partition-sender"></a>Создание отправителя секции
Несмотря на то, что это наиболее распространенные события концентратора tooan toosend событий без ключа секции, в некоторых случаях может потребоваться toosend события напрямую tooa заданного раздела. Например:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) возвращает [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) , можно использовать раздел toopublish события tooa конкретного события концентратора.

## <a name="event-consumers"></a>Получатели событий
Концентраторы событий имеют две основных модели потребления событий: прямые получатели и абстракции более высокого уровня, такие как [EventProcessorHost][]. Прямые получатели отвечают за собственную координацию доступа toopartitions в группе потребителей.

### <a name="direct-consumer"></a>Прямой потребитель
Hello самый прямой способ tooread из секции в группе потребителей — toouse hello [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) класса. toocreate экземпляра этого класса, необходимо использовать экземпляр hello [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) класса. В следующем примере hello идентификатор секции hello необходимо указать при создании приемника hello для группы потребителей hello.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Hello [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) метод имеет несколько перегрузок, которые упрощают контроль создаваемого читателя hello. Эти методы позволяют указать смещение в виде строки или отметки времени и hello возможности toospecify tooinclude указанного смещения в hello возвращение потоковую передачу или после его запуска. После создания получателя hello, можно начать прием событий на hello, возвращенный объект. Hello [Receive](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) метод имеет четыре перегрузки hello, элемент управления получать параметры операции, такие как размер пакета и время ожидания. Можно использовать асинхронные версии этих методов tooincrease hello пропускной способности потребителя hello. Например:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

С уважением tooa определенной секции обеспечивают получение сообщений hello в hello порядок, в котором они были отправлены toohello концентратора событий. Hello offset является строка токена используется tooidentify сообщения в разделе.

Обратите внимание на то, что одновременно к одной секции в группе потребителей можно подключить не более 5 параллельных модулей чтения. Как подключения или отключении читателей их сеансы могут оставаться активными на несколько минут, прежде чем служба hello распознает, что они отключены. Повторное подключение tooa секции может завершиться ошибкой в течение этого времени. Полный пример написания прямого получателя для концентраторов событий см. в разделе hello [прямые получатели концентраторов событий](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) образца.

### <a name="event-processor-host"></a>Узел обработчика событий
Hello [EventProcessorHost][] класс обрабатывает данные из концентраторов событий. Эту реализацию следует использовать при создании читателя событий на платформе .NET hello. [EventProcessorHost][] предоставляет потокобезопасную многопроцессную среду безопасного выполнения для реализаций обработчиков событий. Эта среда также предоставляет средства управления контрольными точками и аренды секций.

toouse hello [EventProcessorHost][] , можно реализовать [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Этот интерфейс содержит три метода:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

создать экземпляр toostart обработка событий, [EventProcessorHost][], предоставляя hello соответствующие параметры для концентратора событий. Затем вызовите метод [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister вашей [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) реализацию hello среды выполнения. На этом этапе узел hello попытается tooacquire аренду для каждого раздела в концентраторе событий hello, с помощью алгоритма «жадного». Эти аренды будут продолжаться в течение заданного промежутка времени, после чего их необходимо продлить. Когда новые узлы экземпляров рабочих ролей в этом случае переходит в оперативный режим, они резервируют аренды и со временем hello нагрузки переходит между узлами, как каждый пытаться tooacquire дополнительные аренды.

![Узел обработчика событий](./media/event-hubs-programming-guide/IC759863.png)

Со временем устанавливается равновесие. Эта динамическая возможность позволяет Автомасштабирование на основе ЦП tooconsumers toobe применяется для масштабирования вверх и вниз. Поскольку концентраторы событий не имеют прямой требования к количеству сообщений, среднее использование ЦП чаще всего hello оптимизировать механизм toomeasure назад сервера или потребителя размер. Если издатели начинают toopublish больше событий, чем потребителей может обработать, hello увеличить ресурсы ЦП для потребителей можно использовать toocause автоматически регулировать число экземпляров рабочих процессов.

Hello [EventProcessorHost][] класс также реализует механизм контрольные точки на основе хранилища Azure. Смещение по принципу каждой из секций, чтобы каждый получатель может определить, какие hello последнюю контрольную точку предыдущего потребителя hello хранилищ hello этот механизм система была. При переходе разделов между узлами в рамках аренд это hello механизм синхронизации, который упрощает перенос нагрузки.

## <a name="publisher-revocation"></a>Отзыв издателя
В дополнение к этому toohello дополнительные возможности времени выполнения [EventProcessorHost][], концентраторы событий поддерживают функцию отзыва издателя в порядке tooblock некоторым издателям отправлять события концентратора событий tooan. Эти функции особенно полезны, если компрометации маркера издателя или обновления программного обеспечения вызывает их toobehave неверно. В таких случаях удостоверение издателя hello, который является частью маркера SAS, можно заблокировать от событий публикации.

Дополнительные сведения о отзыв издателя и toosend концентраторов tooEvent как издатель, в статье hello [событий концентраторов Крупномасштабная защищенная публикация](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) образца.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о сценариях концентраторов событий в следующих статьях:

* [Общие сведения об API концентраторов событий](event-hubs-api-overview.md)
* [Что такое концентраторы событий?](event-hubs-what-is-event-hubs.md)
* [Доступность и согласованность в концентраторах событий](event-hubs-availability-and-consistency.md)
* [Справочник по API узла обработчика событий](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
