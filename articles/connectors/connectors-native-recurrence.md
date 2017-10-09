---
title: "aaaAdd hello повторения триггера в приложениях для логики | Документы Microsoft"
description: "Общие сведения о hello повторения триггера и как toouse его с помощью Azure логику приложения."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="d3f52-103">Приступая к работе с hello повторения триггера</span><span class="sxs-lookup"><span data-stu-id="d3f52-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="d3f52-104">С помощью hello повторения триггера, можно создавать мощные рабочие процессы в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="d3f52-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="d3f52-105">Вот что вы можете, к примеру, делать:</span><span class="sxs-lookup"><span data-stu-id="d3f52-105">For example, you can:</span></span>

* <span data-ttu-id="d3f52-106">Планирование рабочего процесса toorun хранимая процедура SQL каждый день.</span><span class="sxs-lookup"><span data-stu-id="d3f52-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="d3f52-107">Отправить по электронной почте сводку всех твиты в течение прошлой неделе об определенных хэштегом hello.</span><span class="sxs-lookup"><span data-stu-id="d3f52-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="d3f52-108">tooget начала использования в приложении логику повторения триггера hello. в разделе [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d3f52-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="d3f52-109">Использование триггера повторения</span><span class="sxs-lookup"><span data-stu-id="d3f52-109">Use a recurrence trigger</span></span>
<span data-ttu-id="d3f52-110">Триггер — это событие, которое может быть hello используется toostart рабочий процесс, который определен в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="d3f52-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="d3f52-111">[Дополнительные сведения о триггерах](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3f52-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="d3f52-112">Вот пример последовательность как tooset копирование повторение триггер в приложение логики:</span><span class="sxs-lookup"><span data-stu-id="d3f52-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="d3f52-113">Добавить hello **повторения** hello первым шагом в приложение логики для триггера.</span><span class="sxs-lookup"><span data-stu-id="d3f52-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="d3f52-114">Заполните параметры hello для hello интервал повторения.</span><span class="sxs-lookup"><span data-stu-id="d3f52-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="d3f52-115">приложения логики Hello запускает выполнения после каждого интервала времени.</span><span class="sxs-lookup"><span data-stu-id="d3f52-115">hello logic app now starts a run after each interval of time.</span></span>

![Триггер HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="d3f52-117">Сведения о триггере</span><span class="sxs-lookup"><span data-stu-id="d3f52-117">Trigger details</span></span>
<span data-ttu-id="d3f52-118">Hello повторения триггера имеет следующие свойства, которые можно настроить hello.</span><span class="sxs-lookup"><span data-stu-id="d3f52-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="d3f52-119">Он запускает приложение логики после интервала времени, который нужно указать.</span><span class="sxs-lookup"><span data-stu-id="d3f52-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="d3f52-120">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="d3f52-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="d3f52-121">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="d3f52-121">Display name</span></span> | <span data-ttu-id="d3f52-122">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="d3f52-122">Property name</span></span> | <span data-ttu-id="d3f52-123">Описание</span><span class="sxs-lookup"><span data-stu-id="d3f52-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d3f52-124">Частота*</span><span class="sxs-lookup"><span data-stu-id="d3f52-124">Frequency*</span></span> |<span data-ttu-id="d3f52-125">frequency</span><span class="sxs-lookup"><span data-stu-id="d3f52-125">frequency</span></span> |<span data-ttu-id="d3f52-126">Единица времени Hello: `Second`, `Minute`, `Hour`, `Day`, или `Year`.</span><span class="sxs-lookup"><span data-stu-id="d3f52-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="d3f52-127">Интервал*</span><span class="sxs-lookup"><span data-stu-id="d3f52-127">Interval*</span></span> |<span data-ttu-id="d3f52-128">interval</span><span class="sxs-lookup"><span data-stu-id="d3f52-128">interval</span></span> |<span data-ttu-id="d3f52-129">Интервал приветствия hello заданных частоту повторения hello.</span><span class="sxs-lookup"><span data-stu-id="d3f52-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="d3f52-130">Часовой пояс</span><span class="sxs-lookup"><span data-stu-id="d3f52-130">Time Zone</span></span> |<span data-ttu-id="d3f52-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="d3f52-131">timeZone</span></span> |<span data-ttu-id="d3f52-132">Используется, если для свойства startTime указано значение без смещения от UTC.</span><span class="sxs-lookup"><span data-stu-id="d3f52-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="d3f52-133">Время начала</span><span class="sxs-lookup"><span data-stu-id="d3f52-133">Start time</span></span> |<span data-ttu-id="d3f52-134">startTime</span><span class="sxs-lookup"><span data-stu-id="d3f52-134">startTime</span></span> |<span data-ttu-id="d3f52-135">время начала Hello в [формата ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="d3f52-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="d3f52-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3f52-136">Next steps</span></span>
<span data-ttu-id="d3f52-137">Теперь попробуйте платформы hello и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d3f52-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="d3f52-138">Вы можете просматривать hello других доступных соединителей в приложении логики, просмотрев нашей [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d3f52-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

