---
title: "обновление встроенного по aaaDevice с центром IoT Azure (узел) | Документы Microsoft"
description: "Как обновить toouse управления устройствами в центр IoT Azure tooinitiate микропрограммы устройства. Hello Azure IoT пакетов SDK для Node.js tooimplement используется приложение имитированное устройство и службы приложений, которое вызывает обновление встроенного по hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>Использование устройства управления tooinitiate обновление встроенного по устройства (узлов)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Введение
В hello [начало работы с управлением устройствами] [ lnk-dm-getstarted] учебник, вы видели, как toouse hello [двойных устройства] [ lnk-devtwin] и [прямой методы] [ lnk-c2dmethod] tooremotely примитивы перезагрузить устройство. В этом учебнике используется hello же примитивы центр IoT и предоставляет рекомендации и показано, как toodo-законченный имитируемые обновление встроенного по.  Этот шаблон используется в реализации обновлений встроенного hello для устройства образца hello Intel Edison.

В этом учебнике описаны следующие процедуры.

* Создайте консольное приложение Node.js, которое вызывает метод прямой firmwareUpdate hello в приложение hello имитированное устройство через концентратор IoT.
* Создайте приложение виртуального устройства, которое реализует прямой метод **firmwareUpdate**. Этот метод запускает многоэтапный процесс ожидает образ встроенного по toodownload hello, он загружает образ встроенного по hello и наконец применение hello образ встроенного по. Во время каждого этапа обновления hello hello устройство использует hello сообщил свойства tooreport о ходе выполнения.

В конце этого учебника hello у вас есть два Node.js консольные приложения:

**dmpatterns_fwupdate_service.js**, прямой метод которого вызывает в приложение hello имитированное устройство, отображает ответ hello, и периодически (каждые 500 мс) отображает hello обновлены данные свойства.

**dmpatterns_fwupdate_device.js**, который подключает центра IoT tooyour с идентификатором hello устройства, созданный ранее, получает прямой метод firmwareUpdate, завершит toosimulate многими состояниями процесс обновления встроенного по том числе: ожидание hello загрузить образ, hello новый образ загрузки и наконец применении hello образа.

toocomplete этого учебника требуется hello следующие:

* Node.js версии 0.12.x или более поздней. <br/>  [Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

Выполните hello [начало работы с управлением устройствами](iot-hub-node-node-device-management-get-started.md) статью toocreate ваш центр IoT и получить строки подключения центр IoT.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Вызвать обновление удаленного встроенного по на устройстве hello, с помощью прямой метод
В этом разделе вы создадите консольное приложение Node.js, которое инициирует удаленное обновление встроенного ПО на устройстве. приложение Hello использует прямой метод tooinitiate hello обновления и использует устройство двойных запросы tooperiodically получить состояние hello обновления встроенного по active hello.

1. Создайте пустую папку с именем **triggerfwupdateondevice**.  В hello **triggerfwupdateondevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.  Примите все значения по умолчанию hello:
   
    ```
    npm init
    ```
2. В командной строке в hello **triggerfwupdateondevice** папку, следующая команда tooinstall hello hello **центра iot azure** и **azure iot устройства mqtt** устройства Пакеты SDK:
   
    ```
    npm install azure-iothub --save
    ```
3. В текстовом редакторе создайте **dmpatterns_getstarted_service.js** файла в hello **triggerfwupdateondevice** папки.
4. Добавьте следующие hello «требовать» операторы в начале hello hello **dmpatterns_getstarted_service.js** файла:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Добавьте следующие объявления переменных hello и замените значения заполнителей hello.
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Добавьте следующие hello функцией toofind и отобразить значение hello hello firmwareUpdate сообщил свойство.
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. Добавьте следующие функции tooinvoke hello firmwareUpdate метод tooreboot hello целевое устройство hello:
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. Наконец, добавить следующие hello функцией последовательность обновления встроенного по hello toostart toocode и периодически отображение hello сообщил свойства:
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. Сохраните и закройте hello **dmpatterns_fwupdate_service.js** файла.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Запускайте приложения hello
Теперь вы находитесь toorun готовности приложения hello.

1. В командной строке hello в hello **manageddevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. В командной строке hello в hello **triggerfwupdateondevice** папки, запустите следующие команды tootrigger hello удаленного hello перезагрузите компьютер и запрос hello устройства двойных toofind hello перезагрузите последнего времени.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. Появиться hello устройства toohello прямой метод ответа в консоли hello.

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике используется tootrigger прямой метод удаленного обновления встроенного по на устройстве и используемых hello сообщил свойства toofollow hello ход выполнения обновления встроенного по hello.

toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
