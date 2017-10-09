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
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Чтение сообщения из устройства в облако из встроенных hello конечной точки

По умолчанию сообщения, перенаправленное toohello, встроенные конечной точки службы с выходом (**сообщений и событий**), который совместим с [концентраторов событий][lnk-event-hubs]. Эта конечная точка является в настоящее время доступными только с помощью hello [AMQP] [ lnk-amqp] протокола на порту 5671. Центр IoT предоставляет hello следующие свойства tooenable вы toocontrol hello встроенных концентратора событий-совместимой конечной точки обмена сообщениями **сообщений и событий**.

| Свойство            | Описание |
| ------------------- | ----------- |
| **Количество секций** | Установите это свойство на создание toodefine hello число [секций] [ lnk-event-hub-partitions] приеме событий устройства в облако. |
| **Время хранения**  | Это свойство задает время в днях, в течение которого сообщения хранятся в Центре Интернета вещей. по умолчанию Hello один день, но его можно повысить tooseven дней. |

Центр IoT можно также toomanage групп потребителей на hello встроенные устройства в облако конечная точка получения.

По умолчанию все сообщения, которые явно не соответствуют правило маршрутизации сообщения записываются toohello Встроенные конечной точки. Если отключить этот резервный маршрут, то сообщения, которые явно не соответствуют ни одному правилу маршрутизации сообщений, будут удаляться.

Можно изменить срок хранения hello, либо программным способом с помощью hello [API REST поставщика ресурсов центра IoT][lnk-resource-provider-apis], или с помощью hello [портал Azure] [ lnk-management-portal].

Центр IoT предоставляет hello **сообщений и событий** встроенные конечную точку для настройки сервера служб tooread hello устройства в облако сообщений, полученных концентратор. Эта конечная точка является событие концентратора совместимые, позволяющий toouse поддерживает любой службы концентраторов событий hello hello механизмы чтения сообщений.

## <a name="read-from-hello-built-in-endpoint"></a>Чтение из встроенных hello конечной точки

При использовании hello [Azure Service Bus SDK для .NET] [ lnk-servicebus-sdk] или hello [концентраторов событий - узел обработчика событий][lnk-eventprocessorhost], можно использовать любые соединения, центр IoT строки с hello правильные разрешения. Затем с помощью **сообщений и событий** имени концентратора событий hello.

При использовании SDK (или интеграции продуктов), не знают о центра IoT, необходимо извлечь концентратор событий-совместимой конечной точки и имя совместимое концентратора событий с параметры центра IoT hello в hello [портал Azure] [ lnk-management-portal]:

1. В колонке концентратора IoT hello щелкните **конечные точки**.
1. В hello **встроенных конечных точек** щелкните **события**. Hello колонке содержит hello следующие значения: **концентратора событий-совместимой конечной точки**, **концентратора событий-совместимое имя**, **секций**, **время хранения**, и **групп потребителей**.

    ![Параметры отправки сообщений с устройства в облако][img-eventhubcompatible]

Hello IoT Hub SDK требуется имя конечной точки центра IoT, являющееся hello **сообщений и событий** как показано в hello **конечные точки** колонку.

Если используется пакет SDK для hello требует **имя узла** или **пространства имен** значения, удалите hello схему из hello **концентратора событий-совместимой конечной точки**. Например, если ваш конечная точка совместимое концентратора событий **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** бы  **центром IOT ns-myiothub 1234.servicebus.windows.net**и hello **имен** бы **центром IOT ns-myiothub-1234**.

Затем можно использовать любую политику общего доступа с hello **ServiceConnect** toohello tooconnect разрешения указанного концентратора событий.

Если требуется toobuild строку подключения концентратора событий, используя сведения о предыдущих hello используйте hello следующий шаблон:

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

пакеты SDK Hello и интеграций, которые можно использовать с конечными точками совместимое концентратора событий, предоставляемых центра IoT включает элементы hello hello после списка:

* [клиент концентраторов событий Java;](https://github.com/hdinsight/eventhubs-client)
* [Воронка Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). Можно просмотреть hello [spout источника](https://github.com/apache/storm/tree/master/external/storm-eventhubs) на GitHub.
* [интеграция Apache Spark.](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md)

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о конечных точках Центра Интернета вещей см. в [этом разделе][lnk-endpoints].

Hello [начать] [ lnk-get-started] учебники показано, как сообщения из устройства в облако toosend из имитируемые устройства и считывать сообщения hello из встроенных hello конечной точки. Дополнительные сведения см. в разделе hello [сообщения из устройства в облако центра IoT процесса с помощью маршрутов] [ lnk-d2c-tutorial] учебника.

Если вы хотите tooroute вашего устройства в облако сообщения toocustom конечных точек см. в разделе [использовать маршруты сообщений и пользовательские конечные точки для сообщения из устройства в облако][lnk-custom].

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
