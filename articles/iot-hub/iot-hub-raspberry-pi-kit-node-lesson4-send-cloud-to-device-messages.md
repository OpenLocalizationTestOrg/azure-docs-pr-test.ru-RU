---
featureFlags: usabilla
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 4: облака на устройство | Документы Microsoft"
description: "Пример приложения Hello работает на Pi и отслеживает входящие сообщения от вашего центра IoT. Новая задача gulp отправляет сообщения tooPi из вашей hello tooblink концентратора IoT Индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "toodevice облака, сообщение из облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="8b055-105">Запустите сообщений hello образец приложения tooreceive облака на устройство</span><span class="sxs-lookup"><span data-stu-id="8b055-105">Run hello sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="8b055-106">В этой статье вы развернете пример приложения на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="8b055-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="8b055-107">Пример приложения Hello отслеживает входящие сообщения от вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="8b055-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="8b055-108">Можно также запустить задание gulp на tooPi сообщения toosend вашего компьютера из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="8b055-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="8b055-109">Пример приложения hello, получив сообщений hello, он мигает Индикатор hello.</span><span class="sxs-lookup"><span data-stu-id="8b055-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="8b055-110">Если у вас возникнут проблемы, поиска решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8b055-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8b055-111">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="8b055-111">What you will do</span></span>
* <span data-ttu-id="8b055-112">Подключите пример приложения hello tooyour-центр IoT.</span><span class="sxs-lookup"><span data-stu-id="8b055-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="8b055-113">Развертывание и запуск образца приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8b055-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="8b055-114">Отправьте сообщения из вашей IoT hub tooPi tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="8b055-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8b055-115">Новые знания</span><span class="sxs-lookup"><span data-stu-id="8b055-115">What you will learn</span></span>
<span data-ttu-id="8b055-116">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="8b055-116">In this article, you will learn:</span></span>
* <span data-ttu-id="8b055-117">Способ toomonitor входящих сообщений из вашего центра IoT</span><span class="sxs-lookup"><span data-stu-id="8b055-117">How toomonitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="8b055-118">Способ toosend облака на устройство сообщений из вашей tooPi концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="8b055-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8b055-119">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="8b055-119">What you need</span></span>
* <span data-ttu-id="8b055-120">Устройство Raspberry Pi 3, подготовленное к использованию.</span><span class="sxs-lookup"><span data-stu-id="8b055-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="8b055-121">статье tooset копирование Pi, toolearn [настройки устройства](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="8b055-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="8b055-122">Центр Интернета вещей, созданный в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="8b055-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="8b055-123">toolearn как toocreate ваш центр IoT. в разделе [ваш центр IoT и регистрации Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="8b055-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="8b055-124">Пример приложения hello tooyour-центр IoT подключения</span><span class="sxs-lookup"><span data-stu-id="8b055-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="8b055-125">Убедитесь, что вы находитесь в папке репозитория hello `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="8b055-125">Make sure that you're in hello repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="8b055-126">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="8b055-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="8b055-127">Обратите внимание hello `app.js` файла в hello `app` вложенную папку.</span><span class="sxs-lookup"><span data-stu-id="8b055-127">Notice hello `app.js` file in hello `app` subfolder.</span></span> <span data-ttu-id="8b055-128">Hello `app.js` файл является hello ключа исходного файла, содержащего hello кода toomonitor входящие сообщения от центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="8b055-128">hello `app.js` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="8b055-129">Hello `blinkLED` hello Индикатор мигает функции.</span><span class="sxs-lookup"><span data-stu-id="8b055-129">hello `blinkLED` function blinks hello LED.</span></span>
   
   ![Структура репозитория в пример приложения hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="8b055-131">Инициализируйте hello файл конфигурации с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="8b055-131">Initialize hello configuration file by using hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="8b055-132">Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) на этом компьютере наследуются все конфигурации hello, поэтому вы можете пропустить toohello задачи развертывания и выполнения примера приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8b055-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="8b055-133">Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) на другом компьютере, необходимо tooreplace hello меток-заполнителей в hello `config-raspberrypi.json` файла.</span><span class="sxs-lookup"><span data-stu-id="8b055-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="8b055-134">Hello `config-raspberrypi.json` файл находится в подпапке hello домашней папке.</span><span class="sxs-lookup"><span data-stu-id="8b055-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>
   
   ![Содержимое файла конфигурации raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="8b055-136">Замените **[устройства имя узла или IP-адрес]** с IP-адресом hello Pi или hello имени узла, который можно получить, выполнив hello `devdisco list --eth` команды.</span><span class="sxs-lookup"><span data-stu-id="8b055-136">Replace **[device hostname or IP address]** with hello IP address of Pi or hello host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="8b055-137">Замените **[строка подключения устройств IoT]** со строкой подключения устройства hello, можно получить, выполнив hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` команды.</span><span class="sxs-lookup"><span data-stu-id="8b055-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="8b055-138">Замените **[строка подключения концентратора IoT]** с hello строка подключения концентратора IoT, можно получить, выполнив hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` команды.</span><span class="sxs-lookup"><span data-stu-id="8b055-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="8b055-139">Выполните также **gulp install-tools**, если это не было сделано на уроке 1.</span><span class="sxs-lookup"><span data-stu-id="8b055-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="8b055-140">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="8b055-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="8b055-141">Развертывание и запуск образца приложения hello на Pi, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="8b055-141">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="8b055-142">Команда Hello развертывает tooPi приложения образец hello.</span><span class="sxs-lookup"><span data-stu-id="8b055-142">hello command deploys hello sample application tooPi.</span></span> <span data-ttu-id="8b055-143">Затем она запускает приложение hello на Pi и отдельную задачу на узле tooPi сообщений blink toosend 20 компьютера из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="8b055-143">Then, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="8b055-144">После запуска образца приложения hello, она запускает прослушивание toomessages из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="8b055-144">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="8b055-145">В то же время задачу hello gulp отправляет несколько сообщений «blink» из вашей tooPi концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="8b055-145">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="8b055-146">Для каждого получаемого Pi сообщения blink hello образец приложения вызывает hello `blinkLED` tooblink функции hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="8b055-146">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="8b055-147">Вы увидите мигающий Индикатор hello каждые две секунды как hello gulp задача отправляет 20 сообщения из вашей tooPi концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="8b055-147">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="8b055-148">Hello последнего одним является «остановить» сообщение о том, под управлением toostop приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8b055-148">hello last one is a "stop" message that tells hello application toostop running.</span></span>

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="8b055-150">Сводка</span><span class="sxs-lookup"><span data-stu-id="8b055-150">Summary</span></span>
<span data-ttu-id="8b055-151">Успешно отправлено сообщений из вашей IoT hub tooPi tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="8b055-151">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="8b055-152">Следующая задача Hello является необязательным: изменение hello и отключать поведение hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="8b055-152">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b055-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b055-153">Next steps</span></span>
[<span data-ttu-id="8b055-154">Изменить hello и отключать поведение hello Индикатора</span><span class="sxs-lookup"><span data-stu-id="8b055-154">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

