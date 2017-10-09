---
title: "Центр IoT Azure aaaUse прямой методы (.NET/.NET) | Документы Microsoft"
description: "Как toouse центр IoT Azure направлять методы. Использовать устройства Azure IoT hello SDK для .NET tooimplement приложение имитированное устройство, которое включает прямой метод и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="2cd23-104">Использование прямых методов (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="2cd23-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="2cd23-105">В этом учебнике мы являются постоянной toodevelop два .NET консольного приложения:</span><span class="sxs-lookup"><span data-stu-id="2cd23-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="2cd23-106">**CallMethodOnDevice**, серверная часть приложения, который вызывает метод в приложение hello имитированное устройство и отображает ответ hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="2cd23-107">**SimulateDeviceMethods**, консольного приложения имитирует устройство соединение центра IoT tooyour с помощью удостоверения устройства hello, созданную ранее, которое отвечает toohello методе, вызванном hello облака.</span><span class="sxs-lookup"><span data-stu-id="2cd23-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="2cd23-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.</span><span class="sxs-lookup"><span data-stu-id="2cd23-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="2cd23-109">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="2cd23-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="2cd23-110">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2cd23-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2cd23-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2cd23-111">An active Azure account.</span></span> <span data-ttu-id="2cd23-112">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2cd23-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="2cd23-113">Следует удостоверения устройства hello toocreate программно вместо чтения hello соответствующий раздел в hello [подключиться с помощью .NET концентратор IoT tooyour имитированное устройство] [ lnk-device-identity-csharp] статьи.</span><span class="sxs-lookup"><span data-stu-id="2cd23-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2cd23-114">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="2cd23-114">Create a simulated device app</span></span>
<span data-ttu-id="2cd23-115">В этом разделе создайте консольное приложение .NET, которое отвечает tooa методе, вызванном обратно в решение hello end.</span><span class="sxs-lookup"><span data-stu-id="2cd23-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="2cd23-116">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="2cd23-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="2cd23-117">Имя проекта hello **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="2cd23-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Новое классическое приложение устройства Windows на языке Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="2cd23-119">В обозревателе решений щелкните правой кнопкой мыши hello **SimulateDeviceMethods** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2cd23-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2cd23-120">В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="2cd23-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="2cd23-121">Выберите **установить** tooinstall hello **Microsoft.Azure.Devices.Client** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="2cd23-122">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [устройств Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cd23-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Клиентское приложение в окне "Диспетчер пакетов NuGet"][img-clientnuget]
1. <span data-ttu-id="2cd23-124">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="2cd23-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="2cd23-125">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="2cd23-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="2cd23-126">Замените значение заполнителя hello строкой подключения устройства hello, записанное в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="2cd23-127">Добавьте следующие прямой метод tooimplement hello на устройстве hello hello:</span><span class="sxs-lookup"><span data-stu-id="2cd23-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="2cd23-128">Наконец, добавьте следующий код toohello hello **Main** метод tooopen hello tooyour IoT концентратора и инициализируйте hello метод прослушивателе подключений:</span><span class="sxs-lookup"><span data-stu-id="2cd23-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="2cd23-129">В обозревателе решений Visual Studio hello, щелкните правой кнопкой мыши решение и нажмите кнопку **назначить запускаемые проекты...** . Выберите **один запускаемый проект**, а затем выберите hello **SimulateDeviceMethods** проект в раскрывающемся меню hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="2cd23-130">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="2cd23-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2cd23-131">В рабочем коде следует реализовать политики повтора (например, повторного соединения), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="2cd23-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="2cd23-132">Вызов прямого метода на устройстве</span><span class="sxs-lookup"><span data-stu-id="2cd23-132">Call a direct method on a device</span></span>
<span data-ttu-id="2cd23-133">В этом разделе создайте консольное приложение .NET, которое вызывает метод в приложение hello имитированное устройство, а затем отображает hello ответа.</span><span class="sxs-lookup"><span data-stu-id="2cd23-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="2cd23-134">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="2cd23-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="2cd23-135">Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2cd23-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="2cd23-136">Имя проекта hello **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="2cd23-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createserviceapp]
2. <span data-ttu-id="2cd23-138">В обозревателе решений щелкните правой кнопкой мыши hello **CallMethodOnDevice** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2cd23-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="2cd23-139">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="2cd23-140">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="2cd23-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]

4. <span data-ttu-id="2cd23-142">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="2cd23-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="2cd23-143">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="2cd23-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="2cd23-144">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="2cd23-145">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="2cd23-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="2cd23-146">Этот метод вызывает прямой метод с именем `writeLine` на hello `myDeviceId` устройства.</span><span class="sxs-lookup"><span data-stu-id="2cd23-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="2cd23-147">Затем она записывает ответ hello, предоставляемый hello устройства на консоли hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="2cd23-148">Обратите внимание, как возможные toospecify значение времени ожидания для hello toorespond устройства.</span><span class="sxs-lookup"><span data-stu-id="2cd23-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="2cd23-149">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="2cd23-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="2cd23-150">В обозревателе решений Visual Studio hello, щелкните правой кнопкой мыши решение и нажмите кнопку **назначить запускаемые проекты...** . Выберите **один запускаемый проект**, а затем выберите hello **CallMethodOnDevice** проект в раскрывающемся меню hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="2cd23-151">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="2cd23-151">Run hello applications</span></span>
<span data-ttu-id="2cd23-152">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="2cd23-153">Выполните приложение устройства .NET hello **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="2cd23-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="2cd23-154">Оно будет ожидать вызовы методов от вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="2cd23-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Запуск приложения для устройства][img-deviceapprun]
1. <span data-ttu-id="2cd23-156">Теперь это устройство hello подключен и ожидание вызовов методов, запустите hello .NET **CallMethodOnDevice** метод hello tooinvoke приложения в приложение hello имитированное устройство.</span><span class="sxs-lookup"><span data-stu-id="2cd23-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="2cd23-157">Должно появиться hello устройства записи в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-157">You should see hello device response written in hello console.</span></span>
   
    ![Запуск приложения службы][img-serviceapprun]
1. <span data-ttu-id="2cd23-159">Затем устройство Hello реагирует метод toohello с печати это сообщение:</span><span class="sxs-lookup"><span data-stu-id="2cd23-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Прямой метод, вызываемый на устройстве hello][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="2cd23-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2cd23-161">Next steps</span></span>
<span data-ttu-id="2cd23-162">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="2cd23-163">Вы использовали этот устройства удостоверения tooenable hello имитируемые устройства приложения tooreact toomethods вызываемая hello облака.</span><span class="sxs-lookup"><span data-stu-id="2cd23-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="2cd23-164">Также было создано приложение, которое вызывает методы на устройстве hello и отображает hello ответа от устройства hello.</span><span class="sxs-lookup"><span data-stu-id="2cd23-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="2cd23-165">Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:</span><span class="sxs-lookup"><span data-stu-id="2cd23-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="2cd23-166">[Приступая к работе с Центром Интернета вещей]</span><span class="sxs-lookup"><span data-stu-id="2cd23-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="2cd23-167">[Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="2cd23-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="2cd23-168">toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="2cd23-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Приступая к работе с Центром Интернета вещей]: iot-hub-node-node-getstarted.md
