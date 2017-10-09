---
title: "aaaProcess сообщения из устройства в облако Azure IoT Hub (Java) | Документы Microsoft"
description: "Способ tooprocess сообщения из устройства в облако центр IoT с помощью правила маршрутизации и toodispatch пользовательские конечные точки сообщений tooother серверными службами."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="235ad-103">Обработка сообщений Центра Интернета вещей, отправляемых с устройства в облако (Java)</span><span class="sxs-lookup"><span data-stu-id="235ad-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="235ad-104">Центр Интернета вещей Azure —это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств Интернета вещей и серверной частью решения.</span><span class="sxs-lookup"><span data-stu-id="235ad-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="235ad-105">Другие учебники ([приступить к работе с центром IoT] и [отправки сообщений облака на устройство с центром IoT][lnk-c2d]) показано, как toouse hello основные устройства для облака и облака для устройства обмен сообщениями из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="235ad-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="235ad-106">Этот учебник построен на hello код, показываемый в hello [приступить к работе с центром IoT] учебника и показано, как toouse сообщений маршрутизации сообщения из устройства в облако tooprocess масштабируемой способом.</span><span class="sxs-lookup"><span data-stu-id="235ad-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="235ad-107">Hello учебник демонстрирует, как tooprocess сообщений, которые требуют немедленных действий из решения hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="235ad-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="235ad-108">Например, устройство может отправить аварийный сигнал, который активирует вставку билета в системе CRM.</span><span class="sxs-lookup"><span data-stu-id="235ad-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="235ad-109">При этом обычные сообщения от точек данных просто поступают в модуль аналитики.</span><span class="sxs-lookup"><span data-stu-id="235ad-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="235ad-110">Например температура телеметрии с устройства, которое является toobe сохранить для последующего анализа — это сообщение точки данных.</span><span class="sxs-lookup"><span data-stu-id="235ad-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="235ad-111">В конце этого учебника hello выполните три консольные приложения Java:</span><span class="sxs-lookup"><span data-stu-id="235ad-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="235ad-112">**имитируемые устройства**, измененная версия приложения hello, созданного в hello [приступить к работе с центром IoT] учебник, отправляет сообщения из устройства в облако точки данных каждую секунду и интерактивные устройства в облако сообщений каждые 10 количество секунд.</span><span class="sxs-lookup"><span data-stu-id="235ad-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="235ad-113">Это приложение использует toocommunicate протокол AMQP hello с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="235ad-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="235ad-114">**чтение d2c сообщений** отображает hello телеметрии, отправленные приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="235ad-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="235ad-115">**чтение критического очередь** исключении из очереди hello важные сообщения из toohello присоединенного очереди Service Bus hello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="235ad-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="235ad-116">Для Центра Интернета вещей существуют пакеты SDK для многих платформ устройств и языков (включая C, Java и JavaScript).</span><span class="sxs-lookup"><span data-stu-id="235ad-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="235ad-117">Инструкции по как tooreplace hello устройства в этом учебнике с физическим устройством и tooan устройств tooconnect центр IoT. в статье hello [Центр разработчиков Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="235ad-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="235ad-118">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="235ad-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="235ad-119">Полные рабочую версию hello [приступить к работе с центром IoT] учебника.</span><span class="sxs-lookup"><span data-stu-id="235ad-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="235ad-120">Здравствуйте, последняя версия [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="235ad-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="235ad-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="235ad-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="235ad-122">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="235ad-122">An active Azure account.</span></span> <span data-ttu-id="235ad-123">(Если ее нет, можно создать [бесплатную учетную запись] [lnk-free-trial] всего за несколько минут.)</span><span class="sxs-lookup"><span data-stu-id="235ad-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="235ad-124">Кроме того, у вас должны быть базовые знания о [службе хранилища Azure] и [служебной шине Azure].</span><span class="sxs-lookup"><span data-stu-id="235ad-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="235ad-125">Отправка интерактивных сообщений из приложения устройства</span><span class="sxs-lookup"><span data-stu-id="235ad-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="235ad-126">В этом разделе, измените приложение hello устройства, созданный в hello [приступить к работе с центром IoT] учебника toooccasionally отправлять сообщения, которые требуют немедленного обработки.</span><span class="sxs-lookup"><span data-stu-id="235ad-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="235ad-127">Используйте текстовый редактор tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java файл.</span><span class="sxs-lookup"><span data-stu-id="235ad-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="235ad-128">Этот файл содержит код hello для hello **имитируемые устройства** приложения, созданного в hello [приступить к работе с центром IoT] учебника.</span><span class="sxs-lookup"><span data-stu-id="235ad-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="235ad-129">Замените hello **MessageSender** класса hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="235ad-129">Replace hello **MessageSender** class with hello following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="235ad-130">Этот метод случайным образом добавляет свойство hello `"level": "critical"` toomessages отправленных hello устройство, которое имитирует сообщение, которое требуется немедленное вмешательство с серверной части приложения hello.</span><span class="sxs-lookup"><span data-stu-id="235ad-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="235ad-131">приложение Hello передает данные в свойствах сообщения hello, вместо в тело сообщения hello, поэтому этот центр IoT может направлять toohello соответствующее сообщение hello сообщения целевой.</span><span class="sxs-lookup"><span data-stu-id="235ad-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="235ad-132">Сообщения tooroute свойства сообщения можно использовать для различных сценариев, включая холодного путь к обработке, кроме приведенном здесь примере toohello критический путь.</span><span class="sxs-lookup"><span data-stu-id="235ad-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="235ad-133">Сохраните и закройте файл simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="235ad-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="235ad-134">Ради hello простоты этого учебника не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="235ad-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="235ad-135">В рабочем коде следует реализовать политику повтора, например экспоненциальной отсрочки, описанным в статье MSDN hello [обработка временных сбоев].</span><span class="sxs-lookup"><span data-stu-id="235ad-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="235ad-136">toobuild hello **имитируемые устройства** приложения с помощью Maven, выполните следующую команду в командной строке hello в папке имитируемые устройства hello hello:</span><span class="sxs-lookup"><span data-stu-id="235ad-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="235ad-137">Добавление очереди tooyour IoT hub и маршрутизации сообщений tooit</span><span class="sxs-lookup"><span data-stu-id="235ad-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="235ad-138">В этом разделе Создание очереди служебной шины, подключите его tooyour центр IoT и настройка вашей IoT концентратора toosend сообщения toohello очередь на основе наличия свойства на приветственное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="235ad-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="235ad-139">Дополнительные сведения о как tooprocess сообщений из очереди Service Bus см. в разделе [приступить к работе с очередями][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="235ad-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="235ad-140">Создайте очередь служебной шины, как описано в статье [Начало работы с очередями служебной шины][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="235ad-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="235ad-141">Запишите hello пространство имен и имя очереди.</span><span class="sxs-lookup"><span data-stu-id="235ad-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="235ad-142">В hello портал Azure, откройте ваш центр IoT и щелкните **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="235ad-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Конечные точки в Центре Интернета вещей][30]

3. <span data-ttu-id="235ad-144">В hello **конечные точки** колонке нажмите кнопку **добавить** в hello top tooadd концентратор IoT tooyour очереди.</span><span class="sxs-lookup"><span data-stu-id="235ad-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="235ad-145">Конечная точка hello имя **CriticalQueue** и используйте раскрывающиеся tooselect hello **очереди Service Bus**hello имен Service Bus, в котором находится Ваша очередь и hello именем очереди.</span><span class="sxs-lookup"><span data-stu-id="235ad-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="235ad-146">Закончив, нажмите кнопку **Сохранить** внизу hello.</span><span class="sxs-lookup"><span data-stu-id="235ad-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Добавление конечной точки][31]

4. <span data-ttu-id="235ad-148">Теперь щелкните **Маршруты** в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="235ad-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="235ad-149">Нажмите кнопку **добавить** вверху hello toocreate колонке hello правило маршрутизации сообщений, toohello очередь вы только что добавлен.</span><span class="sxs-lookup"><span data-stu-id="235ad-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="235ad-150">Выберите **DeviceTelemetry** как hello источник данных.</span><span class="sxs-lookup"><span data-stu-id="235ad-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="235ad-151">Введите `level="critical"` в качестве условия hello и выберите только что добавленный как настраиваемую конечную точку как конечную точку правила маршрутизации hello очереди hello.</span><span class="sxs-lookup"><span data-stu-id="235ad-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="235ad-152">Закончив, нажмите кнопку **Сохранить** внизу hello.</span><span class="sxs-lookup"><span data-stu-id="235ad-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Добавление правила][32]

    <span data-ttu-id="235ad-154">Убедитесь, что резервный маршрута hello задано слишком**ON**.</span><span class="sxs-lookup"><span data-stu-id="235ad-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="235ad-155">Этот параметр является конфигурацией по умолчанию hello центра IoT.</span><span class="sxs-lookup"><span data-stu-id="235ad-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Резервный маршрут][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="235ad-157">(Необязательно) Чтение из конечной очереди hello</span><span class="sxs-lookup"><span data-stu-id="235ad-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="235ad-158">При необходимости можно читать сообщения hello из конечной очереди hello, следуя инструкциям hello [приступить к работе с очередями][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="235ad-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="235ad-159">Имя приложения hello **чтение критического очередь**.</span><span class="sxs-lookup"><span data-stu-id="235ad-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="235ad-160">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="235ad-160">Run hello applications</span></span>

<span data-ttu-id="235ad-161">Теперь все три приложения hello toorun готовности.</span><span class="sxs-lookup"><span data-stu-id="235ad-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="235ad-162">toorun hello **чтение d2c сообщений** приложения, в командной строке или оболочки перейдите toohello d2c чтения папку и запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="235ad-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Запуск read-d2c-messages][readd2c]

2. <span data-ttu-id="235ad-164">toorun hello **чтение критического очередь** приложения, в командной строке или оболочки перейдите toohello чтение критического очередь папку и запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="235ad-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Запуск read-critical-messages][readqueue]

3. <span data-ttu-id="235ad-166">toorun hello **имитируемые устройства** приложения, в командной строке или оболочки перейдите toohello имитируемые устройства папку и запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="235ad-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Запуск приложения simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="235ad-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="235ad-168">Next steps</span></span>

<span data-ttu-id="235ad-169">В этом учебнике вы узнали, каким образом tooreliably отправки сообщения из устройства в облако с помощью средства маршрутизации сообщений hello из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="235ad-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="235ad-170">Hello [способ сообщений toosend облака на устройство с центром IoT] [ lnk-c2d] показано, как toosend сообщений tooyour устройств из серверной части вашего решения.</span><span class="sxs-lookup"><span data-stu-id="235ad-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="235ad-171">см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="235ad-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="235ad-172">toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].</span><span class="sxs-lookup"><span data-stu-id="235ad-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="235ad-173">. в разделе toolearn Дополнительные сведения о маршрутизации сообщений в центре IoT [отправлять и получать сообщения с центром IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="235ad-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[службе хранилища Azure]: https://azure.microsoft.com/documentation/services/storage/
[служебной шине Azure]: https://azure.microsoft.com/documentation/services/service-bus/

[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[приступить к работе с центром IoT]: iot-hub-java-java-getstarted.md
[Центр разработчиков Azure IoT]: https://azure.microsoft.com/develop/iot
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Обработка временного сбоя]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
