---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 3. Запуск примера приложения | Документация Майкрософт"
description: "Запустите пример приложения BLE для получения данных из BLE SensorTag и Центра Интернета вещей."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "приложение BLE, приложение мониторинга датчиков, сбор данных датчиков, данные датчиков, передача данных датчиков в облако"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="30c4e-104">Настройка и запуск примера приложения BLE</span><span class="sxs-lookup"><span data-stu-id="30c4e-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="30c4e-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="30c4e-105">What you will do</span></span>

- <span data-ttu-id="30c4e-106">Клонируйте репозиторий.</span><span class="sxs-lookup"><span data-stu-id="30c4e-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="30c4e-107">Настройте подключение между SensorTag и Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="30c4e-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="30c4e-108">Используйте Azure CLI для получения сведений о Центре Интернета вещей и SensorTag для примера приложения BLE (Bluetooth с низким энергопотреблением).</span><span class="sxs-lookup"><span data-stu-id="30c4e-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="30c4e-109">Настройте и запустите пример приложения BLE.</span><span class="sxs-lookup"><span data-stu-id="30c4e-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="30c4e-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="30c4e-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="30c4e-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="30c4e-111">What you will learn</span></span>

<span data-ttu-id="30c4e-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="30c4e-112">In this article, you will learn:</span></span>

- <span data-ttu-id="30c4e-113">Как настроить и запустить пример приложения BLE.</span><span class="sxs-lookup"><span data-stu-id="30c4e-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="30c4e-114">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="30c4e-114">What you need</span></span>

<span data-ttu-id="30c4e-115">Необходимо успешно выполнить инструкции, изложенные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="30c4e-115">You must have successfully completed</span></span>

- [<span data-ttu-id="30c4e-116">Создание Центра Интернета вещей и регистрация SensorTag</span><span class="sxs-lookup"><span data-stu-id="30c4e-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="30c4e-117">Клонирование примера репозитория на главном компьютере</span><span class="sxs-lookup"><span data-stu-id="30c4e-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="30c4e-118">Чтобы клонировать пример репозитория на главном компьютере, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="30c4e-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="30c4e-119">Откройте окно командной строки в Windows или терминала в macOS или Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="30c4e-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="30c4e-120">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="30c4e-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="30c4e-121">Настройте подключение между SensorTag и Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="30c4e-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="30c4e-122">Для этого сделайте следующее на главном компьютере:</span><span class="sxs-lookup"><span data-stu-id="30c4e-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="30c4e-123">Запустите файл конфигурации, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="30c4e-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="30c4e-124">Откройте файл `config-gateway.json` в Visual Studio Code, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="30c4e-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="30c4e-125">Найдите следующую строку кода и замените `[device hostname or IP address]` IP-адресом или именем Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="30c4e-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="30c4e-126">![снимок экрана настройки шлюза](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="30c4e-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="30c4e-127">Установите вспомогательные инструменты на устройстве Intel NUC, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="30c4e-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="30c4e-128">Включите SensorTag, нажав кнопку питания, как на следующем рисунке. После этого зеленый светодиодный индикатор должен мигнуть.</span><span class="sxs-lookup"><span data-stu-id="30c4e-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![включение SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="30c4e-130">Отсканируйте устройства SensorTag, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="30c4e-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="30c4e-131">Проверьте подключение между SensorTag и Intel NUC, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="30c4e-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="30c4e-132">Замените `{mac address}` MAC-адресом, полученным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="30c4e-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="30c4e-133">Получение строки подключения SensorTag</span><span class="sxs-lookup"><span data-stu-id="30c4e-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="30c4e-134">Чтобы получить строку подключения Центра Интернета вещей Azure для SensorTag, выполните следующую команду на главном компьютере:</span><span class="sxs-lookup"><span data-stu-id="30c4e-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="30c4e-135">`{IoT hub name}` — это имя использованного Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="30c4e-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="30c4e-136">Используйте iot-gateway в качестве значения `{resource group name}`, а mydevice в качестве значения `{device id}`, если в уроке 2 значение не изменялось.</span><span class="sxs-lookup"><span data-stu-id="30c4e-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="30c4e-137">Настройка примера приложения BLE</span><span class="sxs-lookup"><span data-stu-id="30c4e-137">Configure the BLE sample application</span></span>

<span data-ttu-id="30c4e-138">Чтобы настроить и запустить пример приложения BLE, сделайте следующее на главном компьютере:</span><span class="sxs-lookup"><span data-stu-id="30c4e-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="30c4e-139">Откройте файл `config-sensortag.json` в Visual Studio Code, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="30c4e-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![снимок экрана настройки SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="30c4e-141">Выполните следующие замены в коде:</span><span class="sxs-lookup"><span data-stu-id="30c4e-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="30c4e-142">Замените `[IoT hub name]` именем использованного Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="30c4e-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="30c4e-143">Замените `[IoT device connection string]` полученной строкой подключения SensorTag.</span><span class="sxs-lookup"><span data-stu-id="30c4e-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="30c4e-144">Замените `[device_mac_address]` полученным MAC-адресом SensorTag.</span><span class="sxs-lookup"><span data-stu-id="30c4e-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="30c4e-145">Запустите пример приложения BLE</span><span class="sxs-lookup"><span data-stu-id="30c4e-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="30c4e-146">Чтобы запустить пример приложения BLE, сделайте следующее на главном компьютере:</span><span class="sxs-lookup"><span data-stu-id="30c4e-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="30c4e-147">Включите SensorTag.</span><span class="sxs-lookup"><span data-stu-id="30c4e-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="30c4e-148">Разверните и запустите пример приложения BLE на устройстве Intel NUC, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="30c4e-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="30c4e-149">Проверка работы примера приложения BLE</span><span class="sxs-lookup"><span data-stu-id="30c4e-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="30c4e-150">Должны отобразиться подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="30c4e-150">You should now see an output like the following:</span></span>

![выходные данные примера приложения BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="30c4e-152">Пример приложения выполняет сбор данных температуры и отправляет их в ваш Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="30c4e-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="30c4e-153">Пример приложения автоматически завершает работу через 40 секунд после отправки.</span><span class="sxs-lookup"><span data-stu-id="30c4e-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="30c4e-154">Сводка</span><span class="sxs-lookup"><span data-stu-id="30c4e-154">Summary</span></span>

<span data-ttu-id="30c4e-155">Вы успешно настроили подключение между SensorTag и Intel NUC, а также запустили пример приложения BLE, который собирает и отправляет данные из SensorTag в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="30c4e-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="30c4e-156">Теперь можно перейти к проверке получения данных в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="30c4e-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30c4e-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30c4e-157">Next steps</span></span>
[<span data-ttu-id="30c4e-158">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="30c4e-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)