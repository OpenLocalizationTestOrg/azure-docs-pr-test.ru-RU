---
featureFlags: usabilla
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 1: развертывание приложения | Документы Microsoft"
description: "Клонирование приложений Node.js образец hello из GitHub и gulp toodeploy tooyour Raspberry Pi 3 этого приложения плата. В этом образце приложения мигает hello Индикатор подключен toohello плата каждые две секунды."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "мигание светодиодного индикатора raspberry pi, включение индикатора с помощью raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Создание и развертывание приложения hello мерцания
## <a name="what-you-will-do"></a>Выполняемая задача
Клонировать hello образец приложения Node.js из GitHub и использовать hello gulp средство toodeploy hello образец приложения tooyour Raspberry Pi 3. Пример приложения Hello мигает hello Индикатор подключен toohello плата каждые две секунды. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете следующее:

* Как toouse hello `device-discover-cli` tooretrieve средство сети сведения о Pi.
* Как toodeploy и выполнения hello образец приложения на Pi.
* Как toodeploy и отладки приложения, выполняющегося удаленно на Pi.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить hello следующие операции:

* [Настройка устройства](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [Получить средства hello](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

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

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования
Привет tooopen пример кода, выполните следующие действия:

1. Клонирование репозитория образец hello из GitHub, выполнив следующую команду hello:
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Структура репозитория](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

Hello `app.js` файла в hello `app` подпапка является hello ключа исходного файла, содержащего hello toocontrol кода hello Индикатора.

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
   
   # For macOS or Ubuntu
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
### <a name="install-nodejs-and-npm-on-pi"></a>Установка Node.js и NPM на устройстве Pi
Установите Node.js и NPM на Pi, выполнив следующую команду hello:

```bash
gulp install-tools
```

Эта задача может занять 10 минут toocomplete hello первый раз при запуске.

### <a name="deploy-and-run-hello-sample-app"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello, выполнив следующую команду hello:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Проверки работы приложения hello
Теперь вы увидите hello Светодиод на Pi мигает каждые две секунды.  Если вы не видите hello Индикатор мигает, см. раздел hello [руководство по устранению неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md) для решения проблемы toocommon.
![Индикатор мигает](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Сводка
Вы установили hello необходимые средства toowork с Pi и развернуть образец приложения tooPi tooblink hello Индикатора. Вы теперь можно создать, развернуть и выполнения другой пример приложения, которое подключается Pi tooAzure toosend центр IoT и получать сообщения.

## <a name="next-steps"></a>Дальнейшие действия
[Получить инструменты Azure hello](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

