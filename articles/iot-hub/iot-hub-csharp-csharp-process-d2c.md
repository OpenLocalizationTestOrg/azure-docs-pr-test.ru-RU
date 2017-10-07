---
title: "сообщения из устройства в облако Azure IoT Hub aaaProcess с помощью маршрутов (.Net) | Документы Microsoft"
description: "Способ tooprocess сообщения из устройства в облако центр IoT с помощью правила маршрутизации и toodispatch пользовательские конечные точки сообщений tooother серверными службами."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>Обработка сообщений Центра Интернета вещей, отправляемых с устройства в облако, с использованием маршрутов (.NET)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Этот учебник построен на hello [приступить к работе с центром IoT] учебника. Учебник Hello.

* Показывает, как маршрутизации toouse правила сообщения из устройства в облако toodispatch образом простой, основанные на конфигурации.
* Показано, как интерактивный tooisolate сообщений, которые требуют немедленных действий из решения hello серверной части для дальнейшей обработки. Например, устройство может отправить аварийный сигнал, который активирует вставку билета в системе CRM. При этом обычные сообщения от точек данных, такие как данные телеизмерения температуры, поступают в модуль аналитики.

В конце этого учебника hello выполните три консольных приложений .NET:

* **SimulatedDevice**, измененная версия приложения hello, созданного в hello [приступить к работе с центром IoT] учебника отправляет сообщения из устройства в облако точки данных каждую секунду и интерактивные устройства в облако сообщений каждые 10 количество секунд.
* **ReadDeviceToCloudMessages** , отображает hello некритические телеметрии, отправленные приложение устройства.
* **ReadCriticalQueue** исключении из очереди hello важные сообщения, отправленные приложение устройства из очереди Service Bus. Эта очередь используется вложенного toohello центр IoT.

> [!NOTE]
> Для Центра Интернета вещей существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и JavaScript). toolearn tooreplace hello имитированное устройство в этом учебнике с физического устройства разделе hello [Центр разработчиков Azure IoT].

toocomplete этого учебника требуется hello следующие:

* Visual Studio 2015 или Visual Studio 2017.
* Активная учетная запись Azure. <br/>Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/free/) всего за несколько минут.

Кроме того, у вас должны быть базовые знания о [службе хранилища Azure] и [служебной шине Azure].

## <a name="send-interactive-messages"></a>Отправка интерактивных сообщений

Измените приложение hello устройства, созданный в hello [приступить к работе с центром IoT] учебника toooccasionally интерактивной отправки.

В Visual Studio в hello **SimulatedDevice** проекта, замените hello `SendDeviceToCloudMessagesAsync` метод с hello, следующий код:

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

Этот метод случайным образом добавляет свойство hello `"level": "critical"` toomessages отправленных hello устройство, которое имитирует сообщение, которое требуется немедленное вмешательство с серверной части решения hello. приложение Hello устройство передает данные в свойствах сообщения hello, вместо в тело сообщения hello, поэтому этот центр IoT может направлять toohello соответствующее сообщение hello сообщение целевой.

> [!NOTE]
> Сообщения tooroute свойства сообщения можно использовать для различных сценариев, включая новый путь, обработки, кроме приведенном здесь примере toohello-path.

> [!NOTE]
> Ради hello простоты этого учебника не реализует никакую политику повтора. В рабочем коде следует реализовать политику повтора, например экспоненциальной отсрочки, описанным в статье MSDN hello [обработка временных сбоев].

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>Сообщений в очереди tooa маршрута в концентратор IoT

В этом разделе выполняются следующие действия:

* Создается очередь служебной шины.
* Подключите tooyour центр IoT.
* Настройка вашего IoT концентратора toosend сообщения toohello очередь на основе наличия свойства на приветственное сообщение hello.

Дополнительные сведения о как tooprocess сообщений из очереди Service Bus см. в разделе [приступить к работе с очередями][Service Bus queue].

1. Создайте очередь служебной шины, как описано в статье [Начало работы с очередями служебной шины][Service Bus queue]. Hello очередь должна быть в hello ту же подписку и регион вашего центра IoT. Запишите hello пространство имен и имя очереди.

    > [!NOTE]
    > Для очередей и разделов служебной шины, которые используются как конечные точки Центра Интернета вещей, **сеансы** или **поиск повторяющихся данных** должны быть выключены. Если любой из этих параметров включены, конечная точка hello отображается как **недостижимо** в hello портал Azure.

2. В hello портал Azure, откройте ваш центр IoT и щелкните **конечные точки**.
    
    ![Конечные точки в Центре Интернета вещей][30]

3. В hello **конечные точки** колонке нажмите кнопку **добавить** в hello top tooadd концентратор IoT tooyour очереди. Конечная точка hello имя **CriticalQueue** и используйте раскрывающиеся tooselect hello **очереди Service Bus**hello имен Service Bus, в котором находится Ваша очередь и hello именем очереди. Закончив, нажмите кнопку **Сохранить** внизу hello.
    
    ![Добавление конечной точки][31]
    
4. Теперь щелкните **Маршруты** в Центре Интернета вещей. Нажмите кнопку **добавить** вверху hello toocreate колонке hello правило маршрутизации сообщений, toohello очередь вы только что добавлен. Выберите **DeviceTelemetry** как hello источник данных. Введите `level="critical"` в качестве условия hello и выберите только что добавленный как настраиваемую конечную точку как конечную точку правила маршрутизации hello очереди hello. Закончив, нажмите кнопку **Сохранить** внизу hello.
    
    ![Добавление правила][32]
    
    Убедитесь, что резервный маршрута hello задано слишком**ON**. Это значение является конфигурацией по умолчанию hello центра IoT.
    
    ![Резервный маршрут][33]

## <a name="read-from-hello-queue-endpoint"></a>Чтение из конечной очереди hello

В этом разделе вы читаете hello сообщения из конечной очереди hello.

1. В Visual Studio, добавить Visual C# Windows классического проекта toohello текущее решение, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта. Имя проекта hello **ReadCriticalQueue**.

2. В обозревателе решений щелкните правой кнопкой мыши hello **ReadCriticalQueue** проекта, а затем нажмите кнопку **управление пакетами NuGet**. Эта операция отображает hello **диспетчера пакетов NuGet** окна.

3. Поиск **WindowsAzure.ServiceBus**, нажмите кнопку **установить**и примите условия использования hello. Эта операция загрузки, устанавливает и добавляет toohello ссылку Azure Service Bus с его зависимости.

4. Добавьте следующее hello **с помощью** инструкции вверху hello hello **Program.cs** файла:
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. Наконец, добавьте следующие строки toohello hello **Main** метод. Замените строку hello подключения с **прослушивания** разрешения для очереди hello:
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Запускать приложения hello
Теперь все готово toorun приложения hello.

1. В обозревателе решений Visual Studio щелкните правой кнопкой мыши решение и выберите пункт **Настроить запускаемые проекты**. Выберите **несколько запускаемых проектов**, а затем выберите **запустить** как действие hello для hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, и **ReadCriticalQueue** проектов.
2. Нажмите клавишу **F5** toostart hello три консольных приложениях. Hello **ReadDeviceToCloudMessages** приложение имеет только некритические сообщения, отправленные из hello **SimulatedDevice** приложения и hello **ReadCriticalQueue** приложение имеет только важные сообщения.
   
   ![Три консольных приложения][50]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, каким образом tooreliably отправки сообщения из устройства в облако с помощью средства маршрутизации сообщений hello из центра IoT.

Hello [способ сообщений toosend облака на устройство с центром IoT] [ lnk-c2d] показано, как toosend сообщений tooyour устройств из серверной части вашего решения.

см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite][lnk-suite].

toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].

. в разделе toolearn Дополнительные сведения о маршрутизации сообщений в центре IoT [отправлять и получать сообщения с центром IoT][lnk-devguide-messaging].

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[службе хранилища Azure]: https://azure.microsoft.com/documentation/services/storage/
[служебной шине Azure]: https://azure.microsoft.com/documentation/services/service-bus/
[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[приступить к работе с центром IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Центр разработчиков Azure IoT]: https://azure.microsoft.com/develop/iot
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
