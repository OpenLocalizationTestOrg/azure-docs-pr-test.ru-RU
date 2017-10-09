---
title: "aaaAzure IoT управление устройствами с помощью обозревателя с центром IOT | Документы Microsoft"
description: "Используйте hello центром IOT-CLI анализатор для управления устройствами центра IoT Azure, непосредственные методы hello и параметры управления hello двойных требуемые свойства."
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
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="c8b0e-104">Использование обозревателя Центра Интернета вещей для управления устройствами в Центре Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="c8b0e-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="c8b0e-106">[обозреватель центром IOT](https://github.com/azure/iothub-explorer) является средством CLI, которое запускается на удостоверения устройства toomanage компьютера узла в реестре концентратора IoT.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="c8b0e-107">Поставляется со параметры управления, которые можно использовать tooperform различные задачи.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="c8b0e-108">Возможность управления</span><span class="sxs-lookup"><span data-stu-id="c8b0e-108">Management option</span></span>          | <span data-ttu-id="c8b0e-109">Задача</span><span class="sxs-lookup"><span data-stu-id="c8b0e-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c8b0e-110">Прямые методы</span><span class="sxs-lookup"><span data-stu-id="c8b0e-110">Direct methods</span></span>             | <span data-ttu-id="c8b0e-111">Перевести устройство действовать, такие как запуск и остановка отправки сообщений или перезагрузка устройства hello.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="c8b0e-112">Требуемые свойства двойников</span><span class="sxs-lookup"><span data-stu-id="c8b0e-112">Twin desired properties</span></span>    | <span data-ttu-id="c8b0e-113">Перевести устройство в определенных состояниях, например установку toogreen Индикатор или задание телеметрии hello отправки too30 интервал в минутах.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="c8b0e-114">Сообщаемые свойства двойника</span><span class="sxs-lookup"><span data-stu-id="c8b0e-114">Twin reported properties</span></span>   | <span data-ttu-id="c8b0e-115">Получить hello сообщил о состоянии устройства.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-115">Get hello reported state of a device.</span></span> <span data-ttu-id="c8b0e-116">Например устройство hello сообщает Индикатор мигает теперь приветствия.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="c8b0e-117">Теги двойников</span><span class="sxs-lookup"><span data-stu-id="c8b0e-117">Twin tags</span></span>                  | <span data-ttu-id="c8b0e-118">Метаданные для конкретного устройства хранения в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="c8b0e-119">Здравствуйте, например, Торговый автомат расположение развертывания.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="c8b0e-120">Получение сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="c8b0e-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="c8b0e-121">Отправьте уведомления tooa устройства.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-121">Send notifications tooa device.</span></span> <span data-ttu-id="c8b0e-122">Например «это скорее всего toorain сегодня.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="c8b0e-123">Не забывайте о toobring зонтик.»</span><span class="sxs-lookup"><span data-stu-id="c8b0e-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="c8b0e-124">Запросы двойника устройства</span><span class="sxs-lookup"><span data-stu-id="c8b0e-124">Device twin queries</span></span>        | <span data-ttu-id="c8b0e-125">Запрос tooretrieve близнецы все устройства с произвольной условиями, например указания hello устройств, которые доступны для использования.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="c8b0e-126">Более подробные сведения о различиях hello и рекомендации по использованию этих параметров см. в разделе [руководство связи устройства в облако](iot-hub-devguide-d2c-guidance.md) и [облака на устройство связи руководство](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c8b0e-127">Двойники устройств — это документы JSON, хранящие сведения о состоянии устройства (метаданные, конфигурации и условия).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="c8b0e-128">Центр IoT сохранение двойных устройства для каждого устройства, которое подключается tooit.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="c8b0e-129">Дополнительные сведения о двойниках устройства см. в статье [Начало работы с двойниками устройств](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="c8b0e-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="c8b0e-130">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="c8b0e-130">What you learn</span></span>

<span data-ttu-id="c8b0e-131">Вы узнаете, как использовать обозреватель Центра Интернета вещей для работы с различными средствами на компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c8b0e-132">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-132">What you do</span></span>

<span data-ttu-id="c8b0e-133">Запустим обозреватель Центра Интернета вещей, используя различные средства управления.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c8b0e-134">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="c8b0e-134">What you need</span></span>

- <span data-ttu-id="c8b0e-135">Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="c8b0e-136">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="c8b0e-137">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="c8b0e-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="c8b0e-138">Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="c8b0e-139">Убедитесь, что устройство работает под управлением с hello клиентского приложения с помощью этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="c8b0e-140">iothub-explorer. [Установите iothub-explorer](https://github.com/azure/iothub-explorer) на компьютер разработки.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="c8b0e-141">Центр IoT tooyour подключения</span><span class="sxs-lookup"><span data-stu-id="c8b0e-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="c8b0e-142">Подключите концентратор IoT tooyour, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="c8b0e-143">Использование обозревателя Центра Интернета вещей для работы с прямыми методами</span><span class="sxs-lookup"><span data-stu-id="c8b0e-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="c8b0e-144">Вызвать hello `start` метод в hello устройства приложения toosend сообщения tooyour центра IoT, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="c8b0e-145">Вызвать hello `stop` метод при отправке toostop приложения hello устройства сообщений центра IoT tooyour, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="c8b0e-146">Использование обозревателя Центра Интернета вещей для работы с требуемыми свойствами двойника</span><span class="sxs-lookup"><span data-stu-id="c8b0e-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="c8b0e-147">Установка интервала нужное свойство = 3000, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="c8b0e-148">Устройство может прочитать это свойство.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="c8b0e-149">Использование обозревателя Центра Интернета вещей для работы с сообщаемыми свойствами двойника</span><span class="sxs-lookup"><span data-stu-id="c8b0e-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="c8b0e-150">Получить hello выводятся свойства устройства hello, запустив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="c8b0e-151">Одно из свойств hello — $metadata. $lastUpdated с буквами hello время последнего это устройство отправляет или получает сообщение.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="c8b0e-152">Использование обозревателя Центра Интернета вещей для работы с тегами двойника</span><span class="sxs-lookup"><span data-stu-id="c8b0e-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="c8b0e-153">Отображение тегов hello и свойства устройства hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="c8b0e-154">Добавьте роль поле = температуры и влажности toohello устройство, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="c8b0e-155">Использование обозревателя Центра Интернета вещей для работы с сообщениями, отправляемыми из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="c8b0e-156">Отправьте устройство toohello сообщение «Hello World», выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="c8b0e-157">В разделе [использовать обозреватель центром IOT toosend и получения сообщений между устройством и центр IoT](iot-hub-explorer-cloud-device-messaging.md) реальные сценарии использования этой команды.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="c8b0e-158">Использование обозревателя Центра Интернета вещей для запросов данных двойников устройства</span><span class="sxs-lookup"><span data-stu-id="c8b0e-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="c8b0e-159">Запрос устройства тег роли = 'температуры и влажности», выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="c8b0e-160">Запрос всех устройств, за исключением тех, с помощью тега роли = 'температуры и влажности», выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c8b0e-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="c8b0e-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8b0e-161">Next steps</span></span>

<span data-ttu-id="c8b0e-162">Вы узнали, каким образом центром IOT explorer toouse с различными параметрами управления.</span><span class="sxs-lookup"><span data-stu-id="c8b0e-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
