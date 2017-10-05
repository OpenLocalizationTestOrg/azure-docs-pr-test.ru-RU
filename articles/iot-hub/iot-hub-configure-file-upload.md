---
title: "Настройка отправки файлов с помощью портала Azure | Документация Майкрософт"
description: "Использование портала Azure для настройки Центра Интернета вещей, чтобы включить отправку файлов с подключенных устройств. Содержит сведения о настройке целевой учетной записи хранения Azure."
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
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="5c174-104">Настройка отправки файлов Центра Интернета вещей с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5c174-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="5c174-105">Передача файла</span><span class="sxs-lookup"><span data-stu-id="5c174-105">File upload</span></span>

<span data-ttu-id="5c174-106">Чтобы использовать [функции отправки файлов в Центре Интернета вещей][lnk-upload], сначала необходимо связать учетную запись хранения Azure с центром.</span><span class="sxs-lookup"><span data-stu-id="5c174-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="5c174-107">Выберите **Отправка файла**, чтобы отобразить список свойств передачи файлов для Центра Интернета вещей, который вы изменяете.</span><span class="sxs-lookup"><span data-stu-id="5c174-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![Просмотр параметров отправки файлов в Центре Интернета вещей на портале][13]

<span data-ttu-id="5c174-109">**Контейнер хранилища.** На портале Azure выберите контейнер больших двоичных объектов в учетной записи хранения своей текущей подписки Azure, чтобы связать его с центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5c174-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="5c174-110">При необходимости можно создать новую учетную запись хранения Azure в колонке **Учетные записи хранения** и новый контейнер больших двоичных объектов в колонке **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="5c174-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="5c174-111">Центр IoT автоматически генерирует универсальные коды ресурсов (URI) подписанных URL-адресов с разрешениями на запись в этом контейнере больших двоичных объектов, чтобы устройства могли их использовать во время передач файлов.</span><span class="sxs-lookup"><span data-stu-id="5c174-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![Просмотр контейнеров хранилища для отправки файла на портале][14]

<span data-ttu-id="5c174-113">**Receive notifications for uploaded files** (Получать уведомления об отправленных файлах). Включите или отключите уведомления об отправке файлов с помощью переключателя.</span><span class="sxs-lookup"><span data-stu-id="5c174-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="5c174-114">**SAS TTL** (Срок жизни SAS). Этот параметр определяет срок жизни универсальных кодов ресурса (URI) SAS, возвращаемых центром Интернета вещей на устройство.</span><span class="sxs-lookup"><span data-stu-id="5c174-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="5c174-115">По умолчанию устанавливается значение "один час", но его можно изменить с помощью ползунка.</span><span class="sxs-lookup"><span data-stu-id="5c174-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="5c174-116">**File notification settings default TTL** (Стандартный срок жизни уведомления о файле). Срок жизни уведомления об отправке файла.</span><span class="sxs-lookup"><span data-stu-id="5c174-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="5c174-117">По умолчанию устанавливается значение "один день", но его можно изменить с помощью ползунка.</span><span class="sxs-lookup"><span data-stu-id="5c174-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="5c174-118">**File notification maximum delivery count**(Максимальное число доставок уведомления о файле): число попыток доставки уведомления о передаче файла, предпринимаемых центром IoT.</span><span class="sxs-lookup"><span data-stu-id="5c174-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="5c174-119">По умолчанию устанавливается значение 10, но его можно изменить с помощью ползунка.</span><span class="sxs-lookup"><span data-stu-id="5c174-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![Настройка отправки файла Центра Интернета вещей на портале][15]

## <a name="next-steps"></a><span data-ttu-id="5c174-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c174-121">Next steps</span></span>

<span data-ttu-id="5c174-122">Дополнительные сведения о возможностях центра Интернета вещей, касающихся отправки файлов, см. в разделе об [отправке файлов с устройства][lnk-upload] в руководстве разработчика для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5c174-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="5c174-123">Дополнительные сведения об управлении Центром Интернета вещей в Azure см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="5c174-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="5c174-124">[Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="5c174-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="5c174-125">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="5c174-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="5c174-126">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="5c174-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="5c174-127">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="5c174-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5c174-128">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5c174-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5c174-129">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="5c174-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="5c174-130">[Все аспекты безопасности решения Центра Интернета вещей][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="5c174-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
