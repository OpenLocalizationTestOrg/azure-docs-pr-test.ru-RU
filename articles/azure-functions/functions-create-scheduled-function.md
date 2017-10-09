---
title: "функция, которая выполняется по расписанию в Azure aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate функции в Azure, которая выполняется на основе определяемому вами расписанию."
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
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="5cb2e-103">Создание в Azure функции, активируемой по таймеру</span><span class="sxs-lookup"><span data-stu-id="5cb2e-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="5cb2e-104">Узнайте, как toocreate функции Azure toouse функцию, которая выполняется на основе определяемому вами расписанию.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Создание функции приложения в hello портал Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="5cb2e-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5cb2e-106">Prerequisites</span></span>

<span data-ttu-id="5cb2e-107">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="5cb2e-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="5cb2e-108">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="5cb2e-109">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="5cb2e-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="5cb2e-111">Создайте функцию в приложение новые функции hello.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="5cb2e-112">Создание функции, активируемой по таймеру</span><span class="sxs-lookup"><span data-stu-id="5cb2e-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="5cb2e-113">Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="5cb2e-114">Если это первая функция hello в приложении функции, выберите **пользовательские функции**.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="5cb2e-115">Откроется hello полный набор шаблонов функций.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-115">This displays hello complete set of function templates.</span></span>

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="5cb2e-117">Выберите hello **TimerTrigger** шаблона для нужный язык.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="5cb2e-118">Затем используйте hello параметры, как указано в таблице hello:</span><span class="sxs-lookup"><span data-stu-id="5cb2e-118">Then use hello settings as specified in hello table:</span></span>

    ![Создайте функцию таймер запускается в hello портал Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="5cb2e-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="5cb2e-120">Setting</span></span> | <span data-ttu-id="5cb2e-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="5cb2e-121">Suggested value</span></span> | <span data-ttu-id="5cb2e-122">Описание</span><span class="sxs-lookup"><span data-stu-id="5cb2e-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="5cb2e-123">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="5cb2e-123">**Name your function**</span></span> | <span data-ttu-id="5cb2e-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="5cb2e-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="5cb2e-125">Определяет имя hello этой функции запуска таймера.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="5cb2e-126">**[Расписание](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="5cb2e-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="5cb2e-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="5cb2e-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="5cb2e-128">Шесть полей [выражение CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) , планирует вашей toorun функция каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="5cb2e-129">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-129">Click **Create**.</span></span> <span data-ttu-id="5cb2e-130">Будет создана функция на выбранном вами языке, которая будет выполняться каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="5cb2e-131">Проверьте выполнение, просмотр сведений трассировки записываются журналы toohello.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![Функции просмотра журнала в hello портал Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="5cb2e-133">Теперь можно изменить расписание функции hello, чтобы он запускался реже, например один раз в час.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="5cb2e-134">Обновить расписание таймера hello</span><span class="sxs-lookup"><span data-stu-id="5cb2e-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="5cb2e-135">Разверните вашу функцию и щелкните **Интеграция**.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="5cb2e-136">Это где определение входных данных и вывода привязки функции, а также задать расписание hello.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="5cb2e-137">Введите в поле **Расписания** новое значение `0 0 */1 * * *`, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Функции Обновить расписание таймера в hello портал Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="5cb2e-139">Теперь функция будет выполняться раз в час.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="5cb2e-140">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="5cb2e-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="5cb2e-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5cb2e-141">Next steps</span></span>

<span data-ttu-id="5cb2e-142">Вы создали функцию, которая выполняется на основе расписания.</span><span class="sxs-lookup"><span data-stu-id="5cb2e-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="5cb2e-143">Дополнительные сведения о триггерах см.в статье [Настройка триггеров для выполнения кода с помощью Функций Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="5cb2e-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>