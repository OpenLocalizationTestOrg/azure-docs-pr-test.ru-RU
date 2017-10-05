---
title: "Подключение Raspberry Pi (Node.js) к Центру Интернета вещей для передачи данных в облако | Документация Майкрософт"
description: "Подключение компьютера Raspberry Pi к Центру Интернета вещей Azure для передачи данных с него в облако Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Raspberry Pi и Центр Интернета вещей Azure, Raspberry Pi и Центр Интернета вещей, отправка данных с Raspberry Pi в облако, подключение Raspberry Pi к облаку"
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
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="7e177-104">Подключение Raspberry Pi к Центру Интернета вещей Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="7e177-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="7e177-105">В этом учебнике описано, как начать работу с устройством Raspberry Pi под управлением Raspbian.</span><span class="sxs-lookup"><span data-stu-id="7e177-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="7e177-106">Также вы узнаете, как можно легко подключать устройства к облаку с помощью [Центра Интернета вещей Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="7e177-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="7e177-107">Примеры для Windows 10 IoT Базовая представлены в [Центре разработки для Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="7e177-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="7e177-108">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="7e177-108">Don't have a kit yet?</span></span> <span data-ttu-id="7e177-109">Воспользуйтесь [эмулятором Raspberry Pi 3](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="7e177-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="7e177-110">Или купите новый комплект [здесь](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="7e177-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="7e177-111">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="7e177-111">What you do</span></span>

* <span data-ttu-id="7e177-112">Настроим Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7e177-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="7e177-113">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e177-113">Create an IoT hub.</span></span>
* <span data-ttu-id="7e177-114">Зарегистрируем устройство для Pi в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e177-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="7e177-115">Мы запустим пример приложения на Pi для отправки данных в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e177-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="7e177-116">Подключим Raspberry Pi к созданному Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e177-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="7e177-117">Затем запустим пример приложения на Pi, чтобы собрать данные о температуре и влажности, полученные с датчика BME280.</span><span class="sxs-lookup"><span data-stu-id="7e177-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="7e177-118">После этого отправим данные с датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e177-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="7e177-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="7e177-119">What you learn</span></span>

* <span data-ttu-id="7e177-120">Как создать Центр Интернета вещей Azure и получить строку подключения нового устройства.</span><span class="sxs-lookup"><span data-stu-id="7e177-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="7e177-121">Как подключать Pi к датчику BME280.</span><span class="sxs-lookup"><span data-stu-id="7e177-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="7e177-122">Как собирать данные датчика, запустив пример приложения на Pi.</span><span class="sxs-lookup"><span data-stu-id="7e177-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="7e177-123">Как отправить данные датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e177-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7e177-124">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="7e177-124">What you need</span></span>

![Необходимые элементы](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="7e177-126">Плата Raspberry Pi 2 или Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="7e177-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="7e177-127">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="7e177-127">An active Azure subscription.</span></span> <span data-ttu-id="7e177-128">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7e177-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="7e177-129">Монитор, USB-клавиатура и мышь, подключенные к Pi.</span><span class="sxs-lookup"><span data-stu-id="7e177-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="7e177-130">ПК или компьютер Mac под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="7e177-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="7e177-131">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="7e177-131">An Internet connection.</span></span>
* <span data-ttu-id="7e177-132">Карта microSD емкостью 16 ГБ или больше.</span><span class="sxs-lookup"><span data-stu-id="7e177-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="7e177-133">Адаптер USB-SD или карта microSD для записи образа операционной системы на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="7e177-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="7e177-134">Источник питания 5 В 2 A с кабелем Micro USB длиной примерно 1,8 метра.</span><span class="sxs-lookup"><span data-stu-id="7e177-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="7e177-135">Ниже приведены необязательные компоненты.</span><span class="sxs-lookup"><span data-stu-id="7e177-135">The following items are optional:</span></span>

* <span data-ttu-id="7e177-136">Датчик температуры, давления и влажности Adafruit BME280 в сборе.</span><span class="sxs-lookup"><span data-stu-id="7e177-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="7e177-137">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="7e177-137">A breadboard.</span></span>
* <span data-ttu-id="7e177-138">6 оптоволоконных кабелей с разъемом на одном конце и гнездом на другом.</span><span class="sxs-lookup"><span data-stu-id="7e177-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="7e177-139">Светодиодный индикатор 10 мм с рассеянным освещением.</span><span class="sxs-lookup"><span data-stu-id="7e177-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="7e177-140">Эти компоненты необязательны, поскольку пример кода поддерживает использование смоделированных данных датчиков.</span><span class="sxs-lookup"><span data-stu-id="7e177-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="7e177-141">Настройка Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="7e177-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="7e177-142">Установка операционной системы Raspbian на Pi</span><span class="sxs-lookup"><span data-stu-id="7e177-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="7e177-143">Подготовьте карту microSD для установки образа ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="7e177-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="7e177-144">Скачайте ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="7e177-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="7e177-145">[Скачайте Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (ZIP-файл).</span><span class="sxs-lookup"><span data-stu-id="7e177-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="7e177-146">Извлеките образ ОС Raspbian в папку на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7e177-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="7e177-147">Установите ОС Raspbian на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="7e177-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="7e177-148">[Скачайте и установите служебную программу Etcher для записи данных на карты SD](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="7e177-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="7e177-149">Запустите Etcher и выберите образ Raspbian, извлеченный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="7e177-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="7e177-150">Выберите устройство для чтения карт microSD.</span><span class="sxs-lookup"><span data-stu-id="7e177-150">Select the microSD card drive.</span></span> <span data-ttu-id="7e177-151">Обратите внимание, что в программе Etcher уже может быть выбрано правильное устройство для чтения.</span><span class="sxs-lookup"><span data-stu-id="7e177-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="7e177-152">Щелкните Flash (Переключиться), чтобы установить ОС Raspbian на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="7e177-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="7e177-153">По завершении установки удалите карту microSD из компьютера.</span><span class="sxs-lookup"><span data-stu-id="7e177-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="7e177-154">Удалять карту microSD напрямую безопасно, так как программа Etcher автоматически извлекает или отключает карту microSD после завершения.</span><span class="sxs-lookup"><span data-stu-id="7e177-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="7e177-155">Вставьте карту microSD в устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="7e177-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="7e177-156">Включение SSH и I2C</span><span class="sxs-lookup"><span data-stu-id="7e177-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="7e177-157">Подключите Pi к монитору, клавиатуре и мыши, запустите Pi, а затем войдите в Raspbian, используя `pi` в качестве имени пользователя и `raspberry` в качестве пароля.</span><span class="sxs-lookup"><span data-stu-id="7e177-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="7e177-158">Щелкните значок Raspberry и выберите **Preferences** (Параметры) > **Raspberry Pi Configuration** (Конфигурация Raspberry Pi).</span><span class="sxs-lookup"><span data-stu-id="7e177-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Меню параметров Raspbian](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="7e177-160">На вкладке **Interfaces** (Интерфейсы) установите для параметров **I2C** и **SSH** значение **Enable** (Включить), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7e177-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="7e177-161">Этот шаг является необязательным, если у вас нет физических датчиков и вы будете использовать симулированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="7e177-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Включение I2C и SSH на Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="7e177-163">Сведения о том, как включить SSH и I2C, можно найти в дополнительных справочных документах на [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) и [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="7e177-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="7e177-164">Подключение датчика к Pi</span><span class="sxs-lookup"><span data-stu-id="7e177-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="7e177-165">Подключите светодиодный индикатор и датчик BME280 к Pi с помощью монтажной платы и оптоволоконных кабелей, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7e177-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="7e177-166">Если у вас нет датчика, пропустите этот раздел.</span><span class="sxs-lookup"><span data-stu-id="7e177-166">If you don’t have the sensor, skip this section.</span></span>

![Подключение Raspberry Pi и датчика](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="7e177-168">Датчик BME280 может собирать данные о температуре и влажности.</span><span class="sxs-lookup"><span data-stu-id="7e177-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="7e177-169">Светодиодный индикатор мигает при обмене данными между устройством и облаком.</span><span class="sxs-lookup"><span data-stu-id="7e177-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="7e177-170">Чтобы подключить выводы датчика, используйте следующие кабели:</span><span class="sxs-lookup"><span data-stu-id="7e177-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="7e177-171">Начало (датчик и светодиодный индикатор)</span><span class="sxs-lookup"><span data-stu-id="7e177-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="7e177-172">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="7e177-172">End (Board)</span></span>            | <span data-ttu-id="7e177-173">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="7e177-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="7e177-174">VDD (вывод 5G)</span><span class="sxs-lookup"><span data-stu-id="7e177-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="7e177-175">3.3V PWR (вывод 1)</span><span class="sxs-lookup"><span data-stu-id="7e177-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="7e177-176">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="7e177-176">White cable</span></span>   |
| <span data-ttu-id="7e177-177">GND (вывод 7G)</span><span class="sxs-lookup"><span data-stu-id="7e177-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="7e177-178">GND (вывод 6)</span><span class="sxs-lookup"><span data-stu-id="7e177-178">GND (Pin 6)</span></span>            | <span data-ttu-id="7e177-179">Коричневый кабель</span><span class="sxs-lookup"><span data-stu-id="7e177-179">Brown cable</span></span>   |
| <span data-ttu-id="7e177-180">SCK (вывод 8G)</span><span class="sxs-lookup"><span data-stu-id="7e177-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="7e177-181">I2C1 SDA (вывод 3)</span><span class="sxs-lookup"><span data-stu-id="7e177-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="7e177-182">Оранжевый кабель</span><span class="sxs-lookup"><span data-stu-id="7e177-182">Orange cable</span></span>  |
| <span data-ttu-id="7e177-183">SDI (вывод 10G)</span><span class="sxs-lookup"><span data-stu-id="7e177-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="7e177-184">I2C1 SCL (вывод 5)</span><span class="sxs-lookup"><span data-stu-id="7e177-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="7e177-185">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="7e177-185">Red cable</span></span>     |
| <span data-ttu-id="7e177-186">LED VDD (вывод 18F)</span><span class="sxs-lookup"><span data-stu-id="7e177-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="7e177-187">GPIO 24 (вывод 18)</span><span class="sxs-lookup"><span data-stu-id="7e177-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="7e177-188">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="7e177-188">White cable</span></span>   |
| <span data-ttu-id="7e177-189">LED GND (вывод 17F)</span><span class="sxs-lookup"><span data-stu-id="7e177-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="7e177-190">GND (вывод 20)</span><span class="sxs-lookup"><span data-stu-id="7e177-190">GND (Pin 20)</span></span>           | <span data-ttu-id="7e177-191">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="7e177-191">Black cable</span></span>   |

<span data-ttu-id="7e177-192">Щелкните, чтобы просмотреть [схему соответствия выводов Raspberry Pi 2 и 3](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) для справки.</span><span class="sxs-lookup"><span data-stu-id="7e177-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="7e177-193">После успешного подключения датчика BME280 к Raspberry Pi схема должна выглядеть так, как на изображении ниже.</span><span class="sxs-lookup"><span data-stu-id="7e177-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Подключенный компьютер Pi и датчик BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="7e177-195">Подключение устройства Pi к сети</span><span class="sxs-lookup"><span data-stu-id="7e177-195">Connect Pi to the network</span></span>

<span data-ttu-id="7e177-196">Включите устройство Pi, используя кабель Micro USB и источник питания.</span><span class="sxs-lookup"><span data-stu-id="7e177-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="7e177-197">Подключите Pi к проводной сети с помощью кабеля Ethernet или выполните [инструкции](https://www.raspberrypi.org/learning/software-guide/wifi/) от Raspberry Pi Foundation для подключения устройства Pi к беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="7e177-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="7e177-198">После успешного подключения Pi к сети необходимо запомнить [IP-адрес устройства Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="7e177-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Подключение к проводной сети](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="7e177-200">Убедитесь, что плата Pi подключена к той же сети, что и компьютер.</span><span class="sxs-lookup"><span data-stu-id="7e177-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="7e177-201">Например, если компьютер подключен к беспроводной сети, а плата Pi подключена к проводной сети, то IP-адрес может не отобразиться в выходных данных devdisco.</span><span class="sxs-lookup"><span data-stu-id="7e177-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="7e177-202">Запуск примера приложения на Pi</span><span class="sxs-lookup"><span data-stu-id="7e177-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="7e177-203">Клонирование примера приложения и установка пакетов необходимых компонентов</span><span class="sxs-lookup"><span data-stu-id="7e177-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="7e177-204">Используйте один из следующих SSH-клиентов для подключения к Raspberry Pi с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="7e177-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="7e177-205">[PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="7e177-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="7e177-206">IP-адрес устройства Pi требуется для подключения по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="7e177-206">You need the IP address of your Pi to connect it via SSH.</span></span>
    - <span data-ttu-id="7e177-207">Встроенный SSH-клиент ОС Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="7e177-207">The built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="7e177-208">Может потребоваться выполнить `ssh pi@<ip address of pi>` для подключения Pi по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="7e177-208">You might need run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="7e177-209">Имя пользователя по умолчанию — `pi`, а пароль — `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="7e177-209">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="7e177-210">Установите Node.js и NPM на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="7e177-210">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="7e177-211">Сначала следует проверить версию Node.js с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="7e177-211">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="7e177-212">Если версия меньше 4.x или на устройстве Pi отсутствует Node.js, выполните следующую команду для установки или обновления Node.js.</span><span class="sxs-lookup"><span data-stu-id="7e177-212">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="7e177-213">Создайте клон примера приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e177-213">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="7e177-214">Установите все пакеты,</span><span class="sxs-lookup"><span data-stu-id="7e177-214">Install all packages by the following command.</span></span> <span data-ttu-id="7e177-215">в том числе пакет SDK для устройств Azure IoT, библиотеку датчика BME280 и библиотеку Wiring Pi, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e177-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="7e177-216">В зависимости от сетевого подключения процесс установки может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7e177-216">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="7e177-217">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="7e177-217">Configure the sample application</span></span>

1. <span data-ttu-id="7e177-218">Откройте файл конфигурации, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e177-218">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Файл конфигурации](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="7e177-220">В этом файле можно настроить два элемента.</span><span class="sxs-lookup"><span data-stu-id="7e177-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="7e177-221">Первый из них — `interval`, который определяет промежуток времени между отправкой двух сообщений в облако.</span><span class="sxs-lookup"><span data-stu-id="7e177-221">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="7e177-222">Второй — `simulatedData`, который представляет собой логическое значение, определяющее, будут ли использоваться смоделированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="7e177-222">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="7e177-223">Если у вас **нет датчика**, задайте для параметра `simulatedData` значение `true`, чтобы пример приложения создал и использовал смоделированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="7e177-223">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="7e177-224">Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.</span><span class="sxs-lookup"><span data-stu-id="7e177-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="7e177-225">Запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="7e177-225">Run the sample application</span></span>

1. <span data-ttu-id="7e177-226">Запустите пример приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e177-226">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="7e177-227">Обязательно скопируйте и вставьте строку подключения устройства, заключив ее в одинарные кавычки.</span><span class="sxs-lookup"><span data-stu-id="7e177-227">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="7e177-228">Должны отобразиться следующие результаты, содержащие данные датчика и сообщения, которые отправляются в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e177-228">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Выходные данные — данные датчика, отправленные с Raspberry Pi в Центр Интернета вещей](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="7e177-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e177-230">Next steps</span></span>

<span data-ttu-id="7e177-231">Вы запустили пример приложения, чтобы собрать данные датчика и отправить их в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7e177-231">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]