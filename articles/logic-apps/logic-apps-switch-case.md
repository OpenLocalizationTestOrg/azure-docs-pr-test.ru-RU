---
title: "Оператор switch для разных действий в Azure Logic Apps | Документация Майкрософт"
description: "Выбор различных действий, выполняемых в приложениях логики с помощью оператора switch на основе значений выражений"
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
ms.openlocfilehash: 338b6a5b549d7bf81186550295608438ac4aee32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="16893-104">Выполнение различных действий в приложениях логики с помощью оператора switch</span><span class="sxs-lookup"><span data-stu-id="16893-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="16893-105">При создании рабочего процесса часто требуется выполнять разные действия в зависимости от значения объекта или выражения.</span><span class="sxs-lookup"><span data-stu-id="16893-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span></span> <span data-ttu-id="16893-106">Например, поведение приложения логики может быть разным при разных кодах состояния HTTP-запроса или выборе разных параметров в сообщении электронной почты.</span><span class="sxs-lookup"><span data-stu-id="16893-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="16893-107">Для реализации этих сценариев можно использовать оператор switch.</span><span class="sxs-lookup"><span data-stu-id="16893-107">You can use a switch statement to implement these scenarios.</span></span> <span data-ttu-id="16893-108">Приложение логики может оценить маркер или выражение и выбрать вариант с тем же значением для выполнения указанного действия.</span><span class="sxs-lookup"><span data-stu-id="16893-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span></span> <span data-ttu-id="16893-109">Проверяемое выражение должно совпадать только с одним вариантом.</span><span class="sxs-lookup"><span data-stu-id="16893-109">Only one case should match the switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="16893-110">Как и в других языках программирования, операторы switch поддерживают только операторы равенства.</span><span class="sxs-lookup"><span data-stu-id="16893-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="16893-111">Если вам нужны другие операторы сравнения (к примеру, оператор greater than), используйте выражение условия.</span><span class="sxs-lookup"><span data-stu-id="16893-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="16893-112">Чтобы выполнение было детерминированным, варианты должны содержать уникальные статические значения, а не динамические маркеры или выражения.</span><span class="sxs-lookup"><span data-stu-id="16893-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16893-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="16893-113">Prerequisites</span></span>

- <span data-ttu-id="16893-114">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="16893-114">An active Azure subscription.</span></span> <span data-ttu-id="16893-115">Если у вас еще нет активной подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/) или [попробуйте бесплатную версию Logic Apps](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="16893-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="16893-116">Базовые сведения о приложениях логики</span><span class="sxs-lookup"><span data-stu-id="16893-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-to-your-workflow"></a><span data-ttu-id="16893-117">Добавление оператора switch для рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="16893-117">Add a switch statement to your workflow</span></span>

<span data-ttu-id="16893-118">Чтобы показать, как работает оператор switch, в этом примере создается приложение логики, которое отслеживает файлы, переданные в Dropbox.</span><span class="sxs-lookup"><span data-stu-id="16893-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span></span> <span data-ttu-id="16893-119">При передаче новых файлов приложение логики отправляет сообщение электронной почты подтверждающему лицу, которое выбирает, нужно ли переносить эти файлы в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="16893-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span></span> <span data-ttu-id="16893-120">Приложение использует оператор switch, который выполняет различные действия на основе значения, выбранного подтверждающим лицом.</span><span class="sxs-lookup"><span data-stu-id="16893-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span></span>

1. <span data-ttu-id="16893-121">Создайте приложение логики и выберите триггер **Dropbox – When a file is created** (Dropbox — при создании файла).</span><span class="sxs-lookup"><span data-stu-id="16893-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Использование триггера Dropbox — When a file is created (Dropbox — при создании файла)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="16893-123">Для этого триггера создайте действие **Outlook.com – Send approval email** (Outlook — отправка сообщения электронной почты для утверждения).</span><span class="sxs-lookup"><span data-stu-id="16893-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="16893-124">Приложения логики поддерживают также утверждение по электронной почте из учетной записи Outlook в Office 365.</span><span class="sxs-lookup"><span data-stu-id="16893-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="16893-125">Если вы не установили подключение, вам будет предложено создать его.</span><span class="sxs-lookup"><span data-stu-id="16893-125">If you don't have an existing connection, you're prompted to create one.</span></span>
   - <span data-ttu-id="16893-126">Заполните обязательные поля.</span><span class="sxs-lookup"><span data-stu-id="16893-126">Fill in the required fields.</span></span> <span data-ttu-id="16893-127">Например, в поле **Кому** укажите адрес электронной почты для отправки сообщения электронной почты подтверждающему лицу.</span><span class="sxs-lookup"><span data-stu-id="16893-127">For example, under **To**, specify the email address for sending the approver email.</span></span>
   - <span data-ttu-id="16893-128">В разделе **User Options** (Параметры пользователя) введите `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="16893-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Настройка подключения](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="16893-130">Добавьте оператор switch.</span><span class="sxs-lookup"><span data-stu-id="16893-130">Add a switch statement.</span></span>

   - <span data-ttu-id="16893-131">Выберите **+ New step** (+Новый шаг) > **... Дополнительно** > **Add a switch case** (Добавить вариант для оператора switch).</span><span class="sxs-lookup"><span data-stu-id="16893-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="16893-132">Теперь нужно выбрать действие, выполняемое на основе выходных данных `SelectedOptions` из действия *Send approval email* (Отправка сообщения электронной почты для утверждения).</span><span class="sxs-lookup"><span data-stu-id="16893-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span></span> 
   <span data-ttu-id="16893-133">Это поле можно найти в селекторе **Добавить динамическое содержимое**.</span><span class="sxs-lookup"><span data-stu-id="16893-133">You can find this field in the **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="16893-134">Используйте *Вариант 1* для обработки, когда подтверждающее лицо выбирает `Approve`.</span><span class="sxs-lookup"><span data-stu-id="16893-134">Use *Case 1* to handle when the approver selects `Approve`.</span></span>
     - <span data-ttu-id="16893-135">Если поступит утверждение, исходный файл копируется в SharePoint Online с помощью действия [**SharePoint Online – Create file**](../connectors/connectors-create-api-sharepointonline.md) (SharePoint Online — создать файл).</span><span class="sxs-lookup"><span data-stu-id="16893-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="16893-136">Добавьте в этот вариант еще одно действие, которое уведомит пользователей о наличии нового файла на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="16893-136">Add another action within the case to notify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="16893-137">Добавьте другой вариант на случай, если пользователь выберет `Reject`.</span><span class="sxs-lookup"><span data-stu-id="16893-137">Add another case to handle when user selects `Reject`.</span></span>
     - <span data-ttu-id="16893-138">Если поступит отклонение, другим утверждающим отправляется уведомление по электронной почте о том, что файл отклоняется и никаких дальнейших действий не требуется.</span><span class="sxs-lookup"><span data-stu-id="16893-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="16893-139">`SelectedOptions` предоставляет только два варианта, поэтому вариант **По умолчанию** можно оставить пустым.</span><span class="sxs-lookup"><span data-stu-id="16893-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span></span>

   ![Оператор switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="16893-141">В операторе switch должен быть создан по меньшей мере один вариант (Case), помимо варианта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="16893-141">A switch statement needs at least one case in addition to the default case.</span></span>

4. <span data-ttu-id="16893-142">После выполнения оператора switch следует удалить исходный файл, загруженный в Dropbox, с помощью действия **Dropbox – Delete file** (Dropbox — удалить файл).</span><span class="sxs-lookup"><span data-stu-id="16893-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="16893-143">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="16893-143">Save your logic app.</span></span> <span data-ttu-id="16893-144">Тестирование приложения путем загрузки файла в Dropbox.</span><span class="sxs-lookup"><span data-stu-id="16893-144">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="16893-145">Вскоре должно прийти сообщение электронной почты утверждения.</span><span class="sxs-lookup"><span data-stu-id="16893-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="16893-146">Выберите параметр и понаблюдайте за поведением.</span><span class="sxs-lookup"><span data-stu-id="16893-146">Select an option, and observe the behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="16893-147">Узнайте о возможностях [мониторинга приложений логики](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="16893-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-the-code-behind-switch-statements"></a><span data-ttu-id="16893-148">Смысл программного кода оператора switch</span><span class="sxs-lookup"><span data-stu-id="16893-148">Understand the code behind switch statements</span></span>

<span data-ttu-id="16893-149">Теперь, когда приложение логики создано с помощью оператора switch, можно рассмотреть определение программного кода оператора switch.</span><span class="sxs-lookup"><span data-stu-id="16893-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span></span>

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

* <span data-ttu-id="16893-150">`"Switch"` — это имя оператора switch, которое можно изменить для большей удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="16893-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="16893-151">`"type": "Switch"` обозначает, что конструкция является оператором switch.</span><span class="sxs-lookup"><span data-stu-id="16893-151">`"type": "Switch"` indicates that the action is a switch statement.</span></span> 
* <span data-ttu-id="16893-152">`"expression"` указывает на вариант, выбранный подтверждающим лицом, который здесь сравнивается с указанными далее в определении вариантами значений.</span><span class="sxs-lookup"><span data-stu-id="16893-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span></span> 
* <span data-ttu-id="16893-153">`"cases"` может содержать любое число вариантов.</span><span class="sxs-lookup"><span data-stu-id="16893-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="16893-154">Для каждого варианта `"Case *"` является именем по умолчанию, которое можно изменить для большей удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="16893-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span></span> 
<span data-ttu-id="16893-155">`"case"` является меткой значения case, которое выражение switch использует для сравнения. Это значение должно быть постоянным и уникальным.</span><span class="sxs-lookup"><span data-stu-id="16893-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="16893-156">Если ни один из вариантов не соответствует оператору switch, действия в `"default"` выполняются.</span><span class="sxs-lookup"><span data-stu-id="16893-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="16893-157">Получение справки</span><span class="sxs-lookup"><span data-stu-id="16893-157">Get help</span></span>

<span data-ttu-id="16893-158">Чтобы задать вопросы, помочь другим пользователям и узнать, что делают другие пользователи, посетите [форум по Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="16893-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="16893-159">Чтобы улучшить Azure Logic Apps и соединители, голосуйте за идеи или предлагайте собственные на [сайте обратной связи Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="16893-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16893-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16893-160">Next steps</span></span>

- <span data-ttu-id="16893-161">Инструкции по [добавлению условий](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="16893-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="16893-162">Узнайте, как [обрабатываются ошибки и исключения в Logic Apps](logic-apps-exception-handling.md).</span><span class="sxs-lookup"><span data-stu-id="16893-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="16893-163">Ознакомьтесь с [возможностями языка для описания рабочих процессов](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="16893-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>