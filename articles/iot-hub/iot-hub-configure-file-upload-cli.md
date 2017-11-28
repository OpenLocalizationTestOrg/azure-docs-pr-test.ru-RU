---
title: "Настройка отправки файлов в Центр Интернета вещей с помощью Azure CLI (az.py) | Документация Майкрософт"
description: "Настройка отправки файлов в Центр Интернета вещей Azure, используя кроссплатформенный интерфейс командной строки Azure 2.0 (az.py)."
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
ms.openlocfilehash: a9af26d7ebacf5513952786621aaa92f64be263b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="50427-103">Настройка отправки файлов в Центре Интернета вещей с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="50427-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="50427-104">Чтобы использовать [функцию передачи файлов в Центре Интернета вещей][lnk-upload], сначала необходимо связать учетную запись хранения Azure с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="50427-104">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="50427-105">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="50427-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="50427-106">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="50427-106">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="50427-107">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="50427-107">An active Azure account.</span></span> <span data-ttu-id="50427-108">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="50427-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="50427-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="50427-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="50427-110">Центр интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="50427-110">An Azure IoT hub.</span></span> <span data-ttu-id="50427-111">Выполните [команду][lnk-cli-create-iothub] `az iot hub create` или воспользуйтесь порталом Azure, чтобы создать Центр Интернета вещей (если у вас его еще нет) [lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="50427-111">If you don't have an IoT hub, you can use the `az iot hub create` [command][lnk-cli-create-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="50427-112">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="50427-112">An Azure Storage account.</span></span> <span data-ttu-id="50427-113">Ознакомьтесь со сведениями раздела [Управление учетными записями хранения][lnk-manage-storage] или воспользуйтесь порталом, чтобы [создать учетную запись хранения Azure][lnk-portal-storage] (если у вас ее еще нет).</span><span class="sxs-lookup"><span data-stu-id="50427-113">If you don't have an Azure Storage account, you can use the [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="50427-114">Выполнение входа и установка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="50427-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="50427-115">Войдите в учетную запись Azure и выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="50427-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="50427-116">В командной строке запустите [команду для входа][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="50427-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="50427-117">Следуйте инструкциям, чтобы выполнить аутентификацию с использованием кода и войти в учетную запись Azure через веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="50427-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

1. <span data-ttu-id="50427-118">Если у вас есть несколько подписок Azure, то при выполнении входа в Azure вы получаете доступ ко всем учетным записям Azure, связанным с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="50427-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="50427-119">Используйте следующую [команду для вывода учетных записей Azure][lnk-az-account-command], доступных для использования:</span><span class="sxs-lookup"><span data-stu-id="50427-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="50427-120">Используйте следующую команду, чтобы выбрать подписку, которая будет использоваться для выполнения команд для создания Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="50427-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="50427-121">Вы можете использовать имя подписки или идентификатор из выходных данных предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="50427-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="50427-122">Получение сведений об учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="50427-122">Retrieve your storage account details</span></span>

<span data-ttu-id="50427-123">В следующих шагах предполагается, что для создания учетной записи хранения вы использовали модель развертывания **с помощью Resource Manager**, а не **классическую** модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="50427-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="50427-124">Для настройки отправки файлов с ваших устройств необходима строка подключения учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="50427-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="50427-125">Эта учетная запись хранения должна относиться к той же подписке, что и Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="50427-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="50427-126">Кроме того, вам понадобится имя контейнера BLOB-объектов в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="50427-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="50427-127">Для получения ключей учетной записи хранения используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50427-127">Use the following command to retrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="50427-128">Запишите значение **connectionString**.</span><span class="sxs-lookup"><span data-stu-id="50427-128">Make a note of the **connectionString** value.</span></span> <span data-ttu-id="50427-129">Оно понадобится вам на следующих этапах.</span><span class="sxs-lookup"><span data-stu-id="50427-129">You need it in the following steps.</span></span>

<span data-ttu-id="50427-130">Для отправки файлов можно использовать существующий контейнер BLOB-объектов или создать новый.</span><span class="sxs-lookup"><span data-stu-id="50427-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="50427-131">Чтобы получить список имеющихся контейнеров больших двоичных объектов в вашей учетной записи хранения, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50427-131">To list the existing blob containers in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="50427-132">Для создания контейнера больших двоичных объектов в учетной записи хранения выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50427-132">To create a blob container in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="50427-133">Передача файла</span><span class="sxs-lookup"><span data-stu-id="50427-133">File upload</span></span>

<span data-ttu-id="50427-134">Теперь с помощью данных учетной записи хранения можно настроить Центр Интернета вещей для включения [функции отправки файлов][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="50427-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="50427-135">Для настройки потребуются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="50427-135">The configuration requires the following values:</span></span>

<span data-ttu-id="50427-136">**Контейнер хранилища**. Контейнер BLOB-объектов в учетной записи хранения Azure в текущей подписке Azure, который нужно связать с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="50427-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="50427-137">Необходимые сведения об учетной записи хранения вы получили в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="50427-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="50427-138">Центр Интернета вещей автоматически генерирует универсальные коды ресурсов (URI) подписанных URL-адресов с разрешениями на запись в этом контейнере больших двоичных объектов, чтобы устройства могли их использовать во время передач файлов.</span><span class="sxs-lookup"><span data-stu-id="50427-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="50427-139">**Receive notifications for uploaded files** (Получать уведомления об отправленных файлах). Включите или отключите уведомления об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="50427-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="50427-140">**SAS TTL** (Срок жизни SAS). Этот параметр определяет срок жизни универсальных кодов ресурса (URI) SAS, возвращаемых Центром Интернета вещей на устройство.</span><span class="sxs-lookup"><span data-stu-id="50427-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="50427-141">Значение по умолчанию — один час.</span><span class="sxs-lookup"><span data-stu-id="50427-141">Set to one hour by default.</span></span>

<span data-ttu-id="50427-142">**File notification settings default TTL** (Стандартный срок жизни уведомления о файле). Срок жизни уведомления об отправке файла.</span><span class="sxs-lookup"><span data-stu-id="50427-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="50427-143">Значение по умолчанию — один день.</span><span class="sxs-lookup"><span data-stu-id="50427-143">Set to one day by default.</span></span>

<span data-ttu-id="50427-144">**File notification maximum delivery count**(Максимальное число доставок уведомления о файле): число попыток доставки уведомления о передаче файла, предпринимаемых Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="50427-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="50427-145">Значение по умолчанию — 10.</span><span class="sxs-lookup"><span data-stu-id="50427-145">Set to 10 by default.</span></span>

<span data-ttu-id="50427-146">Чтобы настроить параметры отправки файлов в Центре Интернета вещей, выполните следующие команды Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="50427-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span></span>

<span data-ttu-id="50427-147">Выполните следующие команды в оболочке Bash:</span><span class="sxs-lookup"><span data-stu-id="50427-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="50427-148">В командной строке Windows выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="50427-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="50427-149">Вы можете просмотреть конфигурацию отправки файла в Центре Интернета вещей, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="50427-149">You can review the file upload configuration on your IoT hub using the following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="50427-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50427-150">Next steps</span></span>

<span data-ttu-id="50427-151">Дополнительные сведения о возможностях Центра Интернета вещей, касающихся отправки файлов, см. в разделе об [отправке файлов с устройства][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="50427-151">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="50427-152">Дополнительные сведения об управлении Центром Интернета вещей в Azure см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="50427-152">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="50427-153">[Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="50427-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="50427-154">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="50427-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="50427-155">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="50427-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="50427-156">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="50427-156">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="50427-157">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="50427-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="50427-158">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="50427-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="50427-159">[Все аспекты безопасности решения Центра Интернета вещей][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="50427-159">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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