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
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="04e5a-104">Использование устройства управления tooinitiate обновление встроенного по устройства (узлов)</span><span class="sxs-lookup"><span data-stu-id="04e5a-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="04e5a-105">Введение</span><span class="sxs-lookup"><span data-stu-id="04e5a-105">Introduction</span></span>
<span data-ttu-id="04e5a-106">В hello [начало работы с управлением устройствами] [ lnk-dm-getstarted] учебник, вы видели, как toouse hello [двойных устройства] [ lnk-devtwin] и [прямой методы] [ lnk-c2dmethod] tooremotely примитивы перезагрузить устройство.</span><span class="sxs-lookup"><span data-stu-id="04e5a-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="04e5a-107">В этом учебнике используется hello же примитивы центр IoT и предоставляет рекомендации и показано, как toodo-законченный имитируемые обновление встроенного по.</span><span class="sxs-lookup"><span data-stu-id="04e5a-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="04e5a-108">Этот шаблон используется в реализации обновлений встроенного hello для устройства образца hello Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="04e5a-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="04e5a-109">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="04e5a-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="04e5a-110">Создайте консольное приложение Node.js, которое вызывает метод прямой firmwareUpdate hello в приложение hello имитированное устройство через концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="04e5a-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="04e5a-111">Создайте приложение виртуального устройства, которое реализует прямой метод **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="04e5a-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="04e5a-112">Этот метод запускает многоэтапный процесс ожидает образ встроенного по toodownload hello, он загружает образ встроенного по hello и наконец применение hello образ встроенного по.</span><span class="sxs-lookup"><span data-stu-id="04e5a-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="04e5a-113">Во время каждого этапа обновления hello hello устройство использует hello сообщил свойства tooreport о ходе выполнения.</span><span class="sxs-lookup"><span data-stu-id="04e5a-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="04e5a-114">В конце этого учебника hello у вас есть два Node.js консольные приложения:</span><span class="sxs-lookup"><span data-stu-id="04e5a-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="04e5a-115">**dmpatterns_fwupdate_service.js**, прямой метод которого вызывает в приложение hello имитированное устройство, отображает ответ hello, и периодически (каждые 500 мс) отображает hello обновлены данные свойства.</span><span class="sxs-lookup"><span data-stu-id="04e5a-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="04e5a-116">**dmpatterns_fwupdate_device.js**, который подключает центра IoT tooyour с идентификатором hello устройства, созданный ранее, получает прямой метод firmwareUpdate, завершит toosimulate многими состояниями процесс обновления встроенного по том числе: ожидание hello загрузить образ, hello новый образ загрузки и наконец применении hello образа.</span><span class="sxs-lookup"><span data-stu-id="04e5a-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="04e5a-117">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="04e5a-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="04e5a-118">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="04e5a-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="04e5a-119">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="04e5a-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="04e5a-120">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="04e5a-120">An active Azure account.</span></span> <span data-ttu-id="04e5a-121">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="04e5a-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="04e5a-122">Выполните hello [начало работы с управлением устройствами](iot-hub-node-node-device-management-get-started.md) статью toocreate ваш центр IoT и получить строки подключения центр IoT.</span><span class="sxs-lookup"><span data-stu-id="04e5a-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="04e5a-123">Вызвать обновление удаленного встроенного по на устройстве hello, с помощью прямой метод</span><span class="sxs-lookup"><span data-stu-id="04e5a-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="04e5a-124">В этом разделе вы создадите консольное приложение Node.js, которое инициирует удаленное обновление встроенного ПО на устройстве.</span><span class="sxs-lookup"><span data-stu-id="04e5a-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="04e5a-125">приложение Hello использует прямой метод tooinitiate hello обновления и использует устройство двойных запросы tooperiodically получить состояние hello обновления встроенного по active hello.</span><span class="sxs-lookup"><span data-stu-id="04e5a-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="04e5a-126">Создайте пустую папку с именем **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="04e5a-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="04e5a-127">В hello **triggerfwupdateondevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="04e5a-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="04e5a-128">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="04e5a-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="04e5a-129">В командной строке в hello **triggerfwupdateondevice** папку, следующая команда tooinstall hello hello **центра iot azure** и **azure iot устройства mqtt** устройства Пакеты SDK:</span><span class="sxs-lookup"><span data-stu-id="04e5a-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="04e5a-130">В текстовом редакторе создайте **dmpatterns_getstarted_service.js** файла в hello **triggerfwupdateondevice** папки.</span><span class="sxs-lookup"><span data-stu-id="04e5a-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="04e5a-131">Добавьте следующие hello «требовать» операторы в начале hello hello **dmpatterns_getstarted_service.js** файла:</span><span class="sxs-lookup"><span data-stu-id="04e5a-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="04e5a-132">Добавьте следующие объявления переменных hello и замените значения заполнителей hello.</span><span class="sxs-lookup"><span data-stu-id="04e5a-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="04e5a-133">Добавьте следующие hello функцией toofind и отобразить значение hello hello firmwareUpdate сообщил свойство.</span><span class="sxs-lookup"><span data-stu-id="04e5a-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="04e5a-134">Добавьте следующие функции tooinvoke hello firmwareUpdate метод tooreboot hello целевое устройство hello:</span><span class="sxs-lookup"><span data-stu-id="04e5a-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
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
8. <span data-ttu-id="04e5a-135">Наконец, добавить следующие hello функцией последовательность обновления встроенного по hello toostart toocode и периодически отображение hello сообщил свойства:</span><span class="sxs-lookup"><span data-stu-id="04e5a-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="04e5a-136">Сохраните и закройте hello **dmpatterns_fwupdate_service.js** файла.</span><span class="sxs-lookup"><span data-stu-id="04e5a-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="04e5a-137">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="04e5a-137">Run hello apps</span></span>
<span data-ttu-id="04e5a-138">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="04e5a-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="04e5a-139">В командной строке hello в hello **manageddevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="04e5a-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="04e5a-140">В командной строке hello в hello **triggerfwupdateondevice** папки, запустите следующие команды tootrigger hello удаленного hello перезагрузите компьютер и запрос hello устройства двойных toofind hello перезагрузите последнего времени.</span><span class="sxs-lookup"><span data-stu-id="04e5a-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="04e5a-141">Появиться hello устройства toohello прямой метод ответа в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="04e5a-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04e5a-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04e5a-142">Next steps</span></span>
<span data-ttu-id="04e5a-143">В этом учебнике используется tootrigger прямой метод удаленного обновления встроенного по на устройстве и используемых hello сообщил свойства toofollow hello ход выполнения обновления встроенного по hello.</span><span class="sxs-lookup"><span data-stu-id="04e5a-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="04e5a-144">toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="04e5a-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
