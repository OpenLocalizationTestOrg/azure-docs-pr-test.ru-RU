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
# <a name="upload-files-with-iot-hub"></a>Отправка файлов с помощью Центра Интернета вещей

Как описано в hello [конечные точки центра IoT] [ lnk-endpoints] статьи, устройство может инициировать передачу файла путем отправки уведомления через конечную точку с выходом устройства (**/devices/ {deviceId} / файлы**). Когда устройство уведомляет центра IoT о завершении передачи, центр IoT посылает сообщение уведомления передачи файлов через hello **/messages/servicebound/filenotifications** конечной точки службы с выходом.

Вместо посредничества сообщения через Центр IoT сам, центр IoT вместо действует как dispatcher tooan связанную учетную запись хранилища Azure. Токен хранилища из центра IoT, определенных toohello файл hello устройства, которые tooupload запросы устройства. Hello устройство использует универсальный код Ресурса SAS tooupload hello файл toostorage hello и после завершения передачи hello hello устройство отправляет уведомление о завершении tooIoT концентратора. Центр IoT проверяет hello отправки файла завершена, а затем добавляет файл отправки уведомлений сообщение toohello ориентированных на службы уведомления конечную точку файла.

Перед отправкой файла tooIoT концентратора с устройства, необходимо настроить концентратор с [связывание хранилища Azure] [ lnk-associate-storage] tooit учетной записи.

Устройства можно затем [инициализировать передачи] [ lnk-initialize] и затем [уведомления центра IoT] [ lnk-notify] после завершения передачи hello. При необходимости при устройства уведомляет центра IoT завершения этой отправки hello, hello службы можно создать [уведомление][lnk-service-notification].

### <a name="when-toouse"></a>Когда toouse

Использование файлов мультимедиа toosend передачи файла и телеметрии больших пакетов, отправляемых периодически подключенных устройств или сжатый toosave пропускной способности.

См. слишком[руководство связи устройства в облако] [ lnk-d2c-guidance] if сомнительных между использованием выводятся свойства, сообщения из устройства в облако или передачи файла.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Связывание учетной записи хранения Azure с Центром Интернета вещей

функции передачи файлов toouse hello, необходимо сначала связать toohello учетной записи хранилища Azure IoT Hub. Вы эту задачу можно выполнить либо с помощью hello [портал Azure][lnk-management-portal], или программно через hello [API REST поставщика ресурсов центра IoT] [ lnk-resource-provider-apis]. После привязки учетной записи хранилища Azure с вашего центра IoT hello служба возвращает SAS URI tooa устройства устройства hello инициирует запрос передачи файла.

> [!NOTE]
> Hello [пакеты SDK Azure IoT] [ lnk-sdks] автоматически извлечение дескриптора hello универсальный код Ресурса SAS, передача файла hello и уведомление центра IoT завершения загрузки.


## <a name="initialize-a-file-upload"></a>Инициализация отправки файла
Центр IoT есть конечная точка, специально для устройств toorequest универсальный код Ресурса SAS для хранения tooupload файла. процесс загрузки файла hello tooinitiate hello устройство отправляет запрос POST слишком`{iot hub}.azure-devices.net/devices/{deviceId}/files` с hello следующий текст JSON:

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

Центр IoT возвращает следующие данные, какое устройство hello использует файл hello tooupload hello:

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>Инициализация передачи файла с использованием запроса GET (не рекомендуется)

> [!NOTE]
> В этом разделе описаны устаревшие функциональные возможности для как tooreceive URI SAS из центра IoT. Используйте метод POST hello было описано выше.

Центр IoT имеет два файла toosupport конечные точки REST Отправка одного hello tooget универсальный код Ресурса SAS для хранения и hello других центра IoT toonotify hello завершения загрузки. Hello устройства инициирует процесс загрузки файла hello, отправляя концентратор IoT toohello GET на `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`. Возвращает центр IoT Hello:

* Универсальный код Ресурса SAS, загружен toobe toohello конкретного файла.
* Toobe идентификатор корреляции, использовать после окончания загрузки hello.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>Уведомление Центра Интернета вещей о завершении отправки файла

устройство Hello отвечает за Отправка файла toostorage hello, с помощью пакетов SDK хранилища Azure hello. После завершения передачи hello hello устройства также отправляет запрос POST`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` с hello следующий текст JSON:

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

Здравствуйте, значение `isSuccess` является логическое значение, указывающее ли hello файл успешно отправлен. Здравствуйте, код состояния для `statusCode` hello состояние передачи hello toostorage файл hello и hello `statusDescription` соответствует toohello `statusCode`.

## <a name="reference-topics"></a>Справочные материалы

Hello следующие справочные разделы предоставляют дополнительные сведения о загрузке файлов с устройства.

## <a name="file-upload-notifications"></a>Уведомления об отправке файлов

При необходимости при устройства уведомляет центра IoT о завершении передачи, центра IoT можно создать сообщение уведомления, содержащий hello имя и место хранения файла hello.

Как описано в разделе [Конечные точки][lnk-endpoints], Центр Интернета вещей доставляет уведомления об отправке файлов через конечную точку, доступную для службы (**/messages/servicebound/fileuploadnotifications**), в виде сообщений. Hello семантику получения для уведомления о передачи файла: hello же, как и для облака на устройство сообщения и иметь hello же [жизненный цикл сообщения][lnk-lifecycle]. Каждое сообщение, полученные из конечной точки уведомления для отправки файла hello является запись JSON с hello следующие свойства:

| Свойство | Описание |
| --- | --- |
| EnqueuedTimeUtc |Отметка времени, указывающее, при создании уведомления о hello. |
| deviceId |**DeviceId** hello устройства, который отправили файл hello. |
| BlobUri |Файл загружен URI hello. |
| BlobName |Файл загружен имя hello. |
| LastUpdatedTime |Отметка времени, указывающее время последнего обновления файла hello. |
| BlobSizeInBytes |Файл загружен размер hello. |

**Пример**. Этот пример текста hello файла отправить сообщение уведомления.

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

## <a name="file-upload-notification-configuration-options"></a>Параметры конфигурации уведомлений об отправке файла

Каждый центр IoT предоставляет следующие параметры конфигурации для уведомлений о передачи файла hello:

| Свойство | Описание | Диапазон и значение по умолчанию |
| --- | --- | --- |
| **enableFileUploadNotifications** |Определяет, записываются ли файл отправках конечную точку уведомлений toohello файла. |Bool. По умолчанию: True. |
| **fileNotifications.ttlAsIso8601** |Значение TTL по умолчанию для уведомлений об отправке файлов. |Интервал ISO_8601 копирование too48H (минимальное 1 минута). Значение по умолчанию — 1 час. |
| **fileNotifications.lockDuration** |Длительность блокировки для отправки уведомлений hello файл очереди. |5 too300 секунд (минимальное 5 секунд). Значение по умолчанию — 60 секунд. |
| **fileNotifications.maxDeliveryCount** |Максимальное число доставок файла hello отправить очередь уведомлений. |1 too100. Значение по умолчанию — 100. |

## <a name="additional-reference-material"></a>Дополнительные справочные материалы

Другие разделы ссылку в hello центра IoT руководстве для разработчиков:

* [Конечные точки центра IoT] [ lnk-endpoints] описывает hello различные конечные точки, предоставляемые каждый центр IoT для операций времени выполнения и управления.
* [Регулирование и квоты] [ lnk-quotas] описывает hello квот и регулирования, применяющимся toohello службы центра IoT.
* [Пакеты SDK устройств и служб Azure IoT] [ lnk-sdks] списки hello языка различных пакетов SDK, которые можно использовать при разработке приложений, устройств и служб, которые взаимодействуют с центром IoT.
* [Язык запросов центра IoT] [ lnk-query] описывает hello язык запросов, можно использовать tooretrieve сведения из центра IoT близнецы устройства и заданий.
* [Поддержка MQTT концентратора IoT] [ lnk-devguide-mqtt] приведены более подробные сведения о поддержке центра IoT протокола MQTT hello.

## <a name="next-steps"></a>Дальнейшие действия

Теперь вы узнали, как tooupload файлы с устройств с помощью центра IoT, вам могут быть интересны следующие разделы руководства разработчика центра IoT hello:

* [Manage device identities in IoT Hub][lnk-devguide-identities] (Управление удостоверениями устройств в Центре Интернета вещей)
* [Элемент управления доступом tooIoT концентратора][lnk-devguide-security]
* [Конфигурации и состояния toosynchronize близнецы устройства][lnk-devguide-device-twins]
* [Вызов прямого метода на устройстве (предварительная версия)][lnk-devguide-directmethods]
* [Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)

При желании tootry некоторые основные понятия hello, описанных в этой статье, могут быть интересны следующие учебника центра IoT hello параметры:

* [Об облачных tooupload файлы из toohello устройства с центром IoT][lnk-fileupload-tutorial]

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
