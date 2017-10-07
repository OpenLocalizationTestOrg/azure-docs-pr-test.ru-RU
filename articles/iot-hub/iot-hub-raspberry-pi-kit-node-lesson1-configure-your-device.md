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
# <a name="configure-your-device"></a>Настройка устройства
## <a name="what-you-will-do"></a>Выполняемая задача
Настройте Pi для первого использования и установите hello Raspbian операционной системы. Raspbian является бесплатной операционной системы, оптимизированный для hello Raspberry Pi оборудования. Если у вас возникнут проблемы, может выполнять поиск решений на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:

* Как tooinstall Raspbian на Pi.
* Как toopower копирование пи с помощью USB-кабеля.
* Как tooconnect Pi toohello сети с помощью кабеля Ethernet или беспроводной сети.
* Как breadboard tooadd toohello Индикатор и подключите его tooPi.

## <a name="what-you-will-need"></a>Необходимые условия
toocomplete этой операции требуется hello следующую частей из начального набора Raspberry Pi 3:

* Hello плата Raspberry Pi 3
* карта microSD 16 ГБ Hello
* Hello 5В 2 amp питания с hello 6 фут micro USB-кабель
* Hello breadboard
* соединительные провода;
* резистор 560 Ом;
* светодиодный индикатор 10 мм с рассеянным освещением;
* Hello кабель Ethernet

![Предметы в начальном наборе](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Кроме того, вам понадобится следующее:

* Для tooconnect Pi для проводного или беспроводного подключения.
* USB-SD адаптер или miniSD карты tooburn hello образа операционной системы на карту microSD, hello.
* Компьютер под управлением Windows, Mac или Linux. Hello компьютер будет использоваться tooinstall Raspbian на карте microSD hello.
* Toodownload подключения Internet hello необходимых средств и программного обеспечения.

## <a name="install-raspbian-on-hello-microsd-card"></a>Установка Raspbian на карте microSD hello
Подготовьте карта microSD hello для установки образа Raspbian hello.

1. Скачайте ОС Raspbian.
   1. [Загрузить](https://www.raspberrypi.org/downloads/raspbian/) hello ZIP-файл для детском Raspbian с точки.
   2. Извлеките hello Raspbian изображения tooa папку на локальном компьютере.
2. Установите карту microSD toohello Raspbian.
   1. [Загрузить](https://www.etcher.io) и установить программу записи карты SD гравировальная hello.
   2. Запустите гравировальная и выберите изображение Raspbian hello, извлеченный на шаге 1.
   3. Выберите диск, карту microSD hello.
      Обратите внимание, что гравировальная может уже выбран правильный диск hello.
   4. Нажмите кнопку **Flash** tooinstall Raspbian toohello microSD карты.
   5. Удаление карта microSD hello с компьютера после завершения установки.
      Это карта microSD безопасные tooremove hello непосредственно из-за гравировальная автоматически извлечение или отключение карта microSD hello после завершения.
   6. Вставьте карту microSD hello в Pi.

![Вставьте карту SD hello](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Включение устройства Pi
Включите Pi при помощи micro USB-кабель hello и hello питания.

![Включение](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> Это важные toouse hello источник питания в комплекте hello, по крайней мере toomake 2A убедиться, что ваш Raspberry имеет недостаточно питания toowork правильно.

## <a name="enable-ssh"></a>Включение SSH
Начиная с hello ноября 2016 г. Raspbian предоставляет hello сервера SSH, по умолчанию отключены. Требуется tooenable его вручную. Можно ссылаться toohello [официальный инструкции](https://www.raspberrypi.org/documentation/remote-access/ssh/) или подключите мониторы и перейти слишком**настройки -> Конфигурация Pi Raspberry** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Подключение к сети toohello Raspberry Pi 3
Вы можете подключиться к проводной или беспроводной сети tooa tooa Pi. Убедитесь, что Pi подключенных toohello сетевых как на компьютере. Например можно подключиться Pi toohello же переключиться, что компьютер подключен к.

### <a name="connect-tooa-wired-network"></a>Подключение tooa проводной сети
Используйте tooconnect кабель Ethernet hello tooyour Pi проводной сети. Hello два индикатора на Pi включить, если соединения hello.

![Подключение с помощью кабеля Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Подключение к беспроводной сети tooa
Выполните hello [инструкции](https://www.raspberrypi.org/learning/software-guide/wifi/) hello Raspberry Pi Foundation tooconnect Pi tooyour беспроводной сети. Эти инструкции требуют toofirst подключения монитора и tooPi клавиатуры.

## <a name="connect-hello-led-toopi"></a>Подключение tooPi hello Индикатора
toocomplete этой задачи, используйте hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello проводов соединителя, hello Индикатор и hello резистор. Подключите их toohello [общего назначения ввода вывода](https://www.raspberrypi.org/documentation/usage/gpio/) порты Pi (объект групповой ПОЛИТИКИ).

![Монтажная плата, светодиодный индикатор и резистор](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Подключения слишком короткий участок hello hello Индикатор**Земля объект групповой ПОЛИТИКИ (6 ПИН-код)**.
2. Подключите hello дольше участок hello Индикатор участок tooone резистор hello.
3. Подключение слишком hello других участок hello резистор**4 объект групповой ПОЛИТИКИ (7 ПИН-код)**.

Обратите внимание, что полярности hello Индикатор важные. Этот параметр полярности известен как "Активный низкий".

![Подключение выводов](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Поздравляем! Вы успешно настроили устройство Pi.

## <a name="summary"></a>Сводка
В этой статье вы узнали, как tooconfigure Pi, установив Raspbian подключении Pi tooa сети и подключение tooPi Индикатора. Обратите внимание, что Индикатор еще не подсвечивается приветствия. Следующая задача Hello-tooinstall hello необходимых средств и программного обеспечения в подготовке к запуску примера приложения на Pi.

![Оборудование готово](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Дальнейшие действия
[Получить средства hello](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

