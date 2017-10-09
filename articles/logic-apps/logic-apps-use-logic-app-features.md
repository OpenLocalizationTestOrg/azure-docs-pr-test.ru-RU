---
title: "aaaAdd условия и запустить рабочие процессы — приложения логики Azure | Документы Microsoft"
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
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="2a061-103">Использование функций приложений логики</span><span class="sxs-lookup"><span data-stu-id="2a061-103">Use Logic Apps features</span></span>

<span data-ttu-id="2a061-104">В [предыдущем разделе](../logic-apps/logic-apps-create-a-logic-app.md) вы создали свое первое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="2a061-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="2a061-105">toocontrol приложения логики рабочего процесса, можно указать разные пути для вашего toorun логику приложения и слишком способ обработки данных в массивы, коллекции и пакетах.</span><span class="sxs-lookup"><span data-stu-id="2a061-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="2a061-106">Эти элементы можно включить в рабочий процесс приложения логики:</span><span class="sxs-lookup"><span data-stu-id="2a061-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="2a061-107">Условия и [операторы switch](../logic-apps/logic-apps-switch-case.md) позволяют вашему приложению логики выполнять различные действия в зависимости от того, выполняются ли определенные условия.</span><span class="sxs-lookup"><span data-stu-id="2a061-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="2a061-108">[Циклы](../logic-apps/logic-apps-loops-and-scopes.md) позволяют приложению логики выполнять шаги неоднократно.</span><span class="sxs-lookup"><span data-stu-id="2a061-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="2a061-109">Например, можно повторить действия по всему массиву, используя цикл **For_each**,</span><span class="sxs-lookup"><span data-stu-id="2a061-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="2a061-110">или повторять действия, пока не выполнится условие, используя цикл **Until**.</span><span class="sxs-lookup"><span data-stu-id="2a061-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="2a061-111">[Области](../logic-apps/logic-apps-loops-and-scopes.md) let можно сгруппировать последовательность действий, например, tooimplement обработку исключений.</span><span class="sxs-lookup"><span data-stu-id="2a061-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="2a061-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) позволяет запустить отдельные рабочие процессы для элементов в массиве, при использовании hello логику приложения **SplitOn** команды.</span><span class="sxs-lookup"><span data-stu-id="2a061-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="2a061-113">Здесь описываются другие понятия для создания приложения логики:</span><span class="sxs-lookup"><span data-stu-id="2a061-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="2a061-114">Код представления tooedit существующего приложения логики</span><span class="sxs-lookup"><span data-stu-id="2a061-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="2a061-115">Варианты запуска рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="2a061-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="2a061-116">Условия: выполнение шагов только после выполнения условия</span><span class="sxs-lookup"><span data-stu-id="2a061-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="2a061-117">toohave приложения логику выполнения действия только в том случае, если данные удовлетворяют указанным критериям, можно добавить условие, которое сравнивает данные в рабочие hello для конкретных полей или значений.</span><span class="sxs-lookup"><span data-stu-id="2a061-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="2a061-118">Например, предположим, что у вас есть приложение логики, которое отправляет слишком много электронных писем для записей в RSS-канале веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="2a061-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="2a061-119">Можно добавить условия, чтобы логика приложения отправляет по электронной почте только в том случае, когда новый hello учет принадлежит tooa определенной категории.</span><span class="sxs-lookup"><span data-stu-id="2a061-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="2a061-120">В hello [портал Azure](https://portal.azure.com), найдите и откройте приложение логики в конструктор логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2a061-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="2a061-121">Добавьте условие местоположение рабочего процесса toohello нужного.</span><span class="sxs-lookup"><span data-stu-id="2a061-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="2a061-122">условие hello tooadd между существующего действия в рабочем процессе hello логики приложения, наведите указатель на hello стрелка hello место tooadd hello условие.</span><span class="sxs-lookup"><span data-stu-id="2a061-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="2a061-123">Выберите hello **плюс** (**+**), затем выберите **добавить условие**.</span><span class="sxs-lookup"><span data-stu-id="2a061-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="2a061-124">Например:</span><span class="sxs-lookup"><span data-stu-id="2a061-124">For example:</span></span>

   ![Добавить условие toologic приложение](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="2a061-126">Если вы хотите tooadd условие в конце hello текущего рабочего процесса, перейдите toohello нижней части логики приложения и выберите **+ новый шаг**.</span><span class="sxs-lookup"><span data-stu-id="2a061-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="2a061-127">Определите условие hello.</span><span class="sxs-lookup"><span data-stu-id="2a061-127">Now define hello condition.</span></span> <span data-ttu-id="2a061-128">Задания поля источника hello требуется tooevaluate, tooperform операции hello и hello целевое значение или поле.</span><span class="sxs-lookup"><span data-stu-id="2a061-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="2a061-129">tooadd существующие поля условие tooyour выбрать hello **добавить динамического содержимого списка**.</span><span class="sxs-lookup"><span data-stu-id="2a061-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="2a061-130">Например:</span><span class="sxs-lookup"><span data-stu-id="2a061-130">For example:</span></span>

   ![Изменение условий в базовом режиме](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="2a061-132">Ниже приведен полный условие hello.</span><span class="sxs-lookup"><span data-stu-id="2a061-132">Here's hello complete condition:</span></span>

   ![Полное условие](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="2a061-134">Выберите условия hello toodefine в коде, **изменение в расширенном режиме**.</span><span class="sxs-lookup"><span data-stu-id="2a061-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="2a061-135">Например:</span><span class="sxs-lookup"><span data-stu-id="2a061-135">For example:</span></span>
   > 
   > ![Изменение условия в коде](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="2a061-137">В разделе **Да, если** и **Если нет**, добавьте hello действия tooperform зависимости от того, является ли hello условия.</span><span class="sxs-lookup"><span data-stu-id="2a061-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="2a061-138">Например:</span><span class="sxs-lookup"><span data-stu-id="2a061-138">For example:</span></span>

   ![Условия с путями "Да" и "Нет"](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="2a061-140">Существующих действий можно перетаскивать в hello **Да, если** и **Если нет** пути.</span><span class="sxs-lookup"><span data-stu-id="2a061-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="2a061-141">Сохраните приложение логики, когда закончите.</span><span class="sxs-lookup"><span data-stu-id="2a061-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="2a061-142">Теперь при получении сообщения электронной почты только в том случае, когда сообщения hello соответствует условия.</span><span class="sxs-lookup"><span data-stu-id="2a061-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="2a061-143">Повтор действия для каждого элемента списка с помощью forEach</span><span class="sxs-lookup"><span data-stu-id="2a061-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="2a061-144">цикл Hello указывает массив toorepeat действие.</span><span class="sxs-lookup"><span data-stu-id="2a061-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="2a061-145">Если он не является массивом, потоком hello завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="2a061-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="2a061-146">Например если у вас есть action1, который выводит массив сообщений, и требуется toosend каждое сообщение, можно включить этот оператор forEach в hello свойства действия:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="2a061-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="2a061-147">Измените определение кода hello для приложения логики</span><span class="sxs-lookup"><span data-stu-id="2a061-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="2a061-148">Несмотря на то, что у вас есть hello конструктор логики приложения, можно непосредственно редактировать код hello, определяющий приложения логики.</span><span class="sxs-lookup"><span data-stu-id="2a061-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="2a061-149">На панели команд hello, выберите **кода представление**.</span><span class="sxs-lookup"><span data-stu-id="2a061-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="2a061-150">Полный редактор открывается и отображается определение hello измененные.</span><span class="sxs-lookup"><span data-stu-id="2a061-150">A full editor opens and shows hello definition you edited.</span></span>

    ![Просмотр кода](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="2a061-152">В текстовом редакторе hello, можно скопировать и вставить любое количество действий в рамках hello же логику приложения или между логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2a061-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="2a061-153">Можно легко добавить или удалить все разделы из определения hello и определения могут также совместно с другими разделами.</span><span class="sxs-lookup"><span data-stu-id="2a061-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="2a061-154">Выберите изменения, toosave **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2a061-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="2a061-155">Параметры</span><span class="sxs-lookup"><span data-stu-id="2a061-155">Parameters</span></span>

<span data-ttu-id="2a061-156">Некоторые возможности Logic Apps (например, параметры) доступны только в представлении кода.</span><span class="sxs-lookup"><span data-stu-id="2a061-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="2a061-157">Параметры позволяют легко tooreuse значения во всей логики приложения.</span><span class="sxs-lookup"><span data-stu-id="2a061-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="2a061-158">Например, если вы хотите использовать один адрес электронной почты в нескольких действиях, можно задать его как параметр.</span><span class="sxs-lookup"><span data-stu-id="2a061-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="2a061-159">Параметры подходят по запросу, скорее всего, toochange много значений.</span><span class="sxs-lookup"><span data-stu-id="2a061-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="2a061-160">Они особенно полезны при необходимости toooverride параметры в разных средах.</span><span class="sxs-lookup"><span data-stu-id="2a061-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="2a061-161">toooverride параметры в зависимости от среды, в статье toolearn [создавать логику приложения определения](../logic-apps/logic-apps-author-definitions.md) и [документация по REST API](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="2a061-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="2a061-162">В этом примере показано, как tooupdate существующего логики приложения, которые можно использовать параметры по поисковому запросу hello.</span><span class="sxs-lookup"><span data-stu-id="2a061-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="2a061-163">В окне просмотра кода найти hello `parameters : {}` и добавьте `currentFeedUrl` объекта:</span><span class="sxs-lookup"><span data-stu-id="2a061-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="2a061-164">Go toohello `When_a_feed-item_is_published` действия, найти hello `queries` раздела и заменить значение hello запроса:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="2a061-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="2a061-165">toojoin двух или более строк можно также использовать hello `concat` функции.</span><span class="sxs-lookup"><span data-stu-id="2a061-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="2a061-166">Например `"@concat('#',parameters('currentFeedUrl'))"` works Здравствуйте таким же, как hello выше.</span><span class="sxs-lookup"><span data-stu-id="2a061-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="2a061-167">Когда все будет готово, нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2a061-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="2a061-168">Теперь вы можете изменить hello веб-сайта канал RSS, передавая различные URL-адреса через hello `currentFeedURL` объекта.</span><span class="sxs-lookup"><span data-stu-id="2a061-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="2a061-169">Дополнительные сведения о [как tooauthor логику приложения определения](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="2a061-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="2a061-170">Запуск рабочих процессов приложения логики</span><span class="sxs-lookup"><span data-stu-id="2a061-170">Start logic app workflows</span></span>

<span data-ttu-id="2a061-171">У вас есть различные параметры для запуска процесса hello, определенных в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="2a061-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="2a061-172">Всегда можно запустить рабочий процесс по запросу в hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="2a061-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="2a061-173">Триггеры повторения</span><span class="sxs-lookup"><span data-stu-id="2a061-173">Recurrence triggers</span></span>

<span data-ttu-id="2a061-174">Триггер повторения запускается с заданным интервалом.</span><span class="sxs-lookup"><span data-stu-id="2a061-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="2a061-175">Если триггер hello условную логику, триггер hello определяет, должен ли hello рабочего процесса toorun.</span><span class="sxs-lookup"><span data-stu-id="2a061-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="2a061-176">Указывает триггер должен выполняться рабочий процесс hello, возвращая `200` код состояния.</span><span class="sxs-lookup"><span data-stu-id="2a061-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="2a061-177">При рабочего процесса hello не должно toorun, hello триггера возвращает `202` код состояния.</span><span class="sxs-lookup"><span data-stu-id="2a061-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="2a061-178">Обратный вызов с использованием REST API</span><span class="sxs-lookup"><span data-stu-id="2a061-178">Callback using REST APIs</span></span>

<span data-ttu-id="2a061-179">toostart рабочий процесс службы можно вызывать конечную точку приложения логики.</span><span class="sxs-lookup"><span data-stu-id="2a061-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="2a061-180">Выберите этот тип логики приложения по требованию, toostart **запустить сейчас** на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="2a061-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="2a061-181">Дополнительные сведения см. в статье [Приложения логики как вызываемые конечные точки](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="2a061-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[портал Azure]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="2a061-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2a061-183">Next steps</span></span>

* [<span data-ttu-id="2a061-184">Выполнение различных действий в приложениях логики с помощью оператора switch</span><span class="sxs-lookup"><span data-stu-id="2a061-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="2a061-185">Циклы, области действия и индивидуальная обработка</span><span class="sxs-lookup"><span data-stu-id="2a061-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="2a061-186">Создание определений приложений логики</span><span class="sxs-lookup"><span data-stu-id="2a061-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)