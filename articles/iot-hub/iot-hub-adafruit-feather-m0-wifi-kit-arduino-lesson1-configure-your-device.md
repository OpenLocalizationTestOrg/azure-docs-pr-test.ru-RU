---
title: "Connect Arduino (C) tooAzure IoT — занятия 1: Настройка устройства | Документы Microsoft"
description: "Настройте Adafruit Feather M0 WiFi для первого использования."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino настройки подключения arduino toopc, arduino установки, плата arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="eb4c9-104">Настройка устройства</span><span class="sxs-lookup"><span data-stu-id="eb4c9-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="eb4c9-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="eb4c9-105">What you will do</span></span>
<span data-ttu-id="eb4c9-106">Настройте доске Adafruit Растушевка M0 Wi-Fi Arduino для первого использования путем сборки hello доски, его включение питания.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="eb4c9-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="eb4c9-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eb4c9-108">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="eb4c9-108">What you need</span></span>
<span data-ttu-id="eb4c9-109">toocomplete этой операции требуется hello следующие элементы для начального набора Adafruit Растушевка M0 Wi-Fi:</span><span class="sxs-lookup"><span data-stu-id="eb4c9-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="eb4c9-110">плата Wi-Fi M0 Растушевка Adafruit Hello</span><span class="sxs-lookup"><span data-stu-id="eb4c9-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="eb4c9-111">Micro B tooType USB-кабель</span><span class="sxs-lookup"><span data-stu-id="eb4c9-111">A Micro B tooType A USB cable</span></span>

![набор][kit]

<span data-ttu-id="eb4c9-113">Кроме того, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="eb4c9-113">You also need:</span></span>

* <span data-ttu-id="eb4c9-114">Компьютер под управлением Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="eb4c9-115">Беспроводное подключение для вашей tooconnect платы Arduino для.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="eb4c9-116">Подключение toodownload конфигурации инструментальных средств Интернета.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eb4c9-117">Новые знания</span><span class="sxs-lookup"><span data-stu-id="eb4c9-117">What you will learn</span></span>
<span data-ttu-id="eb4c9-118">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="eb4c9-118">In this article, you will learn:</span></span>

* <span data-ttu-id="eb4c9-119">Как tooassemble Arduino платы и power ее для hello следующие уроки.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="eb4c9-120">Каким образом разрешения tooadd последовательного порта для Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="eb4c9-121">Подключите компьютер tooyour Arduino платы</span><span class="sxs-lookup"><span data-stu-id="eb4c9-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="eb4c9-122">Подключите кабель USB micro hello hello top micro USB-порту.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Верхний порт micro-USB][top-micro-usb-port]

2. <span data-ttu-id="eb4c9-124">Другой конец USB-кабель Здравствуйте, подключаемых к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-124">Plug hello other end of USB cable into your computer.</span></span>

   ![Подключение USB к компьютеру][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="eb4c9-126">Добавление разрешений для последовательного порта в Ubuntu</span><span class="sxs-lookup"><span data-stu-id="eb4c9-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="eb4c9-127">Этот раздел можно пропустить, если вы используете Windows или macOS.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="eb4c9-128">Для Ubuntu требуются следующие шаги toomake hello linux обычный пользователь должен toooperate hello разрешения на USB-порту hello системной платы Arduino для hello.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="eb4c9-129">Для обычного пользователя из терминала</span><span class="sxs-lookup"><span data-stu-id="eb4c9-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="eb4c9-130">отобразится примерно такой текст:</span><span class="sxs-lookup"><span data-stu-id="eb4c9-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="eb4c9-131">Hello «0» может быть другой номер, или может быть возвращено несколько записей.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="eb4c9-132">В данных вариантов hello первый hello, нам нужно будет `uucp`, в hello второй — `dialout`, который является владельцем группы hello hello файла.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="eb4c9-133">Добавьте группу toohello toohello пользователей:</span><span class="sxs-lookup"><span data-stu-id="eb4c9-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="eb4c9-134">Где `group-name` — hello данных из первого шага hello и `username` — имя пользователя linux.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="eb4c9-135">Необходимо будет toolog извлечение и возврат снова для этой tootake эффект изменений и hello завершения установки.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="eb4c9-136">Сводка</span><span class="sxs-lookup"><span data-stu-id="eb4c9-136">Summary</span></span>
<span data-ttu-id="eb4c9-137">В этой статье вы узнали, как tooconfigure Arduino доске.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="eb4c9-138">Следующая задача Hello-tooinstall hello необходимых средств и программного обеспечения в подготовке к запуску примера приложения в Arduino на доске.</span><span class="sxs-lookup"><span data-stu-id="eb4c9-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Оборудование готово][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="eb4c9-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb4c9-140">Next steps</span></span>
<span data-ttu-id="eb4c9-141">[Получить средства hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="eb4c9-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md