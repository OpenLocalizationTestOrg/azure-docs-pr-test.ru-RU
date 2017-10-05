---
title: "Подключение Intel Edison (Node) к Интернету вещей Azure. Урок 4. Получение сообщений | Документация Майкрософт"
description: "Пример приложения выполняется на устройстве Edison и отслеживает входящие сообщения от Центра Интернета вещей. Новая задача Gulp отправляет сообщения из Центра Интернета вещей на устройство Edison для управления состоянием светодиодного индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "управление светодиодным индикатором с помощью Arduino с веб-интерфейса, управление светодиодным индикатором с помощью Arduino через веб-интерфейс"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="5c746-105">Запуск примера приложения для получения сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="5c746-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="5c746-106">В этой статье вы развернете пример приложения на устройстве Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="5c746-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="5c746-107">Пример приложения отслеживает входящие сообщения от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5c746-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="5c746-108">Вы можете также запустить на компьютере задачу Gulp для отправки сообщений из Центра Интернета вещей на устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="5c746-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="5c746-109">При получении сообщений пример приложения включает и отключает светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="5c746-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="5c746-110">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5c746-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5c746-111">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="5c746-111">What you will do</span></span>
* <span data-ttu-id="5c746-112">Подключите пример приложения к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5c746-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="5c746-113">Развернете и запустите пример приложения.</span><span class="sxs-lookup"><span data-stu-id="5c746-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="5c746-114">Отправьте сообщения от Центра Интернета вещей на устройство Edison для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="5c746-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5c746-115">Новые знания</span><span class="sxs-lookup"><span data-stu-id="5c746-115">What you will learn</span></span>
<span data-ttu-id="5c746-116">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="5c746-116">In this article, you will learn:</span></span>
* <span data-ttu-id="5c746-117">Как отслеживать входящие сообщения от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5c746-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="5c746-118">Как отправлять сообщения из облака на устройство, т. е. из Центра Интернета вещей на устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="5c746-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5c746-119">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="5c746-119">What you need</span></span>
* <span data-ttu-id="5c746-120">Настройка Intel Edison для использования.</span><span class="sxs-lookup"><span data-stu-id="5c746-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="5c746-121">Узнайте, как настроить устройство Edison, в статье [Настройка устройства][configure-your-device] (Настройка Intel Edison).</span><span class="sxs-lookup"><span data-stu-id="5c746-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="5c746-122">Центр Интернета вещей, созданный в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="5c746-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="5c746-123">Создание Центра Интернета вещей описано в статье [Создание Центра Интернета вещей и регистрация Intel Edison][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="5c746-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="5c746-124">Подключение примера приложения к Центру Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="5c746-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="5c746-125">Перейдите в папку репозитория `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="5c746-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="5c746-126">Откройте пример приложения в Visual Studio Code, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5c746-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="5c746-127">Файл во вложенной папке `app` содержит основной код для отслеживания входящих сообщений из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5c746-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="5c746-128">Функция `blinkLED` включает и отключает светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="5c746-128">The `blinkLED` function blinks the LED.</span></span>

   ![Структура репозитория в примере приложения][repo-structure]
2. <span data-ttu-id="5c746-130">Запустите файл конфигурации, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="5c746-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="5c746-131">Если вы выполнили действия, описанные в статье [Создание приложения-функции Azure и учетной записи хранения Azure][create-an-azure-function-app-and-storage-account], на этом компьютере, то все конфигурации наследуются, поэтому вы можете пропустить шаг с задачей развертывания и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="5c746-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="5c746-132">Если вы выполнили действия, описанные в статье [Создание приложения-функции Azure и учетной записи хранения Azure][create-an-azure-function-app-and-storage-account], на другом компьютере, то необходимо заменить заполнители в файле `config-edison.json`.</span><span class="sxs-lookup"><span data-stu-id="5c746-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="5c746-133">Файл `config-edison.json` находится во вложенной папке вашей домашней папки.</span><span class="sxs-lookup"><span data-stu-id="5c746-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![Содержимое файла config-edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="5c746-135">Замените **[device hostname or IP address]** IP-адресом, указанным при настройке устройства.</span><span class="sxs-lookup"><span data-stu-id="5c746-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="5c746-136">Замените **[IoT device connection string]** строкой подключения к устройству, которую можно получить с помощью команды `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="5c746-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="5c746-137">Замените **[IoT hub connection string]** строкой подключения к Центру Интернета вещей, которую можно получить с помощью команды `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="5c746-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="5c746-138">Развертывание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="5c746-138">Deploy and run the sample application</span></span>
<span data-ttu-id="5c746-139">Разверните и запустите пример приложения в Edison, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5c746-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="5c746-140">Эта команда Gulp развертывает пример приложения на устройстве Edison.</span><span class="sxs-lookup"><span data-stu-id="5c746-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="5c746-141">Затем она запускает приложение на устройстве Edison и отдельную задачу на главном компьютере, которая отправляет на устройство Edison из Центра Интернета вещей 20 сообщений для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="5c746-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="5c746-142">Запущенное приложение начинает ожидать передачи сообщений от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5c746-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="5c746-143">Одновременно с этим задача Gulp отправляет несколько сообщений для включения и отключения светодиодного индикатора из Центра Интернета вещей на устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="5c746-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="5c746-144">При получении устройством Edison каждого такого сообщения пример приложения вызывает функцию `blinkLED` для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="5c746-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="5c746-145">В результате этот индикатор должен мигать каждые две секунды, пока задача Gulp отправляет 20 сообщений от Центра Интернета вещей на устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="5c746-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="5c746-146">Последнее сообщение содержит команду stop, при получении которой приложение завершит работу.</span><span class="sxs-lookup"><span data-stu-id="5c746-146">The last one is a "stop" message that stops the application from running.</span></span>

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="5c746-148">Сводка</span><span class="sxs-lookup"><span data-stu-id="5c746-148">Summary</span></span>
<span data-ttu-id="5c746-149">Итак, вы успешно отправили сообщения от Центра Интернета вещей на устройство Edison для включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="5c746-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="5c746-150">Следующая задача является необязательной: изменение режима включения и отключения светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="5c746-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c746-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c746-151">Next steps</span></span>
<span data-ttu-id="5c746-152">[Изменение режима включения и отключения светодиодного индикатора][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="5c746-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md