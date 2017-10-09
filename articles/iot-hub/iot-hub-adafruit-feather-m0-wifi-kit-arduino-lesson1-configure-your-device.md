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
# <a name="configure-your-device"></a>Настройка устройства
## <a name="what-you-will-do"></a>Выполняемая задача
Настройте доске Adafruit Растушевка M0 Wi-Fi Arduino для первого использования путем сборки hello доски, его включение питания. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Необходимые элементы
toocomplete этой операции требуется hello следующие элементы для начального набора Adafruit Растушевка M0 Wi-Fi:

* плата Wi-Fi M0 Растушевка Adafruit Hello
* Micro B tooType USB-кабель

![набор][kit]

Кроме того, вам понадобится следующее:

* Компьютер под управлением Windows, Mac или Linux.
* Беспроводное подключение для вашей tooconnect платы Arduino для.
* Подключение toodownload конфигурации инструментальных средств Интернета.

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:

* Как tooassemble Arduino платы и power ее для hello следующие уроки.
* Каким образом разрешения tooadd последовательного порта для Ubuntu.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Подключите компьютер tooyour Arduino платы

1. Подключите кабель USB micro hello hello top micro USB-порту.

   ![Верхний порт micro-USB][top-micro-usb-port]

2. Другой конец USB-кабель Здравствуйте, подключаемых к компьютеру.

   ![Подключение USB к компьютеру][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Добавление разрешений для последовательного порта в Ubuntu

Этот раздел можно пропустить, если вы используете Windows или macOS. Для Ubuntu требуются следующие шаги toomake hello linux обычный пользователь должен toooperate hello разрешения на USB-порту hello системной платы Arduino для hello.

1. Для обычного пользователя из терминала

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   отобразится примерно такой текст:

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   Hello «0» может быть другой номер, или может быть возвращено несколько записей. В данных вариантов hello первый hello, нам нужно будет `uucp`, в hello второй — `dialout`, который является владельцем группы hello hello файла.

2. Добавьте группу toohello toohello пользователей:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Где `group-name` — hello данных из первого шага hello и `username` — имя пользователя linux.

3. Необходимо будет toolog извлечение и возврат снова для этой tootake эффект изменений и hello завершения установки.

## <a name="summary"></a>Сводка
В этой статье вы узнали, как tooconfigure Arduino доске. Следующая задача Hello-tooinstall hello необходимых средств и программного обеспечения в подготовке к запуску примера приложения в Arduino на доске.

![Оборудование готово][hardware-is-ready]

## <a name="next-steps"></a>Дальнейшие действия
[Получить средства hello][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md