---
title: "Intel Edison в облако (C) — подключение Intel Edison к Центру Интернета вещей Azure | Документы Майкрософт"
description: "Узнайте, как настроить и подключить модуль Intel Edison к Центру Интернета вещей Azure и передавать данные с этого модуля в облако Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Интернет вещей azure intel edison, Центр Интернета вещей intel edison, отправка данных intel edison в облако, intel edison в облако"
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: edbdbe0230f742cd7228f04a4a83c9bd567527e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-c"></a><span data-ttu-id="a7b1e-104">Подключение Intel Edison к Центру Интернета вещей Azure (C)</span><span class="sxs-lookup"><span data-stu-id="a7b1e-104">Connect Intel Edison to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="a7b1e-105">В этом руководстве вы начнете с того, что узнаете основы работы с Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="a7b1e-106">Также вы узнаете, как можно легко подключать устройства к облаку с помощью [Центра Интернета вещей Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="a7b1e-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="a7b1e-107">Нет начального набора?</span><span class="sxs-lookup"><span data-stu-id="a7b1e-107">Don't have a kit yet?</span></span> <span data-ttu-id="a7b1e-108">Начните [здесь](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="a7b1e-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="a7b1e-109">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="a7b1e-109">What you do</span></span>

* <span data-ttu-id="a7b1e-110">Настройте модули Intel Edison и Grove.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="a7b1e-111">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-111">Create an IoT hub.</span></span>
* <span data-ttu-id="a7b1e-112">Зарегистрируйте устройство для Edison в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="a7b1e-113">Запустите пример приложения на Edison для отправки данных в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="a7b1e-114">Подключите Intel Edison к созданному Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="a7b1e-115">После этого запустите пример приложения на Edison, чтобы собрать данные о температуре и влажности с датчика температуры Grove.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="a7b1e-116">После этого отправьте данные с датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="a7b1e-117">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="a7b1e-117">What you learn</span></span>

* <span data-ttu-id="a7b1e-118">Как создать Центр Интернета вещей Azure и получить строку подключения нового устройства.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="a7b1e-119">Как подключить Edison к датчику температуры Grove.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="a7b1e-120">Как собирать данные датчика, запустив пример приложения на Edison.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="a7b1e-121">Как отправить данные датчика в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a7b1e-122">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="a7b1e-122">What you need</span></span>

![Необходимые элементы](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="a7b1e-124">Плата Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-124">The Intel Edison board</span></span>
* <span data-ttu-id="a7b1e-125">плата расширения Arduino;</span><span class="sxs-lookup"><span data-stu-id="a7b1e-125">Arduino expansion board</span></span>
* <span data-ttu-id="a7b1e-126">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-126">An active Azure subscription.</span></span> <span data-ttu-id="a7b1e-127">Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="a7b1e-128">ПК или компьютер Mac под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="a7b1e-129">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-129">An Internet connection.</span></span>
* <span data-ttu-id="a7b1e-130">кабель micro-USB (тип B-A);</span><span class="sxs-lookup"><span data-stu-id="a7b1e-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="a7b1e-131">источник питания постоянного тока (DC).</span><span class="sxs-lookup"><span data-stu-id="a7b1e-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="a7b1e-132">Источник питания должен иметь такие параметры:</span><span class="sxs-lookup"><span data-stu-id="a7b1e-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="a7b1e-133">напряжение постоянного тока 7–15 В;</span><span class="sxs-lookup"><span data-stu-id="a7b1e-133">7-15V DC</span></span>
  - <span data-ttu-id="a7b1e-134">мощность не менее 1500 мА;</span><span class="sxs-lookup"><span data-stu-id="a7b1e-134">At least 1500mA</span></span>
  - <span data-ttu-id="a7b1e-135">центральная клемма положительной полярности.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="a7b1e-136">Ниже приведены необязательные компоненты.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-136">The following items are optional:</span></span>

* <span data-ttu-id="a7b1e-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="a7b1e-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="a7b1e-138">Grove — датчик температуры</span><span class="sxs-lookup"><span data-stu-id="a7b1e-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="a7b1e-139">Кабель Grove</span><span class="sxs-lookup"><span data-stu-id="a7b1e-139">Grove Cable</span></span>
* <span data-ttu-id="a7b1e-140">все прокладки и винты, которые входят в комплект поставки, включая два винта для крепления модуля к плате расширения и четыре набора винтов с пластиковыми опорами;</span><span class="sxs-lookup"><span data-stu-id="a7b1e-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="a7b1e-141">Эти компоненты необязательны, поскольку пример кода поддерживает использование смоделированных данных датчиков.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="a7b1e-142">Настройка Intel Edison</span><span class="sxs-lookup"><span data-stu-id="a7b1e-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="a7b1e-143">Сборка платы</span><span class="sxs-lookup"><span data-stu-id="a7b1e-143">Assemble your board</span></span>

<span data-ttu-id="a7b1e-144">Этот раздел описывает процедуру подключения модуля Intel® Edison к плате расширения.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="a7b1e-145">Поместите модуль Intel® Edison в белый контур на плате расширения, совместив отверстия в модуле с винтами на плате расширения.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="a7b1e-146">Нажмите на модуль в точке под словами `What will you make?`, опустив его вниз до щелчка.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![Сборка платы 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="a7b1e-148">Используйте две шестигранные гайки (входят в комплект) для крепления модуля к плате расширения.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![Сборка платы 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="a7b1e-150">Вставьте винт в одно из четырех угловых отверстий на плате расширения.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="a7b1e-151">Наденьте на винт и плотно затяните белую пластмассовую опору.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![Сборка платы 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="a7b1e-153">Повторите этот шаг для других угловых опор.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-153">Repeat for the other three corner spacers.</span></span>

   ![Сборка платы 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="a7b1e-155">Сборка платы завершена.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-155">Now your board is assembled.</span></span>

   ![Собранная плата](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="a7b1e-157">Подключение Grove Base Shield и датчика температуры</span><span class="sxs-lookup"><span data-stu-id="a7b1e-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="a7b1e-158">Расположите Grove Base Shield на плате.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="a7b1e-159">Убедитесь, что все контакты хорошо подключены к плате.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="a7b1e-161">С помощью кабеля Grove подключите датчик температуры Grove к порту **A0** Grove Base Shield.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Подключение к датчику температуры](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Подключение Edison и датчика](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="a7b1e-164">Теперь датчик готов.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="a7b1e-165">Подключение питания Edison</span><span class="sxs-lookup"><span data-stu-id="a7b1e-165">Power up Edison</span></span>

1. <span data-ttu-id="a7b1e-166">Подключите источник питания.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-166">Plug in the power supply.</span></span>

   ![Подключение источника питания](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="a7b1e-168">Должен загореться зеленый светодиод (на плате расширения Arduino* он обозначен как DS1).</span><span class="sxs-lookup"><span data-stu-id="a7b1e-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="a7b1e-169">Подождите минуту, пока завершится загрузка системной платы.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a7b1e-170">Если у вас нет источника питания постоянного тока, вы можете подать на плату питание через порт USB.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="a7b1e-171">Дополнительные сведения см. в разделе `Connect Edison to your computer`.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="a7b1e-172">Такой способ подачи питания может привести к непредсказуемому поведению системной платы, особенно при использовании Wi-Fi или двигателей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="a7b1e-173">Подключение Edison к компьютеру</span><span class="sxs-lookup"><span data-stu-id="a7b1e-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="a7b1e-174">Переведите микропереключатель вниз, в сторону двух портов micro-USB, чтобы перевести Edison в режим устройства.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="a7b1e-175">Различия между режимами устройства и узла описаны [здесь](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="a7b1e-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Переключение микропереключателя вниз](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="a7b1e-177">Подключите кабель micro-USB к верхнему порту micro-USB.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Верхний порт micro-USB](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="a7b1e-179">Другой конец кабеля USB подключите к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-179">Plug the other end of USB cable into your computer.</span></span>

   ![Подключение USB к компьютеру](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="a7b1e-181">Вы можете быть уверены, что инициализация платы завершилась, когда компьютер присоединит новый диск (примерно так же, как при подключении SD-карты).</span><span class="sxs-lookup"><span data-stu-id="a7b1e-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="a7b1e-182">Скачивание и запуск инструмента настройки</span><span class="sxs-lookup"><span data-stu-id="a7b1e-182">Download and run the configuration tool</span></span>
<span data-ttu-id="a7b1e-183">Скачайте последнюю версию инструмента настройки, выбрав нужный вариант в разделе `Installers` на [этой странице](https://software.intel.com/en-us/iot/hardware/edison/downloads).</span><span class="sxs-lookup"><span data-stu-id="a7b1e-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="a7b1e-184">Запустите инструмент и выполните инструкции, которые будут отображаться на экране. Нажимайте кнопку "Далее" по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="a7b1e-185">Встроенное ПО</span><span class="sxs-lookup"><span data-stu-id="a7b1e-185">Flash firmware</span></span>
1. <span data-ttu-id="a7b1e-186">На странице `Set up options` нажмите кнопку `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="a7b1e-187">Выберите образ, который нужно установить на плату:</span><span class="sxs-lookup"><span data-stu-id="a7b1e-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="a7b1e-188">чтобы скачать и установить последнюю версию встроенного ПО, предлагаемого Intel для вашей платы, выберите `Download the latest image version xxxx`;</span><span class="sxs-lookup"><span data-stu-id="a7b1e-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="a7b1e-189">чтобы установить образ, который вы ранее сохранили на своем компьютере, выберите `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="a7b1e-190">Найдите и выберите образ для установки на плату.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="a7b1e-191">Инструмент настройки попытается установить ПО на плату.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="a7b1e-192">Этот процесс может занять до 10 минут.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="a7b1e-193">Установка пароля</span><span class="sxs-lookup"><span data-stu-id="a7b1e-193">Set password</span></span>
1. <span data-ttu-id="a7b1e-194">На странице `Set up options` нажмите кнопку `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="a7b1e-195">Для платы Intel® Edison вы можете задать пользовательское имя.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="a7b1e-196">Это необязательно.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-196">This is optional.</span></span>
3. <span data-ttu-id="a7b1e-197">Введите пароль для вашей платы, а затем щелкните `Set password`.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="a7b1e-198">Запишите пароль, он вам пригодится позднее.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="a7b1e-199">Подключение Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="a7b1e-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="a7b1e-200">На странице `Set up options` нажмите кнопку `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="a7b1e-201">Подождите примерно одну минуту, пока компьютер найдет доступные сети Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="a7b1e-202">В раскрывающемся списке `Detected Networks` выберите нужную сеть.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="a7b1e-203">В раскрывающемся списке `Security` выберите режим безопасности для этой сети.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="a7b1e-204">Укажите имя и пароль для входа, затем нажмите `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="a7b1e-205">Запишите полученный IP-адрес, он вам пригодится позже.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="a7b1e-206">Убедитесь, что плата Edison подключена к той же сети, что и компьютер.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="a7b1e-207">Компьютер подключается к плате Edison по IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Подключение к датчику температуры](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="a7b1e-209">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="a7b1e-209">Congratulations!</span></span> <span data-ttu-id="a7b1e-210">Вы успешно настроили устройство Edison.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="a7b1e-211">Запуск примера приложения на Intel Edison</span><span class="sxs-lookup"><span data-stu-id="a7b1e-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="a7b1e-212">Подготовка пакета SDK устройства для Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="a7b1e-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="a7b1e-213">Используйте один из следующих SSH-клиентов для подключения к Intel Edison с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="a7b1e-214">IP-адрес и пароль взяты из средства настройки.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="a7b1e-215">[PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="a7b1e-216">Встроенный SSH-клиент ОС Ubuntu или macOS (выполните `ssh root@"the IP address"`).</span><span class="sxs-lookup"><span data-stu-id="a7b1e-216">The built-in SSH client on Ubuntu or macOS (run `ssh root@"the IP address"`).</span></span>

2. <span data-ttu-id="a7b1e-217">Клонируйте пример клиентского приложения на свое устройство.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="a7b1e-218">После этого перейдите к папке репозитория и выполните указанную ниже команду, чтобы создать пакет SDK Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-218">Then navigate to the repo folder to run the following command to build Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-the-sample-application"></a><span data-ttu-id="a7b1e-219">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="a7b1e-219">Configure the sample application</span></span>

1. <span data-ttu-id="a7b1e-220">Откройте файл конфигурации, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a7b1e-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Файл конфигурации](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="a7b1e-222">В этом файле можно настроить два макроса.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="a7b1e-223">Первый из них — `INTERVAL`, который определяет промежуток времени между отправкой двух сообщений в облако.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="a7b1e-224">Второй — `SIMULATED_DATA`, который представляет собой логическое значение, определяющее, будут ли использоваться смоделированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="a7b1e-225">Если у вас **нет датчика**, задайте для параметра `SIMULATED_DATA` значение `1`, чтобы пример приложения создал и использовал смоделированные данные датчика.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="a7b1e-226">Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="a7b1e-227">Создание и запуск примера приложения</span><span class="sxs-lookup"><span data-stu-id="a7b1e-227">Build and run the sample application</span></span>

1. <span data-ttu-id="a7b1e-228">Создайте пример приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a7b1e-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Выходные данные при создании](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="a7b1e-230">Запустите пример приложения, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a7b1e-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="a7b1e-231">Обязательно скопируйте и вставьте строку подключения устройства, заключив ее в одинарные кавычки.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="a7b1e-232">Должны отобразиться следующие результаты, содержащие данные датчика и сообщения, которые отправляются в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Выходные данные — данные датчика, отправленные с Intel Edison в Центр Интернета вещей](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="a7b1e-234">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7b1e-234">Next steps</span></span>

<span data-ttu-id="a7b1e-235">Вы запустили пример приложения, чтобы собрать данные датчика и отправить их в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a7b1e-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
