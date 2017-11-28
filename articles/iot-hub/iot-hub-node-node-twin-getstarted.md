---
title: "Начало работы с двойниками устройств Центра Интернета вещей (Node) | Документация Майкрософт"
description: "Добавление тегов и последующее использование запроса Центра Интернета вещей с помощью двойников устройств Центра Интернета вещей. Используйте пакеты SDK для Центра Интернета вещей Azure для Node.js, чтобы реализовать приложение имитации устройства и приложение службы, которое добавит теги, и выполнить запрос Центра Интернета вещей."
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
ms.openlocfilehash: 633c9fd4f8a1d017d93148f8c2e860ccba14238c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="bee07-104">Начало работы с двойниками устройств (Node)</span><span class="sxs-lookup"><span data-stu-id="bee07-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="bee07-105">По завершении работы с этим руководством у вас будет два консольных приложения Node.js:</span><span class="sxs-lookup"><span data-stu-id="bee07-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="bee07-106">**AddTagsAndQuery.js** — это внутреннее приложение Node.js, которое добавляет теги и выполняет запросы к двойникам устройств.</span><span class="sxs-lookup"><span data-stu-id="bee07-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="bee07-107">**TwinSimulatedDevice.js** — это приложение Node.js, которое имитирует устройство, подключающееся к Центру Интернета вещей с использованием удостоверения устройства, созданного ранее, и сообщает о его условии подключения.</span><span class="sxs-lookup"><span data-stu-id="bee07-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="bee07-108">Статья [IoT Hub SDKs][lnk-hub-sdks] (Пакеты SDK для Центра Интернета вещей) содержит сведения о разных пакетах SDK для Azure IoT, с помощью которых можно создать приложения для устройств и внутренние приложения.</span><span class="sxs-lookup"><span data-stu-id="bee07-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="bee07-109">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="bee07-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="bee07-110">Node.js версии 0.10.x или более поздней.</span><span class="sxs-lookup"><span data-stu-id="bee07-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="bee07-111">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="bee07-111">An active Azure account.</span></span> <span data-ttu-id="bee07-112">Если ее нет, можно создать [бесплатную учетную запись][lnk-free-trial] всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="bee07-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="bee07-113">Создание приложения службы</span><span class="sxs-lookup"><span data-stu-id="bee07-113">Create the service app</span></span>
<span data-ttu-id="bee07-114">В этом разделе вы создадите консольное приложение Node.js, которое добавляет метаданные расположения в двойник устройства, связанный с **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="bee07-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="bee07-115">После этого оно запрашивает данные двойников устройств, хранящихся в Центре Интернета вещей, выбирает устройства, находящиеся в США, а затем те, которые сообщили о подключении по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="bee07-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="bee07-116">Создайте пустую папку с именем **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="bee07-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="bee07-117">В папке **addtagsandqueryapp** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="bee07-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="bee07-118">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="bee07-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="bee07-119">В командной строке в папке **addtagsandqueryapp** выполните следующую команду, чтобы установить пакет **azure-iothub**.</span><span class="sxs-lookup"><span data-stu-id="bee07-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="bee07-120">В текстовом редакторе создайте файл **AddTagsAndQuery.js** в папке **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="bee07-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="bee07-121">Добавьте следующий код в файл **AddTagsAndQuery.js** и замените заполнитель **{iot hub connection string}** на строку подключения Центра Интернета вещей, скопированную при создании центра:</span><span class="sxs-lookup"><span data-stu-id="bee07-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
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
   
    <span data-ttu-id="bee07-122">Объект **Registry** позволяет получить все методы, необходимые для взаимодействия с двойниками устройства из службы.</span><span class="sxs-lookup"><span data-stu-id="bee07-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="bee07-123">Предыдущий код сначала инициализирует объект **Registry**, затем извлекает двойник устройства для **myDeviceId** и, наконец, обновляет его теги, используя сведения о требуемом расположении.</span><span class="sxs-lookup"><span data-stu-id="bee07-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="bee07-124">После обновления тегов он вызывает функцию **queryTwins**.</span><span class="sxs-lookup"><span data-stu-id="bee07-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="bee07-125">Добавьте следующий код в конце файла **AddTagsAndQuery.js** для реализации функции **queryTwins**:</span><span class="sxs-lookup"><span data-stu-id="bee07-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="bee07-126">Предыдущий код выполняет два запроса: первый выбирает только двойников устройства, расположенных на фабрике **Redmond43**, а второй уточняет условия первого запроса и выбирает устройства, подключенные по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="bee07-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="bee07-127">Обратите внимание, что при создании объекта **query** предыдущий код указывает максимальное количество возвращаемых документов.</span><span class="sxs-lookup"><span data-stu-id="bee07-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="bee07-128">Объект **query** содержит логическое свойство **hasMoreResults**, которое можно использовать для вызова методов **nextAsTwin** несколько раз, чтобы получить все результаты.</span><span class="sxs-lookup"><span data-stu-id="bee07-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="bee07-129">Метод **next** доступен для результатов, которые не являются двойниками устройств, например результаты статистических запросов.</span><span class="sxs-lookup"><span data-stu-id="bee07-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="bee07-130">Запустите приложение, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bee07-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="bee07-131">В результатах запроса на все устройства, расположенные на фабрике **Redmond43**, отобразится одно устройство, а для запроса на ограничение результатов устройствами, использующими сеть мобильной связи, не отобразится ни одного устройства.</span><span class="sxs-lookup"><span data-stu-id="bee07-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="bee07-132">В следующем разделе вы создадите приложение устройства, которое сообщает сведения о подключении и изменяет результат запроса в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="bee07-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="bee07-133">Создание приложения устройства</span><span class="sxs-lookup"><span data-stu-id="bee07-133">Create the device app</span></span>
<span data-ttu-id="bee07-134">В этом разделе вы создадите консольное приложение Node.js, которое подключается к центру как **myDeviceId** и обновляет сообщаемые свойства двойника устройства, добавив в них сведения о подключении по сети мобильной связи.</span><span class="sxs-lookup"><span data-stu-id="bee07-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="bee07-135">На данный момент доступ к двойникам устройств можно получить только на устройствах, подключающихся к Центру Интернета вещей по протоколу MQTT.</span><span class="sxs-lookup"><span data-stu-id="bee07-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="bee07-136">Инструкции по преобразованию существующего приложения устройства для использования MQTT см. в статье [Поддержка MQTT в Центре Интернета вещей][lnk-devguide-mqtt].</span><span class="sxs-lookup"><span data-stu-id="bee07-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="bee07-137">Создайте пустую папку с именем **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="bee07-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="bee07-138">В папке **reportconnectivity** создайте файл package.json, используя следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="bee07-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="bee07-139">Примите значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="bee07-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="bee07-140">В командной строке в папке **reportconnectivity** выполните следующую команду, чтобы установить пакет SDK для устройств **azure-iot-device** и пакет **azure-iot-device-mqtt**.</span><span class="sxs-lookup"><span data-stu-id="bee07-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="bee07-141">В текстовом редакторе создайте файл **ReportConnectivity.js** в папке **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="bee07-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="bee07-142">Добавьте следующий код в файл **ReportConnectivity.js** и замените заполнитель **{device connection string}** строкой подключения устройства, скопированной при создании удостоверения устройства **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="bee07-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="bee07-143">Объект **Client** позволяет получить все методы, необходимые для взаимодействия с двойниками устройства с устройства.</span><span class="sxs-lookup"><span data-stu-id="bee07-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="bee07-144">После инициализации объекта **Client** предыдущий код извлекает двойник устройства для **myDeviceId** и обновляет его сообщаемое свойство, используя сведения о подключении.</span><span class="sxs-lookup"><span data-stu-id="bee07-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="bee07-145">Запуск приложения устройства</span><span class="sxs-lookup"><span data-stu-id="bee07-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="bee07-146">Отобразится сообщение `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="bee07-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="bee07-147">Теперь, когда устройство сообщило сведения о подключении, оно должно появиться в обоих запросах.</span><span class="sxs-lookup"><span data-stu-id="bee07-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="bee07-148">Вернитесь к папке **addtagsandqueryapp** и выполните запросы снова:</span><span class="sxs-lookup"><span data-stu-id="bee07-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="bee07-149">На этот раз **myDeviceId** должен появиться в результатах обоих запросов.</span><span class="sxs-lookup"><span data-stu-id="bee07-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="bee07-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bee07-150">Next steps</span></span>
<span data-ttu-id="bee07-151">В этом руководстве мы настроили новый Центр Интернета вещей на портале Azure и создали удостоверение устройства в реестре удостоверений Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="bee07-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="bee07-152">Вы добавили метаданные устройства в качестве тегов из внутреннего приложения и написали код приложения имитации устройства, чтобы сообщить сведения о подключении в двойнике устройства.</span><span class="sxs-lookup"><span data-stu-id="bee07-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="bee07-153">Вы также узнали, как запрашивать эти сведения, используя похожий на SQL язык запросов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="bee07-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="bee07-154">Ознакомьтесь со следующими материалами, чтобы узнать как:</span><span class="sxs-lookup"><span data-stu-id="bee07-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="bee07-155">отправить данные телеметрии с устройств (учебник [Приступая к работе с Центром Интернета вещей Azure (Node)][lnk-iothub-getstarted]);</span><span class="sxs-lookup"><span data-stu-id="bee07-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="bee07-156">настроить устройства с помощью требуемых свойств двойника устройства ([Руководство. Настройка устройств с помощью требуемых свойств (предварительная версия)][lnk-twin-how-to-configure]);</span><span class="sxs-lookup"><span data-stu-id="bee07-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="bee07-157">управлять устройствами в интерактивном режиме, например включить вентилятор из управляемого пользователем приложения (учебник [Use direct methods][lnk-methods-tutorial] (Использование прямых методов)).</span><span class="sxs-lookup"><span data-stu-id="bee07-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
