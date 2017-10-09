---
title: "свойства двойных устройства aaaUse центр IoT Azure (узел) | Документы Microsoft"
description: "Как устройства Azure IoT Hub toouse близнецы tooconfigure устройств. Hello Azure IoT пакетов SDK для Node.js tooimplement используется приложение имитированное устройство и приложение службы, которое изменяет конфигурацию устройства, с помощью двойных устройства."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Используйте требуемого свойства tooconfigure устройства (узел)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

В конце этого учебника hello будет иметь два Node.js консольные приложения:

* **SimulateDeviceConfiguration.js**, приложение имитированное устройство, которое ожидает обновления требуемой конфигурацией и сообщает о состоянии hello имитацию конфигурации процесса обновления.
* **SetDesiredConfigurationAndQuery.js**, приложение Node.js серверной части, который задает hello необходимой настройки на устройстве, и запросы hello процесс обновления конфигурации.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.
> 
> 

toocomplete этого учебника требуется hello следующее:

* Node.js версии 0.10.x или более поздней.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

Если вы следовали hello [Приступая к работе с устройством близнецы] [ lnk-twin-tutorial] учебник, вы уже имеется центр IoT и вызывается удостоверение устройства **myDeviceId**; и можно пропустить toohello [ Создание приложения hello имитированное устройство] [ lnk-how-to-configure-createapp] раздела.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Создание приложения hello имитированное устройство
В этом разделе создайте консольное приложение Node.js, которое подключается tooyour концентратора, **myDeviceId**, ожидает обновления требуемой конфигурацией, а затем информирует о на процесс обновления конфигурации имитируемые hello.

1. Создайте пустую папку с именем **simulatedeviceconfiguration**. В hello **simulatedeviceconfiguration** папки, создайте новый файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **simulatedeviceconfiguration** папку, следующая команда tooinstall hello hello **azure iot устройства**, и **azure-iot устройства mqtt**пакета:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. В текстовом редакторе создайте новый **SimulateDeviceConfiguration.js** файла в hello **simulatedeviceconfiguration** папки.
4. Добавьте следующий код toohello hello **SimulateDeviceConfiguration.js** файл и замените hello **{строка подключения устройства}** заполнитель со строкой подключения устройства hello, вы скопировали, когда вы создать hello **myDeviceId** удостоверение устройства:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Hello **клиента** объект предоставляет все необходимые toointeract hello методы с близнецы устройства с устройства hello. Здравствуйте предыдущего кода после инициализации hello **клиента** объекта извлекает hello двойных устройства для **myDeviceId**и присоединяет обработчик для обновления hello на требуемые свойства. Обработчик Hello проверяет, существует запроса на изменение фактических конфигурации путем сравнения hello configIds, затем вызывает метод, который запускает изменение конфигурации hello.
   
    Обратите внимание, что ради hello простоты hello предыдущий код использует жестко запрограммированные значения по умолчанию hello начальной настройки. Настоящее приложение, вероятно, скачало бы эту конфигурацию из локального хранилища.
   
   > [!IMPORTANT]
   > События изменения нужное свойство выдаются всегда, один раз в процессе подключения устройства, убедитесь, что это реальное изменение hello toocheck нужными свойствами, прежде чем выполнять какие-либо действия.
   > 
   > 
5. Добавьте следующие методы перед hello hello `client.open()` вызова:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Hello **initConfigChange** метод обновляет отображаться свойства для hello объекта двойных локального устройства с запрос на обновление конфигурации hello и наборы hello состояние слишком**ожидающие**, а затем обновления hello устройства две службы hello. После успешного обновления двойных hello устройства, в нем имитируется длительного процесса, который прерывает выполнение hello **completeConfigChange**. Этот метод обновления hello локального устройства двойных сообщила свойства Установка состояния hello слишком**успех** и удаление hello **pendingConfig** объекта. Затем он обновляет hello двойных устройства в службе hello.
   
    Обратите внимание, что toosave пропускной способности, выводятся свойства обновляются путем указания изменен только toobe свойства hello (с именем **исправление** в hello над кодом), вместо замены всего документа hello.
   
   > [!NOTE]
   > В этом руководстве не имитируется поведение при одновременном обновлении конфигураций. Некоторые процессы обновления конфигурации могут быть изменения могут tooaccommodate целевой конфигурации, во время обновления hello, другие могут иметь tooqueue, а также другие может отклонить их с состоянием ошибки. Убедитесь, что tooconsider hello желаемое поведение для определенной конфигурации процесса и добавьте соответствующую логику hello перед запуском hello изменение конфигурации.
   > 
   > 
6. Запустите приложение hello устройства:
   
        node SimulateDeviceConfiguration.js
   
    Должно появиться сообщение hello `retrieved device twin`. Оставьте приложение hello под управлением.

## <a name="create-hello-service-app"></a>Создание приложения hello службы
В этом разделе вы создадите консольное приложение Node.js этого обновления hello *требуемого свойства* на двойных hello устройства, связанные с **myDeviceId** новым объектом конфигурации телеметрии. Он запрашивает близнецы устройства hello, хранящихся в центр IoT hello и показывает разность hello hello требуемого и данные конфигурации устройства hello.

1. Создайте пустую папку с именем **setdesiredandqueryapp**. В hello **setdesiredandqueryapp** папки, создайте новый файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **setdesiredandqueryapp** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета:
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. В текстовом редакторе создайте новый **SetDesiredAndQuery.js** файла в hello **addtagsandqueryapp** папки.
4. Добавьте следующий код toohello hello **SetDesiredAndQuery.js** файл и замените hello **{строка подключения концентратора iot}** заполнитель строки подключения центра IoT вы скопировали, когда вы создали концентратор приветствия :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Hello **реестра** объект предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello. Здравствуйте, предыдущий код после инициализации hello **реестра** объекта извлекает hello двойных устройства для **myDeviceId**и обновляет его нужными свойствами нового объекта конфигурации телеметрии. После этого он вызывает hello **queryTwins** функции события 10 секунд.

    > [!IMPORTANT]
    > Это приложение выполняет запрос к Центру Интернета вещей каждые 10 секунд в качестве примера. Используйте запрашивает toogenerate пользовательские отчеты для многих устройств и не toodetect изменения. Если вашему решению требуется отправка уведомлений о событиях устройства в реальном времени, используйте [уведомления двойников][lnk-twin-notifications].
    > 
    >.

1. Добавьте следующий код прямо перед hello hello `registry.getDeviceTwin()` hello вызова tooimplement **queryTwins** функции:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    Hello предыдущих запросов кода hello близнецы устройств хранятся в центре IoT hello и печатает hello требуемого и данные телеметрии конфигураций. См. toohello [язык запросов центра IoT] [ lnk-query] toolearn как toogenerate полнофункциональных отчетов на всех устройствах.
2. С **SimulateDeviceConfiguration.js** запущена, запустите приложение hello с:
   
        node SetDesiredAndQuery.js 5m
   
    Вы увидите изменение из указанной конфигурации hello **успех** слишком**ожидающие** слишком**успех** попытку новой активной hello пять минут, а не 24 частота отправки часы.
   
   > [!IMPORTANT]
   > Нет задержки мин tooa между hello устройство работы и отчетов hello результата запроса. Это toowork tooenable hello запроса инфраструктуры в очень широком масштабе. использовать tooretrieve согласованного представления двойных одно устройство hello **getDeviceTwin** метод в hello **реестра** класса.
   > 
   > 

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике можно задавать нужные параметры как *требуемого свойства* из серверной части приложения и написал toodetect имитированное устройство приложения, изменять и имитировать обновления многоступенчатый процесс, сообщение о состоянии  *отчет свойства* двойных toohello устройства.

Hello используйте следующие ресурсы toolearn как для:

* Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника
* запланировать или выполнять операции с большими наборами устройств в разделе hello [расписание и широковещательных задания] [ lnk-schedule-jobs] учебника.
* Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения), с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
