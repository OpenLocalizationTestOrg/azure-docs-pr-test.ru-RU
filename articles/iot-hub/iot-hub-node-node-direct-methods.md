---
title: "Центр IoT aaaAzure прямой методы (узел) | Документы Microsoft"
description: "Как toouse центр IoT Azure направлять методы. Использовать hello Azure IoT пакетов SDK для Node.js tooimplement приложения имитированное устройство, которое включает прямой метод и приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Использование прямых методов на устройстве Интернета вещей (Node.js)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

В конце этого учебника hello у вас есть два Node.js консольные приложения:

* **CallMethodOnDevice.js**, который вызывает метод в приложение hello имитированное устройство и отображает ответ hello.
* **SimulatedDevice.js**, которой соединяет центр IoT tooyour с удостоверения устройства hello, созданного ранее и отвечает toohello методе, вызванном hello облака.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.
> 
> 

toocomplete этого учебника требуется hello следующие:

* Node.js версии 0.10.x или более поздней.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства
В этом разделе создайте Node.js консольное приложение, которое отвечает tooa методе, вызванном hello облака.

1. Создайте пустую папку с именем **simulateddevice**. В hello **simulateddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **simulateddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. В текстовом редакторе создайте новый **SimulatedDevice.js** файла в hello **simulateddevice** папки.
4. Добавьте следующее hello `require` инструкции на hello начала hello **SimulatedDevice.js** файла:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Добавить **connectionString** переменной и использовать его toocreate **DeviceClient** экземпляра. Замените **{строка подключения устройства}** со строкой подключения устройства hello, созданное в hello *создать удостоверение устройства* раздела:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Добавьте следующий метод hello tooimplement функции на устройстве hello hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Откройте центр IoT tooyour hello подключения и запустить прослушиватель метод initialize hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Сохраните и закройте hello **SimulatedDevice.js** файла.

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например, повторного соединения), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].
> 
> 

## <a name="call-a-method-on-a-device"></a>Вызов метода на устройстве
В этом разделе создайте консольное приложение Node.js, которое вызывает метод в приложение hello имитированное устройство, а затем отображает hello ответа.

1. Создайте пустую папку с именем **callmethodondevice**. В hello **callmethodondevice** папки, создайте файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **callmethodondevice** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета:
   
    ```
    npm install azure-iothub --save
    ```
3. В текстовом редакторе создайте **CallMethodOnDevice.js** файла в hello **callmethodondevice** папки.
4. Добавьте следующее hello `require` инструкции на hello начала hello **CallMethodOnDevice.js** файла:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Добавьте следующие объявления переменных hello и замените значение заполнителя hello hello центра IoT строку подключения для концентратор.
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Создайте tooyour центр IoT tooopen hello hello клиентского соединения.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. Добавьте следующие функции tooinvoke hello метод и печати hello устройства ответа toohello консоли устройства hello:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Сохраните и закройте hello **CallMethodOnDevice.js** файла.

## <a name="run-hello-apps"></a>Запускайте приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке в hello **simulateddevice** папки, запустите следующие команды toostart прослушивание вызовы методов из вашего центра IoT hello:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. В командной строке в hello **callmethodondevice** папки, запустите следующие команды toobegin мониторинга вашего центра IoT hello:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Вы увидите устройства hello реагировать метод toohello, выводя сообщение hello и приложения hello, который вызывается hello метод отображения hello ответа от устройства hello.
   
    ![][9]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы использовали этот устройства удостоверения tooenable hello имитируемые устройства приложения tooreact toomethods вызываемая hello облака. Также было создано приложение, которое вызывает методы на устройстве hello и отображает hello ответа от устройства hello. 

Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:

* [Приступая к работе с Центром Интернета вещей]
* [Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)

toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Приступая к работе с Центром Интернета вещей]: iot-hub-node-node-getstarted.md
