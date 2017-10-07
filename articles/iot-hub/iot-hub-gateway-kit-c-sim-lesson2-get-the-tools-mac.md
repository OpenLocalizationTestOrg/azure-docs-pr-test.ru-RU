---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 2. Получение инструментов (macOS) | Документация Майкрософт"
description: "Установка средств на компьютере Mac, создать центр IoT и зарегистрировать устройство в центре IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, программное обеспечение Интернета вещей, облачные службы Интернета вещей, ПО Интернета вещей, Azure CLI, установка Python на компьютере Mac, установка git на компьютере Mac, запуск инструмента Gulp, установка Node.js на компьютере Mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 391d60f3cbb209698cae53098efed360ac0f5fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a>Получить средства hello (macOS)
> [!div class="op_single_selector"]
> * [Windows 7 или более поздние версии](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Выполняемая задача

- Установка Git, Node.js, Gulp и Python.
- Установите hello Azure командной строки (CLI Azure). 

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Из этого урока вы узнаете:

- Как tooinstall [Git](https://git-scm.com/) и [Node.js](https://nodejs.org/en/).
  - Git — это распределенная система управления версиями с открытым кодом. Пример приложения Hello на этом занятии будет храниться на Git.
  - Node.js — это среда выполнения JavaScript, характеризующаяся экосистемой пакета с широкими возможностями.
- Как toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.
  - Минимальная требуемая версия Hello Node.js — 4,5 LTS.
  - NPM является одним из диспетчеров пакетов приветствия для Node.js.
- Как tooinstall кода Visual Studio.
  - Visual Studio Code — это упрощенный кроссплатформенный, но мощный редактор исходного кода для платформ Windows, Linux и macOS. Он поддерживает возможности отладки, выделения синтаксиса, интеллектуального автозавершения кода, встроенные элементы управления Git, фрагменты кода, а также возможности рефакторинга кода.
- Как tooinstall Python.
  - Python — это широко используемый высокоуровневый интерпретируемый и динамический язык программирования общего назначения.
- Как tooinstall hello Azure CLI.
  - Hello Azure CLI обеспечивает многоплатформенного командной строки для Azure. Работа непосредственно из tooprovision командной строки и управления ресурсами.
- Как toouse hello Azure CLI toocreate центр IoT.

## <a name="what-you-need"></a>Необходимые элементы

- Toodownload подключения Internet hello средств и программного обеспечения.
- Компьютер Mac под управлением OS X Yosemite (10.10) или более поздней версии.

## <a name="install-git-and-nodejs"></a>Установка Git и Node.js

tooinstall Git и Node.js, используйте программу управления пакетов Homebrew hello, выполните следующие действия:

1. [Скачайте](http://brew.sh/) и установите Homebrew. Если Homebrew уже установлен, воспользуйтесь toostep 2.
   1. Нажмите клавишу `Cmd + Space` и введите `Terminal` tooopen терминала.
   2. Выполните следующую команду hello.

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. Установите Git и Node.js, выполнив следующую команду hello:

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a>Установка инструментов разработки Node.js

Вы используете [gulp.js](http://gulpjs.com/) tooautomate развертывания и выполнения скриптов.

gulp tooinstall, запустите следующую команду в терминале hello hello:

```bash
npm install -g gulp
```

При возникновении проблем с установкой hello. в разделе hello [руководство по устранению неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md) для решения проблемы toocommon.

> [!Note]
> Узел, NPM и Gulp являются необходимые toorun сценариев автоматизации, разработанные в Node.js.

## <a name="install-python"></a>Установка Python

Несмотря на то что Mac OS X поставляется с версией Python 2.7, мы рекомендуем установить Python через Homebrew. Ознакомьтесь со статьей [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Установка Python на Mac OS X).

Установите Python и pip, выполнив следующую команду hello:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Установка hello Azure CLI

tooinstall hello Azure CLI, выполните следующие действия.

1. Выполните следующие команды в терминале hello hello.
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   Hello установки может потребоваться 5 минут.

2. Проверка установки hello, выполнив следующую команду hello:
   ```bash
   az iot -h
   ```
   Вы увидите следующее hello выходных данных, если hello успешно установлен.

   ![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a>Установка Visual Studio Code

Использование кода Visual Studio в файлах конфигурации учебника tooedit hello в более поздней версии.

[Скачайте](https://code.visualstudio.com/docs/setup/osx) и установите Visual Studio Code.

## <a name="summary"></a>Сводка

Вы установили все необходимые hello средств и программного обеспечения на компьютере Mac. Следующая задача является toouse hello Azure CLI toocreate центр IoT и зарегистрировать устройство в концентратор IoT.

## <a name="next-steps"></a>Дальнейшие действия
[Создание Центра Интернета вещей и регистрация устройства](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
