---
title: "Метаданные сведений об устройстве в решении для удаленного мониторинга | Документация Майкрософт"
description: "Описание предварительно настроенного решения удаленного мониторинга Azure IoT и его архитектура."
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
ms.openlocfilehash: f8fd452806a0a0b98cf8e434c9bd55700083a6c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="45522-103">Метаданные сведений об устройстве в предварительно настроенном решении для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="45522-103">Device information metadata in the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="45522-104">В предварительно настроенном решении для удаленного мониторинга Azure IoT Suite демонстрируется, как управлять метаданными устройства.</span><span class="sxs-lookup"><span data-stu-id="45522-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="45522-105">В этой статье описан подход, применяемый в этом решении. Он позволяет понять следующее:</span><span class="sxs-lookup"><span data-stu-id="45522-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="45522-106">какие метаданные устройства хранятся в решении;</span><span class="sxs-lookup"><span data-stu-id="45522-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="45522-107">как решение управляет метаданными устройства.</span><span class="sxs-lookup"><span data-stu-id="45522-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="45522-108">Context</span><span class="sxs-lookup"><span data-stu-id="45522-108">Context</span></span>

<span data-ttu-id="45522-109">Предварительно настроенное решение для удаленного мониторинга использует [Центр Интернета вещей Azure][lnk-iot-hub], чтобы позволить устройствам отправлять данные в облако.</span><span class="sxs-lookup"><span data-stu-id="45522-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="45522-110">Решение сохраняет сведения об устройствах в трех разных местах.</span><span class="sxs-lookup"><span data-stu-id="45522-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="45522-111">Расположение</span><span class="sxs-lookup"><span data-stu-id="45522-111">Location</span></span> | <span data-ttu-id="45522-112">Сохраненные сведения</span><span class="sxs-lookup"><span data-stu-id="45522-112">Information stored</span></span> | <span data-ttu-id="45522-113">Реализация</span><span class="sxs-lookup"><span data-stu-id="45522-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="45522-114">Реестр удостоверений</span><span class="sxs-lookup"><span data-stu-id="45522-114">Identity registry</span></span> | <span data-ttu-id="45522-115">Идентификатор устройства, ключи проверки подлинности, включенное состояние</span><span class="sxs-lookup"><span data-stu-id="45522-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="45522-116">Встроены в центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="45522-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="45522-117">Двойники устройства</span><span class="sxs-lookup"><span data-stu-id="45522-117">Device twins</span></span> | <span data-ttu-id="45522-118">Метаданные: сообщаемые свойства, требуемые свойства, теги</span><span class="sxs-lookup"><span data-stu-id="45522-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="45522-119">Встроены в центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="45522-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="45522-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="45522-120">Cosmos DB</span></span> | <span data-ttu-id="45522-121">Журнал методов и команд</span><span class="sxs-lookup"><span data-stu-id="45522-121">Command and method history</span></span> | <span data-ttu-id="45522-122">Специальная для каждого решения</span><span class="sxs-lookup"><span data-stu-id="45522-122">Custom for solution</span></span> |

<span data-ttu-id="45522-123">Центр Интернета вещей содержит [реестр удостоверений устройств][lnk-identity-registry] для управления доступом к центру Интернета вещей и управления метаданными устройства с помощью [двойников устройства][lnk-device-twin].</span><span class="sxs-lookup"><span data-stu-id="45522-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="45522-124">В центре также есть *реестр устройств* для удаленного мониторинга каждого решения. В этом реестре хранится журнал методов и команд.</span><span class="sxs-lookup"><span data-stu-id="45522-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="45522-125">Решение для удаленного мониторинга использует базу данных [Cosmos DB][lnk-docdb] для реализации специального хранилища журнала методов и команд.</span><span class="sxs-lookup"><span data-stu-id="45522-125">The remote monitoring solution uses a [Cosmos DB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="45522-126">Предварительно настроенное решение для удаленного мониторинга обеспечивает синхронизацию реестра удостоверений устройств и сведений в базе данных Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="45522-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the Cosmos DB database.</span></span> <span data-ttu-id="45522-127">И в том, и в другом используется один и тот же идентификатор устройства для уникальной идентификации каждого устройства, подключенного к центру IoT.</span><span class="sxs-lookup"><span data-stu-id="45522-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="45522-128">Метаданные устройства</span><span class="sxs-lookup"><span data-stu-id="45522-128">Device metadata</span></span>

<span data-ttu-id="45522-129">Центр Интернета вещей поддерживает [двойники устройств][lnk-device-twin] для каждого имитируемого и физического устройства, подключенного к решению удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="45522-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="45522-130">Решение использует двойники устройств для управления метаданными, связанными с устройствами.</span><span class="sxs-lookup"><span data-stu-id="45522-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="45522-131">Двойник устройства — это документ JSON, поддерживаемый центром Интернета вещей. Решение использует API центра Интернета вещей для взаимодействия с двойниками устройств.</span><span class="sxs-lookup"><span data-stu-id="45522-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="45522-132">Двойник устройства содержит три типа метаданных.</span><span class="sxs-lookup"><span data-stu-id="45522-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="45522-133">*Сообщаемые свойства* отправляются устройством в центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="45522-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="45522-134">В решении удаленного мониторинга имитируемые устройства отправляют сообщаемые свойства при запуске в ответ на команды и методы **изменения состояния устройства**.</span><span class="sxs-lookup"><span data-stu-id="45522-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="45522-135">Вы можете просмотреть сообщаемые свойства в **списке устройств** и **сведениях устройства** на портале решения.</span><span class="sxs-lookup"><span data-stu-id="45522-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="45522-136">Сообщаемые свойства доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="45522-136">Reported properties are read only.</span></span>
- <span data-ttu-id="45522-137">Устройства извлекают *нужные свойства* из центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="45522-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="45522-138">Необходимые изменения конфигурации устройства выполняет само устройство.</span><span class="sxs-lookup"><span data-stu-id="45522-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="45522-139">Устройство также должно сообщить центру о внесенных изменениях, отправив сообщаемые свойства.</span><span class="sxs-lookup"><span data-stu-id="45522-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="45522-140">Вы можете задать нужное значение свойства на портале решения.</span><span class="sxs-lookup"><span data-stu-id="45522-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="45522-141">*Теги* существуют только в двойниках устройств и никогда не синхронизируются с устройством.</span><span class="sxs-lookup"><span data-stu-id="45522-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="45522-142">Вы можете указать значения тегов на портале решения и использовать их для фильтрации списка устройств.</span><span class="sxs-lookup"><span data-stu-id="45522-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="45522-143">Решение также использует тег, чтобы определить, какой значок отображать для устройства на портале решения.</span><span class="sxs-lookup"><span data-stu-id="45522-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="45522-144">Пример сообщаемых свойств с имитируемого устройства включает производителя, номер модели, широту и долготу.</span><span class="sxs-lookup"><span data-stu-id="45522-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="45522-145">Имитируемые устройства также отправляют в сообщаемых свойствах список поддерживаемых методов.</span><span class="sxs-lookup"><span data-stu-id="45522-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="45522-146">Код имитируемого устройства использует только требуемые свойства **Desired.Config.TemperatureMeanValue** и **Desired.Config.TelemetryInterval**, чтобы обновить сообщаемые свойства, отправляемые в центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="45522-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="45522-147">Все прочие запросы на изменение требуемых свойств игнорируются.</span><span class="sxs-lookup"><span data-stu-id="45522-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="45522-148">Ниже представлена структура документа JSON с метаданными сведений об устройстве, хранящегося в базе данных Cosmos DB в реестре устройств:</span><span class="sxs-lookup"><span data-stu-id="45522-148">A device information metadata JSON document stored in the device registry Cosmos DB database has the following structure:</span></span>

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
> <span data-ttu-id="45522-149">Сведения об устройстве могут также включать метаданные, описывающие данные телеметрии, которые устройство отправляет в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="45522-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="45522-150">Решение для удаленного мониторинга использует эти метаданные телеметрии, чтобы настроить отображение [динамической телеметрии][lnk-dynamic-telemetry] на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="45522-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="45522-151">Жизненный цикл</span><span class="sxs-lookup"><span data-stu-id="45522-151">Lifecycle</span></span>

<span data-ttu-id="45522-152">Когда вы создаете устройство на портале решения, решение создает запись в базе данных Cosmos DB для хранения журнала методов команд.</span><span class="sxs-lookup"><span data-stu-id="45522-152">When you first create a device in the solution portal, the solution creates an entry in the Cosmos DB database to store command and method history.</span></span> <span data-ttu-id="45522-153">На этом этапе решение также формирует запись для устройства в реестре удостоверений устройств, которая создает ключи. Устройство использует их для аутентификации в центре IoT.</span><span class="sxs-lookup"><span data-stu-id="45522-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="45522-154">Оно также создает двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="45522-154">It also creates a device twin.</span></span>

<span data-ttu-id="45522-155">При первом подключении к решению устройство отправляет сообщаемые свойства и свои сведения.</span><span class="sxs-lookup"><span data-stu-id="45522-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="45522-156">Значения сообщаемых свойств автоматически сохраняются в двойниках устройств.</span><span class="sxs-lookup"><span data-stu-id="45522-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="45522-157">Сообщаемые свойства включают изготовителя устройства, номер модели, серийный номер и список поддерживаемых методов.</span><span class="sxs-lookup"><span data-stu-id="45522-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="45522-158">Кроме того, сообщение со сведениями устройства содержит список команд, которые поддерживает устройство, а также сведения о всех параметрах этих команд.</span><span class="sxs-lookup"><span data-stu-id="45522-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="45522-159">При получении этого сообщения решение обновляет в базе данных Cosmos DB сведения об устройстве.</span><span class="sxs-lookup"><span data-stu-id="45522-159">When the solution receives this message, it updates the device information in the Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="45522-160">Просмотр и изменение сведений об устройстве на портале решения</span><span class="sxs-lookup"><span data-stu-id="45522-160">View and edit device information in the solution portal</span></span>

<span data-ttu-id="45522-161">В списке устройств на портале решения по умолчанию отображаются следующие свойства устройства в виде столбцов: **Состояние**, **Идентификатор устройства**, **Производитель**, **Номер модели**, **Серийный номер**, **Встроенное ПО**, **Платформа**, **Процессор** и **Установлено ОЗУ**.</span><span class="sxs-lookup"><span data-stu-id="45522-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="45522-162">Вы можете настроить столбцы, щелкнув **редактор столбцов**.</span><span class="sxs-lookup"><span data-stu-id="45522-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="45522-163">Такие свойства устройства, как **Широта** и **Долгота**, управляют расположением на карте Bing на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="45522-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![Редактор столбцов в списке устройств][img-device-list]

<span data-ttu-id="45522-165">В области **Сведения устройства** на портале решения можно изменить требуемые свойства и теги (сообщаемые свойства доступны только для чтения).</span><span class="sxs-lookup"><span data-stu-id="45522-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Область "Сведения устройства"][img-device-edit]

<span data-ttu-id="45522-167">На портале решения можно удалить устройство из решения.</span><span class="sxs-lookup"><span data-stu-id="45522-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="45522-168">Когда вы удаляете устройство, решение удаляет запись устройства из реестра удостоверений, а затем удаляет двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="45522-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="45522-169">Решение также удаляет из базы данных Cosmos DB сведения, связанные с устройством.</span><span class="sxs-lookup"><span data-stu-id="45522-169">The solution also removes information related to the device from the Cosmos DB database.</span></span> <span data-ttu-id="45522-170">Перед удалением устройства его необходимо отключить.</span><span class="sxs-lookup"><span data-stu-id="45522-170">Before you can remove a device, you must disable it.</span></span>

![Удаление устройства][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="45522-172">Обработка сообщений со сведениями об устройстве</span><span class="sxs-lookup"><span data-stu-id="45522-172">Device information message processing</span></span>

<span data-ttu-id="45522-173">Сообщения со сведениями об устройстве, отправляемые устройством, отличаются от сообщений телеметрии.</span><span class="sxs-lookup"><span data-stu-id="45522-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="45522-174">Сообщения со сведениями об устройстве содержат команды, на которые может реагировать устройство, и журнал команд.</span><span class="sxs-lookup"><span data-stu-id="45522-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="45522-175">В центре IoT отсутствуют сведения о метаданных в сообщении со сведениями об устройстве. Он обрабатывает такое сообщение так же, как и все сообщения, отправляемые с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="45522-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="45522-176">В решении для удаленного мониторинга задание [Azure Stream Analytics][lnk-stream-analytics] (ASA) считывает сообщения из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="45522-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="45522-177">Задание **DeviceInfo** Stream Analytics отфильтровывает сообщения, содержащие фрагмент кода **"ObjectType": "DeviceInfo"**, и пересылает их экземпляру узла **EventProcessorHost**, выполняющемуся в веб-задании.</span><span class="sxs-lookup"><span data-stu-id="45522-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="45522-178">Логика в экземпляре **EventProcessorHost** использует идентификатор устройства, чтобы найти запись Cosmos DB для конкретного устройства и обновить ее.</span><span class="sxs-lookup"><span data-stu-id="45522-178">Logic in the **EventProcessorHost** instance uses the device id to find the Cosmos DB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="45522-179">Сообщение со сведениями об устройстве — это стандартное сообщение, отправляемое с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="45522-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="45522-180">Решение различает сообщения со сведениями об устройстве и сообщения с телеметрией с помощью запросов ASA.</span><span class="sxs-lookup"><span data-stu-id="45522-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45522-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45522-181">Next steps</span></span>

<span data-ttu-id="45522-182">Теперь когда вы знаете, как менять параметры предварительно настроенных решений IoT Suite, можете ознакомиться с другими функциями и возможностями таких решений:</span><span class="sxs-lookup"><span data-stu-id="45522-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="45522-183">[Обзор предварительно настроенного решения прогнозируемого обслуживания][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="45522-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="45522-184">[Часто задаваемые вопросы об IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="45522-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="45522-185">[Все аспекты безопасности Интернета вещей][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="45522-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

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
