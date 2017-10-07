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
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="a6143-103">Обработка сообщений Центра Интернета вещей, отправляемых с устройства в облако, с использованием маршрутов (.NET)</span><span class="sxs-lookup"><span data-stu-id="a6143-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="a6143-104">Этот учебник построен на hello [приступить к работе с центром IoT] учебника.</span><span class="sxs-lookup"><span data-stu-id="a6143-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="a6143-105">Учебник Hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-105">hello tutorial:</span></span>

* <span data-ttu-id="a6143-106">Показывает, как маршрутизации toouse правила сообщения из устройства в облако toodispatch образом простой, основанные на конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a6143-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="a6143-107">Показано, как интерактивный tooisolate сообщений, которые требуют немедленных действий из решения hello серверной части для дальнейшей обработки.</span><span class="sxs-lookup"><span data-stu-id="a6143-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="a6143-108">Например, устройство может отправить аварийный сигнал, который активирует вставку билета в системе CRM.</span><span class="sxs-lookup"><span data-stu-id="a6143-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="a6143-109">При этом обычные сообщения от точек данных, такие как данные телеизмерения температуры, поступают в модуль аналитики.</span><span class="sxs-lookup"><span data-stu-id="a6143-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="a6143-110">В конце этого учебника hello выполните три консольных приложений .NET:</span><span class="sxs-lookup"><span data-stu-id="a6143-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="a6143-111">**SimulatedDevice**, измененная версия приложения hello, созданного в hello [приступить к работе с центром IoT] учебника отправляет сообщения из устройства в облако точки данных каждую секунду и интерактивные устройства в облако сообщений каждые 10 количество секунд.</span><span class="sxs-lookup"><span data-stu-id="a6143-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="a6143-112">**ReadDeviceToCloudMessages** , отображает hello некритические телеметрии, отправленные приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="a6143-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="a6143-113">**ReadCriticalQueue** исключении из очереди hello важные сообщения, отправленные приложение устройства из очереди Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a6143-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="a6143-114">Эта очередь используется вложенного toohello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="a6143-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="a6143-115">Для Центра Интернета вещей существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и JavaScript).</span><span class="sxs-lookup"><span data-stu-id="a6143-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="a6143-116">toolearn tooreplace hello имитированное устройство в этом учебнике с физического устройства разделе hello [Центр разработчиков Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="a6143-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="a6143-117">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a6143-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a6143-118">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a6143-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a6143-119">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a6143-119">An active Azure account.</span></span> <br/><span data-ttu-id="a6143-120">Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a6143-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="a6143-121">Кроме того, у вас должны быть базовые знания о [службе хранилища Azure] и [служебной шине Azure].</span><span class="sxs-lookup"><span data-stu-id="a6143-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="a6143-122">Отправка интерактивных сообщений</span><span class="sxs-lookup"><span data-stu-id="a6143-122">Send interactive messages</span></span>

<span data-ttu-id="a6143-123">Измените приложение hello устройства, созданный в hello [приступить к работе с центром IoT] учебника toooccasionally интерактивной отправки.</span><span class="sxs-lookup"><span data-stu-id="a6143-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="a6143-124">В Visual Studio в hello **SimulatedDevice** проекта, замените hello `SendDeviceToCloudMessagesAsync` метод с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="a6143-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

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

<span data-ttu-id="a6143-125">Этот метод случайным образом добавляет свойство hello `"level": "critical"` toomessages отправленных hello устройство, которое имитирует сообщение, которое требуется немедленное вмешательство с серверной части решения hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="a6143-126">приложение Hello устройство передает данные в свойствах сообщения hello, вместо в тело сообщения hello, поэтому этот центр IoT может направлять toohello соответствующее сообщение hello сообщение целевой.</span><span class="sxs-lookup"><span data-stu-id="a6143-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="a6143-127">Сообщения tooroute свойства сообщения можно использовать для различных сценариев, включая новый путь, обработки, кроме приведенном здесь примере toohello-path.</span><span class="sxs-lookup"><span data-stu-id="a6143-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="a6143-128">Ради hello простоты этого учебника не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="a6143-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a6143-129">В рабочем коде следует реализовать политику повтора, например экспоненциальной отсрочки, описанным в статье MSDN hello [обработка временных сбоев].</span><span class="sxs-lookup"><span data-stu-id="a6143-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="a6143-130">Сообщений в очереди tooa маршрута в концентратор IoT</span><span class="sxs-lookup"><span data-stu-id="a6143-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="a6143-131">В этом разделе выполняются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a6143-131">In this section, you:</span></span>

* <span data-ttu-id="a6143-132">Создается очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a6143-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="a6143-133">Подключите tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="a6143-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="a6143-134">Настройка вашего IoT концентратора toosend сообщения toohello очередь на основе наличия свойства на приветственное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="a6143-135">Дополнительные сведения о как tooprocess сообщений из очереди Service Bus см. в разделе [приступить к работе с очередями][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="a6143-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="a6143-136">Создайте очередь служебной шины, как описано в статье [Начало работы с очередями служебной шины][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="a6143-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="a6143-137">Hello очередь должна быть в hello ту же подписку и регион вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="a6143-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="a6143-138">Запишите hello пространство имен и имя очереди.</span><span class="sxs-lookup"><span data-stu-id="a6143-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a6143-139">Для очередей и разделов служебной шины, которые используются как конечные точки Центра Интернета вещей, **сеансы** или **поиск повторяющихся данных** должны быть выключены.</span><span class="sxs-lookup"><span data-stu-id="a6143-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="a6143-140">Если любой из этих параметров включены, конечная точка hello отображается как **недостижимо** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a6143-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="a6143-141">В hello портал Azure, откройте ваш центр IoT и щелкните **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="a6143-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Конечные точки в Центре Интернета вещей][30]

3. <span data-ttu-id="a6143-143">В hello **конечные точки** колонке нажмите кнопку **добавить** в hello top tooadd концентратор IoT tooyour очереди.</span><span class="sxs-lookup"><span data-stu-id="a6143-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="a6143-144">Конечная точка hello имя **CriticalQueue** и используйте раскрывающиеся tooselect hello **очереди Service Bus**hello имен Service Bus, в котором находится Ваша очередь и hello именем очереди.</span><span class="sxs-lookup"><span data-stu-id="a6143-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="a6143-145">Закончив, нажмите кнопку **Сохранить** внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Добавление конечной точки][31]
    
4. <span data-ttu-id="a6143-147">Теперь щелкните **Маршруты** в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="a6143-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="a6143-148">Нажмите кнопку **добавить** вверху hello toocreate колонке hello правило маршрутизации сообщений, toohello очередь вы только что добавлен.</span><span class="sxs-lookup"><span data-stu-id="a6143-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="a6143-149">Выберите **DeviceTelemetry** как hello источник данных.</span><span class="sxs-lookup"><span data-stu-id="a6143-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="a6143-150">Введите `level="critical"` в качестве условия hello и выберите только что добавленный как настраиваемую конечную точку как конечную точку правила маршрутизации hello очереди hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="a6143-151">Закончив, нажмите кнопку **Сохранить** внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Добавление правила][32]
    
    <span data-ttu-id="a6143-153">Убедитесь, что резервный маршрута hello задано слишком**ON**.</span><span class="sxs-lookup"><span data-stu-id="a6143-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="a6143-154">Это значение является конфигурацией по умолчанию hello центра IoT.</span><span class="sxs-lookup"><span data-stu-id="a6143-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![Резервный маршрут][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="a6143-156">Чтение из конечной очереди hello</span><span class="sxs-lookup"><span data-stu-id="a6143-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="a6143-157">В этом разделе вы читаете hello сообщения из конечной очереди hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="a6143-158">В Visual Studio, добавить Visual C# Windows классического проекта toohello текущее решение, с помощью hello **консольного приложения (.NET Framework)** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="a6143-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="a6143-159">Имя проекта hello **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="a6143-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="a6143-160">В обозревателе решений щелкните правой кнопкой мыши hello **ReadCriticalQueue** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a6143-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="a6143-161">Эта операция отображает hello **диспетчера пакетов NuGet** окна.</span><span class="sxs-lookup"><span data-stu-id="a6143-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="a6143-162">Поиск **WindowsAzure.ServiceBus**, нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="a6143-163">Эта операция загрузки, устанавливает и добавляет toohello ссылку Azure Service Bus с его зависимости.</span><span class="sxs-lookup"><span data-stu-id="a6143-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="a6143-164">Добавьте следующее hello **с помощью** инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="a6143-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="a6143-165">Наконец, добавьте следующие строки toohello hello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="a6143-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="a6143-166">Замените строку hello подключения с **прослушивания** разрешения для очереди hello:</span><span class="sxs-lookup"><span data-stu-id="a6143-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
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

## <a name="run-hello-applications"></a><span data-ttu-id="a6143-167">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="a6143-167">Run hello applications</span></span>
<span data-ttu-id="a6143-168">Теперь все готово toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a6143-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="a6143-169">В обозревателе решений Visual Studio щелкните правой кнопкой мыши решение и выберите пункт **Настроить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="a6143-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="a6143-170">Выберите **несколько запускаемых проектов**, а затем выберите **запустить** как действие hello для hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, и **ReadCriticalQueue** проектов.</span><span class="sxs-lookup"><span data-stu-id="a6143-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="a6143-171">Нажмите клавишу **F5** toostart hello три консольных приложениях.</span><span class="sxs-lookup"><span data-stu-id="a6143-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="a6143-172">Hello **ReadDeviceToCloudMessages** приложение имеет только некритические сообщения, отправленные из hello **SimulatedDevice** приложения и hello **ReadCriticalQueue** приложение имеет только важные сообщения.</span><span class="sxs-lookup"><span data-stu-id="a6143-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Три консольных приложения][50]

## <a name="next-steps"></a><span data-ttu-id="a6143-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6143-174">Next steps</span></span>
<span data-ttu-id="a6143-175">В этом учебнике вы узнали, каким образом tooreliably отправки сообщения из устройства в облако с помощью средства маршрутизации сообщений hello из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="a6143-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="a6143-176">Hello [способ сообщений toosend облака на устройство с центром IoT] [ lnk-c2d] показано, как toosend сообщений tooyour устройств из серверной части вашего решения.</span><span class="sxs-lookup"><span data-stu-id="a6143-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="a6143-177">см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="a6143-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="a6143-178">toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].</span><span class="sxs-lookup"><span data-stu-id="a6143-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="a6143-179">. в разделе toolearn Дополнительные сведения о маршрутизации сообщений в центре IoT [отправлять и получать сообщения с центром IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="a6143-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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
