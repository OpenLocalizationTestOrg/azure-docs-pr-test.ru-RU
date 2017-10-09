---
title: "aaaSchedule заданий с центром IoT Azure (узел) | Документы Microsoft"
description: "Как tooschedule центр IoT Azure заданий tooinvoke прямой метод на нескольких устройствах. Использовать hello Azure IoT пакетов SDK для Node.js tooimplement hello имитируемые приложения для устройств и задание службы toorun приложения hello."
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
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="58736-104">Планирование и трансляция заданий (Node)</span><span class="sxs-lookup"><span data-stu-id="58736-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="58736-105">Центр IoT Azure является полностью управляемой службы, которая позволяет toocreate серверной части приложения и задания отслеживания, планировать и обновлять миллионов устройств.</span><span class="sxs-lookup"><span data-stu-id="58736-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="58736-106">Задания можно использовать для hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="58736-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="58736-107">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="58736-107">Update desired properties</span></span>
* <span data-ttu-id="58736-108">Обновление тегов</span><span class="sxs-lookup"><span data-stu-id="58736-108">Update tags</span></span>
* <span data-ttu-id="58736-109">Вызов прямых методов</span><span class="sxs-lookup"><span data-stu-id="58736-109">Invoke direct methods</span></span>

<span data-ttu-id="58736-110">По существу задание включает один из этих действий и отслеживает hello ход выполнения для набора устройств, в которой определяется запросом двойных устройства.</span><span class="sxs-lookup"><span data-stu-id="58736-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="58736-111">Например приложение серверной части можно использовать tooinvoke задания метод перезагрузки на 10 000 устройств, указанных запросом двойных устройства и по расписанию время в будущем.</span><span class="sxs-lookup"><span data-stu-id="58736-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="58736-112">Это приложение можно отслеживать ход выполнения, как каждая из этих устройств получают hello перезагрузки метод execute.</span><span class="sxs-lookup"><span data-stu-id="58736-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="58736-113">Дополнительные сведения о каждой из этих возможностей см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="58736-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="58736-114">Двойных устройства и свойства: [Приступая к работе с устройством близнецы] [ lnk-get-started-twin] и [учебника: как свойства двойных toouse устройства][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="58736-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="58736-115">Прямые методы: [Вызов прямого метода на устройстве (предварительная версия)][lnk-dev-methods] и [Руководство. Использование прямых методов][lnk-c2d-methods].</span><span class="sxs-lookup"><span data-stu-id="58736-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="58736-116">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="58736-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="58736-117">Создать приложение имитированное устройство, которое имеет прямой метод, который позволяет **lockDoor** которого может быть вызван hello решения серверной части.</span><span class="sxs-lookup"><span data-stu-id="58736-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="58736-118">Создайте консольное приложение Node.js, hello вызовов **lockDoor** прямой метод в приложение hello имитированное устройство с помощью задания и обновления hello требуемого свойства с помощью задания устройства.</span><span class="sxs-lookup"><span data-stu-id="58736-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="58736-119">В конце этого учебника hello у вас есть два Node.js консольные приложения:</span><span class="sxs-lookup"><span data-stu-id="58736-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="58736-120">**simDevice.js**, который соединяет центр IoT tooyour с hello удостоверения устройства и получает **lockDoor** прямой метод.</span><span class="sxs-lookup"><span data-stu-id="58736-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="58736-121">**scheduleJobService.js**, которого вызывает метод с прямой hello имитированное устройство приложения и обновления hello устройства в двойных нужными свойствами при помощи задания.</span><span class="sxs-lookup"><span data-stu-id="58736-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="58736-122">toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="58736-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="58736-123">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="58736-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="58736-124">[Подготовка среды разработки] [ lnk-dev-setup] описывает способ tooinstall Node.js для этого учебника в Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="58736-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="58736-125">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="58736-125">An active Azure account.</span></span> <span data-ttu-id="58736-126">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="58736-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="58736-127">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="58736-127">Create a simulated device app</span></span>
<span data-ttu-id="58736-128">В этом разделе создайте консольное приложение Node.js, которое отвечает tooa прямой метод, вызываемый hello облака, активизирующий перезагрузка имитации устройства и использует hello выводятся свойства tooenable устройствами двойных запросы tooidentify устройства и когда они последней перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="58736-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="58736-129">Создайте пустую папку с именем **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="58736-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="58736-130">В hello **simDevice** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="58736-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="58736-131">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="58736-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="58736-132">В командной строке в hello **simDevice** папку, следующая команда tooinstall hello hello **azure iot устройства** пакета SDK для устройства и **azure iot устройства mqtt** пакет:</span><span class="sxs-lookup"><span data-stu-id="58736-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="58736-133">В текстовом редакторе создайте новый **simDevice.js** файла в hello **simDevice** папки.</span><span class="sxs-lookup"><span data-stu-id="58736-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="58736-134">Добавьте следующие hello «требовать» операторы в начале hello hello **simDevice.js** файла:</span><span class="sxs-lookup"><span data-stu-id="58736-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="58736-135">Добавить **connectionString** переменной и использовать его toocreate **клиента** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="58736-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="58736-136">Добавить следующие функции hello toohandle hello **lockDoor** метод.</span><span class="sxs-lookup"><span data-stu-id="58736-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="58736-137">Добавьте следующий код обработчика hello tooregister для hello hello **lockDoor** метод.</span><span class="sxs-lookup"><span data-stu-id="58736-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="58736-138">Сохраните и закройте hello **simDevice.js** файла.</span><span class="sxs-lookup"><span data-stu-id="58736-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="58736-139">простые действия tookeep, этот учебник не реализует никакую политику повтора.</span><span class="sxs-lookup"><span data-stu-id="58736-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="58736-140">В рабочем коде следует реализовать политики повтора (например экспоненциальную отсрочку), описанным в статье MSDN hello [обработка временных сбоев][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="58736-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="58736-141">Планирование заданий для вызова прямого метода и обновления свойств двойника устройства</span><span class="sxs-lookup"><span data-stu-id="58736-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="58736-142">В этом разделе создайте консольное приложение Node.js, который инициирует удаленный **lockDoor** на устройстве с помощью прямой метод и обновление hello устройства двойных его свойств.</span><span class="sxs-lookup"><span data-stu-id="58736-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="58736-143">Создайте пустую папку с именем **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="58736-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="58736-144">В hello **scheduleJobService** папки, создайте файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="58736-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="58736-145">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="58736-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="58736-146">В командной строке в hello **scheduleJobService** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета SDK для устройства и **azure-iot устройства mqtt**пакета:</span><span class="sxs-lookup"><span data-stu-id="58736-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="58736-147">В текстовом редакторе создайте новый **scheduleJobService.js** файла в hello **scheduleJobService** папки.</span><span class="sxs-lookup"><span data-stu-id="58736-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="58736-148">Добавьте следующие hello «требовать» операторы в начале hello hello **dmpatterns_gscheduleJobServiceetstarted_service.js** файла:</span><span class="sxs-lookup"><span data-stu-id="58736-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="58736-149">Добавьте следующие объявления переменных hello и замените значения заполнителей hello.</span><span class="sxs-lookup"><span data-stu-id="58736-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="58736-150">Добавьте следующие функции, которая будет использоваться toomonitor hello выполнение задания hello hello:</span><span class="sxs-lookup"><span data-stu-id="58736-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="58736-151">Добавьте следующие задания hello tooschedule код, вызывающий метод устройства hello hello:</span><span class="sxs-lookup"><span data-stu-id="58736-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="58736-152">Добавьте следующий код tooschedule hello задания tooupdate hello устройства двойных hello:</span><span class="sxs-lookup"><span data-stu-id="58736-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="58736-153">Сохраните и закройте hello **scheduleJobService.js** файла.</span><span class="sxs-lookup"><span data-stu-id="58736-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="58736-154">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="58736-154">Run hello applications</span></span>
<span data-ttu-id="58736-155">Теперь вы находитесь toorun готовности приложения hello.</span><span class="sxs-lookup"><span data-stu-id="58736-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="58736-156">В командной строке hello в hello **simDevice** папки, запустите следующие команды toobegin прослушивание прямой метод перезагрузки hello hello.</span><span class="sxs-lookup"><span data-stu-id="58736-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="58736-157">В командной строке hello в hello **scheduleJobService** папку, следующая команда tootrigger hello задания toolock hello дверцы и обновление hello двойных hello</span><span class="sxs-lookup"><span data-stu-id="58736-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="58736-158">Появиться hello устройства toohello прямой метод ответа в консоли hello.</span><span class="sxs-lookup"><span data-stu-id="58736-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58736-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58736-159">Next steps</span></span>
<span data-ttu-id="58736-160">В этом учебнике используется задание tooschedule прямой метод tooa устройства и hello обновление свойств устройства двойных hello.</span><span class="sxs-lookup"><span data-stu-id="58736-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="58736-161">Приступая к работе с центр IoT и шаблонов управления устройства, такие как удаленное через обновление встроенного по воздуху hello, toocontinue см.:</span><span class="sxs-lookup"><span data-stu-id="58736-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="58736-162">[Учебник: Как toodo встроенное по обновить][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="58736-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="58736-163">Приступая к работе с центром IoT toocontinue в разделе [Приступая к работе с Azure IoT Edge][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="58736-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
