---
title: "Connect Arduino (C) tooAzure IoT — занятия 3: выполнение примера | Документы Microsoft"
description: "Развертывание и запуск образца приложения tooAdafruit Растушевка M0 Wi-Fi, отправляет сообщения центр IoT tooyour и hello Индикатор мигает."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "IOT облачной службы, arduino отправки данных toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Запустите образец приложения toosend сообщения из устройства в облако
## <a name="what-you-will-do"></a>Выполняемая задача
В этой статье показано, как toodeploy и выполнение примера приложения на ваш Adafruit Растушевка M0 Wi-Fi Arduino плата центра IoT tooyour, отправляет сообщения.

Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок][troubleshooting].

## <a name="what-you-will-learn"></a>Новые знания
Вы узнаете, как toouse hello gulp toodeploy средства и запустите приложение Arduino образец hello в Arduino на доске.

## <a name="what-you-need"></a>Необходимые элементы
* Прежде чем начать эту задачу, необходимо успешно выполнить [создания приложения Azure функции и концентратор IoT tooprocess и хранилище учетной записи хранилища сообщений][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Получение строк подключения Центра Интернета вещей и устройства
Здравствуйте, строка подключения устройства является используется tooconnect ваш центр IoT Arduino tooyour платы. Строка подключения концентратора IoT Hello — используется tooconnect вашей IoT hub toohello удостоверение устройства, представляющий вашей Arduino плата в центр IoT hello.

* Перечислить все центры IoT в группе ресурсов, выполнив следующую команду Azure CLI hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Используйте `iot-sample` в качестве значения hello `{resource group name}` Если вы не изменили значение hello.

* Получите строку подключения концентратора IoT hello, выполнив следующую команду Azure CLI hello:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`— hello имя, указанное при создании ваш центр IoT и зарегистрирован Arduino доске.

* Получите строку подключения устройства hello, выполнив следующую команду hello:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Используйте `mym0wifi` в качестве значения hello `{device id}` Если вы не изменили значение hello.
## <a name="configure-hello-device-connection"></a>Настройка подключения устройства hello
tooconfigure Здравствуйте подключения устройства, выполните следующие действия:

1. Получите hello последовательного порта hello устройства с cli обнаружения устройства hello.

   ```bash
   devdisco list --usb
   ```

   Должны видеть выходные данные, аналогичные следующие toohello и найти COM-порт hello usb плата Arduino:

   ![Обнаружение устройства][device-discovery]

2. Привет открыть файл `config.json` в hello папку занятия и добавьте значение hello hello, найти номер COM-порта:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > Для порта hello COM, на платформе Windows, он имеет формат hello `COM1, COM2, ...`. На macOS или Ubuntu он начинается с `/dev/`.

3. Инициализируйте hello файл конфигурации, выполнив следующие команды hello:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Файл конфигурации устройства Привет открыть `config-arduino.json` в коде Visual Studio, выполнив следующую команду hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. Сделать после замены в hello hello `config-arduino.json` файла:

   * Замените **[Wi-Fi SSID]** с вашей SSID Wi-Fi, подключенный toohello Интернета.
   * Замените **[Wi-Fi password]** своим паролем Wi-Fi. Удалите строку hello, если Wi-Fi не требует пароля.
   * Замените **[строка подключения устройств IoT]** с hello `device connection string` полученных.
   * Замените **[строка подключения концентратора IoT]** с hello `iot hub connection string` полученных.

   > [!NOTE]
   > В этой статье не требуется `azure_storage_connection_string`. Оставьте эту настройку без изменений.

## <a name="deploy-and-run-hello-sample-application"></a>Развертывание и запуск образца приложения hello
Развертывание и запуск образца приложения hello на доске Arduino, выполнив следующую команду hello:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Hello gulp задачи по умолчанию выполняется `install-tools` и `run` задачи последовательно. Когда вы [hello blink приложение развернуто][deployed-the-blink-app], выполнении этих задач отдельно.

## <a name="verify-that-hello-sample-application-works"></a>Проверка работы образца приложения hello
Вы увидите hello объект групповой ПОЛИТИКИ #0 встроенный Индикатор мигает. каждые две секунды. Каждый раз hello Индикатор мигает, пример приложения hello отправляет центр IoT tooyour сообщения и подтверждает, что это сообщение hello было успешно отправлено tooyour центр IoT. Кроме того каждое сообщение, полученных центра IoT hello выводится в окне консоли hello. Пример приложения Hello автоматически завершает после отправки 20 сообщений.

![Пример приложения с отправленными и полученными сообщениями][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Сводка
После развертывания и запустить hello новый blink пример приложения на концентратор IoT tooyour Arduino плата toosend сообщения из устройства в облако. Теперь отслеживать сообщения, записываемые toohello учетной записи хранилища.

## <a name="next-steps"></a>Дальнейшие действия
[Чтение сообщений, сохраненных в службе хранилища Azure][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md