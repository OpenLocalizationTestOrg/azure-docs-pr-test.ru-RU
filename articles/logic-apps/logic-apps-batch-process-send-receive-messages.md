---
title: "Обработка сообщений aaaBatch как группы или коллекции - приложения логики Azure | Документы Microsoft"
description: "Отправка и получение сообщений для пакетной обработки в приложениях логики"
keywords: "пакет, пакетная обработка"
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="2f79d-104">Отправка, получение и пакетная обработка сообщений в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="2f79d-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="2f79d-105">tooprocess сообщений в группах, можно отправить данные tooa элементы или сообщений, *пакета*, а затем пакетной обработки этих элементов.</span><span class="sxs-lookup"><span data-stu-id="2f79d-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="2f79d-106">Этот подход полезен, если нужно убедиться, что элементы данных toomake группируются особым образом и обрабатываются вместе.</span><span class="sxs-lookup"><span data-stu-id="2f79d-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="2f79d-107">Можно создать логику приложения, получающие элементов в виде пакета с помощью hello **пакета** триггера.</span><span class="sxs-lookup"><span data-stu-id="2f79d-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="2f79d-108">Затем можно создать логику приложения, отправить пакет tooa элементов с помощью hello **пакета** действие.</span><span class="sxs-lookup"><span data-stu-id="2f79d-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="2f79d-109">В этом разделе показано, как создать решение пакетной обработки, выполнив следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2f79d-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="2f79d-110">[Создание приложения логики, которое получает и собирает элементы как пакет](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="2f79d-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="2f79d-111">Это приложение логики «пакета получатель» указывает hello пакета имя и выпуск критерии toomeet перед логику приложения hello приемника освобождает и обрабатывает элементы.</span><span class="sxs-lookup"><span data-stu-id="2f79d-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="2f79d-112">[Создание приложения логики, который отправляет пакет tooa элементы](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="2f79d-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="2f79d-113">Это приложение логики «пакета отправителя» указывает, где toosend элементов, которые должны быть существующие приложения логики приемника пакета.</span><span class="sxs-lookup"><span data-stu-id="2f79d-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="2f79d-114">Можно также указать уникальный ключ, например, номер клиента, слишком «секции» или разделить целевом пакете hello в подмножества, на основе такого ключа.</span><span class="sxs-lookup"><span data-stu-id="2f79d-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="2f79d-115">Таким образом все элементы с этим ключом будут собираться и обрабатываться вместе.</span><span class="sxs-lookup"><span data-stu-id="2f79d-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="2f79d-116">Требования</span><span class="sxs-lookup"><span data-stu-id="2f79d-116">Requirements</span></span>

<span data-ttu-id="2f79d-117">toofollow в этом примере потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="2f79d-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="2f79d-118">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="2f79d-118">An Azure subscription.</span></span> <span data-ttu-id="2f79d-119">Если у вас нет подписки, вы можете [создать бесплатную пробную версию учетной записи Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2f79d-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="2f79d-120">В противном случае вы можете [зарегистрироваться на получение подписки с оплатой по мере использования](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="2f79d-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="2f79d-121">Базовые знания о [как toocreate приложения логики](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="2f79d-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="2f79d-122">Учетная запись электронной почты любого [поставщика электронной почты, поддерживаемого Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="2f79d-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="2f79d-123">Создание приложения логики, которое получает сообщения как пакет</span><span class="sxs-lookup"><span data-stu-id="2f79d-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="2f79d-124">Перед тем как отправлять сообщения tooa пакет, сначала необходимо создать приложение логику «получатель пакета» с hello **пакета** триггера.</span><span class="sxs-lookup"><span data-stu-id="2f79d-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="2f79d-125">Таким образом, можно выбрать этот получатель приложения логики, при создании приложения логики hello отправителя.</span><span class="sxs-lookup"><span data-stu-id="2f79d-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="2f79d-126">Для получателя hello укажите имя пакета hello, условия выпуска и другие параметры.</span><span class="sxs-lookup"><span data-stu-id="2f79d-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="2f79d-127">Приложения логики отправителя необходимы сведения, где элементы toosend, пока получатель логику приложения не требуется tooknow что-либо о отправителей hello.</span><span class="sxs-lookup"><span data-stu-id="2f79d-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="2f79d-128">В hello [портал Azure](https://portal.azure.com), создание логики приложения с таким именем: «BatchReceiver»</span><span class="sxs-lookup"><span data-stu-id="2f79d-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="2f79d-129">В конструкторе приложений логики добавьте hello **пакета** срабатывание триггера, который запускает рабочий процесс приложения логики.</span><span class="sxs-lookup"><span data-stu-id="2f79d-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="2f79d-130">В поле поиска hello введите «раздел» фильтра.</span><span class="sxs-lookup"><span data-stu-id="2f79d-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="2f79d-131">Выберите триггер **Пакет — Пакетные сообщения**.</span><span class="sxs-lookup"><span data-stu-id="2f79d-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Добавление триггера "Пакет"](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="2f79d-133">Укажите имя для пакета hello и укажите критерии освобождения hello пакета, например:</span><span class="sxs-lookup"><span data-stu-id="2f79d-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="2f79d-134">**Имя пакета**: hello имя, используемое tooidentify hello пакетах, что в этом примере является «TestBatch».</span><span class="sxs-lookup"><span data-stu-id="2f79d-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="2f79d-135">**Число сообщений**: hello число toohold сообщения в виде пакета, не отпуская для обработки, который является «5» в этом примере.</span><span class="sxs-lookup"><span data-stu-id="2f79d-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Ввод сведений для триггера "Пакет"](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="2f79d-137">Добавьте другое действие, которое отправляет сообщение электронной почты, когда срабатывает триггер hello пакета.</span><span class="sxs-lookup"><span data-stu-id="2f79d-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="2f79d-138">Каждый пакет hello времени имеет пять элементов, приложение hello логику отправляет сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2f79d-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="2f79d-139">В разделе hello пакета триггер, выберите **+ новый шаг** > **добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="2f79d-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="2f79d-140">В поле поиска hello введите «email» фильтра.</span><span class="sxs-lookup"><span data-stu-id="2f79d-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="2f79d-141">Выберите соединитель электронной почты в зависимости от своего поставщика электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2f79d-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="2f79d-142">Например при наличии рабочей или учебной учетной записи выберите соединитель hello Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="2f79d-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="2f79d-143">Если учетную запись Gmail, выберите соединитель Gmail hello.</span><span class="sxs-lookup"><span data-stu-id="2f79d-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="2f79d-144">Выберите это действие для соединителя: **{*поставщик электронной почты*} - Отправить электронное письмо**</span><span class="sxs-lookup"><span data-stu-id="2f79d-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="2f79d-145">Например:</span><span class="sxs-lookup"><span data-stu-id="2f79d-145">For example:</span></span>

      ![Выбор действия "Отправить электронное письмо" для поставщика электронной почты](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="2f79d-147">Если вы еще не создали подключение для поставщика электронной почты, то укажите учетные данные электронной почты для аутентификации при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="2f79d-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="2f79d-148">Дополнительные сведения об аутентификации учетных данных электронной почты см. в [этой статье](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2f79d-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="2f79d-149">Установить свойства hello hello действие, которое вы только что добавили.</span><span class="sxs-lookup"><span data-stu-id="2f79d-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="2f79d-150">В hello **для** введите адрес электронной почты получателя hello.</span><span class="sxs-lookup"><span data-stu-id="2f79d-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="2f79d-151">Для тестировании можете использовать свой собственный адрес.</span><span class="sxs-lookup"><span data-stu-id="2f79d-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="2f79d-152">В hello **субъекта** поле, когда hello **динамическое содержимое** появится список, выберите hello **имя секции** поля.</span><span class="sxs-lookup"><span data-stu-id="2f79d-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     ![Выберите из списка «Динамического содержимого» hello «Раздела»](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="2f79d-154">В следующем разделе можно указать ключ уникальную секцию, разделяет hello целевом пакете в логические наборы toowhere можно отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="2f79d-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="2f79d-155">Каждый набор имеет уникальный номер, создаваемое приложение логики hello отправителя.</span><span class="sxs-lookup"><span data-stu-id="2f79d-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="2f79d-156">Эта возможность позволяет использовать один пакет с несколькими подмножеств и определить каждое подмножество с указываемое имя hello.</span><span class="sxs-lookup"><span data-stu-id="2f79d-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="2f79d-157">В hello **текст** поле, когда hello **динамическое содержимое** появится список, выберите hello **идентификатор сообщения** поля.</span><span class="sxs-lookup"><span data-stu-id="2f79d-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     ![Выбор значения "Идентификатор сообщения" для поля "Текст"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="2f79d-159">Поскольку hello входные данные для действия электронной почты для отправки hello является массивом, hello конструктор автоматически добавляет **для каждого** цикла вокруг hello **отправить сообщение электронной почты** действие.</span><span class="sxs-lookup"><span data-stu-id="2f79d-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="2f79d-160">Этот цикл выполняет внутреннее действие hello для каждого элемента в пакете hello.</span><span class="sxs-lookup"><span data-stu-id="2f79d-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="2f79d-161">Таким образом элементы toofive set триггера пакета hello, вы получаете пять сообщений электронной почты, который срабатывает триггер hello каждый раз.</span><span class="sxs-lookup"><span data-stu-id="2f79d-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="2f79d-162">Когда приложение логики для получения пакета создано, сохраните это приложение.</span><span class="sxs-lookup"><span data-stu-id="2f79d-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Сохранение приложения логики](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="2f79d-164">Создавать логику приложения, отправляющие сообщения tooa пакета</span><span class="sxs-lookup"><span data-stu-id="2f79d-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="2f79d-165">Теперь можно создайте один или несколько логики приложения, отправить пакет toohello элементов определяются hello приемника логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2f79d-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="2f79d-166">Для отправителя hello укажите hello приемника логику приложения и имя пакета, содержимое сообщения и все другие параметры.</span><span class="sxs-lookup"><span data-stu-id="2f79d-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="2f79d-167">Дополнительно можно присвоить hello пакета ключей toodivide уникальную секцию в подмножеств toocollect элементы с этим ключом.</span><span class="sxs-lookup"><span data-stu-id="2f79d-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="2f79d-168">Приложения логики отправителя необходимы сведения, где элементы toosend, пока получатель логику приложения не требуется tooknow что-либо о отправителей hello.</span><span class="sxs-lookup"><span data-stu-id="2f79d-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="2f79d-169">Создайте второе приложение логики с именем BatchSender.</span><span class="sxs-lookup"><span data-stu-id="2f79d-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="2f79d-170">В поле поиска hello введите «повторение» фильтра.</span><span class="sxs-lookup"><span data-stu-id="2f79d-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="2f79d-171">Выберите триггер **Расписание — повторение**.</span><span class="sxs-lookup"><span data-stu-id="2f79d-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Добавить триггер hello «Периодичности расписания»](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="2f79d-173">Задайте частоту hello и интервала toorun hello отправителя логику приложения каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="2f79d-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![Настройка частоты и интервала триггера повторения](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="2f79d-175">Добавьте новое действие для отправки сообщений tooa пакета.</span><span class="sxs-lookup"><span data-stu-id="2f79d-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="2f79d-176">В разделе hello повторения триггера, выберите **+ новый шаг** > **добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="2f79d-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="2f79d-177">В поле поиска hello введите «раздел» фильтра.</span><span class="sxs-lookup"><span data-stu-id="2f79d-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="2f79d-178">Выберите это действие: **отправки сообщений toobatch: выберите рабочий процесс приложения логики с триггером пакета**</span><span class="sxs-lookup"><span data-stu-id="2f79d-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Выберите «Отправить сообщения toobatch»](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="2f79d-180">Теперь выберите приложение логики BatchReceiver, которое вы создали ранее и которое теперь доступно как действие.</span><span class="sxs-lookup"><span data-stu-id="2f79d-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Выбор приложения логики для "получения пакета"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="2f79d-182">Hello также перечислены другие приложения логики которых определены триггеры пакета.</span><span class="sxs-lookup"><span data-stu-id="2f79d-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="2f79d-183">Установить свойства пакета hello.</span><span class="sxs-lookup"><span data-stu-id="2f79d-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="2f79d-184">**Имя пакета**: имя пакета hello, определяемое приложение логики hello получателя, то в этом примере является «TestBatch» и выполняется проверка во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2f79d-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="2f79d-185">Убедитесь, что не изменять имя пакета hello, которое должно совпадать с именем пакета hello, определяемый hello приемника логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2f79d-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="2f79d-186">Изменение имени пакета hello приводит отправителя hello toofail логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2f79d-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="2f79d-187">**Содержимое сообщения**: hello, которые должны toosend содержимое сообщения.</span><span class="sxs-lookup"><span data-stu-id="2f79d-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="2f79d-188">Для этого примера добавьте это выражение вставок hello текущую дату и время в сообщение hello отправки toohello пакета содержимого:</span><span class="sxs-lookup"><span data-stu-id="2f79d-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="2f79d-189">Здравствуйте, когда **динамическое содержимое** появится список, выберите **выражение**.</span><span class="sxs-lookup"><span data-stu-id="2f79d-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="2f79d-190">Введите выражение hello **utcnow()**и выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2f79d-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        ![В поле "Содержимое сообщения" выберите "Выражение".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="2f79d-193">Теперь настройка секции для пакетной hello.</span><span class="sxs-lookup"><span data-stu-id="2f79d-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="2f79d-194">В hello действие «BatchReceiver», выберите **Показывать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="2f79d-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="2f79d-195">**Имя секции**: необязательное секционирование уникальных ключей toouse разделения hello целевого пакета.</span><span class="sxs-lookup"><span data-stu-id="2f79d-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="2f79d-196">Например, добавьте выражение, которое генерирует случайное число от 1 до 5.</span><span class="sxs-lookup"><span data-stu-id="2f79d-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="2f79d-197">Здравствуйте, когда **динамическое содержимое** появится список, выберите **выражение**.</span><span class="sxs-lookup"><span data-stu-id="2f79d-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="2f79d-198">Введите следующее выражение: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="2f79d-198">Enter this expression: **rand(1,6)**</span></span>

        ![Настройка секции для целевого пакета](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="2f79d-200">Эта функция **rand** генерирует число от 1 до 5.</span><span class="sxs-lookup"><span data-stu-id="2f79d-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="2f79d-201">То есть пакет разделяется на пять нумерованных секций, которые динамически задаются этим выражением.</span><span class="sxs-lookup"><span data-stu-id="2f79d-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="2f79d-202">**Идентификатор сообщения**: необязательный идентификатор сообщения. Если это поле оставить пустым, то генерируется идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="2f79d-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="2f79d-203">Для данного примера оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="2f79d-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="2f79d-204">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="2f79d-204">Save your logic app.</span></span> <span data-ttu-id="2f79d-205">Логика приложения отправителя теперь выглядит аналогичный пример toothis:</span><span class="sxs-lookup"><span data-stu-id="2f79d-205">Your sender logic app now looks similar toothis example:</span></span>

   ![Сохранение отправляющего приложения логики](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="2f79d-207">Тестирование приложений логики</span><span class="sxs-lookup"><span data-stu-id="2f79d-207">Test your logic apps</span></span>

<span data-ttu-id="2f79d-208">tootest вашей пакетной обработки решений, оставьте свои приложения логики, выполняться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2f79d-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="2f79d-209">Скоро вы начните получать сообщения электронной почты в пяти группах, с hello же ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="2f79d-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="2f79d-210">BatchSender логику приложения запускается каждую минуту, создает случайное число в диапазоне от одного до пяти и использует этот созданный номер в качестве ключа секции hello для hello целевого пакета, куда должны отправляться сообщения.</span><span class="sxs-lookup"><span data-stu-id="2f79d-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="2f79d-211">Каждый раз hello пакета содержит пять элементов с hello одинаковым ключом секции BatchReceiver логику приложения срабатывает и отправляет сообщения для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="2f79d-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f79d-212">После завершения тестирования, убедитесь, что отключение hello BatchSender логику приложения toostop отправки сообщений и избежать перегрузки папку "Входящие".</span><span class="sxs-lookup"><span data-stu-id="2f79d-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f79d-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f79d-213">Next steps</span></span>

* [<span data-ttu-id="2f79d-214">Создание определений рабочих процессов для приложений логики с помощью JSON</span><span class="sxs-lookup"><span data-stu-id="2f79d-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="2f79d-215">Создание бессерверного приложения в Visual Studio с использованием приложений логики и функций</span><span class="sxs-lookup"><span data-stu-id="2f79d-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="2f79d-216">Сценарий обработки исключений и ведения журнала ошибок для приложений логики</span><span class="sxs-lookup"><span data-stu-id="2f79d-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
