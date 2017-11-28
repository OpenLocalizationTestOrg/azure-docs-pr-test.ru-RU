---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 1: Настройка устройства | Документы Microsoft"
description: "Настройка Intel Edison для первого использования."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino настройки подключения arduino toopc, arduino установки, плата arduino"
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
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="eb51d-104">Настройка Intel Edison</span><span class="sxs-lookup"><span data-stu-id="eb51d-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="eb51d-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="eb51d-105">What you will do</span></span>
<span data-ttu-id="eb51d-106">Настройте Intel Edison для первого использования путем сборки hello доски, его включение питания и установка конфигурации средства tooyour настольных ОС tooflash встроенного по Edison, задать пароль и подключите его tooWi-Fi.</span><span class="sxs-lookup"><span data-stu-id="eb51d-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="eb51d-107">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="eb51d-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eb51d-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="eb51d-108">What you will learn</span></span>
<span data-ttu-id="eb51d-109">В этой статье вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="eb51d-109">In this article, you will learn:</span></span>

* <span data-ttu-id="eb51d-110">Как плата tooassemble Edison и включите его.</span><span class="sxs-lookup"><span data-stu-id="eb51d-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="eb51d-111">Как tooflash Edison встроенного по, задать пароль и подключения Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="eb51d-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eb51d-112">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="eb51d-112">What you need</span></span>
<span data-ttu-id="eb51d-113">toocomplete этой операции требуется hello следующую частей из начального набора Edison Intel:</span><span class="sxs-lookup"><span data-stu-id="eb51d-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="eb51d-114">модуль Intel® Edison;</span><span class="sxs-lookup"><span data-stu-id="eb51d-114">Intel® Edison module</span></span>
* <span data-ttu-id="eb51d-115">плата расширения Arduino;</span><span class="sxs-lookup"><span data-stu-id="eb51d-115">Arduino expansion board</span></span>
* <span data-ttu-id="eb51d-116">Разделитель строки или винты, включенных в пакетов hello, включая два винты toofasten hello модуля toohello плата расширения и четыре набора винты и пластиковая разделителей.</span><span class="sxs-lookup"><span data-stu-id="eb51d-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="eb51d-117">Micro B tooType USB-кабель</span><span class="sxs-lookup"><span data-stu-id="eb51d-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="eb51d-118">источник питания постоянного тока (DC).</span><span class="sxs-lookup"><span data-stu-id="eb51d-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="eb51d-119">Источник питания должен иметь такие параметры:</span><span class="sxs-lookup"><span data-stu-id="eb51d-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="eb51d-120">напряжение постоянного тока 7–15 В;</span><span class="sxs-lookup"><span data-stu-id="eb51d-120">7-15V DC</span></span>
  - <span data-ttu-id="eb51d-121">мощность не менее 1500 мА;</span><span class="sxs-lookup"><span data-stu-id="eb51d-121">At least 1500mA</span></span>
  - <span data-ttu-id="eb51d-122">Hello center или внутренний ПИН-код должен быть полюса положительный результат hello hello источника питания</span><span class="sxs-lookup"><span data-stu-id="eb51d-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![Предметы в начальном наборе](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="eb51d-124">Кроме того, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="eb51d-124">You also need:</span></span>

* <span data-ttu-id="eb51d-125">Компьютер под управлением Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="eb51d-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="eb51d-126">Беспроводное подключение для tooconnect Edison для.</span><span class="sxs-lookup"><span data-stu-id="eb51d-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="eb51d-127">Подключение toodownload конфигурации инструментальных средств Интернета.</span><span class="sxs-lookup"><span data-stu-id="eb51d-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="eb51d-128">Сборка платы</span><span class="sxs-lookup"><span data-stu-id="eb51d-128">Assemble your board</span></span>

<span data-ttu-id="eb51d-129">Этот раздел содержит действия tooattach доске Intel® Edison tooyour модуля расширения.</span><span class="sxs-lookup"><span data-stu-id="eb51d-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="eb51d-130">Поместите модуль Intel® Edison hello внутри структуры hello белого на доске расширения, выравнивается отверстия hello hello модуля с винты hello платы расширения hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="eb51d-131">Нажмите и удерживайте на модуль hello сразу после слова hello `What will you make?` до привязки.</span><span class="sxs-lookup"><span data-stu-id="eb51d-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![Сборка платы 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="eb51d-133">Используйте toohello плата расширения toosecure hello hello два шестнадцатеричных основы (включен в пакет hello) модуля.</span><span class="sxs-lookup"><span data-stu-id="eb51d-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![Сборка платы 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="eb51d-135">Вставьте винт одним hello четыре угла отверстия на доске расширения hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="eb51d-136">Скручивание и усилить одним из разделителей пластиковая hello белого на винт hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![Сборка платы 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="eb51d-138">Повторите эти действия для hello других разделителей трех углов.</span><span class="sxs-lookup"><span data-stu-id="eb51d-138">Repeat for hello other three corner spacers.</span></span>

   ![Сборка платы 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="eb51d-140">Сборка платы завершена.</span><span class="sxs-lookup"><span data-stu-id="eb51d-140">Now your board is assembled.</span></span>

   ![Собранная плата](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="eb51d-142">Подключение питания Edison</span><span class="sxs-lookup"><span data-stu-id="eb51d-142">Power up Edison</span></span>

1. <span data-ttu-id="eb51d-143">Подключите питание hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-143">Plug in hello power supply.</span></span>

   ![Подключение источника питания](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="eb51d-145">Зеленый Индикатор (с меткой DS1 hello плата расширения Arduino *) необходимо включить и оставаться включенными.</span><span class="sxs-lookup"><span data-stu-id="eb51d-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="eb51d-146">Подождите одну минуту, для загрузки toofinish плата hello.</span><span class="sxs-lookup"><span data-stu-id="eb51d-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="eb51d-147">Если у вас питания постоянного ТОКА, вы можете платы hello питания через USB-порт.</span><span class="sxs-lookup"><span data-stu-id="eb51d-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="eb51d-148">Дополнительные сведения см. в разделе `Connect Edison tooyour computer`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="eb51d-149">Такой способ подачи питания может привести к непредсказуемому поведению системной платы, особенно при использовании Wi-Fi или двигателей.</span><span class="sxs-lookup"><span data-stu-id="eb51d-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="eb51d-150">Подключите компьютер tooyour Edison</span><span class="sxs-lookup"><span data-stu-id="eb51d-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="eb51d-151">Переключение вниз микропереключателя hello сторону hello два micro USB-портов, так, чтобы Edison режим устройства.</span><span class="sxs-lookup"><span data-stu-id="eb51d-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="eb51d-152">Различия между режимами устройства и узла описаны [здесь](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="eb51d-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Переключение вниз микропереключателя hello](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="eb51d-154">Подключите кабель USB micro hello hello top micro USB-порту.</span><span class="sxs-lookup"><span data-stu-id="eb51d-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Верхний порт micro-USB](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="eb51d-156">Другой конец USB-кабель Здравствуйте, подключаемых к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="eb51d-156">Plug hello other end of USB cable into your computer.</span></span>

   ![Подключение USB к компьютеру](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="eb51d-158">Вы можете быть уверены, что инициализация платы завершилась, когда компьютер присоединит новый диск (примерно так же, как при подключении SD-карты).</span><span class="sxs-lookup"><span data-stu-id="eb51d-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="eb51d-159">Загрузите и запустите средство настройки hello</span><span class="sxs-lookup"><span data-stu-id="eb51d-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="eb51d-160">Получить последние средство настройки hello из [эту ссылку](https://software.intel.com/en-us/iot/hardware/edison/downloads) списке hello `Installers` заголовок.</span><span class="sxs-lookup"><span data-stu-id="eb51d-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="eb51d-161">Выполнение средства hello и выполните его на экране инструкции, нажав кнопку Далее, при необходимости</span><span class="sxs-lookup"><span data-stu-id="eb51d-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="eb51d-162">Встроенное ПО</span><span class="sxs-lookup"><span data-stu-id="eb51d-162">Flash firmware</span></span>
1. <span data-ttu-id="eb51d-163">На hello `Set up options` щелкните `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="eb51d-164">Выберите tooflash hello изображения на доске, выполнив одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="eb51d-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="eb51d-165">Выберите toodownload и flash вашей системной платы с hello последнюю образ встроенного ПО Intel, доступные `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="eb51d-166">tooflash вашей системной платы с изображением, уже сохранен на компьютере, выберите `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="eb51d-167">Обзор tooand выберите hello изображения должны tooflash tooyour платы.</span><span class="sxs-lookup"><span data-stu-id="eb51d-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="eb51d-168">средство установки Hello попытается tooflash доске.</span><span class="sxs-lookup"><span data-stu-id="eb51d-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="eb51d-169">весь процесс Мерцающий Hello может занять too10 минут.</span><span class="sxs-lookup"><span data-stu-id="eb51d-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="eb51d-170">Установка пароля</span><span class="sxs-lookup"><span data-stu-id="eb51d-170">Set password</span></span>
1. <span data-ttu-id="eb51d-171">На hello `Set up options` щелкните `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="eb51d-172">Для платы Intel® Edison вы можете задать пользовательское имя.</span><span class="sxs-lookup"><span data-stu-id="eb51d-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="eb51d-173">Это необязательно.</span><span class="sxs-lookup"><span data-stu-id="eb51d-173">This is optional.</span></span>
3. <span data-ttu-id="eb51d-174">Введите пароль для вашей платы, а затем щелкните `Set password`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="eb51d-175">Помечен как неработающий hello пароль, который будет использоваться позднее.</span><span class="sxs-lookup"><span data-stu-id="eb51d-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="eb51d-176">Подключение Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="eb51d-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="eb51d-177">На hello `Set up options` щелкните `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="eb51d-178">Ожидание копирования tooone минуты в виде проверки вашего компьютера для доступных сетей Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="eb51d-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="eb51d-179">Из hello `Detected Networks` раскрывающегося списка выберите сети.</span><span class="sxs-lookup"><span data-stu-id="eb51d-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="eb51d-180">Из hello `Security` раскрывающегося списка, выберите hello сетевой безопасности типа.</span><span class="sxs-lookup"><span data-stu-id="eb51d-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="eb51d-181">Укажите имя и пароль для входа, затем нажмите `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="eb51d-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="eb51d-182">Помечен как неработающий hello IP-адрес, который будет использоваться позднее.</span><span class="sxs-lookup"><span data-stu-id="eb51d-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="eb51d-183">Убедитесь, что Edison подключенных toohello сетевых как на компьютере.</span><span class="sxs-lookup"><span data-stu-id="eb51d-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="eb51d-184">Tooyour Edison подключения компьютера с помощью hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="eb51d-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="eb51d-185">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="eb51d-185">Congratulations!</span></span> <span data-ttu-id="eb51d-186">Вы успешно настроили устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="eb51d-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="eb51d-187">Сводка</span><span class="sxs-lookup"><span data-stu-id="eb51d-187">Summary</span></span>
<span data-ttu-id="eb51d-188">В этой статье вы узнали, как tooassemble hello Edison платы, flash его встроенного по, установка пароля и подключите его tooWi-Fi с помощью средства настройки.</span><span class="sxs-lookup"><span data-stu-id="eb51d-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="eb51d-189">Обратите внимание, что Индикатор еще не подсвечивается приветствия.</span><span class="sxs-lookup"><span data-stu-id="eb51d-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="eb51d-190">Следующая задача Hello-tooinstall hello необходимых средств и программного обеспечения в подготовке к запуску примера приложения на Edison.</span><span class="sxs-lookup"><span data-stu-id="eb51d-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb51d-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb51d-191">Next steps</span></span>
<span data-ttu-id="eb51d-192">[Получить средства hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="eb51d-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md