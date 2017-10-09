---
title: "Connect Raspberry PI (C) tooAzure IoT — занятия 4: облака на устройство | Документы Microsoft"
description: "Пример приложения выполняется на устройстве Pi и отслеживает входящие сообщения от Центра Интернета вещей. Новая задача gulp отправляет сообщения tooPi из вашей hello tooblink концентратора IoT Индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "toodevice облака, сообщение из облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Запустите образец приложения tooreceive сообщений облака на устройство
В этой статье вы развернете пример приложения на устройстве Raspberry Pi 3. Пример приложения Hello отслеживает входящие сообщения от вашего центра IoT. Можно также запустить задание gulp на tooPi сообщения toosend вашего компьютера из вашего центра IoT. Пример приложения hello, получив сообщений hello, он мигает Индикатор hello. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-do"></a>Выполняемая задача
* Подключите пример приложения hello tooyour-центр IoT.
* Развертывание и запуск образца приложения hello.
* Отправьте сообщения из вашей IoT hub tooPi tooblink hello Индикатора.

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Способ toomonitor входящих сообщений из вашего центра IoT.
* Способ toosend облака на устройство сообщений из вашей tooPi концентратора IoT.

## <a name="what-you-need"></a>Необходимые элементы
* Устройство Raspberry Pi 3, подготовленное к использованию. статье tooset копирование Pi, toolearn [настройки устройства](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).
* Центр Интернета вещей, созданный в вашей подписке Azure. toolearn как toocreate ваш центр IoT. в разделе [ваш центр IoT и регистрации Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Пример приложения hello tooyour-центр IoT подключения
1. Убедитесь, что вы находитесь в папке репозитория hello `iot-hub-c-raspberrypi-getting-started`. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:

   ```bash
   cd Lesson4
   code .
   ```

   Обратите внимание hello `app.c` файла в hello `app` вложенную папку. Hello `app.c` файл является hello ключа исходного файла, содержащего hello кода toomonitor входящие сообщения от центра IoT hello. Hello `blinkLED` hello Индикатор мигает функции.

   ![Структура репозитория в пример приложения hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. Инициализируйте hello файл конфигурации, выполнив следующие команды hello:

   ```bash
   npm install
   gulp init
   ```

   Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) на этом компьютере наследуются все конфигурации hello, поэтому вы можете пропустить toostep toohello задачи развертывания и выполнения примера приложения hello. Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) на другом компьютере, необходимо tooreplace hello меток-заполнителей в hello `config-raspberrypi.json` файла. Hello `config-raspberrypi.json` файл находится в подпапке hello домашней папке.

   ![Содержимое файла конфигурации raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Замените **[устройства имя узла или IP-адрес]** с Pi IP адрес или имя узла, можно получить, выполнив hello `devdisco list --eth` команды.
* Замените **[строка подключения устройств IoT]** со строкой подключения устройства hello, можно получить, выполнив hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` команды.
* Замените **[строка подключения концентратора IoT]** с hello строка подключения концентратора IoT, можно получить, выполнив hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` команды.

> [!NOTE]
> Выполните также **gulp install-tools**, если это не было сделано на уроке 1.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на Pi, выполнив следующие команды hello:

```
gulp deploy && gulp run
```

команда запускает Hello gulp сначала hello задач установки средства. Затем он развертывает tooPi приложения образец hello. Наконец он выполняется приложения hello на Pi и отдельную задачу на узле tooPi сообщений blink toosend 20 компьютера из вашего центра IoT.

После запуска образца приложения hello, она запускает прослушивание toomessages из вашего центра IoT. В то же время задачу hello gulp отправляет несколько сообщений «blink» из вашей tooPi концентратора IoT. Для каждого получаемого Pi сообщения blink hello образец приложения вызывает hello `blinkLED` tooblink функции hello Индикатора.

Вы увидите мигающий Индикатор hello каждые две секунды как hello gulp задача отправляет 20 сообщения из вашей tooPi концентратора IoT. Hello последнего одним является сообщение «остановить», мешающий выполнению приложения hello.

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a>Сводка
Успешно отправлено сообщений из вашей IoT hub tooPi tooblink hello Индикатора. Следующая задача Hello является необязательным: изменение hello и отключать поведение hello Индикатора.

## <a name="next-steps"></a>Дальнейшие действия
[Изменить hello и отключать поведение hello Индикатора](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
