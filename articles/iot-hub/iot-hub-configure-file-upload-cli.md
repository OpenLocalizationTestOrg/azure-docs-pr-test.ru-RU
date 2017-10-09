---
title: "tooIoT передачи файла aaaConfigure концентратора с помощью Azure CLI (az.py) | Документы Microsoft"
description: "Как с помощью tooconfigure fileuploads tooAzure центр IoT hello кросс платформенных Azure CLI 2.0 (az.py)."
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
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>Настройка отправки файлов в Центре Интернета вещей с помощью Azure CLI

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello [файла функций передачи данных в центр IoT][lnk-upload], его необходимо связать учетную запись хранилища Azure с вашего центра IoT. Можно использовать существующую учетную запись хранения или создать новую.

toocomplete этого учебника требуется hello следующие:

* Активная учетная запись Azure. Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* [Azure CLI 2.0][lnk-CLI-install].
* Центр интернета вещей Azure. При отсутствии центра IoT можно использовать hello `az iot hub create` [команда] [ lnk-cli-create-iothub] toocreate один или используйте hello портала слишком [создать центр IoT] [lnk портала концентратора].
* Учетная запись хранения Azure. При отсутствии учетной записи хранилища Azure можно использовать hello [Azure CLI 2.0 — управление учетными записями хранения] [ lnk-manage-storage] toocreate одно или используйте hello портала слишком[создать учетную запись хранилища] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Выполнение входа и установка учетной записи Azure

Войдите в tooyour учетная запись Azure и выберите свою подписку.

1. Hello командной строки, выполнив hello [входа команда][lnk-login-command]:

    ```azurecli
    az login
    ```

    Выполните инструкции tooauthenticate hello, с помощью кода hello и войдите в tooyour учетная запись Azure через веб-браузер.

1. Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello Azure учетные записи, связанные с учетными данными. Используйте следующие hello [toolist команда hello учетных записей Azure] [ lnk-az-account-command] для toouse вы:

    ```azurecli
    az account list
    ```

    Используется следующая команда tooselect подписки требуется toouse toorun hello команды toocreate концентратор IoT hello. Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>Получение сведений об учетной записи хранения

Hello следующие шаги предполагают, что вы создали учетную запись хранилища с помощью hello **диспетчера ресурсов** модель развертывания, а не hello **классический** модели развертывания.

отправляет файл tooconfigure с устройств, необходимо hello строку подключения для учетной записи хранилища Azure. Учетная запись хранения Hello должна быть в hello той же подписке, ваш центр IoT. Необходимо также hello имя контейнера BLOB-объектов в учетной записи хранения hello. Используйте следующие команды tooretrieve hello ключи учетной записи хранилища:

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Запишите hello **connectionString** значение. Необходимо в hello следующие шаги.

Для отправки файлов можно использовать существующий контейнер BLOB-объектов или создать новый.

* toolist hello существующие BLOB-объект контейнеры в учетной записи используйте hello следующую команду:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate контейнер больших двоичных объектов в вашей учетной записи хранилища, hello используйте следующую команду:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Передача файла

Теперь вы можете настроить ваш tooenable концентратора IoT [файл функций передачи] [ lnk-upload] с помощью сведений о своей учетной записи хранилища.

Конфигурация Hello требует hello следующие значения:

**Контейнер хранилища**: контейнер больших двоичных объектов в учетной записи хранилища Azure в вашей текущей подписки Azure tooassociate с вашего центра IoT. Вы получили сведения об учетной записи хранилище hello в предшествующих раздел hello. Центр IoT автоматически создает идентификаторы URI SAS с контейнер больших двоичных объектов toothis разрешения записи для устройств toouse, когда они отправляют файлы.

**Receive notifications for uploaded files** (Получать уведомления об отправленных файлах). Включите или отключите уведомления об отправке файлов.

**Срок ЖИЗНИ SAS**: этот параметр — hello, время жизни объекта hello идентификаторы URI SAS возвращенных toohello устройства центра IoT. По умолчанию значение tooone час.

**Уведомления об параметры по умолчанию срок ЖИЗНИ файла**: hello time-to-live уведомления передачи файла до окончания срока их. По умолчанию значение tooone день.

**Файл уведомления максимальное число доставок**: hello время hello toodeliver попыток центра IoT уведомление передачи файла. По умолчанию значение too10.

Используйте следующие параметры передачи файла hello tooconfigure Azure CLI команды на концентратор IoT hello.

Выполните следующие команды в оболочке Bash:

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

В командной строке Windows выполните следующие команды:

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Вы можете просмотреть hello конфигурации загрузки файла на ваш центр IoT с помощью hello следующую команду:

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о возможности передачи файлов hello центра IoT см. в разделе [передачи файлов на устройстве][lnk-upload].

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


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create