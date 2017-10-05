---
title: "Использование прямых методов Центра Интернета вещей Azure (.NET или Node) | Документация Майкрософт"
description: "Использование прямых методов Центра Интернета вещей Azure. Используйте пакет SDK для устройств Azure IoT для Node.js, чтобы реализовать приложение имитации устройства, включающее прямой метод, и пакет SDK для служб Azure IoT для .NET, чтобы реализовать приложение-службу, вызывающее прямой метод."
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
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="7ed0f-104">Использование прямых методов (.NET или Node)</span><span class="sxs-lookup"><span data-stu-id="7ed0f-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="7ed0f-105">В этом руководстве мы разработаем консольное приложение .NET и Node.js.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="7ed0f-106">**CallMethodOnDevice.sln**, внутреннее приложение для .NET, которое вызывает метод в приложении имитации устройства и выводит ответ;</span><span class="sxs-lookup"><span data-stu-id="7ed0f-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="7ed0f-107">**TwinSimulatedDevice.js** — это приложение Node.js, имитирующее устройство, которое подключается к Центру Интернета вещей с созданным ранее удостоверением устройства и отвечает на метод, вызванный облаком.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="7ed0f-108">Статья о [пакетах SDK для Центра Интернета вещей Azure][lnk-hub-sdks] содержит сведения о различных пакетах SDK, которые можно использовать для создания приложений, которые будут работать на устройствах и в серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="7ed0f-109">Для работы с этим руководством необходимы указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="7ed0f-110">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="7ed0f-111">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="7ed0f-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-112">An active Azure account.</span></span> <span data-ttu-id="7ed0f-113">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="7ed0f-114">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="7ed0f-114">Create a simulated device app</span></span>
<span data-ttu-id="7ed0f-115">В этом разделе вы создадите консольное приложение для Node.js, отвечающее на метод, вызываемый из серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="7ed0f-116">Создайте пустую папку с именем **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="7ed0f-117">В папке **simulateddevice** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="7ed0f-118">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="7ed0f-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7ed0f-119">Чтобы установить пакеты **azure-iot-device** и **azure-iot-device-mqtt**, в командной строке в папке **simulateddevice** выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="7ed0f-120">В текстовом редакторе создайте в папке **simulateddevice** файл **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="7ed0f-121">Добавьте следующие инструкции `require` в начало файла **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="7ed0f-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="7ed0f-122">Добавьте переменную **connectionString**, чтобы создать с ее помощью экземпляр **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="7ed0f-123">Замените **{device connection string}** строкой подключения устройства, созданной в разделе *Создание удостоверения устройства*.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="7ed0f-124">Чтобы реализовать прямой метод на устройстве, добавьте следующую функцию:</span><span class="sxs-lookup"><span data-stu-id="7ed0f-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="7ed0f-125">Откройте подключение к Центру Интернета вещей и начните инициализацию прослушивателя метода.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="7ed0f-126">Сохраните и закройте файл **SimulatedDevice.js** .</span><span class="sxs-lookup"><span data-stu-id="7ed0f-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="7ed0f-127">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7ed0f-128">В рабочем коде следует реализовать политики повтора (например, повторную попытку подключения), как указано в статье MSDN [Обработка временного сбоя][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="7ed0f-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="7ed0f-129">Вызов прямого метода на устройстве</span><span class="sxs-lookup"><span data-stu-id="7ed0f-129">Call a direct method on a device</span></span>
<span data-ttu-id="7ed0f-130">В этом разделе вы создадите консольное приложение .NET, которое вызывает метод в приложении виртуального устройства и выводит ответ.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="7ed0f-131">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения** .</span><span class="sxs-lookup"><span data-stu-id="7ed0f-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="7ed0f-132">Убедитесь, что указана версия платформы .NET 4.5.1 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="7ed0f-133">Назовите проект **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][10]
2. <span data-ttu-id="7ed0f-135">В обозревателе решений щелкните правой кнопкой мыши проект **CallMethodOnDevice** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="7ed0f-136">В окне **Диспетчер пакетов NuGet** нажмите кнопку **Обзор**, найдите **microsoft.azure.devices**, щелкните **Установить**, чтобы установить пакет **Microsoft.Azure.Devices**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="7ed0f-137">В результате выполняется скачивание и установка пакета NuGet [SDK для служб Интернета вещей Azure][lnk-nuget-service-sdk] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][11]

4. <span data-ttu-id="7ed0f-139">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="7ed0f-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="7ed0f-140">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="7ed0f-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="7ed0f-141">Замените значение заполнителя строкой подключения к Центру Интернета вещей, созданному в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="7ed0f-142">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="7ed0f-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="7ed0f-143">Этот метод вызывает прямой метод с именем `writeLine` на устройстве `myDeviceId`.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="7ed0f-144">Затем он записывает ответ, предоставленный устройством, в консоли.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="7ed0f-145">Обратите внимание, что можно указать значение времени ожидания для ответа устройства.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="7ed0f-146">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="7ed0f-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="7ed0f-147">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="7ed0f-147">Run the applications</span></span>
<span data-ttu-id="7ed0f-148">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="7ed0f-149">В обозревателе решений Visual Studio щелкните правой кнопкой мыши решение и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="7ed0f-150">Щелкните **Один запускаемый проект**, а затем в раскрывающемся меню выберите проект **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="7ed0f-151">В командной строке в папке **simulateddevice** выполните следующую команду, чтобы начать прослушивать вызовы метода из Центра Интернета вещей:</span><span class="sxs-lookup"><span data-stu-id="7ed0f-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="7ed0f-152">Подождите, пока откроется виртуальное устройство: ![][7].</span><span class="sxs-lookup"><span data-stu-id="7ed0f-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="7ed0f-153">Теперь, когда устройство подключено и ожидает вызовов методов, запустите приложение .NET **CallMethodOnDevice** для вызова метода в приложении виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="7ed0f-154">В консоли отобразится ответ устройства.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="7ed0f-155">Устройство отреагирует на метод, выведя следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="7ed0f-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="7ed0f-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ed0f-156">Next steps</span></span>
<span data-ttu-id="7ed0f-157">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="7ed0f-158">Вы использовали удостоверение устройства, с помощью которого приложение имитации устройства может отвечать на методы, вызванные из облака.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="7ed0f-159">Вы также создали приложение, вызывающее методы на устройстве и выводящее ответ устройства.</span><span class="sxs-lookup"><span data-stu-id="7ed0f-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="7ed0f-160">Чтобы продолжить знакомство с Центром Интернета вещей и изучить другие сценарии Интернета вещей, см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7ed0f-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="7ed0f-161">[Начало работы с Центром Интернета вещей]</span><span class="sxs-lookup"><span data-stu-id="7ed0f-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="7ed0f-162">[Планирование заданий на нескольких устройствах (предварительная версия)][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="7ed0f-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="7ed0f-163">Дополнительные сведения о расширении решения Центра Интернета вещей и планировании вызовов методов на нескольких устройствах см. в учебнике [Планирование и трансляция заданий][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="7ed0f-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
<span data-ttu-id="7ed0f-164">[Начало работы с Центром Интернета вещей]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="7ed0f-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
