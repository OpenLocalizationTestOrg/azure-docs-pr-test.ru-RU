---
title: "aaaDevice сведения метаданных в hello удаленное наблюдение решения | Документы Microsoft"
description: "Описание удаленный мониторинг hello Azure IoT предварительно настроенное решение и его архитектуры."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="53861-103">Устройство сведения метаданных в удаленное наблюдение предварительно настроенных решений hello</span><span class="sxs-lookup"><span data-stu-id="53861-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="53861-104">Hello Azure IoT Suite удаленное наблюдение предварительно настроенных решений показано подход, управление метаданными устройства.</span><span class="sxs-lookup"><span data-stu-id="53861-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="53861-105">В этой статье рассматриваются подход hello это решение принимает tooenable toounderstand вы:</span><span class="sxs-lookup"><span data-stu-id="53861-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="53861-106">Сохраняет какие hello метаданных устройствами.</span><span class="sxs-lookup"><span data-stu-id="53861-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="53861-107">Как решение hello управляет метаданными hello устройства.</span><span class="sxs-lookup"><span data-stu-id="53861-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="53861-108">Context</span><span class="sxs-lookup"><span data-stu-id="53861-108">Context</span></span>

<span data-ttu-id="53861-109">Hello удаленный мониторинг предварительно настроенное решение использует [центр IoT Azure] [ lnk-iot-hub] tooenable облако toohello данных toosend вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="53861-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="53861-110">решение Hello хранит сведения об устройствах в трех разных местах:</span><span class="sxs-lookup"><span data-stu-id="53861-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="53861-111">Расположение</span><span class="sxs-lookup"><span data-stu-id="53861-111">Location</span></span> | <span data-ttu-id="53861-112">Сохраненные сведения</span><span class="sxs-lookup"><span data-stu-id="53861-112">Information stored</span></span> | <span data-ttu-id="53861-113">Реализация</span><span class="sxs-lookup"><span data-stu-id="53861-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="53861-114">Реестр удостоверений</span><span class="sxs-lookup"><span data-stu-id="53861-114">Identity registry</span></span> | <span data-ttu-id="53861-115">Идентификатор устройства, ключи проверки подлинности, включенное состояние</span><span class="sxs-lookup"><span data-stu-id="53861-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="53861-116">Встроенная tooIoT концентратора</span><span class="sxs-lookup"><span data-stu-id="53861-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="53861-117">Двойники устройства</span><span class="sxs-lookup"><span data-stu-id="53861-117">Device twins</span></span> | <span data-ttu-id="53861-118">Метаданные: сообщаемые свойства, требуемые свойства, теги</span><span class="sxs-lookup"><span data-stu-id="53861-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="53861-119">Встроенная tooIoT концентратора</span><span class="sxs-lookup"><span data-stu-id="53861-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="53861-120">База данных Cosmos</span><span class="sxs-lookup"><span data-stu-id="53861-120">Cosmos DB</span></span> | <span data-ttu-id="53861-121">Журнал методов и команд</span><span class="sxs-lookup"><span data-stu-id="53861-121">Command and method history</span></span> | <span data-ttu-id="53861-122">Специальная для каждого решения</span><span class="sxs-lookup"><span data-stu-id="53861-122">Custom for solution</span></span> |

<span data-ttu-id="53861-123">Включает центр IoT [реестре удостоверений устройств] [ lnk-identity-registry] toomanage доступа центра IoT tooan и использует [близнецы устройства] [ lnk-device-twin] toomanage метаданные устройства .</span><span class="sxs-lookup"><span data-stu-id="53861-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="53861-124">В центре также есть *реестр устройств* для удаленного мониторинга каждого решения. В этом реестре хранится журнал методов и команд.</span><span class="sxs-lookup"><span data-stu-id="53861-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="53861-125">удаленный мониторинг решение использует Hello [Cosmos DB] [ lnk-docdb] базы данных tooimplement настраиваемое хранилище для журнала команд и метод.</span><span class="sxs-lookup"><span data-stu-id="53861-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="53861-126">Hello удаленное наблюдение предварительно настроенных решений сохраняет реестре удостоверений устройств hello в соответствии с hello сведения в базе данных Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="53861-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="53861-127">Используют hello же toouniquely идентификатор устройства идентификации каждого устройство подключено tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="53861-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="53861-128">Метаданные устройства</span><span class="sxs-lookup"><span data-stu-id="53861-128">Device metadata</span></span>

<span data-ttu-id="53861-129">Центр IoT поддерживает [двойных устройства] [ lnk-device-twin] каждого имитацию и физического устройства, подключенного tooa удаленного решением для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="53861-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="53861-130">Hello решение использует устройство близнецы toomanage hello метаданные, связанные с устройствами.</span><span class="sxs-lookup"><span data-stu-id="53861-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="53861-131">Двойных устройства является документ JSON, обслуживается центр IoT и hello решение использует интерфейс API концентратора IoT toointeract hello с близнецы устройства.</span><span class="sxs-lookup"><span data-stu-id="53861-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="53861-132">Двойник устройства содержит три типа метаданных.</span><span class="sxs-lookup"><span data-stu-id="53861-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="53861-133">*Отчет свойства* отправляются центра IoT tooan устройством.</span><span class="sxs-lookup"><span data-stu-id="53861-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="53861-134">В удаленных решением для мониторинга hello, смоделированные устройства отправляют свойства отчета при запуске и в ответ слишком**изменение состояния устройства** команды и методы.</span><span class="sxs-lookup"><span data-stu-id="53861-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="53861-135">Можно просмотреть свойства отчета в hello **список устройств** и **сведений об устройстве** hello решение портала.</span><span class="sxs-lookup"><span data-stu-id="53861-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="53861-136">Сообщаемые свойства доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="53861-136">Reported properties are read only.</span></span>
- <span data-ttu-id="53861-137">*Требуемого свойства* извлекаются из центра IoT hello на устройствах.</span><span class="sxs-lookup"><span data-stu-id="53861-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="53861-138">Он несет hello hello устройства toomake изменить какой-либо необходимые настройки на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="53861-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="53861-139">Также hello обязанностью является hello устройства tooreport hello изменений назад toohello концентратора как свойство отчета.</span><span class="sxs-lookup"><span data-stu-id="53861-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="53861-140">Можно задать значение нужного свойства через портал hello решения.</span><span class="sxs-lookup"><span data-stu-id="53861-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="53861-141">*Теги* существуют только в двойных устройства hello и никогда не синхронизированы с устройством.</span><span class="sxs-lookup"><span data-stu-id="53861-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="53861-142">Можно задать значения тега hello решение портала и использовать их при фильтрации hello список устройств.</span><span class="sxs-lookup"><span data-stu-id="53861-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="53861-143">решение Hello также использует toodisplay значок тега hello tooidentify для устройства на портале решения hello.</span><span class="sxs-lookup"><span data-stu-id="53861-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="53861-144">Пример сообщила, что свойства из hello имитируемые устройства включают производителя и номер модели, широту и долготу.</span><span class="sxs-lookup"><span data-stu-id="53861-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="53861-145">Имитация устройств также возвращать hello список поддерживаемых методов как свойство отчета.</span><span class="sxs-lookup"><span data-stu-id="53861-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="53861-146">Hello имитированное устройство код использует только hello **Desired.Config.TemperatureMeanValue** и **Desired.Config.TelemetryInterval** hello tooupdate нужными свойствами сообщил отправил обратно свойства tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="53861-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="53861-147">Все прочие запросы на изменение требуемых свойств игнорируются.</span><span class="sxs-lookup"><span data-stu-id="53861-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="53861-148">Метаданные JSON устройства сведения документа, хранящегося в системный реестр Cosmos DB hello устройство имеет hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="53861-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="53861-149">Сведения об устройстве можно также включить метаданные toodescribe hello телеметрии hello устройство отправляет tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="53861-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="53861-150">решение для удаленного мониторинга Hello использует этот toocustomize телеметрии метаданных, как панель мониторинга hello отображает [динамического телеметрии][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="53861-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="53861-151">Жизненный цикл</span><span class="sxs-lookup"><span data-stu-id="53861-151">Lifecycle</span></span>

<span data-ttu-id="53861-152">При создании устройства на портале решения hello, hello решение создает запись в hello команда toostore Cosmos DB базы данных и журнала метод.</span><span class="sxs-lookup"><span data-stu-id="53861-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="53861-153">На этом этапе hello решения также создает запись для устройства hello в реестре удостоверений устройств hello, создающий hello ключи hello устройство использует tooauthenticate с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="53861-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="53861-154">Оно также создает двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="53861-154">It also creates a device twin.</span></span>

<span data-ttu-id="53861-155">Устройства сначала подключается toohello решения, отправляет свойства отчета и сообщение сведения устройства.</span><span class="sxs-lookup"><span data-stu-id="53861-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="53861-156">Hello сообщила, что значения свойств автоматически сохраняются в двойных hello устройства.</span><span class="sxs-lookup"><span data-stu-id="53861-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="53861-157">Hello сообщила, что свойства включают hello изготовителя устройства, номер модели, серийный номер и список поддерживаемых методов.</span><span class="sxs-lookup"><span data-stu-id="53861-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="53861-158">Информационное сообщение Hello устройств включает список hello hello команды, которые поддерживает устройство hello, включая данные о любые параметры.</span><span class="sxs-lookup"><span data-stu-id="53861-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="53861-159">Когда hello решение получает это сообщение, он обновляет hello сведений об устройстве в базе данных Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="53861-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="53861-160">Просмотр и редактирование сведений об устройстве в портале решения hello</span><span class="sxs-lookup"><span data-stu-id="53861-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="53861-161">Hello список устройств на портале решения hello отображаются следующие свойства устройства как столбцы по умолчанию hello: **состояние**, **DeviceId**, **производителя**, **Номер модели**, **серийный номер**, **встроенного по**, **платформы**, **процессора**и  **Установлено ОЗУ**.</span><span class="sxs-lookup"><span data-stu-id="53861-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="53861-162">Можно выбрать столбцы hello, щелкнув **редактор столбец**.</span><span class="sxs-lookup"><span data-stu-id="53861-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="53861-163">Здравствуйте, свойства устройства **широты** и **долготы** диск расположение hello в hello карты Bing на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="53861-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![Редактор столбцов в списке устройств][img-device-list]

<span data-ttu-id="53861-165">В hello **сведений об устройстве** области портала hello решения можно изменять нужными свойствами и теги (предупреждение свойства доступны только для чтения).</span><span class="sxs-lookup"><span data-stu-id="53861-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Область "Сведения устройства"][img-device-edit]

<span data-ttu-id="53861-167">Hello решение портала tooremove устройства можно использовать из решения.</span><span class="sxs-lookup"><span data-stu-id="53861-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="53861-168">При удалении устройства решения hello удаляет запись устройства hello из реестра удостоверений, а затем удаляет двойных hello устройства.</span><span class="sxs-lookup"><span data-stu-id="53861-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="53861-169">решение Hello также удаляет устройство toohello связанные сведения из базы данных Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="53861-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="53861-170">Перед удалением устройства его необходимо отключить.</span><span class="sxs-lookup"><span data-stu-id="53861-170">Before you can remove a device, you must disable it.</span></span>

![Удаление устройства][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="53861-172">Обработка сообщений со сведениями об устройстве</span><span class="sxs-lookup"><span data-stu-id="53861-172">Device information message processing</span></span>

<span data-ttu-id="53861-173">Сообщения со сведениями об устройстве, отправляемые устройством, отличаются от сообщений телеметрии.</span><span class="sxs-lookup"><span data-stu-id="53861-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="53861-174">Устройство сведения сообщения включают устройство может реагировать на команды hello и любые журнала команд.</span><span class="sxs-lookup"><span data-stu-id="53861-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="53861-175">Центр IoT сам не имеет сведений о hello метаданные, содержащиеся в сообщении сведения устройств и процессов hello сообщение hello так же, как он обрабатывает все сообщения устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="53861-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="53861-176">В удаленное наблюдение решения, hello [Azure Stream Analytics] [ lnk-stream-analytics] задания (ASA) считывает сообщения hello из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="53861-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="53861-177">Hello **DeviceInfo** фильтры для сообщений, которые содержат задания stream analytics **«ObjectType»: «DeviceInfo»** и пересылает их toohello **EventProcessorHost** узла экземпляр, который выполняется в веб-задание.</span><span class="sxs-lookup"><span data-stu-id="53861-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="53861-178">Логика в hello **EventProcessorHost** экземпляр использует запись Cosmos DB hello toofind идентификатор hello устройства hello определенной устройства и обновления записи hello.</span><span class="sxs-lookup"><span data-stu-id="53861-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="53861-179">Сообщение со сведениями об устройстве — это стандартное сообщение, отправляемое с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="53861-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="53861-180">решение Hello отличия между устройства информационные сообщения и сообщения телеметрии с помощью ASA запросов.</span><span class="sxs-lookup"><span data-stu-id="53861-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53861-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53861-181">Next steps</span></span>

<span data-ttu-id="53861-182">После завершения обучения, как можно настроить hello предварительно настроенных решений можно изучить некоторые hello и другие возможности hello IoT Suite предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="53861-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="53861-183">[Обзор предварительно настроенного решения прогнозируемого обслуживания][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="53861-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="53861-184">[Часто задаваемые вопросы об IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="53861-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="53861-185">[Основание безопасности IoT из hello,][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="53861-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
