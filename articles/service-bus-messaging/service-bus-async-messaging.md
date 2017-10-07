---
title: "aaaService шины асинхронный обмен сообщениями | Документы Microsoft"
description: "Описание асинхронного обмена сообщениями в служебной шине Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Шаблоны асинхронного обмена сообщениями и высокий уровень доступности

Асинхронный обмен сообщениями может осуществляться различными способами. Служебная шина Azure поддерживает асинхронность за счет механизма сохранения и пересылки. Этот механизм оперирует очередями, разделами и подписками. В нормальных условиях (синхронный) отправлять сообщения tooqueues и разделы и получения сообщений из очереди и подписки. Для создаваемых приложений важно, чтобы эти сущности всегда были доступны. При изменения работоспособности hello объекта, из-за различных обстоятельств tooa необходим способ tooprovide сниженном сущность, которая может удовлетворить большинство потребностей.

Приложения обычно используют асинхронного обмена сообщениями шаблоны tooenable ряд сценариев связи. Вы можете создавать приложения, в которых клиенты могут отправлять сообщения tooservices, даже в том случае, если не запущена служба hello. Для приложений, которые испытывают пиковыми периодами отправки сообщений очередь может помочь уровня hello загрузки, предоставляя связи toobuffer месте. Наконец вы можете получить простой, но эффективный нагрузки балансировки toodistribute сообщений между несколькими компьютерами.

В порядке toomaintain доступности какой-либо из этих сущностей следует учитывать ряд различными способами, в котором они могут быть недоступными для устойчивой системы обмена сообщениями. Вообще говоря мы увидим hello сущности становятся недоступны tooapplications, которые мы пишем в hello, следуя различными способами:

* Не удается toosend сообщения.
* Не удается tooreceive сообщения.
* Не удается toomanage сущностями (создать, извлекать, обновлять или удалять сущности).
* Не удается toocontact hello службы.

Для каждой из этих ошибок разных режимов сбоя существует, позволяющие приложения toocontinue tooperform работы некоторых сниженном уровне. Например, если система может отправлять сообщения, но не может их получать, вы по-прежнему будете получать заказы от клиентов, но не сможете их обрабатывать. В этой статье рассматриваются возможные проблемы и способы их устранения. Service Bus был представлен ряд исправлений, которые должны согласиться на, а в этом разделе также рассматриваются правила, определяющие hello использование этих исправлений участия в программе приветствия.

## <a name="reliability-in-service-bus"></a>Надежность служебной шины
Существует несколько способов toohandle проблемы сообщения и сущности и существуют рекомендации, регулирующие соответствующее использование этих исправлений hello. рекомендации по toounderstand hello, необходимо сначала понять, что может произойти сбой в Service Bus. Из-за toohello проектирования систем Azure все эти проблемы, как правило, toobe кратковременными. На высоком уровне hello различные причины недоступности могут выглядеть следующим образом:

* Регулирование из внешней системы, от которой зависит служебная шина. Регулирование возникает вследствие взаимодействия с ресурсами хранилища и вычислительными ресурсами.
* Проблема в системе, от которой зависит служебная шина. Например, могут возникнуть ошибки в определенной части хранилища.
* Сбой служебной шины в единой подсистеме. В этом случае вычислительного узла можно получить в несогласованном состоянии и должен перезагрузиться, что вынуждает все сущности служит баланс tooload tooother узлов. Это, в свою очередь, может стать причиной кратковременного замедления обработки сообщений.
* Сбой служебной шины в центре обработки данных Azure. Это «разрушительного сбоя» во время которого hello система недоступна в течение многих минут или нескольких часов.

> [!NOTE]
> Термин Hello **хранения** может означать хранилища Azure и SQL Azure.
> 
> 

В служебной шине предусмотрен ряд способов устранения рисков, связанных с этими проблемами. Привет, в следующих разделах описываются все проблемы и их исправления.

### <a name="throttling"></a>Регулирование
Регулирование в служебной шине позволяет управлять скоростью обмена сообщениями "кооперативным" способом. Каждый отдельный узел служебной шины хранит множество сущностей. Каждая из этих сущностей предъявляет требования hello системы с точки зрения ЦП, памяти, хранилища и других аспектов. Если использование какого-либо из ресурсов превысит установленные ограничения, служебная шина может отклонить запрос. Hello вызывающий объект получает [ServerBusyException] [ ServerBusyException] и повторяет попытку через 10 секунд.

С целью предотвращения кода hello hello Ошибка чтения и прервать попытки приветственное сообщение в течение 10 секунд. Поскольку hello ошибка может произойти в разных частях приложения hello клиента, предполагается, что любая часть независимо выполняет логику повторных попыток hello. Hello код может уменьшить вероятность регулировки за счет разбиения в очередь или раздел hello.

### <a name="issue-for-an-azure-dependency"></a>Проблема с зависимостью в Azure
В любом из компонентов Azure время от времени могут возникать проблемы, связанные с работой службы. Например, обновление системы, которая используется служебной шиной, может привести к временному снижению производительности этой системы. toowork вокруг таких проблем, Service Bus регулярно исследует причины и применяет исправления. Однако при применении этих способов возможны побочные эффекты. Например toohandle временной проблемы с хранилищем, Service Bus реализует систему, которая позволяет согласованно toowork операции отправки сообщения. Из-за особенностей toohello уменьшение hello отправленного сообщения может занять tooappear минут too15 в затронутых hello очереди или подписки и готовности к приему. Вообще говоря, эта проблема не затронет большинство сущностей. Тем не менее, учитывая hello число сущностей в Service Bus в Azure, это исправление иногда требуется для небольшого подмножества клиентов Service Bus.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Сбой служебной шины в единой подсистеме
В любом приложении определенные обстоятельства могут вызвать внутренним компонентом несогласованные toobecome Service Bus. Когда Service Bus обнаруживает это, он собирает данные из tooaid приложения hello в диагностике причин. После сбора данных hello, является приложение hello перезагрузки на tooreturn попытки его tooa согласованное состояние. Этот процесс происходит достаточно быстро, и результаты в сущность toobe недоступным для копирования tooa несколько минут на то, что обычно простоями намного короче.

В этих случаях клиентское приложение hello приводит к возникновению ошибки [System.TimeoutException] [ System.TimeoutException] или [MessagingException] [ MessagingException] исключение. Service Bus содержится исправление для этой проблемы в форме hello логику повторных попыток автоматического клиента. После hello период повторения исчерпан приветственное сообщение не доставлено, можно изучить использование других компонентов, таких как [пару пространства имен][paired namespaces]. С сопряженными пространствами имен связаны другие особенности, которые рассматриваются в этой статье.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Сбой служебной шины в центре обработки данных Azure
Hello наиболее вероятная причина сбоев в центре обработки данных Azure — сбой при развертывании обновления Service Bus или зависимой системы. Как взросления платформы hello снизилась hello вероятность сбоев данного типа. Сбой центра обработки данных также может произойти по причинам, которые включают следующие hello:

* перебои с электропитанием (сбой источника питания или генераторов);
* сбой подключения (обрыв интернет-подключения между клиентами и Azure).

В обоих случаях естественная или техногенная аварийного причиной проблемы hello. toowork этой и убедитесь в том, что вы можете отправлять сообщения, можно использовать [пару пространства имен] [ paired namespaces] tooenable сообщений отправленных toobe tooa второе расположение пока hello первичное расположение станет работоспособным. Дополнительные сведения см. в статье [Рекомендации по изолированию приложений от простоев и аварий служебной шины][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Сопряженные пространства имен
Hello [пару пространства имен] [ paired namespaces] функция поддерживает сценарии, в котором сущности служебной шины или развертывания в центре обработки данных становится недоступным. Хотя это событие возникает редко, распределенные системы по-прежнему должен быть подготовлен toohandle худшего варианта развития событий. Как правило, это связано с краткосрочными проблемами в элементах, от которых зависит служебная шина. toomaintain доступности приложений во время сбоя, пользователи, служебной шины можно использовать два разных пространства имен, желательно в разных центрах обработки данных, toohost своих сущностей обмена сообщениями. Hello остальной части этого раздела используется следующая терминология hello:

* Основное пространство имен: hello пространства имен, с которым взаимодействует приложение для отправки и получения операций.
* Дополнительное пространство имен: hello пространства имен, который выступает в качестве резервного копирования toohello основного пространства имен. Логика приложения не взаимодействует с этим пространством имен.
* Интервал отработки отказа: hello объем времени tooaccept обычных ошибок перед приложения hello переходит от основного пространства имен hello toohello дополнительного пространства имен.

Сопряженные пространства имен поддерживают *доступность отправки*. Отправка доступности сохраняет toosend сообщений hello возможности. доступность отправки toouse, приложения должны отвечать hello следующие требования:

1. Сообщения принимаются только от основного пространства имен hello.
2. Сообщения, отправленные tooa заданным очереди или раздела могут приходить в неправильном порядке.
3. Сообщения в рамках сеанса могут поступать не по порядку. Такой подход не соответствует стандартному порядку работы сеансов. Это означает, что приложение использует сеансы toologically группы сообщений.
4. Состояние сеанса поддерживается только на hello основного пространства имен.
5. основная очередь Hello можно переходит в оперативный режим и начать прием сообщений, прежде чем hello дополнительная очередь доставит все сообщения в основную очередь hello.

Hello в следующих разделах обсуждаются hello API-интерфейсы, реализация hello API-интерфейсов и пример кода показывает, используется функция hello. Обратите внимание, что использование этой возможности может быть сопряжено с дополнительными расходами.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Hello MessagingFactory.PairNamespaceAsync API
сопряженные пространства имен поддерживают Hello включает hello [PairNamespaceAsync] [ PairNamespaceAsync] метод hello [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] класса:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

По завершении задачи hello hello пары имен являются также готов tooact на предмет [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], или [TopicClient] [ TopicClient] созданными hello [MessagingFactory] [ MessagingFactory] экземпляра. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] — hello базовый класс для hello различных типов сопряжения, доступных с [MessagingFactory] [ MessagingFactory] объекта. В настоящее время hello только производный класс — один с именем [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], который реализует требования к доступности отправки hello. Класс [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions] имеет набор взаимозависимых конструкторов. Глядя на конструктор hello с hello большинство параметров, можно понять поведение hello hello других конструкторов.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Эти параметры имеют следующие значения hello.

* *secondaryNamespaceManager*: инициализированный [NamespaceManager] [ NamespaceManager] экземпляра для дополнительного пространства имен hello, hello [PairNamespaceAsync] [ PairNamespaceAsync] метод может использовать tooset копирование hello дополнительного пространства имен. Диспетчер пространств имен Hello — список hello используется tooobtain очередей из пространства имен hello и toomake наличие необходимых hello очередей невыполненной работы. Если очереди отсутствуют, они будут созданы. [NamespaceManager] [ NamespaceManager] требуется возможность hello toocreate маркер с hello **управление** утверждения.
* *messagingFactory*: hello [MessagingFactory] [ MessagingFactory] экземпляр для hello дополнительного пространства имен. Hello [MessagingFactory] [ MessagingFactory] объект является используемым toosend и, если hello [EnableSyphon] [ EnableSyphon] задано слишком**true** , получать сообщения из очередей невыполненной работы hello.
* *backlogQueueCount*: hello число невыполненной работы по очереди toocreate. Минимальное значение — 1. При отправке сообщения toohello невыполненной работы по одной из этих очередей выбирается случайным образом. Только одна очередь можно когда-либо использовать, если задать значение too1 hello. Если при этом hello единственной очереди возникают ошибки, hello клиента не может tootry другую очередь и может завершиться сбоем toosend сообщения. Рекомендуется установить это значение toosome большего значения и по умолчанию hello значение too10. Вы можете изменить этот tooa высокий или более низкого значения в зависимости от объема данных приложение отправляет за день. Каждая очередь необработанных сообщений может быть установлено too5 ГБ сообщений.
* *failoverInterval*: hello объем времени, в течение которого будут приниматься сбои основного пространства имен hello перед переключением отдельных сущностей через toohello дополнительного пространства имен. При отработке отказов сущности обрабатываются поочередно. Сущности в одном пространстве имен зачастую размещаются на разных узлах служебной шины. Сбой в одной сущности не подразумевает сбой в другой. Можно задать это значение слишком[System.DateTime.MaxValue и] [ System.TimeSpan.Zero] toofailover toohello получателей сразу после первого, не является временной ошибкой. Сбои, запускающие таймер обработки отказов hello они есть [MessagingException] [ MessagingException] в какой hello [IsTransient] [ IsTransient] свойство имеет значение false, или [System.TimeoutException][System.TimeoutException]. Другие исключения, таких как [UnauthorizedAccessException] [ UnauthorizedAccessException] не вызвать отработку отказа, поскольку они указывают на приветствия клиента настроен неправильно. Объект [ServerBusyException] [ ServerBusyException] может вызвать отработку поскольку правильный шаблон hello toowait 10 секунд, отправьте сообщение hello еще раз.
* *enableSyphon*: Указывает, что данное сопряжение также должно передавать сообщения из дополнительного пространства имен hello задней toohello основного пространства имен. В общем случае приложения, отправляющие сообщения следует установить это значение слишком**false**; приложения, которые получают сообщения, должны задать значение слишком**true**. Hello причина этого заключается в том, что часто, существует получателей сообщений меньше числа отправителей сообщений. В зависимости от числа получателей hello вы можете toohave процесс выкачивания сборов hello дескриптор экземпляра одного приложения. Увеличение количества получателей отразится на стоимости каждой очереди невыполненной работы.

toouse Здравствуйте кода, создайте основной [MessagingFactory] [ MessagingFactory] экземпляра дополнительного [MessagingFactory] [ MessagingFactory] экземпляра получателя [NamespaceManager] [ NamespaceManager] экземпляр и [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] экземпляра. Hello вызов может быть простым hello следующим образом:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Здравствуйте, когда задача, возвращаемая hello [PairNamespaceAsync] [ PairNamespaceAsync] метод завершения, все настроено и Готово toouse. Перед возвращением задачи hello возможно не завершена все необходимые для связывания справа toowork hello hello фоновой работы. Поэтому не следует начинать отправку сообщения до возврата задачу hello. При возникновении каких-либо ошибок, например неправильные учетные данные или очередей невыполненной работы hello toocreate сбоя, эти исключения будут создаваться после завершения задачи hello. После возвращения задачу hello, убедитесь, что hello очереди были найдены или созданы, проверив hello [BacklogQueueCount] [ BacklogQueueCount] свойство вашей [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] экземпляра. Для hello предшествующий код эта операция выглядит следующим образом:

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello асинхронный обмен сообщениями в шине обслуживания, узнать дополнительные сведения о [пару пространства имен][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
