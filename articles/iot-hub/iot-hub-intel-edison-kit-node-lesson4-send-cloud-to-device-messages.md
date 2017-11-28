---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 4: получение сообщений | Документы Microsoft"
description: "Пример приложения выполняется на устройстве Edison и отслеживает входящие сообщения от Центра Интернета вещей. Новая задача gulp отправляет сообщения tooEdison из вашей hello tooblink концентратора IoT Индикатора."
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
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="bb8d8-105">Запустите образец приложения tooreceive сообщений облака на устройство</span><span class="sxs-lookup"><span data-stu-id="bb8d8-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="bb8d8-106">В этой статье вы развернете пример приложения на устройстве Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="bb8d8-107">Пример приложения Hello отслеживает входящие сообщения от вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="bb8d8-108">Можно также запустить задание gulp на tooEdison сообщения toosend вашего компьютера из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="bb8d8-109">Пример приложения hello, получив сообщений hello, он мигает Индикатор hello.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="bb8d8-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="bb8d8-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bb8d8-111">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="bb8d8-111">What you will do</span></span>
* <span data-ttu-id="bb8d8-112">Подключите пример приложения hello tooyour-центр IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="bb8d8-113">Развертывание и запуск образца приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="bb8d8-114">Отправьте сообщения из вашей IoT hub tooEdison tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bb8d8-115">Новые знания</span><span class="sxs-lookup"><span data-stu-id="bb8d8-115">What you will learn</span></span>
<span data-ttu-id="bb8d8-116">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="bb8d8-116">In this article, you will learn:</span></span>
* <span data-ttu-id="bb8d8-117">Способ toomonitor входящих сообщений из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="bb8d8-118">Способ toosend облака на устройство сообщений из вашей tooEdison концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bb8d8-119">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="bb8d8-119">What you need</span></span>
* <span data-ttu-id="bb8d8-120">Настройка Intel Edison для использования.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="bb8d8-121">статье tooset копирование Edison toolearn [настройки устройства][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="bb8d8-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="bb8d8-122">Центр Интернета вещей, созданный в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="bb8d8-123">toolearn как toocreate ваш центр IoT. в разделе [создать концентратор IoT Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="bb8d8-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="bb8d8-124">Пример приложения hello tooyour-центр IoT подключения</span><span class="sxs-lookup"><span data-stu-id="bb8d8-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="bb8d8-125">Убедитесь, что вы находитесь в папке репозитория hello `iot-hub-node-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-125">Make sure that you're in hello repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="bb8d8-126">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="bb8d8-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="bb8d8-127">файл Hello в hello `app` подпапка является hello ключа исходного файла, содержащего hello кода toomonitor входящие сообщения от центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="bb8d8-128">Hello `blinkLED` hello Индикатор мигает функции.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Структура репозитория в пример приложения hello][repo-structure]
2. <span data-ttu-id="bb8d8-130">Инициализируйте hello файл конфигурации, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="bb8d8-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="bb8d8-131">Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция] [ create-an-azure-function-app-and-storage-account] на этом компьютере наследуются все конфигурации hello, поэтому вы можете пропустить задачу toohello hello шаг развертывания и Выполнение образца приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="bb8d8-132">Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция] [ create-an-azure-function-app-and-storage-account] на другом компьютере, необходимо tooreplace hello меток-заполнителей в hello `config-edison.json` файла.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="bb8d8-133">Hello `config-edison.json` файл находится в подпапке hello домашней папке.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Содержимое файла конфигурации edison.json hello](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="bb8d8-135">Замените **[устройства имя узла или IP-адрес]** с IP-адрес устройства hello помечен работу при настройке устройства.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="bb8d8-136">Замените **[строка подключения устройств IoT]** со строкой подключения устройства hello, можно получить, выполнив hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` команды.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="bb8d8-137">Замените **[строка подключения концентратора IoT]** с hello строка подключения концентратора IoT, можно получить, выполнив hello `az iot hub show-connection-string --name {my hub name}` команды.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="bb8d8-138">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="bb8d8-138">Deploy and run hello sample application</span></span>
<span data-ttu-id="bb8d8-139">Развертывание и запуск образца приложения hello на Edison, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="bb8d8-139">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="bb8d8-140">Команда gulp Hello развертывает tooEdison приложения образец hello.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-140">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="bb8d8-141">Затем она запускает приложение hello Edison и отдельную задачу на узле tooEdison сообщений blink toosend 20 компьютера из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-141">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="bb8d8-142">После запуска образца приложения hello, она запускает прослушивание toomessages из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-142">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="bb8d8-143">В то же время задачу hello gulp отправляет несколько сообщений «blink» из вашей tooEdison концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-143">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="bb8d8-144">Для каждого получаемого Edison сообщения blink hello образец приложения вызывает hello `blinkLED` tooblink функции hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-144">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="bb8d8-145">Вы увидите мигающий Индикатор hello каждые две секунды как hello gulp задача отправляет 20 сообщения из вашей tooEdison концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-145">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="bb8d8-146">Hello последнего одним является сообщение «остановить», мешающий выполнению приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-146">hello last one is a "stop" message that stops hello application from running.</span></span>

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="bb8d8-148">Сводка</span><span class="sxs-lookup"><span data-stu-id="bb8d8-148">Summary</span></span>
<span data-ttu-id="bb8d8-149">Успешно отправлено сообщений из вашей IoT hub tooEdison tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-149">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="bb8d8-150">Следующая задача Hello является необязательным: изменение hello и отключать поведение hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="bb8d8-150">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb8d8-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb8d8-151">Next steps</span></span>
<span data-ttu-id="bb8d8-152">[Изменить hello и отключать поведение hello Индикатора][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="bb8d8-152">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md