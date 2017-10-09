---
title: "aaaManage центр IoT Azure облака устройство обмен сообщениями с центром IOT explorer | Документы Microsoft"
description: "Узнайте, как toouse hello центром IOT explorer CLI средство toomonitor устройства toocloud (D2C) сообщений и отправки сообщений toodevice (C2D) облака в Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "облако центром IOT обозревателе облака устройство обмена сообщениями, toodevice облака концентратора iot, toodevice обмена сообщениями"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="c71b9-104">Используйте обозреватель центром IOT toosend и получения сообщений между устройством и центр IoT</span><span class="sxs-lookup"><span data-stu-id="c71b9-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![Сквозная схема](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="c71b9-106">В [обозревателе Центра Интернета вещей](https://github.com/azure/iothub-explorer) доступно несколько команд, которые упрощают управление Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c71b9-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="c71b9-107">Этот учебник содержит сведения о toosend explorer центром IOT toouse и получения сообщений между устройством и концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="c71b9-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c71b9-108">Новые знания</span><span class="sxs-lookup"><span data-stu-id="c71b9-108">What you will learn</span></span>

<span data-ttu-id="c71b9-109">Вы узнаете, как toouse explorer центром IOT toomonitor устройства в облако и toosend сообщений облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="c71b9-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="c71b9-110">Сообщения из устройства в облако может быть датчиков, устройство собирает и затем отправляет tooyour центр IoT.</span><span class="sxs-lookup"><span data-stu-id="c71b9-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="c71b9-111">Сообщения облака на устройство может быть команды концентратор IoT отправляет tooblink tooyour устройства Индикатор, tooyour подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="c71b9-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c71b9-112">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="c71b9-112">What you will do</span></span>

- <span data-ttu-id="c71b9-113">С помощью обозревателя с центром IOT toomonitor устройства в облако сообщений.</span><span class="sxs-lookup"><span data-stu-id="c71b9-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="c71b9-114">С помощью обозревателя с центром IOT toosend облака на устройство сообщений.</span><span class="sxs-lookup"><span data-stu-id="c71b9-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c71b9-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="c71b9-115">What you need</span></span>

- <span data-ttu-id="c71b9-116">Учебник по [настроить на устройстве](iot-hub-raspberry-pi-kit-node-get-started.md) завершения, который охватывает hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="c71b9-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="c71b9-117">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="c71b9-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="c71b9-118">Центр Интернета вещей Azure в подписке;</span><span class="sxs-lookup"><span data-stu-id="c71b9-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="c71b9-119">Клиентское приложение, которое отправляет центр Azure IoT tooyour сообщений.</span><span class="sxs-lookup"><span data-stu-id="c71b9-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="c71b9-120">Обозреватель Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c71b9-120">iothub-explorer.</span></span> <span data-ttu-id="c71b9-121">([Установить обозреватель Центра Интернета вещей](https://github.com/azure/iothub-explorer).)</span><span class="sxs-lookup"><span data-stu-id="c71b9-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="c71b9-122">Отслеживание сообщений, отправляемых с устройства в облако</span><span class="sxs-lookup"><span data-stu-id="c71b9-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="c71b9-123">toomonitor сообщений, отправленных из tooyour IoT hub устройства, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c71b9-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="c71b9-124">Откройте окно консоли.</span><span class="sxs-lookup"><span data-stu-id="c71b9-124">Open a console window.</span></span>
1. <span data-ttu-id="c71b9-125">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="c71b9-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="c71b9-126">Получите `<device-id>` и `<IoTHubConnectionString>` из Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="c71b9-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="c71b9-127">Убедитесь, что после завершения предыдущего учебника hello.</span><span class="sxs-lookup"><span data-stu-id="c71b9-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="c71b9-128">Или можно попробовать toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` при наличии `HostName`, `SharedAccessKeyName` и `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="c71b9-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="c71b9-129">Отправка сообщений из облака на устройство</span><span class="sxs-lookup"><span data-stu-id="c71b9-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="c71b9-130">toosend сообщения с устройства tooyour IoT hub, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c71b9-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="c71b9-131">Откройте окно консоли.</span><span class="sxs-lookup"><span data-stu-id="c71b9-131">Open a console window.</span></span>
1. <span data-ttu-id="c71b9-132">Запуск сеанса на концентратор IoT, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c71b9-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="c71b9-133">Отправьте сообщение tooyour устройства, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c71b9-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="c71b9-134">Команда Hello мигает hello Индикатор, tooyour подключенных устройств и отправляет устройства tooyour сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="c71b9-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="c71b9-135">Нет необходимости для hello устройства toosend концентратор IoT задней tooyour команда отдельные ack при получении сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="c71b9-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c71b9-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c71b9-136">Next steps</span></span>

<span data-ttu-id="c71b9-137">Вы узнали, как сообщения и отправлять сообщения облака на устройство между устройствами IoT и центр IoT Azure toomonitor устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="c71b9-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
