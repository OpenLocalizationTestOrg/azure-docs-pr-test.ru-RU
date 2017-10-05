---
title: "Добавление условий и запуск рабочих процессов в Azure Logic Apps | Документация Майкрософт"
description: "Узнайте, как управлять запуском рабочих процессов в Azure Logic Apps с помощью добавления условной логики, триггеров, действий и параметров."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: e632c48ed31e82536db55a9c54438bece0c38fd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="cae3b-103">Использование функций приложений логики</span><span class="sxs-lookup"><span data-stu-id="cae3b-103">Use Logic Apps features</span></span>

<span data-ttu-id="cae3b-104">В [предыдущем разделе](../logic-apps/logic-apps-create-a-logic-app.md) вы создали свое первое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="cae3b-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="cae3b-105">Чтобы управлять рабочим процессом приложения логики, необходимо указать различные пути выполнения для него и способы обработки данных в массивах, коллекциях и пакетах.</span><span class="sxs-lookup"><span data-stu-id="cae3b-105">To control your logic app's workflow, you can specify different paths for your logic app to run and how to process data in arrays, collections, and batches.</span></span> <span data-ttu-id="cae3b-106">Эти элементы можно включить в рабочий процесс приложения логики:</span><span class="sxs-lookup"><span data-stu-id="cae3b-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="cae3b-107">Условия и [операторы switch](../logic-apps/logic-apps-switch-case.md) позволяют вашему приложению логики выполнять различные действия в зависимости от того, выполняются ли определенные условия.</span><span class="sxs-lookup"><span data-stu-id="cae3b-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="cae3b-108">[Циклы](../logic-apps/logic-apps-loops-and-scopes.md) позволяют приложению логики выполнять шаги неоднократно.</span><span class="sxs-lookup"><span data-stu-id="cae3b-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="cae3b-109">Например, можно повторить действия по всему массиву, используя цикл **For_each**,</span><span class="sxs-lookup"><span data-stu-id="cae3b-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="cae3b-110">или повторять действия, пока не выполнится условие, используя цикл **Until**.</span><span class="sxs-lookup"><span data-stu-id="cae3b-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="cae3b-111">[Области](../logic-apps/logic-apps-loops-and-scopes.md) позволяют группировать последовательности действий, например, чтобы реализовать обработку исключений.</span><span class="sxs-lookup"><span data-stu-id="cae3b-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, to implement exception handling.</span></span>

* <span data-ttu-id="cae3b-112">[Индивидуальная обработка](../logic-apps/logic-apps-loops-and-scopes.md) позволяет приложению логики запускать отдельные рабочие процессы для элементов в массиве при использовании команды **SplitOn**.</span><span class="sxs-lookup"><span data-stu-id="cae3b-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use the **SplitOn** command.</span></span>

<span data-ttu-id="cae3b-113">Здесь описываются другие понятия для создания приложения логики:</span><span class="sxs-lookup"><span data-stu-id="cae3b-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="cae3b-114">Представление кода для изменения имеющегося приложения логики.</span><span class="sxs-lookup"><span data-stu-id="cae3b-114">Code view to edit an existing logic app</span></span>
* <span data-ttu-id="cae3b-115">Варианты запуска рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="cae3b-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="cae3b-116">Условия: выполнение шагов только после выполнения условия</span><span class="sxs-lookup"><span data-stu-id="cae3b-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="cae3b-117">Чтобы приложение логики выполняло шаги только тогда, когда данные соответствуют указанным критериям, можно добавить условие, которое сравнивает данные в рабочем процессе с определенными полями и значениями.</span><span class="sxs-lookup"><span data-stu-id="cae3b-117">To have your logic app run steps only when data meets specific criteria, you can add a condition that compares data in the workflow against specific fields or values.</span></span>

<span data-ttu-id="cae3b-118">Например, предположим, что у вас есть приложение логики, которое отправляет слишком много электронных писем для записей в RSS-канале веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="cae3b-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="cae3b-119">Можно добавить условие, чтобы приложение логики отсылало электронное письмо только в том случае, когда новая запись принадлежит к определенной категории.</span><span class="sxs-lookup"><span data-stu-id="cae3b-119">You can add a condition so that your logic app sends email only when the new post belongs to a specific category.</span></span>

1. <span data-ttu-id="cae3b-120">На [портале Azure](https://portal.azure.com) найдите приложение логики и откройте его в конструкторе приложений логики.</span><span class="sxs-lookup"><span data-stu-id="cae3b-120">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="cae3b-121">Добавьте условие в нужное место в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="cae3b-121">Add a condition to the workflow location that you want.</span></span> 

   <span data-ttu-id="cae3b-122">Чтобы добавить условие между имеющимися шагами в рабочем процессе приложения логики, переместите указатель над стрелкой, где вы хотите добавить условие.</span><span class="sxs-lookup"><span data-stu-id="cae3b-122">To add the condition between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the condition.</span></span> 
   <span data-ttu-id="cae3b-123">Щелкните **знак "плюс"** (**+**), а затем выберите **Добавить условие**.</span><span class="sxs-lookup"><span data-stu-id="cae3b-123">Choose the **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="cae3b-124">Например:</span><span class="sxs-lookup"><span data-stu-id="cae3b-124">For example:</span></span>

   ![Добавление условия в приложение логики](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="cae3b-126">Если условие надо добавить в конце текущего рабочего процесса, перейдите в нижнюю часть приложения логики и выберите **+ Новый шаг**.</span><span class="sxs-lookup"><span data-stu-id="cae3b-126">If you want to add a condition at the end of your current workflow, go to the bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="cae3b-127">Теперь определите условие.</span><span class="sxs-lookup"><span data-stu-id="cae3b-127">Now define the condition.</span></span> <span data-ttu-id="cae3b-128">Укажите исходное поле, которое необходимо оценить, операцию, которую нужно выполнить, и целевое значение или поле.</span><span class="sxs-lookup"><span data-stu-id="cae3b-128">Specify the source field that you want to evaluate, the operation to perform, and the target value or field.</span></span> <span data-ttu-id="cae3b-129">Чтобы добавить имеющиеся поля в условие, выберите их из **списка добавления динамического содержимого**.</span><span class="sxs-lookup"><span data-stu-id="cae3b-129">To add existing fields to your condition, choose from the **Add dynamic content list**.</span></span>

   <span data-ttu-id="cae3b-130">Например:</span><span class="sxs-lookup"><span data-stu-id="cae3b-130">For example:</span></span>

   ![Изменение условий в базовом режиме](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="cae3b-132">Ниже приведено полное условие:</span><span class="sxs-lookup"><span data-stu-id="cae3b-132">Here's the complete condition:</span></span>

   ![Полное условие](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="cae3b-134">Чтобы определить условие в коде, выберите **Edit in advanced mode** (Изменить в расширенном режиме).</span><span class="sxs-lookup"><span data-stu-id="cae3b-134">To define the condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="cae3b-135">Например:</span><span class="sxs-lookup"><span data-stu-id="cae3b-135">For example:</span></span>
   > 
   > ![Изменение условия в коде](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="cae3b-137">В разделе **IF YES** (Если да) и **IF NO** (Если нет) добавьте шаги для выполнения в зависимости от удовлетворения условия.</span><span class="sxs-lookup"><span data-stu-id="cae3b-137">Under **IF YES** and **IF NO**, add the steps to perform based on whether the condition is met.</span></span>

   <span data-ttu-id="cae3b-138">Например:</span><span class="sxs-lookup"><span data-stu-id="cae3b-138">For example:</span></span>

   ![Условия с путями "Да" и "Нет"](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="cae3b-140">Имеющиеся действия можно перетаскивать в пути **IF YES** (Если да) и **IF NO** (Если нет).</span><span class="sxs-lookup"><span data-stu-id="cae3b-140">You can drag existing actions into the **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="cae3b-141">Сохраните приложение логики, когда закончите.</span><span class="sxs-lookup"><span data-stu-id="cae3b-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="cae3b-142">Теперь вы будете получать сообщения электронной почты только в том случае, если записи соответствуют условию.</span><span class="sxs-lookup"><span data-stu-id="cae3b-142">Now you get emails only when the posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="cae3b-143">Повтор действия для каждого элемента списка с помощью forEach</span><span class="sxs-lookup"><span data-stu-id="cae3b-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="cae3b-144">Цикл forEach определяет массив, для каждого элемента которого должно быть выполнено действие.</span><span class="sxs-lookup"><span data-stu-id="cae3b-144">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="cae3b-145">Если определенный объект не является массивом, цикл завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="cae3b-145">If it is not an array, the flow fails.</span></span> <span data-ttu-id="cae3b-146">Например, если есть действие action1, которое выводит массив сообщений, и нужно отправить каждое сообщение, то можно включить оператор forEach в свойства действия: forEach: `forEach : "@action('action1').outputs.messages"`.</span><span class="sxs-lookup"><span data-stu-id="cae3b-146">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="cae3b-147">Изменение определения кода в приложении логики</span><span class="sxs-lookup"><span data-stu-id="cae3b-147">Edit the code definition for a logic app</span></span>

<span data-ttu-id="cae3b-148">Помимо конструктора приложения логики, вы можете изменять непосредственно код, задающий приложение логики.</span><span class="sxs-lookup"><span data-stu-id="cae3b-148">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="cae3b-149">В панели команд выберите **Представление кода**.</span><span class="sxs-lookup"><span data-stu-id="cae3b-149">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="cae3b-150">Откроется полный редактор, показывающий определение, которое вы только что изменили.</span><span class="sxs-lookup"><span data-stu-id="cae3b-150">A full editor opens and shows the definition you edited.</span></span>

    ![Просмотр кода](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="cae3b-152">С помощью текстового редактора вы можете копировать и вставлять любое количество действий в том же приложении логики или в разных приложениях логики.</span><span class="sxs-lookup"><span data-stu-id="cae3b-152">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="cae3b-153">Вы также можете легко добавлять или удалять целые разделы в определении или совместно использовать определения с другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="cae3b-153">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="cae3b-154">Чтобы сохранить изменения, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cae3b-154">To save your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="cae3b-155">Параметры</span><span class="sxs-lookup"><span data-stu-id="cae3b-155">Parameters</span></span>

<span data-ttu-id="cae3b-156">Некоторые возможности Logic Apps (например, параметры) доступны только в представлении кода.</span><span class="sxs-lookup"><span data-stu-id="cae3b-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="cae3b-157">Параметры облегчают многократное использование значений во всем приложении логики.</span><span class="sxs-lookup"><span data-stu-id="cae3b-157">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="cae3b-158">Например, если вы хотите использовать один адрес электронной почты в нескольких действиях, можно задать его как параметр.</span><span class="sxs-lookup"><span data-stu-id="cae3b-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="cae3b-159">Параметры — это хороший способ извлечения значений, которые вы планируете часто изменять.</span><span class="sxs-lookup"><span data-stu-id="cae3b-159">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="cae3b-160">Их особенно удобно использовать, когда вам нужно переопределять параметры в разных средах.</span><span class="sxs-lookup"><span data-stu-id="cae3b-160">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="cae3b-161">Дополнительные сведения о переопределении параметров в зависимости от среды см. в статье [Создание определений рабочих процессов для приложений логики с помощью JSON](../logic-apps/logic-apps-author-definitions.md) и [документации по REST API](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="cae3b-161">To learn how to override parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="cae3b-162">Далее приводится пример обновления существующего приложения логики, чтобы в нем использовались параметры для условия запроса.</span><span class="sxs-lookup"><span data-stu-id="cae3b-162">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="cae3b-163">В представлении кода найдите объект `parameters : {}` и вставьте в него следующий объект `currentFeedUrl`:</span><span class="sxs-lookup"><span data-stu-id="cae3b-163">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="cae3b-164">Выберите действие `When_a_feed-item_is_published`, найдите раздел `queries` и замените значение запроса значением: `"feedUrl": "#@{parameters('currentFeedUrl')}"`.</span><span class="sxs-lookup"><span data-stu-id="cae3b-164">Go to the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="cae3b-165">Чтобы объединить несколько строк, можно использовать функцию `concat`.</span><span class="sxs-lookup"><span data-stu-id="cae3b-165">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="cae3b-166">Например `"@concat('#',parameters('currentFeedUrl'))"` работает так же, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="cae3b-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the above.</span></span>

3.  <span data-ttu-id="cae3b-167">Когда все будет готово, нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cae3b-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="cae3b-168">Теперь вы можете изменить RSS-канал веб-сайта, передав другой URL-адрес через объект `currentFeedURL`.</span><span class="sxs-lookup"><span data-stu-id="cae3b-168">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<span data-ttu-id="cae3b-169">Дополнительные сведения о создании определений приложений логики см. в [этой статье](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="cae3b-169">Learn more about [how to author logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="cae3b-170">Запуск рабочих процессов приложения логики</span><span class="sxs-lookup"><span data-stu-id="cae3b-170">Start logic app workflows</span></span>

<span data-ttu-id="cae3b-171">Существует несколько различных вариантов запуска рабочего процесса, заданного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="cae3b-171">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="cae3b-172">Рабочий процесс всегда можно запустить по запросу на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="cae3b-172">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="cae3b-173">Триггеры повторения</span><span class="sxs-lookup"><span data-stu-id="cae3b-173">Recurrence triggers</span></span>

<span data-ttu-id="cae3b-174">Триггер повторения запускается с заданным интервалом.</span><span class="sxs-lookup"><span data-stu-id="cae3b-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="cae3b-175">Если в триггере предусмотрена условная логика, он проверяет, нужно ли запустить рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="cae3b-175">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="cae3b-176">Триггер указывает, что рабочий процесс должен быть запущен, возвращая код состояния `200`.</span><span class="sxs-lookup"><span data-stu-id="cae3b-176">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="cae3b-177">Если не требуется запускать рабочий процесс, триггер возвращает код состояния `202`.</span><span class="sxs-lookup"><span data-stu-id="cae3b-177">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="cae3b-178">Обратный вызов с использованием REST API</span><span class="sxs-lookup"><span data-stu-id="cae3b-178">Callback using REST APIs</span></span>

<span data-ttu-id="cae3b-179">Службы могут вызывать конечную точку приложения логики для запуска рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="cae3b-179">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="cae3b-180">Чтобы запустить подобное приложение логики по требованию, нажмите кнопку **Запустить сейчас** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="cae3b-180">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="cae3b-181">Дополнительные сведения см. в статье [Приложения логики как вызываемые конечные точки](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="cae3b-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
<span data-ttu-id="cae3b-182">[портале Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="cae3b-182">[Azure portal]: https://portal.azure.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="cae3b-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cae3b-183">Next steps</span></span>

* [<span data-ttu-id="cae3b-184">Выполнение различных действий в приложениях логики с помощью оператора switch</span><span class="sxs-lookup"><span data-stu-id="cae3b-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="cae3b-185">Циклы, области действия и индивидуальная обработка</span><span class="sxs-lookup"><span data-stu-id="cae3b-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="cae3b-186">Создание определений приложений логики</span><span class="sxs-lookup"><span data-stu-id="cae3b-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)