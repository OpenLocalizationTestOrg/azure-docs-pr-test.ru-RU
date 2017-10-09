---
title: "Connect Arduino (C) tooAzure IoT — занятия 4: облака на устройство | Документы Microsoft"
description: "Пример приложения выполняется на устройстве Adafruit Feather M0 WiFi и отслеживает входящие сообщения от Центра Интернета вещей. Новая задача gulp отправляет сообщения tooAdafruit Растушевка M0 Wi-Fi из вашего hello tooblink концентратора IoT Индикатора."
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
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="7b61e-105">Запустите образец приложения tooreceive сообщений облака на устройство</span><span class="sxs-lookup"><span data-stu-id="7b61e-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="7b61e-106">В этой статье на плате Adafruit Feather M0 WiFi Arduino развертывается пример приложения.</span><span class="sxs-lookup"><span data-stu-id="7b61e-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="7b61e-107">Пример приложения Hello отслеживает входящие сообщения от вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="7b61e-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="7b61e-108">Вы также выполнение задачи gulp на ваш компьютер tooyour сообщения toosend плата Arduino из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="7b61e-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="7b61e-109">Пример приложения hello, получив сообщений hello, он мигает Индикатор hello.</span><span class="sxs-lookup"><span data-stu-id="7b61e-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="7b61e-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="7b61e-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7b61e-111">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="7b61e-111">What you will do</span></span>
* <span data-ttu-id="7b61e-112">Подключите пример приложения hello tooyour-центр IoT.</span><span class="sxs-lookup"><span data-stu-id="7b61e-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="7b61e-113">Развертывание и запуск образца приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7b61e-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="7b61e-114">Отправьте сообщения из вашей IoT hub tooyour Arduino плата tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="7b61e-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7b61e-115">Новые знания</span><span class="sxs-lookup"><span data-stu-id="7b61e-115">What you will learn</span></span>
<span data-ttu-id="7b61e-116">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="7b61e-116">In this article, you will learn:</span></span>
* <span data-ttu-id="7b61e-117">Способ toomonitor входящих сообщений из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="7b61e-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="7b61e-118">Способ toosend облака на устройство сообщений из вашей tooyour концентратора IoT Arduino платы.</span><span class="sxs-lookup"><span data-stu-id="7b61e-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7b61e-119">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="7b61e-119">What you need</span></span>
* <span data-ttu-id="7b61e-120">Плата Arduino, настроенная для работы.</span><span class="sxs-lookup"><span data-stu-id="7b61e-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="7b61e-121">в статье tooset вашей платы Arduino toolearn [настройки устройства][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="7b61e-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="7b61e-122">Центр Интернета вещей, созданный в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="7b61e-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="7b61e-123">toolearn как toocreate ваш центр IoT. в разделе [создать концентратор IoT Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="7b61e-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="7b61e-124">Пример приложения hello tooyour-центр IoT подключения</span><span class="sxs-lookup"><span data-stu-id="7b61e-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="7b61e-125">Убедитесь, что вы находитесь в папке репозитория hello `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="7b61e-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="7b61e-126">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="7b61e-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="7b61e-127">Обратите внимание hello `app.ino` файла в hello `app` вложенную папку.</span><span class="sxs-lookup"><span data-stu-id="7b61e-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="7b61e-128">Hello `app.ino` файл является hello ключа исходного файла, содержащего hello кода toomonitor входящие сообщения от центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="7b61e-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="7b61e-129">Hello `blinkLED` hello Индикатор мигает функции.</span><span class="sxs-lookup"><span data-stu-id="7b61e-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Структура репозитория в пример приложения hello][repo-structure]

2. <span data-ttu-id="7b61e-131">Получите hello последовательного порта hello устройства с cli обнаружения устройства hello.</span><span class="sxs-lookup"><span data-stu-id="7b61e-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="7b61e-132">Должны видеть выходные данные, аналогичные следующие toohello и найти COM-порт hello usb плата Arduino:</span><span class="sxs-lookup"><span data-stu-id="7b61e-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Обнаружение устройства][device-discovery]

3. <span data-ttu-id="7b61e-134">Привет открыть файл `config.json` в папке занятия hello и значение входной hello hello, найти номер COM-порта:</span><span class="sxs-lookup"><span data-stu-id="7b61e-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="7b61e-136">Для порта hello COM, на платформе Windows, он имеет формат hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="7b61e-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="7b61e-137">На платформе MacOS или Ubuntu он будет начинаться с `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="7b61e-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="7b61e-138">Инициализируйте hello файл конфигурации, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="7b61e-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="7b61e-139">Сделать после замены в hello hello `config-arduino.json` файла:</span><span class="sxs-lookup"><span data-stu-id="7b61e-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="7b61e-140">Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция] [ create-an-azure-function-app-and-storage-account] на этом компьютере наследуются все конфигурации hello, поэтому вы можете пропустить задачу toohello hello шаг развертывания и Выполнение образца приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7b61e-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="7b61e-141">Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция] [ create-an-azure-function-app-and-storage-account] на другом компьютере, необходимо tooreplace hello меток-заполнителей в hello `config-arduino.json` файла.</span><span class="sxs-lookup"><span data-stu-id="7b61e-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="7b61e-142">Hello `config-arduino.json` файл находится в подпапке hello домашней папке.</span><span class="sxs-lookup"><span data-stu-id="7b61e-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Содержимое файла конфигурации arduino.json hello][config-arduino-json]

   * <span data-ttu-id="7b61e-144">Замените **[Wi-Fi SSID]** с вашей SSID Wi-Fi, подключенный toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="7b61e-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="7b61e-145">Замените **[Wi-Fi password]** своим паролем Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="7b61e-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="7b61e-146">Удалите строку hello, если Wi-Fi не требует пароля.</span><span class="sxs-lookup"><span data-stu-id="7b61e-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="7b61e-147">Замените **[строка подключения устройств IoT]** со строкой подключения устройства hello, можно получить, выполнив hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` команды.</span><span class="sxs-lookup"><span data-stu-id="7b61e-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="7b61e-148">Замените **[строка подключения концентратора IoT]** с hello строка подключения концентратора IoT, можно получить, выполнив hello `az iot hub show-connection-string --name {my hub name}` команды.</span><span class="sxs-lookup"><span data-stu-id="7b61e-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="7b61e-149">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="7b61e-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="7b61e-150">Развертывание и запуск образца приложения hello в Arduino на доске, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="7b61e-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="7b61e-151">Команда gulp Hello развертывает hello образец приложения tooyour Arduino платы.</span><span class="sxs-lookup"><span data-stu-id="7b61e-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="7b61e-152">Затем она запускает приложение hello на доске Arduino и отдельную задачу на узле компьютера toosend 20 blink сообщения tooyour Arduino плата из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="7b61e-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="7b61e-153">После запуска образца приложения hello, она запускает прослушивание toomessages из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="7b61e-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="7b61e-154">В то же время задачу hello gulp отправляет несколько сообщений «blink» из вашей tooyour концентратора IoT Arduino платы.</span><span class="sxs-lookup"><span data-stu-id="7b61e-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="7b61e-155">Вызывается для каждого сообщения blink hello плата получает, пример приложения hello hello `blinkLED` tooblink функции hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="7b61e-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="7b61e-156">Вы увидите hello Индикатор мигает каждые две секунды как задачу hello gulp 20 сообщения отправляются от вашей tooyour концентратора IoT Arduino платы.</span><span class="sxs-lookup"><span data-stu-id="7b61e-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="7b61e-157">Hello последнего одним является сообщение «остановить», мешающий выполнению приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7b61e-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора][sample-application]

## <a name="summary"></a><span data-ttu-id="7b61e-159">Сводка</span><span class="sxs-lookup"><span data-stu-id="7b61e-159">Summary</span></span>
<span data-ttu-id="7b61e-160">Успешно отправлено сообщений из вашей IoT hub tooyour Arduino плата tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="7b61e-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="7b61e-161">Следующая задача Hello является необязательным: изменение hello и отключать поведение hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="7b61e-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b61e-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b61e-162">Next steps</span></span>
<span data-ttu-id="7b61e-163">[Изменить hello и отключать поведение hello Индикатора][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="7b61e-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


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