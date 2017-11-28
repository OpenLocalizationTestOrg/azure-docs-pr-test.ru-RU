---
title: "Использование шлюза Интернета вещей для подключения устройства к Центру Интернета вещей Azure | Документация Майкрософт"
description: "Узнайте, как использовать Intel NUC в качестве шлюза Интернета вещей для подключения TI SensorTag и отправлять данные датчиков в Центр Интернета вещей Azure в облаке."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "шлюз Интернета вещей для подключения устройства к облаку"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 4fb77ed0241d15338c2574fd22828507c3e40cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="8a711-104">Использование шлюза Интернета вещей для подключения объектов к облаку (подключение SensorTag к Центру Интернета вещей Azure)</span><span class="sxs-lookup"><span data-stu-id="8a711-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="8a711-105">Перед началом работы с руководством убедитесь, что вы завершили [настройку Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="8a711-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="8a711-106">Из учебника [Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) вы узнали, как настроить устройство Intel NUC таким образом.</span><span class="sxs-lookup"><span data-stu-id="8a711-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8a711-107">Новые знания</span><span class="sxs-lookup"><span data-stu-id="8a711-107">What you will learn</span></span>

<span data-ttu-id="8a711-108">Вы научитесь использовать шлюз Интернета вещей для подключения устройства Texas Instruments SensorTag (CC2650STK) к Центру Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="8a711-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="8a711-109">Шлюз Центра Интернета вещей отправляет данные о температуре и влажности, собранные с устройства SensorTag, в Центр Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="8a711-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8a711-110">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="8a711-110">What you will do</span></span>

- <span data-ttu-id="8a711-111">Создайте центр IoT.</span><span class="sxs-lookup"><span data-stu-id="8a711-111">Create an IoT hub.</span></span>
- <span data-ttu-id="8a711-112">Зарегистрируйте устройство в Центре Интернета вещей для SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8a711-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="8a711-113">Включите подключение между шлюзом Интернета вещей и SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8a711-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="8a711-114">Запустите пример приложения BLE для отправки данных SensorTag в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8a711-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="8a711-115">What you need</span></span>

- <span data-ttu-id="8a711-116">Пройден учебник [Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), в котором рассказывается, как настроить устройство Intel NUC в качестве шлюза Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="8a711-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="8a711-117">An active Azure subscription.</span></span> <span data-ttu-id="8a711-118">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8a711-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="8a711-119">Клиент SSH, который выполняется на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8a711-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="8a711-120">В Windows рекомендуется использовать PuTTY.</span><span class="sxs-lookup"><span data-stu-id="8a711-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="8a711-121">Клиент SSH изначально входит в состав ОС Linux и Mac OS.</span><span class="sxs-lookup"><span data-stu-id="8a711-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="8a711-122">IP-адрес, имя пользователя и пароль для доступа к шлюзу из клиента SSH.</span><span class="sxs-lookup"><span data-stu-id="8a711-122">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="8a711-123">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="8a711-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="8a711-124">Здесь следует зарегистрировать новое устройство для SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8a711-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="8a711-125">Включение подключения между шлюзом Интернета вещей и SensorTag</span><span class="sxs-lookup"><span data-stu-id="8a711-125">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="8a711-126">В этом разделе описывается выполнение следующих задач:</span><span class="sxs-lookup"><span data-stu-id="8a711-126">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="8a711-127">Получите MAC-адрес SensorTag для подключения Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="8a711-127">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="8a711-128">Инициируйте подключение Bluetooth из шлюза Интернета вещей к SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8a711-128">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="8a711-129">Получение MAC-адреса SensorTag для подключения Bluetooth</span><span class="sxs-lookup"><span data-stu-id="8a711-129">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="8a711-130">На главном компьютере запустите клиент SSH и установите подключение к шлюзу Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-130">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="8a711-131">Разблокируйте Bluetooth, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a711-131">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="8a711-132">Запустите службу Bluetooth на шлюзе Интернета вещей и войдите в оболочку Bluetooth для настройки Bluetooth, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="8a711-132">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="8a711-133">Включите питание на контроллере Bluetooth, выполнив следующую команду в оболочке Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="8a711-133">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![Включение питания на контроллере Bluetooth в шлюзе Интернета вещей с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="8a711-135">Начните поиск находящихся поблизости устройств Bluetooth, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a711-135">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![Поиск находящихся поблизости устройств Bluetooth с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="8a711-137">Нажмите кнопку связывания на SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8a711-137">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="8a711-138">На SensorTag начнет мигать зеленый индикатор.</span><span class="sxs-lookup"><span data-stu-id="8a711-138">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="8a711-139">В оболочке Bluetooth должно отобразиться найденное устройство SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8a711-139">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="8a711-140">Запишите MAC-адрес устройства SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8a711-140">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="8a711-141">В данном примере MAC-адрес устройства SensorTag — `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="8a711-141">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="8a711-142">Выключите поиск, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a711-142">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![Остановка поиска находящихся поблизости устройств Bluetooth с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="8a711-144">Инициализация подключения Bluetooth к SensorTag из шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8a711-144">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="8a711-145">Подключитесь к SensorTag с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="8a711-145">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Подключение к SensorTag с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="8a711-147">Отключитесь от SensorTag и выйдите из оболочки Bluetooth с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="8a711-147">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Отключение от SensorTag с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="8a711-149">Вы успешно включили подключение между SensorTag и шлюзом Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-149">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="8a711-150">Запуск примера приложения BLE для отправки данных SensorTag в Центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8a711-150">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="8a711-151">Пример приложения для подключения по Bluetooth с низким энергопотреблением (BLE) предоставляется в Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="8a711-151">The Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="8a711-152">Этот пример приложения собирает данные, поступающие через подключение BLE, и отправляет их в центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-152">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="8a711-153">Для запуска примера приложения необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8a711-153">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="8a711-154">настроить пример приложения;</span><span class="sxs-lookup"><span data-stu-id="8a711-154">Configure the sample application.</span></span>
1. <span data-ttu-id="8a711-155">запустить его на шлюзе Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-155">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="8a711-156">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="8a711-156">Configure the sample application</span></span>

1. <span data-ttu-id="8a711-157">Перейдите в папку примера приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a711-157">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="8a711-158">Откройте файл конфигурации, выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="8a711-158">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="8a711-159">В файле конфигурации задайте такие значения:</span><span class="sxs-lookup"><span data-stu-id="8a711-159">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="8a711-160">**IoTHubName** — имя Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-160">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="8a711-161">**IoTHubSuffix** — получение IoTHubSuffix из первичного ключа в записанной ранее строке подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="8a711-161">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="8a711-162">Убедитесь, что вы используете первичный ключ из строки подключения устройства, а не из строки подключения Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-162">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="8a711-163">Первичный ключ строки подключения устройства указывается в формате `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="8a711-163">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="8a711-164">**Transport** По умолчанию используется значение `amqp`.</span><span class="sxs-lookup"><span data-stu-id="8a711-164">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="8a711-165">Это значение указывает протокол во время транспортировки.</span><span class="sxs-lookup"><span data-stu-id="8a711-165">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="8a711-166">Оно может быть равным `http`, `amqp` или `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="8a711-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="8a711-167">**macAddress** MAC-адрес SensorTag, который вы записали ранее.</span><span class="sxs-lookup"><span data-stu-id="8a711-167">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="8a711-168">**deviceID** Идентификатор устройства, которое вы создали в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8a711-168">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="8a711-169">**deviceKey** Первичный ключ строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="8a711-169">**deviceKey**: The primary key of the device connection string.</span></span>

   ![Заполнение файла конфигурации примера приложения BLE](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="8a711-171">Нажмите клавишу `ESC` и введите `:wq`, чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="8a711-171">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="8a711-172">Запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="8a711-172">Run the sample application</span></span>

1. <span data-ttu-id="8a711-173">Убедитесь, что устройство SensorTag включено.</span><span class="sxs-lookup"><span data-stu-id="8a711-173">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="8a711-174">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a711-174">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="8a711-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a711-175">Next steps</span></span>

[<span data-ttu-id="8a711-176">Использование шлюза Интернета вещей для преобразования данных датчиков с помощью Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="8a711-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
