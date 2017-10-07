---
title: "Центр IoT Azure aaaUse прямой методы (.NET или узел) | Документы Microsoft"
description: "Как toouse центр IoT Azure направлять методы. Использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement приложение имитированное устройство, которое включает прямой метод и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое вызывает метод прямой hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="1aaef-104">Использование прямых методов (.NET или Node)</span><span class="sxs-lookup"><span data-stu-id="1aaef-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="1aaef-105">В этом учебнике мы будем toodevelop .NET и Node.js консольного приложения:</span><span class="sxs-lookup"><span data-stu-id="1aaef-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="1aaef-106">**CallMethodOnDevice.sln**, приложении серверной части .NET, который вызывает метод в приложение hello имитированное устройство и отображает hello ответа.</span><span class="sxs-lookup"><span data-stu-id="1aaef-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="1aaef-107">**SimulatedDevice.js**, Node.js приложение, которое имитирует устройство соединение центра IoT tooyour с помощью удостоверения устройства hello, созданного ранее и отвечает toohello методе, вызванном hello облака.</span><span class="sxs-lookup"><span data-stu-id="1aaef-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="1aaef-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild toorun обоих приложений на устройствах и серверной части вашего решения.</span><span class="sxs-lookup"><span data-stu-id="1aaef-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="1aaef-109">toocomplete этого учебника, необходимо:</span><span class="sxs-lookup"><span data-stu-id="1aaef-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="1aaef-110">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1aaef-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1aaef-111">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="1aaef-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="1aaef-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1aaef-112">An active Azure account.</span></span> <span data-ttu-id="1aaef-113">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1aaef-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="1aaef-114">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="1aaef-114">Create a simulated device app</span></span>
<span data-ttu-id="1aaef-115">В этом разделе создайте консольное приложение Node.js, которое отвечает tooa методе, вызванном обратно в решение hello окончания.</span><span class="sxs-lookup"><span data-stu-id="1aaef-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="1aaef-116">Создайте пустую папку с именем **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="1aaef-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="1aaef-117">В hello **simulateddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="1aaef-118">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="1aaef-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1aaef-119">В командной строке в hello **simulateddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** и **azure iot устройства mqtt** пакетов:</span><span class="sxs-lookup"><span data-stu-id="1aaef-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="1aaef-120">В текстовом редакторе создайте файл в hello **simulateddevice** папки и назовите его **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="1aaef-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="1aaef-121">Добавьте следующее hello `require` инструкции на hello начала hello **SimulatedDevice.js** файла:</span><span class="sxs-lookup"><span data-stu-id="1aaef-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="1aaef-122">Добавить **connectionString** переменной и использовать его toocreate **DeviceClient** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1aaef-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="1aaef-123">Замените **{строка подключения устройства}** со строкой подключения устройства hello, созданное в hello *создать удостоверение устройства* раздела:</span><span class="sxs-lookup"><span data-stu-id="1aaef-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="1aaef-124">Добавьте следующие функции tooimplement hello прямого метода на устройстве hello hello:</span><span class="sxs-lookup"><span data-stu-id="1aaef-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="1aaef-125">Откройте центр IoT tooyour подключения hello и инициализировать прослушиватель hello метод:</span><span class="sxs-lookup"><span data-stu-id="1aaef-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="1aaef-126">Сохраните и закройте hello **SimulatedDevice.js** файла.</span><span class="sxs-lookup"><span data-stu-id="1aaef-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="1aaef-127">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="1aaef-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1aaef-128">В рабочем коде следует реализовать политики повтора (например, повторного соединения), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="1aaef-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="1aaef-129">Вызов прямого метода на устройстве</span><span class="sxs-lookup"><span data-stu-id="1aaef-129">Call a direct method on a device</span></span>
<span data-ttu-id="1aaef-130">В этом разделе создайте консольное приложение .NET, которое вызывает метод в приложение hello имитированное устройство, а затем отображает hello ответа.</span><span class="sxs-lookup"><span data-stu-id="1aaef-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="1aaef-131">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="1aaef-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="1aaef-132">Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1aaef-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="1aaef-133">Имя проекта hello **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="1aaef-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][10]
2. <span data-ttu-id="1aaef-135">В обозревателе решений щелкните правой кнопкой мыши hello **CallMethodOnDevice** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="1aaef-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="1aaef-136">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="1aaef-137">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="1aaef-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][11]

4. <span data-ttu-id="1aaef-139">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="1aaef-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="1aaef-140">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="1aaef-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="1aaef-141">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="1aaef-142">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="1aaef-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="1aaef-143">Этот метод вызывает прямой метод с именем `writeLine` на hello `myDeviceId` устройства.</span><span class="sxs-lookup"><span data-stu-id="1aaef-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="1aaef-144">Затем она записывает ответ hello, предоставляемый hello устройства на консоли hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="1aaef-145">Обратите внимание, как возможные toospecify значение времени ожидания для hello toorespond устройства.</span><span class="sxs-lookup"><span data-stu-id="1aaef-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="1aaef-146">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="1aaef-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="1aaef-147">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="1aaef-147">Run hello applications</span></span>
<span data-ttu-id="1aaef-148">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="1aaef-149">В обозревателе решений Visual Studio hello, щелкните правой кнопкой мыши решение и нажмите кнопку **назначить запускаемые проекты...** . Выберите **один запускаемый проект**, а затем выберите hello **CallMethodOnDevice** проект в раскрывающемся меню hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="1aaef-150">В командной строке в hello **simulateddevice** папки, запустите следующие команды toostart прослушивание вызовы методов из вашего центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="1aaef-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="1aaef-151">Ожидание tooopen hello имитируемые устройства.![][7]</span><span class="sxs-lookup"><span data-stu-id="1aaef-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="1aaef-152">Теперь это устройство hello подключен и ожидание вызовов методов, запустите hello .NET **CallMethodOnDevice** метод hello tooinvoke приложения в приложение hello имитированное устройство.</span><span class="sxs-lookup"><span data-stu-id="1aaef-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="1aaef-153">Должно появиться hello устройства записи в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="1aaef-154">Затем устройство Hello реагирует метод toohello с печати это сообщение:</span><span class="sxs-lookup"><span data-stu-id="1aaef-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="1aaef-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1aaef-155">Next steps</span></span>
<span data-ttu-id="1aaef-156">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="1aaef-157">Вы использовали этот устройства удостоверения tooenable hello имитируемые устройства приложения tooreact toomethods вызываемая hello облака.</span><span class="sxs-lookup"><span data-stu-id="1aaef-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="1aaef-158">Также было создано приложение, которое вызывает методы на устройстве hello и отображает hello ответа от устройства hello.</span><span class="sxs-lookup"><span data-stu-id="1aaef-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="1aaef-159">Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:</span><span class="sxs-lookup"><span data-stu-id="1aaef-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="1aaef-160">[Приступая к работе с Центром Интернета вещей]</span><span class="sxs-lookup"><span data-stu-id="1aaef-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="1aaef-161">[Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)</span><span class="sxs-lookup"><span data-stu-id="1aaef-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="1aaef-162">toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="1aaef-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Приступая к работе с Центром Интернета вещей]: iot-hub-node-node-getstarted.md
