---
title: "Подключение Arduino (C) к Интернету вещей Azure. Урок 4. Передача из облака на устройство | Документация Майкрософт"
description: "Пример приложения выполняется на устройстве Adafruit Feather M0 WiFi и отслеживает входящие сообщения от Центра Интернета вещей. Новая задача Gulp отправляет из Центра Интернета вещей сообщения на устройство Adafruit Feather M0 WiFi для управления состоянием индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "управление светодиодным индикатором с помощью Arduino с веб-интерфейса, управление светодиодным индикатором с помощью Arduino через веб-интерфейс"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="a1adb-105">Запуск примера приложения для получения сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="a1adb-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="a1adb-106">В этой статье на плате Adafruit Feather M0 WiFi Arduino развертывается пример приложения.</span><span class="sxs-lookup"><span data-stu-id="a1adb-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="a1adb-107">Пример приложения отслеживает входящие сообщения от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a1adb-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="a1adb-108">Также вы можете запустить на компьютере задачу Gulp для отправки сообщений из Центра Интернета вещей на плату Arduino.</span><span class="sxs-lookup"><span data-stu-id="a1adb-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="a1adb-109">При получении сообщений пример приложения включает и отключает светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="a1adb-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="a1adb-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a1adb-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a1adb-111">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="a1adb-111">What you will do</span></span>
* <span data-ttu-id="a1adb-112">Подключите пример приложения к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a1adb-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="a1adb-113">Развернете и запустите пример приложения.</span><span class="sxs-lookup"><span data-stu-id="a1adb-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="a1adb-114">Отправка сообщения из Центра Интернета вещей на плату Arduino для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="a1adb-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a1adb-115">Новые знания</span><span class="sxs-lookup"><span data-stu-id="a1adb-115">What you will learn</span></span>
<span data-ttu-id="a1adb-116">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="a1adb-116">In this article, you will learn:</span></span>
* <span data-ttu-id="a1adb-117">Как отслеживать входящие сообщения от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a1adb-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="a1adb-118">Как отправлять сообщения, передаваемые из облака на устройство, из Центра Интернета вещей на плату Arduino.</span><span class="sxs-lookup"><span data-stu-id="a1adb-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a1adb-119">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="a1adb-119">What you need</span></span>
* <span data-ttu-id="a1adb-120">Плата Arduino, настроенная для работы.</span><span class="sxs-lookup"><span data-stu-id="a1adb-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="a1adb-121">Чтобы узнать, как настроить плату Arduino, ознакомьтесь с разделом [Настройка устройства][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="a1adb-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="a1adb-122">Центр Интернета вещей, созданный в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="a1adb-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="a1adb-123">Создание Центра Интернета вещей описано в статье [Создание Центра Интернета вещей и регистрация Intel Edison][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="a1adb-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="a1adb-124">Подключение примера приложения к Центру Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="a1adb-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="a1adb-125">Перейдите в папку репозитория `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="a1adb-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="a1adb-126">Откройте пример приложения в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="a1adb-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="a1adb-127">Обратите внимание на файл `app.ino`, созданный во вложенной папке `app`.</span><span class="sxs-lookup"><span data-stu-id="a1adb-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="a1adb-128">Файл `app.ino` содержит основной код для отслеживания входящих сообщений из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a1adb-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="a1adb-129">Функция `blinkLED` включает и отключает светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="a1adb-129">The `blinkLED` function blinks the LED.</span></span>

   ![Структура репозитория в примере приложения][repo-structure]

2. <span data-ttu-id="a1adb-131">Получите последовательный порт устройства, используя интерфейс командной строки обнаружения устройств.</span><span class="sxs-lookup"><span data-stu-id="a1adb-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="a1adb-132">Отобразятся следующие выходные данные, и вы сможете найти COM-порт вашей платы Arduino.</span><span class="sxs-lookup"><span data-stu-id="a1adb-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Обнаружение устройства][device-discovery]

3. <span data-ttu-id="a1adb-134">Откройте файл `config.json` в папке урока и введите значение найденного номера COM-порта.</span><span class="sxs-lookup"><span data-stu-id="a1adb-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="a1adb-136">Для COM-порта на платформе Windows он имеет формат `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="a1adb-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="a1adb-137">На платформе MacOS или Ubuntu он будет начинаться с `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="a1adb-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="a1adb-138">Запустите файл конфигурации, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="a1adb-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="a1adb-139">В файле `config-arduino.json` выполните следующие замены.</span><span class="sxs-lookup"><span data-stu-id="a1adb-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="a1adb-140">Если вы выполнили действия, описанные в статье [Создание приложения-функции Azure и учетной записи хранения Azure][create-an-azure-function-app-and-storage-account], на этом компьютере, то все конфигурации наследуются, поэтому вы можете пропустить шаг с задачей развертывания и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="a1adb-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="a1adb-141">Если вы выполнили действия, описанные в статье [Создание приложения-функции Azure и учетной записи хранения Azure][create-an-azure-function-app-and-storage-account], на другом компьютере, то необходимо заменить заполнители в файле `config-arduino.json`.</span><span class="sxs-lookup"><span data-stu-id="a1adb-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="a1adb-142">Файл `config-arduino.json` находится во вложенной папке вашей домашней папки.</span><span class="sxs-lookup"><span data-stu-id="a1adb-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![Содержимое файла config-arduino.json][config-arduino-json]

   * <span data-ttu-id="a1adb-144">Замените **[Wi-Fi SSID]** своим SSID для подключения Wi-Fi к Интернету.</span><span class="sxs-lookup"><span data-stu-id="a1adb-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="a1adb-145">Замените **[Wi-Fi password]** своим паролем Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a1adb-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="a1adb-146">Удалите строку, если для подключения к Wi-Fi не требуется пароль.</span><span class="sxs-lookup"><span data-stu-id="a1adb-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="a1adb-147">Замените **[IoT device connection string]** строкой подключения к устройству, которую можно получить с помощью команды `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="a1adb-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="a1adb-148">Замените **[IoT hub connection string]** строкой подключения к Центру Интернета вещей, которую можно получить с помощью команды `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="a1adb-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="a1adb-149">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="a1adb-149">Deploy and run the sample application</span></span>
<span data-ttu-id="a1adb-150">Разверните и запустите пример приложения на плате Arduino, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a1adb-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="a1adb-151">Эта команда Gulp развертывает пример приложения на плате Arduino.</span><span class="sxs-lookup"><span data-stu-id="a1adb-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="a1adb-152">Затем она запускает приложение на плате Arduino и отдельную задачу на главном компьютере, которая отправляет из Центра Интернета вещей 20 сообщений для включения и отключения светодиодного индикатора на плату Arduino.</span><span class="sxs-lookup"><span data-stu-id="a1adb-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="a1adb-153">Запущенное приложение начинает ожидать передачи сообщений от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a1adb-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="a1adb-154">Одновременно с этим задача Gulp отправляет из Центра Интернета вещей на плату Arduino несколько сообщений для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="a1adb-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="a1adb-155">При получении каждого такого сообщения платой пример приложения вызывает функцию `blinkLED` для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="a1adb-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="a1adb-156">В результате этот индикатор должен мигать каждые две секунды, пока задача Gulp отправляет 20 сообщений из Центра Интернета вещей на плату Arduino.</span><span class="sxs-lookup"><span data-stu-id="a1adb-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="a1adb-157">Последнее сообщение содержит команду stop, при получении которой приложение завершит работу.</span><span class="sxs-lookup"><span data-stu-id="a1adb-157">The last one is a "stop" message that stops the application from running.</span></span>

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора][sample-application]

## <a name="summary"></a><span data-ttu-id="a1adb-159">Сводка</span><span class="sxs-lookup"><span data-stu-id="a1adb-159">Summary</span></span>
<span data-ttu-id="a1adb-160">Итак, вы успешно отправили из Центра Интернета вещей на плату Arduino сообщения для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="a1adb-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="a1adb-161">Следующая задача является необязательной: изменение режима включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="a1adb-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1adb-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1adb-162">Next steps</span></span>
<span data-ttu-id="a1adb-163">[Изменение режима включения и отключения светодиодного индикатора][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="a1adb-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md