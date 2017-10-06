---
title: "aaaWhat является концентраторов событий Azure и зачем использовать | Документы Microsoft"
description: "Общие сведения и введение tooAzure концентраторов событий - масштабирования в облаке приема данных телеметрии из веб-сайтов, приложений и устройств"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="fdce5-103">Что такое концентраторы событий?</span><span class="sxs-lookup"><span data-stu-id="fdce5-103">What is Event Hubs?</span></span>

<span data-ttu-id="fdce5-104">Концентраторы событий Azure — это высокомасштабируемая платформа потоковой передачи данных и служба потребления событий, принимающая и обрабатывающая миллионы событий в секунду.</span><span class="sxs-lookup"><span data-stu-id="fdce5-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="fdce5-105">Концентраторы событий могут обрабатывать и сохранять события, данные и телеметрию, созданные распределенным программным обеспечением и устройствами.</span><span class="sxs-lookup"><span data-stu-id="fdce5-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="fdce5-106">Данные отправляются в концентратор событий tooan можно преобразовать и хранятся с использованием любого поставщика аналитика в реальном времени или адаптеры пакетной обработки хранилища.</span><span class="sxs-lookup"><span data-stu-id="fdce5-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="fdce5-107">С возможностью tooprovide hello [возможности публикации и подписки](https://msdn.microsoft.com/library/aa560414.aspx) с низкой задержкой и в большом масштабе, концентраторы событий служит hello «для увеличения» для больших данных.</span><span class="sxs-lookup"><span data-stu-id="fdce5-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="fdce5-108">Каковы преимущества концентраторов событий?</span><span class="sxs-lookup"><span data-stu-id="fdce5-108">Why use Event Hubs?</span></span>

<span data-ttu-id="fdce5-109">Концентраторы событий и функции обработки телеметрии используются для решения следующих задач:</span><span class="sxs-lookup"><span data-stu-id="fdce5-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="fdce5-110">инструментирования приложения;</span><span class="sxs-lookup"><span data-stu-id="fdce5-110">Application instrumentation</span></span>
* <span data-ttu-id="fdce5-111">взаимодействия с пользователем или обработки рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="fdce5-111">User experience or workflow processing</span></span>
* <span data-ttu-id="fdce5-112">использования сценариев "Интернета вещей" (IoT).</span><span class="sxs-lookup"><span data-stu-id="fdce5-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="fdce5-113">Например, концентраторы событий также позволяют отслеживать поведение в мобильных приложениях, регистрировать события в играх для игровых консолей, а также собирать данные о трафике от веб-ферм или данные телеметрии от промышленного оборудования, подключенных автомобилей или других устройств.</span><span class="sxs-lookup"><span data-stu-id="fdce5-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="fdce5-114">Общие сведения о концентраторах событий Azure</span><span class="sxs-lookup"><span data-stu-id="fdce5-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="fdce5-115">Hello общих роль концентраторов событий в архитектурах решений — hello «дверью» для конвейера событий, часто называют *службой сбора событий*.</span><span class="sxs-lookup"><span data-stu-id="fdce5-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="fdce5-116">Это событие — это компонент или служба, которая располагается между издателей событий и производственного hello toodecouple потребителей событий из потока событий от использования этих событий hello.</span><span class="sxs-lookup"><span data-stu-id="fdce5-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="fdce5-117">Hello на этом рисунке показана эта архитектура:</span><span class="sxs-lookup"><span data-stu-id="fdce5-117">hello following figure depicts this architecture:</span></span>

![Концентраторы событий](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="fdce5-119">Концентраторы событий позволяют обрабатывать потоки сообщений. По своим характеристикам они отличаются от традиционных корпоративных служб обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="fdce5-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="fdce5-120">Концентраторы событий разработаны с учетом высокой пропускной способности и сценариев обработки событий.</span><span class="sxs-lookup"><span data-stu-id="fdce5-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="fdce5-121">Таким образом, концентраторы событий отличается от [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) обмена сообщениями и не реализует ряд возможностей hello, доступных для [сообщений Service Bus](/azure/service-bus-messaging/) сущности, такие как разделы.</span><span class="sxs-lookup"><span data-stu-id="fdce5-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="fdce5-122">Особенности концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="fdce5-122">Event Hubs features</span></span>

<span data-ttu-id="fdce5-123">Концентраторы событий содержит следующие основные элементы hello:</span><span class="sxs-lookup"><span data-stu-id="fdce5-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="fdce5-124">[**Производители или издатели событий**](event-hubs-features.md#event-publishers): сущность, которая отправляет концентратора событий tooan данных.</span><span class="sxs-lookup"><span data-stu-id="fdce5-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="fdce5-125">Событие публикуется по протоколу AMQP 1.0 или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fdce5-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="fdce5-126">[**Записать**](event-hubs-features.md#capture): позволяет концентраторов событий toocapture потоковой передачи данных и сохраняет его в учетную запись службы хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="fdce5-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="fdce5-127">[**Секции**](event-hubs-features.md#partitions): каждый потребитель tooonly чтение определенное подмножество или раздел, включает hello поток событий.</span><span class="sxs-lookup"><span data-stu-id="fdce5-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="fdce5-128">[**Маркеры SAS**](event-hubs-features.md#sas-tokens): Определяет и выполняет проверку подлинности издатель событий hello.</span><span class="sxs-lookup"><span data-stu-id="fdce5-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="fdce5-129">[**Потребители событий**](event-hubs-features.md#event-consumers) — сущности, считывающие данные из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="fdce5-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="fdce5-130">Потребители событий подключаются по протоколу AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="fdce5-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="fdce5-131">[**Группы потребителей**](event-hubs-features.md#consumer-groups): предоставляет каждой кратной использование приложений с отдельное представление потока событий hello, включение этих потребителей tooact независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="fdce5-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="fdce5-132">[**Единицы пропускной способности**](event-hubs-features.md#capacity) — это предварительно приобретенные единицы емкости.</span><span class="sxs-lookup"><span data-stu-id="fdce5-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="fdce5-133">Максимальный масштаб одной секции составляет одну единицу пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="fdce5-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="fdce5-134">Технические сведения об этих и других возможностей концентраторов событий см. в разделе hello [Общие сведения о возможностях концентраторов событий](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="fdce5-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fdce5-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fdce5-135">Next steps</span></span>

<span data-ttu-id="fdce5-136">Подробные сведения о ценах см. на странице [цен на концентраторы событий](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="fdce5-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="fdce5-137">Дополнительные сведения о концентраторах событий посетите hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="fdce5-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="fdce5-138">Начните работу с [руководства по концентраторам событий](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="fdce5-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="fdce5-139">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="fdce5-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="fdce5-140">Примеры приложений, использующих концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="fdce5-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

