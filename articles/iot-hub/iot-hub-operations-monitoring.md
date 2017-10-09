---
title: "Мониторинг операций центра IoT aaaAzure | Документы Microsoft"
description: "Способ мониторинга toomonitor операций центр IoT Azure toouse hello состояние операций на ваш центр IoT в режиме реального времени."
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
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="64c78-103">Мониторинг операций центра IoT</span><span class="sxs-lookup"><span data-stu-id="64c78-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="64c78-104">Мониторинга операций центра IoT позволяет toomonitor hello состояния операций на ваш центр IoT в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="64c78-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="64c78-105">Центр Интернета вещей отслеживает события по нескольким категориям операций.</span><span class="sxs-lookup"><span data-stu-id="64c78-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="64c78-106">Вы можете отправить из одного или нескольких категорий tooan конечную точку в центр IoT для обработки события.</span><span class="sxs-lookup"><span data-stu-id="64c78-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="64c78-107">Можно отслеживать данные hello ошибок или настроить более сложную обработку на основе закономерностей в данных.</span><span class="sxs-lookup"><span data-stu-id="64c78-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="64c78-108">Центр Интернета вещей отслеживает шесть категорий событий:</span><span class="sxs-lookup"><span data-stu-id="64c78-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="64c78-109">Операции с удостоверениями устройства</span><span class="sxs-lookup"><span data-stu-id="64c78-109">Device identity operations</span></span>
* <span data-ttu-id="64c78-110">Телеметрия устройства</span><span class="sxs-lookup"><span data-stu-id="64c78-110">Device telemetry</span></span>
* <span data-ttu-id="64c78-111">Получение сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="64c78-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="64c78-112">Подключения</span><span class="sxs-lookup"><span data-stu-id="64c78-112">Connections</span></span>
* <span data-ttu-id="64c78-113">Передача файлов</span><span class="sxs-lookup"><span data-stu-id="64c78-113">File uploads</span></span>
* <span data-ttu-id="64c78-114">Маршрутизация сообщений</span><span class="sxs-lookup"><span data-stu-id="64c78-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="64c78-115">Способ мониторинга операций tooenable</span><span class="sxs-lookup"><span data-stu-id="64c78-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="64c78-116">Создайте Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="64c78-116">Create an IoT hub.</span></span> <span data-ttu-id="64c78-117">Инструкции о том, как можно найти центр IoT в hello toocreate [приступить к работе] [ lnk-get-started] руководства.</span><span class="sxs-lookup"><span data-stu-id="64c78-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="64c78-118">Откройте колонку hello из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="64c78-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="64c78-119">В колонке щелкните **Мониторинг операций**.</span><span class="sxs-lookup"><span data-stu-id="64c78-119">From there, click **Operations monitoring**.</span></span>

    ![Операции доступа к конфигурации портала hello мониторинга][1]

1. <span data-ttu-id="64c78-121">Выберите hello категории правильно toomonitor и нажмите кнопку контроля **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="64c78-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="64c78-122">Hello события, доступные для чтения из конечной точки hello совместимое концентратора событий, перечисленных в **параметры мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="64c78-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="64c78-123">Hello конечной точки центра IoT вызывается `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="64c78-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Настройка мониторинга операций в Центре Интернета вещей][2]

> [!NOTE]
> <span data-ttu-id="64c78-125">При выборе **Verbose** наблюдение за hello **подключений** категория приводит центра IoT toogenerate дополнительные диагностические сообщения.</span><span class="sxs-lookup"><span data-stu-id="64c78-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="64c78-126">Все остальные категории hello **Verbose** изменения параметров hello количество сведения центра IoT включает в каждое сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="64c78-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="64c78-127">Категории событий и как toouse их</span><span class="sxs-lookup"><span data-stu-id="64c78-127">Event categories and how toouse them</span></span>

<span data-ttu-id="64c78-128">Каждая категория мониторинга операций отслеживает отдельный тип взаимодействия с центром IoT и имеет схему, которая определяет способ структурирования событий в этой категории.</span><span class="sxs-lookup"><span data-stu-id="64c78-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="64c78-129">Операции с удостоверениями устройства</span><span class="sxs-lookup"><span data-stu-id="64c78-129">Device identity operations</span></span>

<span data-ttu-id="64c78-130">категории операций идентификаторов устройств Hello отслеживает ошибки, возникающие при попытке toocreate, обновление или удаление записи в реестре удостоверений центр IoT.</span><span class="sxs-lookup"><span data-stu-id="64c78-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="64c78-131">Отслеживание этой категории целесообразно для сценариев подготовки.</span><span class="sxs-lookup"><span data-stu-id="64c78-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="64c78-132">Телеметрия устройства</span><span class="sxs-lookup"><span data-stu-id="64c78-132">Device telemetry</span></span>

<span data-ttu-id="64c78-133">категории телеметрии устройств Hello отслеживает ошибок, возникших в центр IoT hello и являются связанные toohello конвейера телеметрии.</span><span class="sxs-lookup"><span data-stu-id="64c78-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="64c78-134">В эту категорию входят ошибки, возникающие при отправке событий телеметрии (например: регулирование) и при получении событий телеметрии (например: неавторизованный модуль чтения).</span><span class="sxs-lookup"><span data-stu-id="64c78-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="64c78-135">Эта категория не может перехватить ошибки, вызванные кодом, выполняемым на самом устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="64c78-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="64c78-136">Отправка команд из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="64c78-136">Cloud-to-device commands</span></span>

<span data-ttu-id="64c78-137">категории команд облака на устройство Hello отслеживает ошибок, возникших в центр IoT hello и являются связанные toohello конвейер сообщений облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="64c78-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="64c78-138">В эту категорию входят ошибки, возникающие при отправке сообщений из облака на устройство (например, неавторизированный отправитель), при получении сообщений из облака на устройство (например, превышение числа доставок) и при получении отзыва на сообщение из облака на устройство (например, истечение срока действия отзыва).</span><span class="sxs-lookup"><span data-stu-id="64c78-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="64c78-139">Эта категория не перехватывает ошибки с устройств, которые неправильно обрабатывает сообщение облака на устройство, если успешно доставлено сообщение hello облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="64c78-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="64c78-140">Подключения</span><span class="sxs-lookup"><span data-stu-id="64c78-140">Connections</span></span>

<span data-ttu-id="64c78-141">Категория соединения Hello отслеживает ошибки, которые возникают, когда устройства подключиться или отключиться от центра IoT.</span><span class="sxs-lookup"><span data-stu-id="64c78-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="64c78-142">Отслеживание этой категории полезно для определения попыток несанкционированных подключений и для отслеживания потери подключений к устройствам в областях с проблемами связи.</span><span class="sxs-lookup"><span data-stu-id="64c78-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="64c78-143">Передача файлов</span><span class="sxs-lookup"><span data-stu-id="64c78-143">File uploads</span></span>

<span data-ttu-id="64c78-144">Категория передачи файла Hello отслеживает ошибок, возникших в центр IoT hello и связанные toofile передачи возможностям.</span><span class="sxs-lookup"><span data-stu-id="64c78-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="64c78-145">В эту категорию входят:</span><span class="sxs-lookup"><span data-stu-id="64c78-145">This category includes:</span></span>

* <span data-ttu-id="64c78-146">Ошибки, происходящие с hello универсальный код Ресурса SAS, например при истечении перед устройства уведомляет концентратора hello завершения загрузки.</span><span class="sxs-lookup"><span data-stu-id="64c78-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="64c78-147">Сбой передачи, сообщаемые hello устройства.</span><span class="sxs-lookup"><span data-stu-id="64c78-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="64c78-148">ошибки, связанные с отсутствием файла в хранилище при создании уведомления для Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="64c78-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="64c78-149">Эта категория нельзя перехватить ошибки, которые непосредственно выполняются, пока hello устройство отправляет toostorage файла.</span><span class="sxs-lookup"><span data-stu-id="64c78-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="64c78-150">Маршрутизация сообщений</span><span class="sxs-lookup"><span data-stu-id="64c78-150">Message routing</span></span>

<span data-ttu-id="64c78-151">Категория маршрутизации сообщений Hello отслеживает ошибки, возникающие во время оценки маршрут сообщения и исправности конечной точки с точки зрения центра IoT.</span><span class="sxs-lookup"><span data-stu-id="64c78-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="64c78-152">В эту категорию входят события, такие, как правило, результатом является слишком «undefined», когда Центр IoT помечает конечную точку как сообщений и других ошибок, полученных из конечной точки.</span><span class="sxs-lookup"><span data-stu-id="64c78-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="64c78-153">Эта категория не включает определенные ошибки, о hello сами сообщения (например, устройство ошибки регулирования), которые отображаются в категории «устройства телеметрии» hello.</span><span class="sxs-lookup"><span data-stu-id="64c78-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="64c78-154">Просмотр событий</span><span class="sxs-lookup"><span data-stu-id="64c78-154">View events</span></span>

<span data-ttu-id="64c78-155">Можно использовать hello *explorer центром IOT* tooquickly средства проверки, что ваш центр IoT создает события наблюдения.</span><span class="sxs-lookup"><span data-stu-id="64c78-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="64c78-156">tooinstall hello инструмент, см. инструкции hello в hello [explorer центром IOT] [ lnk-iothub-explorer] репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="64c78-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="64c78-157">Убедитесь, что hello **подключений** мониторинг категории задано слишком**Verbose** hello портала.</span><span class="sxs-lookup"><span data-stu-id="64c78-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="64c78-158">В командной строке выполните следующую команду tooread из конечной точки мониторинга hello hello.</span><span class="sxs-lookup"><span data-stu-id="64c78-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="64c78-159">В другой командной строки выполните следующие команды toosimulate hello устройство, отправляющее сообщения из устройства в облако:</span><span class="sxs-lookup"><span data-stu-id="64c78-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="64c78-160">Hello первой командной строки показано событий мониторинга hello hello имитированное устройство подключается tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="64c78-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="64c78-161">Подключение toohello конечной точки мониторинга</span><span class="sxs-lookup"><span data-stu-id="64c78-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="64c78-162">Привет, наблюдение за конечной точкой на ваш центр IoT является конечной точкой совместимое концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="64c78-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="64c78-163">Можно использовать любой механизм, который работает с сообщениями мониторинга tooread концентраторов событий этой конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="64c78-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="64c78-164">Hello следующий пример создает основные средства чтения, не подходит для развертывания высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="64c78-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="64c78-165">Дополнительные сведения о том, как tooprocess сообщений из концентраторов событий см. в разделе hello [Приступая к работе с концентраторами событий] [ lnk-eventhubs-tutorial] учебника.</span><span class="sxs-lookup"><span data-stu-id="64c78-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="64c78-166">tooconnect toohello конечной точки мониторинга, необходимо имя конечной точки соединения строки и hello.</span><span class="sxs-lookup"><span data-stu-id="64c78-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="64c78-167">следующие шаги Hello Показать как toofind hello необходимые значения в портале hello:</span><span class="sxs-lookup"><span data-stu-id="64c78-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="64c78-168">На портале hello перейдите tooyour колонки ресурсов центра IoT.</span><span class="sxs-lookup"><span data-stu-id="64c78-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="64c78-169">Выберите **мониторинга операций**и запишите значение hello **концентратора событий-совместимое имя** и **конечной точки концентратора событий в совместимом** значения:</span><span class="sxs-lookup"><span data-stu-id="64c78-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Значения конечной точки, совместимой с концентраторами событий][img-endpoints]

1. <span data-ttu-id="64c78-171">Выберите **Политики общего доступа**, а затем — **служба**.</span><span class="sxs-lookup"><span data-stu-id="64c78-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="64c78-172">Запишите hello **первичного ключа** значение:</span><span class="sxs-lookup"><span data-stu-id="64c78-172">Make a note of hello **Primary key** value:</span></span>

    ![Первичный ключ политики общего доступа службы][img-service-key]

<span data-ttu-id="64c78-174">Hello следующий код C# берется из Visual Studio **Windows классического** консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="64c78-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="64c78-175">проект Hello имеет hello **WindowsAzure.ServiceBus** установлен пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="64c78-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="64c78-176">Замените заполнитель строки подключения hello со строкой соединения, использующего hello **концентратора событий-совместимой конечной точки** и служба **первичного ключа** значений было сказано ранее, как показано в следующих hello Пример:</span><span class="sxs-lookup"><span data-stu-id="64c78-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="64c78-177">Замените hello мониторинга заполнитель имя конечной точки hello **концентратора событий-совместимое имя** значение было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="64c78-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="64c78-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64c78-178">Next steps</span></span>
<span data-ttu-id="64c78-179">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="64c78-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="64c78-180">[Руководство разработчика для Центра Интернета вещей][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="64c78-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="64c78-181">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="64c78-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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