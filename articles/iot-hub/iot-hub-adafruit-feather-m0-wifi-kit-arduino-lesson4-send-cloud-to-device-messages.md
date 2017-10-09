---
title: "Connect Arduino (C) tooAzure IoT — занятия 4: облака на устройство | Документы Microsoft"
description: "Пример приложения выполняется на устройстве Adafruit Feather M0 WiFi и отслеживает входящие сообщения от Центра Интернета вещей. Новая задача gulp отправляет сообщения tooAdafruit Растушевка M0 Wi-Fi из вашего hello tooblink концентратора IoT Индикатора."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "управление светодиодным индикатором с помощью Arduino с веб-интерфейса, управление светодиодным индикатором с помощью Arduino через веб-интерфейс"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Запустите образец приложения tooreceive сообщений облака на устройство
В этой статье на плате Adafruit Feather M0 WiFi Arduino развертывается пример приложения.

Пример приложения Hello отслеживает входящие сообщения от вашего центра IoT. Вы также выполнение задачи gulp на ваш компьютер tooyour сообщения toosend плата Arduino из вашего центра IoT. Пример приложения hello, получив сообщений hello, он мигает Индикатор hello. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-do"></a>Выполняемая задача
* Подключите пример приложения hello tooyour-центр IoT.
* Развертывание и запуск образца приложения hello.
* Отправьте сообщения из вашей IoT hub tooyour Arduino плата tooblink hello Индикатора.

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:
* Способ toomonitor входящих сообщений из вашего центра IoT.
* Способ toosend облака на устройство сообщений из вашей tooyour концентратора IoT Arduino платы.

## <a name="what-you-need"></a>Необходимые элементы
* Плата Arduino, настроенная для работы. в статье tooset вашей платы Arduino toolearn [настройки устройства][configure-your-device].
* Центр Интернета вещей, созданный в вашей подписке Azure. toolearn как toocreate ваш центр IoT. в разделе [создать концентратор IoT Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Пример приложения hello tooyour-центр IoT подключения

1. Убедитесь, что вы находитесь в папке репозитория hello `iot-hub-c-feather-m0-getting-started`.

   Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:

   ```bash
   cd Lesson4
   code .
   ```

   Обратите внимание hello `app.ino` файла в hello `app` вложенную папку. Hello `app.ino` файл является hello ключа исходного файла, содержащего hello кода toomonitor входящие сообщения от центра IoT hello. Hello `blinkLED` hello Индикатор мигает функции.

   ![Структура репозитория в пример приложения hello][repo-structure]

2. Получите hello последовательного порта hello устройства с cli обнаружения устройства hello.

   ```bash
   devdisco list --usb
   ```

   Должны видеть выходные данные, аналогичные следующие toohello и найти COM-порт hello usb плата Arduino:

   ![Обнаружение устройства][device-discovery]

3. Привет открыть файл `config.json` в папке занятия hello и значение входной hello hello, найти номер COM-порта:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Для порта hello COM, на платформе Windows, он имеет формат hello `COM1, COM2, ...`. На платформе MacOS или Ubuntu он будет начинаться с `/dev/`.

4. Инициализируйте hello файл конфигурации, выполнив следующие команды hello:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Сделать после замены в hello hello `config-arduino.json` файла:

   Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция] [ create-an-azure-function-app-and-storage-account] на этом компьютере наследуются все конфигурации hello, поэтому вы можете пропустить задачу toohello hello шаг развертывания и Выполнение образца приложения hello. Если вы выполнили шаги hello в [создать учетную запись приложения и хранилища Azure функция] [ create-an-azure-function-app-and-storage-account] на другом компьютере, необходимо tooreplace hello меток-заполнителей в hello `config-arduino.json` файла. Hello `config-arduino.json` файл находится в подпапке hello домашней папке.

   ![Содержимое файла конфигурации arduino.json hello][config-arduino-json]

   * Замените **[Wi-Fi SSID]** с вашей SSID Wi-Fi, подключенный toohello Интернета.
   * Замените **[Wi-Fi password]** своим паролем Wi-Fi. Удалите строку hello, если Wi-Fi не требует пароля.
   * Замените **[строка подключения устройств IoT]** со строкой подключения устройства hello, можно получить, выполнив hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` команды.
   * Замените **[строка подключения концентратора IoT]** с hello строка подключения концентратора IoT, можно получить, выполнив hello `az iot hub show-connection-string --name {my hub name}` команды.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello в Arduino на доске, выполнив следующие команды hello:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Команда gulp Hello развертывает hello образец приложения tooyour Arduino платы. Затем она запускает приложение hello на доске Arduino и отдельную задачу на узле компьютера toosend 20 blink сообщения tooyour Arduino плата из вашего центра IoT.

После запуска образца приложения hello, она запускает прослушивание toomessages из вашего центра IoT. В то же время задачу hello gulp отправляет несколько сообщений «blink» из вашей tooyour концентратора IoT Arduino платы. Вызывается для каждого сообщения blink hello плата получает, пример приложения hello hello `blinkLED` tooblink функции hello Индикатора.

Вы увидите hello Индикатор мигает каждые две секунды как задачу hello gulp 20 сообщения отправляются от вашей tooyour концентратора IoT Arduino платы. Hello последнего одним является сообщение «остановить», мешающий выполнению приложения hello.

![Пример приложения с командой Gulp и сообщениями для включения и отключения светодиодного индикатора][sample-application]

## <a name="summary"></a>Сводка
Успешно отправлено сообщений из вашей IoT hub tooyour Arduino плата tooblink hello Индикатора. Следующая задача Hello является необязательным: изменение hello и отключать поведение hello Индикатора.

## <a name="next-steps"></a>Дальнейшие действия
[Изменить hello и отключать поведение hello Индикатора][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md