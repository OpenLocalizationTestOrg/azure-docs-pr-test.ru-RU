---
title: "сообщения aaaCloud на устройство с центром IoT Azure (узел) | Документы Microsoft"
description: "Способ toosend облака на устройство сообщений tooa устройств из центра Azure IoT с помощью hello Azure IoT пакетов SDK для Node.js. Изменение сообщений облака на устройство имитированное устройство tooreceive приложения и изменения сообщений облака на устройство hello toosend серверной части приложения."
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
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="850dc-104">Отправка сообщений из облака на устройства с помощью Центра Интернета вещей (Node)</span><span class="sxs-lookup"><span data-stu-id="850dc-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="850dc-105">Введение</span><span class="sxs-lookup"><span data-stu-id="850dc-105">Introduction</span></span>
<span data-ttu-id="850dc-106">Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения.</span><span class="sxs-lookup"><span data-stu-id="850dc-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="850dc-107">Hello [приступить к работе с центром IoT] учебнике показано, как подготовить удостоверение устройства в нем toocreate центр IoT и кода приложения имитацию устройств, которое отправляет сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="850dc-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="850dc-108">Это руководство является логическим продолжением статьи [приступить к работе с центром IoT].</span><span class="sxs-lookup"><span data-stu-id="850dc-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="850dc-109">В нем показано следующее:</span><span class="sxs-lookup"><span data-stu-id="850dc-109">It shows you how to:</span></span>

* <span data-ttu-id="850dc-110">Из серверной части вашего решения отправьте сообщения облака на устройство tooa одно устройство через Центр IoT.</span><span class="sxs-lookup"><span data-stu-id="850dc-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="850dc-111">Получение на устройстве сообщений, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="850dc-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="850dc-112">Из вашего решения внутренний запрос подтверждения доставки (*отзывы*) для сообщений отправленных tooa устройств из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="850dc-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="850dc-113">Дополнительные сведения о сообщениях облака на устройство можно найти в hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="850dc-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="850dc-114">В конце этого учебника hello выполните два Node.js консольные приложения:</span><span class="sxs-lookup"><span data-stu-id="850dc-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="850dc-115">**SimulatedDevice**, измененная версия приложения hello, созданного в [приступить к работе с центром IoT], который подключается tooyour центр IoT и получает сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="850dc-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="850dc-116">**SendCloudToDeviceMessage**, который отправляет приложения имитированное устройство toohello сообщение облака на устройство с помощью центра IoT, а затем получает подтверждение его доставки.</span><span class="sxs-lookup"><span data-stu-id="850dc-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="850dc-117">Для центра IoT существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и Javascript). Эти пакеты работают на основе пакетов SDK для устройств Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="850dc-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="850dc-118">Пошаговые инструкции по tooconnect кода учебник toothis устройства и обычно tooAzure центр IoT. в статье hello [Центр разработчиков Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="850dc-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="850dc-119">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="850dc-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="850dc-120">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="850dc-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="850dc-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="850dc-121">An active Azure account.</span></span> <span data-ttu-id="850dc-122">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="850dc-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="850dc-123">Получать сообщения в приложение hello имитированное устройство</span><span class="sxs-lookup"><span data-stu-id="850dc-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="850dc-124">В этом разделе, измените приложение hello имитированное устройство, вы создали в [приступить к работе с центром IoT] tooreceive сообщений облака на устройство из центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="850dc-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="850dc-125">В текстовом редакторе откройте файл SimulatedDevice.js hello.</span><span class="sxs-lookup"><span data-stu-id="850dc-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="850dc-126">Изменение hello **connectCallback** функции toohandle сообщений, отправленных из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="850dc-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="850dc-127">В этом примере hello устройства всегда вызывает hello **завершения** функции toonotify центра IoT, что он обработал сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="850dc-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="850dc-128">На новую версию hello **connectCallback** функция выглядит как следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="850dc-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
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
        // Create a message and send it toohello IoT Hub every second
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
   > <span data-ttu-id="850dc-129">При использовании HTTP вместо MQTT или AMQP транспорта hello hello **DeviceClient** экземпляра проверяет наличие сообщений от редко центр IoT (меньше, чем каждые 25 минут).</span><span class="sxs-lookup"><span data-stu-id="850dc-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="850dc-130">Дополнительные сведения об отличиях hello поддержки MQTT, AMQP и HTTP и центр IoT регулирования см. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="850dc-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="850dc-131">Отправка сообщения из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="850dc-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="850dc-132">В этом разделе создайте консольное приложение Node.js, которое отправляет сообщения облака на устройство toohello имитированное устройство приложения.</span><span class="sxs-lookup"><span data-stu-id="850dc-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="850dc-133">Требуется hello идентификатор устройства устройства hello, добавленного в hello [приступить к работе с центром IoT] учебника.</span><span class="sxs-lookup"><span data-stu-id="850dc-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="850dc-134">Строка подключения концентратора IoT требуется hello для концентратору, который можно найти в hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="850dc-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="850dc-135">Создайте пустую папку **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="850dc-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="850dc-136">В hello **sendcloudtodevicemessage** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="850dc-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="850dc-137">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="850dc-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="850dc-138">В командной строке в hello **sendcloudtodevicemessage** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета:</span><span class="sxs-lookup"><span data-stu-id="850dc-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="850dc-139">В текстовом редакторе создайте **SendCloudToDeviceMessage.js** файла в hello **sendcloudtodevicemessage** папки.</span><span class="sxs-lookup"><span data-stu-id="850dc-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="850dc-140">Добавьте следующее hello `require` инструкции на hello начала hello **SendCloudToDeviceMessage.js** файла:</span><span class="sxs-lookup"><span data-stu-id="850dc-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="850dc-141">Добавьте следующий код слишком hello**SendCloudToDeviceMessage.js** файла.</span><span class="sxs-lookup"><span data-stu-id="850dc-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="850dc-142">Замените значение заполнителя hello «{iot строка подключения концентратора}» hello центра IoT строку подключения для hello концентратор создан в hello [приступить к работе с центром IoT] учебника.</span><span class="sxs-lookup"><span data-stu-id="850dc-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="850dc-143">Подставьте вместо hello «{идентификатор устройства}» hello код (ID) устройства hello, добавленного в hello [приступить к работе с центром IoT] учебника:</span><span class="sxs-lookup"><span data-stu-id="850dc-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="850dc-144">Добавьте следующие функции tooprint результатов toohello консоль управления hello:</span><span class="sxs-lookup"><span data-stu-id="850dc-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="850dc-145">Добавьте следующие функции tooprint доставки отзыв сообщения toohello консоли hello:</span><span class="sxs-lookup"><span data-stu-id="850dc-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="850dc-146">Добавьте следующую hello кода toosend устройства tooyour сообщений и обработки отзывов приветственное сообщение, если устройство hello подтверждает сообщение hello облака на устройство:</span><span class="sxs-lookup"><span data-stu-id="850dc-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="850dc-147">Сохраните и закройте файл **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="850dc-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="850dc-148">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="850dc-148">Run hello applications</span></span>
<span data-ttu-id="850dc-149">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="850dc-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="850dc-150">В командной строке hello в hello **simulateddevice** папку, выполните ниже hello команд tooIoT телеметрии toosend концентратора и toolisten для облака на устройство сообщений:</span><span class="sxs-lookup"><span data-stu-id="850dc-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Запустить имитированное устройство приложение hello][img-simulated-device]
2. <span data-ttu-id="850dc-152">В командной строке в hello **sendcloudtodevicemessage** папки, запустите следующие команды toosend hello сообщение облака на устройство и дождитесь hello подтверждения отзыв:</span><span class="sxs-lookup"><span data-stu-id="850dc-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Команда hello приложения toosend hello облака на устройство][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="850dc-154">Для упрощения в этом учебнике не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="850dc-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="850dc-155">В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].</span><span class="sxs-lookup"><span data-stu-id="850dc-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="850dc-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="850dc-156">Next steps</span></span>
<span data-ttu-id="850dc-157">В этом учебнике вы узнали, как toosend и получать сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="850dc-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="850dc-158">см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="850dc-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="850dc-159">toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].</span><span class="sxs-lookup"><span data-stu-id="850dc-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[приступить к работе с центром IoT]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[Центр разработчиков Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[портал Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
