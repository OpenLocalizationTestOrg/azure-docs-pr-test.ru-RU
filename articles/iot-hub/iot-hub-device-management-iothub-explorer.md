---
title: "Управление устройствами Azure IoT с помощью обозревателя Центра Интернета вещей | Документация Майкрософт"
description: "С помощью средства командной строки iothub-explorer (обозревателя Центра Интернета вещей) можно управлять устройствами в Центре Интернета вещей Azure, используя прямые методы и возможности управления требуемыми свойствами двойника."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "управление устройствами Интернета вещей Azure, управление устройствами в Центре Интернета вещей Azure, управление устройствами, Интернет вещей, управление устройствами в Центре Интернета вещей"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="6ce88-104">Использование обозревателя Центра Интернета вещей для управления устройствами в Центре Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="6ce88-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6ce88-106">[Обозреватель Центра Интернета вещей](https://github.com/azure/iothub-explorer) — это средство командной строки, которое выполняется на главном компьютере для управления удостоверениями устройств в реестре Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="6ce88-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="6ce88-107">В нем предусмотрены возможности управления, с помощью которых можно выполнять различные задачи.</span><span class="sxs-lookup"><span data-stu-id="6ce88-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="6ce88-108">Возможность управления</span><span class="sxs-lookup"><span data-stu-id="6ce88-108">Management option</span></span>          | <span data-ttu-id="6ce88-109">Задача</span><span class="sxs-lookup"><span data-stu-id="6ce88-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6ce88-110">Прямые методы</span><span class="sxs-lookup"><span data-stu-id="6ce88-110">Direct methods</span></span>             | <span data-ttu-id="6ce88-111">Выполнение на устройстве таких действий, как запуск и остановка отправки сообщений или перезагрузка устройства.</span><span class="sxs-lookup"><span data-stu-id="6ce88-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="6ce88-112">Требуемые свойства двойников</span><span class="sxs-lookup"><span data-stu-id="6ce88-112">Twin desired properties</span></span>    | <span data-ttu-id="6ce88-113">Перевод устройства в определенные состояния, например включение зеленого светодиодного индикатора или установка 30-минутного интервала отправки данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="6ce88-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="6ce88-114">Сообщаемые свойства двойника</span><span class="sxs-lookup"><span data-stu-id="6ce88-114">Twin reported properties</span></span>   | <span data-ttu-id="6ce88-115">Получение зарегистрированного состояния устройства,</span><span class="sxs-lookup"><span data-stu-id="6ce88-115">Get the reported state of a device.</span></span> <span data-ttu-id="6ce88-116">например данных о том, что сейчас на устройстве мигает индикатор.</span><span class="sxs-lookup"><span data-stu-id="6ce88-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="6ce88-117">Теги двойников</span><span class="sxs-lookup"><span data-stu-id="6ce88-117">Twin tags</span></span>                  | <span data-ttu-id="6ce88-118">Хранение метаданных для конкретного устройства в облаке.</span><span class="sxs-lookup"><span data-stu-id="6ce88-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="6ce88-119">Например, расположение развертывания торгового автомата.</span><span class="sxs-lookup"><span data-stu-id="6ce88-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="6ce88-120">Получение сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="6ce88-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="6ce88-121">Отправка уведомлений на устройство,</span><span class="sxs-lookup"><span data-stu-id="6ce88-121">Send notifications to a device.</span></span> <span data-ttu-id="6ce88-122">например "Скорее всего сегодня будет дождь.</span><span class="sxs-lookup"><span data-stu-id="6ce88-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="6ce88-123">Не забудьте взять зонтик".</span><span class="sxs-lookup"><span data-stu-id="6ce88-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="6ce88-124">Запросы двойника устройства</span><span class="sxs-lookup"><span data-stu-id="6ce88-124">Device twin queries</span></span>        | <span data-ttu-id="6ce88-125">Запрос всех двойников устройства для получения тех из них, которые соответствуют произвольным условиям, например для определения устройств, которые доступны для использования.</span><span class="sxs-lookup"><span data-stu-id="6ce88-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="6ce88-126">Более подробное объяснение различий и рекомендации по использованию этих параметров см. в статьях [Руководство по обмену данными между устройством и облаком](iot-hub-devguide-d2c-guidance.md) и [Руководство по обмену данными между облаком и устройством](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="6ce88-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6ce88-127">Двойники устройств — это документы JSON, хранящие сведения о состоянии устройства (метаданные, конфигурации и условия).</span><span class="sxs-lookup"><span data-stu-id="6ce88-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="6ce88-128">Центр Интернета вещей сохраняет двойник устройства для каждого устройства, подключаемого к нему.</span><span class="sxs-lookup"><span data-stu-id="6ce88-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="6ce88-129">Дополнительные сведения о двойниках устройства см. в статье [Начало работы с двойниками устройств](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="6ce88-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6ce88-130">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="6ce88-130">What you learn</span></span>

<span data-ttu-id="6ce88-131">Вы узнаете, как использовать обозреватель Центра Интернета вещей для работы с различными средствами на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="6ce88-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6ce88-132">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="6ce88-132">What you do</span></span>

<span data-ttu-id="6ce88-133">Запустим обозреватель Центра Интернета вещей, используя различные средства управления.</span><span class="sxs-lookup"><span data-stu-id="6ce88-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6ce88-134">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="6ce88-134">What you need</span></span>

- <span data-ttu-id="6ce88-135">Изучите руководство [Настройка вашего устройства](iot-hub-raspberry-pi-kit-node-get-started.md), где описаны следующие требования.</span><span class="sxs-lookup"><span data-stu-id="6ce88-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="6ce88-136">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce88-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="6ce88-137">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="6ce88-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="6ce88-138">клиентское приложение, которое отправляет сообщения в Центр Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce88-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="6ce88-139">Во время работы с этим руководством на устройстве должно работать клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="6ce88-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="6ce88-140">iothub-explorer. [Установите iothub-explorer](https://github.com/azure/iothub-explorer) на компьютер разработки.</span><span class="sxs-lookup"><span data-stu-id="6ce88-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="6ce88-141">Подключение к Центру Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="6ce88-141">Connect to your IoT hub</span></span>

<span data-ttu-id="6ce88-142">Подключитесь к Центру Интернета вещей с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="6ce88-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="6ce88-143">Использование обозревателя Центра Интернета вещей для работы с прямыми методами</span><span class="sxs-lookup"><span data-stu-id="6ce88-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="6ce88-144">Вызовите метод `start` в приложении для устройства, чтобы отправить сообщения в Центр Интернета вещей с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="6ce88-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="6ce88-145">Вызовите метод `stop` в приложении для устройства, чтобы прекратить отправку сообщений в Центр Интернета вещей с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="6ce88-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="6ce88-146">Использование обозревателя Центра Интернета вещей для работы с требуемыми свойствами двойника</span><span class="sxs-lookup"><span data-stu-id="6ce88-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="6ce88-147">Установите для требуемого свойства интервал 3000, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ce88-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="6ce88-148">Устройство может прочитать это свойство.</span><span class="sxs-lookup"><span data-stu-id="6ce88-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="6ce88-149">Использование обозревателя Центра Интернета вещей для работы с сообщаемыми свойствами двойника</span><span class="sxs-lookup"><span data-stu-id="6ce88-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="6ce88-150">Получите сообщаемые свойства устройства, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ce88-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6ce88-151">Одно из свойств ($metadata.$lastUpdated) указывает время последней отправки или получения сообщения устройством.</span><span class="sxs-lookup"><span data-stu-id="6ce88-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="6ce88-152">Использование обозревателя Центра Интернета вещей для работы с тегами двойника</span><span class="sxs-lookup"><span data-stu-id="6ce88-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="6ce88-153">Отобразите теги и свойства устройства, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ce88-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6ce88-154">Добавьте на устройство поле role = temperature&humidity, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ce88-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="6ce88-155">Использование обозревателя Центра Интернета вещей для работы с сообщениями, отправляемыми из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="6ce88-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="6ce88-156">Отправьте сообщение "Hello World" на устройство с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="6ce88-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="6ce88-157">Практические сценарии использования этой команды см. в статье [Использование обозревателя Центра Интернета вещей для обмена сообщениями между устройством и Центром Интернета вещей](iot-hub-explorer-cloud-device-messaging.md)</span><span class="sxs-lookup"><span data-stu-id="6ce88-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="6ce88-158">Использование обозревателя Центра Интернета вещей для запросов данных двойников устройства</span><span class="sxs-lookup"><span data-stu-id="6ce88-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="6ce88-159">Отправьте запрос на предоставление данных устройств с тегом роли 'temperature&humidity', выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ce88-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="6ce88-160">Отправьте запрос на предоставление данных всех устройств, кроме тех, для которых задан тег роли 'temperature&humidity', выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6ce88-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="6ce88-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ce88-161">Next steps</span></span>

<span data-ttu-id="6ce88-162">Вы узнали, как использовать обозреватель Центра Интернета вещей для работы с различными средствами управления.</span><span class="sxs-lookup"><span data-stu-id="6ce88-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
