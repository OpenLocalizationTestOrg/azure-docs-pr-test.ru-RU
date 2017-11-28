---
title: "aaaGet к работе с близнецы устройства Azure IoT Hub (.NET или узел) | Документы Microsoft"
description: "Как tooadd близнецы устройства Azure IoT Hub toouse теги и затем использовать запрос центр IoT. Использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement hello имитированное устройство приложения и hello служба Azure IoT SDK для .NET tooimplement приложение службы, которое добавляет теги hello и запускает hello центра IoT запроса."
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
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="cd68e-104">Начало работы с двойниками устройств (.NET или Node)</span><span class="sxs-lookup"><span data-stu-id="cd68e-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="cd68e-105">В конце этого учебника hello будет иметь .NET и Node.js консольного приложения:</span><span class="sxs-lookup"><span data-stu-id="cd68e-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="cd68e-106">**AddTagsAndQuery.sln** — это внутреннее приложение .NET, которое добавляет теги и выполняет запросы к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="cd68e-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="cd68e-107">**TwinSimulatedDevice.js**, приложение Node.js, которое имитирует устройство, соединяющее центра IoT tooyour с идентификатором hello устройства, созданного ранее и сообщает о условия его подключения.</span><span class="sxs-lookup"><span data-stu-id="cd68e-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="cd68e-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="cd68e-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="cd68e-109">toocomplete этого учебника требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="cd68e-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="cd68e-110">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cd68e-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="cd68e-111">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="cd68e-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="cd68e-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="cd68e-112">An active Azure account.</span></span> <span data-ttu-id="cd68e-113">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="cd68e-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="cd68e-114">Создание приложения hello службы</span><span class="sxs-lookup"><span data-stu-id="cd68e-114">Create hello service app</span></span>
<span data-ttu-id="cd68e-115">В этом разделе создайте .NET консольного приложения (с помощью C#), добавляет связанные с устройством двойных расположение метаданных toohello **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="cd68e-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="cd68e-116">Затем выполняется запрос близнецы hello устройства хранится в центр IoT hello, выбрав hello устройствах, находящихся в hello нам и Здравствуйте, те, о которых сообщает сотовой связи.</span><span class="sxs-lookup"><span data-stu-id="cd68e-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="cd68e-117">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="cd68e-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="cd68e-118">Имя проекта hello **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="cd68e-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. <span data-ttu-id="cd68e-120">В обозревателе решений щелкните правой кнопкой мыши hello **AddTagsAndQuery** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="cd68e-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="cd68e-121">В hello **диспетчера пакетов NuGet** выберите **Обзор** и выполните поиск **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="cd68e-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="cd68e-122">Выберите **установить** tooinstall hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="cd68e-123">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="cd68e-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="cd68e-125">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="cd68e-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="cd68e-126">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="cd68e-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="cd68e-127">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="cd68e-128">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="cd68e-128">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="cd68e-129">Hello **RegistryManager** класс предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="cd68e-130">Предыдущий код Hello сначала инициализирует hello **registryManager** объекта, а затем извлекает hello двойных устройства для **myDeviceId**и наконец обновляет сведения о расположении hello требуемого этим тегам.</span><span class="sxs-lookup"><span data-stu-id="cd68e-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="cd68e-131">После обновления, он выполняет два запроса: hello сначала выделяются hello близнецы устройств для устройств, расположенных в hello **Redmond43** здания, сооружения и hello второй уточняет hello запроса tooselect только hello устройства, подключенные через также сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="cd68e-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="cd68e-132">Обратите внимание, что предыдущего код hello, при создании hello **запроса** объекта, указывает максимальное количество возвращенных документов.</span><span class="sxs-lookup"><span data-stu-id="cd68e-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="cd68e-133">Hello **запроса** объект содержит **HasMoreResults** логического свойства, которые можно использовать tooinvoke hello **GetNextAsTwinAsync** методы все tooretrieve несколько раз результаты.</span><span class="sxs-lookup"><span data-stu-id="cd68e-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="cd68e-134">Метод **GetNextAsJson** доступен для результатов, которые не являются двойниками устройств, например результатов статистических запросов.</span><span class="sxs-lookup"><span data-stu-id="cd68e-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="cd68e-135">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="cd68e-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="cd68e-136">В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **AddTagsAndQuery** проект является **запустить**.</span><span class="sxs-lookup"><span data-stu-id="cd68e-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="cd68e-137">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-137">Build hello solution.</span></span>
1. <span data-ttu-id="cd68e-138">Запустить это приложение, щелкнув hello **AddTagsAndQuery** проекта и выбрав **отладки**, за которым следует **запустить новый экземпляр**.</span><span class="sxs-lookup"><span data-stu-id="cd68e-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="cd68e-139">Вы увидите одно устройство в результатах hello для hello запрос запросом для всех устройств, расположенных в **Redmond43** и для hello запрос, который ограничивает hello нет результатов toodevices используемой сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="cd68e-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![Результаты запроса в окне][img-addtagapp]

<span data-ttu-id="cd68e-141">В следующем разделе hello создается приложение устройства, которое сообщает сведения о подключении hello и изменения hello результат запроса hello в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="cd68e-142">Создание приложения hello устройства</span><span class="sxs-lookup"><span data-stu-id="cd68e-142">Create hello device app</span></span>
<span data-ttu-id="cd68e-143">В этом разделе создайте консольное приложение Node.js, которое подключается tooyour концентратора, **myDeviceId**и обновляет сведения о hello toocontain свойства отчета, он соединяется с использованием сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="cd68e-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="cd68e-144">Создайте пустую папку с именем **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="cd68e-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="cd68e-145">В hello **reportconnectivity** папки, создайте новый файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="cd68e-146">Примите все значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="cd68e-147">В командной строке в hello **reportconnectivity** папку, следующая команда tooinstall hello hello **azure iot устройства**, и **azure iot устройства mqtt** пакета :</span><span class="sxs-lookup"><span data-stu-id="cd68e-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="cd68e-148">В текстовом редакторе создайте новый **ReportConnectivity.js** файла в hello **reportconnectivity** папки.</span><span class="sxs-lookup"><span data-stu-id="cd68e-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="cd68e-149">Добавьте следующий код toohello hello **ReportConnectivity.js** файл и замените заполнитель hello для строки подключения устройства с hello один копируются при создании hello **myDeviceId** устройства удостоверение:</span><span class="sxs-lookup"><span data-stu-id="cd68e-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="cd68e-150">Hello **клиента** объект представляет все методы hello, требующих toointeract с близнецы устройства с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="cd68e-151">Здравствуйте предыдущего кода после инициализации hello **клиента** объекта извлекает hello двойных устройства для **myDeviceId** и обновляет сведения о подключении hello свойства отчета.</span><span class="sxs-lookup"><span data-stu-id="cd68e-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="cd68e-152">Выполните приложение hello устройства</span><span class="sxs-lookup"><span data-stu-id="cd68e-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="cd68e-153">Должно появиться сообщение hello `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="cd68e-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="cd68e-154">Теперь, когда hello устройство сообщило его сведения о соединении, он должен отображаться в обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="cd68e-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="cd68e-155">Запустите hello .NET **AddTagsAndQuery** hello toorun приложение запрашивает еще раз.</span><span class="sxs-lookup"><span data-stu-id="cd68e-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="cd68e-156">На этот раз **myDeviceId** должен появиться в результатах обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="cd68e-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="cd68e-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd68e-157">Next steps</span></span>
<span data-ttu-id="cd68e-158">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="cd68e-159">Добавить метаданные устройства как теги из серверной части приложения, а написал имитированное устройство приложения tooreport подключения сведений об устройстве в двойных hello устройства.</span><span class="sxs-lookup"><span data-stu-id="cd68e-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="cd68e-160">Вы также узнали, каким образом tooquery эти сведения, с помощью языка запросов SQL-подобного центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="cd68e-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="cd68e-161">Hello используйте следующие ресурсы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="cd68e-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="cd68e-162">Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника</span><span class="sxs-lookup"><span data-stu-id="cd68e-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="cd68e-163">Настройка устройств с нужными свойствами устройства двойных hello [используйте требуемого свойства устройства tooconfigure] [ lnk-twin-how-to-configure] учебника</span><span class="sxs-lookup"><span data-stu-id="cd68e-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="cd68e-164">Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения) с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="cd68e-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

