---
title: "Подключение Feather HUZZAH ESP8266 к Центру Интернета вещей Azure в облаке | Документация Майкрософт"
description: "Узнайте, как настроить и подключить плату Adafruit Feather HUZZAH ESP8266 к Центру Интернета вещей Azure и передавать с нее данные в облако Azure."
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
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="657b8-103">Подключение Adafruit Feather HUZZAH ESP8266 к Центру Интернета вещей Azure в облаке</span><span class="sxs-lookup"><span data-stu-id="657b8-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Подключение между DHT22, Feather HUZZAH ESP8266 и Центром Интернета вещей](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="657b8-105">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="657b8-105">What you do</span></span>


<span data-ttu-id="657b8-106">В рамках этого руководства мы подключим плату Adafruit Feather HUZZAH ESP8266 к созданному Центру Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="657b8-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="657b8-107">Затем мы запустим пример приложения на ESP8266, чтобы собрать данные о температуре и влажности, зафиксированные датчиком DHT22.</span><span class="sxs-lookup"><span data-stu-id="657b8-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="657b8-108">После этого отправим данные с датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="657b8-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="657b8-109">При использовании других плат ESP8266 вы по-прежнему можете выполнить эти действия, чтобы подключиться к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="657b8-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="657b8-110">В зависимости от используемой платы ESP8266 вам может потребоваться изменить параметр `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="657b8-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="657b8-111">Например, если вы используете ESP8266 от AI-Thinker, вы можете изменить его значение с `0` на `2`.</span><span class="sxs-lookup"><span data-stu-id="657b8-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="657b8-112">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="657b8-112">Don't have a kit yet?</span></span> <span data-ttu-id="657b8-113">Получите его на [веб-сайте Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="657b8-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="657b8-114">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="657b8-114">What you learn</span></span>

* <span data-ttu-id="657b8-115">Как создать Центр Интернета вещей и зарегистрировать устройство для Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="657b8-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="657b8-116">Как подключить Feather HUZZAH ESP8266 к датчику и компьютеру.</span><span class="sxs-lookup"><span data-stu-id="657b8-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="657b8-117">Как собирать данные датчиков, запустив пример приложения на Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="657b8-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="657b8-118">Как отправить данные датчиков в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="657b8-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="657b8-119">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="657b8-119">What you need</span></span>

![Элементы, необходимые в рамках руководства:](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="657b8-121">Чтобы выполнить эту операцию, вам понадобятся следующие элементы из начального набора Feather HUZZAH ESP8266:</span><span class="sxs-lookup"><span data-stu-id="657b8-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="657b8-122">плата Feather HUZZAH ESP8266;</span><span class="sxs-lookup"><span data-stu-id="657b8-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="657b8-123">кабель micro-USB (тип A).</span><span class="sxs-lookup"><span data-stu-id="657b8-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="657b8-124">Кроме того, вам понадобятся следующие элементы среды разработки:</span><span class="sxs-lookup"><span data-stu-id="657b8-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="657b8-125">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="657b8-125">An active Azure subscription.</span></span> <span data-ttu-id="657b8-126">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="657b8-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="657b8-127">ПК или компьютер Mac под управлением Windows или Ubuntu;</span><span class="sxs-lookup"><span data-stu-id="657b8-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="657b8-128">беспроводная сеть, к которой подключается Feather HUZZAH ESP8266;</span><span class="sxs-lookup"><span data-stu-id="657b8-128">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="657b8-129">подключение к Интернету для скачивания средства настройки;</span><span class="sxs-lookup"><span data-stu-id="657b8-129">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="657b8-130">[Arduino IDE](https://www.arduino.cc/en/main/software) версии 1.6.8 или более новой.</span><span class="sxs-lookup"><span data-stu-id="657b8-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="657b8-131">Более ранние версии несовместимы с библиотекой Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="657b8-131">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="657b8-132">Ниже приведены необязательные элементы, используемые в случае отсутствия датчика.</span><span class="sxs-lookup"><span data-stu-id="657b8-132">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="657b8-133">Вы также можете использовать симулированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="657b8-133">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="657b8-134">Датчик температуры и влажности Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="657b8-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="657b8-135">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="657b8-135">A breadboard</span></span>
* <span data-ttu-id="657b8-136">Многомодовый оптоволоконный кабель с разъемами на обоих концах.</span><span class="sxs-lookup"><span data-stu-id="657b8-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="657b8-137">Подключение Feather HUZZAH ESP8266 к датчику и компьютеру</span><span class="sxs-lookup"><span data-stu-id="657b8-137">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="657b8-138">В этом разделе рассказывается о том, как подключить датчики к плате.</span><span class="sxs-lookup"><span data-stu-id="657b8-138">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="657b8-139">Затем устройство нужно подключить к компьютеру для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="657b8-139">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="657b8-140">Подключение датчика температуры и влажности DHT22 к Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="657b8-140">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="657b8-141">Чтобы установить подключение, используйте монтажную плату и оптоволоконный кабель с разъемами на обоих концах, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="657b8-141">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="657b8-142">Если у вас нет датчика, пропустите этот раздел, так как вместо него вы можете использовать симулированные данные.</span><span class="sxs-lookup"><span data-stu-id="657b8-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Справочные материалы по подключению](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="657b8-144">Чтобы подключить выводы датчика, используйте следующие кабели:</span><span class="sxs-lookup"><span data-stu-id="657b8-144">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="657b8-145">Начало (датчик)</span><span class="sxs-lookup"><span data-stu-id="657b8-145">Start (Sensor)</span></span>           | <span data-ttu-id="657b8-146">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="657b8-146">End (Board)</span></span>           | <span data-ttu-id="657b8-147">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="657b8-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="657b8-148">VDD (вывод 31F)</span><span class="sxs-lookup"><span data-stu-id="657b8-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="657b8-149">3V (вывод 58H)</span><span class="sxs-lookup"><span data-stu-id="657b8-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="657b8-150">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="657b8-150">Red cable</span></span>     |
| <span data-ttu-id="657b8-151">DATA (вывод 32F)</span><span class="sxs-lookup"><span data-stu-id="657b8-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="657b8-152">GPIO 2 (вывод 46A)</span><span class="sxs-lookup"><span data-stu-id="657b8-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="657b8-153">Синий кабель</span><span class="sxs-lookup"><span data-stu-id="657b8-153">Blue cable</span></span>    |
| <span data-ttu-id="657b8-154">GND (вывод 34F)</span><span class="sxs-lookup"><span data-stu-id="657b8-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="657b8-155">GND (вывод 56I)</span><span class="sxs-lookup"><span data-stu-id="657b8-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="657b8-156">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="657b8-156">Black cable</span></span>   |

<span data-ttu-id="657b8-157">Дополнительные сведения см. в статьях о [подключении к датчику Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) и [выводах Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="657b8-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="657b8-158">Теперь работающий датчик должен быть подключен к Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="657b8-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Подключение DHT22 к Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="657b8-160">Подключение Feather HUZZAH ESP8266 к компьютеру</span><span class="sxs-lookup"><span data-stu-id="657b8-160">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="657b8-161">Чтобы подключить Feather HUZZAH ESP8266 к своему компьютеру, используйте кабель micro-USB типа A, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="657b8-161">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Подключение Feather Huzzah к компьютеру](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="657b8-163">Добавление разрешений для последовательного порта (только в Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="657b8-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="657b8-164">При использовании Ubuntu получите разрешения для работы с USB-портом платы Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="657b8-164">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="657b8-165">Чтобы добавить разрешения для работы с последовательным портом, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="657b8-165">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="657b8-166">В окне терминала выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="657b8-166">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="657b8-167">Вы получите выходные данные одного из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="657b8-167">You get one of the following outputs:</span></span>

   * <span data-ttu-id="657b8-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="657b8-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="657b8-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="657b8-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="657b8-170">В выходных данных обратите внимание на параметр `uucp` или `dialout`. Это имя владельца группы USB-порта.</span><span class="sxs-lookup"><span data-stu-id="657b8-170">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="657b8-171">Добавьте пользователя в группу, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="657b8-171">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="657b8-172">`<group-owner-name>` — это имя владельца группы, полученное на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="657b8-172">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="657b8-173">`<username>` — это имя пользователя Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="657b8-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="657b8-174">Чтобы изменения стали видны, выйдите из Ubuntu и войдите снова.</span><span class="sxs-lookup"><span data-stu-id="657b8-174">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="657b8-175">Сбор данных датчиков и их отправка в Центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="657b8-175">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="657b8-176">В этом разделе вы развернете и запустите пример приложения на плате Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="657b8-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="657b8-177">Пример приложения включает и отключает светодиодный индикатор на плате Feather HUZZAH ESP8266 и отправляет данные о температуре и влажности, собранные с датчика DHT22, в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="657b8-177">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="657b8-178">Получение примера приложения из GitHub</span><span class="sxs-lookup"><span data-stu-id="657b8-178">Get the sample application from GitHub</span></span>

<span data-ttu-id="657b8-179">Пример приложения находится на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="657b8-179">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="657b8-180">Клонируйте репозиторий, содержащий пример приложения с GitHub.</span><span class="sxs-lookup"><span data-stu-id="657b8-180">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="657b8-181">Чтобы клонировать пример репозитория, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="657b8-181">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="657b8-182">Откройте окно командной строки или терминала.</span><span class="sxs-lookup"><span data-stu-id="657b8-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="657b8-183">Перейдите к папке, в которую необходимо сохранить пример приложения.</span><span class="sxs-lookup"><span data-stu-id="657b8-183">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="657b8-184">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="657b8-184">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="657b8-185">Установите пакет для Feather HUZZAH ESP8266 в Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="657b8-185">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="657b8-186">Откройте папку, где хранится пример приложения.</span><span class="sxs-lookup"><span data-stu-id="657b8-186">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="657b8-187">Откройте файл app.ino в папке приложения в Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="657b8-187">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Открытие примера приложения в Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="657b8-189">В Arduino IDE щелкните **Файл** > **Настройки**.</span><span class="sxs-lookup"><span data-stu-id="657b8-189">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="657b8-190">В диалоговом окне **Настройки** щелкните значок рядом с текстовым полем **Additional Boards Manager URLs** (Дополнительные URL-адреса для менеджера плат).</span><span class="sxs-lookup"><span data-stu-id="657b8-190">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="657b8-191">Во всплывающем окне введите приведенный ниже URL-адрес и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="657b8-191">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Указание URL-адреса пакета в Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="657b8-193">В диалоговом окне **Настройки** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="657b8-193">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="657b8-194">Щелкните **Инструменты** > **Платы** > **Менеджер плат**, а затем выполните поиск по esp8266.</span><span class="sxs-lookup"><span data-stu-id="657b8-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="657b8-195">Диспетчер плат показывает, что установлена плата ESP8266 2.2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="657b8-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Завершение установки пакета ESP8266](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="657b8-197">Щелкните **Инструменты** > **Платы** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="657b8-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="657b8-198">Установка необходимых библиотек</span><span class="sxs-lookup"><span data-stu-id="657b8-198">Install necessary libraries</span></span>

1. <span data-ttu-id="657b8-199">В Arduino IDE щелкните **Скетч** > **Подключить библиотеку** > **Управлять библиотеками**.</span><span class="sxs-lookup"><span data-stu-id="657b8-199">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="657b8-200">Выполните поиск приведенных ниже имен библиотек по очереди.</span><span class="sxs-lookup"><span data-stu-id="657b8-200">Search for the following library names one by one.</span></span> <span data-ttu-id="657b8-201">Для каждой найденной библиотеки щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="657b8-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="657b8-202">У вас нет датчика DHT22?</span><span class="sxs-lookup"><span data-stu-id="657b8-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="657b8-203">Если у вас нет датчика DHT22, пример приложения может смоделировать данные о температуре и влажности.</span><span class="sxs-lookup"><span data-stu-id="657b8-203">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="657b8-204">Чтобы настроить пример приложения для использования имитации данных, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="657b8-204">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="657b8-205">Откройте файл `config.h` в папке `app`.</span><span class="sxs-lookup"><span data-stu-id="657b8-205">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="657b8-206">Найдите приведенную ниже строку кода и измените значение `false` на `true`.</span><span class="sxs-lookup"><span data-stu-id="657b8-206">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Настройка примера приложения для использования имитации данных](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="657b8-208">Сохраните файл с помощью клавиш `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="657b8-208">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="657b8-209">Развертывание примера приложения для Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="657b8-209">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="657b8-210">В Arduino IDE щелкните **Инструменты** > **Порт**, а затем выберите последовательный порт для Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="657b8-210">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="657b8-211">Чтобы создать и развернуть пример приложения для Feather HUZZAH ESP8266, щелкните **Скетч** > **Загрузка**.</span><span class="sxs-lookup"><span data-stu-id="657b8-211">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="657b8-212">Ввод учетных данных</span><span class="sxs-lookup"><span data-stu-id="657b8-212">Enter your credentials</span></span>

<span data-ttu-id="657b8-213">После успешного завершения загрузки введите учетные данные следующим образом:</span><span class="sxs-lookup"><span data-stu-id="657b8-213">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="657b8-214">В Arduino IDE щелкните **Инструменты** > **Монитор последовательного порта**.</span><span class="sxs-lookup"><span data-stu-id="657b8-214">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="657b8-215">В окне монитора последовательного порта обратите внимание на два раскрывающихся списка в нижнем правом углу.</span><span class="sxs-lookup"><span data-stu-id="657b8-215">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="657b8-216">В раскрывающемся списке слева выберите **No line ending** (Ничего не добавлять к отправляемой строке).</span><span class="sxs-lookup"><span data-stu-id="657b8-216">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="657b8-217">В раскрывающемся списке справа выберите **115200 baud** (115200 бод).</span><span class="sxs-lookup"><span data-stu-id="657b8-217">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="657b8-218">При появлении запроса в поле ввода, расположенном в верхней части окна монитора последовательного порта, введете приведенные ниже сведения, а затем нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="657b8-218">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="657b8-219">Идентификатор SSID для подключения Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="657b8-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="657b8-220">Пароль Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="657b8-220">Wi-Fi password</span></span>
   * <span data-ttu-id="657b8-221">Строка подключения к устройству.</span><span class="sxs-lookup"><span data-stu-id="657b8-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="657b8-222">Учетные данные хранятся в EEPROM платы Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="657b8-222">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="657b8-223">При нажатии кнопки сброса на плате Feather HUZZAH ESP8266 в примере приложения отобразится сообщение с запросом на удаление информации.</span><span class="sxs-lookup"><span data-stu-id="657b8-223">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="657b8-224">Введите `Y` для удаления данных.</span><span class="sxs-lookup"><span data-stu-id="657b8-224">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="657b8-225">Вам будет предложено предоставить их еще раз.</span><span class="sxs-lookup"><span data-stu-id="657b8-225">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="657b8-226">Проверка работоспособности примера приложения</span><span class="sxs-lookup"><span data-stu-id="657b8-226">Verify the sample application is running successfully</span></span>

<span data-ttu-id="657b8-227">Если в окне монитора последовательного порта отобразились приведенные ниже выходные данные и на плате Feather HUZZAH ESP8266 мигает светодиодный индикатор, значит пример приложения запущен успешно.</span><span class="sxs-lookup"><span data-stu-id="657b8-227">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Конечные выходные данные в Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="657b8-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="657b8-229">Next steps</span></span>

<span data-ttu-id="657b8-230">Вы успешно подключили плату Feather HUZZAH ESP8266 к Центру Интернета вещей и отправили в него собранные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="657b8-230">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

