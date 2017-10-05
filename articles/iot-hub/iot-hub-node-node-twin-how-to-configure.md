---
title: "Использование свойств двойников устройств Центра Интернета вещей (Node) | Документация Майкрософт"
description: "Настройка устройств с помощью двойников устройств Центра Интернета вещей Azure. Используйте пакеты SDK для Центра Интернета вещей Azure для Node.js, чтобы реализовать приложение имитации устройства и приложение службы, которое изменяет конфигурацию устройства с помощью двойника устройства."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 771106ce7b00a5231d9929e4b5ea34aefe693597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-desired-properties-to-configure-devices-node"></a><span data-ttu-id="c1293-104">Настройка устройств с помощью требуемых свойств (Node)</span><span class="sxs-lookup"><span data-stu-id="c1293-104">Use desired properties to configure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="c1293-105">По завершении работы с этим руководством у вас будет два консольных приложения Node.js:</span><span class="sxs-lookup"><span data-stu-id="c1293-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="c1293-106">**SimulateDeviceConfiguration.js** — это приложение имитации устройства, которое ожидает обновления требуемой конфигурации и сообщает о состоянии обновления имитации конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c1293-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="c1293-107">**SetDesiredConfigurationAndQuery.js** — это внутреннее приложение Node.js, которое задает требуемую конфигурацию на устройстве и выполняет запрос к процессу обновления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c1293-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="c1293-108">Статья [IoT Hub SDKs][lnk-hub-sdks] (Пакеты SDK для Центра Интернета вещей) содержит сведения о разных пакетах SDK для Azure IoT, с помощью которых можно создать приложения для устройств и внутренние приложения.</span><span class="sxs-lookup"><span data-stu-id="c1293-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="c1293-109">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="c1293-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="c1293-110">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="c1293-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="c1293-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c1293-111">An active Azure account.</span></span> <span data-ttu-id="c1293-112">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c1293-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="c1293-113">Если вы выполнили указания руководства [Приступая к работе с двойниками устройств (предварительная версия)][lnk-twin-tutorial], то у вас уже есть Центр Интернета вещей и удостоверение устройства **myDeviceId**. Вы можете перейти к разделу [Создание приложения имитации устройства][lnk-how-to-configure-createapp].</span><span class="sxs-lookup"><span data-stu-id="c1293-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-simulated-device-app"></a><span data-ttu-id="c1293-114">Создание приложения имитации устройства</span><span class="sxs-lookup"><span data-stu-id="c1293-114">Create the simulated device app</span></span>
<span data-ttu-id="c1293-115">В этом разделе вы создаете консольное приложение Node.js, которое подключается к центру как **myDeviceId**, ожидает обновления требуемой конфигурации и сообщает об обновлениях в ходе обновления имитации конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c1293-115">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="c1293-116">Создайте пустую папку с именем **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="c1293-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="c1293-117">В папке **simulatedeviceconfiguration** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="c1293-117">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="c1293-118">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c1293-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="c1293-119">В командной строке в папке **simulatedeviceconfiguration** выполните следующую команду, чтобы установить пакеты **azure-iot-device** и **azure-iot-device-mqtt**.</span><span class="sxs-lookup"><span data-stu-id="c1293-119">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="c1293-120">В текстовом редакторе создайте файл **SimulateDeviceConfiguration.js** в папке **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="c1293-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="c1293-121">Добавьте следующий код в файл **SimulateDeviceConfiguration.js** и замените заполнитель **{device connection string}** строкой подключения устройства, скопированной при создании удостоверения устройства **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="c1293-121">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="c1293-122">Объект **Client** позволяет получить все методы, необходимые для взаимодействия с двойниками устройства с устройства.</span><span class="sxs-lookup"><span data-stu-id="c1293-122">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="c1293-123">После инициализации объекта **Client** предыдущий код извлекает двойник устройства для **myDeviceId** и подключает обработчик для обновления требуемых свойств.</span><span class="sxs-lookup"><span data-stu-id="c1293-123">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId**, and attaches a handler for the update on desired properties.</span></span> <span data-ttu-id="c1293-124">Обработчик проверяет, отправлен ли запрос на изменение конфигурации. Для этого он сравнивает идентификаторы конфигураций, а затем вызывает метод, который запускает изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c1293-124">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="c1293-125">Обратите внимание, что для простоты приведенный выше код использует жестко заданное значение по умолчанию для выполнения начальной настройки.</span><span class="sxs-lookup"><span data-stu-id="c1293-125">Note that for the sake of simplicity, the previous code uses a hard-coded default for the inital configuration.</span></span> <span data-ttu-id="c1293-126">Настоящее приложение, вероятно, скачало бы эту конфигурацию из локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="c1293-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c1293-127">События изменения требуемых свойств всегда создаются единожды при подключении устройства. Прежде чем что-либо делать, обязательно убедитесь, что требуемые свойства действительно изменились.</span><span class="sxs-lookup"><span data-stu-id="c1293-127">Desired property change events are always emitted once at device connection, make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="c1293-128">Добавьте следующие методы перед осуществлением вызова `client.open()`:</span><span class="sxs-lookup"><span data-stu-id="c1293-128">Add the following methods before the `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="c1293-129">Метод **initConfigChange** обновляет сообщаемые свойства в объекте локального двойника устройства с помощью запроса на обновление конфигурации и устанавливает для состояния значение **Ожидание**, а затем обновляет двойник устройства в службе.</span><span class="sxs-lookup"><span data-stu-id="c1293-129">The **initConfigChange** method updates reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="c1293-130">После успешного обновления двойника устройства он имитирует длительный процесс, который завершается выполнением **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="c1293-130">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="c1293-131">Этот метод обновляет сообщаемые свойства локального двойника устройства, установив для состояния значение **Success** и удалив объект **pendingConfig**.</span><span class="sxs-lookup"><span data-stu-id="c1293-131">This method updates the local device twin's reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="c1293-132">Затем он обновляет двойник устройства в службе.</span><span class="sxs-lookup"><span data-stu-id="c1293-132">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="c1293-133">Обратите внимание, что для сокращения нагрузки на полосу пропускания при обновлении сообщаемых свойств указываются только свойства, которые нужно изменить (**patch** в коде выше), а не заменяется весь документ.</span><span class="sxs-lookup"><span data-stu-id="c1293-133">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1293-134">В этом руководстве не имитируется поведение при одновременном обновлении конфигураций.</span><span class="sxs-lookup"><span data-stu-id="c1293-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="c1293-135">В некоторых случаях обновление конфигурации может пройти в соответствии с изменениями целевой конфигурации, в других может потребоваться поместить изменения в очередь, а в остальных они могут быть отклонены с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="c1293-135">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, others might have to queue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="c1293-136">Следует учитывать желаемое поведение для конкретной конфигурации и добавить соответствующую логику перед ее изменением.</span><span class="sxs-lookup"><span data-stu-id="c1293-136">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="c1293-137">Запустите приложение устройства:</span><span class="sxs-lookup"><span data-stu-id="c1293-137">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="c1293-138">Отобразится сообщение `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="c1293-138">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="c1293-139">Не отключайте приложение.</span><span class="sxs-lookup"><span data-stu-id="c1293-139">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="c1293-140">Создание приложения службы</span><span class="sxs-lookup"><span data-stu-id="c1293-140">Create the service app</span></span>
<span data-ttu-id="c1293-141">В этом разделе вы создадите консольное приложение Node.js, которое обновляет *требуемые свойства* двойника устройства, связанного с **myDeviceId**, с использованием нового объекта конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="c1293-141">In this section, you will create a Node.js console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="c1293-142">Затем оно выполняет запрос к двойникам устройств, которые хранятся в Центре Интернета вещей, и показывает разницу между требуемой и сообщаемой конфигурацией устройства.</span><span class="sxs-lookup"><span data-stu-id="c1293-142">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="c1293-143">Создайте пустую папку с именем **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="c1293-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="c1293-144">В папке **setdesiredandqueryapp** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="c1293-144">In the **setdesiredandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="c1293-145">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c1293-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="c1293-146">В командной строке в папке **setdesiredandqueryapp** выполните следующую команду, чтобы установить пакет **azure-iothub**.</span><span class="sxs-lookup"><span data-stu-id="c1293-146">At your command prompt in the **setdesiredandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="c1293-147">В текстовом редакторе создайте файл **SetDesiredAndQuery.js** в папке **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="c1293-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="c1293-148">Добавьте следующий код в файл **SetDesiredAndQuery.js** и замените заполнитель **{iot hub connection string}** на строку подключения Центра Интернета вещей, скопированную при создании центра:</span><span class="sxs-lookup"><span data-stu-id="c1293-148">Add the following code to the **SetDesiredAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="c1293-149">Объект **Registry** позволяет получить все методы, необходимые для взаимодействия с двойниками устройства из службы.</span><span class="sxs-lookup"><span data-stu-id="c1293-149">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="c1293-150">После инициализации объекта **Registry** предыдущий код извлекает двойник устройства для **myDeviceId** и обновляет его требуемые свойства, используя новый объект конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="c1293-150">The previous code, after it initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="c1293-151">После этого он вызывает функцию **queryTwins** каждые 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="c1293-151">After that, it calls the **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c1293-152">Это приложение выполняет запрос к Центру Интернета вещей каждые 10 секунд в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c1293-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="c1293-153">Используйте запросы для создания представляемых пользователям отчетов на многих устройствах, а не для обнаружения изменений.</span><span class="sxs-lookup"><span data-stu-id="c1293-153">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="c1293-154">Если вашему решению требуется отправка уведомлений о событиях устройства в реальном времени, используйте [уведомления двойников][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="c1293-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="c1293-155">.</span><span class="sxs-lookup"><span data-stu-id="c1293-155">.</span></span>

1. <span data-ttu-id="c1293-156">Добавьте следующий код перед осуществлением вызова `registry.getDeviceTwin()` для реализации функции **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="c1293-156">Add the following code right before the `registry.getDeviceTwin()` invocation to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="c1293-157">Предыдущий код выполняет запрос к двойникам устройств, которые хранятся в Центре Интернета вещей, и выводит требуемые и сообщаемые конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="c1293-157">The previous code queries the device twins stored in the IoT hub and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="c1293-158">Чтобы узнать, как создавать эффективные отчеты на всех устройствах, см. статью [Справочник по языку запросов для двойников и заданий][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="c1293-158">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
2. <span data-ttu-id="c1293-159">Запустив файл **SimulateDeviceConfiguration.js**, запустите приложение с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="c1293-159">With **SimulateDeviceConfiguration.js** running, run the application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="c1293-160">Состояние сообщаемой конфигурации изменится с **Success** на **Pending** и снова на **Success**, а значение активной частоты отправки изменится с 24 часов на пять минут.</span><span class="sxs-lookup"><span data-stu-id="c1293-160">You should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c1293-161">Результаты запроса выводятся после операции сообщения устройства с задержкой (не более минуты).</span><span class="sxs-lookup"><span data-stu-id="c1293-161">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="c1293-162">Таким образом обеспечивается работа инфраструктуры запросов в очень широком масштабе.</span><span class="sxs-lookup"><span data-stu-id="c1293-162">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="c1293-163">Для получения согласованных представлений одного двойника устройства используйте метод **getDeviceTwin** в классе **Registry**.</span><span class="sxs-lookup"><span data-stu-id="c1293-163">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="c1293-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1293-164">Next steps</span></span>
<span data-ttu-id="c1293-165">В этом руководстве вы установили требуемую конфигурацию в качестве *требуемых свойств* из внутреннего приложения и написали код приложения для имитации устройства, которое обнаруживает изменения и имитирует многоэтапный процесс обновления, о состоянии которого сообщается двойнику устройства в качестве *сообщаемых свойств*.</span><span class="sxs-lookup"><span data-stu-id="c1293-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app to detect that change and simulate a multi-step update process reporting its status as *reported properties* to the device twin.</span></span>

<span data-ttu-id="c1293-166">Ознакомьтесь со следующими материалами, чтобы узнать как:</span><span class="sxs-lookup"><span data-stu-id="c1293-166">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="c1293-167">отправить данные телеметрии с устройств (учебник [Приступая к работе с Центром Интернета вещей Azure (Node)][lnk-iothub-getstarted]);</span><span class="sxs-lookup"><span data-stu-id="c1293-167">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="c1293-168">запланировать или выполнить операции на больших наборах устройств (см. учебник [Планирование и трансляция заданий][lnk-schedule-jobs];</span><span class="sxs-lookup"><span data-stu-id="c1293-168">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="c1293-169">управлять устройствами в интерактивном режиме, например включить вентилятор из управляемого пользователем приложения (учебник [Use direct methods][lnk-methods-tutorial] (Использование прямых методов)).</span><span class="sxs-lookup"><span data-stu-id="c1293-169">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

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
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
