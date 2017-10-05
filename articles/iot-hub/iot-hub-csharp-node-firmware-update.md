---
title: "Обновление встроенного ПО устройства c помощью Центра Интернета вещей Azure (.NET или Node) | Документация Майкрософт"
description: "Запуск обновления встроенного ПО устройства с помощью функции управления устройствами в Центре Интернета вещей. Используйте пакет SDK для устройств Azure IoT для Node.js, чтобы реализовать приложение имитации устройства, и пакет SDK для служб Azure IoT для .NET, чтобы реализовать приложение-службу, которое запустит процесс обновления встроенного ПО."
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
ms.openlocfilehash: c2192328a152e955d182c4a07b391c98a5960964
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="e5be6-104">Использование функции управления устройствами для начала обновления встроенного ПО устройства (.NET или Node)</span><span class="sxs-lookup"><span data-stu-id="e5be6-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="e5be6-105">Введение</span><span class="sxs-lookup"><span data-stu-id="e5be6-105">Introduction</span></span>
<span data-ttu-id="e5be6-106">В руководстве по [началу управления устройством][lnk-dm-getstarted] вы узнали, как использовать [двойник устройства][lnk-devtwin] и [прямые методы][lnk-c2dmethod] для удаленной перезагрузки устройства.</span><span class="sxs-lookup"><span data-stu-id="e5be6-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="e5be6-107">В этом руководстве используются те же примитивы Центра Интернета вещей, а также содержатся рекомендации по комплексному обновлению имитации встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="e5be6-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="e5be6-108">Этот шаблон используется в реализации обновления встроенного ПО для [примера реализации устройства Raspberry Pi][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="e5be6-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="e5be6-109">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="e5be6-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="e5be6-110">Создание консольного приложения для .NET, вызывающего прямой метод firmwareUpdate в приложении имитации устройства с помощью Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e5be6-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="e5be6-111">Создайте приложение виртуального устройства, которое реализует прямой метод **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="e5be6-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="e5be6-112">Этот метод запускает многоэтапный процесс, который сначала ожидает скачивания образа встроенного ПО, а затем скачивает его и применяет.</span><span class="sxs-lookup"><span data-stu-id="e5be6-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="e5be6-113">В ходе выполнения каждого этапа обновления устройство использует сообщаемые свойства для продолжения процесса.</span><span class="sxs-lookup"><span data-stu-id="e5be6-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="e5be6-114">По завершении работы с этим руководством у вас будет консольное приложение устройства Node.js и консольное приложение серверной части .NET (C#).</span><span class="sxs-lookup"><span data-stu-id="e5be6-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="e5be6-115">**dmpatterns_fwupdate_service.js**, которое вызывает прямой метод в приложении виртуального устройства, выводит ответ и периодически (каждые 500 миллисекунд) отображает обновленные сообщаемые свойства.</span><span class="sxs-lookup"><span data-stu-id="e5be6-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="e5be6-116">**TriggerFWUpdate**, которое подключается к Центру Интернета вещей с использованием удостоверения устройства, созданного ранее, получает прямой метод firmwareUpdate, запускает процесс с несколькими состояниями для имитации обновления встроенного ПО, состоящий из нескольких этапов (ожидание скачивания образа, скачивание нового образа и применение образа).</span><span class="sxs-lookup"><span data-stu-id="e5be6-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="e5be6-117">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="e5be6-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e5be6-118">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e5be6-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="e5be6-119">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e5be6-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="e5be6-120">В статье [Prepare your development environment][lnk-dev-setup] (Подготовка среды разработки) описывается, как установить Node.js для работы с этим учебником в ОС Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="e5be6-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="e5be6-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e5be6-121">An active Azure account.</span></span> <span data-ttu-id="e5be6-122">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e5be6-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="e5be6-123">Следуйте указаниям статьи [Руководство по началу работы с управлением устройствами](iot-hub-csharp-node-device-management-get-started.md), чтобы создать Центр Интернета вещей и получить строку подключения Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="e5be6-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="e5be6-124">Активация удаленного обновления встроенного ПО на устройстве с помощью прямого метода</span><span class="sxs-lookup"><span data-stu-id="e5be6-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="e5be6-125">В этом разделе вы создадите консольное приложение .NET (с помощью C#), которое инициирует удаленное обновление встроенного ПО на устройстве.</span><span class="sxs-lookup"><span data-stu-id="e5be6-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="e5be6-126">Приложение использует прямой метод для запуска обновления, а также применяет запросы двойников устройства для периодического получения состояния обновления активного встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="e5be6-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="e5be6-127">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения** .</span><span class="sxs-lookup"><span data-stu-id="e5be6-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="e5be6-128">Назовите проект **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="e5be6-128">Name the project **TriggerFWUpdate**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

1. <span data-ttu-id="e5be6-130">В обозревателе решений щелкните правой кнопкой мыши проект **TriggerFWUpdate** и выберите **Управление пакетами NuGet…**.</span><span class="sxs-lookup"><span data-stu-id="e5be6-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="e5be6-131">В окне **Диспетчер пакетов NuGet** нажмите кнопку **Обзор**, найдите **microsoft.azure.devices**, щелкните **Установить**, чтобы установить пакет **Microsoft.Azure.Devices**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="e5be6-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="e5be6-132">В результате выполняется скачивание и установка пакета NuGet [SDK для служб Интернета вещей Azure][lnk-nuget-service-sdk] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="e5be6-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="e5be6-134">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="e5be6-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="e5be6-135">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="e5be6-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="e5be6-136">Замените несколько значений заполнителей строкой подключения Центра Интернета вещей, созданного в предыдущем разделе, и идентификатором устройства.</span><span class="sxs-lookup"><span data-stu-id="e5be6-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="e5be6-137">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="e5be6-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="e5be6-138">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="e5be6-138">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="e5be6-139">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="e5be6-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="e5be6-140">В обозревателе решений откройте **Задать автозагружаемые проекты...** и задайте значение **Запустить** для параметра **Действие** проекта **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="e5be6-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="e5be6-141">Выполните сборку решения.</span><span class="sxs-lookup"><span data-stu-id="e5be6-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="e5be6-142">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="e5be6-142">Run the apps</span></span>
<span data-ttu-id="e5be6-143">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="e5be6-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="e5be6-144">В командной строке в папке **manageddevice** выполните следующую команду, чтобы начать прослушивание прямого метода перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5be6-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="e5be6-145">В Visual Studio щелкните правой кнопкой мыши проект **TriggerFWUpdate**, запустите его в консольном приложении C#, а затем выберите **Отладка** и **Запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="e5be6-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="e5be6-146">В консоли появится ответ устройства на прямой метод.</span><span class="sxs-lookup"><span data-stu-id="e5be6-146">You see the device response to the direct method in the console.</span></span>

    ![Успешное обновление встроенного ПО][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="e5be6-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5be6-148">Next steps</span></span>
<span data-ttu-id="e5be6-149">В этом руководстве вы использовали прямой метод для активации удаленного обновления встроенного ПО на устройстве. Также вы использовали переданные свойства для отслеживания хода обновления встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="e5be6-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="e5be6-150">Дополнительные сведения о расширении решения Центра Интернета вещей и планировании вызовов методов на нескольких устройствах см. в учебнике [Планирование и трансляция заданий][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="e5be6-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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