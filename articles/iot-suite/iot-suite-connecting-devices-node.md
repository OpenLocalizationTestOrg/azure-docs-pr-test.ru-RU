---
title: "aaaConnect устройство с помощью Node.js | Документы Microsoft"
description: "Описывает, как tooconnect toohello устройства Azure IoT Suite заранее настроенные удаленного мониторинга решения, с помощью приложения, написанного на Node.js."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>Подключение к toohello устройство, удаленное наблюдение предварительно настроенных решений (Node.js)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>Создание примера решения Node.js

Убедитесь, что на компьютере разработки установлен компонент Node.js 0.11.5 или более поздней версии. Можно запустить `node --version` toocheck hello hello командной строки версии.

1. Создайте папку **RemoteMonitoring** на компьютере разработки. Перейдите в папку toothis в среде командной строки.

1. Выполнения hello следующие команды toodownload и установите пакеты hello требуется пример приложения hello toocomplete:

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. В hello **RemoteMonitoring** папки, создайте файл с именем **remote_monitoring.js**. Откройте этот файл в текстовом редакторе.

1. В hello **remote_monitoring.js** файл, добавьте следующее hello `require` инструкции:

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. Добавьте следующие объявления переменных после hello hello `require` инструкции. Замените значения заполнителей hello [идентификатор устройства] и [ключ устройства] со значениями, записанные для этого устройства в hello удаленного решений мониторинга. Здравствуйте, используйте имя узла концентратора IoT из hello решений мониторинга tooreplace [центром IOT Name]. Например, если имя узла Центра Интернета вещей — **contoso.azure-devices.net**, замените [имя_Центра_Интернета_вещей] на **contoso**.

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. Добавьте следующие переменные toodefine hello данные телеметрии базового:

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. Добавьте следующие результаты операции tooprint вспомогательные функции hello.

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. Добавьте следующие значения телеметрии hello toorandomize toouse вспомогательные функции hello.

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. Добавьте следующие определения для hello hello **DeviceInfo** отправляет устройства hello объекта во время запуска:

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. Добавьте hello следующее определение для hello устройства двойных сообщил значения. Это определение включает описания hello прямой методов, которые поддерживает hello устройство:

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. Добавить следующие функции hello toohandle hello **перезагрузить** прямой вызов метода:

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. Добавить следующие функции hello toohandle hello **InitiateFirmwareUpdate** прямой вызов метода. Этот метод прямой использует расположение параметра toospecify hello toodownload образ встроенного по hello и инициирует hello обновление встроенного по на устройстве hello асинхронно:

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. Добавьте следующий код toocreate экземпляр клиента hello:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Добавьте следующий код, чтобы hello:

    * Привет открыть соединение.
    * Отправить hello **DeviceInfo** объекта.
    * настраивает обработчик для требуемых свойств;
    * отправляет сообщаемые свойства;
    * Регистрировать обработчики для методов прямой hello.
    * начинает отправку данных телеметрии.

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. Сохранить изменения toohello hello **remote_monitoring.js** файла.

1. Выполните следующую команду в командную строку hello toolaunch пример приложения hello.
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
