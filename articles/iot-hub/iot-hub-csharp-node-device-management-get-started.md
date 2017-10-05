---
title: "Приступая к работе с функцией управления устройствами Центра Интернета вещей Azure (.NET или Node) | Документация Майкрософт"
description: "Использование функции управления устройствами в Центре Интернета вещей Azure для начала удаленной перезагрузки устройства. Используйте пакет SDK для устройств Azure IoT для Node.js, чтобы реализовать приложение имитации устройства, включающее прямой метод, и пакет SDK для служб Azure IoT для .NET, чтобы реализовать приложение-службу, вызывающее прямой метод."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: d97fc5493570985f94c23032c870628d6a089dcd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="1dd54-104">Приступая к работе с управлением устройствами (.NET или Node)</span><span class="sxs-lookup"><span data-stu-id="1dd54-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="1dd54-105">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="1dd54-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="1dd54-106">Создание экземпляра Центра Интернета вещей на портале Azure и удостоверения устройства в экземпляре Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1dd54-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="1dd54-107">Создание приложения для имитации устройства с прямым методом, который позволяет выполнить перезагрузку устройства.</span><span class="sxs-lookup"><span data-stu-id="1dd54-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="1dd54-108">Прямые методы вызываются из облака.</span><span class="sxs-lookup"><span data-stu-id="1dd54-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="1dd54-109">Создание консольного приложения для .NET, вызывающего прямой метод перезагрузки в приложении имитации устройства с помощью Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="1dd54-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="1dd54-110">По завершении работы с этим руководством у вас будет консольное приложение устройства Node.js и консольное приложение серверной части .NET (C#).</span><span class="sxs-lookup"><span data-stu-id="1dd54-110">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="1dd54-111">**dmpatterns_getstarted_device.js**, которое подключается к вашему центру Интернета вещей с ранее созданным идентификатором устройства, получает прямой метод перезагрузки, имитирует физическую перезагрузку и сообщает о времени последней перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="1dd54-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="1dd54-112">**TriggerReboot**, которое вызывает прямой метод в приложении виртуального устройства, выводит ответ и отображает обновленные сообщаемые свойства.</span><span class="sxs-lookup"><span data-stu-id="1dd54-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="1dd54-113">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="1dd54-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1dd54-114">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1dd54-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1dd54-115">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="1dd54-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="1dd54-116">В статье [Prepare your development environment][lnk-dev-setup] (Подготовка среды разработки) описывается, как установить Node.js для работы с этим учебником в ОС Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd54-116">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="1dd54-117">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1dd54-117">An active Azure account.</span></span> <span data-ttu-id="1dd54-118">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1dd54-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="1dd54-119">Активация удаленной перезагрузки на устройстве с помощью прямого метода</span><span class="sxs-lookup"><span data-stu-id="1dd54-119">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="1dd54-120">В этом разделе вы создадите консольное приложение .NET (с помощью C#), которое инициирует удаленное обновление устройства с помощью прямого метода.</span><span class="sxs-lookup"><span data-stu-id="1dd54-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="1dd54-121">Приложение использует запросы двойника устройства для определения времени последней перезагрузки этого устройства.</span><span class="sxs-lookup"><span data-stu-id="1dd54-121">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="1dd54-122">В Visual Studio добавьте в новое решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-122">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="1dd54-123">Убедитесь, что указана версия платформы .NET 4.5.1 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="1dd54-123">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="1dd54-124">Назовите проект **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-124">Name the project **TriggerReboot**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

2. <span data-ttu-id="1dd54-126">В обозревателе решений щелкните правой кнопкой мыши проект **TriggerReboot** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-126">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="1dd54-127">В окне **Диспетчер пакетов NuGet** нажмите кнопку **Обзор**, найдите **microsoft.azure.devices**, щелкните **Установить**, чтобы установить пакет **Microsoft.Azure.Devices**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="1dd54-127">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="1dd54-128">В результате выполняется скачивание и установка пакета NuGet [SDK для служб Интернета вещей Azure][lnk-nuget-service-sdk] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="1dd54-128">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
4. <span data-ttu-id="1dd54-130">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="1dd54-130">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="1dd54-131">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="1dd54-131">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="1dd54-132">Замените значение заполнителя строкой подключения Центра Интернета вещей, созданного в предыдущем разделе, и целевого устройства.</span><span class="sxs-lookup"><span data-stu-id="1dd54-132">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="1dd54-133">Добавьте следующий метод в класс **Program**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-133">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="1dd54-134">Этот код получает двойник устройства для перезагрузки устройства и выводит сообщаемые свойства.</span><span class="sxs-lookup"><span data-stu-id="1dd54-134">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="1dd54-135">Добавьте следующий метод в класс **Program**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-135">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="1dd54-136">Этот код инициирует удаленную перезагрузку на устройстве с помощью прямого метода.</span><span class="sxs-lookup"><span data-stu-id="1dd54-136">This code initiates the reboot on the device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="1dd54-137">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="1dd54-137">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. <span data-ttu-id="1dd54-138">Выполните сборку решения.</span><span class="sxs-lookup"><span data-stu-id="1dd54-138">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="1dd54-139">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="1dd54-139">Create a simulated device app</span></span>
<span data-ttu-id="1dd54-140">В этом разделе вы сделаете следующее:</span><span class="sxs-lookup"><span data-stu-id="1dd54-140">In this section, you will</span></span>

* <span data-ttu-id="1dd54-141">создадите консольное приложение Node.js, отвечающее на прямой метод, вызываемый из облака;</span><span class="sxs-lookup"><span data-stu-id="1dd54-141">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="1dd54-142">запустите перезагрузку имитации устройства;</span><span class="sxs-lookup"><span data-stu-id="1dd54-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="1dd54-143">используете сообщаемые свойства в запросах двойника устройства для определения устройств и времени последней перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="1dd54-143">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="1dd54-144">Создайте пустую папку с именем **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="1dd54-145">В папке **manageddevice** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="1dd54-145">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="1dd54-146">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="1dd54-146">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1dd54-147">В командной строке в папке **manageddevice** выполните следующую команду, чтобы установить пакет SDK для устройств **azure-iot-device** и пакет **azure-iot-device-mqtt**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-147">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="1dd54-148">В текстовом редакторе создайте файл **dmpatterns_getstarted_device.js** в папке **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="1dd54-149">Добавьте следующие инструкции require в начале файла **dmpatterns_getstarted_device.js**:</span><span class="sxs-lookup"><span data-stu-id="1dd54-149">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="1dd54-150">Добавьте переменную **connectionString**, чтобы создать с ее помощью экземпляр **клиента**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-150">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="1dd54-151">Замените connection string строкой подключения своего устройства.</span><span class="sxs-lookup"><span data-stu-id="1dd54-151">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="1dd54-152">Добавьте следующую функцию, чтобы реализовать прямой метод на устройстве:</span><span class="sxs-lookup"><span data-stu-id="1dd54-152">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="1dd54-153">Добавьте следующий код, чтобы открыть подключение к Центру Интернета вещей и запустить прослушиватель прямого метода:</span><span class="sxs-lookup"><span data-stu-id="1dd54-153">Add the following code to open the connection to your IoT hub and start the direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="1dd54-154">Сохраните и закройте файл **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-154">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="1dd54-155">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="1dd54-155">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1dd54-156">В рабочем коде следует реализовать политики повторных попыток (например, с экспоненциальной задержкой), как указано в статье [Обработка временного сбоя][lnk-transient-faults] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="1dd54-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="1dd54-157">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="1dd54-157">Run the apps</span></span>
<span data-ttu-id="1dd54-158">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="1dd54-158">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="1dd54-159">В командной строке в папке **manageddevice** выполните следующую команду, чтобы начать прослушивание прямого метода перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="1dd54-159">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="1dd54-160">Запустите консольное приложение C# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-160">Run the C# console app **TriggerReboot**.</span></span> <span data-ttu-id="1dd54-161">Щелкните правой кнопкой мыши проект **TriggerReboot**, выберите **Отладка**, а затем щелкните **Запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="1dd54-161">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="1dd54-162">В консоли отобразится ответ устройства на прямой метод.</span><span class="sxs-lookup"><span data-stu-id="1dd54-162">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/