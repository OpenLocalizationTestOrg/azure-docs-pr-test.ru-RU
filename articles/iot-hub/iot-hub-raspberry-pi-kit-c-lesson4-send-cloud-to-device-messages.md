---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 4. Передача из облака на устройство | Документация Майкрософт"
description: "Пример приложения выполняется на устройстве Pi и отслеживает входящие сообщения от Центра Интернета вещей. Новая задача Gulp отправляет из Центра Интернета вещей сообщения на устройство Pi для управления состоянием индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Из облака на устройство, сообщение из облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 86c7be931319d9995c2a7311267c7e7c03c3c1b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="cf12e-105">Запуск примера приложения для получения сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="cf12e-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="cf12e-106">В этой статье вы развернете пример приложения на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="cf12e-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="cf12e-107">Пример приложения отслеживает входящие сообщения от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cf12e-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="cf12e-108">Вы можете также запустить на компьютере задачу Gulp для отправки сообщений из Центра Интернета вещей на устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="cf12e-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="cf12e-109">При получении сообщений пример приложения включает и отключает светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="cf12e-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="cf12e-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cf12e-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="cf12e-111">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="cf12e-111">What you will do</span></span>
* <span data-ttu-id="cf12e-112">Подключите пример приложения к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cf12e-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="cf12e-113">Развернете и запустите пример приложения.</span><span class="sxs-lookup"><span data-stu-id="cf12e-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="cf12e-114">Отправите сообщения от Центра Интернета вещей на устройство Pi для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="cf12e-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cf12e-115">Новые знания</span><span class="sxs-lookup"><span data-stu-id="cf12e-115">What you will learn</span></span>
<span data-ttu-id="cf12e-116">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="cf12e-116">In this article, you will learn:</span></span>
* <span data-ttu-id="cf12e-117">Как отслеживать входящие сообщения от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cf12e-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="cf12e-118">Как отправлять сообщения из облака на устройство, т. е. из Центра Интернета вещей на устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="cf12e-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cf12e-119">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="cf12e-119">What you need</span></span>
* <span data-ttu-id="cf12e-120">Устройство Raspberry Pi 3, подготовленное к использованию.</span><span class="sxs-lookup"><span data-stu-id="cf12e-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="cf12e-121">Узнайте, как настроить устройство Pi, в разделе [Настройка устройства](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="cf12e-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="cf12e-122">Центр Интернета вещей, созданный в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="cf12e-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="cf12e-123">Узнайте, как создать Центр Интернета вещей, в разделе [Создание Центра Интернета вещей и регистрация Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="cf12e-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="cf12e-124">Подключение примера приложения к Центру Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="cf12e-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="cf12e-125">Перейдите в папку репозитория `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="cf12e-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="cf12e-126">Откройте пример приложения в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="cf12e-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="cf12e-127">Обратите внимание на файл `app.c`, созданный во вложенной папке `app`.</span><span class="sxs-lookup"><span data-stu-id="cf12e-127">Notice the `app.c` file in the `app` subfolder.</span></span> <span data-ttu-id="cf12e-128">Файл `app.c` содержит основной код для отслеживания входящих сообщений из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cf12e-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="cf12e-129">Функция `blinkLED` включает и отключает светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="cf12e-129">The `blinkLED` function blinks the LED.</span></span>

   ![Структура репозитория в примере приложения](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="cf12e-131">Запустите файл конфигурации, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="cf12e-131">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="cf12e-132">Если вы выполнили действия, описанные в статье [Создание приложения-функции Azure и учетной записи хранения Azure](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md), на этом компьютере, то все конфигурации наследуются, поэтому вы можете пропустить задачу развертывания и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="cf12e-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="cf12e-133">Если вы выполнили действия, описанные в разделе [Create an Azure function app and Azure storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) (Создание приложения-функции Azure и учетной записи хранения Azure), на другом компьютере, то необходимо заменить заполнители в файле `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="cf12e-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="cf12e-134">Файл `config-raspberrypi.json` находится во вложенной папке вашей домашней папки.</span><span class="sxs-lookup"><span data-stu-id="cf12e-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>

   ![Содержимое файла config-raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="cf12e-136">Замените строку **[device hostname or IP address]** IP-адресом или именем узла вашего устройства Pi. Эти сведения можно получить, выполнив команду `devdisco list --eth`.</span><span class="sxs-lookup"><span data-stu-id="cf12e-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="cf12e-137">Замените **[IoT device connection string]** строкой подключения к устройству, которую можно получить с помощью команды `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="cf12e-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="cf12e-138">Замените **[IoT hub connection string]** строкой подключения к Центру Интернета вещей, которую можно получить с помощью команды `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}`.</span><span class="sxs-lookup"><span data-stu-id="cf12e-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="cf12e-139">Выполните также **gulp install-tools**, если это не было сделано на уроке 1.</span><span class="sxs-lookup"><span data-stu-id="cf12e-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="cf12e-140">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="cf12e-140">Deploy and run the sample application</span></span>
<span data-ttu-id="cf12e-141">Разверните и запустите пример приложения на устройстве Pi, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cf12e-141">Deploy and run the sample application on Pi by running the following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="cf12e-142">Команда Gulp в первую очередь устанавливает средства.</span><span class="sxs-lookup"><span data-stu-id="cf12e-142">The gulp command runs the install-tools task first.</span></span> <span data-ttu-id="cf12e-143">Затем она развертывает пример приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="cf12e-143">Then it deploys the sample application to Pi.</span></span> <span data-ttu-id="cf12e-144">В конце она запускает приложение на устройстве Pi и отдельную задачу на главном компьютере, которая отправляет из Центра Интернета вещей 20 сообщений для включения и отключения светодиодного индикатора на устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="cf12e-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="cf12e-145">Запущенное приложение начинает ожидать передачи сообщений от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cf12e-145">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="cf12e-146">Одновременно с этим задача Gulp отправляет несколько сообщений для включения и отключения светодиодного индикатора из Центра Интернета вещей на устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="cf12e-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="cf12e-147">При получении каждого такого сообщения пример приложения вызывает функцию `blinkLED` для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="cf12e-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="cf12e-148">В результате этот индикатор должен мигать каждые две секунды, пока задача Gulp отправляет 20 сообщений от Центра Интернета вещей на устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="cf12e-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="cf12e-149">Последнее сообщение содержит команду stop, при получении которой приложение завершит работу.</span><span class="sxs-lookup"><span data-stu-id="cf12e-149">The last one is a "stop" message that stops the application from running.</span></span>

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="cf12e-151">Сводка</span><span class="sxs-lookup"><span data-stu-id="cf12e-151">Summary</span></span>
<span data-ttu-id="cf12e-152">Итак, вы успешно отправили сообщения от Центра Интернета вещей на устройство Pi для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="cf12e-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="cf12e-153">Следующая задача является необязательной: изменение режима включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="cf12e-153">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf12e-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf12e-154">Next steps</span></span>
[<span data-ttu-id="cf12e-155">Изменение режима включения и отключения светодиодного индикатора</span><span class="sxs-lookup"><span data-stu-id="cf12e-155">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
