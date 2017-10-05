---
title: "Приступая к работе с Центром Интернета вещей Azure (Node) | Документация Майкрософт"
description: "Узнайте, как отправлять сообщения из устройства на облако в Центр Интернета вещей Azure с помощью пакетов SDK Интернета вещей для Node.js. Создайте виртуальное устройство и приложения службы для регистрации устройства, отправки сообщений и чтения сообщений из Центра Интернета вещей."
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
ms.openlocfilehash: b27a34c0f1f127628912ad68a002e15cc838b4d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-node"></a><span data-ttu-id="40f6b-104">Подключение виртуального устройства к Центру Интернета вещей с помощью Node</span><span class="sxs-lookup"><span data-stu-id="40f6b-104">Connect your simulated device to your IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="40f6b-105">С помощью этого руководства вы создадите три консольных приложения Node.js:</span><span class="sxs-lookup"><span data-stu-id="40f6b-105">At the end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="40f6b-106">**CreateDeviceIdentity.js**. Создает удостоверение устройства и соответствующий ключ безопасности для подключения имитирующего устройство приложения.</span><span class="sxs-lookup"><span data-stu-id="40f6b-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="40f6b-107">**ReadDeviceToCloudMessages.js**. Отображает данные телеметрии, отправленные приложением, которое имитирует устройство.</span><span class="sxs-lookup"><span data-stu-id="40f6b-107">**ReadDeviceToCloudMessages.js**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="40f6b-108">**SimulatedDevice.js** — подключается к Центру Интернета вещей с созданным ранее удостоверением устройства и отправляет сообщения телеметрии с частотой один раз в секунду с использованием протокола MQTT.</span><span class="sxs-lookup"><span data-stu-id="40f6b-108">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="40f6b-109">Статья о [пакетах SDK для Центра Интернета вещей Azure][lnk-hub-sdks] содержит сведения о различных пакетах SDK, которые можно использовать для создания приложений, которые будут работать на устройствах и в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="40f6b-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="40f6b-110">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="40f6b-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="40f6b-111">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="40f6b-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="40f6b-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="40f6b-112">An active Azure account.</span></span> <span data-ttu-id="40f6b-113">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="40f6b-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="40f6b-114">Теперь центр IoT создан</span><span class="sxs-lookup"><span data-stu-id="40f6b-114">You have now created your IoT hub.</span></span> <span data-ttu-id="40f6b-115">и у вас есть соответствующие имя узла и строка подключения, необходимые для завершения работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="40f6b-115">You have the IoT Hub host name and the IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="40f6b-116">Создание удостоверения устройства</span><span class="sxs-lookup"><span data-stu-id="40f6b-116">Create a device identity</span></span>
<span data-ttu-id="40f6b-117">В этом разделе вам предстоит написать консольное приложение Node.js, которое создает удостоверение устройства в реестре удостоверений в центре IoT.</span><span class="sxs-lookup"><span data-stu-id="40f6b-117">In this section, you create a Node.js console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="40f6b-118">Устройство может подключиться к Центру Интернета вещей, только если в реестре удостоверений есть соответствующая запись.</span><span class="sxs-lookup"><span data-stu-id="40f6b-118">A device can only connect to IoT hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="40f6b-119">Дополнительные сведения см. в разделе, посвященном **реестру удостоверений**, в [руководстве разработчика по Центру Интернета вещей Azure][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="40f6b-119">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="40f6b-120">При запуске этого консольного приложения создается уникальный идентификатор устройства и ключ, с помощью которых выполняется идентификация во время отправки сообщений из устройства в облако для центра IoT.</span><span class="sxs-lookup"><span data-stu-id="40f6b-120">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="40f6b-121">Создайте пустую папку с именем **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="40f6b-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="40f6b-122">В папке **createdeviceidentity** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="40f6b-122">In the **createdeviceidentity** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="40f6b-123">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="40f6b-123">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="40f6b-124">В командной строке в папке **createdeviceidentity** выполните следующую команду, чтобы установить пакет SDK для службы **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="40f6b-124">At your command prompt in the **createdeviceidentity** folder, run the following command to install the **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="40f6b-125">В текстовом редакторе создайте файл **CreateDeviceIdentity.js** в папке **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="40f6b-125">Using a text editor, create a **CreateDeviceIdentity.js** file in the **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="40f6b-126">Добавьте следующую инструкцию `require` в начало файла **CreateDeviceIdentity.js** :</span><span class="sxs-lookup"><span data-stu-id="40f6b-126">Add the following `require` statement at the start of the **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="40f6b-127">Добавьте следующий код в файл **CreateDeviceIdentity.js**, заменив заполнитель строкой подключения к Центру Интернета вещей, созданному в предыдущем разделе:</span><span class="sxs-lookup"><span data-stu-id="40f6b-127">Add the following code to the **CreateDeviceIdentity.js** file and replace the placeholder value with the IoT Hub connection string for the hub you created in the previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="40f6b-128">Добавьте следующий код, чтобы создать определение устройства в реестре удостоверений в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="40f6b-128">Add the following code to create a device definition in the identity registry in your IoT hub.</span></span> <span data-ttu-id="40f6b-129">Этот код создает устройство, если идентификатор устройства отсутствует в реестре удостоверений. В противном случае он возвращает ключ существующего устройства:</span><span class="sxs-lookup"><span data-stu-id="40f6b-129">This code creates a device if the device ID does not exist in the identity registry, otherwise it returns the key of the existing device:</span></span>
   
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

7. <span data-ttu-id="40f6b-130">Сохраните и закройте файл **CreateDeviceIdentity.js** .</span><span class="sxs-lookup"><span data-stu-id="40f6b-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="40f6b-131">Чтобы запустить приложение **createdeviceidentity**, выполните в командной строке в папке createdeviceidentity следующую команду:</span><span class="sxs-lookup"><span data-stu-id="40f6b-131">To run the **createdeviceidentity** application, execute the following command at the command prompt in the createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="40f6b-132">Запишите значения полей **Идентификатор устройства** и **Device key** (Ключ устройства).</span><span class="sxs-lookup"><span data-stu-id="40f6b-132">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="40f6b-133">Эти значения понадобятся вам позже, когда вы будете создавать приложение, которое подключается к центру IoT как устройство.</span><span class="sxs-lookup"><span data-stu-id="40f6b-133">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="40f6b-134">В реестре удостоверений в Центре Интернета вещей хранятся только идентификаторы устройств, необходимые для безопасного доступа к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="40f6b-134">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="40f6b-135">В этом реестре хранятся идентификаторы и ключи устройств, которые используются в качестве учетных данных безопасности, и флажок включения или выключения, который позволяет вам отключить доступ для отдельного устройства.</span><span class="sxs-lookup"><span data-stu-id="40f6b-135">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="40f6b-136">Если в приложении необходимо хранить другие метаданные для конкретного устройства, следует использовать хранилище конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="40f6b-136">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="40f6b-137">Дополнительные сведения см. в [руководстве для разработчиков Центра Интернета вещей][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="40f6b-137">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="40f6b-138">Получение сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="40f6b-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="40f6b-139">В этом разделе вы научитесь создавать консольное приложение Node.js, которое считывает сообщения, передаваемые с устройства в облако из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="40f6b-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="40f6b-140">Центр Интернета вещей предоставляет совместимую с [концентраторами событий][lnk-event-hubs-overview] конечную точку для считывания сообщений, передаваемых с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="40f6b-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="40f6b-141">Для простоты в этом руководстве создается базовый модуль чтения, который не подходит для развертывания с высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="40f6b-141">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="40f6b-142">В руководстве по [обработке сообщений, передаваемых с устройства в облако][lnk-process-d2c-tutorial], показано, как обрабатывать такие сообщения в больших количествах.</span><span class="sxs-lookup"><span data-stu-id="40f6b-142">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="40f6b-143">В руководстве по [началу работы с концентраторами событий][lnk-eventhubs-tutorial] приведены дополнительные сведения о том, как обрабатываются сообщения из концентраторов событий. Это руководство применимо к конечным точкам Центра Интернета вещей, совместимым с концентраторами событий.</span><span class="sxs-lookup"><span data-stu-id="40f6b-143">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="40f6b-144">Совместимая с концентраторами событий конечная точка для чтения сообщений, отправляемых с устройства в облако, всегда использует протокол AMQP.</span><span class="sxs-lookup"><span data-stu-id="40f6b-144">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="40f6b-145">Создайте пустую папку с именем **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="40f6b-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="40f6b-146">В папке **readdevicetocloudmessages** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="40f6b-146">In the **readdevicetocloudmessages** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="40f6b-147">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="40f6b-147">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="40f6b-148">В командной строке в папке **readdevicetocloudmessages** выполните следующую команду, чтобы установить пакет **azure-event-hubs**:</span><span class="sxs-lookup"><span data-stu-id="40f6b-148">At your command prompt in the **readdevicetocloudmessages** folder, run the following command to install the **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="40f6b-149">В текстовом редакторе создайте файл **ReadDeviceToCloudMessages.js** в папке **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="40f6b-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in the **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="40f6b-150">Добавьте следующие инструкции `require` в начало файла **ReadDeviceToCloudMessages.js** :</span><span class="sxs-lookup"><span data-stu-id="40f6b-150">Add the following `require` statements at the start of the **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="40f6b-151">Добавьте следующее объявление переменной и замените заполнитель строкой подключения к своему экземпляру Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="40f6b-151">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="40f6b-152">Добавьте следующие две функции для вывода результатов на консоль:</span><span class="sxs-lookup"><span data-stu-id="40f6b-152">Add the following two functions that print output to the console:</span></span>
   
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
7. <span data-ttu-id="40f6b-153">Добавьте следующий код, чтобы создать **EventHubClient**, открыть подключение к Центру Интернета вещей и создать получатель для каждой секции.</span><span class="sxs-lookup"><span data-stu-id="40f6b-153">Add the following code to create the **EventHubClient**, open the connection to your IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="40f6b-154">Это приложение использует фильтр во время создания приемника, чтобы приемник считывал только сообщения, отправленные в центр IoT после запуска получателя.</span><span class="sxs-lookup"><span data-stu-id="40f6b-154">This application uses a filter when it creates a receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="40f6b-155">Этот фильтр удобно использовать в тестовой среде для просмотра только текущего набора сообщений.</span><span class="sxs-lookup"><span data-stu-id="40f6b-155">This filter is useful in a test environment so you see just the current set of messages.</span></span> <span data-ttu-id="40f6b-156">В рабочей среде убедитесь, что ваш код обрабатывает все сообщения.</span><span class="sxs-lookup"><span data-stu-id="40f6b-156">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="40f6b-157">Дополнительные сведения см. в руководстве [по обработке сообщений Центра Интернета вещей, отправляемых с устройства в облако][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="40f6b-157">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
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
8. <span data-ttu-id="40f6b-158">Сохраните и закройте файл **ReadDeviceToCloudMessages.js** .</span><span class="sxs-lookup"><span data-stu-id="40f6b-158">Save and close the **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="40f6b-159">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="40f6b-159">Create a simulated device app</span></span>
<span data-ttu-id="40f6b-160">В этом разделе вам предстоит создать консольное приложение Node.js, которое имитирует устройство, отправляющее сообщения с устройства в облако в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="40f6b-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="40f6b-161">Создайте пустую папку с именем **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="40f6b-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="40f6b-162">В папке **simulateddevice** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="40f6b-162">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="40f6b-163">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="40f6b-163">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="40f6b-164">В командной строке в папке **simulateddevice** выполните следующую команду, чтобы установить пакет SDK для устройства **azure-iot-device** и пакет **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="40f6b-164">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="40f6b-165">В текстовом редакторе создайте файл **SimulatedDevice.js** в папке **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="40f6b-165">Using a text editor, create a **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="40f6b-166">Добавьте следующие инструкции `require` в начало файла **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="40f6b-166">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="40f6b-167">Добавьте переменную **connectionString**, чтобы создать с ее помощью экземпляр **клиента**.</span><span class="sxs-lookup"><span data-stu-id="40f6b-167">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="40f6b-168">Замените **{youriothostname}** именем центра IoT, созданного в разделе *Создание центра IoT* .</span><span class="sxs-lookup"><span data-stu-id="40f6b-168">Replace **{youriothostname}** with the name of the IoT hub you created the *Create an IoT Hub* section.</span></span> <span data-ttu-id="40f6b-169">Замените **{yourdevicekey}** ключом устройства, созданным в разделе *Создание удостоверения устройства* :</span><span class="sxs-lookup"><span data-stu-id="40f6b-169">Replace **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="40f6b-170">Добавьте следующую функцию для вывода данных приложения:</span><span class="sxs-lookup"><span data-stu-id="40f6b-170">Add the following function to display output from the application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="40f6b-171">Создайте обратный вызов и используйте функцию **setInterval**, чтобы отправлять сообщение в Центр Интернета вещей каждую секунду:</span><span class="sxs-lookup"><span data-stu-id="40f6b-171">Create a callback and use the **setInterval** function to send a message to your IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. <span data-ttu-id="40f6b-172">Откройте подключение к центру IoT и начните отправку сообщений.</span><span class="sxs-lookup"><span data-stu-id="40f6b-172">Open the connection to your IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="40f6b-173">Сохраните и закройте файл **SimulatedDevice.js** .</span><span class="sxs-lookup"><span data-stu-id="40f6b-173">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="40f6b-174">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="40f6b-174">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="40f6b-175">В рабочем коде следует реализовать политики повторных попыток (например, с экспоненциальной задержкой), как указано в статье [Обработка временного сбоя][lnk-transient-faults] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="40f6b-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="40f6b-176">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="40f6b-176">Run the apps</span></span>
<span data-ttu-id="40f6b-177">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="40f6b-177">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="40f6b-178">В командной строке в папке **readdevicetocloudmessages** выполните следующую команду, чтобы начать наблюдение за Центром Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="40f6b-178">At a command prompt in the **readdevicetocloudmessages** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Приложение службы Центра Интернета вещей на платформе Node.js для мониторинга сообщений, отправляемых с устройства в облако][7]
2. <span data-ttu-id="40f6b-180">В командной строке в папке **simulateddevice** выполните следующую команду, чтобы начать отправку данных телеметрии в Центр Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="40f6b-180">At a command prompt in the **simulateddevice** folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Приложение устройства Центра Интернета вещей на платформе Node.js для отправки сообщений с устройства в облако][8]
3. <span data-ttu-id="40f6b-182">На плитке **Использование** на [портале Azure][lnk-portal] отображается количество сообщений, отправленных в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="40f6b-182">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![Плитка "Использование" на портале Azure, отображающая количество сообщений, отправленных в Центр Интернета вещей][43]

## <a name="next-steps"></a><span data-ttu-id="40f6b-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40f6b-184">Next steps</span></span>
<span data-ttu-id="40f6b-185">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="40f6b-185">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="40f6b-186">Это удостоверение позволяет приложению виртуального устройства отправлять в Центр Интернета вещей сообщения, передаваемые из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="40f6b-186">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="40f6b-187">Кроме того, мы создали приложение, которое отображает сообщения, полученные Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="40f6b-187">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="40f6b-188">Чтобы продолжить знакомство с Центром Интернета вещей и изучить другие сценарии Интернета вещей, см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="40f6b-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="40f6b-189">[Подключение устройства к Azure IoT][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="40f6b-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="40f6b-190">[How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))</span><span class="sxs-lookup"><span data-stu-id="40f6b-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="40f6b-191">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)</span><span class="sxs-lookup"><span data-stu-id="40f6b-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="40f6b-192">Сведения о том, как расширить решение для Интернета вещей и обрабатывать сообщения, отправляемые с устройства в облако в большом количестве, см. [здесь][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="40f6b-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
