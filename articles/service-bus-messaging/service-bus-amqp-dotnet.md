---
title: "aaaService шины с помощью .NET и AMQP 1.0 | Документы Microsoft"
description: "Использование служебной шины Azure на платформе .NET с протоколом AMQP"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>Использование служебной шины на платформе .NET с протоколом AMQP 1.0

## <a name="downloading-hello-service-bus-sdk"></a>Загрузка hello пакет SDK служебной шины

Поддержка AMQP 1.0 доступна в hello пакет SDK служебной шины версии 2.1 или более поздней версии. Необходимо убедиться, есть последняя версия hello путем загрузки bits Service Bus hello из [NuGet][NuGet].

## <a name="configuring-net-applications-toouse-amqp-10"></a>Настройка приложений .NET toouse AMQP 1.0

По умолчанию клиентская библиотека .NET служебной шины hello взаимодействует с hello службы Service Bus с помощью выделенного протокола на основе SOAP. toouse AMQP 1.0 вместо протокола по умолчанию hello, требуется явно настроить в строке подключения Service Bus hello, как описано в следующем разделе hello. Помимо этих изменений, код приложения остается без изменений при использовании AMQP 1.0.

В текущем выпуске hello существует несколько функций API, которые не поддерживаются при использовании AMQP. Неподдерживаемые функции перечислены ниже в разделе "hello" [неподдерживаемые функции, ограничения и различия в поведении](#unsupported-features-restrictions-and-behavioral-differences). При использовании AMQP некоторые дополнительные параметры настройки hello также имеют другое значение.

### <a name="configuration-using-appconfig"></a>Настройка с помощью файла App.config

Рекомендуется для приложений toouse hello App.config toostore настройки файла. Для приложения Service Bus можно использовать строку подключения Service Bus hello toostore App.config. Ниже приводится пример файла App.config:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

Здравствуйте, значение hello `Microsoft.ServiceBus.ConnectionString` задана строка подключения шины обслуживания hello, используемые tooconfigure hello подключения tooService шины. Hello имеет следующий формат:

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

Где `[namespace]` и `SharedAccessKey` извлекаются из hello [портал Azure] [ Azure portal] при создании пространства имен Service Bus. Дополнительные сведения см. в разделе [создание пространства имен Service Bus с помощью портала Azure hello][Create a Service Bus namespace using hello Azure portal].

При использовании AMQP добавьте строку hello подключения с `;TransportType=Amqp`. Такая запись предписывает hello клиента библиотеки toomake его tooService соединений шины с помощью AMQP 1.0.

## <a name="message-serialization"></a>Сериализация сообщений

При использовании протокола по умолчанию hello hello поведение сериализации по умолчанию клиентская библиотека .NET hello — toouse hello [DataContractSerializer] [ DataContractSerializer] введите tooserialize [BrokeredMessage ] [ BrokeredMessage] экземпляр для передачи данных между клиентской библиотеки hello и hello службы шины обслуживания. При использовании транспортного режима AMQP hello hello клиентская библиотека использует hello систему типов AMQP для сериализации hello [сообщений брокера] [ BrokeredMessage] в сообщение AMQP. Это позволяет toobe сообщение hello полученных и обработанных принимающим приложением, которое может работать на другой платформе, например, приложение Java, которое использует JMS API hello tooaccess Service Bus.

При построении [BrokeredMessage] [ BrokeredMessage] экземпляр, можно ввести объект .NET в качестве tooserve конструктор параметра toohello тексте hello приветственное сообщение. Для объектов, которые могут быть простыми типами сопоставленных tooAMQP текст hello сериализуется в типы данных AMQP. Если hello объекта не может быть непосредственно сопоставить с примитивным типом AMQP; то есть, пользовательский тип, определенный приложения hello, а затем hello объект сериализуется с использованием hello [DataContractSerializer][DataContractSerializer], и сериализации hello байт в сообщении данных AMQP.

toofacilitate взаимодействие с клиентами, отличными от .NET, используйте только те типы .NET, которые могут быть непосредственно сериализованы в типы AMQP для hello текст сообщения hello. Hello в следующей таблице приведены эти типы и hello соответствующего сопоставления toohello типы amqp.

| Тип объекта текста .NET | Сопоставленный тип AMQP | Тип раздела текста AMQP |
| --- | --- | --- |
| bool |Логическое |Значение AMQP |
| byte |ubyte |Значение AMQP |
| ushort |ushort |Значение AMQP |
| uint |uint |Значение AMQP |
| ulong |ulong |Значение AMQP |
| sbyte |byte |Значение AMQP |
| short |short |Значение AMQP |
| int |int |Значение AMQP |
| длинное целое число |длинное целое число |Значение AMQP |
| float; |float; |Значение AMQP |
| double |double |Значение AMQP |
| decimal |decimal128 |Значение AMQP |
| char; |char; |Значение AMQP |
| DateTime |Timestamp |Значение AMQP |
| Guid |uuid |Значение AMQP |
| byte[] |binary; |Значение AMQP |
| string |string |Значение AMQP |
| System.Collections.IList |list |Значение AMQP: элементов, содержащихся в коллекции hello можно только те, которые определены в этой таблице. |
| System.Array |array |Значение AMQP: элементов, содержащихся в коллекции hello можно только те, которые определены в этой таблице. |
| System.Collections.IDictionary |map |Значение AMQP: элементов, содержащихся в коллекции hello можно только те, которые определены в этой таблице. Примечание: поддерживаются только строковые ключи. |
| URI |Описано строки (см. в следующей таблице hello.) |Значение AMQP |
| Datetimeoffset |Описано long (см. в следующей таблице hello.) |Значение AMQP |
| TimeSpan |Описано long (см. ниже hello.) |Значение AMQP |
| Поток |binary; |Данные AMQP (может быть несколько). Hello разделы данных содержат необработанные байты hello, считанных из объекта потока hello. |
| Другой объект |binary; |Данные AMQP (может быть несколько). Содержит двоичной сериализации hello hello объекта, который использует hello DataContractSerializer или сериализатор, предоставляемый приложения hello. |

| Тип .NET | Сопоставленный описанный тип AMQP | Примечания |
| --- | --- | --- |
| URI |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| Datetimeoffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>Неподдерживаемые функции, ограничения и различия в поведении

Привет, следующие функции hello API .NET служебной шины не поддерживается в настоящее время при использовании AMQP:

* Транзакции
* Отправка через место назначения передачи

Существуют также некоторые небольшие различия в поведении hello hello API .NET служебной шины при использовании AMQP сравнения toohello протокола по умолчанию:

* Hello [OperationTimeout] [ OperationTimeout] свойство игнорируется.
* `MessageReceiver.Receive(TimeSpan.Zero)` реализуется в виде `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`.
* Завершение сообщения с помощью маркеров блокировки можно будет только получателями сообщения hello, первоначально полученных сообщений hello.

## <a name="controlling-amqp-protocol-settings"></a>Параметры управления протоколом AMQP

Hello [API-интерфейсы .NET](/dotnet/api/) предоставляют несколько параметров toocontrol hello поведение hello протокола AMQP:

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: элементы управления hello начальные разрешения, которые применены tooa ссылку. Hello по умолчанию — 0.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: элементы управления hello максимальный размер кадра AMQP, доступный при hello согласования во время открытия соединения. по умолчанию Hello — 65 536 байт.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: Если перенос batchable, это значение определяет максимальную задержку отправки распоряжений hello. По умолчанию наследуется отправителями и получателями. Отдельные отправители и получатели могут переопределить hello значения по умолчанию — 20 миллисекунд.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)** определяет, устанавливаются ли AMQP-подключения с использованием протокола SSL. по умолчанию Hello — **true**.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные готов toolearn? Посетите hello ссылкам:

* [Протокол AMQP служебной шины — обзор]
* [Поддержка AMQP 1.0 для секционированных очередей и разделов служебной шины]
* [Протокол AMQP служебной шины для Windows Server]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Протокол AMQP служебной шины — обзор]: service-bus-amqp-overview.md
[Поддержка AMQP 1.0 для секционированных очередей и разделов служебной шины]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Протокол AMQP служебной шины для Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
