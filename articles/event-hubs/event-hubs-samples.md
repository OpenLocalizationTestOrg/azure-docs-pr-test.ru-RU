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
# <a name="event-hubs-samples"></a><span data-ttu-id="125c1-103">Примеры концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="125c1-103">Event Hubs samples</span></span> 

<span data-ttu-id="125c1-104">Hello набор образцов концентраторов событий Azure демонстрирует ключевые возможности [концентраторов событий Azure](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="125c1-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="125c1-105">В этой статье, категорию и описание образцов hello, доступных с tooeach ссылки.</span><span class="sxs-lookup"><span data-stu-id="125c1-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="125c1-106">Во время hello написания этой статьи образцы концентраторов событий находятся в разных местах.</span><span class="sxs-lookup"><span data-stu-id="125c1-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="125c1-107">Примеры кода для разработчиков на сайте MSDN</span><span class="sxs-lookup"><span data-stu-id="125c1-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="125c1-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="125c1-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="125c1-109">Дополнительные сведения о различных версиях hello .NET Framework см. в разделе [платформы и целевых объектов](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="125c1-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="125c1-110">Со временем примеры будут добавляться, поэтому регулярно проверяйте наличие обновлений.</span><span class="sxs-lookup"><span data-stu-id="125c1-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="125c1-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="125c1-111">.NET Standard</span></span>

<span data-ttu-id="125c1-112">Hello следующих примерах показано, как toosend и получать события с помощью hello [концентраторов событий клиента](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) для hello [.NET стандартной библиотеки](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="125c1-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="125c1-113">Отправка событий</span><span class="sxs-lookup"><span data-stu-id="125c1-113">Send events</span></span> 

<span data-ttu-id="125c1-114">Hello [начать отправку](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) образце показано, как .NET Core toowrite консоли приложение, которое отправляет концентратора событий tooan события.</span><span class="sxs-lookup"><span data-stu-id="125c1-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="125c1-115">Получение событий</span><span class="sxs-lookup"><span data-stu-id="125c1-115">Receive events</span></span> 

<span data-ttu-id="125c1-116">Hello [начать получение с hello узел обработчика событий](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) образец представляет собой консольное приложение .NET Core, которая получает сообщения из концентратора событий с помощью hello узел обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="125c1-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="125c1-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="125c1-117">.NET Framework</span></span>   

<span data-ttu-id="125c1-118">В этих примерах демонстрируются другие возможности концентраторов событий Azure, предназначенных для hello [библиотеки .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="125c1-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="125c1-119">Уведомление пользователей о полученных событиях</span><span class="sxs-lookup"><span data-stu-id="125c1-119">Notify users of events received</span></span>

<span data-ttu-id="125c1-120">Hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) образец уведомляет пользователей данных, полученных из датчиков или других систем.</span><span class="sxs-lookup"><span data-stu-id="125c1-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="125c1-121">Приступая к работе с концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="125c1-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="125c1-122">Hello [событий концентраторов Приступая к работе](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) образец демонстрирует hello основных возможностей концентраторов событий, например, как отправлять события концентратора событий tooan toocreate концентратор событий и получать события с помощью hello [узел обработчика событий](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="125c1-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="125c1-123">Развертывание обработки событий</span><span class="sxs-lookup"><span data-stu-id="125c1-123">Scale out event processing</span></span> 

<span data-ttu-id="125c1-124">Hello [масштабирования обработки событий](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) образце показано, как toouse hello [узел обработчика событий](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) рабочей нагрузки hello toodistribute потребления поток концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="125c1-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="125c1-125">Здесь показано, как tooimplement hello **EventProcessor** и **EventProcessorFactory** поток событий hello toomanage объектов.</span><span class="sxs-lookup"><span data-stu-id="125c1-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="125c1-126">Извлечение данных из SQL в концентратор событий</span><span class="sxs-lookup"><span data-stu-id="125c1-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="125c1-127">Hello [SQL извлечение данных](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) примере показано, как таблицы и принудительно отправить его концентратора событий tooan, toouse в качестве входных данных в нисходящие приложения аналитических toopull данные из SQL.</span><span class="sxs-lookup"><span data-stu-id="125c1-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="125c1-128">Извлечение веб-данных в концентратор событий</span><span class="sxs-lookup"><span data-stu-id="125c1-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="125c1-129">Hello [Импорт данных из Интернета hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) образце показано, как toopull данных из открытых каналов (такие как hello департаментом транспорта сведений о трафике веб-канала) и отправьте его tooan концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="125c1-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="125c1-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="125c1-130">Next steps</span></span>

<span data-ttu-id="125c1-131">Дополнительные сведения о версии платформы .NET Framework, перейдя по адресу hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="125c1-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="125c1-132">Платформы и целевые объекты</span><span class="sxs-lookup"><span data-stu-id="125c1-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="125c1-133">.NET Framework 4.6 и 4.5</span><span class="sxs-lookup"><span data-stu-id="125c1-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="125c1-134">Дополнительные сведения о концентраторах событий в hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="125c1-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="125c1-135">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="125c1-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="125c1-136">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="125c1-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="125c1-137">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="125c1-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)