---
title: "aaaGet работы с Azure IoT Hub (узел) | Документы Microsoft"
description: "Узнайте, как toosend устройства в облако сообщений tooAzure центр IoT с помощью IoT пакеты SDK для Node.js. Создать имитированное устройство и службы приложений tooregister устройства, отправлять сообщения и чтения сообщений из центра IoT."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="41dfb-104">Подключиться с помощью узла концентратор IoT tooyour имитированное устройство</span><span class="sxs-lookup"><span data-stu-id="41dfb-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="41dfb-105">В конце этого учебника hello у вас есть три Node.js консольные приложения:</span><span class="sxs-lookup"><span data-stu-id="41dfb-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="41dfb-106">**CreateDeviceIdentity.js**, которая создает удостоверения устройства и связана защита ключа tooconnect приложение имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="41dfb-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="41dfb-107">**ReadDeviceToCloudMessages.js**, которая отображает hello телеметрии, отправленные приложения имитированное устройство.</span><span class="sxs-lookup"><span data-stu-id="41dfb-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="41dfb-108">**SimulatedDevice.js**, который подключается центра IoT tooyour с идентификатором hello устройства, созданный ранее и будет отправлять данные телеметрии каждый второй с помощью протокола MQTT "hello".</span><span class="sxs-lookup"><span data-stu-id="41dfb-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="41dfb-109">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.</span><span class="sxs-lookup"><span data-stu-id="41dfb-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="41dfb-110">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="41dfb-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="41dfb-111">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="41dfb-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="41dfb-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="41dfb-112">An active Azure account.</span></span> <span data-ttu-id="41dfb-113">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="41dfb-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="41dfb-114">Теперь Центр Интернета вещей создан.</span><span class="sxs-lookup"><span data-stu-id="41dfb-114">You have now created your IoT hub.</span></span> <span data-ttu-id="41dfb-115">У вас есть hello имя узла Центр IoT и hello центра IoT строку соединения, необходимость toocomplete hello конца данного учебника.</span><span class="sxs-lookup"><span data-stu-id="41dfb-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="41dfb-116">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="41dfb-116">Create a device identity</span></span>
<span data-ttu-id="41dfb-117">В этом разделе создайте консольное приложение Node.js, которое создает удостоверение устройства в реестре hello identity в вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="41dfb-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="41dfb-118">Устройства могут подключаться концентратора tooIoT только в том случае, если он имеет запись в реестре удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="41dfb-119">Дополнительные сведения см. в разделе hello **реестра удостоверений** раздел hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="41dfb-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="41dfb-120">При запуске это консольное приложение, он создает уникальный идентификатор устройства и ключ, что при отправке устройства в облако, устройство может использовать tooidentify самого сообщения tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="41dfb-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="41dfb-121">Создайте пустую папку с именем **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="41dfb-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="41dfb-122">В hello **createdeviceidentity** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="41dfb-123">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="41dfb-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="41dfb-124">В командной строке в hello **createdeviceidentity** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета SDK для службы:</span><span class="sxs-lookup"><span data-stu-id="41dfb-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="41dfb-125">В текстовом редакторе создайте **CreateDeviceIdentity.js** файла в hello **createdeviceidentity** папки.</span><span class="sxs-lookup"><span data-stu-id="41dfb-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="41dfb-126">Добавьте следующее hello `require` инструкции в начале hello hello **CreateDeviceIdentity.js** файла:</span><span class="sxs-lookup"><span data-stu-id="41dfb-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="41dfb-127">Добавьте следующий код toohello hello **CreateDeviceIdentity.js** и замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданный в предыдущем разделе hello:</span><span class="sxs-lookup"><span data-stu-id="41dfb-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="41dfb-128">Добавьте следующий код toocreate определение устройства в реестре hello identity в вашего центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="41dfb-129">Этот код создает устройства, если идентификатор устройства hello не существует в реестре удостоверений hello, в противном случае он возвращает ключ hello hello существующее устройство:</span><span class="sxs-lookup"><span data-stu-id="41dfb-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="41dfb-130">Сохраните и закройте файл **CreateDeviceIdentity.js** .</span><span class="sxs-lookup"><span data-stu-id="41dfb-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="41dfb-131">toorun hello **createdeviceidentity** приложения, выполните следующую команду в командной строке hello в папке createdeviceidentity hello hello:</span><span class="sxs-lookup"><span data-stu-id="41dfb-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="41dfb-132">Запишите hello **идентификатор устройства** и **ключ устройства**.</span><span class="sxs-lookup"><span data-stu-id="41dfb-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="41dfb-133">Эти значения должны позже при создании приложения, которое подключается tooIoT концентратора как устройство.</span><span class="sxs-lookup"><span data-stu-id="41dfb-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="41dfb-134">Hello реестра удостоверений центра IoT хранится только toohello устройства удостоверения tooenable безопасного доступа центра IoT.</span><span class="sxs-lookup"><span data-stu-id="41dfb-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="41dfb-135">Он сохраняет идентификаторы и ключи toouse устройства как учетные данные безопасности и включение или отключение флага, что toodisable доступа можно использовать для отдельных устройств.</span><span class="sxs-lookup"><span data-stu-id="41dfb-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="41dfb-136">Если приложению toostore другие метаданные для конкретного устройства, его следует использовать хранилище конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="41dfb-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="41dfb-137">Дополнительные сведения см. в разделе hello [руководстве для разработчиков центра IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="41dfb-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="41dfb-138">Получение сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="41dfb-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="41dfb-139">В этом разделе вы научитесь создавать консольное приложение Node.js, которое считывает сообщения, передаваемые с устройства в облако из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="41dfb-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="41dfb-140">Центр IoT предоставляет [концентраторов событий][lnk-event-hubs-overview]-совместимую конечную точку tooenable вам сообщения tooread устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="41dfb-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="41dfb-141">простые действия tookeep, данный учебник создает основные средства чтения, не подходит для развертывания высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="41dfb-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="41dfb-142">Hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебнике показано, как сообщения tooprocess устройства в облако в масштабе.</span><span class="sxs-lookup"><span data-stu-id="41dfb-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="41dfb-143">Hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника содержатся дополнительные сведения о предоставлении tooprocess сообщений из концентраторов событий и определяется применимо toohello конечными точками события концентратора IoT Hub совместимой.</span><span class="sxs-lookup"><span data-stu-id="41dfb-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="41dfb-144">Hello концентратора событий-совместимой конечной точки для чтения сообщения из устройства в облако, всегда использует протокол AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="41dfb-145">Создайте пустую папку с именем **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="41dfb-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="41dfb-146">В hello **readdevicetocloudmessages** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="41dfb-147">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="41dfb-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="41dfb-148">В командной строке в hello **readdevicetocloudmessages** папку, следующая команда tooinstall hello hello **концентраторов событий azure** пакета:</span><span class="sxs-lookup"><span data-stu-id="41dfb-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="41dfb-149">В текстовом редакторе создайте **ReadDeviceToCloudMessages.js** файла в hello **readdevicetocloudmessages** папки.</span><span class="sxs-lookup"><span data-stu-id="41dfb-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="41dfb-150">Добавьте следующее hello `require` инструкции на hello начала hello **ReadDeviceToCloudMessages.js** файла:</span><span class="sxs-lookup"><span data-stu-id="41dfb-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="41dfb-151">Добавьте следующие объявления переменных hello и замените значение заполнителя hello hello центра IoT строку подключения для концентратор.</span><span class="sxs-lookup"><span data-stu-id="41dfb-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="41dfb-152">Добавьте следующие две функции, которые печати выходных данных консоли toohello hello:</span><span class="sxs-lookup"><span data-stu-id="41dfb-152">Add hello following two functions that print output toohello console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="41dfb-153">Добавьте следующий код toocreate hello hello **EventHubClient**откройте tooyour подключения hello центр IoT и Создание приемника для каждой секции.</span><span class="sxs-lookup"><span data-stu-id="41dfb-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="41dfb-154">Это приложение использует фильтр при создании получателя, чтобы hello приемник считывает только сообщения, отправленные tooIoT концентратора после hello получатель начинает выполнение.</span><span class="sxs-lookup"><span data-stu-id="41dfb-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="41dfb-155">Этот фильтр может применяться в тестовой среде, чтобы видеть только hello текущего набора сообщений.</span><span class="sxs-lookup"><span data-stu-id="41dfb-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="41dfb-156">В рабочей среде кода следует убедиться, оно обрабатывает все сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="41dfb-157">Дополнительные сведения см. в разделе hello [как tooprocess сообщения из устройства в облако центра IoT] [ lnk-process-d2c-tutorial] учебника:</span><span class="sxs-lookup"><span data-stu-id="41dfb-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="41dfb-158">Сохраните и закройте hello **ReadDeviceToCloudMessages.js** файла.</span><span class="sxs-lookup"><span data-stu-id="41dfb-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="41dfb-159">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="41dfb-159">Create a simulated device app</span></span>
<span data-ttu-id="41dfb-160">В этом разделе создайте консольное приложение Node.js, которое имитирует устройство, которое отправляет центр IoT tooan сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="41dfb-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="41dfb-161">Создайте пустую папку с именем **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="41dfb-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="41dfb-162">В hello **simulateddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="41dfb-163">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="41dfb-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="41dfb-164">В командной строке в hello **simulateddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:</span><span class="sxs-lookup"><span data-stu-id="41dfb-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="41dfb-165">В текстовом редакторе создайте **SimulatedDevice.js** файла в hello **simulateddevice** папки.</span><span class="sxs-lookup"><span data-stu-id="41dfb-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="41dfb-166">Добавьте следующее hello `require` инструкции на hello начала hello **SimulatedDevice.js** файла:</span><span class="sxs-lookup"><span data-stu-id="41dfb-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="41dfb-167">Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="41dfb-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="41dfb-168">Замените **{youriothostname}** с именем hello hello центра IoT вы создали hello *создать центр IoT* раздела.</span><span class="sxs-lookup"><span data-stu-id="41dfb-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="41dfb-169">Замените **{yourdevicekey}** со значением ключа устройства hello созданный hello *создать удостоверение устройства* раздела:</span><span class="sxs-lookup"><span data-stu-id="41dfb-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="41dfb-170">Добавьте следующие выходные данные функции toodisplay из приложения hello hello:</span><span class="sxs-lookup"><span data-stu-id="41dfb-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="41dfb-171">Создание обратного вызова и использовать hello **setInterval** функции toosend концентратор IoT tooyour сообщение каждую секунду:</span><span class="sxs-lookup"><span data-stu-id="41dfb-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. <span data-ttu-id="41dfb-172">Откройте tooyour подключения hello центр IoT и приступить к отправке сообщений:</span><span class="sxs-lookup"><span data-stu-id="41dfb-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="41dfb-173">Сохраните и закройте hello **SimulatedDevice.js** файла.</span><span class="sxs-lookup"><span data-stu-id="41dfb-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="41dfb-174">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="41dfb-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="41dfb-175">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="41dfb-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="41dfb-176">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="41dfb-176">Run hello apps</span></span>
<span data-ttu-id="41dfb-177">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="41dfb-178">В командной строке в hello **readdevicetocloudmessages** папки, запустите следующие команды toobegin мониторинга вашего центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="41dfb-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Сообщения из устройства в облако node.js центр IoT службы приложения toomonitor][7]
2. <span data-ttu-id="41dfb-180">В командной строке в hello **simulateddevice** папки, запустите hello, следующая команда toobegin отправки центра IoT tooyour данных телеметрии:</span><span class="sxs-lookup"><span data-stu-id="41dfb-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Устройства в облако сообщения toosend приложения node.js центр IoT устройства][8]
3. <span data-ttu-id="41dfb-182">Hello **использование** плитки в hello [портал Azure] [ lnk-portal] показано hello число сообщений, отправляемых toohello центр IoT:</span><span class="sxs-lookup"><span data-stu-id="41dfb-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure портала использование плитки, показывающего количество сообщений, отправляемых tooIoT концентратора][43]

## <a name="next-steps"></a><span data-ttu-id="41dfb-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41dfb-184">Next steps</span></span>
<span data-ttu-id="41dfb-185">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="41dfb-186">Вы использовали устройства удостоверения tooenable hello имитируемые устройства приложения toosend сообщения из устройства в облако toohello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="41dfb-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="41dfb-187">Также было создано приложение, которое отображает hello сообщений, полученных центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="41dfb-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="41dfb-188">Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:</span><span class="sxs-lookup"><span data-stu-id="41dfb-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="41dfb-189">[Подключение устройства к Azure IoT][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="41dfb-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="41dfb-190">[How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))</span><span class="sxs-lookup"><span data-stu-id="41dfb-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="41dfb-191">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)</span><span class="sxs-lookup"><span data-stu-id="41dfb-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="41dfb-192">toolearn tooextend сообщений в масштабе, IoT решение и процесс устройства в облако. в статье hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="41dfb-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
