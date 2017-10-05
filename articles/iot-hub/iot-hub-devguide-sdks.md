---
title: "Общие сведения о пакетах SDK для Azure IoT | Документация Майкрософт"
description: "Руководство разработчика. Сведения и ссылки на различные пакеты SDK для устройств и служб Azure IoT, которые можно использовать для создания приложений для устройств и внутренних приложений."
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
ms.openlocfilehash: bcbf4b9633f58293edb19aeb33dec6602ac4ec8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="14b7c-103">Общие сведения о пакетах SDK для Azure IoT и их использование</span><span class="sxs-lookup"><span data-stu-id="14b7c-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="14b7c-104">Существуют три категории пакетов SDK для работы с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="14b7c-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="14b7c-105">**Пакеты SDK для устройств** позволяют создавать приложения, работающие на ваших устройствах Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="14b7c-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="14b7c-106">Эти приложения отправляют данные телеметрии в центр Интернета вещей и при необходимости получают из него сообщения.</span><span class="sxs-lookup"><span data-stu-id="14b7c-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="14b7c-107">**Пакеты SDK для служб** позволяют управлять Центром Интернета вещей и при необходимости отправлять сообщения на устройства Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="14b7c-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="14b7c-108">**Edge Интернета вещей Azure** позволяет создавать шлюзы, чтобы подключать устройства, не использующие ни один из поддерживаемых протоколов, или чтобы обрабатывать сообщения на границе, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="14b7c-108">**Azure IoT Edge** enables you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="14b7c-109">Пакеты SDK предоставляются для поддержки нескольких языков программирования.</span><span class="sxs-lookup"><span data-stu-id="14b7c-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="14b7c-110">Пакеты SDK для устройств Azure IoT</span><span class="sxs-lookup"><span data-stu-id="14b7c-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="14b7c-111">Пакеты SDK для устройств центра Microsoft Azure IoT содержат код, упрощающий построение устройств и приложений, которые подключаются к службам центра IoT и управляются с помощью этих служб.</span><span class="sxs-lookup"><span data-stu-id="14b7c-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="14b7c-112">В GitHub для скачивания доступны следующие пакеты SDK для устройств Azure IoT:</span><span class="sxs-lookup"><span data-stu-id="14b7c-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="14b7c-113">[Пакет SDK для устройств Azure IoT для C][lnk-c-device-sdk], написанный в соответствии со стандартом ANSI C (C99) для обеспечения переносимости и совместимости с широким диапазоном платформ.</span><span class="sxs-lookup"><span data-stu-id="14b7c-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="14b7c-114">Существуют две клиентские библиотеки устройств для C: низкоуровневая  **iothub_client**  и  **сериализатор**.</span><span class="sxs-lookup"><span data-stu-id="14b7c-114">There are two device client libraries for C, the low-level **iothub_client** and the **serializer**.</span></span>
* <span data-ttu-id="14b7c-115">[Пакет SDK для устройств Azure IoT для .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="14b7c-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="14b7c-116">[Пакет SDK для устройств Azure IoT для Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="14b7c-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="14b7c-117">[Пакет SDK для устройств Azure IoT для Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="14b7c-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="14b7c-118">[Пакет SDK для устройств Azure IoT для Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="14b7c-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="14b7c-119">Сведения об установке двоичных файлов и зависимостей на компьютере для разработки с помощью диспетчера пакетов, зависящего от языка или платформы, см. в файле сведений в репозиториях GitHub.</span><span class="sxs-lookup"><span data-stu-id="14b7c-119">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="14b7c-120">Платформа ОС и совместимость оборудования</span><span class="sxs-lookup"><span data-stu-id="14b7c-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="14b7c-121">Дополнительные сведения о совместимости пакета SDK с определенными устройствами см. в [каталоге устройств, сертифицированных по программе Microsoft Azure Certified for IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="14b7c-121">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="14b7c-122">Пакеты SDK для служб Azure IoT</span><span class="sxs-lookup"><span data-stu-id="14b7c-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="14b7c-123">Пакеты SDK для службы Интернета вещей Azure содержат код, который облегчает создание приложений, взаимодействующих непосредственно с Центром Интернета вещей, для управления устройствами и безопасностью.</span><span class="sxs-lookup"><span data-stu-id="14b7c-123">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="14b7c-124">В GitHub для скачивания доступны следующие пакеты SDK для служб Azure IoT:</span><span class="sxs-lookup"><span data-stu-id="14b7c-124">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="14b7c-125">[Пакет SDK для служб Azure IoT для .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="14b7c-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="14b7c-126">[Пакет SDK для служб Azure IoT для Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="14b7c-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="14b7c-127">[Пакет SDK для служб Azure IoT для Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="14b7c-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="14b7c-128">[Пакет SDK для службы Интернета вещей Azure для Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="14b7c-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="14b7c-129">[Пакет SDK для служб Azure IoT для .NET][lnk-c-service-sdk].</span><span class="sxs-lookup"><span data-stu-id="14b7c-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="14b7c-130">Сведения об установке двоичных файлов и зависимостей на компьютере для разработки с помощью диспетчера пакетов, зависящего от языка или платформы, см. в файле сведений в репозиториях GitHub.</span><span class="sxs-lookup"><span data-stu-id="14b7c-130">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="14b7c-131">Edge Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="14b7c-131">Azure IoT Edge</span></span>

<span data-ttu-id="14b7c-132">Edge Интернета вещей Azure содержит инфраструктуру и модули, предназначенные для создания решений шлюза Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="14b7c-132">Azure IoT Edge contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="14b7c-133">Чтобы создавать шлюзы, адаптированные к любому комплексному сценарию, вы можете расширить Edge Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="14b7c-133">You can extend IoT Edge to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="14b7c-134">Вы можете скачать [Edge Интернета вещей Azure][lnk-iot-edge] с GitHub.</span><span class="sxs-lookup"><span data-stu-id="14b7c-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="14b7c-135">Справочная документация по API в Интернете</span><span class="sxs-lookup"><span data-stu-id="14b7c-135">Online API reference documentation</span></span>

<span data-ttu-id="14b7c-136">Ниже приведен список ссылок на электронную справочную документацию по API для библиотек шлюзов, служб и устройств Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="14b7c-136">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="14b7c-137">[Интернет вещей (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="14b7c-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="14b7c-138">[REST для Центра Интернета вещей][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="14b7c-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="14b7c-139">[Пакет SDK для устройств Azure IoT для C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="14b7c-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="14b7c-140">[Пакет SDK для устройств Azure IoT для Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="14b7c-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="14b7c-141">[Пакет SDK для служб Azure IoT для Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="14b7c-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="14b7c-142">[Пакет SDK для устройств Azure IoT для Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="14b7c-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="14b7c-143">[Пакет SDK для служб Azure IoT для Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="14b7c-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="14b7c-144">[Edge Интернета вещей Azure][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="14b7c-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="14b7c-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="14b7c-145">Next steps</span></span>

<span data-ttu-id="14b7c-146">Другие справочные статьи в руководстве для разработчиков Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="14b7c-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="14b7c-147">[IoT Hub endpoints][lnk-devguide-endpoints] (Конечные точки Центра Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="14b7c-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="14b7c-148">[Справочник по языку запросов Центра Интернета вещей для двойников устройств и заданий][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="14b7c-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="14b7c-149">[Quotas and throttling][lnk-devguide-quotas] (Квоты и регулирование)</span><span class="sxs-lookup"><span data-stu-id="14b7c-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="14b7c-150">[Поддержка MQTT в Центре Интернета вещей][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="14b7c-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
