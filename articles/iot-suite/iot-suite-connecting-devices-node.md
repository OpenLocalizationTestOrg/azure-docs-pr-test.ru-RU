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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="8dca2-103">Подключение к toohello устройство, удаленное наблюдение предварительно настроенных решений (Node.js)</span><span class="sxs-lookup"><span data-stu-id="8dca2-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="8dca2-104">Создание примера решения Node.js</span><span class="sxs-lookup"><span data-stu-id="8dca2-104">Create a node.js sample solution</span></span>

<span data-ttu-id="8dca2-105">Убедитесь, что на компьютере разработки установлен компонент Node.js 0.11.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8dca2-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="8dca2-106">Можно запустить `node --version` toocheck hello hello командной строки версии.</span><span class="sxs-lookup"><span data-stu-id="8dca2-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="8dca2-107">Создайте папку **RemoteMonitoring** на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="8dca2-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="8dca2-108">Перейдите в папку toothis в среде командной строки.</span><span class="sxs-lookup"><span data-stu-id="8dca2-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="8dca2-109">Выполнения hello следующие команды toodownload и установите пакеты hello требуется пример приложения hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8dca2-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="8dca2-110">В hello **RemoteMonitoring** папки, создайте файл с именем **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="8dca2-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="8dca2-111">Откройте этот файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="8dca2-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="8dca2-112">В hello **remote_monitoring.js** файл, добавьте следующее hello `require` инструкции:</span><span class="sxs-lookup"><span data-stu-id="8dca2-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="8dca2-113">Добавьте следующие объявления переменных после hello hello `require` инструкции.</span><span class="sxs-lookup"><span data-stu-id="8dca2-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="8dca2-114">Замените значения заполнителей hello [идентификатор устройства] и [ключ устройства] со значениями, записанные для этого устройства в hello удаленного решений мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8dca2-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="8dca2-115">Здравствуйте, используйте имя узла концентратора IoT из hello решений мониторинга tooreplace [центром IOT Name].</span><span class="sxs-lookup"><span data-stu-id="8dca2-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="8dca2-116">Например, если имя узла Центра Интернета вещей — **contoso.azure-devices.net**, замените [имя_Центра_Интернета_вещей] на **contoso**.</span><span class="sxs-lookup"><span data-stu-id="8dca2-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="8dca2-117">Добавьте следующие переменные toodefine hello данные телеметрии базового:</span><span class="sxs-lookup"><span data-stu-id="8dca2-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="8dca2-118">Добавьте следующие результаты операции tooprint вспомогательные функции hello.</span><span class="sxs-lookup"><span data-stu-id="8dca2-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="8dca2-119">Добавьте следующие значения телеметрии hello toorandomize toouse вспомогательные функции hello.</span><span class="sxs-lookup"><span data-stu-id="8dca2-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="8dca2-120">Добавьте следующие определения для hello hello **DeviceInfo** отправляет устройства hello объекта во время запуска:</span><span class="sxs-lookup"><span data-stu-id="8dca2-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

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

1. <span data-ttu-id="8dca2-121">Добавьте hello следующее определение для hello устройства двойных сообщил значения.</span><span class="sxs-lookup"><span data-stu-id="8dca2-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="8dca2-122">Это определение включает описания hello прямой методов, которые поддерживает hello устройство:</span><span class="sxs-lookup"><span data-stu-id="8dca2-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

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

1. <span data-ttu-id="8dca2-123">Добавить следующие функции hello toohandle hello **перезагрузить** прямой вызов метода:</span><span class="sxs-lookup"><span data-stu-id="8dca2-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

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

1. <span data-ttu-id="8dca2-124">Добавить следующие функции hello toohandle hello **InitiateFirmwareUpdate** прямой вызов метода.</span><span class="sxs-lookup"><span data-stu-id="8dca2-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="8dca2-125">Этот метод прямой использует расположение параметра toospecify hello toodownload образ встроенного по hello и инициирует hello обновление встроенного по на устройстве hello асинхронно:</span><span class="sxs-lookup"><span data-stu-id="8dca2-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

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

1. <span data-ttu-id="8dca2-126">Добавьте следующий код toocreate экземпляр клиента hello:</span><span class="sxs-lookup"><span data-stu-id="8dca2-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="8dca2-127">Добавьте следующий код, чтобы hello:</span><span class="sxs-lookup"><span data-stu-id="8dca2-127">Add hello following code to:</span></span>

    * <span data-ttu-id="8dca2-128">Привет открыть соединение.</span><span class="sxs-lookup"><span data-stu-id="8dca2-128">Open hello connection.</span></span>
    * <span data-ttu-id="8dca2-129">Отправить hello **DeviceInfo** объекта.</span><span class="sxs-lookup"><span data-stu-id="8dca2-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="8dca2-130">настраивает обработчик для требуемых свойств;</span><span class="sxs-lookup"><span data-stu-id="8dca2-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="8dca2-131">отправляет сообщаемые свойства;</span><span class="sxs-lookup"><span data-stu-id="8dca2-131">Send reported properties.</span></span>
    * <span data-ttu-id="8dca2-132">Регистрировать обработчики для методов прямой hello.</span><span class="sxs-lookup"><span data-stu-id="8dca2-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="8dca2-133">начинает отправку данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="8dca2-133">Start sending telemetry.</span></span>

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

1. <span data-ttu-id="8dca2-134">Сохранить изменения toohello hello **remote_monitoring.js** файла.</span><span class="sxs-lookup"><span data-stu-id="8dca2-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="8dca2-135">Выполните следующую команду в командную строку hello toolaunch пример приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8dca2-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
