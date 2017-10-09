---
title: "aaaSwitch инструкции для различных действий в приложениях для логики Azure | Документы Microsoft"
description: "Выберите tooperform различные действия на логику приложения, на основе выражения значений с помощью оператора выбора."
services: logic-apps
keywords: "оператор switch"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="fc270-104">Выполнение различных действий в приложениях логики с помощью оператора switch</span><span class="sxs-lookup"><span data-stu-id="fc270-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="fc270-105">При создании рабочего процесса, часто имеют разные действия tootake на основе значения hello объекта или выражение.</span><span class="sxs-lookup"><span data-stu-id="fc270-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="fc270-106">Например может потребоваться вашей toobehave логику приложения, по-разному на основе hello кода состояния HTTP-запроса или параметра, выбранного в сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="fc270-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="fc270-107">Эти сценарии можно использовать tooimplement оператора switch.</span><span class="sxs-lookup"><span data-stu-id="fc270-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="fc270-108">Логика приложения можно оценить маркера или выражение и выберите случай hello с hello же hello tooexecute значение указанного действия.</span><span class="sxs-lookup"><span data-stu-id="fc270-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="fc270-109">Только один вариант должен соответствовать инструкцию switch hello.</span><span class="sxs-lookup"><span data-stu-id="fc270-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="fc270-110">Как и в других языках программирования, операторы switch поддерживают только операторы равенства.</span><span class="sxs-lookup"><span data-stu-id="fc270-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="fc270-111">Если вам нужны другие операторы сравнения (к примеру, оператор greater than), используйте выражение условия.</span><span class="sxs-lookup"><span data-stu-id="fc270-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="fc270-112">поведение детерминированным выполнения tooensure, вариантов должен содержать значение уникальный и статические вместо динамических токены или выражение.</span><span class="sxs-lookup"><span data-stu-id="fc270-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc270-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fc270-113">Prerequisites</span></span>

- <span data-ttu-id="fc270-114">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="fc270-114">An active Azure subscription.</span></span> <span data-ttu-id="fc270-115">Если у вас еще нет активной подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/) или [попробуйте бесплатную версию Logic Apps](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fc270-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="fc270-116">Базовые сведения о приложениях логики</span><span class="sxs-lookup"><span data-stu-id="fc270-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="fc270-117">Добавление рабочего процесса tooyour оператора switch</span><span class="sxs-lookup"><span data-stu-id="fc270-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="fc270-118">как работает оператор switch tooshow, в этом примере создается логики приложения, что мониторы файлы загружены tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="fc270-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="fc270-119">При отправке новых файлов hello приложения hello логики отправляет утверждающего tooan электронной почты, выбирает ли tootransfer tooSharePoint этих файлов.</span><span class="sxs-lookup"><span data-stu-id="fc270-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="fc270-120">приложение Hello использует инструкцию switch, который будет выполнять различные действия на основе значения hello hello выбирает утверждающий.</span><span class="sxs-lookup"><span data-stu-id="fc270-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="fc270-121">Создайте приложение логики и выберите триггер **Dropbox – When a file is created** (Dropbox — при создании файла).</span><span class="sxs-lookup"><span data-stu-id="fc270-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Использование триггера Dropbox — When a file is created (Dropbox — при создании файла)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="fc270-123">Добавьте это действие триггера hello: **Outlook.com - утверждения отправлять по электронной почте**</span><span class="sxs-lookup"><span data-stu-id="fc270-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="fc270-124">Приложения логики поддерживают также утверждение по электронной почте из учетной записи Outlook в Office 365.</span><span class="sxs-lookup"><span data-stu-id="fc270-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="fc270-125">Если у вас нет существующего подключения, вам предложат toocreate один.</span><span class="sxs-lookup"><span data-stu-id="fc270-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="fc270-126">Заполните необходимые hello.</span><span class="sxs-lookup"><span data-stu-id="fc270-126">Fill in hello required fields.</span></span> <span data-ttu-id="fc270-127">Например, в разделе **для**, укажите hello адрес электронной почты для отправки электронной почты утверждающий hello.</span><span class="sxs-lookup"><span data-stu-id="fc270-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="fc270-128">В разделе **User Options** (Параметры пользователя) введите `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="fc270-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Настройка подключения](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="fc270-130">Добавьте оператор switch.</span><span class="sxs-lookup"><span data-stu-id="fc270-130">Add a switch statement.</span></span>

   - <span data-ttu-id="fc270-131">Выберите **+ New step** (+Новый шаг) > **... Дополнительно** > **Add a switch case** (Добавить вариант для оператора switch).</span><span class="sxs-lookup"><span data-stu-id="fc270-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="fc270-132">Теперь мы хотим tooselect hello действие tooperform основании hello `SelectedOptions` выходные данные hello *письмо утверждения* действие.</span><span class="sxs-lookup"><span data-stu-id="fc270-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="fc270-133">Это поле можно найти в hello **добавить динамическое содержимое** селектора.</span><span class="sxs-lookup"><span data-stu-id="fc270-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="fc270-134">Используйте *случая 1* toohandle при выборе утверждающий hello `Approve`.</span><span class="sxs-lookup"><span data-stu-id="fc270-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="fc270-135">Утвержденный, скопируйте hello исходный файл tooSharePoint через Интернет с hello [ **SharePoint Online — создать файл** действия](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="fc270-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="fc270-136">Добавьте еще одно действие hello пользователи toonotify вариантов, что файл доступен на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fc270-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="fc270-137">Добавление другого варианта toohandle при выборе пользователем `Reject`.</span><span class="sxs-lookup"><span data-stu-id="fc270-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="fc270-138">В случае отклонения отправляете уведомления по электронной почте о том других утверждающих, что файл hello отклоняется и никаких дальнейших действий не требуется.</span><span class="sxs-lookup"><span data-stu-id="fc270-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="fc270-139">`SelectedOptions`предоставляет только два варианта, поэтому можно оставить hello **по умолчанию** варианта пустая.</span><span class="sxs-lookup"><span data-stu-id="fc270-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Оператор switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="fc270-141">Оператор switch требуется по крайней мере один вариант в случае по умолчанию toohello сложения.</span><span class="sxs-lookup"><span data-stu-id="fc270-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="fc270-142">После инструкции switch hello, удалить исходный файл, отправленный tooDropbox hello путем добавления этого действия: **общего банка данных - удалить файл**</span><span class="sxs-lookup"><span data-stu-id="fc270-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="fc270-143">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="fc270-143">Save your logic app.</span></span> <span data-ttu-id="fc270-144">Протестируйте приложение, передав tooDropbox файла.</span><span class="sxs-lookup"><span data-stu-id="fc270-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="fc270-145">Вскоре должно прийти сообщение электронной почты утверждения.</span><span class="sxs-lookup"><span data-stu-id="fc270-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="fc270-146">Выберите параметр и наблюдать за поведением hello.</span><span class="sxs-lookup"><span data-stu-id="fc270-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="fc270-147">Узнать о возможностях слишком[Отслеживайте свои приложения логики](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="fc270-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="fc270-148">Понимание кода hello за операторами switch</span><span class="sxs-lookup"><span data-stu-id="fc270-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="fc270-149">Теперь, когда создан логику приложения, используя инструкцию switch, давайте взглянем на определение кода hello за инструкцию switch hello.</span><span class="sxs-lookup"><span data-stu-id="fc270-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="fc270-150">`"Switch"`— Имя hello инструкцию switch hello, его можно переименовать для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="fc270-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="fc270-151">`"type": "Switch"`Указывает действие hello в операторе switch.</span><span class="sxs-lookup"><span data-stu-id="fc270-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="fc270-152">`"expression"`hello утверждающий выбранный параметр в этом примере и вычисляется для каждого варианта case, объявленном позже в определении hello.</span><span class="sxs-lookup"><span data-stu-id="fc270-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="fc270-153">`"cases"` может содержать любое число вариантов.</span><span class="sxs-lookup"><span data-stu-id="fc270-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="fc270-154">Для каждого варианта `"Case *"` является именем по умолчанию hello hello случай, который можно переименовать для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="fc270-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="fc270-155">`"case"`Указывает метку case hello, hello коммутатора использует выражение для сравнения, которое должно быть константой и уникальные значения.</span><span class="sxs-lookup"><span data-stu-id="fc270-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="fc270-156">Если ни один из вариантов hello соответствует hello switch-выражения, в рамках `"default"` выполняются.</span><span class="sxs-lookup"><span data-stu-id="fc270-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="fc270-157">Получение справки</span><span class="sxs-lookup"><span data-stu-id="fc270-157">Get help</span></span>

<span data-ttu-id="fc270-158">tooask вопросы, ответы на вопросы и см. какие другие пользователи приложения логики Azure делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="fc270-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="fc270-159">toohelp улучшить логику приложения Azure и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="fc270-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc270-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc270-160">Next steps</span></span>

- <span data-ttu-id="fc270-161">Узнайте, каким образом слишком[Добавление условий](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="fc270-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="fc270-162">Узнайте, как [обрабатываются ошибки и исключения в Logic Apps](logic-apps-exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="fc270-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="fc270-163">Ознакомьтесь с [возможностями языка для описания рабочих процессов](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="fc270-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>