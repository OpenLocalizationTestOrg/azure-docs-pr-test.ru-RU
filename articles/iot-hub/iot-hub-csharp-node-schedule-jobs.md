---
title: "Планирование заданий c помощью Центра Интернета вещей Azure (.NET или Node) | Документация Майкрософт"
description: "Планирование заданий с помощью Центра Интернета вещей Azure для вызова прямого метода на нескольких устройствах. Используйте пакет SDK для устройств Azure IoT для Node.js, чтобы реализовать приложение имитации устройства, и пакет SDK для служб Azure IoT для .NET, чтобы реализовать приложение-службу, которое выполняет задание."
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
ms.openlocfilehash: a8f4f34aa99c4a9966957cac213ec9170de80a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="e4965-104">Планирование и трансляция заданий (.NET или Node.js)</span><span class="sxs-lookup"><span data-stu-id="e4965-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="e4965-105">Центр Интернета вещей Azure позволяет планировать и отслеживать задания по обновлению для миллионов устройств.</span><span class="sxs-lookup"><span data-stu-id="e4965-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="e4965-106">Что можно сделать с помощью заданий?</span><span class="sxs-lookup"><span data-stu-id="e4965-106">Use jobs to:</span></span>

* <span data-ttu-id="e4965-107">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="e4965-107">Update desired properties</span></span>
* <span data-ttu-id="e4965-108">Обновление тегов</span><span class="sxs-lookup"><span data-stu-id="e4965-108">Update tags</span></span>
* <span data-ttu-id="e4965-109">Вызов прямых методов</span><span class="sxs-lookup"><span data-stu-id="e4965-109">Invoke direct methods</span></span>

<span data-ttu-id="e4965-110">Задание выступает в роли оболочки для одного из этих действий и отслеживает его выполнение для определенного набора устройств в соответствии с запросом на двойнике устройства.</span><span class="sxs-lookup"><span data-stu-id="e4965-110">A job wraps one of these actions and tracks the execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="e4965-111">Например, внутреннее приложение может использовать задание для вызова прямого метода перезапуска на 10 000 устройств.</span><span class="sxs-lookup"><span data-stu-id="e4965-111">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="e4965-112">Вы можете определить набор устройств с помощью запроса на двойнике устройства и запланировать момент времени в будущем для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="e4965-112">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="e4965-113">Задание отслеживает ход выполнения по мере того, как каждое из устройств получает вызов и выполняет прямой метод перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="e4965-113">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="e4965-114">Дополнительные сведения об этих возможностях см. в указанных ниже статьях.</span><span class="sxs-lookup"><span data-stu-id="e4965-114">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="e4965-115">Двойники устройств и свойства: [Приступая к работе с двойниками устройств (предварительная версия)][lnk-get-started-twin] и [Руководство. Настройка устройств с помощью требуемых свойств (предварительная версия)][lnk-twin-props].</span><span class="sxs-lookup"><span data-stu-id="e4965-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="e4965-116">Прямые методы: [Общие сведения о прямых методах и информация о вызове этих методов из Центра Интернета вещей][lnk-dev-methods] и [Использование прямых методов на устройстве Интернета вещей (Node.js)][lnk-c2d-methods].</span><span class="sxs-lookup"><span data-stu-id="e4965-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="e4965-117">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="e4965-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="e4965-118">Создание приложения для устройств, которое реализует прямой метод **lockDoor**, вызываемый внутренним приложением.</span><span class="sxs-lookup"><span data-stu-id="e4965-118">Create a device app that implements a direct method called **lockDoor** that can be called by the back-end app.</span></span> <span data-ttu-id="e4965-119">Приложение для устройств также получает от внутреннего приложения запросы на изменение свойств.</span><span class="sxs-lookup"><span data-stu-id="e4965-119">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="e4965-120">Создание внутреннего приложения, которое создает задание для вызова прямого метода **lockDoor** на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="e4965-120">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="e4965-121">Еще одно задание отправляет обновления нужных свойств на несколько устройств.</span><span class="sxs-lookup"><span data-stu-id="e4965-121">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="e4965-122">По завершении работы с этим руководством у вас будет консольное приложение устройства Node.js и консольное приложение серверной части .NET (C#).</span><span class="sxs-lookup"><span data-stu-id="e4965-122">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="e4965-123">**simDevice.js** подключается к Центру Интернета вещей, выполняет прямой метод **lockDoor** и обрабатывает изменения свойств.</span><span class="sxs-lookup"><span data-stu-id="e4965-123">**simDevice.js** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="e4965-124">**ScheduleJob** использует задания для вызова прямого метода **lockDoor** и для обновления на нескольких устройствах свойств, установленных на двойнике устройства.</span><span class="sxs-lookup"><span data-stu-id="e4965-124">**ScheduleJob** that uses jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="e4965-125">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="e4965-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e4965-126">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e4965-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="e4965-127">Node.js 0.12.x или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e4965-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="e4965-128">В статье [Prepare your development environment][lnk-dev-setup] (Подготовка среды разработки) описывается, как установить Node.js для работы с этим руководством в операционной системе Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="e4965-128">The article [Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="e4965-129">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e4965-129">An active Azure account.</span></span> <span data-ttu-id="e4965-130">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e4965-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="e4965-131">Планирование заданий для вызова прямого метода и обновления свойств двойника устройства</span><span class="sxs-lookup"><span data-stu-id="e4965-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="e4965-132">В этом разделе вы создадите консольное приложение .NET на языке C#, которое использует задания для вызова прямого метода **lockDoor** и для обновления свойств на нескольких устройствах.</span><span class="sxs-lookup"><span data-stu-id="e4965-132">In this section, you create a .NET console app (using C#) that uses jobs to call the **lockDoor** direct method and send desired property updates to multiple devices.</span></span>

1. <span data-ttu-id="e4965-133">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения** .</span><span class="sxs-lookup"><span data-stu-id="e4965-133">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="e4965-134">Назовите проект **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="e4965-134">Name the project **ScheduleJob**.</span></span>

    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]

1. <span data-ttu-id="e4965-136">В обозревателе решений щелкните правой кнопкой мыши проект **ScheduleJob** и выберите **Управление пакетами NuGet…**.</span><span class="sxs-lookup"><span data-stu-id="e4965-136">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="e4965-137">В окне **Диспетчер пакетов NuGet** нажмите кнопку **Обзор**, найдите **microsoft.azure.devices**, щелкните **Установить**, чтобы установить пакет **Microsoft.Azure.Devices**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="e4965-137">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="e4965-138">В результате выполняется скачивание и установка пакета NuGet [SDK для служб Интернета вещей Azure][lnk-nuget-service-sdk] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="e4965-138">This step downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="e4965-140">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="e4965-140">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="e4965-141">Добавьте следующую инструкцию `using`, если она отсутствует в инструкциях по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e4965-141">Add the following `using` statement if not already present in the default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="e4965-142">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="e4965-142">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="e4965-143">Замените значение заполнителя строкой подключения Центра Интернета вещей, созданного в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="e4965-143">Replace the placeholder with the IoT Hub connection string for the hub that you created in the previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="e4965-144">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="e4965-144">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="e4965-145">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="e4965-145">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="e4965-146">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="e4965-146">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="e4965-147">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="e4965-147">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER to run the next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER to exit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="e4965-148">В обозревателе решений откройте **Задать автозагружаемые проекты...** и задайте значение **Запустить** для параметра **Действие** проекта **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="e4965-148">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="e4965-149">Выполните сборку решения.</span><span class="sxs-lookup"><span data-stu-id="e4965-149">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e4965-150">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="e4965-150">Create a simulated device app</span></span>

<span data-ttu-id="e4965-151">В этом разделе вы создадите консольное приложение Node.js, которое отвечает на прямой метод, вызываемый из облака. Этот метод запускает перезагрузку имитации устройства и использует сообщаемые свойства для определения устройств и времени их последней перезагрузки в запросах двойников устройства.</span><span class="sxs-lookup"><span data-stu-id="e4965-151">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="e4965-152">Создайте пустую папку с именем **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="e4965-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="e4965-153">В папке **simDevice** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="e4965-153">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="e4965-154">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="e4965-154">Accept all the defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="e4965-155">Чтобы установить пакеты **azure-iot-device** и **azure-iot-device-mqtt**, в командной строке в папке **simDevice** выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e4965-155">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="e4965-156">В текстовом редакторе создайте файл **simDevice.js** в папке **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="e4965-156">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>

1. <span data-ttu-id="e4965-157">Добавьте следующие инструкции require в начало файла **simDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="e4965-157">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="e4965-158">Добавьте переменную **connectionString**, чтобы создать с ее помощью экземпляр **клиента**.</span><span class="sxs-lookup"><span data-stu-id="e4965-158">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="e4965-159">Замените заполнители значениями, подходящими для ваших настроек.</span><span class="sxs-lookup"><span data-stu-id="e4965-159">Make sure to replace the placeholders with values appropriate to your setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="e4965-160">Добавьте следующую функцию для обработки метода **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="e4965-160">Add the following function to handle the **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="e4965-161">Добавьте следующий код для регистрации обработчика для метода **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="e4965-161">Add the following code to register the handler for the **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="e4965-162">Сохраните и закройте файл **simDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="e4965-162">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="e4965-163">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="e4965-163">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e4965-164">В рабочем коде следует реализовать политики повторных попыток (например, с экспоненциальной задержкой), как указано в статье [Обработка временного сбоя][lnk-transient-faults] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="e4965-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="e4965-165">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="e4965-165">Run the apps</span></span>

<span data-ttu-id="e4965-166">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="e4965-166">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="e4965-167">В командной строке в папке **simDevice** выполните следующую команду, чтобы начать прослушивание прямого метода перезагрузки:</span><span class="sxs-lookup"><span data-stu-id="e4965-167">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="e4965-168">Запустите консольное приложение C# **ScheduleJob**. Щелкните правой кнопкой мыши проект **ScheduleJob**, выберите **Отладка** и **Запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="e4965-168">Run the C# console app **ScheduleJob** by right-clicking on the **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="e4965-169">Отобразятся выходные данные с устройства и серверных приложений.</span><span class="sxs-lookup"><span data-stu-id="e4965-169">You see the output from both device and back-end apps.</span></span>

    ![Выполнение приложений для планирования заданий][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="e4965-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4965-171">Next steps</span></span>

<span data-ttu-id="e4965-172">В этом учебнике описано использование задания для планирования прямого метода на устройстве и обновления свойств двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="e4965-172">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="e4965-173">Чтобы продолжить знакомство с Центром Интернета вещей и шаблонами управления устройствами, такими как удаленное обновление встроенного ПО, ознакомьтесь с [этим руководством][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="e4965-173">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="e4965-174">Чтобы продолжить знакомство с Центром Интернета вещей, см. сведения в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="e4965-174">To continue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

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
