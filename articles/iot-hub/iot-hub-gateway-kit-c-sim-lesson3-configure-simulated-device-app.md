---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 3. Запуск примера приложения | Документация Майкрософт"
description: "Запустить имитированное устройство образец приложения toosend температуры данных tooyour центра IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "toocloud данных"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Настройка и запуск примера приложения для имитации устройства

## <a name="what-you-will-do"></a>Выполняемая задача

- Репозиторий образец hello клона.
- Используйте hello Azure CLI tooget центр IoT и сведения о логических устройств для устройств, имитация образца приложения. Настроить и запустить пример приложения hello имитируемые устройства.

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

В этой статье вы узнаете следующее:

- Как tooconfigure и выполнения hello имитировать образец приложения для устройства.

## <a name="what-you-need"></a>Необходимые элементы

Необходимо успешно выполнить инструкции, изложенные в следующих статьях:

- [Создание Центра Интернета вещей и регистрация устройства](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Клон образец hello репозитория toohello главного компьютера

репозиторий образец hello tooclone, выполните следующие действия на главном компьютере hello:

1. Откройте командную строку в Windows или окно терминала в МacOS или Ubuntu.
2. Выполните следующие команды hello.

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>Настройка устройств, имитация hello и вашей NUC

1. Привет открыть файл конфигурации `config.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   code config.json
   ```

2. Замените `"has_sensortag": true` на `"has_sensortag": false`:

   ![конфигурация, нет устройства TI SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Инициализируйте hello файл конфигурации, выполнив следующие команды hello:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Откройте `config-gateway.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Найдите следующие строки кода hello и замените `[device hostname or IP address]` с IP-адрес или имя hello Intel NUC.
   ![снимок экрана настройки шлюза](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>Получить строку подключения hello логического устройства концентратора IoT

hello tooget строка подключения концентратора Azure IoT логического устройства, запустите следующую команду на главном компьютере hello hello:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`— Имя концентратора IoT hello, который использовался. Iot шлюз можно использовать в качестве значения hello `{resource group name}` и использовать в качестве значения hello mydevice `{device id}` Если вы не изменили значение hello в занятии 2.

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>Настройка hello имитируемые устройства облака передачи образца приложения

tooconfigure и выполнения hello имитируемые устройства облако загрузить пример приложения, выполните следующие действия на главном компьютере hello:

1. Откройте `config-sensortag.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![снимок экрана настройки SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Внесите hello после замены в коде hello.
   - Замените `[IoT hub name]` с именем концентратора IoT hello.
   - Замените `[IoT device connection string]` со строкой hello подключения логического устройства концентратора IoT.

3. Запустите приложение hello.

   Развертывание и запуск приложения hello, выполнив следующую команду hello:

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>Проверка работы приложения образца hello

Теперь вы увидите выходные данные hello следующим образом:

![выходные данные примера приложения для имитации устройства](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

приложение Hello отправляет температуры данных tooyour IoT hub, который длится 40 секунд.

## <a name="summary"></a>Сводка

Успешной настройки и выполнения hello имитируемые устройства облака загрузки примера приложения, которое отправляет центр IoT tooyour данных с устройств, имитация.

## <a name="next-steps"></a>Дальнейшие действия
[Чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)