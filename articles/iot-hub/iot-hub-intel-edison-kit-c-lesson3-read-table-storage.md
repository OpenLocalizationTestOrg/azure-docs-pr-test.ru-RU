---
title: "Connect Intel Edison (C) tooAzure IoT — занятия 3: наблюдения за сообщениями | Документы Microsoft"
description: "Они записываются в хранилище таблиц Azure tooyour наблюдать за сообщений hello устройства в облако."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "данные в облако hello, сбор данных облака, iot облачной службы, iot данных"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2679b22f2987f77ecd1eea03044ed8ea03bf73f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a>Чтение сообщений, сохраненных в службе хранилища Azure
## <a name="what-you-will-do"></a>Выполняемая задача
Монитор hello устройства в облако сообщения, которые отправляются из центра IoT tooyour Intel Edison в виде сообщений hello записываются tooyour хранилище таблиц Azure. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
В этой статье вы узнаете, как toouse hello gulp задачи чтения сообщений tooread сообщения сохраняются в хранилище таблиц Azure.

## <a name="what-you-need"></a>Необходимые элементы
Прежде чем запустить этот процесс, необходимо успешно выполнить [проведение пример приложения hello Azure blink Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].

## <a name="read-new-messages-from-your-storage-account"></a>Чтение новых сообщений из учетной записи хранения
В предыдущей статье hello выполнена образец приложения для Edison. Пример приложения Hello отправлено центр Azure IoT tooyour сообщений. Центр IoT tooyour сообщения Hello хранятся в хранилище таблиц Azure через приложение Azure функции hello. Вы должны сообщений tooread строку соединения хранения Azure hello от хранилища таблиц Azure.

tooread сообщения, хранящиеся в хранилище таблиц Azure, выполните следующие действия.

1. Получите строку подключения hello, выполнив следующие команды hello:

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   Первая команда Hello получает hello `storage name` , используемый в hello второй команды tooget hello строки подключения. Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.
2. Привет открыть файл конфигурации `config-edison.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. Замените `[Azure storage connection string]` со строкой подключения hello, полученный на шаге 1.
4. Сохранить hello `config-edison.json` файла.
5. Попытку отправки сообщений и их чтения из хранилища таблиц Azure, выполнив следующую команду hello:

   ```bash
   gulp run --read-storage
   ```

   Hello логику для чтения из хранилища Azure таблицы находится в hello `azure-table.js` файла.

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a>Сводка
Вы успешно подключен центра IoT tooyour Edison в облаке hello и использовать сообщения hello blink образец приложения toosend устройства в облако. Можно также использовать hello Azure функция приложения toostore входящих IoT hub сообщения tooyour хранилище таблиц Azure. Теперь можно отправлять сообщения облака на устройство из вашего tooEdison концентратора IoT.

## <a name="next-steps"></a>Дальнейшие действия
[Запустите образец приложения tooreceive сообщений облака на устройство][receive-cloud-to-device-messages]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md