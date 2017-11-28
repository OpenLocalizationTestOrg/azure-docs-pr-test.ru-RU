---
title: "Начать подключение физического устройства tooAzure центр IoT | Документы Microsoft"
description: "Узнайте, как tooconnect физических устройств и на досках tooAzure центр IoT. Устройства можно отправить tooIoT телеметрии концентратора и центра IoT можно отслеживать и управлять устройствами."
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
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="901b4-105">Руководства по началу работы с Центром Интернета вещей и физическими устройствами</span><span class="sxs-lookup"><span data-stu-id="901b4-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="901b4-106">В этих учебниках представлены tooAzure центр IoT и устройством hello пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="901b4-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="901b4-107">Hello учебниках рассматриваются общие возможности IoT сценариев toodemonstrate hello из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="901b4-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="901b4-108">Hello учебниках также представлены как toocombine центр IoT с другими Azure службы и средств toobuild более мощные решения IoT.</span><span class="sxs-lookup"><span data-stu-id="901b4-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="901b4-109">Hello учебники, перечисленные в hello после Показать таблицу можно как toocreate физическими устройствами IoT.</span><span class="sxs-lookup"><span data-stu-id="901b4-109">hello tutorials listed in hello following table show you how toocreate physical IoT devices.</span></span>

| <span data-ttu-id="901b4-110">Устройство IoT</span><span class="sxs-lookup"><span data-stu-id="901b4-110">IoT device</span></span>                       | <span data-ttu-id="901b4-111">Язык программирования</span><span class="sxs-lookup"><span data-stu-id="901b4-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="901b4-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="901b4-112">Raspberry Pi</span></span>                    | <span data-ttu-id="901b4-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="901b4-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="901b4-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="901b4-114">IoT DevKit</span></span>                      | <span data-ttu-id="901b4-115">[Arduino в VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="901b4-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="901b4-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="901b4-116">Intel Edison</span></span>                    | <span data-ttu-id="901b4-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="901b4-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="901b4-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="901b4-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="901b4-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="901b4-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="901b4-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="901b4-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="901b4-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="901b4-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="901b4-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="901b4-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="901b4-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="901b4-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="901b4-124">Кроме того можно использовать центр IoT tooyour IoT пограничного шлюза tooenable устройств tooconnect.</span><span class="sxs-lookup"><span data-stu-id="901b4-124">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="901b4-125">Устройство шлюза</span><span class="sxs-lookup"><span data-stu-id="901b4-125">Gateway device</span></span>               | <span data-ttu-id="901b4-126">Язык программирования</span><span class="sxs-lookup"><span data-stu-id="901b4-126">Programming language</span></span> | <span data-ttu-id="901b4-127">Платформа</span><span class="sxs-lookup"><span data-stu-id="901b4-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="901b4-128">Intel NUC (модель DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="901b4-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="901b4-129">C</span><span class="sxs-lookup"><span data-stu-id="901b4-129">C</span></span>                    | <span data-ttu-id="901b4-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="901b4-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
