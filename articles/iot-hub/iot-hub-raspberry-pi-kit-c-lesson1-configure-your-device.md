---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 1. Настройка устройства | Документация Майкрософт"
description: "Настройте устройство Raspberry Pi 3 для первого использования и установите бесплатную ОС Raspbian, которая оптимизирована для оборудования Raspberry Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "установить raspbian, скачать raspbian, как установить raspbian, настройка raspbian, установка raspbian на raspberry pi, установка ОС на raspberry pi, установка sd-карты raspberry pi, подключение raspberry pi, подключиться к raspberry pi, подключения raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="557c4-104">Настройка устройства</span><span class="sxs-lookup"><span data-stu-id="557c4-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="557c4-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="557c4-105">What you will do</span></span>
<span data-ttu-id="557c4-106">Настройка устройства Pi для первого использования и установка операционной системы Raspbian.</span><span class="sxs-lookup"><span data-stu-id="557c4-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="557c4-107">Raspbian — это бесплатная операционная система, которая оптимизирована для оборудования Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="557c4-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="557c4-108">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="557c4-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="557c4-109">Новые знания</span><span class="sxs-lookup"><span data-stu-id="557c4-109">What you will learn</span></span>
<span data-ttu-id="557c4-110">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="557c4-110">In this article, you will learn:</span></span>

* <span data-ttu-id="557c4-111">Как установить ОС Raspbian на устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="557c4-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="557c4-112">Как подключить питание к устройству Pi с помощью USB-кабеля.</span><span class="sxs-lookup"><span data-stu-id="557c4-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="557c4-113">Как подключить устройство Pi к сети с помощью кабеля Ethernet или беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="557c4-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="557c4-114">Как добавить на монтажную плату светодиодный индикатор и подключить его к устройству Pi.</span><span class="sxs-lookup"><span data-stu-id="557c4-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="557c4-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="557c4-115">What you need</span></span>
<span data-ttu-id="557c4-116">Чтобы выполнить эту операцию, вам понадобятся следующие элементы из начального набора Raspberry Pi 3:</span><span class="sxs-lookup"><span data-stu-id="557c4-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="557c4-117">плата Raspberry Pi 3;</span><span class="sxs-lookup"><span data-stu-id="557c4-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="557c4-118">карта microSD на 16 ГБ;</span><span class="sxs-lookup"><span data-stu-id="557c4-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="557c4-119">источник питания 5 В 2 A с кабелем Micro USB длиной примерно 1,8 метра;</span><span class="sxs-lookup"><span data-stu-id="557c4-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="557c4-120">монтажная плата;</span><span class="sxs-lookup"><span data-stu-id="557c4-120">The breadboard</span></span>
* <span data-ttu-id="557c4-121">соединительные провода;</span><span class="sxs-lookup"><span data-stu-id="557c4-121">Connector wires</span></span>
* <span data-ttu-id="557c4-122">резистор 560 Ом;</span><span class="sxs-lookup"><span data-stu-id="557c4-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="557c4-123">светодиодный индикатор 10 мм с рассеянным освещением;</span><span class="sxs-lookup"><span data-stu-id="557c4-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="557c4-124">кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="557c4-124">The Ethernet cable</span></span>

![Предметы в начальном наборе](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="557c4-126">Кроме того, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="557c4-126">You also need:</span></span>

* <span data-ttu-id="557c4-127">Проводное или беспроводное подключение к устройству Pi.</span><span class="sxs-lookup"><span data-stu-id="557c4-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="557c4-128">Адаптер USB-SD или карта miniSD для записи образа ОС на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="557c4-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="557c4-129">Компьютер под управлением Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="557c4-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="557c4-130">С помощью компьютера ОС Raspbian устанавливается на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="557c4-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="557c4-131">Подключение к Интернету для скачивания необходимых инструментов и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="557c4-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="557c4-132">Установка ОС Raspbian на карту microSD</span><span class="sxs-lookup"><span data-stu-id="557c4-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="557c4-133">Подготовьте карту microSD для установки образа ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="557c4-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="557c4-134">Скачайте ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="557c4-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="557c4-135">[Скачайте](https://www.raspberrypi.org/downloads/raspbian/) ZIP-файл с Raspbian Jessie with PIXEL.</span><span class="sxs-lookup"><span data-stu-id="557c4-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="557c4-136">Извлеките образ ОС Raspbian в папку на компьютере.</span><span class="sxs-lookup"><span data-stu-id="557c4-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="557c4-137">Установите ОС Raspbian на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="557c4-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="557c4-138">[Скачайте](https://www.etcher.io) и установите служебную программу Etcher для записи карт SD.</span><span class="sxs-lookup"><span data-stu-id="557c4-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="557c4-139">Запустите Etcher и выберите образ Raspbian, извлеченный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="557c4-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="557c4-140">Выберите устройство для чтения карт microSD.</span><span class="sxs-lookup"><span data-stu-id="557c4-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="557c4-141">Обратите внимание, что в программе Etcher уже может быть выбрано правильное устройство для чтения.</span><span class="sxs-lookup"><span data-stu-id="557c4-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="557c4-142">Щелкните **Flash** (Переключиться), чтобы установить ОС Raspbian на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="557c4-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="557c4-143">По завершении установки удалите карту microSD из компьютера.</span><span class="sxs-lookup"><span data-stu-id="557c4-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="557c4-144">Удалять карту microSD напрямую безопасно, так как программа Etcher автоматически извлекает или отключает карту microSD после завершения.</span><span class="sxs-lookup"><span data-stu-id="557c4-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="557c4-145">Вставьте карту microSD в устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="557c4-145">Insert the microSD card into your Pi.</span></span>

![Вставка карты SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="557c4-147">Включение устройства Pi</span><span class="sxs-lookup"><span data-stu-id="557c4-147">Turn on Pi</span></span>
<span data-ttu-id="557c4-148">Включите устройство Pi, используя кабель Micro USB и источник питания.</span><span class="sxs-lookup"><span data-stu-id="557c4-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Включение](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="557c4-150">Важно использовать источник питания из набора с силой тока не менее 2 А, чтобы на устройство Raspberry подавалась энергия, которой достаточно для правильной работы.</span><span class="sxs-lookup"><span data-stu-id="557c4-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="557c4-151">Включение SSH</span><span class="sxs-lookup"><span data-stu-id="557c4-151">Enable SSH</span></span>
<span data-ttu-id="557c4-152">В выпуске за ноябрь 2016 г. в настройках ОС Raspbian сервер SSH по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="557c4-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="557c4-153">Его необходимо включить вручную.</span><span class="sxs-lookup"><span data-stu-id="557c4-153">You need to enable it manually.</span></span> <span data-ttu-id="557c4-154">Вы можете ознакомиться с [официальными инструкциями](https://www.raspberrypi.org/documentation/remote-access/ssh/) или подключить монитор и перейти в меню **Preferences -> Raspberry Pi Configuration** (Настройки -> Конфигурация Raspberry Pi), чтобы включить SSH.</span><span class="sxs-lookup"><span data-stu-id="557c4-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="557c4-155">Подключение устройства Raspberry Pi 3 к сети</span><span class="sxs-lookup"><span data-stu-id="557c4-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="557c4-156">Устройство Pi можно подключить к проводной или беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="557c4-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="557c4-157">Убедитесь, что плата Pi подключена к той же сети, что и компьютер.</span><span class="sxs-lookup"><span data-stu-id="557c4-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="557c4-158">Например, можно подключить плату Pi к тому же коммутатору, к которому подключен компьютер.</span><span class="sxs-lookup"><span data-stu-id="557c4-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="557c4-159">Подключение к проводной сети</span><span class="sxs-lookup"><span data-stu-id="557c4-159">Connect to a wired network</span></span>
<span data-ttu-id="557c4-160">Подключите устройство Pi к проводной сети с помощью кабеля Ethernet.</span><span class="sxs-lookup"><span data-stu-id="557c4-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="557c4-161">Если соединение установлено, то на устройстве Pi загорятся два светодиодных индикатора.</span><span class="sxs-lookup"><span data-stu-id="557c4-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Подключение с помощью кабеля Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="557c4-163">Подключение к беспроводной сети</span><span class="sxs-lookup"><span data-stu-id="557c4-163">Connect to a wireless network</span></span>
<span data-ttu-id="557c4-164">Следуйте [инструкциям](https://www.raspberrypi.org/learning/software-guide/wifi/) от Raspberry Pi Foundation для подключения устройства Pi к беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="557c4-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="557c4-165">Для выполнения этих инструкций необходимо сначала подключить к устройству Pi монитор и клавиатуру.</span><span class="sxs-lookup"><span data-stu-id="557c4-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="557c4-166">Подключение светодиодного индикатора к устройству Pi</span><span class="sxs-lookup"><span data-stu-id="557c4-166">Connect the LED to Pi</span></span>
<span data-ttu-id="557c4-167">Для этого используйте [монтажную плату](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), соединительные провода, светодиодный индикатор и резистор.</span><span class="sxs-lookup"><span data-stu-id="557c4-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="557c4-168">Их необходимо подключить к портам [ввода-вывода общего назначения](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) устройства Pi.</span><span class="sxs-lookup"><span data-stu-id="557c4-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Монтажная плата, светодиодный индикатор и резистор](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="557c4-170">Подключите более короткую ножку индикатора к **GPIO GND (штырь 6)**.</span><span class="sxs-lookup"><span data-stu-id="557c4-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="557c4-171">Подключите более длинную ножку индикатора к резистору.</span><span class="sxs-lookup"><span data-stu-id="557c4-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="557c4-172">Подключите другую ножку резистора к **GPIO 4 (штырь 7)**.</span><span class="sxs-lookup"><span data-stu-id="557c4-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="557c4-173">Обратите внимание, что полярность индикатора приоритетнее.</span><span class="sxs-lookup"><span data-stu-id="557c4-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="557c4-174">Этот параметр полярности известен как "Активный низкий".</span><span class="sxs-lookup"><span data-stu-id="557c4-174">This polarity setting is commonly known as Active Low.</span></span>

![Подключение выводов](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="557c4-176">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="557c4-176">Congratulations!</span></span> <span data-ttu-id="557c4-177">Вы успешно настроили устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="557c4-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="557c4-178">Сводка</span><span class="sxs-lookup"><span data-stu-id="557c4-178">Summary</span></span>
<span data-ttu-id="557c4-179">В этой статье вы узнали, как настроить устройство Pi, установив ОС Raspbian, подключив устройство к сети, а также подключив светодиодный индикатор к устройству.</span><span class="sxs-lookup"><span data-stu-id="557c4-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="557c4-180">Обратите внимание, что светодиодный индикатор еще не светится.</span><span class="sxs-lookup"><span data-stu-id="557c4-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="557c4-181">Следующая задача — установить необходимые инструменты и программное обеспечение в рамках подготовки к запуску примера приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="557c4-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Оборудование готово](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="557c4-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="557c4-183">Next steps</span></span>
[<span data-ttu-id="557c4-184">Получение инструментов</span><span class="sxs-lookup"><span data-stu-id="557c4-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

