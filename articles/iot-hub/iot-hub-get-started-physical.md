---
title: "Начало работы с подключением физических устройств к Центру Интернета вещей Azure | Документация Майкрософт"
description: "Узнайте, как подключать физические устройства и платы к Центру Интернета вещей Azure. Устройства могут отправлять данные телеметрии в Центр Интернета вещей, который, в свою очередь, может отслеживать эти устройства и управлять ими."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: "Руководство по работе с Центром Интернета вещей Azure"
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: f4128b6b049aa876e170c56dcf2e40720644dc3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="fc941-105">Руководства по началу работы с Центром Интернета вещей и физическими устройствами</span><span class="sxs-lookup"><span data-stu-id="fc941-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="fc941-106">В этих руководствах представлены общие сведения о Центре Интернета вещей Azure и пакетах SDK для устройств.</span><span class="sxs-lookup"><span data-stu-id="fc941-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="fc941-107">Также описаны распространенные сценарии с использованием Интернета вещей, в которых демонстрируются возможности Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc941-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="fc941-108">В руководствах также объясняется, как объединить Центр Интернета вещей с другими службами и средствами Azure для создания более мощных решений Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc941-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="fc941-109">В руководствах, перечисленных в следующей таблице, показано как создавать физические устройства Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc941-109">The tutorials listed in the following table show you how to create physical IoT devices.</span></span>

| <span data-ttu-id="fc941-110">Устройство IoT</span><span class="sxs-lookup"><span data-stu-id="fc941-110">IoT device</span></span>                       | <span data-ttu-id="fc941-111">Язык программирования</span><span class="sxs-lookup"><span data-stu-id="fc941-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="fc941-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="fc941-112">Raspberry Pi</span></span>                    | <span data-ttu-id="fc941-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="fc941-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="fc941-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="fc941-114">IoT DevKit</span></span>                      | <span data-ttu-id="fc941-115">[Arduino в VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="fc941-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="fc941-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="fc941-116">Intel Edison</span></span>                    | <span data-ttu-id="fc941-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="fc941-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="fc941-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="fc941-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="fc941-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="fc941-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="fc941-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="fc941-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="fc941-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="fc941-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="fc941-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="fc941-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="fc941-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="fc941-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="fc941-124">Кроме того, можно использовать шлюз Edge Интернета вещей, чтобы устройство могло подключаться к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="fc941-124">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="fc941-125">Устройство шлюза</span><span class="sxs-lookup"><span data-stu-id="fc941-125">Gateway device</span></span>               | <span data-ttu-id="fc941-126">Язык программирования</span><span class="sxs-lookup"><span data-stu-id="fc941-126">Programming language</span></span> | <span data-ttu-id="fc941-127">Платформа</span><span class="sxs-lookup"><span data-stu-id="fc941-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="fc941-128">Intel NUC (модель DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="fc941-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="fc941-129">C</span><span class="sxs-lookup"><span data-stu-id="fc941-129">C</span></span>                    | <span data-ttu-id="fc941-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="fc941-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
