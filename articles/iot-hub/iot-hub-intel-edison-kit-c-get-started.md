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
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a>Подключение Intel Edison tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

В этом учебнике сначала обучения hello основы работы с Intel Edison. Затем вы узнаете, как tooseamlessly подключаться toohello облачных устройств с помощью [центр IoT Azure](iot-hub-what-is-iot-hub.md).

Нет начального набора? Начните [здесь](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>В рамках этого руководства мы:

* Настройте модули Intel Edison и Grove.
* Создайте Центр Интернета вещей.
* Зарегистрируйте устройство для Edison в Центре Интернета вещей.
* Запустите образец приложения на tooyour Edison toosend датчиков данных центра IoT.

Подключение центра IoT tooan Intel Edison созданного вами. Тогда выполнение примера приложения на Edison toocollect температуры и влажности данных из Grove датчика температуры. Отправьте центра IoT tooyour данных датчика hello.

## <a name="what-you-learn"></a>Что вы узнаете

* Как toocreate центр Azure IoT и получить новые строки подключения устройства.
* Как tooconnect Edison с Grove датчика температуры.
* Как toocollect датчиков, выполнив пример приложения на Edison.
* Как центр IoT tooyour данных датчика toosend.

## <a name="what-you-need"></a>Необходимые элементы

![Необходимые элементы](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* плата Intel Edison Hello
* плата расширения Arduino;
* Активная подписка Azure. Если ее нет, можно создать [бесплатную пробную учетную запись Azure](https://azure.microsoft.com/free/) всего за несколько минут.
* ПК или компьютер Mac под управлением Windows или Linux.
* Подключение к Интернету.
* Micro B tooType USB-кабель
* источник питания постоянного тока (DC). Источник питания должен иметь такие параметры:
  - напряжение постоянного тока 7–15 В;
  - мощность не менее 1500 мА;
  - Hello center или внутренний ПИН-код должен быть полюса положительный результат hello hello источника питания

Привет, следующие элементы являются необязательными.

* Grove Base Shield V2
* Grove — датчик температуры
* Кабель Grove
* Разделитель строки или винты, включенных в пакетов hello, включая два винты toofasten hello модуля toohello плата расширения и четыре набора винты и пластиковая разделителей.

> [!NOTE] 
Эти элементы являются необязательными, поскольку поддержка образец кода hello смоделированные данные датчиков.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Настройка Intel Edison

### <a name="assemble-your-board"></a>Сборка платы

Этот раздел содержит действия tooattach доске Intel® Edison tooyour модуля расширения.

1. Поместите модуль Intel® Edison hello внутри структуры hello белого на доске расширения, выравнивается отверстия hello hello модуля с винты hello платы расширения hello.

2. Нажмите и удерживайте на модуль hello сразу после слова hello `What will you make?` до привязки.

   ![Сборка платы 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. Используйте toohello плата расширения toosecure hello hello два шестнадцатеричных основы (включен в пакет hello) модуля.

   ![Сборка платы 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. Вставьте винт одним hello четыре угла отверстия на доске расширения hello. Скручивание и усилить одним из разделителей пластиковая hello белого на винт hello.

   ![Сборка платы 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. Повторите эти действия для hello других разделителей трех углов.

   ![Сборка платы 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

Сборка платы завершена.

   ![Собранная плата](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Подключения hello щита базы Grove и датчик температуры hello

1. Поместите hello щита базы Grove tooyour системной платы. Убедитесь, что все контакты хорошо подключены к плате.
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. Используйте Grove кабель tooconnect Grove датчик температуры на hello щита базы Grove **A0** порта.

   ![Подключение tootemperature датчика](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Подключение Edison и датчика](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

Теперь датчик готов.

### <a name="power-up-edison"></a>Подключение питания Edison

1. Подключите питание hello.

   ![Подключение источника питания](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. Зеленый Индикатор (с меткой DS1 hello плата расширения Arduino *) необходимо включить и оставаться включенными.

3. Подождите одну минуту, для загрузки toofinish плата hello.

   > [!NOTE]
   > Если у вас питания постоянного ТОКА, вы можете платы hello питания через USB-порт. Дополнительные сведения см. в разделе `Connect Edison tooyour computer`. Такой способ подачи питания может привести к непредсказуемому поведению системной платы, особенно при использовании Wi-Fi или двигателей.

### <a name="connect-edison-tooyour-computer"></a>Подключите компьютер tooyour Edison

1. Переключение вниз микропереключателя hello сторону hello два micro USB-портов, так, чтобы Edison режим устройства. Различия между режимами устройства и узла описаны [здесь](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Переключение вниз микропереключателя hello](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. Подключите кабель USB micro hello hello top micro USB-порту.

   ![Верхний порт micro-USB](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. Другой конец USB-кабель Здравствуйте, подключаемых к компьютеру.

   ![Подключение USB к компьютеру](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. Вы можете быть уверены, что инициализация платы завершилась, когда компьютер присоединит новый диск (примерно так же, как при подключении SD-карты).

## <a name="download-and-run-hello-configuration-tool"></a>Загрузите и запустите средство настройки hello
Получить последние средство настройки hello из [эту ссылку](https://software.intel.com/en-us/iot/hardware/edison/downloads) списке hello `Installers` заголовок. Выполнение средства hello и выполните его на экране инструкции, нажав кнопку Далее, при необходимости

### <a name="flash-firmware"></a>Встроенное ПО
1. На hello `Set up options` щелкните `Flash Firmware`.
2. Выберите tooflash hello изображения на доске, выполнив одно из следующих hello:
   - Выберите toodownload и flash вашей системной платы с hello последнюю образ встроенного ПО Intel, доступные `Download hello latest image version xxxx`.
   - tooflash вашей системной платы с изображением, уже сохранен на компьютере, выберите `Select hello local image`. Обзор tooand выберите hello изображения должны tooflash tooyour платы.
3. средство установки Hello попытается tooflash доске. весь процесс Мерцающий Hello может занять too10 минут.

### <a name="set-password"></a>Установка пароля
1. На hello `Set up options` щелкните `Enable Security`.
2. Для платы Intel® Edison вы можете задать пользовательское имя. Это необязательно.
3. Введите пароль для вашей платы, а затем щелкните `Set password`.
4. Помечен как неработающий hello пароль, который будет использоваться позднее.

### <a name="connect-wi-fi"></a>Подключение Wi-Fi
1. На hello `Set up options` щелкните `Connect Wi-Fi`. Ожидание копирования tooone минуты в виде проверки вашего компьютера для доступных сетей Wi-Fi.
2. Из hello `Detected Networks` раскрывающегося списка выберите сети.
3. Из hello `Security` раскрывающегося списка, выберите hello сетевой безопасности типа.
4. Укажите имя и пароль для входа, затем нажмите `Configure Wi-Fi`.
5. Помечен как неработающий hello IP-адрес, который будет использоваться позднее.

> [!NOTE]
> Убедитесь, что Edison подключенных toohello сетевых как на компьютере. Tooyour Edison подключения компьютера с помощью hello IP-адрес.

   ![Подключение tootemperature датчика](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

Поздравляем! Вы успешно настроили устройство Edison.

## <a name="run-a-sample-application-on-intel-edison"></a>Запуск примера приложения на Intel Edison

### <a name="prepare-hello-azure-iot-device-sdk"></a>Подготовка hello устройств IoT Azure SDK

1. Используйте одну из hello следующую SSH клиентов из вашего узла компьютера tooconnect tooyour Intel Edison. Hello IP-адрес имеет из средства настройки hello и пароль hello hello один, которые заданы в нем.
    - [PuTTY](http://www.putty.org/) для Windows.
    - Hello встроенный клиент SSH на Ubuntu или macOS (запустить `ssh root@"hello IP address"`).

2. Клонирование hello образец клиентского приложения tooyour устройства. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. Затем перейдите toohello папки репозитория toorun hello, следующая команда toobuild IoT Azure SDK

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a>Настройка образца приложения hello

1. Откройте файл конфигурации hello, запустив hello, следующие команды:

   ```bash
   nano config.h
   ```

   ![Файл конфигурации](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   В этом файле можно настроить два макроса. Hello сначала он `INTERVAL`, который определяет hello временной интервал между двумя сообщений, передаваемых toocloud. Здравствуйте, вторая — `SIMULATED_DATA`, — логическое значение для ли toouse смоделированные данные датчиков или нет.

   Если вы **нет hello датчика**, задайте hello `SIMULATED_DATA` значение слишком`1` пример приложения hello toomake создать и использовать имитацию датчиков.

2. Сохраните изменения и закройте окно, нажав клавиши Control-O > ВВОД > Control-X.

### <a name="build-and-run-hello-sample-application"></a>Построение и запуск образца приложения hello

1. Построение образца приложения hello, выполнив следующую команду hello:

   ```bash
   cmake . && make
   ```
   ![Выходные данные при создании](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. Выполните пример приложения hello, выполнив следующую команду hello:

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Убедитесь, что вы скопированные и вставленные строки подключения устройств hello в одинарных кавычках hello.

Вы увидите следующее hello выходных данных, показано hello датчик данных и hello сообщений, отправляемых tooyour центр IoT.

![Вывод — данные датчика, отправленные из центра IoT tooyour Intel Edison](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a>Дальнейшие действия

Вы впервые запускаете в образце данных датчика toocollect приложения и отправьте его центр IoT tooyour.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
