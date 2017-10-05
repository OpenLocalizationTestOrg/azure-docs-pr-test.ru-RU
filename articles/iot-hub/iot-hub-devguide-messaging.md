---
title: "Общие сведения об обмене сообщениями в Центре Интернета вещей Azure | Документация Майкрософт"
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
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="c9434-104">Обмен сообщениями между устройством и облаком с помощью Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c9434-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="c9434-105">Сообщения Центра Интернета вещей служат для связи с устройством путем:</span><span class="sxs-lookup"><span data-stu-id="c9434-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="c9434-106">отправки сообщений [с устройства в облако][lnk-d2c] с ваших устройств в серверную часть решения;</span><span class="sxs-lookup"><span data-stu-id="c9434-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="c9434-107">отправки сообщений [из облака на устройство][lnk-c2d] из серверной части решения на ваши устройства.</span><span class="sxs-lookup"><span data-stu-id="c9434-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="c9434-108">Основные свойства функции обмена сообщениями в центре IoT — надежность и устойчивость сообщений.</span><span class="sxs-lookup"><span data-stu-id="c9434-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="c9434-109">Эти свойства сохраняются, если на стороне устройства прерывается подключение и если наступает момент пиковой загрузки на стороне облака при обработке событий.</span><span class="sxs-lookup"><span data-stu-id="c9434-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="c9434-110">Центр IoT гарантирует *как минимум однократную* доставку при двухстороннем обмене сообщениями между устройством и облаком.</span><span class="sxs-lookup"><span data-stu-id="c9434-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="c9434-111">Общие сведения о возможностях Центра Интернета вещей см. в статьях [Azure и Интернет вещей][lnk-azure-iot] и [Общие сведения о службе Центра Интернета вещей Azure][lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="c9434-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="c9434-112">Для чего используются сообщения Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="c9434-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="c9434-113">Для отправки телеметрии и оповещений с учетом временных рядов из приложения для устройства используйте сообщения, отправляемые с устройства в облако, а для отправки односторонних уведомлений в приложение для устройства — сообщения, отправляемые из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="c9434-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="c9434-114">Дополнительные сведения см. в [руководстве по обмену данными между устройством и облаком][lnk-d2c-guidance], которое поможет вам выбрать оптимальный вариант: сообщения, отправляемые с устройства в облако, переданные свойства или отправку файла.</span><span class="sxs-lookup"><span data-stu-id="c9434-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="c9434-115">Чтобы принять решение об использовании сообщений, отправляемых из облака на устройство, требуемых свойств или прямых методов см. сведения в [руководстве по обмену данными между облаком и устройством][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="c9434-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9434-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9434-116">Next steps</span></span>

* <span data-ttu-id="c9434-117">Дополнительные сведения о [сообщениях, передаваемых с устройства в облако][lnk-d2c], Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c9434-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="c9434-118">Дополнительные сведения о [сообщениях, передаваемых из облака на устройство][lnk-c2d], Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c9434-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md