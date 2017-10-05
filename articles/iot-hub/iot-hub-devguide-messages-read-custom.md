---
title: "Общие сведения о пользовательских конечных точках Центра Интернета вещей Azure | Документы Майкрософт"
description: "Руководство разработчика — использование правил маршрутизации для маршрутизации сообщений, передаваемых с устройства в облако, в пользовательские конечные точки."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="03784-103">Использование правил маршрутизации и пользовательских конечных точек для сообщений, отправляемых с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="03784-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="03784-104">Центр Интернета вещей позволяет направлять [сообщения, отправляемые с устройства в облако][lnk-device-to-cloud], в обращенные к службе конечные точки Центра Интернета вещей, исходя из свойств этих сообщений.</span><span class="sxs-lookup"><span data-stu-id="03784-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="03784-105">Правила маршрутизации обеспечивают гибкость, позволяя отправлять сообщения в нужном направлении без установки каких-либо дополнительных служб обработки сообщений или написания дополнительного кода.</span><span class="sxs-lookup"><span data-stu-id="03784-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="03784-106">Каждое настраиваемое правило маршрутизации имеет следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="03784-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="03784-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="03784-107">Property</span></span>      | <span data-ttu-id="03784-108">Описание</span><span class="sxs-lookup"><span data-stu-id="03784-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="03784-109">**Имя**</span><span class="sxs-lookup"><span data-stu-id="03784-109">**Name**</span></span>      | <span data-ttu-id="03784-110">Уникальное имя, которое определяет правило.</span><span class="sxs-lookup"><span data-stu-id="03784-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="03784-111">**Источник**</span><span class="sxs-lookup"><span data-stu-id="03784-111">**Source**</span></span>    | <span data-ttu-id="03784-112">Источник потока данных, в отношении которого выполняются действия.</span><span class="sxs-lookup"><span data-stu-id="03784-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="03784-113">Например, телеметрия устройства.</span><span class="sxs-lookup"><span data-stu-id="03784-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="03784-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="03784-114">**Condition**</span></span> | <span data-ttu-id="03784-115">Выражение запроса для правила маршрутизации, которое выполняется для заголовка и текста сообщения и используется для определения соответствия сообщения конечной точке.</span><span class="sxs-lookup"><span data-stu-id="03784-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="03784-116">Дополнительные сведения о создании условия маршрутизации см. в статье [Справочник по языку запросов Центр Интернета вещей для двойников устройств и заданий][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="03784-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="03784-117">**Конечная точка**</span><span class="sxs-lookup"><span data-stu-id="03784-117">**Endpoint**</span></span>  | <span data-ttu-id="03784-118">Имя конечной точки, в которую Центр Интернета вещей отправляет сообщения, соответствующие условию.</span><span class="sxs-lookup"><span data-stu-id="03784-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="03784-119">Конечные точки должны находиться в одном регионе с Центром Интернета вещей, в противном случае может взиматься плата за межрегиональный трафик.</span><span class="sxs-lookup"><span data-stu-id="03784-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="03784-120">Одно сообщение может соответствовать условиям в нескольких правилах маршрутизации. В таких случаях Центр Интернета вещей доставляет сообщение в конечную точку, связанную с каждым из этих правил.</span><span class="sxs-lookup"><span data-stu-id="03784-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="03784-121">Центр Интернета вещей также выполняет автоматическую дедупликацию доставки сообщений. То есть, если сообщение соответствует нескольким правилам, имеющим общее назначение, то оно записывается в это назначение только один раз.</span><span class="sxs-lookup"><span data-stu-id="03784-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="03784-122">Центр Интернета вещей имеет [встроенную конечную точку][lnk-built-in] по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="03784-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="03784-123">Кроме того, можно создать пользовательские конечные точки для маршрутизации сообщений, связав с Центром другие службы в подписке.</span><span class="sxs-lookup"><span data-stu-id="03784-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="03784-124">Сейчас Центр Интернета вещей поддерживает использование следующих служб в качестве пользовательских конечных точек: концентраторы событий, очереди служебной шины и разделы служебной шины.</span><span class="sxs-lookup"><span data-stu-id="03784-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="03784-125">Очереди и разделы служебной шины, для которых включены **сеансы** или **поиск повторяющихся данных**, не поддерживаются в качестве пользовательских конечных точек.</span><span class="sxs-lookup"><span data-stu-id="03784-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="03784-126">Дополнительные сведения о создании пользовательских конечных точек в Центре Интернета вещей см. в статье [Руководство. Конечные точки Центра Интернета вещей][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="03784-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="03784-127">Дополнительные сведения о чтении из пользовательских конечных точек см. в статьях, посвященных:</span><span class="sxs-lookup"><span data-stu-id="03784-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="03784-128">чтению из [концентраторов событий][lnk-getstarted-eh];</span><span class="sxs-lookup"><span data-stu-id="03784-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="03784-129">чтению из [очередей служебной шины][lnk-getstarted-queue];</span><span class="sxs-lookup"><span data-stu-id="03784-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="03784-130">чтению из [разделов служебной шины][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="03784-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="03784-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03784-131">Next steps</span></span>

<span data-ttu-id="03784-132">Дополнительные сведения о конечных точках Центра Интернета вещей см. в руководстве [Конечные точки Центра Интернета вещей][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="03784-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="03784-133">Дополнительные сведения о языке запросов, который используется для определения правил маршрутизации, см. в справочнике по [языку запросов Центра Интернета вещей для двойников устройств, заданий и маршрутизации сообщений][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="03784-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="03784-134">В руководстве [Обработка сообщений Центра Интернета вещей, отправляемых с устройства в облако, с использованием маршрутов][lnk-d2c-tutorial] демонстрируется использование правил маршрутизации и пользовательских конечных точек.</span><span class="sxs-lookup"><span data-stu-id="03784-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
