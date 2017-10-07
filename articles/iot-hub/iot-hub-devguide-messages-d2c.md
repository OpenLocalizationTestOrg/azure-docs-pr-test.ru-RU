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
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>Отправлять сообщения из устройства в облако tooIoT концентратора

Данные телеметрии toosend временных рядов и предупреждений с вашего устройства tooyour решения серверной части, отправлять сообщения устройства в облако из центра IoT tooyour вашего устройства. Обсуждение других вариантов передачи данных с устройства в облако, поддерживаемых Центром Интернета вещей, см. в [руководстве по обмену данными между устройством и облаком][lnk-d2c-guidance].

Отправка сообщений с устройства в облако осуществляется через обращенную к устройству конечную точку (**/devices/{deviceId}/messages/events**). Правила маршрутизации, а затем Маршрутизация вашей tooone сообщений из конечных точек службы с выходом hello концентратор IoT. Использовать правила маршрутизации hello заголовки и текст сообщений hello устройства в облако, проходящие через ваш концентратор toodetermine где tooroute их. По умолчанию сообщения, перенаправленное toohello, встроенные конечной точки службы с выходом (**сообщений и событий**), который совместим с [концентраторов событий][lnk-event-hubs]. Таким образом, можно использовать стандартный [интеграции концентраторов событий и пакетов SDK] [ lnk-compatible-endpoint] tooreceive сообщения из устройства в облако в своем решении серверной части.

Для реализация отправки сообщений с устройства в облако Центр Интернета вещей использует модель потоковой передачи сообщений. Скорее сообщения из устройства в облако центра IoT являются [концентраторов событий] [ lnk-event-hubs] *событий* чем [Service Bus] [ lnk-servicebus] *сообщения* в том, что имеется большое количество событий, передаваемых через службу hello, могут быть прочитаны несколько модулей чтения.

Устройства в облако обмена сообщениями с центром IoT имеет следующие характеристики hello.

* Сообщения из устройства в облако, являются устойчивыми и сохраненные в по умолчанию центр IoT **сообщений и событий** конечную точку для копирования tooseven дней.
* Сообщения из устройства в облако может быть не более 256 КБ и могут быть сгруппированы в пакетах, которые отправляет toooptimize. Размер пакетов не может превышать 256 КБ.
* Как описано в hello [tooIoT управления доступом концентратора] [ lnk-devguide-security] раздела центра IoT включает элемент управления доступом и проверка подлинности на устройство.
* Центр IoT позволяет toocreate копирование too10 пользовательские конечные точки. Сообщения доставляются toohello конечные точки, основанные на маршрутов, заданных в концентратор IoT. Дополнительные сведения см. в статье, посвященной [правилам маршрутизации](#routing-rules).
* Центр Интернета вещей обеспечивает работу большого числа одновременно подключенных устройств (см. раздел [Квоты и регулирование][lnk-quotas]).
* Центр Интернета вещей не позволяет выполнять произвольное секционирование. Сообщения, отправляемые с устройства в облако, секционируются по исходному идентификатору **deviceId**.

Дополнительные сведения об отличиях hello hello центр IoT и службы концентраторов событий см. в разделе [сравнения из центра IoT Azure и концентраторов событий Azure][lnk-comparison].

## <a name="send-non-telemetry-traffic"></a>Отправка данных, не относящихся к телеметрии

Часто кроме точек данных tootelemetry, устройства отправляют сообщения и запросов, которые требуют выполнения отдельных и обработка событий в серверной части решения hello. Например критические оповещения, которые необходимо активировать определенное действие в hello серверной части. Можно легко написать [правила маршрутизации] [ lnk-devguide-custom] toosend эти типы сообщений tooan endpoint выделенного tootheir обработку в зависимости от заголовка сообщения hello или значения в тело сообщения hello.

Дополнительные сведения о hello лучшим способом tooprocess этом kind сообщения hello в разделе [учебника: как tooprocess сообщения из устройства в облако центра IoT] [ lnk-d2c-tutorial] учебника.

## <a name="route-device-to-cloud-messages"></a>Маршрутизация сообщений, отправленных с устройства в облако

У вас есть два варианта для маршрутизации сообщения из устройства в облако tooyour серверной части приложения:

* Используйте встроенные hello [концентратора событий-совместимой конечной точки] [ lnk-compatible-endpoint] сообщений tooenable серверной части приложения tooread hello устройства в облако, полученных hello концентратора. toolearn о hello встроенных концентратора событий-совместимой конечной точки в разделе [чтения сообщения из устройства в облако из встроенных hello конечной точки][lnk-devguide-builtin].
* Использование маршрутизации правила toosend сообщения toocustom конечных точек в концентратор IoT. Пользовательские конечные точки позволяют сообщений серверной части приложения tooread устройства в облако с помощью концентраторов событий, Service Bus очереди или разделы служебной шины. toolearn о маршрутизации и пользовательских конечных точек, в разделе [использовать пользовательские конечные точки и правила маршрутизации для сообщения из устройства в облако][lnk-devguide-custom].

## <a name="anti-spoofing-properties"></a>Свойства для защиты от спуфинга

устройство tooavoid подделкой сообщения из устройства в облако, центр IoT штампы, все сообщения с hello следующие свойства:

* **ConnectionDeviceId;**
* **ConnectionDeviceGenerationId;**
* **ConnectionAuthMethod.**

Hello первых двух содержат hello **deviceId** и **generationId** из hello, рассчитанные на устройстве, согласно [свойства удостоверения устройства][lnk-device-properties].

Hello **ConnectionAuthMethod** свойство содержит сериализованный объект JSON, с hello следующие свойства:

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>Дальнейшие действия

Сведения о пакетах SDK hello можно использовать сообщения из устройства в облако toosend см [пакеты SDK Azure IoT][lnk-sdks].

Hello [начать] [ lnk-get-started] руководствах показано, как сообщения toosend устройства в облако с имитацию и физических устройств. Дополнительные сведения см. в разделе hello [сообщения из устройства в облако центра IoT процесса с помощью маршрутов] [ lnk-d2c-tutorial] учебника.

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
