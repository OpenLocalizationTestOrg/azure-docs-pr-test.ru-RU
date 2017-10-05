---
title: "Подключение Raspberry Pi (Node) к Интернету вещей Azure. Урок 1. Настройка устройства | Документация Майкрософт"
description: Configure Raspberry Pi 3 for first-time use and install the Raspbian OS, a free operating system that is optimized for the Raspberry Pi hardware.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "установить raspbian, скачать raspbian, как установить raspbian, настройка raspbian, установка raspbian на raspberry pi, установка ОС на raspberry pi, установка sd-карты raspberry pi, подключение raspberry pi, подключиться к raspberry pi, подключения raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b848c48157a2310f0eb1d6398f8b9aaa4395d47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="6ef31-104">Настройка устройства</span><span class="sxs-lookup"><span data-stu-id="6ef31-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="6ef31-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="6ef31-105">What you will do</span></span>
<span data-ttu-id="6ef31-106">Настройка устройства Pi для первого использования и установка операционной системы Raspbian.</span><span class="sxs-lookup"><span data-stu-id="6ef31-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="6ef31-107">Raspbian — это бесплатная операционная система, которая оптимизирована для оборудования Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6ef31-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="6ef31-108">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6ef31-108">If you have any problems, you can seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6ef31-109">Новые знания</span><span class="sxs-lookup"><span data-stu-id="6ef31-109">What you will learn</span></span>
<span data-ttu-id="6ef31-110">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="6ef31-110">In this article, you will learn:</span></span>

* <span data-ttu-id="6ef31-111">Как установить ОС Raspbian на устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="6ef31-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="6ef31-112">Как подключить питание к устройству Pi с помощью USB-кабеля.</span><span class="sxs-lookup"><span data-stu-id="6ef31-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="6ef31-113">Как подключить устройство Pi к сети с помощью кабеля Ethernet или беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="6ef31-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="6ef31-114">Как добавить на монтажную плату светодиодный индикатор и подключить его к устройству Pi.</span><span class="sxs-lookup"><span data-stu-id="6ef31-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="6ef31-115">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="6ef31-115">What you will need</span></span>
<span data-ttu-id="6ef31-116">Чтобы выполнить эту операцию, вам понадобятся следующие элементы из начального набора Raspberry Pi 3:</span><span class="sxs-lookup"><span data-stu-id="6ef31-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="6ef31-117">плата Raspberry Pi 3;</span><span class="sxs-lookup"><span data-stu-id="6ef31-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="6ef31-118">карта microSD на 16 ГБ;</span><span class="sxs-lookup"><span data-stu-id="6ef31-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="6ef31-119">источник питания 5 В 2 A с кабелем Micro USB длиной примерно 1,8 метра;</span><span class="sxs-lookup"><span data-stu-id="6ef31-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="6ef31-120">монтажная плата;</span><span class="sxs-lookup"><span data-stu-id="6ef31-120">The breadboard</span></span>
* <span data-ttu-id="6ef31-121">соединительные провода;</span><span class="sxs-lookup"><span data-stu-id="6ef31-121">Connector wires</span></span>
* <span data-ttu-id="6ef31-122">резистор 560 Ом;</span><span class="sxs-lookup"><span data-stu-id="6ef31-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="6ef31-123">светодиодный индикатор 10 мм с рассеянным освещением;</span><span class="sxs-lookup"><span data-stu-id="6ef31-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="6ef31-124">кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="6ef31-124">The Ethernet cable</span></span>

![Предметы в начальном наборе](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="6ef31-126">Кроме того, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="6ef31-126">You also need:</span></span>

* <span data-ttu-id="6ef31-127">Проводное или беспроводное подключение к устройству Pi.</span><span class="sxs-lookup"><span data-stu-id="6ef31-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="6ef31-128">Адаптер USB-SD или карта miniSD для записи образа операционной системы на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="6ef31-128">A USB-SD adapter or miniSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="6ef31-129">Компьютер под управлением Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="6ef31-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="6ef31-130">С помощью компьютера ОС Raspbian устанавливается на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="6ef31-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="6ef31-131">Подключение к Интернету для скачивания необходимых инструментов и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="6ef31-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="6ef31-132">Установка ОС Raspbian на карту microSD</span><span class="sxs-lookup"><span data-stu-id="6ef31-132">Install Raspbian on the microSD card</span></span>
<span data-ttu-id="6ef31-133">Подготовьте карту microSD для установки образа ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="6ef31-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="6ef31-134">Скачайте ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="6ef31-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="6ef31-135">[Скачайте](https://www.raspberrypi.org/downloads/raspbian/) ZIP-файл с Raspbian Jessie with PIXEL.</span><span class="sxs-lookup"><span data-stu-id="6ef31-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="6ef31-136">Извлеките образ ОС Raspbian в папку на компьютере.</span><span class="sxs-lookup"><span data-stu-id="6ef31-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="6ef31-137">Установите ОС Raspbian на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="6ef31-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="6ef31-138">[Скачайте](https://www.etcher.io) и установите служебную программу Etcher для записи карт SD.</span><span class="sxs-lookup"><span data-stu-id="6ef31-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="6ef31-139">Запустите Etcher и выберите образ Raspbian, извлеченный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="6ef31-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="6ef31-140">Выберите устройство для чтения карт microSD.</span><span class="sxs-lookup"><span data-stu-id="6ef31-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="6ef31-141">Обратите внимание, что в программе Etcher уже может быть выбрано правильное устройство для чтения.</span><span class="sxs-lookup"><span data-stu-id="6ef31-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="6ef31-142">Щелкните **Flash** (Переключиться), чтобы установить ОС Raspbian на карту microSD.</span><span class="sxs-lookup"><span data-stu-id="6ef31-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="6ef31-143">По завершении установки удалите карту microSD из компьютера.</span><span class="sxs-lookup"><span data-stu-id="6ef31-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="6ef31-144">Удалять карту microSD напрямую безопасно, так как программа Etcher автоматически извлекает или отключает карту microSD после завершения.</span><span class="sxs-lookup"><span data-stu-id="6ef31-144">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="6ef31-145">Вставьте карту microSD в устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="6ef31-145">Insert the microSD card into Pi.</span></span>

![Вставка карты SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="6ef31-147">Включение устройства Pi</span><span class="sxs-lookup"><span data-stu-id="6ef31-147">Turn on Pi</span></span>
<span data-ttu-id="6ef31-148">Включите устройство Pi, используя кабель Micro USB и источник питания.</span><span class="sxs-lookup"><span data-stu-id="6ef31-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Включение](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="6ef31-150">Важно использовать источник питания из набора с силой тока не менее 2 А, чтобы на устройство Raspberry подавалась энергия, которой достаточно для правильной работы.</span><span class="sxs-lookup"><span data-stu-id="6ef31-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="6ef31-151">Включение SSH</span><span class="sxs-lookup"><span data-stu-id="6ef31-151">Enable SSH</span></span>
<span data-ttu-id="6ef31-152">В выпуске за ноябрь 2016 г. в настройках ОС Raspbian сервер SSH по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="6ef31-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="6ef31-153">Его необходимо включить вручную.</span><span class="sxs-lookup"><span data-stu-id="6ef31-153">You need to enable it manually.</span></span> <span data-ttu-id="6ef31-154">Вы можете ознакомиться с [официальными инструкциями](https://www.raspberrypi.org/documentation/remote-access/ssh/) или подключить монитор и перейти в меню **Preferences -> Raspberry Pi Configuration** (Настройки -> Конфигурация Raspberry Pi), чтобы включить SSH.</span><span class="sxs-lookup"><span data-stu-id="6ef31-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="6ef31-155">Подключение устройства Raspberry Pi 3 к сети</span><span class="sxs-lookup"><span data-stu-id="6ef31-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="6ef31-156">Устройство Pi можно подключить к проводной или беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="6ef31-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="6ef31-157">Убедитесь, что плата Pi подключена к той же сети, что и компьютер.</span><span class="sxs-lookup"><span data-stu-id="6ef31-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="6ef31-158">Например, можно подключить плату Pi к тому же коммутатору, к которому подключен компьютер.</span><span class="sxs-lookup"><span data-stu-id="6ef31-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="6ef31-159">Подключение к проводной сети</span><span class="sxs-lookup"><span data-stu-id="6ef31-159">Connect to a wired network</span></span>
<span data-ttu-id="6ef31-160">Подключите устройство Pi к проводной сети с помощью кабеля Ethernet.</span><span class="sxs-lookup"><span data-stu-id="6ef31-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="6ef31-161">Если соединение установлено, то на устройстве Pi загорятся два светодиодных индикатора.</span><span class="sxs-lookup"><span data-stu-id="6ef31-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Подключение с помощью кабеля Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="6ef31-163">Подключение к беспроводной сети</span><span class="sxs-lookup"><span data-stu-id="6ef31-163">Connect to a wireless network</span></span>
<span data-ttu-id="6ef31-164">Следуйте [инструкциям](https://www.raspberrypi.org/learning/software-guide/wifi/) от Raspberry Pi Foundation для подключения устройства Pi к беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="6ef31-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="6ef31-165">Для выполнения этих инструкций необходимо сначала подключить к устройству Pi монитор и клавиатуру.</span><span class="sxs-lookup"><span data-stu-id="6ef31-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="6ef31-166">Подключение светодиодного индикатора к устройству Pi</span><span class="sxs-lookup"><span data-stu-id="6ef31-166">Connect the LED to Pi</span></span>
<span data-ttu-id="6ef31-167">Для этого используйте [монтажную плату](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), соединительные провода, светодиодный индикатор и резистор.</span><span class="sxs-lookup"><span data-stu-id="6ef31-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="6ef31-168">Их необходимо подключить к портам [ввода-вывода общего назначения](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) устройства Pi.</span><span class="sxs-lookup"><span data-stu-id="6ef31-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Монтажная плата, светодиодный индикатор и резистор](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="6ef31-170">Подключите более короткую ножку индикатора к **GPIO GND (штырь 6)**.</span><span class="sxs-lookup"><span data-stu-id="6ef31-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="6ef31-171">Подключите более длинную ножку индикатора к резистору.</span><span class="sxs-lookup"><span data-stu-id="6ef31-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="6ef31-172">Подключите другую ножку резистора к **GPIO 4 (штырь 7)**.</span><span class="sxs-lookup"><span data-stu-id="6ef31-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="6ef31-173">Обратите внимание, что полярность индикатора приоритетнее.</span><span class="sxs-lookup"><span data-stu-id="6ef31-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="6ef31-174">Этот параметр полярности известен как "Активный низкий".</span><span class="sxs-lookup"><span data-stu-id="6ef31-174">This polarity setting is commonly known as Active Low.</span></span>

![Подключение выводов](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="6ef31-176">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="6ef31-176">Congratulations!</span></span> <span data-ttu-id="6ef31-177">Вы успешно настроили устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="6ef31-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="6ef31-178">Сводка</span><span class="sxs-lookup"><span data-stu-id="6ef31-178">Summary</span></span>
<span data-ttu-id="6ef31-179">В этой статье вы узнали, как настроить устройство Pi, установив ОС Raspbian, подключив устройство к сети, а также подключив светодиодный индикатор к устройству.</span><span class="sxs-lookup"><span data-stu-id="6ef31-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="6ef31-180">Обратите внимание, что светодиодный индикатор еще не светится.</span><span class="sxs-lookup"><span data-stu-id="6ef31-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="6ef31-181">Следующая задача — установить необходимые инструменты и программное обеспечение в рамках подготовки к запуску примера приложения на устройстве Pi.</span><span class="sxs-lookup"><span data-stu-id="6ef31-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Оборудование готово](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="6ef31-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ef31-183">Next steps</span></span>
[<span data-ttu-id="6ef31-184">Получение инструментов</span><span class="sxs-lookup"><span data-stu-id="6ef31-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

