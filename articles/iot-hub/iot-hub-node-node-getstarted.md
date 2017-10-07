---
title: "aaaGet работы с Azure IoT Hub (узел) | Документы Microsoft"
description: "Узнайте, как toosend устройства в облако сообщений tooAzure центр IoT с помощью IoT пакеты SDK для Node.js. Создать имитированное устройство и службы приложений tooregister устройства, отправлять сообщения и чтения сообщений из центра IoT."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>Подключиться с помощью узла концентратор IoT tooyour имитированное устройство
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

В конце этого учебника hello у вас есть три Node.js консольные приложения:

* **CreateDeviceIdentity.js**, которая создает удостоверения устройства и связана защита ключа tooconnect приложение имитации устройства.
* **ReadDeviceToCloudMessages.js**, которая отображает hello телеметрии, отправленные приложения имитированное устройство.
* **SimulatedDevice.js**, который подключается центра IoT tooyour с идентификатором hello устройства, созданный ранее и будет отправлять данные телеметрии каждый второй с помощью протокола MQTT "hello".

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.
> 
> 

toocomplete этого учебника требуется hello следующие:

* Node.js версии 0.10.x или более поздней.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Теперь Центр Интернета вещей создан. У вас есть hello имя узла Центр IoT и hello центра IoT строку соединения, необходимость toocomplete hello конца данного учебника.

## <a name="create-a-device-identity"></a>Создание удостоверения устройства
В этом разделе создайте консольное приложение Node.js, которое создает удостоверение устройства в реестре hello identity в вашего центра IoT. Устройства могут подключаться концентратора tooIoT только в том случае, если он имеет запись в реестре удостоверений hello. Дополнительные сведения см. в разделе hello **реестра удостоверений** раздел hello [руководстве для разработчиков центра IoT][lnk-devguide-identity]. При запуске это консольное приложение, он создает уникальный идентификатор устройства и ключ, что при отправке устройства в облако, устройство может использовать tooidentify самого сообщения tooIoT концентратора.

1. Создайте пустую папку с именем **createdeviceidentity**. В hello **createdeviceidentity** папки, создайте файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **createdeviceidentity** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета SDK для службы:
   
    ```
    npm install azure-iothub --save
    ```
3. В текстовом редакторе создайте **CreateDeviceIdentity.js** файла в hello **createdeviceidentity** папки.
4. Добавьте следующее hello `require` инструкции в начале hello hello **CreateDeviceIdentity.js** файла:
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. Добавьте следующий код toohello hello **CreateDeviceIdentity.js** и замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданный в предыдущем разделе hello: 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. Добавьте следующий код toocreate определение устройства в реестре hello identity в вашего центра IoT hello. Этот код создает устройства, если идентификатор устройства hello не существует в реестре удостоверений hello, в противном случае он возвращает ключ hello hello существующее устройство:
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. Сохраните и закройте файл **CreateDeviceIdentity.js** .
8. toorun hello **createdeviceidentity** приложения, выполните следующую команду в командной строке hello в папке createdeviceidentity hello hello:
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. Запишите hello **идентификатор устройства** и **ключ устройства**. Эти значения должны позже при создании приложения, которое подключается tooIoT концентратора как устройство.

> [!NOTE]
> Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT. Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности и включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств. Если приложению toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения. Дополнительные сведения см. в разделе hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>Получение сообщений с устройства в облако
В этом разделе вы научитесь создавать консольное приложение Node.js, которое считывает сообщения, передаваемые с устройства в облако из центра IoT. Центр IoT предоставляет [концентраторов событий][lnk-event-hubs-overview]-совместимую конечную точку tooenable вам сообщения tooread устройства в облако. простые действия tookeep, данный учебник создает основные средства чтения, не подходит для развертывания высокой пропускной способностью. Hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебнике показано, как сообщения tooprocess устройства в облако в масштабе. Hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника содержатся дополнительные сведения о предоставлении tooprocess сообщений из концентраторов событий и определяется применимо toohello конечными точками события концентратора IoT Hub совместимой.

> [!NOTE]
> Hello концентратора событий-совместимой конечной точки для чтения сообщения из устройства в облако, всегда использует протокол AMQP hello.
> 
> 

1. Создайте пустую папку с именем **readdevicetocloudmessages**. В hello **readdevicetocloudmessages** папки, создайте файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **readdevicetocloudmessages** папку, следующая команда tooinstall hello hello **концентраторов событий azure** пакета:
   
    ```
    npm install azure-event-hubs --save
    ```
3. В текстовом редакторе создайте **ReadDeviceToCloudMessages.js** файла в hello **readdevicetocloudmessages** папки.
4. Добавьте следующее hello `require` инструкции на hello начала hello **ReadDeviceToCloudMessages.js** файла:
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. Добавьте следующие объявления переменных hello и замените значение заполнителя hello hello центра IoT строку подключения для концентратор.
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. Добавьте следующие две функции, которые печати выходных данных консоли toohello hello:
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. Добавьте следующий код toocreate hello hello **EventHubClient**откройте tooyour подключения hello центр IoT и Создание приемника для каждой секции. Это приложение использует фильтр при создании получателя, чтобы hello приемник считывает только сообщения, отправленные tooIoT концентратора после hello получатель начинает выполнение. Этот фильтр может применяться в тестовой среде, чтобы видеть только hello текущего набора сообщений. В рабочей среде кода следует убедиться, оно обрабатывает все сообщения hello. Дополнительные сведения см. в разделе hello [как tooprocess сообщения из устройства в облако центра IoT] [ lnk-process-d2c-tutorial] учебника:
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. Сохраните и закройте hello **ReadDeviceToCloudMessages.js** файла.

## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства
В этом разделе создайте консольное приложение Node.js, которое имитирует устройство, которое отправляет центр IoT tooan сообщения из устройства в облако.

1. Создайте пустую папку с именем **simulateddevice**. В hello **simulateddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **simulateddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. В текстовом редакторе создайте **SimulatedDevice.js** файла в hello **simulateddevice** папки.
4. Добавьте следующее hello `require` инструкции на hello начала hello **SimulatedDevice.js** файла:
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра. Замените **{youriothostname}** с именем hello hello центра IoT вы создали hello *создать центр IoT* раздела. Замените **{yourdevicekey}** со значением ключа устройства hello созданный hello *создать удостоверение устройства* раздела:
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. Добавьте следующие выходные данные функции toodisplay из приложения hello hello:
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Создание обратного вызова и использовать hello **setInterval** функции toosend концентратор IoT tooyour сообщение каждую секунду:
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. Откройте tooyour подключения hello центр IoT и приступить к отправке сообщений:
   
    ```
    client.open(connectCallback);
    ```
9. Сохраните и закройте hello **SimulatedDevice.js** файла.

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].
> 
> 

## <a name="run-hello-apps"></a>Запускайте приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке в hello **readdevicetocloudmessages** папки, запустите следующие команды toobegin мониторинга вашего центра IoT hello:
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Сообщения из устройства в облако node.js центр IoT службы приложения toomonitor][7]
2. В командной строке в hello **simulateddevice** папки, запустите hello, следующая команда toobegin отправки центра IoT tooyour данных телеметрии:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Устройства в облако сообщения toosend приложения node.js центр IoT устройства][8]
3. Hello **использование** плитки в hello [портал Azure] [ lnk-portal] показано hello число сообщений, отправляемых toohello центр IoT:
   
    ![Azure портала использование плитки, показывающего количество сообщений, отправляемых tooIoT концентратора][43]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы использовали устройства удостоверения tooenable hello имитируемые устройства приложения toosend сообщения из устройства в облако toohello центр IoT. Также было создано приложение, которое отображает hello сообщений, полученных центра IoT hello. 

Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:

* [Подключение устройства к Azure IoT][lnk-connect-device]
* [How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))
* [Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)

toolearn tooextend сообщений в масштабе, IoT решение и процесс устройства в облако. в статье hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
