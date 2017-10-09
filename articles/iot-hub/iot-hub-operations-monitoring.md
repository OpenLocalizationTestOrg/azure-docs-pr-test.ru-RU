---
title: "Мониторинг операций центра IoT aaaAzure | Документы Microsoft"
description: "Способ мониторинга toomonitor операций центр IoT Azure toouse hello состояние операций на ваш центр IoT в режиме реального времени."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a>Мониторинг операций центра IoT

Мониторинга операций центра IoT позволяет toomonitor hello состояния операций на ваш центр IoT в режиме реального времени. Центр Интернета вещей отслеживает события по нескольким категориям операций. Вы можете отправить из одного или нескольких категорий tooan конечную точку в центр IoT для обработки события. Можно отслеживать данные hello ошибок или настроить более сложную обработку на основе закономерностей в данных.

Центр Интернета вещей отслеживает шесть категорий событий:

* Операции с удостоверениями устройства
* Телеметрия устройства
* Получение сообщений из облака на устройство
* Подключения
* Передача файлов
* Маршрутизация сообщений

## <a name="how-tooenable-operations-monitoring"></a>Способ мониторинга операций tooenable

1. Создайте Центр Интернета вещей. Инструкции о том, как можно найти центр IoT в hello toocreate [приступить к работе] [ lnk-get-started] руководства.

1. Откройте колонку hello из вашего центра IoT. В колонке щелкните **Мониторинг операций**.

    ![Операции доступа к конфигурации портала hello мониторинга][1]

1. Выберите hello категории правильно toomonitor и нажмите кнопку контроля **Сохранить**. Hello события, доступные для чтения из конечной точки hello совместимое концентратора событий, перечисленных в **параметры мониторинга**. Hello конечной точки центра IoT вызывается `messages/operationsmonitoringevents`.

    ![Настройка мониторинга операций в Центре Интернета вещей][2]

> [!NOTE]
> При выборе **Verbose** наблюдение за hello **подключений** категория приводит центра IoT toogenerate дополнительные диагностические сообщения. Все остальные категории hello **Verbose** изменения параметров hello количество сведения центра IoT включает в каждое сообщение об ошибке.

## <a name="event-categories-and-how-toouse-them"></a>Категории событий и как toouse их

Каждая категория мониторинга операций отслеживает отдельный тип взаимодействия с центром IoT и имеет схему, которая определяет способ структурирования событий в этой категории.

### <a name="device-identity-operations"></a>Операции с удостоверениями устройства

категории операций идентификаторов устройств Hello отслеживает ошибки, возникающие при попытке toocreate, обновление или удаление записи в реестре удостоверений центр IoT. Отслеживание этой категории целесообразно для сценариев подготовки.

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a>Телеметрия устройства

категории телеметрии устройств Hello отслеживает ошибок, возникших в центр IoT hello и являются связанные toohello конвейера телеметрии. В эту категорию входят ошибки, возникающие при отправке событий телеметрии (например: регулирование) и при получении событий телеметрии (например: неавторизованный модуль чтения). Эта категория не может перехватить ошибки, вызванные кодом, выполняемым на самом устройстве hello.

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a>Отправка команд из облака на устройство

категории команд облака на устройство Hello отслеживает ошибок, возникших в центр IoT hello и являются связанные toohello конвейер сообщений облака на устройство. В эту категорию входят ошибки, возникающие при отправке сообщений из облака на устройство (например, неавторизированный отправитель), при получении сообщений из облака на устройство (например, превышение числа доставок) и при получении отзыва на сообщение из облака на устройство (например, истечение срока действия отзыва). Эта категория не перехватывает ошибки с устройств, которые неправильно обрабатывает сообщение облака на устройство, если успешно доставлено сообщение hello облака на устройство.

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a>Подключения

Категория соединения Hello отслеживает ошибки, которые возникают, когда устройства подключиться или отключиться от центра IoT. Отслеживание этой категории полезно для определения попыток несанкционированных подключений и для отслеживания потери подключений к устройствам в областях с проблемами связи.

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a>Передача файлов

Категория передачи файла Hello отслеживает ошибок, возникших в центр IoT hello и связанные toofile передачи возможностям. В эту категорию входят:

* Ошибки, происходящие с hello универсальный код Ресурса SAS, например при истечении перед устройства уведомляет концентратора hello завершения загрузки.
* Сбой передачи, сообщаемые hello устройства.
* ошибки, связанные с отсутствием файла в хранилище при создании уведомления для Центра Интернета вещей.

Эта категория нельзя перехватить ошибки, которые непосредственно выполняются, пока hello устройство отправляет toostorage файла.

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a>Маршрутизация сообщений

Категория маршрутизации сообщений Hello отслеживает ошибки, возникающие во время оценки маршрут сообщения и исправности конечной точки с точки зрения центра IoT. В эту категорию входят события, такие, как правило, результатом является слишком «undefined», когда Центр IoT помечает конечную точку как сообщений и других ошибок, полученных из конечной точки. Эта категория не включает определенные ошибки, о hello сами сообщения (например, устройство ошибки регулирования), которые отображаются в категории «устройства телеметрии» hello.

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a>Просмотр событий

Можно использовать hello *explorer центром IOT* tooquickly средства проверки, что ваш центр IoT создает события наблюдения. tooinstall hello инструмент, см. инструкции hello в hello [explorer центром IOT] [ lnk-iothub-explorer] репозитории GitHub.

1. Убедитесь, что hello **подключений** мониторинг категории задано слишком**Verbose** hello портала.

1. В командной строке выполните следующую команду tooread из конечной точки мониторинга hello hello.

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. В другой командной строки выполните следующие команды toosimulate hello устройство, отправляющее сообщения из устройства в облако:

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. Hello первой командной строки показано событий мониторинга hello hello имитированное устройство подключается tooyour центр IoT.

## <a name="connect-toohello-monitoring-endpoint"></a>Подключение toohello конечной точки мониторинга

Привет, наблюдение за конечной точкой на ваш центр IoT является конечной точкой совместимое концентратора событий. Можно использовать любой механизм, который работает с сообщениями мониторинга tooread концентраторов событий этой конечной точкой. Hello следующий пример создает основные средства чтения, не подходит для развертывания высокой пропускной способностью. Дополнительные сведения о том, как tooprocess сообщений из концентраторов событий см. в разделе hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника.

tooconnect toohello конечной точки мониторинга, необходимо имя конечной точки соединения строки и hello. следующие шаги Hello Показать как toofind hello необходимые значения в портале hello:

1. На портале hello перейдите tooyour колонки ресурсов центра IoT.

1. Выберите **мониторинга операций**и запишите значение hello **концентратора событий-совместимое имя** и **конечной точки концентратора событий в совместимом** значения:

    ![Значения конечной точки, совместимой с концентраторами событий][img-endpoints]

1. Выберите **Политики общего доступа**, а затем — **служба**. Запишите hello **первичного ключа** значение:

    ![Первичный ключ политики общего доступа службы][img-service-key]

Hello следующий код C# берется из Visual Studio **Windows классического** консольное приложение C#. проект Hello имеет hello **WindowsAzure.ServiceBus** установлен пакет NuGet.

* Замените заполнитель строки подключения hello со строкой соединения, использующего hello **концентратора событий-совместимой конечной точки** и служба **первичного ключа** значений было сказано ранее, как показано в следующих hello Пример:

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Замените hello мониторинга заполнитель имя конечной точки hello **концентратора событий-совместимое имя** значение было сказано ранее.

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия
Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Руководство разработчика для Центра Интернета вещей][lnk-devguide]
* [Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md