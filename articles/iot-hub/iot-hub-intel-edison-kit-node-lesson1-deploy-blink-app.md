---
title: "Подключение Intel Edison (Node) к Интернету вещей Azure. Урок 1. Развертывание приложения | Документация Майкрософт"
description: "Клонируйте пример приложения C c GitHub и разверните его с помощью инструмента Gulp на плате Intel Edison. Это приложение будет каждые две секунды включать и выключать светодиодный индикатор на компьютере."
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
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>Создание и развертывание приложения для включения индикатора
## <a name="what-you-will-do"></a>Выполняемая задача
Клонирование примера приложения C из GitHub и его развертывание с помощью инструмента Gulp на устройстве Intel Edison. Этот пример приложения будет каждые две секунды включать светодиодный индикатор, подключенный к плате. Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
* Как развертывать и запускать пример приложения в Edison.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить следующие операции:

* [Настройка устройства][configure-your-device]
* [Get the tools][get-the-tools] (Получение инструментов)

## <a name="open-the-sample-application"></a>Открытие примера приложения
Чтобы открыть пример приложения, сделайте следующее:

1. Клонируйте пример репозитория из GitHub, выполнив следующую команду.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Откройте пример приложения в Visual Studio Code, выполнив следующие команды:

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Структура репозитория][repo-structure]

Файл в подпапке `app` — это ключевой исходный файл, содержащий код для управления светодиодным индикатором.

### <a name="install-application-dependencies"></a>Установка зависимостей приложения
Установите библиотеки и другие модули, необходимые для примера приложения, выполнив следующую команду:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>Настройка подключения устройства
Чтобы настроить подключение устройства, выполните следующие действия.

1. Создайте файл конфигурации устройства, выполнив приведенную ниже команду.

   ```bash
   gulp init
   ```

   Файл конфигурации `config-edison.json` содержит учетные данные пользователя для входа в Edison. Чтобы избежать утечки учетных данных пользователя, файл конфигурации создается в подпапке `.iot-hub-getting-started` домашней папки на компьютере.

2. Откройте файл конфигурации устройства в Visual Studio Code, выполнив приведенную ниже команду.

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Замените заполнитель `[device hostname or IP address]` и `[device password]` на IP-адрес и пароль, указанный на предыдущем уроке.

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Поздравляем! Вы успешно создали пример приложения для платы Edison.

## <a name="deploy-and-run-the-sample-application"></a>Развертывание и запуск примера приложения

### <a name="deploy-and-run-the-sample-app"></a>Развертывание и запуск примера приложения
Разверните и запустите пример приложения, выполнив следующую команду.

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a>Проверка работы приложения
После того, как светодиодный индикатор мигнет 20 раз, пример приложения завершит работу автоматически. Если светодиодный индикатор не мигает, см. способы решения распространенных проблем в [руководстве по устранению неполадок][troubleshooting].

![Светодиодный индикатор мигает][led-blinking]

## <a name="summary"></a>Сводка
Вы установили необходимые инструменты для работы с устройством Edison и развернули пример приложения, заставляющего светодиодный индикатор мигать. Теперь можно приступать к созданию, развертыванию и запуску другого примера приложения, которое подключает устройство Edison к Центру Интернета вещей Azure для отправки и получения сообщений.

## <a name="next-steps"></a>Дальнейшие действия
[Get the Azure tools][get-the-azure-tools] (Получение инструментов Azure)

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
