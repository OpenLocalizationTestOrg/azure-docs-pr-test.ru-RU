---
title: "обмен сообщениями устройства в облако Azure IoT Hub aaaUnderstand | Документы Microsoft"
description: "Руководство разработчика - как toouse устройства в облако обмена сообщениями с центром IoT. Содержит сведения об отправке данных телеметрии и не telemtry и с помощью маршрутизации сообщений toodeliver."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="79071-104">Отправлять сообщения из устройства в облако tooIoT концентратора</span><span class="sxs-lookup"><span data-stu-id="79071-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="79071-105">Данные телеметрии toosend временных рядов и предупреждений с вашего устройства tooyour решения серверной части, отправлять сообщения устройства в облако из центра IoT tooyour вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="79071-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="79071-106">Обсуждение других вариантов передачи данных с устройства в облако, поддерживаемых Центром Интернета вещей, см. в [руководстве по обмену данными между устройством и облаком][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="79071-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="79071-107">Отправка сообщений с устройства в облако осуществляется через обращенную к устройству конечную точку (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="79071-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="79071-108">Правила маршрутизации, а затем Маршрутизация вашей tooone сообщений из конечных точек службы с выходом hello концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="79071-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="79071-109">Использовать правила маршрутизации hello заголовки и текст сообщений hello устройства в облако, проходящие через ваш концентратор toodetermine где tooroute их.</span><span class="sxs-lookup"><span data-stu-id="79071-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="79071-110">По умолчанию сообщения, перенаправленное toohello, встроенные конечной точки службы с выходом (**сообщений и событий**), который совместим с [концентраторов событий][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="79071-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="79071-111">Таким образом, можно использовать стандартный [интеграции концентраторов событий и пакетов SDK] [ lnk-compatible-endpoint] tooreceive сообщения из устройства в облако в своем решении серверной части.</span><span class="sxs-lookup"><span data-stu-id="79071-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="79071-112">Для реализация отправки сообщений с устройства в облако Центр Интернета вещей использует модель потоковой передачи сообщений.</span><span class="sxs-lookup"><span data-stu-id="79071-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="79071-113">Скорее сообщения из устройства в облако центра IoT являются [концентраторов событий] [ lnk-event-hubs] *событий* чем [Service Bus] [ lnk-servicebus] *сообщения* в том, что имеется большое количество событий, передаваемых через службу hello, могут быть прочитаны несколько модулей чтения.</span><span class="sxs-lookup"><span data-stu-id="79071-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="79071-114">Устройства в облако обмена сообщениями с центром IoT имеет следующие характеристики hello.</span><span class="sxs-lookup"><span data-stu-id="79071-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="79071-115">Сообщения из устройства в облако, являются устойчивыми и сохраненные в по умолчанию центр IoT **сообщений и событий** конечную точку для копирования tooseven дней.</span><span class="sxs-lookup"><span data-stu-id="79071-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="79071-116">Сообщения из устройства в облако может быть не более 256 КБ и могут быть сгруппированы в пакетах, которые отправляет toooptimize.</span><span class="sxs-lookup"><span data-stu-id="79071-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="79071-117">Размер пакетов не может превышать 256 КБ.</span><span class="sxs-lookup"><span data-stu-id="79071-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="79071-118">Как описано в hello [tooIoT управления доступом концентратора] [ lnk-devguide-security] раздела центра IoT включает элемент управления доступом и проверка подлинности на устройство.</span><span class="sxs-lookup"><span data-stu-id="79071-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="79071-119">Центр IoT позволяет toocreate копирование too10 пользовательские конечные точки.</span><span class="sxs-lookup"><span data-stu-id="79071-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="79071-120">Сообщения доставляются toohello конечные точки, основанные на маршрутов, заданных в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="79071-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="79071-121">Дополнительные сведения см. в статье, посвященной [правилам маршрутизации](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="79071-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="79071-122">Центр Интернета вещей обеспечивает работу большого числа одновременно подключенных устройств (см. раздел [Квоты и регулирование][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="79071-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="79071-123">Центр Интернета вещей не позволяет выполнять произвольное секционирование.</span><span class="sxs-lookup"><span data-stu-id="79071-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="79071-124">Сообщения, отправляемые с устройства в облако, секционируются по исходному идентификатору **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="79071-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="79071-125">Дополнительные сведения об отличиях hello hello центр IoT и службы концентраторов событий см. в разделе [сравнения из центра IoT Azure и концентраторов событий Azure][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="79071-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="79071-126">Отправка данных, не относящихся к телеметрии</span><span class="sxs-lookup"><span data-stu-id="79071-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="79071-127">Часто кроме точек данных tootelemetry, устройства отправляют сообщения и запросов, которые требуют выполнения отдельных и обработка событий в серверной части решения hello.</span><span class="sxs-lookup"><span data-stu-id="79071-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="79071-128">Например критические оповещения, которые необходимо активировать определенное действие в hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="79071-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="79071-129">Можно легко написать [правила маршрутизации] [ lnk-devguide-custom] toosend эти типы сообщений tooan endpoint выделенного tootheir обработку в зависимости от заголовка сообщения hello или значения в тело сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="79071-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="79071-130">Дополнительные сведения о hello лучшим способом tooprocess этом kind сообщения hello в разделе [учебника: как tooprocess сообщения из устройства в облако центра IoT] [ lnk-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="79071-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="79071-131">Маршрутизация сообщений, отправленных с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="79071-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="79071-132">У вас есть два варианта для маршрутизации сообщения из устройства в облако tooyour серверной части приложения:</span><span class="sxs-lookup"><span data-stu-id="79071-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="79071-133">Используйте встроенные hello [концентратора событий-совместимой конечной точки] [ lnk-compatible-endpoint] сообщений tooenable серверной части приложения tooread hello устройства в облако, полученных hello концентратора.</span><span class="sxs-lookup"><span data-stu-id="79071-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="79071-134">toolearn о hello встроенных концентратора событий-совместимой конечной точки в разделе [чтения сообщения из устройства в облако из встроенных hello конечной точки][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="79071-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="79071-135">Использование маршрутизации правила toosend сообщения toocustom конечных точек в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="79071-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="79071-136">Пользовательские конечные точки позволяют сообщений серверной части приложения tooread устройства в облако с помощью концентраторов событий, Service Bus очереди или разделы служебной шины.</span><span class="sxs-lookup"><span data-stu-id="79071-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="79071-137">toolearn о маршрутизации и пользовательских конечных точек, в разделе [использовать пользовательские конечные точки и правила маршрутизации для сообщения из устройства в облако][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="79071-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="79071-138">Свойства для защиты от спуфинга</span><span class="sxs-lookup"><span data-stu-id="79071-138">Anti-spoofing properties</span></span>

<span data-ttu-id="79071-139">устройство tooavoid подделкой сообщения из устройства в облако, центр IoT штампы, все сообщения с hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="79071-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="79071-140">**ConnectionDeviceId;**</span><span class="sxs-lookup"><span data-stu-id="79071-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="79071-141">**ConnectionDeviceGenerationId;**</span><span class="sxs-lookup"><span data-stu-id="79071-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="79071-142">**ConnectionAuthMethod.**</span><span class="sxs-lookup"><span data-stu-id="79071-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="79071-143">Hello первых двух содержат hello **deviceId** и **generationId** из hello, рассчитанные на устройстве, согласно [свойства удостоверения устройства][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="79071-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="79071-144">Hello **ConnectionAuthMethod** свойство содержит сериализованный объект JSON, с hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="79071-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="79071-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79071-145">Next steps</span></span>

<span data-ttu-id="79071-146">Сведения о пакетах SDK hello можно использовать сообщения из устройства в облако toosend см [пакеты SDK Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="79071-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="79071-147">Hello [начать] [ lnk-get-started] руководствах показано, как сообщения toosend устройства в облако с имитацию и физических устройств.</span><span class="sxs-lookup"><span data-stu-id="79071-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="79071-148">Дополнительные сведения см. в разделе hello [сообщения из устройства в облако центра IoT процесса с помощью маршрутов] [ lnk-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="79071-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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
