---
title: "сообщения aaaCloud на устройство с центром IoT Azure (узел) | Документы Microsoft"
description: "Способ toosend облака на устройство сообщений tooa устройств из центра Azure IoT с помощью hello Azure IoT пакетов SDK для Node.js. Изменение сообщений облака на устройство имитированное устройство tooreceive приложения и изменения сообщений облака на устройство hello toosend серверной части приложения."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>Отправка сообщений из облака на устройства с помощью Центра Интернета вещей (Node)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Введение
Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения. Hello [приступить к работе с центром IoT] учебнике показано, как подготовить удостоверение устройства в нем toocreate центр IoT и кода приложения имитацию устройств, которое отправляет сообщения из устройства в облако.

Это руководство является логическим продолжением статьи [приступить к работе с центром IoT]. В нем показано следующее:

* Из серверной части вашего решения отправьте сообщения облака на устройство tooa одно устройство через Центр IoT.
* Получение на устройстве сообщений, передаваемых из облака на устройство.
* Из вашего решения внутренний запрос подтверждения доставки (*отзывы*) для сообщений отправленных tooa устройств из центра IoT.

Дополнительные сведения о сообщениях облака на устройство можно найти в hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].

В конце этого учебника hello выполните два Node.js консольные приложения:

* **SimulatedDevice**, измененная версия приложения hello, созданного в [приступить к работе с центром IoT], который подключается tooyour центр IoT и получает сообщения облака на устройство.
* **SendCloudToDeviceMessage**, который отправляет приложения имитированное устройство toohello сообщение облака на устройство с помощью центра IoT, а затем получает подтверждение его доставки.

> [!NOTE]
> Для центра IoT существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и Javascript). Эти пакеты работают на основе пакетов SDK для устройств Azure IoT. Пошаговые инструкции по tooconnect кода учебник toothis устройства и обычно tooAzure центр IoT. в статье hello [Центр разработчиков Azure IoT].
> 
> 

toocomplete этого учебника требуется hello следующие:

* Node.js версии 0.10.x или более поздней.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

## <a name="receive-messages-in-hello-simulated-device-app"></a>Получать сообщения в приложение hello имитированное устройство
В этом разделе, измените приложение hello имитированное устройство, вы создали в [приступить к работе с центром IoT] tooreceive сообщений облака на устройство из центра IoT hello.

1. В текстовом редакторе откройте файл SimulatedDevice.js hello.
2. Изменение hello **connectCallback** функции toohandle сообщений, отправленных из центра IoT. В этом примере hello устройства всегда вызывает hello **завершения** функции toonotify центра IoT, что он обработал сообщение hello. На новую версию hello **connectCallback** функция выглядит как следующий фрагмент кода hello:
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
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
   
   > [!NOTE]
   > При использовании HTTP вместо MQTT или AMQP транспорта hello hello **DeviceClient** экземпляра проверяет наличие сообщений от редко центр IoT (меньше, чем каждые 25 минут). Дополнительные сведения об отличиях hello поддержки MQTT, AMQP и HTTP и центр IoT регулирования см. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>Отправка сообщения из облака на устройство
В этом разделе создайте консольное приложение Node.js, которое отправляет сообщения облака на устройство toohello имитированное устройство приложения. Требуется hello идентификатор устройства устройства hello, добавленного в hello [приступить к работе с центром IoT] учебника. Строка подключения концентратора IoT требуется hello для концентратору, который можно найти в hello [портал Azure].

1. Создайте пустую папку **sendcloudtodevicemessage**. В hello **sendcloudtodevicemessage** папки, создайте файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```shell
    npm init
    ```
2. В командной строке в hello **sendcloudtodevicemessage** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета:
   
    ```shell
    npm install azure-iothub --save
    ```
3. В текстовом редакторе создайте **SendCloudToDeviceMessage.js** файла в hello **sendcloudtodevicemessage** папки.
4. Добавьте следующее hello `require` инструкции на hello начала hello **SendCloudToDeviceMessage.js** файла:
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. Добавьте следующий код слишком hello**SendCloudToDeviceMessage.js** файла. Замените значение заполнителя hello «{iot строка подключения концентратора}» hello центра IoT строку подключения для hello концентратор создан в hello [приступить к работе с центром IoT] учебника. Подставьте вместо hello «{идентификатор устройства}» hello код (ID) устройства hello, добавленного в hello [приступить к работе с центром IoT] учебника:
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. Добавьте следующие функции tooprint результатов toohello консоль управления hello:
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Добавьте следующие функции tooprint доставки отзыв сообщения toohello консоли hello:
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Добавьте следующую hello кода toosend устройства tooyour сообщений и обработки отзывов приветственное сообщение, если устройство hello подтверждает сообщение hello облака на устройство:
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. Сохраните и закройте файл **SendCloudToDeviceMessage.js** .

## <a name="run-hello-applications"></a>Запускать приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке hello в hello **simulateddevice** папку, выполните ниже hello команд tooIoT телеметрии toosend концентратора и toolisten для облака на устройство сообщений:
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Запустить имитированное устройство приложение hello][img-simulated-device]
2. В командной строке в hello **sendcloudtodevicemessage** папки, запустите следующие команды toosend hello сообщение облака на устройство и дождитесь hello подтверждения отзыв:
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Команда hello приложения toosend hello облака на устройство][img-send-command]
   
   > [!NOTE]
   > Для упрощения в этом учебнике не реализуются какие-либо политики повтора. В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].
   > 
   > 

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, как toosend и получать сообщения облака на устройство. 

см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite].

toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[приступить к работе с центром IoT]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[Центр разработчиков Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[портал Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
