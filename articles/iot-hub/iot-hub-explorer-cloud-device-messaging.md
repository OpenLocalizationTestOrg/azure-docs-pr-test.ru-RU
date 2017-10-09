---
title: "aaaManage центр IoT Azure облака устройство обмен сообщениями с центром IOT explorer | Документы Microsoft"
description: "Узнайте, как toouse hello центром IOT explorer CLI средство toomonitor устройства toocloud (D2C) сообщений и отправки сообщений toodevice (C2D) облака в Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "облако центром IOT обозревателе облака устройство обмена сообщениями, toodevice облака концентратора iot, toodevice обмена сообщениями"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Используйте обозреватель центром IOT toosend и получения сообщений между устройством и центр IoT

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

В [обозревателе Центра Интернета вещей](https://github.com/azure/iothub-explorer) доступно несколько команд, которые упрощают управление Центром Интернета вещей. Этот учебник содержит сведения о toosend explorer центром IOT toouse и получения сообщений между устройством и концентратор IoT.

## <a name="what-you-will-learn"></a>Новые знания

Вы узнаете, как toouse explorer центром IOT toomonitor устройства в облако и toosend сообщений облака на устройство. Сообщения из устройства в облако может быть датчиков, устройство собирает и затем отправляет tooyour центр IoT. Сообщения облака на устройство может быть команды концентратор IoT отправляет tooblink tooyour устройства Индикатор, tooyour подключенных устройств.

## <a name="what-you-will-do"></a>Выполняемая задача

- С помощью обозревателя с центром IOT toomonitor устройства в облако сообщений.
- С помощью обозревателя с центром IOT toosend облака на устройство сообщений.

## <a name="what-you-need"></a>Необходимые элементы

- Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:
  - Активная подписка Azure.
  - Центр Интернета вещей Azure в подписке;
  - Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.
- Обозреватель Центра Интернета вещей. ([Установить обозреватель Центра Интернета вещей](https://github.com/azure/iothub-explorer).)

## <a name="monitor-device-to-cloud-messages"></a>Отслеживание сообщений, отправляемых с устройства в облако

toomonitor сообщений, отправленных из tooyour IoT hub устройства, выполните следующие действия.

1. Откройте окно консоли.
1. Выполните следующую команду hello.

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > Получите `<device-id>` и `<IoTHubConnectionString>` из Центра Интернета вещей. Убедитесь, что после завершения предыдущего учебника hello. Или можно попробовать toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` при наличии `HostName`, `SharedAccessKeyName` и `SharedAccessKey`.

## <a name="send-cloud-to-device-messages"></a>Отправка сообщений из облака на устройство

toosend сообщения с устройства tooyour IoT hub, выполните следующие действия.

1. Откройте окно консоли.
1. Запуск сеанса на концентратор IoT, выполнив следующую команду hello:

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Отправьте сообщение tooyour устройства, выполнив следующую команду hello:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

Команда Hello мигает hello Индикатор, tooyour подключенных устройств и отправляет устройства tooyour сообщение hello.

> [!Note]
> Нет необходимости для hello устройства toosend концентратор IoT задней tooyour команда отдельные ack при получении сообщения hello.

## <a name="next-steps"></a>Дальнейшие действия

Вы узнали, как сообщения и отправлять сообщения облака на устройство между устройствами IoT и центр IoT Azure toomonitor устройства в облако.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
