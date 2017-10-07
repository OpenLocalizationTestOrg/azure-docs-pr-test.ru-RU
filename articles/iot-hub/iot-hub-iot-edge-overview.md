---
title: "aaaOverview края IoT Azure | Документы Microsoft"
description: "Описываются hello основные принципы в Azure IoT Edge как шлюзы, модули и брокеры."
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
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="07472-103">Сведения об архитектуре Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="07472-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="07472-104">Прежде чем проверить любой пример кода, или создать собственные поля шлюз, с помощью IoT края, проанализируйте hello основные понятия, которые обеспечивают архитектура hello IoT края.</span><span class="sxs-lookup"><span data-stu-id="07472-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="07472-105">Модули Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="07472-105">IoT Edge modules</span></span>

<span data-ttu-id="07472-106">Шлюз создается с использованием Azure IoT Edge путем создания и сборки *модулей IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="07472-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="07472-107">Модули используют *сообщений* tooexchange данные друг с другом.</span><span class="sxs-lookup"><span data-stu-id="07472-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="07472-108">Модуль получает сообщение, выполняющий некоторое действие, при необходимости преобразует их в новое сообщение и затем публикует его для других модулей tooprocess.</span><span class="sxs-lookup"><span data-stu-id="07472-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="07472-109">Некоторые модули могут только создавать сообщения и никогда не обрабатывают входящие сообщения.</span><span class="sxs-lookup"><span data-stu-id="07472-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="07472-110">Цепочка модулей создает конвейера обработки данных с каждого модуля, выполняя преобразование данных hello в одной точке в этом конвейере.</span><span class="sxs-lookup"><span data-stu-id="07472-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![Цепочка модулей в шлюзе, созданном с помощью Edge Интернета вещей Azure][1]

<span data-ttu-id="07472-112">IoT Edge содержит hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="07472-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="07472-113">Предварительно написанные модули, которые выполняют общие функции шлюза.</span><span class="sxs-lookup"><span data-stu-id="07472-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="07472-114">интерфейсы Hello a developer можно использовать пользовательские модули toowrite.</span><span class="sxs-lookup"><span data-stu-id="07472-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="07472-115">Здравствуйте, необходимые toodeploy инфраструктуры и запустите набор модулей.</span><span class="sxs-lookup"><span data-stu-id="07472-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="07472-116">Hello SDK предоставляет уровень абстракции, который позволяет toorun toobuild шлюзов в различных операционных системах и платформах.</span><span class="sxs-lookup"><span data-stu-id="07472-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Уровень абстракции Edge Интернета вещей Azure][2]

## <a name="messages"></a><span data-ttu-id="07472-118">Сообщения</span><span class="sxs-lookup"><span data-stu-id="07472-118">Messages</span></span>

<span data-ttu-id="07472-119">Несмотря на то, что говорить о модулях передачи сообщения tooeach других является tooconceptualize удобным способом, как функции шлюза, он не отражать, что происходит.</span><span class="sxs-lookup"><span data-stu-id="07472-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="07472-120">Модули IoT Edge используют broker toocommunicate друг с другом.</span><span class="sxs-lookup"><span data-stu-id="07472-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="07472-121">Модули публикации broker toohello сообщений (с помощью шаблонов обмена сообщениями, например шины или публикации или подписки) и подождите, пока hello broker маршрута hello сообщение toohello модули подключенных tooit.</span><span class="sxs-lookup"><span data-stu-id="07472-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="07472-122">Модуль использует hello **Broker_Publish** функции toopublish toohello посредник сообщений.</span><span class="sxs-lookup"><span data-stu-id="07472-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="07472-123">Hello broker доставляет сообщения tooa модуль путем вызова функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="07472-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="07472-124">Сообщение состоит из набора пар ключ-значение, а содержимое передается как блок памяти.</span><span class="sxs-lookup"><span data-stu-id="07472-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![роль Hello hello брокера в Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="07472-126">Маршрутизация и фильтрация сообщений</span><span class="sxs-lookup"><span data-stu-id="07472-126">Message routing and filtering</span></span>

<span data-ttu-id="07472-127">Существует два способа toodirect сообщения toohello правильный IoT Edge модули:</span><span class="sxs-lookup"><span data-stu-id="07472-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="07472-128">Вы можете передать набор ссылок могут быть переданы toohello брокера, чтобы hello broker знал hello источника и приемника для каждого модуля.</span><span class="sxs-lookup"><span data-stu-id="07472-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="07472-129">Модуль можно фильтровать по свойствам приветственное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="07472-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="07472-130">Модуль только следует обрабатывают сообщения, если приветственное сообщение предназначено для него.</span><span class="sxs-lookup"><span data-stu-id="07472-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="07472-131">Фильтрация ссылок и сообщений создает конвейер сообщений.</span><span class="sxs-lookup"><span data-stu-id="07472-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07472-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07472-132">Next steps</span></span>

<span data-ttu-id="07472-133">toosee этих основных понятий в образец можно запустить, в разделе [архитектура исследовать Edge Azure IoT][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="07472-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md