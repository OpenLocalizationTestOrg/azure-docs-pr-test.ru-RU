---
title: "Сообщения облака на устройство с Центра Интернета вещей Azure | Документации Майкрософт"
description: "Как отправлять сообщения из облака на устройство из Центра Интернета вещей Azure, используя пакеты SDK Интернета вещей Azure для Node.js. Для получения сообщений, отправляемых из облака на устройство, следует изменить приложение имитации устройства, а для отправки таких сообщений следует изменить внутреннее приложение."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="72f3f-104">Отправка сообщений из облака на устройства с помощью Центра Интернета вещей (Node)</span><span class="sxs-lookup"><span data-stu-id="72f3f-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="72f3f-105">Введение</span><span class="sxs-lookup"><span data-stu-id="72f3f-105">Introduction</span></span>
<span data-ttu-id="72f3f-106">Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения.</span><span class="sxs-lookup"><span data-stu-id="72f3f-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="72f3f-107">В руководстве [Приступая к работе с Центром Интернета вещей Azure (Node)] показано, как создать Центр Интернета вещей, подготовить в нем удостоверение устройства и написать код приложения для имитации устройства, которое отправляет сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="72f3f-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="72f3f-108">Это руководство является логическим продолжением статьи [Приступая к работе с Центром Интернета вещей Azure (Node)].</span><span class="sxs-lookup"><span data-stu-id="72f3f-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="72f3f-109">В нем показано следующее:</span><span class="sxs-lookup"><span data-stu-id="72f3f-109">It shows you how to:</span></span>

* <span data-ttu-id="72f3f-110">Отправка сообщений, передаваемых из облака на устройство, из серверной части решения на одно устройство через Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="72f3f-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="72f3f-111">Получение на устройстве сообщений, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="72f3f-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="72f3f-112">Запрос из серверной части решения подтверждения доставки (*отзыва*) для сообщений, отправленных на устройство из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="72f3f-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="72f3f-113">Дополнительные сведения о сообщениях, отправляемых из облака на устройство, см. в [руководстве разработчика для Центра Интернета вещей][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="72f3f-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="72f3f-114">По завершении работы с этим руководством запустите два консольных приложения Node.js:</span><span class="sxs-lookup"><span data-stu-id="72f3f-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="72f3f-115">**SimulatedDevice**, измененную версию приложения, созданного в руководстве [Приступая к работе с Центром Интернета вещей Azure (Node)]. Это приложение подключается к центру IoT и получает сообщения с облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="72f3f-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="72f3f-116">**SendCloudToDeviceMessage**, которое отправляет сообщение из облака в приложение для имитации устройства с помощью Центра Интернета вещей, а затем получает подтверждение о его доставке.</span><span class="sxs-lookup"><span data-stu-id="72f3f-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="72f3f-117">Для центра IoT существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и Javascript). Эти пакеты работают на основе пакетов SDK для устройств Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="72f3f-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="72f3f-118">Пошаговые указания по связыванию устройства с кодом из этого руководства, а также по подключению к Центру Интернета вещей Azure см. в [центре разработчиков для Интернета вещей Azure].</span><span class="sxs-lookup"><span data-stu-id="72f3f-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="72f3f-119">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="72f3f-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="72f3f-120">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="72f3f-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="72f3f-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="72f3f-121">An active Azure account.</span></span> <span data-ttu-id="72f3f-122">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="72f3f-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="72f3f-123">Получение сообщений в приложении для имитации устройства</span><span class="sxs-lookup"><span data-stu-id="72f3f-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="72f3f-124">В этом разделе вы измените приложение для имитации устройства, созданное в разделе [Приступая к работе с Центром Интернета вещей Azure (Node)], для получения от Центра Интернета вещей сообщений из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="72f3f-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="72f3f-125">В текстовом редакторе откройте файл SimulatedDevice.js.</span><span class="sxs-lookup"><span data-stu-id="72f3f-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="72f3f-126">Измените функцию **connectCallback** для обработки сообщений, отправленных из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="72f3f-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="72f3f-127">В этом примере устройство всегда вызывает функцию **complete** для уведомления центра IoT о том, что сообщение обработано.</span><span class="sxs-lookup"><span data-stu-id="72f3f-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="72f3f-128">Новая версия функции **connectCallback** выглядит как следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="72f3f-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it to the IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > <span data-ttu-id="72f3f-129">Если в качестве транспорта вместо MQTT или AMQP используется HTTP, то экземпляр **DeviceClient** редко проверяет наличие сообщений от Центра Интернета вещей (реже чем каждые 25 минут).</span><span class="sxs-lookup"><span data-stu-id="72f3f-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="72f3f-130">Дополнительные сведения о различиях между поддержкой MQTT, AMQP и HTTP, а также регулировании Центра Интернета вещей см. в [руководстве разработчика для Центра Интернета вещей][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="72f3f-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="72f3f-131">Отправка сообщения из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="72f3f-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="72f3f-132">В этом разделе создается консольное приложение Node.js, которое отправляет сообщения, передаваемые из облака на устройство, в приложение имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="72f3f-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="72f3f-133">Необходим идентификатор устройства, добавленного при изучении руководства [Приступая к работе с Центром Интернета вещей Azure (Node)].</span><span class="sxs-lookup"><span data-stu-id="72f3f-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="72f3f-134">Кроме того, нужна строка подключения для вашего экземпляра Центра Интернета вещей, которую можно найти на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="72f3f-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="72f3f-135">Создайте пустую папку **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="72f3f-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="72f3f-136">В папке **sendcloudtodevicemessage** создайте файл package.json, введя в командной строке следующую команду.</span><span class="sxs-lookup"><span data-stu-id="72f3f-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="72f3f-137">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="72f3f-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="72f3f-138">В командной строке в папке **sendcloudtodevicemessage** выполните следующую команду, чтобы установить пакет **azure-iothub**.</span><span class="sxs-lookup"><span data-stu-id="72f3f-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="72f3f-139">В текстовом редакторе создайте файл **SendCloudToDeviceMessage.js** в папке **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="72f3f-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="72f3f-140">Добавьте следующие операторы `require` в начало файла **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="72f3f-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="72f3f-141">Добавьте в файл **SendCloudToDeviceMessage.js** следующий код.</span><span class="sxs-lookup"><span data-stu-id="72f3f-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="72f3f-142">Замените заполнитель строки {iot hub connection string} значением строки для Центра Интернета вещей, созданного при изучении руководства [Приступая к работе с Центром Интернета вещей Azure (Node)].</span><span class="sxs-lookup"><span data-stu-id="72f3f-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="72f3f-143">Замените заполнитель {device id} значением идентификатора устройства, добавленного при изучении руководства [Приступая к работе с Центром Интернета вещей Azure (Node)]:</span><span class="sxs-lookup"><span data-stu-id="72f3f-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="72f3f-144">Добавьте следующую функцию для вывода результатов операции в консоль.</span><span class="sxs-lookup"><span data-stu-id="72f3f-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="72f3f-145">Добавьте следующую функцию для вывода сообщений о доставке в консоль.</span><span class="sxs-lookup"><span data-stu-id="72f3f-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="72f3f-146">Добавьте приведенный ниже код для отправки сообщения на устройство и обработки сообщения о доставке, получаемого после подтверждения устройством получения сообщения из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="72f3f-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="72f3f-147">Сохраните и закройте файл **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="72f3f-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="72f3f-148">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="72f3f-148">Run the applications</span></span>
<span data-ttu-id="72f3f-149">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="72f3f-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="72f3f-150">В командной строке в папке **simulateddevice** выполните следующую команду, чтобы начать отправку данных телеметрии в Центр Интернета вещей и прослушивание сообщений из облака на устройства:</span><span class="sxs-lookup"><span data-stu-id="72f3f-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Запуск приложения виртуального устройства][img-simulated-device]
2. <span data-ttu-id="72f3f-152">В командной строке в папке **sendcloudtodevicemessage** выполните следующую команду, чтобы отправить сообщение из облака на устройство и ожидать подтверждения доставки:</span><span class="sxs-lookup"><span data-stu-id="72f3f-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Запуск приложения для отправки команды из облака на устройство][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="72f3f-154">Для упрощения в этом руководстве не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="72f3f-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="72f3f-155">В рабочем коде следует реализовать политики повтора (например, экспоненциальную задержку), как указано в статье MSDN [Обработка временного сбоя].</span><span class="sxs-lookup"><span data-stu-id="72f3f-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="72f3f-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="72f3f-156">Next steps</span></span>
<span data-ttu-id="72f3f-157">В этом учебнике вы научились отправлять и получать сообщения с облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="72f3f-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="72f3f-158">Примеры комплексных решений, в которых используется Центр Интернета вещей, см. в [документации по Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="72f3f-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="72f3f-159">Дополнительные сведения о разработке решений с помощью Центра Интернета вещей см. в [руководстве разработчика для Центра Интернета вещей].</span><span class="sxs-lookup"><span data-stu-id="72f3f-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="72f3f-160">[Приступая к работе с Центром Интернета вещей Azure (Node)]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="72f3f-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="72f3f-161">[руководстве разработчика для Центра Интернета вещей]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="72f3f-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="72f3f-162">[центре разработчиков для Интернета вещей Azure]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="72f3f-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="72f3f-163">[Обработка временного сбоя]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="72f3f-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="72f3f-164">[портале Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="72f3f-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="72f3f-165">[документации по Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="72f3f-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
