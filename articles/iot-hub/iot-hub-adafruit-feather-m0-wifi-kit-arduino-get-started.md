---
title: "M0 toocloud: подключение Wi-Fi M0 Растушевка tooAzure центр IoT | Документы Microsoft"
description: "Узнайте, как tooset Настройка и подключение Wi-Fi M0 Растушевка Adafruit tooAzure центр IoT toosend данные toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="71b6b-103">Подключения Wi-Fi M0 Растушевка Adafruit tooAzure центр IoT в облаке hello</span><span class="sxs-lookup"><span data-stu-id="71b6b-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Подключение между датчиком BME280, платой Feather M0 WiFi и Центром Интернета вещей](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="71b6b-105">В этом учебнике сначала обучения hello основы работы с Arduino доске.</span><span class="sxs-lookup"><span data-stu-id="71b6b-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="71b6b-106">Затем вы узнаете, как tooseamlessly подключаться toohello облачных устройств с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="71b6b-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="71b6b-107">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="71b6b-107">What you do</span></span>

<span data-ttu-id="71b6b-108">Подключите центра IoT tooan Adafruit Растушевка M0 WiFi, создаваемом.</span><span class="sxs-lookup"><span data-stu-id="71b6b-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="71b6b-109">Затем запустите пример приложения на M0 Wi-Fi toocollect hello температуры и влажности данных из BME280.</span><span class="sxs-lookup"><span data-stu-id="71b6b-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="71b6b-110">Отправьте центра IoT tooyour данных датчика hello.</span><span class="sxs-lookup"><span data-stu-id="71b6b-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="71b6b-111">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="71b6b-111">What you learn</span></span>

* <span data-ttu-id="71b6b-112">Как toocreate центр IoT и регистрация устройства для Растушевка M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="71b6b-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="71b6b-113">Как tooconnect Растушевка M0 Wi-Fi с датчика hello и компьютера</span><span class="sxs-lookup"><span data-stu-id="71b6b-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="71b6b-114">Как toocollect датчиков, выполнив пример приложения на Растушевка M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="71b6b-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="71b6b-115">Как toosend hello центра IoT tooyour данных датчика</span><span class="sxs-lookup"><span data-stu-id="71b6b-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="71b6b-116">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="71b6b-116">What you need</span></span>

![Детали, необходимые для работы с руководством hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="71b6b-118">toocomplete этой операции требуется hello следующую частей из начального набора Растушевка M0 Wi-Fi:</span><span class="sxs-lookup"><span data-stu-id="71b6b-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="71b6b-119">Hello плата Растушевка M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="71b6b-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="71b6b-120">Micro USB tooType USB-кабель</span><span class="sxs-lookup"><span data-stu-id="71b6b-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="71b6b-121">Также необходим hello следующие действия для среды разработки.</span><span class="sxs-lookup"><span data-stu-id="71b6b-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="71b6b-122">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="71b6b-122">An active Azure subscription.</span></span> <span data-ttu-id="71b6b-123">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="71b6b-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="71b6b-124">ПК или компьютер Mac под управлением Windows или Ubuntu;</span><span class="sxs-lookup"><span data-stu-id="71b6b-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="71b6b-125">Беспроводная сеть Wi-Fi M0 Растушевка tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="71b6b-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="71b6b-126">Подключение toodownload hello конфигурации средств Интернета.</span><span class="sxs-lookup"><span data-stu-id="71b6b-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="71b6b-127">[Arduino IDE](https://www.arduino.cc/en/main/software) версии 1.6.8 или более новой.</span><span class="sxs-lookup"><span data-stu-id="71b6b-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="71b6b-128">Более ранних версий не работают с библиотекой hello центр IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="71b6b-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="71b6b-129">Если у вас нет датчика, hello следующие элементы являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="71b6b-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="71b6b-130">Также имеется возможность использовать имитацию датчиков hello:</span><span class="sxs-lookup"><span data-stu-id="71b6b-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="71b6b-131">Датчик температуры и влажности BME280</span><span class="sxs-lookup"><span data-stu-id="71b6b-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="71b6b-132">Монтажная плата</span><span class="sxs-lookup"><span data-stu-id="71b6b-132">A breadboard</span></span>
* <span data-ttu-id="71b6b-133">Многомодовый оптоволоконный кабель с разъемами на обоих концах</span><span class="sxs-lookup"><span data-stu-id="71b6b-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="71b6b-134">Подключения Wi-Fi M0 Растушевка датчика hello и компьютера</span><span class="sxs-lookup"><span data-stu-id="71b6b-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="71b6b-135">В этом разделе подключиться hello датчики tooyour платы.</span><span class="sxs-lookup"><span data-stu-id="71b6b-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="71b6b-136">Затем можно подключить компьютер tooyour устройство для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="71b6b-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="71b6b-137">Подключение DHT22 температуры и влажности датчика tooFeather M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="71b6b-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="71b6b-138">Используйте hello breadboard и перемычки проводов toomake hello подключение.</span><span class="sxs-lookup"><span data-stu-id="71b6b-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="71b6b-139">Если у вас нет датчика, пропустите этот раздел, так как вместо него вы можете использовать симулированные данные.</span><span class="sxs-lookup"><span data-stu-id="71b6b-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Справочные материалы по подключению](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="71b6b-141">Для датчика ПИН-коды используйте hello после подключения:</span><span class="sxs-lookup"><span data-stu-id="71b6b-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="71b6b-142">Начало (датчик)</span><span class="sxs-lookup"><span data-stu-id="71b6b-142">Start (sensor)</span></span>           | <span data-ttu-id="71b6b-143">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="71b6b-143">End (board)</span></span>            | <span data-ttu-id="71b6b-144">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="71b6b-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="71b6b-145">VDD (вывод 27A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="71b6b-146">3V (вывод 3A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="71b6b-147">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="71b6b-147">Red cable</span></span>     |
| <span data-ttu-id="71b6b-148">GND (вывод 29A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="71b6b-149">GND (вывод 6A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="71b6b-150">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="71b6b-150">Black cable</span></span>   |
| <span data-ttu-id="71b6b-151">SCK (вывод 30A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="71b6b-152">SCK (вывод 12A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="71b6b-153">Желтый кабель</span><span class="sxs-lookup"><span data-stu-id="71b6b-153">Yellow cable</span></span>  |
| <span data-ttu-id="71b6b-154">SDO (вывод 31A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="71b6b-155">MI (вывод 14A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="71b6b-156">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="71b6b-156">White cable</span></span>   |
| <span data-ttu-id="71b6b-157">SDI (вывод 32A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="71b6b-158">M0 (вывод 13A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="71b6b-159">Синий кабель</span><span class="sxs-lookup"><span data-stu-id="71b6b-159">Blue cable</span></span>    |
| <span data-ttu-id="71b6b-160">CS (вывод 33A)</span><span class="sxs-lookup"><span data-stu-id="71b6b-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="71b6b-161">GPIO 5 (вывод 15J)</span><span class="sxs-lookup"><span data-stu-id="71b6b-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="71b6b-162">Оранжевый кабель</span><span class="sxs-lookup"><span data-stu-id="71b6b-162">Orange cable</span></span>  |

<span data-ttu-id="71b6b-163">Дополнительные сведения см. в статье [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Выходы датчика влажности, атмосферного давления и температуры Adafruit BME280) и [Adafruit Feather M0 WiFi Pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts) (Выводы платы Adafruit Feather M0 WiFi).</span><span class="sxs-lookup"><span data-stu-id="71b6b-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="71b6b-164">Теперь работающий датчик должен быть подключен к Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Подключение DHT22 к Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="71b6b-166">Подключения Wi-Fi M0 Растушевка tooyour компьютера</span><span class="sxs-lookup"><span data-stu-id="71b6b-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="71b6b-167">Используется hello Micro USB tooType USB кабель tooconnect Wi-Fi M0 Растушевка tooyour компьютеров, как показано:</span><span class="sxs-lookup"><span data-stu-id="71b6b-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![Подключите компьютер tooyour Huzzah Растушевка](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="71b6b-169">Добавление разрешений для последовательного порта (только в Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="71b6b-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="71b6b-170">Если вы используете Ubuntu, убедитесь, что у вас разрешения toooperate hello на hello USB порта из Растушевка M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="71b6b-171">tooadd последовательный порт, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="71b6b-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="71b6b-172">В терминалов выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="71b6b-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="71b6b-173">При получении одного из hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="71b6b-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="71b6b-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="71b6b-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="71b6b-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="71b6b-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="71b6b-176">Обратите внимание, что в выходных данных hello `uucp` или `dialout` — имя владельца группы hello hello USB-порту.</span><span class="sxs-lookup"><span data-stu-id="71b6b-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="71b6b-177">tooadd hello toohello группы пользователей, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="71b6b-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="71b6b-178">В предыдущем шаге hello, получения имени владельца группы hello `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="71b6b-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="71b6b-179">`<username>` — это имя пользователя Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="71b6b-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="71b6b-180">Для tooappear изменение hello выйдите из Ubuntu и снова войдите в нее.</span><span class="sxs-lookup"><span data-stu-id="71b6b-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="71b6b-181">Собирать данные датчиков и отправлять их tooyour центра IoT</span><span class="sxs-lookup"><span data-stu-id="71b6b-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="71b6b-182">В этом разделе рассказывается о том, как развернуть и запустить пример приложения на плате Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="71b6b-183">Пример приложения Hello делает hello мигающий Индикатор на Растушевка M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="71b6b-184">После этого он отправляет hello температуры и влажности собранные данные датчика tooyour hello BME280 центр IoT.</span><span class="sxs-lookup"><span data-stu-id="71b6b-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="71b6b-185">Пример приложения hello из GitHub и подготовка hello Arduino интегрированной среды разработки</span><span class="sxs-lookup"><span data-stu-id="71b6b-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="71b6b-186">Пример приложения Hello находится на GitHub.</span><span class="sxs-lookup"><span data-stu-id="71b6b-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="71b6b-187">Клонирование репозитория образец hello, который содержит пример приложения hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="71b6b-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="71b6b-188">репозиторий образец hello tooclone, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="71b6b-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="71b6b-189">Откройте окно командной строки или терминала.</span><span class="sxs-lookup"><span data-stu-id="71b6b-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="71b6b-190">Go tooa папку hello образец приложения toobe хранятся.</span><span class="sxs-lookup"><span data-stu-id="71b6b-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="71b6b-191">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="71b6b-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="71b6b-192">Установить пакет hello для Растушевка M0 Wi-Fi в hello Arduino интегрированной среды разработки</span><span class="sxs-lookup"><span data-stu-id="71b6b-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="71b6b-193">Откройте папку hello, где хранится пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="71b6b-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="71b6b-194">Откройте файл app.ino hello в папке приложения hello в hello Arduino интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="71b6b-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Откройте пример приложения hello в интегрированной среде разработки Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="71b6b-196">Нажмите кнопку **файл** > **предпочтения** (Windows или Linux) или **Arduino** > **предпочтения** (Mac) и скопируйте ее и Вставить hello следующую ссылку в hello **дополнительные URL-адреса диспетчера досок** в диалоговом окне приветствия предпочтения Arduino интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="71b6b-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="71b6b-197">Нажмите кнопку **средства** > **плата** > **досок Manager**и установите hello `Arduino SAMD Boards` версии `1.6.2` или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="71b6b-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="71b6b-198">Затем в том же окне hello, установите `Adafruit SAMD Boards` tooadd hello плата файл определения пакета.</span><span class="sxs-lookup"><span data-stu-id="71b6b-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![установлен пакет esp8266 Hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="71b6b-200">Щелкните **Инструменты** > **Платы** > **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="71b6b-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="71b6b-201">Установите драйверы (только для Windows).</span><span class="sxs-lookup"><span data-stu-id="71b6b-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="71b6b-202">После подключения Wi-Fi M0 Растушевка, может потребоваться tooinstall драйвера.</span><span class="sxs-lookup"><span data-stu-id="71b6b-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="71b6b-203">Нажмите кнопку [hello ссылку на веб-странице hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) установщик драйвера toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="71b6b-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="71b6b-204">Выполните hello действия tooinstall hello драйверы.</span><span class="sxs-lookup"><span data-stu-id="71b6b-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="71b6b-205">Установка необходимых библиотек</span><span class="sxs-lookup"><span data-stu-id="71b6b-205">Install necessary libraries</span></span>

1. <span data-ttu-id="71b6b-206">В hello Arduino IDE, щелкните **схематической** > **включают библиотеки** > **Управление библиотеками**.</span><span class="sxs-lookup"><span data-stu-id="71b6b-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="71b6b-207">Поиск hello следующие имена библиотек по одному.</span><span class="sxs-lookup"><span data-stu-id="71b6b-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="71b6b-208">Для каждой найденной библиотеки щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="71b6b-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="71b6b-209">Вручную установите `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="71b6b-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="71b6b-210">Go слишком[этот веб-сайт](https://github.com/adafruit/Adafruit_WINC1500) и нажмите кнопку **клон или загрузки** > **загрузить ZIP**.</span><span class="sxs-lookup"><span data-stu-id="71b6b-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="71b6b-211">В вашей СРЕДЕ Arduino перейдите слишком**схематической** > **включают библиотеки** > **добавьте .zip библиотеки** и добавьте hello ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="71b6b-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="71b6b-212">Используйте пример приложения hello, при отсутствии реальных BME280 датчика</span><span class="sxs-lookup"><span data-stu-id="71b6b-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="71b6b-213">При отсутствии реальных датчика BME280 пример приложения hello можно смоделировать температуры и влажности данных.</span><span class="sxs-lookup"><span data-stu-id="71b6b-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="71b6b-214">tooset hello образец приложения toouse моделирования данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="71b6b-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="71b6b-215">Откройте hello `config.h` файла в hello `app` папки.</span><span class="sxs-lookup"><span data-stu-id="71b6b-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="71b6b-216">Найдите следующие строки кода hello и измените значение hello из `false` слишком`true`:</span><span class="sxs-lookup"><span data-stu-id="71b6b-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Настройка приложения toouse имитируемые hello примеров данных](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="71b6b-218">Сохраните файл hello с `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="71b6b-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="71b6b-219">Развертывание tooFeather приложения образец hello M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="71b6b-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="71b6b-220">В hello Arduino IDE, щелкните **средство** > **порт**и нажмите кнопку hello последовательного порта для Растушевка M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="71b6b-221">Нажмите кнопку **схематической** > **отправить** toobuild и развернуть tooFeather приложения образец hello M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="71b6b-222">Ввод учетных данных</span><span class="sxs-lookup"><span data-stu-id="71b6b-222">Enter your credentials</span></span>

<span data-ttu-id="71b6b-223">После успешного завершения передачи hello, выполните эти шаги tooenter учетные данные.</span><span class="sxs-lookup"><span data-stu-id="71b6b-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="71b6b-224">В hello Arduino IDE, щелкните **средства** > **последовательного монитор**.</span><span class="sxs-lookup"><span data-stu-id="71b6b-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="71b6b-225">В hello нижнем правом углу окна последовательной монитор hello, выберите **без завершения строк** в раскрывающемся списке hello слева hello.</span><span class="sxs-lookup"><span data-stu-id="71b6b-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="71b6b-226">Выберите **115200 бод** в hello раскрывающегося списка в правом hello.</span><span class="sxs-lookup"><span data-stu-id="71b6b-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="71b6b-227">В поле ввода hello вверху hello, введите hello следующую информацию, если вы задаваемые tooprovide и нажмите кнопку **отправки**:</span><span class="sxs-lookup"><span data-stu-id="71b6b-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="71b6b-228">Идентификатор SSID для подключения Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="71b6b-229">Пароль Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-229">Wi-Fi password</span></span>
   * <span data-ttu-id="71b6b-230">Строка подключения к устройству.</span><span class="sxs-lookup"><span data-stu-id="71b6b-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="71b6b-231">Hello учетные данные хранятся в hello EEPROM из Растушевка M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="71b6b-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="71b6b-232">Если вы нажмете кнопку Сброс hello hello плата Растушевка M0 Wi-Fi, пример приложения hello запросом tooerase hello сведения.</span><span class="sxs-lookup"><span data-stu-id="71b6b-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="71b6b-233">Введите `Y` tooerase hello сведения.</span><span class="sxs-lookup"><span data-stu-id="71b6b-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="71b6b-234">Появится сообщение hello tooprovide сведения еще раз.</span><span class="sxs-lookup"><span data-stu-id="71b6b-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="71b6b-235">Убедитесь, что пример приложения hello успешно запущен</span><span class="sxs-lookup"><span data-stu-id="71b6b-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="71b6b-236">Если вы видите hello следующие выходные данные из окна последовательной монитор hello и hello мигающий Индикатор на M0 Растушевка Wi-Fi, пример приложения hello выполняется успешно:</span><span class="sxs-lookup"><span data-stu-id="71b6b-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Окончательные выходные данные в интегрированной среде разработки Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="71b6b-238">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71b6b-238">Next steps</span></span>

<span data-ttu-id="71b6b-239">Успешно подключен центра IoT tooyour Растушевка M0 Wi-Fi и отправленных центра IoT tooyour данных датчика захвачен hello.</span><span class="sxs-lookup"><span data-stu-id="71b6b-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

