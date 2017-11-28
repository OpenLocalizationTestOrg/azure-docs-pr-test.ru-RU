---
title: "Добавление триггера повторения в приложения логики | Документация Майкрософт"
description: "Обзор триггера повторения и его использования с приложением логики Azure."
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
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="7b33d-103">Начало работы с триггером повторения</span><span class="sxs-lookup"><span data-stu-id="7b33d-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="7b33d-104">Благодаря триггеру повторения можно создавать эффективные рабочие процессы в облаке.</span><span class="sxs-lookup"><span data-stu-id="7b33d-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="7b33d-105">Вот что вы можете, к примеру, делать:</span><span class="sxs-lookup"><span data-stu-id="7b33d-105">For example, you can:</span></span>

* <span data-ttu-id="7b33d-106">запланировать рабочий процесс так, чтобы он запускал хранимую процедуру SQL ежедневно;</span><span class="sxs-lookup"><span data-stu-id="7b33d-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="7b33d-107">отправить по почте сводки всех твитов с определенным хэштегом за последнюю неделю.</span><span class="sxs-lookup"><span data-stu-id="7b33d-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="7b33d-108">Сведения о начале работы с триггером повторения в приложении логики см. в статье [Создание нового приложения логики, подключающего службы SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7b33d-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="7b33d-109">Использование триггера повторения</span><span class="sxs-lookup"><span data-stu-id="7b33d-109">Use a recurrence trigger</span></span>
<span data-ttu-id="7b33d-110">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="7b33d-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="7b33d-111">[Дополнительные сведения о триггерах](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b33d-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="7b33d-112">Ниже приведен пример последовательности настройки триггера повторения в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="7b33d-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="7b33d-113">Сначала добавьте триггер **повторения** в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="7b33d-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="7b33d-114">Укажите параметры интервала повторения.</span><span class="sxs-lookup"><span data-stu-id="7b33d-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="7b33d-115">Теперь приложение логики будет запускаться с определенным интервалом.</span><span class="sxs-lookup"><span data-stu-id="7b33d-115">The logic app now starts a run after each interval of time.</span></span>

![Триггер HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="7b33d-117">Сведения о триггере</span><span class="sxs-lookup"><span data-stu-id="7b33d-117">Trigger details</span></span>
<span data-ttu-id="7b33d-118">Ниже приведены свойства триггера повторения, которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="7b33d-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="7b33d-119">Он запускает приложение логики после интервала времени, который нужно указать.</span><span class="sxs-lookup"><span data-stu-id="7b33d-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="7b33d-120">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="7b33d-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="7b33d-121">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="7b33d-121">Display name</span></span> | <span data-ttu-id="7b33d-122">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="7b33d-122">Property name</span></span> | <span data-ttu-id="7b33d-123">Описание</span><span class="sxs-lookup"><span data-stu-id="7b33d-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b33d-124">Частота*</span><span class="sxs-lookup"><span data-stu-id="7b33d-124">Frequency*</span></span> |<span data-ttu-id="7b33d-125">frequency</span><span class="sxs-lookup"><span data-stu-id="7b33d-125">frequency</span></span> |<span data-ttu-id="7b33d-126">Единица времени: `Second`, `Minute`, `Hour`, `Day` или `Year`.</span><span class="sxs-lookup"><span data-stu-id="7b33d-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="7b33d-127">Интервал*</span><span class="sxs-lookup"><span data-stu-id="7b33d-127">Interval*</span></span> |<span data-ttu-id="7b33d-128">interval</span><span class="sxs-lookup"><span data-stu-id="7b33d-128">interval</span></span> |<span data-ttu-id="7b33d-129">Интервал повторения в указанной единице времени.</span><span class="sxs-lookup"><span data-stu-id="7b33d-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="7b33d-130">Часовой пояс</span><span class="sxs-lookup"><span data-stu-id="7b33d-130">Time Zone</span></span> |<span data-ttu-id="7b33d-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="7b33d-131">timeZone</span></span> |<span data-ttu-id="7b33d-132">Используется, если для свойства startTime указано значение без смещения от UTC.</span><span class="sxs-lookup"><span data-stu-id="7b33d-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="7b33d-133">Время начала</span><span class="sxs-lookup"><span data-stu-id="7b33d-133">Start time</span></span> |<span data-ttu-id="7b33d-134">startTime</span><span class="sxs-lookup"><span data-stu-id="7b33d-134">startTime</span></span> |<span data-ttu-id="7b33d-135">Время начала в [формате ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="7b33d-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="7b33d-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b33d-136">Next steps</span></span>
<span data-ttu-id="7b33d-137">Теперь опробуйте платформу и [создайте приложение логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7b33d-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="7b33d-138">Чтобы узнать, какие еще соединители доступны в приложениях логики, ознакомьтесь со [списком интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7b33d-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

