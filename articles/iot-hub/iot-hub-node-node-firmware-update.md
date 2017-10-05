---
title: "Обновление встроенного ПО устройства c помощью Центра Интернета вещей Azure (Node) | Документация Майкрософт"
description: "Запуск обновления встроенного ПО устройства с помощью функции управления устройствами в Центре Интернета вещей. Используйте пакеты SDK для Центра Интернета вещей Azure для Node.js, чтобы реализовать приложение имитации устройства и приложение службы, которое активирует обновление встроенного ПО."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 350cf1cbec8847d1bbf29814435502af6f098e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="de6e8-104">Используйте управление устройствами, чтобы запустить обновление встроенного ПО устройства (Node/Node).</span><span class="sxs-lookup"><span data-stu-id="de6e8-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="de6e8-105">Введение</span><span class="sxs-lookup"><span data-stu-id="de6e8-105">Introduction</span></span>
<span data-ttu-id="de6e8-106">В статье [Приступая к работе с функцией управления устройствами центра IoT Azure с использованием C# (предварительная версия)][lnk-dm-getstarted] вы узнали, как использовать [двойник устройства][lnk-devtwin] и [прямые методы][lnk-c2dmethod] для удаленной перезагрузки устройства.</span><span class="sxs-lookup"><span data-stu-id="de6e8-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="de6e8-107">В этом руководстве используются те же примитивы Центра Интернета вещей, а также содержатся рекомендации по комплексному обновлению имитации встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="de6e8-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="de6e8-108">Этот шаблон используется в реализации обновления встроенного ПО для примера устройства Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="de6e8-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="de6e8-109">В этом учебнике описаны следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="de6e8-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="de6e8-110">Создание консольного приложения Node.js, вызывающего прямой метод firmwareUpdate в приложении имитации устройства с помощью Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="de6e8-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="de6e8-111">Создайте приложение виртуального устройства, которое реализует прямой метод **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="de6e8-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="de6e8-112">Этот метод запускает многоэтапный процесс, который сначала ожидает скачивания образа встроенного ПО, а затем скачивает его и применяет.</span><span class="sxs-lookup"><span data-stu-id="de6e8-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="de6e8-113">В ходе выполнения каждого этапа обновления устройство использует сообщаемые свойства для продолжения процесса.</span><span class="sxs-lookup"><span data-stu-id="de6e8-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="de6e8-114">По завершении работы с этим руководством у вас будет два консольных приложения Node.js:</span><span class="sxs-lookup"><span data-stu-id="de6e8-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="de6e8-115">**dmpatterns_fwupdate_service.js**, которое вызывает прямой метод в приложении для имитации устройства, выводит ответ и периодически (каждые 500 миллисекунд) отображает обновленные сообщаемые свойства.</span><span class="sxs-lookup"><span data-stu-id="de6e8-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="de6e8-116">**dmpatterns_fwupdate_device.js**, которое подключается к Центру Интернета вещей с использованием удостоверения устройства, созданного ранее, получает прямой метод firmwareUpdate, запускает процесс с несколькими состояниями для имитации обновления встроенного ПО, состоящий из нескольких этапов (ожидание скачивания образа, скачивание нового образа и применение образа).</span><span class="sxs-lookup"><span data-stu-id="de6e8-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="de6e8-117">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="de6e8-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="de6e8-118">Node.js версии 0.12.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="de6e8-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="de6e8-119">В статье [Prepare your development environment][lnk-dev-setup] (Подготовка среды разработки) описывается, как установить Node.js для работы с этим учебником в ОС Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="de6e8-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="de6e8-120">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="de6e8-120">An active Azure account.</span></span> <span data-ttu-id="de6e8-121">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="de6e8-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="de6e8-122">Следуйте указаниям статьи [Руководство по началу работы с управлением устройствами](iot-hub-node-node-device-management-get-started.md), чтобы создать Центр Интернета вещей и получить строку подключения Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="de6e8-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="de6e8-123">Активация удаленного обновления встроенного ПО на устройстве с помощью прямого метода</span><span class="sxs-lookup"><span data-stu-id="de6e8-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="de6e8-124">В этом разделе вы создадите консольное приложение Node.js, которое инициирует удаленное обновление встроенного ПО на устройстве.</span><span class="sxs-lookup"><span data-stu-id="de6e8-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="de6e8-125">Приложение использует прямой метод для запуска обновления, а также применяет запросы двойников устройства для периодического получения состояния обновления активного встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="de6e8-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="de6e8-126">Создайте пустую папку с именем **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="de6e8-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="de6e8-127">В папке **triggerfwupdateondevice** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="de6e8-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="de6e8-128">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="de6e8-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="de6e8-129">В командной строке в папке **triggerfwupdateondevice** выполните следующую команду, чтобы установить пакеты SDK для устройств **azure-iothub** и пакет **azure-iot-device-mqtt**.</span><span class="sxs-lookup"><span data-stu-id="de6e8-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="de6e8-130">В текстовом редакторе создайте файл **dmpatterns_etstarted_service.js** в папке **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="de6e8-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="de6e8-131">Добавьте следующие инструкции require в начале файла **dmpatterns_getstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="de6e8-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="de6e8-132">Добавьте следующие объявления переменных и замените значения заполнителей:</span><span class="sxs-lookup"><span data-stu-id="de6e8-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="de6e8-133">Добавьте следующую функцию, чтобы найти и отобразить значение сообщаемого свойства firmwareUpdate.</span><span class="sxs-lookup"><span data-stu-id="de6e8-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="de6e8-134">Добавьте следующую функцию, чтобы вызвать метод firmwareUpdate для перезагрузки целевого устройства:</span><span class="sxs-lookup"><span data-stu-id="de6e8-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="de6e8-135">Наконец, добавьте следующую функцию в код, чтобы запустить последовательность обновления встроенного ПО и периодическое отображение сообщаемых свойств:</span><span class="sxs-lookup"><span data-stu-id="de6e8-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="de6e8-136">Сохраните и закройте файл **dmpatterns_fwupdate_service.js**.</span><span class="sxs-lookup"><span data-stu-id="de6e8-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="de6e8-137">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="de6e8-137">Run the apps</span></span>
<span data-ttu-id="de6e8-138">Теперь все готово к запуску приложений.</span><span class="sxs-lookup"><span data-stu-id="de6e8-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="de6e8-139">В командной строке в папке **manageddevice** выполните следующую команду, чтобы начать прослушивание прямого метода перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="de6e8-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="de6e8-140">В командной строке в папке **triggerfwupdateondevice** выполните следующую команду, чтобы активировать удаленную перезагрузку и выполнить запрос к двойнику устройства для поиска значения времени последней перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="de6e8-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="de6e8-141">В консоли отобразится ответ устройства на прямой метод.</span><span class="sxs-lookup"><span data-stu-id="de6e8-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de6e8-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de6e8-142">Next steps</span></span>
<span data-ttu-id="de6e8-143">В этом руководстве вы использовали прямой метод для активации удаленного обновления встроенного ПО на устройстве. Также вы использовали переданные свойства для отслеживания хода обновления встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="de6e8-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="de6e8-144">Дополнительные сведения о расширении решения Центра Интернета вещей и планировании вызовов методов на нескольких устройствах см. в учебнике [Планирование и трансляция заданий][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="de6e8-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
