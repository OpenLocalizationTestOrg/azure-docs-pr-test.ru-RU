---
title: "сообщения aaaCloud на устройство с Azure IoT Hub (.NET) | Документы Microsoft"
description: "Способ toosend облака на устройство сообщений tooa устройств из центра Azure IoT с помощью hello Azure IoT, пакеты SDK для .NET. Изменение сообщений облака на устройство устройства tooreceive приложения и изменения сообщений облака на устройство hello toosend серверной части приложения."
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
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a><span data-ttu-id="e6ca8-104">Отправлять сообщения с устройства tooyour hello облака с IoT Hub (.NET)</span><span class="sxs-lookup"><span data-stu-id="e6ca8-104">Send messages from hello cloud tooyour device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="e6ca8-105">Введение</span><span class="sxs-lookup"><span data-stu-id="e6ca8-105">Introduction</span></span>
<span data-ttu-id="e6ca8-106">Центр Интернета вещей Azure — это полностью управляемая служба, которая обеспечивает надежный и защищенный двунаправленный обмен данными между миллионами устройств и серверной частью решения.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="e6ca8-107">Hello [приступить к работе с центром IoT] учебнике показано, как подготовить удостоверение устройства в нем toocreate центр IoT и кода приложения для устройств, отправляет сообщения из устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="e6ca8-108">Это руководство является логическим продолжением статьи [приступить к работе с центром IoT].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="e6ca8-109">В нем показано следующее:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-109">It shows you how to:</span></span>

* <span data-ttu-id="e6ca8-110">Из серверной части вашего решения отправьте сообщения облака на устройство tooa одно устройство через Центр IoT.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="e6ca8-111">Получение на устройстве сообщений, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="e6ca8-112">Из вашего решения внутренний запрос подтверждения доставки (*отзывы*) для сообщений отправленных tooa устройств из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="e6ca8-113">Дополнительные сведения о сообщениях облака на устройство можно найти в hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="e6ca8-114">В конце этого учебника hello выполните два консольных приложений .NET:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-114">At hello end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="e6ca8-115">**SimulatedDevice**, измененная версия приложения hello, созданного в [приступить к работе с центром IoT], который подключается tooyour центр IoT и получает сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="e6ca8-116">**SendCloudToDevice**, который отправляет приложения устройства toohello сообщение облака на устройство с помощью центра IoT, а затем получает подтверждение его доставки.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-116">**SendCloudToDevice**, which sends a cloud-to-device message toohello device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="e6ca8-117">В Центре Интернета вещей реализована поддержка для пакетов SDK для многих платформ устройств и языков (включая C, Java и Javascript). Эти пакеты работают на основе [пакетов SDK для устройств Интернета вещей Azure].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="e6ca8-118">Пошаговые инструкции по tooconnect кода учебник toothis устройства и обычно tooAzure центр IoT. в статье hello [руководстве для разработчиков центра IoT].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="e6ca8-119">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e6ca8-120">Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e6ca8-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="e6ca8-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-121">An active Azure account.</span></span> <span data-ttu-id="e6ca8-122">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-device-app"></a><span data-ttu-id="e6ca8-123">Получать сообщения в приложение hello устройства</span><span class="sxs-lookup"><span data-stu-id="e6ca8-123">Receive messages in hello device app</span></span>
<span data-ttu-id="e6ca8-124">В этом разделе необходимо изменить приложение hello устройства, созданный в [приступить к работе с центром IoT] tooreceive сообщений облака на устройство из центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-124">In this section, you'll modify hello device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="e6ca8-125">В Visual Studio в hello **SimulatedDevice** , добавьте следующий метод toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-125">In Visual Studio, in hello **SimulatedDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
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
   
    <span data-ttu-id="e6ca8-126">Hello `ReceiveAsync` метод асинхронно возвращает сообщение hello получено во время hello, получаемой устройством hello.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-126">hello `ReceiveAsync` method asynchronously returns hello received message at hello time that it is received by hello device.</span></span> <span data-ttu-id="e6ca8-127">Он возвращает *null* после задаваемого ожидания (в этом случае используется значение по умолчанию hello в минуту).</span><span class="sxs-lookup"><span data-stu-id="e6ca8-127">It returns *null* after a specifiable timeout period (in this case, hello default of one minute is used).</span></span> <span data-ttu-id="e6ca8-128">При получении приложение hello *null*, должен быть продолжен toowait для новых сообщений.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-128">When hello app receives a *null*, it should continue toowait for new messages.</span></span> <span data-ttu-id="e6ca8-129">Это требование является причиной hello hello `if (receivedMessage == null) continue` строки.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-129">This requirement is hello reason for hello `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="e6ca8-130">Здравствуйте вызов слишком`CompleteAsync()` уведомляет центра IoT успешно обработал сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-130">hello call too`CompleteAsync()` notifies IoT Hub that hello message has been successfully processed.</span></span> <span data-ttu-id="e6ca8-131">приветственное сообщение можно безопасно удалить из очереди устройства hello.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-131">hello message can be safely removed from hello device queue.</span></span> <span data-ttu-id="e6ca8-132">Если что-то произошло, приложение устройства предотвращено hello из завершение обработки приветственное сообщение hello, центр IoT доставляет его еще раз.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-132">If something happened that prevented hello device app from completing hello processing of hello message, IoT Hub delivers it again.</span></span> <span data-ttu-id="e6ca8-133">Очень важно затем этой логики в приложение hello устройства обработки сообщений был *идемпотентными*, после чего получение hello повторяется несколько раз выводятся hello того же результата.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-133">It is then important that message processing logic in hello device app is *idempotent*, so that receiving hello same message multiple times produces hello same result.</span></span> <span data-ttu-id="e6ca8-134">Приложения можно также временно отказ от сообщения, которое приводит к центра IoT, сохраняя приветственное сообщение hello очереди для последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-134">An application can also temporarily abandon a message, which results in IoT hub retaining hello message in hello queue for future consumption.</span></span> <span data-ttu-id="e6ca8-135">Или hello приложение может отклонить сообщение, которое окончательно удаляет приветственное сообщение из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-135">Or, hello application can reject a message, which permanently removes hello message from hello queue.</span></span> <span data-ttu-id="e6ca8-136">Дополнительные сведения о жизненного цикла облака на устройство сообщение hello. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-136">For more information about hello cloud-to-device message lifecycle, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e6ca8-137">При использовании HTTP вместо MQTT или AMQP, как транспорт, hello `ReceiveAsync` метод возвращается немедленно.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-137">When using HTTP instead of MQTT or AMQP as a transport, hello `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="e6ca8-138">шаблон Hello поддерживается для облака на устройство сообщений с HTTP является периодически подключенные устройства, которые проверьте редко сообщений (менее чем каждые 25 минут).</span><span class="sxs-lookup"><span data-stu-id="e6ca8-138">hello supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="e6ca8-139">Выдача дополнительные HTTP Получает результаты в центр IoT регулирования запросов hello.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-139">Issuing more HTTP receives results in IoT Hub throttling hello requests.</span></span> <span data-ttu-id="e6ca8-140">Дополнительные сведения об отличиях hello поддержки MQTT, AMQP и HTTP и центр IoT регулирования см. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-140">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="e6ca8-141">Добавьте следующий метод в hello hello **Main** метод прямо перед hello `Console.ReadLine()` строки:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-141">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="e6ca8-142">Для упрощения в этом учебнике не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e6ca8-143">В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="e6ca8-144">Отправка сообщения из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="e6ca8-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="e6ca8-145">В этом разделе записи .NET консольное приложение, которое отправляет приложения для устройств toohello сообщений облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-145">In this section, you write a .NET console app that sends cloud-to-device messages toohello device app.</span></span>

1. <span data-ttu-id="e6ca8-146">В текущем решении Visual Studio hello, создайте проект приложения рабочего стола Visual C# с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-146">In hello current Visual Studio solution, create a Visual C# Desktop App project by using hello **Console Application** project template.</span></span> <span data-ttu-id="e6ca8-147">Имя проекта hello **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-147">Name hello project **SendCloudToDevice**.</span></span>
   
    ![Новый проект в Visual Studio][20]
2. <span data-ttu-id="e6ca8-149">В обозревателе решений щелкните правой кнопкой мыши решение hello затем **управление пакетами NuGet для решения...** .</span><span class="sxs-lookup"><span data-stu-id="e6ca8-149">In Solution Explorer, right-click hello solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="e6ca8-150">Это действие открывает hello **управление пакетами NuGet** окна.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-150">This action opens hello **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="e6ca8-151">Поиск **Microsoft.Azure.Devices**, нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span> 
   
    <span data-ttu-id="e6ca8-152">Это загружает, устанавливает и добавляет toohello ссылки [пакет SDK NuGet службы Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-152">This downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="e6ca8-153">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-153">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="e6ca8-154">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="e6ca8-155">Замените значение заполнителя hello со строкой подключения концентратора IoT hello из [приступить к работе с центром IoT]:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-155">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="e6ca8-156">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-156">Add hello following method toohello **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="e6ca8-157">Этот метод отправляет новое устройство toohello облака на устройство сообщение с Идентификатором hello `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-157">This method sends a new cloud-to-device message toohello device with hello ID, `myFirstDevice`.</span></span> <span data-ttu-id="e6ca8-158">Измените этот параметр только в том случае, если он изменен из hello календарем, используемым в [приступить к работе с центром IoT].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-158">Change this parameter only if you modified it from hello one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="e6ca8-159">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-159">Finally, add hello following lines toohello **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="e6ca8-160">В Visual Studio щелкните правой кнопкой мыши свое решение и выберите пункт **Назначить запускаемые проекты**. Выберите **несколько запускаемых проектов**, а затем выберите hello **запустить** действие для **ReadDeviceToCloudMessages**, **SimulatedDevice**, и **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select hello **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="e6ca8-161">Нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-161">Press **F5**.</span></span> <span data-ttu-id="e6ca8-162">Должны запуститься все три приложения.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-162">All three applications should start.</span></span> <span data-ttu-id="e6ca8-163">Выберите hello **SendCloudToDevice** windows и клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-163">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="e6ca8-164">Вы увидите приветственных сообщений, полученных приложение hello устройства.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-164">You should see hello message being received by hello device app.</span></span>
   
   ![Приложение получает сообщение][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="e6ca8-166">Получение подтверждений доставки</span><span class="sxs-lookup"><span data-stu-id="e6ca8-166">Receive delivery feedback</span></span>
<span data-ttu-id="e6ca8-167">Это возможно toorequest доставки (или истечения срока действия) подтверждений от центра IoT для каждого сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-167">It is possible toorequest delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="e6ca8-168">Этот параметр включает hello решения серверной части tooeasily сообщают логику повтора или компенсации.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-168">This option enables hello solution back end tooeasily inform retry or compensation logic.</span></span> <span data-ttu-id="e6ca8-169">Дополнительные сведения об обратной связи облака на устройство см. в разделе hello [руководстве для разработчиков центра IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-169">For more information about cloud-to-device feedback, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="e6ca8-170">В этом разделе можно изменить hello **SendCloudToDevice** toorequest отзыва о приложении и его получения с центра IoT.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-170">In this section, you modify hello **SendCloudToDevice** app toorequest feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="e6ca8-171">В Visual Studio в hello **SendCloudToDevice** , добавьте следующий метод toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-171">In Visual Studio, in hello **SendCloudToDevice** project, add hello following method toohello **Program** class.</span></span>
   
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
   
    <span data-ttu-id="e6ca8-172">Обратите внимание, этот шаблон receive hello же сообщения облака на устройство tooreceive используется один из приложения hello устройства.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-172">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>
2. <span data-ttu-id="e6ca8-173">Добавьте следующий метод в hello hello **Main** метод сразу же после hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` строки:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-173">Add hello following method in hello **Main** method, right after hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="e6ca8-174">отзыв toorequest hello доставки сообщения облака на устройство, у вас есть toospecify свойство в hello **SendCloudToDeviceMessageAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-174">toorequest feedback for hello delivery of your cloud-to-device message, you have toospecify a property in hello **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="e6ca8-175">Добавьте следующие строки, сразу после hello hello `var commandMessage = new Message(...);` строки:</span><span class="sxs-lookup"><span data-stu-id="e6ca8-175">Add hello following line, right after hello `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="e6ca8-176">Запускайте приложения hello, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-176">Run hello apps by pressing **F5**.</span></span> <span data-ttu-id="e6ca8-177">Должны запуститься все три приложения.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-177">You should see all three applications start.</span></span> <span data-ttu-id="e6ca8-178">Выберите hello **SendCloudToDevice** windows и клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-178">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="e6ca8-179">Вы увидите hello сообщений, принимаемых приложением устройства hello и через несколько секунд, hello сообщение отзывов, полученных на **SendCloudToDevice** приложения.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-179">You should see hello message being received by hello device app, and after a few seconds, hello feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Приложение получает сообщение][22]

> [!NOTE]
> <span data-ttu-id="e6ca8-181">Для упрощения в этом учебнике не реализуются какие-либо политики повтора.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e6ca8-182">В рабочем коде следует реализовать политики повтора (например, экспоненциального отката), описанным в статье MSDN hello [обработка временных сбоев].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e6ca8-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6ca8-183">Next steps</span></span>
<span data-ttu-id="e6ca8-184">В этом учебнике вы узнали, как toosend и получать сообщения облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="e6ca8-184">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="e6ca8-185">см. Примеры toosee полное и всестороннее решений, использующих центр IoT [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-185">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="e6ca8-186">toolearn Дополнительные сведения о разработке решений с центром IoT разделе hello [руководстве для разработчиков центра IoT].</span><span class="sxs-lookup"><span data-stu-id="e6ca8-186">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[пакет SDK NuGet службы Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[обработка временных сбоев]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[руководстве для разработчиков центра IoT]: iot-hub-devguide.md
[приступить к работе с центром IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[пакетов SDK для устройств Интернета вещей Azure]: iot-hub-devguide-sdks.md