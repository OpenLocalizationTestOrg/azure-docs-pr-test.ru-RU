---
title: "Управление обменом сообщениями между устройством и облаком Центра Интернета вещей Azure с помощью обозревателя Центра Интернета вещей | Документация Майкрософт"
description: "Узнайте, как с помощью интерфейса командной строки обозревателя Центра Интернета вещей отслеживать сообщения, отправляемые с устройства в облако (D2C), и отправлять сообщения из облака на устройство (C2D) в Центре Интернета вещей Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "обозреватель Центра Интернета вещей, обмен сообщениями между облаком и устройством, отправка сообщений из облака на устройство с помощью Центра Интернета вещей"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 30151b7bdc544bc36e959cc3528d37897198fc7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-iothub-explorer-to-send-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="16747-104">Использование обозревателя Центра Интернета вещей для обмена сообщениями между устройством и Центром Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="16747-104">Use iothub-explorer to send and receive messages between your device and IoT Hub</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="16747-106">В [обозревателе Центра Интернета вещей](https://github.com/azure/iothub-explorer) доступно несколько команд, которые упрощают управление Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="16747-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="16747-107">В этом руководстве объясняется, как использовать обозреватель Центра Интернета вещей для обмена сообщениями между устройством и Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="16747-107">This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="16747-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="16747-108">What you will learn</span></span>

<span data-ttu-id="16747-109">Вы узнаете, как использовать обозреватель Центра Интернета вещей для отслеживания сообщений, отправляемых с устройства в облако, и отправки сообщений из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="16747-109">You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages.</span></span> <span data-ttu-id="16747-110">В сообщениях, отправляемых с устройства в облако, могут содержаться данные датчиков, которые устройство собирает и отправляет в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="16747-110">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span></span> <span data-ttu-id="16747-111">Сообщения, отправляемые из облака на устройство, могут содержать команды, которые Центр Интернета вещей отправляет на устройство и которые активируют светодиодный индикатор, подключенный к устройству.</span><span class="sxs-lookup"><span data-stu-id="16747-111">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="16747-112">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="16747-112">What you will do</span></span>

- <span data-ttu-id="16747-113">Использование обозревателя Центра Интернета вещей для мониторинга сообщений, отправляемых с устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="16747-113">Use iothub-explorer to monitor device-to-cloud messages.</span></span>
- <span data-ttu-id="16747-114">Использование обозревателя Центра Интернета вещей для мониторинга сообщений, отправляемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="16747-114">Use iothub-explorer to send cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="16747-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="16747-115">What you need</span></span>

- <span data-ttu-id="16747-116">Изучите руководство [Настройка вашего устройства](iot-hub-raspberry-pi-kit-node-get-started.md), где описаны следующие требования.</span><span class="sxs-lookup"><span data-stu-id="16747-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="16747-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="16747-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="16747-118">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="16747-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="16747-119">клиентское приложение, которое отправляет сообщения в Центр Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="16747-119">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="16747-120">Обозреватель Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="16747-120">iothub-explorer.</span></span> <span data-ttu-id="16747-121">([Установить обозреватель Центра Интернета вещей](https://github.com/azure/iothub-explorer).)</span><span class="sxs-lookup"><span data-stu-id="16747-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="16747-122">Отслеживание сообщений, отправляемых с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="16747-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="16747-123">Чтобы отслеживать сообщения, отправляемые в Центр Интернета вещей с устройства, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="16747-123">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="16747-124">Откройте окно консоли.</span><span class="sxs-lookup"><span data-stu-id="16747-124">Open a console window.</span></span>
1. <span data-ttu-id="16747-125">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16747-125">Run the following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="16747-126">Получите `<device-id>` и `<IoTHubConnectionString>` из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="16747-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="16747-127">Обязательно выполните предыдущее руководство.</span><span class="sxs-lookup"><span data-stu-id="16747-127">Make sure you've finished the previous tutorial.</span></span> <span data-ttu-id="16747-128">Или можно попробовать использовать `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` при наличии `HostName`, `SharedAccessKeyName` и `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="16747-128">Or you can try to use `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="16747-129">Отправка сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="16747-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="16747-130">Чтобы отправить сообщение из Центра Интернета вещей на устройство, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="16747-130">To send a message from your IoT hub to your device, follow these steps:</span></span>

1. <span data-ttu-id="16747-131">Откройте окно консоли.</span><span class="sxs-lookup"><span data-stu-id="16747-131">Open a console window.</span></span>
1. <span data-ttu-id="16747-132">Запустите сеанс в Центре Интернета вещей с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="16747-132">Start a session on your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="16747-133">Отправьте сообщение на устройство с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="16747-133">Send a message to your device by running the following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="16747-134">Команда включает мигающий светодиодный индикатор, подключенный к устройству, и отправляет сообщение на устройство.</span><span class="sxs-lookup"><span data-stu-id="16747-134">The command blinks the LED that is connected to your device and sends the message to your device.</span></span>

> [!Note]
> <span data-ttu-id="16747-135">Устройству не нужно отправлять отдельную команду подтверждения в Центр Интернета вещей после получения сообщения.</span><span class="sxs-lookup"><span data-stu-id="16747-135">There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16747-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16747-136">Next steps</span></span>

<span data-ttu-id="16747-137">Вы узнали, как отслеживать сообщения, отправляемые из устройства Интернета вещей в облако Центра Интернета вещей, и отправлять сообщения из этого облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="16747-137">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
