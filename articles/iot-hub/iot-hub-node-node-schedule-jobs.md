---
title: "aaaSchedule заданий с центром IoT Azure (узел) | Документы Microsoft"
description: "Как tooschedule центр IoT Azure заданий tooinvoke прямой метод на нескольких устройствах. Использовать hello Azure IoT пакетов SDK для Node.js tooimplement hello имитируемые приложения для устройств и задание службы toorun приложения hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>Планирование и трансляция заданий (Node)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Центр IoT Azure является полностью управляемой службы, которая позволяет toocreate серверной части приложения и задания отслеживания, планировать и обновлять миллионов устройств.  Задания можно использовать для hello, следующие действия:

* Обновление требуемых свойств
* Обновление тегов
* Вызов прямых методов

По существу задание включает один из этих действий и отслеживает hello ход выполнения для набора устройств, в которой определяется запросом двойных устройства.  Например приложение серверной части можно использовать tooinvoke задания метод перезагрузки на 10 000 устройств, указанных запросом двойных устройства и по расписанию время в будущем.  Это приложение можно отслеживать ход выполнения, как каждая из этих устройств получают hello перезагрузки метод execute.

Дополнительные сведения о каждой из этих возможностей см. в следующих статьях:

* Двойных устройства и свойства: [Приступая к работе с устройством близнецы] [ lnk-get-started-twin] и [учебника: как свойства двойных toouse устройства][lnk-twin-props]
* Прямые методы: [Вызов прямого метода на устройстве (предварительная версия)][lnk-dev-methods] и [Руководство. Использование прямых методов][lnk-c2d-methods].

В этом учебнике описаны следующие процедуры.

* Создать приложение имитированное устройство, которое имеет прямой метод, который позволяет **lockDoor** которого может быть вызван hello решения серверной части.
* Создайте консольное приложение Node.js, hello вызовов **lockDoor** прямой метод в приложение hello имитированное устройство с помощью задания и обновления hello требуемого свойства с помощью задания устройства.

В конце этого учебника hello у вас есть два Node.js консольные приложения:

**simDevice.js**, который соединяет центр IoT tooyour с hello удостоверения устройства и получает **lockDoor** прямой метод.

**scheduleJobService.js**, которого вызывает метод с прямой hello имитированное устройство приложения и обновления hello устройства в двойных нужными свойствами при помощи задания.

toocomplete этого учебника требуется hello следующие:

* Node.js версии 0.12.x или более поздней. <br/>  [Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Создание приложения виртуального устройства
В этом разделе создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака, активизирующий перезагрузка имитации устройства и использует hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и когда они последней перезагрузки.

1. Создайте пустую папку с именем **simDevice**.  В hello **simDevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.  Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **simDevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure iot устройства mqtt** пакет:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. В текстовом редакторе создайте новый **simDevice.js** файла в hello **simDevice** папки.
4. Добавьте следующие hello «требовать» операторы в начале hello hello **simDevice.js** файла:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Добавить следующие функции hello toohandle hello **lockDoor** метод.
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Добавьте следующий код обработчика hello tooregister для hello hello **lockDoor** метод.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. Сохраните и закройте hello **simDevice.js** файла.

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>Планирование заданий для вызова прямого метода и обновления свойств двойника устройства
В этом разделе создайте консольное приложение Node.js, который инициирует удаленный **lockDoor** на устройстве с помощью прямой метод и обновление hello устройства двойных его свойств.

1. Создайте пустую папку с именем **scheduleJobService**.  В hello **scheduleJobService** папки, создайте файл package.json, используя следующую команду в командной строке hello.  Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **scheduleJobService** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:
   
    ```
    npm install azure-iothub uuid --save
    ```
3. В текстовом редакторе создайте новый **scheduleJobService.js** файла в hello **scheduleJobService** папки.
4. Добавьте следующие hello «требовать» операторы в начале hello hello **dmpatterns_gscheduleJobServiceetstarted_service.js** файла:
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. Добавьте следующие объявления переменных hello и замените значения заполнителей hello.
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Добавьте следующие функции, которая будет использоваться toomonitor hello выполнение задания hello hello:
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. Добавьте следующие задания hello tooschedule код, вызывающий метод устройства hello hello:
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. Добавьте следующий код tooschedule hello задания tooupdate hello устройства двойных hello:
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. Сохраните и закройте hello **scheduleJobService.js** файла.

## <a name="run-hello-applications"></a>Запускать приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке hello в hello **simDevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.
   
    ```
    node simDevice.js
    ```
2. В командной строке hello в hello **scheduleJobService** папку, следующая команда tootrigger hello задания toolock hello дверцы и обновление hello двойных hello
   
    ```
    node scheduleJobService.js
    ```
3. Появиться hello устройства toohello прямой метод ответа в консоли hello.

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике используется задание tooschedule прямой метод tooa устройства и hello обновление свойств устройства двойных hello.

Приступая к работе с центр IoT и шаблонов управления устройства, такие как удаленное через обновление встроенного по воздуху hello, toocontinue см.:

[Учебник: Как toodo встроенное по обновить][lnk-fwupdate]

Приступая к работе с центром IoT toocontinue в разделе [Приступая к работе с Azure IoT Edge][lnk-iot-edge].

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
