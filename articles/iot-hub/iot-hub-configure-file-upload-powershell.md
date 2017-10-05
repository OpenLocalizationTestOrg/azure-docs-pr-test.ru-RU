---
title: "Использование Azure PowerShell для настройки отправки файлов | Документация Майкрософт"
description: "В этой статье рассказывается, как с помощью командлетов Azure PowerShell настроить Центр Интернета вещей, чтобы включить отправку файлов с подключенных устройств. Содержит сведения о настройке целевой учетной записи хранения Azure."
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
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="d2e29-104">Настройка отправки файлов в Центре Интернета вещей с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2e29-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="d2e29-105">Чтобы использовать [функцию передачи файлов в Центре Интернета вещей][lnk-upload], сначала необходимо связать учетную запись хранения Azure с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="d2e29-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="d2e29-106">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="d2e29-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="d2e29-107">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="d2e29-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d2e29-108">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d2e29-108">An active Azure account.</span></span> <span data-ttu-id="d2e29-109">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d2e29-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="d2e29-110">[Командлеты Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="d2e29-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="d2e29-111">Центр интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="d2e29-111">An Azure IoT hub.</span></span> <span data-ttu-id="d2e29-112">[Создать Центр Интернета вещей][lnk-portal-hub] (если у вас его еще нет) можно с помощью [командлета New-AzureRmIoTHub][lnk-powershell-iothub] или на портале.</span><span class="sxs-lookup"><span data-stu-id="d2e29-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="d2e29-113">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="d2e29-113">An Azure storage account.</span></span> <span data-ttu-id="d2e29-114">[Создать учетную запись хранения][lnk-portal-storage] Azure (если у вас ее еще нет) можно с помощью [командлетов PowerShell службы хранилища Azure][lnk-powershell-storage] или на портале.</span><span class="sxs-lookup"><span data-stu-id="d2e29-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="d2e29-115">Выполнение входа и установка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="d2e29-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="d2e29-116">Войдите в учетную запись Azure и выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="d2e29-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="d2e29-117">В командной строке PowerShell выполните командлет **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="d2e29-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="d2e29-118">Если у вас есть несколько подписок Azure, то при входе в Azure вы получите доступ ко всем подпискам Azure, связанным с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="d2e29-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="d2e29-119">Используйте следующую команду, чтобы просмотреть подписки Azure, доступные для использования:</span><span class="sxs-lookup"><span data-stu-id="d2e29-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="d2e29-120">Используйте следующую команду, чтобы выбрать подписку, с помощью которой будут выполняться команды для управления Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="d2e29-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="d2e29-121">Вы можете использовать имя подписки или идентификатор из выходных данных предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="d2e29-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="d2e29-122">Получение сведений об учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="d2e29-122">Retrieve your storage account details</span></span>

<span data-ttu-id="d2e29-123">В следующих шагах предполагается, что для создания учетной записи хранения вы использовали модель развертывания **с помощью Resource Manager**, а не **классическую** модель развертывания.</span><span class="sxs-lookup"><span data-stu-id="d2e29-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="d2e29-124">Для настройки отправки файлов с ваших устройств необходима строка подключения учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="d2e29-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="d2e29-125">Эта учетная запись хранения должна относиться к той же подписке, что и Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="d2e29-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="d2e29-126">Кроме того, вам понадобится имя контейнера BLOB-объектов в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d2e29-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="d2e29-127">Для получения ключей учетной записи хранения используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2e29-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="d2e29-128">Запишите значение ключа **key1** учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d2e29-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="d2e29-129">Оно понадобится вам на следующих этапах.</span><span class="sxs-lookup"><span data-stu-id="d2e29-129">You need it in the following steps.</span></span>

<span data-ttu-id="d2e29-130">Для отправки файлов можно использовать существующий контейнер BLOB-объектов или создать новый.</span><span class="sxs-lookup"><span data-stu-id="d2e29-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="d2e29-131">Чтобы получить список существующих контейнеров BLOB-объектов в вашей учетной записи хранения, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="d2e29-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="d2e29-132">Для создания контейнера BLOB-объектов в учетной записи хранения используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="d2e29-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="d2e29-133">Настройка Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="d2e29-133">Configure your IoT hub</span></span>

<span data-ttu-id="d2e29-134">Теперь с помощью данных учетной записи хранения можно настроить Центр Интернета вещей для включения [функции отправки файлов][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="d2e29-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="d2e29-135">Для настройки потребуются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d2e29-135">The configuration requires the following values:</span></span>

<span data-ttu-id="d2e29-136">**Контейнер хранилища**. Контейнер BLOB-объектов в учетной записи хранения Azure в текущей подписке Azure, который нужно связать с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="d2e29-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="d2e29-137">Необходимые сведения об учетной записи хранения вы получили в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="d2e29-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="d2e29-138">Центр Интернета вещей автоматически генерирует универсальные коды ресурсов (URI) подписанных URL-адресов с разрешениями на запись в этом контейнере больших двоичных объектов, чтобы устройства могли их использовать во время передач файлов.</span><span class="sxs-lookup"><span data-stu-id="d2e29-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="d2e29-139">**Receive notifications for uploaded files** (Получать уведомления об отправленных файлах). Включите или отключите уведомления об отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="d2e29-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="d2e29-140">**SAS TTL** (Срок жизни SAS). Этот параметр определяет срок жизни универсальных кодов ресурса (URI) SAS, возвращаемых Центром Интернета вещей на устройство.</span><span class="sxs-lookup"><span data-stu-id="d2e29-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="d2e29-141">Значение по умолчанию — один час.</span><span class="sxs-lookup"><span data-stu-id="d2e29-141">Set to one hour by default.</span></span>

<span data-ttu-id="d2e29-142">**File notification settings default TTL** (Стандартный срок жизни уведомления о файле). Срок жизни уведомления об отправке файла.</span><span class="sxs-lookup"><span data-stu-id="d2e29-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="d2e29-143">Значение по умолчанию — один день.</span><span class="sxs-lookup"><span data-stu-id="d2e29-143">Set to one day by default.</span></span>

<span data-ttu-id="d2e29-144">**File notification maximum delivery count**(Максимальное число доставок уведомления о файле): число попыток доставки уведомления о передаче файла, предпринимаемых Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="d2e29-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="d2e29-145">Значение по умолчанию — 10.</span><span class="sxs-lookup"><span data-stu-id="d2e29-145">Set to 10 by default.</span></span>

<span data-ttu-id="d2e29-146">Чтобы настроить параметры отправки файлов в Центре Интернета вещей, используйте следующий командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d2e29-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d2e29-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2e29-147">Next steps</span></span>

<span data-ttu-id="d2e29-148">Дополнительные сведения о возможностях Центра Интернета вещей, касающихся отправки файлов, см. в разделе об [отправке файлов с устройства][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="d2e29-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="d2e29-149">Дополнительные сведения об управлении Центром Интернета вещей в Azure см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="d2e29-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="d2e29-150">[Массовое управление удостоверениями устройств Центра Интернета вещей][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="d2e29-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="d2e29-151">[Метрики Центра Интернета вещей][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="d2e29-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="d2e29-152">[Мониторинг операций][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="d2e29-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="d2e29-153">Для дальнейшего изучения возможностей Центра Интернета вещей см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="d2e29-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d2e29-154">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d2e29-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d2e29-155">[Simulating a device with IoT Edge][lnk-iotedge] (Моделирование устройства с помощью Edge Интернета вещей)</span><span class="sxs-lookup"><span data-stu-id="d2e29-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="d2e29-156">[Все аспекты безопасности решения Центра Интернета вещей][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="d2e29-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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