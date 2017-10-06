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
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Использование правил маршрутизации и пользовательских конечных точек для сообщений, отправляемых с устройства в облако

Центр IoT позволяет tooroute [сообщения из устройства в облако] [ lnk-device-to-cloud] tooIoT концентратора, конечные точки службы с выходом в зависимости от свойств сообщения. Здравствуйте toosend гибкость обеспечивает правила маршрутизации сообщений, где они должны toogo без hello для сообщения tooprocess дополнительных служб или требуются toowrite дополнительный код. Каждое правило маршрутизации, настроенного имеет hello следующие свойства:

| Свойство      | Описание |
| ------------- | ----------- |
| **Имя**      | Hello уникальное имя, которое определяет правила hello. |
| **Источник**    | Происхождение Hello hello данных потока ответных toobe. Например, телеметрия устройства. |
| **Condition** | выражение запроса Hello для правила маршрутизации hello, которое выполняется заголовки и текст приветственное сообщение, а затем использовать toodetermine, является ли совпадение для конечной точки hello. Дополнительные сведения о построении условие маршрутизации см. в разделе hello [ссылка - язык запросов для задания и близнецы устройства][lnk-devguide-query-language]. |
| **Конечная точка**  | Имя конечной точки hello, где центр IoT отправляет сообщения, которые соответствуют условию hello Hello. Конечные точки должны находиться в hello же регионе, что центр IoT hello, в противном случае может взиматься для записывает в различных регионах. |

Одно сообщение может соответствовать hello условие для нескольких правил маршрутизации, в которых регистр центра IoT доставляет hello сообщение toohello конечная точка, связанная с каждым правилом сопоставленная. Центр IoT также автоматически deduplicates доставки сообщений, если сообщение соответствует несколько правил, имеющих hello того же конечного расположения, оно записывается только назначения toothat один раз.

Центр Интернета вещей имеет [встроенную конечную точку][lnk-built-in] по умолчанию. Можно создать настраиваемые конечные точки tooroute сообщения tooby связывание других служб на концентраторе toohello подписки. Сейчас Центр Интернета вещей поддерживает использование следующих служб в качестве пользовательских конечных точек: концентраторы событий, очереди служебной шины и разделы служебной шины.

> [!WARNING]
> Очереди и разделы служебной шины, для которых включены **сеансы** или **поиск повторяющихся данных**, не поддерживаются в качестве пользовательских конечных точек.

Дополнительные сведения о создании пользовательских конечных точек в Центре Интернета вещей см. в статье [Руководство. Конечные точки Центра Интернета вещей][lnk-devguide-endpoints].

Дополнительные сведения о чтении из пользовательских конечных точек см. в статьях, посвященных:

* чтению из [концентраторов событий][lnk-getstarted-eh];
* чтению из [очередей служебной шины][lnk-getstarted-queue];
* чтению из [разделов служебной шины][lnk-getstarted-topic].

### <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о конечных точках Центра Интернета вещей см. в [этом разделе][lnk-devguide-endpoints].

Дополнительные сведения о языке запросов hello можно использовать правила маршрутизации toodefine см. в разделе [центр IoT язык запросов для близнецы устройства, задания и маршрутизация сообщений][lnk-devguide-query-language].

Hello [сообщения из устройства в облако центра IoT процесса с помощью маршрутов] [ lnk-d2c-tutorial] учебнике показано, как правила маршрутизации toouse и пользовательские конечные точки.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
