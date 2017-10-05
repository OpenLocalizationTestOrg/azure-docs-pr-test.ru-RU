---
title: "Отправка сообщений из облака на устройство с помощью Центра Интернета вещей Azure (.NET) | Документация Майкрософт"
description: "Сведения об отправке сообщений из облака на устройство из Центра Интернета вещей Azure с помощью пакетов SDK для Интернета вещей Azure для .NET. Для получения сообщений, отправляемых из облака на устройство, следует изменить приложение для устройства, а для отправки таких сообщений — внутреннее приложение."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: 3f5f83671054c30afde3d7f18ff0edcdb8f78a01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="send-messages-from-the-cloud-to-your-device-with-iot-hub-net"></a><span data-ttu-id="609d5-104">Отправка сообщений из облака на устройство с помощью Центра Интернета вещей (.NET)</span><span class="sxs-lookup"><span data-stu-id="609d5-104">Send messages from the cloud to your device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="609d5-105">Введение</span><span class="sxs-lookup"><span data-stu-id="609d5-105">Introduction</span></span>
<span data-ttu-id="609d5-106">Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения.</span><span class="sxs-lookup"><span data-stu-id="609d5-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="609d5-107">В руководстве [Подключение устройства к Центру Интернета вещей с помощью .NET] описывается, как создать Центр Интернета вещей, подготовить в нем удостоверение устройства и написать код приложения для устройства, которое отправляет сообщения с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="609d5-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="609d5-108">Это руководство является логическим продолжением статьи [Подключение устройства к Центру Интернета вещей с помощью .NET].</span><span class="sxs-lookup"><span data-stu-id="609d5-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="609d5-109">В нем показано следующее:</span><span class="sxs-lookup"><span data-stu-id="609d5-109">It shows you how to:</span></span>

* <span data-ttu-id="609d5-110">Отправка сообщений, передаваемых из облака на устройство, из серверной части решения на одно устройство через Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="609d5-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="609d5-111">Получение на устройстве сообщений, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="609d5-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="609d5-112">Запрос из серверной части решения подтверждения доставки (*отзыва*) для сообщений, отправленных на устройство из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="609d5-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="609d5-113">Дополнительные сведения о сообщениях, отправляемых из облака на устройство, см. в [руководстве разработчика для Центра Интернета вещей][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="609d5-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="609d5-114">В конце этого руководства запускаются два консольных приложения для .NET:</span><span class="sxs-lookup"><span data-stu-id="609d5-114">At the end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="609d5-115">**SimulatedDevice**, измененную версию приложения, созданного в руководстве [Подключение устройства к Центру Интернета вещей с помощью .NET]. Это приложение подключается к Центру Интернета вещей и получает сообщения с облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="609d5-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="609d5-116">**SendCloudToDevice** — отправляет сообщение из облака в приложение устройства с помощью Центра Интернета вещей, а затем получает подтверждение о его доставке.</span><span class="sxs-lookup"><span data-stu-id="609d5-116">**SendCloudToDevice**, which sends a cloud-to-device message to the device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="609d5-117">В Центре Интернета вещей реализована поддержка для пакетов SDK для многих платформ устройств и языков (включая C, Java и Javascript). Эти пакеты работают на основе [пакетов SDK для устройств Интернета вещей Azure].</span><span class="sxs-lookup"><span data-stu-id="609d5-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="609d5-118">Пошаговые инструкции по связыванию устройства с кодом из этого руководства, а также по подключению к Центру Интернета вещей Azure см. в [руководстве для разработчиков Центра Интернета вещей].</span><span class="sxs-lookup"><span data-stu-id="609d5-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="609d5-119">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="609d5-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="609d5-120">Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="609d5-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="609d5-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="609d5-121">An active Azure account.</span></span> <span data-ttu-id="609d5-122">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="609d5-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-device-app"></a><span data-ttu-id="609d5-123">Получение сообщений в приложении для устройства</span><span class="sxs-lookup"><span data-stu-id="609d5-123">Receive messages in the device app</span></span>
<span data-ttu-id="609d5-124">В этом разделе вы измените приложение для устройства, созданное в разделе [Подключение устройства к Центру Интернета вещей с помощью .NET], для получения сообщений из облака на устройство от Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="609d5-124">In this section, you'll modify the device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="609d5-125">В Visual Studio в проекте **SimulatedDevice** добавьте в класс **Program** следующий метод:</span><span class="sxs-lookup"><span data-stu-id="609d5-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="609d5-126">Метод `ReceiveAsync` асинхронно возвращает полученное сообщение, когда устройство его получило.</span><span class="sxs-lookup"><span data-stu-id="609d5-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span></span> <span data-ttu-id="609d5-127">Он возвращает значение *NULL* после истечения заданного времени ожидания (в этом примере используется значение по умолчанию, равное одной минуте).</span><span class="sxs-lookup"><span data-stu-id="609d5-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span></span> <span data-ttu-id="609d5-128">Когда приложение получит значение *NULL*, оно продолжит ожидание новых сообщений.</span><span class="sxs-lookup"><span data-stu-id="609d5-128">When the app receives a *null*, it should continue to wait for new messages.</span></span> <span data-ttu-id="609d5-129">Из-за этого требования присутствует строка `if (receivedMessage == null) continue`.</span><span class="sxs-lookup"><span data-stu-id="609d5-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="609d5-130">Вызов `CompleteAsync()` уведомляет центр Интернета вещей об успешной обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="609d5-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span></span> <span data-ttu-id="609d5-131">Можно спокойно удалить сообщение из очереди устройства.</span><span class="sxs-lookup"><span data-stu-id="609d5-131">The message can be safely removed from the device queue.</span></span> <span data-ttu-id="609d5-132">Если что-то помешает приложению устройства завершить обработку сообщения, Центр Интернета вещей доставит его снова.</span><span class="sxs-lookup"><span data-stu-id="609d5-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span></span> <span data-ttu-id="609d5-133">Поэтому важно, чтобы логика обработки сообщений в приложении устройства была *идемпотентной*. Это обеспечит одинаковый результат при многократном получении одного и того же сообщения.</span><span class="sxs-lookup"><span data-stu-id="609d5-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span></span> <span data-ttu-id="609d5-134">Приложение может также временно отказаться от сообщения. Тогда Центр Интернета вещей будет хранить сообщение в очереди для последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="609d5-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span></span> <span data-ttu-id="609d5-135">Или приложение может отклонить сообщение, и тогда оно будет окончательно удалено из очереди.</span><span class="sxs-lookup"><span data-stu-id="609d5-135">Or, the application can reject a message, which permanently removes the message from the queue.</span></span> <span data-ttu-id="609d5-136">Дополнительные сведения о жизненном цикле сообщений, передаваемых из облака на устройство, см. в статье [Отправка и получение сообщений в Центре Интернета вещей][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="609d5-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="609d5-137">При использовании HTTP вместо MQTT или AMQP в качестве транспорта немедленно возвращается метод `ReceiveAsync`.</span><span class="sxs-lookup"><span data-stu-id="609d5-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="609d5-138">Схема сообщений, передаваемых из облака на устройство с помощью HTTP, может использоваться на периодически подключаемых устройствах, которые редко проверяют наличие новых сообщений (реже, чем раз в 25 минут).</span><span class="sxs-lookup"><span data-stu-id="609d5-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="609d5-139">Передача большего количества получений HTTP приводит к регулированию запросов в центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="609d5-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span></span> <span data-ttu-id="609d5-140">Дополнительные сведения о различиях между поддержкой MQTT, AMQP и HTTP, а также регулировании Центра Интернета вещей см. в [руководстве разработчика для Центра Интернета вещей][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="609d5-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="609d5-141">Добавьте в метод **Main** непосредственно перед строкой `Console.ReadLine()` следующий метод:</span><span class="sxs-lookup"><span data-stu-id="609d5-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="609d5-142">Для упрощения в этом руководстве не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="609d5-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="609d5-143">В рабочем коде следует реализовать политики повтора (например, экспоненциальную задержку), как указано в статье MSDN [Обработка временного сбоя].</span><span class="sxs-lookup"><span data-stu-id="609d5-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="609d5-144">Отправка сообщения из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="609d5-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="609d5-145">В этом разделе вы напишете консольное приложение для .NET, которое отправляет сообщения из облака в приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="609d5-145">In this section, you write a .NET console app that sends cloud-to-device messages to the device app.</span></span>

1. <span data-ttu-id="609d5-146">В текущем решении Visual Studio создайте проект классического приложения Visual C# с помощью шаблона проекта **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="609d5-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span></span> <span data-ttu-id="609d5-147">Присвойте проекту имя **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="609d5-147">Name the project **SendCloudToDevice**.</span></span>
   
    ![Новый проект в Visual Studio][20]
2. <span data-ttu-id="609d5-149">В обозревателе решений щелкните правой кнопкой мыши решение и выберите пункт **Управление пакетами NuGet для решения...**.</span><span class="sxs-lookup"><span data-stu-id="609d5-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="609d5-150">Это действие откроет окно **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="609d5-150">This action opens the **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="609d5-151">Найдите **Microsoft.Azure.Devices**, щелкните **Установить** и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="609d5-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="609d5-152">После этого будут выполнены скачивание, установка и добавление ссылки на [пакет SDK NuGet для служб Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="609d5-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="609d5-153">Добавьте следующий оператор `using` в начало файла **Program.cs** .</span><span class="sxs-lookup"><span data-stu-id="609d5-153">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="609d5-154">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="609d5-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="609d5-155">Замените значение заполнителя строкой подключения центра Интернета вещей из раздела [Подключение устройства к Центру Интернета вещей с помощью .NET].</span><span class="sxs-lookup"><span data-stu-id="609d5-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="609d5-156">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="609d5-156">Add the following method to the **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="609d5-157">Этот метод отправляет на устройство с идентификатором `myFirstDevice`новое сообщение, передаваемое из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="609d5-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span></span> <span data-ttu-id="609d5-158">Измените этот параметр соответствующим образом, если вы использовали значение, отличное от указанного в инструкциях о [Подключение устройства к Центру Интернета вещей с помощью .NET].</span><span class="sxs-lookup"><span data-stu-id="609d5-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="609d5-159">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="609d5-159">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="609d5-160">В Visual Studio щелкните правой кнопкой мыши свое решение и выберите пункт **Назначить запускаемые проекты**. Щелкните **Несколько запускаемых проектов**, а затем выберите действие **Запуск** для **ReadDeviceToCloudMessages**, **SimulatedDevice** и **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="609d5-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="609d5-161">Нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="609d5-161">Press **F5**.</span></span> <span data-ttu-id="609d5-162">Должны запуститься все три приложения.</span><span class="sxs-lookup"><span data-stu-id="609d5-162">All three applications should start.</span></span> <span data-ttu-id="609d5-163">Выберите окна **SendCloudToDevice** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="609d5-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="609d5-164">Приложение для устройства должно получить сообщение.</span><span class="sxs-lookup"><span data-stu-id="609d5-164">You should see the message being received by the device app.</span></span>
   
   ![Приложение получает сообщение][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="609d5-166">Получение подтверждений доставки</span><span class="sxs-lookup"><span data-stu-id="609d5-166">Receive delivery feedback</span></span>
<span data-ttu-id="609d5-167">Для каждого сообщения, передаваемого из облака на устройство, в Центре Интернета вещей можно запросить подтверждения доставки (или истечения срока действия).</span><span class="sxs-lookup"><span data-stu-id="609d5-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="609d5-168">Этот параметр позволяет серверной части решения легко передавать данные в логику повторных попыток или компенсаций.</span><span class="sxs-lookup"><span data-stu-id="609d5-168">This option enables the solution back end to easily inform retry or compensation logic.</span></span> <span data-ttu-id="609d5-169">Дополнительные сведения о подтверждениях при передаче из облака на устройство см. в статье [Отправка и получение сообщений в Центре Интернета вещей][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="609d5-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="609d5-170">В этом разделе вы измените приложение **SendCloudToDevice**, чтобы оно запрашивало подтверждение и получало его из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="609d5-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="609d5-171">В Visual Studio в проекте **SendCloudToDevice** добавьте в класс **Program** следующий метод:</span><span class="sxs-lookup"><span data-stu-id="609d5-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="609d5-172">Обратите внимание, что шаблон получения здесь аналогичен шаблону, использовавшемуся для получения сообщений из облака на устройство из приложения устройства.</span><span class="sxs-lookup"><span data-stu-id="609d5-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
2. <span data-ttu-id="609d5-173">Добавьте следующий метод в метод **Main** непосредственно после строки `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)`.</span><span class="sxs-lookup"><span data-stu-id="609d5-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="609d5-174">Чтобы запросить подтверждение доставки сообщения из облака на устройство, необходимо указать свойство в методе **SendCloudToDeviceMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="609d5-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="609d5-175">Добавьте следующую строку сразу после строки `var commandMessage = new Message(...);` :</span><span class="sxs-lookup"><span data-stu-id="609d5-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="609d5-176">Запустите приложения, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="609d5-176">Run the apps by pressing **F5**.</span></span> <span data-ttu-id="609d5-177">Должны запуститься все три приложения.</span><span class="sxs-lookup"><span data-stu-id="609d5-177">You should see all three applications start.</span></span> <span data-ttu-id="609d5-178">Выберите окна **SendCloudToDevice** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="609d5-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="609d5-179">Приложение для устройства должно получить сообщение, а через несколько секунд ваше приложение **SendCloudToDevice** должно получить сообщение о подтверждении.</span><span class="sxs-lookup"><span data-stu-id="609d5-179">You should see the message being received by the device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Приложение получает сообщение][22]

> [!NOTE]
> <span data-ttu-id="609d5-181">Для упрощения в этом учебнике не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="609d5-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="609d5-182">В рабочем коде следует реализовать политики повтора (например, экспоненциальную задержку), как указано в статье MSDN [Обработка временного сбоя].</span><span class="sxs-lookup"><span data-stu-id="609d5-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="609d5-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="609d5-183">Next steps</span></span>
<span data-ttu-id="609d5-184">В этом учебнике вы научились отправлять и получать сообщения с облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="609d5-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="609d5-185">Примеры комплексных решений, в которых используется Центр Интернета вещей, см. в [документации по Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="609d5-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="609d5-186">Дополнительные сведения о разработке решений с помощью Центра Интернета вещей см. в [руководстве для разработчиков Центра Интернета вещей].</span><span class="sxs-lookup"><span data-stu-id="609d5-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[пакет SDK NuGet для служб Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Обработка временного сбоя]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[руководстве для разработчиков Центра Интернета вещей]: iot-hub-devguide.md
[Подключение устройства к Центру Интернета вещей с помощью .NET]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[документации по Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[пакетов SDK для устройств Интернета вещей Azure]: iot-hub-devguide-sdks.md