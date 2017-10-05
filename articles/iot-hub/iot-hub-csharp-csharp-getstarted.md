---
title: "Приступая к работе с Центром Интернета вещей Azure (.NET) | Документация Майкрософт"
description: "Узнайте, как отправлять сообщения из устройства в облако в Центр Интернета вещей Azure с помощью пакетов SDK для Центра Интернета вещей для .NET. Создайте виртуальное устройство и приложения службы для регистрации устройства, отправки сообщений и чтения сообщений из Центра Интернета вещей."
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
ms.openlocfilehash: 69296eb9ac2a74a97b632d27733a6a06500b4abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-net"></a><span data-ttu-id="cdffd-104">Подключение устройства к Центру Интернета вещей с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="cdffd-104">Connect your device to your IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="cdffd-105">В конце этого руководства у вас будет три консольных приложения .NET:</span><span class="sxs-lookup"><span data-stu-id="cdffd-105">At the end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="cdffd-106">**CreateDeviceIdentity** — создает удостоверение устройства и соответствующий ключ безопасности для подключения к приложению устройства.</span><span class="sxs-lookup"><span data-stu-id="cdffd-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="cdffd-107">**ReadDeviceToCloudMessages** — отображает данные телеметрии, отправленные приложением устройства.</span><span class="sxs-lookup"><span data-stu-id="cdffd-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="cdffd-108">**SimulatedDevice** — подключается к Центру Интернета вещей с созданным ранее удостоверением устройства и один раз в секунду отправляет сообщения телеметрии с использованием протокола MQTT.</span><span class="sxs-lookup"><span data-stu-id="cdffd-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span></span>

<span data-ttu-id="cdffd-109">Вы можете скачать или клонировать решения Visual Studio, которые содержат три приложения с Github.</span><span class="sxs-lookup"><span data-stu-id="cdffd-109">You can download or clone the Visual Studio solution, which contains the three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="cdffd-110">Статья о [пакетах SDK для Центра Интернета вещей Azure][lnk-hub-sdks] содержит сведения о различных пакетах SDK, которые можно использовать для создания приложений, которые будут работать на устройствах и в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="cdffd-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="cdffd-111">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="cdffd-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="cdffd-112">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cdffd-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="cdffd-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="cdffd-113">An active Azure account.</span></span> <span data-ttu-id="cdffd-114">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="cdffd-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="cdffd-115">Теперь у вас есть Центр Интернета вещей, а также имя узла и строка подключения Центра Интернета вещей, необходимые для завершения работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="cdffd-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="cdffd-116">Получение сообщений с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="cdffd-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="cdffd-117">В этом разделе вы создадите консольное приложение .NET, которое считывает сообщения, передаваемые с устройства в облако из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="cdffd-118">Центр Интернета вещей предоставляет совместимую с [концентраторами событий Azure][lnk-event-hubs-overview] конечную точку для считывания сообщений, отправляемых с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="cdffd-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="cdffd-119">Для простоты в этом руководстве создается базовый модуль чтения, который не подходит для развертывания с высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="cdffd-119">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="cdffd-120">В руководстве по [обработке сообщений, отправляемых с устройства в облако][lnk-process-d2c-tutorial], показано, как обрабатывать такие сообщения в больших количествах.</span><span class="sxs-lookup"><span data-stu-id="cdffd-120">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="cdffd-121">Дополнительные сведения о способах обработки сообщений из концентраторов событий см. в руководстве [Приступая к работе с концентраторами событий][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="cdffd-121">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="cdffd-122">(Это руководство относится к конечным точкам, совместимым с концентраторами событий в Центре Интернета вещей.)</span><span class="sxs-lookup"><span data-stu-id="cdffd-122">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="cdffd-123">Совместимая с концентраторами событий конечная точка для чтения сообщений, отправляемых с устройства в облако, всегда использует протокол AMQP.</span><span class="sxs-lookup"><span data-stu-id="cdffd-123">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="cdffd-124">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="cdffd-124">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="cdffd-125">Убедитесь, что указана версия платформы .NET 4.5.1 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="cdffd-125">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="cdffd-126">Присвойте проекту имя **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="cdffd-126">Name the project **ReadDeviceToCloudMessages**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][10a]

2. <span data-ttu-id="cdffd-128">В обозревателе решений щелкните правой кнопкой мыши проект **ReadDeviceToCloudMessages** и выберите **Manage NuGet Packages** (Управление пакетами NuGet).</span><span class="sxs-lookup"><span data-stu-id="cdffd-128">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="cdffd-129">В окне **Диспетчер пакетов NuGet** найдите пакет **WindowsAzure.ServiceBus**, щелкните **Установить** и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="cdffd-129">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span></span> <span data-ttu-id="cdffd-130">Эта процедура выполняет загрузку и установку [служебной шины Azure][lnk-servicebus-nuget] со всеми ее зависимостями, а также добавляет соответствующую ссылку.</span><span class="sxs-lookup"><span data-stu-id="cdffd-130">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="cdffd-131">С помощью этого пакета приложение может подключаться к конечной точке, совместимой с концентратором событий, в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-131">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="cdffd-132">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="cdffd-132">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="cdffd-133">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="cdffd-133">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="cdffd-134">Замените значения заполнителей строкой подключения к Центру Интернета вещей, созданному в разделе "Создание Центра Интернета вещей".</span><span class="sxs-lookup"><span data-stu-id="cdffd-134">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="cdffd-135">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="cdffd-135">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="cdffd-136">Этот метод использует экземпляр **EventHubReceiver** для получения сообщений из всех разделов Центра Интернета вещей, которые отвечают за прием сообщений, передаваемых с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="cdffd-136">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="cdffd-137">Обратите внимание, что при создании объекта `DateTime.Now`EventHubReceiver **параметр**  передается так, чтобы получать только сообщения, отправленные после его запуска.</span><span class="sxs-lookup"><span data-stu-id="cdffd-137">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="cdffd-138">Этот фильтр удобно использовать в тестовой среде для просмотра текущего набора сообщений.</span><span class="sxs-lookup"><span data-stu-id="cdffd-138">This filter is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="cdffd-139">В рабочей среде убедитесь, что ваш код обрабатывает все сообщения.</span><span class="sxs-lookup"><span data-stu-id="cdffd-139">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="cdffd-140">Дополнительные сведения см. в руководстве [по обработке сообщений Центра Интернета вещей, отправляемых с устройства в облако][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="cdffd-140">For more information, see the tutorial [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="cdffd-141">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="cdffd-141">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
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

## <a name="create-a-device-app"></a><span data-ttu-id="cdffd-142">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="cdffd-142">Create a device app</span></span>

<span data-ttu-id="cdffd-143">В этом разделе вы создаете консольное приложение .NET, которое имитирует устройство, отправляющее сообщения с устройства в облако в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="cdffd-144">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="cdffd-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="cdffd-145">Убедитесь, что указана версия платформы .NET 4.5.1 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="cdffd-145">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="cdffd-146">Назовите проект **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="cdffd-146">Name the project **SimulatedDevice**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][10b]

2. <span data-ttu-id="cdffd-148">В обозревателе решений щелкните правой кнопкой мыши проект **SimulatedDevice** и выберите **Manage NuGet Packages** (Управление пакетами NuGet).</span><span class="sxs-lookup"><span data-stu-id="cdffd-148">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="cdffd-149">В окне **Диспетчер пакетов NuGet** нажмите кнопку **Обзор**, найдите **Microsoft.Azure.Devices.Client**, щелкните **Установить**, чтобы установить пакет **Microsoft.Azure.Devices.Client**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="cdffd-149">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="cdffd-150">В результате выполняется скачивание и установка [пакета NuGet SDK для устройств Azure IoT][lnk-device-nuget] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="cdffd-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="cdffd-151">Добавьте следующий оператор `using` в начало файла **Program.cs** .</span><span class="sxs-lookup"><span data-stu-id="cdffd-151">Add the following `using` statement at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="cdffd-152">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="cdffd-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="cdffd-153">Замените `{iot hub hostname}` на имя узла Центра Интернета вещей, полученное в разделе "Создание Центра Интернета вещей".</span><span class="sxs-lookup"><span data-stu-id="cdffd-153">Substitute `{iot hub hostname}` with the IoT hub host name you retrieved in the "Create an IoT hub" section.</span></span> <span data-ttu-id="cdffd-154">Замените `{device key}` на ключ устройства, полученный в разделе "Создание удостоверение устройства".</span><span class="sxs-lookup"><span data-stu-id="cdffd-154">Substitute `{device key}` with the device key you retrieved in the "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="cdffd-155">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="cdffd-155">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="cdffd-156">Этот метод отправляет новое сообщение с устройства в облако каждую секунду.</span><span class="sxs-lookup"><span data-stu-id="cdffd-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="cdffd-157">Сообщение содержит объект сериализации JSON с идентификатором устройства и случайные числа, что позволяет имитировать датчик температуры и влажности.</span><span class="sxs-lookup"><span data-stu-id="cdffd-157">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="cdffd-158">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="cdffd-158">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="cdffd-159">По умолчанию метод **Create** в приложении .NET Framework создает экземпляр **DeviceClient**, который использует протокол AMQP для связи с Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-159">By default, the **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span></span> <span data-ttu-id="cdffd-160">Для использования протокола MQTT или HTTP используйте переопределение метода **Create**, чтобы указать протокол.</span><span class="sxs-lookup"><span data-stu-id="cdffd-160">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span></span> <span data-ttu-id="cdffd-161">Клиенты UWP и PCL по умолчанию используют протокол HTTP.</span><span class="sxs-lookup"><span data-stu-id="cdffd-161">UWP and PCL clients use the HTTP protocol by default.</span></span> <span data-ttu-id="cdffd-162">Если вы используете протокол HTTPS, вам также следует добавить в свой проект пакет NuGet **Microsoft.AspNet.WebApi.Client**, чтобы включить пространство имен **System.Net.Http.Formatting**.</span><span class="sxs-lookup"><span data-stu-id="cdffd-162">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="cdffd-163">В этом руководстве описываются шаги по созданию приложения устройства Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-163">This tutorial takes you through the steps to create an IoT Hub device app.</span></span> <span data-ttu-id="cdffd-164">Вы также можете использовать расширение [подключенной службы для Центра Интернета вещей Azure][lnk-connected-service] (Visual Studio), чтобы добавить необходимый код в приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="cdffd-164">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span></span>

> [!NOTE]
> <span data-ttu-id="cdffd-165">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="cdffd-165">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="cdffd-166">В рабочем коде следует реализовать политики повторных попыток (например, с экспоненциальной задержкой), как указано в статье [Обработка временного сбоя][lnk-transient-faults] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="cdffd-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="cdffd-167">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="cdffd-167">Run the apps</span></span>

<span data-ttu-id="cdffd-168">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="cdffd-168">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="cdffd-169">В обозревателе решений Visual Studio щелкните правой кнопкой мыши решение и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="cdffd-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="cdffd-170">Выберите **Несколько запускаемых проектов**, а затем – **Запуск** в качестве действия для проектов **ReadDeviceToCloudMessages** и **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="cdffd-170">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Свойства запускаемого проекта][41]

2. <span data-ttu-id="cdffd-172">Нажмите клавишу **F5** , чтобы запустить оба приложения.</span><span class="sxs-lookup"><span data-stu-id="cdffd-172">Press **F5** to start both apps running.</span></span> <span data-ttu-id="cdffd-173">В выходных данных консоли для приложения **SimulatedDevice** будут отображаться сообщения, которые приложение устройства отправляет в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-173">The console output from the **SimulatedDevice** app shows the messages your device app sends to your IoT hub.</span></span> <span data-ttu-id="cdffd-174">В выходных данных консоли для приложения **ReadDeviceToCloudMessages** будут отображаться сообщения, которые получает Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-174">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span></span>

    ![Выходные данные консоли для приложений][42]

3. <span data-ttu-id="cdffd-176">На плитке **Использование** на [портале Azure][lnk-portal] отображается количество сообщений, отправленных в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-176">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Плитка "Использование" на портале Azure][43]

## <a name="next-steps"></a><span data-ttu-id="cdffd-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cdffd-178">Next steps</span></span>

<span data-ttu-id="cdffd-179">С помощью этого руководства вы настроили Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений этого Центра.</span><span class="sxs-lookup"><span data-stu-id="cdffd-179">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="cdffd-180">Это удостоверение позволяет приложению устройства отправлять в Центр Интернета вещей сообщения, передаваемые из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="cdffd-180">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="cdffd-181">Кроме того, мы создали приложение, которое отображает сообщения, полученные Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cdffd-181">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="cdffd-182">Чтобы продолжить знакомство с Центром Интернета вещей и изучить другие сценарии Интернета вещей, см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="cdffd-182">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="cdffd-183">[Подключение устройства к Azure IoT][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="cdffd-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="cdffd-184">[How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))</span><span class="sxs-lookup"><span data-stu-id="cdffd-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="cdffd-185">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)</span><span class="sxs-lookup"><span data-stu-id="cdffd-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="cdffd-186">Сведения о том, как расширить решение для Интернета вещей и обрабатывать сообщения, отправляемые с устройства в облако в большом количестве, см. [здесь][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="cdffd-186">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
