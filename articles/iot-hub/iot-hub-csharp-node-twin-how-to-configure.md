---
title: "Использование двойников устройств Центра Интернета вещей (.NET или Node) | Документация Майкрософт"
description: "Настройка устройств с помощью двойников устройств Центра Интернета вещей Azure. Используйте пакет SDK для устройств Azure IoT для Node.js, чтобы реализовать приложение имитации устройства, и пакет SDK для служб Azure IoT для .NET, чтобы реализовать приложение-службу, которое изменит конфигурацию устройства с помощью двойника устройства."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 78b4523fa7d0c056f84214429730a5df1bcdcef7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="53c28-104">Настройка устройств с помощью требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="53c28-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="53c28-105">По завершении работы с этим руководством у вас будет два консольных приложения:</span><span class="sxs-lookup"><span data-stu-id="53c28-105">At the end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="53c28-106">**SimulateDeviceConfiguration.js** — это приложение имитации устройства, которое ожидает обновления требуемой конфигурации и сообщает о состоянии обновления имитации конфигурации.</span><span class="sxs-lookup"><span data-stu-id="53c28-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="53c28-107">**SetDesiredConfigurationAndQuery** — это внутреннее приложение .NET, которое задает требуемую конфигурацию на устройстве и выполняет запрос к процессу обновления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="53c28-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="53c28-108">Статья [IoT Hub SDKs][lnk-hub-sdks] (Пакеты SDK для Центра Интернета вещей) содержит сведения о разных пакетах SDK для Azure IoT, с помощью которых можно создать приложения для устройств и внутренние приложения.</span><span class="sxs-lookup"><span data-stu-id="53c28-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="53c28-109">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="53c28-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="53c28-110">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="53c28-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="53c28-111">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="53c28-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="53c28-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="53c28-112">An active Azure account.</span></span> <span data-ttu-id="53c28-113">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="53c28-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="53c28-114">Если вы выполнили указания руководства [Начало работы с двойниками устройств][lnk-twin-tutorial], то у вас уже есть Центр Интернета вещей и удостоверение устройства **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="53c28-114">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="53c28-115">В этом случае можно перейти к разделу [Создание приложения имитации устройства][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="53c28-115">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="53c28-116">Создание приложения имитации устройства</span><span class="sxs-lookup"><span data-stu-id="53c28-116">Create the simulated device app</span></span>
<span data-ttu-id="53c28-117">В этом разделе вы создаете консольное приложение Node.js, которое подключается к центру как **myDeviceId**, ожидает обновления требуемой конфигурации и сообщает об обновлениях в ходе обновления имитации конфигурации.</span><span class="sxs-lookup"><span data-stu-id="53c28-117">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="53c28-118">Создайте пустую папку с именем **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="53c28-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="53c28-119">В папке **simulatedeviceconfiguration** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="53c28-119">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="53c28-120">Примите все значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="53c28-120">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="53c28-121">В командной строке в папке **simulatedeviceconfiguration** выполните следующую команду, чтобы установить пакеты **azure-iot-device** и **azure-iot-device-mqtt**.</span><span class="sxs-lookup"><span data-stu-id="53c28-121">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="53c28-122">В текстовом редакторе создайте файл **SimulateDeviceConfiguration.js** в папке **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="53c28-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="53c28-123">Добавьте следующий код в файл **SimulateDeviceConfiguration.js** и замените заполнитель **{device connection string}** строкой подключения устройства, скопированной при создании удостоверения устройства **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="53c28-123">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="53c28-124">Объект **Client** позволяет получить все методы, необходимые для взаимодействия с двойниками устройства с устройства.</span><span class="sxs-lookup"><span data-stu-id="53c28-124">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="53c28-125">Этот код инициализирует объект **Client**, извлекает двойник устройства для **myDeviceId**, а затем подключает обработчик для обновления *требуемых свойств*.</span><span class="sxs-lookup"><span data-stu-id="53c28-125">This code initializes the **Client** object, retrieves the device twin for **myDeviceId**, and then attaches a handler for the update on *desired properties*.</span></span> <span data-ttu-id="53c28-126">Обработчик проверяет, отправлен ли запрос на изменение конфигурации. Для этого он сравнивает идентификаторы конфигураций, а затем вызывает метод, который запускает изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="53c28-126">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="53c28-127">Обратите внимание, что для простоты в этом коде используется жестко заданное значение по умолчанию для выполнения начальной настройки.</span><span class="sxs-lookup"><span data-stu-id="53c28-127">Note that for the sake of simplicity, this code uses a hard-coded default for the initial configuration.</span></span> <span data-ttu-id="53c28-128">Настоящее приложение, вероятно, скачало бы эту конфигурацию из локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="53c28-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="53c28-129">События изменения требуемых свойств всегда инициируются единожды при подключении устройства.</span><span class="sxs-lookup"><span data-stu-id="53c28-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="53c28-130">Прежде чем что-либо делать, обязательно убедитесь, что требуемые свойства действительно изменились.</span><span class="sxs-lookup"><span data-stu-id="53c28-130">Make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="53c28-131">Добавьте следующие методы перед осуществлением вызова `client.open()`:</span><span class="sxs-lookup"><span data-stu-id="53c28-131">Add the following methods before the `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="53c28-132">Метод **initConfigChange** обновляет сообщаемые свойства в объекте локального двойника устройства с помощью запроса на обновление конфигурации и устанавливает для состояния значение **Pending** (Ожидание), а затем обновляет двойник устройства в службе.</span><span class="sxs-lookup"><span data-stu-id="53c28-132">The **initConfigChange** method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="53c28-133">После успешного обновления двойника устройства он имитирует длительный процесс, который завершается выполнением **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="53c28-133">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="53c28-134">Этот метод обновляет сообщаемые локальные свойства, установив для состояния значение **Success** и удалив объект **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="53c28-134">This method updates the local reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="53c28-135">Затем он обновляет двойник устройства в службе.</span><span class="sxs-lookup"><span data-stu-id="53c28-135">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="53c28-136">Обратите внимание, что для сокращения нагрузки на полосу пропускания при обновлении сообщаемых свойств указываются только свойства, которые нужно изменить (**patch** в коде выше), а не заменяется весь документ.</span><span class="sxs-lookup"><span data-stu-id="53c28-136">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="53c28-137">В этом руководстве не имитируется поведение при одновременном обновлении конфигураций.</span><span class="sxs-lookup"><span data-stu-id="53c28-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="53c28-138">В некоторых случаях обновление конфигурации может пройти в соответствии с изменениями целевой конфигурации, в других может потребоваться поместить изменения в очередь, а в остальных они могут быть отклонены с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="53c28-138">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="53c28-139">Следует учитывать желаемое поведение для конкретной конфигурации и добавить соответствующую логику перед ее изменением.</span><span class="sxs-lookup"><span data-stu-id="53c28-139">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="53c28-140">Запустите приложение устройства:</span><span class="sxs-lookup"><span data-stu-id="53c28-140">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="53c28-141">Отобразится сообщение `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="53c28-141">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="53c28-142">Не отключайте приложение.</span><span class="sxs-lookup"><span data-stu-id="53c28-142">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="53c28-143">Создание приложения службы</span><span class="sxs-lookup"><span data-stu-id="53c28-143">Create the service app</span></span>
<span data-ttu-id="53c28-144">В этом разделе вы создадите консольное приложение .NET, которое обновляет *требуемые свойства* двойника устройства, связанного с **myDeviceId**, с использованием нового объекта конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="53c28-144">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="53c28-145">Затем оно выполняет запрос к двойникам устройств, которые хранятся в Центре Интернета вещей, и показывает разницу между требуемой и сообщаемой конфигурацией устройства.</span><span class="sxs-lookup"><span data-stu-id="53c28-145">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="53c28-146">В Visual Studio добавьте в текущее решение проект классического приложения Windows на языке Visual C# с помощью шаблона проекта **консольного приложения** .</span><span class="sxs-lookup"><span data-stu-id="53c28-146">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="53c28-147">Назовите проект **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="53c28-147">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. <span data-ttu-id="53c28-149">В обозревателе решений щелкните правой кнопкой мыши проект **SetDesiredConfigurationAndQuery** и выберите **Управление пакетами Nuget...**</span><span class="sxs-lookup"><span data-stu-id="53c28-149">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="53c28-150">В окне **Диспетчер пакетов NuGet** нажмите кнопку **Обзор**, найдите **microsoft.azure.devices**, щелкните **Установить**, чтобы установить пакет **Microsoft.Azure.Devices**, и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="53c28-150">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="53c28-151">В результате выполняется скачивание и установка пакета NuGet [SDK для служб Интернета вещей Azure][lnk-nuget-service-sdk] и его зависимостей, а также добавляется соответствующая ссылка.</span><span class="sxs-lookup"><span data-stu-id="53c28-151">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="53c28-153">Добавьте следующие инструкции `using` в начало файла **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="53c28-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="53c28-154">Добавьте следующие поля в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="53c28-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="53c28-155">Замените значение заполнителя строкой подключения к Центру Интернета вещей, созданному в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="53c28-155">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="53c28-156">Добавьте следующий метод в класс **Program** .</span><span class="sxs-lookup"><span data-stu-id="53c28-156">Add the following method to the **Program** class:</span></span>
   
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
   
            try
            {
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
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="53c28-157">Объект **Registry** позволяет получить все методы, необходимые для взаимодействия с двойниками устройства из службы.</span><span class="sxs-lookup"><span data-stu-id="53c28-157">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="53c28-158">Этот код инициализирует объект **Registry**, извлекает двойник устройства для **myDeviceId**, а затем обновляет его требуемые свойства, используя новый объект конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="53c28-158">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="53c28-159">Затем он каждые 10 секунд запрашивает данные двойников устройств, которые хранятся в Центре Интернета вещей, и выводит требуемые и сообщаемые конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="53c28-159">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="53c28-160">Чтобы узнать, как создавать эффективные отчеты на всех устройствах, см. статью [Справочник по языку запросов для двойников и заданий][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="53c28-160">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="53c28-161">Это приложение выполняет запрос к Центру Интернета вещей каждые 10 секунд в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="53c28-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="53c28-162">Используйте запросы для создания представляемых пользователям отчетов на многих устройствах, а не для обнаружения изменений.</span><span class="sxs-lookup"><span data-stu-id="53c28-162">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="53c28-163">Если вашему решению требуется отправка уведомлений о событиях устройства в реальном времени, используйте [уведомления двойников][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="53c28-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="53c28-164">Наконец, добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="53c28-164">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="53c28-165">В обозревателе решений выберите **Задать автозагружаемые проекты...** и убедитесь, что для параметра **Действие** проекта **SetDesiredConfigurationAndQuery** задано значение **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="53c28-165">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="53c28-166">Выполните сборку решения.</span><span class="sxs-lookup"><span data-stu-id="53c28-166">Build the solution.</span></span>
1. <span data-ttu-id="53c28-167">Во время выполнения **SimulateDeviceConfiguration.js** запустите приложение .NET из Visual Studio, нажав клавишу **F5**. Состояние сообщаемой конфигурации изменится с **Успешно** на **В ожидании** и снова на **Успешно**, а значение активной частоты отправки изменится с 24 часов на 5 минут.</span><span class="sxs-lookup"><span data-stu-id="53c28-167">With **SimulateDeviceConfiguration.js** running, run the .NET application from Visual Studio using **F5** and you should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Устройство успешно настроено][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="53c28-169">Результаты запроса выводятся после операции сообщения устройства с задержкой (не более минуты).</span><span class="sxs-lookup"><span data-stu-id="53c28-169">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="53c28-170">Таким образом обеспечивается работа инфраструктуры запросов в очень широком масштабе.</span><span class="sxs-lookup"><span data-stu-id="53c28-170">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="53c28-171">Для получения согласованных представлений одного двойника устройства используйте метод **getDeviceTwin** в классе **Registry**.</span><span class="sxs-lookup"><span data-stu-id="53c28-171">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="53c28-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53c28-172">Next steps</span></span>
<span data-ttu-id="53c28-173">В этом руководстве вы установили требуемую конфигурацию в качестве *требуемых свойств* из серверной части решения и написали код приложения для устройства, которое обнаруживает изменения и имитирует многоэтапный процесс обновления, о состоянии которого сообщается в качестве сообщаемых свойств.</span><span class="sxs-lookup"><span data-stu-id="53c28-173">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="53c28-174">Ознакомьтесь со следующими материалами, чтобы узнать как:</span><span class="sxs-lookup"><span data-stu-id="53c28-174">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="53c28-175">отправить данные телеметрии с устройств (учебник [Приступая к работе с Центром Интернета вещей Azure (Node)][lnk-iothub-getstarted]);</span><span class="sxs-lookup"><span data-stu-id="53c28-175">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="53c28-176">запланировать или выполнить операции на больших наборах устройств (см. учебник [Планирование и трансляция заданий][lnk-schedule-jobs];</span><span class="sxs-lookup"><span data-stu-id="53c28-176">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="53c28-177">управлять устройствами в интерактивном режиме, например включить вентилятор из управляемого пользователем приложения (учебник [Use direct methods][lnk-methods-tutorial] (Использование прямых методов)).</span><span class="sxs-lookup"><span data-stu-id="53c28-177">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
