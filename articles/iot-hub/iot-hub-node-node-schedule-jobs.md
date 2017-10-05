---
title: "Планирование заданий с помощью Центра Интернета вещей Azure (Node) | Документация Майкрософт"
description: "Планирование заданий с помощью Центра Интернета вещей Azure для вызова прямого метода на нескольких устройствах. Используйте пакеты SDK для Центра Интернета вещей Azure для Node.js, чтобы реализовать приложения имитации устройства и приложение службы, на которых будет выполнено задание."
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
ms.openlocfilehash: 42e594dc6a8a8be619b5652bf8e44cf883650489
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="c9541-104">Планирование и трансляция заданий (Node)</span><span class="sxs-lookup"><span data-stu-id="c9541-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="c9541-105">Центр Интернета вещей Azure — это полностью управляемая служба, которая позволяет внутреннему приложению создавать и отслеживать задания, осуществляющие планирование и обновление миллионов устройств.</span><span class="sxs-lookup"><span data-stu-id="c9541-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="c9541-106">Задания можно использовать для следующих действий:</span><span class="sxs-lookup"><span data-stu-id="c9541-106">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="c9541-107">Обновление требуемых свойств</span><span class="sxs-lookup"><span data-stu-id="c9541-107">Update desired properties</span></span>
* <span data-ttu-id="c9541-108">Обновление тегов</span><span class="sxs-lookup"><span data-stu-id="c9541-108">Update tags</span></span>
* <span data-ttu-id="c9541-109">Вызов прямых методов</span><span class="sxs-lookup"><span data-stu-id="c9541-109">Invoke direct methods</span></span>

<span data-ttu-id="c9541-110">По сути, задание включает одно из этих действий, отслеживая ход его выполнения на наборе устройств (определяется запросом двойника устройства).</span><span class="sxs-lookup"><span data-stu-id="c9541-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="c9541-111">Например, с помощью задания внутреннее приложение может вызывать метод перезагрузки на 10 000 устройств, определенных запросом двойника устройства и запланированных в будущем.</span><span class="sxs-lookup"><span data-stu-id="c9541-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="c9541-112">Затем это приложение может отследить ход выполнения задания по мере получения и выполнения метода Reboot на каждом из этих устройств.</span><span class="sxs-lookup"><span data-stu-id="c9541-112">That application can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="c9541-113">Дополнительные сведения о каждой из этих возможностей см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c9541-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="c9541-114">Двойники устройств и свойства: [Приступая к работе с двойниками устройств (предварительная версия)][lnk-get-started-twin] и [Руководство. Настройка устройств с помощью требуемых свойств (предварительная версия)][lnk-twin-props].</span><span class="sxs-lookup"><span data-stu-id="c9541-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="c9541-115">Прямые методы: [Вызов прямого метода на устройстве (предварительная версия)][lnk-dev-methods] и [Руководство. Использование прямых методов][lnk-c2d-methods].</span><span class="sxs-lookup"><span data-stu-id="c9541-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="c9541-116">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="c9541-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="c9541-117">Создание приложения имитации устройства с прямым методом, который позволяет выполнить действие **lockDoor** путем вызова из серверной части решения.</span><span class="sxs-lookup"><span data-stu-id="c9541-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the solution back end.</span></span>
* <span data-ttu-id="c9541-118">Создание консольного приложения Node.js, которое с помощью задания вызывает в приложении имитации устройства прямой метод **lockDoor** и обновляет требуемые свойства с помощью задания устройства.</span><span class="sxs-lookup"><span data-stu-id="c9541-118">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="c9541-119">По завершении работы с этим руководством у вас будет два консольных приложения Node.js:</span><span class="sxs-lookup"><span data-stu-id="c9541-119">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="c9541-120">**simDevice.js**, которое подключается к Центру Интернета вещей с удостоверением устройства и получает прямой метод **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="c9541-120">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="c9541-121">**scheduleJobService.js**, которое вызывает прямой метод в приложении для имитации устройства и обновляет требуемые свойства двойника устройства с помощью задания.</span><span class="sxs-lookup"><span data-stu-id="c9541-121">**scheduleJobService.js**, which calls a direct method in the simulated device app and update the device twin's desired properties using a job.</span></span>

<span data-ttu-id="c9541-122">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="c9541-122">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="c9541-123">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="c9541-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="c9541-124">В статье [Prepare your development environment][lnk-dev-setup] (Подготовка среды разработки) описывается, как установить Node.js для работы с этим учебником в ОС Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="c9541-124">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c9541-125">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c9541-125">An active Azure account.</span></span> <span data-ttu-id="c9541-126">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c9541-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c9541-127">Создание приложения виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="c9541-127">Create a simulated device app</span></span>
<span data-ttu-id="c9541-128">В этом разделе вы создадите консольное приложение Node.js, которое отвечает на прямой метод, вызываемый из облака. Этот метод запускает перезагрузку имитации устройства и использует сообщаемые свойства для определения устройств и времени их последней перезагрузки в запросах двойников устройства.</span><span class="sxs-lookup"><span data-stu-id="c9541-128">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="c9541-129">Создайте пустую папку с именем **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="c9541-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="c9541-130">В папке **simDevice** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="c9541-130">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="c9541-131">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c9541-131">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="c9541-132">В командной строке в папке **simDevice** выполните следующую команду, чтобы установить пакет SDK для устройств **azure-iot-device** и пакет **azure-iot-device-mqtt**.</span><span class="sxs-lookup"><span data-stu-id="c9541-132">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="c9541-133">В текстовом редакторе создайте файл **simDevice.js** в папке **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="c9541-133">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>
4. <span data-ttu-id="c9541-134">Добавьте следующие инструкции require в начало файла **simDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="c9541-134">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="c9541-135">Добавьте переменную **connectionString**, чтобы создать с ее помощью экземпляр **клиента**.</span><span class="sxs-lookup"><span data-stu-id="c9541-135">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="c9541-136">Добавьте следующую функцию для обработки метода **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="c9541-136">Add the following function to handle the **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="c9541-137">Добавьте следующий код для регистрации обработчика для метода **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="c9541-137">Add the following code to register the handler for the **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="c9541-138">Сохраните и закройте файл **simDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="c9541-138">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="c9541-139">Для простоты в этом руководстве не реализуются политики повтора.</span><span class="sxs-lookup"><span data-stu-id="c9541-139">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c9541-140">В рабочем коде следует реализовать политики повторных попыток (например, с экспоненциальной задержкой), как указано в статье [Обработка временного сбоя][lnk-transient-faults] на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="c9541-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="c9541-141">Планирование заданий для вызова прямого метода и обновления свойств двойника устройства</span><span class="sxs-lookup"><span data-stu-id="c9541-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="c9541-142">В этом разделе создается консольное приложение Node.js, которое инициирует удаленное действие **lockDoor** на устройстве с помощью прямого метода и обновляет свойства двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="c9541-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="c9541-143">Создайте пустую папку с именем **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="c9541-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="c9541-144">В папке **scheduleJobService** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="c9541-144">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="c9541-145">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c9541-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="c9541-146">В командной строке в папке **scheduleJobService** выполните следующую команду, чтобы установить пакет SDK для устройств **azure-iothub** и пакет **azure-iot-device-mqtt**.</span><span class="sxs-lookup"><span data-stu-id="c9541-146">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="c9541-147">В текстовом редакторе создайте файл **scheduleJobService.js** в папке **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="c9541-147">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="c9541-148">Добавьте следующие инструкции require в начале файла **dmpatterns_gscheduleJobServiceetstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="c9541-148">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="c9541-149">Добавьте следующие объявления переменных и замените значения заполнителей:</span><span class="sxs-lookup"><span data-stu-id="c9541-149">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="c9541-150">Добавьте следующую функцию, которая будет использоваться для отслеживания процесса выполнения задания:</span><span class="sxs-lookup"><span data-stu-id="c9541-150">Add the following function that will be used to monitor the execution of the job:</span></span>
   
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
7. <span data-ttu-id="c9541-151">Добавьте следующий код, чтобы запланировать задание, которое вызывает метод устройства:</span><span class="sxs-lookup"><span data-stu-id="c9541-151">Add the following code to schedule the job that calls the device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable to process method
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
8. <span data-ttu-id="c9541-152">Добавьте следующий код, чтобы запланировать задание, которое обновляет двойник устройства:</span><span class="sxs-lookup"><span data-stu-id="c9541-152">Add the following code to schedule the job to update the device twin:</span></span>
   
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
9. <span data-ttu-id="c9541-153">Сохраните и закройте файл **scheduleJobService.js**.</span><span class="sxs-lookup"><span data-stu-id="c9541-153">Save and close the **scheduleJobService.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="c9541-154">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="c9541-154">Run the applications</span></span>
<span data-ttu-id="c9541-155">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="c9541-155">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="c9541-156">В командной строке в папке **simDevice** выполните следующую команду, чтобы начать прослушивание прямого метода перезагрузки:</span><span class="sxs-lookup"><span data-stu-id="c9541-156">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="c9541-157">В командной строке в папке **scheduleJobService** выполните следующую команду, чтобы активировать задачи для блокировки дверей и обновления двойника.</span><span class="sxs-lookup"><span data-stu-id="c9541-157">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="c9541-158">В консоли отобразится ответ устройства на прямой метод.</span><span class="sxs-lookup"><span data-stu-id="c9541-158">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9541-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9541-159">Next steps</span></span>
<span data-ttu-id="c9541-160">В этом учебнике описано использование задания для планирования прямого метода на устройстве и обновления свойств двойника устройства.</span><span class="sxs-lookup"><span data-stu-id="c9541-160">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="c9541-161">Чтобы продолжить знакомство с Центром Интернета вещей и шаблонами управления устройствами, такими как удаленное обновление встроенного ПО, см. следующие материалы:</span><span class="sxs-lookup"><span data-stu-id="c9541-161">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="c9541-162">[Учебник. Обновление встроенного ПО][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="c9541-162">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="c9541-163">Чтобы продолжить знакомство с Центром Интернета вещей, см. сведения в статье [Приступая к работе с архитектурой Edge Интернета вещей в Linux][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="c9541-163">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
