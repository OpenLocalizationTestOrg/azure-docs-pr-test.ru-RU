---
title: "Приступая к работе с устройством SensorTag и шлюзом Azure IoT. Урок 4. Хранилище таблиц | Документация Майкрософт"
description: "Сохранять сообщения из центра IoT tooyour Intel NUC, записывать их в хранилище таблиц tooAzure и затем прочитать их из облака hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "получить данные из облака, облачная служба Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Чтение сообщений, сохраненных в Хранилище таблиц Azure

## <a name="what-you-will-do"></a>Выполняемая задача

- Запустите образец приложения hello шлюза на шлюзе, отправляет сообщения tooyour IoT hub.
- Затем выполните пример кода на сообщения hello tooread компьютера узла в хранилище таблиц Azure. 

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Как toouse hello gulp средство toorun образец кода tooread сообщений hello в хранилище таблиц Azure.

## <a name="what-you-need"></a>Необходимые элементы

Будет иметь успешно hello следующие задания:

- [Создать приложение Azure функции hello и учетной записи хранилища Azure hello](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).
- [Запустить образец приложения hello шлюза](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).
- [Чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)

## <a name="get-your-azure-storage-connection-strings"></a>Получение строк подключения службы хранилища Azure

Раньше в ходе этого урока вы успешно создали учетную запись хранения Azure. Строка подключения tooget hello учетной записи хранилища Azure hello, запуска hello, следующие команды:

* Выведите список всех учетных записей хранения.

```bash
az storage account list -g iot-gateway --query [].name
```

* Получите строку подключения к службе хранилища Azure.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Iot шлюз можно использовать в качестве значения hello `{resource group name}` Если вы не изменили значение hello в занятии 2.

## <a name="configure-hello-device-connection"></a>Настройка подключения устройства hello

Обновление hello `config-azure.json` так, чтобы hello образец кода, который выполняется на главном компьютере hello можно прочитать сообщение в хранилище таблиц Azure. tooconfigure Здравствуйте подключения устройства, выполните следующие действия:

1. Файл конфигурации устройства Привет открыть `config-azure.json` , выполнив следующие команды hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![Конфигурация](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Замените `[Azure storage connection string]` с hello строка подключения хранилища Azure, который был получен.

   `[IoT hub connection string]` уже должна быть заменена в разделе [Чтение сообщений из Центра Интернета вещей Azure](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) в уроке 3.

## <a name="read-messages-in-your-azure-table-storage"></a>Чтение сообщений в Хранилище таблиц Azure

Запустить образец приложения hello шлюза и чтения сообщений хранилища таблиц Azure, hello следующую команду:

```bash
gulp run --table-storage
```

Сообщение toosave приложения Azure функция инициирует ваш центр IoT в хранилище таблиц Azure при поступлении нового сообщения.
Hello `gulp run` команда выполняет шлюза образец приложения, который отправляет сообщения tooyour IoT hub. С `table-storage` параметра, оно также создает hello tooreceive дочерних процесса, сохраненные сообщения в хранилище таблиц Azure.

сообщения приветствия, отправки и получения всех отображаемых мгновенно на hello же консоли окна в hello хост-компьютера. экземпляр приложения Образец Hello нарушит автоматически в 40 секунд.

   ![чтение Gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a>Сводка

После выполнения сообщений hello tooread кода образца hello в хранилище таблиц Azure сохранен приложением Azure функции.
