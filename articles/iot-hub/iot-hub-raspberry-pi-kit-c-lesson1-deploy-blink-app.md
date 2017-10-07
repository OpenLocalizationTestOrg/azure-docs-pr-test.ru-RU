---
title: "Connect Raspberry PI (C) tooAzure IoT — занятия 1: развертывание приложения | Документы Microsoft"
description: "Клонировать пример C приложения hello из GitHub и gulp toodeploy tooyour Raspberry Pi 3 этого приложения плата. В этом образце приложения мигает hello Индикатор подключен toohello плата каждые две секунды."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "мигание светодиодного индикатора raspberry pi, включение индикатора с помощью raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Создание и развертывание приложения hello мерцания
## <a name="what-you-will-do"></a>Выполняемая задача
Клонировать hello образец приложения C из GitHub и использовать tooRaspberry образец приложения средство toodeploy hello gulp hello Pi 3. Пример приложения Hello мигает hello Индикатор подключен toohello плата каждые две секунды. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:

* Как toouse hello `device-discover-cli` tooretrieve средство сети сведения о Pi.
* Как toodeploy и выполнения hello образец приложения на Pi.
* Как toodeploy и отладки приложения, выполняющегося удаленно на Pi.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить hello следующие операции:

* [Настройка устройства](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [Получить средства hello](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>Получить hello IP адрес и имя узла Pi
В Windows или терминала в macOS или Ubuntu откройте командную строку и затем выполните hello следующую команду:

```bash
devdisco list --eth
```

Вы увидите выходные данные, аналогичные toohello следующее:

![Обнаружение устройства](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Запишите hello `IP address` и `hostname` числа пи. Эти сведения потребуются позже в данной статье.

> [!NOTE]
> Убедитесь, что Pi подключенных toohello сетевых как на компьютере. Например, если компьютер находится подключенных tooa беспроводной сети при подключенном tooa проводной сети Pi, могут отображаться не hello IP адрес в выходных данных devdisco hello.

## <a name="open-hello-sample-application"></a>Привет открыть образец приложения
tooopen hello образец приложения, выполните следующие действия:

1. Клонирование репозитория образец hello из GitHub, выполнив следующую команду hello:
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Структура репозитория](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

Hello `main.c` файла в hello `app` подпапка является hello ключа исходного файла, содержащего hello toocontrol кода hello Индикатора.

### <a name="install-application-dependencies"></a>Установка зависимостей приложения
Установка библиотеки hello и другие модули, необходимые для образца приложения hello, выполнив следующую команду hello:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Настройка подключения устройства hello
tooconfigure Здравствуйте подключения устройства, выполните следующие действия:

1. Создайте файл конфигурации устройства hello, выполнив hello следующую команду:
   
   ```bash
   gulp init
   ```
   
   файл конфигурации Hello `config-raspberrypi.json` содержит учетные данные пользователя hello использовать toolog в tooPi. tooavoid hello утечки учетных данных пользователя, создается файл конфигурации hello hello во вложенной папке `.iot-hub-getting-started` hello домашней папки на компьютере.

2. Откройте файл конфигурации устройства hello в коде Visual Studio, выполнив следующую команду hello:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. Замените заполнитель hello `[device hostname or IP address]` с hello IP-адрес или имя узла hello, полученный ранее на «Получение hello IP адрес и имя узла пи.»
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> SSH-ключ можно использовать вместо имени пользователя и пароль при подключении tooRaspberry Pi. Чтобы toodo это будет иметь toogenerate hello ключ при помощи **ssh-keygen** и **pi ssh-copy-id @\<адрес устройства\>**.
>
> В Windows эти команды доступны следующие в **Git Bash**.
>
> На MacOS необходимо toorun **brew установить ssh-copy-id**.
>
> После успешной отправки hello ключа toohello Raspberry Pi, замените **device_password** с **device_key_path** свойство в **raspberrypi.json конфигурации**.
>
> Обновленные строки должны выглядеть следующим образом:
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Поздравляем! Первый пример приложения hello для Pi успешно создана.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a>Установите пакет SDK Azure IoT Hub hello на Pi
Установите hello Azure IoT Hub SDK на Pi, выполнив hello следующую команду:

```bash
gulp install-tools
```

Эта задача может занять несколько минут toocomplete hello первый раз при запуске.

### <a name="deploy-and-run-hello-sample-app"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello, выполнив следующую команду hello:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Проверки работы приложения hello
Пример приложения Hello автоматически завершается после hello Индикатор мигает в течение 20 раз. Если вы не видите hello Индикатор мигает, см. раздел hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md) для решения проблемы toocommon.
![Индикатор мигает](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Сводка
Вы установили hello необходимые средства toowork с Pi и развернуть образец приложения tooPi tooblink hello Индикатора. Вы теперь можно создать, развернуть и выполнения другой пример приложения, которое подключается Pi tooAzure toosend центр IoT и получать сообщения.

## <a name="next-steps"></a>Дальнейшие действия
[Get Azure tools](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md) (Получение инструментов Azure)

