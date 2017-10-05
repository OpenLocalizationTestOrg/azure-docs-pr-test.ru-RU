---
title: "Подключение Intel Edison (Node) к Интернету вещей Azure. Урок 1. Настройка устройства | Документация Майкрософт"
description: "Настройка Intel Edison для первого использования."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Arduino, настройка, подключение Arduino к компьютеру, настройка Arduino, плата Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 87bf3a917af096e43a43a2143afa4bf43a72d7fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="dccf4-104">Настройка Intel Edison</span><span class="sxs-lookup"><span data-stu-id="dccf4-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="dccf4-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="dccf4-105">What you will do</span></span>
<span data-ttu-id="dccf4-106">Настройте Intel Edison для первого использования: соберите плату, подключите ее и установите на компьютере инструмент для настройки, с помощью которого установите встроенное ПО Intel Edison, настроите пароль и подключите устройство к Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="dccf4-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="dccf4-107">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="dccf4-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="dccf4-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="dccf4-108">What you will learn</span></span>
<span data-ttu-id="dccf4-109">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="dccf4-109">In this article, you will learn:</span></span>

* <span data-ttu-id="dccf4-110">как собрать и включить плату Edison;</span><span class="sxs-lookup"><span data-stu-id="dccf4-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="dccf4-111">как прошить встроенное ПО Edison, установить пароль и подключиться к Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="dccf4-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="dccf4-112">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="dccf4-112">What you need</span></span>
<span data-ttu-id="dccf4-113">Чтобы выполнить эту операцию, вам понадобятся следующие элементы из начального набора Intel Edison:</span><span class="sxs-lookup"><span data-stu-id="dccf4-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="dccf4-114">модуль Intel® Edison;</span><span class="sxs-lookup"><span data-stu-id="dccf4-114">Intel® Edison module</span></span>
* <span data-ttu-id="dccf4-115">плата расширения Arduino;</span><span class="sxs-lookup"><span data-stu-id="dccf4-115">Arduino expansion board</span></span>
* <span data-ttu-id="dccf4-116">все прокладки и винты, которые входят в комплект поставки, включая два винта для крепления модуля к плате расширения и четыре набора винтов с пластиковыми опорами;</span><span class="sxs-lookup"><span data-stu-id="dccf4-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="dccf4-117">кабель micro-USB (тип B-A);</span><span class="sxs-lookup"><span data-stu-id="dccf4-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="dccf4-118">источник питания постоянного тока (DC).</span><span class="sxs-lookup"><span data-stu-id="dccf4-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="dccf4-119">Источник питания должен иметь такие параметры:</span><span class="sxs-lookup"><span data-stu-id="dccf4-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="dccf4-120">напряжение постоянного тока 7–15 В;</span><span class="sxs-lookup"><span data-stu-id="dccf4-120">7-15V DC</span></span>
  - <span data-ttu-id="dccf4-121">мощность не менее 1500 мА;</span><span class="sxs-lookup"><span data-stu-id="dccf4-121">At least 1500mA</span></span>
  - <span data-ttu-id="dccf4-122">центральная клемма положительной полярности.</span><span class="sxs-lookup"><span data-stu-id="dccf4-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Предметы в начальном наборе](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="dccf4-124">Кроме того, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="dccf4-124">You also need:</span></span>

* <span data-ttu-id="dccf4-125">Компьютер под управлением Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="dccf4-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="dccf4-126">Беспроводное подключение, к которому будет подключаться Edison.</span><span class="sxs-lookup"><span data-stu-id="dccf4-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="dccf4-127">Подключение к Интернету для скачивания инструмента настройки.</span><span class="sxs-lookup"><span data-stu-id="dccf4-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="dccf4-128">Сборка платы</span><span class="sxs-lookup"><span data-stu-id="dccf4-128">Assemble your board</span></span>

<span data-ttu-id="dccf4-129">Этот раздел описывает процедуру подключения модуля Intel® Edison к плате расширения.</span><span class="sxs-lookup"><span data-stu-id="dccf4-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="dccf4-130">Поместите модуль Intel® Edison в белый контур на плате расширения, совместив отверстия в модуле с винтами на плате расширения.</span><span class="sxs-lookup"><span data-stu-id="dccf4-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="dccf4-131">Нажмите на модуль в точке под словами `What will you make?`, опустив его вниз до щелчка.</span><span class="sxs-lookup"><span data-stu-id="dccf4-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![Сборка платы 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="dccf4-133">Используйте две шестигранные гайки (входят в комплект) для крепления модуля к плате расширения.</span><span class="sxs-lookup"><span data-stu-id="dccf4-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![Сборка платы 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="dccf4-135">Вставьте винт в одно из четырех угловых отверстий на плате расширения.</span><span class="sxs-lookup"><span data-stu-id="dccf4-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="dccf4-136">Наденьте на винт и плотно затяните белую пластмассовую опору.</span><span class="sxs-lookup"><span data-stu-id="dccf4-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![Сборка платы 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="dccf4-138">Повторите этот шаг для других угловых опор.</span><span class="sxs-lookup"><span data-stu-id="dccf4-138">Repeat for the other three corner spacers.</span></span>

   ![Сборка платы 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="dccf4-140">Сборка платы завершена.</span><span class="sxs-lookup"><span data-stu-id="dccf4-140">Now your board is assembled.</span></span>

   ![Собранная плата](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="dccf4-142">Подключение питания Edison</span><span class="sxs-lookup"><span data-stu-id="dccf4-142">Power up Edison</span></span>

1. <span data-ttu-id="dccf4-143">Подключите источник питания.</span><span class="sxs-lookup"><span data-stu-id="dccf4-143">Plug in the power supply.</span></span>

   ![Подключение источника питания](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="dccf4-145">Должен загореться зеленый светодиод (на плате расширения Arduino* он обозначен как DS1).</span><span class="sxs-lookup"><span data-stu-id="dccf4-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="dccf4-146">Подождите минуту, пока завершится загрузка системной платы.</span><span class="sxs-lookup"><span data-stu-id="dccf4-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dccf4-147">Если у вас нет источника питания постоянного тока, вы можете подать на плату питание через порт USB.</span><span class="sxs-lookup"><span data-stu-id="dccf4-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="dccf4-148">Дополнительные сведения см. в разделе `Connect Edison to your computer`.</span><span class="sxs-lookup"><span data-stu-id="dccf4-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="dccf4-149">Такой способ подачи питания может привести к непредсказуемому поведению системной платы, особенно при использовании Wi-Fi или двигателей.</span><span class="sxs-lookup"><span data-stu-id="dccf4-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="dccf4-150">Подключение Edison к компьютеру</span><span class="sxs-lookup"><span data-stu-id="dccf4-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="dccf4-151">Переведите микропереключатель вниз, в сторону двух портов micro-USB, чтобы перевести Edison в режим устройства.</span><span class="sxs-lookup"><span data-stu-id="dccf4-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="dccf4-152">Различия между режимами устройства и узла описаны [здесь](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="dccf4-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Переключение микропереключателя вниз](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="dccf4-154">Подключите кабель micro-USB к верхнему порту micro-USB.</span><span class="sxs-lookup"><span data-stu-id="dccf4-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Верхний порт micro-USB](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="dccf4-156">Другой конец кабеля USB подключите к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="dccf4-156">Plug the other end of USB cable into your computer.</span></span>

   ![Подключение USB к компьютеру](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="dccf4-158">Вы можете быть уверены, что инициализация платы завершилась, когда компьютер присоединит новый диск (примерно так же, как при подключении SD-карты).</span><span class="sxs-lookup"><span data-stu-id="dccf4-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="dccf4-159">Скачивание и запуск инструмента настройки</span><span class="sxs-lookup"><span data-stu-id="dccf4-159">Download and run the configuration tool</span></span>
<span data-ttu-id="dccf4-160">Скачайте последнюю версию инструмента настройки, выбрав нужный вариант в разделе `Installers` на [этой странице](https://software.intel.com/en-us/iot/hardware/edison/downloads).</span><span class="sxs-lookup"><span data-stu-id="dccf4-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="dccf4-161">Запустите инструмент и выполните инструкции, которые будут отображаться на экране. Нажимайте кнопку "Далее" по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="dccf4-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="dccf4-162">Встроенное ПО</span><span class="sxs-lookup"><span data-stu-id="dccf4-162">Flash firmware</span></span>
1. <span data-ttu-id="dccf4-163">На странице `Set up options` нажмите кнопку `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="dccf4-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="dccf4-164">Выберите образ, который нужно установить на плату:</span><span class="sxs-lookup"><span data-stu-id="dccf4-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="dccf4-165">чтобы скачать и установить последнюю версию встроенного ПО, предлагаемого Intel для вашей платы, выберите `Download the latest image version xxxx`;</span><span class="sxs-lookup"><span data-stu-id="dccf4-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="dccf4-166">чтобы установить образ, который вы ранее сохранили на своем компьютере, выберите `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="dccf4-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="dccf4-167">Найдите и выберите образ для установки на плату.</span><span class="sxs-lookup"><span data-stu-id="dccf4-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="dccf4-168">Инструмент настройки попытается установить ПО на плату.</span><span class="sxs-lookup"><span data-stu-id="dccf4-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="dccf4-169">Этот процесс может занять до 10 минут.</span><span class="sxs-lookup"><span data-stu-id="dccf4-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="dccf4-170">Установка пароля</span><span class="sxs-lookup"><span data-stu-id="dccf4-170">Set password</span></span>
1. <span data-ttu-id="dccf4-171">На странице `Set up options` нажмите кнопку `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="dccf4-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="dccf4-172">Для платы Intel® Edison вы можете задать пользовательское имя.</span><span class="sxs-lookup"><span data-stu-id="dccf4-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="dccf4-173">Это необязательно.</span><span class="sxs-lookup"><span data-stu-id="dccf4-173">This is optional.</span></span>
3. <span data-ttu-id="dccf4-174">Введите пароль для вашей платы, а затем щелкните `Set password`.</span><span class="sxs-lookup"><span data-stu-id="dccf4-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="dccf4-175">Запишите пароль, он вам пригодится позднее.</span><span class="sxs-lookup"><span data-stu-id="dccf4-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="dccf4-176">Подключение Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="dccf4-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="dccf4-177">На странице `Set up options` нажмите кнопку `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="dccf4-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="dccf4-178">Подождите примерно одну минуту, пока компьютер найдет доступные сети Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="dccf4-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="dccf4-179">В раскрывающемся списке `Detected Networks` выберите нужную сеть.</span><span class="sxs-lookup"><span data-stu-id="dccf4-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="dccf4-180">В раскрывающемся списке `Security` выберите режим безопасности для этой сети.</span><span class="sxs-lookup"><span data-stu-id="dccf4-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="dccf4-181">Укажите имя и пароль для входа, затем нажмите `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="dccf4-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="dccf4-182">Запишите полученный IP-адрес, он вам пригодится позже.</span><span class="sxs-lookup"><span data-stu-id="dccf4-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="dccf4-183">Убедитесь, что плата Edison подключена к той же сети, что и компьютер.</span><span class="sxs-lookup"><span data-stu-id="dccf4-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="dccf4-184">Компьютер подключается к плате Edison по IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="dccf4-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="dccf4-185">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="dccf4-185">Congratulations!</span></span> <span data-ttu-id="dccf4-186">Вы успешно настроили устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="dccf4-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="dccf4-187">Сводка</span><span class="sxs-lookup"><span data-stu-id="dccf4-187">Summary</span></span>
<span data-ttu-id="dccf4-188">Из этой статьи вы узнали, как собрать плату Edison, как установить встроенное ПО, задать пароль и подключить устройство к Wi-Fi с помощью инструмента настройки.</span><span class="sxs-lookup"><span data-stu-id="dccf4-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="dccf4-189">Обратите внимание, что светодиодный индикатор еще не светится.</span><span class="sxs-lookup"><span data-stu-id="dccf4-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="dccf4-190">Следующая задача — установить необходимые инструменты и программное обеспечение, которые потребуются для запуска примера приложения на устройстве Edison.</span><span class="sxs-lookup"><span data-stu-id="dccf4-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dccf4-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dccf4-191">Next steps</span></span>
<span data-ttu-id="dccf4-192">[Get the tools][get-the-tools] (Получение инструментов)</span><span class="sxs-lookup"><span data-stu-id="dccf4-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md