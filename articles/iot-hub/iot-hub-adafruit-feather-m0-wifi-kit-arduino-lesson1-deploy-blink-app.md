---
title: "Подключение Arduino tooAzure IoT — занятия 1: развертывание приложения | Документы Microsoft"
description: "Клонировать hello образец приложения Arduino из GitHub и запустите это приложение tooyour Wi-Fi M0 Растушевка Adafruit gulp toodeploy. В этом образце приложения мигает hello объект групповой ПОЛИТИКИ"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "проекты светодиодного индикатора Arduino, включение светодиодного индикатора Arduino, код включения индикатора Arduino, программа включения индикатора Arduino, пример включения индикатора Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Создание и развертывание приложения hello мерцания
## <a name="what-you-will-do"></a>Выполняемая задача
Клонировать hello образец приложения Arduino из GitHub и использовать hello gulp средство toodeploy hello образец приложения tooyour Adafruit Растушевка M0 Wi-Fi Arduino системной платы. Каждое приложение hello объект групповой ПОЛИТИКИ #13 на barod для Hello образец ПРИВЕЛО каждые две секунды.

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting-page].

## <a name="what-you-will-learn"></a>Новые знания
* Как toodeploy и выполнения hello образец приложения в Arduino на доске.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить hello следующие операции:

* [Настройка устройства][configure-your-device]
* [Получить средства hello][get-the-tools]

## <a name="open-hello-sample-application"></a>Привет открыть образец приложения
tooopen hello образец приложения, выполните следующие действия:

1. Клонирование репозитория образец hello из GitHub, выполнив следующую команду hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Структура репозитория][repo-structure]

Hello `app.ino` файла в hello `app` подпапка является hello ключа исходного файла, содержащего hello toocontrol кода hello Индикатора.

### <a name="install-application-dependencies"></a>Установка зависимостей приложения
Установка библиотеки hello и другие модули, необходимые для образца приложения hello, выполнив следующую команду hello:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Настройка подключения устройства hello
tooconfigure Здравствуйте подключения устройства, выполните следующие действия:

1. Получите hello последовательного порта hello устройства с cli обнаружения устройства hello.

   ```bash
   devdisco list --usb
   ```

   Должны видеть выходные данные, аналогичные следующие toohello и найти COM-порт hello usb плата Arduino: ![обнаружение устройств][device-discovery]

2. Привет открыть файл `config.json` в hello папку занятия и добавьте значение hello hello, найти номер COM-порта:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > Для порта hello COM, на платформе Windows, он имеет формат hello `COM1, COM2, ...`. На macOS или Ubuntu он начинается с `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Установка средств требуется hello плата Arduino

Установите hello Azure IoT Hub SDK плата Arduino, выполнив hello следующую команду:

```bash
gulp install-tools
```

Эта задача может занять длительное время toocomplete, в зависимости от сетевого подключения.

> [!NOTE]
> Завершите работу hello экземпляр Arduino IDE при выполнении задачи gulp: `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello, выполнив следующую команду hello:

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Проверки работы приложения hello
Если вы не видите hello Индикатор мигает, см. раздел hello [руководство по устранению неполадок] [ troubleshooting-page] для решения проблемы toocommon.

![Светодиодный индикатор мигает][led-blinking]

## <a name="summary"></a>Сводка
Вы установили toowork hello необходимые средства с вашей платой Arduino и развернуть образец приложения tooyour Arduino плата tooblink hello Индикатора. Вы теперь можно создать, развернуть и запустить другой пример приложения, который подключается ваш tooAzure платы Arduino toosend центр IoT и получать сообщения.

## <a name="next-steps"></a>Дальнейшие действия
[Получить инструменты Azure hello][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md