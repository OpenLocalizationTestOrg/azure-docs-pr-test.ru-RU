---
title: "Подключение Arduino к Интернету вещей Azure. Урок 1. Развертывание приложения | Документация Майкрософт"
description: "Клонируйте пример приложения Arduino из Github и разверните его с помощью инструмента Gulp на плате Adafruit Feather M0 WiFi. Этот пример приложения включает и отключает GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "проекты светодиодного индикатора Arduino, включение светодиодного индикатора Arduino, код включения индикатора Arduino, программа включения индикатора Arduino, пример включения индикатора Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="251b4-105">Создание и развертывание приложения для включения индикатора</span><span class="sxs-lookup"><span data-stu-id="251b4-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="251b4-106">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="251b4-106">What you will do</span></span>
<span data-ttu-id="251b4-107">Клонируйте пример приложения Arduino для включения индикатора из Github и разверните его с помощью средства Gulp на плате Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="251b4-107">Clone the sample Arduino application from GitHub, and use the gulp tool to deploy the sample application to your Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="251b4-108">Этот пример приложения будет каждые две секунды включать встроенный светодиодный индикатор GPIO #13.</span><span class="sxs-lookup"><span data-stu-id="251b4-108">The sample application blinks the GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="251b4-109">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="251b4-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="251b4-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="251b4-110">What you will learn</span></span>
* <span data-ttu-id="251b4-111">Как развертывать и запускать пример приложения на плате Arduino.</span><span class="sxs-lookup"><span data-stu-id="251b4-111">How to deploy and run the sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="251b4-112">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="251b4-112">What you need</span></span>
<span data-ttu-id="251b4-113">Необходимо успешно выполнить следующие операции:</span><span class="sxs-lookup"><span data-stu-id="251b4-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="251b4-114">[Настройка устройства][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="251b4-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="251b4-115">[Get the tools][get-the-tools] (Получение инструментов)</span><span class="sxs-lookup"><span data-stu-id="251b4-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="251b4-116">Открытие примера приложения</span><span class="sxs-lookup"><span data-stu-id="251b4-116">Open the sample application</span></span>
<span data-ttu-id="251b4-117">Чтобы открыть пример приложения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="251b4-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="251b4-118">Клонируйте пример репозитория из GitHub, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="251b4-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="251b4-119">Откройте пример приложения в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="251b4-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Структура репозитория][repo-structure]

<span data-ttu-id="251b4-121">Файл `app.ino` в подпапке `app` — это ключевой исходный файл, содержащий код для управления светодиодным индикатором.</span><span class="sxs-lookup"><span data-stu-id="251b4-121">The `app.ino` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="251b4-122">Установка зависимостей приложения</span><span class="sxs-lookup"><span data-stu-id="251b4-122">Install application dependencies</span></span>
<span data-ttu-id="251b4-123">Установите библиотеки и другие модули, необходимые для примера приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="251b4-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="251b4-124">Настройка подключения устройства</span><span class="sxs-lookup"><span data-stu-id="251b4-124">Configure the device connection</span></span>
<span data-ttu-id="251b4-125">Чтобы настроить подключение устройства, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="251b4-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="251b4-126">Получите последовательный порт устройства, используя интерфейс командной строки обнаружения устройств:</span><span class="sxs-lookup"><span data-stu-id="251b4-126">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="251b4-127">Вы должны увидеть результат, аналогичный приведенному ниже и найти COM-порт вашей платы Arduino:![Обнаружение устройства][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="251b4-127">You should see an output that is similar to the following and find the usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="251b4-128">Откройте файл `config.json` в папке занятия и добавьте значение найденного номера COM-порта:</span><span class="sxs-lookup"><span data-stu-id="251b4-128">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="251b4-130">Для COM-порта на платформе Windows он имеет формат `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="251b4-130">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="251b4-131">На macOS или Ubuntu он начинается с `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="251b4-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="251b4-132">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="251b4-132">Deploy and run the sample application</span></span>
### <a name="install-the-required-tools-for-your-arduino-board"></a><span data-ttu-id="251b4-133">Установка необходимых инструментов для платы Arduino</span><span class="sxs-lookup"><span data-stu-id="251b4-133">Install the required tools for your Arduino board</span></span>

<span data-ttu-id="251b4-134">Установите пакет SDK для Центра Интернета вещей Azure для платы Arduino, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="251b4-134">Install the Azure IoT Hub SDK for your Arduino board by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="251b4-135">В зависимости от сетевого подключения для выполнения этой команды может потребоваться много времени.</span><span class="sxs-lookup"><span data-stu-id="251b4-135">This task might take a long time to complete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="251b4-136">Завершите работу экземпляра IDE Arduino при выполнении задач Gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="251b4-136">Please exit the running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="251b4-137">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="251b4-137">Deploy and run the sample app</span></span>
<span data-ttu-id="251b4-138">Разверните и запустите пример приложения, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="251b4-138">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a><span data-ttu-id="251b4-139">Проверка работы приложения</span><span class="sxs-lookup"><span data-stu-id="251b4-139">Verify the app works</span></span>
<span data-ttu-id="251b4-140">Если светодиодный индикатор не мигает, см. способы решения распространенных проблем в [руководстве по устранению неполадок][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="251b4-140">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting-page] for solutions to common problems.</span></span>

![Светодиодный индикатор мигает][led-blinking]

## <a name="summary"></a><span data-ttu-id="251b4-142">Сводка</span><span class="sxs-lookup"><span data-stu-id="251b4-142">Summary</span></span>
<span data-ttu-id="251b4-143">Вы установили необходимые инструменты для работы с платой Arduino и развернули пример приложения, заставляющего светодиодный индикатор мигать.</span><span class="sxs-lookup"><span data-stu-id="251b4-143">You've installed the required tools to work with your Arduino board and deployed a sample application to your Arduino board to blink the LED.</span></span> <span data-ttu-id="251b4-144">Теперь можно приступать к созданию, развертыванию и запуску другого примера приложения, которое подключает плату Arduino к Центру Интернета вещей Azure для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="251b4-144">You can now create, deploy, and run another sample application that connects your Arduino board to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="251b4-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="251b4-145">Next steps</span></span>
<span data-ttu-id="251b4-146">[Get the Azure tools][get-the-azure-tools] (Получение инструментов Azure)</span><span class="sxs-lookup"><span data-stu-id="251b4-146">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md