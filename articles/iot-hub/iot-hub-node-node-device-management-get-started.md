---
title: "aaaGet работы с управлением устройства Azure IoT Hub (узел) | Документы Microsoft"
description: "Как toouse tooinitiate управления устройствами центра IoT перезагрузите удаленного устройства. Использовать hello IoT Azure SDK для Node.js tooimplement приложения имитированное устройство, которое включает прямой метод и приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="d7d60-104">Начало работы с управлением устройствами (Node)</span><span class="sxs-lookup"><span data-stu-id="d7d60-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="d7d60-105">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="d7d60-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d7d60-106">Используйте hello Azure портала toocreate центр IoT и создать удостоверение устройства в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="d7d60-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="d7d60-107">Создание приложения для имитации устройства с прямым методом, который позволяет выполнить перезагрузку устройства.</span><span class="sxs-lookup"><span data-stu-id="d7d60-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="d7d60-108">Прямой методы вызываются из облака hello.</span><span class="sxs-lookup"><span data-stu-id="d7d60-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="d7d60-109">Создайте консольное приложение Node.js, которое вызывает метод прямой перезагрузки hello в приложение hello имитированное устройство через концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="d7d60-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="d7d60-110">В конце этого учебника hello у вас есть два Node.js консольные приложения:</span><span class="sxs-lookup"><span data-stu-id="d7d60-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="d7d60-111">**dmpatterns_getstarted_device.js**, который подключает центра IoT tooyour с идентификатором hello устройства, созданный ранее, получает прямой метод перезагрузки, имитирует перезагрузка физического и отчеты hello время последней перезагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="d7d60-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="d7d60-112">**dmpatterns_getstarted_service.js**, прямой метод которого вызывает в приложение hello имитированное устройство, отображает ответ hello, и отображает hello обновлены данные свойства.</span><span class="sxs-lookup"><span data-stu-id="d7d60-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="d7d60-113">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d7d60-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d7d60-114">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d7d60-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="d7d60-115">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="d7d60-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d7d60-116">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d60-116">An active Azure account.</span></span> <span data-ttu-id="d7d60-117">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d7d60-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d7d60-118">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="d7d60-118">Create a simulated device app</span></span>
<span data-ttu-id="d7d60-119">В этом разделе вы сделаете следующее:</span><span class="sxs-lookup"><span data-stu-id="d7d60-119">In this section, you will</span></span>

* <span data-ttu-id="d7d60-120">Создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака</span><span class="sxs-lookup"><span data-stu-id="d7d60-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="d7d60-121">запустите перезагрузку имитации устройства;</span><span class="sxs-lookup"><span data-stu-id="d7d60-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="d7d60-122">Используйте hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и при их последней перезагрузки</span><span class="sxs-lookup"><span data-stu-id="d7d60-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="d7d60-123">Создайте пустую папку с именем **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="d7d60-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="d7d60-124">В hello **manageddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="d7d60-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="d7d60-125">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="d7d60-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d7d60-126">В командной строке в hello **manageddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:</span><span class="sxs-lookup"><span data-stu-id="d7d60-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="d7d60-127">В текстовом редакторе создайте **dmpatterns_getstarted_device.js** файла в hello **manageddevice** папки.</span><span class="sxs-lookup"><span data-stu-id="d7d60-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="d7d60-128">Добавьте следующие hello «требовать» операторы в начале hello hello **dmpatterns_getstarted_device.js** файла:</span><span class="sxs-lookup"><span data-stu-id="d7d60-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="d7d60-129">Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="d7d60-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="d7d60-130">Замените строку соединения hello строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="d7d60-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="d7d60-131">Добавить следующие функции tooimplement hello прямого метода на устройстве hello hello</span><span class="sxs-lookup"><span data-stu-id="d7d60-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="d7d60-132">Откройте центр IoT tooyour подключения hello и запустите hello прямой метод прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="d7d60-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="d7d60-133">Сохраните и закройте hello **dmpatterns_getstarted_device.js** файла.</span><span class="sxs-lookup"><span data-stu-id="d7d60-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="d7d60-134">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="d7d60-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d7d60-135">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="d7d60-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="d7d60-136">Триггер удаленной перезагрузки на устройстве hello, с помощью прямой метод</span><span class="sxs-lookup"><span data-stu-id="d7d60-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="d7d60-137">В этом разделе вы создадите консольное приложение Node.js, которое инициирует удаленное обновление устройства с помощью прямого метода.</span><span class="sxs-lookup"><span data-stu-id="d7d60-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="d7d60-138">приложение Hello использует устройство двойных запросы toodiscover hello время последней перезагрузки для этого устройства.</span><span class="sxs-lookup"><span data-stu-id="d7d60-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="d7d60-139">Создайте пустую папку с именем **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="d7d60-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="d7d60-140">В hello **triggerrebootondevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="d7d60-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="d7d60-141">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="d7d60-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d7d60-142">В командной строке в hello **triggerrebootondevice** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета SDK для устройства и **azure-iot устройства mqtt** пакета:</span><span class="sxs-lookup"><span data-stu-id="d7d60-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="d7d60-143">В текстовом редакторе создайте **dmpatterns_getstarted_service.js** файла в hello **triggerrebootondevice** папки.</span><span class="sxs-lookup"><span data-stu-id="d7d60-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="d7d60-144">Добавьте следующие hello «требовать» операторы в начале hello hello **dmpatterns_getstarted_service.js** файла:</span><span class="sxs-lookup"><span data-stu-id="d7d60-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="d7d60-145">Добавьте следующие объявления переменных hello и замените значения заполнителей hello.</span><span class="sxs-lookup"><span data-stu-id="d7d60-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="d7d60-146">Добавьте следующие функции tooinvoke hello устройства метод tooreboot hello целевое устройство hello:</span><span class="sxs-lookup"><span data-stu-id="d7d60-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="d7d60-147">Добавьте следующие hello функцией tooquery для hello устройства и получить hello время последней перезагрузки:</span><span class="sxs-lookup"><span data-stu-id="d7d60-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="d7d60-148">Добавьте следующие функции hello toocall кода, которые запускают hello hello перезагрузить прямой метод и запросов для hello последней перезагрузки времени:</span><span class="sxs-lookup"><span data-stu-id="d7d60-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="d7d60-149">Сохраните и закройте hello **dmpatterns_getstarted_service.js** файла.</span><span class="sxs-lookup"><span data-stu-id="d7d60-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="d7d60-150">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="d7d60-150">Run hello apps</span></span>
<span data-ttu-id="d7d60-151">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d7d60-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="d7d60-152">В командной строке hello в hello **manageddevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="d7d60-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="d7d60-153">В командной строке hello в hello **triggerrebootondevice** папки, запустите следующие команды tootrigger hello удаленного hello перезагрузите компьютер и запрос hello устройства двойных toofind hello перезагрузите последнего времени.</span><span class="sxs-lookup"><span data-stu-id="d7d60-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="d7d60-154">Появиться hello устройства toohello прямой метод ответа в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="d7d60-154">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
