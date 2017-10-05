---
title: "Начало работы с двойниками устройств Центра Интернета вещей Azure (.NET/.NET) | Документы Майкрософт"
description: "Добавление тегов и последующее использование запроса Центра Интернета вещей с помощью двойников устройств Центра Интернета вещей. Используйте пакет SDK для устройств Azure IoT для .NET, чтобы реализовать приложение имитации устройства, и пакет SDK для служб Azure IoT для .NET, чтобы реализовать приложение-службу, которое добавит теги и выполнит запрос к Центру Интернета вещей."
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
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="ab5de-104">Начало работы с двойниками устройств (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="ab5de-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="ab5de-105">Выполнив это руководство, вы создадите следующие консольные приложения .NET:</span><span class="sxs-lookup"><span data-stu-id="ab5de-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="ab5de-106">**CreateDeviceIdentity** — приложение .NET, создающее удостоверение устройства и соответствующий ключ безопасности для подключения к приложению виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="ab5de-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="ab5de-107">**AddTagsAndQuery** — внутреннее приложение .NET, которое добавляет теги и выполняет запросы к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="ab5de-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="ab5de-108">**ReportConnectivity** — приложение .NET, которое имитирует устройство, подключающееся к Центру Интернета вещей с использованием удостоверения устройства, созданного ранее, и передает условия его подключения.</span><span class="sxs-lookup"><span data-stu-id="ab5de-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="ab5de-109">Статья [IoT Hub SDKs][lnk-hub-sdks] (Пакеты SDK для Центра Интернета вещей) содержит сведения о разных пакетах SDK для Azure IoT, с помощью которых можно создать приложения для устройств и внутренние приложения.</span><span class="sxs-lookup"><span data-stu-id="ab5de-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="ab5de-110">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="ab5de-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="ab5de-111">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ab5de-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ab5de-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="ab5de-112">An active Azure account.</span></span> <span data-ttu-id="ab5de-113">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ab5de-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="ab5de-114">Если требуется создать удостоверение устройства программным способом, см. соответствующий подраздел в статье [Подключение виртуального устройства к Центру Интернета вещей с помощью .NET][lnk-device-identity-csharp].</span><span class="sxs-lookup"><span data-stu-id="ab5de-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="ab5de-115">Создание приложения службы</span><span class="sxs-lookup"><span data-stu-id="ab5de-115">Create the service app</span></span>
<span data-ttu-id="ab5de-116">В этом разделе рассказывается о том, как создать консольное приложение .NET (с помощью C#), которое добавляет метаданные расположения в двойник устройства, связанный с **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="ab5de-117">После этого оно запрашивает данные двойников устройств, хранящихся в Центре Интернета вещей, выбирает устройства, находящиеся в США, а затем те, которые сообщили о подключении по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="ab5de-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="ab5de-118">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения** .</span><span class="sxs-lookup"><span data-stu-id="ab5de-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="ab5de-119">Назовите проект **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. <span data-ttu-id="ab5de-121">В обозревателе решений щелкните правой кнопкой мыши проект **AddTagsAndQuery**, а затем **Управление пакетами Nuget...**</span><span class="sxs-lookup"><span data-stu-id="ab5de-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="ab5de-122">В окне **Диспетчер пакетов NuGet** выберите **Обзор** и найдите **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="ab5de-123">Выберите **Установить**, чтобы установить пакет **Microsoft.Azure.Devices**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="ab5de-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="ab5de-124">В результате выполняется скачивание и установка пакета NuGet [SDK для служб Интернета вещей Azure][lnk-nuget-service-sdk] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="ab5de-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="ab5de-126">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="ab5de-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="ab5de-127">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="ab5de-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="ab5de-128">Замените значение заполнителя строкой подключения к Центру Интернета вещей, созданному в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="ab5de-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="ab5de-129">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="ab5de-129">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="ab5de-130">Класс **RegistryManager** предоставляет все методы, необходимые для взаимодействия с двойниками устройства из службы.</span><span class="sxs-lookup"><span data-stu-id="ab5de-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="ab5de-131">Предыдущий код сначала инициализирует объект **RegistryManager**, затем извлекает двойник устройства для **MyDeviceId** и обновляет его теги, используя сведения о требуемом расположении.</span><span class="sxs-lookup"><span data-stu-id="ab5de-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="ab5de-132">После обновления он выполняет два запроса: первый выбирает только двойники устройств, расположенные на фабрике **Redmond43**, а второй уточняет условия первого запроса и выбирает устройства, подключенные по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="ab5de-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="ab5de-133">Обратите внимание, что при создании объекта **query** предыдущий код указывает максимальное количество возвращаемых документов.</span><span class="sxs-lookup"><span data-stu-id="ab5de-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="ab5de-134">Объект **Query** содержит логическое свойство **HasMoreResults**, которое можно использовать для вызова методов **GetNextAsTwinAsync** несколько раз, чтобы получить все результаты.</span><span class="sxs-lookup"><span data-stu-id="ab5de-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="ab5de-135">Метод **GetNextAsJson** доступен для результатов, которые не являются двойниками устройств, например результатов статистических запросов.</span><span class="sxs-lookup"><span data-stu-id="ab5de-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="ab5de-136">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="ab5de-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="ab5de-137">В обозревателе решений выберите **Задать автозагружаемые проекты...** и убедитесь, что для параметра **Действие** проекта **AddTagsAndQuery** задано значение **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="ab5de-138">Выполните сборку решения.</span><span class="sxs-lookup"><span data-stu-id="ab5de-138">Build the solution.</span></span>
1. <span data-ttu-id="ab5de-139">Запустите это приложение, щелкнув правой кнопкой мыши проект **AddTagsAndQuery** и выбрав **Отладка**, а затем — **Запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="ab5de-140">В результатах запроса на все устройства, расположенные на фабрике **Redmond43**, отобразится одно устройство, а для запроса на ограничение результатов устройствами, использующими сеть мобильной связи, не отобразится ни одного устройства.</span><span class="sxs-lookup"><span data-stu-id="ab5de-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Результаты запроса в окне][img-addtagapp]

<span data-ttu-id="ab5de-142">В следующем разделе рассказывается о том, как создать приложение устройства, которое сообщает сведения о подключении и изменяет результат запроса, описанного в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="ab5de-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="ab5de-143">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="ab5de-143">Create the device app</span></span>
<span data-ttu-id="ab5de-144">В этом разделе вы создадите консольное приложение .NET, которое подключается к центру как **myDeviceId** и обновляет передаваемые свойства, добавив в них сведения о подключении по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="ab5de-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="ab5de-145">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения** .</span><span class="sxs-lookup"><span data-stu-id="ab5de-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="ab5de-146">Назовите проект **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-146">Name the project **ReportConnectivity**.</span></span>
   
    ![Новое классическое приложение устройства Windows на языке Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="ab5de-148">В обозревателе решений щелкните правой кнопкой мыши проект **ReportConnectivity**, а затем **Управление пакетами NuGet...**</span><span class="sxs-lookup"><span data-stu-id="ab5de-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="ab5de-149">В окне **Диспетчер пакетов NuGet** выберите **Обзор** и найдите **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="ab5de-150">Выберите **Установить**, чтобы установить пакет **Microsoft.Azure.Devices.Client**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="ab5de-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="ab5de-151">В результате выполняется скачивание и установка [пакета NuGet SDK для устройств Azure IoT][lnk-nuget-client-sdk] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="ab5de-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Клиентское приложение в окне "Диспетчер пакетов NuGet"][img-clientnuget]
1. <span data-ttu-id="ab5de-153">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="ab5de-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="ab5de-154">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="ab5de-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="ab5de-155">Замените значение заполнителя строкой подключения устройства, записанной в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="ab5de-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="ab5de-156">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="ab5de-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
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

    <span data-ttu-id="ab5de-157">Объект **Client** позволяет получить все методы, необходимые для взаимодействия с двойниками устройства с устройства.</span><span class="sxs-lookup"><span data-stu-id="ab5de-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="ab5de-158">Приведенный выше код инициализирует объект **Client**, а затем получает двойник устройства для **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="ab5de-159">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="ab5de-159">Add the following method to the **Program** class:</span></span>
   
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

   <span data-ttu-id="ab5de-160">Вышеприведенный код изменяет передаваемое свойство **myDeviceId** с помощью сведений о подключении.</span><span class="sxs-lookup"><span data-stu-id="ab5de-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="ab5de-161">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="ab5de-161">Finally, add the following lines to the **Main** method:</span></span>
   
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
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="ab5de-162">В обозревателе решений выберите **Задать автозагружаемые проекты...** и убедитесь, что для параметра **Действие** проекта **ReportConnectivity** задано значение **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="ab5de-163">Выполните сборку решения.</span><span class="sxs-lookup"><span data-stu-id="ab5de-163">Build the solution.</span></span>
1. <span data-ttu-id="ab5de-164">Запустите это приложение, щелкнув правой кнопкой мыши проект **ReportConnectivity** и выбрав **Отладка**, а затем — **Запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="ab5de-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="ab5de-165">Программа получит сведения о двойнике, а затем отправит данные подключения как *переданное свойство*.</span><span class="sxs-lookup"><span data-stu-id="ab5de-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Запуск приложения устройства для передачи данных подключения][img-rundeviceapp]
    
    
1. <span data-ttu-id="ab5de-167">Теперь, когда устройство сообщило сведения о подключении, оно должно появиться в обоих запросах.</span><span class="sxs-lookup"><span data-stu-id="ab5de-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="ab5de-168">Запустите приложение .NET **AddTagsAndQuery**, чтобы возобновить выполнение запросов.</span><span class="sxs-lookup"><span data-stu-id="ab5de-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="ab5de-169">На этот раз **myDeviceId** должен появиться в результатах обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="ab5de-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Сведения о подключении устройства успешно переданы][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="ab5de-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab5de-171">Next steps</span></span>
<span data-ttu-id="ab5de-172">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ab5de-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="ab5de-173">Вы добавили метаданные устройства в качестве тегов из внутреннего приложения и написали код приложения имитации устройства, чтобы сообщить сведения о подключении в двойнике устройства.</span><span class="sxs-lookup"><span data-stu-id="ab5de-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="ab5de-174">Вы также узнали, как запрашивать эти сведения, используя похожий на SQL язык запросов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ab5de-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="ab5de-175">Ознакомьтесь со следующими материалами, чтобы узнать как:</span><span class="sxs-lookup"><span data-stu-id="ab5de-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="ab5de-176">отправить данные телеметрии с устройств (учебник [Приступая к работе с Центром Интернета вещей Azure (Node)][lnk-iothub-getstarted]);</span><span class="sxs-lookup"><span data-stu-id="ab5de-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="ab5de-177">настроить устройства с помощью требуемых свойств двойника устройства (руководство по [настройке устройств с помощью требуемых устройств][lnk-twin-how-to-configure]);</span><span class="sxs-lookup"><span data-stu-id="ab5de-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="ab5de-178">управлять устройствами в интерактивном режиме, например включить вентилятор из управляемого пользователем приложения (руководство по [использованию прямых методов][lnk-methods-tutorial]).</span><span class="sxs-lookup"><span data-stu-id="ab5de-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

