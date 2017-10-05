---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Урок 3. Запуск примера | Документация Майкрософт"
description: "Развертывание и запуск на устройстве Raspberry Pi 3 примера приложения, которое отправляет сообщения в Центр Интернета вещей и заставляет светодиодный индикатор мигать."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "мигающий светодиодный индикатор облако pi, мигающий индикатор из облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e583ba455a94f9afcc7b31e49425b518d7968919
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Запуск примера приложения для отправки сообщений с устройства в облако
## <a name="what-you-will-do"></a>Выполняемая задача
В этой статье показано, как развернуть и запустить на устройстве Raspberry Pi 3 пример приложения, которое отправляет сообщения в Центр Интернета вещей. Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
Вы узнаете, как с помощью средства Gulp развернуть и запустить пример приложения Node.js на устройстве Pi.

## <a name="what-you-need"></a>Необходимые элементы
* К выполнению этой задачи следует приступать только после выполнения действий, описанных в статье [Create an Azure function app and an Azure Storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) (Создание приложения-функции Azure и учетной записи хранения Azure для обработки и хранения сообщений Центра Интернета вещей).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Получение строк подключения Центра Интернета вещей и устройства
Строка подключения устройства используется устройством Pi для подключения к Центру Интернета вещей. Строка подключения Центра Интернета вещей используется для подключения к реестру удостоверений в Центре Интернета вещей, чтобы управлять устройствами, которым разрешено подключаться к этому центру. 

* Для вывода списка всех Центров Интернета вещей в группе ресурсов выполните следующую команду Azure CLI:

```bash
az iot hub list -g iot-sample --query [].name
```

Используйте `iot-sample` в качестве значения `{resource group name}`, если вы не меняли это значение.

* Для получения строки подключения Центра Интернета вещей выполните следующую команду интерфейса командной строки Azure:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}` — это имя, которое вы указали при создании Центра Интернета вещей и регистрации устройства Pi.

* Для получения строки подключения устройства выполните следующую команду:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Используйте `myraspberrypi` в качестве значения `{device id}`, если вы не меняли это значение.

## <a name="configure-the-device-connection"></a>Настройка подключения устройства
1. Запустите файл конфигурации, выполнив приведенную ниже команду.
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> Выполните также **gulp install-tools**, если это не было сделано на уроке 1.

2. Откройте файл конфигурации устройства `config-raspberrypi.json` в Visual Studio Code, выполнив приведенную ниже команду.
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. В файле `config-raspberrypi.json` выполните следующие замены.
   
   * Замените **[device hostname or IP address]** IP-адресом или именем узла устройства, полученным в результате выполнения команды `device-discovery-cli`, или значением, унаследованным из настроек устройства.
   * Замените **[строка подключения устройства Интернета вещей]** на полученное значение `device connection string`.
   * Замените **[IoT hub connection string]** (строка подключения Центра Интернета вещей) полученным значением `iot hub connection string`.

> [!NOTE]
> В этой статье не требуется `azure_storage_connection_string`. Оставьте эту настройку без изменений.

Обновите файл `config-raspberrypi.json`, чтобы можно было развернуть пример приложения с компьютера.

## <a name="deploy-and-run-the-sample-application"></a>Развертывание и запуск примера приложения
Разверните и запустите пример приложения на устройстве Pi, выполнив следующую команду.

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a>Проверка работы примера приложения
Светодиодный индикатор, подключенный к устройству Pi, должен мигать с частотой в две секунды. Каждый раз, когда индикатор мигает, пример приложения отправляет сообщение в Центр Интернета вещей и проверяет, что сообщение успешно отправлено. Кроме того, каждое сообщение, полученное Центром Интернета вещей, выводится в окне консоли. Пример приложения автоматически завершает работу после отправки 20 сообщений.

![Пример приложения с отправленными и полученными сообщениями](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a>Сводка
Вы развернули и запустили новый пример приложения для включения индикатора на устройстве Pi для отправки сообщений с устройства в облако, то есть в Центр Интернета вещей. Теперь можно отслеживать сообщения по мере их записывания в учетную запись хранения.

## <a name="next-steps"></a>Дальнейшие действия
[Чтение сообщений, сохраненных в службе хранилища Azure](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

