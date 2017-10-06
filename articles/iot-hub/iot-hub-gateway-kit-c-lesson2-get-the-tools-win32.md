---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 2. Получение инструментов (Windows) | Документация Майкрософт"
description: "Установите на главный компьютер под управлением Windows hello средств и программного обеспечения hello, создать центр IoT и зарегистрировать устройство в центре IoT hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "разработка для Интернета вещей, облачная служба Интернета вещей, программное обеспечение Интернета вещей, Azure CLI, ПО Интернета вещей, установка git в Windows, запуск инструмента Gulp, установка Node.js в Windows, установка Npm в Windows, установка Python в Windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3b30b60a0115413394992061a88dde4cd442ac19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a>Получить средства hello (Windows 7 и более поздние версии)
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
- Компьютер Windows.

## <a name="install-git-and-nodejs"></a>Установка Git и Node.js

Щелкните следующие ссылки toodownload hello и установите Git и LTS Node.js для Windows.

- [Скачать Git для Windows](https://git-scm.com/download/win/)
- [Скачать Node.js LTS для Windows](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Установка инструментов разработки Node.js

Вы используете [gulp.js](http://gulpjs.com/) tooautomate развертывания и выполнения скриптов.

Нажмите клавишу `Windows + R`, тип `cmd` и нажмите клавишу `Enter` tooopen окно командной строки и затем выполнения hello следующую команду:

```cmd
npm install -g gulp
```

При возникновении проблем с установкой hello. в разделе hello [руководство по устранению неполадок](iot-hub-gateway-kit-c-troubleshooting.md) для решения проблемы toocommon.

> [!Note]
> Узел, NPM и Gulp являются необходимые toorun сценариев автоматизации, разработанные в Node.js.

## <a name="install-python"></a>Установка Python

Вы можете выбрать одну из следующих версий Python: 2.7, 3.4 или 3.5. В этом руководстве мы используем Python 2.7. Если python уже установлен, перейдите следующему разделу toohello.

[Скачать Python для Windows](https://www.python.org/downloads/)

Необходимо также tooadd hello путь к папкам hello, где Python.exe и pip.exe — установленных toohello системы `PATH` переменной среды. По умолчанию файл python.exe устанавливается в папку `C:\Python27`, а pip.exe — в `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Установка hello Azure CLI

tooinstall hello Azure CLI, выполните следующие действия.

1. Откройте окно командной строки с правами администратора.

2. Установите hello Azure CLI, выполнив следующие команды hello:

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   Hello установки может потребоваться 5 минут.

3. Проверка установки hello, выполнив следующую команду hello:

   ```cmd
   az iot -h
   ```

   Вы увидите следующее hello выходных данных, если hello успешно установлен.

   ![Проверка установки Azure CLI](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Установка Visual Studio Code

Использование кода Visual Studio в файлах конфигурации учебника tooedit hello в более поздней версии.

[Скачайте](https://code.visualstudio.com/docs/setup/windows) и установите Visual Studio Code.

## <a name="summary"></a>Сводка

Вы установили все необходимые hello средств и программного обеспечения на главный компьютер. Следующая задача является toouse hello Azure CLI toocreate центр IoT и зарегистрировать устройство в концентратор IoT.

## <a name="next-steps"></a>Дальнейшие действия
[Создание Центра Интернета вещей и регистрация устройства](iot-hub-gateway-kit-c-lesson2-register-device.md)
