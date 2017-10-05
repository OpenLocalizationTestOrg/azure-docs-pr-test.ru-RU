---
title: "Пакетная обработка сообщений как группы или коллекции в Azure Logic Apps | Документация Майкрософт"
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
ms.openlocfilehash: 480ffce5dbe7c25181bb0ba5639de884e98ff4e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="ce4d5-104">Отправка, получение и пакетная обработка сообщений в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="ce4d5-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="ce4d5-105">Для обработки сообщений группами можно отправить элементы данных (или сообщения) в *пакет*, а затем обработать эти элементы как пакет.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-105">To process messages together in groups, you can send data items, or messages, to a *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="ce4d5-106">Этот подход полезен, когда необходимо быть уверенным, что элементы данных сгруппированы определенным образом и обрабатываются вместе.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-106">This approach is useful when you want to make sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="ce4d5-107">Можно создать приложения логики, которые получают элементы как пакет, используя триггер **Пакет**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-107">You can create logic apps that receive items as a batch by using the **Batch** trigger.</span></span> <span data-ttu-id="ce4d5-108">Затем можно создать приложения логики, которые отправляют элементы в пакет, используя действие **Пакет**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-108">You can then create logic apps that send items to a batch by using the **Batch** action.</span></span>

<span data-ttu-id="ce4d5-109">В этом разделе показано, как создать решение пакетной обработки, выполнив следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ce4d5-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="ce4d5-110">[Создание приложения логики, которое получает и собирает элементы как пакет](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="ce4d5-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="ce4d5-111">Это приложение логики для "получения пакета" указывает имя пакета и условия отправки пакета, которые должны выполняться, прежде чем получающее приложение отправит и обработает элементы.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-111">This "batch receiver" logic app specifies the batch name and release criteria to meet before the receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="ce4d5-112">[Создание приложения логики, которое отправляет элементы в пакет](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="ce4d5-112">[Create a logic app that sends items to a batch](#batch-sender).</span></span> <span data-ttu-id="ce4d5-113">Это приложение логики для "отправки пакета" указывает, куда отправлять элементы. Точкой назначения должно быть существующее приложение логики для получения пакета.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-113">This "batch sender" logic app specifies where to send items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="ce4d5-114">Вы также можете указать уникальный ключ, например номер клиента, чтобы "секционировать" (разделить) целевой пакет на подмножества на основе этого ключа.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-114">You can also specify a unique key, like a customer number, to "partition", or divide, the target batch into subsets based on that key.</span></span> <span data-ttu-id="ce4d5-115">Таким образом все элементы с этим ключом будут собираться и обрабатываться вместе.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="ce4d5-116">Требования</span><span class="sxs-lookup"><span data-stu-id="ce4d5-116">Requirements</span></span>

<span data-ttu-id="ce4d5-117">Для выполнения этого примера необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="ce4d5-117">To follow this example, you need these items:</span></span>

* <span data-ttu-id="ce4d5-118">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-118">An Azure subscription.</span></span> <span data-ttu-id="ce4d5-119">Если у вас нет подписки, вы можете [создать бесплатную пробную версию учетной записи Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ce4d5-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="ce4d5-120">В противном случае вы можете [зарегистрироваться на получение подписки с оплатой по мере использования](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="ce4d5-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="ce4d5-121">Базовые знания [создания приложений логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ce4d5-121">Basic knowledge about [how to create logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="ce4d5-122">Учетная запись электронной почты любого [поставщика электронной почты, поддерживаемого Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ce4d5-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="ce4d5-123">Создание приложения логики, которое получает сообщения как пакет</span><span class="sxs-lookup"><span data-stu-id="ce4d5-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="ce4d5-124">Прежде чем отправлять сообщения в пакет, необходимо сначала создать приложение логики для "получения пакета" с помощью триггера **Пакет**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-124">Before you can send messages to a batch, you must first create a "batch receiver" logic app with the **Batch** trigger.</span></span> <span data-ttu-id="ce4d5-125">Тогда вы сможете выбрать это получающее приложение логики при создании отправляющего приложения.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-125">That way, you can select this receiver logic app when you create the sender logic app.</span></span> <span data-ttu-id="ce4d5-126">В настройках получения укажите имя пакета, условия его отправки и другие параметры.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-126">For the receiver, you specify the batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="ce4d5-127">Отправляющее приложение логики должно знать, куда отправлять элементы, в то время как получающее приложение логики не нуждается в сведениях об отправителях.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-127">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="ce4d5-128">На [портале Azure](https://portal.azure.com) создайте приложение логики с именем BatchReceiver.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-128">In the [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="ce4d5-129">В конструкторе Logic Apps добавьте триггер **Пакет**, который запускает рабочий процесс приложения логики.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-129">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="ce4d5-130">В поле поиска введите слово "пакет" в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-130">In the search box, enter "batch" as your filter.</span></span> <span data-ttu-id="ce4d5-131">Выберите триггер **Пакет — Пакетные сообщения**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Добавление триггера "Пакет"](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="ce4d5-133">Задайте имя пакета и укажите критерии для его отправки, например:</span><span class="sxs-lookup"><span data-stu-id="ce4d5-133">Provide a name for the batch, and specify criteria for releasing the batch, for example:</span></span>

   * <span data-ttu-id="ce4d5-134">**Имя пакета**: имя, используемое для идентификации пакета. В данном примере — TestBatch.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-134">**Batch Name**: The name used to identify the batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="ce4d5-135">**Число сообщений**: количество сообщений, которое хранится как пакет, а затем отправляется в обработку. В данном примере — 5.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-135">**Message Count**: The number of messages to hold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Ввод сведений для триггера "Пакет"](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="ce4d5-137">Добавьте другое действие, которое отправляет сообщение электронной почты, когда срабатывает триггер "Пакет".</span><span class="sxs-lookup"><span data-stu-id="ce4d5-137">Add another action that sends an email when the batch trigger fires.</span></span> <span data-ttu-id="ce4d5-138">Каждый раз, когда в пакете собирается пять элементов, приложение логики отправляет сообщение.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-138">Each time the batch has five items, the logic app sends an email.</span></span>

   1. <span data-ttu-id="ce4d5-139">Под триггером "Пакет" нажмите кнопку **+ Новый шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-139">Under the batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="ce4d5-140">В поле поиска введите слово "почта" в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-140">In the search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="ce4d5-141">Выберите соединитель электронной почты в зависимости от своего поставщика электронной почты.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="ce4d5-142">Например, если у вас рабочая или учебная учетная запись, то выберите соединитель Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-142">For example, if you have a work or school account, select the Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="ce4d5-143">Если у вас учетная запись Gmail, то выберите соединитель Gmail.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-143">If you have a Gmail account, select the Gmail connector.</span></span>

   3. <span data-ttu-id="ce4d5-144">Выберите это действие для соединителя: **{*поставщик электронной почты*} - Отправить электронное письмо**</span><span class="sxs-lookup"><span data-stu-id="ce4d5-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="ce4d5-145">Например:</span><span class="sxs-lookup"><span data-stu-id="ce4d5-145">For example:</span></span>

      ![Выбор действия "Отправить электронное письмо" для поставщика электронной почты](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="ce4d5-147">Если вы еще не создали подключение для поставщика электронной почты, то укажите учетные данные электронной почты для аутентификации при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="ce4d5-148">Дополнительные сведения об аутентификации учетных данных электронной почты см. в [этой статье](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ce4d5-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="ce4d5-149">Задайте свойства для только что добавленного действия.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-149">Set the properties for the action you just added.</span></span>

   * <span data-ttu-id="ce4d5-150">В поле **Кому** введите адрес электронной почты получателя.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-150">In the **To** box, enter the recipient's email address.</span></span> 
   <span data-ttu-id="ce4d5-151">Для тестировании можете использовать свой собственный адрес.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="ce4d5-152">В поле **Тема**, когда отобразится список **Динамическое содержимое**, выберите **Имя секции**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-152">In the **Subject** box, when the **Dynamic content** list appears, select the **Partition Name** field.</span></span>

     ![Выбор значения "Имя секции" в списке "Динамическое содержимое"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="ce4d5-154">В следующем разделе можно указать уникальный ключ секции, который разделит целевой пакет на логические наборы, в которые затем можно отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-154">In a later section, you can specify a unique partition key that divides the target batch into logical sets to where you can send messages.</span></span> 
     <span data-ttu-id="ce4d5-155">Каждый набор имеет уникальный номер, который создается отправляющим приложением логики.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-155">Each set has a unique number that's generated by the sender logic app.</span></span> 
     <span data-ttu-id="ce4d5-156">Эта функция позволяет использовать один пакет с несколькими подмножествами и определить каждое подмножество с помощью задаваемого имени.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-156">This capability lets you use a single batch with multiple subsets and define each subset with the name that you provide.</span></span>

   * <span data-ttu-id="ce4d5-157">В поле **Текст**, когда отобразится список **Динамическое содержимое**, выберите **Идентификатор сообщения**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-157">In the **Body** box, when the **Dynamic content** list appears, select the **Message Id** field.</span></span>

     ![Выбор значения "Идентификатор сообщения" для поля "Текст"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="ce4d5-159">Так как входные данные для действия **Отправить электронное письмо** являются массивом, конструктор автоматически добавляет для этого действия цикл **For each** (Для каждого).</span><span class="sxs-lookup"><span data-stu-id="ce4d5-159">Because the input for the send email action is an array, the designer automatically adds a **For each** loop around the **Send an email** action.</span></span> 
     <span data-ttu-id="ce4d5-160">Этот цикл выполняет действие в отношении каждого элемента внутри пакета.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-160">This loop performs the inner action on each item in the batch.</span></span> 
     <span data-ttu-id="ce4d5-161">То есть если в триггере "Пакет" задано пять элементов, то вы получите пять сообщений при каждом срабатывании триггера.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-161">So, with the batch trigger set to five items, you get five emails each time the trigger fires.</span></span>

7.  <span data-ttu-id="ce4d5-162">Когда приложение логики для получения пакета создано, сохраните это приложение.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Сохранение приложения логики](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-to-a-batch"></a><span data-ttu-id="ce4d5-164">Создание приложения логики, которое отправляет сообщения в пакет</span><span class="sxs-lookup"><span data-stu-id="ce4d5-164">Create logic apps that send messages to a batch</span></span>

<span data-ttu-id="ce4d5-165">Теперь создайте одно или несколько приложений логики, которые отправляют элементы в пакет, заданный получающим приложением логики.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-165">Now create one or more logic apps that send items to the batch defined by the receiver logic app.</span></span> <span data-ttu-id="ce4d5-166">В настройках отправки укажите получающее приложение логики, имя пакета, содержимое сообщения и другие параметры.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-166">For the sender, you specify the receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="ce4d5-167">При необходимости можно указать уникальный ключ секции, чтобы разделить пакет на подмножества для сбора элементов с помощью этого ключа.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-167">You can optionally provide a unique partition key to divide the batch into subsets to collect items with that key.</span></span>

<span data-ttu-id="ce4d5-168">Отправляющее приложение логики должно знать, куда отправлять элементы, в то время как получающее приложение логики не нуждается в сведениях об отправителях.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-168">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="ce4d5-169">Создайте второе приложение логики с именем BatchSender.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="ce4d5-170">В поле поиска введите слово "повторение" в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-170">In the search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="ce4d5-171">Выберите триггер **Расписание — повторение**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Добавление триггера "Расписание — повторение"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="ce4d5-173">Задайте частоту и интервал, чтобы отправляющее приложение логики запускалось каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-173">Set the frequency and interval to run the sender logic app every minute.</span></span>

      ![Настройка частоты и интервала триггера повторения](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="ce4d5-175">Добавьте новый шаг для отправки сообщений в пакет.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-175">Add a new step for sending messages to a batch.</span></span>

   1. <span data-ttu-id="ce4d5-176">Под триггером "Повторение" нажмите кнопку **+ Новый шаг** > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-176">Under the recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="ce4d5-177">В поле поиска введите слово "пакет" в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-177">In the search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="ce4d5-178">Выберите действие **Отправить сообщения в пакет — Выберите рабочий процесс Logic Apps с триггером пакета**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-178">Select this action: **Send messages to batch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Выбор действия "Отправить сообщения в пакет"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="ce4d5-180">Теперь выберите приложение логики BatchReceiver, которое вы создали ранее и которое теперь доступно как действие.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Выбор приложения логики для "получения пакета"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="ce4d5-182">В этом списке также отображаются все прочие приложения логики, которые содержат триггеры пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-182">The list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="ce4d5-183">Задайте свойства пакета.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-183">Set the batch properties.</span></span>

   * <span data-ttu-id="ce4d5-184">**Имя пакета**: имя пакета, определяемое принимающим приложением логики. В данном примере — TestBatch. Это имя проверяется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-184">**Batch Name**: The batch name defined by the receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="ce4d5-185">Убедитесь, что имя пакета не было изменено. Оно должно совпадать с именем пакета, указанным в принимающем приложении логики.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-185">Make sure that you don't change the batch name, which must match the batch name that's specified by the receiver logic app.</span></span>
     > <span data-ttu-id="ce4d5-186">Изменение имени пакета приводит к сбою в работе отправляющего приложения логики.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-186">Changing the batch name causes the sender logic app to fail.</span></span>

   * <span data-ttu-id="ce4d5-187">**Содержимое сообщения**: текст отправляемого сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-187">**Message Content**: The message content that you want to send.</span></span> 
   <span data-ttu-id="ce4d5-188">В данном примере добавьте следующее выражение, которое вставляет текущую дату и время в содержимое сообщения, отправляемого в пакет:</span><span class="sxs-lookup"><span data-stu-id="ce4d5-188">For this example, add this expression that inserts the current date and time into the message content that you send to the batch:</span></span>

     1. <span data-ttu-id="ce4d5-189">Когда отобразится список **Динамическое содержимое**, выберите **Выражение**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-189">When the **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="ce4d5-190">Введите выражение **utcnow()** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-190">Enter the expression **utcnow()**, and choose **OK**.</span></span> 

        ![В поле "Содержимое сообщения" выберите "Выражение".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="ce4d5-193">Теперь настройте для пакета секцию.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-193">Now set up a partition for the batch.</span></span> <span data-ttu-id="ce4d5-194">В действии BatchReceiver выберите **Показать расширенные параметры**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-194">In the "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="ce4d5-195">**Имя секции**: здесь можно указать необязательный уникальный ключ секции для разделения целевого пакета.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-195">**Partition Name**: An optional unique partition key to use for dividing the target batch.</span></span> <span data-ttu-id="ce4d5-196">Например, добавьте выражение, которое генерирует случайное число от 1 до 5.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="ce4d5-197">Когда отобразится список **Динамическое содержимое**, выберите **Выражение**.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-197">When the **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="ce4d5-198">Введите следующее выражение: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="ce4d5-198">Enter this expression: **rand(1,6)**</span></span>

        ![Настройка секции для целевого пакета](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="ce4d5-200">Эта функция **rand** генерирует число от 1 до 5.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="ce4d5-201">То есть пакет разделяется на пять нумерованных секций, которые динамически задаются этим выражением.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="ce4d5-202">**Идентификатор сообщения**: необязательный идентификатор сообщения. Если это поле оставить пустым, то генерируется идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="ce4d5-203">Для данного примера оставьте это поле пустым.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="ce4d5-204">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-204">Save your logic app.</span></span> <span data-ttu-id="ce4d5-205">Теперь ваше отправляющее приложение логики выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="ce4d5-205">Your sender logic app now looks similar to this example:</span></span>

   ![Сохранение отправляющего приложения логики](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="ce4d5-207">Тестирование приложений логики</span><span class="sxs-lookup"><span data-stu-id="ce4d5-207">Test your logic apps</span></span>

<span data-ttu-id="ce4d5-208">Чтобы проверить решение пакетной обработки, запустите приложения логики и дайте им поработать несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-208">To test your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="ce4d5-209">Скоро вы начнете получать сообщения электронной почты группами по пять сообщений. Все они будут иметь один ключ секции.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-209">Soon, you start getting emails in groups of five, all with the same partition key.</span></span>

<span data-ttu-id="ce4d5-210">Приложение логики BatchSender запускается каждую минуту, генерирует случайное число в диапазоне от 1 до 5 и использует это число в качестве ключа секции для целевого пакета, в который отправляются сообщения.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as the partition key for the target batch where messages are sent.</span></span> <span data-ttu-id="ce4d5-211">Каждый раз пакет содержит пять элементов с одинаковым ключом секции. Приложение логики BatchReceiver срабатывает и отправляет сообщение для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="ce4d5-211">Each time the batch has five items with the same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce4d5-212">После выполнения проверки убедитесь, что приложение логики BatchSender отключено, чтобы оно прекратило отправлять сообщения и не перегружало папку "Входящие".</span><span class="sxs-lookup"><span data-stu-id="ce4d5-212">When you're done testing, make sure that you disable the BatchSender logic app to stop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce4d5-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce4d5-213">Next steps</span></span>

* [<span data-ttu-id="ce4d5-214">Создание определений рабочих процессов для приложений логики с помощью JSON</span><span class="sxs-lookup"><span data-stu-id="ce4d5-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="ce4d5-215">Создание бессерверного приложения в Visual Studio с использованием приложений логики и функций</span><span class="sxs-lookup"><span data-stu-id="ce4d5-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="ce4d5-216">Сценарий обработки исключений и ведения журнала ошибок для приложений логики</span><span class="sxs-lookup"><span data-stu-id="ce4d5-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
