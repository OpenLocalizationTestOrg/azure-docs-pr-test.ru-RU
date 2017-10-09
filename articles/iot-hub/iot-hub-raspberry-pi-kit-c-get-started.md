---
title: "toocloud aaaRaspberry Pi (C) - подключения Pi Raspberry tooAzure центр IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключите Raspberry Pi tooAzure центр IoT для Raspberry Pi toosend данные toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot малиновая pi малиновая pi iot hub, малиновая pi отправки данных toocloud, малиновая pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a><span data-ttu-id="de1e1-104">Подключение Raspberry Pi tooAzure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="de1e1-104">Connect Raspberry Pi tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="de1e1-105">В этом учебнике сначала hello основы работы с Raspberry Pi, на котором выполняется Raspbian обучения.</span><span class="sxs-lookup"><span data-stu-id="de1e1-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="de1e1-106">Затем вы узнаете, как tooseamlessly подключаться toohello облачных устройств с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="de1e1-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="de1e1-107">Примеры Windows 10 IoT базовая go toohello [центра разработчиков Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="de1e1-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="de1e1-108">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="de1e1-108">Don't have a kit yet?</span></span> <span data-ttu-id="de1e1-109">Используйте [онлайн-симулятор Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="de1e1-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="de1e1-110">Или купите новый комплект [здесь](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="de1e1-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="de1e1-111">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="de1e1-111">What you do</span></span>

* <span data-ttu-id="de1e1-112">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="de1e1-112">Create an IoT hub.</span></span>
* <span data-ttu-id="de1e1-113">Зарегистрируем устройство для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="de1e1-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="de1e1-114">Настроим Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="de1e1-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="de1e1-115">Запустите образец приложения на Pi toosend датчиков данных tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="de1e1-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="de1e1-116">Подключение центра IoT tooan Raspberry Pi созданного вами.</span><span class="sxs-lookup"><span data-stu-id="de1e1-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="de1e1-117">Затем запустите пример приложения на Pi toocollect температуры и влажности данных с использованием BME280 датчиков.</span><span class="sxs-lookup"><span data-stu-id="de1e1-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="de1e1-118">Отправьте центра IoT tooyour данных датчика hello.</span><span class="sxs-lookup"><span data-stu-id="de1e1-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="de1e1-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="de1e1-119">What you learn</span></span>

* <span data-ttu-id="de1e1-120">Как toocreate центр Azure IoT и получить новые строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="de1e1-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="de1e1-121">Как tooconnect числа пи с BME280 датчика.</span><span class="sxs-lookup"><span data-stu-id="de1e1-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="de1e1-122">Как toocollect датчиков, выполнив пример приложения на Pi.</span><span class="sxs-lookup"><span data-stu-id="de1e1-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="de1e1-123">Как центр IoT tooyour данных датчика toosend.</span><span class="sxs-lookup"><span data-stu-id="de1e1-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="de1e1-124">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="de1e1-124">What you need</span></span>

![Необходимые элементы](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="de1e1-126">Здравствуйте, Raspberry Pi 2 или Raspberry Pi 3 на доске.</span><span class="sxs-lookup"><span data-stu-id="de1e1-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="de1e1-127">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="de1e1-127">An active Azure subscription.</span></span> <span data-ttu-id="de1e1-128">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="de1e1-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="de1e1-129">Монитор, USB-клавиатуры и мыши подключаются tooPi.</span><span class="sxs-lookup"><span data-stu-id="de1e1-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="de1e1-130">ПК или компьютер Mac под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="de1e1-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="de1e1-131">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="de1e1-131">An Internet connection.</span></span>
* <span data-ttu-id="de1e1-132">Карта microSD емкостью 16 ГБ или больше.</span><span class="sxs-lookup"><span data-stu-id="de1e1-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="de1e1-133">USB-SD адаптер или microSD карты tooburn hello образа операционной системы на карту microSD, hello.</span><span class="sxs-lookup"><span data-stu-id="de1e1-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="de1e1-134">Питания 2 amp 5В с hello 6 фут micro USB-кабель.</span><span class="sxs-lookup"><span data-stu-id="de1e1-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="de1e1-135">Привет, следующие элементы являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="de1e1-135">hello following items are optional:</span></span>

* <span data-ttu-id="de1e1-136">Датчик температуры, давления и влажности Adafruit BME280 в сборе.</span><span class="sxs-lookup"><span data-stu-id="de1e1-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="de1e1-137">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="de1e1-137">A breadboard.</span></span>
* <span data-ttu-id="de1e1-138">6 оптоволоконных кабелей с разъемом на одном конце и гнездом на другом.</span><span class="sxs-lookup"><span data-stu-id="de1e1-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="de1e1-139">Светодиодный индикатор 10 мм с рассеянным освещением.</span><span class="sxs-lookup"><span data-stu-id="de1e1-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="de1e1-140">Эти элементы являются необязательными, поскольку поддержка образец кода hello смоделированные данные датчиков.</span><span class="sxs-lookup"><span data-stu-id="de1e1-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="de1e1-141">Настройка Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="de1e1-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="de1e1-142">Установка операционной системы Raspbian hello для Pi</span><span class="sxs-lookup"><span data-stu-id="de1e1-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="de1e1-143">Подготовьте карта microSD hello для установки образа Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="de1e1-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="de1e1-144">Скачайте ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="de1e1-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="de1e1-145">[Загрузите детском Raspbian с рабочим столом](https://www.raspberrypi.org/downloads/raspbian/) (hello ZIP-файл).</span><span class="sxs-lookup"><span data-stu-id="de1e1-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="de1e1-146">Извлеките hello Raspbian изображения tooa папку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="de1e1-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="de1e1-147">Установите карту microSD toohello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="de1e1-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="de1e1-148">[Загрузите и установите программу записи карты SD гравировальная hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="de1e1-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="de1e1-149">Запустите гравировальная и выберите изображение Raspbian hello, извлеченный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="de1e1-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="de1e1-150">Выберите диск, карту microSD hello.</span><span class="sxs-lookup"><span data-stu-id="de1e1-150">Select hello microSD card drive.</span></span> <span data-ttu-id="de1e1-151">Обратите внимание, что гравировальная может уже выбран правильный диск hello.</span><span class="sxs-lookup"><span data-stu-id="de1e1-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="de1e1-152">Щелкните карту microSD toohello Raspbian tooinstall флэш-памяти.</span><span class="sxs-lookup"><span data-stu-id="de1e1-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="de1e1-153">Удаление карта microSD hello с компьютера после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="de1e1-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="de1e1-154">Это карта microSD безопасные tooremove hello непосредственно из-за гравировальная автоматически извлечение или отключение карта microSD hello после завершения.</span><span class="sxs-lookup"><span data-stu-id="de1e1-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="de1e1-155">Вставьте карту microSD hello в Pi.</span><span class="sxs-lookup"><span data-stu-id="de1e1-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="de1e1-156">Включение SSH и SPI</span><span class="sxs-lookup"><span data-stu-id="de1e1-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="de1e1-157">Подключение Pi toohello монитора, клавиатуры и мыши, запустите Pi и затем войдите Raspbian с помощью `pi` имени пользователя hello и `raspberry` hello паролем.</span><span class="sxs-lookup"><span data-stu-id="de1e1-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="de1e1-158">Щелкните значок малиновая hello > **предпочтения** > **Raspberry Pi конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="de1e1-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![меню настройки Raspbian Hello](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="de1e1-160">На hello **интерфейсы** установите **SPI** и **SSH** слишком**включить**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="de1e1-160">On hello **Interfaces** tab, set **SPI** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="de1e1-161">Если нет физических датчиков и toouse смоделированные данные датчика, этот шаг является необязательным.</span><span class="sxs-lookup"><span data-stu-id="de1e1-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Включение SPI и SSH на Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="de1e1-163">tooenable SSH и SPI, можно найти дополнительные справочные документы на [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) и [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="de1e1-163">tooenable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="de1e1-164">Подключение tooPi датчик hello</span><span class="sxs-lookup"><span data-stu-id="de1e1-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="de1e1-165">Используйте hello breadboard и перемычки проводов tooconnect Светодиодный индикатор и BME280 tooPi.</span><span class="sxs-lookup"><span data-stu-id="de1e1-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="de1e1-166">Если у вас нет датчик hello [пропустите этот раздел](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="de1e1-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hello Raspberry Pi и датчик подключения](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="de1e1-168">Датчик Hello BME280 можно собирать данные, температуры и влажности.</span><span class="sxs-lookup"><span data-stu-id="de1e1-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="de1e1-169">И hello Индикатор мигает, при наличии связи между локальными устройствами и hello.</span><span class="sxs-lookup"><span data-stu-id="de1e1-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="de1e1-170">Для датчика ПИН-коды используйте hello после подключения:</span><span class="sxs-lookup"><span data-stu-id="de1e1-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="de1e1-171">Начало (датчик и светодиодный индикатор)</span><span class="sxs-lookup"><span data-stu-id="de1e1-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="de1e1-172">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="de1e1-172">End (Board)</span></span>            | <span data-ttu-id="de1e1-173">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="de1e1-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="de1e1-174">LED VDD (вывод 5G)</span><span class="sxs-lookup"><span data-stu-id="de1e1-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="de1e1-175">GPIO 4 (вывод 7)</span><span class="sxs-lookup"><span data-stu-id="de1e1-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="de1e1-176">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="de1e1-176">White cable</span></span>   |
| <span data-ttu-id="de1e1-177">LED GND (вывод 6G)</span><span class="sxs-lookup"><span data-stu-id="de1e1-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="de1e1-178">GND (вывод 6)</span><span class="sxs-lookup"><span data-stu-id="de1e1-178">GND (Pin 6)</span></span>            | <span data-ttu-id="de1e1-179">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="de1e1-179">Black cable</span></span>   |
| <span data-ttu-id="de1e1-180">VDD (вывод 18F)</span><span class="sxs-lookup"><span data-stu-id="de1e1-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="de1e1-181">3.3V PWR (вывод 17)</span><span class="sxs-lookup"><span data-stu-id="de1e1-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="de1e1-182">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="de1e1-182">White cable</span></span>   |
| <span data-ttu-id="de1e1-183">GND (вывод 20F)</span><span class="sxs-lookup"><span data-stu-id="de1e1-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="de1e1-184">GND (вывод 20)</span><span class="sxs-lookup"><span data-stu-id="de1e1-184">GND (Pin 20)</span></span>           | <span data-ttu-id="de1e1-185">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="de1e1-185">Black cable</span></span>   |
| <span data-ttu-id="de1e1-186">SCK (вывод 21F)</span><span class="sxs-lookup"><span data-stu-id="de1e1-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="de1e1-187">SPI0 SCLK (вывод 23)</span><span class="sxs-lookup"><span data-stu-id="de1e1-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="de1e1-188">Оранжевый кабель</span><span class="sxs-lookup"><span data-stu-id="de1e1-188">Orange cable</span></span>  |
| <span data-ttu-id="de1e1-189">SDO (вывод 22F)</span><span class="sxs-lookup"><span data-stu-id="de1e1-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="de1e1-190">SPI0 MISO (вывод 21)</span><span class="sxs-lookup"><span data-stu-id="de1e1-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="de1e1-191">Желтый кабель</span><span class="sxs-lookup"><span data-stu-id="de1e1-191">Yellow cable</span></span>  |
| <span data-ttu-id="de1e1-192">SDI (вывод 23F)</span><span class="sxs-lookup"><span data-stu-id="de1e1-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="de1e1-193">SPI0 MOSI (вывод 19)</span><span class="sxs-lookup"><span data-stu-id="de1e1-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="de1e1-194">Зеленый кабель</span><span class="sxs-lookup"><span data-stu-id="de1e1-194">Green cable</span></span>   |
| <span data-ttu-id="de1e1-195">CS (вывод 24F)</span><span class="sxs-lookup"><span data-stu-id="de1e1-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="de1e1-196">SPI0 CS (вывод 24)</span><span class="sxs-lookup"><span data-stu-id="de1e1-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="de1e1-197">Синий кабель</span><span class="sxs-lookup"><span data-stu-id="de1e1-197">Blue cable</span></span>    |

<span data-ttu-id="de1e1-198">Нажмите кнопку tooview [Raspberry Pi 2 и 3 ПИН-код сопоставления](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) для справки.</span><span class="sxs-lookup"><span data-stu-id="de1e1-198">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="de1e1-199">После успешного соединения BME280 tooyour Raspberry Pi должно быть как под изображением.</span><span class="sxs-lookup"><span data-stu-id="de1e1-199">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Подключенный компьютер Pi и датчик BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="de1e1-201">Подключение к сети toohello Pi</span><span class="sxs-lookup"><span data-stu-id="de1e1-201">Connect Pi toohello network</span></span>

<span data-ttu-id="de1e1-202">Включите Pi при помощи micro USB-кабель hello и hello питания.</span><span class="sxs-lookup"><span data-stu-id="de1e1-202">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="de1e1-203">Используйте hello Ethernet кабель tooconnect Pi tooyour проводной сети, или выполните hello [инструкции hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="de1e1-203">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="de1e1-204">После вашей Pi было успешно выполнено подключение toohello сети, необходимо tootake заметку hello [IP-адрес вашего Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="de1e1-204">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Toowired подключенной сети](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="de1e1-206">Запуск примера приложения на Pi</span><span class="sxs-lookup"><span data-stu-id="de1e1-206">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="de1e1-207">Установите пакеты необходимых компонентов hello</span><span class="sxs-lookup"><span data-stu-id="de1e1-207">Install hello prerequisite packages</span></span>

1. <span data-ttu-id="de1e1-208">Используйте одну из hello следующую SSH клиентов из вашего узла компьютера tooconnect tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="de1e1-208">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="de1e1-209">**Пользователи Windows**</span><span class="sxs-lookup"><span data-stu-id="de1e1-209">**Windows Users**</span></span>
   1. <span data-ttu-id="de1e1-210">Скачайте и установите [PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="de1e1-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="de1e1-211">Скопируйте hello IP-адрес раздела Pi в hello узел имя (или IP-адрес) и выберите в качестве типа соединения hello SSH.</span><span class="sxs-lookup"><span data-stu-id="de1e1-211">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="de1e1-213">**Пользователи MAC и Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="de1e1-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="de1e1-214">Используйте встроенный клиент SSH hello Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="de1e1-214">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="de1e1-215">Может потребоваться toorun `ssh pi@<ip address of pi>` tooconnect Pi по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="de1e1-215">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="de1e1-216">имя пользователя по умолчанию Hello `pi` , и пароль hello `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="de1e1-216">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="de1e1-217">Установите пакеты необходимых компонентов hello для hello IoT устройство Microsoft Azure SDK для C и Cmake, выполнив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="de1e1-217">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C and Cmake by running hello following commands:</span></span>

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a><span data-ttu-id="de1e1-218">Настройка образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="de1e1-218">Configure hello sample application</span></span>

1. <span data-ttu-id="de1e1-219">Пример приложения hello клона, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="de1e1-219">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="de1e1-220">Откройте файл конфигурации hello, запустив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="de1e1-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Файл конфигурации](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="de1e1-222">В этом файле можно настроить два макроса.</span><span class="sxs-lookup"><span data-stu-id="de1e1-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="de1e1-223">Hello сначала он `INTERVAL`, который определяет hello временной интервал (в миллисекундах) между двумя сообщений, передаваемых toocloud.</span><span class="sxs-lookup"><span data-stu-id="de1e1-223">hello first one is `INTERVAL`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="de1e1-224">Здравствуйте, вторая — `SIMULATED_DATA`, — логическое значение для ли toouse смоделированные данные датчиков или нет.</span><span class="sxs-lookup"><span data-stu-id="de1e1-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="de1e1-225">Если вы **нет hello датчика**, задайте hello `SIMULATED_DATA` значение слишком`1` пример приложения hello toomake создать и использовать имитацию датчиков.</span><span class="sxs-lookup"><span data-stu-id="de1e1-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="de1e1-226">Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.</span><span class="sxs-lookup"><span data-stu-id="de1e1-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="de1e1-227">Построение и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="de1e1-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="de1e1-228">Построение образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="de1e1-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Выходные данные при создании](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="de1e1-230">Выполните пример приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="de1e1-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="de1e1-231">Убедитесь, что вы скопированные и вставленные строки подключения устройств hello в одинарных кавычках hello.</span><span class="sxs-lookup"><span data-stu-id="de1e1-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="de1e1-232">Вы увидите следующее hello выходных данных, показано hello датчик данных и hello сообщений, отправляемых tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="de1e1-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Вывод — данные датчика, отправленные из центра IoT tooyour Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="de1e1-234">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de1e1-234">Next steps</span></span>

<span data-ttu-id="de1e1-235">Вы впервые запускаете в образце данных датчика toocollect приложения и отправьте его центр IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="de1e1-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="de1e1-236">сообщения приветствия toosee, Pi вашей Raspberry отправленных IoT tooyour концентратор или отправки tooyour сообщений Raspberry Pi в интерфейс командной строки, в разделе hello [управление облака устройство обмен сообщениями с центром IOT учебнике](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="de1e1-236">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
