---
title: "обновление встроенного по aaaDevice с центром IoT Azure (.NET или узел) | Документы Microsoft"
description: "Как обновить toouse управления устройствами в центр IoT Azure tooinitiate микропрограммы устройства. Можно использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement приложения имитированное устройство и hello Azure IoT служба пакета SDK для .NET tooimplement службы приложений, которое вызывает обновление встроенного по hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a><span data-ttu-id="a8059-104">Использование устройства управления tooinitiate обновление встроенного по устройства (.NET или узел)</span><span class="sxs-lookup"><span data-stu-id="a8059-104">Use device management tooinitiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="a8059-105">Введение</span><span class="sxs-lookup"><span data-stu-id="a8059-105">Introduction</span></span>
<span data-ttu-id="a8059-106">В hello [начало работы с управлением устройствами] [ lnk-dm-getstarted] учебник, вы видели, как toouse hello [двойных устройства] [ lnk-devtwin] и [прямой методы] [ lnk-c2dmethod] tooremotely примитивы перезагрузить устройство.</span><span class="sxs-lookup"><span data-stu-id="a8059-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="a8059-107">В этом учебнике используется hello же примитивы центр IoT и показано, как toodo-законченный имитируемые обновление встроенного по.</span><span class="sxs-lookup"><span data-stu-id="a8059-107">This tutorial uses hello same IoT Hub primitives and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="a8059-108">Этот шаблон используется в реализации обновлений встроенного hello для hello [образец реализации устройства Raspberry Pi][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="a8059-108">This pattern is used in hello firmware update implementation for hello [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="a8059-109">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="a8059-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a8059-110">Создайте консольное приложение .NET, которое вызывает метод прямой firmwareUpdate hello в приложение hello имитированное устройство через концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="a8059-110">Create a .NET console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="a8059-111">Создайте приложение виртуального устройства, которое реализует прямой метод **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="a8059-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="a8059-112">Этот метод запускает многоэтапный процесс ожидает образ встроенного по toodownload hello, он загружает образ встроенного по hello и наконец применение hello образ встроенного по.</span><span class="sxs-lookup"><span data-stu-id="a8059-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="a8059-113">Во время каждого этапа обновления hello hello устройство использует hello сообщил свойства tooreport о ходе выполнения.</span><span class="sxs-lookup"><span data-stu-id="a8059-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="a8059-114">В конце этого учебника hello у вас есть приложение Node.js консоли устройства и консольного приложения серверной части .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="a8059-114">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="a8059-115">**dmpatterns_fwupdate_service.js**, прямой метод которого вызывает в приложение hello имитированное устройство, отображает ответ hello, и периодически (каждые 500 мс) отображает hello обновлены данные свойства.</span><span class="sxs-lookup"><span data-stu-id="a8059-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="a8059-116">**TriggerFWUpdate**, который подключает центра IoT tooyour с идентификатором hello устройства, созданный ранее, получает прямой метод firmwareUpdate, завершит toosimulate многими состояниями процесс обновления встроенного по том числе: ожидание hello образа загрузки, Загрузка нового образа hello и наконец применение образа hello.</span><span class="sxs-lookup"><span data-stu-id="a8059-116">**TriggerFWUpdate**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="a8059-117">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a8059-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a8059-118">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a8059-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a8059-119">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a8059-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="a8059-120">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="a8059-120">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a8059-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a8059-121">An active Azure account.</span></span> <span data-ttu-id="a8059-122">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a8059-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="a8059-123">Выполните hello [начало работы с управлением устройствами](iot-hub-csharp-node-device-management-get-started.md) статью toocreate ваш центр IoT и получить строки подключения центр IoT.</span><span class="sxs-lookup"><span data-stu-id="a8059-123">Follow hello [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="a8059-124">Вызвать обновление удаленного встроенного по на устройстве hello, с помощью прямой метод</span><span class="sxs-lookup"><span data-stu-id="a8059-124">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="a8059-125">В этом разделе вы создадите консольное приложение .NET (с помощью C#), которое инициирует удаленное обновление встроенного ПО на устройстве.</span><span class="sxs-lookup"><span data-stu-id="a8059-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="a8059-126">приложение Hello использует прямой метод tooinitiate hello обновления и использует устройство двойных запросы tooperiodically получить состояние hello обновления встроенного по active hello.</span><span class="sxs-lookup"><span data-stu-id="a8059-126">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="a8059-127">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="a8059-127">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="a8059-128">Имя проекта hello **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="a8059-128">Name hello project **TriggerFWUpdate**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

1. <span data-ttu-id="a8059-130">В обозревателе решений щелкните правой кнопкой мыши hello **TriggerFWUpdate** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="a8059-130">In Solution Explorer, right-click hello **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a8059-131">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="a8059-131">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="a8059-132">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="a8059-132">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="a8059-134">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="a8059-134">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="a8059-135">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="a8059-135">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="a8059-136">Замените hello несколько значений заполнитель с hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello и hello идентификатор устройства.</span><span class="sxs-lookup"><span data-stu-id="a8059-136">Replace hello multiple placeholder values with hello IoT Hub connection string for hello hub that you created in hello previous section and hello Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="a8059-137">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="a8059-137">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="a8059-138">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="a8059-138">Add hello following method toohello **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="a8059-139">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="a8059-139">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. <span data-ttu-id="a8059-140">В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **TriggerFWUpdate** проект является **запустить**.</span><span class="sxs-lookup"><span data-stu-id="a8059-140">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="a8059-141">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="a8059-141">Build hello solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="a8059-142">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="a8059-142">Run hello apps</span></span>
<span data-ttu-id="a8059-143">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a8059-143">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="a8059-144">В командной строке hello в hello **manageddevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="a8059-144">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="a8059-145">В Visual Studio щелкните правой кнопкой мыши на hello **TriggerFWUpdate** projectRun toohello C# консольное приложение, выберите **отладки** и **запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="a8059-145">In Visual Studio, right-click on hello **TriggerFWUpdate** projectRun toohello C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="a8059-146">Появиться hello устройства toohello прямой метод ответа в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="a8059-146">You see hello device response toohello direct method in hello console.</span></span>

    ![Успешное обновление встроенного ПО][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="a8059-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8059-148">Next steps</span></span>
<span data-ttu-id="a8059-149">В этом учебнике используется tootrigger прямой метод удаленного обновления встроенного по на устройстве и используемых hello сообщил свойства toofollow hello ход выполнения обновления встроенного по hello.</span><span class="sxs-lookup"><span data-stu-id="a8059-149">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="a8059-150">toolearn tooextend IoT решения и расписание метод вызывает на нескольких устройствах и разделе hello [расписание и широковещательных задания] [ lnk-tutorial-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="a8059-150">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/