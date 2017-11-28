---
title: "Общие сведения об отправке файлов в Центре Интернета вещей Azure | Документация Майкрософт"
description: "Руководство разработчика. Воспользуйтесь функцией отправки файлов в Центре Интернета вещей для управления передачей файлов с устройства в контейнер больших двоичных объектов службы хранилища Azure."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="cc76e-103">Отправка файлов с помощью Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="cc76e-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="cc76e-104">Как описано в статье о [конечных точках Центра Интернета вещей][lnk-endpoints], устройства могут инициировать передачу файлов путем отправки уведомления через конечную точку, доступную для устройства (**/devices/{deviceId}/files**).</span><span class="sxs-lookup"><span data-stu-id="cc76e-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="cc76e-105">Когда устройство уведомляет Центр Интернета вещей о завершении отправки, Центр Интернета вещей отправляет сообщение уведомления о передаче файлов через конечную точку, доступную для службы (**/messages/servicebound/filenotifications**).</span><span class="sxs-lookup"><span data-stu-id="cc76e-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="cc76e-106">Вместо функций брокера сообщений Центр Интернета вещей выполняет роль диспетчера для связанной учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="cc76e-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="cc76e-107">Устройство запрашивает из Центра Интернета вещей маркер хранилища, относящийся к файлу, который должно отправить устройство.</span><span class="sxs-lookup"><span data-stu-id="cc76e-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="cc76e-108">Для отправки файла в хранилище устройство использует код URI SAS, а по завершении загрузки отправляет соответствующее уведомление в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cc76e-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="cc76e-109">Центр Интернета вещей проверяет, завершена ли отправка файлов, а затем добавляет сообщение уведомления о передаче файлов в конечную точку уведомления о файлах, доступную для службы.</span><span class="sxs-lookup"><span data-stu-id="cc76e-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="cc76e-110">Перед отправкой файла в Центр Интернета вещей с устройства необходимо настроить центр, [связав учетную запись хранения Azure][lnk-associate-storage] с ним.</span><span class="sxs-lookup"><span data-stu-id="cc76e-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="cc76e-111">После этого устройство сможет [инициализировать отправку][lnk-initialize] и [уведомить Центр Интернета вещей][lnk-notify] о завершении передачи.</span><span class="sxs-lookup"><span data-stu-id="cc76e-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="cc76e-112">Служба может дополнительно создавать [ уведомительные сообщения][lnk-service-notification], когда устройство будет уведомлять Центр Интернета вещей о завершении передачи.</span><span class="sxs-lookup"><span data-stu-id="cc76e-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="cc76e-113">Сценарии использования</span><span class="sxs-lookup"><span data-stu-id="cc76e-113">When to use</span></span>

<span data-ttu-id="cc76e-114">Передача файлов используется для отправки файлов мультимедиа и больших пакетов телеметрии, передаваемых периодически подключаемыми устройствами или сжатых для экономии пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="cc76e-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="cc76e-115">Дополнительные сведения см. в [руководстве по обмену данными, отправляемыми с устройства в облако][lnk-d2c-guidance], если сомневаетесь между использованием сообщаемых свойств, сообщений, отправляемых с устройства в облако, или передачей файла.</span><span class="sxs-lookup"><span data-stu-id="cc76e-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="cc76e-116">Связывание учетной записи хранения Azure с Центром Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="cc76e-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="cc76e-117">Чтобы использовать функции отправки файлов, сначала необходимо связать учетную запись хранения Azure с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cc76e-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="cc76e-118">Это можно сделать на [портале Azure][lnk-management-portal] или программно (с помощью [интерфейсов REST API поставщика ресурсов Центра Интернета вещей][lnk-resource-provider-apis]).</span><span class="sxs-lookup"><span data-stu-id="cc76e-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="cc76e-119">После привязки учетной записи хранения к Центру Интернета вещей служба возвращает универсальный код ресурса (URI) SAS на устройство, получив от него запрос на отправку файла.</span><span class="sxs-lookup"><span data-stu-id="cc76e-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="cc76e-120">[Пакеты SDK для Azure IoT][lnk-sdks] автоматически управляют получением кода URI SAS, отправкой файла и уведомлением Центра Интернета вещей о завершении отправки.</span><span class="sxs-lookup"><span data-stu-id="cc76e-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="cc76e-121">Инициализация отправки файла</span><span class="sxs-lookup"><span data-stu-id="cc76e-121">Initialize a file upload</span></span>
<span data-ttu-id="cc76e-122">У Центра Интернета вещей есть конечная точка, предназначенная для выполнения устройствами запросов на URI SAS хранилища, куда необходимо отправить файл.</span><span class="sxs-lookup"><span data-stu-id="cc76e-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="cc76e-123">Чтобы инициировать процесс передачи файла, устройство отправляет запрос POST в `{iot hub}.azure-devices.net/devices/{deviceId}/files` со следующим текстом в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="cc76e-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="cc76e-124">Центр Интернета вещей возвращает следующие данные, которые устройство использует для передачи файла:</span><span class="sxs-lookup"><span data-stu-id="cc76e-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="cc76e-125">Инициализация передачи файла с использованием запроса GET (не рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="cc76e-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="cc76e-126">В этом разделе описаны нерекомендуемые возможности получения кода URI SAS из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cc76e-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="cc76e-127">Используйте метод POST, описанный выше.</span><span class="sxs-lookup"><span data-stu-id="cc76e-127">Use the POST method described previously.</span></span>

<span data-ttu-id="cc76e-128">Центр Интернета вещей располагает двумя конечными точками REST для поддержки отправки файлов. Одна предназначена для получения кода URI SAS для хранения, а другая — для уведомления Центра Интернета вещей о завершении загрузки.</span><span class="sxs-lookup"><span data-stu-id="cc76e-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="cc76e-129">Устройство инициирует передачу файла, отправив запрос GET в Центр Интернета вещей по адресу `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="cc76e-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="cc76e-130">Центр Интернета вещей возвращает следующие данные:</span><span class="sxs-lookup"><span data-stu-id="cc76e-130">The IoT hub returns:</span></span>

* <span data-ttu-id="cc76e-131">универсальный код ресурса (URI) SAS, относящийся к передаваемому файлу;</span><span class="sxs-lookup"><span data-stu-id="cc76e-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="cc76e-132">идентификатор корреляции, который необходимо использовать по завершении передачи.</span><span class="sxs-lookup"><span data-stu-id="cc76e-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="cc76e-133">Уведомление Центра Интернета вещей о завершении отправки файла</span><span class="sxs-lookup"><span data-stu-id="cc76e-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="cc76e-134">Устройство отвечает за отправку файла в хранилище при помощи пакетов SDK службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cc76e-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="cc76e-135">По завершении передачи устройство отправляет запрос POST в `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` со следующим текстом в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="cc76e-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="cc76e-136">Значение `isSuccess` является логическим и указывает, успешно ли загружен файл.</span><span class="sxs-lookup"><span data-stu-id="cc76e-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="cc76e-137">Код состояния для `statusCode` является состоянием отправки файла в хранилище и `statusDescription` соответствует `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="cc76e-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="cc76e-138">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="cc76e-138">Reference topics:</span></span>

<span data-ttu-id="cc76e-139">Далее предоставлены дополнительные сведения о передаче файлов с устройства.</span><span class="sxs-lookup"><span data-stu-id="cc76e-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="cc76e-140">Уведомления об отправке файлов</span><span class="sxs-lookup"><span data-stu-id="cc76e-140">File upload notifications</span></span>

<span data-ttu-id="cc76e-141">Когда устройство уведомляет Центр Интернета вещей о завершении передачи, Центр Интернета вещей может при необходимости создать сообщение уведомления, которое содержит имя и расположение файла.</span><span class="sxs-lookup"><span data-stu-id="cc76e-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="cc76e-142">Как описано в разделе [Конечные точки][lnk-endpoints], Центр Интернета вещей доставляет уведомления об отправке файлов через конечную точку, доступную для службы (**/messages/servicebound/fileuploadnotifications**), в виде сообщений.</span><span class="sxs-lookup"><span data-stu-id="cc76e-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="cc76e-143">Семантика получения уведомлений об отправке файлов идентична семантике, используемой для сообщений, отправляемых из облака на устройство, и предусматривает такой же [жизненный цикл сообщения][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="cc76e-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="cc76e-144">Каждое сообщение, полученное из конечной точки уведомления об отправке файла, — это запись JSON с перечисленными ниже свойствами.</span><span class="sxs-lookup"><span data-stu-id="cc76e-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="cc76e-145">Свойство</span><span class="sxs-lookup"><span data-stu-id="cc76e-145">Property</span></span> | <span data-ttu-id="cc76e-146">Описание</span><span class="sxs-lookup"><span data-stu-id="cc76e-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc76e-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="cc76e-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="cc76e-148">Метка времени, указывающая, когда было создано уведомление.</span><span class="sxs-lookup"><span data-stu-id="cc76e-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="cc76e-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="cc76e-149">DeviceId</span></span> |<span data-ttu-id="cc76e-150">**DeviceId** устройства, с которого был отправлен файл.</span><span class="sxs-lookup"><span data-stu-id="cc76e-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="cc76e-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="cc76e-151">BlobUri</span></span> |<span data-ttu-id="cc76e-152">Код URI переданного файла.</span><span class="sxs-lookup"><span data-stu-id="cc76e-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="cc76e-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="cc76e-153">BlobName</span></span> |<span data-ttu-id="cc76e-154">Имя переданного файла.</span><span class="sxs-lookup"><span data-stu-id="cc76e-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="cc76e-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="cc76e-155">LastUpdatedTime</span></span> |<span data-ttu-id="cc76e-156">Метка времени, указывающая, когда файл был в последний раз обновлен.</span><span class="sxs-lookup"><span data-stu-id="cc76e-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="cc76e-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="cc76e-157">BlobSizeInBytes</span></span> |<span data-ttu-id="cc76e-158">Размер переданного файла.</span><span class="sxs-lookup"><span data-stu-id="cc76e-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="cc76e-159">**Пример**.</span><span class="sxs-lookup"><span data-stu-id="cc76e-159">**Example**.</span></span> <span data-ttu-id="cc76e-160">В этом примере показан текст уведомления об отправке файла.</span><span class="sxs-lookup"><span data-stu-id="cc76e-160">This example shows the body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="cc76e-161">Параметры конфигурации уведомлений об отправке файла</span><span class="sxs-lookup"><span data-stu-id="cc76e-161">File upload notification configuration options</span></span>

<span data-ttu-id="cc76e-162">Каждый Центр Интернета вещей предоставляет перечисленные ниже параметры конфигурации уведомлений об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="cc76e-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="cc76e-163">Свойство</span><span class="sxs-lookup"><span data-stu-id="cc76e-163">Property</span></span> | <span data-ttu-id="cc76e-164">Описание</span><span class="sxs-lookup"><span data-stu-id="cc76e-164">Description</span></span> | <span data-ttu-id="cc76e-165">Диапазон и значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="cc76e-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc76e-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="cc76e-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="cc76e-167">Позволяет указать, следует ли записывать уведомления об отправке файлов в конечную точку файловых уведомлений.</span><span class="sxs-lookup"><span data-stu-id="cc76e-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="cc76e-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="cc76e-168">Bool.</span></span> <span data-ttu-id="cc76e-169">По умолчанию: True.</span><span class="sxs-lookup"><span data-stu-id="cc76e-169">Default: True.</span></span> |
| <span data-ttu-id="cc76e-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="cc76e-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="cc76e-171">Значение TTL по умолчанию для уведомлений об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="cc76e-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="cc76e-172">Интервал ISO_8601 — до 48 часов (минимум 1 минута).</span><span class="sxs-lookup"><span data-stu-id="cc76e-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="cc76e-173">Значение по умолчанию — 1 час.</span><span class="sxs-lookup"><span data-stu-id="cc76e-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="cc76e-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="cc76e-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="cc76e-175">Длительность блокировки для очереди уведомлений об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="cc76e-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="cc76e-176">5–300 секунд (минимум 5 секунд).</span><span class="sxs-lookup"><span data-stu-id="cc76e-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="cc76e-177">Значение по умолчанию — 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="cc76e-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="cc76e-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="cc76e-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="cc76e-179">Максимальное количество доставок для очереди уведомлений об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="cc76e-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="cc76e-180">От 1 до 100.</span><span class="sxs-lookup"><span data-stu-id="cc76e-180">1 to 100.</span></span> <span data-ttu-id="cc76e-181">Значение по умолчанию — 100.</span><span class="sxs-lookup"><span data-stu-id="cc76e-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="cc76e-182">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="cc76e-182">Additional reference material</span></span>

<span data-ttu-id="cc76e-183">Другие справочные статьи в руководстве разработчика для Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="cc76e-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="cc76e-184">Статья [IoT Hub endpoints][lnk-endpoints] (Конечные точки Центра Интернета вещей) содержит сведения о конечных точках, которые каждый Центр Интернета вещей предоставляет для операций управления и среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="cc76e-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="cc76e-185">Статья [Квоты и регулирование в Центре Интернета вещей][lnk-quotas] содержит сведения о квотах, применимых к службе Центра Интернета вещей, и поведении регулирования.</span><span class="sxs-lookup"><span data-stu-id="cc76e-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="cc76e-186">В статье [Пакеты SDK для устройств и служб Интернета вещей Azure][lnk-sdks] указаны различные языковые пакеты SDK, которые можно использовать при разработке приложений для устройств и служб, взаимодействующих с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cc76e-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="cc76e-187">В статье [Справочник — язык запросов Центра Интернета вещей для двойников устройств, заданий и маршрутизации сообщений][lnk-query] описывается язык запросов, который можно использовать для получения сведений о двойниках устройств и заданиях из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cc76e-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="cc76e-188">Статья [Поддержка MQTT в Центре Интернета вещей][lnk-devguide-mqtt] содержит дополнительные сведения о поддержке протокола MQTT в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cc76e-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc76e-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc76e-189">Next steps</span></span>

<span data-ttu-id="cc76e-190">Теперь, когда вы узнали, как передавать файлы с устройств с помощью Центра Интернета вещей, вас могут заинтересовать следующие статьи в руководстве разработчика для Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="cc76e-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="cc76e-191">[Manage device identities in IoT Hub][lnk-devguide-identities] (Управление удостоверениями устройств в Центре Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="cc76e-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="cc76e-192">[Управление доступом к Центру Интернета вещей][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="cc76e-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="cc76e-193">[Основные сведения о двойниках устройств (предварительная версия)][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="cc76e-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="cc76e-194">[Вызов прямого метода на устройстве (предварительная версия)][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="cc76e-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="cc76e-195">[Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="cc76e-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="cc76e-196">Если вы хотели бы применить на практике некоторые основные понятия, описанные в этой статье, можно просмотреть следующее руководство по Центру Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="cc76e-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="cc76e-197">[Учебник: как передать файлы из устройств в облако с помощью Центра Интернета вещей][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="cc76e-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
