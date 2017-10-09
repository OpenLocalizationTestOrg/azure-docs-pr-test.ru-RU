---
title: "toocloud aaaESP8266 - tooAzure подключения Dev самое Sparkfun ESP8266 центр IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключите toosend данных toohello Azure облачной платформы разработки самое ESP8266 Sparkfun tooAzure центр IoT для него в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="841c7-103">Подключение Dev самое ESP8266 Sparkfun tooAzure центр IoT в облаке hello</span><span class="sxs-lookup"><span data-stu-id="841c7-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Подключение DHT22 и Thing Dev к Центру Интернета вещей](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="841c7-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="841c7-105">What you will do</span></span>

<span data-ttu-id="841c7-106">Подключите центра IoT tooan Sparkfun ESP8266 самое разработки, вы создадите.</span><span class="sxs-lookup"><span data-stu-id="841c7-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="841c7-107">Запустите образец приложения ESP8266 toocollect температуры и влажности данных с использованием DHT22 датчиков.</span><span class="sxs-lookup"><span data-stu-id="841c7-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="841c7-108">Наконец отправьте центра IoT tooyour данных датчика hello.</span><span class="sxs-lookup"><span data-stu-id="841c7-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="841c7-109">При использовании других плат ESP8266 все равно можно выполнять эти действия tooconnect его tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="841c7-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="841c7-110">В зависимости от hello ESP8266 Доска вы используете, может потребоваться tooreconfigure hello `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="841c7-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="841c7-111">Например, при использовании ESP8266 из AI-Thinker, можно изменить его из `0` слишком`2`.</span><span class="sxs-lookup"><span data-stu-id="841c7-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="841c7-112">Нет начального набора? Щелкните [здесь](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="841c7-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="841c7-113">Новые знания</span><span class="sxs-lookup"><span data-stu-id="841c7-113">What you will learn</span></span>

* <span data-ttu-id="841c7-114">Как toocreate центр IoT и регистрация устройства для всего устройствам.</span><span class="sxs-lookup"><span data-stu-id="841c7-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="841c7-115">Как tooconnect самое разработки с датчика hello и на компьютере.</span><span class="sxs-lookup"><span data-stu-id="841c7-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="841c7-116">Как toocollect датчиков, выполнив пример приложения на самое устройствам.</span><span class="sxs-lookup"><span data-stu-id="841c7-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="841c7-117">Как toosend hello центра IoT tooyour данных датчика.</span><span class="sxs-lookup"><span data-stu-id="841c7-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="841c7-118">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="841c7-118">What you will need</span></span>

![Детали, необходимые для работы с руководством hello](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="841c7-120">toocomplete этой операции требуется hello следующую частей из начального набора разработки вещь:</span><span class="sxs-lookup"><span data-stu-id="841c7-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="841c7-121">Здравствуйте, плата Sparkfun ESP8266 самое разработки.</span><span class="sxs-lookup"><span data-stu-id="841c7-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="841c7-122">Micro USB tooType USB-кабель.</span><span class="sxs-lookup"><span data-stu-id="841c7-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="841c7-123">Следующие hello также необходим для среды разработки.</span><span class="sxs-lookup"><span data-stu-id="841c7-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="841c7-124">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="841c7-124">An active Azure subscription.</span></span> <span data-ttu-id="841c7-125">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="841c7-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="841c7-126">ПК или компьютер Mac под управлением Windows или Ubuntu;</span><span class="sxs-lookup"><span data-stu-id="841c7-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="841c7-127">Беспроводной сети для разработки самое ESP8266 Sparkfun tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="841c7-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="841c7-128">Средство настройки hello toodownload подключения Интернета.</span><span class="sxs-lookup"><span data-stu-id="841c7-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="841c7-129">[Интегрированная среда разработки Arduino](https://www.arduino.cc/en/main/software) версии 1.6.8 (или более поздней версии), более ранних версий не будет работать с hello AzureIoT библиотеки.</span><span class="sxs-lookup"><span data-stu-id="841c7-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="841c7-130">Hello следующие элементы являются необязательными случаю, когда не датчика.</span><span class="sxs-lookup"><span data-stu-id="841c7-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="841c7-131">Также имеется возможность использовать имитацию датчиков hello.</span><span class="sxs-lookup"><span data-stu-id="841c7-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="841c7-132">Датчик температуры и влажности Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="841c7-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="841c7-133">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="841c7-133">A breadboard.</span></span>
* <span data-ttu-id="841c7-134">Многомодовый оптоволоконный кабель с разъемами на обоих концах.</span><span class="sxs-lookup"><span data-stu-id="841c7-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="841c7-135">Связь ESP8266 самое разработки с датчика hello и компьютера</span><span class="sxs-lookup"><span data-stu-id="841c7-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="841c7-136">Датчик температуры и влажности DHT22 подключения tooESP8266 самое разработки</span><span class="sxs-lookup"><span data-stu-id="841c7-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="841c7-137">Используйте hello breadboard и перемычки проводов toomake hello соединения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="841c7-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="841c7-138">Если у вас нет датчика, пропустите этот раздел, так как вместо него вы можете использовать симулированные данные.</span><span class="sxs-lookup"><span data-stu-id="841c7-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Справочные материалы по подключению](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="841c7-140">Для датчика ПИН-коды мы будем использовать следующие привязки hello:</span><span class="sxs-lookup"><span data-stu-id="841c7-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="841c7-141">Начало (датчик)</span><span class="sxs-lookup"><span data-stu-id="841c7-141">Start (Sensor)</span></span>           | <span data-ttu-id="841c7-142">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="841c7-142">End (Board)</span></span>           | <span data-ttu-id="841c7-143">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="841c7-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="841c7-144">VDD (вывод 27F)</span><span class="sxs-lookup"><span data-stu-id="841c7-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="841c7-145">3V (вывод 8A)</span><span class="sxs-lookup"><span data-stu-id="841c7-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="841c7-146">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="841c7-146">Red cable</span></span>     |
| <span data-ttu-id="841c7-147">DATA (вывод 28F)</span><span class="sxs-lookup"><span data-stu-id="841c7-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="841c7-148">GPIO 2 (вывод 9A)</span><span class="sxs-lookup"><span data-stu-id="841c7-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="841c7-149">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="841c7-149">White cable</span></span>    |
| <span data-ttu-id="841c7-150">GND (вывод 30F)</span><span class="sxs-lookup"><span data-stu-id="841c7-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="841c7-151">GND (вывод 7J)</span><span class="sxs-lookup"><span data-stu-id="841c7-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="841c7-152">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="841c7-152">Black cable</span></span>   |


- <span data-ttu-id="841c7-153">Дополнительные сведения см. в [документации по установке датчика DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) и в [спецификации Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="841c7-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="841c7-154">Теперь работающий датчик должен быть подключен к Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="841c7-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![Подключение dht22 к ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="841c7-156">Подключите компьютер разработки самое ESP8266 Sparkfun tooyour</span><span class="sxs-lookup"><span data-stu-id="841c7-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="841c7-157">Используйте hello Micro USB tooType USB кабель tooconnect разработки самое ESP8266 Sparkfun tooyour компьютера следующим образом.</span><span class="sxs-lookup"><span data-stu-id="841c7-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![Подключите компьютер tooyour huzzah Растушевка](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="841c7-159">Добавление разрешений для последовательного порта (только в Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="841c7-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="841c7-160">Если вы используете Ubuntu, убедитесь, что обычный пользователь имеет разрешения toooperate hello на hello USB порта из Sparkfun ESP8266 самое устройствам.</span><span class="sxs-lookup"><span data-stu-id="841c7-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="841c7-161">разрешения tooadd последовательного порта для обычного пользователя, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="841c7-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="841c7-162">Выполните следующие команды в терминал hello.</span><span class="sxs-lookup"><span data-stu-id="841c7-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="841c7-163">При получении одного из hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="841c7-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="841c7-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="841c7-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="841c7-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="841c7-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="841c7-166">Обратите внимание, в выходных данных hello, `uucp` или `dialout` , представляющим hello группы владельца имя hello USB-порту.</span><span class="sxs-lookup"><span data-stu-id="841c7-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="841c7-167">Добавление группы toohello hello пользователей, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="841c7-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="841c7-168">`<group-owner-name>`— Имя владельца группы hello, полученную на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="841c7-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="841c7-169">`<username>` — это имя пользователя Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="841c7-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="841c7-170">Выйдите из Ubuntu и снова войти в нем для hello изменение tootake эффекта.</span><span class="sxs-lookup"><span data-stu-id="841c7-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="841c7-171">Собирать данные датчиков и отправлять их tooyour центра IoT</span><span class="sxs-lookup"><span data-stu-id="841c7-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="841c7-172">В этом разделе вы развернете и запустите пример приложения на плате Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="841c7-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="841c7-173">Пример приложения Hello мигает hello Светодиод Sparkfun ESP8266 самое разработки и отправляет hello температуры и влажности собранные данные датчика tooyour hello DHT22 центр IoT.</span><span class="sxs-lookup"><span data-stu-id="841c7-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="841c7-174">Получение образца приложения hello из GitHub</span><span class="sxs-lookup"><span data-stu-id="841c7-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="841c7-175">Пример приложения Hello находится на GitHub.</span><span class="sxs-lookup"><span data-stu-id="841c7-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="841c7-176">Клонирование репозитория образец hello, который содержит пример приложения hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="841c7-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="841c7-177">репозиторий образец hello tooclone, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="841c7-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="841c7-178">Откройте окно командной строки или терминала.</span><span class="sxs-lookup"><span data-stu-id="841c7-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="841c7-179">Go tooa папку hello образец приложения toobe хранятся.</span><span class="sxs-lookup"><span data-stu-id="841c7-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="841c7-180">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="841c7-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="841c7-181">Установка пакета hello для разработки самое ESP8266 Sparkfun в интегрированной среде разработки Arduino:</span><span class="sxs-lookup"><span data-stu-id="841c7-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="841c7-182">Откройте папку hello, где хранится пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="841c7-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="841c7-183">Откройте файл app.ino hello в папке приложения hello Arduino интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="841c7-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![Откройте пример приложения hello в интегрированной среде разработки arduino](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="841c7-185">В hello Arduino IDE, щелкните **файл** > **предпочтения**.</span><span class="sxs-lookup"><span data-stu-id="841c7-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="841c7-186">В hello **предпочтения** диалоговое окно, нажмите кнопку Далее toohello hello значок **дополнительные URL-адреса диспетчера досок** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="841c7-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="841c7-187">Во всплывающем окне приветствия, введите URL-адреса hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="841c7-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![tooa точки URL-адреса пакета в интегрированной среде разработки arduino](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="841c7-189">В hello **предпочтения** диалоговое окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="841c7-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="841c7-190">Щелкните **Инструменты** > **Платы** > **Менеджер плат**, а затем выполните поиск по esp8266.</span><span class="sxs-lookup"><span data-stu-id="841c7-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="841c7-191">Должен быть установлен пакет ESP8266 версии 2.2.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="841c7-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![установлен пакет esp8266 Hello](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="841c7-193">Щелкните **Инструменты** > **Платы** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="841c7-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="841c7-194">Установка необходимых библиотек</span><span class="sxs-lookup"><span data-stu-id="841c7-194">Install necessary libraries</span></span>

1. <span data-ttu-id="841c7-195">В hello Arduino IDE, щелкните **схематической** > **включают библиотеки** > **Управление библиотеками**.</span><span class="sxs-lookup"><span data-stu-id="841c7-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="841c7-196">Поиск hello следующие имена библиотек по одному.</span><span class="sxs-lookup"><span data-stu-id="841c7-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="841c7-197">Для каждого из библиотеки hello, можно найти, установите **установить**.</span><span class="sxs-lookup"><span data-stu-id="841c7-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="841c7-198">У вас нет датчика DHT22?</span><span class="sxs-lookup"><span data-stu-id="841c7-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="841c7-199">Пример приложения Hello можно смоделировать температуры и влажности данных на случай реальные датчика DHT22 не нужно.</span><span class="sxs-lookup"><span data-stu-id="841c7-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="841c7-200">tooenable hello образец приложения toouse моделирования данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="841c7-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="841c7-201">Откройте hello `config.h` файла в hello `app` папки.</span><span class="sxs-lookup"><span data-stu-id="841c7-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="841c7-202">Найдите следующие строки кода hello и измените значение hello из `false` слишком`true`:</span><span class="sxs-lookup"><span data-stu-id="841c7-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Настройка приложения toouse имитируемые hello примеров данных](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="841c7-204">Сохраните изменения с помощью `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="841c7-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="841c7-205">Развертывание hello образец приложения tooSparkfun ESP8266 самое разработки</span><span class="sxs-lookup"><span data-stu-id="841c7-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="841c7-206">В hello Arduino IDE, щелкните **средство** > **порт**и нажмите кнопку hello последовательного порта для устройствам Sparkfun ESP8266 вещь.</span><span class="sxs-lookup"><span data-stu-id="841c7-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="841c7-207">Нажмите кнопку **схематической** > **отправить** toobuild и развернуть tooSparkfun приложения образец hello устройствам ESP8266 вещь.</span><span class="sxs-lookup"><span data-stu-id="841c7-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="841c7-208">При использовании macOS, вероятно, могут быть hello следующие сообщения во время передачи данных.</span><span class="sxs-lookup"><span data-stu-id="841c7-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="841c7-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="841c7-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="841c7-210">Откройте окно ternimal и Готово ниже toosolve действия этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="841c7-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="841c7-211">Ввод учетных данных</span><span class="sxs-lookup"><span data-stu-id="841c7-211">Enter your credentials</span></span>

<span data-ttu-id="841c7-212">После успешного завершения передачи hello, выполните шаги tooenter hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="841c7-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="841c7-213">В hello Arduino IDE, щелкните **средства** > **последовательного монитор**.</span><span class="sxs-lookup"><span data-stu-id="841c7-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="841c7-214">В окне приветствия последовательного монитора Обратите внимание, hello двух раскрывающихся списках на hello нижнем правом углу.</span><span class="sxs-lookup"><span data-stu-id="841c7-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="841c7-215">Выберите **без завершения строк** для hello левом раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="841c7-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="841c7-216">Выберите **115200 бод** для hello правого раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="841c7-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="841c7-217">В hello входной расположенный вверху hello hello последовательного «монитор» введите следующую информацию в ответ на запрос tooprovide hello их, а затем нажмите кнопку **отправки**.</span><span class="sxs-lookup"><span data-stu-id="841c7-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="841c7-218">Идентификатор SSID для подключения Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="841c7-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="841c7-219">Пароль Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="841c7-219">Wi-Fi password</span></span>
   * <span data-ttu-id="841c7-220">Строка подключения к устройству.</span><span class="sxs-lookup"><span data-stu-id="841c7-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="841c7-221">Hello учетные данные хранятся в hello EEPROM из Sparkfun ESP8266 самое устройствам.</span><span class="sxs-lookup"><span data-stu-id="841c7-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="841c7-222">При нажатии кнопки сброса hello на hello Dev самое ESP8266 Sparkfun плата пример приложения hello запрашивает Если интересующий вас tooerase hello.</span><span class="sxs-lookup"><span data-stu-id="841c7-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="841c7-223">Введите `Y` удалены сведения hello toohave и предлагают tooprovide hello их еще раз.</span><span class="sxs-lookup"><span data-stu-id="841c7-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="841c7-224">Убедитесь, что успешно выполняется пример приложения hello</span><span class="sxs-lookup"><span data-stu-id="841c7-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="841c7-225">Если вы видите hello следующие выходные данные из окна последовательной монитор hello и hello мигающий Индикатор на ESP8266 самое Sparkfun разработки, пример приложения hello выполняется успешно.</span><span class="sxs-lookup"><span data-stu-id="841c7-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![Окончательные выходные данные в Arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="841c7-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="841c7-227">Next steps</span></span>

<span data-ttu-id="841c7-228">Успешно подключен концентратор IoT tooyour Sparkfun ESP8266 самое разработки и отправки центра IoT tooyour данных датчика захвачен hello.</span><span class="sxs-lookup"><span data-stu-id="841c7-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
