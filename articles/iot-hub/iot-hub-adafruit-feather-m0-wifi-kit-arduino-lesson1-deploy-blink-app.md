---
title: "Подключение Arduino к Интернету вещей Azure. Урок 1. Развертывание приложения | Документация Майкрософт"
description: "Клонируйте пример приложения Arduino из Github и разверните его с помощью инструмента Gulp на плате Adafruit Feather M0 WiFi. Этот пример приложения включает и отключает GPIO"
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
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>Создание и развертывание приложения для включения индикатора
## <a name="what-you-will-do"></a>Выполняемая задача
Клонируйте пример приложения Arduino для включения индикатора из Github и разверните его с помощью средства Gulp на плате Adafruit Feather M0 WiFi Arduino. Этот пример приложения будет каждые две секунды включать встроенный светодиодный индикатор GPIO #13.

Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок][troubleshooting-page].

## <a name="what-you-will-learn"></a>Новые знания
* Как развертывать и запускать пример приложения на плате Arduino.

## <a name="what-you-need"></a>Необходимые элементы
Необходимо успешно выполнить следующие операции:

* [Настройка устройства][configure-your-device]
* [Get the tools][get-the-tools] (Получение инструментов)

## <a name="open-the-sample-application"></a>Открытие примера приложения
Чтобы открыть пример приложения, сделайте следующее:

1. Клонируйте пример репозитория из GitHub, выполнив следующую команду.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Откройте пример приложения в Visual Studio Code, выполнив следующие команды:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Структура репозитория][repo-structure]

Файл `app.ino` в подпапке `app` — это ключевой исходный файл, содержащий код для управления светодиодным индикатором.

### <a name="install-application-dependencies"></a>Установка зависимостей приложения
Установите библиотеки и другие модули, необходимые для примера приложения, выполнив следующую команду:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>Настройка подключения устройства
Чтобы настроить подключение устройства, выполните следующие действия.

1. Получите последовательный порт устройства, используя интерфейс командной строки обнаружения устройств:

   ```bash
   devdisco list --usb
   ```

   Вы должны увидеть результат, аналогичный приведенному ниже и найти COM-порт вашей платы Arduino:![Обнаружение устройства][device-discovery]

2. Откройте файл `config.json` в папке занятия и добавьте значение найденного номера COM-порта:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > Для COM-порта на платформе Windows он имеет формат `COM1, COM2, ...`. На macOS или Ubuntu он начинается с `/dev/`.

## <a name="deploy-and-run-the-sample-application"></a>Развертывание и запуск примера приложения
### <a name="install-the-required-tools-for-your-arduino-board"></a>Установка необходимых инструментов для платы Arduino

Установите пакет SDK для Центра Интернета вещей Azure для платы Arduino, выполнив следующую команду:

```bash
gulp install-tools
```

В зависимости от сетевого подключения для выполнения этой команды может потребоваться много времени.

> [!NOTE]
> Завершите работу экземпляра IDE Arduino при выполнении задач Gulp: `install-tools`, `run`.

### <a name="deploy-and-run-the-sample-app"></a>Развертывание и запуск примера приложения
Разверните и запустите пример приложения, выполнив следующую команду.

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a>Проверка работы приложения
Если светодиодный индикатор не мигает, см. способы решения распространенных проблем в [руководстве по устранению неполадок][troubleshooting-page].

![Светодиодный индикатор мигает][led-blinking]

## <a name="summary"></a>Сводка
Вы установили необходимые инструменты для работы с платой Arduino и развернули пример приложения, заставляющего светодиодный индикатор мигать. Теперь можно приступать к созданию, развертыванию и запуску другого примера приложения, которое подключает плату Arduino к Центру Интернета вещей Azure для отправки и получения сообщений.

## <a name="next-steps"></a>Дальнейшие действия
[Get the Azure tools][get-the-azure-tools] (Получение инструментов Azure)

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md