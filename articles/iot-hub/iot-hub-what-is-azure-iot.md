---
title: "aaaAzure решений для Интернета вещей (IoT Suite) | Документы Microsoft"
description: "Обзор архитектуры решения IoT образца и его связь toodevices, hello Azure IoT Hub service, пакеты SDK Azure IoT, пакеты SDK службы Azure IoT и другими службами Azure."
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
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="f3066-103">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3066-103">Next steps</span></span>

<span data-ttu-id="f3066-104">Центр Интернета вещей Azure — это служба Azure, обеспечивающая надежный и защищенный двунаправленный обмен данными между серверной частью вашего решения и миллионами устройств.</span><span class="sxs-lookup"><span data-stu-id="f3066-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="f3066-105">Она позволяет hello решения серверной части для:</span><span class="sxs-lookup"><span data-stu-id="f3066-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="f3066-106">получать данные телеметрии с ваших устройств;</span><span class="sxs-lookup"><span data-stu-id="f3066-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="f3066-107">Извлекая данные из потока событий устройств tooa процессора.</span><span class="sxs-lookup"><span data-stu-id="f3066-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="f3066-108">получать отправляемые с устройств файлы;</span><span class="sxs-lookup"><span data-stu-id="f3066-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="f3066-109">Отправка сообщений облака на устройство toospecific устройств.</span><span class="sxs-lookup"><span data-stu-id="f3066-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="f3066-110">Можно использовать собственное решение обратно завершить tooimplement центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f3066-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="f3066-111">Кроме того центр IoT включает удостоверение реестра используется tooprovision устройства, их учетные данные безопасности и их центра IoT toohello tooconnect права.</span><span class="sxs-lookup"><span data-stu-id="f3066-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="f3066-112">toolearn Дополнительные сведения о центра IoT. в разделе [возможности центр IoT?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="f3066-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="f3066-113">toolearn центр IoT Azure обеспечивает управление устройствами, основанную на стандартах tooremotely можно управлять, настраивать и обновлять устройства, в статье [Обзор управления устройствами с центром IoT][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="f3066-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="f3066-114">tooimplement клиентским приложениям на разнообразных платформах оборудования и операционных систем, можно использовать устройства Azure IoT hello пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="f3066-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="f3066-115">устройство Hello SDK включает библиотеки, которые упрощают отправку телеметрии tooan IoT hub и получения облака на устройство сообщений.</span><span class="sxs-lookup"><span data-stu-id="f3066-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="f3066-116">При использовании устройства hello пакеты SDK, можно выбрать несколько сетевых протоколов toocommunicate с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="f3066-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="f3066-117">toolearn. более того, в разделе hello [сведения об устройстве SDK][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="f3066-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="f3066-118">запущен написания кода и выполнение некоторых образцов tooget разделе hello [приступить к работе с центром IoT] [ lnk-getstarted] учебника.</span><span class="sxs-lookup"><span data-stu-id="f3066-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="f3066-119">Кроме того, рекомендуем ознакомиться с набором [Azure IoT Suite][lnk-iot-suite], который представляет собой коллекцию предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="f3066-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="f3066-120">IoT Suite позволяет tooget к работе и масштабировать IoT проекты tooaddress распространенные IoT сценарии — например удаленный мониторинг, управление ресурсами и превентивного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="f3066-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
