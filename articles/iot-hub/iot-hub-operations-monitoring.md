---
title: "Мониторинг операций Центра Интернета вещей Azure | Документация Майкрософт"
description: "Использование мониторинга операций Центра Интернета вещей Azure для отслеживания состояния операций Центра Интернета вещей в реальном времени."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="edffe-103">Мониторинг операций центра IoT</span><span class="sxs-lookup"><span data-stu-id="edffe-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="edffe-104">Мониторинг операций центра IoT позволяет отслеживать состояние операций в центре IoT в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="edffe-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="edffe-105">Центр Интернета вещей отслеживает события по нескольким категориям операций.</span><span class="sxs-lookup"><span data-stu-id="edffe-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="edffe-106">Вы можете выбрать отправку событий из одной или нескольких категорий в конечную точку Центра Интернета вещей для обработки.</span><span class="sxs-lookup"><span data-stu-id="edffe-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="edffe-107">Вы можете отслеживать данные на наличие ошибок или настроить более сложную обработку на основе закономерностей в данных.</span><span class="sxs-lookup"><span data-stu-id="edffe-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="edffe-108">Центр Интернета вещей отслеживает шесть категорий событий:</span><span class="sxs-lookup"><span data-stu-id="edffe-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="edffe-109">Операции с удостоверениями устройства</span><span class="sxs-lookup"><span data-stu-id="edffe-109">Device identity operations</span></span>
* <span data-ttu-id="edffe-110">Телеметрия устройства</span><span class="sxs-lookup"><span data-stu-id="edffe-110">Device telemetry</span></span>
* <span data-ttu-id="edffe-111">Получение сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="edffe-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="edffe-112">Подключения</span><span class="sxs-lookup"><span data-stu-id="edffe-112">Connections</span></span>
* <span data-ttu-id="edffe-113">Передача файлов</span><span class="sxs-lookup"><span data-stu-id="edffe-113">File uploads</span></span>
* <span data-ttu-id="edffe-114">Маршрутизация сообщений</span><span class="sxs-lookup"><span data-stu-id="edffe-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="edffe-115">Включение мониторинга операций</span><span class="sxs-lookup"><span data-stu-id="edffe-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="edffe-116">Создайте центр IoT.</span><span class="sxs-lookup"><span data-stu-id="edffe-116">Create an IoT hub.</span></span> <span data-ttu-id="edffe-117">Инструкции по созданию Центра Интернета вещей см. в руководстве [по началу работы][lnk-get-started].</span><span class="sxs-lookup"><span data-stu-id="edffe-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="edffe-118">Откройте колонку центра IoT.</span><span class="sxs-lookup"><span data-stu-id="edffe-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="edffe-119">В колонке щелкните **Мониторинг операций**.</span><span class="sxs-lookup"><span data-stu-id="edffe-119">From there, click **Operations monitoring**.</span></span>

    ![Доступ к конфигурации мониторинга операций на портале][1]

1. <span data-ttu-id="edffe-121">Выберите категории для наблюдения, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="edffe-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="edffe-122">События доступны для чтения из совместимой с концентраторами событий конечной точки, указанной в разделе **Параметры мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="edffe-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="edffe-123">Конечная точка центра IoT называется `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="edffe-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Настройка мониторинга операций в Центре Интернета вещей][2]

> [!NOTE]
> <span data-ttu-id="edffe-125">Если выбрать **Подробный** мониторинг для категории **Подключения**, то Центр Интернета вещей будет создавать дополнительные сообщения с диагностическими сведениями.</span><span class="sxs-lookup"><span data-stu-id="edffe-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="edffe-126">Для всех других категорий параметр **Подробный** изменяет количество сведений, которые Центр Интернета вещей включает в каждое сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="edffe-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="edffe-127">Категории событий и их использование</span><span class="sxs-lookup"><span data-stu-id="edffe-127">Event categories and how to use them</span></span>

<span data-ttu-id="edffe-128">Каждая категория мониторинга операций отслеживает отдельный тип взаимодействия с центром IoT и имеет схему, которая определяет способ структурирования событий в этой категории.</span><span class="sxs-lookup"><span data-stu-id="edffe-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="edffe-129">Операции с удостоверениями устройства</span><span class="sxs-lookup"><span data-stu-id="edffe-129">Device identity operations</span></span>

<span data-ttu-id="edffe-130">Категория операций с удостоверениями устройств отслеживает ошибки, возникающие, когда вы пытаетесь создать, обновить или удалить запись реестра удостоверений центра IoT.</span><span class="sxs-lookup"><span data-stu-id="edffe-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="edffe-131">Отслеживание этой категории целесообразно для сценариев подготовки.</span><span class="sxs-lookup"><span data-stu-id="edffe-131">Tracking this category is useful for provisioning scenarios.</span></span>

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a><span data-ttu-id="edffe-132">Телеметрия устройства</span><span class="sxs-lookup"><span data-stu-id="edffe-132">Device telemetry</span></span>

<span data-ttu-id="edffe-133">Категория телеметрии устройств отслеживает ошибки, которые возникают в центре IoT и связаны с конвейером телеметрии.</span><span class="sxs-lookup"><span data-stu-id="edffe-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="edffe-134">В эту категорию входят ошибки, возникающие при отправке событий телеметрии (например: регулирование) и при получении событий телеметрии (например: неавторизованный модуль чтения).</span><span class="sxs-lookup"><span data-stu-id="edffe-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="edffe-135">Эта категория не может перехватывать ошибки, которые вызваны кодом, выполняемым на самом устройстве.</span><span class="sxs-lookup"><span data-stu-id="edffe-135">This category cannot catch errors caused by code running on the device itself.</span></span>

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a><span data-ttu-id="edffe-136">Отправка команд из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="edffe-136">Cloud-to-device commands</span></span>

<span data-ttu-id="edffe-137">Категория отправки команд из облака на устройство отслеживает ошибки, которые возникают в Центре Интернета вещей и связаны с конвейером сообщений из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="edffe-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="edffe-138">В эту категорию входят ошибки, возникающие при отправке сообщений из облака на устройство (например, неавторизированный отправитель), при получении сообщений из облака на устройство (например, превышение числа доставок) и при получении отзыва на сообщение из облака на устройство (например, истечение срока действия отзыва).</span><span class="sxs-lookup"><span data-stu-id="edffe-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="edffe-139">Эта категория не перехватывает ошибки с устройства, которое неправильно обрабатывает сообщение из облака на устройство, если такое сообщение было успешно доставлено.</span><span class="sxs-lookup"><span data-stu-id="edffe-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a><span data-ttu-id="edffe-140">Подключения</span><span class="sxs-lookup"><span data-stu-id="edffe-140">Connections</span></span>

<span data-ttu-id="edffe-141">Категория подключений отслеживает ошибки, возникающие при подключении устройств к центру IoT или отключении от него.</span><span class="sxs-lookup"><span data-stu-id="edffe-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="edffe-142">Отслеживание этой категории полезно для определения попыток несанкционированных подключений и для отслеживания потери подключений к устройствам в областях с проблемами связи.</span><span class="sxs-lookup"><span data-stu-id="edffe-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a><span data-ttu-id="edffe-143">Передача файлов</span><span class="sxs-lookup"><span data-stu-id="edffe-143">File uploads</span></span>

<span data-ttu-id="edffe-144">Категория передачи файлов позволяет отслеживать ошибки, которые возникают в центре IoT и связаны с функцией передачи файлов.</span><span class="sxs-lookup"><span data-stu-id="edffe-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="edffe-145">В эту категорию входят:</span><span class="sxs-lookup"><span data-stu-id="edffe-145">This category includes:</span></span>

* <span data-ttu-id="edffe-146">ошибки, связанные с универсальным кодом ресурса (URI) SAS (например, если срок его действия истекает до того, как устройство уведомит центр о завершении передачи);</span><span class="sxs-lookup"><span data-stu-id="edffe-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="edffe-147">сбои передач, о которых сообщает устройство;</span><span class="sxs-lookup"><span data-stu-id="edffe-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="edffe-148">ошибки, связанные с отсутствием файла в хранилище при создании уведомления для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="edffe-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="edffe-149">Обратите внимание, что эта категория не может перехватывать ошибки, которые возникают, когда устройство непосредственно передает файл в хранилище.</span><span class="sxs-lookup"><span data-stu-id="edffe-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a><span data-ttu-id="edffe-150">Маршрутизация сообщений</span><span class="sxs-lookup"><span data-stu-id="edffe-150">Message routing</span></span>

<span data-ttu-id="edffe-151">Категория маршрутизации сообщений отслеживает ошибки, возникающие во время оценки маршрута сообщений и при определении состояния работоспособности конечной точки Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="edffe-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="edffe-152">В эту категорию входят следующие события: когда правило возвращает значение "Не определено", когда Центр Интернета вещей помечает конечную точку как неиспользуемую, а также любые другие ошибки, полученные от конечной точки.</span><span class="sxs-lookup"><span data-stu-id="edffe-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="edffe-153">Эта категория не содержит конкретных ошибок, связанных с самими сообщениями (например, ошибки регулирования устройств), которые попадают в категорию "телеметрии устройств".</span><span class="sxs-lookup"><span data-stu-id="edffe-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a><span data-ttu-id="edffe-154">Просмотр событий</span><span class="sxs-lookup"><span data-stu-id="edffe-154">View events</span></span>

<span data-ttu-id="edffe-155">Чтобы быстро проверить, что Центр Интернета вещей создает события мониторинга, можно использовать *iothub-explorer*.</span><span class="sxs-lookup"><span data-stu-id="edffe-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="edffe-156">Инструкции по его установке см. в репозитории GitHub [iothub-explorer][lnk-iothub-explorer].</span><span class="sxs-lookup"><span data-stu-id="edffe-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="edffe-157">Убедитесь, что на портале для категории мониторинга **Подключения** задано значение **Подробные сведения**.</span><span class="sxs-lookup"><span data-stu-id="edffe-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="edffe-158">В командной строке выполните следующую команду для чтения из конечной точки мониторинга:</span><span class="sxs-lookup"><span data-stu-id="edffe-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="edffe-159">В другой командной строке выполните следующую команду для имитации устройства, отправляющего сообщения в облако:</span><span class="sxs-lookup"><span data-stu-id="edffe-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="edffe-160">В первой командной строке события мониторинга отображаются после подключения имитированного устройства к Центру Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="edffe-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="edffe-161">Подключение к конечной точке мониторинга</span><span class="sxs-lookup"><span data-stu-id="edffe-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="edffe-162">Конечная точка мониторинга в Центре Интернета вещей совместима с концентраторами событий.</span><span class="sxs-lookup"><span data-stu-id="edffe-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="edffe-163">Чтобы считывать сообщения мониторинга из этой конечной точки, можно использовать любой механизм, который работает с концентраторами событий.</span><span class="sxs-lookup"><span data-stu-id="edffe-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="edffe-164">В этом примере создается базовый модуль чтения, который не подходит для развертывания с высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="edffe-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="edffe-165">Дополнительные сведения о способах обработки сообщений из концентраторов событий см. в руководстве [Приступая к работе с концентраторами событий][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="edffe-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="edffe-166">Чтобы подключиться к конечной точке мониторинга, потребуется строка подключения и имя конечной точки.</span><span class="sxs-lookup"><span data-stu-id="edffe-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="edffe-167">Ниже показано, как найти необходимые значения на портале.</span><span class="sxs-lookup"><span data-stu-id="edffe-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="edffe-168">На портале перейдите к колонке ресурсов Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="edffe-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="edffe-169">Выберите **Мониторинг операций** и запишите значения полей **Event Hub-compatible name** (Имя, совместимое с концентраторами событий) и **Event Hub-compatible endpoint** (Конечная точка, совместимая с концентраторами событий).</span><span class="sxs-lookup"><span data-stu-id="edffe-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Значения конечной точки, совместимой с концентраторами событий][img-endpoints]

1. <span data-ttu-id="edffe-171">Выберите **Политики общего доступа**, а затем — **служба**.</span><span class="sxs-lookup"><span data-stu-id="edffe-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="edffe-172">Запишите значение поля **Первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="edffe-172">Make a note of the **Primary key** value:</span></span>

    ![Первичный ключ политики общего доступа службы][img-service-key]

<span data-ttu-id="edffe-174">Следующий пример кода C# взят из проекта консольного **классического приложения Windows** на языке C# в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="edffe-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="edffe-175">В состав этого проекта входит установленный пакет NuGet **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="edffe-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="edffe-176">Замените заполнитель строки подключения строкой подключения, в которой используются записанные ранее значения **конечной точки, совместимой с концентраторами событий**, и **первичного ключа** службы, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="edffe-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="edffe-177">Замените заполнитель имени конечной точки мониторинга записанным ранее значением **имени конечной точки, совместимой с концентраторами событий**.</span><span class="sxs-lookup"><span data-stu-id="edffe-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="edffe-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="edffe-178">Next steps</span></span>
<span data-ttu-id="edffe-179">Для дальнейшего изучения возможностей центра IoT см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="edffe-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="edffe-180">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="edffe-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="edffe-181">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="edffe-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md