---
title: "aaaAzure IoT управление устройствами с помощью обозревателя с центром IOT | Документы Microsoft"
description: "Используйте hello центром IOT-CLI анализатор для управления устройствами центра IoT Azure, непосредственные методы hello и параметры управления hello двойных требуемые свойства."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "управление устройствами Интернета вещей Azure, управление устройствами в Центре Интернета вещей Azure, управление устройствами, Интернет вещей, управление устройствами в Центре Интернета вещей"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Использование обозревателя Центра Интернета вещей для управления устройствами в Центре Интернета вещей Azure

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[обозреватель центром IOT](https://github.com/azure/iothub-explorer) является средством CLI, которое запускается на удостоверения устройства toomanage компьютера узла в реестре концентратора IoT. Поставляется со параметры управления, которые можно использовать tooperform различные задачи.

| Возможность управления          | Задача                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Прямые методы             | Перевести устройство действовать, такие как запуск и остановка отправки сообщений или перезагрузка устройства hello.                                        |
| Требуемые свойства двойников    | Перевести устройство в определенных состояниях, например установку toogreen Индикатор или задание телеметрии hello отправки too30 интервал в минутах.         |
| Сообщаемые свойства двойника   | Получить hello сообщил о состоянии устройства. Например устройство hello сообщает Индикатор мигает теперь приветствия.                                    |
| Теги двойников                  | Метаданные для конкретного устройства хранения в облаке hello. Здравствуйте, например, Торговый автомат расположение развертывания.                         |
| Получение сообщений из облака на устройство   | Отправьте уведомления tooa устройства. Например «это скорее всего toorain сегодня. Не забывайте о toobring зонтик.»              |
| Запросы двойника устройства        | Запрос tooretrieve близнецы все устройства с произвольной условиями, например указания hello устройств, которые доступны для использования. |

Более подробные сведения о различиях hello и рекомендации по использованию этих параметров см. в разделе [руководство связи устройства в облако](iot-hub-devguide-d2c-guidance.md) и [облака на устройство связи руководство](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Двойники устройств — это документы JSON, хранящие сведения о состоянии устройства (метаданные, конфигурации и условия). Центр IoT сохранение двойных устройства для каждого устройства, которое подключается tooit. Дополнительные сведения о двойниках устройства см. в статье [Начало работы с двойниками устройств](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>Что вы узнаете

Вы узнаете, как использовать обозреватель Центра Интернета вещей для работы с различными средствами на компьютере разработки.

## <a name="what-you-do"></a>В рамках этого руководства мы:

Запустим обозреватель Центра Интернета вещей, используя различные средства управления.

## <a name="what-you-need"></a>Необходимые элементы

- Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:
  - Активная подписка Azure.
  - Центр Интернета вещей Azure в подписке;
  - Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.
- Убедитесь, что устройство работает под управлением с hello клиентского приложения с помощью этого учебника.
- iothub-explorer. [Установите iothub-explorer](https://github.com/azure/iothub-explorer) на компьютер разработки.

## <a name="connect-tooyour-iot-hub"></a>Центр IoT tooyour подключения

Подключите концентратор IoT tooyour, выполнив следующую команду hello.

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Использование обозревателя Центра Интернета вещей для работы с прямыми методами

Вызвать hello `start` метод в hello устройства приложения toosend сообщения tooyour центра IoT, выполнив следующую команду hello:

```bash
iothub-explorer device-method <your device Id> start
```

Вызвать hello `stop` метод при отправке toostop приложения hello устройства сообщений центра IoT tooyour, выполнив следующую команду hello:

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Использование обозревателя Центра Интернета вещей для работы с требуемыми свойствами двойника

Установка интервала нужное свойство = 3000, выполнив следующую команду hello:

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

Устройство может прочитать это свойство.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Использование обозревателя Центра Интернета вещей для работы с сообщаемыми свойствами двойника

Получить hello выводятся свойства устройства hello, запустив hello следующую команду:

```bash
iothub-explorer get-twin <your device id>
```

Одно из свойств hello — $metadata. $lastUpdated с буквами hello время последнего это устройство отправляет или получает сообщение.

## <a name="use-iothub-explorer-with-twins-tags"></a>Использование обозревателя Центра Интернета вещей для работы с тегами двойника

Отображение тегов hello и свойства устройства hello, выполнив следующую команду hello:

```bash
iothub-explorer get-twin <your device id>
```

Добавьте роль поле = температуры и влажности toohello устройство, выполнив следующую команду hello:

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Использование обозревателя Центра Интернета вещей для работы с сообщениями, отправляемыми из облака на устройство.

Отправьте устройство toohello сообщение «Hello World», выполнив следующую команду hello:

```bash
iothub-explorer send <device-id> "Hello World"
```

В разделе [использовать обозреватель центром IOT toosend и получения сообщений между устройством и центр IoT](iot-hub-explorer-cloud-device-messaging.md) реальные сценарии использования этой команды.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Использование обозревателя Центра Интернета вещей для запросов данных двойников устройства

Запрос устройства тег роли = 'температуры и влажности», выполнив следующую команду hello:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Запрос всех устройств, за исключением тех, с помощью тега роли = 'температуры и влажности», выполнив следующую команду hello:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Дальнейшие действия

Вы узнали, каким образом центром IOT explorer toouse с различными параметрами управления.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
