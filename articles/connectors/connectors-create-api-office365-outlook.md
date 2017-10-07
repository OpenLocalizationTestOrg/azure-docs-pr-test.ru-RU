---
title: "Соединитель Office 365 Outlook aaaAdd hello в приложениях для логики | Документы Microsoft"
description: "Для создания логики приложений Office 365 соединитель tooenable взаимодействие с Office 365. Например, он позволяет создавать, редактировать и обновлять контакты и элементы календаря."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="02b19-104">Приступая к работе с Office 365 Outlook соединителя hello</span><span class="sxs-lookup"><span data-stu-id="02b19-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="02b19-105">Соединитель Office 365 Outlook Hello разрешает взаимодействие с Outlook в Office 365.</span><span class="sxs-lookup"><span data-stu-id="02b19-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="02b19-106">Используйте этот соединитель toocreate, изменения и обновления контактов и элементы календаря, также получить, отправки и ответ tooemail.</span><span class="sxs-lookup"><span data-stu-id="02b19-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="02b19-107">Office 365 Outlook позволяет следующее:</span><span class="sxs-lookup"><span data-stu-id="02b19-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="02b19-108">Сборки рабочего процесса с помощью функций электронной почты и календаря hello в Office 365.</span><span class="sxs-lookup"><span data-stu-id="02b19-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="02b19-109">Использование триггеров toostart рабочего процесса при наличии новых сообщений электронной почты, при обновлении элемента календаря и многое другое.</span><span class="sxs-lookup"><span data-stu-id="02b19-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="02b19-110">Использовать действия toosend сообщение электронной почты, создайте нового события календаря и многое другое.</span><span class="sxs-lookup"><span data-stu-id="02b19-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="02b19-111">Например, при наличии нового объекта в Salesforce (триггер), отправить сообщение электронной почты tooyour Outlook Office 365 (действие).</span><span class="sxs-lookup"><span data-stu-id="02b19-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="02b19-112">В этом разделе показано, как toouse hello соединителя Office 365 Outlook в приложение логики, а также списки hello триггеров и действий.</span><span class="sxs-lookup"><span data-stu-id="02b19-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="02b19-113">Эта версия статьи hello применяется tooLogic приложений общедоступной (версии GA).</span><span class="sxs-lookup"><span data-stu-id="02b19-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="02b19-114">toolearn Дополнительные сведения о приложении логики в разделе [Каковы приложения логики](../logic-apps/logic-apps-what-are-logic-apps.md) и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="02b19-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="02b19-115">Подключение tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="02b19-115">Connect tooOffice 365</span></span>
<span data-ttu-id="02b19-116">Логика приложения можно получить доступ к любой службы, сначала создайте *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="02b19-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="02b19-117">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="02b19-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="02b19-118">Например, tooconnect tooOffice 365 Outlook, необходимо сначала Office 365 *соединения*.</span><span class="sxs-lookup"><span data-stu-id="02b19-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="02b19-119">toocreate соединения, введите учетные данные hello, обычно используется служба hello tooaccess которых надо tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="02b19-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="02b19-120">Поэтому с Office 365 Outlook, введите tooyour hello учетные данные подключения к hello toocreate учетной записи Office 365.</span><span class="sxs-lookup"><span data-stu-id="02b19-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="02b19-121">Создайте соединение hello</span><span class="sxs-lookup"><span data-stu-id="02b19-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="02b19-122">Использование триггера</span><span class="sxs-lookup"><span data-stu-id="02b19-122">Use a trigger</span></span>
<span data-ttu-id="02b19-123">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="02b19-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="02b19-124">Триггеры «опрос» hello службы в частоту и интервал.</span><span class="sxs-lookup"><span data-stu-id="02b19-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="02b19-125">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="02b19-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="02b19-126">В приложение логику hello введите «office 365» tooget список триггеров hello:</span><span class="sxs-lookup"><span data-stu-id="02b19-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="02b19-127">Выберите триггер Office 365 Outlook **When an upcoming event is starting soon** (Если приближается время начала предстоящего события).</span><span class="sxs-lookup"><span data-stu-id="02b19-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="02b19-128">Если подключение уже существует, затем выберите календарь из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="02b19-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="02b19-129">Если, запрашиваемые toosign в, а затем введите знак hello в соединении hello toocreate сведения.</span><span class="sxs-lookup"><span data-stu-id="02b19-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="02b19-130">[Создайте соединение hello](connectors-create-api-office365-outlook.md#create-the-connection) в этом разделе перечислены шаги hello.</span><span class="sxs-lookup"><span data-stu-id="02b19-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="02b19-131">В этом примере логика приложения hello выполняются обновления события календаря.</span><span class="sxs-lookup"><span data-stu-id="02b19-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="02b19-132">результаты hello toosee триггера, добавьте другое действие, которое отправляет вам текстовое сообщение.</span><span class="sxs-lookup"><span data-stu-id="02b19-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="02b19-133">Например, добавить hello Twilio *отправляемого сообщения* действие, которое запускает текстов, когда hello календарь событий в течение 15 минут.</span><span class="sxs-lookup"><span data-stu-id="02b19-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="02b19-134">Выберите hello **изменить** кнопку и задайте hello **частоты** и **интервал** значения.</span><span class="sxs-lookup"><span data-stu-id="02b19-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="02b19-135">Например, если требуется toopoll триггер hello каждые 15 минут, задайте hello **частоты** слишком**минуту**и набор hello **интервал** слишком**15**.</span><span class="sxs-lookup"><span data-stu-id="02b19-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="02b19-136">**Сохранить** изменения (левом верхнем углу панели инструментов hello).</span><span class="sxs-lookup"><span data-stu-id="02b19-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="02b19-137">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="02b19-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="02b19-138">Использование действий</span><span class="sxs-lookup"><span data-stu-id="02b19-138">Use an action</span></span>
<span data-ttu-id="02b19-139">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="02b19-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="02b19-140">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="02b19-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="02b19-141">Выберите hello "плюс".</span><span class="sxs-lookup"><span data-stu-id="02b19-141">Select hello plus sign.</span></span> <span data-ttu-id="02b19-142">Вы видите несколько вариантов: **добавить действие**, **добавить условие**, или один из hello **дополнительные** параметры.</span><span class="sxs-lookup"><span data-stu-id="02b19-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="02b19-143">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="02b19-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="02b19-144">В текстовом поле hello введите «office 365» tooget список всех доступных действий hello.</span><span class="sxs-lookup"><span data-stu-id="02b19-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="02b19-145">В этом примере мы выберем действие Office 365 Outlook **Создание контакта**.</span><span class="sxs-lookup"><span data-stu-id="02b19-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="02b19-146">Если подключение уже существует, а затем выберите hello **идентификатор папки**, **заданное имя**и другие свойства:</span><span class="sxs-lookup"><span data-stu-id="02b19-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="02b19-147">При появлении соответствующего запроса сведений о соединении hello введите toocreate hello hello сведения соединения.</span><span class="sxs-lookup"><span data-stu-id="02b19-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="02b19-148">[Создайте соединение hello](connectors-create-api-office365-outlook.md#create-the-connection) в этом разделе описываются эти свойства.</span><span class="sxs-lookup"><span data-stu-id="02b19-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="02b19-149">В этом примере мы создадим контакт в Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="02b19-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="02b19-150">Можно использовать результаты из другого триггера toocreate hello контакта.</span><span class="sxs-lookup"><span data-stu-id="02b19-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="02b19-151">Например, добавить hello SalesForce *при создании объекта* триггера.</span><span class="sxs-lookup"><span data-stu-id="02b19-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="02b19-152">Затем добавьте hello Office 365 Outlook *создать контакт* действие, которое использует hello SalesForce полей toocreate hello новый новый контакт в Office 365.</span><span class="sxs-lookup"><span data-stu-id="02b19-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="02b19-153">**Сохранить** изменения (левом верхнем углу панели инструментов hello).</span><span class="sxs-lookup"><span data-stu-id="02b19-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="02b19-154">Приложение логики сохранено и теперь может быть включено автоматически.</span><span class="sxs-lookup"><span data-stu-id="02b19-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="02b19-155">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="02b19-155">Connector-specific details</span></span>

<span data-ttu-id="02b19-156">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="02b19-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="02b19-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02b19-157">Next Steps</span></span>
<span data-ttu-id="02b19-158">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="02b19-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="02b19-159">Просмотр hello другие доступные соединители в приложениях для логики в наших [список API-интерфейсы](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="02b19-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

