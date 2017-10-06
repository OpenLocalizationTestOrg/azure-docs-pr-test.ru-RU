---
title: "Поддержка Azure IoT Hub MQTT aaaUnderstand | Документы Microsoft"
description: "Разработчик руководства — поддержка для устройств, подключающихся с помощью конечной точки центра IoT устройств с выходом tooan hello MQTT протокола. Содержит сведения о встроенной поддержке MQTT в hello Azure IoT пакеты SDK."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Взаимодействовать с помощью протокола MQTT hello концентратор IoT

Центр IoT позволяет toocommunicate устройств с hello центра IoT устройства конечные точки, использующие hello [MQTT v3.1.1] [ lnk-mqtt-org] протокола на порт 8883 или v3.1.1 MQTT по протоколу WebSocket на порте 443. Центр IoT требует связи toobe все устройства, защищены с помощью TLS/SSL (таким образом, центр IoT не поддерживает небезопасные подключения через порт 1883).

## <a name="connecting-tooiot-hub"></a>Подключение tooIoT концентратора

Устройства можно использовать центр IoT tooan tooconnect протокола hello MQTT либо с помощью библиотек hello в hello [пакеты SDK Azure IoT] [ lnk-device-sdks] или напрямую с помощью протокола MQTT hello.

## <a name="using-hello-device-sdks"></a>С помощью устройства hello пакеты SDK

[Пакеты SDK] [ lnk-device-sdks] hello, поддержка протокола MQTT доступны для Java, Node.js, C, C# и Python. устройство Hello SDK использовать hello Стандартная центра IoT соединения строки tooestablish концентратор IoT tooan соединения. протокол MQTT toouse hello, hello клиентского протокола параметра должно быть установлено слишком**MQTT**. По умолчанию hello устройство пакеты SDK, подключить к hello tooan центр IoT **CleanSession** слишком установлен флаг**0** и использовать **QoS 1** для обмена сообщениями с центром IoT hello.

После перехода устройства подключенных tooan центра IoT, устройство hello SDK предоставлять методы, которые включить toosend сообщений hello устройства, tooand получать сообщения от центра IoT.

Hello Следующая таблица содержит примеры toocode ссылки для каждого поддерживаемого языка и указывает hello параметр toouse tooestablish tooIoT подключение концентратора с помощью протокола MQTT hello.

| Язык | Параметр протокола |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Миграция приложения для устройств с AMQP tooMQTT

Если вы используете hello [устройства SDK][lnk-device-sdks], переключение с помощью AMQP tooMQTT, необходимо изменить параметр протокола hello в инициализации клиента hello как уже говорилось ранее.

При этом убедитесь, что hello toocheck следующих элементов:

* AMQP возвращает ошибки для многих условий во время MQTT разрывает подключение hello. В результате может потребоваться изменить логику обработки исключений.
* MQTT не поддерживает hello *Отклонить* операции при получении [сообщений облака на устройство][lnk-messaging]. Если ваше приложение серверной части должно tooreceive ответа от устройства приложение hello, рассмотрите возможность использования [прямой методы][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>Непосредственно с помощью протокола MQTT hello
Если устройство не может использовать устройство hello пакеты SDK, он по-прежнему подключиться toohello конечных точек открытый устройства на порт 8883 с использованием протокола MQTT hello. В hello **CONNECT** пакетов hello устройство должно использовать hello следующие значения:

* Для hello **ClientId** воспользуйтесь hello **deviceId**.
* Для hello **Username** поле `{iothubhostname}/{device_id}/api-version=2016-11-14`, где {iothubhostname} hello полный CName центра IoT hello.

    Например, если hello концентратор IoT называется **contoso.azure devices.net** и hello имя устройства — **MyDevice01**, hello полный **Username** поле должно содержать `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Для hello **пароль** поля, используйте маркер SAS. Формат маркера SAS является приветствия Hello hello таким же как для hello HTTP и AMQP протоколы:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Дополнительные сведения о маркерах SAS toogenerate см в разделе hello устройства [маркеров безопасности с помощью центра IoT][lnk-sas-tokens].

    При тестировании, можно также использовать hello [обозреватель устройств] [ lnk-device-explorer] tooquickly средство создать токен SAS, который можно скопировать и вставить в собственный код:

  1. Go toohello **управления** вкладке **обозреватель устройств**.
  2. Щелкните **Маркер SAS** (вверху справа).
  3. На **SASTokenForm**, выберите устройство в hello **DeviceID** раскрывающийся список. Задайте значение **срока жизни**.
  4. Нажмите кнопку **формирования** toocreate срок действия токена.

     Hello маркер SAS, которое создается, имеет следующую структуру: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     Здравствуйте, часть этого маркера toouse как hello **пароль** — с помощью MQTT tooconnect поля: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

MQTT подключение и отключение пакетов, центр IoT выдает событие hello **мониторинг операций** канала с дополнительной информацией, которые могут помочь tootroubleshoot проблемы с подключением.

### <a name="sending-device-to-cloud-messages"></a>Отправка сообщений из устройства в облако

После успешного подключения, устройство может отправлять сообщения tooIoT концентратора с помощью `devices/{device_id}/messages/events/` или `devices/{device_id}/messages/events/{property_bag}` как **имя раздела**. Hello `{property_bag}` элемент включает сообщений toosend hello устройства с дополнительными свойствами в формате URL-адрес. Например:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Это `{property_bag}` элемент использует hello кодировкой как для строк запросов в протоколе hello HTTP.
>
>

приложение Hello устройства можно также использовать `devices/{device_id}/messages/events/{property_bag}` как hello **название раздела будет** toodefine *будет сообщения* toobe пересланный телеметрии сообщение.

- Центр Интернета вещей не поддерживает сообщения со вторым уровнем качества обслуживания. Если приложение для устройства публикует сообщение с **QoS 2**, центр IoT закрывает hello сетевое подключение.
- Центр Интернета вещей не сохраняет сообщения retain. Если устройство отправляет сообщение hello **Сохранить** too1 установлен флаг, центр IoT добавляет hello **x-opt Сохранить** сообщение toohello свойств приложения. В этом случае вместо сохранения hello сохранить сообщение, центр IoT передает toohello серверной части приложения.
- Центр Интернета вещей поддерживает только одно активное подключение MQTT на устройство. Любое новое соединение MQTT от имени hello таким же Идентификатором устройства вызывает центра IoT toodrop hello существующее подключение.

Дополнительные сведения см. в статье [Отправка и получение сообщений в Центре Интернета вещей][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Получение сообщений из облака на устройство

tooreceive сообщения из центра IoT, устройство необходимо подписаться с помощью `devices/{device_id}/messages/devicebound/#` как **фильтра разделов**. Здравствуйте многоуровневого подстановочные  **#**  в hello фильтра разделов используется только tooallow hello устройства tooreceive дополнительные свойства в разделе имени hello. Центр IoT не допускает использование hello hello  **#**  или **?** для фильтрации вложенных разделов. Поскольку центр IoT не брокера обмена сообщениями pub-sub общего назначения, он поддерживает только имена разделе документированы hello и фильтры разделов.

Hello устройства сообщения получены не из центра IoT, пока не будет успешно подписана конкретного устройства tooits конечной точки, представленный hello `devices/{device_id}/messages/devicebound/#` фильтра статьи. После установления успешная подписка hello устройства начинается получение сообщений только облака на устройство, которые были отправлены tooit после hello срока действия подписки hello. Если устройство hello подключается с **CleanSession** слишком установлен флаг**0**, hello подписки сохраняется в разных сеансах. В этом случае hello в следующий раз, он соединяется с **CleanSession 0** hello устройство получает ожидающих сообщений, которые были отправлены tooit пока он был отключен. Если устройство hello использует **CleanSession** слишком установлен флаг**1** , не получает сообщения из центра IoT пока она подписывается устройства tooits конечной точки.

Центр IoT доставляет сообщения с hello **имя раздела** `devices/{device_id}/messages/devicebound/`, или `devices/{device_id}/messages/devicebound/{property_bag}` при наличии любого свойства сообщения. `{property_bag}` содержит закодированные в формате URL-адреса пары "ключ-значение" свойств сообщения. Только для свойств приложения и задаваемое пользователем системные свойства (такие как **messageId** или **correlationId**) включаются в контейнере свойств hello. Имена системных свойств имеют префикс hello  **$** , свойства приложения использование исходного имени свойства и hello без префикса.

Когда приложение устройства подписывается tooa раздела с **QoS 2**, центр IoT предоставляет максимальный уровень качества обслуживания 1 в hello **SUBACK** пакетов. После этого центр IoT доставляет сообщения toohello устройства с помощью QoS 1.

### <a name="retrieving-a-device-twins-properties"></a>Получение свойств двойника устройства

Во-первых, устройство подписывается слишком`$iothub/twin/res/#`, ответов tooreceive hello операции. Затем он отправляет пустое сообщение tootopic `$iothub/twin/GET/?$rid={request id}`, заполненных значением **идентификатор запроса**. hello service отправляет ответное сообщение, содержащее данные двойных hello устройства в разделе `$iothub/twin/res/{status}/?$rid={request id}`, используя же hello  **Идентификатор запроса** как запрос hello.

Идентификатором запроса может быть любое допустимое значение свойства сообщения, как указано в статье [Отправка и получение сообщений в Центре Интернета вещей][lnk-messaging], а состояние проверяется как целое число.
текст ответа Hello содержит hello в разделе свойств двойных hello устройства:

текст Hello запись реестра идентификаторов hello ограничения toohello элемент «свойства», например:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

приведены коды возможных состояний Hello.

|Состояние | Описание |
| ----- | ----------- |
| 200 | Успешно |
| 429 | Слишком много запросов (регулирование), как указано в статье [Reference - quotas and throttling][lnk-quotas] (Справочные материалы. Квоты и регулирование) |
| 5** | ошибки сервера; |

Дополнительные сведения см. в статье [Двойники устройства][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Обновление сообщаемых свойств двойника устройства

Hello Ниже описана последовательность как устройство обновляет hello сообщил свойства в двойных hello устройств в центре IoT:

1. Устройство, сначала необходимо подписаться toohello `$iothub/twin/res/#` ответов операции для раздела tooreceive hello из центра IoT.

1. Устройство отправляет сообщение, содержащее двойных обновления hello устройства toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` раздела. Это сообщение содержит значение **request id** (идентификатор запроса).

1. Здравствуйте службы, а затем отправляет ответное сообщение, содержащее hello новое значение ETag для hello коллекции свойств отчета в разделе `$iothub/twin/res/{status}/?$rid={request id}`. Это сообщение ответа, использует hello же **идентификатор запроса** как запрос hello.

текст сообщения Hello запроса содержит документ JSON, который предоставляет новые значения для отчета свойства (нет свойств или метаданных можно изменить).
Каждого элемента в документе JSON hello обновляет или добавьте соответствующий элемент hello в документе двойных устройства hello. Набор элементов слишком`null`, удаляет hello элемент из hello, содержащий объект. Например:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

приведены коды возможных состояний Hello.

|Состояние | Описание |
| ----- | ----------- |
| 200 | Успешно |
| 400 | Недопустимый запрос. Неправильно сформированный JSON. |
| 429 | Слишком много запросов (регулирование), как указано в статье [Reference - quotas and throttling][lnk-quotas] (Справочные материалы. Квоты и регулирование) |
| 5** | ошибки сервера; |

Дополнительные сведения см. в статье [Двойники устройства][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Получение уведомлений об обновлении требуемых свойств

Когда устройство подключено, центр IoT отправляет уведомления toohello разделе `$iothub/twin/PATCH/properties/desired/?$version={new version}`, который содержимым hello hello обновления, выполненные hello решения серверной части. Например:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Как и для обновления свойств `null` средних значений, hello JSON объект удаляется элемент.


> [!IMPORTANT] 
> Центр Интернета вещей создает уведомления об изменении только в том случае, если устройства подключены. Убедитесь, что hello tooimplement [потока повторного подключения устройства] [ lnk-devguide-twin-reconnection] tookeep hello требуемого свойства синхронизируются между центр IoT и приложение hello устройства.

Дополнительные сведения см. в статье [Двойники устройства][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Ответ tooa прямой метод

Во-первых, устройство имеет toosubscribe слишком`$iothub/methods/POST/#`. Центр IoT отправляет разделе toohello запросы метод `$iothub/methods/POST/{method name}/?$rid={request id}`с недопустимым JSON или пустой текст.

toorespond, hello устройство отправляет сообщение с допустимых данных JSON или разделе toohello пустым телом `$iothub/methods/res/{status}/?$rid={request id}`, где **идентификатор запроса** имеет toomatch hello в приветственное сообщение запроса, и **состояние** имеет toobe целое число .

Дополнительные сведения см. в статье [Прямые методы][lnk-methods].

### <a name="additional-considerations"></a>Дополнительные замечания

В последнее соображение, если необходимо поведение toocustomize hello MQTT протокола со стороны hello облака, необходимо просмотреть hello [шлюз протокола Azure IoT] [ lnk-azure-protocol-gateway] , позволяющий toodeploy высокой производительности шлюз пользовательский протокол, который взаимодействует непосредственно с центром IoT. шлюз протокола Hello Azure IoT позволяет вы toocustomize hello протокола tooaccommodate brownfield MQTT развертывания устройств или других протоколов. Однако при этом подходе необходимо запустить настраиваемый шлюз протокола и управлять им.

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о hello MQTT протокола, в разделе hello [документации MQTT][lnk-mqtt-docs].

toolearn Дополнительные сведения о планировании развертывания центра IoT, см.:

* [Каталог устройств, сертифицированных по программе Microsoft Azure Certified for IoT][lnk-devices]
* [Поддержка дополнительных протоколов для центра IoT][lnk-protocols]
* [Сравнение центра IoT и концентраторов событий][lnk-compare]
* [Масштабирование центра IoT][lnk-scaling]

Изучение возможностей hello центра IoT toofurther см. в разделе:

* [Руководство разработчика для Центра Интернета вещей][lnk-devguide]
* [Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
