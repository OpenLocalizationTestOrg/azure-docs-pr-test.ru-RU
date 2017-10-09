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
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="43d21-104">Обмен сообщениями между устройством и облаком с помощью Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="43d21-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="43d21-105">Используйте центр IoT обмен сообщениями toocommunicate с устройствами по:</span><span class="sxs-lookup"><span data-stu-id="43d21-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="43d21-106">Отправка [устройства в облако] [ lnk-d2c] сообщений из решения tooyour устройств серверной части.</span><span class="sxs-lookup"><span data-stu-id="43d21-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="43d21-107">Отправка [облака на устройство] [ lnk-c2d] сообщений из решения hello обратно завершения tooyour устройств.</span><span class="sxs-lookup"><span data-stu-id="43d21-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="43d21-108">Основные свойства функциональные возможности обмена сообщениями центра IoT являются надежность hello и срок жизни сообщения.</span><span class="sxs-lookup"><span data-stu-id="43d21-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="43d21-109">Эти свойства позволяют устойчивости toointermittent подключения на стороне устройства hello и tooload резко возрастает в облако со стороны hello для обработки событий.</span><span class="sxs-lookup"><span data-stu-id="43d21-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="43d21-110">Центр IoT гарантирует *как минимум однократную* доставку при двухстороннем обмене сообщениями между устройством и облаком.</span><span class="sxs-lookup"><span data-stu-id="43d21-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="43d21-111">Возможности toohello введение концентратора IoT, см. статьях hello [Azure и Интернета вещей] [ lnk-azure-iot] и [Обзор hello Azure IoT Hub service] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="43d21-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="43d21-112">Когда toouse центр IoT обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="43d21-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="43d21-113">Используйте устройства в облако сообщения для отправки телеметрии ряда времени и оповещений из приложения, устройства и облака для устройства для односторонней уведомления tooyour устройства приложения.</span><span class="sxs-lookup"><span data-stu-id="43d21-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="43d21-114">См. слишком[руководство связи устройства в облако] [ lnk-d2c-guidance] Если вы сомневаетесь между использованием сообщения из устройства в облако, о которой свойства или передачи файла.</span><span class="sxs-lookup"><span data-stu-id="43d21-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="43d21-115">См. слишком[руководство связи облака на устройство] [ lnk-c2d-guidance] if сомнительных между использованием прямого методов, сообщения облака на устройство или требуемые свойства.</span><span class="sxs-lookup"><span data-stu-id="43d21-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43d21-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43d21-116">Next steps</span></span>

* <span data-ttu-id="43d21-117">Дополнительные сведения о [сообщениях, передаваемых с устройства в облако][lnk-d2c], Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="43d21-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="43d21-118">Дополнительные сведения о [сообщениях, передаваемых из облака на устройство][lnk-c2d], Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="43d21-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md