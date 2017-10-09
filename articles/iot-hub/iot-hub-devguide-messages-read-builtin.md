---
title: "встроенные конечной точки центра IoT Azure hello aaaUnderstand | Документы Microsoft"
description: "Руководство разработчика - описывает, как toouse hello встроенные читать устройства в облако концентратора событий-совместимой конечной точки сообщений."
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
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="e8868-103">Чтение сообщения из устройства в облако из встроенных hello конечной точки</span><span class="sxs-lookup"><span data-stu-id="e8868-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="e8868-104">По умолчанию сообщения, перенаправленное toohello, встроенные конечной точки службы с выходом (**сообщений и событий**), который совместим с [концентраторов событий][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="e8868-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="e8868-105">Эта конечная точка является в настоящее время доступными только с помощью hello [AMQP] [ lnk-amqp] протокола на порту 5671.</span><span class="sxs-lookup"><span data-stu-id="e8868-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="e8868-106">Центр IoT предоставляет hello следующие свойства tooenable вы toocontrol hello встроенных концентратора событий-совместимой конечной точки обмена сообщениями **сообщений и событий**.</span><span class="sxs-lookup"><span data-stu-id="e8868-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="e8868-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="e8868-107">Property</span></span>            | <span data-ttu-id="e8868-108">Описание</span><span class="sxs-lookup"><span data-stu-id="e8868-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="e8868-109">**Количество секций**</span><span class="sxs-lookup"><span data-stu-id="e8868-109">**Partition count**</span></span> | <span data-ttu-id="e8868-110">Установите это свойство на создание toodefine hello число [секций] [ lnk-event-hub-partitions] приеме событий устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="e8868-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="e8868-111">**Время хранения**</span><span class="sxs-lookup"><span data-stu-id="e8868-111">**Retention time**</span></span>  | <span data-ttu-id="e8868-112">Это свойство задает время в днях, в течение которого сообщения хранятся в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e8868-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="e8868-113">по умолчанию Hello один день, но его можно повысить tooseven дней.</span><span class="sxs-lookup"><span data-stu-id="e8868-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="e8868-114">Центр IoT можно также toomanage групп потребителей на hello встроенные устройства в облако конечная точка получения.</span><span class="sxs-lookup"><span data-stu-id="e8868-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="e8868-115">По умолчанию все сообщения, которые явно не соответствуют правило маршрутизации сообщения записываются toohello Встроенные конечной точки.</span><span class="sxs-lookup"><span data-stu-id="e8868-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="e8868-116">Если отключить этот резервный маршрут, то сообщения, которые явно не соответствуют ни одному правилу маршрутизации сообщений, будут удаляться.</span><span class="sxs-lookup"><span data-stu-id="e8868-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="e8868-117">Можно изменить срок хранения hello, либо программным способом с помощью hello [API REST поставщика ресурсов центра IoT][lnk-resource-provider-apis], или с помощью hello [портал Azure] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="e8868-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="e8868-118">Центр IoT предоставляет hello **сообщений и событий** встроенные конечную точку для настройки сервера служб tooread hello устройства в облако сообщений, полученных концентратор.</span><span class="sxs-lookup"><span data-stu-id="e8868-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="e8868-119">Эта конечная точка является событие концентратора совместимые, позволяющий toouse поддерживает любой службы концентраторов событий hello hello механизмы чтения сообщений.</span><span class="sxs-lookup"><span data-stu-id="e8868-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="e8868-120">Чтение из встроенных hello конечной точки</span><span class="sxs-lookup"><span data-stu-id="e8868-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="e8868-121">При использовании hello [Azure Service Bus SDK для .NET] [ lnk-servicebus-sdk] или hello [концентраторов событий - узел обработчика событий][lnk-eventprocessorhost], можно использовать любые соединения, центр IoT строки с hello правильные разрешения.</span><span class="sxs-lookup"><span data-stu-id="e8868-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="e8868-122">Затем с помощью **сообщений и событий** имени концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="e8868-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="e8868-123">При использовании SDK (или интеграции продуктов), не знают о центра IoT, необходимо извлечь концентратор событий-совместимой конечной точки и имя совместимое концентратора событий с параметры центра IoT hello в hello [портал Azure] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="e8868-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="e8868-124">В колонке концентратора IoT hello щелкните **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="e8868-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="e8868-125">В hello **встроенных конечных точек** щелкните **события**.</span><span class="sxs-lookup"><span data-stu-id="e8868-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="e8868-126">Hello колонке содержит hello следующие значения: **концентратора событий-совместимой конечной точки**, **концентратора событий-совместимое имя**, **секций**, **время хранения**, и **групп потребителей**.</span><span class="sxs-lookup"><span data-stu-id="e8868-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Параметры отправки сообщений с устройства в облако][img-eventhubcompatible]

<span data-ttu-id="e8868-128">Hello IoT Hub SDK требуется имя конечной точки центра IoT, являющееся hello **сообщений и событий** как показано в hello **конечные точки** колонку.</span><span class="sxs-lookup"><span data-stu-id="e8868-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="e8868-129">Если используется пакет SDK для hello требует **имя узла** или **пространства имен** значения, удалите hello схему из hello **концентратора событий-совместимой конечной точки**.</span><span class="sxs-lookup"><span data-stu-id="e8868-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="e8868-130">Например, если ваш конечная точка совместимое концентратора событий **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** бы  **центром IOT ns-myiothub 1234.servicebus.windows.net**и hello **имен** бы **центром IOT ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="e8868-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="e8868-131">Затем можно использовать любую политику общего доступа с hello **ServiceConnect** toohello tooconnect разрешения указанного концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="e8868-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="e8868-132">Если требуется toobuild строку подключения концентратора событий, используя сведения о предыдущих hello используйте hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="e8868-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="e8868-133">пакеты SDK Hello и интеграций, которые можно использовать с конечными точками совместимое концентратора событий, предоставляемых центра IoT включает элементы hello hello после списка:</span><span class="sxs-lookup"><span data-stu-id="e8868-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="e8868-134">[клиент концентраторов событий Java;](https://github.com/hdinsight/eventhubs-client)</span><span class="sxs-lookup"><span data-stu-id="e8868-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="e8868-135">[Воронка Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e8868-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="e8868-136">Можно просмотреть hello [spout источника](https://github.com/apache/storm/tree/master/external/storm-eventhubs) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="e8868-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="e8868-137">[интеграция Apache Spark.](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md)</span><span class="sxs-lookup"><span data-stu-id="e8868-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8868-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e8868-138">Next steps</span></span>

<span data-ttu-id="e8868-139">Дополнительные сведения о конечных точках Центра Интернета вещей см. в [этом разделе][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="e8868-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="e8868-140">Hello [начать] [ lnk-get-started] учебники показано, как сообщения из устройства в облако toosend из имитируемые устройства и считывать сообщения hello из встроенных hello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="e8868-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="e8868-141">Дополнительные сведения см. в разделе hello [сообщения из устройства в облако центра IoT процесса с помощью маршрутов] [ lnk-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="e8868-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="e8868-142">Если вы хотите tooroute вашего устройства в облако сообщения toocustom конечных точек см. в разделе [использовать маршруты сообщений и пользовательские конечные точки для сообщения из устройства в облако][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="e8868-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
