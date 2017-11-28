---
title: "Решения Azure для Интернета вещей (IoT Suite) | Документация Майкрософт"
description: "Общие сведения об архитектуре примера решения Интернета вещей и о том, как оно связано с устройствами, службой Центра Интернета вещей Azure, пакетами SDK для устройств Azure IoT, пакетами SDK для служб Интернета вещей Azure и другими службами Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1d54f090a0e07cd5102cb48cd70a1377845d6654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="91c2a-103">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91c2a-103">Next steps</span></span>

<span data-ttu-id="91c2a-104">Центр Интернета вещей Azure — это служба Azure, обеспечивающая надежный и защищенный двунаправленный обмен данными между серверной частью вашего решения и миллионами устройств.</span><span class="sxs-lookup"><span data-stu-id="91c2a-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="91c2a-105">В результате серверная часть решения может:</span><span class="sxs-lookup"><span data-stu-id="91c2a-105">It enables the solution back end to:</span></span>

* <span data-ttu-id="91c2a-106">получать данные телеметрии с ваших устройств;</span><span class="sxs-lookup"><span data-stu-id="91c2a-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="91c2a-107">перенаправлять эти данные в обработчик потоковых событий;</span><span class="sxs-lookup"><span data-stu-id="91c2a-107">Route data from your devices to a stream event processor.</span></span>
* <span data-ttu-id="91c2a-108">получать отправляемые с устройств файлы;</span><span class="sxs-lookup"><span data-stu-id="91c2a-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="91c2a-109">отправлять сообщения из облака на определенные устройства.</span><span class="sxs-lookup"><span data-stu-id="91c2a-109">Send cloud-to-device messages to specific devices.</span></span>

<span data-ttu-id="91c2a-110">Вы можете использовать центр IoT для реализации собственной серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="91c2a-110">You can use IoT Hub to implement your own solution back end.</span></span> <span data-ttu-id="91c2a-111">Кроме того, Центр Интернета вещей включает реестр удостоверений, который используется для подготовки устройств, настройки их учетных данных и прав доступа к этому центру.</span><span class="sxs-lookup"><span data-stu-id="91c2a-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span></span> <span data-ttu-id="91c2a-112">Дополнительные сведения о Центре Интернета вещей см. в статье [Что такое Центр Интернета вещей в Azure][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="91c2a-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="91c2a-113">Сведения о том, как в Центре Интернета вещей Azure реализовано стандартизированное управление устройствами для их удаленного администрирования, настройки и обновления, см. в статье [Общие сведения об управлении устройствами с помощью Центра Интернета вещей][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="91c2a-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="91c2a-114">Вы можете внедрить клиентские приложения на различных аппаратных платформах и в операционных системах с помощью пакетов SDK для устройств Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="91c2a-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span></span> <span data-ttu-id="91c2a-115">Пакеты SDK для устройств включают библиотеки, упрощающие отправку данных телеметрии в Центр Интернета вещей и получение сообщений, отправляемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="91c2a-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="91c2a-116">Используя эти пакеты, для взаимодействия с Центром Интернета вещей вы можете выбрать один из нескольких сетевых протоколов.</span><span class="sxs-lookup"><span data-stu-id="91c2a-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span></span> <span data-ttu-id="91c2a-117">Дополнительные сведения о пакетах SDK для устройств см. [здесь][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="91c2a-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="91c2a-118">Начальное руководство по написанию кода и выполнению некоторых примеров см. в [этой статье][lnk-getstarted].</span><span class="sxs-lookup"><span data-stu-id="91c2a-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="91c2a-119">Кроме того, рекомендуем ознакомиться с набором [Azure IoT Suite][lnk-iot-suite], который представляет собой коллекцию предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="91c2a-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="91c2a-120">позволяющих быстро начать работу и масштабировать проекты IoT для решения распространенных сценариев IoT, например удаленного мониторинга, управления ресурсами-контейнерами и прогнозного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="91c2a-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
