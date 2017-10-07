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
# <a name="configure-your-intel-edison"></a>Настройка Intel Edison
## <a name="what-you-will-do"></a>Выполняемая задача
Настройте Intel Edison для первого использования путем сборки hello доски, его включение питания и установка конфигурации средства tooyour настольных ОС tooflash встроенного по Edison, задать пароль и подключите его tooWi-Fi. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:

* Как плата tooassemble Edison и включите его.
* Как tooflash Edison встроенного по, задать пароль и подключения Wi-Fi.

## <a name="what-you-need"></a>Необходимые элементы
toocomplete этой операции требуется hello следующую частей из начального набора Edison Intel:

* модуль Intel® Edison;
* плата расширения Arduino;
* Разделитель строки или винты, включенных в пакетов hello, включая два винты toofasten hello модуля toohello плата расширения и четыре набора винты и пластиковая разделителей.
* Micro B tooType USB-кабель
* источник питания постоянного тока (DC). Источник питания должен иметь такие параметры:
  - напряжение постоянного тока 7–15 В;
  - мощность не менее 1500 мА;
  - Hello center или внутренний ПИН-код должен быть полюса положительный результат hello hello источника питания

  ![Предметы в начальном наборе](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Кроме того, вам понадобится следующее:

* Компьютер под управлением Windows, Mac или Linux.
* Беспроводное подключение для tooconnect Edison для.
* Подключение toodownload конфигурации инструментальных средств Интернета.

## <a name="assemble-your-board"></a>Сборка платы

Этот раздел содержит действия tooattach доске Intel® Edison tooyour модуля расширения.

1. Поместите модуль Intel® Edison hello внутри структуры hello белого на доске расширения, выравнивается отверстия hello hello модуля с винты hello платы расширения hello.

2. Нажмите и удерживайте на модуль hello сразу после слова hello `What will you make?` до привязки.

   ![Сборка платы 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Используйте toohello плата расширения toosecure hello hello два шестнадцатеричных основы (включен в пакет hello) модуля.

   ![Сборка платы 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Вставьте винт одним hello четыре угла отверстия на доске расширения hello. Скручивание и усилить одним из разделителей пластиковая hello белого на винт hello.

   ![Сборка платы 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Повторите эти действия для hello других разделителей трех углов.

   ![Сборка платы 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Сборка платы завершена.

   ![Собранная плата](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Подключение питания Edison

1. Подключите питание hello.

   ![Подключение источника питания](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Зеленый Индикатор (с меткой DS1 hello плата расширения Arduino *) необходимо включить и оставаться включенными.

3. Подождите одну минуту, для загрузки toofinish плата hello.

   > [!NOTE]
   > Если у вас питания постоянного ТОКА, вы можете платы hello питания через USB-порт. Дополнительные сведения см. в разделе `Connect Edison tooyour computer`. Такой способ подачи питания может привести к непредсказуемому поведению системной платы, особенно при использовании Wi-Fi или двигателей.

## <a name="connect-edison-tooyour-computer"></a>Подключите компьютер tooyour Edison

1. Переключение вниз микропереключателя hello сторону hello два micro USB-портов, так, чтобы Edison режим устройства. Различия между режимами устройства и узла описаны [здесь](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Переключение вниз микропереключателя hello](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Подключите кабель USB micro hello hello top micro USB-порту.

   ![Верхний порт micro-USB](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Другой конец USB-кабель Здравствуйте, подключаемых к компьютеру.

   ![Подключение USB к компьютеру](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

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

Поздравляем! Вы успешно настроили устройство Edison.

## <a name="summary"></a>Сводка
В этой статье вы узнали, как tooassemble hello Edison платы, flash его встроенного по, установка пароля и подключите его tooWi-Fi с помощью средства настройки. Обратите внимание, что Индикатор еще не подсвечивается приветствия. Следующая задача Hello-tooinstall hello необходимых средств и программного обеспечения в подготовке к запуску примера приложения на Edison.

## <a name="next-steps"></a>Дальнейшие действия
[Получить средства hello][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md