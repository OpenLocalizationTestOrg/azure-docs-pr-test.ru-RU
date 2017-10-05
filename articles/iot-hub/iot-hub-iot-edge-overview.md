---
title: "Обзор Azure IoT Edge | Документация Майкрософт"
description: "Основные сведения об архитектуре Azure IoT Edge, в том числе о шлюзах, модулях и брокерах."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="16ddb-103">Сведения об архитектуре Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="16ddb-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="16ddb-104">Прежде чем изучать любой пример кода или создавать собственные поля шлюза с использованием IoT Edge, необходимо изучить основные понятия, которые лежат в основе архитектуры IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="16ddb-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="16ddb-105">Модули Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="16ddb-105">IoT Edge modules</span></span>

<span data-ttu-id="16ddb-106">Шлюз создается с использованием Azure IoT Edge путем создания и сборки *модулей IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="16ddb-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="16ddb-107">Модули обмениваются данным с помощью *сообщений* .</span><span class="sxs-lookup"><span data-stu-id="16ddb-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="16ddb-108">Модуль получает сообщение, выполняет с ним определенное действие, при необходимости преобразует их в новое сообщение и публикует его для других модулей.</span><span class="sxs-lookup"><span data-stu-id="16ddb-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="16ddb-109">Некоторые модули могут только создавать сообщения и никогда не обрабатывают входящие сообщения.</span><span class="sxs-lookup"><span data-stu-id="16ddb-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="16ddb-110">Цепочка модулей создает конвейер обработки данных с каждым модулем, который выполняет преобразование данных в определенной точке этого конвейера.</span><span class="sxs-lookup"><span data-stu-id="16ddb-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Цепочка модулей в шлюзе, созданном с помощью Edge Интернета вещей Azure][1]

<span data-ttu-id="16ddb-112">IoT Edge состоит из следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="16ddb-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="16ddb-113">Предварительно написанные модули, которые выполняют общие функции шлюза.</span><span class="sxs-lookup"><span data-stu-id="16ddb-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="16ddb-114">Интерфейсы, которые разработчик может использовать для написания пользовательских модулей.</span><span class="sxs-lookup"><span data-stu-id="16ddb-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="16ddb-115">Инфраструктура, необходимая для развертывания и запуска набора модулей.</span><span class="sxs-lookup"><span data-stu-id="16ddb-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="16ddb-116">Пакет средств разработки включает слой абстракции, который позволяет собирать шлюзы для запуска в различных операционных системах и на разных платформах.</span><span class="sxs-lookup"><span data-stu-id="16ddb-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Уровень абстракции Edge Интернета вещей Azure][2]

## <a name="messages"></a><span data-ttu-id="16ddb-118">Сообщения</span><span class="sxs-lookup"><span data-stu-id="16ddb-118">Messages</span></span>

<span data-ttu-id="16ddb-119">Функционирование шлюза удобно представлять как передачу сообщений между модулями, однако, это не совсем так.</span><span class="sxs-lookup"><span data-stu-id="16ddb-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="16ddb-120">Модули IoT Edge используют брокер для взаимодействия между собой.</span><span class="sxs-lookup"><span data-stu-id="16ddb-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="16ddb-121">Модули публикуют сообщения в брокер (используя схему обмена сообщениями через шину либо подписки и публикации), а затем брокер направляет сообщения в подключенные к нему модули.</span><span class="sxs-lookup"><span data-stu-id="16ddb-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="16ddb-122">Чтобы опубликовать сообщение в брокер, модуль использует функцию **Broker_Publish**.</span><span class="sxs-lookup"><span data-stu-id="16ddb-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="16ddb-123">Брокер доставляет сообщения в модуль, вызывая функцию обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="16ddb-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="16ddb-124">Сообщение состоит из набора пар ключ-значение, а содержимое передается как блок памяти.</span><span class="sxs-lookup"><span data-stu-id="16ddb-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Роль брокера в Edge Интернета вещей Azure][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="16ddb-126">Маршрутизация и фильтрация сообщений</span><span class="sxs-lookup"><span data-stu-id="16ddb-126">Message routing and filtering</span></span>

<span data-ttu-id="16ddb-127">Сообщения направляются в нужные модули IoT Edge двумя способами:</span><span class="sxs-lookup"><span data-stu-id="16ddb-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="16ddb-128">В брокер может передаваться набор ссылок, в котором для брокера указывается источник и приемник для каждого модуля.</span><span class="sxs-lookup"><span data-stu-id="16ddb-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="16ddb-129">Модуль может выполнять фильтрацию по свойствам сообщения.</span><span class="sxs-lookup"><span data-stu-id="16ddb-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="16ddb-130">Модуль обрабатывает сообщение, только если оно предназначено для него.</span><span class="sxs-lookup"><span data-stu-id="16ddb-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="16ddb-131">Фильтрация ссылок и сообщений создает конвейер сообщений.</span><span class="sxs-lookup"><span data-stu-id="16ddb-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16ddb-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16ddb-132">Next steps</span></span>

<span data-ttu-id="16ddb-133">Дополнительные сведения о концепциях, применяемых в примере, который можно выполнить, см. в статье [Приступая к работе с архитектурой IoT Edge в Linux][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="16ddb-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md