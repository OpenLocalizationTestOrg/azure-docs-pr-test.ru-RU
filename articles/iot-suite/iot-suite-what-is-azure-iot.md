---
title: "Решения Azure для Интернета вещей (IoT Suite) | Документация Майкрософт"
description: "Общие сведения об Интернете вещей в Azure, включая пример архитектуры решения, а также о его связи с набором Azure IoT Suite и предварительно настроенных решениях."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 437d2655-896f-4a9e-a4a8-b864790d3ef8
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 320190488bb4c7b8192421f9dd50a5264f558584
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a><span data-ttu-id="6746b-103">Набор Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="6746b-103">Azure IoT Suite</span></span>
<span data-ttu-id="6746b-104">Набор Microsoft Azure IoT — это решение корпоративного уровня, которое позволяет быстро приступить к работе с помощью набора расширяемых предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="6746b-104">The Microsoft Azure IoT Suite is an enterprise-grade solution that enables you to get started quickly through a set of extensible preconfigured solutions.</span></span> <span data-ttu-id="6746b-105">Эти решения подходят для таких распространенных сценариев Интернета вещей, как [Удаленный мониторинг][lnk-preconfigured-solutions], [Прогнозное обслуживание][lnk-predictive-maintenance] и [Подключенная фабрика][lnk-connected-factory].</span><span class="sxs-lookup"><span data-stu-id="6746b-105">These solutions address common IoT scenarios, such as [remote monitoring][lnk-preconfigured-solutions], [predictive maintenance][lnk-predictive-maintenance], and [connected factory][lnk-connected-factory].</span></span> <span data-ttu-id="6746b-106">Эти решения представляют собой реализацию архитектуры решений IoT, описанной в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6746b-106">These solutions are implementations of the IoT solution architecture outlined in this article.</span></span>

<span data-ttu-id="6746b-107">Предварительно настроенные решения являются полными, работающими, комплексными решениями, которые включают в себя следующее:</span><span class="sxs-lookup"><span data-stu-id="6746b-107">The preconfigured solutions are complete, working, end-to-end solutions that include:</span></span>

- <span data-ttu-id="6746b-108">виртуальные устройства, необходимые для начала работы;</span><span class="sxs-lookup"><span data-stu-id="6746b-108">Simulated devices to get you started.</span></span>
- <span data-ttu-id="6746b-109">предварительно настроенные службы Azure, такие как [Центр Интернета вещей Azure][Azure IoT Hub], [концентраторы событий Azure][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [машинное обучение Azure][Azure Machine Learning] и [служба хранилища Azure][Azure storage];</span><span class="sxs-lookup"><span data-stu-id="6746b-109">Preconfigured Azure services such as [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning], and [Azure storage][Azure storage].</span></span>
- <span data-ttu-id="6746b-110">консоли управления определенного решения.</span><span class="sxs-lookup"><span data-stu-id="6746b-110">Solution-specific management consoles.</span></span>

<span data-ttu-id="6746b-111">Предварительно настроенные решения содержат проверенный, готовый к работе код, который можно настраивать и расширять для реализации определенных сценариев IoT.</span><span class="sxs-lookup"><span data-stu-id="6746b-111">The preconfigured solutions contain proven, production-ready code that you can customize and extend to implement your own specific IoT scenarios.</span></span>

<span data-ttu-id="6746b-112">Возможно, вас также интересует служба [Центра Интернета вещей Azure][Azure IoT Hub], которую используют многие из предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="6746b-112">You may also be interested in the [Azure IoT Hub][Azure IoT Hub] service that many of the preconfigured solutions use.</span></span> <span data-ttu-id="6746b-113">[Центр Интернета вещей Azure][Azure IoT Hub] обеспечивает безопасный и надежный двунаправленный обмен данными между устройствами и облаком, которые используются в архитектуре предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="6746b-113">[Azure IoT Hub][Azure IoT Hub] provides the secure and reliable bi-directional communications between devices and the cloud used in the preconfigured solution architecture.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6746b-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6746b-114">Next steps</span></span>
<span data-ttu-id="6746b-115">Ознакомьтесь с этими статьями, чтобы узнать больше об IoT Suite и предварительно настроенных решениях.</span><span class="sxs-lookup"><span data-stu-id="6746b-115">Explore these resources to continue learning about IoT Suite and the preconfigured solutions:</span></span>

* <span data-ttu-id="6746b-116">[Что такое Azure IoT Suite?][lnk-whatissuite]</span><span class="sxs-lookup"><span data-stu-id="6746b-116">[What is Azure IoT Suite?][lnk-whatissuite]</span></span>
* <span data-ttu-id="6746b-117">[Что такое предварительно настроенные решения Azure IoT Suite?][lnk-whatarepreconfigured]</span><span class="sxs-lookup"><span data-stu-id="6746b-117">[What are the Azure IoT Suite preconfigured solutions?][lnk-whatarepreconfigured]</span></span>

[lnk-whatissuite]: iot-suite-overview.md
[lnk-whatarepreconfigured]: iot-suite-what-are-preconfigured-solutions.md

[lnk-preconfigured-solutions]: iot-suite-getstarted-preconfigured-solutions.md
[Azure IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Azure Event Hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Azure Stream Analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[Azure Machine Learning]: https://azure.microsoft.com/documentation/services/machine-learning/
[Azure storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-connected-factory]: iot-suite-connected-factory-overview.md