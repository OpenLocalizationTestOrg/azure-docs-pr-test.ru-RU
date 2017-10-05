---
title: "Подключение Raspberry Pi (Python) к Центру Интернета вещей для передачи данных в облако | Документация Майкрософт"
description: "Узнайте, как подключить компьютер Raspberry Pi к Центру Интернета вещей Azure и передавать данные с этого компьютера в облако Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Raspberry Pi и Центр Интернета вещей Azure, Raspberry Pi и Центр Интернета вещей, отправка данных с Raspberry Pi в облако, подключение Raspberry Pi к облаку"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 1b1a9dc960846cbc15ce09d0fd106e1492937439
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-python"></a><span data-ttu-id="6b381-104">Подключение Raspberry Pi к Центру Интернета вещей (Python)</span><span class="sxs-lookup"><span data-stu-id="6b381-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="6b381-105">В этом учебнике описано, как начать работу с устройством Raspberry Pi под управлением Raspbian.</span><span class="sxs-lookup"><span data-stu-id="6b381-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="6b381-106">Также вы узнаете, как можно легко подключать устройства к облаку с помощью [Центра Интернета вещей Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="6b381-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="6b381-107">Примеры для Windows 10 IoT Базовая представлены в [Центре разработки для Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="6b381-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="6b381-108">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="6b381-108">Don't have a kit yet?</span></span> <span data-ttu-id="6b381-109">Используйте [онлайн-симулятор Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6b381-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="6b381-110">Или купите новый комплект [здесь](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="6b381-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6b381-111">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="6b381-111">What you do</span></span>

* <span data-ttu-id="6b381-112">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6b381-112">Create an IoT hub.</span></span>
* <span data-ttu-id="6b381-113">Зарегистрируем устройство для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6b381-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="6b381-114">Настроим Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6b381-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="6b381-115">Мы запустим пример приложения на Pi для отправки данных в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6b381-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="6b381-116">Подключим Raspberry Pi к созданному Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6b381-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="6b381-117">Затем запустим пример приложения на Pi, чтобы собрать данные о температуре и влажности, полученные с датчика BME280.</span><span class="sxs-lookup"><span data-stu-id="6b381-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="6b381-118">После этого отправим данные с датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6b381-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6b381-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="6b381-119">What you learn</span></span>

* <span data-ttu-id="6b381-120">Как создать Центр Интернета вещей Azure и получить строку подключения нового устройства.</span><span class="sxs-lookup"><span data-stu-id="6b381-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="6b381-121">Как подключать Pi к датчику BME280.</span><span class="sxs-lookup"><span data-stu-id="6b381-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="6b381-122">Как собирать данные датчика, запустив пример приложения на Pi.</span><span class="sxs-lookup"><span data-stu-id="6b381-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="6b381-123">Как отправить данные датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6b381-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6b381-124">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="6b381-124">What you need</span></span>

![Необходимые элементы](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="6b381-126">Плата Raspberry Pi 2 или Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="6b381-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="6b381-127">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="6b381-127">An active Azure subscription.</span></span> <span data-ttu-id="6b381-128">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6b381-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="6b381-129">Монитор, USB-клавиатура и мышь, подключенные к Pi.</span><span class="sxs-lookup"><span data-stu-id="6b381-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="6b381-130">ПК или компьютер Mac под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="6b381-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="6b381-131">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="6b381-131">An Internet connection.</span></span>
* <span data-ttu-id="6b381-132">Карта microSD емкостью 16 ГБ или больше.</span><span class="sxs-lookup"><span data-stu-id="6b381-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="6b381-133">Адаптер USB-SD или карта microSD для записи образа операционной системы на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="6b381-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="6b381-134">Источник питания 5 В 2 A с кабелем Micro USB длиной примерно 1,8 метра.</span><span class="sxs-lookup"><span data-stu-id="6b381-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="6b381-135">Ниже приведены необязательные компоненты.</span><span class="sxs-lookup"><span data-stu-id="6b381-135">The following items are optional:</span></span>

* <span data-ttu-id="6b381-136">Датчик температуры, давления и влажности Adafruit BME280 в сборе.</span><span class="sxs-lookup"><span data-stu-id="6b381-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="6b381-137">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="6b381-137">A breadboard.</span></span>
* <span data-ttu-id="6b381-138">6 оптоволоконных кабелей с разъемом на одном конце и гнездом на другом.</span><span class="sxs-lookup"><span data-stu-id="6b381-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="6b381-139">Светодиодный индикатор 10 мм с рассеянным освещением.</span><span class="sxs-lookup"><span data-stu-id="6b381-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="6b381-140">Эти компоненты необязательны, поскольку пример кода поддерживает использование смоделированных данных датчиков.</span><span class="sxs-lookup"><span data-stu-id="6b381-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="6b381-141">Настройка Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="6b381-141">Set up Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="6b381-142">Установка операционной системы Raspbian на Pi</span><span class="sxs-lookup"><span data-stu-id="6b381-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="6b381-143">Подготовьте карту microSD для установки образа ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="6b381-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="6b381-144">Скачайте ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="6b381-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="6b381-145">[Скачайте Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (ZIP-файл).</span><span class="sxs-lookup"><span data-stu-id="6b381-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="6b381-146">Извлеките образ ОС Raspbian в папку на компьютере.</span><span class="sxs-lookup"><span data-stu-id="6b381-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="6b381-147">Установите ОС Raspbian на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="6b381-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="6b381-148">[Скачайте и установите служебную программу Etcher для записи данных на карты SD](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="6b381-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="6b381-149">Запустите Etcher и выберите образ Raspbian, извлеченный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="6b381-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="6b381-150">Выберите устройство для чтения карт microSD.</span><span class="sxs-lookup"><span data-stu-id="6b381-150">Select the microSD card drive.</span></span> <span data-ttu-id="6b381-151">Обратите внимание, что в программе Etcher уже может быть выбрано правильное устройство для чтения.</span><span class="sxs-lookup"><span data-stu-id="6b381-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="6b381-152">Щелкните Flash (Переключиться), чтобы установить ОС Raspbian на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="6b381-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="6b381-153">По завершении установки удалите карту microSD из компьютера.</span><span class="sxs-lookup"><span data-stu-id="6b381-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="6b381-154">Удалять карту microSD напрямую безопасно, так как программа Etcher автоматически извлекает или отключает карту microSD после завершения.</span><span class="sxs-lookup"><span data-stu-id="6b381-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="6b381-155">Вставьте карту microSD в устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="6b381-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="6b381-156">Включение SSH и I2C</span><span class="sxs-lookup"><span data-stu-id="6b381-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="6b381-157">Подключите Pi к монитору, клавиатуре и мыши, запустите Pi, а затем войдите в Raspbian, используя `pi` в качестве имени пользователя и `raspberry` в качестве пароля.</span><span class="sxs-lookup"><span data-stu-id="6b381-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="6b381-158">Щелкните значок Raspberry и выберите **Preferences** (Параметры) > **Raspberry Pi Configuration** (Конфигурация Raspberry Pi).</span><span class="sxs-lookup"><span data-stu-id="6b381-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Меню параметров Raspbian](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="6b381-160">На вкладке **Interfaces** (Интерфейсы) установите для параметров **I2C** и **SSH** значение **Enable** (Включить), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6b381-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="6b381-161">Этот шаг является необязательным, если у вас нет физических датчиков и вы будете использовать симулированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="6b381-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Включение I2C и SSH на Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="6b381-163">Сведения о том, как включить SSH и I2C, можно найти в дополнительных справочных документах на сайтах [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) и [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="6b381-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="6b381-164">Подключение датчика к Pi</span><span class="sxs-lookup"><span data-stu-id="6b381-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="6b381-165">Подключите светодиодный индикатор и датчик BME280 к Pi с помощью монтажной платы и оптоволоконных кабелей, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6b381-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="6b381-166">Если у вас нет датчика, [пропустите этот раздел](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="6b381-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Подключение Raspberry Pi и датчика](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="6b381-168">Датчик BME280 может собирать данные о температуре и влажности.</span><span class="sxs-lookup"><span data-stu-id="6b381-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="6b381-169">Светодиодный индикатор мигает при обмене данными между устройством и облаком.</span><span class="sxs-lookup"><span data-stu-id="6b381-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="6b381-170">Чтобы подключить выводы датчика, используйте следующие кабели:</span><span class="sxs-lookup"><span data-stu-id="6b381-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="6b381-171">Начало (датчик и светодиодный индикатор)</span><span class="sxs-lookup"><span data-stu-id="6b381-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="6b381-172">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="6b381-172">End (Board)</span></span>            | <span data-ttu-id="6b381-173">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="6b381-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="6b381-174">VDD (вывод 5G)</span><span class="sxs-lookup"><span data-stu-id="6b381-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="6b381-175">3.3V PWR (вывод 1)</span><span class="sxs-lookup"><span data-stu-id="6b381-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="6b381-176">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="6b381-176">White cable</span></span>   |
| <span data-ttu-id="6b381-177">GND (вывод 7G)</span><span class="sxs-lookup"><span data-stu-id="6b381-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="6b381-178">GND (вывод 6)</span><span class="sxs-lookup"><span data-stu-id="6b381-178">GND (Pin 6)</span></span>            | <span data-ttu-id="6b381-179">Коричневый кабель</span><span class="sxs-lookup"><span data-stu-id="6b381-179">Brown cable</span></span>   |
| <span data-ttu-id="6b381-180">SDI (вывод 10G)</span><span class="sxs-lookup"><span data-stu-id="6b381-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="6b381-181">I2C1 SDA (вывод 3)</span><span class="sxs-lookup"><span data-stu-id="6b381-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="6b381-182">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="6b381-182">Red cable</span></span>     |
| <span data-ttu-id="6b381-183">SCK (вывод 8G)</span><span class="sxs-lookup"><span data-stu-id="6b381-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="6b381-184">I2C1 SCL (вывод 5)</span><span class="sxs-lookup"><span data-stu-id="6b381-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="6b381-185">Оранжевый кабель</span><span class="sxs-lookup"><span data-stu-id="6b381-185">Orange cable</span></span>  |
| <span data-ttu-id="6b381-186">LED VDD (вывод 18F)</span><span class="sxs-lookup"><span data-stu-id="6b381-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="6b381-187">GPIO 24 (вывод 18)</span><span class="sxs-lookup"><span data-stu-id="6b381-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="6b381-188">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="6b381-188">White cable</span></span>   |
| <span data-ttu-id="6b381-189">LED GND (вывод 17F)</span><span class="sxs-lookup"><span data-stu-id="6b381-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="6b381-190">GND (вывод 20)</span><span class="sxs-lookup"><span data-stu-id="6b381-190">GND (Pin 20)</span></span>           | <span data-ttu-id="6b381-191">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="6b381-191">Black cable</span></span>   |

<span data-ttu-id="6b381-192">Щелкните, чтобы просмотреть [схему соответствия выводов Raspberry Pi 2 и 3](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) для справки.</span><span class="sxs-lookup"><span data-stu-id="6b381-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="6b381-193">После успешного подключения датчика BME280 к Raspberry Pi схема должна выглядеть так, как на изображении ниже.</span><span class="sxs-lookup"><span data-stu-id="6b381-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Подключенный компьютер Pi и датчик BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="6b381-195">Подключение устройства Pi к сети</span><span class="sxs-lookup"><span data-stu-id="6b381-195">Connect Pi to the network</span></span>

<span data-ttu-id="6b381-196">Включите устройство Pi, используя кабель Micro USB и источник питания.</span><span class="sxs-lookup"><span data-stu-id="6b381-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="6b381-197">Подключите Pi к проводной сети с помощью кабеля Ethernet или выполните [инструкции](https://www.raspberrypi.org/learning/software-guide/wifi/) от Raspberry Pi Foundation для подключения устройства Pi к беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="6b381-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="6b381-198">После успешного подключения Pi к сети необходимо запомнить [IP-адрес устройства Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="6b381-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Подключение к проводной сети](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="6b381-200">Убедитесь, что плата Pi подключена к той же сети, что и компьютер.</span><span class="sxs-lookup"><span data-stu-id="6b381-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="6b381-201">Например, если компьютер подключен к беспроводной сети, а плата Pi подключена к проводной сети, то IP-адрес может не отобразиться в выходных данных devdisco.</span><span class="sxs-lookup"><span data-stu-id="6b381-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="6b381-202">Запуск примера приложения на Pi</span><span class="sxs-lookup"><span data-stu-id="6b381-202">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="6b381-203">Установка пакетов необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="6b381-203">Install the prerequisite packages</span></span>

<span data-ttu-id="6b381-204">Используйте один из следующих SSH-клиентов для подключения к Raspberry Pi с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="6b381-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="6b381-205">**Пользователи Windows**</span><span class="sxs-lookup"><span data-stu-id="6b381-205">**Windows Users**</span></span>
   1. <span data-ttu-id="6b381-206">Скачайте и установите [PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="6b381-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="6b381-207">Скопируйте IP-адрес устройства Pi и вставьте его в поле для имени узла (или для IP-адреса), а затем выберите тип подключения SSH.</span><span class="sxs-lookup"><span data-stu-id="6b381-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   
   <span data-ttu-id="6b381-208">**Пользователи MAC и Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="6b381-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="6b381-209">Используйте SSH-клиент, встроенный в Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="6b381-209">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="6b381-210">Возможно, для подключения устройства Pi по протоколу SSH потребуется выполнить `ssh pi@<ip address of pi>`.</span><span class="sxs-lookup"><span data-stu-id="6b381-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="6b381-211">Имя пользователя по умолчанию — `pi`, а пароль — `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="6b381-211">The default username is `pi` , and the password is `raspberry`.</span></span>


### <a name="configure-the-sample-application"></a><span data-ttu-id="6b381-212">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="6b381-212">Configure the sample application</span></span>

1. <span data-ttu-id="6b381-213">Создайте клон примера приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6b381-213">Clone the sample application by running the following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="6b381-214">Откройте файл конфигурации, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6b381-214">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="6b381-215">В этом файле можно настроить 5 макросов.</span><span class="sxs-lookup"><span data-stu-id="6b381-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="6b381-216">Первый из них — `MESSAGE_TIMESPAN`, который задает время (в миллисекундах) между отправкой двух сообщений в облако.</span><span class="sxs-lookup"><span data-stu-id="6b381-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="6b381-217">Второй, `SIMULATED_DATA`, представляет собой логическое значение, которое определяет, будут ли использоваться смоделированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="6b381-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span></span> <span data-ttu-id="6b381-218">`I2C_ADDRESS` — I2C-адрес, к которому подключен датчик BME280.</span><span class="sxs-lookup"><span data-stu-id="6b381-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="6b381-219">`GPIO_PIN_ADDRESS` — адрес объекта групповой политики для индикатора.</span><span class="sxs-lookup"><span data-stu-id="6b381-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span></span> <span data-ttu-id="6b381-220">И наконец, `BLINK_TIMESPAN` задает длительность включения индикатора в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="6b381-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="6b381-221">Если у вас **нет датчика**, задайте для параметра `SIMULATED_DATA` значение `True`, чтобы пример приложения создал и использовал смоделированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="6b381-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="6b381-222">Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.</span><span class="sxs-lookup"><span data-stu-id="6b381-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="6b381-223">Создание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="6b381-223">Build and run the sample application</span></span>

1. <span data-ttu-id="6b381-224">Создайте пример приложения, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6b381-224">Build the sample application by running the following command.</span></span> <span data-ttu-id="6b381-225">Пакеты SDK для Azure IoT для Python являются оболочкой аналогичных пакетов для языка C. Поэтому, если вам нужно собрать библиотеки Python из исходного кода, вам потребуется скомпилировать библиотеки C.</span><span class="sxs-lookup"><span data-stu-id="6b381-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="6b381-226">Вы можете указать требуемую версию, выполнив скрипт `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="6b381-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="6b381-227">Если запустить этот скрипт без параметра, он автоматически обнаружит установленную версию Python (методом перебора в следующей последовательности: 2.7 -> 3.4 -> 3.5).</span><span class="sxs-lookup"><span data-stu-id="6b381-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="6b381-228">Следите за тем, чтобы версии Python во время сборки и выполнения совпадали.</span><span class="sxs-lookup"><span data-stu-id="6b381-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="6b381-229">Процесс сборки клиентской библиотеки Python (iothub_client.so) на устройствах Linux, которые имеют менее 1 ГБ оперативной памяти, может "зависнуть" на уровне 98 % при сборке файла iothub_client_python.cpp, как показано ниже: `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="6b381-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="6b381-230">Если вы встретите такую проблему, проверьте потребление памяти на устройстве, выполнив в другом окне терминала команду `free -m command`.</span><span class="sxs-lookup"><span data-stu-id="6b381-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="6b381-231">Если памяти для сборки файла iothub_client_python.cpp недостаточно, вы можете попробовать временно увеличить область буфера. Это увеличит объем доступной памяти и повысит шансы успешной сборки библиотеки пакета SDK для Python на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="6b381-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="6b381-232">Запустите пример приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6b381-232">Run the sample application by running the following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="6b381-233">Обязательно скопируйте и вставьте строку подключения устройства, заключив ее в одинарные кавычки.</span><span class="sxs-lookup"><span data-stu-id="6b381-233">Make sure you copy-paste the device connection string into the single quotes.</span></span> <span data-ttu-id="6b381-234">Если вы используете Python 3, можете выполнить команду `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="6b381-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="6b381-235">Должны отобразиться следующие результаты, содержащие данные датчика и сообщения, которые отправляются в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6b381-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![Выходные данные — данные датчика, отправленные с Raspberry Pi в Центр Интернета вещей](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="6b381-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b381-237">Next steps</span></span>

<span data-ttu-id="6b381-238">Вы запустили пример приложения, чтобы собрать данные датчика и отправить их в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6b381-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="6b381-239">Сведения о том, как просматривать сообщения, отправляемые устройством Raspberry Pi в Центр Интернета вещей, а также как отправлять сообщения на устройство Raspberry Pi в интерфейсе командной строки, см. в руководстве по [управлению обменом сообщениями между облаком и устройством с помощью обозревателя Центра Интернета вещей](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="6b381-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
