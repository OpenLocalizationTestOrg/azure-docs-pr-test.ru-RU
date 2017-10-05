---
title: "Создание функции, которая выполняется по расписанию, в Azure | Документация Майкрософт"
description: "Узнайте, как создать в Azure функцию, которая выполняется по определенному расписанию."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="c05c7-103">Создание в Azure функции, активируемой по таймеру</span><span class="sxs-lookup"><span data-stu-id="c05c7-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="c05c7-104">Узнайте, как создать функцию, которая выполняется на основе определенного расписания с помощь Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="c05c7-104">Learn how to use Azure Functions to create a function that runs based a schedule that you define.</span></span>

![Создание приложения-функции на портале Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="c05c7-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c05c7-106">Prerequisites</span></span>

<span data-ttu-id="c05c7-107">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="c05c7-107">To complete this tutorial:</span></span>

+ <span data-ttu-id="c05c7-108">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="c05c7-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="c05c7-109">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="c05c7-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="c05c7-111">Затем создайте функцию в новом приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="c05c7-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="c05c7-112">Создание функции, активируемой по таймеру</span><span class="sxs-lookup"><span data-stu-id="c05c7-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="c05c7-113">Разверните приложение-функцию и нажмите кнопку **+** рядом с элементом **Функции**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="c05c7-114">Если это первая функция в приложении-функции, выберите **Пользовательская функция**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="c05c7-115">Откроется полный набор шаблонов функций.</span><span class="sxs-lookup"><span data-stu-id="c05c7-115">This displays the complete set of function templates.</span></span>

    ![Страница быстрого начала работы с функциями на портале Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="c05c7-117">Выберите шаблон **TimerTrigger** для нужного языка.</span><span class="sxs-lookup"><span data-stu-id="c05c7-117">Select the **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="c05c7-118">Затем используйте настройки, указанные в таблице.</span><span class="sxs-lookup"><span data-stu-id="c05c7-118">Then use the settings as specified in the table:</span></span>

    ![Создайте функцию, активируемую по таймеру, на портале Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="c05c7-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="c05c7-120">Setting</span></span> | <span data-ttu-id="c05c7-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="c05c7-121">Suggested value</span></span> | <span data-ttu-id="c05c7-122">Описание</span><span class="sxs-lookup"><span data-stu-id="c05c7-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="c05c7-123">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="c05c7-123">**Name your function**</span></span> | <span data-ttu-id="c05c7-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="c05c7-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="c05c7-125">Определяет имя функции, активируемой по таймеру.</span><span class="sxs-lookup"><span data-stu-id="c05c7-125">Defines the name of your timer triggered function.</span></span> |
    | <span data-ttu-id="c05c7-126">**[Расписание](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="c05c7-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="c05c7-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="c05c7-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="c05c7-128">[Выражение CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) с шестью полями, в котором запланировано ежеминутное выполнение функции.</span><span class="sxs-lookup"><span data-stu-id="c05c7-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function to run every minute.</span></span> |

2. <span data-ttu-id="c05c7-129">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-129">Click **Create**.</span></span> <span data-ttu-id="c05c7-130">Будет создана функция на выбранном вами языке, которая будет выполняться каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="c05c7-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="c05c7-131">Проверьте выполнение, просмотрев записанные в журналах сведения трассировки.</span><span class="sxs-lookup"><span data-stu-id="c05c7-131">Verify execution by viewing trace information written to the logs.</span></span>

    ![Средство просмотра журналов Функций на портале Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="c05c7-133">Теперь вы можете изменить расписание функции, чтобы она выполнялась реже, например раз в час.</span><span class="sxs-lookup"><span data-stu-id="c05c7-133">Now, you can change the function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-the-timer-schedule"></a><span data-ttu-id="c05c7-134">Обновление расписания таймера</span><span class="sxs-lookup"><span data-stu-id="c05c7-134">Update the timer schedule</span></span>

1. <span data-ttu-id="c05c7-135">Разверните вашу функцию и щелкните **Интеграция**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="c05c7-136">Здесь вы определяете входные и выходные привязки для вашей функции, а также задаете расписание.</span><span class="sxs-lookup"><span data-stu-id="c05c7-136">This is where you define input and output bindings for your function and also set the schedule.</span></span> 

2. <span data-ttu-id="c05c7-137">Введите в поле **Расписания** новое значение `0 0 */1 * * *`, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Обновление расписания таймера функций на портале Azure](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="c05c7-139">Теперь функция будет выполняться раз в час.</span><span class="sxs-lookup"><span data-stu-id="c05c7-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="c05c7-140">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="c05c7-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="c05c7-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c05c7-141">Next steps</span></span>

<span data-ttu-id="c05c7-142">Вы создали функцию, которая выполняется на основе расписания.</span><span class="sxs-lookup"><span data-stu-id="c05c7-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="c05c7-143">Дополнительные сведения о триггерах см.в статье [Настройка триггеров для выполнения кода с помощью Функций Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="c05c7-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>