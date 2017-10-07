---
title: "Подключение Raspberry Pi (узел) tooAzure IoT — занятия 3: выполнение примера | Документы Microsoft"
description: "Развертывание и запуск образца приложения tooRaspberry Pi 3, отправляет сообщения центр IoT tooyour и hello Индикатор мигает."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "мигающий светодиодный индикатор облако pi, мигающий индикатор из облака"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Запустите образец приложения toosend сообщения из устройства в облако
## <a name="what-you-will-do"></a>Выполняемая задача
В этой статье показано, как toodeploy и выполнение примера приложения на 3 Raspberry Pi, который отправляет сообщения tooyour центр IoT. Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Новые знания
Вы узнаете, как toouse hello gulp toodeploy средства и запустите приложение Node.js образец hello на Pi.

## <a name="what-you-need"></a>Необходимые элементы
* Прежде чем начать эту задачу, необходимо успешно выполнить [создания приложения Azure функции и концентратор IoT tooprocess и хранилище учетной записи хранилища сообщений](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Получение строк подключения Центра Интернета вещей и устройства
Строка подключения устройства Hello используется ваш центр IoT tooyour tooconnect Pi. Строка подключения концентратора IoT Hello — реестра удостоверений toohello tooconnect используется в вашей IoT hub toomanage hello устройства, которым разрешен центра IoT tooyour tooconnect. 

* Перечислить все центры IoT в группе ресурсов, выполнив следующую команду Azure CLI hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.

* Получите строку подключения концентратора IoT hello, выполнив следующую команду Azure CLI hello:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`— Имя hello, указанный вами создали концентратор IoT при регистрации Pi.

* Получите строку подключения устройства hello, выполнив следующую команду hello:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Используйте `myraspberrypi` в качестве значения hello `{device id}` Если вы не изменили значение hello.

## <a name="configure-hello-device-connection"></a>Настройка подключения устройства hello
1. Инициализируйте hello файл конфигурации, выполнив следующие команды hello:
   
   ```bash
   npm install
   gulp init
   ```
2. Файл конфигурации устройства Привет открыть `config-raspberrypi.json` в коде Visual Studio, выполнив следующую команду hello:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Сделать после замены в hello hello `config-raspberrypi.json` файла:
   
   * Замените **[устройства имя узла или IP-адрес]** hello IP адрес или имя устройства, полученный из `device-discovery-cli` или со значением hello наследуется при настройке устройства.
   * Замените **[строка подключения устройств IoT]** с hello `device connection string` полученных.
   * Замените **[строка подключения концентратора IoT]** с hello `iot hub connection string` полученных.

Обновление hello `config-raspberrypi.json` так, можно развернуть пример приложения hello с вашего компьютера.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на Pi, выполнив следующую команду hello:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Проверка работы образца приложения hello
Вы увидите hello Индикатор, подключенных tooPi мигает каждые две секунды. Каждый раз hello Индикатор мигает, пример приложения hello отправляет центр IoT tooyour сообщения и подтверждает, что это сообщение hello было успешно отправлено tooyour центр IoT. Кроме того каждое сообщение, полученных центра IoT hello выводится в окне консоли hello. Пример приложения Hello автоматически завершает после отправки 20 сообщений.

![Пример приложения с отправленными и полученными сообщениями](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>Сводка
Вы развертывания и запуска hello новый blink образца приложения-концентратора IoT tooyour Pi toosend сообщения из устройства в облако. Теперь можно отслеживать сообщения, записываемые toohello учетной записи хранилища.

## <a name="next-steps"></a>Дальнейшие действия
[Чтение сообщений, сохраненных в службе хранилища Azure](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

