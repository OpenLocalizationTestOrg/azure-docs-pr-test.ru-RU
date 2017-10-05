---
title: "Общие сведения о двойниках устройств в Центре Интернета вещей Azure | Документация Майкрософт"
description: "Руководство разработчика. Синхронизация данных состояния и конфигурации Центра Интернета вещей и устройств с помощью двойников устройств."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b316aa419d558547f90a914a22fb29935076de21
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="1704f-103">Общие сведения о двойниках устройств и их использование в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="1704f-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="1704f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1704f-104">Overview</span></span>
<span data-ttu-id="1704f-105">*Двойники устройств* — это документы JSON, хранящие сведения о состоянии устройства (метаданные, конфигурации и условия).</span><span class="sxs-lookup"><span data-stu-id="1704f-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="1704f-106">Центр Интернета вещей сохраняет двойник устройства для каждого устройства, подключаемого к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1704f-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span></span> <span data-ttu-id="1704f-107">Содержание статьи</span><span class="sxs-lookup"><span data-stu-id="1704f-107">This article describes:</span></span>

* <span data-ttu-id="1704f-108">структура двойника устройства: *теги*, *требуемые* и *сообщаемые свойства*;</span><span class="sxs-lookup"><span data-stu-id="1704f-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="1704f-109">операции, которые приложения устройств и серверные части могут выполнить на двойнике устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-109">The operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="1704f-110">На данный момент доступ к двойникам устройств можно получить только на устройствах, подключающихся к Центру Интернета вещей по протоколу MQTT.</span><span class="sxs-lookup"><span data-stu-id="1704f-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="1704f-111">Инструкции по преобразованию существующего приложения устройства для использования MQTT см. в статье [Взаимодействие с Центром Интернета вещей с помощью протокола MQTT][lnk-devguide-mqtt].</span><span class="sxs-lookup"><span data-stu-id="1704f-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

### <a name="when-to-use"></a><span data-ttu-id="1704f-112">Сценарии использования</span><span class="sxs-lookup"><span data-stu-id="1704f-112">When to use</span></span>
<span data-ttu-id="1704f-113">Двойники устройства используются для выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="1704f-113">Use device twins to:</span></span>

* <span data-ttu-id="1704f-114">Хранение метаданных для конкретного устройства в облаке.</span><span class="sxs-lookup"><span data-stu-id="1704f-114">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="1704f-115">Например, расположение развертывания торгового автомата.</span><span class="sxs-lookup"><span data-stu-id="1704f-115">For example, the deployment location of a vending machine.</span></span>
* <span data-ttu-id="1704f-116">Сообщение сведений о текущем состоянии приложения устройства, таких как доступные возможности и условия.</span><span class="sxs-lookup"><span data-stu-id="1704f-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="1704f-117">Например, подключение устройства к Центру Интернета вещей по сети мобильной связи или Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="1704f-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="1704f-118">Синхронизация состояния длительных рабочих процессов между приложением устройства и внутренним приложением.</span><span class="sxs-lookup"><span data-stu-id="1704f-118">Synchronize the state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="1704f-119">Например, при указании новой версии встроенного ПО в серверной части решения и сообщении различных этапов процесса обновления в приложении для устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span></span>
* <span data-ttu-id="1704f-120">выполнение запроса метаданных, конфигурации или состояния устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="1704f-121">Руководство по использованию сообщаемых свойств, сообщений, отправляемых с устройства в облако, или передаче файла см. в статье [Руководство по обмену данными между устройством и облаком][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="1704f-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="1704f-122">Руководство по использованию требуемых свойств, прямых методов или сообщений, отправляемых из облака на устройство, см. в статье [Руководство по обмену данными между облаком и устройством][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="1704f-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="1704f-123">Двойники устройства</span><span class="sxs-lookup"><span data-stu-id="1704f-123">Device twins</span></span>
<span data-ttu-id="1704f-124">Двойники устройств хранят сведения об устройствах:</span><span class="sxs-lookup"><span data-stu-id="1704f-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="1704f-125">Устройства и серверные части могут использовать их для синхронизации условий и конфигурации устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-125">Device and back ends can use to synchronize device conditions and configuration.</span></span>
* <span data-ttu-id="1704f-126">Серверная часть решения может использовать их для выполнения запроса и указания длительных операций.</span><span class="sxs-lookup"><span data-stu-id="1704f-126">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="1704f-127">Жизненный цикл двойника устройства связан с соответствующим [удостоверением устройства][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="1704f-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="1704f-128">Двойники устройства неявно создаются и удаляются при создании или удалении удостоверения устройства в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1704f-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="1704f-129">Двойник устройства является документом JSON, содержащим следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="1704f-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="1704f-130">**Теги**.</span><span class="sxs-lookup"><span data-stu-id="1704f-130">**Tags**.</span></span> <span data-ttu-id="1704f-131">Раздел документа JSON, который может считывать и в который может выполнять запись серверная часть решения.</span><span class="sxs-lookup"><span data-stu-id="1704f-131">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="1704f-132">Теги не видны для приложений устройств.</span><span class="sxs-lookup"><span data-stu-id="1704f-132">Tags are not visible to device apps.</span></span>
* <span data-ttu-id="1704f-133">**Требуемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="1704f-133">**Desired properties**.</span></span> <span data-ttu-id="1704f-134">Используются совместно с сообщаемыми свойствами для синхронизации конфигурации или условий устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-134">Used along with reported properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="1704f-135">Требуемые свойства задаются только в серверной части решения, а их чтение осуществляется в приложении для устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-135">Desired properties can only be set by the solution back end and can be read by the device app.</span></span> <span data-ttu-id="1704f-136">Приложение устройства может также в режиме реального времени получать уведомления об изменениях в требуемых свойствах.</span><span class="sxs-lookup"><span data-stu-id="1704f-136">The device app can also be notified in real time of changes in the desired properties.</span></span>
* <span data-ttu-id="1704f-137">**Сообщаемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="1704f-137">**Reported properties**.</span></span> <span data-ttu-id="1704f-138">Используется совместно с требуемыми свойствами для синхронизации конфигурации или условий устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-138">Used along with desired properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="1704f-139">Сообщаемые свойства задаются только в приложении для устройства, а их чтение и запрос осуществляется в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="1704f-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span></span>

<span data-ttu-id="1704f-140">Кроме того, корень документа JSON двойника устройства содержит свойства только для чтения из соответствующего удостоверения устройства, хранимые в [реестре удостоверений][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="1704f-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="1704f-141">Ниже приведен пример документа JSON двойника устройства:</span><span class="sxs-lookup"><span data-stu-id="1704f-141">The following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="1704f-142">В корневом объекте содержатся системные свойства и объекты контейнера для свойств `tags`, `reported` и `desired`.</span><span class="sxs-lookup"><span data-stu-id="1704f-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="1704f-143">Контейнер `properties` содержит некоторые элементы только для чтения (`$metadata`, `$etag` и `$version`), описанные в разделах [Метаданные двойника устройства][lnk-twin-metadata] и [Оптимистичный параллелизм][lnk-concurrency].</span><span class="sxs-lookup"><span data-stu-id="1704f-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="1704f-144">Пример сообщаемых свойств</span><span class="sxs-lookup"><span data-stu-id="1704f-144">Reported property example</span></span>
<span data-ttu-id="1704f-145">В предыдущем примере двойник устройства содержит свойство `batteryLevel`, сообщаемое приложением устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span></span> <span data-ttu-id="1704f-146">Это свойство позволяет выполнить запрос и работать на устройствах на основе последних сообщенных сведений об уровне заряда аккумулятора.</span><span class="sxs-lookup"><span data-stu-id="1704f-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span></span> <span data-ttu-id="1704f-147">Другой пример: приложение устройства сообщает о возможностях и вариантах подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-147">Other examples include the device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="1704f-148">Сообщаемые свойства упрощают сценарии, в которых серверной части решения нужно последнее известное значение свойства.</span><span class="sxs-lookup"><span data-stu-id="1704f-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="1704f-149">Используйте [сообщения, отправленные с устройства в облако][lnk-d2c], если серверной части решения нужно обработать данные телеметрии устройства в виде последовательности событий с метками времени, например временные ряды.</span><span class="sxs-lookup"><span data-stu-id="1704f-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="1704f-150">Пример требуемого свойства</span><span class="sxs-lookup"><span data-stu-id="1704f-150">Desired property example</span></span>
<span data-ttu-id="1704f-151">В предыдущем примере требуемые и сообщаемые свойства двойника устройства `telemetryConfig` используются в серверной части решения и приложении для устройства, чтобы синхронизировать конфигурацию телеметрии для этого устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span></span> <span data-ttu-id="1704f-152">Например:</span><span class="sxs-lookup"><span data-stu-id="1704f-152">For example:</span></span>

1. <span data-ttu-id="1704f-153">Серверная часть решения задает требуемое свойство со значением требуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1704f-153">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="1704f-154">Ниже приведен фрагмент документа с требуемым заданным свойством:</span><span class="sxs-lookup"><span data-stu-id="1704f-154">Here is the portion of the document with the desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="1704f-155">Приложение устройства получает уведомление об изменении немедленно, если оно подключено, или при первом повторном подключении.</span><span class="sxs-lookup"><span data-stu-id="1704f-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="1704f-156">Затем приложение устройства сообщает об обновленной конфигурации (или об условии ошибки с помощью свойства `status`).</span><span class="sxs-lookup"><span data-stu-id="1704f-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="1704f-157">Ниже представлена часть сообщаемого свойства.</span><span class="sxs-lookup"><span data-stu-id="1704f-157">Here is the portion of the reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="1704f-158">Серверная часть решения может отслеживать результаты операции изменения конфигурации на множестве устройств, [отправляя запросы][lnk-query] на двойники устройств.</span><span class="sxs-lookup"><span data-stu-id="1704f-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="1704f-159">Предыдущие фрагменты являются примерами способа кодирования конфигурации устройства и его состояния, оптимизированными для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="1704f-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span></span> <span data-ttu-id="1704f-160">Центр Интернета вещей не использует специальную схему для требуемых и сообщаемых свойств в двойниках устройств.</span><span class="sxs-lookup"><span data-stu-id="1704f-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span></span>
> 
> 

<span data-ttu-id="1704f-161">Двойники используются для синхронизации длительных операций, например обновления встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="1704f-161">You can use twins to synchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="1704f-162">Дополнительные сведения о синхронизации и отслеживании длительных операций на устройствах с помощью свойств см. в статье [Настройка устройств с помощью требуемых свойств (Node)][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="1704f-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="1704f-163">Операции серверной части</span><span class="sxs-lookup"><span data-stu-id="1704f-163">Back-end operations</span></span>
<span data-ttu-id="1704f-164">Серверная часть решения выполняет действия в двойнике устройства с помощью следующих атомарных операций, доступных по протоколу HTTP:</span><span class="sxs-lookup"><span data-stu-id="1704f-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="1704f-165">**Получение двойника устройства по идентификатору.** Эта операция возвращает документ двойника устройства, включая теги, а также требуемые, сообщаемые и системные свойства.</span><span class="sxs-lookup"><span data-stu-id="1704f-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="1704f-166">**Частичное обновление двойника устройства.**</span><span class="sxs-lookup"><span data-stu-id="1704f-166">**Partially update device twin**.</span></span> <span data-ttu-id="1704f-167">Эта операция позволяет серверной части решения частично обновить теги или требуемые свойства двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span></span> <span data-ttu-id="1704f-168">Частичное обновление выражается в качестве документа JSON, который добавляет или обновляет все свойства.</span><span class="sxs-lookup"><span data-stu-id="1704f-168">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="1704f-169">Свойства, для которых указано значение `null`, удаляются.</span><span class="sxs-lookup"><span data-stu-id="1704f-169">Properties set to `null` are removed.</span></span> <span data-ttu-id="1704f-170">Следующий пример создает требуемое свойство со значением `{"newProperty": "newValue"}`, перезаписывает существующее значение `existingProperty` на `"otherNewValue"` и удаляет `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="1704f-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="1704f-171">Другие существующие требуемые свойства или теги не изменяются:</span><span class="sxs-lookup"><span data-stu-id="1704f-171">No other changes are made to existing desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="1704f-172">**Заменить требуемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="1704f-172">**Replace desired properties**.</span></span> <span data-ttu-id="1704f-173">Эта операция позволяет серверной части решения полностью перезаписать все существующие требуемые свойства и заменить новый документ JSON для `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="1704f-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="1704f-174">**Заменить теги**.</span><span class="sxs-lookup"><span data-stu-id="1704f-174">**Replace tags**.</span></span> <span data-ttu-id="1704f-175">Эта операция позволяет серверной части решения полностью перезаписать все существующие теги и заменить новый документ JSON для `tags`.</span><span class="sxs-lookup"><span data-stu-id="1704f-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="1704f-176">**Получение уведомлений двойника**.</span><span class="sxs-lookup"><span data-stu-id="1704f-176">**Receive twin notifications**.</span></span> <span data-ttu-id="1704f-177">Эта операция позволяет серверной части решения получать уведомления при изменении двойника.</span><span class="sxs-lookup"><span data-stu-id="1704f-177">This operation allows the solution back end to be notified when the twin is modified.</span></span> <span data-ttu-id="1704f-178">Для этого в решении Интернета вещей необходимо создать маршрут и присвоить источнику данных значение *twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="1704f-178">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span></span> <span data-ttu-id="1704f-179">По умолчанию уведомления двойника не отправляются, то есть такие маршруты не существуют.</span><span class="sxs-lookup"><span data-stu-id="1704f-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="1704f-180">Если скорость изменения слишком высока или имеются какие-либо другие причины (например, внутренние сбои), Центр Интернета вещей может отправлять только одно уведомление, которое содержит все изменения.</span><span class="sxs-lookup"><span data-stu-id="1704f-180">If the rate of change is too high, or for other reasons, such as internal failures, the IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="1704f-181">Поэтому, если приложению требуется надежный аудит и ведение журнала всех промежуточных состояний, по-прежнему рекомендуется использовать сообщения, отправляемые с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="1704f-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="1704f-182">Уведомление двойника содержит свойства и текст.</span><span class="sxs-lookup"><span data-stu-id="1704f-182">The twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="1704f-183">Свойства</span><span class="sxs-lookup"><span data-stu-id="1704f-183">Properties</span></span>

    | <span data-ttu-id="1704f-184">Имя</span><span class="sxs-lookup"><span data-stu-id="1704f-184">Name</span></span> | <span data-ttu-id="1704f-185">Значение</span><span class="sxs-lookup"><span data-stu-id="1704f-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="1704f-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="1704f-186">$content-type</span></span> | <span data-ttu-id="1704f-187">приложение/json</span><span class="sxs-lookup"><span data-stu-id="1704f-187">application/json</span></span> |
    <span data-ttu-id="1704f-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="1704f-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="1704f-189">Время отправки уведомления</span><span class="sxs-lookup"><span data-stu-id="1704f-189">Time when the notification was sent</span></span> |
    <span data-ttu-id="1704f-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="1704f-190">$iothub-message-source</span></span> | <span data-ttu-id="1704f-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="1704f-191">twinChangeEvents</span></span> |
    <span data-ttu-id="1704f-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="1704f-192">$content-encoding</span></span> | <span data-ttu-id="1704f-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="1704f-193">utf-8</span></span> |
    <span data-ttu-id="1704f-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="1704f-194">deviceId</span></span> | <span data-ttu-id="1704f-195">Идентификатор устройства</span><span class="sxs-lookup"><span data-stu-id="1704f-195">Id of the device</span></span> |
    <span data-ttu-id="1704f-196">hubName</span><span class="sxs-lookup"><span data-stu-id="1704f-196">hubName</span></span> | <span data-ttu-id="1704f-197">Имя Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="1704f-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="1704f-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="1704f-198">operationTimestamp</span></span> | <span data-ttu-id="1704f-199">Метка времени операции по стандарту [ISO8601]</span><span class="sxs-lookup"><span data-stu-id="1704f-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="1704f-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="1704f-200">iothub-message-schema</span></span> | <span data-ttu-id="1704f-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="1704f-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="1704f-202">opType</span><span class="sxs-lookup"><span data-stu-id="1704f-202">opType</span></span> | <span data-ttu-id="1704f-203">"replaceTwin" или "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="1704f-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="1704f-204">Системные свойства сообщений начинаются с символов `'$'`.</span><span class="sxs-lookup"><span data-stu-id="1704f-204">Message system properties are prefixed with the `'$'` symbol.</span></span>

    - <span data-ttu-id="1704f-205">Текст</span><span class="sxs-lookup"><span data-stu-id="1704f-205">Body</span></span>
        
    <span data-ttu-id="1704f-206">Этот раздел содержит все изменения двойника в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="1704f-206">This section includes all the twin changes in a JSON format.</span></span> <span data-ttu-id="1704f-207">Он использует тот же формат, что и исправление, с тем отличием, что он может содержать все разделы двойника (теги, properties.reported, properties.desired) и что он содержит элементы "$metadata".</span><span class="sxs-lookup"><span data-stu-id="1704f-207">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span></span> <span data-ttu-id="1704f-208">Например,</span><span class="sxs-lookup"><span data-stu-id="1704f-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="1704f-209">Все предыдущие операции поддерживают [оптимистичный параллелизм][lnk-concurrency] и требуют разрешения **ServiceConnect**, как указано в статье о [безопасности][lnk-security].</span><span class="sxs-lookup"><span data-stu-id="1704f-209">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="1704f-210">Помимо выполнения этих операций серверная часть решений может:</span><span class="sxs-lookup"><span data-stu-id="1704f-210">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="1704f-211">отправлять запросы к двойникам устройств с помощью [языка запросов Центра Интернета вещей][lnk-query] типа SQL;</span><span class="sxs-lookup"><span data-stu-id="1704f-211">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="1704f-212">выполнять операции с большими наборами двойников устройств с помощью [заданий][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="1704f-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="1704f-213">Операции с устройствами</span><span class="sxs-lookup"><span data-stu-id="1704f-213">Device operations</span></span>
<span data-ttu-id="1704f-214">Приложение устройства выполняет действия в двойнике устройства с помощью следующих атомарных операций.</span><span class="sxs-lookup"><span data-stu-id="1704f-214">The device app operates on the device twin using the following atomic operations:</span></span>

1. <span data-ttu-id="1704f-215">**Получение двойника устройства.**</span><span class="sxs-lookup"><span data-stu-id="1704f-215">**Retrieve device twin**.</span></span> <span data-ttu-id="1704f-216">Эта операция возвращает документ двойника (включая теги, а также требуемые, сообщаемые и системные свойства) для подключенного устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-216">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span></span>
2. <span data-ttu-id="1704f-217">**Частично обновить сообщаемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="1704f-217">**Partially update reported properties**.</span></span> <span data-ttu-id="1704f-218">Эта операция позволяет частично обновить сообщаемые свойства подключенного устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-218">This operation enables the partial update of the reported properties of the currently connected device.</span></span> <span data-ttu-id="1704f-219">В этой операции используется тот же формат обновления JSON, как и при частичном обновлении требуемых свойств в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="1704f-219">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="1704f-220">**Отслеживать требуемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="1704f-220">**Observe desired properties**.</span></span> <span data-ttu-id="1704f-221">Для подключенного устройства можно настроить немедленное получение уведомлений об обновлениях нужного свойства в момент такого обновления.</span><span class="sxs-lookup"><span data-stu-id="1704f-221">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="1704f-222">Устройство выполняет такое же обновление (частичное обновление или полная замена), как и при выполнении в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="1704f-222">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="1704f-223">Все предыдущие операции требуют разрешения **DeviceConnect**, как указано в статье о [безопасности][lnk-security].</span><span class="sxs-lookup"><span data-stu-id="1704f-223">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="1704f-224">[Пакеты SDK для устройств Azure IoT][lnk-sdks] упрощают использование указанных выше операций на многих языках и платформах.</span><span class="sxs-lookup"><span data-stu-id="1704f-224">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span> <span data-ttu-id="1704f-225">Дополнительные сведения о примитивах Центра Интернета вещей для синхронизации требуемых свойств см. в разделе [Процедура при повторном подключении устройства][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="1704f-225">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="1704f-226">На данный момент доступ к двойникам устройств можно получить только на устройствах, подключающихся к Центру Интернета вещей по протоколу MQTT.</span><span class="sxs-lookup"><span data-stu-id="1704f-226">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="1704f-227">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="1704f-227">Reference topics:</span></span>
<span data-ttu-id="1704f-228">В следующих материалах предоставлены дополнительные сведения об управлении доступом к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1704f-228">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="1704f-229">Формат тегов и свойств</span><span class="sxs-lookup"><span data-stu-id="1704f-229">Tags and properties format</span></span>
<span data-ttu-id="1704f-230">Теги, а также требуемые и сообщаемые свойства являются объектами JSON, на которые накладываются следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="1704f-230">Tags, desired, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="1704f-231">Все ключи в объектах JSON представляют собой 64-байтовые строки Юникода UTF-8 с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="1704f-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="1704f-232">Разрешено использовать все знаки, кроме управляющих символов Юникода (сегменты C0 и C1), а также `'.'`, `' '` и `'$'`.</span><span class="sxs-lookup"><span data-stu-id="1704f-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="1704f-233">Все значения в объектах JSON могут быть следующих типов JSON: логический, число, строка и объект.</span><span class="sxs-lookup"><span data-stu-id="1704f-233">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="1704f-234">Запрещено использовать массивы.</span><span class="sxs-lookup"><span data-stu-id="1704f-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="1704f-235">Все объекты JSON в тегах, требуемых и сообщаемых свойствах могут иметь глубину не более 5.</span><span class="sxs-lookup"><span data-stu-id="1704f-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="1704f-236">Например, допустим следующий объект:</span><span class="sxs-lookup"><span data-stu-id="1704f-236">For instance, the following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="1704f-237">Все строковые значения могут быть длиной не более 512 байт.</span><span class="sxs-lookup"><span data-stu-id="1704f-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="1704f-238">Размер двойника устройства</span><span class="sxs-lookup"><span data-stu-id="1704f-238">Device twin size</span></span>
<span data-ttu-id="1704f-239">Центр Интернета вещей ограничивает размер значений `tags`, `properties/desired` и `properties/reported` до 8 КБ. Это ограничение не относится к элементам только для чтения.</span><span class="sxs-lookup"><span data-stu-id="1704f-239">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="1704f-240">Размер вычисляется путем подсчета всех знаков, кроме управляющих символов Юникода (сегменты C0 и C1) и пространства со знаком `' '`, если оно находится вне строковой константы.</span><span class="sxs-lookup"><span data-stu-id="1704f-240">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="1704f-241">Центр Интернета вещей отклоняет с ошибкой все операции, увеличивающие размер этих документов сверх ограничения.</span><span class="sxs-lookup"><span data-stu-id="1704f-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="1704f-242">Метаданные двойника устройства</span><span class="sxs-lookup"><span data-stu-id="1704f-242">Device twin metadata</span></span>
<span data-ttu-id="1704f-243">Центр Интернета вещей сохраняет метку времени последнего обновления для каждого объекта JSON в требуемых и сообщаемых свойствах двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="1704f-243">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="1704f-244">Метки времени указываются в формате UTC и кодируются в формате [ISO8601] (`YYYY-MM-DDTHH:MM:SS.mmmZ`).</span><span class="sxs-lookup"><span data-stu-id="1704f-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="1704f-245">Например:</span><span class="sxs-lookup"><span data-stu-id="1704f-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="1704f-246">Эти сведения хранятся на каждом уровне (а не только в конечных элементах структуры JSON) для сохранения обновлений, удаляющих ключи объекта.</span><span class="sxs-lookup"><span data-stu-id="1704f-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="1704f-247">Оптимистичный параллелизм</span><span class="sxs-lookup"><span data-stu-id="1704f-247">Optimistic concurrency</span></span>
<span data-ttu-id="1704f-248">Теги, а также требуемые и сообщаемые свойства поддерживают оптимистичный параллелизм.</span><span class="sxs-lookup"><span data-stu-id="1704f-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="1704f-249">Теги содержат ETag (согласно [RFC7232]), являющийся представлением JSON тега.</span><span class="sxs-lookup"><span data-stu-id="1704f-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="1704f-250">ETag можно использовать в операциях условного обновления в серверной части решения, чтобы обеспечить согласованность.</span><span class="sxs-lookup"><span data-stu-id="1704f-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="1704f-251">В требуемых и сообщаемых свойствах двойника устройства отсутствует ETag, но они содержат значение `$version`, которое гарантированно будет добавочным.</span><span class="sxs-lookup"><span data-stu-id="1704f-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="1704f-252">Аналогично ETag для обеспечения согласованности обновлений компонент, выполняющий обновление, использует версию.</span><span class="sxs-lookup"><span data-stu-id="1704f-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="1704f-253">Например, приложение устройства для сообщаемого свойства или серверная сторона для требуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="1704f-253">For example, a device app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="1704f-254">Версии также полезны, если агент, выполняющий отслеживание (например, приложение устройства, отслеживающее требуемые свойства), должен устранить состояние гонки между результатом извлечения и отправкой уведомлений об обновлении.</span><span class="sxs-lookup"><span data-stu-id="1704f-254">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="1704f-255">Дополнительные сведения см. в разделе [Процедура при повторном подключении устройства][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="1704f-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="1704f-256">Процедура при повторном подключении устройства</span><span class="sxs-lookup"><span data-stu-id="1704f-256">Device reconnection flow</span></span>
<span data-ttu-id="1704f-257">Центр Интернета вещей не сохраняет уведомления об обновлении требуемых свойств для отключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="1704f-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="1704f-258">Это значит, что подключающееся устройство должно получить весь документ требуемых свойств и подписаться на уведомления об обновлениях.</span><span class="sxs-lookup"><span data-stu-id="1704f-258">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span></span> <span data-ttu-id="1704f-259">Учитывая возможность возникновения состояния гонки между уведомлениями об обновлениях и полным извлечением, следуйте процедуре ниже:</span><span class="sxs-lookup"><span data-stu-id="1704f-259">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span></span>

1. <span data-ttu-id="1704f-260">Приложение устройства подключается к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1704f-260">Device app connects to an IoT hub.</span></span>
2. <span data-ttu-id="1704f-261">Приложение устройства подписывается на уведомления об обновлениях требуемых свойств.</span><span class="sxs-lookup"><span data-stu-id="1704f-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="1704f-262">Приложение устройства получает весь документ требуемых свойств.</span><span class="sxs-lookup"><span data-stu-id="1704f-262">Device app retrieves the full document for desired properties.</span></span>

<span data-ttu-id="1704f-263">Приложение устройства может игнорировать все уведомления со значением `$version`, которое меньше значения версии полного полученного документа или равно ему.</span><span class="sxs-lookup"><span data-stu-id="1704f-263">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span></span> <span data-ttu-id="1704f-264">Такой подход возможен, так как Центр Интернета вещей гарантирует постоянное увеличение версий.</span><span class="sxs-lookup"><span data-stu-id="1704f-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="1704f-265">Эта логика уже реализована в [пакетах SDK для устройств Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="1704f-265">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="1704f-266">Это описание полезно, только если приложение устройства не может использовать пакеты SDK для устройств Azure IoT и должно программировать интерфейс MQTT напрямую.</span><span class="sxs-lookup"><span data-stu-id="1704f-266">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="1704f-267">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="1704f-267">Additional reference material</span></span>
<span data-ttu-id="1704f-268">Другие справочные статьи в руководстве разработчика для Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="1704f-268">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="1704f-269">В статье [Руководство. Конечные точки Центра Интернета вещей][lnk-endpoints] содержатся сведения о конечных точках, которые каждый Центр Интернета вещей предоставляет для операций управления и среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="1704f-269">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="1704f-270">Статья [Руководство. Квоты и регулирование в Центре Интернета вещей][lnk-quotas] содержит сведения о квотах, применимых к службе Центра Интернета вещей, и ожидаемом поведении регулирования при использовании службы.</span><span class="sxs-lookup"><span data-stu-id="1704f-270">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="1704f-271">В статье [Общие сведения о пакетах SDK для Azure IoT и их использование][lnk-sdks] указаны различные языковые пакеты SDK, которые можно использовать при разработке приложений для устройств и служб, взаимодействующих с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1704f-271">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="1704f-272">[Справочник по языку запросов Центра Интернета вещей для двойников устройств, заданий и маршрутизации сообщений][lnk-query] содержит сведения о языке запросов, который можно использовать для получения сведений о двойниках устройств и заданиях из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1704f-272">The [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="1704f-273">В статье [Взаимодействие с Центром Интернета вещей с помощью протокола MQTT][lnk-devguide-mqtt] приведены дополнительные сведения о поддержке протокола MQTT в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1704f-273">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1704f-274">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1704f-274">Next steps</span></span>
<span data-ttu-id="1704f-275">Теперь, когда вы узнали о двойниках устройств, вас могут заинтересовать следующие статьи руководства разработчика для Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="1704f-275">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="1704f-276">[Вызов прямого метода на устройстве][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="1704f-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="1704f-277">[Schedule jobs on multiple devices][lnk-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="1704f-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="1704f-278">Если вы хотели бы применить на практике некоторые основные понятия, описанные в этой статье, можно просмотреть следующие руководства по Центру Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="1704f-278">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="1704f-279">[Приступая к работе с двойниками устройств (предварительная версия)][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="1704f-279">[How to use the device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="1704f-280">[Руководство. Настройка устройств с помощью требуемых свойств (предварительная версия)][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="1704f-280">[How to use device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
