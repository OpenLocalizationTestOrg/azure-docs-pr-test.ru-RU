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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="be8d8-103">Настройка отправки файлов в Центре Интернета вещей с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="be8d8-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="be8d8-104">toouse hello [файла функций передачи данных в центр IoT][lnk-upload], его необходимо связать учетную запись хранилища Azure с вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="be8d8-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="be8d8-105">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="be8d8-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="be8d8-106">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="be8d8-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="be8d8-107">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="be8d8-107">An active Azure account.</span></span> <span data-ttu-id="be8d8-108">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="be8d8-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="be8d8-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="be8d8-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="be8d8-110">Центр интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="be8d8-110">An Azure IoT hub.</span></span> <span data-ttu-id="be8d8-111">При отсутствии центра IoT можно использовать hello `az iot hub create` [команда] [ lnk-cli-create-iothub] toocreate один или используйте hello портала слишком [создать центр IoT] [lnk портала концентратора].</span><span class="sxs-lookup"><span data-stu-id="be8d8-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="be8d8-112">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="be8d8-112">An Azure Storage account.</span></span> <span data-ttu-id="be8d8-113">При отсутствии учетной записи хранилища Azure можно использовать hello [Azure CLI 2.0 — управление учетными записями хранения] [ lnk-manage-storage] toocreate одно или используйте hello портала слишком[создать учетную запись хранилища] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="be8d8-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="be8d8-114">Выполнение входа и установка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="be8d8-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="be8d8-115">Войдите в tooyour учетная запись Azure и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="be8d8-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="be8d8-116">Hello командной строки, выполнив hello [входа команда][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="be8d8-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="be8d8-117">Выполните инструкции tooauthenticate hello, с помощью кода hello и войдите в tooyour учетная запись Azure через веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="be8d8-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="be8d8-118">Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello Azure учетные записи, связанные с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="be8d8-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="be8d8-119">Используйте следующие hello [toolist команда hello учетных записей Azure] [ lnk-az-account-command] для toouse вы:</span><span class="sxs-lookup"><span data-stu-id="be8d8-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="be8d8-120">Используется следующая команда tooselect подписки требуется toouse toorun hello команды toocreate концентратор IoT hello.</span><span class="sxs-lookup"><span data-stu-id="be8d8-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="be8d8-121">Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:</span><span class="sxs-lookup"><span data-stu-id="be8d8-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="be8d8-122">Получение сведений об учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="be8d8-122">Retrieve your storage account details</span></span>

<span data-ttu-id="be8d8-123">Hello следующие шаги предполагают, что вы создали учетную запись хранилища с помощью hello **диспетчера ресурсов** модель развертывания, а не hello **классический** модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="be8d8-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="be8d8-124">отправляет файл tooconfigure с устройств, необходимо hello строку подключения для учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="be8d8-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="be8d8-125">Учетная запись хранения Hello должна быть в hello той же подписке, ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="be8d8-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="be8d8-126">Необходимо также hello имя контейнера BLOB-объектов в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="be8d8-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="be8d8-127">Используйте следующие команды tooretrieve hello ключи учетной записи хранилища:</span><span class="sxs-lookup"><span data-stu-id="be8d8-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="be8d8-128">Запишите hello **connectionString** значение.</span><span class="sxs-lookup"><span data-stu-id="be8d8-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="be8d8-129">Необходимо в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="be8d8-129">You need it in hello following steps.</span></span>

<span data-ttu-id="be8d8-130">Для отправки файлов можно использовать существующий контейнер BLOB-объектов или создать новый.</span><span class="sxs-lookup"><span data-stu-id="be8d8-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="be8d8-131">toolist hello существующие BLOB-объект контейнеры в учетной записи используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="be8d8-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="be8d8-132">toocreate контейнер больших двоичных объектов в вашей учетной записи хранилища, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="be8d8-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="be8d8-133">Передача файла</span><span class="sxs-lookup"><span data-stu-id="be8d8-133">File upload</span></span>

<span data-ttu-id="be8d8-134">Теперь вы можете настроить ваш tooenable концентратора IoT [файл функций передачи] [ lnk-upload] с помощью сведений о своей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="be8d8-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="be8d8-135">Конфигурация Hello требует hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="be8d8-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="be8d8-136">**Контейнер хранилища**: контейнер больших двоичных объектов в учетной записи хранилища Azure в вашей текущей подписки Azure tooassociate с вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="be8d8-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="be8d8-137">Вы получили сведения об учетной записи хранилище hello в предшествующих раздел hello.</span><span class="sxs-lookup"><span data-stu-id="be8d8-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="be8d8-138">Центр IoT автоматически создает идентификаторы URI SAS с контейнер больших двоичных объектов toothis разрешения записи для устройств toouse, когда они отправляют файлы.</span><span class="sxs-lookup"><span data-stu-id="be8d8-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="be8d8-139">**Receive notifications for uploaded files** (Получать уведомления об отправленных файлах). Включите или отключите уведомления об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="be8d8-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="be8d8-140">**Срок ЖИЗНИ SAS**: этот параметр — hello, время жизни объекта hello идентификаторы URI SAS возвращенных toohello устройства центра IoT.</span><span class="sxs-lookup"><span data-stu-id="be8d8-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="be8d8-141">По умолчанию значение tooone час.</span><span class="sxs-lookup"><span data-stu-id="be8d8-141">Set tooone hour by default.</span></span>

<span data-ttu-id="be8d8-142">**Уведомления об параметры по умолчанию срок ЖИЗНИ файла**: hello time-to-live уведомления передачи файла до окончания срока их.</span><span class="sxs-lookup"><span data-stu-id="be8d8-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="be8d8-143">По умолчанию значение tooone день.</span><span class="sxs-lookup"><span data-stu-id="be8d8-143">Set tooone day by default.</span></span>

<span data-ttu-id="be8d8-144">**Файл уведомления максимальное число доставок**: hello время hello toodeliver попыток центра IoT уведомление передачи файла.</span><span class="sxs-lookup"><span data-stu-id="be8d8-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="be8d8-145">По умолчанию значение too10.</span><span class="sxs-lookup"><span data-stu-id="be8d8-145">Set too10 by default.</span></span>

<span data-ttu-id="be8d8-146">Используйте следующие параметры передачи файла hello tooconfigure Azure CLI команды на концентратор IoT hello.</span><span class="sxs-lookup"><span data-stu-id="be8d8-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="be8d8-147">Выполните следующие команды в оболочке Bash:</span><span class="sxs-lookup"><span data-stu-id="be8d8-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="be8d8-148">В командной строке Windows выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="be8d8-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="be8d8-149">Вы можете просмотреть hello конфигурации загрузки файла на ваш центр IoT с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="be8d8-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="be8d8-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be8d8-150">Next steps</span></span>

<span data-ttu-id="be8d8-151">Дополнительные сведения о возможности передачи файлов hello центра IoT см. в разделе [передачи файлов на устройстве][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="be8d8-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="be8d8-152">Выполните эти дополнительные сведения об управлении центр IoT Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="be8d8-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="be8d8-153">[Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="be8d8-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="be8d8-154">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="be8d8-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="be8d8-155">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="be8d8-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="be8d8-156">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="be8d8-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="be8d8-157">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="be8d8-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="be8d8-158">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="be8d8-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="be8d8-159">[Защита вашего решения IoT из hello основание,][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="be8d8-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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