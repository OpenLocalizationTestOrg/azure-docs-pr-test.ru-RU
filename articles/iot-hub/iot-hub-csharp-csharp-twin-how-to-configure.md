---
title: "свойства двойных устройства aaaUse центр IoT Azure (.NET/.NET) | Документы Microsoft"
description: "Как устройства Azure IoT Hub toouse близнецы tooconfigure устройств. Можно использовать устройства Azure IoT hello пакета SDK для .NET tooimplement приложения имитированное устройство и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое изменяет конфигурацию устройства, с помощью двойных устройства."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="bff75-104">Использовать нужными свойствами tooconfigure устройства</span><span class="sxs-lookup"><span data-stu-id="bff75-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="bff75-105">В конце этого учебника hello будет иметь два консольных приложений .NET:</span><span class="sxs-lookup"><span data-stu-id="bff75-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="bff75-106">**SimulateDeviceConfiguration**, приложение имитированное устройство, которое ожидает обновления требуемой конфигурацией и сообщает о состоянии hello имитацию конфигурации процесса обновления.</span><span class="sxs-lookup"><span data-stu-id="bff75-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="bff75-107">**SetDesiredConfigurationAndQuery**, серверная часть приложения, который устанавливает hello необходимой настройки на устройстве, и запросы hello процесс обновления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bff75-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="bff75-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="bff75-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="bff75-109">toocomplete этого учебника требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="bff75-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="bff75-110">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bff75-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="bff75-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="bff75-111">An active Azure account.</span></span> <span data-ttu-id="bff75-112">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="bff75-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="bff75-113">Если вы следовали hello [Приступая к работе с устройством близнецы] [ lnk-twin-tutorial] учебник, вы уже имеется центр IoT и вызывается удостоверение устройства **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="bff75-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="bff75-114">В этом случае можно пропустить toohello [имитированное устройство hello создать приложение] [ lnk-how-to-configure-createapp] раздела.</span><span class="sxs-lookup"><span data-stu-id="bff75-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="bff75-115">Создание приложения hello имитированное устройство</span><span class="sxs-lookup"><span data-stu-id="bff75-115">Create hello simulated device app</span></span>
<span data-ttu-id="bff75-116">В этом разделе создайте консольное приложение .NET, которое подключается tooyour концентратора, **myDeviceId**, ожидает обновления требуемой конфигурацией, а затем информирует о на процесс обновления конфигурации имитируемые hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="bff75-117">В Visual Studio, создайте новый проект Visual C# Windows классического с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="bff75-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="bff75-118">Имя проекта hello **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="bff75-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![Новое классическое приложение устройства Windows на языке Visual C#][img-createdeviceapp]

1. <span data-ttu-id="bff75-120">В обозревателе решений щелкните правой кнопкой мыши hello **SimulateDeviceConfiguration** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="bff75-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="bff75-121">В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="bff75-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="bff75-122">Выберите **установить** tooinstall hello **Microsoft.Azure.Devices.Client** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="bff75-123">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [устройств Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="bff75-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Клиентское приложение в окне "Диспетчер пакетов NuGet"][img-clientnuget]
1. <span data-ttu-id="bff75-125">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="bff75-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="bff75-126">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="bff75-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="bff75-127">Замените значение заполнителя hello строкой подключения устройства hello, записанное в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="bff75-128">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="bff75-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="bff75-129">Hello **клиента** объект представляет все методы hello, требующих toointeract с близнецы устройства с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="bff75-130">Здравствуйте, приведенный выше код инициализирует hello **клиента** объекта, а затем извлекает hello устройства двойных для **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="bff75-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="bff75-131">Добавьте следующий метод toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="bff75-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="bff75-132">Этот метод задает начальные значения hello телеметрии на локальном устройстве hello и затем обновления hello двойных устройства.</span><span class="sxs-lookup"><span data-stu-id="bff75-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="bff75-133">Добавьте следующий метод toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="bff75-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="bff75-134">Это обратный вызов, который обнаруживает изменения в *требуемого свойства* в двойных hello устройства.</span><span class="sxs-lookup"><span data-stu-id="bff75-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="bff75-135">Этот метод обновления hello сообщил свойства hello объекта двойных локального устройства с конфигурацией hello обновить запрос и задает состояние hello слишком**ожидающие**, а затем обновления hello двойных устройства в службе hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="bff75-136">После успешного обновления двойных устройства hello, изменение конфигурации hello завершается путем вызова метода hello `CompleteConfigChange` описано в следующей точке hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="bff75-137">Добавьте следующий метод toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="bff75-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="bff75-138">Этот метод имитирует сброса устройства, а затем обновления hello локальные свойства отчета, установка состояния hello слишком**успех** и удаляет hello **pendingConfig** элемента.</span><span class="sxs-lookup"><span data-stu-id="bff75-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="bff75-139">Затем он обновляет hello двойных устройства в службе hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-139">It then updates hello device twin on hello service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="bff75-140">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="bff75-140">Finally add hello following lines toohello **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="bff75-141">В этом руководстве не имитируется поведение при одновременном обновлении конфигураций.</span><span class="sxs-lookup"><span data-stu-id="bff75-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="bff75-142">Некоторые процессы обновления конфигурации могут быть изменения могут tooaccommodate целевой конфигурации, во время обновления hello, некоторые могут иметь tooqueue их, а некоторые может отклонить их с состоянием ошибки.</span><span class="sxs-lookup"><span data-stu-id="bff75-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="bff75-143">Убедитесь, что tooconsider hello желаемое поведение для определенной конфигурации процесса и добавьте соответствующую логику hello перед запуском hello изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bff75-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="bff75-144">Выполните построение решения hello и запустите приложение hello устройства из Visual Studio, нажав кнопку **F5**.</span><span class="sxs-lookup"><span data-stu-id="bff75-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="bff75-145">На консоли вывода hello вы увидите сообщений hello, указывающее, что имитированное устройство получение двойных hello устройства, Настройка телеметрии hello и ожидающих изменений нужного свойства.</span><span class="sxs-lookup"><span data-stu-id="bff75-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="bff75-146">Оставьте приложение hello под управлением.</span><span class="sxs-lookup"><span data-stu-id="bff75-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="bff75-147">Создание приложения hello службы</span><span class="sxs-lookup"><span data-stu-id="bff75-147">Create hello service app</span></span>
<span data-ttu-id="bff75-148">В этом разделе вы создадите консольное приложение .NET, hello обновления *требуемого свойства* на двойных hello устройства, связанные с **myDeviceId** новым объектом конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="bff75-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="bff75-149">Он запрашивает близнецы устройства hello, хранящихся в центр IoT hello и показывает разность hello hello требуемого и данные конфигурации устройства hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="bff75-150">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="bff75-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="bff75-151">Имя проекта hello **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="bff75-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. <span data-ttu-id="bff75-153">В обозревателе решений щелкните правой кнопкой мыши hello **SetDesiredConfigurationAndQuery** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="bff75-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="bff75-154">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="bff75-155">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="bff75-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="bff75-157">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="bff75-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="bff75-158">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="bff75-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="bff75-159">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="bff75-160">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="bff75-160">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            while (true)
            {
                var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                var results = await query.GetNextAsTwinAsync();
                foreach (var result in results)
                {
                    Console.WriteLine("Config report for: {0}", result.DeviceId);
                    Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine();
                }
                Thread.Sleep(10000);
            }
        }
   
    <span data-ttu-id="bff75-161">Hello **реестра** объект предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="bff75-162">Этот код инициализирует hello **реестра** объекта извлекает hello двойных устройства для **myDeviceId**и затем обновляет ее нужными свойствами нового объекта конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="bff75-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="bff75-163">После этого он запрашивает близнецы устройства hello, хранящихся в центр IoT hello каждые 10 секунд и печатает hello требуемого и данные телеметрии конфигураций.</span><span class="sxs-lookup"><span data-stu-id="bff75-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="bff75-164">См. toohello [язык запросов центра IoT] [ lnk-query] toolearn как toogenerate полнофункциональных отчетов на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="bff75-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="bff75-165">Это приложение выполняет запрос к Центру Интернета вещей каждые 10 секунд в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="bff75-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="bff75-166">Используйте запрашивает toogenerate пользовательские отчеты для многих устройств и не toodetect изменения.</span><span class="sxs-lookup"><span data-stu-id="bff75-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="bff75-167">Если вашему решению требуется отправка уведомлений о событиях устройства в реальном времени, используйте [уведомления двойников][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="bff75-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="bff75-168">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="bff75-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="bff75-169">В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **SetDesiredConfigurationAndQuery** проект является **запустить**.</span><span class="sxs-lookup"><span data-stu-id="bff75-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="bff75-170">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="bff75-170">Build hello solution.</span></span>
1. <span data-ttu-id="bff75-171">С **SimulateDeviceConfiguration** устройство под управлением приложения, приложение hello выполнения службы из Visual Studio с помощью **F5**.</span><span class="sxs-lookup"><span data-stu-id="bff75-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="bff75-172">Вы увидите изменение из указанной конфигурации hello **ожидающие** слишком**успех** новой активной hello отправки частоту 5 минут, а не 24 часа.</span><span class="sxs-lookup"><span data-stu-id="bff75-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Устройство успешно настроено][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="bff75-174">Нет задержки мин tooa между hello устройство работы и отчетов hello результата запроса.</span><span class="sxs-lookup"><span data-stu-id="bff75-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="bff75-175">Это toowork tooenable hello запроса инфраструктуры в очень широком масштабе.</span><span class="sxs-lookup"><span data-stu-id="bff75-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="bff75-176">использовать tooretrieve согласованного представления двойных одно устройство hello **getDeviceTwin** метод в hello **реестра** класса.</span><span class="sxs-lookup"><span data-stu-id="bff75-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="bff75-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bff75-177">Next steps</span></span>
<span data-ttu-id="bff75-178">В этом учебнике можно задавать нужные параметры как *требуемого свойства* из решения hello серверной части и написал toodetect приложения устройства, изменение и имитировать обновления многоступенчатый процесс, его через hello сообщил о состоянии свойства.</span><span class="sxs-lookup"><span data-stu-id="bff75-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="bff75-179">Hello используйте следующие ресурсы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="bff75-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="bff75-180">Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника</span><span class="sxs-lookup"><span data-stu-id="bff75-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="bff75-181">запланировать или выполнять операции с большими наборами устройств в разделе hello [расписание и широковещательных задания] [ lnk-schedule-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="bff75-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="bff75-182">Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения), с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="bff75-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
