---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 4. Хранилище таблиц | Документация Майкрософт"
description: "Сохраняйте сообщения из Intel NUC в Центр Интернета вещей, записывайте их в Хранилище таблиц Azure, а затем читайте их из облака."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "получить данные из облака, облачная служба Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: de5fae794c195132e2a487c0095845c756aa28e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a>Чтение сообщений, сохраненных в Хранилище таблиц Azure

## <a name="what-you-will-do"></a>Выполняемая задача

- Запуск примера приложения шлюза для шлюза, который отправляет сообщения в Центр Интернета вещей.
- Запустите пример кода на главном компьютере для чтения сообщений в Хранилище таблиц Azure.

Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания

Использование инструмента Gulp для чтения сообщений в Хранилище таблиц Azure.

## <a name="what-you-need"></a>Необходимые элементы

Вы успешно выполнили следующие задачи:

- [Создание приложения-функции Azure и учетной записи хранения Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)
- [Запуск примера приложения шлюза](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)
- [Чтение сообщений из Центра Интернета вещей](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)

## <a name="get-your-azure-storage-connection-strings"></a>Получение строк подключения службы хранилища Azure

Раньше в ходе этого урока вы успешно создали учетную запись хранения Azure. Чтобы получить строку подключения учетной записи хранения Azure, выполните следующие команды:

* Выведите список всех учетных записей хранения.

```bash
az storage account list -g iot-gateway --query [].name
```

* Получите строку подключения к службе хранилища Azure.

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

Используйте `iot-gateway` в качестве значения `{resource group name}`, если в уроке 2 значение не изменялось.

## <a name="configure-the-device-connection"></a>Настройка подключения устройства

Обновите файл `config-azure.json`, чтобы пример кода, который выполняется на главном компьютере, смог читать сообщения в Хранилище таблиц Azure. Чтобы настроить подключение устройства, выполните следующие действия.

1. Откройте файл конфигурации устройства `config-azure.json`, выполнив следующие команды:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![Конфигурация](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. Замените `[Azure storage connection string]` полученной строкой подключения к службе хранилища Azure.

   `[IoT hub connection string]` уже должна быть заменена в разделе [Чтение сообщений из Центра Интернета вещей Azure](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) в уроке 3.

## <a name="read-messages-in-your-azure-table-storage"></a>Чтение сообщений в Хранилище таблиц Azure

Запустите пример приложения шлюза и прочтите сообщения Хранилища таблиц Azure, выполнив следующую команду:

```bash
gulp run --table-storage
```

Ваш Центр Интернета вещей активирует приложение-функцию Azure, чтобы сохранить сообщение в Хранилище таблиц Azure при поступлении нового сообщения.
Команда `gulp run` запускает пример приложения шлюза, который отправляет сообщения в Центр Интернета вещей. С помощью параметра `table-storage` она также создает дочерний процесс для получения сохраненного сообщения в Хранилище таблиц Azure.

Все отправленные и полученные сообщения мгновенно появляются в том же окне консоли на главном компьютере. Экземпляр примера приложения прекращает свое действие автоматически через 40 секунд.

   ![чтение Gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a>Сводка

Вы запустили пример кода для чтения сообщений в Хранилище таблиц Azure, сохраненных приложением-функцией Azure.
