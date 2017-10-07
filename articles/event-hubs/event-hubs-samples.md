---
title: "образцы концентраторов событий aaaAzure | Документы Microsoft"
description: "Примеры концентраторов событий Azure"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a>Примеры концентраторов событий 

Hello набор образцов концентраторов событий Azure демонстрирует ключевые возможности [концентраторов событий Azure](/azure/event-hubs/). В этой статье, категорию и описание образцов hello, доступных с tooeach ссылки.

Во время hello написания этой статьи образцы концентраторов событий находятся в разных местах.

- [Примеры кода для разработчиков на сайте MSDN](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Дополнительные сведения о различных версиях hello .NET Framework см. в разделе [платформы и целевых объектов](/dotnet/articles/standard/frameworks).

Со временем примеры будут добавляться, поэтому регулярно проверяйте наличие обновлений.

## <a name="net-standard"></a>.NET Standard

Hello следующих примерах показано, как toosend и получать события с помощью hello [концентраторов событий клиента](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) для hello [.NET стандартной библиотеки](/dotnet/articles/standard/library).

### <a name="send-events"></a>Отправка событий 

Hello [начать отправку](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) образце показано, как .NET Core toowrite консоли приложение, которое отправляет концентратора событий tooan события.

### <a name="receive-events"></a>Получение событий 

Hello [начать получение с hello узел обработчика событий](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) образец представляет собой консольное приложение .NET Core, которая получает сообщения из концентратора событий с помощью hello узел обработчика событий.

## <a name="net-framework"></a>.NET Framework   

В этих примерах демонстрируются другие возможности концентраторов событий Azure, предназначенных для hello [библиотеки .NET Framework](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Уведомление пользователей о полученных событиях

Hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) образец уведомляет пользователей данных, полученных из датчиков или других систем.

### <a name="get-started-with-event-hubs"></a>Приступая к работе с концентраторами событий 

Hello [событий концентраторов Приступая к работе](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) образец демонстрирует hello основных возможностей концентраторов событий, например, как отправлять события концентратора событий tooan toocreate концентратор событий и получать события с помощью hello [узел обработчика событий](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Развертывание обработки событий 

Hello [масштабирования обработки событий](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) образце показано, как toouse hello [узел обработчика событий](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) рабочей нагрузки hello toodistribute потребления поток концентраторов событий. Здесь показано, как tooimplement hello **EventProcessor** и **EventProcessorFactory** поток событий hello toomanage объектов. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Извлечение данных из SQL в концентратор событий

Hello [SQL извлечение данных](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) примере показано, как таблицы и принудительно отправить его концентратора событий tooan, toouse в качестве входных данных в нисходящие приложения аналитических toopull данные из SQL.

### <a name="pull-web-data-into-an-event-hub"></a>Извлечение веб-данных в концентратор событий 

Hello [Импорт данных из Интернета hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) образце показано, как toopull данных из открытых каналов (такие как hello департаментом транспорта сведений о трафике веб-канала) и отправьте его tooan концентратора событий.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о версии платформы .NET Framework, перейдя по адресу hello ссылкам:

- [Платформы и целевые объекты](/dotnet/articles/standard/frameworks)
- [.NET Framework 4.6 и 4.5](/dotnet/framework/index)

Дополнительные сведения о концентраторах событий в hello в следующих статьях:

- [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)
- [Создание концентратора событий](event-hubs-create.md)
- [Часто задаваемые вопросы о концентраторах событий](event-hubs-faq.md)