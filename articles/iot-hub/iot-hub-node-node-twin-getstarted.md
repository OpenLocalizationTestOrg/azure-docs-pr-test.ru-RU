---
title: "aaaGet к работе с близнецы устройства Azure IoT Hub (узел) | Документы Microsoft"
description: "Как tooadd близнецы устройства Azure IoT Hub toouse теги и затем использовать запрос центр IoT. Можно использовать hello Azure IoT пакетов SDK для Node.js tooimplement hello имитированное устройство приложения и приложение службы, которое добавляет теги hello и запускает hello центра IoT запроса."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>Начало работы с двойниками устройств (Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

В конце этого учебника hello будет иметь два Node.js консольные приложения:

* **AddTagsAndQuery.js** — это внутреннее приложение Node.js, которое добавляет теги и выполняет запросы к двойникам устройств.
* **TwinSimulatedDevice.js**, приложение Node.js, которое имитирует устройство, соединяющее центра IoT tooyour с идентификатором hello устройства, созданного ранее и сообщает о условия его подключения.

> [!NOTE]
> статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.
> 
> 

toocomplete этого учебника требуется hello следующее:

* Node.js версии 0.10.x или более поздней.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Создание приложения hello службы
В этом разделе создайте Node.js консольное приложение, которое добавляет связанные с устройством двойных расположение метаданных toohello **myDeviceId**. Затем выполняется запрос близнецы hello устройства хранится в центр IoT hello, выбрав hello устройствах, находящихся в hello нам и Здравствуйте, те, которые подчиняются сотовой связи.

1. Создайте пустую папку с именем **addtagsandqueryapp**. В hello **addtagsandqueryapp** папки, создайте новый файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **addtagsandqueryapp** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета:
   
    ```
    npm install azure-iothub --save
    ```
3. В текстовом редакторе создайте новый **AddTagsAndQuery.js** файла в hello **addtagsandqueryapp** папки.
4. Добавьте следующий код toohello hello **AddTagsAndQuery.js** файл и замените hello **{строка подключения концентратора iot}** заполнитель строки подключения центра IoT вы скопировали, когда вы создали концентратор приветствия:
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    Hello **реестра** объект предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello. Предыдущий код Hello сначала инициализирует hello **реестра** объекта, а затем извлекает hello двойных устройства для **myDeviceId**и наконец обновляет сведения о расположении hello требуемого этим тегам.
   
    После hello обновление hello его теги hello вызовов **queryTwins** функции.
5. Добавьте следующий код в конце hello hello **AddTagsAndQuery.js** tooimplement hello **queryTwins** функции:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    Предыдущий код Hello выполняет два запроса: hello сначала выделяются hello близнецы устройств для устройств, расположенных в hello **Redmond43** здания, сооружения и hello второй уточняет hello запроса tooselect только hello устройства, подключенные через также сети мобильной связи.
   
    Обратите внимание, что предыдущего код hello, при создании hello **запроса** объекта, указывает максимальное количество возвращенных документов. Hello **запроса** объект содержит **hasMoreResults** логического свойства, которые можно использовать tooinvoke hello **nextAsTwin** методы приводит все tooretrieve несколько раз. Метод **next** доступен для результатов, которые не являются двойниками устройств, например результаты статистических запросов.
6. Запустите приложение hello с:
   
        node AddTagsAndQuery.js
   
    Вы увидите одно устройство в результатах hello для hello запрос запросом для всех устройств, расположенных в **Redmond43** и для hello запрос, который ограничивает hello нет результатов toodevices используемой сети мобильной связи.
   
    ![][1]

В следующем разделе hello создается приложение устройства, которое сообщает сведения о подключении hello и изменения hello результат запроса hello в предыдущем разделе hello.

## <a name="create-hello-device-app"></a>Создание приложения hello устройства
В этом разделе создайте консольное приложение Node.js, которое подключается tooyour концентратора, **myDeviceId**и затем обновления, его устройство двойных сообщила свойства toocontain hello сведения, что она подключена с помощью сети мобильной связи.

> [!NOTE]
> В настоящее время устройство близнецы доступны только из устройств, которые подключаются tooIoT концентратора с помощью протокола MQTT hello. См. toohello [поддержки MQTT] [ lnk-devguide-mqtt] статье инструкции о том, как приложение toouse tooconvert существующие устройства MQTT.
> 
> 

1. Создайте пустую папку с именем **reportconnectivity**. В hello **reportconnectivity** папки, создайте новый файл package.json, используя следующую команду в командной строке hello. Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **reportconnectivity** папку, следующая команда tooinstall hello hello **azure iot устройства**, и **azure iot устройства mqtt** пакета :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. В текстовом редакторе создайте новый **ReportConnectivity.js** файла в hello **reportconnectivity** папки.
4. Добавьте следующий код toohello hello **ReportConnectivity.js** файл и замените hello **{строка подключения устройства}** заполнитель со строкой подключения устройства hello, скопированный во время создания hello **myDeviceId** удостоверение устройства:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Hello **клиента** объект представляет все методы hello, требующих toointeract с близнецы устройства с устройства hello. Здравствуйте предыдущего кода после инициализации hello **клиента** объекта извлекает hello двойных устройства для **myDeviceId** и обновляет сведения о подключении hello свойства отчета.
5. Выполните приложение hello устройства
   
        node ReportConnectivity.js
   
    Должно появиться сообщение hello `twin state reported`.
6. Теперь, когда hello устройство сообщило его сведения о соединении, он должен отображаться в обоих запросов. Перейдите обратно в hello **addtagsandqueryapp** hello папку и запустите запрос еще раз:
   
        node AddTagsAndQuery.js
   
    На этот раз **myDeviceId** должен появиться в результатах обоих запросов.
   
    ![][3]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Добавить метаданные устройства как теги из серверной части приложения, а написал имитированное устройство приложения tooreport подключения сведений об устройстве в двойных hello устройства. Вы также узнали, каким образом tooquery эти сведения, с помощью языка запросов SQL-подобного центра IoT hello.

Hello используйте следующие ресурсы toolearn как для:

* Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника
* Настройка устройств с нужными свойствами устройства двойных hello [используйте требуемого свойства устройства tooconfigure] [ lnk-twin-how-to-configure] учебника
* Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения), с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
