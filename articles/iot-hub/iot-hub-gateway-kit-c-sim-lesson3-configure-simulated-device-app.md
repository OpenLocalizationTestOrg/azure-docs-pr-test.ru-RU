---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 3. Запуск примера приложения | Документация Майкрософт"
description: "Запустить имитированное устройство образец приложения toosend температуры данных tooyour центра IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "toocloud данных"
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
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="cbca2-104">Настройка и запуск примера приложения для имитации устройства</span><span class="sxs-lookup"><span data-stu-id="cbca2-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="cbca2-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="cbca2-105">What you will do</span></span>

- <span data-ttu-id="cbca2-106">Репозиторий образец hello клона.</span><span class="sxs-lookup"><span data-stu-id="cbca2-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="cbca2-107">Используйте hello Azure CLI tooget центр IoT и сведения о логических устройств для устройств, имитация образца приложения.</span><span class="sxs-lookup"><span data-stu-id="cbca2-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="cbca2-108">Настроить и запустить пример приложения hello имитируемые устройства.</span><span class="sxs-lookup"><span data-stu-id="cbca2-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="cbca2-109">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cbca2-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cbca2-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="cbca2-110">What you will learn</span></span>

<span data-ttu-id="cbca2-111">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="cbca2-111">In this article, you will learn:</span></span>

- <span data-ttu-id="cbca2-112">Как tooconfigure и выполнения hello имитировать образец приложения для устройства.</span><span class="sxs-lookup"><span data-stu-id="cbca2-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cbca2-113">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="cbca2-113">What you need</span></span>

<span data-ttu-id="cbca2-114">Необходимо успешно выполнить инструкции, изложенные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="cbca2-114">You must have successfully completed</span></span>

- [<span data-ttu-id="cbca2-115">Создание Центра Интернета вещей и регистрация устройства</span><span class="sxs-lookup"><span data-stu-id="cbca2-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="cbca2-116">Клон образец hello репозитория toohello главного компьютера</span><span class="sxs-lookup"><span data-stu-id="cbca2-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="cbca2-117">репозиторий образец hello tooclone, выполните следующие действия на главном компьютере hello:</span><span class="sxs-lookup"><span data-stu-id="cbca2-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="cbca2-118">Откройте командную строку в Windows или окно терминала в МacOS или Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="cbca2-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="cbca2-119">Выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="cbca2-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="cbca2-120">Настройка устройств, имитация hello и вашей NUC</span><span class="sxs-lookup"><span data-stu-id="cbca2-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="cbca2-121">Привет открыть файл конфигурации `config.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="cbca2-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="cbca2-122">Замените `"has_sensortag": true` на `"has_sensortag": false`:</span><span class="sxs-lookup"><span data-stu-id="cbca2-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![конфигурация, нет устройства TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="cbca2-124">Инициализируйте hello файл конфигурации, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="cbca2-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="cbca2-125">Откройте `config-gateway.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="cbca2-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="cbca2-126">Найдите следующие строки кода hello и замените `[device hostname or IP address]` с IP-адрес или имя hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="cbca2-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="cbca2-127">![снимок экрана настройки шлюза](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="cbca2-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="cbca2-128">Получить строку подключения hello логического устройства концентратора IoT</span><span class="sxs-lookup"><span data-stu-id="cbca2-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="cbca2-129">hello tooget строка подключения концентратора Azure IoT логического устройства, запустите следующую команду на главном компьютере hello hello:</span><span class="sxs-lookup"><span data-stu-id="cbca2-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="cbca2-130">`{IoT hub name}`— Имя концентратора IoT hello, который использовался.</span><span class="sxs-lookup"><span data-stu-id="cbca2-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="cbca2-131">Iot шлюз можно использовать в качестве значения hello `{resource group name}` и использовать в качестве значения hello mydevice `{device id}` Если вы не изменили значение hello в занятии 2.</span><span class="sxs-lookup"><span data-stu-id="cbca2-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="cbca2-132">Настройка hello имитируемые устройства облака передачи образца приложения</span><span class="sxs-lookup"><span data-stu-id="cbca2-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="cbca2-133">tooconfigure и выполнения hello имитируемые устройства облако загрузить пример приложения, выполните следующие действия на главном компьютере hello:</span><span class="sxs-lookup"><span data-stu-id="cbca2-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="cbca2-134">Откройте `config-sensortag.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="cbca2-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![снимок экрана настройки SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="cbca2-136">Внесите hello после замены в коде hello.</span><span class="sxs-lookup"><span data-stu-id="cbca2-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="cbca2-137">Замените `[IoT hub name]` с именем концентратора IoT hello.</span><span class="sxs-lookup"><span data-stu-id="cbca2-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="cbca2-138">Замените `[IoT device connection string]` со строкой hello подключения логического устройства концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="cbca2-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="cbca2-139">Запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="cbca2-139">Run hello application.</span></span>

   <span data-ttu-id="cbca2-140">Развертывание и запуск приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="cbca2-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="cbca2-141">Проверка работы приложения образца hello</span><span class="sxs-lookup"><span data-stu-id="cbca2-141">Verify hello sample application works</span></span>

<span data-ttu-id="cbca2-142">Теперь вы увидите выходные данные hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cbca2-142">You should now see output like hello following:</span></span>

![выходные данные примера приложения для имитации устройства](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="cbca2-144">приложение Hello отправляет температуры данных tooyour IoT hub, который длится 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="cbca2-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="cbca2-145">Сводка</span><span class="sxs-lookup"><span data-stu-id="cbca2-145">Summary</span></span>

<span data-ttu-id="cbca2-146">Успешной настройки и выполнения hello имитируемые устройства облака загрузки примера приложения, которое отправляет центр IoT tooyour данных с устройств, имитация.</span><span class="sxs-lookup"><span data-stu-id="cbca2-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbca2-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cbca2-147">Next steps</span></span>
[<span data-ttu-id="cbca2-148">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="cbca2-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)