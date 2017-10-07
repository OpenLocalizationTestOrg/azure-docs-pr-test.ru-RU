---
title: "Подключение Arduino tooAzure IoT — занятия 1: развертывание приложения | Документы Microsoft"
description: "Клонировать hello образец приложения Arduino из GitHub и запустите это приложение tooyour Wi-Fi M0 Растушевка Adafruit gulp toodeploy. В этом образце приложения мигает hello объект групповой ПОЛИТИКИ"
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
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="bb8dd-105">Создание и развертывание приложения hello мерцания</span><span class="sxs-lookup"><span data-stu-id="bb8dd-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="bb8dd-106">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="bb8dd-106">What you will do</span></span>
<span data-ttu-id="bb8dd-107">Клонировать hello образец приложения Arduino из GitHub и использовать hello gulp средство toodeploy hello образец приложения tooyour Adafruit Растушевка M0 Wi-Fi Arduino системной платы.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="bb8dd-108">Каждое приложение hello объект групповой ПОЛИТИКИ #13 на barod для Hello образец ПРИВЕЛО каждые две секунды.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="bb8dd-109">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="bb8dd-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bb8dd-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="bb8dd-110">What you will learn</span></span>
* <span data-ttu-id="bb8dd-111">Как toodeploy и выполнения hello образец приложения в Arduino на доске.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bb8dd-112">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="bb8dd-112">What you need</span></span>
<span data-ttu-id="bb8dd-113">Необходимо успешно выполнить hello следующие операции:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="bb8dd-114">[Настройка устройства][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="bb8dd-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="bb8dd-115">[Получить средства hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="bb8dd-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="bb8dd-116">Привет открыть образец приложения</span><span class="sxs-lookup"><span data-stu-id="bb8dd-116">Open hello sample application</span></span>
<span data-ttu-id="bb8dd-117">tooopen hello образец приложения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="bb8dd-118">Клонирование репозитория образец hello из GitHub, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="bb8dd-119">Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Структура репозитория][repo-structure]

<span data-ttu-id="bb8dd-121">Hello `app.ino` файла в hello `app` подпапка является hello ключа исходного файла, содержащего hello toocontrol кода hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="bb8dd-122">Установка зависимостей приложения</span><span class="sxs-lookup"><span data-stu-id="bb8dd-122">Install application dependencies</span></span>
<span data-ttu-id="bb8dd-123">Установка библиотеки hello и другие модули, необходимые для образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="bb8dd-124">Настройка подключения устройства hello</span><span class="sxs-lookup"><span data-stu-id="bb8dd-124">Configure hello device connection</span></span>
<span data-ttu-id="bb8dd-125">tooconfigure Здравствуйте подключения устройства, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="bb8dd-126">Получите hello последовательного порта hello устройства с cli обнаружения устройства hello.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="bb8dd-127">Должны видеть выходные данные, аналогичные следующие toohello и найти COM-порт hello usb плата Arduino: ![обнаружение устройств][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="bb8dd-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="bb8dd-128">Привет открыть файл `config.json` в hello папку занятия и добавьте значение hello hello, найти номер COM-порта:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="bb8dd-130">Для порта hello COM, на платформе Windows, он имеет формат hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="bb8dd-131">На macOS или Ubuntu он начинается с `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="bb8dd-132">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="bb8dd-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="bb8dd-133">Установка средств требуется hello плата Arduino</span><span class="sxs-lookup"><span data-stu-id="bb8dd-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="bb8dd-134">Установите hello Azure IoT Hub SDK плата Arduino, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="bb8dd-135">Эта задача может занять длительное время toocomplete, в зависимости от сетевого подключения.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="bb8dd-136">Завершите работу hello экземпляр Arduino IDE при выполнении задачи gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="bb8dd-137">Развертывание и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="bb8dd-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="bb8dd-138">Развертывание и запуск образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="bb8dd-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="bb8dd-139">Проверки работы приложения hello</span><span class="sxs-lookup"><span data-stu-id="bb8dd-139">Verify hello app works</span></span>
<span data-ttu-id="bb8dd-140">Если вы не видите hello Индикатор мигает, см. раздел hello [руководство по устранению неполадок] [ troubleshooting-page] для решения проблемы toocommon.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![Светодиодный индикатор мигает][led-blinking]

## <a name="summary"></a><span data-ttu-id="bb8dd-142">Сводка</span><span class="sxs-lookup"><span data-stu-id="bb8dd-142">Summary</span></span>
<span data-ttu-id="bb8dd-143">Вы установили toowork hello необходимые средства с вашей платой Arduino и развернуть образец приложения tooyour Arduino плата tooblink hello Индикатора.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="bb8dd-144">Вы теперь можно создать, развернуть и запустить другой пример приложения, который подключается ваш tooAzure платы Arduino toosend центр IoT и получать сообщения.</span><span class="sxs-lookup"><span data-stu-id="bb8dd-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb8dd-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb8dd-145">Next steps</span></span>
<span data-ttu-id="bb8dd-146">[Получить инструменты Azure hello][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="bb8dd-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md