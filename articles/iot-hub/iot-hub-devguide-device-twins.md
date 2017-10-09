---
title: "близнецы устройства Azure IoT Hub aaaUnderstand | Документы Microsoft"
description: "Руководство разработчика - использовать устройство близнецы toosynchronize состояние и данные конфигурации между центр IoT и устройств"
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
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="f26b0-103">Общие сведения о двойниках устройств и их использование в Центре Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f26b0-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="f26b0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f26b0-104">Overview</span></span>
<span data-ttu-id="f26b0-105">*Двойники устройств* — это документы JSON, хранящие сведения о состоянии устройства (метаданные, конфигурации и условия).</span><span class="sxs-lookup"><span data-stu-id="f26b0-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="f26b0-106">Центр IoT сохранение двойных устройства для каждого устройства, подключении tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="f26b0-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="f26b0-107">Содержание статьи</span><span class="sxs-lookup"><span data-stu-id="f26b0-107">This article describes:</span></span>

* <span data-ttu-id="f26b0-108">Здравствуйте структура двойных устройства hello: *теги*, *требуемой* и *сообщил свойства*, и</span><span class="sxs-lookup"><span data-stu-id="f26b0-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="f26b0-109">операции Hello, приложений для устройств и заканчивается обратной можно выполнить на устройстве близнецы.</span><span class="sxs-lookup"><span data-stu-id="f26b0-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="f26b0-110">В настоящее время устройство близнецы доступны только из устройств, которые подключаются tooIoT концентратора с помощью протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="f26b0-111">Ссылки toohello [MQTT поддержки] [ lnk-devguide-mqtt] статье инструкции о том, как приложение toouse tooconvert существующие устройства MQTT.</span><span class="sxs-lookup"><span data-stu-id="f26b0-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="f26b0-112">Когда toouse</span><span class="sxs-lookup"><span data-stu-id="f26b0-112">When toouse</span></span>
<span data-ttu-id="f26b0-113">Двойники устройства используются для выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="f26b0-113">Use device twins to:</span></span>

* <span data-ttu-id="f26b0-114">Метаданные для конкретного устройства хранения в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="f26b0-115">Здравствуйте, например, Торговый автомат расположение развертывания.</span><span class="sxs-lookup"><span data-stu-id="f26b0-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="f26b0-116">Сообщение сведений о текущем состоянии приложения устройства, таких как доступные возможности и условия.</span><span class="sxs-lookup"><span data-stu-id="f26b0-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="f26b0-117">Например, устройство является центр IoT подключенных tooyour over сотовой и Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="f26b0-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="f26b0-118">Синхронизируйте состояние hello длительных рабочих процессов между приложением устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="f26b0-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="f26b0-119">Например при hello решение обратно end указывает hello новый tooinstall версии встроенного по и отчеты приложения hello устройств hello различные этапы процесса обновления hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="f26b0-120">выполнение запроса метаданных, конфигурации или состояния устройства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="f26b0-121">См. слишком[руководство связи устройства в облако] [ lnk-d2c-guidance] рекомендации по использованию выводятся свойства, сообщения из устройства в облако или передачи файла.</span><span class="sxs-lookup"><span data-stu-id="f26b0-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="f26b0-122">См. слишком[руководство связи облака на устройство] [ lnk-c2d-guidance] рекомендации по работе с нужными свойствами, непосредственные методы или сообщений облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="f26b0-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="f26b0-123">Двойники устройства</span><span class="sxs-lookup"><span data-stu-id="f26b0-123">Device twins</span></span>
<span data-ttu-id="f26b0-124">Двойники устройств хранят сведения об устройствах:</span><span class="sxs-lookup"><span data-stu-id="f26b0-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="f26b0-125">Заканчивается устройства и обратно можно использовать условия toosynchronize устройств и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f26b0-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="f26b0-126">Hello решения серверной части можно использовать tooquery и целевой длительных операций.</span><span class="sxs-lookup"><span data-stu-id="f26b0-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="f26b0-127">жизненный цикл Hello двойных устройства связан соответствующий toohello [удостоверение устройства][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="f26b0-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="f26b0-128">Двойники устройства неявно создаются и удаляются при создании или удалении удостоверения устройства в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f26b0-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="f26b0-129">Двойник устройства является документом JSON, содержащим следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="f26b0-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="f26b0-130">**Теги**.</span><span class="sxs-lookup"><span data-stu-id="f26b0-130">**Tags**.</span></span> <span data-ttu-id="f26b0-131">Раздела документа JSON hello, hello серверной части решения могут считывать и записывать.</span><span class="sxs-lookup"><span data-stu-id="f26b0-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="f26b0-132">Теги не видны toodevice приложения.</span><span class="sxs-lookup"><span data-stu-id="f26b0-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="f26b0-133">**Требуемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="f26b0-133">**Desired properties**.</span></span> <span data-ttu-id="f26b0-134">Используется вместе с конфигурации устройства toosynchronize свойств отчета или условий.</span><span class="sxs-lookup"><span data-stu-id="f26b0-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="f26b0-135">Требуемые свойства может устанавливаться только обратно решением hello end и может быть прочитан приложение hello устройства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="f26b0-136">приложение Hello устройства можно также получать уведомления в режиме реального времени изменения в hello требуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="f26b0-137">**Сообщаемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="f26b0-137">**Reported properties**.</span></span> <span data-ttu-id="f26b0-138">Используется вместе с нужными свойствами конфигурации устройства toosynchronize или условий.</span><span class="sxs-lookup"><span data-stu-id="f26b0-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="f26b0-139">Отчета свойства могут задаваться только приложение hello устройства и можно считывать и запрашивать hello решения серверной части.</span><span class="sxs-lookup"><span data-stu-id="f26b0-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="f26b0-140">Кроме того, корневой каталог hello устройства двойных hello JSON-документ содержит hello свойства только для чтения из удостоверения устройства соответствующие hello, хранящихся в hello [реестра удостоверений][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="f26b0-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="f26b0-141">Следующий пример Hello показано устройства двойных документа JSON.</span><span class="sxs-lookup"><span data-stu-id="f26b0-141">hello following example shows a device twin JSON document:</span></span>

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

<span data-ttu-id="f26b0-142">В корневой объект hello, являются системными свойствами hello и контейнер объектов для `tags` и `reported` и `desired` свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="f26b0-143">Hello `properties` контейнер содержит некоторые элементы, доступные только для чтения (`$metadata`, `$etag`, и `$version`) описано в hello [метаданные двойных устройства] [ lnk-twin-metadata] и [ Оптимистический параллелизм] [ lnk-concurrency] разделы.</span><span class="sxs-lookup"><span data-stu-id="f26b0-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="f26b0-144">Пример сообщаемых свойств</span><span class="sxs-lookup"><span data-stu-id="f26b0-144">Reported property example</span></span>
<span data-ttu-id="f26b0-145">В предыдущем примере hello содержит две устройства hello `batteryLevel` свойство, которое выдается приложение hello устройства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="f26b0-146">Это свойство позволяет возможных tooquery и работать на устройствах, в зависимости от последнего уровня отчета батареи hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="f26b0-147">Другие примеры отчетов возможности устройства hello устройства приложения или параметры подключения.</span><span class="sxs-lookup"><span data-stu-id="f26b0-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="f26b0-148">Свойства отчета упрощения сценариев, где серверной части решения hello интересует hello последнее известное значение свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="f26b0-149">Используйте [сообщения из устройства в облако] [ lnk-d2c] серверной части hello решения необходимо tooprocess устройства телеметрии в форме hello последовательностей событий отметку времени, таких как временных рядов.</span><span class="sxs-lookup"><span data-stu-id="f26b0-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="f26b0-150">Пример требуемого свойства</span><span class="sxs-lookup"><span data-stu-id="f26b0-150">Desired property example</span></span>
<span data-ttu-id="f26b0-151">В предыдущем примере hello hello `telemetryConfig` требуемого двойных устройства и выводятся свойства используются в серверной части решения hello и конфигурации телеметрии hello toosynchronize приложения hello устройства для этого устройства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="f26b0-152">Например:</span><span class="sxs-lookup"><span data-stu-id="f26b0-152">For example:</span></span>

1. <span data-ttu-id="f26b0-153">серверной части решения Hello присваивает свойству hello требуемого значения hello требуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f26b0-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="f26b0-154">Вот hello часть документа hello с набором hello требуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="f26b0-155">приложение Hello устройство получает уведомление hello изменения немедленно в том случае, если подключение или на hello сначала повторное подключение.</span><span class="sxs-lookup"><span data-stu-id="f26b0-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="f26b0-156">Hello приложения для устройств затем отчет hello обновления конфигурации (или об ошибке с помощью hello `status` свойство).</span><span class="sxs-lookup"><span data-stu-id="f26b0-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="f26b0-157">Вот часть hello hello сообщил свойства:</span><span class="sxs-lookup"><span data-stu-id="f26b0-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="f26b0-158">серверной части решения Hello можно отслеживать результаты hello hello конфигурации операции на множестве устройств по [запрос] [ lnk-query] близнецы устройства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="f26b0-159">Hello выше фрагменты являются примерами, оптимизированный для удобочитаемость, одним из способов tooencode конфигурации устройства и его состояние.</span><span class="sxs-lookup"><span data-stu-id="f26b0-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="f26b0-160">Центр IoT никак не определенной схеме для требуемого двойных устройства hello и которые сообщили свойства в устройство близнецы hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="f26b0-161">Можно использовать близнецы toosynchronize продолжительных операций, таких как обновления встроенного по.</span><span class="sxs-lookup"><span data-stu-id="f26b0-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="f26b0-162">Дополнительные сведения о статье toosynchronize свойства toouse и отслеживания продолжительной операции на устройствах, [используйте требуемого свойства устройства tooconfigure][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="f26b0-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="f26b0-163">Операции серверной части</span><span class="sxs-lookup"><span data-stu-id="f26b0-163">Back-end operations</span></span>
<span data-ttu-id="f26b0-164">серверной части решения Hello оперирует двойных устройства hello hello, следуя атомарных операций, доступных через HTTP с помощью:</span><span class="sxs-lookup"><span data-stu-id="f26b0-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="f26b0-165">**Получение двойника устройства по идентификатору.** Эта операция возвращает устройства двойных hello документ, в том числе теги и необходимо, в отчет и системные свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="f26b0-166">**Частичное обновление двойника устройства.**</span><span class="sxs-lookup"><span data-stu-id="f26b0-166">**Partially update device twin**.</span></span> <span data-ttu-id="f26b0-167">Эта операция включает hello hello решения серверной части toopartially обновления тегов или требуемые свойства в двойных устройства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="f26b0-168">Частичное обновление Hello выражается как документ JSON, который добавляет или обновляет любого свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="f26b0-169">Заданы слишком`null` удаляются.</span><span class="sxs-lookup"><span data-stu-id="f26b0-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="f26b0-170">Hello следующий пример создает новое нужного свойство со значением `{"newProperty": "newValue"}`, перезаписывает существующее значение hello объекта `existingProperty` с `"otherNewValue"`и удаляет `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="f26b0-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="f26b0-171">Другие изменения не вносятся tooexisting требуемого свойства или теги:</span><span class="sxs-lookup"><span data-stu-id="f26b0-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
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
3. <span data-ttu-id="f26b0-172">**Заменить требуемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="f26b0-172">**Replace desired properties**.</span></span> <span data-ttu-id="f26b0-173">Перезаписать все существующие нужные свойства этой операции включает hello решения серверной части toocompletely и замените документ JSON для `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="f26b0-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="f26b0-174">**Заменить теги**.</span><span class="sxs-lookup"><span data-stu-id="f26b0-174">**Replace tags**.</span></span> <span data-ttu-id="f26b0-175">Это операция включает hello решения серверной части toocompletely перезаписать все существующие теги и замените документ JSON для `tags`.</span><span class="sxs-lookup"><span data-stu-id="f26b0-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="f26b0-176">**Получение уведомлений двойника**.</span><span class="sxs-lookup"><span data-stu-id="f26b0-176">**Receive twin notifications**.</span></span> <span data-ttu-id="f26b0-177">Эта операция позволяет toobe серверной части решения hello, уведомления, когда изменяется двойных hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="f26b0-178">toodo таким образом, вашего решения IoT должен toocreate маршрута и равенства источника данных hello tooset слишком*twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="f26b0-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="f26b0-179">По умолчанию уведомления двойника не отправляются, то есть такие маршруты не существуют.</span><span class="sxs-lookup"><span data-stu-id="f26b0-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="f26b0-180">Если скорость изменения hello слишком велико или по другим причинам, например внутренними сбоями hello центра IoT может отправлять только одно уведомление, которая содержит все изменения.</span><span class="sxs-lookup"><span data-stu-id="f26b0-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="f26b0-181">Поэтому, если приложению требуется надежный аудит и ведение журнала всех промежуточных состояний, по-прежнему рекомендуется использовать сообщения, отправляемые с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="f26b0-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="f26b0-182">сообщение уведомления двойных Hello включает свойства и текст.</span><span class="sxs-lookup"><span data-stu-id="f26b0-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="f26b0-183">Свойства</span><span class="sxs-lookup"><span data-stu-id="f26b0-183">Properties</span></span>

    | <span data-ttu-id="f26b0-184">Имя</span><span class="sxs-lookup"><span data-stu-id="f26b0-184">Name</span></span> | <span data-ttu-id="f26b0-185">Значение</span><span class="sxs-lookup"><span data-stu-id="f26b0-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="f26b0-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="f26b0-186">$content-type</span></span> | <span data-ttu-id="f26b0-187">приложение/json</span><span class="sxs-lookup"><span data-stu-id="f26b0-187">application/json</span></span> |
    <span data-ttu-id="f26b0-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="f26b0-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="f26b0-189">Время отправки уведомлений hello</span><span class="sxs-lookup"><span data-stu-id="f26b0-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="f26b0-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="f26b0-190">$iothub-message-source</span></span> | <span data-ttu-id="f26b0-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="f26b0-191">twinChangeEvents</span></span> |
    <span data-ttu-id="f26b0-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="f26b0-192">$content-encoding</span></span> | <span data-ttu-id="f26b0-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="f26b0-193">utf-8</span></span> |
    <span data-ttu-id="f26b0-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="f26b0-194">deviceId</span></span> | <span data-ttu-id="f26b0-195">Идентификатор устройства hello</span><span class="sxs-lookup"><span data-stu-id="f26b0-195">Id of hello device</span></span> |
    <span data-ttu-id="f26b0-196">hubName</span><span class="sxs-lookup"><span data-stu-id="f26b0-196">hubName</span></span> | <span data-ttu-id="f26b0-197">Имя Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f26b0-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="f26b0-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="f26b0-198">operationTimestamp</span></span> | <span data-ttu-id="f26b0-199">Метка времени операции по стандарту [ISO8601]</span><span class="sxs-lookup"><span data-stu-id="f26b0-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="f26b0-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="f26b0-200">iothub-message-schema</span></span> | <span data-ttu-id="f26b0-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="f26b0-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="f26b0-202">opType</span><span class="sxs-lookup"><span data-stu-id="f26b0-202">opType</span></span> | <span data-ttu-id="f26b0-203">"replaceTwin" или "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="f26b0-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="f26b0-204">Системные свойства сообщения имеют префикс hello `'$'` символов.</span><span class="sxs-lookup"><span data-stu-id="f26b0-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="f26b0-205">Текст</span><span class="sxs-lookup"><span data-stu-id="f26b0-205">Body</span></span>
        
    <span data-ttu-id="f26b0-206">Этот раздел содержит все изменения двойных hello в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="f26b0-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="f26b0-207">Она использует hello в том же формате, что исправление, отличие hello что он может содержать все разделы двойных: теги, properties.reported, properties.desired и что он содержит элементы hello «$metadata».</span><span class="sxs-lookup"><span data-stu-id="f26b0-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="f26b0-208">Например,</span><span class="sxs-lookup"><span data-stu-id="f26b0-208">For example,</span></span>
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

<span data-ttu-id="f26b0-209">Все hello предыдущей операции поддержки [оптимистичного параллелизма] [ lnk-concurrency] и требуют hello **ServiceConnect** разрешения, как определено в hello [безопасности ] [ lnk-security] статьи.</span><span class="sxs-lookup"><span data-stu-id="f26b0-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="f26b0-210">В дополнение к этому toothese операций, решение hello резервные окончания может:</span><span class="sxs-lookup"><span data-stu-id="f26b0-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="f26b0-211">Запрос близнецы hello устройства, с помощью hello SQL-подобного [язык запросов центра IoT][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="f26b0-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="f26b0-212">выполнять операции с большими наборами двойников устройств с помощью [заданий][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="f26b0-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="f26b0-213">Операции с устройствами</span><span class="sxs-lookup"><span data-stu-id="f26b0-213">Device operations</span></span>
<span data-ttu-id="f26b0-214">приложение Hello устройство работает двойных устройства hello hello, следуя атомарных операций с помощью:</span><span class="sxs-lookup"><span data-stu-id="f26b0-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="f26b0-215">**Получение двойника устройства.**</span><span class="sxs-lookup"><span data-stu-id="f26b0-215">**Retrieve device twin**.</span></span> <span data-ttu-id="f26b0-216">Эта операция возвращает документ двойных hello устройства (в том числе теги и требуемого, отчет и системные свойства) для hello устройств, подключенных в данный момент.</span><span class="sxs-lookup"><span data-stu-id="f26b0-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="f26b0-217">**Частично обновить сообщаемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="f26b0-217">**Partially update reported properties**.</span></span> <span data-ttu-id="f26b0-218">Этой операции включает hello частичное обновление hello сообщил свойства hello подключенного устройства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="f26b0-219">Hello использует этой операции, обновление же JSON форматирования, hello решения задней использует для частичного обновления требуемых свойств.</span><span class="sxs-lookup"><span data-stu-id="f26b0-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="f26b0-220">**Отслеживать требуемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="f26b0-220">**Observe desired properties**.</span></span> <span data-ttu-id="f26b0-221">Hello в настоящее время подключенные устройства, которые можно выбрать toobe уведомления об обновлениях toohello требуемого свойства при их возникновении.</span><span class="sxs-lookup"><span data-stu-id="f26b0-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="f26b0-222">Hello получает hello же форме обновления (частично или полностью замена) исполнен hello решения серверной части.</span><span class="sxs-lookup"><span data-stu-id="f26b0-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="f26b0-223">Здравствуйте, всех предшествующих операций требуется hello **DeviceConnect** разрешения, как определено в hello [безопасности] [ lnk-security] статьи.</span><span class="sxs-lookup"><span data-stu-id="f26b0-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="f26b0-224">Hello [устройств Azure IoT SDK] [ lnk-sdks] сделать его легко toouse hello предыдущих операций из многих языках и платформах.</span><span class="sxs-lookup"><span data-stu-id="f26b0-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="f26b0-225">Дополнительные сведения о hello примитивов центр IoT для синхронизации с нужными свойствами можно найти в [потока повторного подключения устройства][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="f26b0-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="f26b0-226">В настоящее время устройство близнецы доступны только из устройств, которые подключаются tooIoT концентратора с помощью протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="f26b0-227">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="f26b0-227">Reference topics:</span></span>
<span data-ttu-id="f26b0-228">Hello следующие справочные разделы предоставляют дополнительные сведения о центра IoT tooyour управления доступом.</span><span class="sxs-lookup"><span data-stu-id="f26b0-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="f26b0-229">Формат тегов и свойств</span><span class="sxs-lookup"><span data-stu-id="f26b0-229">Tags and properties format</span></span>
<span data-ttu-id="f26b0-230">Теги, необходимые и выводятся свойства являются объектами JSON с hello следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="f26b0-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="f26b0-231">Все ключи в объектах JSON представляют собой 64-байтовые строки Юникода UTF-8 с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="f26b0-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="f26b0-232">Разрешено использовать все знаки, кроме управляющих символов Юникода (сегменты C0 и C1), а также `'.'`, `' '` и `'$'`.</span><span class="sxs-lookup"><span data-stu-id="f26b0-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="f26b0-233">Все значения в объектах JSON может иметь следующие типы JSON hello: логическое значение, число, строка, объект.</span><span class="sxs-lookup"><span data-stu-id="f26b0-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="f26b0-234">Запрещено использовать массивы.</span><span class="sxs-lookup"><span data-stu-id="f26b0-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="f26b0-235">Все объекты JSON в тегах, требуемых и сообщаемых свойствах могут иметь глубину не более 5.</span><span class="sxs-lookup"><span data-stu-id="f26b0-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="f26b0-236">Для экземпляра hello следующий объект является допустимым:</span><span class="sxs-lookup"><span data-stu-id="f26b0-236">For instance, hello following object is valid:</span></span>

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

* <span data-ttu-id="f26b0-237">Все строковые значения могут быть длиной не более 512 байт.</span><span class="sxs-lookup"><span data-stu-id="f26b0-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="f26b0-238">Размер двойника устройства</span><span class="sxs-lookup"><span data-stu-id="f26b0-238">Device twin size</span></span>
<span data-ttu-id="f26b0-239">Центр IoT применяет ограничение на размер 8 КБ значениям hello `tags`, `properties/desired`, и `properties/reported`, за исключением элементы, доступные только для чтения.</span><span class="sxs-lookup"><span data-stu-id="f26b0-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="f26b0-240">Hello размер вычисляется путем подсчета все символы, за исключением ЮНИКОДА управляющие символы (сегменты C0 и C1) и пространства `' '` при появлении за пределами строковая константа.</span><span class="sxs-lookup"><span data-stu-id="f26b0-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="f26b0-241">Центр IoT с ошибкой отклоняет все операции, которые увеличит размер hello эти документы выше ограничение hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="f26b0-242">Метаданные двойника устройства</span><span class="sxs-lookup"><span data-stu-id="f26b0-242">Device twin metadata</span></span>
<span data-ttu-id="f26b0-243">Центр IoT сохраняет отметки времени hello hello последнего обновления для каждого объекта JSON в устройстве двойных требуемого и данные свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="f26b0-244">Hello отметки времени в формате UTC и закодированы в hello [ISO8601] формат `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="f26b0-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="f26b0-245">Например:</span><span class="sxs-lookup"><span data-stu-id="f26b0-245">For example:</span></span>

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

<span data-ttu-id="f26b0-246">Эта информация хранится на каждого уровня обновления toopreserve (не только hello концевые hello структуры JSON), которые удалить ключи объекта.</span><span class="sxs-lookup"><span data-stu-id="f26b0-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="f26b0-247">Оптимистичный параллелизм</span><span class="sxs-lookup"><span data-stu-id="f26b0-247">Optimistic concurrency</span></span>
<span data-ttu-id="f26b0-248">Теги, а также требуемые и сообщаемые свойства поддерживают оптимистичный параллелизм.</span><span class="sxs-lookup"><span data-stu-id="f26b0-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="f26b0-249">Теги ETag, имеют согласно [RFC7232], представляющий тег hello JSON-представление.</span><span class="sxs-lookup"><span data-stu-id="f26b0-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="f26b0-250">Теги eTag можно использовать в операциях условного обновления из серверной части tooensure hello решения согласованности.</span><span class="sxs-lookup"><span data-stu-id="f26b0-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="f26b0-251">Устройство двойных требуемого и данные свойства не обладают теги eTag, но которым `$version` значение, которое гарантированно toobe добавочное.</span><span class="sxs-lookup"><span data-stu-id="f26b0-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="f26b0-252">Аналогичным образом можно использовать tooan ETag, версия hello hello обновление стороны tooenforce согласованности обновлений.</span><span class="sxs-lookup"><span data-stu-id="f26b0-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="f26b0-253">Например устройство приложения для отчета свойства или hello решения серверную часть для нужного свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="f26b0-254">Версии также полезны, когда агент наблюдения (например, наблюдая hello требуемого свойства приложения для устройств hello) необходимо согласовать состязания между hello результат операции извлечения и уведомление об обновлении.</span><span class="sxs-lookup"><span data-stu-id="f26b0-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="f26b0-255">Здравствуйте, раздел [потока повторного подключения устройства] [ lnk-reconnection] предоставляет дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="f26b0-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="f26b0-256">Процедура при повторном подключении устройства</span><span class="sxs-lookup"><span data-stu-id="f26b0-256">Device reconnection flow</span></span>
<span data-ttu-id="f26b0-257">Центр Интернета вещей не сохраняет уведомления об обновлении требуемых свойств для отключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="f26b0-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="f26b0-258">Следует, что устройство, которое подключается необходимо получить полный нужными свойствами документе hello в toosubscribing сложения для уведомления об обновлениях.</span><span class="sxs-lookup"><span data-stu-id="f26b0-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="f26b0-259">Имея возможность состязания между уведомления об обновлениях, а также полный поиск hello, hello последовательности должна быть гарантирована:</span><span class="sxs-lookup"><span data-stu-id="f26b0-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="f26b0-260">Приложения для устройств подключается tooan центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f26b0-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="f26b0-261">Приложение устройства подписывается на уведомления об обновлениях требуемых свойств.</span><span class="sxs-lookup"><span data-stu-id="f26b0-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="f26b0-262">Приложения для устройств получает полный документ hello для нужного свойства.</span><span class="sxs-lookup"><span data-stu-id="f26b0-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="f26b0-263">приложение Hello устройства можно пропустить все уведомления с `$version` меньше или равно, чем версия hello полного документа полученные hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="f26b0-264">Такой подход возможен, так как Центр Интернета вещей гарантирует постоянное увеличение версий.</span><span class="sxs-lookup"><span data-stu-id="f26b0-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="f26b0-265">Эта логика уже реализован в hello [устройств Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="f26b0-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="f26b0-266">Это описание полезно только в том случае, если приложение hello устройство нельзя использовать никакие устройств Azure IoT SDK и необходимо запрограммировать hello MQTT интерфейса напрямую.</span><span class="sxs-lookup"><span data-stu-id="f26b0-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="f26b0-267">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="f26b0-267">Additional reference material</span></span>
<span data-ttu-id="f26b0-268">Другие разделы ссылку в hello центра IoT руководстве для разработчиков:</span><span class="sxs-lookup"><span data-stu-id="f26b0-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="f26b0-269">Hello [конечные точки центра IoT] [ lnk-endpoints] статье hello различные конечные точки, предоставляемые каждый центр IoT для операций времени выполнения и управления.</span><span class="sxs-lookup"><span data-stu-id="f26b0-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="f26b0-270">Hello [регулирование и квоты] [ lnk-quotas] статье hello квот, применяемые toohello службы центр IoT и hello регулирования tooexpect поведение при использовании службы hello.</span><span class="sxs-lookup"><span data-stu-id="f26b0-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="f26b0-271">Hello [пакетов SDK устройств и служб Azure IoT] [ lnk-sdks] статье списки hello различных пакетов SDK для языка, можно использовать при разработке приложений, устройств и служб, которые взаимодействуют с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="f26b0-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="f26b0-272">Hello [центр IoT язык запросов для близнецы устройства, задания и маршрутизация сообщений] [ lnk-query] статье hello tooretrieve сведения из центра IoT близнецы устройства и заданий можно использовать язык запросов центра IoT .</span><span class="sxs-lookup"><span data-stu-id="f26b0-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="f26b0-273">Hello [поддержки MQTT концентратора IoT] [ lnk-devguide-mqtt] статье приведены дополнительные сведения о поддержке протокола MQTT hello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f26b0-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f26b0-274">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f26b0-274">Next steps</span></span>
<span data-ttu-id="f26b0-275">Теперь вы узнали о близнецы устройства, можно получить в следующие разделы руководства разработчика центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="f26b0-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="f26b0-276">[Вызов прямого метода на устройстве (предварительная версия)][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="f26b0-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="f26b0-277">[Schedule jobs on multiple devices][lnk-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="f26b0-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="f26b0-278">При желании tootry некоторые основные понятия hello, описанных в этой статье, могут быть интересны следующие учебники центра IoT hello параметры:</span><span class="sxs-lookup"><span data-stu-id="f26b0-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="f26b0-279">[Как toouse hello двойных устройства][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f26b0-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="f26b0-280">[Как свойства двойных toouse устройства][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="f26b0-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

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
