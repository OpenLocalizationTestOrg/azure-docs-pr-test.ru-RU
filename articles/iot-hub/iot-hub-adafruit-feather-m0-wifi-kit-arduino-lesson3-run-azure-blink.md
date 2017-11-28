---
title: "Подключение Arduino (C) к Интернету вещей Azure. Урок 3. Запуск примера | Документация Майкрософт"
description: "Разверните и запустите на плате Adafruit Feather M0 WiFi пример приложения, которое отправляет сообщения в Центр Интернета вещей и заставляет светодиодный индикатор мигать."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "облачная служба Интернета вещей, отправка данных в облако с помощью Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="959b3-104">Запуск примера приложения для отправки сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="959b3-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="959b3-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="959b3-105">What you will do</span></span>
<span data-ttu-id="959b3-106">В этой статье показано, как развернуть и запустить на плате Adafruit Feather M0 WiFi Arduino пример приложения, которое отправляет сообщения в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="959b3-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="959b3-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="959b3-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="959b3-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="959b3-108">What you will learn</span></span>
<span data-ttu-id="959b3-109">Вы узнаете, как с помощью инструмента Gulp развернуть и запустить пример приложения Arduino на плате Arduino.</span><span class="sxs-lookup"><span data-stu-id="959b3-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="959b3-110">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="959b3-110">What you need</span></span>
* <span data-ttu-id="959b3-111">К выполнению этой задачи следует приступать только после выполнения действий, описанных в статье [Создание приложения-функции Azure и учетной записи хранения Azure][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="959b3-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="959b3-112">Получение строк подключения Центра Интернета вещей и устройства</span><span class="sxs-lookup"><span data-stu-id="959b3-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="959b3-113">Строка подключения устройства используется для подключения платы Arduino к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="959b3-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="959b3-114">Строка подключения Центра Интернета вещей используется для его подключения к удостоверению устройства, которое представляет плату Arduino в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="959b3-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="959b3-115">Для вывода списка всех Центров Интернета вещей в группе ресурсов выполните следующую команду Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="959b3-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="959b3-116">Используйте `iot-sample` в качестве значения `{resource group name}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="959b3-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="959b3-117">Для получения строки подключения Центра Интернета вещей выполните следующую команду интерфейса командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="959b3-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="959b3-118">`{my hub name}` — это имя, указанное при создании Центра Интернета вещей и регистрации платы Arduinoi.</span><span class="sxs-lookup"><span data-stu-id="959b3-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="959b3-119">Для получения строки подключения устройства выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="959b3-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="959b3-120">Используйте `mym0wifi` в качестве значения `{device id}`, если вы не меняли это значение.</span><span class="sxs-lookup"><span data-stu-id="959b3-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="959b3-121">Настройка подключения устройства</span><span class="sxs-lookup"><span data-stu-id="959b3-121">Configure the device connection</span></span>
<span data-ttu-id="959b3-122">Чтобы настроить подключение устройства, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="959b3-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="959b3-123">Получите последовательный порт устройства, используя интерфейс командной строки обнаружения устройств:</span><span class="sxs-lookup"><span data-stu-id="959b3-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="959b3-124">Отобразятся следующие выходные данные, и вы сможете найти COM-порт вашей платы Arduino.</span><span class="sxs-lookup"><span data-stu-id="959b3-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Обнаружение устройства][device-discovery]

2. <span data-ttu-id="959b3-126">Откройте файл `config.json` в папке занятия и добавьте значение найденного номера COM-порта:</span><span class="sxs-lookup"><span data-stu-id="959b3-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="959b3-128">Для COM-порта на платформе Windows он имеет формат `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="959b3-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="959b3-129">На macOS или Ubuntu он начинается с `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="959b3-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="959b3-130">Запустите файл конфигурации, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="959b3-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="959b3-131">Откройте файл конфигурации устройства `config-arduino.json` в Visual Studio Code, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="959b3-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="959b3-133">В файле `config-arduino.json` выполните следующие замены.</span><span class="sxs-lookup"><span data-stu-id="959b3-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="959b3-134">Замените **[Wi-Fi SSID]** своим SSID для Wi-Fi, подключенным к Интернету.</span><span class="sxs-lookup"><span data-stu-id="959b3-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="959b3-135">Замените **[Wi-Fi password]** своим паролем Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="959b3-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="959b3-136">Удалите строку, если для подключения к Wi-Fi не требуется пароль.</span><span class="sxs-lookup"><span data-stu-id="959b3-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="959b3-137">Замените **[строка подключения устройства Интернета вещей]** на полученное значение `device connection string`.</span><span class="sxs-lookup"><span data-stu-id="959b3-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="959b3-138">Замените **[IoT hub connection string]** (строка подключения Центра Интернета вещей) полученным значением `iot hub connection string`.</span><span class="sxs-lookup"><span data-stu-id="959b3-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="959b3-139">В этой статье не требуется `azure_storage_connection_string`.</span><span class="sxs-lookup"><span data-stu-id="959b3-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="959b3-140">Оставьте эту настройку без изменений.</span><span class="sxs-lookup"><span data-stu-id="959b3-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="959b3-141">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="959b3-141">Deploy and run the sample application</span></span>
<span data-ttu-id="959b3-142">Разверните и запустите пример приложения на плате Arduino, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="959b3-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="959b3-143">Задача инструмента Gulp по умолчанию последовательно запускает задачи `install-tools` и `run`.</span><span class="sxs-lookup"><span data-stu-id="959b3-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="959b3-144">[Развернув приложение для включения индикатора][deployed-the-blink-app], выполните эти задачи отдельно.</span><span class="sxs-lookup"><span data-stu-id="959b3-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="959b3-145">Проверка работы примера приложения</span><span class="sxs-lookup"><span data-stu-id="959b3-145">Verify that the sample application works</span></span>
<span data-ttu-id="959b3-146">Встроенный светодиодный индикатор GPIO #0 должен мигать каждые две секунды.</span><span class="sxs-lookup"><span data-stu-id="959b3-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="959b3-147">Каждый раз, когда индикатор мигает, пример приложения отправляет сообщение в Центр Интернета вещей и проверяет, что сообщение успешно отправлено.</span><span class="sxs-lookup"><span data-stu-id="959b3-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="959b3-148">Кроме того, каждое сообщение, полученное Центром Интернета вещей, выводится в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="959b3-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="959b3-149">Пример приложения автоматически завершает работу после отправки 20 сообщений.</span><span class="sxs-lookup"><span data-stu-id="959b3-149">The sample application terminates automatically after sending 20 messages.</span></span>

![Пример приложения с отправленными и полученными сообщениями][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="959b3-151">Сводка</span><span class="sxs-lookup"><span data-stu-id="959b3-151">Summary</span></span>
<span data-ttu-id="959b3-152">Вы развернули и запустили новый пример приложения для включения светодиодного индикатора на плате Arduino для отправки сообщений с устройства в облако, в котором находится Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="959b3-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="959b3-153">Теперь можно отслеживать сообщения по мере их записывания в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="959b3-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="959b3-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="959b3-154">Next steps</span></span>
<span data-ttu-id="959b3-155">[Чтение сообщений, сохраненных в службе хранилища Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="959b3-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md