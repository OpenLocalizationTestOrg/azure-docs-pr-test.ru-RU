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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>Настройка центра IoT передачи файлов, с помощью портала Azure hello

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Передача файла

toouse hello [файла функций передачи данных в центр IoT][lnk-upload], его необходимо связать учетную запись хранилища Azure с концентратор. Выберите **передачу файла** toodisplay список свойств передачи файла для центра IoT hello, которая изменяется.

![Файл представления центра IoT Отправка параметров на портале hello][13]

**Контейнер хранилища**: используйте hello Azure портала tooselect контейнер больших двоичных объектов в учетной записи хранилища Azure в вашей текущей подписки Azure tooassociate с вашего центра IoT. Если необходимо, можно создать учетную запись хранилища Azure на hello **учетные записи хранения** колонки и больших двоичных объектов контейнера на hello **контейнеры** колонку. Центр IoT автоматически создает идентификаторы URI SAS с контейнер больших двоичных объектов toothis разрешения записи для устройств toouse, когда они отправляют файлы.

![Просмотр контейнеров хранилища для отправки файла на портале hello][14]

**Получать уведомления об отправленных файлов**: Включение и отключение уведомлений передачи файлов через hello переключателя.

**Срок ЖИЗНИ SAS**: этот параметр — hello, время жизни объекта hello идентификаторы URI SAS возвращенных toohello устройства центра IoT. По умолчанию значение tooone час, но может быть настроенные tooother значений при помощи ползунок hello.

**Уведомления об параметры по умолчанию срок ЖИЗНИ файла**: hello time-to-live уведомления передачи файла до окончания срока их. По умолчанию значение tooone день, но может быть настроенные tooother значений при помощи ползунок hello.

**Файл уведомления максимальное число доставок**: hello время hello toodeliver попыток центра IoT уведомление передачи файла. По умолчанию значение too10, но может быть настроенные tooother значений при помощи ползунок hello.

![Настройка центра IoT отправки файла на портале hello][15]

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о возможности передачи файлов hello центра IoT см. в разделе [передачи файлов на устройстве] [ lnk-upload] в hello руководстве разработчика центр IoT.

Выполните эти дополнительные сведения об управлении центр IoT Azure toolearn ссылки.

* [Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]
* [Метрики Центра Интернета вещей][lnk-metrics]
* [Мониторинг операций][lnk-monitor]

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Руководство разработчика для Центра Интернета вещей][lnk-devguide]
* [Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)
* [Защита вашего решения IoT из hello основание,][lnk-securing]

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
