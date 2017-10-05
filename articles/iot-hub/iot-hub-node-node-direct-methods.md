---
title: "Прямые методы Центра Интернета вещей Azure (Node) | Документация Майкрософт"
description: "Использование прямых методов Центра Интернета вещей Azure. Используйте пакеты SDK для Центра Интернета вещей Azure для Node.js, чтобы реализовать приложение имитации устройства, содержащее прямой метод и приложение службы, которое его вызывает."
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
ms.openlocfilehash: 83725c3ae3fd3807f2469be888e270ba078a8972
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="8f3a8-104">Использование прямых методов на устройстве Интернета вещей (Node.js)</span><span class="sxs-lookup"><span data-stu-id="8f3a8-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="8f3a8-105">По завершении работы с этим руководством у вас будет два консольных приложения Node.js:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-105">At the end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="8f3a8-106">**CallMethodOnDevice.js**, которое вызывает метод в приложении для имитации устройства и выводит ответ;</span><span class="sxs-lookup"><span data-stu-id="8f3a8-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="8f3a8-107">**SimulatedDevice.js**, которое подключается к Центру Интернета вещей с созданным ранее удостоверением устройства и отвечает на метод, вызванный облаком.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="8f3a8-108">Статья о [пакетах SDK для Центра Интернета вещей Azure][lnk-hub-sdks] содержит сведения о различных пакетах SDK, которые можно использовать для создания приложений, которые будут работать на устройствах и в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="8f3a8-109">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="8f3a8-110">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="8f3a8-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-111">An active Azure account.</span></span> <span data-ttu-id="8f3a8-112">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="8f3a8-113">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="8f3a8-113">Create a simulated device app</span></span>
<span data-ttu-id="8f3a8-114">В этом разделе вы создадите консольное приложение Node.js, отвечающее на метод, вызванный из облака.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span></span>

1. <span data-ttu-id="8f3a8-115">Создайте пустую папку с именем **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="8f3a8-116">В папке **simulateddevice** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="8f3a8-117">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-117">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8f3a8-118">В командной строке в папке **simulateddevice** выполните следующую команду, чтобы установить пакет SDK для устройства **azure-iot-device** и пакет **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="8f3a8-119">В текстовом редакторе создайте файл **SimulatedDevice.js** в папке **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="8f3a8-120">Добавьте следующие инструкции `require` в начало файла **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="8f3a8-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="8f3a8-121">Добавьте переменную **connectionString**, чтобы создать с ее помощью экземпляр **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="8f3a8-122">Замените **{device connection string}** строкой подключения устройства, созданной в разделе *Создание удостоверения устройства*.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="8f3a8-123">Добавьте следующую функцию, чтобы реализовать метод на устройстве:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-123">Add the following function to implement the method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="8f3a8-124">Откройте подключение к Центру Интернета вещей и начните инициализацию прослушивателя метода:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-124">Open the connection to your IoT hub and start initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="8f3a8-125">Сохраните и закройте файл **SimulatedDevice.js** .</span><span class="sxs-lookup"><span data-stu-id="8f3a8-125">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="8f3a8-126">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="8f3a8-127">В рабочем коде следует реализовать политики повтора (например, повторную попытку подключения), как указано в статье [Обработка временного сбоя][lnk-transient-faults] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="8f3a8-128">Вызов метода на устройстве</span><span class="sxs-lookup"><span data-stu-id="8f3a8-128">Call a method on a device</span></span>
<span data-ttu-id="8f3a8-129">В этом разделе вы создадите консольное приложение Node.js, которое вызывает метод в приложении для имитации устройства и выводит ответ.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="8f3a8-130">Создайте пустую папку с именем **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="8f3a8-131">В папке **callmethodondevice** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="8f3a8-132">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8f3a8-133">В командной строке в папке **callmethodondevice** выполните следующую команду, чтобы установить пакет **azure-iothub**.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="8f3a8-134">В текстовом редакторе создайте файл **CallMethodOnDevice.js** в папке **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="8f3a8-135">Добавьте следующие инструкции `require` в начало файла **CallMethodOnDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="8f3a8-136">Добавьте следующее объявление переменной и замените заполнитель строкой подключения к своему экземпляру Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="8f3a8-137">Создайте клиент, чтобы открыть подключение к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-137">Create the client to open the connection to your IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="8f3a8-138">Добавьте следующую функцию, чтобы вызвать метод устройства и вывести ответ устройства в консоль:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-138">Add the following function to invoke the device method and print the device response to the console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed to invoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="8f3a8-139">Сохраните и закройте файл **CallMethodOnDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-139">Save and close the **CallMethodOnDevice.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="8f3a8-140">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="8f3a8-140">Run the apps</span></span>
<span data-ttu-id="8f3a8-141">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-141">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="8f3a8-142">В командной строке в папке **simulateddevice** выполните следующую команду, чтобы начать прослушивать вызовы метода из Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="8f3a8-143">В командной строке в папке **callmethodondevice** выполните следующую команду, чтобы начать мониторинг Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="8f3a8-144">Устройство отреагирует на метод и выведет сообщение, а приложение, вызвавшее метод, выведет ответ устройства:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="8f3a8-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f3a8-145">Next steps</span></span>
<span data-ttu-id="8f3a8-146">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="8f3a8-147">Вы использовали удостоверение устройства, с помощью которого приложение имитации устройства может отвечать на методы, вызванные из облака.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="8f3a8-148">Вы также создали приложение, вызывающее методы на устройстве и выводящее ответ устройства.</span><span class="sxs-lookup"><span data-stu-id="8f3a8-148">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="8f3a8-149">Чтобы продолжить знакомство с Центром Интернета вещей и изучить другие сценарии Интернета вещей, см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="8f3a8-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="8f3a8-150">[Начало работы с Центром Интернета вещей]</span><span class="sxs-lookup"><span data-stu-id="8f3a8-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="8f3a8-151">[Планирование заданий на нескольких устройствах (предварительная версия)][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="8f3a8-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="8f3a8-152">Дополнительные сведения о расширении решения Центра Интернета вещей и планировании вызовов методов на нескольких устройствах см. в учебнике [Планирование и трансляция заданий][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="8f3a8-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
[Начало работы с Центром Интернета вещей]: iot-hub-node-node-getstarted.md
