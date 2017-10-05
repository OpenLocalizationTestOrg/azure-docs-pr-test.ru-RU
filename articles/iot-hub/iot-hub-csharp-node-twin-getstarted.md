---
title: "Начало работы с двойниками устройств Центра Интернета вещей Azure (.NET или Node) | Документация Майкрософт"
description: "Добавление тегов и последующее использование запроса Центра Интернета вещей с помощью двойников устройств Центра Интернета вещей. Используйте пакет SDK для устройств Azure IoT для Node.js, чтобы реализовать приложение имитации устройства, и пакет SDK для служб Azure IoT для .NET, чтобы реализовать приложение-службу, которое добавит теги и выполнит запрос к Центру Интернета вещей."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 07797b9159c9b926e9eb47d8864c63048951931a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="3b887-104">Начало работы с двойниками устройств (.NET или Node)</span><span class="sxs-lookup"><span data-stu-id="3b887-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="3b887-105">По завершении работы с этим руководством у вас будет два консольных приложения — для .NET и Node.js:</span><span class="sxs-lookup"><span data-stu-id="3b887-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="3b887-106">**AddTagsAndQuery.sln** — это внутреннее приложение .NET, которое добавляет теги и выполняет запросы к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="3b887-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="3b887-107">**TwinSimulatedDevice.js** — это приложение Node.js, которое имитирует устройство, подключающееся к Центру Интернета вещей с использованием удостоверения устройства, созданного ранее, и сообщает о его условии подключения.</span><span class="sxs-lookup"><span data-stu-id="3b887-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="3b887-108">Статья [IoT Hub SDKs][lnk-hub-sdks] (Пакеты SDK для Центра Интернета вещей) содержит сведения о разных пакетах SDK для Azure IoT, с помощью которых можно создать приложения для устройств и внутренние приложения.</span><span class="sxs-lookup"><span data-stu-id="3b887-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="3b887-109">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="3b887-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="3b887-110">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3b887-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3b887-111">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="3b887-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="3b887-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="3b887-112">An active Azure account.</span></span> <span data-ttu-id="3b887-113">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="3b887-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="3b887-114">Создание приложения службы</span><span class="sxs-lookup"><span data-stu-id="3b887-114">Create the service app</span></span>
<span data-ttu-id="3b887-115">В этом разделе рассказывается о том, как создать консольное приложение .NET (с помощью C#), которое добавляет метаданные расположения в двойник устройства, связанный с **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3b887-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="3b887-116">После этого оно запрашивает данные двойников устройств, хранящихся в Центре Интернета вещей, выбирает устройства, находящиеся в США, а затем те, которые сообщили о подключении по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="3b887-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="3b887-117">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения** .</span><span class="sxs-lookup"><span data-stu-id="3b887-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="3b887-118">Назовите проект **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="3b887-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. <span data-ttu-id="3b887-120">В обозревателе решений щелкните правой кнопкой мыши проект **AddTagsAndQuery**, а затем **Управление пакетами Nuget...**</span><span class="sxs-lookup"><span data-stu-id="3b887-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3b887-121">В окне **Диспетчер пакетов NuGet** выберите **Обзор** и найдите **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="3b887-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="3b887-122">Выберите **Установить**, чтобы установить пакет **Microsoft.Azure.Devices**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="3b887-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="3b887-123">В результате выполняется скачивание и установка пакета NuGet [SDK для служб Интернета вещей Azure][lnk-nuget-service-sdk] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="3b887-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="3b887-125">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="3b887-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="3b887-126">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="3b887-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="3b887-127">Замените значение заполнителя строкой подключения к Центру Интернета вещей, созданному в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="3b887-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="3b887-128">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="3b887-128">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="3b887-129">Класс **RegistryManager** предоставляет все методы, необходимые для взаимодействия с двойниками устройства из службы.</span><span class="sxs-lookup"><span data-stu-id="3b887-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="3b887-130">Предыдущий код сначала инициализирует объект **RegistryManager**, затем извлекает двойник устройства для **MyDeviceId** и обновляет его теги, используя сведения о требуемом расположении.</span><span class="sxs-lookup"><span data-stu-id="3b887-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="3b887-131">После обновления он выполняет два запроса: первый выбирает только двойники устройств, расположенные на фабрике **Redmond43**, а второй уточняет условия первого запроса и выбирает устройства, подключенные по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="3b887-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="3b887-132">Обратите внимание, что при создании объекта **query** предыдущий код указывает максимальное количество возвращаемых документов.</span><span class="sxs-lookup"><span data-stu-id="3b887-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="3b887-133">Объект **Query** содержит логическое свойство **HasMoreResults**, которое можно использовать для вызова методов **GetNextAsTwinAsync** несколько раз, чтобы получить все результаты.</span><span class="sxs-lookup"><span data-stu-id="3b887-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="3b887-134">Метод **GetNextAsJson** доступен для результатов, которые не являются двойниками устройств, например результатов статистических запросов.</span><span class="sxs-lookup"><span data-stu-id="3b887-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="3b887-135">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="3b887-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="3b887-136">В обозревателе решений выберите **Задать автозагружаемые проекты...** и убедитесь, что для параметра **Действие** проекта **AddTagsAndQuery** задано значение **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="3b887-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="3b887-137">Выполните сборку решения.</span><span class="sxs-lookup"><span data-stu-id="3b887-137">Build the solution.</span></span>
1. <span data-ttu-id="3b887-138">Запустите это приложение, щелкнув правой кнопкой мыши проект **AddTagsAndQuery** и выбрав **Отладка**, а затем — **Запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="3b887-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="3b887-139">В результатах запроса на все устройства, расположенные на фабрике **Redmond43**, отобразится одно устройство, а для запроса на ограничение результатов устройствами, использующими сеть мобильной связи, не отобразится ни одного устройства.</span><span class="sxs-lookup"><span data-stu-id="3b887-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![Результаты запроса в окне][img-addtagapp]

<span data-ttu-id="3b887-141">В следующем разделе рассказывается о том, как создать приложение устройства, которое сообщает сведения о подключении и изменяет результат запроса, описанного в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="3b887-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="3b887-142">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="3b887-142">Create the device app</span></span>
<span data-ttu-id="3b887-143">В этом разделе вы создадите консольное приложение Node.js, которое подключается к центру как **myDeviceId** и обновляет сообщаемые свойства, добавив в них сведения о подключении по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="3b887-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="3b887-144">Создайте пустую папку с именем **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="3b887-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="3b887-145">В папке **reportconnectivity** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="3b887-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="3b887-146">Примите все значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3b887-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="3b887-147">В командной строке в папке **reportconnectivity** выполните следующую команду, чтобы установить пакет SDK для устройств **azure-iot-device** и пакет **azure-iot-device-mqtt**.</span><span class="sxs-lookup"><span data-stu-id="3b887-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="3b887-148">В текстовом редакторе создайте файл **ReportConnectivity.js** в папке **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="3b887-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="3b887-149">Добавьте следующий код в файл **ReportConnectivity.js** и замените заполнитель для строки подключения устройства на строку, скопированную при создании удостоверения устройства **myDeviceId**:</span><span class="sxs-lookup"><span data-stu-id="3b887-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="3b887-150">Объект **Client** позволяет получить все методы, необходимые для взаимодействия с двойниками устройства с устройства.</span><span class="sxs-lookup"><span data-stu-id="3b887-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="3b887-151">После инициализации объекта **Client** предыдущий код извлекает двойник устройства для **myDeviceId** и обновляет его сообщаемое свойство, используя сведения о подключении.</span><span class="sxs-lookup"><span data-stu-id="3b887-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="3b887-152">Запуск приложения устройства</span><span class="sxs-lookup"><span data-stu-id="3b887-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="3b887-153">Отобразится сообщение `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="3b887-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="3b887-154">Теперь, когда устройство сообщило сведения о подключении, оно должно появиться в обоих запросах.</span><span class="sxs-lookup"><span data-stu-id="3b887-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="3b887-155">Запустите приложение .NET **AddTagsAndQuery**, чтобы возобновить выполнение запросов.</span><span class="sxs-lookup"><span data-stu-id="3b887-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="3b887-156">На этот раз **myDeviceId** должен появиться в результатах обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="3b887-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="3b887-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b887-157">Next steps</span></span>
<span data-ttu-id="3b887-158">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="3b887-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="3b887-159">Вы добавили метаданные устройства в качестве тегов из внутреннего приложения и написали код приложения имитации устройства, чтобы сообщить сведения о подключении в двойнике устройства.</span><span class="sxs-lookup"><span data-stu-id="3b887-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="3b887-160">Вы также узнали, как запрашивать эти сведения, используя похожий на SQL язык запросов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="3b887-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="3b887-161">Ознакомьтесь со следующими материалами, чтобы узнать как:</span><span class="sxs-lookup"><span data-stu-id="3b887-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="3b887-162">отправить данные телеметрии с устройств (учебник [Приступая к работе с Центром Интернета вещей Azure (Node)][lnk-iothub-getstarted]);</span><span class="sxs-lookup"><span data-stu-id="3b887-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="3b887-163">настроить устройства с помощью требуемых свойств двойника устройства (руководство по [настройке устройств с помощью требуемых устройств][lnk-twin-how-to-configure]);</span><span class="sxs-lookup"><span data-stu-id="3b887-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="3b887-164">управлять устройствами в интерактивном режиме, например включить вентилятор из управляемого пользователем приложения (руководство по [использованию прямых методов][lnk-methods-tutorial]).</span><span class="sxs-lookup"><span data-stu-id="3b887-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

