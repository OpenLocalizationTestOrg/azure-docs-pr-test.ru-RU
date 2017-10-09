---
title: "Центр IoT Azure — начать подключение облака toohello устройств IoT | Документы Microsoft"
description: "Узнайте, как tooconnect ваших досок IoT и начальные наборы tooAzure центр IoT. Устройства можно отправить tooIoT телеметрии концентратора и центра IoT можно отслеживать и управлять устройствами."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Руководство по работе с Центром Интернета вещей Azure"
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="295ca-105">Руководства по началу работы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="295ca-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="295ca-106">Можно использовать центр IoT Azure и hello Azure IoT SDK toobuild Интернета вещей (IoT) устройствами:</span><span class="sxs-lookup"><span data-stu-id="295ca-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="295ca-107">Центр IoT Azure — это полностью управляемая служба в облаке hello, безопасно подключаются, отслеживает и управляет устройствами IoT.</span><span class="sxs-lookup"><span data-stu-id="295ca-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="295ca-108">Используйте пакеты SDK Azure IoT tooimplement hello устройствами IoT.</span><span class="sxs-lookup"><span data-stu-id="295ca-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="295ca-109">С помощью шлюза Интернета вещей можно реализовать более сложные сценарии, связанные с Интернетом вещей.</span><span class="sxs-lookup"><span data-stu-id="295ca-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="295ca-110">Например, когда необходимо tooconsider факторов, таких как устаревшие устройства, затраты на полосу пропускания, политик безопасности и конфиденциальности или край обработки данных.</span><span class="sxs-lookup"><span data-stu-id="295ca-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="295ca-111">В этих сценариях используется tooimplement Azure IoT пограничного шлюза, который соединяет центр IoT tooyour устройств.</span><span class="sxs-lookup"><span data-stu-id="295ca-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="295ca-112">Что входит в учебниках hello</span><span class="sxs-lookup"><span data-stu-id="295ca-112">What hello tutorials cover</span></span>

<span data-ttu-id="295ca-113">В этих учебниках представлены tooAzure центр IoT и устройством hello пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="295ca-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="295ca-114">Hello учебниках рассматриваются общие возможности IoT сценариев toodemonstrate hello из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="295ca-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="295ca-115">Hello учебниках также представлены как toocombine центр IoT с другими Azure службы и средств toobuild более мощные решения IoT.</span><span class="sxs-lookup"><span data-stu-id="295ca-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="295ca-116">В учебниках hello вы можете toouse либо имитируемой или реальной устройствами IoT.</span><span class="sxs-lookup"><span data-stu-id="295ca-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="295ca-117">Кроме того, рассказывается, как toouse шлюза tooenable устройств tooconnect tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="295ca-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="295ca-118">Настройка устройства</span><span class="sxs-lookup"><span data-stu-id="295ca-118">Set up your device</span></span>

<span data-ttu-id="295ca-119">Подключите IoT устройства или шлюза tooAzure центр IoT.</span><span class="sxs-lookup"><span data-stu-id="295ca-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="295ca-120">Можно выбрать tooget физического или имитации устройства к работе.</span><span class="sxs-lookup"><span data-stu-id="295ca-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="295ca-121">Устройство IoT</span><span class="sxs-lookup"><span data-stu-id="295ca-121">IoT device</span></span>                       | <span data-ttu-id="295ca-122">Язык программирования</span><span class="sxs-lookup"><span data-stu-id="295ca-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="295ca-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="295ca-123">Raspberry Pi</span></span>                     | <span data-ttu-id="295ca-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="295ca-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="295ca-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="295ca-125">IoT DevKit</span></span>                       | <span data-ttu-id="295ca-126">[Arduino в VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="295ca-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="295ca-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="295ca-127">Intel Edison</span></span>                     | <span data-ttu-id="295ca-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="295ca-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="295ca-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="295ca-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="295ca-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="295ca-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="295ca-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="295ca-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="295ca-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="295ca-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="295ca-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="295ca-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="295ca-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="295ca-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="295ca-135">Имитация устройства на компьютере</span><span class="sxs-lookup"><span data-stu-id="295ca-135">Simulated device on PC</span></span>           | <span data-ttu-id="295ca-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="295ca-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="295ca-137">Онлайн-симулятор устройства</span><span class="sxs-lookup"><span data-stu-id="295ca-137">Online device simulator</span></span>         | <span data-ttu-id="295ca-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="295ca-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="295ca-139">Кроме того можно использовать центр IoT tooyour IoT пограничного шлюза tooenable устройств tooconnect:</span><span class="sxs-lookup"><span data-stu-id="295ca-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="295ca-140">Устройство шлюза</span><span class="sxs-lookup"><span data-stu-id="295ca-140">Gateway device</span></span>               | <span data-ttu-id="295ca-141">Язык программирования</span><span class="sxs-lookup"><span data-stu-id="295ca-141">Programming language</span></span> | <span data-ttu-id="295ca-142">Платформа</span><span class="sxs-lookup"><span data-stu-id="295ca-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="295ca-143">Intel NUC (модель DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="295ca-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="295ca-144">C</span><span class="sxs-lookup"><span data-stu-id="295ca-144">C</span></span>                    | <span data-ttu-id="295ca-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="295ca-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="295ca-146">Виртуальное устройство</span><span class="sxs-lookup"><span data-stu-id="295ca-146">Simulated gateway</span></span>            | <span data-ttu-id="295ca-147">C</span><span class="sxs-lookup"><span data-stu-id="295ca-147">C</span></span>                    | <span data-ttu-id="295ca-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="295ca-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
