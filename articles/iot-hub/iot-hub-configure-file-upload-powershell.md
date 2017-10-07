---
title: "Отправка файла tooconfigure Azure PowerShell hello aaaUse | Документы Microsoft"
description: "Как tooconfigure командлеты Azure PowerShell hello toouse файл tooenable концентратора IoT передач с подключенных устройств. Содержит сведения о настройке учетной записи хранилища Azure hello назначения."
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
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>Настройка отправки файлов в Центре Интернета вещей с помощью PowerShell

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello [файла функций передачи данных в центр IoT][lnk-upload], его необходимо связать учетную запись хранения Azure с вашего центра IoT. Можно использовать существующую учетную запись хранения или создать новую.

toocomplete этого учебника требуется hello следующие:

* Активная учетная запись Azure. Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.
* [Командлеты Azure PowerShell][lnk-powershell-install].
* Центр интернета вещей Azure. Если у вас нет центра IoT, можно использовать hello [командлет New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate один или используйте hello портала слишком[создать центр IoT] [ lnk-portal-hub].
* Учетная запись хранения Azure. При отсутствии учетной записи хранилища Azure можно использовать hello [командлеты PowerShell хранилища Azure] [ lnk-powershell-storage] toocreate один или используйте hello портала слишком[создать учетную запись хранилища] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Выполнение входа и установка учетной записи Azure

Войдите в tooyour учетная запись Azure и выберите свою подписку.

1. В командной строке PowerShell hello, запустите hello **AzureRmAccount входа** командлета:

    ```powershell
    Login-AzureRmAccount
    ```

1. Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello подписок Azure, связанных с учетными данными. Используйте следующую команду, toolist hello подписки Azure доступны для вас toouse hello.

    ```powershell
    Get-AzureRMSubscription
    ```

    Используется следующая команда tooselect подписки требуется toouse toorun hello команды toomanage концентратор IoT hello. Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>Получение сведений об учетной записи хранения

Hello следующие шаги предполагают, что вы создали учетную запись хранилища с помощью hello **диспетчера ресурсов** модель развертывания, а не hello **классический** модели развертывания.

отправляет файл tooconfigure с устройств, необходимо hello строку подключения для учетной записи хранилища Azure. Учетная запись хранения Hello должна быть в hello той же подписке, ваш центр IoT. Необходимо также hello имя контейнера BLOB-объектов в учетной записи хранения hello. Используйте следующие команды tooretrieve hello ключи учетной записи хранилища:

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Запишите hello **key1** значение ключа учетной записи хранилища. Необходимо в hello следующие шаги.

Для отправки файлов можно использовать существующий контейнер BLOB-объектов или создать новый.

* toolist hello существующие BLOB-объект контейнеры в учетной записи используйте hello, следующие команды:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* toocreate контейнер больших двоичных объектов в вашей учетной записи хранилища, hello используйте следующие команды:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>Настройка Центра Интернета вещей

Теперь вы можете настроить ваш tooenable концентратора IoT [файл функций передачи] [ lnk-upload] с помощью сведений о своей учетной записи хранилища.

Конфигурация Hello требует hello следующие значения:

**Контейнер хранилища**: контейнер больших двоичных объектов в учетной записи хранилища Azure в вашей текущей подписки Azure tooassociate с вашего центра IoT. Вы получили сведения об учетной записи хранилище hello в предшествующих раздел hello. Центр IoT автоматически создает идентификаторы URI SAS с контейнер больших двоичных объектов toothis разрешения записи для устройств toouse, когда они отправляют файлы.

**Receive notifications for uploaded files** (Получать уведомления об отправленных файлах). Включите или отключите уведомления об отправке файлов.

**Срок ЖИЗНИ SAS**: этот параметр — hello, время жизни объекта hello идентификаторы URI SAS возвращенных toohello устройства центра IoT. По умолчанию значение tooone час.

**Уведомления об параметры по умолчанию срок ЖИЗНИ файла**: hello time-to-live уведомления передачи файла до окончания срока их. По умолчанию значение tooone день.

**Файл уведомления максимальное число доставок**: hello время hello toodeliver попыток центра IoT уведомление передачи файла. По умолчанию значение too10.

Используйте следующие параметры для передачи PowerShell командлет tooconfigure hello файла на ваш центр IoT hello.

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
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

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md