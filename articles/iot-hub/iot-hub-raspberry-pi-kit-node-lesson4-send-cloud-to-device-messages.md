---
featureFlags: usabilla
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 4: облака на устройство | Документы Microsoft"
description: "Пример приложения Hello работает на Pi и отслеживает входящие сообщения от вашего центра IoT. Новая задача gulp отправляет сообщения tooPi из вашей hello tooblink концентратора IoT Индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "toodevice облака, сообщение из облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a>Запустите сообщений hello образец приложения tooreceive облака на устройство
В этой статье вы развернете пример приложения на устройстве Raspberry Pi 3. Пример приложения Hello отслеживает входящие сообщения от вашего центра IoT. Можно также запустить задание gulp на tooPi сообщения toosend вашего компьютера из вашего центра IoT. Пример приложения hello, получив сообщений hello, он мигает Индикатор hello. Если у вас возникнут проблемы, поиска решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-do"></a>Выполняемая задача
* Подключите пример приложения hello tooyour-центр IoT.
* Развертывание и запуск образца приложения hello.
* Отправьте сообщения из вашей IoT hub tooPi tooblink hello Индикатора.

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Способ toomonitor входящих сообщений из вашего центра IoT
* Способ toosend облака на устройство сообщений из вашей tooPi концентратора IoT.

## <a name="what-you-need"></a>Необходимые элементы
* Устройство Raspberry Pi 3, подготовленное к использованию. статье tooset копирование Pi, toolearn [настройки устройства](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* Центр Интернета вещей, созданный в вашей подписке Azure. toolearn как toocreate ваш центр IoT. в разделе [ваш центр IoT и регистрации Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Пример приложения hello tooyour-центр IoT подключения
1. Убедитесь, что вы находитесь в папке репозитория hello `iot-hub-node-raspberrypi-getting-started`. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   Обратите внимание hello `app.js` файла в hello `app` вложенную папку. Hello `app.js` файл является hello ключа исходного файла, содержащего hello кода toomonitor входящие сообщения от центра IoT hello. Hello `blinkLED` hello Индикатор мигает функции.
   
   ![Структура репозитория в пример приложения hello](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Инициализируйте hello файл конфигурации с помощью hello, следующие команды:
   
   ```bash
   npm install
   gulp init
   ```
   
   Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) на этом компьютере наследуются все конфигурации hello, поэтому вы можете пропустить toohello задачи развертывания и выполнения примера приложения hello. Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) на другом компьютере, необходимо tooreplace hello меток-заполнителей в hello `config-raspberrypi.json` файла. Hello `config-raspberrypi.json` файл находится в подпапке hello домашней папке.
   
   ![Содержимое файла конфигурации raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Замените **[устройства имя узла или IP-адрес]** с IP-адресом hello Pi или hello имени узла, который можно получить, выполнив hello `devdisco list --eth` команды.
* Замените **[строка подключения устройств IoT]** со строкой подключения устройства hello, можно получить, выполнив hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` команды.
* Замените **[строка подключения концентратора IoT]** с hello строка подключения концентратора IoT, можно получить, выполнив hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` команды.

> [!NOTE]
> Выполните также **gulp install-tools**, если это не было сделано на уроке 1.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на Pi, выполнив следующую команду hello:

```bash
gulp deploy && gulp run
```

Команда Hello развертывает tooPi приложения образец hello. Затем она запускает приложение hello на Pi и отдельную задачу на узле tooPi сообщений blink toosend 20 компьютера из вашего центра IoT.

После запуска образца приложения hello, она запускает прослушивание toomessages из вашего центра IoT. В то же время задачу hello gulp отправляет несколько сообщений «blink» из вашей tooPi концентратора IoT. Для каждого получаемого Pi сообщения blink hello образец приложения вызывает hello `blinkLED` tooblink функции hello Индикатора.

Вы увидите мигающий Индикатор hello каждые две секунды как hello gulp задача отправляет 20 сообщения из вашей tooPi концентратора IoT. Hello последнего одним является «остановить» сообщение о том, под управлением toostop приложения hello.

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>Сводка
Успешно отправлено сообщений из вашей IoT hub tooPi tooblink hello Индикатора. Следующая задача Hello является необязательным: изменение hello и отключать поведение hello Индикатора.

## <a name="next-steps"></a>Дальнейшие действия
[Изменить hello и отключать поведение hello Индикатора](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

