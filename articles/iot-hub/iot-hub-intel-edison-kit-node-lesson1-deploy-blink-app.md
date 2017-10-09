---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 1: развертывание приложения | Документы Microsoft"
description: "Клонировать пример C приложения hello из GitHub и запуска этого приложения tooyour плата Intel Edison gulp toodeploy. В этом образце приложения мигает hello Индикатор подключен toohello плата каждые две секунды."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "проекты светодиодного индикатора Arduino, включение светодиодного индикатора Arduino, код включения индикатора Arduino, программа включения индикатора Arduino, пример включения индикатора Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Создание и развертывание приложения hello мерцания
## <a name="what-you-will-do"></a>Выполняемая задача
Клонировать пример C приложения hello из GitHub и использовать приложения образец tooIntel Edison hello gulp средство toodeploy hello. Пример приложения Hello мигает hello Индикатор подключен toohello плата каждые две секунды. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
* Как toodeploy и выполнения hello образец приложения на Edison.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить hello следующие операции:

* [Настройка устройства][configure-your-device]
* [Получить средства hello][get-the-tools]

## <a name="open-hello-sample-application"></a>Привет открыть образец приложения
tooopen hello образец приложения, выполните следующие действия:

1. Клонирование репозитория образец hello из GitHub, выполнив следующую команду hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Откройте пример приложения hello в коде Visual Studio, выполнив следующие команды hello:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Структура репозитория][repo-structure]

файл Hello в hello `app` подпапка является hello ключа исходного файла, содержащего hello toocontrol кода hello Индикатора.

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

   файл конфигурации Hello `config-edison.json` содержит учетные данные пользователя hello использовать toolog в tooEdison. tooavoid hello утечки учетных данных пользователя, создается файл конфигурации hello hello во вложенной папке `.iot-hub-getting-started` hello домашней папки на компьютере.

2. Откройте файл конфигурации устройства hello в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Замените заполнитель hello `[device hostname or IP address]` и `[device password]` hello IP-адрес и пароль, который помечен на предыдущем занятии.

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Поздравляем! Первый пример приложения hello для Edison успешно создана.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello

### <a name="deploy-and-run-hello-sample-app"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello, выполнив следующую команду hello:

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Проверки работы приложения hello
Пример приложения Hello автоматически завершается после hello Индикатор мигает в течение 20 раз. Если вы не видите hello Индикатор мигает, см. раздел hello [руководство по устранению неполадок] [ troubleshooting] для решения проблемы toocommon.

![Светодиодный индикатор мигает][led-blinking]

## <a name="summary"></a>Сводка
Вы установили hello необходимые средства toowork с Edison и развернуть образец приложения tooEdison tooblink hello Индикатора. Вы теперь можно создать, развернуть и выполнения другой пример приложения, которое подключается Edison tooAzure toosend центр IoT и получать сообщения.

## <a name="next-steps"></a>Дальнейшие действия
[Получить инструменты Azure hello][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
