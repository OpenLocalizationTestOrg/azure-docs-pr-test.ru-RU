---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 2. Получение инструментов (Ubuntu) | Документация Майкрософт"
description: "Установите на главный компьютер под управлением Ubuntu hello средств и программного обеспечения hello, создать центр IoT и зарегистрировать устройство в центре IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, облачные службы Интернета вещей, ПО Интернета вещей, Azure CLI, установка git в Ubuntu, запуск инструмента Gulp, установка Node.js в Ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Получить средства hello (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 или более поздние версии](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Выполняемая задача

- Установка Git, Node.js, Gulp и Python.
- Установите hello Azure командной строки (CLI Azure). 

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).
## <a name="what-you-will-learn"></a>Новые знания

Из этого урока вы узнаете:

- Как tooinstall Git и Node.js.
  - Git — это распределенная система управления версиями с открытым кодом. Пример приложения Hello на этом занятии будет храниться на Git.
  - Node.js — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.
- Как NPM tooinstall toouse Node.js-средств разработки.
  - Минимальная требуемая версия Hello Node.js — 4,5 LTS.
  - NPM является одним из диспетчеров пакетов приветствия для Node.js.
- Как tooinstall кода Visual Studio.
  - Visual Studio Code — это упрощенный кроссплатформенный, но мощный редактор исходного кода для платформ Windows, Linux и macOS. Он поддерживает возможности отладки, выделения синтаксиса, интеллектуального автозавершения кода, встроенные элементы управления Git, фрагменты кода, а также возможности рефакторинга кода.
- Как tooinstall hello Azure CLI
  - Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure. Работа непосредственно из tooprovision командной строки и управления ресурсами.
- Как toouse hello Azure CLI toocreate центр IoT.

## <a name="what-you-need"></a>Необходимые элементы

- Toodownload подключения Internet hello средств и программного обеспечения.
- Компьютер под управлением Ubuntu 16.04 или более поздней версии.

## <a name="install-git-and-nodejs"></a>Установка Git и Node.js

tooinstall Git и Node.js, выполните следующие действия.

1. Нажмите клавишу `Ctrl + Alt + T` tooopen терминала.
2. Выполните следующие команды hello.

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Установка инструментов разработки Node.js

Вы используете [gulp.js](http://gulpjs.com/) tooautomate развертывания и выполнения скриптов.

gulp tooinstall, запустите следующую команду в терминале hello hello:

```bash
sudo npm install -g gulp
```

При возникновении проблем с установкой hello. в разделе hello [руководство по устранению неполадок](iot-hub-gateway-kit-c-troubleshooting.md) для решения проблемы toocommon.

> [!Note]
> Узел, NPM и Gulp являются необходимые toorun сценариев автоматизации, разработанные в Node.js.

## <a name="install-hello-azure-cli"></a>Установка hello Azure CLI

tooinstall hello Azure CLI, выполните следующие действия.

1. Выполните следующие команды в терминале hello hello.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   Hello установки может потребоваться 5 минут.

2. Проверка установки hello, выполнив следующую команду hello:

   ```bash
   az iot -h
   ```
Вы увидите следующее hello выходных данных, если hello успешно установлен.
![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Установка Visual Studio Code

Использование кода Visual Studio в файлах конфигурации учебника tooedit hello в более поздней версии.

[Скачайте](https://code.visualstudio.com/docs/setup/linux) и установите Visual Studio Code.

## <a name="summary"></a>Сводка

Вы установили все необходимые hello средств и программного обеспечения на главный компьютер. Следующая задача является toouse hello Azure CLI toocreate центр IoT и зарегистрировать устройство в концентратор IoT.

## <a name="next-steps"></a>Дальнейшие действия
[Создание Центра Интернета вещей и регистрация устройства](iot-hub-gateway-kit-c-lesson2-register-device.md)
