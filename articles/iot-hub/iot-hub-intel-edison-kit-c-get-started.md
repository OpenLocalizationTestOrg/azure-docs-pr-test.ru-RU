---
title: "aaaIntel Edison toocloud (C) - подключения Edison Intel tooAzure центр IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключите tooAzure Intel Edison центр IoT для Intel Edison toosend данных toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot intel edison, intel центр iot edison, intel edison отправки данных toocloud, intel edison toocloud"
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a><span data-ttu-id="85d9e-104">Подключение Intel Edison tooAzure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="85d9e-104">Connect Intel Edison tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="85d9e-105">В этом учебнике сначала обучения hello основы работы с Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="85d9e-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="85d9e-106">Затем вы узнаете, как tooseamlessly подключаться toohello облачных устройств с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="85d9e-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="85d9e-107">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="85d9e-107">Don't have a kit yet?</span></span> <span data-ttu-id="85d9e-108">Начните [здесь](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="85d9e-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="85d9e-109">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="85d9e-109">What you do</span></span>

* <span data-ttu-id="85d9e-110">Настройте модули Intel Edison и Grove.</span><span class="sxs-lookup"><span data-stu-id="85d9e-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="85d9e-111">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="85d9e-111">Create an IoT hub.</span></span>
* <span data-ttu-id="85d9e-112">Зарегистрируйте устройство для Edison в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="85d9e-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="85d9e-113">Запустите образец приложения на tooyour Edison toosend датчиков данных центра IoT.</span><span class="sxs-lookup"><span data-stu-id="85d9e-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="85d9e-114">Подключение центра IoT tooan Intel Edison созданного вами.</span><span class="sxs-lookup"><span data-stu-id="85d9e-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="85d9e-115">Тогда выполнение примера приложения на Edison toocollect температуры и влажности данных из Grove датчика температуры.</span><span class="sxs-lookup"><span data-stu-id="85d9e-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="85d9e-116">Отправьте центра IoT tooyour данных датчика hello.</span><span class="sxs-lookup"><span data-stu-id="85d9e-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="85d9e-117">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="85d9e-117">What you learn</span></span>

* <span data-ttu-id="85d9e-118">Как toocreate центр Azure IoT и получить новые строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="85d9e-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="85d9e-119">Как tooconnect Edison с Grove датчика температуры.</span><span class="sxs-lookup"><span data-stu-id="85d9e-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="85d9e-120">Как toocollect датчиков, выполнив пример приложения на Edison.</span><span class="sxs-lookup"><span data-stu-id="85d9e-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="85d9e-121">Как центр IoT tooyour данных датчика toosend.</span><span class="sxs-lookup"><span data-stu-id="85d9e-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="85d9e-122">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="85d9e-122">What you need</span></span>

![Необходимые элементы](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="85d9e-124">плата Intel Edison Hello</span><span class="sxs-lookup"><span data-stu-id="85d9e-124">hello Intel Edison board</span></span>
* <span data-ttu-id="85d9e-125">плата расширения Arduino;</span><span class="sxs-lookup"><span data-stu-id="85d9e-125">Arduino expansion board</span></span>
* <span data-ttu-id="85d9e-126">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="85d9e-126">An active Azure subscription.</span></span> <span data-ttu-id="85d9e-127">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="85d9e-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="85d9e-128">ПК или компьютер Mac под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="85d9e-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="85d9e-129">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="85d9e-129">An Internet connection.</span></span>
* <span data-ttu-id="85d9e-130">Micro B tooType USB-кабель</span><span class="sxs-lookup"><span data-stu-id="85d9e-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="85d9e-131">источник питания постоянного тока (DC).</span><span class="sxs-lookup"><span data-stu-id="85d9e-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="85d9e-132">Источник питания должен иметь такие параметры:</span><span class="sxs-lookup"><span data-stu-id="85d9e-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="85d9e-133">напряжение постоянного тока 7–15 В;</span><span class="sxs-lookup"><span data-stu-id="85d9e-133">7-15V DC</span></span>
  - <span data-ttu-id="85d9e-134">мощность не менее 1500 мА;</span><span class="sxs-lookup"><span data-stu-id="85d9e-134">At least 1500mA</span></span>
  - <span data-ttu-id="85d9e-135">Hello center или внутренний ПИН-код должен быть полюса положительный результат hello hello источника питания</span><span class="sxs-lookup"><span data-stu-id="85d9e-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="85d9e-136">Привет, следующие элементы являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="85d9e-136">hello following items are optional:</span></span>

* <span data-ttu-id="85d9e-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="85d9e-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="85d9e-138">Grove — датчик температуры</span><span class="sxs-lookup"><span data-stu-id="85d9e-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="85d9e-139">Кабель Grove</span><span class="sxs-lookup"><span data-stu-id="85d9e-139">Grove Cable</span></span>
* <span data-ttu-id="85d9e-140">Разделитель строки или винты, включенных в пакетов hello, включая два винты toofasten hello модуля toohello плата расширения и четыре набора винты и пластиковая разделителей.</span><span class="sxs-lookup"><span data-stu-id="85d9e-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="85d9e-141">Эти элементы являются необязательными, поскольку поддержка образец кода hello смоделированные данные датчиков.</span><span class="sxs-lookup"><span data-stu-id="85d9e-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="85d9e-142">Настройка Intel Edison</span><span class="sxs-lookup"><span data-stu-id="85d9e-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="85d9e-143">Сборка платы</span><span class="sxs-lookup"><span data-stu-id="85d9e-143">Assemble your board</span></span>

<span data-ttu-id="85d9e-144">Этот раздел содержит действия tooattach доске Intel® Edison tooyour модуля расширения.</span><span class="sxs-lookup"><span data-stu-id="85d9e-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="85d9e-145">Поместите модуль Intel® Edison hello внутри структуры hello белого на доске расширения, выравнивается отверстия hello hello модуля с винты hello платы расширения hello.</span><span class="sxs-lookup"><span data-stu-id="85d9e-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="85d9e-146">Нажмите и удерживайте на модуль hello сразу после слова hello `What will you make?` до привязки.</span><span class="sxs-lookup"><span data-stu-id="85d9e-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![Сборка платы 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="85d9e-148">Используйте toohello плата расширения toosecure hello hello два шестнадцатеричных основы (включен в пакет hello) модуля.</span><span class="sxs-lookup"><span data-stu-id="85d9e-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![Сборка платы 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="85d9e-150">Вставьте винт одним hello четыре угла отверстия на доске расширения hello.</span><span class="sxs-lookup"><span data-stu-id="85d9e-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="85d9e-151">Скручивание и усилить одним из разделителей пластиковая hello белого на винт hello.</span><span class="sxs-lookup"><span data-stu-id="85d9e-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![Сборка платы 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="85d9e-153">Повторите эти действия для hello других разделителей трех углов.</span><span class="sxs-lookup"><span data-stu-id="85d9e-153">Repeat for hello other three corner spacers.</span></span>

   ![Сборка платы 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="85d9e-155">Сборка платы завершена.</span><span class="sxs-lookup"><span data-stu-id="85d9e-155">Now your board is assembled.</span></span>

   ![Собранная плата](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="85d9e-157">Подключения hello щита базы Grove и датчик температуры hello</span><span class="sxs-lookup"><span data-stu-id="85d9e-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="85d9e-158">Поместите hello щита базы Grove tooyour системной платы.</span><span class="sxs-lookup"><span data-stu-id="85d9e-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="85d9e-159">Убедитесь, что все контакты хорошо подключены к плате.</span><span class="sxs-lookup"><span data-stu-id="85d9e-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="85d9e-161">Используйте Grove кабель tooconnect Grove датчик температуры на hello щита базы Grove **A0** порта.</span><span class="sxs-lookup"><span data-stu-id="85d9e-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Подключение tootemperature датчика](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Подключение Edison и датчика](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="85d9e-164">Теперь датчик готов.</span><span class="sxs-lookup"><span data-stu-id="85d9e-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="85d9e-165">Подключение питания Edison</span><span class="sxs-lookup"><span data-stu-id="85d9e-165">Power up Edison</span></span>

1. <span data-ttu-id="85d9e-166">Подключите питание hello.</span><span class="sxs-lookup"><span data-stu-id="85d9e-166">Plug in hello power supply.</span></span>

   ![Подключение источника питания](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="85d9e-168">Зеленый Индикатор (с меткой DS1 hello плата расширения Arduino *) необходимо включить и оставаться включенными.</span><span class="sxs-lookup"><span data-stu-id="85d9e-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="85d9e-169">Подождите одну минуту, для загрузки toofinish плата hello.</span><span class="sxs-lookup"><span data-stu-id="85d9e-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="85d9e-170">Если у вас питания постоянного ТОКА, вы можете платы hello питания через USB-порт.</span><span class="sxs-lookup"><span data-stu-id="85d9e-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="85d9e-171">Дополнительные сведения см. в разделе `Connect Edison tooyour computer`.</span><span class="sxs-lookup"><span data-stu-id="85d9e-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="85d9e-172">Такой способ подачи питания может привести к непредсказуемому поведению системной платы, особенно при использовании Wi-Fi или двигателей.</span><span class="sxs-lookup"><span data-stu-id="85d9e-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="85d9e-173">Подключите компьютер tooyour Edison</span><span class="sxs-lookup"><span data-stu-id="85d9e-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="85d9e-174">Переключение вниз микропереключателя hello сторону hello два micro USB-портов, так, чтобы Edison режим устройства.</span><span class="sxs-lookup"><span data-stu-id="85d9e-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="85d9e-175">Различия между режимами устройства и узла описаны [здесь](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="85d9e-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Переключение вниз микропереключателя hello](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="85d9e-177">Подключите кабель USB micro hello hello top micro USB-порту.</span><span class="sxs-lookup"><span data-stu-id="85d9e-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Верхний порт micro-USB](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="85d9e-179">Другой конец USB-кабель Здравствуйте, подключаемых к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="85d9e-179">Plug hello other end of USB cable into your computer.</span></span>

   ![Подключение USB к компьютеру](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="85d9e-181">Вы можете быть уверены, что инициализация платы завершилась, когда компьютер присоединит новый диск (примерно так же, как при подключении SD-карты).</span><span class="sxs-lookup"><span data-stu-id="85d9e-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="85d9e-182">Загрузите и запустите средство настройки hello</span><span class="sxs-lookup"><span data-stu-id="85d9e-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="85d9e-183">Получить последние средство настройки hello из [эту ссылку](https://software.intel.com/en-us/iot/hardware/edison/downloads) списке hello `Installers` заголовок.</span><span class="sxs-lookup"><span data-stu-id="85d9e-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="85d9e-184">Выполнение средства hello и выполните его на экране инструкции, нажав кнопку Далее, при необходимости</span><span class="sxs-lookup"><span data-stu-id="85d9e-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="85d9e-185">Встроенное ПО</span><span class="sxs-lookup"><span data-stu-id="85d9e-185">Flash firmware</span></span>
1. <span data-ttu-id="85d9e-186">На hello `Set up options` щелкните `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="85d9e-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="85d9e-187">Выберите tooflash hello изображения на доске, выполнив одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="85d9e-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="85d9e-188">Выберите toodownload и flash вашей системной платы с hello последнюю образ встроенного ПО Intel, доступные `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="85d9e-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="85d9e-189">tooflash вашей системной платы с изображением, уже сохранен на компьютере, выберите `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="85d9e-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="85d9e-190">Обзор tooand выберите hello изображения должны tooflash tooyour платы.</span><span class="sxs-lookup"><span data-stu-id="85d9e-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="85d9e-191">средство установки Hello попытается tooflash доске.</span><span class="sxs-lookup"><span data-stu-id="85d9e-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="85d9e-192">весь процесс Мерцающий Hello может занять too10 минут.</span><span class="sxs-lookup"><span data-stu-id="85d9e-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="85d9e-193">Установка пароля</span><span class="sxs-lookup"><span data-stu-id="85d9e-193">Set password</span></span>
1. <span data-ttu-id="85d9e-194">На hello `Set up options` щелкните `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="85d9e-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="85d9e-195">Для платы Intel® Edison вы можете задать пользовательское имя.</span><span class="sxs-lookup"><span data-stu-id="85d9e-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="85d9e-196">Это необязательно.</span><span class="sxs-lookup"><span data-stu-id="85d9e-196">This is optional.</span></span>
3. <span data-ttu-id="85d9e-197">Введите пароль для вашей платы, а затем щелкните `Set password`.</span><span class="sxs-lookup"><span data-stu-id="85d9e-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="85d9e-198">Помечен как неработающий hello пароль, который будет использоваться позднее.</span><span class="sxs-lookup"><span data-stu-id="85d9e-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="85d9e-199">Подключение Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="85d9e-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="85d9e-200">На hello `Set up options` щелкните `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="85d9e-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="85d9e-201">Ожидание копирования tooone минуты в виде проверки вашего компьютера для доступных сетей Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="85d9e-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="85d9e-202">Из hello `Detected Networks` раскрывающегося списка выберите сети.</span><span class="sxs-lookup"><span data-stu-id="85d9e-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="85d9e-203">Из hello `Security` раскрывающегося списка, выберите hello сетевой безопасности типа.</span><span class="sxs-lookup"><span data-stu-id="85d9e-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="85d9e-204">Укажите имя и пароль для входа, затем нажмите `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="85d9e-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="85d9e-205">Помечен как неработающий hello IP-адрес, который будет использоваться позднее.</span><span class="sxs-lookup"><span data-stu-id="85d9e-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="85d9e-206">Убедитесь, что Edison подключенных toohello сетевых как на компьютере.</span><span class="sxs-lookup"><span data-stu-id="85d9e-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="85d9e-207">Tooyour Edison подключения компьютера с помощью hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="85d9e-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Подключение tootemperature датчика](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="85d9e-209">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="85d9e-209">Congratulations!</span></span> <span data-ttu-id="85d9e-210">Вы успешно настроили устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="85d9e-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="85d9e-211">Запуск примера приложения на Intel Edison</span><span class="sxs-lookup"><span data-stu-id="85d9e-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="85d9e-212">Подготовка hello устройств IoT Azure SDK</span><span class="sxs-lookup"><span data-stu-id="85d9e-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="85d9e-213">Используйте одну из hello следующую SSH клиентов из вашего узла компьютера tooconnect tooyour Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="85d9e-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="85d9e-214">Hello IP-адрес имеет из средства настройки hello и пароль hello hello один, которые заданы в нем.</span><span class="sxs-lookup"><span data-stu-id="85d9e-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="85d9e-215">[PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="85d9e-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="85d9e-216">Hello встроенный клиент SSH на Ubuntu или macOS (запустить `ssh root@"hello IP address"`).</span><span class="sxs-lookup"><span data-stu-id="85d9e-216">hello built-in SSH client on Ubuntu or macOS (run `ssh root@"hello IP address"`).</span></span>

2. <span data-ttu-id="85d9e-217">Клонирование hello образец клиентского приложения tooyour устройства.</span><span class="sxs-lookup"><span data-stu-id="85d9e-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="85d9e-218">Затем перейдите toohello папки репозитория toorun hello, следующая команда toobuild IoT Azure SDK</span><span class="sxs-lookup"><span data-stu-id="85d9e-218">Then navigate toohello repo folder toorun hello following command toobuild Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a><span data-ttu-id="85d9e-219">Настройка образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="85d9e-219">Configure hello sample application</span></span>

1. <span data-ttu-id="85d9e-220">Откройте файл конфигурации hello, запустив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="85d9e-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Файл конфигурации](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="85d9e-222">В этом файле можно настроить два макроса.</span><span class="sxs-lookup"><span data-stu-id="85d9e-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="85d9e-223">Hello сначала он `INTERVAL`, который определяет hello временной интервал между двумя сообщений, передаваемых toocloud.</span><span class="sxs-lookup"><span data-stu-id="85d9e-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="85d9e-224">Здравствуйте, вторая — `SIMULATED_DATA`, — логическое значение для ли toouse смоделированные данные датчиков или нет.</span><span class="sxs-lookup"><span data-stu-id="85d9e-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="85d9e-225">Если вы **нет hello датчика**, задайте hello `SIMULATED_DATA` значение слишком`1` пример приложения hello toomake создать и использовать имитацию датчиков.</span><span class="sxs-lookup"><span data-stu-id="85d9e-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="85d9e-226">Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.</span><span class="sxs-lookup"><span data-stu-id="85d9e-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="85d9e-227">Построение и запуск образца приложения hello</span><span class="sxs-lookup"><span data-stu-id="85d9e-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="85d9e-228">Построение образца приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="85d9e-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Выходные данные при создании](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="85d9e-230">Выполните пример приложения hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="85d9e-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="85d9e-231">Убедитесь, что вы скопированные и вставленные строки подключения устройств hello в одинарных кавычках hello.</span><span class="sxs-lookup"><span data-stu-id="85d9e-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="85d9e-232">Вы увидите следующее hello выходных данных, показано hello датчик данных и hello сообщений, отправляемых tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="85d9e-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Вывод — данные датчика, отправленные из центра IoT tooyour Intel Edison](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="85d9e-234">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="85d9e-234">Next steps</span></span>

<span data-ttu-id="85d9e-235">Вы впервые запускаете в образце данных датчика toocollect приложения и отправьте его центр IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="85d9e-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
