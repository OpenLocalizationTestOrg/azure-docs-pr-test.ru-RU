---
title: "aaaOverview из hello стандартных API концентраторов событий .NET Azure | Документы Microsoft"
description: "Обзор API для платформы .NET Standard"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="bb85a-103">Обзор API концентраторов событий для платформы .NET Standard</span><span class="sxs-lookup"><span data-stu-id="bb85a-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="bb85a-104">В этой статье приведена сводка hello ключа интерфейсов API .NET концентраторов событий Standard клиента.</span><span class="sxs-lookup"><span data-stu-id="bb85a-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="bb85a-105">В настоящее время существует две клиентские библиотеки .NET Standard:</span><span class="sxs-lookup"><span data-stu-id="bb85a-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="bb85a-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="bb85a-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="bb85a-107">Эта библиотека содержит все основные операции среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="bb85a-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="bb85a-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="bb85a-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="bb85a-109">Эта библиотека добавляет дополнительные функциональные возможности, позволяет для отслеживания обработанные события, которое tooread простым способом hello из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="bb85a-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="bb85a-110">Клиент концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="bb85a-110">Event Hubs client</span></span>
<span data-ttu-id="bb85a-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) hello основного объекта, используйте события toosend создана получатели и tooget информации во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="bb85a-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="bb85a-112">Этот клиент — центр связанного tooa определенного события и создает новую конечную точку подключения toohello концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="bb85a-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="bb85a-113">Создание клиента концентратора событий</span><span class="sxs-lookup"><span data-stu-id="bb85a-113">Create an Event Hubs client</span></span>
<span data-ttu-id="bb85a-114">Объект [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) создается из строки подключения.</span><span class="sxs-lookup"><span data-stu-id="bb85a-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="bb85a-115">Следующий пример hello показано Hello простейший способ tooinstantiate нового клиента:</span><span class="sxs-lookup"><span data-stu-id="bb85a-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="bb85a-116">tooprogrammatically изменить строку соединения hello, вы можете использовать hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) класса и передать в качестве параметра строки подключения hello слишком[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="bb85a-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="bb85a-117">Отправка событий</span><span class="sxs-lookup"><span data-stu-id="bb85a-117">Send events</span></span>
<span data-ttu-id="bb85a-118">события toosend tooan концентратора событий, используйте hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) класса.</span><span class="sxs-lookup"><span data-stu-id="bb85a-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="bb85a-119">текст Hello должен быть `byte` массива, или `byte` фрагмента массива.</span><span class="sxs-lookup"><span data-stu-id="bb85a-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="bb85a-120">Получение событий</span><span class="sxs-lookup"><span data-stu-id="bb85a-120">Receive events</span></span>
<span data-ttu-id="bb85a-121">Hello рекомендуется способом tooreceive события из концентраторов событий использует hello [узел обработчика событий](#event-processor-host-apis), который предоставляет функциональные возможности tooautomatically отслеживать смещение и сведения о секции.</span><span class="sxs-lookup"><span data-stu-id="bb85a-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="bb85a-122">Однако существуют ситуаций, в которых может потребоваться гибкость hello toouse hello основные концентраторов событий библиотеки tooreceive события.</span><span class="sxs-lookup"><span data-stu-id="bb85a-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="bb85a-123">Создание приемника</span><span class="sxs-lookup"><span data-stu-id="bb85a-123">Create a receiver</span></span>
<span data-ttu-id="bb85a-124">Приемники — это связанные toospecific секций, так чтобы tooreceive все события в концентратор событий, вы должны будете toocreate несколько экземпляров.</span><span class="sxs-lookup"><span data-stu-id="bb85a-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="bb85a-125">Вообще говоря это хороший способ сведения о разделах tooget hello программным путем, вместо жестко запрограммированного идентификаторы секций hello.</span><span class="sxs-lookup"><span data-stu-id="bb85a-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="bb85a-126">Порядок toodo так, можете воспользоваться hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) метод.</span><span class="sxs-lookup"><span data-stu-id="bb85a-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

<span data-ttu-id="bb85a-127">Поскольку события никогда не удаляются из концентратора событий (и только срок действия), необходимо toospecify hello правильную отправной точки.</span><span class="sxs-lookup"><span data-stu-id="bb85a-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="bb85a-128">Hello пример возможных сочетаний.</span><span class="sxs-lookup"><span data-stu-id="bb85a-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="bb85a-129">Использование события</span><span class="sxs-lookup"><span data-stu-id="bb85a-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="bb85a-130">Интерфейсы API узла обработчика событий</span><span class="sxs-lookup"><span data-stu-id="bb85a-130">Event Processor Host APIs</span></span>
<span data-ttu-id="bb85a-131">Эти API обеспечивают отказоустойчивость tooworker процессов, которые могут стать недоступными, распространив секций среди всех имеющихся работников.</span><span class="sxs-lookup"><span data-stu-id="bb85a-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="bb85a-132">Hello ниже приведен пример реализации hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="bb85a-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="bb85a-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb85a-133">Next steps</span></span>
<span data-ttu-id="bb85a-134">toolearn Дополнительные сведения о сценариях концентраторов событий в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="bb85a-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="bb85a-135">Что такое концентраторы событий Azure?</span><span class="sxs-lookup"><span data-stu-id="bb85a-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="bb85a-136">Общие сведения об API концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="bb85a-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="bb85a-137">Здесь приведены ссылки .NET API Hello.</span><span class="sxs-lookup"><span data-stu-id="bb85a-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="bb85a-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="bb85a-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="bb85a-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="bb85a-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)