---
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 1: Настройка устройства | Документы Microsoft"
description: "Настройте Raspberry Pi 3 для первого использования и установите hello Raspbian ОС, свободного операционной системы, оптимизированный для hello Raspberry Pi оборудования."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Установка raspbian, загрузки raspbian tooinstall raspbian raspbian установки малиновая pi установки raspbian, малиновая pi установки операционной системы, малиновая pi sd карты установки малиновая pi подключиться, подключения tooraspberry pi, малиновая pi подключения"
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
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="92a8f-104">Настройка устройства</span><span class="sxs-lookup"><span data-stu-id="92a8f-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="92a8f-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="92a8f-105">What you will do</span></span>
<span data-ttu-id="92a8f-106">Настройте Pi для первого использования и установите hello Raspbian операционной системы.</span><span class="sxs-lookup"><span data-stu-id="92a8f-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="92a8f-107">Raspbian является бесплатной операционной системы, оптимизированный для hello Raspberry Pi оборудования.</span><span class="sxs-lookup"><span data-stu-id="92a8f-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="92a8f-108">Если у вас возникнут проблемы, может выполнять поиск решений на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="92a8f-108">If you have any problems, you can seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="92a8f-109">Новые знания</span><span class="sxs-lookup"><span data-stu-id="92a8f-109">What you will learn</span></span>
<span data-ttu-id="92a8f-110">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="92a8f-110">In this article, you will learn:</span></span>

* <span data-ttu-id="92a8f-111">Как tooinstall Raspbian на Pi.</span><span class="sxs-lookup"><span data-stu-id="92a8f-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="92a8f-112">Как toopower копирование пи с помощью USB-кабеля.</span><span class="sxs-lookup"><span data-stu-id="92a8f-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="92a8f-113">Как tooconnect Pi toohello сети с помощью кабеля Ethernet или беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="92a8f-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="92a8f-114">Как breadboard tooadd toohello Индикатор и подключите его tooPi.</span><span class="sxs-lookup"><span data-stu-id="92a8f-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="92a8f-115">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="92a8f-115">What you will need</span></span>
<span data-ttu-id="92a8f-116">toocomplete этой операции требуется hello следующую частей из начального набора Raspberry Pi 3:</span><span class="sxs-lookup"><span data-stu-id="92a8f-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="92a8f-117">Hello плата Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="92a8f-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="92a8f-118">карта microSD 16 ГБ Hello</span><span class="sxs-lookup"><span data-stu-id="92a8f-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="92a8f-119">Hello 5В 2 amp питания с hello 6 фут micro USB-кабель</span><span class="sxs-lookup"><span data-stu-id="92a8f-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="92a8f-120">Hello breadboard</span><span class="sxs-lookup"><span data-stu-id="92a8f-120">hello breadboard</span></span>
* <span data-ttu-id="92a8f-121">соединительные провода;</span><span class="sxs-lookup"><span data-stu-id="92a8f-121">Connector wires</span></span>
* <span data-ttu-id="92a8f-122">резистор 560 Ом;</span><span class="sxs-lookup"><span data-stu-id="92a8f-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="92a8f-123">светодиодный индикатор 10 мм с рассеянным освещением;</span><span class="sxs-lookup"><span data-stu-id="92a8f-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="92a8f-124">Hello кабель Ethernet</span><span class="sxs-lookup"><span data-stu-id="92a8f-124">hello Ethernet cable</span></span>

![Предметы в начальном наборе](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="92a8f-126">Кроме того, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="92a8f-126">You also need:</span></span>

* <span data-ttu-id="92a8f-127">Для tooconnect Pi для проводного или беспроводного подключения.</span><span class="sxs-lookup"><span data-stu-id="92a8f-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="92a8f-128">USB-SD адаптер или miniSD карты tooburn hello образа операционной системы на карту microSD, hello.</span><span class="sxs-lookup"><span data-stu-id="92a8f-128">A USB-SD adapter or miniSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="92a8f-129">Компьютер под управлением Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="92a8f-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="92a8f-130">Hello компьютер будет использоваться tooinstall Raspbian на карте microSD hello.</span><span class="sxs-lookup"><span data-stu-id="92a8f-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="92a8f-131">Toodownload подключения Internet hello необходимых средств и программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="92a8f-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="92a8f-132">Установка Raspbian на карте microSD hello</span><span class="sxs-lookup"><span data-stu-id="92a8f-132">Install Raspbian on hello microSD card</span></span>
<span data-ttu-id="92a8f-133">Подготовьте карта microSD hello для установки образа Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="92a8f-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="92a8f-134">Скачайте ОС Raspbian.</span><span class="sxs-lookup"><span data-stu-id="92a8f-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="92a8f-135">[Загрузить](https://www.raspberrypi.org/downloads/raspbian/) hello ZIP-файл для детском Raspbian с точки.</span><span class="sxs-lookup"><span data-stu-id="92a8f-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="92a8f-136">Извлеките hello Raspbian изображения tooa папку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="92a8f-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="92a8f-137">Установите карту microSD toohello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="92a8f-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="92a8f-138">[Загрузить](https://www.etcher.io) и установить программу записи карты SD гравировальная hello.</span><span class="sxs-lookup"><span data-stu-id="92a8f-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="92a8f-139">Запустите гравировальная и выберите изображение Raspbian hello, извлеченный на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="92a8f-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="92a8f-140">Выберите диск, карту microSD hello.</span><span class="sxs-lookup"><span data-stu-id="92a8f-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="92a8f-141">Обратите внимание, что гравировальная может уже выбран правильный диск hello.</span><span class="sxs-lookup"><span data-stu-id="92a8f-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="92a8f-142">Нажмите кнопку **Flash** tooinstall Raspbian toohello microSD карты.</span><span class="sxs-lookup"><span data-stu-id="92a8f-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="92a8f-143">Удаление карта microSD hello с компьютера после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="92a8f-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="92a8f-144">Это карта microSD безопасные tooremove hello непосредственно из-за гравировальная автоматически извлечение или отключение карта microSD hello после завершения.</span><span class="sxs-lookup"><span data-stu-id="92a8f-144">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="92a8f-145">Вставьте карту microSD hello в Pi.</span><span class="sxs-lookup"><span data-stu-id="92a8f-145">Insert hello microSD card into Pi.</span></span>

![Вставьте карту SD hello](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="92a8f-147">Включение устройства Pi</span><span class="sxs-lookup"><span data-stu-id="92a8f-147">Turn on Pi</span></span>
<span data-ttu-id="92a8f-148">Включите Pi при помощи micro USB-кабель hello и hello питания.</span><span class="sxs-lookup"><span data-stu-id="92a8f-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Включение](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="92a8f-150">Это важные toouse hello источник питания в комплекте hello, по крайней мере toomake 2A убедиться, что ваш Raspberry имеет недостаточно питания toowork правильно.</span><span class="sxs-lookup"><span data-stu-id="92a8f-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="92a8f-151">Включение SSH</span><span class="sxs-lookup"><span data-stu-id="92a8f-151">Enable SSH</span></span>
<span data-ttu-id="92a8f-152">Начиная с hello ноября 2016 г. Raspbian предоставляет hello сервера SSH, по умолчанию отключены.</span><span class="sxs-lookup"><span data-stu-id="92a8f-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="92a8f-153">Требуется tooenable его вручную.</span><span class="sxs-lookup"><span data-stu-id="92a8f-153">You need tooenable it manually.</span></span> <span data-ttu-id="92a8f-154">Можно ссылаться toohello [официальный инструкции](https://www.raspberrypi.org/documentation/remote-access/ssh/) или подключите мониторы и перейти слишком**настройки -> Конфигурация Pi Raspberry** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="92a8f-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="92a8f-155">Подключение к сети toohello Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="92a8f-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="92a8f-156">Вы можете подключиться к проводной или беспроводной сети tooa tooa Pi.</span><span class="sxs-lookup"><span data-stu-id="92a8f-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="92a8f-157">Убедитесь, что Pi подключенных toohello сетевых как на компьютере.</span><span class="sxs-lookup"><span data-stu-id="92a8f-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="92a8f-158">Например можно подключиться Pi toohello же переключиться, что компьютер подключен к.</span><span class="sxs-lookup"><span data-stu-id="92a8f-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="92a8f-159">Подключение tooa проводной сети</span><span class="sxs-lookup"><span data-stu-id="92a8f-159">Connect tooa wired network</span></span>
<span data-ttu-id="92a8f-160">Используйте tooconnect кабель Ethernet hello tooyour Pi проводной сети.</span><span class="sxs-lookup"><span data-stu-id="92a8f-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="92a8f-161">Hello два индикатора на Pi включить, если соединения hello.</span><span class="sxs-lookup"><span data-stu-id="92a8f-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Подключение с помощью кабеля Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="92a8f-163">Подключение к беспроводной сети tooa</span><span class="sxs-lookup"><span data-stu-id="92a8f-163">Connect tooa wireless network</span></span>
<span data-ttu-id="92a8f-164">Выполните hello [инструкции](https://www.raspberrypi.org/learning/software-guide/wifi/) hello Raspberry Pi Foundation tooconnect Pi tooyour беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="92a8f-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="92a8f-165">Эти инструкции требуют toofirst подключения монитора и tooPi клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="92a8f-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="92a8f-166">Подключение tooPi hello Индикатора</span><span class="sxs-lookup"><span data-stu-id="92a8f-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="92a8f-167">toocomplete этой задачи, используйте hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello проводов соединителя, hello Индикатор и hello резистор.</span><span class="sxs-lookup"><span data-stu-id="92a8f-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="92a8f-168">Подключите их toohello [общего назначения ввода вывода](https://www.raspberrypi.org/documentation/usage/gpio/) порты Pi (объект групповой ПОЛИТИКИ).</span><span class="sxs-lookup"><span data-stu-id="92a8f-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Монтажная плата, светодиодный индикатор и резистор](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="92a8f-170">Подключения слишком короткий участок hello hello Индикатор**Земля объект групповой ПОЛИТИКИ (6 ПИН-код)**.</span><span class="sxs-lookup"><span data-stu-id="92a8f-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="92a8f-171">Подключите hello дольше участок hello Индикатор участок tooone резистор hello.</span><span class="sxs-lookup"><span data-stu-id="92a8f-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="92a8f-172">Подключение слишком hello других участок hello резистор**4 объект групповой ПОЛИТИКИ (7 ПИН-код)**.</span><span class="sxs-lookup"><span data-stu-id="92a8f-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="92a8f-173">Обратите внимание, что полярности hello Индикатор важные.</span><span class="sxs-lookup"><span data-stu-id="92a8f-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="92a8f-174">Этот параметр полярности известен как "Активный низкий".</span><span class="sxs-lookup"><span data-stu-id="92a8f-174">This polarity setting is commonly known as Active Low.</span></span>

![Подключение выводов](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="92a8f-176">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="92a8f-176">Congratulations!</span></span> <span data-ttu-id="92a8f-177">Вы успешно настроили устройство Pi.</span><span class="sxs-lookup"><span data-stu-id="92a8f-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="92a8f-178">Сводка</span><span class="sxs-lookup"><span data-stu-id="92a8f-178">Summary</span></span>
<span data-ttu-id="92a8f-179">В этой статье вы узнали, как tooconfigure Pi, установив Raspbian подключении Pi tooa сети и подключение tooPi Индикатора.</span><span class="sxs-lookup"><span data-stu-id="92a8f-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="92a8f-180">Обратите внимание, что Индикатор еще не подсвечивается приветствия.</span><span class="sxs-lookup"><span data-stu-id="92a8f-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="92a8f-181">Следующая задача Hello-tooinstall hello необходимых средств и программного обеспечения в подготовке к запуску примера приложения на Pi.</span><span class="sxs-lookup"><span data-stu-id="92a8f-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Оборудование готово](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="92a8f-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="92a8f-183">Next steps</span></span>
[<span data-ttu-id="92a8f-184">Получить средства hello</span><span class="sxs-lookup"><span data-stu-id="92a8f-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

