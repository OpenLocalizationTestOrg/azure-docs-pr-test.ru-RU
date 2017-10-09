---
title: "обмен сообщениями центр IoT Azure aaaUnderstand | Документы Microsoft"
description: "Руководство разработчика для Центра Интернета вещей. Обмен сообщениями между устройством и облаком. Содержит сведения о форматах сообщений и поддерживаемых протоколах связи."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Обмен сообщениями между устройством и облаком с помощью Центра Интернета вещей.

Используйте центр IoT обмен сообщениями toocommunicate с устройствами по:

* Отправка [устройства в облако] [ lnk-d2c] сообщений из решения tooyour устройств серверной части.
* Отправка [облака на устройство] [ lnk-c2d] сообщений из решения hello обратно завершения tooyour устройств.

Основные свойства функциональные возможности обмена сообщениями центра IoT являются надежность hello и срок жизни сообщения. Эти свойства позволяют устойчивости toointermittent подключения на стороне устройства hello и tooload резко возрастает в облако со стороны hello для обработки событий. Центр IoT гарантирует *как минимум однократную* доставку при двухстороннем обмене сообщениями между устройством и облаком.

Возможности toohello введение концентратора IoT, см. статьях hello [Azure и Интернета вещей] [ lnk-azure-iot] и [Обзор hello Azure IoT Hub service] [lnk-iot-hub-overview].

## <a name="when-toouse-iot-hub-messaging"></a>Когда toouse центр IoT обмена сообщениями

Используйте устройства в облако сообщения для отправки телеметрии ряда времени и оповещений из приложения, устройства и облака для устройства для односторонней уведомления tooyour устройства приложения.

* См. слишком[руководство связи устройства в облако] [ lnk-d2c-guidance] Если вы сомневаетесь между использованием сообщения из устройства в облако, о которой свойства или передачи файла.
* См. слишком[руководство связи облака на устройство] [ lnk-c2d-guidance] if сомнительных между использованием прямого методов, сообщения облака на устройство или требуемые свойства.

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о [сообщениях, передаваемых с устройства в облако][lnk-d2c], Центра Интернета вещей.
* Дополнительные сведения о [сообщениях, передаваемых из облака на устройство][lnk-c2d], Центра Интернета вещей.

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md