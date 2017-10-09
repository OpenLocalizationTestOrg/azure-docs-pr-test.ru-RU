---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 3. Запуск примера приложения | Документация Майкрософт"
description: "Выполняются приложения tooreceive ЛЮЧИТЬ образец данных из SensorTag ЛЮЧИТЬ и концентратор IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "отключить приложение, датчик мониторинг приложения, сбор данных датчика, данные с помощью датчиков toocloud данных датчика"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Настройка и запуск примера приложения BLE

## <a name="what-you-will-do"></a>Выполняемая задача

- Репозиторий образец hello клона. 
- Настройте подключение hello между SensorTag и Intel NUC. 
- Используйте hello Azure CLI tooget центр IoT и SensorTag сведения образец приложения ЛЮЧИТЬ (низкий энергии Bluetooth). Настроить и запустить пример приложения hello отключить. 

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

В этой статье вы узнаете следующее:

- Как tooconfigure и выполнения hello ЛЮЧИТЬ образец приложения.

## <a name="what-you-need"></a>Необходимые элементы

Необходимо успешно выполнить инструкции, изложенные в следующих статьях:

- [Создание Центра Интернета вещей и регистрация SensorTag](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Клон образец hello репозитория toohello главного компьютера

репозиторий образец hello tooclone, выполните следующие действия на главном компьютере hello:

1. Откройте окно командной строки в Windows или терминала в macOS или Ubuntu.
2. Выполните следующие команды hello.

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>Настроить подключение hello между SensorTag и Intel NUC

tooset копирование hello подключения, выполните следующие действия на главном компьютере hello.

1. Инициализируйте hello файл конфигурации, выполнив следующие команды hello:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Откройте `config-gateway.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Найдите следующие строки кода hello и замените `[device hostname or IP address]` с hello IP-адрес или имя Intel NUC.
   ![снимок экрана настройки шлюза](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Установите средства поддержки на Intel NUC, выполнив следующую команду hello.

   ```bash
   gulp install-tools
   ```

5. Включите SensorTag нажатием кнопки питания hello как hello следующий рисунок и мигания hello зеленый Индикатор.

   ![включение SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. SensorTag устройств сканирования, выполнив следующие команды hello:

   ```bash
   gulp discover-sensortag
   ```

7. Проверка подключения hello между hello SensorTag и Intel NUC, выполнив следующую команду hello:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Замените `{mac address}` с MAC-адрес, полученный на предыдущем шаге hello hello.

## <a name="get-hello-connection-string-of-sensortag"></a>Получить строку подключения hello объекта SensorTag

hello tooget SensorTag, запустите следующую команду на главном компьютере hello hello строка подключения концентратора Azure IoT:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`— Имя концентратора IoT hello, который использовался. Iot шлюз можно использовать в качестве значения hello `{resource group name}` и использовать в качестве значения hello mydevice `{device id}` Если вы не изменили значение hello в занятии 2.

## <a name="configure-hello-ble-sample-application"></a>Настройка образца приложения hello ЛЮЧИТЬ

tooconfigure и выполнения hello ЛЮЧИТЬ образец приложения, выполните следующие действия на главном компьютере hello.

1. Откройте `config-sensortag.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![снимок экрана настройки SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Внесите hello после замены в коде hello.
   - Замените `[IoT hub name]` с именем концентратора IoT hello, который использовался.
   - Замените `[IoT device connection string]` со строкой соединения hello объекта SensorTag, который был получен.
   - Замените `[device_mac_address]` с hello hello SensorTag, полученный MAC-адрес.

3. Запустите образец приложения hello отключить.

   hello toorun ЛЮЧИТЬ образец приложения, выполните следующие действия на главном компьютере hello.

   1. Включите SensorTag.

   2. Развертывание и запуск образца приложения hello ЛЮЧИТЬ на Intel NUC, выполнив следующую команду hello:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Проверить, что пример приложения hello ЛЮЧИТЬ работает

Теперь вы увидите выходные данные hello следующим образом:

![выходные данные примера приложения BLE](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

Пример приложения Hello отслеживает сбор данных температуры и отправляет его tooyour центр IoT. Пример приложения Hello автоматически завершает после отправки 40 секунд.

## <a name="summary"></a>Сводка

Вы успешно настройки hello связи между SensorTag и Intel NUC и запустить образец приложения ЛЮЧИТЬ, который собирает и отправляет данные из центра IoT tooyour SensorTag. Вы будете готовы toolearn как tooverify концентратор IoT получила hello данных.

## <a name="next-steps"></a>Дальнейшие действия
[Чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)