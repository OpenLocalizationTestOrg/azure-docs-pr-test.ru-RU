---
title: "aaaAvailability и согласованность концентраторов событий Azure | Документы Microsoft"
description: "Каким образом разделяет tooprovide hello максимальный объем доступности и согласованности с помощью концентраторов событий Azure."
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
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="d550a-103">Доступность и согласованность в концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="d550a-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="d550a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d550a-104">Overview</span></span>
<span data-ttu-id="d550a-105">Концентраторы событий Azure использует [секционирование модели](event-hubs-features.md#partitions) tooimprove доступности и параллелизации в концентраторе одно событие.</span><span class="sxs-lookup"><span data-stu-id="d550a-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="d550a-106">Например если концентратор событий состоит из четырех секций, а для одного из этих разделов перемещается с одного сервера tooanother в операции с балансировкой нагрузки, можно по-прежнему отправлять и получать из трех разделов.</span><span class="sxs-lookup"><span data-stu-id="d550a-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="d550a-107">Кроме того, наличие нескольких секций позволяет toohave более параллельных чтений, обработки данных, повышения вашей суммарную пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="d550a-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="d550a-108">Основные сведения о последствиях hello секционирование и упорядочение в распределенной системе является ключевой аспект архитектуры решения.</span><span class="sxs-lookup"><span data-stu-id="d550a-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="d550a-109">toohelp объяснить hello компромисса между упорядочения и доступности см. в разделе hello [Крепления Теорема](https://en.wikipedia.org/wiki/CAP_theorem), также называемой Теорема Brewer элемента.</span><span class="sxs-lookup"><span data-stu-id="d550a-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="d550a-110">Это Теорема рассматриваются hello Выбор между согласованности, доступность и отказоустойчивость секции.</span><span class="sxs-lookup"><span data-stu-id="d550a-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="d550a-111">В теореме Брюера согласованность и доступность определяются следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d550a-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="d550a-112">Секции отклонение: hello возможность toocontinue системы обработки данных, обработки данных, даже если происходит сбой секции.</span><span class="sxs-lookup"><span data-stu-id="d550a-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="d550a-113">Доступность — защищенный от сбоев узел возвращает обоснованный ответ в течение приемлемого времени (без ошибок и простоев).</span><span class="sxs-lookup"><span data-stu-id="d550a-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="d550a-114">: Чтение гарантируется согласованность tooreturn hello самой последней записи для данного клиента.</span><span class="sxs-lookup"><span data-stu-id="d550a-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="d550a-115">Устойчивость к разделению</span><span class="sxs-lookup"><span data-stu-id="d550a-115">Partition tolerance</span></span>
<span data-ttu-id="d550a-116">В основе концентраторов событий лежит модель секционированных данных.</span><span class="sxs-lookup"><span data-stu-id="d550a-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="d550a-117">Можно настроить hello количество разделов в концентраторе событий во время установки, но не может изменить это значение позднее.</span><span class="sxs-lookup"><span data-stu-id="d550a-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="d550a-118">Поскольку секции необходимо использовать с концентраторами событий, у вас toomake принятия решений о доступности и согласованности для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d550a-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="d550a-119">Доступность</span><span class="sxs-lookup"><span data-stu-id="d550a-119">Availability</span></span>
<span data-ttu-id="d550a-120">Hello tooget простейший способ работы с концентраторами событий является поведением по умолчанию hello toouse.</span><span class="sxs-lookup"><span data-stu-id="d550a-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="d550a-121">Если вы создаете новый `EventHubClient` и используйте hello `Send` метода события автоматически распространяются среди разделов в концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="d550a-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="d550a-122">Это поведение позволяет hello значительная часть времени.</span><span class="sxs-lookup"><span data-stu-id="d550a-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="d550a-123">Для случаев, требующих hello минимальное время эта модель является предпочтительной.</span><span class="sxs-lookup"><span data-stu-id="d550a-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="d550a-124">Целостность</span><span class="sxs-lookup"><span data-stu-id="d550a-124">Consistency</span></span>
<span data-ttu-id="d550a-125">В некоторых сценариях может быть важно hello упорядоченных событий.</span><span class="sxs-lookup"><span data-stu-id="d550a-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="d550a-126">Например может потребоваться вашей внутренней системы tooprocess команды update перед выполнением команды delete.</span><span class="sxs-lookup"><span data-stu-id="d550a-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="d550a-127">В данном экземпляре, задайте ключ раздела hello события или использовать `PartitionSender` tooonly объекта отправки событий tooa определенную секцию.</span><span class="sxs-lookup"><span data-stu-id="d550a-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="d550a-128">Это гарантирует, что если эти события считываются из секции hello, они считываются в порядке.</span><span class="sxs-lookup"><span data-stu-id="d550a-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="d550a-129">В этой конфигурации следует помнить, что в случае недоступности toowhich hello заданной секции, отправляемого вы получите ответ с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="d550a-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="d550a-130">Как точка сравнения Если нет соответствия tooa с одним разделом hello службы концентраторов событий отправляет на событие toohello следующий доступный раздел.</span><span class="sxs-lookup"><span data-stu-id="d550a-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="d550a-131">Один из возможных решений tooensure, упорядочение, повышая также системы, будет tooaggregate события как часть вашего приложения обработки событий.</span><span class="sxs-lookup"><span data-stu-id="d550a-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="d550a-132">Это Hello tooaccomplish простым способом является toostamp события со свойством пользовательские последовательности чисел.</span><span class="sxs-lookup"><span data-stu-id="d550a-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="d550a-133">Привет, следующий код представляет собой пример:</span><span class="sxs-lookup"><span data-stu-id="d550a-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="d550a-134">В этом примере отправляет вашей tooone событий hello доступных разделов в концентраторе событий и задает соответствующий номер последовательности hello из приложения.</span><span class="sxs-lookup"><span data-stu-id="d550a-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="d550a-135">Это решение требует toobe состояние приложения обработки, поддерживаемые, но предоставляет конечную точку, скорее всего, toobe доступных вашей отправителей.</span><span class="sxs-lookup"><span data-stu-id="d550a-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d550a-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d550a-136">Next steps</span></span>
<span data-ttu-id="d550a-137">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="d550a-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="d550a-138">Обзор службы концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="d550a-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="d550a-139">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="d550a-139">Create an event hub</span></span>](event-hubs-create.md)
