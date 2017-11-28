---
title: "aaaGet работы с управлением устройства Azure IoT Hub (.NET или узел) | Документы Microsoft"
description: "Как tooinitiate управления устройства Azure IoT Hub toouse перезагрузите удаленного устройства. Использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement приложение имитированное устройство, которое включает прямой метод и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое вызывает метод прямой hello."
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
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="99c99-104">Приступая к работе с управлением устройствами (.NET или Node)</span><span class="sxs-lookup"><span data-stu-id="99c99-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="99c99-105">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="99c99-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="99c99-106">Используйте hello Azure портала toocreate центр IoT и создать удостоверение устройства в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="99c99-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="99c99-107">Создание приложения для имитации устройства с прямым методом, который позволяет выполнить перезагрузку устройства.</span><span class="sxs-lookup"><span data-stu-id="99c99-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="99c99-108">Прямой методы вызываются из облака hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="99c99-109">Создайте консольное приложение .NET, которое вызывает метод прямой перезагрузки hello в приложение hello имитированное устройство через концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="99c99-109">Create a .NET console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="99c99-110">В конце этого учебника hello у вас есть приложение Node.js консоли устройства и консольного приложения серверной части .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="99c99-110">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="99c99-111">**dmpatterns_getstarted_device.js**, который подключает центра IoT tooyour с идентификатором hello устройства, созданный ранее, получает прямой метод перезагрузки, имитирует перезагрузка физического и отчеты hello время последней перезагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="99c99-112">**TriggerReboot**, прямой метод которого вызывает в приложение hello имитированное устройство, отображает ответ hello, и отображает hello обновлены данные свойства.</span><span class="sxs-lookup"><span data-stu-id="99c99-112">**TriggerReboot**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="99c99-113">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="99c99-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="99c99-114">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="99c99-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="99c99-115">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="99c99-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="99c99-116">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="99c99-116">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="99c99-117">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="99c99-117">An active Azure account.</span></span> <span data-ttu-id="99c99-118">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="99c99-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="99c99-119">Триггер удаленной перезагрузки на устройстве hello, с помощью прямой метод</span><span class="sxs-lookup"><span data-stu-id="99c99-119">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="99c99-120">В этом разделе вы создадите консольное приложение .NET (с помощью C#), которое инициирует удаленное обновление устройства с помощью прямого метода.</span><span class="sxs-lookup"><span data-stu-id="99c99-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="99c99-121">приложение Hello использует устройство двойных запросы toodiscover hello время последней перезагрузки для этого устройства.</span><span class="sxs-lookup"><span data-stu-id="99c99-121">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="99c99-122">В Visual Studio добавьте новое решение tooa проекта Visual C# Windows классического с помощью hello **консольного приложения (.NET Framework)** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="99c99-122">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="99c99-123">Убедитесь, что hello версии платформы .NET Framework 4.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="99c99-123">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="99c99-124">Имя проекта hello **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="99c99-124">Name hello project **TriggerReboot**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

2. <span data-ttu-id="99c99-126">В обозревателе решений щелкните правой кнопкой мыши hello **TriggerReboot** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="99c99-126">In Solution Explorer, right-click hello **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="99c99-127">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-127">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="99c99-128">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="99c99-128">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
4. <span data-ttu-id="99c99-130">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="99c99-130">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="99c99-131">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="99c99-131">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="99c99-132">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello и hello целевое устройство.</span><span class="sxs-lookup"><span data-stu-id="99c99-132">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section and hello target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="99c99-133">Добавьте следующий метод toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="99c99-133">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="99c99-134">Это двойных код получает hello устройства для перезагрузки устройства и выходы hello hello сообщил свойства.</span><span class="sxs-lookup"><span data-stu-id="99c99-134">This code gets hello device twin for hello rebooting device and outputs hello reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="99c99-135">Добавьте следующий метод toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="99c99-135">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="99c99-136">Этот код запускает hello перезагрузки на устройстве hello, с помощью прямого метода.</span><span class="sxs-lookup"><span data-stu-id="99c99-136">This code initiates hello reboot on hello device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="99c99-137">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="99c99-137">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. <span data-ttu-id="99c99-138">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-138">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="99c99-139">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="99c99-139">Create a simulated device app</span></span>
<span data-ttu-id="99c99-140">В этом разделе вы сделаете следующее:</span><span class="sxs-lookup"><span data-stu-id="99c99-140">In this section, you will</span></span>

* <span data-ttu-id="99c99-141">Создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака</span><span class="sxs-lookup"><span data-stu-id="99c99-141">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="99c99-142">запустите перезагрузку имитации устройства;</span><span class="sxs-lookup"><span data-stu-id="99c99-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="99c99-143">Используйте hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и при их последней перезагрузки</span><span class="sxs-lookup"><span data-stu-id="99c99-143">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="99c99-144">Создайте пустую папку с именем **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="99c99-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="99c99-145">В hello **manageddevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-145">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="99c99-146">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="99c99-146">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="99c99-147">В командной строке в hello **manageddevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:</span><span class="sxs-lookup"><span data-stu-id="99c99-147">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="99c99-148">В текстовом редакторе создайте новый **dmpatterns_getstarted_device.js** файла в hello **manageddevice** папки.</span><span class="sxs-lookup"><span data-stu-id="99c99-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="99c99-149">Добавьте следующие hello «требовать» операторы в начале hello hello **dmpatterns_getstarted_device.js** файла:</span><span class="sxs-lookup"><span data-stu-id="99c99-149">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="99c99-150">Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="99c99-150">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="99c99-151">Замените строку соединения hello строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="99c99-151">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="99c99-152">Добавить следующие функции tooimplement hello прямого метода на устройстве hello hello</span><span class="sxs-lookup"><span data-stu-id="99c99-152">Add hello following function tooimplement hello direct method on hello device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
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
7. <span data-ttu-id="99c99-153">Добавьте следующую hello кода hello подключения tooopen tooyour-центр IoT и запустить прослушиватель прямой метод hello:</span><span class="sxs-lookup"><span data-stu-id="99c99-153">Add hello following code tooopen hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="99c99-154">Сохраните и закройте hello **dmpatterns_getstarted_device.js** файла.</span><span class="sxs-lookup"><span data-stu-id="99c99-154">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="99c99-155">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="99c99-155">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="99c99-156">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="99c99-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-hello-apps"></a><span data-ttu-id="99c99-157">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="99c99-157">Run hello apps</span></span>
<span data-ttu-id="99c99-158">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-158">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="99c99-159">В командной строке hello в hello **manageddevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-159">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="99c99-160">Консольное приложение hello выполнения C# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="99c99-160">Run hello C# console app **TriggerReboot**.</span></span> <span data-ttu-id="99c99-161">Щелкните правой кнопкой мыши hello **TriggerReboot** проекта, выберите **отладки**и выберите **запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="99c99-161">Right-click hello **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="99c99-162">Появиться hello устройства toohello прямой метод ответа в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="99c99-162">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/