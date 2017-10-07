---
title: "масштабирование центра IoT aaaAzure | Документы Microsoft"
description: "Как tooscale вашей toosupport концентратора IoT пропускная способность ожидаемые сообщения. Сводка по пропускной способности hello поддерживается для каждого уровня и параметры для сегментирования."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="90963-104">Масштабирование решения для Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="90963-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="90963-105">Центр IoT Azure может поддерживать tooa миллионов одновременно подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="90963-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="90963-106">Дополнительные сведения см. на странице с [ценами на Центр Интернета вещей Azure][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="90963-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="90963-107">Каждая единица центра IoT предусматривает определенное количество сообщений в день.</span><span class="sxs-lookup"><span data-stu-id="90963-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="90963-108">tooproperly масштабирования решения, рассмотрите возможность использования центра IoT.</span><span class="sxs-lookup"><span data-stu-id="90963-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="90963-109">В частности примите во внимание пропускную способность пиковых нагрузок hello необходимые для hello, следующие категории операций.</span><span class="sxs-lookup"><span data-stu-id="90963-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="90963-110">Отправка сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="90963-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="90963-111">Получение сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="90963-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="90963-112">операции с реестром удостоверений.</span><span class="sxs-lookup"><span data-stu-id="90963-112">Identity registry operations</span></span>

<span data-ttu-id="90963-113">Добавление сведений о toothis пропускной способности, см. [центр IoT квот и регулировок] [ IoT Hub quotas and throttles] и разработать решение соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="90963-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="90963-114">Пропускная способность для передачи сообщений с устройств в облако и из облака на устройства</span><span class="sxs-lookup"><span data-stu-id="90963-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="90963-115">Hello лучшим способом toosize решения центр IoT — это трафик hello tooevaluate на основе единицу.</span><span class="sxs-lookup"><span data-stu-id="90963-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="90963-116">Для сообщений, передаваемых с устройства в облако, следует соблюдать такие правила.</span><span class="sxs-lookup"><span data-stu-id="90963-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="90963-117">Уровень</span><span class="sxs-lookup"><span data-stu-id="90963-117">Tier</span></span> | <span data-ttu-id="90963-118">Непрерывная пропускная способность</span><span class="sxs-lookup"><span data-stu-id="90963-118">Sustained throughput</span></span> | <span data-ttu-id="90963-119">Непрерывная скорость отправки</span><span class="sxs-lookup"><span data-stu-id="90963-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90963-120">S1</span><span class="sxs-lookup"><span data-stu-id="90963-120">S1</span></span> |<span data-ttu-id="90963-121">Копирование too1111 КБ за минуту на единицу</span><span class="sxs-lookup"><span data-stu-id="90963-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="90963-122">(1,5 ГБ/день на единицу)</span><span class="sxs-lookup"><span data-stu-id="90963-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="90963-123">В среднем 278 сообщений/мин на единицу</span><span class="sxs-lookup"><span data-stu-id="90963-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="90963-124">(400 000 сообщений/день на единицу)</span><span class="sxs-lookup"><span data-stu-id="90963-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="90963-125">S2</span><span class="sxs-lookup"><span data-stu-id="90963-125">S2</span></span> |<span data-ttu-id="90963-126">Копирование too16 МБ в минуту на единицу</span><span class="sxs-lookup"><span data-stu-id="90963-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="90963-127">(22,8 ГБ/день на единицу)</span><span class="sxs-lookup"><span data-stu-id="90963-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="90963-128">В среднем 4167 сообщений/мин на единицу</span><span class="sxs-lookup"><span data-stu-id="90963-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="90963-129">(6 миллионов сообщений/день на единицу)</span><span class="sxs-lookup"><span data-stu-id="90963-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="90963-130">S3</span><span class="sxs-lookup"><span data-stu-id="90963-130">S3</span></span> |<span data-ttu-id="90963-131">Копирование too814 МБ в минуту на единицу</span><span class="sxs-lookup"><span data-stu-id="90963-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="90963-132">(1144,4 ГБ/день на единицу).</span><span class="sxs-lookup"><span data-stu-id="90963-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="90963-133">В среднем 208 333 сообщения/мин на единицу</span><span class="sxs-lookup"><span data-stu-id="90963-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="90963-134">(300 млн сообщений/день на единицу).</span><span class="sxs-lookup"><span data-stu-id="90963-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="90963-135">Пропускная способность для операций с реестром удостоверений</span><span class="sxs-lookup"><span data-stu-id="90963-135">Identity registry operation throughput</span></span>
<span data-ttu-id="90963-136">Центр IoT операциями с реестром идентификаторов не должны toobe во время выполнения операции, как они являются главным образом связанных toodevice подготовки.</span><span class="sxs-lookup"><span data-stu-id="90963-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="90963-137">Сведения о конкретных показателях пиковой пропускной способности см. в статье [Справочник: квоты и регулирование][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="90963-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="90963-138">Сегментирование</span><span class="sxs-lookup"><span data-stu-id="90963-138">Sharding</span></span>
<span data-ttu-id="90963-139">Наряду с одного центра IoT можно масштабировать toomillions устройств, иногда решение требует характеристики производительности, которые один центр IoT не может гарантировать.</span><span class="sxs-lookup"><span data-stu-id="90963-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="90963-140">В этом случае рекомендуется распределить устройства между несколькими центрами IoT.</span><span class="sxs-lookup"><span data-stu-id="90963-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="90963-141">Несколько центры IoT smooth увеличению трафика и получите hello требованиями к пропускной способности или ставки операции, которые являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="90963-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90963-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="90963-142">Next steps</span></span>
<span data-ttu-id="90963-143">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="90963-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="90963-144">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="90963-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="90963-145">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="90963-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
