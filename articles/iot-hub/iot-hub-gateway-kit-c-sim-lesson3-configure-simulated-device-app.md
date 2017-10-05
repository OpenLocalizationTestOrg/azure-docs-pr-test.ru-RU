---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 3. Запуск примера приложения | Документация Майкрософт"
description: "Запуск примера приложения для имитации устройства для отправки данных в Центр Интернета вещей"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "отправка данных в облако"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="c6cbb-104">Настройка и запуск примера приложения для имитации устройства</span><span class="sxs-lookup"><span data-stu-id="c6cbb-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c6cbb-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="c6cbb-105">What you will do</span></span>

- <span data-ttu-id="c6cbb-106">Клонируйте репозиторий.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-106">Clone the sample repository.</span></span>
- <span data-ttu-id="c6cbb-107">Чтобы получить сведения о Центре Интернета вещей и логическом устройстве примера приложения для имитации устройства, используйте Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="c6cbb-108">Затем настройте и запустите пример приложения для имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="c6cbb-109">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c6cbb-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c6cbb-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="c6cbb-110">What you will learn</span></span>

<span data-ttu-id="c6cbb-111">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-111">In this article, you will learn:</span></span>

- <span data-ttu-id="c6cbb-112">Как настроить и запустить пример приложения для имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c6cbb-113">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="c6cbb-113">What you need</span></span>

<span data-ttu-id="c6cbb-114">Необходимо успешно выполнить инструкции, изложенные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-114">You must have successfully completed</span></span>

- [<span data-ttu-id="c6cbb-115">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="c6cbb-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="c6cbb-116">Клонирование примера репозитория на главном компьютере</span><span class="sxs-lookup"><span data-stu-id="c6cbb-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="c6cbb-117">Чтобы клонировать пример репозитория на главном компьютере, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="c6cbb-118">Откройте командную строку в Windows или окно терминала в МacOS или Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="c6cbb-119">Выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="c6cbb-120">Настройка имитации устройства и NUC</span><span class="sxs-lookup"><span data-stu-id="c6cbb-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="c6cbb-121">Откройте файл конфигурации `config.json` в Visual Studio Code, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="c6cbb-122">Замените `"has_sensortag": true` на `"has_sensortag": false`:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![конфигурация, нет устройства TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="c6cbb-124">Запустите файл конфигурации, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="c6cbb-125">Откройте файл `config-gateway.json` в Visual Studio Code, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="c6cbb-126">Найдите следующую строку кода и замените `[device hostname or IP address]` IP-адресом или именем Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="c6cbb-127">![снимок экрана настройки шлюза](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="c6cbb-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="c6cbb-128">Получение строки подключения логического устройства Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="c6cbb-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="c6cbb-129">Чтобы получить строку подключения Центра Интернета вещей Azure для логического устройства, выполните следующую команду на главном компьютере:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="c6cbb-130">`{IoT hub name}` — это имя использованного Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="c6cbb-131">Используйте iot-gateway в качестве значения `{resource group name}`, а mydevice в качестве значения `{device id}`, если в уроке 2 значение не изменялось.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="c6cbb-132">Настройка примера приложения отправки в облако для имитации устройства</span><span class="sxs-lookup"><span data-stu-id="c6cbb-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="c6cbb-133">Чтобы настроить и запустить пример приложения отправки в облако для имитации устройства, сделайте следующее на главном компьютере:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="c6cbb-134">Откройте файл `config-sensortag.json` в Visual Studio Code, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![снимок экрана настройки SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="c6cbb-136">Выполните следующие замены в коде:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="c6cbb-137">Замените `[IoT hub name]` именем Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="c6cbb-138">Замените `[IoT device connection string]` строкой подключения логического устройства Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="c6cbb-139">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-139">Run the application.</span></span>

   <span data-ttu-id="c6cbb-140">Разверните и запустите приложение, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="c6cbb-141">Проверка работы примера приложения</span><span class="sxs-lookup"><span data-stu-id="c6cbb-141">Verify the sample application works</span></span>

<span data-ttu-id="c6cbb-142">Должны отобразиться подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c6cbb-142">You should now see output like the following:</span></span>

![выходные данные примера приложения для имитации устройства](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="c6cbb-144">Приложение отправляет данные о температуре в Центр Интернета вещей в течение 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="c6cbb-145">Сводка</span><span class="sxs-lookup"><span data-stu-id="c6cbb-145">Summary</span></span>

<span data-ttu-id="c6cbb-146">Вы успешно настроили и запустили пример приложения отправки в облако для имитации устройства, которое отправляет данные в Центр Интернета вещей с помощью имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="c6cbb-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6cbb-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6cbb-147">Next steps</span></span>
[<span data-ttu-id="c6cbb-148">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="c6cbb-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)