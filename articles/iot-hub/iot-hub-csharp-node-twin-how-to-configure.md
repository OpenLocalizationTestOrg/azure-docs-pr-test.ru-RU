---
title: "свойства двойных устройства aaaUse центр IoT Azure (.NET или узел) | Документы Microsoft"
description: "Как устройства Azure IoT Hub toouse близнецы tooconfigure устройств. Можно использовать устройства Azure IoT hello пакета SDK для Node.js tooimplement приложения имитированное устройство и hello Azure IoT служба пакета SDK для .NET tooimplement приложение службы, которое изменяет конфигурацию устройства, с помощью двойных устройства."
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
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="d83c9-104">Использовать нужными свойствами tooconfigure устройства</span><span class="sxs-lookup"><span data-stu-id="d83c9-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="d83c9-105">В конце этого учебника hello будет иметь два приложения консоли:</span><span class="sxs-lookup"><span data-stu-id="d83c9-105">At hello end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="d83c9-106">**SimulateDeviceConfiguration.js**, приложение имитированное устройство, которое ожидает обновления требуемой конфигурацией и сообщает о состоянии hello имитацию конфигурации процесса обновления.</span><span class="sxs-lookup"><span data-stu-id="d83c9-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="d83c9-107">**SetDesiredConfigurationAndQuery**, приложении серверной части .NET, который задает hello необходимой настройки на устройстве, и запросы hello процесс обновления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d83c9-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="d83c9-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="d83c9-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="d83c9-109">toocomplete этого учебника требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="d83c9-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="d83c9-110">Visual Studio 2015 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d83c9-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d83c9-111">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d83c9-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="d83c9-112">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d83c9-112">An active Azure account.</span></span> <span data-ttu-id="d83c9-113">Если у вас нет учетной записи, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d83c9-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="d83c9-114">Если вы следовали hello [Приступая к работе с устройством близнецы] [ lnk-twin-tutorial] учебник, вы уже имеется центр IoT и вызывается удостоверение устройства **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="d83c9-114">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="d83c9-115">В этом случае можно пропустить toohello [имитированное устройство hello создать приложение] [ lnk-how-to-configure-createapp] раздела.</span><span class="sxs-lookup"><span data-stu-id="d83c9-115">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="d83c9-116">Создание приложения hello имитированное устройство</span><span class="sxs-lookup"><span data-stu-id="d83c9-116">Create hello simulated device app</span></span>
<span data-ttu-id="d83c9-117">В этом разделе создайте консольное приложение Node.js, которое подключается tooyour концентратора, **myDeviceId**, ожидает обновления требуемой конфигурацией, а затем информирует о на процесс обновления конфигурации имитируемые hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-117">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="d83c9-118">Создайте пустую папку с именем **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="d83c9-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="d83c9-119">В hello **simulatedeviceconfiguration** папки, создайте новый файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-119">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="d83c9-120">Примите все значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-120">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="d83c9-121">В командной строке в hello **simulatedeviceconfiguration** папку, следующая команда tooinstall hello hello **azure iot устройства** и **azure-iot устройства mqtt**пакетов:</span><span class="sxs-lookup"><span data-stu-id="d83c9-121">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="d83c9-122">В текстовом редакторе создайте новый **SimulateDeviceConfiguration.js** файла в hello **simulatedeviceconfiguration** папки.</span><span class="sxs-lookup"><span data-stu-id="d83c9-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="d83c9-123">Добавьте следующий код toohello hello **SimulateDeviceConfiguration.js** файл и замените hello **{строка подключения устройства}** заполнитель со строкой подключения устройства hello, вы скопировали, когда вы создать hello **myDeviceId** удостоверение устройства:</span><span class="sxs-lookup"><span data-stu-id="d83c9-123">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="d83c9-124">Hello **клиента** объект предоставляет все необходимые toointeract hello методы с близнецы устройства с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-124">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="d83c9-125">Этот код инициализирует hello **клиента** объекта извлекает hello двойных устройства для **myDeviceId**, а затем присоединяется обработчик hello обновления на *требуемого свойства*.</span><span class="sxs-lookup"><span data-stu-id="d83c9-125">This code initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and then attaches a handler for hello update on *desired properties*.</span></span> <span data-ttu-id="d83c9-126">Обработчик Hello проверяет, существует запроса на изменение фактических конфигурации путем сравнения hello configIds, затем вызывает метод, который запускает изменение конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-126">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="d83c9-127">Обратите внимание, что ради hello простоты этот код использует значение по умолчанию жестко hello начальной настройки.</span><span class="sxs-lookup"><span data-stu-id="d83c9-127">Note that for hello sake of simplicity, this code uses a hard-coded default for hello initial configuration.</span></span> <span data-ttu-id="d83c9-128">Настоящее приложение, вероятно, скачало бы эту конфигурацию из локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="d83c9-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d83c9-129">События изменения требуемых свойств всегда инициируются единожды при подключении устройства.</span><span class="sxs-lookup"><span data-stu-id="d83c9-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="d83c9-130">Убедитесь, что это реальное изменение hello toocheck нужными свойствами, прежде чем выполнять какие-либо действия.</span><span class="sxs-lookup"><span data-stu-id="d83c9-130">Make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="d83c9-131">Добавьте следующие методы перед hello hello `client.open()` вызова:</span><span class="sxs-lookup"><span data-stu-id="d83c9-131">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="d83c9-132">Hello **initConfigChange** метод обновления hello сообщил свойства hello объекта двойных локального устройства с конфигурацией hello обновить запрос и задает состояние hello слишком**ожидающие**, а затем обновления hello двойных устройства в службе hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-132">hello **initConfigChange** method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="d83c9-133">После успешного обновления двойных hello устройства, в нем имитируется длительного процесса, который прерывает выполнение hello **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="d83c9-133">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="d83c9-134">Этот метод обновляет hello локальные отчета свойства параметра состояния hello слишком**успех** и удаление hello **pendingConfig** объекта.</span><span class="sxs-lookup"><span data-stu-id="d83c9-134">This method updates hello local reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="d83c9-135">Затем он обновляет hello двойных устройства в службе hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-135">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="d83c9-136">Обратите внимание, что toosave пропускной способности, выводятся свойства обновляются путем указания изменен только toobe свойства hello (с именем **исправление** в hello над кодом), вместо замены всего документа hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-136">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d83c9-137">В этом руководстве не имитируется поведение при одновременном обновлении конфигураций.</span><span class="sxs-lookup"><span data-stu-id="d83c9-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="d83c9-138">Некоторые процессы обновления конфигурации могут быть изменения могут tooaccommodate целевой конфигурации, во время обновления hello, некоторые могут иметь tooqueue их, а некоторые может отклонить их с состоянием ошибки.</span><span class="sxs-lookup"><span data-stu-id="d83c9-138">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="d83c9-139">Убедитесь, что tooconsider hello желаемое поведение для определенной конфигурации процесса и добавьте соответствующую логику hello перед запуском hello изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d83c9-139">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="d83c9-140">Запустите приложение hello устройства:</span><span class="sxs-lookup"><span data-stu-id="d83c9-140">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="d83c9-141">Должно появиться сообщение hello `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="d83c9-141">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="d83c9-142">Оставьте приложение hello под управлением.</span><span class="sxs-lookup"><span data-stu-id="d83c9-142">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="d83c9-143">Создание приложения hello службы</span><span class="sxs-lookup"><span data-stu-id="d83c9-143">Create hello service app</span></span>
<span data-ttu-id="d83c9-144">В этом разделе вы создадите консольное приложение .NET, hello обновления *требуемого свойства* на двойных hello устройства, связанные с **myDeviceId** новым объектом конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="d83c9-144">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="d83c9-145">Он запрашивает близнецы устройства hello, хранящихся в центр IoT hello и показывает разность hello hello требуемого и данные конфигурации устройства hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-145">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="d83c9-146">В Visual Studio, добавить проект Visual C# Windows классического toohello текущее решение с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="d83c9-146">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="d83c9-147">Имя проекта hello **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="d83c9-147">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Новый проект классического приложения Windows на языке Visual C#][img-createapp]
1. <span data-ttu-id="d83c9-149">В обозревателе решений щелкните правой кнопкой мыши hello **SetDesiredConfigurationAndQuery** проекта, а затем нажмите кнопку **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="d83c9-149">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="d83c9-150">В hello **диспетчера пакетов NuGet** выберите **Обзор**, поиск **microsoft.azure.devices**выберите **установить** tooinstall Hello **Microsoft.Azure.Devices** пакета и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-150">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="d83c9-151">Эта процедура загрузки, устанавливает и добавляет toohello ссылки [пакета SDK службы Azure IoT] [ lnk-nuget-service-sdk] NuGet пакет и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="d83c9-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Окно "Диспетчер пакетов NuGet"][img-servicenuget]
1. <span data-ttu-id="d83c9-153">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="d83c9-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="d83c9-154">Добавьте следующие поля toohello hello **программы** класса.</span><span class="sxs-lookup"><span data-stu-id="d83c9-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d83c9-155">Замените значение заполнителя hello hello центра IoT строку подключения для hello концентратора, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-155">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="d83c9-156">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="d83c9-156">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="d83c9-157">Hello **реестра** объект предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-157">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="d83c9-158">Этот код инициализирует hello **реестра** объекта извлекает hello двойных устройства для **myDeviceId**и затем обновляет ее нужными свойствами нового объекта конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="d83c9-158">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="d83c9-159">После этого он запрашивает близнецы устройства hello, хранящихся в центр IoT hello каждые 10 секунд и печатает hello требуемого и данные телеметрии конфигураций.</span><span class="sxs-lookup"><span data-stu-id="d83c9-159">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="d83c9-160">См. toohello [язык запросов центра IoT] [ lnk-query] toolearn как toogenerate полнофункциональных отчетов на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="d83c9-160">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d83c9-161">Это приложение выполняет запрос к Центру Интернета вещей каждые 10 секунд в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d83c9-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="d83c9-162">Используйте запрашивает toogenerate пользовательские отчеты для многих устройств и не toodetect изменения.</span><span class="sxs-lookup"><span data-stu-id="d83c9-162">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="d83c9-163">Если вашему решению требуется отправка уведомлений о событиях устройства в реальном времени, используйте [уведомления двойников][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="d83c9-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="d83c9-164">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="d83c9-164">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="d83c9-165">В hello обозревателе решений откройте hello **задать автозагружаемых проектов...**  и убедитесь, что hello **действия** для **SetDesiredConfigurationAndQuery** проект является **запустить**.</span><span class="sxs-lookup"><span data-stu-id="d83c9-165">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="d83c9-166">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="d83c9-166">Build hello solution.</span></span>
1. <span data-ttu-id="d83c9-167">С **SimulateDeviceConfiguration.js** запущена, запустите приложение hello .NET из Visual Studio с помощью **F5** и вы увидите изменение из указанной конфигурации hello **успех** слишком**ожидающие** слишком**успех** снова новой активной hello отправить частоту 5 минут, а не 24 часа.</span><span class="sxs-lookup"><span data-stu-id="d83c9-167">With **SimulateDeviceConfiguration.js** running, run hello .NET application from Visual Studio using **F5** and you should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Устройство успешно настроено][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="d83c9-169">Нет задержки мин tooa между hello устройство работы и отчетов hello результата запроса.</span><span class="sxs-lookup"><span data-stu-id="d83c9-169">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="d83c9-170">Это toowork tooenable hello запроса инфраструктуры в очень широком масштабе.</span><span class="sxs-lookup"><span data-stu-id="d83c9-170">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="d83c9-171">использовать tooretrieve согласованного представления двойных одно устройство hello **getDeviceTwin** метод в hello **реестра** класса.</span><span class="sxs-lookup"><span data-stu-id="d83c9-171">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="d83c9-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d83c9-172">Next steps</span></span>
<span data-ttu-id="d83c9-173">В этом учебнике можно задавать нужные параметры как *требуемого свойства* из решения hello серверной части и написал toodetect приложения устройства, изменение и имитировать обновления многоступенчатый процесс, его через hello сообщил о состоянии свойства.</span><span class="sxs-lookup"><span data-stu-id="d83c9-173">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="d83c9-174">Hello используйте следующие ресурсы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="d83c9-174">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="d83c9-175">Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника</span><span class="sxs-lookup"><span data-stu-id="d83c9-175">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="d83c9-176">запланировать или выполнять операции с большими наборами устройств в разделе hello [расписание и широковещательных задания] [ lnk-schedule-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="d83c9-176">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="d83c9-177">Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения), с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="d83c9-177">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
