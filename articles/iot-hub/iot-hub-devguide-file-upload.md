---
title: "Отправка файла aaaUnderstand центр IoT Azure | Документы Microsoft"
description: "Руководство разработчика - функция передачи файла используйте hello из центра IoT toomanage, передача файлов из контейнера BLOB-объект хранилища Azure tooan устройства."
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
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="38c57-103">Отправка файлов с помощью Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="38c57-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="38c57-104">Как описано в hello [конечные точки центра IoT] [ lnk-endpoints] статьи, устройство может инициировать передачу файла путем отправки уведомления через конечную точку с выходом устройства (**/devices/ {deviceId} / файлы**).</span><span class="sxs-lookup"><span data-stu-id="38c57-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="38c57-105">Когда устройство уведомляет центра IoT о завершении передачи, центр IoT посылает сообщение уведомления передачи файлов через hello **/messages/servicebound/filenotifications** конечной точки службы с выходом.</span><span class="sxs-lookup"><span data-stu-id="38c57-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="38c57-106">Вместо посредничества сообщения через Центр IoT сам, центр IoT вместо действует как dispatcher tooan связанную учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="38c57-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="38c57-107">Токен хранилища из центра IoT, определенных toohello файл hello устройства, которые tooupload запросы устройства.</span><span class="sxs-lookup"><span data-stu-id="38c57-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="38c57-108">Hello устройство использует универсальный код Ресурса SAS tooupload hello файл toostorage hello и после завершения передачи hello hello устройство отправляет уведомление о завершении tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="38c57-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="38c57-109">Центр IoT проверяет hello отправки файла завершена, а затем добавляет файл отправки уведомлений сообщение toohello ориентированных на службы уведомления конечную точку файла.</span><span class="sxs-lookup"><span data-stu-id="38c57-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="38c57-110">Перед отправкой файла tooIoT концентратора с устройства, необходимо настроить концентратор с [связывание хранилища Azure] [ lnk-associate-storage] tooit учетной записи.</span><span class="sxs-lookup"><span data-stu-id="38c57-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="38c57-111">Устройства можно затем [инициализировать передачи] [ lnk-initialize] и затем [уведомления центра IoT] [ lnk-notify] после завершения передачи hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="38c57-112">При необходимости при устройства уведомляет центра IoT завершения этой отправки hello, hello службы можно создать [уведомление][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="38c57-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="38c57-113">Когда toouse</span><span class="sxs-lookup"><span data-stu-id="38c57-113">When toouse</span></span>

<span data-ttu-id="38c57-114">Использование файлов мультимедиа toosend передачи файла и телеметрии больших пакетов, отправляемых периодически подключенных устройств или сжатый toosave пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="38c57-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="38c57-115">См. слишком[руководство связи устройства в облако] [ lnk-d2c-guidance] if сомнительных между использованием выводятся свойства, сообщения из устройства в облако или передачи файла.</span><span class="sxs-lookup"><span data-stu-id="38c57-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="38c57-116">Связывание учетной записи хранения Azure с Центром Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="38c57-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="38c57-117">функции передачи файлов toouse hello, необходимо сначала связать toohello учетной записи хранилища Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="38c57-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="38c57-118">Вы эту задачу можно выполнить либо с помощью hello [портал Azure][lnk-management-portal], или программно через hello [API REST поставщика ресурсов центра IoT] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="38c57-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="38c57-119">После привязки учетной записи хранилища Azure с вашего центра IoT hello служба возвращает SAS URI tooa устройства устройства hello инициирует запрос передачи файла.</span><span class="sxs-lookup"><span data-stu-id="38c57-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="38c57-120">Hello [пакеты SDK Azure IoT] [ lnk-sdks] автоматически извлечение дескриптора hello универсальный код Ресурса SAS, передача файла hello и уведомление центра IoT завершения загрузки.</span><span class="sxs-lookup"><span data-stu-id="38c57-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="38c57-121">Инициализация отправки файла</span><span class="sxs-lookup"><span data-stu-id="38c57-121">Initialize a file upload</span></span>
<span data-ttu-id="38c57-122">Центр IoT есть конечная точка, специально для устройств toorequest универсальный код Ресурса SAS для хранения tooupload файла.</span><span class="sxs-lookup"><span data-stu-id="38c57-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="38c57-123">процесс загрузки файла hello tooinitiate hello устройство отправляет запрос POST слишком`{iot hub}.azure-devices.net/devices/{deviceId}/files` с hello следующий текст JSON:</span><span class="sxs-lookup"><span data-stu-id="38c57-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="38c57-124">Центр IoT возвращает следующие данные, какое устройство hello использует файл hello tooupload hello:</span><span class="sxs-lookup"><span data-stu-id="38c57-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="38c57-125">Инициализация передачи файла с использованием запроса GET (не рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="38c57-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="38c57-126">В этом разделе описаны устаревшие функциональные возможности для как tooreceive URI SAS из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="38c57-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="38c57-127">Используйте метод POST hello было описано выше.</span><span class="sxs-lookup"><span data-stu-id="38c57-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="38c57-128">Центр IoT имеет два файла toosupport конечные точки REST Отправка одного hello tooget универсальный код Ресурса SAS для хранения и hello других центра IoT toonotify hello завершения загрузки.</span><span class="sxs-lookup"><span data-stu-id="38c57-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="38c57-129">Hello устройства инициирует процесс загрузки файла hello, отправляя концентратор IoT toohello GET на `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="38c57-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="38c57-130">Возвращает центр IoT Hello:</span><span class="sxs-lookup"><span data-stu-id="38c57-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="38c57-131">Универсальный код Ресурса SAS, загружен toobe toohello конкретного файла.</span><span class="sxs-lookup"><span data-stu-id="38c57-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="38c57-132">Toobe идентификатор корреляции, использовать после окончания загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="38c57-133">Уведомление Центра Интернета вещей о завершении отправки файла</span><span class="sxs-lookup"><span data-stu-id="38c57-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="38c57-134">устройство Hello отвечает за Отправка файла toostorage hello, с помощью пакетов SDK хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="38c57-135">После завершения передачи hello hello устройства также отправляет запрос POST`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` с hello следующий текст JSON:</span><span class="sxs-lookup"><span data-stu-id="38c57-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="38c57-136">Здравствуйте, значение `isSuccess` является логическое значение, указывающее ли hello файл успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="38c57-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="38c57-137">Здравствуйте, код состояния для `statusCode` hello состояние передачи hello toostorage файл hello и hello `statusDescription` соответствует toohello `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="38c57-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="38c57-138">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="38c57-138">Reference topics:</span></span>

<span data-ttu-id="38c57-139">Hello следующие справочные разделы предоставляют дополнительные сведения о загрузке файлов с устройства.</span><span class="sxs-lookup"><span data-stu-id="38c57-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="38c57-140">Уведомления об отправке файлов</span><span class="sxs-lookup"><span data-stu-id="38c57-140">File upload notifications</span></span>

<span data-ttu-id="38c57-141">При необходимости при устройства уведомляет центра IoT о завершении передачи, центра IoT можно создать сообщение уведомления, содержащий hello имя и место хранения файла hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="38c57-142">Как описано в разделе [Конечные точки][lnk-endpoints], Центр Интернета вещей доставляет уведомления об отправке файлов через конечную точку, доступную для службы (**/messages/servicebound/fileuploadnotifications**), в виде сообщений.</span><span class="sxs-lookup"><span data-stu-id="38c57-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="38c57-143">Hello семантику получения для уведомления о передачи файла: hello же, как и для облака на устройство сообщения и иметь hello же [жизненный цикл сообщения][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="38c57-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="38c57-144">Каждое сообщение, полученные из конечной точки уведомления для отправки файла hello является запись JSON с hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="38c57-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="38c57-145">Свойство</span><span class="sxs-lookup"><span data-stu-id="38c57-145">Property</span></span> | <span data-ttu-id="38c57-146">Описание</span><span class="sxs-lookup"><span data-stu-id="38c57-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38c57-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="38c57-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="38c57-148">Отметка времени, указывающее, при создании уведомления о hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="38c57-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="38c57-149">DeviceId</span></span> |<span data-ttu-id="38c57-150">**DeviceId** hello устройства, который отправили файл hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="38c57-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="38c57-151">BlobUri</span></span> |<span data-ttu-id="38c57-152">Файл загружен URI hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="38c57-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="38c57-153">BlobName</span></span> |<span data-ttu-id="38c57-154">Файл загружен имя hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="38c57-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="38c57-155">LastUpdatedTime</span></span> |<span data-ttu-id="38c57-156">Отметка времени, указывающее время последнего обновления файла hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="38c57-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="38c57-157">BlobSizeInBytes</span></span> |<span data-ttu-id="38c57-158">Файл загружен размер hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="38c57-159">**Пример**.</span><span class="sxs-lookup"><span data-stu-id="38c57-159">**Example**.</span></span> <span data-ttu-id="38c57-160">Этот пример текста hello файла отправить сообщение уведомления.</span><span class="sxs-lookup"><span data-stu-id="38c57-160">This example shows hello body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="38c57-161">Параметры конфигурации уведомлений об отправке файла</span><span class="sxs-lookup"><span data-stu-id="38c57-161">File upload notification configuration options</span></span>

<span data-ttu-id="38c57-162">Каждый центр IoT предоставляет следующие параметры конфигурации для уведомлений о передачи файла hello:</span><span class="sxs-lookup"><span data-stu-id="38c57-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="38c57-163">Свойство</span><span class="sxs-lookup"><span data-stu-id="38c57-163">Property</span></span> | <span data-ttu-id="38c57-164">Описание</span><span class="sxs-lookup"><span data-stu-id="38c57-164">Description</span></span> | <span data-ttu-id="38c57-165">Диапазон и значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="38c57-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38c57-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="38c57-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="38c57-167">Определяет, записываются ли файл отправках конечную точку уведомлений toohello файла.</span><span class="sxs-lookup"><span data-stu-id="38c57-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="38c57-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="38c57-168">Bool.</span></span> <span data-ttu-id="38c57-169">По умолчанию: True.</span><span class="sxs-lookup"><span data-stu-id="38c57-169">Default: True.</span></span> |
| <span data-ttu-id="38c57-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="38c57-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="38c57-171">Значение TTL по умолчанию для уведомлений об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="38c57-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="38c57-172">Интервал ISO_8601 копирование too48H (минимальное 1 минута).</span><span class="sxs-lookup"><span data-stu-id="38c57-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="38c57-173">Значение по умолчанию — 1 час.</span><span class="sxs-lookup"><span data-stu-id="38c57-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="38c57-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="38c57-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="38c57-175">Длительность блокировки для отправки уведомлений hello файл очереди.</span><span class="sxs-lookup"><span data-stu-id="38c57-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="38c57-176">5 too300 секунд (минимальное 5 секунд).</span><span class="sxs-lookup"><span data-stu-id="38c57-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="38c57-177">Значение по умолчанию — 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="38c57-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="38c57-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="38c57-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="38c57-179">Максимальное число доставок файла hello отправить очередь уведомлений.</span><span class="sxs-lookup"><span data-stu-id="38c57-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="38c57-180">1 too100.</span><span class="sxs-lookup"><span data-stu-id="38c57-180">1 too100.</span></span> <span data-ttu-id="38c57-181">Значение по умолчанию — 100.</span><span class="sxs-lookup"><span data-stu-id="38c57-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="38c57-182">Дополнительные справочные материалы</span><span class="sxs-lookup"><span data-stu-id="38c57-182">Additional reference material</span></span>

<span data-ttu-id="38c57-183">Другие разделы ссылку в hello центра IoT руководстве для разработчиков:</span><span class="sxs-lookup"><span data-stu-id="38c57-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="38c57-184">[Конечные точки центра IoT] [ lnk-endpoints] описывает hello различные конечные точки, предоставляемые каждый центр IoT для операций времени выполнения и управления.</span><span class="sxs-lookup"><span data-stu-id="38c57-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="38c57-185">[Регулирование и квоты] [ lnk-quotas] описывает hello квот и регулирования, применяющимся toohello службы центра IoT.</span><span class="sxs-lookup"><span data-stu-id="38c57-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="38c57-186">[Пакеты SDK устройств и служб Azure IoT] [ lnk-sdks] списки hello языка различных пакетов SDK, которые можно использовать при разработке приложений, устройств и служб, которые взаимодействуют с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="38c57-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="38c57-187">[Язык запросов центра IoT] [ lnk-query] описывает hello язык запросов, можно использовать tooretrieve сведения из центра IoT близнецы устройства и заданий.</span><span class="sxs-lookup"><span data-stu-id="38c57-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="38c57-188">[Поддержка MQTT концентратора IoT] [ lnk-devguide-mqtt] приведены более подробные сведения о поддержке центра IoT протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="38c57-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38c57-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38c57-189">Next steps</span></span>

<span data-ttu-id="38c57-190">Теперь вы узнали, как tooupload файлы с устройств с помощью центра IoT, вам могут быть интересны следующие разделы руководства разработчика центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="38c57-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="38c57-191">[Manage device identities in IoT Hub][lnk-devguide-identities] (Управление удостоверениями устройств в Центре Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="38c57-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="38c57-192">[Элемент управления доступом tooIoT концентратора][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="38c57-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="38c57-193">[Конфигурации и состояния toosynchronize близнецы устройства][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="38c57-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="38c57-194">[Вызов прямого метода на устройстве (предварительная версия)][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="38c57-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="38c57-195">[Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="38c57-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="38c57-196">При желании tootry некоторые основные понятия hello, описанных в этой статье, могут быть интересны следующие учебника центра IoT hello параметры:</span><span class="sxs-lookup"><span data-stu-id="38c57-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="38c57-197">[Об облачных tooupload файлы из toohello устройства с центром IoT][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="38c57-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
