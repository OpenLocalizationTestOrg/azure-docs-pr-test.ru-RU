---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 4: получение сообщений | Документы Microsoft"
description: "Пример приложения выполняется на устройстве Edison и отслеживает входящие сообщения от Центра Интернета вещей. Новая задача gulp отправляет сообщения tooEdison из вашей hello tooblink концентратора IoT Индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "управление светодиодным индикатором с помощью Arduino с веб-интерфейса, управление светодиодным индикатором с помощью Arduino через веб-интерфейс"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Запустите образец приложения tooreceive сообщений облака на устройство
В этой статье вы развернете пример приложения на устройстве Intel Edison. Пример приложения Hello отслеживает входящие сообщения от вашего центра IoT. Можно также запустить задание gulp на tooEdison сообщения toosend вашего компьютера из вашего центра IoT. Пример приложения hello, получив сообщений hello, он мигает Индикатор hello. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-do"></a>Выполняемая задача
* Подключите пример приложения hello tooyour-центр IoT.
* Развертывание и запуск образца приложения hello.
* Отправьте сообщения из вашей IoT hub tooEdison tooblink hello Индикатора.

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Способ toomonitor входящих сообщений из вашего центра IoT.
* Способ toosend облака на устройство сообщений из вашей tooEdison концентратора IoT.

## <a name="what-you-need"></a>Необходимые элементы
* Настройка Intel Edison для использования. статье tooset копирование Edison toolearn [настройки устройства][configure-your-device].
* Центр Интернета вещей, созданный в вашей подписке Azure. toolearn как toocreate ваш центр IoT. в разделе [создать концентратор IoT Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Пример приложения hello tooyour-центр IoT подключения
1. Убедитесь, что вы находитесь в папке репозитория hello `iot-hub-node-edison-getting-started`. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:

   ```bash
   cd Lesson4
   code .
   ```

   файл Hello в hello `app` подпапка является hello ключа исходного файла, содержащего hello кода toomonitor входящие сообщения от центра IoT hello. Hello `blinkLED` hello Индикатор мигает функции.

   ![Структура репозитория в пример приложения hello][repo-structure]
2. Инициализируйте hello файл конфигурации, выполнив следующие команды hello:

   ```bash
   npm install
   gulp init
   ```

   Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция] [ create-an-azure-function-app-and-storage-account] на этом компьютере наследуются все конфигурации hello, поэтому вы можете пропустить задачу toohello hello шаг развертывания и Выполнение образца приложения hello. Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция] [ create-an-azure-function-app-and-storage-account] на другом компьютере, необходимо tooreplace hello меток-заполнителей в hello `config-edison.json` файла. Hello `config-edison.json` файл находится в подпапке hello домашней папке.

   ![Содержимое файла конфигурации edison.json hello](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Замените **[устройства имя узла или IP-адрес]** с IP-адрес устройства hello помечен работу при настройке устройства.
   * Замените **[строка подключения устройств IoT]** со строкой подключения устройства hello, можно получить, выполнив hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` команды.
   * Замените **[строка подключения концентратора IoT]** с hello строка подключения концентратора IoT, можно получить, выполнив hello `az iot hub show-connection-string --name {my hub name}` команды.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на Edison, выполнив следующие команды hello:

```bash
gulp deploy && gulp run
```

Команда gulp Hello развертывает tooEdison приложения образец hello. Затем она запускает приложение hello Edison и отдельную задачу на узле tooEdison сообщений blink toosend 20 компьютера из вашего центра IoT.

После запуска образца приложения hello, она запускает прослушивание toomessages из вашего центра IoT. В то же время задачу hello gulp отправляет несколько сообщений «blink» из вашей tooEdison концентратора IoT. Для каждого получаемого Edison сообщения blink hello образец приложения вызывает hello `blinkLED` tooblink функции hello Индикатора.

Вы увидите мигающий Индикатор hello каждые две секунды как hello gulp задача отправляет 20 сообщения из вашей tooEdison концентратора IoT. Hello последнего одним является сообщение «остановить», мешающий выполнению приложения hello.

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора][gulp-command-and-blink-messages]

## <a name="summary"></a>Сводка
Успешно отправлено сообщений из вашей IoT hub tooEdison tooblink hello Индикатора. Следующая задача Hello является необязательным: изменение hello и отключать поведение hello Индикатора.

## <a name="next-steps"></a>Дальнейшие действия
[Изменить hello и отключать поведение hello Индикатора][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md