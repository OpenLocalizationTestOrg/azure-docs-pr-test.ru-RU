---
title: "Общие сведения о встроенной конечной точке Центра Интернета вещей Azure | Документация Майкрософт"
description: "В этом руководстве разработчика описано, как читать сообщения, отправляемые с устройства в облако, с помощью встроенной конечной точки, совместимой с концентратором событий."
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="a5f3a-103">Чтение сообщений, пересылаемых с устройства в облако, из встроенной конечной точки</span><span class="sxs-lookup"><span data-stu-id="a5f3a-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="a5f3a-104">По умолчанию сообщения направляются во встроенную конечную точку, доступную для службы (**/messages/events**), которая совместима с [концентраторами событий][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="a5f3a-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="a5f3a-105">Сейчас эта конечная точка предоставляется только по протоколу [AMQP][lnk-amqp] на порте 5671.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="a5f3a-106">Центр Интернета вещей позволяет управлять встроенной конечной точкой обмена сообщениями **messages/events**, совместимой с концентраторами событий, с помощью приведенных ниже свойств.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="a5f3a-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="a5f3a-107">Property</span></span>            | <span data-ttu-id="a5f3a-108">Описание</span><span class="sxs-lookup"><span data-stu-id="a5f3a-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="a5f3a-109">**Количество секций**</span><span class="sxs-lookup"><span data-stu-id="a5f3a-109">**Partition count**</span></span> | <span data-ttu-id="a5f3a-110">Это свойство можно задать во время создания, чтобы определить количество [разделов][lnk-event-hub-partitions] для приема событий сообщений, отправляемых с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="a5f3a-111">**Время хранения**</span><span class="sxs-lookup"><span data-stu-id="a5f3a-111">**Retention time**</span></span>  | <span data-ttu-id="a5f3a-112">Это свойство задает время в днях, в течение которого сообщения хранятся в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="a5f3a-113">Значение по умолчанию — один день, но это значение можно увеличить до семи дней.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="a5f3a-114">Центр Интернета вещей также предоставляет возможность управлять группами потребителей во встроенной конечной точке, которая получает сообщения, отправляемые с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="a5f3a-115">По умолчанию все сообщения, которые явно не соответствуют правилу маршрутизации сообщений, записываются во встроенную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="a5f3a-116">Если отключить этот резервный маршрут, то сообщения, которые явно не соответствуют ни одному правилу маршрутизации сообщений, будут удаляться.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="a5f3a-117">Вы можете изменить период хранения на [портале Azure][lnk-management-portal] или программно (с помощью [интерфейсов REST API поставщика ресурсов Центра Интернета вещей][lnk-resource-provider-apis]).</span><span class="sxs-lookup"><span data-stu-id="a5f3a-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="a5f3a-118">Центр Интернета вещей предоставляет встроенную конечную точку **messages/events**, с помощью которой внутренние службы считывают сообщения, отправляемые в Центр с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="a5f3a-119">Эта конечная точка совместима с концентраторами событий, поэтому можно использовать любой из механизмов для чтения сообщений, который поддерживает служба концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="a5f3a-120">Считывание данных из встроенной конечной точки</span><span class="sxs-lookup"><span data-stu-id="a5f3a-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="a5f3a-121">При использовании [пакета SDK служебной шины Azure для .NET][lnk-servicebus-sdk] или [концентраторов событий и узла обработчика событий][lnk-eventprocessorhost] вы можете использовать любые строки подключения к Центру Интернета вещей с нужными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="a5f3a-122">А затем использовать **messages/events** в качестве имени концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="a5f3a-123">При использовании пакетов SDK (или интеграции продуктов), которые не поддерживают Центр Интернета вещей, следует получить совместимые с концентраторами событий конечную точку и имя в разделе параметров Центра Интернета вещей на [портале Azure][lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="a5f3a-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="a5f3a-124">В колонке Центра Интернета вещей щелкните **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="a5f3a-125">В разделе **Built-in endpoints** (Встроенные конечные точки) щелкните **События**.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="a5f3a-126">Колонка содержит следующие значения: **Event Hub-compatible endpoint** (Конечная точка, совместимая с концентраторами событий), **Event Hub-compatible name** (Имя, совместимое с концентраторами событий), **Разделы**, **Время хранения** и **Группы потребителей**.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Параметры отправки сообщений с устройства в облако][img-eventhubcompatible]

<span data-ttu-id="a5f3a-128">Для пакета SDK для Центра Интернета вещей требуется указать конечную точку Центра Интернета вещей, и эта точка — **messages/events**, как показано в колонке **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="a5f3a-129">Если для используемого пакета SDK требуется указать **имя узла** или **пространство имен**, то удалите схему из **конечной точки, совместимой с концентраторами событий**.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="a5f3a-130">Например, если конечная точка, совместимая с концентратором событий, — **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, то **именем узла** будет **iothub-ns-myiothub-1234.servicebus.windows.net**, а **пространством имен** — **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="a5f3a-131">Затем можно использовать любую политику общего доступа с разрешениями **ServiceConnect**, которые позволяют подключаться к указанному концентратору событий.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="a5f3a-132">Если нужно создать строку подключения к концентратору событий с помощью указанных выше сведений, можно использовать следующий образец:</span><span class="sxs-lookup"><span data-stu-id="a5f3a-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="a5f3a-133">Ниже приведен список пакетов SDK и интеграций, которые можно применять к совместимым с концентраторами событий конечным точкам, которые предоставляет Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="a5f3a-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="a5f3a-134">[клиент концентраторов событий Java;](https://github.com/hdinsight/eventhubs-client)</span><span class="sxs-lookup"><span data-stu-id="a5f3a-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="a5f3a-135">[Воронка Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a5f3a-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="a5f3a-136">Вы можете просмотреть [источник воронки](https://github.com/apache/storm/tree/master/external/storm-eventhubs) на портале GitHub.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="a5f3a-137">[интеграция Apache Spark.](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md)</span><span class="sxs-lookup"><span data-stu-id="a5f3a-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5f3a-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5f3a-138">Next steps</span></span>

<span data-ttu-id="a5f3a-139">Дополнительные сведения о конечных точках Центра Интернета вещей см. в [этом разделе][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="a5f3a-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="a5f3a-140">В руководствах по [началу работы][lnk-get-started] рассказывается, как отправлять сообщения из устройства в облако с имитируемых устройств и читать их из встроенной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="a5f3a-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="a5f3a-141">Дополнительные сведения см. в руководстве [по обработке сообщений Центра Интернета вещей, отправляемых с устройства в облако с помощью маршрутов][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="a5f3a-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="a5f3a-142">Сведения о перенаправлении сообщений, отправляемых с устройства в облако на пользовательские конечные точки, см. в статье [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom] (Использование маршрутов сообщений и пользовательских конечных точек для сообщений, отправляемых с устройства в облако).</span><span class="sxs-lookup"><span data-stu-id="a5f3a-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
