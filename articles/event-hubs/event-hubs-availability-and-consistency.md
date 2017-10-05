---
title: "Доступность и согласованность в концентраторах событий Azure | Документация Майкрософт"
description: "Узнайте, как обеспечить максимальную доступность и согласованность в концентраторах событий Azure с помощью секций."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 681a9d1636d547492f6f827461c6b2494b918778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="f5f74-103">Доступность и согласованность в концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="f5f74-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="f5f74-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f5f74-104">Overview</span></span>
<span data-ttu-id="f5f74-105">Концентраторы событий Azure используют [модель секционирования](event-hubs-features.md#partitions) для повышения доступности и распараллеливания в пределах одного концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="f5f74-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) to improve availability and parallelization within a single event hub.</span></span> <span data-ttu-id="f5f74-106">Например, если концентратор событий состоит из четырех секций и одна из них перемещается с одного сервера на другой в рамках операции балансировки нагрузки, то вы можете по-прежнему выполнять отправку и получение из трех оставшихся секций.</span><span class="sxs-lookup"><span data-stu-id="f5f74-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server to another in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="f5f74-107">Кроме того, большее число секций обеспечивает большее количество параллельных модулей чтения для обработки данных, повышая тем самым суммарную пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="f5f74-107">Additionally, having more partitions enables you to have more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="f5f74-108">Понимание основных принципов и последствий секционирования и упорядочения в распределенной системе является критически важным аспектом разработки решений.</span><span class="sxs-lookup"><span data-stu-id="f5f74-108">Understanding the implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="f5f74-109">Чтобы лучше понять компромисс между упорядочением и доступностью, ознакомьтесь с [теоремой CAP](https://en.wikipedia.org/wiki/CAP_theorem) (известной также как теорема Брюера).</span><span class="sxs-lookup"><span data-stu-id="f5f74-109">To help explain the trade-off between ordering and availability, see the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="f5f74-110">В ней решается вопрос выбора между согласованностью, доступностью и устойчивостью к разделению.</span><span class="sxs-lookup"><span data-stu-id="f5f74-110">This theorem discusses the choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="f5f74-111">В теореме Брюера согласованность и доступность определяются следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f5f74-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="f5f74-112">Устойчивость к разделению — это способность системы обработки данных продолжать обработку, даже если в одной из секций происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="f5f74-112">Partition tolerance: the ability of a data processing system to continue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="f5f74-113">Доступность — защищенный от сбоев узел возвращает обоснованный ответ в течение приемлемого времени (без ошибок и простоев).</span><span class="sxs-lookup"><span data-stu-id="f5f74-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="f5f74-114">Согласованность — при операциях чтения гарантируется получение результатов самых поздних операций записи для данного клиента.</span><span class="sxs-lookup"><span data-stu-id="f5f74-114">Consistency: a read is guaranteed to return the most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="f5f74-115">Устойчивость к разделению</span><span class="sxs-lookup"><span data-stu-id="f5f74-115">Partition tolerance</span></span>
<span data-ttu-id="f5f74-116">В основе концентраторов событий лежит модель секционированных данных.</span><span class="sxs-lookup"><span data-stu-id="f5f74-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="f5f74-117">Количество секций в концентраторе событий можно настроить во время установки, и это значение невозможно изменить позднее.</span><span class="sxs-lookup"><span data-stu-id="f5f74-117">You can configure the number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="f5f74-118">Поскольку в концентраторах событий необходимо использовать секции, вам требуется принять решение о доступности и согласованности для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="f5f74-118">Since you must use partitions with Event Hubs, you have to make a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="f5f74-119">Доступность</span><span class="sxs-lookup"><span data-stu-id="f5f74-119">Availability</span></span>
<span data-ttu-id="f5f74-120">Самый простой способ начать работу с концентраторами событий — использовать поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f5f74-120">The simplest way to get started with Event Hubs is to use the default behavior.</span></span> <span data-ttu-id="f5f74-121">Если вы создадите объект `EventHubClient` и используете метод `Send`, то события автоматически распределятся между секциями в концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="f5f74-121">If you create a new `EventHubClient` object and use the `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="f5f74-122">Такое поведение обеспечивает наивысший показатель времени непрерывной работы.</span><span class="sxs-lookup"><span data-stu-id="f5f74-122">This behavior allows for the greatest amount of up time.</span></span>

<span data-ttu-id="f5f74-123">Для вариантов использования, требующих максимального времени работы, эта модель является предпочтительной.</span><span class="sxs-lookup"><span data-stu-id="f5f74-123">For use cases that require the maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="f5f74-124">Целостность</span><span class="sxs-lookup"><span data-stu-id="f5f74-124">Consistency</span></span>
<span data-ttu-id="f5f74-125">В некоторых сценариях важным может быть упорядочение событий.</span><span class="sxs-lookup"><span data-stu-id="f5f74-125">In some scenarios, the ordering of events can be important.</span></span> <span data-ttu-id="f5f74-126">Например, вам может потребоваться, чтобы серверная система обрабатывала команду обновления перед командой удаления.</span><span class="sxs-lookup"><span data-stu-id="f5f74-126">For example, you may want your back-end system to process an update command before a delete command.</span></span> <span data-ttu-id="f5f74-127">В данном случае можно задать ключ секции для события или использовать объект `PartitionSender`, чтобы отправлять события только в определенную секцию.</span><span class="sxs-lookup"><span data-stu-id="f5f74-127">In this instance, you can either set the partition key on an event, or use a `PartitionSender` object to only send events to a certain partition.</span></span> <span data-ttu-id="f5f74-128">Такое действие гарантирует, что при считывании этих события из секции они будут считываться по порядку.</span><span class="sxs-lookup"><span data-stu-id="f5f74-128">Doing so ensures that when these events are read from the partition, they are read in order.</span></span>

<span data-ttu-id="f5f74-129">Применяя такую конфигурацию, учитывайте, что в случае недоступности определенной секции, в которую выполняется отправка, вы получите сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="f5f74-129">With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="f5f74-130">Для сравнения: если не привязывать отправку к одной секции, то служба концентраторов событий отправляет событие в следующую доступную секцию.</span><span class="sxs-lookup"><span data-stu-id="f5f74-130">As a point of comparison, if you do not have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.</span></span>

<span data-ttu-id="f5f74-131">Одно из возможных решений для обеспечения упорядочения с максимальным увеличением времени бесперебойной работы — объединение событий в рамках приложения обработки событий.</span><span class="sxs-lookup"><span data-stu-id="f5f74-131">One possible solution to ensure ordering, while also maximizing up time, would be to aggregate events as part of your event processing application.</span></span> <span data-ttu-id="f5f74-132">Самый простой способ это сделать — пометить событие пользовательским свойством SequenceNumber (Порядковый номер).</span><span class="sxs-lookup"><span data-stu-id="f5f74-132">The easiest way to accomplish this is to stamp your event with a custom sequence number property.</span></span> <span data-ttu-id="f5f74-133">Пример кода приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="f5f74-133">The following code shows an example:</span></span>

```csharp
// Get the latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="f5f74-134">В этом примере событие отправляется в одну из доступных секций в концентраторе событий, и ему задается соответствующий порядковый номер из приложения.</span><span class="sxs-lookup"><span data-stu-id="f5f74-134">This example sends your event to one of the available partitions in your event hub, and sets the corresponding sequence number from your application.</span></span> <span data-ttu-id="f5f74-135">Для этого решения требуется, чтобы обрабатывающее приложение сохраняло состояние, но отправителям предоставлялась конечная точка, которая скорее всего будет доступна.</span><span class="sxs-lookup"><span data-stu-id="f5f74-135">This solution requires state to be kept by your processing application, but gives your senders an endpoint that is more likely to be available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5f74-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5f74-136">Next steps</span></span>
<span data-ttu-id="f5f74-137">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="f5f74-137">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="f5f74-138">Обзор службы концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="f5f74-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="f5f74-139">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="f5f74-139">Create an event hub</span></span>](event-hubs-create.md)
