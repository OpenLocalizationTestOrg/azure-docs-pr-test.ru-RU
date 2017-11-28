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
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="19d5c-104">Настройка отправки файлов в Центре Интернета вещей с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="19d5c-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="19d5c-105">toouse hello [файла функций передачи данных в центр IoT][lnk-upload], его необходимо связать учетную запись хранения Azure с вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="19d5c-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="19d5c-106">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="19d5c-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="19d5c-107">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="19d5c-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="19d5c-108">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5c-108">An active Azure account.</span></span> <span data-ttu-id="19d5c-109">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="19d5c-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="19d5c-110">[Командлеты Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="19d5c-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="19d5c-111">Центр интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5c-111">An Azure IoT hub.</span></span> <span data-ttu-id="19d5c-112">Если у вас нет центра IoT, можно использовать hello [командлет New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate один или используйте hello портала слишком[создать центр IoT] [ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="19d5c-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="19d5c-113">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5c-113">An Azure storage account.</span></span> <span data-ttu-id="19d5c-114">При отсутствии учетной записи хранилища Azure можно использовать hello [командлеты PowerShell хранилища Azure] [ lnk-powershell-storage] toocreate один или используйте hello портала слишком[создать учетную запись хранилища] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="19d5c-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="19d5c-115">Выполнение входа и установка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="19d5c-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="19d5c-116">Войдите в tooyour учетная запись Azure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="19d5c-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="19d5c-117">В командной строке PowerShell hello, запустите hello **AzureRmAccount входа** командлета:</span><span class="sxs-lookup"><span data-stu-id="19d5c-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="19d5c-118">Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello подписок Azure, связанных с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="19d5c-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="19d5c-119">Используйте следующую команду, toolist hello подписки Azure доступны для вас toouse hello.</span><span class="sxs-lookup"><span data-stu-id="19d5c-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="19d5c-120">Используется следующая команда tooselect подписки требуется toouse toorun hello команды toomanage концентратор IoT hello.</span><span class="sxs-lookup"><span data-stu-id="19d5c-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="19d5c-121">Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:</span><span class="sxs-lookup"><span data-stu-id="19d5c-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="19d5c-122">Получение сведений об учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="19d5c-122">Retrieve your storage account details</span></span>

<span data-ttu-id="19d5c-123">Hello следующие шаги предполагают, что вы создали учетную запись хранилища с помощью hello **диспетчера ресурсов** модель развертывания, а не hello **классический** модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="19d5c-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="19d5c-124">отправляет файл tooconfigure с устройств, необходимо hello строку подключения для учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="19d5c-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="19d5c-125">Учетная запись хранения Hello должна быть в hello той же подписке, ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="19d5c-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="19d5c-126">Необходимо также hello имя контейнера BLOB-объектов в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="19d5c-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="19d5c-127">Используйте следующие команды tooretrieve hello ключи учетной записи хранилища:</span><span class="sxs-lookup"><span data-stu-id="19d5c-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="19d5c-128">Запишите hello **key1** значение ключа учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="19d5c-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="19d5c-129">Необходимо в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="19d5c-129">You need it in hello following steps.</span></span>

<span data-ttu-id="19d5c-130">Для отправки файлов можно использовать существующий контейнер BLOB-объектов или создать новый.</span><span class="sxs-lookup"><span data-stu-id="19d5c-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="19d5c-131">toolist hello существующие BLOB-объект контейнеры в учетной записи используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="19d5c-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="19d5c-132">toocreate контейнер больших двоичных объектов в вашей учетной записи хранилища, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="19d5c-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="19d5c-133">Настройка Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="19d5c-133">Configure your IoT hub</span></span>

<span data-ttu-id="19d5c-134">Теперь вы можете настроить ваш tooenable концентратора IoT [файл функций передачи] [ lnk-upload] с помощью сведений о своей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="19d5c-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="19d5c-135">Конфигурация Hello требует hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="19d5c-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="19d5c-136">**Контейнер хранилища**: контейнер больших двоичных объектов в учетной записи хранилища Azure в вашей текущей подписки Azure tooassociate с вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="19d5c-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="19d5c-137">Вы получили сведения об учетной записи хранилище hello в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="19d5c-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="19d5c-138">Центр IoT автоматически создает идентификаторы URI SAS с контейнер больших двоичных объектов toothis разрешения записи для устройств toouse, когда они отправляют файлы.</span><span class="sxs-lookup"><span data-stu-id="19d5c-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="19d5c-139">**Receive notifications for uploaded files** (Получать уведомления об отправленных файлах). Включите или отключите уведомления об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="19d5c-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="19d5c-140">**Срок ЖИЗНИ SAS**: этот параметр — hello, время жизни объекта hello идентификаторы URI SAS возвращенных toohello устройства центра IoT.</span><span class="sxs-lookup"><span data-stu-id="19d5c-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="19d5c-141">По умолчанию значение tooone час.</span><span class="sxs-lookup"><span data-stu-id="19d5c-141">Set tooone hour by default.</span></span>

<span data-ttu-id="19d5c-142">**Уведомления об параметры по умолчанию срок ЖИЗНИ файла**: hello time-to-live уведомления передачи файла до окончания срока их.</span><span class="sxs-lookup"><span data-stu-id="19d5c-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="19d5c-143">По умолчанию значение tooone день.</span><span class="sxs-lookup"><span data-stu-id="19d5c-143">Set tooone day by default.</span></span>

<span data-ttu-id="19d5c-144">**Файл уведомления максимальное число доставок**: hello время hello toodeliver попыток центра IoT уведомление передачи файла.</span><span class="sxs-lookup"><span data-stu-id="19d5c-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="19d5c-145">По умолчанию значение too10.</span><span class="sxs-lookup"><span data-stu-id="19d5c-145">Set too10 by default.</span></span>

<span data-ttu-id="19d5c-146">Используйте следующие параметры для передачи PowerShell командлет tooconfigure hello файла на ваш центр IoT hello.</span><span class="sxs-lookup"><span data-stu-id="19d5c-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="19d5c-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19d5c-147">Next steps</span></span>

<span data-ttu-id="19d5c-148">Дополнительные сведения о возможности передачи файлов hello центра IoT см. в разделе [передачи файлов на устройстве][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="19d5c-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="19d5c-149">Выполните эти дополнительные сведения об управлении центр IoT Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="19d5c-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="19d5c-150">[Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="19d5c-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="19d5c-151">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="19d5c-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="19d5c-152">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="19d5c-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="19d5c-153">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="19d5c-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="19d5c-154">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="19d5c-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="19d5c-155">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="19d5c-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="19d5c-156">[Защита вашего решения IoT из hello основание,][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="19d5c-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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