---
title: "hello aaaUnderstand пакеты SDK Azure IoT | Документы Microsoft"
description: "Руководство разработчика по сведения о и ссылки toohello различных Azure IoT устройств и служб пакетов SDK, можно использовать приложения для устройств toobuild и серверной части."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a>Общие сведения о пакетах SDK для Azure IoT и их использование

Существуют три категории пакетов SDK для работы с Центром Интернета вещей.

* **Пакеты SDK** позволяют toobuild приложений, выполняющихся на устройствах IoT. Эти приложения Отправка центра IoT tooyour телеметрии и при необходимости получать сообщения от вашего центра IoT.

* **Служба SDK** включить вашего центра IoT вы toomanage и при необходимости отправлять сообщения tooyour устройствами IoT.

* **Azure IoT Edge** позволяет toobuild шлюзы tooenable устройств, не используйте один из протоколов hello поддерживается, или при необходимости tooprocess сообщений hello границы.

Пакеты SDK, предоставляемые toosupport несколько языков программирования.

## <a name="azure-iot-device-sdks"></a>Пакеты SDK для устройств Azure IoT

пакеты SDK Microsoft Azure IoT Hello содержат код, который облегчает создание устройств и приложений, подключающихся tooand управляются с помощью служб Azure IoT Hub.

Hello следующими пакетами SDK устройства Azure IoT перечислены доступные toodownload из GitHub.

* [Пакет SDK для устройств Azure IoT для C][lnk-c-device-sdk], написанный в соответствии со стандартом ANSI C (C99) для обеспечения переносимости и совместимости с широким диапазоном платформ. Имеются два устройства клиентские библиотеки для C hello низкоуровневые **iothub_client** и hello **сериализатор**.
* [Пакет SDK для устройств Azure IoT для .NET][lnk-dotnet-device-sdk]
* [Пакет SDK для устройств Azure IoT для Java][lnk-java-device-sdk]
* [Пакет SDK для устройств Azure IoT для Node.js][lnk-node-device-sdk]
* [Пакет SDK для устройств Azure IoT для Python][lnk-python-device-sdk]

> [!NOTE]
> См. файлы readme hello в репозиториях GitHub hello сведения об использовании языка и двоичные файлы tooinstall диспетчеры пакета конкретную платформу и зависимостей на компьютере разработки.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>Платформа ОС и совместимость оборудования

Дополнительные сведения о совместимости пакета SDK с определенных устройств см. в разделе hello [Azure Certified для каталога устройств IoT][lnk-certified].

## <a name="azure-iot-service-sdks"></a>Пакеты SDK для служб Azure IoT

Служба Azure IoT Hello SDK содержит toofacilitate кода, сборки приложений, которые взаимодействуют непосредственно с устройства toomanage центр IoT и безопасности.

Hello следующими пакетами SDK службы Azure IoT перечислены доступные toodownload из GitHub.

* [Пакет SDK для служб Azure IoT для .NET][lnk-dotnet-service-sdk]
* [Пакет SDK для служб Azure IoT для Node.js][lnk-node-service-sdk]
* [Пакет SDK для служб Azure IoT для Java][lnk-java-service-sdk]
* [Пакет SDK для службы Интернета вещей Azure для Python][lnk-python-service-sdk]
* [Пакет SDK для служб Azure IoT для .NET][lnk-c-service-sdk].

> [!NOTE]
> См. файлы readme hello в репозиториях GitHub hello сведения об использовании языка и двоичные файлы tooinstall диспетчеры пакета конкретную платформу и зависимостей на компьютере разработки.

## <a name="azure-iot-edge"></a>Edge Интернета вещей Azure

Azure IoT Edge содержит hello инфраструктуры и модули toocreate IoT шлюза решения. Вы можете расширить IoT Edge toocreate шлюзы специально настроенные tooany начала до конца сценария.

Вы можете скачать [Edge Интернета вещей Azure][lnk-iot-edge] с GitHub.

## <a name="online-api-reference-documentation"></a>Справочная документация по API в Интернете

Hello следующий список содержит ссылки tooonline справочная документация по API для устройства Azure IoT, службы и библиотек шлюза.

* [Интернет вещей (IoT) .NET][lnk-dotnet-ref]
* [REST для Центра Интернета вещей][lnk-rest-ref]
* [Пакет SDK для устройств Azure IoT для C][lnk-c-ref]
* [Пакет SDK для устройств Azure IoT для Java][lnk-java-ref]
* [Пакет SDK для служб Azure IoT для Java][lnk-java-service-ref]
* [Пакет SDK для устройств Azure IoT для Node.js][lnk-node-ref]
* [Пакет SDK для служб Azure IoT для Node.js][lnk-node-service-ref]
* [Edge Интернета вещей Azure][lnk-gateway-ref]

## <a name="next-steps"></a>Дальнейшие действия

Другие справочные статьи в руководстве для разработчиков Центра Интернета вещей:

* [IoT Hub endpoints][lnk-devguide-endpoints] (Конечные точки Центра Интернета вещей)
* [Справочник по языку запросов Центра Интернета вещей для двойников устройств и заданий][lnk-devguide-query]
* [Quotas and throttling][lnk-devguide-quotas] (Квоты и регулирование)
* [Поддержка MQTT в Центре Интернета вещей][lnk-devguide-mqtt]

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
