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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>Подключиться к центр IoT tooyour устройства с помощью .NET

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

В конце этого учебника hello имеются три консольных приложений .NET.

* **CreateDeviceIdentity**, которая создает удостоверения устройства и связана защита ключа tooconnect приложение устройства.
* **ReadDeviceToCloudMessages**, которая отображает hello телеметрии, отправленные приложение устройства.
* **SimulatedDevice**, который соединяет центр IoT tooyour с удостоверения устройства hello, созданного ранее и отправляет сообщение телеметрии каждую секунду с помощью протокола MQTT hello.

Можно загрузить или клонировать решения Visual Studio hello, содержащий три приложения hello из Github.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun приложений на устройствах и серверной части вашего решения, в разделе [пакеты SDK Azure IoT][lnk-hub-sdks].

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017.
* Активная учетная запись Azure. Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Вы создали концентратор IoT, и у вас есть имя узла hello и центр IoT строку соединения, необходимость toocomplete hello конца данного учебника.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Получение сообщений с устройства в облако
В этом разделе вы создадите консольное приложение .NET, которое считывает сообщения, передаваемые с устройства в облако из Центра Интернета вещей. Центр IoT предоставляет [концентраторов событий Azure][lnk-event-hubs-overview]-совместимую конечную точку tooenable вам сообщения tooread устройства в облако. простые действия tookeep, данный учебник создает основные средства чтения, не подходит для развертывания высокой пропускной способностью. способ tooprocess устройства в облако сообщений в масштабе, toolearn разделе hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника. Дополнительные сведения о том, как tooprocess сообщений из концентраторов событий см. в разделе hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника. (Этот учебник содержит конечные точки применимо toohello события концентратора IoT Hub совместимой.)

> [!NOTE]
> Hello концентратора событий-совместимой конечной точки для чтения сообщения из устройства в облако, всегда использует протокол AMQP hello.

1. В Visual Studio, добавить Visual C# Windows классического проекта toohello текущее решение, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта. Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии. Имя проекта hello **ReadDeviceToCloudMessages**.

    ![Новый проект классического приложения Windows на языке Visual C#][10a]

2. В обозревателе решений щелкните правой кнопкой мыши hello **ReadDeviceToCloudMessages** проекта, а затем нажмите кнопку **управление пакетами NuGet**.

3. В hello **диспетчера пакетов NuGet** найдите **WindowsAzure.ServiceBus**выберите **установить**и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет ссылку слишком[Azure Service Bus][lnk-servicebus-nuget], с его зависимости. Этот пакет позволяет hello tooconnect приложения toohello конечной точке совместимое концентратора событий в концентратор IoT.

4. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Добавьте следующие поля toohello hello **программы** класса. Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, который вы создали в разделе «Создать центр IoT» hello.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Добавьте следующий метод toohello hello **программы** класса:

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

    Этот метод использует **EventHubReceiver** экземпляр tooreceive сообщения из всех hello IoT hub устройства в облако получать секции. Обратите внимание на то, как можно передать `DateTime.Now` параметр при создании hello **EventHubReceiver** объекта, чтобы он получает только сообщения, отправленные после ее запуска. Этот фильтр может применяться в тестовой среде, чтобы можно было видеть текущий набор сообщений hello. В рабочей среде кода следует убедиться, оно обрабатывает все сообщения hello. Дополнительные сведения см. в разделе учебника hello [как tooprocess сообщения из устройства в облако центра IoT][lnk-process-d2c-tutorial].

7. Наконец, добавьте следующие строки toohello hello **Main** метод:

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

## <a name="create-a-device-app"></a>Создание приложения устройства

В этом разделе создайте консольное приложение .NET, которое имитирует устройство, которое отправляет центр IoT tooan сообщения из устройства в облако.

1. В Visual Studio, добавить Visual C# Windows классического проекта toohello текущее решение, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта. Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии. Имя проекта hello **SimulatedDevice**.

    ![Новый проект классического приложения Windows на языке Visual C#][10b]

2. В обозревателе решений щелкните правой кнопкой мыши hello **SimulatedDevice** проекта, а затем нажмите кнопку **управление пакетами NuGet**.

3. В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **Microsoft.Azure.Devices.Client**выберите **установить** tooinstall hello **Microsoft.Azure.Devices.Client** пакета и примите условия использования hello. Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакет SDK NuGet устройства Azure IoT] [ lnk-device-nuget] и его зависимости.

4. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Добавьте следующие поля toohello hello **программы** класса. Замена `{iot hub hostname}` именем hello IoT hub узла вы получили в разделе «Создание центра IoT» hello. Замена `{device key}` ключом hello устройства вы получили в разделе «Создание удостоверение устройства» hello.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Добавьте следующий метод toohello hello **программы** класса:

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

    Этот метод отправляет новое сообщение с устройства в облако каждую секунду. приветственное сообщение содержит объект с Идентификатором устройства hello сериализации JSON и случайным образом toosimulate номера датчика температуры и влажности датчика.

7. Наконец, добавьте следующие строки toohello hello **Main** метод:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    По умолчанию hello **создать** метод в приложении .NET Framework создает **DeviceClient** экземпляр, который использует toocommunicate протокола AMQP hello с центром IoT. hello toouse MQTT или HTTP-протокола, используйте переопределение hello hello **создать** метод, который позволяет toospecify hello протокола. UWP и PCL клиентов по умолчанию используется протокол HTTP hello. При использовании протокола hello HTTP, следует также добавить hello **Microsoft.AspNet.WebApi.Client** NuGet пакета tooyour проекта tooinclude hello **System.Net.Http.Formatting** пространства имен.

Этот учебник поможет выполнить toocreate действия hello центра IoT приложения для устройств. Можно также использовать hello [подключенной службы для Azure IoT Hub] [ lnk-connected-service] Visual Studio расширения tooadd hello необходимый код tooyour приложения для устройств.

> [!NOTE]
> простые действия tookeep, этот учебник не реализует никакую политику повтора. В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].

## <a name="run-hello-apps"></a>Запускайте приложения hello

Теперь вы находитесь toorun готовности приложения hello.

1. В обозревателе решений Visual Studio щелкните правой кнопкой мыши решение и выберите пункт **Назначить запускаемые проекты**. Выберите **несколько запускаемых проектов**, а затем выберите **запустить** как действие hello для обоих hello **ReadDeviceToCloudMessages** и **SimulatedDevice** проектов.

    ![Свойства запускаемого проекта][41]

2. Нажмите клавишу **F5** toostart обоих приложений под управлением. Здравствуйте, вывод на консоль из hello **SimulatedDevice** приложение устройство отправляет центр IoT tooyour сообщений hello показано приложение. Здравствуйте, вывод на консоль из hello **ReadDeviceToCloudMessages** приложение показывает сообщения приветствия, который принимает ваш центр IoT.

    ![Выходные данные консоли для приложений][42]

3. Hello **использование** плитки в hello [портал Azure] [ lnk-portal] показано hello число сообщений, отправляемых toohello центр IoT:

    ![Плитка "Использование" на портале Azure][43]

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello. Вы использовали устройства удостоверения tooenable hello устройства приложения toosend сообщения из устройства в облако toohello центр IoT. Также было создано приложение, которое отображает hello сообщений, полученных центра IoT hello.

Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:

* [Подключение устройства к Azure IoT][lnk-connect-device]
* [How to get started with device management (Node)][lnk-device-management] (Начало работы с управлением устройствами (Node))
* [Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Приступая к работе с архитектурой Azure IoT Edge в Linux)

toolearn tooextend сообщений в масштабе, IoT решение и процесс устройства в облако. в статье hello [обрабатывать сообщения из устройства в облако] [ lnk-process-d2c-tutorial] учебника.

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
