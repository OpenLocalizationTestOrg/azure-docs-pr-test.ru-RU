---
title: "Принципы отправки сообщений Центра Интернета вещей Azure с устройства в облако | Документы Майкрософт"
description: "Руководство разработчика — обмен сообщениями между устройством и облаком с помощью Центра Интернета вещей. Содержит сведения об отправке данных телеметрии и других данных и использовании маршрутизации для доставки сообщений."
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
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="61861-104">Отправка сообщений, пересылаемых с устройства в облако, в Центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="61861-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="61861-105">Для отправки данных телеметрии временных рядов и оповещений с устройств в серверной части решения отправляйте сообщения "с устройства в облако" с вашего устройства в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="61861-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="61861-106">Обсуждение других вариантов передачи данных с устройства в облако, поддерживаемых Центром Интернета вещей, см. в [руководстве по обмену данными между устройством и облаком][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="61861-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="61861-107">Отправка сообщений с устройства в облако осуществляется через обращенную к устройству конечную точку (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="61861-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="61861-108">Затем правила маршрутизации направляют сообщения в одну из конечных точек, доступных для службы, в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="61861-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="61861-109">Для определения маршрута правила маршрутизации используют заголовок и текст сообщений, отправляемых с устройства в облако, которые проходят через Центр.</span><span class="sxs-lookup"><span data-stu-id="61861-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="61861-110">По умолчанию сообщения направляются во встроенную конечную точку, доступную для службы (**messages/events**), которая совместима с [концентраторами событий][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="61861-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="61861-111">Таким образом, чтобы получать сообщения, отправляемые из устройства в облако, в серверной части решения, можно использовать стандартную [интеграцию концентраторов событий и пакетов SDK][lnk-compatible-endpoint].</span><span class="sxs-lookup"><span data-stu-id="61861-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="61861-112">Для реализация отправки сообщений с устройства в облако Центр Интернета вещей использует модель потоковой передачи сообщений.</span><span class="sxs-lookup"><span data-stu-id="61861-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="61861-113">Сообщения Центра Интернета вещей, отправляемые с устройства в облако, больше похожи на *события* [концентраторов событий][lnk-event-hubs], чем на *сообщения* [служебной шины][lnk-servicebus], где большое количество событий проходит через службу и может считываться несколькими модулями чтения.</span><span class="sxs-lookup"><span data-stu-id="61861-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="61861-114">Отправка сообщений с устройства в облако с помощью Центра Интернета вещей имеет следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="61861-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="61861-115">Сообщения, отправляемые с устройства в облако, устойчивы и хранятся в конечной точке по умолчанию **messages/events** Центра Интернета вещей до семи дней.</span><span class="sxs-lookup"><span data-stu-id="61861-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="61861-116">Размер сообщений, поступающих с устройства в облако, не может превышать 256 КБ, и их можно объединять в пакеты, чтобы оптимизировать отправку.</span><span class="sxs-lookup"><span data-stu-id="61861-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="61861-117">Размер пакетов не может превышать 256 КБ.</span><span class="sxs-lookup"><span data-stu-id="61861-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="61861-118">Как объяснено в разделе [Управление доступом к Центру Интернета вещей][lnk-devguide-security], Центр Интернета вещей обеспечивает аутентификацию и контроль доступа для каждого устройства.</span><span class="sxs-lookup"><span data-stu-id="61861-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="61861-119">В Центре Интернета вещей можно создать до 10 пользовательских конечных точек.</span><span class="sxs-lookup"><span data-stu-id="61861-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="61861-120">Сообщения доставляются в конечные точки, исходя из маршрутов, настроенных в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="61861-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="61861-121">Дополнительные сведения см. в статье, посвященной [правилам маршрутизации](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="61861-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="61861-122">Центр Интернета вещей обеспечивает работу большого числа одновременно подключенных устройств (см. раздел [Квоты и регулирование][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="61861-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="61861-123">Центр Интернета вещей не позволяет выполнять произвольное секционирование.</span><span class="sxs-lookup"><span data-stu-id="61861-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="61861-124">Сообщения, отправляемые с устройства в облако, секционируются по исходному идентификатору **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="61861-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="61861-125">Дополнительные сведения о различиях между Центром Интернета вещей и службой концентраторов событий см. в разделе [Сравнение центра Интернета вещей Azure и концентраторов событий Azure][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="61861-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="61861-126">Отправка данных, не относящихся к телеметрии</span><span class="sxs-lookup"><span data-stu-id="61861-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="61861-127">Часто устройства отправляют не только точки данных телеметрии, но и сообщения и запросы, требующие отдельного выполнения и обработки в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="61861-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="61861-128">Например, устройство отправляет критические оповещения, которые должны активировать определенное действие в серверной части.</span><span class="sxs-lookup"><span data-stu-id="61861-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="61861-129">Можно создать [правило маршрутизации][lnk-devguide-custom] для отправки таких сообщений в конечную точку, назначенную для их обработки, в зависимости от заголовка сообщения или значения в его тексте.</span><span class="sxs-lookup"><span data-stu-id="61861-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="61861-130">Дополнительные сведения о том, как лучше всего обработать такие сообщения, см. в статье [Учебник: как обрабатывать сообщения, отправляемые с устройства центра IoT в облако, с помощью .Net][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="61861-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="61861-131">Маршрутизация сообщений, отправленных с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="61861-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="61861-132">Существует два варианта маршрутизации сообщений, отправляемых с устройства в облако, во внутренних приложениях.</span><span class="sxs-lookup"><span data-stu-id="61861-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="61861-133">Использование встроенной и [совместимой с концентраторами событий конечной точки][lnk-compatible-endpoint], с помощью которой внутренние приложения считывают сообщения, отправляемые в Центр с устройства.</span><span class="sxs-lookup"><span data-stu-id="61861-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="61861-134">Дополнительные сведения о встроенных конечных точках, совместимых с концентраторами событий, см. в разделе [Чтение сообщений, пересылаемых с устройства в облако, из встроенной конечной точки][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="61861-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="61861-135">Правила маршрутизации можно использовать для отправки сообщений в пользовательские конечные точки в собственном центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="61861-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="61861-136">Пользовательские конечные точки позволяют внутренним приложениям считывать сообщения, отправляемые с устройства в облако, с помощью концентраторов событий, очередей или разделов служебной шины.</span><span class="sxs-lookup"><span data-stu-id="61861-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="61861-137">Дополнительные сведения о маршрутизации и пользовательских конечных точках см. в разделе [Использование пользовательских конечных точек и правил маршрутизации для сообщений, отправляемых с устройства в облако][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="61861-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="61861-138">Свойства для защиты от спуфинга</span><span class="sxs-lookup"><span data-stu-id="61861-138">Anti-spoofing properties</span></span>

<span data-ttu-id="61861-139">Чтобы избежать спуфинга устройств при работе с сообщениями, отправляемыми с устройства в облако, центр IoT отмечает все сообщения такими свойствами:</span><span class="sxs-lookup"><span data-stu-id="61861-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="61861-140">**ConnectionDeviceId;**</span><span class="sxs-lookup"><span data-stu-id="61861-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="61861-141">**ConnectionDeviceGenerationId;**</span><span class="sxs-lookup"><span data-stu-id="61861-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="61861-142">**ConnectionAuthMethod.**</span><span class="sxs-lookup"><span data-stu-id="61861-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="61861-143">Первые два свойства содержат параметры **deviceId** и **generationId** исходного устройства (согласно разделу [Device identity properties][lnk-device-properties] (Свойства удостоверений устройств)).</span><span class="sxs-lookup"><span data-stu-id="61861-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="61861-144">Свойство **ConnectionAuthMethod** содержит сериализованный объект JSON, имеющий такие свойства:</span><span class="sxs-lookup"><span data-stu-id="61861-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="61861-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61861-145">Next steps</span></span>

<span data-ttu-id="61861-146">Дополнительные сведения о пакетах SDK, которые можно использовать для отправки сообщений с устройства в облако, см. в статье, посвященной [пакетам SDK для Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="61861-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="61861-147">Руководства [по началу работы][lnk-get-started] демонстрируют отправку сообщений "с устройства в облако" с моделируемых и физических устройств.</span><span class="sxs-lookup"><span data-stu-id="61861-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="61861-148">Дополнительные сведения см. в руководстве [по обработке сообщений Центра Интернета вещей, отправляемых с устройства в облако, с помощью маршрутов][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="61861-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
