---
title: "aaaGet к работе с близнецы устройства Azure IoT Hub (узел) | Документы Microsoft"
description: "Как tooadd близнецы устройства Azure IoT Hub toouse теги и затем использовать запрос центр IoT. Можно использовать hello Azure IoT пакетов SDK для Node.js tooimplement hello имитированное устройство приложения и приложение службы, которое добавляет теги hello и запускает hello центра IoT запроса."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="e7139-104">Начало работы с двойниками устройств (Node)</span><span class="sxs-lookup"><span data-stu-id="e7139-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="e7139-105">В конце этого учебника hello будет иметь два Node.js консольные приложения:</span><span class="sxs-lookup"><span data-stu-id="e7139-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="e7139-106">**AddTagsAndQuery.js** — это внутреннее приложение Node.js, которое добавляет теги и выполняет запросы к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="e7139-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="e7139-107">**TwinSimulatedDevice.js**, приложение Node.js, которое имитирует устройство, соединяющее центра IoT tooyour с идентификатором hello устройства, созданного ранее и сообщает о условия его подключения.</span><span class="sxs-lookup"><span data-stu-id="e7139-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="e7139-108">статья Hello [пакеты SDK Azure IoT] [ lnk-hub-sdks] предоставляет сведения о hello Azure IoT пакетов SDK, которые можно использовать toobuild устройства и серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="e7139-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="e7139-109">toocomplete этого учебника требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e7139-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="e7139-110">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e7139-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="e7139-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e7139-111">An active Azure account.</span></span> <span data-ttu-id="e7139-112">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e7139-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="e7139-113">Создание приложения hello службы</span><span class="sxs-lookup"><span data-stu-id="e7139-113">Create hello service app</span></span>
<span data-ttu-id="e7139-114">В этом разделе создайте Node.js консольное приложение, которое добавляет связанные с устройством двойных расположение метаданных toohello **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="e7139-114">In this section, you create a Node.js console app that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="e7139-115">Затем выполняется запрос близнецы hello устройства хранится в центр IoT hello, выбрав hello устройствах, находящихся в hello нам и Здравствуйте, те, которые подчиняются сотовой связи.</span><span class="sxs-lookup"><span data-stu-id="e7139-115">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="e7139-116">Создайте пустую папку с именем **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="e7139-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="e7139-117">В hello **addtagsandqueryapp** папки, создайте новый файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="e7139-117">In hello **addtagsandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e7139-118">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="e7139-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e7139-119">В командной строке в hello **addtagsandqueryapp** папку, следующая команда tooinstall hello hello **центром IOT azure** пакета:</span><span class="sxs-lookup"><span data-stu-id="e7139-119">At your command prompt in hello **addtagsandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="e7139-120">В текстовом редакторе создайте новый **AddTagsAndQuery.js** файла в hello **addtagsandqueryapp** папки.</span><span class="sxs-lookup"><span data-stu-id="e7139-120">Using a text editor, create a new **AddTagsAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="e7139-121">Добавьте следующий код toohello hello **AddTagsAndQuery.js** файл и замените hello **{строка подключения концентратора iot}** заполнитель строки подключения центра IoT вы скопировали, когда вы создали концентратор приветствия:</span><span class="sxs-lookup"><span data-stu-id="e7139-121">Add hello following code toohello **AddTagsAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="e7139-122">Hello **реестра** объект предоставляет все необходимые toointeract hello методы с близнецы устройства из службы hello.</span><span class="sxs-lookup"><span data-stu-id="e7139-122">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="e7139-123">Предыдущий код Hello сначала инициализирует hello **реестра** объекта, а затем извлекает hello двойных устройства для **myDeviceId**и наконец обновляет сведения о расположении hello требуемого этим тегам.</span><span class="sxs-lookup"><span data-stu-id="e7139-123">hello previous code first initializes hello **Registry** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="e7139-124">После hello обновление hello его теги hello вызовов **queryTwins** функции.</span><span class="sxs-lookup"><span data-stu-id="e7139-124">After hello updating hello tags it calls hello **queryTwins** function.</span></span>
5. <span data-ttu-id="e7139-125">Добавьте следующий код в конце hello hello **AddTagsAndQuery.js** tooimplement hello **queryTwins** функции:</span><span class="sxs-lookup"><span data-stu-id="e7139-125">Add hello following code at hello end of  **AddTagsAndQuery.js** tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="e7139-126">Предыдущий код Hello выполняет два запроса: hello сначала выделяются hello близнецы устройств для устройств, расположенных в hello **Redmond43** здания, сооружения и hello второй уточняет hello запроса tooselect только hello устройства, подключенные через также сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="e7139-126">hello previous code executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="e7139-127">Обратите внимание, что предыдущего код hello, при создании hello **запроса** объекта, указывает максимальное количество возвращенных документов.</span><span class="sxs-lookup"><span data-stu-id="e7139-127">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="e7139-128">Hello **запроса** объект содержит **hasMoreResults** логического свойства, которые можно использовать tooinvoke hello **nextAsTwin** методы приводит все tooretrieve несколько раз.</span><span class="sxs-lookup"><span data-stu-id="e7139-128">hello **query** object contains a **hasMoreResults** boolean property that you can use tooinvoke hello **nextAsTwin** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="e7139-129">Метод **next** доступен для результатов, которые не являются двойниками устройств, например результаты статистических запросов.</span><span class="sxs-lookup"><span data-stu-id="e7139-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="e7139-130">Запустите приложение hello с:</span><span class="sxs-lookup"><span data-stu-id="e7139-130">Run hello application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="e7139-131">Вы увидите одно устройство в результатах hello для hello запрос запросом для всех устройств, расположенных в **Redmond43** и для hello запрос, который ограничивает hello нет результатов toodevices используемой сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="e7139-131">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="e7139-132">В следующем разделе hello создается приложение устройства, которое сообщает сведения о подключении hello и изменения hello результат запроса hello в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="e7139-132">In hello next section you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="e7139-133">Создание приложения hello устройства</span><span class="sxs-lookup"><span data-stu-id="e7139-133">Create hello device app</span></span>
<span data-ttu-id="e7139-134">В этом разделе создайте консольное приложение Node.js, которое подключается tooyour концентратора, **myDeviceId**и затем обновления, его устройство двойных сообщила свойства toocontain hello сведения, что она подключена с помощью сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="e7139-134">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its device twin's reported properties toocontain hello information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="e7139-135">В настоящее время устройство близнецы доступны только из устройств, которые подключаются tooIoT концентратора с помощью протокола MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="e7139-135">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="e7139-136">См. toohello [поддержки MQTT] [ lnk-devguide-mqtt] статье инструкции о том, как приложение toouse tooconvert существующие устройства MQTT.</span><span class="sxs-lookup"><span data-stu-id="e7139-136">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

1. <span data-ttu-id="e7139-137">Создайте пустую папку с именем **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="e7139-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="e7139-138">В hello **reportconnectivity** папки, создайте новый файл package.json, используя следующую команду в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="e7139-138">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e7139-139">Примите все значения по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="e7139-139">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e7139-140">В командной строке в hello **reportconnectivity** папку, следующая команда tooinstall hello hello **azure iot устройства**, и **azure iot устройства mqtt** пакета :</span><span class="sxs-lookup"><span data-stu-id="e7139-140">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="e7139-141">В текстовом редакторе создайте новый **ReportConnectivity.js** файла в hello **reportconnectivity** папки.</span><span class="sxs-lookup"><span data-stu-id="e7139-141">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="e7139-142">Добавьте следующий код toohello hello **ReportConnectivity.js** файл и замените hello **{строка подключения устройства}** заполнитель со строкой подключения устройства hello, скопированный во время создания hello **myDeviceId** удостоверение устройства:</span><span class="sxs-lookup"><span data-stu-id="e7139-142">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="e7139-143">Hello **клиента** объект представляет все методы hello, требующих toointeract с близнецы устройства с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="e7139-143">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="e7139-144">Здравствуйте предыдущего кода после инициализации hello **клиента** объекта извлекает hello двойных устройства для **myDeviceId** и обновляет сведения о подключении hello свойства отчета.</span><span class="sxs-lookup"><span data-stu-id="e7139-144">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
5. <span data-ttu-id="e7139-145">Выполните приложение hello устройства</span><span class="sxs-lookup"><span data-stu-id="e7139-145">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="e7139-146">Должно появиться сообщение hello `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="e7139-146">You should see hello message `twin state reported`.</span></span>
6. <span data-ttu-id="e7139-147">Теперь, когда hello устройство сообщило его сведения о соединении, он должен отображаться в обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="e7139-147">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="e7139-148">Перейдите обратно в hello **addtagsandqueryapp** hello папку и запустите запрос еще раз:</span><span class="sxs-lookup"><span data-stu-id="e7139-148">Go back in hello **addtagsandqueryapp** folder and run hello queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="e7139-149">На этот раз **myDeviceId** должен появиться в результатах обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="e7139-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="e7139-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7139-150">Next steps</span></span>
<span data-ttu-id="e7139-151">В этом учебнике настроен центр IoT в hello портал Azure и затем создать удостоверение устройства в реестре удостоверений центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="e7139-151">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="e7139-152">Добавить метаданные устройства как теги из серверной части приложения, а написал имитированное устройство приложения tooreport подключения сведений об устройстве в двойных hello устройства.</span><span class="sxs-lookup"><span data-stu-id="e7139-152">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="e7139-153">Вы также узнали, каким образом tooquery эти сведения, с помощью языка запросов SQL-подобного центра IoT hello.</span><span class="sxs-lookup"><span data-stu-id="e7139-153">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="e7139-154">Hello используйте следующие ресурсы toolearn как для:</span><span class="sxs-lookup"><span data-stu-id="e7139-154">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="e7139-155">Отправка данных телеметрии с устройствами с помощью hello [приступить к работе с центром IoT] [ lnk-iothub-getstarted] учебника</span><span class="sxs-lookup"><span data-stu-id="e7139-155">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="e7139-156">Настройка устройств с нужными свойствами устройства двойных hello [используйте требуемого свойства устройства tooconfigure] [ lnk-twin-how-to-configure] учебника</span><span class="sxs-lookup"><span data-stu-id="e7139-156">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="e7139-157">Управление устройствами интерактивно (такие как включение вентилятор из управляемой пользователем приложения), с hello [использовать прямые методы] [ lnk-methods-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="e7139-157">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
