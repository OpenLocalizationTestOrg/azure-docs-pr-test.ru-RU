---
title: "пользовательские конечные точки центра IoT Azure aaaUnderstand | Документы Microsoft"
description: "Руководство разработчика - с помощью маршрутизации правил конечных toocustom tooroute сообщения из устройства в облако."
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="326db-103">Использование правил маршрутизации и пользовательских конечных точек для сообщений, отправляемых с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="326db-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="326db-104">Центр IoT позволяет tooroute [сообщения из устройства в облако] [ lnk-device-to-cloud] tooIoT концентратора, конечные точки службы с выходом в зависимости от свойств сообщения.</span><span class="sxs-lookup"><span data-stu-id="326db-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="326db-105">Здравствуйте toosend гибкость обеспечивает правила маршрутизации сообщений, где они должны toogo без hello для сообщения tooprocess дополнительных служб или требуются toowrite дополнительный код.</span><span class="sxs-lookup"><span data-stu-id="326db-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="326db-106">Каждое правило маршрутизации, настроенного имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="326db-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="326db-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="326db-107">Property</span></span>      | <span data-ttu-id="326db-108">Описание</span><span class="sxs-lookup"><span data-stu-id="326db-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="326db-109">**Имя**</span><span class="sxs-lookup"><span data-stu-id="326db-109">**Name**</span></span>      | <span data-ttu-id="326db-110">Hello уникальное имя, которое определяет правила hello.</span><span class="sxs-lookup"><span data-stu-id="326db-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="326db-111">**Источник**</span><span class="sxs-lookup"><span data-stu-id="326db-111">**Source**</span></span>    | <span data-ttu-id="326db-112">Происхождение Hello hello данных потока ответных toobe.</span><span class="sxs-lookup"><span data-stu-id="326db-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="326db-113">Например, телеметрия устройства.</span><span class="sxs-lookup"><span data-stu-id="326db-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="326db-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="326db-114">**Condition**</span></span> | <span data-ttu-id="326db-115">выражение запроса Hello для правила маршрутизации hello, которое выполняется заголовки и текст приветственное сообщение, а затем использовать toodetermine, является ли совпадение для конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="326db-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="326db-116">Дополнительные сведения о построении условие маршрутизации см. в разделе hello [ссылка - язык запросов для задания и близнецы устройства][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="326db-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="326db-117">**Конечная точка**</span><span class="sxs-lookup"><span data-stu-id="326db-117">**Endpoint**</span></span>  | <span data-ttu-id="326db-118">Имя конечной точки hello, где центр IoT отправляет сообщения, которые соответствуют условию hello Hello.</span><span class="sxs-lookup"><span data-stu-id="326db-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="326db-119">Конечные точки должны находиться в hello же регионе, что центр IoT hello, в противном случае может взиматься для записывает в различных регионах.</span><span class="sxs-lookup"><span data-stu-id="326db-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="326db-120">Одно сообщение может соответствовать hello условие для нескольких правил маршрутизации, в которых регистр центра IoT доставляет hello сообщение toohello конечная точка, связанная с каждым правилом сопоставленная.</span><span class="sxs-lookup"><span data-stu-id="326db-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="326db-121">Центр IoT также автоматически deduplicates доставки сообщений, если сообщение соответствует несколько правил, имеющих hello того же конечного расположения, оно записывается только назначения toothat один раз.</span><span class="sxs-lookup"><span data-stu-id="326db-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="326db-122">Центр Интернета вещей имеет [встроенную конечную точку][lnk-built-in] по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="326db-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="326db-123">Можно создать настраиваемые конечные точки tooroute сообщения tooby связывание других служб на концентраторе toohello подписки.</span><span class="sxs-lookup"><span data-stu-id="326db-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="326db-124">Сейчас Центр Интернета вещей поддерживает использование следующих служб в качестве пользовательских конечных точек: концентраторы событий, очереди служебной шины и разделы служебной шины.</span><span class="sxs-lookup"><span data-stu-id="326db-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="326db-125">Очереди и разделы служебной шины, для которых включены **сеансы** или **поиск повторяющихся данных**, не поддерживаются в качестве пользовательских конечных точек.</span><span class="sxs-lookup"><span data-stu-id="326db-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="326db-126">Дополнительные сведения о создании пользовательских конечных точек в Центре Интернета вещей см. в статье [Руководство. Конечные точки Центра Интернета вещей][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="326db-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="326db-127">Дополнительные сведения о чтении из пользовательских конечных точек см. в статьях, посвященных:</span><span class="sxs-lookup"><span data-stu-id="326db-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="326db-128">чтению из [концентраторов событий][lnk-getstarted-eh];</span><span class="sxs-lookup"><span data-stu-id="326db-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="326db-129">чтению из [очередей служебной шины][lnk-getstarted-queue];</span><span class="sxs-lookup"><span data-stu-id="326db-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="326db-130">чтению из [разделов служебной шины][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="326db-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="326db-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="326db-131">Next steps</span></span>

<span data-ttu-id="326db-132">Дополнительные сведения о конечных точках Центра Интернета вещей см. в [этом разделе][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="326db-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="326db-133">Дополнительные сведения о языке запросов hello можно использовать правила маршрутизации toodefine см. в разделе [центр IoT язык запросов для близнецы устройства, задания и маршрутизация сообщений][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="326db-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="326db-134">Hello [сообщения из устройства в облако центра IoT процесса с помощью маршрутов] [ lnk-d2c-tutorial] учебнике показано, как правила маршрутизации toouse и пользовательские конечные точки.</span><span class="sxs-lookup"><span data-stu-id="326db-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
