---
title: "aaaSchedule заданий с центром IoT Azure (.NET или узел) | Документы Microsoft"
description: "Как tooschedule центр IoT Azure заданий tooinvoke прямой метод на нескольких устройствах. Использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement hello имитируемые приложения для устройств и hello Azure IoT служба пакета SDK для .NET tooimplement задание службы toorun приложения hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="43425-104">Планирование и трансляция заданий (.NET или Node.js)</span><span class="sxs-lookup"><span data-stu-id="43425-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="43425-105">Используйте центр IoT Azure tooschedule и отслеживать задания, которые обновляют миллионов устройств.</span><span class="sxs-lookup"><span data-stu-id="43425-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="43425-106">Что можно сделать с помощью заданий?</span><span class="sxs-lookup"><span data-stu-id="43425-106">Use jobs to:</span></span>

* <span data-ttu-id="43425-107">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="43425-107">Update desired properties</span></span>
* <span data-ttu-id="43425-108">Обновление тегов</span><span class="sxs-lookup"><span data-stu-id="43425-108">Update tags</span></span>
* <span data-ttu-id="43425-109">Вызов прямых методов</span><span class="sxs-lookup"><span data-stu-id="43425-109">Invoke direct methods</span></span>

<span data-ttu-id="43425-110">Задание включает одно из следующих действий и отслеживает hello выполнения для набора устройств, определяется запрос двойных устройства.</span><span class="sxs-lookup"><span data-stu-id="43425-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="43425-111">Например приложение серверной части можно использовать tooinvoke задания прямой метод на 10 000 устройств, которые перезагрузки устройства hello.</span><span class="sxs-lookup"><span data-stu-id="43425-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="43425-112">Укажите hello устройств с помощью запроса двойных устройства и запланировать задание toorun hello в будущем.</span><span class="sxs-lookup"><span data-stu-id="43425-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="43425-113">отслеживает ход выполнения задания Hello имени каждого из устройств hello получают и выполнить прямой метод перезагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="43425-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="43425-114">toolearn Дополнительные сведения о каждой из этих возможностей см.:</span><span class="sxs-lookup"><span data-stu-id="43425-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="43425-115">Двойных устройства и свойства: [Приступая к работе с устройством близнецы] [ lnk-get-started-twin] и [учебника: как свойства двойных toouse устройства][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="43425-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="43425-116">Прямые методы: [Общие сведения о прямых методах и информация о вызове этих методов из Центра Интернета вещей][lnk-dev-methods] и [Использование прямых методов на устройстве Интернета вещей (Node.js)][lnk-c2d-methods].</span><span class="sxs-lookup"><span data-stu-id="43425-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="43425-117">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="43425-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="43425-118">Создание приложения для устройств, реализующий прямой метод с именем **lockDoor** , может быть вызван приложение hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="43425-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="43425-119">приложение Hello устройства также получает изменения требуемое свойство из серверной части приложения hello.</span><span class="sxs-lookup"><span data-stu-id="43425-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="43425-120">Создания серверной части приложения, которое создает задание toocall hello **lockDoor** прямой метод на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="43425-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="43425-121">Требуемое свойство обновить устройства toomultiple отправляет другим заданием.</span><span class="sxs-lookup"><span data-stu-id="43425-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="43425-122">В конце этого учебника hello у вас есть приложение Node.js консоли устройства и консольного приложения серверной части .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="43425-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="43425-123">**simDevice.js** , соединяет центр IoT tooyour, реализующий hello **lockDoor** прямой метод и обрабатывает требуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="43425-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="43425-124">**ScheduleJob** , использующий hello задания toocall **lockDoor** прямой метод и обновление двойных hello устройства требуемого свойства на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="43425-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="43425-125">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="43425-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="43425-126">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="43425-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="43425-127">Node.js 0.12.x или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="43425-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="43425-128">статья Hello [подготовить среду разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="43425-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="43425-129">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="43425-129">An active Azure account.</span></span> <span data-ttu-id="43425-130">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="43425-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="43425-131">Планирование заданий для вызова прямого метода и обновления свойств двойника устройства</span><span class="sxs-lookup"><span data-stu-id="43425-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="43425-132">В этом разделе создайте .NET консольного приложения (с помощью C#), использующий hello задания toocall **lockDoor** прямой метод и отправить требуемое свойство обновить toomultiple устройства.</span><span class="sxs-lookup"><span data-stu-id="43425-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="43425-133">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="43425-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="43425-134">Имя проекта hello **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="43425-134">Name hello project **ScheduleJob**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

1. <span data-ttu-id="43425-136">В обозревателе решений щелкните правой кнопкой мыши hello **ScheduleJob** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="43425-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="43425-137">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="43425-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="43425-138">Этот шаг загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="43425-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="43425-140">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="43425-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="43425-141">Добавьте следующее hello `using` инструкции, если он уже имеется в инструкциях по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="43425-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="43425-142">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="43425-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="43425-143">Замените заполнитель hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="43425-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="43425-144">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="43425-144">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. <span data-ttu-id="43425-145">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="43425-145">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. <span data-ttu-id="43425-146">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="43425-146">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. <span data-ttu-id="43425-147">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="43425-147">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="43425-148">В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **ScheduleJob** проект является **запустить**.</span><span class="sxs-lookup"><span data-stu-id="43425-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="43425-149">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="43425-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="43425-150">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="43425-150">Create a simulated device app</span></span>

<span data-ttu-id="43425-151">В этом разделе создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака, активизирующий перезагрузка имитации устройства и использует hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и когда они последней перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="43425-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="43425-152">Создайте пустую папку с именем **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="43425-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="43425-153">В hello **simDevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="43425-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="43425-154">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="43425-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="43425-155">В командной строке в hello **simDevice** папку, следующая команда tooinstall hello hello **azure iot устройства** и **azure iot устройства mqtt** пакетов:</span><span class="sxs-lookup"><span data-stu-id="43425-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="43425-156">В текстовом редакторе создайте новый **simDevice.js** файла в hello **simDevice** папки.</span><span class="sxs-lookup"><span data-stu-id="43425-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="43425-157">Добавьте следующие hello «требовать» операторы в начале hello hello **simDevice.js** файла:</span><span class="sxs-lookup"><span data-stu-id="43425-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="43425-158">Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="43425-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="43425-159">Сделайте заполнители hello убедиться, что tooreplace установки tooyour соответствующие значения.</span><span class="sxs-lookup"><span data-stu-id="43425-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="43425-160">Добавить следующие функции hello toohandle hello **lockDoor** метод.</span><span class="sxs-lookup"><span data-stu-id="43425-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="43425-161">Добавьте следующий код обработчика hello tooregister для hello hello **lockDoor** метод.</span><span class="sxs-lookup"><span data-stu-id="43425-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="43425-162">Сохраните и закройте hello **simDevice.js** файла.</span><span class="sxs-lookup"><span data-stu-id="43425-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="43425-163">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="43425-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="43425-164">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="43425-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="43425-165">Запускайте приложения hello</span><span class="sxs-lookup"><span data-stu-id="43425-165">Run hello apps</span></span>

<span data-ttu-id="43425-166">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="43425-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="43425-167">В командной строке hello в hello **simDevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="43425-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="43425-168">Консольное приложение hello выполнения C# **ScheduleJob** , щелкнув hello **ScheduleJob** проект, выбрав **отладки** и **запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="43425-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="43425-169">Вы видите hello выходные данные из устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="43425-169">You see hello output from both device and back-end apps.</span></span>

    ![Запуск приложения hello tooschedule заданий][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="43425-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43425-171">Next steps</span></span>

<span data-ttu-id="43425-172">В этом учебнике используется задание tooschedule прямой метод tooa устройства и hello обновление свойств устройства двойных hello.</span><span class="sxs-lookup"><span data-stu-id="43425-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="43425-173">Приступая к работе с центр IoT и устройства управления шаблонами, например удаленного через обновление встроенного по воздуху hello, чтение toocontinue [учебника: как toodo встроенное по обновить][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="43425-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="43425-174">Приступая к работе с центром IoT toocontinue в разделе [Приступая к работе с краем IoT][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="43425-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
