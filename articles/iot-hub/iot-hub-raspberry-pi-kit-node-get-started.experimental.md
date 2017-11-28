---
title: "toocloud aaaRaspberry Pi (Node.js) - подключения Pi Raspberry tooAzure центр IoT | Документы Microsoft"
description: "Подключите Raspberry Pi tooAzure центр IoT для Raspberry Pi toosend данные toohello облако Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure iot малиновая pi малиновая pi iot hub, малиновая pi отправки данных toocloud, малиновая pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="c6c4d-104">Подключение tooAzure Raspberry Pi центр IoT (Node.js)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="c6c4d-105">В этом учебнике сначала hello основы работы с Raspberry Pi, на котором выполняется Raspbian обучения.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="c6c4d-106">Затем вы узнаете, как tooseamlessly подключаться toohello облачных устройств с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="c6c4d-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="c6c4d-107">Примеры Windows 10 IoT базовая go toohello [центра разработчиков Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="c6c4d-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="c6c4d-108">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="c6c4d-108">Don't have a kit yet?</span></span> <span data-ttu-id="c6c4d-109">Повторите hello [Raspberry Pi 3 эмулятор](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="c6c4d-109">Try hello [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="c6c4d-110">Или купите новый комплект [здесь](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="c6c4d-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c6c4d-111">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="c6c4d-111">What you do</span></span>

* <span data-ttu-id="c6c4d-112">Настроим Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="c6c4d-113">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-113">Create an IoT hub.</span></span>
* <span data-ttu-id="c6c4d-114">Зарегистрируем устройство для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="c6c4d-115">Запустите образец приложения на Pi toosend датчиков данных tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="c6c4d-116">Подключение центра IoT tooan Raspberry Pi созданного вами.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="c6c4d-117">Затем запустите пример приложения на Pi toocollect температуры и влажности данных с использованием BME280 датчиков.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="c6c4d-118">Отправьте центра IoT tooyour данных датчика hello.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="c6c4d-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="c6c4d-119">What you learn</span></span>

* <span data-ttu-id="c6c4d-120">Как toocreate центр Azure IoT и получить новые строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="c6c4d-121">Как tooconnect числа пи с BME280 датчика.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="c6c4d-122">Как toocollect датчиков, выполнив пример приложения на Pi.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="c6c4d-123">Как центр IoT tooyour данных датчика toosend.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c6c4d-124">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="c6c4d-124">What you need</span></span>

![Необходимые элементы](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="c6c4d-126">Здравствуйте, Raspberry Pi 2 или Raspberry Pi 3 на доске.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="c6c4d-127">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-127">An active Azure subscription.</span></span> <span data-ttu-id="c6c4d-128">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="c6c4d-129">Монитор, USB-клавиатуры и мыши подключаются tooPi.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="c6c4d-130">ПК или компьютер Mac под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="c6c4d-131">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-131">An Internet connection.</span></span>
* <span data-ttu-id="c6c4d-132">Карта microSD емкостью 16 ГБ или больше.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="c6c4d-133">USB-SD адаптер или microSD карты tooburn hello образа операционной системы на карту microSD, hello.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="c6c4d-134">Питания 2 amp 5В с hello 6 фут micro USB-кабель.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="c6c4d-135">Привет, следующие элементы являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-135">hello following items are optional:</span></span>

* <span data-ttu-id="c6c4d-136">Датчик температуры, давления и влажности Adafruit BME280 в сборе.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="c6c4d-137">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-137">A breadboard.</span></span>
* <span data-ttu-id="c6c4d-138">6 оптоволоконных кабелей с разъемом на одном конце и гнездом на другом.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="c6c4d-139">Светодиодный индикатор 10 мм с рассеянным освещением.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="c6c4d-140">Эти элементы являются необязательными, поскольку поддержка образец кода hello смоделированные данные датчиков.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="c6c4d-141">Настройка Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="c6c4d-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="c6c4d-142">Установка операционной системы Raspbian hello для Pi</span><span class="sxs-lookup"><span data-stu-id="c6c4d-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="c6c4d-143">Подготовьте карта microSD hello для установки образа Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="c6c4d-144">Скачайте ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="c6c4d-145">[Загрузите детском Raspbian с пикселей](https://www.raspberrypi.org/downloads/raspbian/) (hello ZIP-файл).</span><span class="sxs-lookup"><span data-stu-id="c6c4d-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="c6c4d-146">Извлеките hello Raspbian изображения tooa папку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="c6c4d-147">Установите карту microSD toohello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="c6c4d-148">[Загрузите и установите программу записи карты SD гравировальная hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="c6c4d-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="c6c4d-149">Запустите гравировальная и выберите изображение Raspbian hello, извлеченный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="c6c4d-150">Выберите диск, карту microSD hello.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-150">Select hello microSD card drive.</span></span> <span data-ttu-id="c6c4d-151">Обратите внимание, что гравировальная может уже выбран правильный диск hello.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="c6c4d-152">Щелкните карту microSD toohello Raspbian tooinstall флэш-памяти.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="c6c4d-153">Удаление карта microSD hello с компьютера после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="c6c4d-154">Это карта microSD безопасные tooremove hello непосредственно из-за гравировальная автоматически извлечение или отключение карта microSD hello после завершения.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="c6c4d-155">Вставьте карту microSD hello в Pi.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="c6c4d-156">Включение SSH и I2C</span><span class="sxs-lookup"><span data-stu-id="c6c4d-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="c6c4d-157">Подключение Pi toohello монитора, клавиатуры и мыши, запустите Pi и затем войдите Raspbian с помощью `pi` имени пользователя hello и `raspberry` hello паролем.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="c6c4d-158">Щелкните значок малиновая hello > **предпочтения** > **Raspberry Pi конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![меню настройки Raspbian Hello](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="c6c4d-160">На hello **интерфейсы** установите **I2C** и **SSH** слишком**включить**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="c6c4d-161">Если нет физических датчиков и toouse смоделированные данные датчика, этот шаг является необязательным.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Включение I2C и SSH на Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="c6c4d-163">tooenable SSH и I2C, можно найти дополнительные справочные документы на [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) и [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="c6c4d-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="c6c4d-164">Подключение tooPi датчик hello</span><span class="sxs-lookup"><span data-stu-id="c6c4d-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="c6c4d-165">Используйте hello breadboard и перемычки проводов tooconnect Светодиодный индикатор и BME280 tooPi.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="c6c4d-166">При отсутствии датчик hello, пропустите этот раздел.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-166">If you don’t have hello sensor, skip this section.</span></span>

![Hello Raspberry Pi и датчик подключения](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="c6c4d-168">Датчик Hello BME280 можно собирать данные, температуры и влажности.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="c6c4d-169">И hello Индикатор мигает, при наличии связи между локальными устройствами и hello.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="c6c4d-170">Для датчика ПИН-коды используйте hello после подключения:</span><span class="sxs-lookup"><span data-stu-id="c6c4d-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="c6c4d-171">Начало (датчик и светодиодный индикатор)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="c6c4d-172">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-172">End (Board)</span></span>            | <span data-ttu-id="c6c4d-173">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="c6c4d-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="c6c4d-174">VDD (вывод 5G)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="c6c4d-175">3.3V PWR (вывод 1)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="c6c4d-176">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="c6c4d-176">White cable</span></span>   |
| <span data-ttu-id="c6c4d-177">GND (вывод 7G)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="c6c4d-178">GND (вывод 6)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-178">GND (Pin 6)</span></span>            | <span data-ttu-id="c6c4d-179">Коричневый кабель</span><span class="sxs-lookup"><span data-stu-id="c6c4d-179">Brown cable</span></span>   |
| <span data-ttu-id="c6c4d-180">SCK (вывод 8G)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="c6c4d-181">I2C1 SDA (вывод 3)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="c6c4d-182">Оранжевый кабель</span><span class="sxs-lookup"><span data-stu-id="c6c4d-182">Orange cable</span></span>  |
| <span data-ttu-id="c6c4d-183">SDI (вывод 10G)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="c6c4d-184">I2C1 SCL (вывод 5)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="c6c4d-185">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="c6c4d-185">Red cable</span></span>     |
| <span data-ttu-id="c6c4d-186">LED VDD (вывод 18F)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="c6c4d-187">GPIO 24 (вывод 18)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="c6c4d-188">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="c6c4d-188">White cable</span></span>   |
| <span data-ttu-id="c6c4d-189">LED GND (вывод 17F)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="c6c4d-190">GND (вывод 20)</span><span class="sxs-lookup"><span data-stu-id="c6c4d-190">GND (Pin 20)</span></span>           | <span data-ttu-id="c6c4d-191">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="c6c4d-191">Black cable</span></span>   |

<span data-ttu-id="c6c4d-192">Нажмите кнопку tooview [Raspberry Pi 2 и 3 ПИН-код сопоставления](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) для справки.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="c6c4d-193">После успешного соединения BME280 tooyour Raspberry Pi должно быть как под изображением.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Подключенный компьютер Pi и датчик BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="c6c4d-195">Подключение к сети toohello Pi</span><span class="sxs-lookup"><span data-stu-id="c6c4d-195">Connect Pi toohello network</span></span>

<span data-ttu-id="c6c4d-196">Включите Pi при помощи micro USB-кабель hello и hello питания.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="c6c4d-197">Используйте hello Ethernet кабель tooconnect Pi tooyour проводной сети, или выполните hello [инструкции hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="c6c4d-198">После вашей Pi было успешно выполнено подключение toohello сети, необходимо tootake заметку hello [IP-адрес вашего Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="c6c4d-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Toowired подключенной сети](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="c6c4d-200">Убедитесь, что Pi подключенных toohello сетевых как на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="c6c4d-201">Например, если компьютер находится подключенных tooa беспроводной сети при подключенном tooa проводной сети Pi, могут отображаться не hello IP адрес в выходных данных devdisco hello.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="c6c4d-202">Запуск примера приложения на Pi</span><span class="sxs-lookup"><span data-stu-id="c6c4d-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="c6c4d-203">Клонирование образца приложения и установите пакеты необходимых компонентов hello</span><span class="sxs-lookup"><span data-stu-id="c6c4d-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="c6c4d-204">Используйте одну из hello следующую SSH клиентов из вашего узла компьютера tooconnect tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
    - <span data-ttu-id="c6c4d-205">[PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="c6c4d-206">Требуется IP-адрес вашего tooconnect Pi hello его по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-206">You need hello IP address of your Pi tooconnect it via SSH.</span></span>
    - <span data-ttu-id="c6c4d-207">Hello встроенный клиент SSH на Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-207">hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="c6c4d-208">Возможно необходимо запустить `ssh pi@<ip address of pi>` tooconnect Pi по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-208">You might need run `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="c6c4d-209">имя пользователя по умолчанию Hello `pi` , и пароль hello `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-209">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="c6c4d-210">Установите Node.js и NPM tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-210">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="c6c4d-211">Сначала следует проверить вашу версию Node.js с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-211">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="c6c4d-212">Если версии hello меньше 4.x или нет не Node.js на ваш Pi, запустите следующие команды tooinstall hello, или обновить Node.js.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-212">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="c6c4d-213">Пример приложения hello клона, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c6c4d-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="c6c4d-214">Установите все пакеты, hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-214">Install all packages by hello following command.</span></span> <span data-ttu-id="c6c4d-215">в том числе пакет SDK для устройств Azure IoT, библиотеку датчика BME280 и библиотеку Wiring Pi, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c6c4d-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="c6c4d-216">Может занять несколько минут toofinish этот denpening процесс установки на подключение к сети.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-216">It might take several minutes toofinish this installation process denpening on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="c6c4d-217">Настройка образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="c6c4d-217">Configure hello sample application</span></span>

1. <span data-ttu-id="c6c4d-218">Откройте файл конфигурации hello, запустив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c6c4d-218">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Файл конфигурации](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="c6c4d-220">В этом файле можно настроить два элемента.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="c6c4d-221">Hello сначала он `interval`, который определяет hello временной интервал между двумя сообщений, передаваемых toocloud.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-221">hello first one is `interval`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="c6c4d-222">Здравствуйте, вторая — `simulatedData`, — логическое значение для ли toouse смоделированные данные датчиков или нет.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-222">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="c6c4d-223">Если вы **нет hello датчика**, задайте hello `simulatedData` значение слишком`true` пример приложения hello toomake создать и использовать имитацию датчиков.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-223">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="c6c4d-224">Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="c6c4d-225">Запустить образец приложения hello</span><span class="sxs-lookup"><span data-stu-id="c6c4d-225">Run hello sample application</span></span>

1. <span data-ttu-id="c6c4d-226">Выполните пример приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c6c4d-226">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="c6c4d-227">Убедитесь, что вы скопированные и вставленные строки подключения устройств hello в одинарных кавычках hello.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-227">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="c6c4d-228">Вы увидите следующее hello выходных данных, показано hello датчик данных и hello сообщений, отправляемых tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-228">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Вывод — данные датчика, отправленные из центра IoT tooyour Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="c6c4d-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6c4d-230">Next steps</span></span>

<span data-ttu-id="c6c4d-231">Вы впервые запускаете в образце данных датчика toocollect приложения и отправьте его центр IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="c6c4d-231">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]