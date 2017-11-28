---
title: "toocloud aaaRaspberry Pi (Python) - подключения Pi Raspberry tooAzure центр IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключите Raspberry Pi tooAzure центр IoT для Raspberry Pi toosend данные toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot малиновая pi малиновая pi iot hub, малиновая pi отправки данных toocloud, малиновая pi toocloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a><span data-ttu-id="f9818-104">Подключение tooAzure Raspberry Pi центр IoT (Python)</span><span class="sxs-lookup"><span data-stu-id="f9818-104">Connect Raspberry Pi tooAzure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="f9818-105">В этом учебнике сначала hello основы работы с Raspberry Pi, на котором выполняется Raspbian обучения.</span><span class="sxs-lookup"><span data-stu-id="f9818-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="f9818-106">Затем вы узнаете, как tooseamlessly подключаться toohello облачных устройств с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f9818-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="f9818-107">Примеры Windows 10 IoT базовая go toohello [центра разработчиков Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="f9818-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="f9818-108">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="f9818-108">Don't have a kit yet?</span></span> <span data-ttu-id="f9818-109">Используйте [онлайн-симулятор Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f9818-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="f9818-110">Или купите новый комплект [здесь](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="f9818-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="f9818-111">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="f9818-111">What you do</span></span>

* <span data-ttu-id="f9818-112">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f9818-112">Create an IoT hub.</span></span>
* <span data-ttu-id="f9818-113">Зарегистрируем устройство для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f9818-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="f9818-114">Настроим Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f9818-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="f9818-115">Запустите образец приложения на Pi toosend датчиков данных tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f9818-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="f9818-116">Подключение центра IoT tooan Raspberry Pi созданного вами.</span><span class="sxs-lookup"><span data-stu-id="f9818-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="f9818-117">Затем запустите пример приложения на Pi toocollect температуры и влажности данных с использованием BME280 датчиков.</span><span class="sxs-lookup"><span data-stu-id="f9818-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="f9818-118">Отправьте центра IoT tooyour данных датчика hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="f9818-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="f9818-119">What you learn</span></span>

* <span data-ttu-id="f9818-120">Как toocreate центр Azure IoT и получить новые строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="f9818-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="f9818-121">Как tooconnect числа пи с BME280 датчика.</span><span class="sxs-lookup"><span data-stu-id="f9818-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="f9818-122">Как toocollect датчиков, выполнив пример приложения на Pi.</span><span class="sxs-lookup"><span data-stu-id="f9818-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="f9818-123">Как центр IoT tooyour данных датчика toosend.</span><span class="sxs-lookup"><span data-stu-id="f9818-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f9818-124">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="f9818-124">What you need</span></span>

![Необходимые элементы](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="f9818-126">Здравствуйте, Raspberry Pi 2 или Raspberry Pi 3 на доске.</span><span class="sxs-lookup"><span data-stu-id="f9818-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="f9818-127">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f9818-127">An active Azure subscription.</span></span> <span data-ttu-id="f9818-128">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f9818-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f9818-129">Монитор, USB-клавиатуры и мыши подключаются tooPi.</span><span class="sxs-lookup"><span data-stu-id="f9818-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="f9818-130">ПК или компьютер Mac под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="f9818-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="f9818-131">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="f9818-131">An Internet connection.</span></span>
* <span data-ttu-id="f9818-132">Карта microSD емкостью 16 ГБ или больше.</span><span class="sxs-lookup"><span data-stu-id="f9818-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="f9818-133">USB-SD адаптер или microSD карты tooburn hello образа операционной системы на карту microSD, hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="f9818-134">Питания 2 amp 5В с hello 6 фут micro USB-кабель.</span><span class="sxs-lookup"><span data-stu-id="f9818-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="f9818-135">Привет, следующие элементы являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="f9818-135">hello following items are optional:</span></span>

* <span data-ttu-id="f9818-136">Датчик температуры, давления и влажности Adafruit BME280 в сборе.</span><span class="sxs-lookup"><span data-stu-id="f9818-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="f9818-137">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="f9818-137">A breadboard.</span></span>
* <span data-ttu-id="f9818-138">6 оптоволоконных кабелей с разъемом на одном конце и гнездом на другом.</span><span class="sxs-lookup"><span data-stu-id="f9818-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="f9818-139">Светодиодный индикатор 10 мм с рассеянным освещением.</span><span class="sxs-lookup"><span data-stu-id="f9818-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="f9818-140">Эти элементы являются необязательными, поскольку поддержка образец кода hello смоделированные данные датчиков.</span><span class="sxs-lookup"><span data-stu-id="f9818-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="f9818-141">Настройка Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="f9818-141">Set up Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="f9818-142">Установка операционной системы Raspbian hello для Pi</span><span class="sxs-lookup"><span data-stu-id="f9818-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="f9818-143">Подготовьте карта microSD hello для установки образа Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="f9818-144">Скачайте ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="f9818-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="f9818-145">[Загрузите детском Raspbian с рабочим столом](https://www.raspberrypi.org/downloads/raspbian/) (hello ZIP-файл).</span><span class="sxs-lookup"><span data-stu-id="f9818-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="f9818-146">Извлеките hello Raspbian изображения tooa папку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f9818-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="f9818-147">Установите карту microSD toohello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="f9818-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="f9818-148">[Загрузите и установите программу записи карты SD гравировальная hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="f9818-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="f9818-149">Запустите гравировальная и выберите изображение Raspbian hello, извлеченный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="f9818-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="f9818-150">Выберите диск, карту microSD hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-150">Select hello microSD card drive.</span></span> <span data-ttu-id="f9818-151">Обратите внимание, что гравировальная может уже выбран правильный диск hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="f9818-152">Щелкните карту microSD toohello Raspbian tooinstall флэш-памяти.</span><span class="sxs-lookup"><span data-stu-id="f9818-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="f9818-153">Удаление карта microSD hello с компьютера после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="f9818-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="f9818-154">Это карта microSD безопасные tooremove hello непосредственно из-за гравировальная автоматически извлечение или отключение карта microSD hello после завершения.</span><span class="sxs-lookup"><span data-stu-id="f9818-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="f9818-155">Вставьте карту microSD hello в Pi.</span><span class="sxs-lookup"><span data-stu-id="f9818-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="f9818-156">Включение SSH и I2C</span><span class="sxs-lookup"><span data-stu-id="f9818-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="f9818-157">Подключение Pi toohello монитора, клавиатуры и мыши, запустите Pi и затем войдите Raspbian с помощью `pi` имени пользователя hello и `raspberry` hello паролем.</span><span class="sxs-lookup"><span data-stu-id="f9818-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="f9818-158">Щелкните значок малиновая hello > **предпочтения** > **Raspberry Pi конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="f9818-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![меню настройки Raspbian Hello](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="f9818-160">На hello **интерфейсы** установите **I2C** и **SSH** слишком**включить**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f9818-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="f9818-161">Если нет физических датчиков и toouse смоделированные данные датчика, этот шаг является необязательным.</span><span class="sxs-lookup"><span data-stu-id="f9818-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Включение I2C и SSH на Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="f9818-163">tooenable SSH и I2C, можно найти дополнительные справочные документы на [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) и [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="f9818-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="f9818-164">Подключение tooPi датчик hello</span><span class="sxs-lookup"><span data-stu-id="f9818-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="f9818-165">Используйте hello breadboard и перемычки проводов tooconnect Светодиодный индикатор и BME280 tooPi.</span><span class="sxs-lookup"><span data-stu-id="f9818-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="f9818-166">Если у вас нет датчик hello [пропустите этот раздел](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="f9818-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hello Raspberry Pi и датчик подключения](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="f9818-168">Датчик Hello BME280 можно собирать данные, температуры и влажности.</span><span class="sxs-lookup"><span data-stu-id="f9818-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="f9818-169">И hello Индикатор мигает, при наличии связи между локальными устройствами и hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="f9818-170">Для датчика ПИН-коды используйте hello после подключения:</span><span class="sxs-lookup"><span data-stu-id="f9818-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="f9818-171">Начало (датчик и светодиодный индикатор)</span><span class="sxs-lookup"><span data-stu-id="f9818-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="f9818-172">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="f9818-172">End (Board)</span></span>            | <span data-ttu-id="f9818-173">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="f9818-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="f9818-174">VDD (вывод 5G)</span><span class="sxs-lookup"><span data-stu-id="f9818-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="f9818-175">3.3V PWR (вывод 1)</span><span class="sxs-lookup"><span data-stu-id="f9818-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="f9818-176">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="f9818-176">White cable</span></span>   |
| <span data-ttu-id="f9818-177">GND (вывод 7G)</span><span class="sxs-lookup"><span data-stu-id="f9818-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="f9818-178">GND (вывод 6)</span><span class="sxs-lookup"><span data-stu-id="f9818-178">GND (Pin 6)</span></span>            | <span data-ttu-id="f9818-179">Коричневый кабель</span><span class="sxs-lookup"><span data-stu-id="f9818-179">Brown cable</span></span>   |
| <span data-ttu-id="f9818-180">SDI (вывод 10G)</span><span class="sxs-lookup"><span data-stu-id="f9818-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="f9818-181">I2C1 SDA (вывод 3)</span><span class="sxs-lookup"><span data-stu-id="f9818-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="f9818-182">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="f9818-182">Red cable</span></span>     |
| <span data-ttu-id="f9818-183">SCK (вывод 8G)</span><span class="sxs-lookup"><span data-stu-id="f9818-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="f9818-184">I2C1 SCL (вывод 5)</span><span class="sxs-lookup"><span data-stu-id="f9818-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="f9818-185">Оранжевый кабель</span><span class="sxs-lookup"><span data-stu-id="f9818-185">Orange cable</span></span>  |
| <span data-ttu-id="f9818-186">LED VDD (вывод 18F)</span><span class="sxs-lookup"><span data-stu-id="f9818-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="f9818-187">GPIO 24 (вывод 18)</span><span class="sxs-lookup"><span data-stu-id="f9818-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="f9818-188">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="f9818-188">White cable</span></span>   |
| <span data-ttu-id="f9818-189">LED GND (вывод 17F)</span><span class="sxs-lookup"><span data-stu-id="f9818-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="f9818-190">GND (вывод 20)</span><span class="sxs-lookup"><span data-stu-id="f9818-190">GND (Pin 20)</span></span>           | <span data-ttu-id="f9818-191">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="f9818-191">Black cable</span></span>   |

<span data-ttu-id="f9818-192">Нажмите кнопку tooview [Raspberry Pi 2 и 3 ПИН-код сопоставления](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) для справки.</span><span class="sxs-lookup"><span data-stu-id="f9818-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="f9818-193">После успешного соединения BME280 tooyour Raspberry Pi должно быть как под изображением.</span><span class="sxs-lookup"><span data-stu-id="f9818-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Подключенный компьютер Pi и датчик BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="f9818-195">Подключение к сети toohello Pi</span><span class="sxs-lookup"><span data-stu-id="f9818-195">Connect Pi toohello network</span></span>

<span data-ttu-id="f9818-196">Включите Pi при помощи micro USB-кабель hello и hello питания.</span><span class="sxs-lookup"><span data-stu-id="f9818-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="f9818-197">Используйте hello Ethernet кабель tooconnect Pi tooyour проводной сети, или выполните hello [инструкции hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="f9818-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="f9818-198">После вашей Pi было успешно выполнено подключение toohello сети, необходимо tootake заметку hello [IP-адрес вашего Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="f9818-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Toowired подключенной сети](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="f9818-200">Убедитесь, что Pi подключенных toohello сетевых как на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f9818-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="f9818-201">Например, если компьютер находится подключенных tooa беспроводной сети при подключенном tooa проводной сети Pi, могут отображаться не hello IP адрес в выходных данных devdisco hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="f9818-202">Запуск примера приложения на Pi</span><span class="sxs-lookup"><span data-stu-id="f9818-202">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="f9818-203">Установите пакеты необходимых компонентов hello</span><span class="sxs-lookup"><span data-stu-id="f9818-203">Install hello prerequisite packages</span></span>

<span data-ttu-id="f9818-204">Используйте одну из hello следующую SSH клиентов из вашего узла компьютера tooconnect tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="f9818-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="f9818-205">**Пользователи Windows**</span><span class="sxs-lookup"><span data-stu-id="f9818-205">**Windows Users**</span></span>
   1. <span data-ttu-id="f9818-206">Скачайте и установите [PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="f9818-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="f9818-207">Скопируйте hello IP-адрес раздела Pi в hello узел имя (или IP-адрес) и выберите в качестве типа соединения hello SSH.</span><span class="sxs-lookup"><span data-stu-id="f9818-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   
   <span data-ttu-id="f9818-208">**Пользователи MAC и Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="f9818-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="f9818-209">Используйте встроенный клиент SSH hello Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="f9818-209">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="f9818-210">Может потребоваться toorun `ssh pi@<ip address of pi>` tooconnect Pi по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="f9818-210">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="f9818-211">имя пользователя по умолчанию Hello `pi` , и пароль hello `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="f9818-211">hello default username is `pi` , and hello password is `raspberry`.</span></span>


### <a name="configure-hello-sample-application"></a><span data-ttu-id="f9818-212">Настройка образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="f9818-212">Configure hello sample application</span></span>

1. <span data-ttu-id="f9818-213">Пример приложения hello клона, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="f9818-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="f9818-214">Откройте файл конфигурации hello, запустив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="f9818-214">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="f9818-215">В этом файле можно настроить 5 макросов.</span><span class="sxs-lookup"><span data-stu-id="f9818-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="f9818-216">Hello сначала он `MESSAGE_TIMESPAN`, который определяет hello временной интервал (в миллисекундах) между двумя сообщений, передаваемых toocloud.</span><span class="sxs-lookup"><span data-stu-id="f9818-216">hello first one is `MESSAGE_TIMESPAN`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="f9818-217">Здравствуйте, вторая — `SIMULATED_DATA`, — логическое значение для ли toouse смоделированные данные датчиков или нет.</span><span class="sxs-lookup"><span data-stu-id="f9818-217">hello second one `SIMULATED_DATA`, which is a Boolean value for whether toouse simulated sensor data or not.</span></span> <span data-ttu-id="f9818-218">`I2C_ADDRESS`— адрес hello I2C, подключенный к BME280 датчика.</span><span class="sxs-lookup"><span data-stu-id="f9818-218">`I2C_ADDRESS` is hello I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="f9818-219">`GPIO_PIN_ADDRESS`— адрес hello объект групповой ПОЛИТИКИ для вашей Индикатора.</span><span class="sxs-lookup"><span data-stu-id="f9818-219">`GPIO_PIN_ADDRESS` is hello GPIO address for your LED.</span></span> <span data-ttu-id="f9818-220">Hello последнего он `BLINK_TIMESPAN`, при включении вашей Индикатора в миллисекундах, который определяется hello timespan.</span><span class="sxs-lookup"><span data-stu-id="f9818-220">hello last one is `BLINK_TIMESPAN`, which defined hello timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="f9818-221">Если вы **нет hello датчика**, задайте hello `SIMULATED_DATA` значение слишком`True` пример приложения hello toomake создать и использовать имитацию датчиков.</span><span class="sxs-lookup"><span data-stu-id="f9818-221">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`True` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="f9818-222">Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.</span><span class="sxs-lookup"><span data-stu-id="f9818-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="f9818-223">Построение и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="f9818-223">Build and run hello sample application</span></span>

1. <span data-ttu-id="f9818-224">Построение образца приложения hello, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-224">Build hello sample application by running hello following command.</span></span> <span data-ttu-id="f9818-225">Поскольку hello Azure IoT пакетов SDK для Python являются оболочками поверх hello Azure IoT устройства C SDK, необходимо будет toocompile hello C библиотеки, если вы желаете или вам библиотеки Python hello toogenerate из исходного кода.</span><span class="sxs-lookup"><span data-stu-id="f9818-225">Because hello Azure IoT SDKs for Python are wrappers on top of hello Azure IoT Device C SDK, you will need toocompile hello C libraries if you want or need toogenerate hello Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="f9818-226">Можно также указать hello версию, выполнив `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="f9818-226">You can also specify hello version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="f9818-227">Если запустить скрипт без параметра hello скрипт автоматически обнаруживает hello версии python установлен (последовательность поиска 2.7 -> 3.4 -> 3.5).</span><span class="sxs-lookup"><span data-stu-id="f9818-227">If you run script without parameter, hello script will automatically detect hello version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="f9818-228">Следите за тем, чтобы версии Python во время сборки и выполнения совпадали.</span><span class="sxs-lookup"><span data-stu-id="f9818-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="f9818-229">О построении библиотека клиентов Python hello (iothub_client.so) на устройствах Linux, которые имеют менее 1 ГБ оперативной памяти, может появиться построения задерживаются на 98% при построении iothub_client_python.cpp, как показано ниже `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="f9818-229">On building hello Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="f9818-230">При возникновении этой проблемы, проверьте потребление памяти hello hello устройства с помощью `free -m command` в другом окне терминалов в течение этого времени.</span><span class="sxs-lookup"><span data-stu-id="f9818-230">If you run into this issue, check hello memory consumption of hello device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="f9818-231">При запуске не хватает памяти при компиляции файла iothub_client_python.cpp, возможно, tootemporarily увеличить tooget пространства подкачки hello более доступной памяти toosuccessfully сборки библиотеки пакета SDK для hello Python на стороне клиента устройства.</span><span class="sxs-lookup"><span data-stu-id="f9818-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have tootemporarily increase hello swap space tooget more available memory toosuccessfully build hello Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="f9818-232">Выполните пример приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="f9818-232">Run hello sample application by running hello following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="f9818-233">Убедитесь, что вы скопированные и вставленные строки подключения устройств hello в одинарных кавычках hello.</span><span class="sxs-lookup"><span data-stu-id="f9818-233">Make sure you copy-paste hello device connection string into hello single quotes.</span></span> <span data-ttu-id="f9818-234">Команда Здравствуйте и если используется hello python 3, то можно использовать `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="f9818-234">And if you use hello python 3, then you can use hello command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="f9818-235">Вы увидите следующее hello выходных данных, показано hello датчик данных и hello сообщений, отправляемых tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f9818-235">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

   ![Вывод — данные датчика, отправленные из центра IoT tooyour Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="f9818-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9818-237">Next steps</span></span>

<span data-ttu-id="f9818-238">Вы впервые запускаете в образце данных датчика toocollect приложения и отправьте его центр IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="f9818-238">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="f9818-239">сообщения приветствия toosee, Pi вашей Raspberry отправленных IoT tooyour концентратор или отправки tooyour сообщений Raspberry Pi в интерфейс командной строки, в разделе hello [управление облака устройство обмен сообщениями с центром IOT учебнике](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="f9818-239">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
