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
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="e1e68-104">Использование прямых методов на устройстве Интернета вещей (Node.js)</span><span class="sxs-lookup"><span data-stu-id="e1e68-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="e1e68-105">В конце этого учебника hello у вас есть два Node.js консольные приложения:</span><span class="sxs-lookup"><span data-stu-id="e1e68-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="e1e68-106">**CallMethodOnDevice.js**, который вызывает метод в приложение hello имитированное устройство и отображает ответ hello.</span><span class="sxs-lookup"><span data-stu-id="e1e68-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="e1e68-107">**SimulatedDevice.js**, которой соединяет центр IoT tooyour с удостоверения устройства hello, созданного ранее и отвечает toohello методе, вызванном hello облака.</span><span class="sxs-lookup"><span data-stu-id="e1e68-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="e1e68-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.</span><span class="sxs-lookup"><span data-stu-id="e1e68-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="e1e68-109">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e1e68-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e1e68-110">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e1e68-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="e1e68-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e68-111">An active Azure account.</span></span> <span data-ttu-id="e1e68-112">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e1e68-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e1e68-113">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="e1e68-113">Create a simulated device app</span></span>
<span data-ttu-id="e1e68-114">В этом разделе создайте Node.js консольное приложение, которое отвечает tooa методе, вызванном hello облака.</span><span class="sxs-lookup"><span data-stu-id="e1e68-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="e1e68-115">Создайте пустую папку с именем **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="e1e68-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="e1e68-116">В hello **simulateddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="e1e68-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e1e68-117">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="e1e68-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e1e68-118">В командной строке в hello **simulateddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:</span><span class="sxs-lookup"><span data-stu-id="e1e68-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="e1e68-119">В текстовом редакторе создайте новый **SimulatedDevice.js** файла в hello **simulateddevice** папки.</span><span class="sxs-lookup"><span data-stu-id="e1e68-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="e1e68-120">Добавьте следующее hello `require` инструкции на hello начала hello **SimulatedDevice.js** файла:</span><span class="sxs-lookup"><span data-stu-id="e1e68-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="e1e68-121">Добавить **connectionString** переменной и использовать его toocreate **DeviceClient** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="e1e68-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="e1e68-122">Замените **{строка подключения устройства}** со строкой подключения устройства hello, созданное в hello *создать удостоверение устройства* раздела:</span><span class="sxs-lookup"><span data-stu-id="e1e68-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="e1e68-123">Добавьте следующий метод hello tooimplement функции на устройстве hello hello:</span><span class="sxs-lookup"><span data-stu-id="e1e68-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
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
7. <span data-ttu-id="e1e68-124">Откройте центр IoT tooyour hello подключения и запустить прослушиватель метод initialize hello:</span><span class="sxs-lookup"><span data-stu-id="e1e68-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="e1e68-125">Сохраните и закройте hello **SimulatedDevice.js** файла.</span><span class="sxs-lookup"><span data-stu-id="e1e68-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="e1e68-126">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="e1e68-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e1e68-127">В рабочем коде следует реализовать политики повтора (например, повторного соединения), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="e1e68-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="e1e68-128">Вызов метода на устройстве</span><span class="sxs-lookup"><span data-stu-id="e1e68-128">Call a method on a device</span></span>
<span data-ttu-id="e1e68-129">В этом разделе создайте консольное приложение Node.js, которое вызывает метод в приложение hello имитированное устройство, а затем отображает hello ответа.</span><span class="sxs-lookup"><span data-stu-id="e1e68-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="e1e68-130">Создайте пустую папку с именем **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="e1e68-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="e1e68-131">В hello **callmethodondevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="e1e68-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e1e68-132">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="e1e68-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e1e68-133">В командной строке в hello **callmethodondevice** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета:</span><span class="sxs-lookup"><span data-stu-id="e1e68-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="e1e68-134">В текстовом редакторе создайте **CallMethodOnDevice.js** файла в hello **callmethodondevice** папки.</span><span class="sxs-lookup"><span data-stu-id="e1e68-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="e1e68-135">Добавьте следующее hello `require` инструкции на hello начала hello **CallMethodOnDevice.js** файла:</span><span class="sxs-lookup"><span data-stu-id="e1e68-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="e1e68-136">Добавьте следующие объявления переменных hello и замените значение заполнителя hello hello центра IoT строку подключения для концентратор.</span><span class="sxs-lookup"><span data-stu-id="e1e68-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="e1e68-137">Создайте tooyour центр IoT tooopen hello hello клиентского соединения.</span><span class="sxs-lookup"><span data-stu-id="e1e68-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="e1e68-138">Добавьте следующие функции tooinvoke hello метод и печати hello устройства ответа toohello консоли устройства hello:</span><span class="sxs-lookup"><span data-stu-id="e1e68-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
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
8. <span data-ttu-id="e1e68-139">Сохраните и закройте hello **CallMethodOnDevice.js** файла.</span><span class="sxs-lookup"><span data-stu-id="e1e68-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="e1e68-140">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="e1e68-140">Run hello apps</span></span>
<span data-ttu-id="e1e68-141">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e1e68-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="e1e68-142">В командной строке в hello **simulateddevice** папки, запустите следующие команды toostart прослушивание вызовы методов из вашего центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="e1e68-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="e1e68-143">В командной строке в hello **callmethodondevice** папки, запустите следующие команды toobegin мониторинга вашего центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="e1e68-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="e1e68-144">Вы увидите устройства hello реагировать метод toohello, выводя сообщение hello и приложения hello, который вызывается hello метод отображения hello ответа от устройства hello.</span><span class="sxs-lookup"><span data-stu-id="e1e68-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="e1e68-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1e68-145">Next steps</span></span>
<span data-ttu-id="e1e68-146">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="e1e68-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="e1e68-147">Вы использовали этот устройства удостоверения tooenable hello имитируемые устройства приложения tooreact toomethods вызываемая hello облака.</span><span class="sxs-lookup"><span data-stu-id="e1e68-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="e1e68-148">Также было создано приложение, которое вызывает методы на устройстве hello и отображает hello ответа от устройства hello.</span><span class="sxs-lookup"><span data-stu-id="e1e68-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="e1e68-149">Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:</span><span class="sxs-lookup"><span data-stu-id="e1e68-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="e1e68-150">[Приступая к работе с Центром Интернета вещей]</span><span class="sxs-lookup"><span data-stu-id="e1e68-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="e1e68-151">[Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="e1e68-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="e1e68-152">toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="e1e68-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
