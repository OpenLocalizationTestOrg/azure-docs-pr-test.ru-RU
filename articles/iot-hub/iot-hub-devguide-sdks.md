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
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="e079e-103">Общие сведения о пакетах SDK для Azure IoT и их использование</span><span class="sxs-lookup"><span data-stu-id="e079e-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="e079e-104">Существуют три категории пакетов SDK для работы с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e079e-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="e079e-105">**Пакеты SDK** позволяют toobuild приложений, выполняющихся на устройствах IoT.</span><span class="sxs-lookup"><span data-stu-id="e079e-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="e079e-106">Эти приложения Отправка центра IoT tooyour телеметрии и при необходимости получать сообщения от вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="e079e-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="e079e-107">**Служба SDK** включить вашего центра IoT вы toomanage и при необходимости отправлять сообщения tooyour устройствами IoT.</span><span class="sxs-lookup"><span data-stu-id="e079e-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="e079e-108">**Azure IoT Edge** позволяет toobuild шлюзы tooenable устройств, не используйте один из протоколов hello поддерживается, или при необходимости tooprocess сообщений hello границы.</span><span class="sxs-lookup"><span data-stu-id="e079e-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="e079e-109">Пакеты SDK, предоставляемые toosupport несколько языков программирования.</span><span class="sxs-lookup"><span data-stu-id="e079e-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="e079e-110">Пакеты SDK для устройств Azure IoT</span><span class="sxs-lookup"><span data-stu-id="e079e-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="e079e-111">пакеты SDK Microsoft Azure IoT Hello содержат код, который облегчает создание устройств и приложений, подключающихся tooand управляются с помощью служб Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e079e-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="e079e-112">Hello следующими пакетами SDK устройства Azure IoT перечислены доступные toodownload из GitHub.</span><span class="sxs-lookup"><span data-stu-id="e079e-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="e079e-113">[Пакет SDK для устройств Azure IoT для C][lnk-c-device-sdk], написанный в соответствии со стандартом ANSI C (C99) для обеспечения переносимости и совместимости с широким диапазоном платформ.</span><span class="sxs-lookup"><span data-stu-id="e079e-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="e079e-114">Имеются два устройства клиентские библиотеки для C hello низкоуровневые **iothub_client** и hello **сериализатор**.</span><span class="sxs-lookup"><span data-stu-id="e079e-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="e079e-115">[Пакет SDK для устройств Azure IoT для .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="e079e-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="e079e-116">[Пакет SDK для устройств Azure IoT для Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="e079e-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="e079e-117">[Пакет SDK для устройств Azure IoT для Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="e079e-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="e079e-118">[Пакет SDK для устройств Azure IoT для Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="e079e-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="e079e-119">См. файлы readme hello в репозиториях GitHub hello сведения об использовании языка и двоичные файлы tooinstall диспетчеры пакета конкретную платформу и зависимостей на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="e079e-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="e079e-120">Платформа ОС и совместимость оборудования</span><span class="sxs-lookup"><span data-stu-id="e079e-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="e079e-121">Дополнительные сведения о совместимости пакета SDK с определенных устройств см. в разделе hello [Azure Certified для каталога устройств IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="e079e-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="e079e-122">Пакеты SDK для служб Azure IoT</span><span class="sxs-lookup"><span data-stu-id="e079e-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="e079e-123">Служба Azure IoT Hello SDK содержит toofacilitate кода, сборки приложений, которые взаимодействуют непосредственно с устройства toomanage центр IoT и безопасности.</span><span class="sxs-lookup"><span data-stu-id="e079e-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="e079e-124">Hello следующими пакетами SDK службы Azure IoT перечислены доступные toodownload из GitHub.</span><span class="sxs-lookup"><span data-stu-id="e079e-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="e079e-125">[Пакет SDK для служб Azure IoT для .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e079e-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="e079e-126">[Пакет SDK для служб Azure IoT для Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e079e-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="e079e-127">[Пакет SDK для служб Azure IoT для Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e079e-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="e079e-128">[Пакет SDK для службы Интернета вещей Azure для Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="e079e-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="e079e-129">[Пакет SDK для служб Azure IoT для .NET][lnk-c-service-sdk].</span><span class="sxs-lookup"><span data-stu-id="e079e-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="e079e-130">См. файлы readme hello в репозиториях GitHub hello сведения об использовании языка и двоичные файлы tooinstall диспетчеры пакета конкретную платформу и зависимостей на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="e079e-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="e079e-131">Edge Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="e079e-131">Azure IoT Edge</span></span>

<span data-ttu-id="e079e-132">Azure IoT Edge содержит hello инфраструктуры и модули toocreate IoT шлюза решения.</span><span class="sxs-lookup"><span data-stu-id="e079e-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="e079e-133">Вы можете расширить IoT Edge toocreate шлюзы специально настроенные tooany начала до конца сценария.</span><span class="sxs-lookup"><span data-stu-id="e079e-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="e079e-134">Вы можете скачать [Edge Интернета вещей Azure][lnk-iot-edge] с GitHub.</span><span class="sxs-lookup"><span data-stu-id="e079e-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="e079e-135">Справочная документация по API в Интернете</span><span class="sxs-lookup"><span data-stu-id="e079e-135">Online API reference documentation</span></span>

<span data-ttu-id="e079e-136">Hello следующий список содержит ссылки tooonline справочная документация по API для устройства Azure IoT, службы и библиотек шлюза.</span><span class="sxs-lookup"><span data-stu-id="e079e-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="e079e-137">[Интернет вещей (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="e079e-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="e079e-138">[REST для Центра Интернета вещей][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="e079e-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="e079e-139">[Пакет SDK для устройств Azure IoT для C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="e079e-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="e079e-140">[Пакет SDK для устройств Azure IoT для Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="e079e-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="e079e-141">[Пакет SDK для служб Azure IoT для Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="e079e-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="e079e-142">[Пакет SDK для устройств Azure IoT для Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="e079e-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="e079e-143">[Пакет SDK для служб Azure IoT для Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="e079e-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="e079e-144">[Edge Интернета вещей Azure][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="e079e-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="e079e-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e079e-145">Next steps</span></span>

<span data-ttu-id="e079e-146">Другие справочные статьи в руководстве для разработчиков Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="e079e-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="e079e-147">[IoT Hub endpoints][lnk-devguide-endpoints] (Конечные точки Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="e079e-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="e079e-148">[Справочник по языку запросов Центра Интернета вещей для двойников устройств и заданий][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="e079e-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="e079e-149">[Quotas and throttling][lnk-devguide-quotas] (Квоты и регулирование)</span><span class="sxs-lookup"><span data-stu-id="e079e-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="e079e-150">[Поддержка MQTT в Центре Интернета вещей][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="e079e-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
