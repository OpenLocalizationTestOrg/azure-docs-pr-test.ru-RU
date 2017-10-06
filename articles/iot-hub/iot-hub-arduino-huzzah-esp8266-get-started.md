---
title: "toocloud aaaESP8266 - tooAzure подключения ESP8266 HUZZAH Растушевка центра IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключения tooAzure ESP8266 HUZZAH Adafruit Растушевка центр IoT для него toosend данных toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="0c715-103">Подключение tooAzure ESP8266 HUZZAH Adafruit Растушевка центр IoT в облаке hello</span><span class="sxs-lookup"><span data-stu-id="0c715-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Подключение между DHT22, Feather HUZZAH ESP8266 и Центром Интернета вещей](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="0c715-105">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="0c715-105">What you do</span></span>


<span data-ttu-id="0c715-106">Подключите центра IoT tooan ESP8266 HUZZAH Adafruit Растушевка созданного вами.</span><span class="sxs-lookup"><span data-stu-id="0c715-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="0c715-107">Затем запустите пример приложения на ESP8266 toocollect hello температуры и влажности данных с использованием DHT22 датчиков.</span><span class="sxs-lookup"><span data-stu-id="0c715-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="0c715-108">Отправьте центра IoT tooyour данных датчика hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="0c715-109">При использовании других плат ESP8266 все равно можно выполнять эти действия tooconnect его tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="0c715-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="0c715-110">В зависимости от hello ESP8266 Доска вы используете, может потребоваться tooreconfigure hello `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="0c715-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="0c715-111">Например, вы используете ESP8266 из Thinker аналитики Активов, может измениться из `0` слишком`2`.</span><span class="sxs-lookup"><span data-stu-id="0c715-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="0c715-112">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="0c715-112">Don't have a kit yet?</span></span> <span data-ttu-id="0c715-113">Получить его из hello [веб-сайте Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="0c715-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="0c715-114">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="0c715-114">What you learn</span></span>

* <span data-ttu-id="0c715-115">Как toocreate центр IoT и регистрация устройства для ESP8266 HUZZAH Растушевка</span><span class="sxs-lookup"><span data-stu-id="0c715-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="0c715-116">Как tooconnect ESP8266 HUZZAH Растушевка с датчика hello и компьютера</span><span class="sxs-lookup"><span data-stu-id="0c715-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="0c715-117">Как toocollect датчиков, выполнив пример приложения на ESP8266 HUZZAH Растушевка</span><span class="sxs-lookup"><span data-stu-id="0c715-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="0c715-118">Как toosend hello центра IoT tooyour данных датчика</span><span class="sxs-lookup"><span data-stu-id="0c715-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0c715-119">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="0c715-119">What you need</span></span>

![Детали, необходимые для работы с руководством hello](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="0c715-121">toocomplete этой операции требуется hello следующую частей из начального набора Растушевка HUZZAH ESP8266:</span><span class="sxs-lookup"><span data-stu-id="0c715-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="0c715-122">плата ESP8266 HUZZAH Растушевка Hello</span><span class="sxs-lookup"><span data-stu-id="0c715-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="0c715-123">Micro USB tooType USB-кабель</span><span class="sxs-lookup"><span data-stu-id="0c715-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="0c715-124">Также необходим hello следующие действия для среды разработки.</span><span class="sxs-lookup"><span data-stu-id="0c715-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="0c715-125">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="0c715-125">An active Azure subscription.</span></span> <span data-ttu-id="0c715-126">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0c715-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="0c715-127">ПК или компьютер Mac под управлением Windows или Ubuntu;</span><span class="sxs-lookup"><span data-stu-id="0c715-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="0c715-128">Tooconnect ESP8266 HUZZAH Растушевка для беспроводных сетей.</span><span class="sxs-lookup"><span data-stu-id="0c715-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="0c715-129">Средство настройки hello toodownload подключения Интернета.</span><span class="sxs-lookup"><span data-stu-id="0c715-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="0c715-130">[Arduino IDE](https://www.arduino.cc/en/main/software) версии 1.6.8 или более новой.</span><span class="sxs-lookup"><span data-stu-id="0c715-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="0c715-131">Более ранних версий не работают с библиотекой AzureIoT hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="0c715-132">Hello следующие элементы являются необязательными случаю, когда не датчика.</span><span class="sxs-lookup"><span data-stu-id="0c715-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="0c715-133">Также имеется возможность использовать имитацию датчиков hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="0c715-134">Датчик температуры и влажности Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="0c715-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="0c715-135">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="0c715-135">A breadboard</span></span>
* <span data-ttu-id="0c715-136">Многомодовый оптоволоконный кабель с разъемами на обоих концах</span><span class="sxs-lookup"><span data-stu-id="0c715-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="0c715-137">Связь ESP8266 HUZZAH Растушевка с датчика hello и компьютера</span><span class="sxs-lookup"><span data-stu-id="0c715-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="0c715-138">В этом разделе подключиться hello датчики tooyour платы.</span><span class="sxs-lookup"><span data-stu-id="0c715-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="0c715-139">Затем можно подключить компьютер tooyour устройство для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="0c715-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="0c715-140">Подключение DHT22 температуры и влажности датчика tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="0c715-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="0c715-141">Используйте hello breadboard и перемычки проводов toomake hello соединения следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0c715-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="0c715-142">Если у вас нет датчика, пропустите этот раздел, так как вместо него вы можете использовать симулированные данные.</span><span class="sxs-lookup"><span data-stu-id="0c715-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Справочные материалы по подключению](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="0c715-144">Для датчика ПИН-коды используйте hello после подключения:</span><span class="sxs-lookup"><span data-stu-id="0c715-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="0c715-145">Начало (датчик)</span><span class="sxs-lookup"><span data-stu-id="0c715-145">Start (Sensor)</span></span>           | <span data-ttu-id="0c715-146">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="0c715-146">End (Board)</span></span>           | <span data-ttu-id="0c715-147">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="0c715-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="0c715-148">VDD (вывод 31F)</span><span class="sxs-lookup"><span data-stu-id="0c715-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="0c715-149">3V (вывод 58H)</span><span class="sxs-lookup"><span data-stu-id="0c715-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="0c715-150">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="0c715-150">Red cable</span></span>     |
| <span data-ttu-id="0c715-151">DATA (вывод 32F)</span><span class="sxs-lookup"><span data-stu-id="0c715-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="0c715-152">GPIO 2 (вывод 46A)</span><span class="sxs-lookup"><span data-stu-id="0c715-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="0c715-153">Синий кабель</span><span class="sxs-lookup"><span data-stu-id="0c715-153">Blue cable</span></span>    |
| <span data-ttu-id="0c715-154">GND (вывод 34F)</span><span class="sxs-lookup"><span data-stu-id="0c715-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="0c715-155">GND (вывод 56I)</span><span class="sxs-lookup"><span data-stu-id="0c715-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="0c715-156">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="0c715-156">Black cable</span></span>   |

<span data-ttu-id="0c715-157">Дополнительные сведения см. в статьях о [подключении к датчику Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) и [выводах Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="0c715-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="0c715-158">Теперь работающий датчик должен быть подключен к Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0c715-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Подключение DHT22 к Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="0c715-160">Подключите компьютер tooyour ESP8266 HUZZAH Растушевка</span><span class="sxs-lookup"><span data-stu-id="0c715-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="0c715-161">Как показано далее, используйте hello Micro USB tooType USB кабель tooconnect ESP8266 HUZZAH Растушевка tooyour компьютера.</span><span class="sxs-lookup"><span data-stu-id="0c715-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Подключите компьютер tooyour Huzzah Растушевка](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="0c715-163">Добавление разрешений для последовательного порта (только в Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="0c715-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="0c715-164">Если вы используете Ubuntu, убедитесь, что имеется на hello USB порта из Растушевка HUZZAH ESP8266 toooperate разрешения hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="0c715-165">tooadd последовательный порт, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0c715-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="0c715-166">Выполните следующие команды в терминал hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="0c715-167">При получении одного из hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0c715-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="0c715-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="0c715-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="0c715-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="0c715-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="0c715-170">Обратите внимание, что в выходных данных hello `uucp` или `dialout` — имя владельца группы hello hello USB-порту.</span><span class="sxs-lookup"><span data-stu-id="0c715-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="0c715-171">Добавление группы toohello hello пользователей, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="0c715-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="0c715-172">`<group-owner-name>`— Имя владельца группы hello, полученную на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="0c715-173">`<username>` — это имя пользователя Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0c715-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="0c715-174">Выйдите из Ubuntu и войдите в нее снова для tooappear изменение hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="0c715-175">Собирать данные датчиков и отправлять их tooyour центра IoT</span><span class="sxs-lookup"><span data-stu-id="0c715-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="0c715-176">В этом разделе вы развернете и запустите пример приложения на плате Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0c715-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="0c715-177">Пример приложения Hello мигает hello Светодиод Растушевка HUZZAH ESP8266 и отправляет hello температуры и влажности собранные данные датчика tooyour hello DHT22 центр IoT.</span><span class="sxs-lookup"><span data-stu-id="0c715-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="0c715-178">Получение образца приложения hello из GitHub</span><span class="sxs-lookup"><span data-stu-id="0c715-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="0c715-179">Пример приложения Hello находится на GitHub.</span><span class="sxs-lookup"><span data-stu-id="0c715-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="0c715-180">Клонирование репозитория образец hello, который содержит пример приложения hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="0c715-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="0c715-181">репозиторий образец hello tooclone, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0c715-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="0c715-182">Откройте окно командной строки или терминала.</span><span class="sxs-lookup"><span data-stu-id="0c715-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="0c715-183">Go tooa папку hello образец приложения toobe хранятся.</span><span class="sxs-lookup"><span data-stu-id="0c715-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="0c715-184">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="0c715-185">Установите пакет hello для ESP8266 HUZZAH Растушевка hello Arduino интегрированной среды разработки:</span><span class="sxs-lookup"><span data-stu-id="0c715-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="0c715-186">Откройте папку hello, где хранится пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="0c715-187">Откройте файл app.ino hello в папке приложения hello в hello Arduino интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="0c715-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Откройте пример приложения hello в интегрированной среде разработки Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="0c715-189">В hello Arduino IDE, щелкните **файл** > **предпочтения**.</span><span class="sxs-lookup"><span data-stu-id="0c715-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="0c715-190">В hello **предпочтения** диалоговое окно, нажмите кнопку Далее toohello hello значок **дополнительные URL-адреса диспетчера досок** поле.</span><span class="sxs-lookup"><span data-stu-id="0c715-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="0c715-191">Во всплывающем окне приветствия, введите URL-адреса hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0c715-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Tooa точки URL-адреса пакета в интегрированной среде разработки Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="0c715-193">В hello **предпочтения** диалоговое окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0c715-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="0c715-194">Щелкните **Инструменты** > **Платы** > **Менеджер плат**, а затем выполните поиск по esp8266.</span><span class="sxs-lookup"><span data-stu-id="0c715-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="0c715-195">Диспетчер плат показывает, что установлена плата ESP8266 2.2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0c715-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![установлен пакет esp8266 Hello](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="0c715-197">Щелкните **Инструменты** > **Платы** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="0c715-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="0c715-198">Установка необходимых библиотек</span><span class="sxs-lookup"><span data-stu-id="0c715-198">Install necessary libraries</span></span>

1. <span data-ttu-id="0c715-199">В hello Arduino IDE, щелкните **схематической** > **включают библиотеки** > **Управление библиотеками**.</span><span class="sxs-lookup"><span data-stu-id="0c715-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="0c715-200">Поиск hello следующие имена библиотек по одному.</span><span class="sxs-lookup"><span data-stu-id="0c715-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="0c715-201">Для каждой найденной библиотеки щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="0c715-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="0c715-202">У вас нет датчика DHT22?</span><span class="sxs-lookup"><span data-stu-id="0c715-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="0c715-203">Пример приложения Hello можно смоделировать температуры и влажности данных на случай реальные датчика DHT22 не нужно.</span><span class="sxs-lookup"><span data-stu-id="0c715-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="0c715-204">tooset hello образец приложения toouse моделирования данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0c715-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="0c715-205">Откройте hello `config.h` файла в hello `app` папки.</span><span class="sxs-lookup"><span data-stu-id="0c715-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="0c715-206">Найдите следующие строки кода hello и измените значение hello из `false` слишком`true`:</span><span class="sxs-lookup"><span data-stu-id="0c715-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Настройка приложения toouse имитируемые hello примеров данных](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="0c715-208">Сохраните файл hello с `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="0c715-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="0c715-209">Развертывание hello образец приложения tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="0c715-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="0c715-210">В hello Arduino IDE, щелкните **средство** > **порт**и выберите для ESP8266 HUZZAH Растушевка hello последовательного порта.</span><span class="sxs-lookup"><span data-stu-id="0c715-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="0c715-211">Нажмите кнопку **схематической** > **отправить** toobuild и развертывание hello образец приложения tooFeather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0c715-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="0c715-212">Ввод учетных данных</span><span class="sxs-lookup"><span data-stu-id="0c715-212">Enter your credentials</span></span>

<span data-ttu-id="0c715-213">После успешного завершения передачи hello, выполните эти шаги tooenter учетные данные.</span><span class="sxs-lookup"><span data-stu-id="0c715-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="0c715-214">В hello Arduino IDE, щелкните **средства** > **последовательного монитор**.</span><span class="sxs-lookup"><span data-stu-id="0c715-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="0c715-215">В окне монитора последовательного hello Обратите внимание, hello два раскрывающихся списков в правом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="0c715-216">Выберите **без завершения строк** для hello левом раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="0c715-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="0c715-217">Выберите **115200 бод** для hello правого раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="0c715-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="0c715-218">В hello входной расположенный вверху hello hello последовательного «монитор» введите следующую информацию в ответ на запрос tooprovide hello их, а затем нажмите кнопку **отправки**.</span><span class="sxs-lookup"><span data-stu-id="0c715-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="0c715-219">Идентификатор SSID для подключения Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="0c715-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="0c715-220">Пароль Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="0c715-220">Wi-Fi password</span></span>
   * <span data-ttu-id="0c715-221">Строка подключения к устройству.</span><span class="sxs-lookup"><span data-stu-id="0c715-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="0c715-222">Hello учетные данные хранятся в hello EEPROM из Растушевка HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="0c715-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="0c715-223">Если вы нажмете кнопку Сброс hello hello Растушевка HUZZAH ESP8266 платы, пример приложения hello запросом tooerase hello сведения.</span><span class="sxs-lookup"><span data-stu-id="0c715-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="0c715-224">Введите `Y` toohave hello сведения удалены.</span><span class="sxs-lookup"><span data-stu-id="0c715-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="0c715-225">Будет предложено сведения hello tooprovide еще раз.</span><span class="sxs-lookup"><span data-stu-id="0c715-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="0c715-226">Убедитесь, что успешно выполняется пример приложения hello</span><span class="sxs-lookup"><span data-stu-id="0c715-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="0c715-227">Если вы видите hello следующие выходные данные из окна последовательной монитор hello и hello мигающий Индикатор на ESP8266 HUZZAH Растушевка, пример приложения hello выполняется успешно.</span><span class="sxs-lookup"><span data-stu-id="0c715-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Окончательные выходные данные в интегрированной среде разработки Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="0c715-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0c715-229">Next steps</span></span>

<span data-ttu-id="0c715-230">Успешно подключен концентратор IoT tooyour ESP8266 HUZZAH Растушевка и отправляются центра IoT tooyour данных датчика захвачен hello.</span><span class="sxs-lookup"><span data-stu-id="0c715-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

