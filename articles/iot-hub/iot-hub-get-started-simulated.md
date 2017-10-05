---
title: "Начало работы с подключением имитируемых устройств к Центру Интернета вещей Azure | Документация Майкрософт"
description: "Узнайте, как создавать имитируемые устройства Интернета вещей и подключать их к Центру Интернета вещей Azure. Устройства могут отправлять данные телеметрии в Центр Интернета вещей, который, в свою очередь, может отслеживать эти устройства и управлять ими."
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
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 436b3057509a831837159e814490959a2d7455a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="09da7-105">Руководства по началу работы с Центром Интернета вещей и имитируемыми устройствами</span><span class="sxs-lookup"><span data-stu-id="09da7-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="09da7-106">В этих руководствах представлены общие сведения о Центре Интернета вещей Azure и пакетах SDK для устройств.</span><span class="sxs-lookup"><span data-stu-id="09da7-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="09da7-107">Также описаны распространенные сценарии с использованием Интернета вещей, в которых демонстрируются возможности Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="09da7-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="09da7-108">В руководствах также объясняется, как объединить Центр Интернета вещей с другими службами и средствами Azure для создания более мощных решений Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="09da7-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="09da7-109">В руководствах, перечисленных в следующей таблице, показано как создавать имитируемые устройства Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="09da7-109">The tutorials listed in the following table show you how to create simulated IoT devices.</span></span>

| <span data-ttu-id="09da7-110">Язык программирования</span><span class="sxs-lookup"><span data-stu-id="09da7-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="09da7-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="09da7-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="09da7-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="09da7-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="09da7-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="09da7-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="09da7-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="09da7-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="09da7-115">Кроме того, вы можете использовать шлюз IoT Edge для подключения имитируемых устройств к вашему Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="09da7-115">In addition, you can use an IoT Edge gateway to enable simulated devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="09da7-116">Язык программирования</span><span class="sxs-lookup"><span data-stu-id="09da7-116">Programming language</span></span> | <span data-ttu-id="09da7-117">Платформа</span><span class="sxs-lookup"><span data-stu-id="09da7-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="09da7-118">C</span><span class="sxs-lookup"><span data-stu-id="09da7-118">C</span></span>                    | <span data-ttu-id="09da7-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="09da7-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="09da7-120">C</span><span class="sxs-lookup"><span data-stu-id="09da7-120">C</span></span>                    | <span data-ttu-id="09da7-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="09da7-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
