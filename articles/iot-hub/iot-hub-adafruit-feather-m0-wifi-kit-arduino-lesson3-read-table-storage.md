---
title: "Connect Arduino (C) tooAzure IoT — занятия 3: хранилище таблиц | Документы Microsoft"
description: "Они записываются в хранилище таблиц Azure tooyour наблюдать за сообщений hello устройства в облако."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облако hello, сбор данных облака, iot облачной службы, iot данных"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Чтение сообщений, сохраненных в службе хранилища Azure
## <a name="what-you-will-do"></a>Выполняемая задача
Монитор hello устройства в облако сообщений, отправляемых из вашего центра IoT Adafruit Растушевка M0 Wi-Fi Arduino tooyour плата как сообщений hello записываются tooyour хранилище таблиц Azure.

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете, как toouse hello gulp задачи чтения сообщений tooread сообщения сохраняются в хранилище таблиц Azure.

## <a name="what-you-need"></a>Необходимые элементы
Прежде чем запустить этот процесс, необходимо успешно выполнить [запустить пример приложения hello Azure blink на доске Arduino][run-blink-application].

## <a name="read-new-messages-from-your-storage-account"></a>Чтение новых сообщений из учетной записи хранения
В предыдущей статье hello на доске Arduino запуска примера приложения. Пример приложения Hello отправлено центр Azure IoT tooyour сообщений. Центр IoT tooyour сообщения Hello хранятся в хранилище таблиц Azure через приложение Azure функции hello. Вы должны сообщений tooread строку соединения хранения Azure hello от хранилища таблиц Azure.

tooread сообщения, хранящиеся в хранилище таблиц Azure, выполните следующие действия.

1. Получите строку подключения hello, выполнив следующие команды hello:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Первая команда Hello получает hello `storage name` , используемый в hello второй команды tooget hello строки подключения. Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.
2. Привет открыть файл конфигурации `config-arduino.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. Замените `[Azure storage connection string]` со строкой подключения hello, полученный на шаге 1.
4. Сохранить hello `config-arduino.json` файла.
5. Попытку отправки сообщений и их чтения из хранилища таблиц Azure, выполнив следующую команду hello:

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   Hello логику для чтения из хранилища Azure таблицы находится в hello `azure-table.js` файла.

   ![gulp run --read-storage][gulp-run]

## <a name="summary"></a>Сводка
Вы успешно подключен концентратор IoT tooyour Arduino платы в облаке hello и использовать сообщения hello blink образец приложения toosend устройства в облако. Можно также использовать hello Azure функция приложения toostore входящих IoT hub сообщения tooyour хранилище таблиц Azure. Теперь можно отправлять сообщения облака на устройство из вашего tooyour концентратора IoT Arduino платы.

## <a name="next-steps"></a>Дальнейшие действия
[Отправка сообщений из облака на устройство][send-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md