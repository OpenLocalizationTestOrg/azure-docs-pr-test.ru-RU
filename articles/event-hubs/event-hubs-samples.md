---
title: "Примеры концентраторов событий Azure | Документация Майкрософт"
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
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="50b16-103">Примеры концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="50b16-103">Event Hubs samples</span></span> 

<span data-ttu-id="50b16-104">Набор примеров концентраторов событий Azure демонстрирует основные функции [концентраторов событий Azure](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="50b16-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="50b16-105">В этой статье приведены категории примеров с описаниями и ссылками.</span><span class="sxs-lookup"><span data-stu-id="50b16-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="50b16-106">На момент написания этой статьи примеры концентраторов событий доступны по нескольким ссылкам:</span><span class="sxs-lookup"><span data-stu-id="50b16-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="50b16-107">Примеры кода для разработчиков на сайте MSDN</span><span class="sxs-lookup"><span data-stu-id="50b16-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="50b16-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="50b16-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="50b16-109">Дополнительные сведения о различных версиях платформы .NET Framework см. в статье [Платформы и целевые объекты](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="50b16-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="50b16-110">Со временем примеры будут добавляться, поэтому регулярно проверяйте наличие обновлений.</span><span class="sxs-lookup"><span data-stu-id="50b16-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="50b16-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="50b16-111">.NET Standard</span></span>

<span data-ttu-id="50b16-112">В следующих примерах демонстрируются способы отправки и получения событий с помощью [клиента концентраторов событий](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) для [библиотеки .NET Standard](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="50b16-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="50b16-113">Отправка событий</span><span class="sxs-lookup"><span data-stu-id="50b16-113">Send events</span></span> 

<span data-ttu-id="50b16-114">В [этом примере](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) показано, как написать консольное приложение .NET Core, которое отправляет события в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="50b16-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="50b16-115">Получение событий</span><span class="sxs-lookup"><span data-stu-id="50b16-115">Receive events</span></span> 

<span data-ttu-id="50b16-116">В [этом примере](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) содержится консольное приложение .NET Core, которое получает сообщения из концентратора событий, используя узел обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="50b16-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="50b16-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="50b16-117">.NET Framework</span></span>   

<span data-ttu-id="50b16-118">В этих примерах демонстрируются другие функции концентраторов событий Azure, предназначенные для [библиотеки .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="50b16-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="50b16-119">Уведомление пользователей о полученных событиях</span><span class="sxs-lookup"><span data-stu-id="50b16-119">Notify users of events received</span></span>

<span data-ttu-id="50b16-120">Пример приложения [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) уведомляет пользователей о данных, полученных с датчиков или из других систем.</span><span class="sxs-lookup"><span data-stu-id="50b16-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="50b16-121">Приступая к работе с концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="50b16-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="50b16-122">В [этом примере](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) демонстрируются базовые возможности концентраторов событий: их создание, отправка событий в концентратор событий и получение событий с помощью [узла обработчика событий](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="50b16-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="50b16-123">Развертывание обработки событий</span><span class="sxs-lookup"><span data-stu-id="50b16-123">Scale out event processing</span></span> 

<span data-ttu-id="50b16-124">В [этом примере](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) демонстрируется, как с помощью [узла обработчика событий](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) распределить рабочую нагрузку потребления потока концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="50b16-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="50b16-125">В нем показано, как реализовать объекты **EventProcessor** и **EventProcessorFactory** для управления потоком событий.</span><span class="sxs-lookup"><span data-stu-id="50b16-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="50b16-126">Извлечение данных из SQL в концентратор событий</span><span class="sxs-lookup"><span data-stu-id="50b16-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="50b16-127">В [этом примере](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) показано, как извлечь данные из таблицы SQL и передать их в концентратор событий для использования в качестве входных данных для нижестоящих аналитических приложений.</span><span class="sxs-lookup"><span data-stu-id="50b16-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="50b16-128">Извлечение веб-данных в концентратор событий</span><span class="sxs-lookup"><span data-stu-id="50b16-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="50b16-129">В [этом примере](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) показано, как извлечь данные из общедоступных веб-каналов (например, из информационного веб-канала Министерства транспорта США) и передать их в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="50b16-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50b16-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50b16-130">Next steps</span></span>

<span data-ttu-id="50b16-131">Дополнительные сведения о версиях платформы .NET Framework см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="50b16-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="50b16-132">Платформы и целевые объекты</span><span class="sxs-lookup"><span data-stu-id="50b16-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="50b16-133">.NET Framework 4.6 и 4.5</span><span class="sxs-lookup"><span data-stu-id="50b16-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="50b16-134">Чтобы узнать больше о концентраторах событий, обратитесь к следующим статьям:</span><span class="sxs-lookup"><span data-stu-id="50b16-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="50b16-135">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="50b16-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="50b16-136">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="50b16-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="50b16-137">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="50b16-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)