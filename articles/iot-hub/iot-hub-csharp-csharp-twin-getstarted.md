---
title: "aaaGet к работе с близнецы устройства Azure IoT Hub (.NET/.NET) | Документы Microsoft"
description: "Как tooadd близнецы устройства Azure IoT Hub toouse теги и затем использовать запрос центр IoT. Использовать устройства Azure IoT hello SDK для .NET tooimplement hello имитированное устройство и приложения hello служба Azure IoT SDK для .NET tooimplement приложение службы, которое добавляет теги hello и запускает hello центра IoT запроса."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="05bec-104">Начало работы с двойниками устройств (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="05bec-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="05bec-105">В конце этого учебника hello будет иметь следующие консольные приложения .NET:</span><span class="sxs-lookup"><span data-stu-id="05bec-105">At hello end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="05bec-106">**CreateDeviceIdentity**, приложение .NET, который создает удостоверения устройства и связанная с защитой ключа tooconnect приложение имитации устройства.</span><span class="sxs-lookup"><span data-stu-id="05bec-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="05bec-107">**AddTagsAndQuery** — внутреннее приложение .NET, которое добавляет теги и выполняет запросы к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="05bec-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="05bec-108">**ReportConnectivity**, приложение .NET устройства, которое имитирует устройство, соединяющее центра IoT tooyour с идентификатором hello устройства, созданного ранее и сообщает о условия его подключения.</span><span class="sxs-lookup"><span data-stu-id="05bec-108">**ReportConnectivity**, a .NET device app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="05bec-109">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="05bec-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="05bec-110">toocomplete этого учебника требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="05bec-110">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="05bec-111">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="05bec-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="05bec-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="05bec-112">An active Azure account.</span></span> <span data-ttu-id="05bec-113">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="05bec-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="05bec-114">Следует удостоверения устройства hello toocreate программно вместо чтения hello соответствующий раздел в hello [подключиться с помощью .NET концентратор IoT tooyour имитированное устройство] [ lnk-device-identity-csharp] статьи.</span><span class="sxs-lookup"><span data-stu-id="05bec-114">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="05bec-115">Создание приложения hello службы</span><span class="sxs-lookup"><span data-stu-id="05bec-115">Create hello service app</span></span>
<span data-ttu-id="05bec-116">В этом разделе создайте .NET консольного приложения (с помощью C#), добавляет связанные с устройством двойных расположение метаданных toohello **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="05bec-116">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="05bec-117">Затем выполняется запрос близнецы hello устройства хранится в центр IoT hello, выбрав hello устройствах, находящихся в hello нам и Здравствуйте, те, о которых сообщает сотовой связи.</span><span class="sxs-lookup"><span data-stu-id="05bec-117">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="05bec-118">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="05bec-118">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="05bec-119">Имя проекта hello **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="05bec-119">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. <span data-ttu-id="05bec-121">В обозревателе решений щелкните правой кнопкой мыши hello **AddTagsAndQuery** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="05bec-121">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="05bec-122">В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="05bec-122">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="05bec-123">Выберите **установить** tooinstall hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-123">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="05bec-124">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="05bec-124">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="05bec-126">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="05bec-126">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="05bec-127">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="05bec-127">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="05bec-128">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-128">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="05bec-129">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="05bec-129">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="05bec-130">Hello **RegistryManager** класс предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-130">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="05bec-131">Предыдущий код Hello сначала инициализирует hello **registryManager** объекта, а затем извлекает hello двойных устройства для **myDeviceId**и наконец обновляет сведения о расположении hello требуемого этим тегам.</span><span class="sxs-lookup"><span data-stu-id="05bec-131">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="05bec-132">После обновления, он выполняет два запроса: hello сначала выделяются hello близнецы устройств для устройств, расположенных в hello **Redmond43** здания, сооружения и hello второй уточняет hello запроса tooselect только hello устройства, подключенные через также сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="05bec-132">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="05bec-133">Обратите внимание, что предыдущего код hello, при создании hello **запроса** объекта, указывает максимальное количество возвращенных документов.</span><span class="sxs-lookup"><span data-stu-id="05bec-133">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="05bec-134">Hello **запроса** объект содержит **HasMoreResults** логического свойства, которые можно использовать tooinvoke hello **GetNextAsTwinAsync** методы все tooretrieve несколько раз результаты.</span><span class="sxs-lookup"><span data-stu-id="05bec-134">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="05bec-135">Метод **GetNextAsJson** доступен для результатов, которые не являются двойниками устройств, например результатов статистических запросов.</span><span class="sxs-lookup"><span data-stu-id="05bec-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="05bec-136">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="05bec-136">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="05bec-137">В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **AddTagsAndQuery** проект является **запустить**.</span><span class="sxs-lookup"><span data-stu-id="05bec-137">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="05bec-138">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-138">Build hello solution.</span></span>
1. <span data-ttu-id="05bec-139">Запустить это приложение, щелкнув hello **AddTagsAndQuery** проекта и выбрав **отладки**, за которым следует **запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="05bec-139">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="05bec-140">Вы увидите одно устройство в результатах hello для hello запрос запросом для всех устройств, расположенных в **Redmond43** и для hello запрос, который ограничивает hello нет результатов toodevices используемой сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="05bec-140">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Результаты запроса в окне][img-addtagapp]

<span data-ttu-id="05bec-142">В следующем разделе hello создается приложение устройства, которое сообщает сведения о подключении hello и изменения hello результат запроса hello в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-142">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="05bec-143">Создание приложения hello устройства</span><span class="sxs-lookup"><span data-stu-id="05bec-143">Create hello device app</span></span>
<span data-ttu-id="05bec-144">В этом разделе создайте консольное приложение .NET, которое подключается tooyour концентратора, **myDeviceId**и обновляет сведения о hello toocontain свойства отчета, он соединяется с использованием сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="05bec-144">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="05bec-145">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="05bec-145">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="05bec-146">Имя проекта hello **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="05bec-146">Name hello project **ReportConnectivity**.</span></span>
   
    ![Новое классическое приложение устройства Windows на языке Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="05bec-148">В обозревателе решений щелкните правой кнопкой мыши hello **ReportConnectivity** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="05bec-148">In Solution Explorer, right-click hello **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="05bec-149">В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="05bec-149">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="05bec-150">Выберите **установить** tooinstall hello **Microsoft.Azure.Devices.Client** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-150">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="05bec-151">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [устройств Azure IoT SDK] [ lnk-nuget-client-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="05bec-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Клиентское приложение в окне "Диспетчер пакетов NuGet"][img-clientnuget]
1. <span data-ttu-id="05bec-153">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="05bec-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="05bec-154">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="05bec-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="05bec-155">Замените значение заполнителя hello строкой подключения устройства hello, записанное в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-155">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="05bec-156">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="05bec-156">Add hello following method toohello **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="05bec-157">Hello **клиента** объект представляет все методы hello, требующих toointeract с близнецы устройства с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-157">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="05bec-158">Здравствуйте, приведенный выше код инициализирует hello **клиента** объекта, а затем извлекает hello устройства двойных для **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="05bec-158">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="05bec-159">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="05bec-159">Add hello following method toohello **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="05bec-160">Здравствуйте кода выше обновления **myDeviceId**сообщила свойство с данных о связности hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-160">hello code above updates **myDeviceId**'s reported property with hello connectivity information.</span></span>

1. <span data-ttu-id="05bec-161">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="05bec-161">Finally, add hello following lines toohello **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. <span data-ttu-id="05bec-162">В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **ReportConnectivity** проект является **запустить**.</span><span class="sxs-lookup"><span data-stu-id="05bec-162">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="05bec-163">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-163">Build hello solution.</span></span>
1. <span data-ttu-id="05bec-164">Запустить это приложение, щелкнув hello **ReportConnectivity** проекта и выбрав **отладки**, за которым следует **запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="05bec-164">Run this application by right-clicking on hello **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="05bec-165">Вы должны увидеть, получение сведений о двойных hello и последующей отправки подключения, как *сообщил свойство*.</span><span class="sxs-lookup"><span data-stu-id="05bec-165">You should see it getting hello twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Запустите подключения tooreport приложения для устройств][img-rundeviceapp]
    
    
1. <span data-ttu-id="05bec-167">Теперь, когда hello устройство сообщило его сведения о соединении, он должен отображаться в обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="05bec-167">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="05bec-168">Запустите hello .NET **AddTagsAndQuery** hello toorun приложение запрашивает еще раз.</span><span class="sxs-lookup"><span data-stu-id="05bec-168">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="05bec-169">На этот раз **myDeviceId** должен появиться в результатах обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="05bec-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Сведения о подключении устройства успешно переданы][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="05bec-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05bec-171">Next steps</span></span>
<span data-ttu-id="05bec-172">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-172">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="05bec-173">Добавить метаданные устройства как теги из серверной части приложения, а написал имитированное устройство приложения tooreport подключения сведений об устройстве в двойных hello устройства.</span><span class="sxs-lookup"><span data-stu-id="05bec-173">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="05bec-174">Вы также узнали, каким образом tooquery эти сведения, с помощью языка запросов SQL-подобного центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="05bec-174">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="05bec-175">Hello используйте следующие ресурсы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="05bec-175">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="05bec-176">Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника</span><span class="sxs-lookup"><span data-stu-id="05bec-176">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="05bec-177">Настройка устройств с нужными свойствами устройства двойных hello [используйте требуемого свойства устройства tooconfigure] [ lnk-twin-how-to-configure] учебника</span><span class="sxs-lookup"><span data-stu-id="05bec-177">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="05bec-178">Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения) с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="05bec-178">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

