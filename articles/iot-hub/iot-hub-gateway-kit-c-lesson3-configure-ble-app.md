---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 3. Запуск примера приложения | Документация Майкрософт"
description: "Выполняются приложения tooreceive ЛЮЧИТЬ образец данных из SensorTag ЛЮЧИТЬ и концентратор IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "отключить приложение, датчик мониторинг приложения, сбор данных датчика, данные с помощью датчиков toocloud данных датчика"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="5a37f-104">Настройка и запуск примера приложения BLE</span><span class="sxs-lookup"><span data-stu-id="5a37f-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5a37f-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="5a37f-105">What you will do</span></span>

- <span data-ttu-id="5a37f-106">Репозиторий образец hello клона.</span><span class="sxs-lookup"><span data-stu-id="5a37f-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="5a37f-107">Настройте подключение hello между SensorTag и Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5a37f-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="5a37f-108">Используйте hello Azure CLI tooget центр IoT и SensorTag сведения образец приложения ЛЮЧИТЬ (низкий энергии Bluetooth).</span><span class="sxs-lookup"><span data-stu-id="5a37f-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="5a37f-109">Настроить и запустить пример приложения hello отключить.</span><span class="sxs-lookup"><span data-stu-id="5a37f-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="5a37f-110">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5a37f-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5a37f-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="5a37f-111">What you will learn</span></span>

<span data-ttu-id="5a37f-112">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="5a37f-112">In this article, you will learn:</span></span>

- <span data-ttu-id="5a37f-113">Как tooconfigure и выполнения hello ЛЮЧИТЬ образец приложения.</span><span class="sxs-lookup"><span data-stu-id="5a37f-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5a37f-114">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="5a37f-114">What you need</span></span>

<span data-ttu-id="5a37f-115">Необходимо успешно выполнить инструкции, изложенные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="5a37f-115">You must have successfully completed</span></span>

- [<span data-ttu-id="5a37f-116">Создание Центра Интернета вещей и регистрация SensorTag</span><span class="sxs-lookup"><span data-stu-id="5a37f-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="5a37f-117">Клон образец hello репозитория toohello главного компьютера</span><span class="sxs-lookup"><span data-stu-id="5a37f-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="5a37f-118">репозиторий образец hello tooclone, выполните следующие действия на главном компьютере hello:</span><span class="sxs-lookup"><span data-stu-id="5a37f-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5a37f-119">Откройте окно командной строки в Windows или терминала в macOS или Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5a37f-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="5a37f-120">Выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="5a37f-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="5a37f-121">Настроить подключение hello между SensorTag и Intel NUC</span><span class="sxs-lookup"><span data-stu-id="5a37f-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="5a37f-122">tooset копирование hello подключения, выполните следующие действия на главном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="5a37f-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5a37f-123">Инициализируйте hello файл конфигурации, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="5a37f-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="5a37f-124">Откройте `config-gateway.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="5a37f-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="5a37f-125">Найдите следующие строки кода hello и замените `[device hostname or IP address]` с hello IP-адрес или имя Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5a37f-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="5a37f-126">![снимок экрана настройки шлюза](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="5a37f-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="5a37f-127">Установите средства поддержки на Intel NUC, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="5a37f-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="5a37f-128">Включите SensorTag нажатием кнопки питания hello как hello следующий рисунок и мигания hello зеленый Индикатор.</span><span class="sxs-lookup"><span data-stu-id="5a37f-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![включение SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="5a37f-130">SensorTag устройств сканирования, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="5a37f-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="5a37f-131">Проверка подключения hello между hello SensorTag и Intel NUC, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="5a37f-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="5a37f-132">Замените `{mac address}` с MAC-адрес, полученный на предыдущем шаге hello hello.</span><span class="sxs-lookup"><span data-stu-id="5a37f-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="5a37f-133">Получить строку подключения hello объекта SensorTag</span><span class="sxs-lookup"><span data-stu-id="5a37f-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="5a37f-134">hello tooget SensorTag, запустите следующую команду на главном компьютере hello hello строка подключения концентратора Azure IoT:</span><span class="sxs-lookup"><span data-stu-id="5a37f-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="5a37f-135">`{IoT hub name}`— Имя концентратора IoT hello, который использовался.</span><span class="sxs-lookup"><span data-stu-id="5a37f-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="5a37f-136">Iot шлюз можно использовать в качестве значения hello `{resource group name}` и использовать в качестве значения hello mydevice `{device id}` Если вы не изменили значение hello в занятии 2.</span><span class="sxs-lookup"><span data-stu-id="5a37f-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="5a37f-137">Настройка образца приложения hello ЛЮЧИТЬ</span><span class="sxs-lookup"><span data-stu-id="5a37f-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="5a37f-138">tooconfigure и выполнения hello ЛЮЧИТЬ образец приложения, выполните следующие действия на главном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="5a37f-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="5a37f-139">Откройте `config-sensortag.json` в коде Visual Studio, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="5a37f-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![снимок экрана настройки SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="5a37f-141">Внесите hello после замены в коде hello.</span><span class="sxs-lookup"><span data-stu-id="5a37f-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="5a37f-142">Замените `[IoT hub name]` с именем концентратора IoT hello, который использовался.</span><span class="sxs-lookup"><span data-stu-id="5a37f-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="5a37f-143">Замените `[IoT device connection string]` со строкой соединения hello объекта SensorTag, который был получен.</span><span class="sxs-lookup"><span data-stu-id="5a37f-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="5a37f-144">Замените `[device_mac_address]` с hello hello SensorTag, полученный MAC-адрес.</span><span class="sxs-lookup"><span data-stu-id="5a37f-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="5a37f-145">Запустите образец приложения hello отключить.</span><span class="sxs-lookup"><span data-stu-id="5a37f-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="5a37f-146">hello toorun ЛЮЧИТЬ образец приложения, выполните следующие действия на главном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="5a37f-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="5a37f-147">Включите SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5a37f-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="5a37f-148">Развертывание и запуск образца приложения hello ЛЮЧИТЬ на Intel NUC, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="5a37f-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="5a37f-149">Проверить, что пример приложения hello ЛЮЧИТЬ работает</span><span class="sxs-lookup"><span data-stu-id="5a37f-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="5a37f-150">Теперь вы увидите выходные данные hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5a37f-150">You should now see an output like hello following:</span></span>

![выходные данные примера приложения BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="5a37f-152">Пример приложения Hello отслеживает сбор данных температуры и отправляет его tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="5a37f-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="5a37f-153">Пример приложения Hello автоматически завершает после отправки 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="5a37f-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="5a37f-154">Сводка</span><span class="sxs-lookup"><span data-stu-id="5a37f-154">Summary</span></span>

<span data-ttu-id="5a37f-155">Вы успешно настройки hello связи между SensorTag и Intel NUC и запустить образец приложения ЛЮЧИТЬ, который собирает и отправляет данные из центра IoT tooyour SensorTag.</span><span class="sxs-lookup"><span data-stu-id="5a37f-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="5a37f-156">Вы будете готовы toolearn как tooverify концентратор IoT получила hello данных.</span><span class="sxs-lookup"><span data-stu-id="5a37f-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a37f-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a37f-157">Next steps</span></span>
[<span data-ttu-id="5a37f-158">Чтение сообщений из Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="5a37f-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)