---
title: "Подключение Sparkfun ESP8266 Thing Dev к Центру Интернета вещей Azure | Документация Майкрософт"
description: "Узнайте, как настроить и подключить плату Sparkfun ESP8266 Thing Dev к Центру Интернета вещей Azure и передавать с нее данные в облако Azure."
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
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="59b23-103">Подключение Sparkfun ESP8266 Thing Dev к Центру Интернета вещей в облаке Azure</span><span class="sxs-lookup"><span data-stu-id="59b23-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Подключение DHT22 и Thing Dev к Центру Интернета вещей](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="59b23-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="59b23-105">What you will do</span></span>

<span data-ttu-id="59b23-106">Подключение Sparkfun ESP8266 Thing Dev к создаваемому Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="59b23-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="59b23-107">Затем запустим пример приложения на ESP8266, чтобы собрать данные о температуре и влажности, зафиксированные датчиком DHT22.</span><span class="sxs-lookup"><span data-stu-id="59b23-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="59b23-108">И наконец, отправим данные датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="59b23-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="59b23-109">При использовании других плат ESP8266 вы по-прежнему можете выполнить эти действия, чтобы подключиться к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="59b23-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="59b23-110">В зависимости от используемой платы ESP8266 вам может потребоваться изменить параметр `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="59b23-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="59b23-111">Например, при использовании ESP8266 от AI-Thinker вы можете изменить его значение с `0` на `2`.</span><span class="sxs-lookup"><span data-stu-id="59b23-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="59b23-112">Нет начального набора? Щелкните [здесь](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="59b23-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="59b23-113">Новые знания</span><span class="sxs-lookup"><span data-stu-id="59b23-113">What you will learn</span></span>

* <span data-ttu-id="59b23-114">Как создать Центр Интернета вещей и зарегистрировать устройство Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="59b23-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="59b23-115">Как подключить Thing Dev к датчику и компьютеру.</span><span class="sxs-lookup"><span data-stu-id="59b23-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="59b23-116">Как собирать данные датчиков, запустив пример приложения на Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="59b23-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="59b23-117">Как отправить данные датчиков в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="59b23-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="59b23-118">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="59b23-118">What you will need</span></span>

![Элементы, необходимые в рамках руководства](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="59b23-120">Чтобы выполнить эту операцию, вам понадобятся следующие элементы из начального набора Thing Dev:</span><span class="sxs-lookup"><span data-stu-id="59b23-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="59b23-121">плата Sparkfun ESP8266 Thing Dev;</span><span class="sxs-lookup"><span data-stu-id="59b23-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="59b23-122">кабель micro-USB (тип A).</span><span class="sxs-lookup"><span data-stu-id="59b23-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="59b23-123">Кроме того, вам понадобятся следующие элементы среды разработки:</span><span class="sxs-lookup"><span data-stu-id="59b23-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="59b23-124">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="59b23-124">An active Azure subscription.</span></span> <span data-ttu-id="59b23-125">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="59b23-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="59b23-126">ПК или компьютер Mac под управлением Windows или Ubuntu;</span><span class="sxs-lookup"><span data-stu-id="59b23-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="59b23-127">Беспроводная сеть, к которой будет подключаться ESP8266 Sparkfun Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="59b23-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="59b23-128">подключение к Интернету для скачивания средства настройки;</span><span class="sxs-lookup"><span data-stu-id="59b23-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="59b23-129">[Arduino IDE](https://www.arduino.cc/en/main/software) версии 1.6.8 или более поздней (более ранние версии несовместимы с библиотекой Центра Интернета вещей Azure).</span><span class="sxs-lookup"><span data-stu-id="59b23-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="59b23-130">Ниже приведены необязательные элементы, используемые в случае отсутствия датчика.</span><span class="sxs-lookup"><span data-stu-id="59b23-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="59b23-131">Вы также можете использовать симулированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="59b23-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="59b23-132">Датчик температуры и влажности Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="59b23-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="59b23-133">Монтажная плата.</span><span class="sxs-lookup"><span data-stu-id="59b23-133">A breadboard.</span></span>
* <span data-ttu-id="59b23-134">Многомодовый оптоволоконный кабель с разъемами на обоих концах.</span><span class="sxs-lookup"><span data-stu-id="59b23-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="59b23-135">Подключение ESP8266 Thing Dev к датчику и компьютеру</span><span class="sxs-lookup"><span data-stu-id="59b23-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="59b23-136">Подключение датчика температуры и влажности DHT22 к ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="59b23-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="59b23-137">Чтобы установить подключение, используйте монтажную плату и оптоволоконный кабель с разъемами на обоих концах, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="59b23-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="59b23-138">Если у вас нет датчика, пропустите этот раздел, так как вместо него вы можете использовать симулированные данные.</span><span class="sxs-lookup"><span data-stu-id="59b23-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Справочные материалы по подключению](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="59b23-140">Чтобы подключить датчик, используйте следующие кабели:</span><span class="sxs-lookup"><span data-stu-id="59b23-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="59b23-141">Начало (датчик)</span><span class="sxs-lookup"><span data-stu-id="59b23-141">Start (Sensor)</span></span>           | <span data-ttu-id="59b23-142">Конец (плата)</span><span class="sxs-lookup"><span data-stu-id="59b23-142">End (Board)</span></span>           | <span data-ttu-id="59b23-143">Цвет кабеля</span><span class="sxs-lookup"><span data-stu-id="59b23-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="59b23-144">VDD (вывод 27F)</span><span class="sxs-lookup"><span data-stu-id="59b23-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="59b23-145">3V (вывод 8A)</span><span class="sxs-lookup"><span data-stu-id="59b23-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="59b23-146">Красный кабель</span><span class="sxs-lookup"><span data-stu-id="59b23-146">Red cable</span></span>     |
| <span data-ttu-id="59b23-147">DATA (вывод 28F)</span><span class="sxs-lookup"><span data-stu-id="59b23-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="59b23-148">GPIO 2 (вывод 9A)</span><span class="sxs-lookup"><span data-stu-id="59b23-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="59b23-149">Белый кабель</span><span class="sxs-lookup"><span data-stu-id="59b23-149">White cable</span></span>    |
| <span data-ttu-id="59b23-150">GND (вывод 30F)</span><span class="sxs-lookup"><span data-stu-id="59b23-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="59b23-151">GND (вывод 7J)</span><span class="sxs-lookup"><span data-stu-id="59b23-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="59b23-152">Черный кабель</span><span class="sxs-lookup"><span data-stu-id="59b23-152">Black cable</span></span>   |


- <span data-ttu-id="59b23-153">Дополнительные сведения см. в [документации по установке датчика DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) и в [спецификации Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="59b23-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="59b23-154">Теперь работающий датчик должен быть подключен к Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="59b23-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![Подключение dht22 к ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="59b23-156">Подключение Sparkfun ESP8266 Thing Dev к компьютеру</span><span class="sxs-lookup"><span data-stu-id="59b23-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="59b23-157">Чтобы подключить Sparkfun ESP8266 Thing Dev к своему компьютеру, используйте кабель Micro-USB — USB типа A, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="59b23-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![Подключение Feather HUZZAH к компьютеру](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="59b23-159">Добавление разрешений для последовательного порта (только в Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="59b23-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="59b23-160">Если вы используете Ubuntu, предоставьте непривилегированному пользователю разрешения для работы с USB-портом, к которому подключена Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="59b23-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="59b23-161">Чтобы добавить разрешения для работы с последовательным портом, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="59b23-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="59b23-162">В окне терминала выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="59b23-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="59b23-163">Вы получите выходные данные одного из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="59b23-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="59b23-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="59b23-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="59b23-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="59b23-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="59b23-166">В выходных данных обратите внимание на параметр `uucp` или `dialout`. Это имя владельца группы USB-порта.</span><span class="sxs-lookup"><span data-stu-id="59b23-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="59b23-167">Добавьте пользователя в группу, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="59b23-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="59b23-168">`<group-owner-name>` — это имя владельца группы, полученное на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="59b23-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="59b23-169">`<username>` — это имя пользователя Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="59b23-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="59b23-170">Чтобы изменения вступили в силу, выйдите из системы Ubuntu и войдите в нее снова.</span><span class="sxs-lookup"><span data-stu-id="59b23-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="59b23-171">Сбор данных датчиков и их отправка в Центр Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="59b23-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="59b23-172">В этом разделе вы развернете и запустите пример приложения на плате Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="59b23-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="59b23-173">Пример приложения включает и отключает светодиодный индикатор на плате Sparkfun ESP8266 Thing Dev, а также отправляет в Центр Интернета вещей данные о температуре и влажности, собранные с датчика DHT22.</span><span class="sxs-lookup"><span data-stu-id="59b23-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="59b23-174">Получение примера приложения из GitHub</span><span class="sxs-lookup"><span data-stu-id="59b23-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="59b23-175">Пример приложения находится на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="59b23-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="59b23-176">Клонируйте репозиторий, содержащий пример приложения с GitHub.</span><span class="sxs-lookup"><span data-stu-id="59b23-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="59b23-177">Чтобы клонировать пример репозитория, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="59b23-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="59b23-178">Откройте окно командной строки или терминала.</span><span class="sxs-lookup"><span data-stu-id="59b23-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="59b23-179">Перейдите к папке, в которую необходимо сохранить пример приложения.</span><span class="sxs-lookup"><span data-stu-id="59b23-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="59b23-180">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="59b23-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="59b23-181">Установите пакет для Sparkfun ESP8266 Thing Dev с помощью Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="59b23-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="59b23-182">Откройте папку, где хранится пример приложения.</span><span class="sxs-lookup"><span data-stu-id="59b23-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="59b23-183">Откройте файл app.ino в папке приложения в Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="59b23-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![Открытие примера приложения в Arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="59b23-185">В Arduino IDE щелкните **Файл** > **Настройки**.</span><span class="sxs-lookup"><span data-stu-id="59b23-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="59b23-186">В диалоговом окне **Настройки** щелкните значок рядом с текстовым полем **Дополнительные ссылки для менеджера плат**.</span><span class="sxs-lookup"><span data-stu-id="59b23-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="59b23-187">Во всплывающем окне введите приведенный ниже URL-адрес и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="59b23-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Указание URL-адреса пакета в Arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="59b23-189">В диалоговом окне **Настройки** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="59b23-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="59b23-190">Щелкните **Инструменты** > **Платы** > **Менеджер плат**, а затем выполните поиск по esp8266.</span><span class="sxs-lookup"><span data-stu-id="59b23-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="59b23-191">Должен быть установлен пакет ESP8266 версии 2.2.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="59b23-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Завершение установки пакета ESP8266](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="59b23-193">Щелкните **Инструменты** > **Платы** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="59b23-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="59b23-194">Установка необходимых библиотек</span><span class="sxs-lookup"><span data-stu-id="59b23-194">Install necessary libraries</span></span>

1. <span data-ttu-id="59b23-195">В Arduino IDE щелкните **Скетч** > **Подключить библиотеку** > **Управлять библиотеками**.</span><span class="sxs-lookup"><span data-stu-id="59b23-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="59b23-196">Выполните поиск приведенных ниже имен библиотек по очереди.</span><span class="sxs-lookup"><span data-stu-id="59b23-196">Search for the following library names one by one.</span></span> <span data-ttu-id="59b23-197">Для каждой найденной библиотеки нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="59b23-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="59b23-198">У вас нет датчика DHT22?</span><span class="sxs-lookup"><span data-stu-id="59b23-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="59b23-199">Если у вас нет датчика DHT22, пример приложения может смоделировать данные о температуре и влажности.</span><span class="sxs-lookup"><span data-stu-id="59b23-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="59b23-200">Чтобы включить использование смоделированных данных в примере приложения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="59b23-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="59b23-201">Откройте файл `config.h` в папке `app`.</span><span class="sxs-lookup"><span data-stu-id="59b23-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="59b23-202">Найдите приведенную ниже строку кода и измените значение `false` на `true`.</span><span class="sxs-lookup"><span data-stu-id="59b23-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Настройка использования смоделированных данных в примере приложения](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="59b23-204">Сохраните изменения с помощью `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="59b23-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="59b23-205">Развертывание примера приложения на Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="59b23-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="59b23-206">В Arduino IDE щелкните **Tool** > **Port** (Средства > Порт), а затем выберите последовательный порт для Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="59b23-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="59b23-207">Чтобы создать и развернуть пример приложения на Sparkfun ESP8266 Thing Dev, щелкните **Sketch** > **Upload** (Скетч > Загрузка).</span><span class="sxs-lookup"><span data-stu-id="59b23-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="59b23-208">Если вы используете macOS, то во время передачи данных могут отображаться следующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="59b23-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="59b23-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="59b23-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="59b23-210">Откройте окно терминала выполните приведенные ниже действия, чтобы устранить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="59b23-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="59b23-211">Ввод учетных данных</span><span class="sxs-lookup"><span data-stu-id="59b23-211">Enter your credentials</span></span>

<span data-ttu-id="59b23-212">После завершения загрузки введите учетные данные следующим образом:</span><span class="sxs-lookup"><span data-stu-id="59b23-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="59b23-213">В Arduino IDE щелкните **Инструменты** > **Монитор последовательного порта**.</span><span class="sxs-lookup"><span data-stu-id="59b23-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="59b23-214">В окне монитора последовательного порта обратите внимание на два раскрывающихся списка в нижнем правом углу.</span><span class="sxs-lookup"><span data-stu-id="59b23-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="59b23-215">В раскрывающемся списке слева выберите **No line ending** (Ничего не добавлять к отправляемой строке).</span><span class="sxs-lookup"><span data-stu-id="59b23-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="59b23-216">В раскрывающемся списке справа выберите **115200 baud** (115200 бод).</span><span class="sxs-lookup"><span data-stu-id="59b23-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="59b23-217">При появлении запроса в поле ввода, расположенном в верхней части окна монитора последовательного порта, введете приведенные ниже сведения, а затем нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="59b23-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="59b23-218">Идентификатор SSID для подключения Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="59b23-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="59b23-219">Пароль Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="59b23-219">Wi-Fi password</span></span>
   * <span data-ttu-id="59b23-220">Строка подключения к устройству.</span><span class="sxs-lookup"><span data-stu-id="59b23-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="59b23-221">Учетные данные хранятся в памяти EEPROM платы Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="59b23-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="59b23-222">Если вы нажмете кнопку сброса на плате Sparkfun ESP8266 Thing Dev, в примере приложения отобразится сообщение с запросом на удаление информации.</span><span class="sxs-lookup"><span data-stu-id="59b23-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="59b23-223">Чтобы удалить информацию, нажмите клавишу `Y`. После этого отобразится запрос на повторный ввод данных.</span><span class="sxs-lookup"><span data-stu-id="59b23-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="59b23-224">Проверка работоспособности примера приложения</span><span class="sxs-lookup"><span data-stu-id="59b23-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="59b23-225">Если в окне монитора последовательного порта отобразились приведенные ниже выходные данные, а на плате Sparkfun ESP8266 Thing Dev мигает светодиодный индикатор, значит пример приложения запущен успешно.</span><span class="sxs-lookup"><span data-stu-id="59b23-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![Окончательные выходные данные в Arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="59b23-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59b23-227">Next steps</span></span>

<span data-ttu-id="59b23-228">Вы успешно подключили плату Sparkfun ESP8266 Thing Dev к Центру Интернета вещей и отправили данные, полученные от датчика.</span><span class="sxs-lookup"><span data-stu-id="59b23-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
