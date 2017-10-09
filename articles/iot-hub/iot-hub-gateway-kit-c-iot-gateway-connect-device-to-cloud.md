---
title: "aaaUse tooconnect шлюза IoT tooAzure устройства центра IoT | Документы Microsoft"
description: "Дополнительные сведения об облачных toouse NUC Intel как tooconnect шлюза IoT TI SensorTag и датчик отправки данных tooAzure центр IoT в hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "шлюз IOT подключаться toocloud устройства"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="32402-104">Использование облачного toohello действия tooconnect шлюза IoT - SensorTag tooAzure центра IoT</span><span class="sxs-lookup"><span data-stu-id="32402-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="32402-105">Перед началом работы с руководством убедитесь, что вы завершили [настройку Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="32402-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="32402-106">В [Настройка NUC Intel виде шлюза IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), настроить устройство Intel NUC hello как шлюз IoT.</span><span class="sxs-lookup"><span data-stu-id="32402-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="32402-107">Новые знания</span><span class="sxs-lookup"><span data-stu-id="32402-107">What you will learn</span></span>

<span data-ttu-id="32402-108">Вы узнаете, как toouse tooconnect шлюза IoT SensorTag инструментов Техас (CC2650STK) tooAzure центр IoT.</span><span class="sxs-lookup"><span data-stu-id="32402-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="32402-109">шлюз IoT Hello отправляет температуры и влажности собранные данные hello SensorTag tooAzure центр IoT.</span><span class="sxs-lookup"><span data-stu-id="32402-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="32402-110">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="32402-110">What you will do</span></span>

- <span data-ttu-id="32402-111">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="32402-111">Create an IoT hub.</span></span>
- <span data-ttu-id="32402-112">Регистрация устройства в центр IoT hello для hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="32402-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="32402-113">Включите hello подключение между шлюзом IoT hello и hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="32402-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="32402-114">Запустите ЛЮЧИТЬ образец приложения toosend SensorTag данные tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="32402-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="32402-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="32402-115">What you need</span></span>

- <span data-ttu-id="32402-116">Пройден учебник [Настройка Intel NUC в качестве шлюза Интернета вещей](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), в котором рассказывается, как настроить устройство Intel NUC в качестве шлюза Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="32402-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="32402-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="32402-117">An active Azure subscription.</span></span> <span data-ttu-id="32402-118">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="32402-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="32402-119">Клиент SSH, который выполняется на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="32402-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="32402-120">В Windows рекомендуется использовать PuTTY.</span><span class="sxs-lookup"><span data-stu-id="32402-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="32402-121">Клиент SSH изначально входит в состав ОС Linux и Mac OS.</span><span class="sxs-lookup"><span data-stu-id="32402-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="32402-122">Hello IP-адрес и hello имя пользователя и пароль tooaccess hello шлюза из клиента SSH hello.</span><span class="sxs-lookup"><span data-stu-id="32402-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="32402-123">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="32402-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="32402-124">Здесь следует зарегистрировать новое устройство для SensorTag.</span><span class="sxs-lookup"><span data-stu-id="32402-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="32402-125">Включить hello подключение между шлюзом IoT hello и hello SensorTag</span><span class="sxs-lookup"><span data-stu-id="32402-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="32402-126">В этом разделе выполните следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="32402-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="32402-127">Получение hello MAC-адрес hello SensorTag для подключения Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="32402-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="32402-128">Инициируйте подключение Bluetooth из hello IoT шлюза toohello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="32402-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="32402-129">Получить hello MAC-адрес hello SensorTag для подключение Bluetooth</span><span class="sxs-lookup"><span data-stu-id="32402-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="32402-130">На главном компьютере hello запустите клиент SSH hello и шлюз IoT toohello подключения.</span><span class="sxs-lookup"><span data-stu-id="32402-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="32402-131">Разблокируйте Bluetooth, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="32402-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="32402-132">Запустите службу hello Bluetooth на шлюз IoT hello и введите tooconfigure оболочки Bluetooth, hello Bluetooth, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="32402-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="32402-133">Питания на контроллере Bluetooth hello, запустив hello следующую команду в hello оболочки Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="32402-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![питания на контроллере Bluetooth hello в шлюзе hello IoT с bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="32402-135">Начните поиск ближайших устройствами Bluetooth, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="32402-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![Поиск находящихся поблизости устройств Bluetooth с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="32402-137">Нажмите клавишу связывание кнопки на hello SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="32402-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="32402-138">Hello зеленый ИНДИКАТОР на мигает SensorTag hello.</span><span class="sxs-lookup"><span data-stu-id="32402-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="32402-139">В hello оболочки Bluetooth вы увидите найден SensorTag приветствия.</span><span class="sxs-lookup"><span data-stu-id="32402-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="32402-140">Запишите hello hello SensorTag MAC-адрес.</span><span class="sxs-lookup"><span data-stu-id="32402-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="32402-141">В этом примере — hello MAC-адрес hello SensorTag `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="32402-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="32402-142">Отключите проверку hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="32402-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![Остановка поиска находящихся поблизости устройств Bluetooth с помощью bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="32402-144">Инициировать подключение Bluetooth из hello IoT шлюза toohello SensorTag</span><span class="sxs-lookup"><span data-stu-id="32402-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="32402-145">Подключитесь toohello SensorTag, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="32402-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Связь с bluetoothctl toohello SensorTag](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="32402-147">Отключитесь от hello SensorTag и выйти из оболочки Bluetooth hello, запустив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="32402-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Отключение от hello SensorTag с bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="32402-149">Hello подключению hello SensorTag hello IoT шлюза успешно активирован.</span><span class="sxs-lookup"><span data-stu-id="32402-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="32402-150">Запустите ЛЮЧИТЬ образец приложения toosend SensorTag данные tooyour центра IoT</span><span class="sxs-lookup"><span data-stu-id="32402-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="32402-151">энергии низкий Bluetooth (Разрешить) пример приложения Hello обеспечивается Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="32402-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="32402-152">Пример приложения Hello собирает данные от ЛЮЧИТЬ подключения и отправки центра IoT tooyou данных hello.</span><span class="sxs-lookup"><span data-stu-id="32402-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="32402-153">Пример приложения hello toorun, необходимо:</span><span class="sxs-lookup"><span data-stu-id="32402-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="32402-154">Настройте пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="32402-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="32402-155">Запустите образец приложения hello в шлюзе IoT hello.</span><span class="sxs-lookup"><span data-stu-id="32402-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="32402-156">Настройка образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="32402-156">Configure hello sample application</span></span>

1. <span data-ttu-id="32402-157">Go toohello папки образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="32402-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="32402-158">Откройте файл конфигурации hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="32402-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="32402-159">В файле конфигурации hello заполните hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="32402-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="32402-160">**IoTHubName**: hello имя вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="32402-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="32402-161">**IoTHubSuffix**: получение IoTHubSuffix из hello первичного ключа строки подключения устройства hello, отмеченный вниз.</span><span class="sxs-lookup"><span data-stu-id="32402-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="32402-162">Убедитесь, что получить первичный ключ строки подключения устройств hello hello, не hello первичного ключа в строке подключения концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="32402-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="32402-163">первичный ключ строки подключения устройств hello Hello указано в формате hello `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="32402-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="32402-164">**Транспорт**: hello значение по умолчанию — `amqp`.</span><span class="sxs-lookup"><span data-stu-id="32402-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="32402-165">Это значение показывает hello протокола во время transpotation.</span><span class="sxs-lookup"><span data-stu-id="32402-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="32402-166">Оно может быть равным `http`, `amqp` или `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="32402-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="32402-167">**macAddress**: hello MAC-адрес hello SensorTag, отмеченный вниз.</span><span class="sxs-lookup"><span data-stu-id="32402-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="32402-168">**deviceID**: идентификатор hello устройства, созданный в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="32402-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="32402-169">**deviceKey**: hello первичного ключа строки подключения устройств hello.</span><span class="sxs-lookup"><span data-stu-id="32402-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![Файл конфигурации завершения hello ЛЮЧИТЬ пример приложения hello](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="32402-171">Нажмите клавишу `ESC` и тип `:wq` toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="32402-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="32402-172">Запустить образец приложения hello</span><span class="sxs-lookup"><span data-stu-id="32402-172">Run hello sample application</span></span>

1. <span data-ttu-id="32402-173">Убедитесь, что включено SensorTag приветствия.</span><span class="sxs-lookup"><span data-stu-id="32402-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="32402-174">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="32402-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="32402-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32402-175">Next steps</span></span>

[<span data-ttu-id="32402-176">Использование шлюза Интернета вещей для преобразования данных датчиков с помощью Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="32402-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
