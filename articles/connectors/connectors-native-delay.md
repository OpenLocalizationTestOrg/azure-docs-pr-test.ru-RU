---
title: "aaaAdd задержки в приложении логики | Документы Microsoft"
description: "Общие сведения о hello задержки и Задержка-до действия и как toouse их с приложением Azure логику."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="5a621-103">Приступая к работе с hello задержки и Задержка-до действия</span><span class="sxs-lookup"><span data-stu-id="5a621-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="5a621-104">С помощью задержки hello и» Задержка-до» действий, можно воспользоваться сценариями рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="5a621-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="5a621-105">Вот что вы можете, к примеру, делать:</span><span class="sxs-lookup"><span data-stu-id="5a621-105">For example, you can:</span></span>

* <span data-ttu-id="5a621-106">Подождите, пока рабочий день toosend состояние обновления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="5a621-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="5a621-107">Рабочий процесс hello задержка до вызова HTTP имеет toofinish времени до возобновления и получение результата hello.</span><span class="sxs-lookup"><span data-stu-id="5a621-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="5a621-108">tooget работы с использованием hello задержки выполнения действия в приложении логику в разделе [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5a621-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="5a621-109">Используйте действия задержки hello</span><span class="sxs-lookup"><span data-stu-id="5a621-109">Use hello delay actions</span></span>
<span data-ttu-id="5a621-110">Действие — это операции, выполняемые hello рабочего процесса, определенные в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5a621-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="5a621-111">[Дополнительные сведения о действиях](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a621-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="5a621-112">Вот пример последовательность как toouse задержки шага в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5a621-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="5a621-113">После добавления триггера, нажмите кнопку **новый шаг** tooadd действие.</span><span class="sxs-lookup"><span data-stu-id="5a621-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="5a621-114">Поиск **задержки** toobring hello действий задержки.</span><span class="sxs-lookup"><span data-stu-id="5a621-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="5a621-115">В этом примере мы выберем действие **Задержка**.</span><span class="sxs-lookup"><span data-stu-id="5a621-115">In this example, we will select **Delay**.</span></span>
   
    ![Действия задержки](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="5a621-117">Завершите все hello действие свойства tooconfigure hello задержки.</span><span class="sxs-lookup"><span data-stu-id="5a621-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![Настройка задержки](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="5a621-119">Нажмите кнопку **Сохранить** toopublish и активировать приложение hello логику.</span><span class="sxs-lookup"><span data-stu-id="5a621-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="5a621-120">Сведения о действиях</span><span class="sxs-lookup"><span data-stu-id="5a621-120">Action details</span></span>
<span data-ttu-id="5a621-121">Hello повторения триггера имеет следующие свойства, которые могут быть настроены hello.</span><span class="sxs-lookup"><span data-stu-id="5a621-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="5a621-122">Действие "Задержка"</span><span class="sxs-lookup"><span data-stu-id="5a621-122">Delay action</span></span>
<span data-ttu-id="5a621-123">Это действие задержки hello, выполнить определенный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="5a621-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="5a621-124">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="5a621-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="5a621-125">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="5a621-125">Display name</span></span> | <span data-ttu-id="5a621-126">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="5a621-126">Property name</span></span> | <span data-ttu-id="5a621-127">Описание</span><span class="sxs-lookup"><span data-stu-id="5a621-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a621-128">Счетчик*</span><span class="sxs-lookup"><span data-stu-id="5a621-128">Count*</span></span> |<span data-ttu-id="5a621-129">count</span><span class="sxs-lookup"><span data-stu-id="5a621-129">count</span></span> |<span data-ttu-id="5a621-130">Hello количество toodelay единиц времени</span><span class="sxs-lookup"><span data-stu-id="5a621-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="5a621-131">Единица измерения*</span><span class="sxs-lookup"><span data-stu-id="5a621-131">Unit*</span></span> |<span data-ttu-id="5a621-132">unit</span><span class="sxs-lookup"><span data-stu-id="5a621-132">unit</span></span> |<span data-ttu-id="5a621-133">Единица времени Hello: `Second`, `Minute`, `Hour`, или`Day`</span><span class="sxs-lookup"><span data-stu-id="5a621-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="5a621-134">Действие "Задержка до"</span><span class="sxs-lookup"><span data-stu-id="5a621-134">Delay-until action</span></span>
<span data-ttu-id="5a621-135">Это действие задержки hello выполняется до указанных даты и времени.</span><span class="sxs-lookup"><span data-stu-id="5a621-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="5a621-136">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="5a621-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="5a621-137">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="5a621-137">Display name</span></span> | <span data-ttu-id="5a621-138">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="5a621-138">Property name</span></span> | <span data-ttu-id="5a621-139">Описание</span><span class="sxs-lookup"><span data-stu-id="5a621-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a621-140">Год*</span><span class="sxs-lookup"><span data-stu-id="5a621-140">Year*</span></span> |<span data-ttu-id="5a621-141">Timestamp</span><span class="sxs-lookup"><span data-stu-id="5a621-141">timestamp</span></span> |<span data-ttu-id="5a621-142">Hello toodelay года до (по Гринвичу)</span><span class="sxs-lookup"><span data-stu-id="5a621-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="5a621-143">Месяц*</span><span class="sxs-lookup"><span data-stu-id="5a621-143">Month*</span></span> |<span data-ttu-id="5a621-144">Timestamp</span><span class="sxs-lookup"><span data-stu-id="5a621-144">timestamp</span></span> |<span data-ttu-id="5a621-145">Hello toodelay месяц до (по Гринвичу)</span><span class="sxs-lookup"><span data-stu-id="5a621-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="5a621-146">День*</span><span class="sxs-lookup"><span data-stu-id="5a621-146">Day*</span></span> |<span data-ttu-id="5a621-147">Timestamp</span><span class="sxs-lookup"><span data-stu-id="5a621-147">timestamp</span></span> |<span data-ttu-id="5a621-148">Hello toodelay день до (по Гринвичу)</span><span class="sxs-lookup"><span data-stu-id="5a621-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="5a621-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a621-149">Next steps</span></span>
<span data-ttu-id="5a621-150">Теперь попробуйте платформы hello и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5a621-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5a621-151">Вы можете просматривать hello других доступных соединителей в приложении логики, просмотрев нашей [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5a621-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

