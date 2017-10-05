---
title: "Добавление задержки в приложения логики | Документация Майкрософт"
description: "В этой статье приведены общие сведения о действиях \"Задержка\" и \"Задержка до\", а также об их использовании с приложением логики Azure."
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
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="041bd-103">Начало работы с действиями "Задержка" и "Задержка до"</span><span class="sxs-lookup"><span data-stu-id="041bd-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="041bd-104">С помощью действий "Задержка" и "Задержка до" можно выполнять сценарии рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="041bd-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="041bd-105">Например, вы можете просматривать:</span><span class="sxs-lookup"><span data-stu-id="041bd-105">For example, you can:</span></span>

* <span data-ttu-id="041bd-106">ожидание буднего дня, чтобы отправить обновление состояния по почте;</span><span class="sxs-lookup"><span data-stu-id="041bd-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="041bd-107">задержка рабочего процесса до завершения вызова HTTP, прежде чем возобновить работу и получить результат.</span><span class="sxs-lookup"><span data-stu-id="041bd-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="041bd-108">Сведения о начале работы с действием задержки в приложении логики см. в статье [Создание нового приложения логики, подключающего службы SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="041bd-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="041bd-109">Использование действий задержки</span><span class="sxs-lookup"><span data-stu-id="041bd-109">Use the delay actions</span></span>
<span data-ttu-id="041bd-110">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="041bd-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="041bd-111">[Дополнительные сведения о действиях](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="041bd-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="041bd-112">Ниже приведен пример последовательности настройки действия задержки в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="041bd-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="041bd-113">Чтобы добавить действие, после добавления триггера нажмите кнопку **Новый шаг** .</span><span class="sxs-lookup"><span data-stu-id="041bd-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="041bd-114">В текстовом поле введите **задержка** , чтобы открыть список действий задержки.</span><span class="sxs-lookup"><span data-stu-id="041bd-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="041bd-115">В этом примере мы выберем действие **Задержка**.</span><span class="sxs-lookup"><span data-stu-id="041bd-115">In this example, we will select **Delay**.</span></span>
   
    ![Действия задержки](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="041bd-117">Чтобы настроить задержку, задайте свойства действия.</span><span class="sxs-lookup"><span data-stu-id="041bd-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![Настройка задержки](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="041bd-119">Щелкните **Сохранить** , чтобы опубликовать и активировать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="041bd-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="041bd-120">Сведения о действиях</span><span class="sxs-lookup"><span data-stu-id="041bd-120">Action details</span></span>
<span data-ttu-id="041bd-121">Ниже приведены свойства, которые можно настроить для триггера повторения.</span><span class="sxs-lookup"><span data-stu-id="041bd-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="041bd-122">Действие "Задержка"</span><span class="sxs-lookup"><span data-stu-id="041bd-122">Delay action</span></span>
<span data-ttu-id="041bd-123">Это действие задерживает запуск на определенный промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="041bd-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="041bd-124">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="041bd-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="041bd-125">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="041bd-125">Display name</span></span> | <span data-ttu-id="041bd-126">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="041bd-126">Property name</span></span> | <span data-ttu-id="041bd-127">Описание</span><span class="sxs-lookup"><span data-stu-id="041bd-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="041bd-128">Счетчик*</span><span class="sxs-lookup"><span data-stu-id="041bd-128">Count*</span></span> |<span data-ttu-id="041bd-129">count</span><span class="sxs-lookup"><span data-stu-id="041bd-129">count</span></span> |<span data-ttu-id="041bd-130">Число единиц времени для задержки</span><span class="sxs-lookup"><span data-stu-id="041bd-130">The number of time units to delay</span></span> |
| <span data-ttu-id="041bd-131">Единица измерения*</span><span class="sxs-lookup"><span data-stu-id="041bd-131">Unit*</span></span> |<span data-ttu-id="041bd-132">unit</span><span class="sxs-lookup"><span data-stu-id="041bd-132">unit</span></span> |<span data-ttu-id="041bd-133">Единица времени: `Second`, `Minute`, `Hour` или `Day`</span><span class="sxs-lookup"><span data-stu-id="041bd-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="041bd-134">Действие "Задержка до"</span><span class="sxs-lookup"><span data-stu-id="041bd-134">Delay-until action</span></span>
<span data-ttu-id="041bd-135">Это действие задерживает запуск до указанной даты или времени.</span><span class="sxs-lookup"><span data-stu-id="041bd-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="041bd-136">Звездочка (*) означает, что это поле обязательное для заполнения.</span><span class="sxs-lookup"><span data-stu-id="041bd-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="041bd-137">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="041bd-137">Display name</span></span> | <span data-ttu-id="041bd-138">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="041bd-138">Property name</span></span> | <span data-ttu-id="041bd-139">Описание</span><span class="sxs-lookup"><span data-stu-id="041bd-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="041bd-140">Год*</span><span class="sxs-lookup"><span data-stu-id="041bd-140">Year*</span></span> |<span data-ttu-id="041bd-141">Timestamp</span><span class="sxs-lookup"><span data-stu-id="041bd-141">timestamp</span></span> |<span data-ttu-id="041bd-142">Задержка до года (GMT)</span><span class="sxs-lookup"><span data-stu-id="041bd-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="041bd-143">Месяц*</span><span class="sxs-lookup"><span data-stu-id="041bd-143">Month*</span></span> |<span data-ttu-id="041bd-144">Timestamp</span><span class="sxs-lookup"><span data-stu-id="041bd-144">timestamp</span></span> |<span data-ttu-id="041bd-145">Задержка до месяца (GMT)</span><span class="sxs-lookup"><span data-stu-id="041bd-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="041bd-146">День*</span><span class="sxs-lookup"><span data-stu-id="041bd-146">Day*</span></span> |<span data-ttu-id="041bd-147">Timestamp</span><span class="sxs-lookup"><span data-stu-id="041bd-147">timestamp</span></span> |<span data-ttu-id="041bd-148">Задержка до дня (GMT)</span><span class="sxs-lookup"><span data-stu-id="041bd-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="041bd-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="041bd-149">Next steps</span></span>
<span data-ttu-id="041bd-150">Теперь опробуйте платформу и [создайте приложение логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="041bd-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="041bd-151">Чтобы узнать, какие еще соединители доступны в приложениях логики, ознакомьтесь со [списком интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="041bd-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

