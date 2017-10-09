---
title: "Connect Intel Edison (C) tooAzure IoT — занятия 3: отправка сообщений | Документы Microsoft"
description: "Развертывание и запуск образца приложения tooIntel Edison, отправляет сообщения центр IoT tooyour и hello Индикатор мигает."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT облачной службы, arduino отправки данных toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 83615335027cc792b89d3894578fc3f7a55e5c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Запустите образец приложения toosend сообщения из устройства в облако
## <a name="what-you-will-do"></a>Выполняемая задача
В этой статье показано, как toodeploy и выполнение примера приложения на Edison Intel, который отправляет сообщения tooyour центр IoT. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
Будет узнать, как toouse hello gulp toodeploy средства и запустите приложение C образец hello на Edison.

## <a name="what-you-need"></a>Необходимые элементы
* Прежде чем начать эту задачу, необходимо успешно выполнить [создания приложения Azure функции и концентратор IoT tooprocess и хранилище учетной записи хранилища сообщений][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Получение строк подключения Центра Интернета вещей и устройства
Строка подключения устройства Hello — используется tooconnect Edison tooyour IoT hub. Здравствуйте, строка подключения концентратора IoT является используется tooconnect вашей IoT hub toohello удостоверение устройства, представляющий Edison в центр IoT hello.

* Перечислить все центры IoT в группе ресурсов, выполнив следующую команду Azure CLI hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.

* Получите строку подключения концентратора IoT hello, выполнив следующую команду Azure CLI hello:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`— Имя hello, указанный вами создали концентратор IoT при регистрации Edison.

* Получите строку подключения устройства hello, выполнив следующую команду hello:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

Используйте `myinteledison` в качестве значения hello `{device id}` Если вы не изменили значение hello.

## <a name="configure-hello-device-connection"></a>Настройка подключения устройства hello
1. Инициализируйте hello файл конфигурации, выполнив следующие команды hello:

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > Выполните также **gulp install-tools**, если это не было сделано на уроке 1.

2. Файл конфигурации устройства Привет открыть `config-edison.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. Сделать после замены в hello hello `config-edison.json` файла:

   * Замените **[устройства имя узла или IP-адрес]** с IP-адрес устройства hello помечен работу при настройке устройства.
   * Замените **[строка подключения устройств IoT]** с hello `device connection string` полученных.
   * Замените **[строка подключения концентратора IoT]** с hello `iot hub connection string` полученных.

   > [!NOTE]
   > В этой статье не требуется `azure_storage_connection_string`. Оставьте эту настройку без изменений.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на Edison, выполнив следующую команду hello:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Проверка работы образца приложения hello
Вы увидите hello Индикатор, подключенных tooEdison мигает каждые две секунды. Каждый раз hello Индикатор мигает, пример приложения hello отправляет центр IoT tooyour сообщения и подтверждает, что это сообщение hello было успешно отправлено tooyour центр IoT. Кроме того каждое сообщение, полученных центра IoT hello выводится в окне консоли hello. Пример приложения Hello автоматически завершает после отправки 20 сообщений.

![Пример приложения с отправленными и полученными сообщениями][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Сводка
Развертывания и запустите hello новый образец приложения blink Edison центр IoT tooyour toosend сообщения из устройства в облако. Теперь отслеживать сообщения, записываемые toohello учетной записи хранилища.

## <a name="next-steps"></a>Дальнейшие действия
[Чтение сообщений, сохраненных в службе хранилища Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md