---
title: "свойства двойных устройства aaaUse центр IoT Azure (узел) | Документы Microsoft"
description: "Как устройства Azure IoT Hub toouse близнецы tooconfigure устройств. Hello Azure IoT пакетов SDK для Node.js tooimplement используется приложение имитированное устройство и приложение службы, которое изменяет конфигурацию устройства, с помощью двойных устройства."
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
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="39244-104">Используйте требуемого свойства tooconfigure устройства (узел)</span><span class="sxs-lookup"><span data-stu-id="39244-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="39244-105">В конце этого учебника hello будет иметь два Node.js консольные приложения:</span><span class="sxs-lookup"><span data-stu-id="39244-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="39244-106">**SimulateDeviceConfiguration.js**, приложение имитированное устройство, которое ожидает обновления требуемой конфигурацией и сообщает о состоянии hello имитацию конфигурации процесса обновления.</span><span class="sxs-lookup"><span data-stu-id="39244-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="39244-107">**SetDesiredConfigurationAndQuery.js**, приложение Node.js серверной части, который задает hello необходимой настройки на устройстве, и запросы hello процесс обновления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="39244-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="39244-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="39244-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="39244-109">toocomplete этого учебника требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="39244-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="39244-110">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="39244-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="39244-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="39244-111">An active Azure account.</span></span> <span data-ttu-id="39244-112">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="39244-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="39244-113">Если вы следовали hello [Приступая к работе с устройством близнецы] [ lnk-twin-tutorial] учебник, вы уже имеется центр IoT и вызывается удостоверение устройства **myDeviceId**; и можно пропустить toohello [ Создание приложения hello имитированное устройство] [ lnk-how-to-configure-createapp] раздела.</span><span class="sxs-lookup"><span data-stu-id="39244-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="39244-114">Создание приложения hello имитированное устройство</span><span class="sxs-lookup"><span data-stu-id="39244-114">Create hello simulated device app</span></span>
<span data-ttu-id="39244-115">В этом разделе создайте консольное приложение Node.js, которое подключается tooyour концентратора, **myDeviceId**, ожидает обновления требуемой конфигурацией, а затем информирует о на процесс обновления конфигурации имитируемые hello.</span><span class="sxs-lookup"><span data-stu-id="39244-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="39244-116">Создайте пустую папку с именем **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="39244-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="39244-117">В hello **simulatedeviceconfiguration** папки, создайте новый файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="39244-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="39244-118">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="39244-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="39244-119">В командной строке в hello **simulatedeviceconfiguration** папку, следующая команда tooinstall hello hello **azure iot устройства**, и **azure-iot устройства mqtt**пакета:</span><span class="sxs-lookup"><span data-stu-id="39244-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="39244-120">В текстовом редакторе создайте новый **SimulateDeviceConfiguration.js** файла в hello **simulatedeviceconfiguration** папки.</span><span class="sxs-lookup"><span data-stu-id="39244-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="39244-121">Добавьте следующий код toohello hello **SimulateDeviceConfiguration.js** файл и замените hello **{строка подключения устройства}** заполнитель со строкой подключения устройства hello, вы скопировали, когда вы создать hello **myDeviceId** удостоверение устройства:</span><span class="sxs-lookup"><span data-stu-id="39244-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="39244-122">Hello **клиента** объект предоставляет все необходимые toointeract hello методы с близнецы устройства с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="39244-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="39244-123">Здравствуйте предыдущего кода после инициализации hello **клиента** объекта извлекает hello двойных устройства для **myDeviceId**и присоединяет обработчик для обновления hello на требуемые свойства.</span><span class="sxs-lookup"><span data-stu-id="39244-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="39244-124">Обработчик Hello проверяет, существует запроса на изменение фактических конфигурации путем сравнения hello configIds, затем вызывает метод, который запускает изменение конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="39244-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="39244-125">Обратите внимание, что ради hello простоты hello предыдущий код использует жестко запрограммированные значения по умолчанию hello начальной настройки.</span><span class="sxs-lookup"><span data-stu-id="39244-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="39244-126">Настоящее приложение, вероятно, скачало бы эту конфигурацию из локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="39244-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="39244-127">События изменения нужное свойство выдаются всегда, один раз в процессе подключения устройства, убедитесь, что это реальное изменение hello toocheck нужными свойствами, прежде чем выполнять какие-либо действия.</span><span class="sxs-lookup"><span data-stu-id="39244-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="39244-128">Добавьте следующие методы перед hello hello `client.open()` вызова:</span><span class="sxs-lookup"><span data-stu-id="39244-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="39244-129">Hello **initConfigChange** метод обновляет отображаться свойства для hello объекта двойных локального устройства с запрос на обновление конфигурации hello и наборы hello состояние слишком**ожидающие**, а затем обновления hello устройства две службы hello.</span><span class="sxs-lookup"><span data-stu-id="39244-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="39244-130">После успешного обновления двойных hello устройства, в нем имитируется длительного процесса, который прерывает выполнение hello **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="39244-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="39244-131">Этот метод обновления hello локального устройства двойных сообщила свойства Установка состояния hello слишком**успех** и удаление hello **pendingConfig** объекта.</span><span class="sxs-lookup"><span data-stu-id="39244-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="39244-132">Затем он обновляет hello двойных устройства в службе hello.</span><span class="sxs-lookup"><span data-stu-id="39244-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="39244-133">Обратите внимание, что toosave пропускной способности, выводятся свойства обновляются путем указания изменен только toobe свойства hello (с именем **исправление** в hello над кодом), вместо замены всего документа hello.</span><span class="sxs-lookup"><span data-stu-id="39244-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="39244-134">В этом руководстве не имитируется поведение при одновременном обновлении конфигураций.</span><span class="sxs-lookup"><span data-stu-id="39244-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="39244-135">Некоторые процессы обновления конфигурации могут быть изменения могут tooaccommodate целевой конфигурации, во время обновления hello, другие могут иметь tooqueue, а также другие может отклонить их с состоянием ошибки.</span><span class="sxs-lookup"><span data-stu-id="39244-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="39244-136">Убедитесь, что tooconsider hello желаемое поведение для определенной конфигурации процесса и добавьте соответствующую логику hello перед запуском hello изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="39244-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="39244-137">Запустите приложение hello устройства:</span><span class="sxs-lookup"><span data-stu-id="39244-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="39244-138">Должно появиться сообщение hello `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="39244-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="39244-139">Оставьте приложение hello под управлением.</span><span class="sxs-lookup"><span data-stu-id="39244-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="39244-140">Создание приложения hello службы</span><span class="sxs-lookup"><span data-stu-id="39244-140">Create hello service app</span></span>
<span data-ttu-id="39244-141">В этом разделе вы создадите консольное приложение Node.js этого обновления hello *требуемого свойства* на двойных hello устройства, связанные с **myDeviceId** новым объектом конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="39244-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="39244-142">Он запрашивает близнецы устройства hello, хранящихся в центр IoT hello и показывает разность hello hello требуемого и данные конфигурации устройства hello.</span><span class="sxs-lookup"><span data-stu-id="39244-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="39244-143">Создайте пустую папку с именем **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="39244-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="39244-144">В hello **setdesiredandqueryapp** папки, создайте новый файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="39244-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="39244-145">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="39244-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="39244-146">В командной строке в hello **setdesiredandqueryapp** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета:</span><span class="sxs-lookup"><span data-stu-id="39244-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="39244-147">В текстовом редакторе создайте новый **SetDesiredAndQuery.js** файла в hello **addtagsandqueryapp** папки.</span><span class="sxs-lookup"><span data-stu-id="39244-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="39244-148">Добавьте следующий код toohello hello **SetDesiredAndQuery.js** файл и замените hello **{строка подключения концентратора iot}** заполнитель строки подключения центра IoT вы скопировали, когда вы создали концентратор приветствия :</span><span class="sxs-lookup"><span data-stu-id="39244-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
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

    <span data-ttu-id="39244-149">Hello **реестра** объект предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello.</span><span class="sxs-lookup"><span data-stu-id="39244-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="39244-150">Здравствуйте, предыдущий код после инициализации hello **реестра** объекта извлекает hello двойных устройства для **myDeviceId**и обновляет его нужными свойствами нового объекта конфигурации телеметрии.</span><span class="sxs-lookup"><span data-stu-id="39244-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="39244-151">После этого он вызывает hello **queryTwins** функции события 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="39244-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="39244-152">Это приложение выполняет запрос к Центру Интернета вещей каждые 10 секунд в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="39244-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="39244-153">Используйте запрашивает toogenerate пользовательские отчеты для многих устройств и не toodetect изменения.</span><span class="sxs-lookup"><span data-stu-id="39244-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="39244-154">Если вашему решению требуется отправка уведомлений о событиях устройства в реальном времени, используйте [уведомления двойников][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="39244-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="39244-155">.</span><span class="sxs-lookup"><span data-stu-id="39244-155">.</span></span>

1. <span data-ttu-id="39244-156">Добавьте следующий код прямо перед hello hello `registry.getDeviceTwin()` hello вызова tooimplement **queryTwins** функции:</span><span class="sxs-lookup"><span data-stu-id="39244-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
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
   
    <span data-ttu-id="39244-157">Hello предыдущих запросов кода hello близнецы устройств хранятся в центре IoT hello и печатает hello требуемого и данные телеметрии конфигураций.</span><span class="sxs-lookup"><span data-stu-id="39244-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="39244-158">См. toohello [язык запросов центра IoT] [ lnk-query] toolearn как toogenerate полнофункциональных отчетов на всех устройствах.</span><span class="sxs-lookup"><span data-stu-id="39244-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="39244-159">С **SimulateDeviceConfiguration.js** запущена, запустите приложение hello с:</span><span class="sxs-lookup"><span data-stu-id="39244-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="39244-160">Вы увидите изменение из указанной конфигурации hello **успех** слишком**ожидающие** слишком**успех** попытку новой активной hello пять минут, а не 24 частота отправки часы.</span><span class="sxs-lookup"><span data-stu-id="39244-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="39244-161">Нет задержки мин tooa между hello устройство работы и отчетов hello результата запроса.</span><span class="sxs-lookup"><span data-stu-id="39244-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="39244-162">Это toowork tooenable hello запроса инфраструктуры в очень широком масштабе.</span><span class="sxs-lookup"><span data-stu-id="39244-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="39244-163">использовать tooretrieve согласованного представления двойных одно устройство hello **getDeviceTwin** метод в hello **реестра** класса.</span><span class="sxs-lookup"><span data-stu-id="39244-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="39244-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="39244-164">Next steps</span></span>
<span data-ttu-id="39244-165">В этом учебнике можно задавать нужные параметры как *требуемого свойства* из серверной части приложения и написал toodetect имитированное устройство приложения, изменять и имитировать обновления многоступенчатый процесс, сообщение о состоянии  *отчет свойства* двойных toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="39244-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="39244-166">Hello используйте следующие ресурсы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="39244-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="39244-167">Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника</span><span class="sxs-lookup"><span data-stu-id="39244-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="39244-168">запланировать или выполнять операции с большими наборами устройств в разделе hello [расписание и широковещательных задания] [ lnk-schedule-jobs] учебника.</span><span class="sxs-lookup"><span data-stu-id="39244-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="39244-169">Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения), с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="39244-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
