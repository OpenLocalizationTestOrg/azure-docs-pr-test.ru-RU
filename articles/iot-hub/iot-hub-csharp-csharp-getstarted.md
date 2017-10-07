---
title: "aaaGet к работе с Azure IoT Hub (.NET) | Документы Microsoft"
description: "Узнайте, как toosend устройства в облако сообщений tooAzure центр IoT с помощью IoT пакеты SDK для .NET. Создать имитированное устройство и службы приложений tooregister устройства, отправлять сообщения и чтения сообщений из центра IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="183f8-104">Подключиться к центр IoT tooyour устройства с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="183f8-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="183f8-105">В конце этого учебника hello имеются три консольных приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="183f8-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="183f8-106">**CreateDeviceIdentity**, которая создает удостоверения устройства и связана защита ключа tooconnect приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="183f8-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="183f8-107">**ReadDeviceToCloudMessages**, которая отображает hello телеметрии, отправленные приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="183f8-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="183f8-108">**SimulatedDevice**, который соединяет центр IoT tooyour с удостоверения устройства hello, созданного ранее и отправляет сообщение телеметрии каждую секунду с помощью протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="183f8-109">Можно загрузить или клонировать решения Visual Studio hello, содержащий три приложения hello из Github.</span><span class="sxs-lookup"><span data-stu-id="183f8-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="183f8-110">Сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun приложений на устройствах и серверной части вашего решения, в разделе [пакеты SDK Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="183f8-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="183f8-111">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="183f8-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="183f8-112">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="183f8-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="183f8-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="183f8-113">An active Azure account.</span></span> <span data-ttu-id="183f8-114">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="183f8-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="183f8-115">Вы создали концентратор IoT, и у вас есть имя узла hello и центр IoT строку соединения, необходимость toocomplete hello конца данного учебника.</span><span class="sxs-lookup"><span data-stu-id="183f8-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="183f8-116">Получение сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="183f8-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="183f8-117">В этом разделе вы создадите консольное приложение .NET, которое считывает сообщения, передаваемые с устройства в облако из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="183f8-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="183f8-118">Центр IoT предоставляет [концентраторов событий Azure][lnk-event-hubs-overview]-совместимую конечную точку tooenable вам сообщения tooread устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="183f8-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="183f8-119">простые действия tookeep, данный учебник создает основные средства чтения, не подходит для развертывания высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="183f8-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="183f8-120">способ tooprocess устройства в облако сообщений в масштабе, toolearn разделе hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="183f8-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="183f8-121">Дополнительные сведения о том, как tooprocess сообщений из концентраторов событий см. в разделе hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="183f8-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="183f8-122">(Этот учебник содержит конечные точки применимо toohello события концентратора IoT Hub совместимой.)</span><span class="sxs-lookup"><span data-stu-id="183f8-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="183f8-123">Hello концентратора событий-совместимой конечной точки для чтения сообщения из устройства в облако, всегда использует протокол AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="183f8-124">В Visual Studio, добавить Visual C# Windows классического проекта toohello текущее решение, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="183f8-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="183f8-125">Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="183f8-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="183f8-126">Имя проекта hello **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="183f8-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][10a]

2. <span data-ttu-id="183f8-128">В обозревателе решений щелкните правой кнопкой мыши hello **ReadDeviceToCloudMessages** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="183f8-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="183f8-129">В hello **диспетчера пакетов NuGet** найдите **WindowsAzure.ServiceBus**выберите **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="183f8-130">Эта процедура загрузки, устанавливает и добавляет ссылку слишком[Azure Service Bus][lnk-servicebus-nuget], с его зависимости.</span><span class="sxs-lookup"><span data-stu-id="183f8-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="183f8-131">Этот пакет позволяет hello tooconnect приложения toohello конечной точке совместимое концентратора событий в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="183f8-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="183f8-132">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="183f8-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="183f8-133">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="183f8-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="183f8-134">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, который вы создали в разделе «Создать центр IoT» hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="183f8-135">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="183f8-135">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    <span data-ttu-id="183f8-136">Этот метод использует **EventHubReceiver** экземпляр tooreceive сообщения из всех hello IoT hub устройства в облако получать секции.</span><span class="sxs-lookup"><span data-stu-id="183f8-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="183f8-137">Обратите внимание на то, как можно передать `DateTime.Now` параметр при создании hello **EventHubReceiver** объекта, чтобы он получает только сообщения, отправленные после ее запуска.</span><span class="sxs-lookup"><span data-stu-id="183f8-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="183f8-138">Этот фильтр может применяться в тестовой среде, чтобы можно было видеть текущий набор сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="183f8-139">В рабочей среде кода следует убедиться, оно обрабатывает все сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="183f8-140">Дополнительные сведения см. в разделе учебника hello [как tooprocess сообщения из устройства в облако центра IoT][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="183f8-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="183f8-141">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="183f8-141">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="183f8-142">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="183f8-142">Create a device app</span></span>

<span data-ttu-id="183f8-143">В этом разделе создайте консольное приложение .NET, которое имитирует устройство, которое отправляет центр IoT tooan сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="183f8-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="183f8-144">В Visual Studio, добавить Visual C# Windows классического проекта toohello текущее решение, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="183f8-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="183f8-145">Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="183f8-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="183f8-146">Имя проекта hello **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="183f8-146">Name hello project **SimulatedDevice**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][10b]

2. <span data-ttu-id="183f8-148">В обозревателе решений щелкните правой кнопкой мыши hello **SimulatedDevice** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="183f8-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="183f8-149">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **Microsoft.Azure.Devices.Client**выберите **установить** tooinstall hello **Microsoft.Azure.Devices.Client** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="183f8-150">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакет SDK NuGet устройства Azure IoT] [ lnk-device-nuget] и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="183f8-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="183f8-151">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="183f8-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="183f8-152">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="183f8-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="183f8-153">Замена `{iot hub hostname}` именем hello IoT hub узла вы получили в разделе «Создание центра IoT» hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="183f8-154">Замена `{device key}` ключом hello устройства вы получили в разделе «Создание удостоверение устройства» hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="183f8-155">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="183f8-155">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    <span data-ttu-id="183f8-156">Этот метод отправляет новое сообщение с устройства в облако каждую секунду.</span><span class="sxs-lookup"><span data-stu-id="183f8-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="183f8-157">приветственное сообщение содержит объект с Идентификатором устройства hello сериализации JSON и случайным образом toosimulate номера датчика температуры и влажности датчика.</span><span class="sxs-lookup"><span data-stu-id="183f8-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="183f8-158">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="183f8-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="183f8-159">По умолчанию hello **создать** метод в приложении .NET Framework создает **DeviceClient** экземпляр, который использует toocommunicate протокола AMQP hello с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="183f8-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="183f8-160">hello toouse MQTT или HTTP-протокола, используйте переопределение hello hello **создать** метод, который позволяет toospecify hello протокола.</span><span class="sxs-lookup"><span data-stu-id="183f8-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="183f8-161">UWP и PCL клиентов по умолчанию используется протокол HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="183f8-162">При использовании протокола hello HTTP, следует также добавить hello **Microsoft.AspNet.WebApi.Client** NuGet пакета tooyour проекта tooinclude hello **System.Net.Http.Formatting** пространства имен.</span><span class="sxs-lookup"><span data-stu-id="183f8-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="183f8-163">Этот учебник поможет выполнить toocreate действия hello центра IoT приложения для устройств.</span><span class="sxs-lookup"><span data-stu-id="183f8-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="183f8-164">Можно также использовать hello [подключенной службы для Azure IoT Hub] [ lnk-connected-service] Visual Studio расширения tooadd hello необходимый код tooyour приложения для устройств.</span><span class="sxs-lookup"><span data-stu-id="183f8-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="183f8-165">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="183f8-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="183f8-166">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="183f8-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="183f8-167">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="183f8-167">Run hello apps</span></span>

<span data-ttu-id="183f8-168">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="183f8-169">В обозревателе решений Visual Studio щелкните правой кнопкой мыши решение и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="183f8-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="183f8-170">Выберите **несколько запускаемых проектов**, а затем выберите **запустить** как действие hello для обоих hello **ReadDeviceToCloudMessages** и **SimulatedDevice** проектов.</span><span class="sxs-lookup"><span data-stu-id="183f8-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Свойства запускаемого проекта][41]

2. <span data-ttu-id="183f8-172">Нажмите клавишу **F5** toostart обоих приложений под управлением.</span><span class="sxs-lookup"><span data-stu-id="183f8-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="183f8-173">Здравствуйте, вывод на консоль из hello **SimulatedDevice** приложение устройство отправляет центр IoT tooyour сообщений hello показано приложение.</span><span class="sxs-lookup"><span data-stu-id="183f8-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="183f8-174">Здравствуйте, вывод на консоль из hello **ReadDeviceToCloudMessages** приложение показывает сообщения приветствия, который принимает ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="183f8-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Выходные данные консоли для приложений][42]

3. <span data-ttu-id="183f8-176">Hello **использование** плитки в hello [портал Azure] [ lnk-portal] показано hello число сообщений, отправляемых toohello центр IoT:</span><span class="sxs-lookup"><span data-stu-id="183f8-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Плитка "Использование" на портале Azure][43]

## <a name="next-steps"></a><span data-ttu-id="183f8-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="183f8-178">Next steps</span></span>

<span data-ttu-id="183f8-179">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="183f8-180">Вы использовали устройства удостоверения tooenable hello устройства приложения toosend сообщения из устройства в облако toohello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="183f8-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="183f8-181">Также было создано приложение, которое отображает hello сообщений, полученных центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="183f8-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="183f8-182">Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:</span><span class="sxs-lookup"><span data-stu-id="183f8-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="183f8-183">[Подключение устройства к Azure IoT][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="183f8-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="183f8-184">[How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))</span><span class="sxs-lookup"><span data-stu-id="183f8-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="183f8-185">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)</span><span class="sxs-lookup"><span data-stu-id="183f8-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="183f8-186">toolearn tooextend сообщений в масштабе, IoT решение и процесс устройства в облако. в статье hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="183f8-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
