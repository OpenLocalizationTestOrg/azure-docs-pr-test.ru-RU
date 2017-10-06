---
title: "Отправка файла aaaUse hello Azure портала tooconfigure | Документы Microsoft"
description: "Как toouse hello Azure портала tooconfigure файл tooenable концентратора IoT передач с подключенных устройств. Содержит сведения о настройке учетной записи хранилища Azure hello назначения."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="294dd-104">Настройка центра IoT передачи файлов, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="294dd-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="294dd-105">Передача файла</span><span class="sxs-lookup"><span data-stu-id="294dd-105">File upload</span></span>

<span data-ttu-id="294dd-106">toouse hello [файла функций передачи данных в центр IoT][lnk-upload], его необходимо связать учетную запись хранилища Azure с концентратор.</span><span class="sxs-lookup"><span data-stu-id="294dd-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="294dd-107">Выберите **передачу файла** toodisplay список свойств передачи файла для центра IoT hello, которая изменяется.</span><span class="sxs-lookup"><span data-stu-id="294dd-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![Файл представления центра IoT Отправка параметров на портале hello][13]

<span data-ttu-id="294dd-109">**Контейнер хранилища**: используйте hello Azure портала tooselect контейнер больших двоичных объектов в учетной записи хранилища Azure в вашей текущей подписки Azure tooassociate с вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="294dd-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="294dd-110">Если необходимо, можно создать учетную запись хранилища Azure на hello **учетные записи хранения** колонки и больших двоичных объектов контейнера на hello **контейнеры** колонку.</span><span class="sxs-lookup"><span data-stu-id="294dd-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="294dd-111">Центр IoT автоматически создает идентификаторы URI SAS с контейнер больших двоичных объектов toothis разрешения записи для устройств toouse, когда они отправляют файлы.</span><span class="sxs-lookup"><span data-stu-id="294dd-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Просмотр контейнеров хранилища для отправки файла на портале hello][14]

<span data-ttu-id="294dd-113">**Получать уведомления об отправленных файлов**: Включение и отключение уведомлений передачи файлов через hello переключателя.</span><span class="sxs-lookup"><span data-stu-id="294dd-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="294dd-114">**Срок ЖИЗНИ SAS**: этот параметр — hello, время жизни объекта hello идентификаторы URI SAS возвращенных toohello устройства центра IoT.</span><span class="sxs-lookup"><span data-stu-id="294dd-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="294dd-115">По умолчанию значение tooone час, но может быть настроенные tooother значений при помощи ползунок hello.</span><span class="sxs-lookup"><span data-stu-id="294dd-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="294dd-116">**Уведомления об параметры по умолчанию срок ЖИЗНИ файла**: hello time-to-live уведомления передачи файла до окончания срока их.</span><span class="sxs-lookup"><span data-stu-id="294dd-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="294dd-117">По умолчанию значение tooone день, но может быть настроенные tooother значений при помощи ползунок hello.</span><span class="sxs-lookup"><span data-stu-id="294dd-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="294dd-118">**Файл уведомления максимальное число доставок**: hello время hello toodeliver попыток центра IoT уведомление передачи файла.</span><span class="sxs-lookup"><span data-stu-id="294dd-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="294dd-119">По умолчанию значение too10, но может быть настроенные tooother значений при помощи ползунок hello.</span><span class="sxs-lookup"><span data-stu-id="294dd-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![Настройка центра IoT отправки файла на портале hello][15]

## <a name="next-steps"></a><span data-ttu-id="294dd-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="294dd-121">Next steps</span></span>

<span data-ttu-id="294dd-122">Дополнительные сведения о возможности передачи файлов hello центра IoT см. в разделе [передачи файлов на устройстве] [ lnk-upload] в hello руководстве разработчика центр IoT.</span><span class="sxs-lookup"><span data-stu-id="294dd-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="294dd-123">Выполните эти дополнительные сведения об управлении центр IoT Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="294dd-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="294dd-124">[Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="294dd-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="294dd-125">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="294dd-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="294dd-126">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="294dd-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="294dd-127">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="294dd-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="294dd-128">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="294dd-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="294dd-129">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="294dd-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="294dd-130">[Защита вашего решения IoT из hello основание,][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="294dd-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
